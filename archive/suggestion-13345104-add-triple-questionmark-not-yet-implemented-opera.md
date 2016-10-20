# Add triple-questionmark not yet implemented operator (???) from Scala [13345104] #

**Submitted by Anonymous on 4/7/2016 12:00:00 AM**  
**11 votes on UserVoice prior to migration**  

In Scala, there is an operator `???`, which is used as a "Convenient as a placeholder for a missing right-hand-side of a method."
This is defined as follows:
def ??? : Nothing = throw new NotImplementedError
In F# I would imagine that we'd define it something like:
[<GeneralizableValue>]
let ???<'a> = raise (NotImplementedException())
Unfortunately, ??? is not a valid name, which is why a library solution won't solve this problem.
The major merit of including this in F#, is that it provides a standardized way to declare incomplete parts of the code, allowing users and tooling to detect this.
You can read the original reasoning by Martin Odersky here at http://www.scala-lang.org/old/node/11113.html
Finally, an article offering more explanation as to it's value and usage can be found here:
http://alvinalexander.com/scala/what-does-three-question-marks-in-scala-mean



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/13345104)**


## Comments ##


#### Comment by Alexei Odeychuk on 4/8/2016 8:52:00 AM ####
Varon, did you consider any other options, for example:
1) Simple comment: // ??? to be done
You can find an uncompleted code fragment in your source code file using Ctrl+F in the Visual Studio and writing: “??? to be done”.
2) Toggle a breakpoint in the Visual Studio when necessary to mark an uncompleted fragment of your code. So, you can run and test your code before a breakpoint.
3) let valueToBeDeveloped<'a>(param1, param2) = Unchecked.defaultof<'a>
// if your function has to return a value of unit type
or: let valueToBeDeveloped<'a>(param1, param2) = ()
instead of: let valueToBeDeveloped<'a>(param1, param2) = ???
The already-existing in F# function Unchecked.defaultof<'a> returns the default value of any type and has a much more readable English name than "???". Paired with a comment describing your intent "to write the body of expression here", such a fragment of your code would be easy-to-understand.
As to maintenance of code containing "???". Code maintenance takes 50% (pro-level mid-size apps) to 90% (large, long-lived apps containing several million lines of code intended to be in use for 5 to 20 years) of time professional programmers spent on software projects. So, how much would "???" say about intents of authors of code to a programmer newly assigned to maintain such a project?
Of course, most of the programming languages borrow new language features from others in order to survive and boost their competitive strengths. But from code readability and maintenance perspective, I see no competitive advantages for F# to borrow this syntax from Scala. I think F# has a better syntax (mentioned in point 3) in this respect as of today.


#### Comment by Gauthier Segay on 4/10/2016 7:51:00 PM ####
I believe a library solution is good enough:
let undefined () = raise (System.NotImplementedException())


#### Comment by Dzmitry Lahoda on 4/12/2016 6:50:00 AM ####
Would be good if F# to support
```
let undefined () = raise NotImplemented
```
I.e. omit `Exception` after raise like with `Attribute`s and new without `()`

