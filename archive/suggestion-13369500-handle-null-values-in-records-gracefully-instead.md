# Handle null values in Records gracefully instead of crashing with a NRE [13369500] #

**Submitted by lr on 4/9/2016 12:00:00 AM**  
**0 votes on UserVoice prior to migration**  

Please see https://github.com/Microsoft/visualfsharp/issues/1044
Currently, if a nonnull field in a record (e.g. another record, or FSharpList<'T>, ...) is null, .GetHashCode (and potentially other methods) throw a NullReferenceException.
While these objects are obviously invalid and AFAIK can't be easily created in pure F#, this case sometimes happens out of the control of the user.
Examples are DataBinding in WPF and Serialization.
If the external code ever calls .GetHashCode on an object under construction, it will blow up.
The suggestion is NOT to change anything semantically but to handle null values gracefully where possible to ease the interop with these external libraries. This is especially important for .GetHashCode, since it is expected that it is always safe to call this method.
In the case of .GetHashCode, this could be handled backwards-compatible by returning a fixed hash for a null value.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/13369500)**


## Comments ##

