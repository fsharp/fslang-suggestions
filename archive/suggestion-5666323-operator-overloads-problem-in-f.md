# Operator Overloads Problem in F# [5666323] #

**Submitted by Iris Sakura on 3/22/2014 12:00:00 AM**  
**5 votes on UserVoice prior to migration**  

When redefine an operator function, the opeartor cannot be used for other purpose.
Example:
type Point = { X : float; Y : float; }
let (-) p1 p2 = { X = p1.X - p2.X; Y = p1.Y - p2.Y; }
then the following code raises a compilation error:
let a = 2 - 1 // Error: excepting type "Point"
Overloading in F# is limited, it may because of the type infering and usually it's not a problem because we may use a different function name. But operator's name cannot be changed due to the semantic reason.
We can overload opeators for a class, but how about a record or a tuple? Since F# allows opeator overloads for class already, so it's should not be too difficult to just extend it to all types.



## Response ##
** by fslang-admin on 3/27/2014 12:00:00 AM **

This is answered by the comments and is not a concrete proposal.


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5666323)**


## Comments ##


#### Comment by Jack Pappas on 3/22/2014 9:43:00 AM ####
You can already overload operators for records:
type Point = {
X : float;
Y : float;
} with
static member (-) (a : Point, b : Point) =
{ X = a.X - b.X; Y = a.Y - b.Y; }
[<EntryPoint>]
let main argv =
let z = 2 - 1
let a = { X = 1.0; Y = 2.0 }
let b = { X = 3.0; Y = 0.0 }
let c = a - b
printfn "Hello world!"
0 // Exit code
You can't (and shouldn't) overload operators for tuples, because they're implemented via the System.Tuple types which are treated just like any other type which is external to your code.


#### Comment by Gustavo Guerra on 3/22/2014 1:31:00 PM ####
If you could define operators in type extensions, it would solve lots of problems. The use case is: there's a .NET maths library that you want to use but is not F# friendly, and you want to define pointwise operators like (.*), (.+), etc... Because the type is defined in another assembly, F# doesn't allow you do define those operators as static members


#### Comment by Mauricio Scheffer on 3/24/2014 10:17:00 PM ####
There are many threads in Stackoverflow that show how to do this:
http://stackoverflow.com/questions/2812084/overload-operator-in-f
http://stackoverflow.com/questions/19682432/global-operator-overloading-in-f
http://stackoverflow.com/questions/22401010/f-operator-overloading-riddle-2
http://stackoverflow.com/questions/7695393/overloading-operator-in-f
http://stackoverflow.com/questions/12971965/overloaded-inline-operators-in-f

