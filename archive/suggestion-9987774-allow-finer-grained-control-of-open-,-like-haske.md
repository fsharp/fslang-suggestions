# Allow finer-grained control of "open", like Haskell's "import hiding" [9987774] #

**Submitted by Robin Munn on 9/30/2015 12:00:00 AM**  
**21 votes on UserVoice prior to migration**  

Currently, F#'s "open" keyword imports everything from the opened namespace, which can result in unexpected shadowing. For example, if I do:
open Foo
// fn1 and fn2 are defined in Foo
let bar (x:Foo.DataType) : DataType = x |> fn1 |> fn2
If a later version of Foo defines a "bar" function that does something completely different, I might later write code that tries to call Foo.bar as "bar", forgetting that I had created my own "bar" function. Worse, if Foo.bar is defined with the type Foo.DataType -> Foo.DataType, then the compiler won't even be able to save me from my mistake!
What I'd like to be able to do is specify exactly which names I'm importing from any given module. Something like one of the following syntax examples:
open Foo using only (fn1, fn2)
open Foo importing (fn1, fn2)
open Foo with only (fn1, fn2)
open Foo with (fn1, fn2)
Or, alternately, to import everything except for a few names:
open Foo hiding (bar)
let bar = ... // Be explicit about not shadowing
The syntax examples I've listed above are only a few possible ideas that I came up with in five minutes; other possible keywords might be better.
This is related to, but not the same as, the following two suggestions:
/archive/suggestion-6958404-allow-opening-of-static-classes-like-modules
/archive/suggestion-6323201-aliases-for-namespaces
/archive/suggestion-5690218-allow-open-in-local-declarations-like-in-standard
The Python community has had a long-standing recommendation NOT to use "from Foo import *" (the Python equivalent of "open Foo", which imports all its names into the current namespace), due to precisely the kinds of namespace pollution issues that "open Foo" can cause. The strong recommendation in Python is to be explicit about what names you're bringing into your local namespace: "from Foo import (fn1, fn2)" and I'd like to see F# allow that very good practice as well.



## Response ##
** by fslang-admin on 2/4/2016 12:00:00 AM **

Thank you for making this suggestion. I’ve marked it as declined per my comment below.
However I sympathise with the suggestion and would like to hear more if yo find specific situations where not having this feature has caused bugs,
Don Syme,
F# Language and Core Library Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/9987774)**


## Comments ##


#### Comment by Radek Micek on 10/19/2015 3:19:00 PM ####
Instead of
open Foo using only (fn1, fn2)
you can write
let fn1, fn2 = Foo.fn1, Foo.fn2
Or instead of opening a module you can create an alias and qualify its values by the alias.


#### Comment by Robin Munn on 1/9/2016 2:52:00 AM ####
While Radek Micek's suggestion of "let fn1, fn2 = Foo.fn1, Foo.fn2" works, I find that I don't like doing that. I don't know why, but that (perfectly workable) solution feels "inelegant" to me, and I'd still prefer to have an expanded "open Foo importing (fn1, fn2)" (or "open Foo hiding (bar)") syntax.


#### Comment by Don Syme on 2/4/2016 4:28:00 PM ####
I sympathise with this suggestion and thank you for taking the time to make it.
We have definitely considered constraining "open" in F#. Strangely, it doesn't seem as necessary for good software engineering to do this as in Haskell and Python. I think this is because of three reasons
1. F# uses a lot of type-qualified name resolution. So x.ABC resolves the name ABC according to the inferred type of x. This means there are far fewer name clashes as names are brought in. Likewise F# uses a lot of module-qualified name resolution like List.map. Together these mean there are far fewer clashes
2. Since F# is typed (unlike Python), name clashes are almost always caught in practice
3. There is always the cop-out of using "module X = SomeModule" or "global.Foo.Bar" to resolve things.
So I am going to mark this as declined. However I would still like to hear of cases where not having this feature has caused bugs in software, particularly when upgrading packages.

