# allow defining function with generic type parameter within another function [12940554] #

**Submitted by Gauthier Segay on 3/15/2016 12:00:00 AM**  
**1 votes on UserVoice prior to migration**  

I encounter cases where I'd like to define a function taking a generic type parameter within another functions.
type Foo = {Bar: int option; Baz: string option}
let doSomething () =
(**)let writer = Console.Out
(**)let writeOption o =
(* *)match o with
(* *)| Some v -> writer.Write(string v)
(* *)| None -> writer.Write("")
(**)writeOption foo.Bar
(**)writeOption foo.Baz
It's not possible to do that right now and even if I define the function outside at module level (with extra writer parameter), I can't curry it to avoid passing the context (writer) parameter I'm trying to elide to keep my code concise.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/12940554)**


## Comments ##


#### Comment by Paul Westcott on 3/21/2016 3:28:00 PM ####
If you make writeOption inline then this is currently valid synatx...

