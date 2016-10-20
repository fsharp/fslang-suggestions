# Implement OCaml's new match/exception syntax [6536829] #

**Submitted by Eirik George Tsarpalis on 10/8/2014 12:00:00 AM**  
**42 votes on UserVoice prior to migration**  

Implement the feature that is nicely described in the following post:
https://blogs.janestreet.com/pattern-matching-and-exception-handling-unite/



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6536829)**


## Comments ##


#### Comment by Eirik George Tsarpalis on 10/14/2014 6:18:00 AM ####
Consider the following hypothetical example:
let readLines (reader : unit -> string) : string list =
let rec loop acc =
try
let l = reader ()
loop (l :: acc)
with e ->
List.rev acc
loop []
This will make successive calls on a reader function until an exception is raised (e.g. IOException), after which the accumulated lines will be returned. The trouble with this example is that it is not tail-recursive, since the recursive call lies inside a try block. Typically, one would have to rewrite the above example like so:
let readLines (reader : unit -> string) =
let rec loop acc =
let result = try reader () |> Choice1Of2 with e -> Choice2Of2 e
match result with
| Choice1Of2 l -> loop (l :: acc)
| Choice2Of2 e -> List.rev acc
loop []
This is an extremely clumsy piece of code which also results in additional allocations. OCaml solves this problem by offering a unifying exception handling with pattern matching:
let readLines (reader : unit -> string) =
let rec loop acc =
match reader () with
| l -> loop (l :: acc)
| exception e -> List.rev acc
loop []
The above ensures that the recursive call is tail recursive, eliminates unnecessary allocations and is easy to read.


#### Comment by Joerg Beekmann on 10/14/2014 6:30:00 AM ####
This is a very nice solution; means production code can look just as nice as sample code!


#### Comment by Vasily Kirichenko on 10/14/2014 6:47:00 AM ####
Looks very nice.


#### Comment by Richard Minerich on 10/14/2014 1:41:00 PM ####
Just be careful, they use exceptions for flow control in OCaml because they're cheap on that runtime. On .NET exceptions are very expensive and should not be used for standard control flow. I would consider that IOException sample to be very bad form on .NET.


#### Comment by Eirik George Tsarpalis on 10/14/2014 2:42:00 PM ####
(Also continuing from https://twitter.com/eiriktsarpalis/status/521968130097049601)
Perhaps the example I gave was a bit unfortunate (I basically just converted it from Yaron's blog post) but the annoyance still exists in F#. Even if exceptions are not intended for control flow, you still have very realistic use cases in which functions are passed lambdas with no particular guarantees on exception safety. In order for your code to be tail recursive, you have to give your code the Choice<_,_> treatment which I agree is more ugly than it is inefficient. A nice example is when implementing the continuation monad with exceptions, e.g.
type Cont<'T> = ('T -> unit) -> (exn -> unit) -> unit
The correct monadic bind will have to be implemented like this:
let bind (f : Cont<'T>) (g : 'T -> Cont<'S>) : Cont<'S> =
fun sc ec -> f (fun t -> let r = try g t |> Choice1Of2 with e -> Choice2Of2 e in match r with Choice1Of2 s -> s sc ec | Choice2Of2 e -> ec e) ec
Whereas with the match/exception syntax it would be like this:
let bind (f : Cont<'T>) (g : 'T -> Cont<'S>) : Cont<'S> =
fun sc ec -> f (fun t -> let r = match g t with s -> s sc ec | exception e -> ec e) ec
To give you a bigger perspective, here is a somewhat complete continuation/exception monad implementation:
https://github.com/nessos/MBrace.Cloud/blob/master/MBrace.Cloud/CloudBuilder.fs
Perhaps one criticism to this feature would be that it might somehow encourage people to use exceptions as control flow? I don't quite see this, most people out there realise that .NET exceptions are expensive. Other than that, it might not be as common a pattern in F#, but I do come across it quite frequently myself.


#### Comment by Greg Chapman on 12/3/2014 2:08:00 PM ####
If we had something like Scala's Try, we could do the readLines example today.
type Either<'a,'b> = Left of 'a | Right of 'b
let Try f = try Right (f()) with e -> Left e
{...}
match Try reader with
| Right l -> loop (l::acc)
| Left e -> List.rev acc
I wish F# had either Scala's notion of call-by-name, or (my preference) a nicer syntax for delayed expressions. For some reason, something like:
{| expr |}
reads nicer than:
(fun()-> expr)
even if they compile to exactly the same thing.
If {| expr |} was a syntax for a delayed expression, you could implement the bind example using:
match Try {| g t |} with Right s -> s sc ec | Left e -> ec e) ec


#### Comment by Don Syme on 2/4/2016 12:55:00 PM ####
Eirik, what would be the desugaring in quotations and computation expressions?
thanks
don


#### Comment by Eirik George Tsarpalis on 6/28/2016 9:01:00 AM ####
Hi Don,
I would imagine that desugaring (both in comp exprs and quotations) could take the following form. The code
async {
match expr with
| Pat1 -> cexpr1
| Pat2 -> cexpr2
| exception Pat3 -> cexpr3
| exception Pat4 -> cexpr4
}
would transform to
async.Delay(fun () ->
match (try Choice1Of2 expr with e -> Choice2Of2 e) with
| Choice1Of2 Pat1 -> cexpr1
| Choice2Of2 Pat2 -> cexpr2
| Choice2Of2 Pat3 -> cexpr3
| Choice3Of3 Pat4 -> cexpr4)
This should work fine, assuming no match! feature is added to computation expressions in the future. In such a case, a match! implementation would have to manage the exception handling logic explicitly.


#### Comment by Eirik George Tsarpalis on 6/28/2016 9:10:00 AM ####
Similarly, the non-monadic expression
match expr with
| Pat1 -> expr1
| Pat2 -> expr2
| exception Pat3 -> expr3
| exception Pat4 -> expr4
would desugar to
let mutable exn = Unchecked.defaultof<Exception>
let mutable result = Unchecked.defaultof<'T>
try result <- expr with e -> exn <- e
match exn with
| null ->
match result with
| Pat1 -> expr1
| Pat2 -> expr2
| Pat3 -> expr3
| Pat4 -> expr4

