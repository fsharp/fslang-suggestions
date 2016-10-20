# Smart constructors for DU cases [5671087] #

**Submitted by Jack Pappas on 3/23/2014 12:00:00 AM**  
**13 votes on UserVoice prior to migration**  

When a DU type is defined, the F# compiler creates a static method on the class for each defined, non-nullary case. The method is called NewXYZ, where XYZ is the name of the case.
It would be useful to be able to decorate a non-nullary case with an attribute [<SmartConstructor>] which would cause the compiler to add a suffix (e.g., "Impl") to the normal factory method for the case (described above) and also mark it 'private'. The compiler would then require you to define a static NewXYZ method on the type, taking the same arguments in the same order as the case.
This would provide a way to implement "smart constructors" for a union type in such a way that there'd be no way to accidentally _not_ call them when creating an instance of the case. These "smart constructors" are extremely useful for enforcing invariants when implementing functional data structures, or automatically applying simplification routines (e.g., to an arithmetic AST) to enforce normalization and minimize computation time; it could also be used to enforce validation of data held by a DU type.
Within the custom factory method for a case, any places where an instance of _this_specific_case_ is created, we'd call the now-private, compiler-generated factory method. For any other cases being created, we'd call the normal, public factory method for that case (which may itself be a custom factory method).
For example:
type Email =
[<SmartConstructor>]
| Valid of EmailAddress:string
| Invalid of ErrorMessage:string
with
static member NewValid (address : string) =
// Validate the given address.
if String.IsNullOrEmpty address then
Invalid "The address was null or empty."
else
// Pretend we have some validation function here which returns an error message if the email is invalid
match EmailAddress.Validate address with
| true, _ ->
Valid address
| false, errMsg ->
Invalid errMsg



## Response ##
** by fslang-admin on 2/5/2016 12:00:00 AM **

Thanks for the suggestion, which is definitely interesting. Declining per my comment, please take a look
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5671087)**


## Comments ##


#### Comment by Don Syme on 2/5/2016 8:49:00 AM ####
Thanks for the suggestion.
Enforcing invariants on union and record types is a serious issue. The recommended way is either to use a class type, or to hide the representation.
This is an interesting midpoint, which is to intercept the construction methods for the union type. It's more difficult to design a corresponding way to do this for a record type.
However, in the balance this feels too adhoc to embrace in the F# language design: would we do the same for Is*? for accessors? Would we make union types purely pattern-based? Just doing the New* case seems like scratching the surface and opening a box with more inside it.
I will mark this as declined, though it's definitely an interesting idea and something I had not thought of doing.

