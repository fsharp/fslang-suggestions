# Introduce the ?. operator into F# [10837866] #

**Submitted by John Azariah on 11/23/2015 12:00:00 AM**  
**16 votes on UserVoice prior to migration**  

Since we allow the . operator to reference fields and properties of objects in F#, we're faced with the same problem of null checking that plagued C# until C# 5.
The C# 6 'elvis' operator propagates nulls in a succinct way, and I think that working with objects in F# will be similarly simplified if we introduce it here as well!



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/10837866)**


## Comments ##


#### Comment by Radek Micek on 11/28/2015 6:18:00 AM ####
I prefer using None instead of null in F#.


#### Comment by Fraser Waters on 12/1/2015 6:54:00 AM ####
@radek, maybe semantics like
a.?b
===
if a = null then None else Some (a.b)
And chained together so
a.?b.?c
===
if a = null then None else (if b = null then None else Some (a.b.c))
Would allow easy matching as well:
match a.?b with
| Some b -> printf "a.b is %A" b
| None -> printf "a is null"


#### Comment by Colin Bull on 12/1/2015 7:46:00 AM ####
There is already an Option.ofObj(F# 4) that can help here
You can do something like,
let a = new System.IO.FileInfo("Foo")
let (<*>) a f = a |> Option.map f
let ($) a f = (Option.ofObj a) <*> f
let x =
a$(fun x -> x.CreationTime) <*> (fun x -> x.ToShortDateString())
Not quiet as succinct but you can always lift those accessors to functions to make things tidier.
In general though I'm opposed to using this type of symbolics as it hides meaning, however well documented it is from (C# etc...). I'd prefer to define these locally like this and just use the functions from F# core.


#### Comment by Bartosz Sypytkowski on 12/4/2015 3:12:00 AM ####
"maybe{}" is a basic lesson about computation expressions and it already solves problems, that "elvis operator" is trying to solve. F# doesn't need to solve monad problems using syntax sugar like C# does. We can use existing tools instead.


#### Comment by Ryan Riley on 1/15/2016 1:07:00 PM ####
I agree with Bartosz. Even though ?. would be more succinct, I would prefer the built-in language symbols remain as few in number as possible.


#### Comment by Harald Steinlechner on 1/18/2016 12:29:00 PM ####
this snippet is a superstrong argument against such a feature ;)
http://pastebin.com/Z6kbuTEE
(be proud if you can compute all types of the variables as well as the return value)

