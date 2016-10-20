# dynamic -keyword support for F# [5664786] #

**Submitted by Tuomas Hietanen on 3/21/2014 12:00:00 AM**  
**9 votes on UserVoice prior to migration**  

There are times that e.g. F# value restriction could be solved with runtime dynamic code. C# has dynamic.
I wish F# could use dynamic as it uses mutable:
let I x = x
let dynamic F = II
As far as I know, there is no this kind of limitation in pure OCaml:
http://en.wikipedia.org/wiki/OCaml#Church_numerals
This could also help cross-language-scenarios (like using SignalR-library) which is possible now, when importing C# core dll, etc, but not easy.
And it would also allow more dynamic actor/agent-model: how to upgrade agent's functionality's type syntax: http://fssnip.net/h3



## Response ##
** by fslang-admin on 9/16/2014 12:00:00 AM **

Declining per the comments – the combination of the “?” operator, the “obj” type is sufficient for F#, plus the FSharp.Dynamic library is a good example of how to achieve this in purely library code.
Don Syme, BDFL F# Language/Library Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5664786)**


## Comments ##


#### Comment by Mark Seemann on 3/22/2014 3:35:00 AM ####
FWIW, I use FSharp.Dynamic to address this scenario: https://github.com/ekonbenefits/FSharp.Dynamic
It works pretty well


#### Comment by Will Smith on 3/23/2014 10:12:00 AM ####
Using existing C# libs that make use of dynamic is a fair argument. But IMO, F# should never support dynamic. Allowing dynamic is the opposite of what F# is, which is strongly typed. The ability to deviate from strong types just adds a layer complexity to the language which I think is unnecessary. I would hate to use existing F# code that made use of or exposed anything as dynamic; F# wouldn't feel the same in regards to safety.
A much stronger argument needs to be made for dynamic support.


#### Comment by Mauricio Scheffer on 3/24/2014 9:17:00 PM ####
How is the OCaml example related to "dynamic"? Also, that example works just fine in F#.


#### Comment by Daniel Slapman on 7/22/2014 10:18:00 AM ####
I'm totally agree with others, F# has a reach type system and has no need in 'dynamic' type.


#### Comment by Onur on 9/29/2014 1:59:00 AM ####
Don, ? operator doesn't support generic methods. Also FSharp.Dynamic has no support for PCL.
So it cannot be used if you have a portable library. I prefer something baked into the language.

