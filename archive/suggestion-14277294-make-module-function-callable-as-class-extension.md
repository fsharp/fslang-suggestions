# Make module function callable as class extension method [14277294] #

**Submitted by trek42 on 5/27/2016 12:00:00 AM**  
**10 votes on UserVoice prior to migration**  

Sometimes it's more convenient and succint to call a function using dot-notation (i.e., class method) than calling module functions with pipeline, yet module function is easier to be composed. I propose the compiler automatically generate class extension methods from module functions, based on a new attribute "CallByInstance" Example:
namespace Namespace
// .fsi
module List =
val map: ('T -> 'U) -> [<CallByInstance>] list<'T> -> list<'U>
Compiler will automatically generate an extension method of list<'U>, in the *containing* namespace, i.e.,
namespace Namespace
module List = ...
// Automatically generated:
[<AutoOpen>]
module ListExtension_map =
type List<'U> with
member this.map f list = List.map f list this
This allows the following syntax:
[1;2;3] |> List.map ((+) 1) // as usual
[1;2;3].map ((+) 1) // call the extension method with dot-notation.
Notes:
1. The extension method is a curried member function. (We don't change the curried parameters to tuple).
2. Similarly we don't change the function name (e.g., no "map" => "Map" thing).
3. We don't need to open module "List" for the extension method. Anywhere "List.map" is accessible, "[1;2;3].map" is also accessible.
4. You can label multiple parameters of a function as [<CallByInstance>], as long as their types are different.
5. Since we require explicitly marking the allowed parameters, there is no compatibility issue. Users can choose to use this feature judiciously.
Finally, this is related to /archive/suggestion-5663326-syntax-for-turning-properties-into-functions, but in a reverse way (i.e., turn a module function to a method). My personal view is we need both.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/14277294)**


## Comments ##


#### Comment by trek42 on 5/27/2016 1:31:00 PM ####
fix an error: the generated extension method is:
type List<'U> with
....member this.map f = List.map f this


#### Comment by Don Syme on 6/13/2016 5:58:00 AM ####
The CallByInstance attribute proposal is very interesting. I've not seen that suggested before. It would, I think, be fairly simple to implement, with many similarities to the existing extension member implementation.


#### Comment by Don Syme on 6/13/2016 5:59:00 AM ####
My intuition would be to make this an F#-specific feature, where the F# compiler inserts the appropriate code at the callsite, and doesn't generate an actual new member in the .NET IL.
That is, instead of auto-generating the actual extension member.


#### Comment by trek42 on 6/18/2016 10:19:00 PM ####
Not knowing much about the F# compiler for judging the way how this would be implemented, but agreed that making this F#-specific feature seems like a good idea. As the feature is proposed, the call-site (call-by-instance) code would still be curried functions, so C# probably won't benefit from it as much as F# code does. A purely F# compiler magic at callsites would definitely work, and probably is more desirable if this simplifies the code and/or reduces the generated assembly.


#### Comment by tranquillity on 9/17/2016 9:20:00 PM ####
This syntax is how Kotlin handles collection functions
val numbers = listOf(1, -1, 2)
numbers.filter { it > 0 } //== listOf(1, 2)
numbers.map { it * it } //== listOf(1, 1, 4)
You can also chain the dot notation together:
numbers.filter { it > 0 }.map { it * it } //== listOf(1, 4)

