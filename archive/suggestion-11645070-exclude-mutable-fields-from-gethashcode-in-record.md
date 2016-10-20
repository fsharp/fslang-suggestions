# Exclude mutable fields from GetHashCode in record types [11645070] #

**Submitted by amazingant on 1/29/2016 12:00:00 AM**  
**6 votes on UserVoice prior to migration**  

The current default implementation for GetHashCode on record types includes all fields, including those marked as mutable. While this certainly helps in testing structural equality, this violates the MSDN documentation's recommendations for how to implement the function (seen at https://msdn.microsoft.com/en-us/library/system.object.gethashcode%28v=vs.110%29.aspx under "Notes to Inheritors").
While this is not typically an issue, as records are normally used as immutable data types, it becomes an issue in cases where the hash codes are relied upon. As an example, if a collection of record values is provided as the ItemsSource for a WPF ListView control (even stored in an ObservableCollection<T>), modifying mutable fields while elements in the list are selected renders those elements impossible to deselect.
This can currently be worked around by overriding GetHashCode on a record type that needs it, although this means also adding the CustomEquality and CustomComparison attributes, overriding the Equals method, and implementing either IComparable or IStructuralComparable. None of this is terribly difficult, but removes the terseness that I've grown to love when defining record types instead of classes.
Originally posted on GitHub as an issue, as this behavior breaks a standard WPF control :) https://github.com/Microsoft/visualfsharp/issues/912



## Response ##
** by fslang-admin on 2/3/2016 12:00:00 AM **

Declined per my comment below, though an off-by-default warning PR would be accepted.
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/11645070)**


## Comments ##


#### Comment by Isaac Abraham on 2/2/2016 4:25:00 AM ####
I think implicitly changing the behaviour of GetHashCode etc. simply based on the fact that a field is mutable or not is a little dangerous - I would prefer something explicit e.g. something like marking the field that you want to use for hashcode directly, and / or a compiler warning that says "you have a record with mutable fields and are using default equality codegen, this is unsafe"


#### Comment by amazingant on 2/2/2016 1:54:00 PM ####
Since someone somewhere may depend on it behaving contrary to the implementation recommendations, and therefore I can't have nice things that work as advertised... I'd lean towards a compiler warning.
It would also be nice to get documentation somewhere like the Records page (https://msdn.microsoft.com/en-us/library/dd233184.aspx) documenting the fact that common UI elements (Microsoft-provided ones at that, so no "some third-party tools may break" crap) are affected by it. The documentation should really be updated somewhere to indicate this, regardless of what (if any) changes are made to the compiler.
Given your first suggestion, if one were to explicitly mark fields as being part of the GetHashCode calculation, I'd say it should be possible to apply to multiple fields at once. I'd still suggest a compiler warning though, such that if you added the attribute to a mutable field, you still got some kind of notification that it may cause issues.


#### Comment by ADMIN
fsharporg-lang (F# Software Foundation Language Group, F# Software Foundation) on 2/3/2016 10:59:00 AM ####
We couldn't accept the change proposed (exclusion) since it would be breaking.
A warning that suggests putting [<NoEquality; NoComparison>] or implement custom comparison might be possible. There is however the question is how to make the warning go away if the default GetHashCode is intended (there are cases where you want mutability during initialization prior to any hashing occuring). If the warning were an off-by-default Level 4 warning it would probably be ok.
I'm going to mark the specific proposal as declined since it would be breaking. However please consider submitting a PR for a level 4 warning along the lines above.
Don Syme, F# Language Evolution


#### Comment by Don Syme on 2/3/2016 3:09:00 PM ####
See also /archive/suggestion-5663332-allow-custom-equality-on-record-types

