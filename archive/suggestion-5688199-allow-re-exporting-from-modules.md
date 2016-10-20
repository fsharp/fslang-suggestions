# Allow re-exporting from modules [5688199] #

**Submitted by Anton Tayanovskyy on 3/27/2014 12:00:00 AM**  
**60 votes on UserVoice prior to migration**  

OCaml, Haskell, Racket all provide mechanisms for re-exporting module bindings that the module imports from somwhere else rather than defining. This allows a simple library development startegy:
First, you start with one module (and file):
module MyLib =
...
...
...
As it grows too large, you move definitions out into separate modules that are kept internal, without breaking the interface.
module Imlp1.. =
...
...
...
module Impl2 =
...
...
module MyLib =
open Impl1
open Impl2
That allows a logical module to be assembled from separately written components, while being a single logical entity to the user.
In F#, some approximations are possible (manually re-exporting aliases, using namespaces), but overall the experience is irritating. Constraints F# currently imposes feel a bit baroque.



## Response ##
** by fslang-admin on 9/16/2014 12:00:00 AM **

As per my comments, I am declining this suggestion for now to allow votes to be recycled.
I am open to continued suggestions and discussions in the area of mixins, that cover both object programming and module programming. More code examples for would be welcome to help guide the discussion.
Don Syme, current BDFL F# Language/Library Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5688199)**


## Comments ##


#### Comment by Bryan Edds on 3/27/2014 9:33:00 PM ####
I find this interesting, and specifically useful in several places in my code.


#### Comment by Suminda Sirinath Salpitikorala Dharmasena on 5/6/2014 8:55:00 AM ####
Also 1st class modules would be interesting. One of the best selling points of OCaml.


#### Comment by Loic Denuziere on 6/10/2014 3:10:00 AM ####
Suggested syntax:
module MyLib =
open Impl1 // doesn't re-export anything from Impl2 (existing syntax)
open public Impl2 // re-exports everything from Impl1
open internal Impl3 // not sure if that would ever be useful, but why not
module SomeSubModule = Impl4 // local module alias (existing syntax)
module public SomeOtherSubModule = Impl5 // export a module alias


#### Comment by Anton Tayanovskyy on 6/18/2014 2:47:00 PM ####
First class modules would be nice but an order of magnitude harder to implement. Say, Haskell does not have them. I would like to keep this proposal simple to implement as this increases the probability it gets actually implemented.


#### Comment by Don Syme on 6/20/2014 8:58:00 AM ####
Hi all,
I generally have a negative predisposition to this feature from my experiences. For example, I've watched some OCaml programmers make a compete mess with it. In the scenarios I've seen, people have been trying to use the feature to achieve mixin-like software engineering composition - though the feature is very limited for this purpose. However, I haven't really seen them succeed with this in any way that looked convincing - and indeed they created code that was very hard to understand even in its basic shape and APIs.
I suppose this means I have a general negative predisposition to mixin features (except perhaps traits), since you have to "execute" the mixins to understand the resulting generated API. It seems wrong for F#. F# code (apart from provided APIs) doesn't generally have this property. For F# software engineering APIs - modules and object types - F# code has a "what you see is what you get" property, at least with regard to named items in the modules and object types.
Could you point us to examples of OCaml code that uses this in what you regard as very positive ways?
Thanks
Don


#### Comment by Don Syme on 9/16/2014 7:34:00 AM ####
One particular concern not mentioned before is that type identity (i.e. the exact module where a type was originally defined) would still be visible after the re-export. That is, a signature couldn't hide that fact that a type ultimately came from Impl1 or Impl2 (because in .NET compiled code types have a full path)

