# Type parameter grouping [7414162] #

**Submitted by Greg Rosenbaum on 4/1/2015 12:00:00 AM**  
**1 votes on UserVoice prior to migration**  

Sometimes, we want to have a method or type where some of the type parameters must be specified explicitly, while others could be inferred. For example, consider:
List.cast<'from,'to>

In this case, the `'from` parameter can always be inferred (unless we're putting the method into a function value), but the `'to` parameter may need to be specified explicitly.
Type parameter groupings allow you to specify some groups of type parameters, and have the compiler infer the rest. The above function for example might look like this:
List.cast<'to;'from> //two groups of type parameters

We can specify the first group of type parameters alone, invoking the function as `List.cast<int>`, or specify both type parameters at once giving `List.cast<int;string>` (if we want to put it in a function value for example).
This works when dealing with types as well. For example, given a type defined:
type Example<'first, 'second; 'third>(...) = ...

We can specify `Example<int, string>` and leave `'third` to be inferred (possibly generic), or we can specify the full `Example<int, string; int>`.
Of course, there is an issue with overload resolution, which is why I think type parameter grouping shouldn't b the default behavior. In the case of overload resolution, the compiler will always attempt to infer parameter groupings last, and try other things first (e.g. or `List.cast<int>` it will first look for `List.cast<'t>`)



## Response ##
** by fslang-admin on 2/3/2016 12:00:00 AM **

Declined per comment


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/7414162)**


## Comments ##


#### Comment by Don Syme on 2/3/2016 2:31:00 PM ####
I understand the proposal. We would probably do it differently, by marking some type parameters as "not required", i.e. inferable. I'll decline that since I believe that suggestion is covered elsewhere.

