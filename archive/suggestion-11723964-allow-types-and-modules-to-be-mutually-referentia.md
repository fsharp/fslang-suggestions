# Allow types and modules to be mutually referential (not across files, only within a closed scope in a single file) [11723964] #

**Submitted by Don Syme on 2/4/2016 12:00:00 AM**  
**15 votes on UserVoice prior to migration**  

Currently types and modules can't be mutually referential - a group of types can be using "type X = ... and Y = ... "
I propose we allow a collection of types and modules within a single file to be mutually referential, either by using
type X = ... and module Y = ...
or by allowing a #mutrec declaration within a module or namespace declaration group that "turns on" mutual-reference within that scope (no larger than the file). The latter option is appealing as "and module" is not required (no new syntax is required) and the syntax of mutually recursive types becomes more regular
namespace Foo
#mutrec
type X = ... refer to Y and Z...
type Y = .... refer to X and Z...
module Z = ... refer to X and Y ...
Inference would be as "one big mutually referential group", just as "type Y = ... and Z = ..." today. Execution of initialization code would be as an initialization graph, just as "static let" today.



## Response ##
** by fslang-admin on 6/23/2016 12:00:00 AM **

Based on the prototypes and experiments with this feature reported at https://github.com/fsharp/FSharpLangDesign/blob/master/RFCs/FS-1009-mutually-referential-types-and-modules-single-scope.mds, I’m marking it as “approved in principle”.
This RFC and its implementation have now been accepted.
Don Syme,
F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/11723964)**


## Comments ##


#### Comment by Mark Seemann on 2/7/2016 4:02:00 PM ####
What is the motivation behind this idea?
One of the features of F# that I greatly appreciate is that it prohibits cyclic references. In my experience, it's always possible to design the code so that mutual references aren't necessary. I don't even use the 'and' keyword.
I'd be sad to see this feature eroded.


#### Comment by Don Syme on 2/8/2016 9:01:00 AM ####
The ability to create a closed set of mutually recursive types (including static methods and data) is part of the F# language design: the intent has never been to adopt an extreme position where all mutual recursion is banned.
Like many things in F# (mutable, implementation inheritance, null etc.), mutual reference is relatively de-emphasized and scoped, but not banned. The F# 1.0-4.0 design for mutual recursion is fine for the vast majority of purposes and sets the defaults in the right way. However, it is fair to say that it places an artificial distinction which can be worse than awkward on the occasions that mutual reference is used: it says that a closed set of types (with static methods) can be mutually referential, but modules containing functions may not be included in that. Likewise data-carrying exception declarations may not be included in that. There's no strong reason for those restrictions.
Were a proposal along these lines to be implemented, F# will continue to de-emphasize mutual references by default, and the intent is not to shift the language towards open mutual references across all files in an assembly. The question, as always, is finding the right balance.


#### Comment by trek42 on 3/12/2016 10:08:00 AM ####
This is great! Not being able to cross-reference between closely-related (basically, the same) type and module is very annoying, esp. if you are used to define type A for state and module A for APIs that operate on A. Sometimes this can be solved by having "module A_Helpers ..." that followed by "type A" and "module A", but there are cases where this isn't sufficient, and the only way is to use static member in "type A" to simulate module functions.
Another related suggestion: while we are at this, can we fix the issue that [<CompilationRepresentation(ModuleSuffix)>] only works when you have the type with the same name already defined before the module, otherwise there is still a name conflict.
See: http://stackoverflow.com/questions/24684918/module-and-class-with-same-name
(note: the workaround proposed in the link doesn't work with Record type, and practically Record type with same-named module is much more common then class type).

