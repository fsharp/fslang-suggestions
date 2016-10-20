# Compiler directive for environment variables [13335678] #

**Submitted by Lenne on 4/6/2016 12:00:00 AM**  
**4 votes on UserVoice prior to migration**  

It would be nice to have a compiler directive for environment variables which can be used in string literals.
This way we can pass different parameters to type providers on a build server.
[<Literal>]
let ConnectionString = #env "MY_DB_CONNECTIONSTRING"
let cmd = new SqlCommandProvider<"...", ConnectionString>()



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/13335678)**


## Comments ##


#### Comment by Alexei Odeychuk on 4/8/2016 1:33:00 AM ####
Lenne, what's wrong with already-existing .NET built-in Environment.GetEnvironmentVariable method (from namespace System)?
You can use a .NET built-in method instead of the #env syntax suggested. The name of the built-in method would make your code more readable.
Code example:
open System
[<Literal>]
let ConnectionString = Environment.GetEnvironmentVariable("MY_DB_CONNECTIONSTRING")
let cmd = new SqlCommandProvider<"...", ConnectionString>()
Please see for more details:
Environment.GetEnvironmentVariable Method (String)
https://msdn.microsoft.com/en-us/library/77zkk0b6(v=vs.110).aspx
Hope it helps.


#### Comment by Gauthier Segay on 4/10/2016 8:35:00 PM ####
Alexey, your example would cause "This is not a valid constant expression." error.
Lenne, do you mean the value to be substituted at compile time? (I guess yes as it is a compiler directive).
I'm not sure I see value in this, is there prior art (any other compiler does that?)
I generally move those type of strings in a separate module, and can consider generating this module file as a preliminary build step.
Also, I think this can be addressed by a type provider altogether, maybe you should consider this instead?

