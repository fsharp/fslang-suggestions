# Add string interpolation to println syntax (from Swift) [6002107] #

**Submitted by Robert Jeppesen on 6/2/2014 12:00:00 AM**  
**179 votes on UserVoice prior to migration**  

The new language from Apple, Swift has a really nice syntax for println:
http://en.wikipedia.org/wiki/Swift_(programming_language)
let people = ["Anna": 67, "Beto": 8, "Jack": 33, "Sam": 25]
for (name, age) in people {
println("\(name) is \(age) years old.")
}
We could steal the idea but use % instead of \ for a better fit. It would also be compatible, and combinable (is that a word?) with existing printfn syntax:
let name = "Robert"
printfn "Hi %(name), your age is %d"
printfn : int -> string
Naturally there would be compiler errors if name does not exist.



## Response ##
** by fslang-admin on 2/4/2016 12:00:00 AM **

Approved in principle (and has been for a while), please see RFC FS-1001 https://github.com/fsharp/FSharpLangDesign/blob/master/RFCs/FS-1001-StringInterpolation.md
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6002107)**


## Comments ##


#### Comment by Jarle Stabell on 6/2/2014 5:50:00 PM ####
I've "always" wanted something like this in F#. It feels very old-fashioned having to manually specify the "types" in printf in a language with type inference. Also, it's a totally separate, although simple, "type language".
(Scala has a much more generic mechanism, perhaps overkill though).


#### Comment by Mauricio Scheffer on 6/2/2014 6:19:00 PM ####
Related: /archive/suggestion-5678806-string-interpolation


#### Comment by Marcin Juraszek on 6/2/2014 7:21:00 PM ####
There is similar idea for C#: http://roslyn.codeplex.com/discussions/540869


#### Comment by Mauricio Scheffer on 6/2/2014 9:45:00 PM ####
@Marcin: not really. The Roslyn thread is about general string interpolation. This one is a limited application for printf. See my link above for the F# discussion about general string interpolation.


#### Comment by Heather Cynede on 6/3/2014 1:55:00 AM ####
from Nemerle?
http://en.wikipedia.org/wiki/Nemerle#String_formatting


#### Comment by Loic Denuziere on 6/3/2014 4:43:00 AM ####
General string interpolation exists in many languages, including Nemerle as you noted Heather. A big inconvenient is that it would require yet another string delimiter (we have 3 already...). This is about having it as an extra *printf format character, which is probably a smaller can of worms to open.


#### Comment by Robert Jeppesen on 6/3/2014 5:57:00 PM ####
It's worth noting that in Swift (and Nemerle), these interpolations are expressions, so you can do
printfn "The sum is %(a + b)"
This would be nice here, but if that raises the amount of work to prohibiting levels, I think it can be skipped.


#### Comment by Don Syme on 6/20/2014 9:57:00 AM ####
I am very positively predisposed to this feature - at least where only a variable name can be interpolated.
Questions
- Could you use a long identifer %(name1.name2)? I presume not, but it may be a relatively simple extension to allow this.
- What formatting would be used, e.g. for floating point values. Is it %A? Can you modify formatting specifiers?
- Could you use a mix of %d and %(name) specifiers in a single printf format string? My intuition is to allow this, but if the implementation becomes too complex then to disallow it.
Do other people have detailed questions about the specification and scope of this feature?
Note that I have begun labelling some features as "approved" (actually the label is currently called "planned", though I think of it as "approved"), see https://fslang.uservoice.com/forums/245727-f-language/status/1225914.
Labelling something as "approved" is not committing to "doing" the feature, but it does mean we would in theory accept implementations (with corresponding testing) of these features into the "fsharp4" branch at https://visualfsharp.codeplex.com/.
So we would ask you to consider implementing this feature and submitting it. The implementation would then flow throughout all delivery vehicles for F#. We would provide lots of assistance to those seeking to implement the feature.
I already labelled a couple of printf suggestions as "approved".
If you disagree with labelling a feature as "approved", please argue your case through the User Voice comments, at least initially :)
Thanks
Don Syme


#### Comment by bleis-tift on 6/20/2014 8:00:00 PM ####
FYI, scala has similar feature.
http://docs.scala-lang.org/overviews/core/string-interpolation.html


#### Comment by Vladimir Matveev on 7/1/2014 5:51:00 PM ####
ok, I took a stab on this feature and have a working prototype (https://visualfsharp.codeplex.com/SourceControl/network/forks/vladima/primary?branch=fsharp4)
briefly: when analyzing format string compiler splits it into chunks: textblocks and embedded expressions (that are denoted by wrapping them in %()).Then final string that will be passed as a parameter to the constructor of PrintFormat is evaluated as ' string.Concat([| textblock1; expr1; textblock2; expr2... |]) '. All logic that manufactures phantom types remains intact. To evaluate expressions typechecker tries to parse it using provided access point to parser and typecheck it.
Pros: implementation is relatively simple, supports both %(expr) and %(d) specifiers, embedded expressions are regular F# expressions so long names or operators inside are not problem.
Cons: the entire feature is implemented on the semantic level so purely syntax based goodies will require extra effort to work with it, As an example if syntax highlighting is implemented only based on syntactic information then embedded expressions will be highlighted as a string.


#### Comment by Nikita Nemkin on 6/2/2015 10:09:00 AM ####
Rascal (metaprogramming language) has an amazing string interpolation facility: http://tutor.rascal-mpl.org/Rascal/Expressions/Values/String/String.html
It works for all strings (not only println argument) and interpolates arbitrary expressions and even basic control structures.


#### Comment by exercitus vir on 6/19/2015 6:05:00 PM ####
This is awesome.


#### Comment by Don Syme on 9/5/2015 6:02:00 AM ####
This feature didn't make it for F# 4.0 due to some lingering concerns about the design. The prototype for this feature can be found here: https://visualfsharp.codeplex.com/SourceControl/network/forks/vladima/primary/contribution/7063. If you would like to pick up the prototype and take it further please rebase it as a fork of "master" of http://github.com/Microsoft/visualfsharp


#### Comment by Steffen Forkmann on 2/1/2016 8:39:00 AM ####
Rebased version can be found at https://github.com/Microsoft/visualfsharp/pull/921


#### Comment by Jon Nyman on 2/18/2016 10:42:00 AM ####
type Person = {name: string; age: int}
let person = {name = "Robert"; age=5}
printfn "Hi %(person, A), your age is %(person.age, 5i) with space or age %(person.age) without."
printfn : int -> unit


#### Comment by Jon Nyman on 2/18/2016 10:43:00 AM ####
or rather
printfn : unit -> string


#### Comment by Robert Jeppesen on 2/19/2016 5:47:00 AM ####
I'd prefer it if this feature isn't limited to printf functions, but applied generally to all string literals, like literals in C# with '$' prefix.

