# Allow lower-case DU cases when [<RequireQualifiedAccess>] is specified [15801949] #

**Submitted by Alex Corrado on 8/24/2016 12:00:00 AM**  
**1 votes on UserVoice prior to migration**  

Currently, it is not allowed to declare DU cases with lower-case letters. For instance, this is not allowed:
type Foo =
| foo
| bar
| baz
// etc...
This yields: error FS0053: Discriminated union cases and exception labels must be uppercase identifiers
As I understand it, this is to prevent ambiguity in pattern matching between matching a union case and binding to an identifier. However, this is not an issue if the [<RequireQualifiedAccess>] attribute is specified on the DU. Therefore, I propose we allow lower-case cases in this case.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/15801949)**


## Comments ##

