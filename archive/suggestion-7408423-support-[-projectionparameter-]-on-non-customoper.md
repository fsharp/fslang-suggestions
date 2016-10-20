# Support [<ProjectionParameter>] on non-CustomOperations, eg. for in () do [7408423] #

**Submitted by Jason K on 4/1/2015 12:00:00 AM**  
**3 votes on UserVoice prior to migration**  

The following CE builder intends to accept a Domain which has enumerable-like members and, for this situation, return a bool. But the member of the domain being checked varies. I try to parameterize the selection of the member, rather than just expecting the member directly (which changes the type).
This code type-checks as is, but it requires the full lambda as the `over` parameter to For.
type Domain = interface end
type Projection<'R> =
abstract member source : Table<'R>
and Table<'R> = inherit Projection<'R>
and Table<'R, 'K> =
inherit Table<('R * 'K)>
abstract member row : 'R
abstract member key : 'K
type proj<'R> = Projection<'R>
type table<'R> = Table<'R>
type Engine<'D> when 'D :> Domain =
abstract member from: 'R table * ('R proj -> 'U) -> 'U
abstract member where: ('R -> bool) * 'R proj -> 'R proj
abstract member any: ('R -> bool) * 'R proj -> bool
abstract member select: ('R -> 'S) * 'R proj -> 'S proj
type A = { ID : int; Name : string }
type B = { ID2 : int; Name2 : string }
type MyDomain =
inherit Domain
abstract member As : A table
abstract member Bs : B table
type CommandBuilder<'D> when 'D :> Domain () =
// [<CustomOperation("for")>] **no effect (?)**
member __.For ([<ProjectionParameter>] over : ('D -> 'R table), expr : ('R proj -> _)) = // [<ProjectionParameter>] is ignored
(fun (engine : Engine<'D>, domain : 'D) -> engine.from(over(domain), expr))
member __.Yield x = x
[<CustomOperation("select")>]
member __.Select (over : (Engine<'D> * 'D -> 'R proj), [<ProjectionParameter>] mapping : ('R -> _)) =
(fun (engine : Engine<'D>, domain : 'D) -> engine.select(mapping, over(engine, domain)))
[<CustomOperation("where", MaintainsVariableSpace = true)>]
member __.Where (over : (Engine<'D> * 'D -> 'R proj), [<ProjectionParameter>] byPredicate : ('R -> bool)) =
(fun (engine : Engine<'D>, domain : 'D) -> engine.where(byPredicate, over(engine, domain)))
[<CustomOperation("any", MaintainsVariableSpace = true)>]
member __.Any (over : (Engine<'D> * 'D -> 'R proj), [<ProjectionParameter>] byPredicate : ('R -> bool)) =
(fun (engine : Engine<'D>, domain : 'D) -> engine.any(byPredicate, over(engine, domain)))
member __.Quote() = ()
member __.Run(q) = q
let command = new CommandBuilder<MyDomain>()
let invariant1 =
command {
for a in (fun _d -> _d.As) do // should be `for a in d.As do`
any (a.Name = "disallowed value")
}
let invariant2 =
command {
for b in (fun _d -> _d.Bs) do // should be `for a in d.Bs do`
any (b.Name2 = "disallowed value")
}
let domainInvariants = [ invariant1; invariant2 ]



## Response ##
** by fslang-admin on 2/4/2016 12:00:00 AM **

Declined per my comment below. Please contact me if you have more informaiton on this – I’m not opposed to the suggestion I just need to understand exactly what’s involved
Don Syme, F# Language Evolution @dsyme


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/7408423)**


## Comments ##


#### Comment by Don Syme on 6/9/2015 1:51:00 PM ####
Hi Jason, could you provide a link to a gist with this code? thanks
Don Syme


#### Comment by Don Syme on 7/17/2015 7:18:00 AM ####
Here's the gist: https://gist.github.com/dsyme/6623d02d1a6065a7f9e0


#### Comment by Don Syme on 7/17/2015 7:19:00 AM ####
When you say "should be `for a in d.Bs do`" - where would "d" be bound?


#### Comment by Don Syme on 2/3/2016 2:58:00 PM ####
This hasn't been updated in a while and there are pending questions below. I propose to decline this.

