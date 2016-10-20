# Allow custom get/set functions when declaring auto-properties (and fix a related FSI bug) [6343892] #

**Submitted by Mark Laws on 8/25/2014 12:00:00 AM**  
**7 votes on UserVoice prior to migration**  

Auto-properties are nice, but there should be a way of providing functions for the get and set methods so that e.g. setting a property can automatically call other side-effecting functions. In other words, it would be nice to be able to write this:
type foo(?boolguy, ?settyguy) =
member val boolguy = defaultArg boolguy true with get
member val x.settyguy = defaultArg settyguy 1 with get, set v = x.settyguy <- v; printfn "hi"
Right now, you have to write this instead:
type foo(?boolguy, ?settyguy) =
let mutable _settyguy = defaultArg settyguy 1
member val boolguy = defaultArg boolguy true with get
member x.settyguy with get() = _settyguy and set v = _settyguy <- v; printfn "hi"
The proposed "member val x.settyguy" syntax would be a non-breaking change, because it's currently not legal syntax. In fact, there is a bug regarding this: in FSI, this passes without any warning or error:
type foo(?settyguy) =
member val x.settyguy = 1 with get, set
member x.settyguy = 1234
let () =
let q = foo()
printfn "%A" foo.settyguy // prints 1234
In FSC, the "member val x.settyguy" is flagged as an error.



## Response ##
** by fslang-admin on 9/6/2014 12:00:00 AM **

Declining per comment. Please add additional information if you think this should be reopened.
Don Syme, BDFL F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6343892)**


## Comments ##


#### Comment by Don Syme on 9/3/2014 4:48:00 AM ####
For me, the second code you show gives an error about a duplicate definition, in both FSI and FSC


#### Comment by Mark Laws on 9/4/2014 5:46:00 AM ####
Seems that FSI doesn't directly accept it, but in emacs fsharp-mode, if you put the second code into foo.fsx and do C-c C-f (fsharp-load-buffer-file), it passes.


#### Comment by Don Syme on 9/4/2014 6:16:00 AM ####
That's very odd! I wonder if something unusual is going on in the emacs mode


#### Comment by Don Syme on 9/6/2014 11:07:00 AM ####
My view on this proposal is that the syntax is not really that good for F# as it stands. While the syntax using a "let mutable" is longer, it is regular uses existing constructs. Making further additions to the auto-property syntax at this stage doesn't seem the right tradeoff of value v. language-churn. It's possible we could revisit this in a later stage.
For now I think we should decline this - though it's not a bad idea as such.

