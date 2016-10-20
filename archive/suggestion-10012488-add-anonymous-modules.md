# Add anonymous modules [10012488] #

**Submitted by Alex Corrado on 10/1/2015 12:00:00 AM**  
**1 votes on UserVoice prior to migration**  

Often, I find myself writing little private modules to provide some syntactic sugar for a type that I'm using heavily in a file.
For instance, take this method for quoting an F# function into a LINQ Expression Tree from http://stackoverflow.com/a/23146624/578190. It would be nice if I could write it like this:
open System.Linq.Expressions
open module =
type Expression with
static member Lambda(e:Expression<_>) = e
The above construct would be equivalent to this:
module private SomeGeneratedNameIDontCareAbout =
type Expression with
static member Lambda(e:Expression<_>) = e
open SomeGeneratedNameIDontCareAbout
Note that the module is implicitly private; it effectively has no name, so there is no way to reference its members outside the scope in which it is open'd.
The `open module =` syntax is just my random suggestion :)



## Response ##
** by fslang-admin on 1/23/2016 12:00:00 AM **

Declined per comment from requestor


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/10012488)**


## Comments ##


#### Comment by Alex Corrado on 10/1/2015 1:03:00 PM ####
A colleague just pointed out that you can do this:
[<AutoOpen>]
module private __ =
...
Not quite as pretty, but adequate. Feeling a little silly, I withdraw my suggestion.

