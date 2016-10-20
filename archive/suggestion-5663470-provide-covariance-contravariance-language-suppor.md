# Provide covariance/contravariance language support with syntaxes in F# in sync with covariance/contravariance in C#/VB [5663470] #

**Submitted by Eriawan Kusumawardhono on 3/21/2014 12:00:00 AM**  
**150 votes on UserVoice prior to migration**  

Covariance/contravariance has its beginning in CLR 2.0 and also with the introduction of generics in .NET 2.0 (also in F#, C# and VB)
Then in C# 4.0 and VB 10, we have covariance/contravariance supports in the language itself. Currently we don't have support for these covariance and contravariance in F#.
I know it is a runtime feature of CLR 2.0 and 4.0 and I don't want to play catch up with C# and VB.
But this covariance/contravariance support in C# and VB are powerful to use and also have proven to provide cleaner and clearer ways to understand the code and variances in the types, especially when using parameterized generic types.
This is not the same as this feedback:
http://visualstudio.uservoice.com/forums/121579-visual-studio/suggestions/2363794-ocaml-like-variance-annotations-a-and-a-
but we can use that OCaml syntax as well for starter.
This feature should also be constrained to only use covariance/contravariance in interfaces and delegates just like in C# and VB, but F# may provide more supports for other types such as events.
An example of this is the way F# has provided the capability to create extensions to properties and methods, not just methods only in C# and VB.
NOTE: Moved from http://visualstudio.uservoice.com/forums/121579-visual-studio/suggestions/3942302-provide-covariance-contravariance-language-support as suggested by Don Syme.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5663470)**


## Comments ##


#### Comment by Jon Harrop on 3/21/2014 11:40:00 AM ####
FWIW, I used OCaml for many years and never once found a use for co/contravariance in real code. There are some corner cases in F# with interop with OO libs like WPF but these are rare IME.
On a related note, I would like implicit upcast when creating a literal list or array of subtypes like let myControls : Control list = [Label(); Button()].


#### Comment by Jack Pappas on 3/23/2014 7:42:00 AM ####
This would be a nice feature to have. Even if it were infrequently used in F#-only code, it would be very handy to have when implementing libraries to be consumed from C#.
BTW, F# already does support a bit of contravariance via "flexible types". Flexible types don't seem to be used very often except with the 'seq<_>' type; if co-/contra-variance are properly supported in F# (a la C# 4.0), flexible types could be deprecated in favor of the variance annotations.
If this feature is implemented, I'd prefer it use the C#-style "in" and "out" keywords instead of OCaml's +/- syntax; I think the keywords are easier to read, they'll stand out when highlighted in an IDE, and it'll make it easier for C# developers to learn F# (or at least, they'll be able to re-use existing knowledge about the in/out keywords).


#### Comment by Eriawan Kusumawardhono on 3/24/2014 12:24:00 AM ####
Thanks for your nice comment, Jack!
IMHO, this is not just a nice feature to have, but it should be nice to have.
It's because the nature of F#'s strong typing, therefore it should span to strict and strong covariance and contravariance type.
These covariance and contravariance support is already supported deep inside the .NET CLR since .NET 2.0, so there should be a strong reason to leverage and promote this powerful runtime feature into language feature, not just C# 4.0 and VB 10 has done.


#### Comment by Eriawan Kusumawardhono on 3/24/2014 12:25:00 AM ####
Pardon my last comment, it should be must have instead of nice to have :)


#### Comment by Mauricio Scheffer on 3/27/2014 11:35:00 AM ####
As a workaround, some time ago I wrote a little program to add variance annotations to an interface after compilation, though this is only for interop purposes. Of course it doesn't add proper variance support in F#
https://github.com/mausch/VariantInterfaces


#### Comment by Bryan Edds on 4/8/2014 8:57:00 AM ####
Please don't do this. If you look at how badly variances complicate scala code and it's type system while realizing how surprisingly non-useful the feature is in practice (which is precisely as Jon H says), you realize such a feature is a net loss.
If you're wanting variance for interop, just remind yourself how much smaller this problem is, and how much easier it is to work around, than all the other problems with writing interop code.


#### Comment by Suminda Sirinath Salpitikorala Dharmasena on 5/6/2014 8:46:00 AM ####
I have run out of votes but this is a nice feature to have +3


#### Comment by Mauricio Scheffer on 7/14/2014 12:19:00 PM ####
Tweet from Erik Meijer related to this: https://twitter.com/headinthebox/status/487572643714203648


#### Comment by Mark Laws on 5/29/2015 5:50:00 AM ####
As the tweet from Erik Meijer linked below would suggest, F# lacks this due to its implications for type inference. Don Syme made a post about this same issue nearly ten years ago: http://osdir.com/ml/lang.fsharp.general/2008-09/msg00043.html
It would be a shame for F# to suffer for the sake of compatibility with a "feature" that's a corner case even in C# and VB.

