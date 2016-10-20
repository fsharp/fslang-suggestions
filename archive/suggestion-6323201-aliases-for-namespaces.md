# Aliases for namespaces [6323201] #

**Submitted by Daniel Bradley on 8/20/2014 12:00:00 AM**  
**17 votes on UserVoice prior to migration**  

[ Edited by admin to apply to namespaces only, since as per comment you can already do this with module aliases ]
When using the ‘open’ keyword, allow a namespace being imported, to be assigned to an alias rather than the imported contents being made available to the current scope e.g.
namespace Foo = Some.Long.Path.To.Foo
This would be useful when importing namespaces containing modules/types with the same name to avoid fully qualifying all of the usages.



## Response ##
** by fslang-admin on 2/10/2016 12:00:00 AM **

Thanks for the suggestion. It is quite a reasonable one and it has taken me a long time to mark this as declined. However I have now done so for the reasons listed below.
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6323201)**


## Comments ##


#### Comment by Loic Denuziere on 8/21/2014 8:00:00 AM ####
You can already do:
module Foo = Some.Long.Path.To.Foo
Unfortunately you can't do that with namespaces, that would indeed be useful.


#### Comment by Don Syme on 7/18/2015 2:08:00 PM ####
I edited the content to apply to namespaces only, since module aliases are already available.


#### Comment by Don Syme on 2/10/2016 11:12:00 AM ####
My feeling is that we will not do this feature. You can already alias types and modules so can define alternative names for those inn ambiguous cases. You can also use "global.Namespace1.Namespace2....." to disambiguate things. My feeling is that is sufficient in F# and also results in a good balance between code readability and aliasing.

