# Implement Syntactic Macros [5674940] #

**Submitted by Bryan Edds on 3/24/2014 12:00:00 AM**  
**453 votes on UserVoice prior to migration**  

At least give it a try in a private branch, and upon success, enable them publicly with a compiler switch initially.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5674940)**


## Comments ##


#### Comment by Tomas Petricek on 3/24/2014 4:03:00 PM ####
I would be quite interested in the use cases that you have in mind for this? Restricted macro functionality is already available with quotations, type providers & reflection, so I'd like to know what interesting use cases are left :-)


#### Comment by Bryan Edds on 3/24/2014 4:17:00 PM ####
Tomas, my friend, you ask for too much! I will attempt to post one use case for F# macros here every business day as long as I can manage :)
For today, the use case is more-automated generation of lens values. Lenses, both full and partial, are no where near first-class enough in F#. You can't do real FP without them. Macros should bring us closer, and also give a prototype showing how the language implementers might design them in the case they do make them first-class.


#### Comment by Giuseppe Maggiore on 3/25/2014 9:20:00 AM ####
Games would greatly benefit from having macros or other similar, high-performance, portable ways to generate complex code.
Seconded with all my heart :)


#### Comment by Will Smith on 3/25/2014 10:05:00 AM ####
Gluseppe,
For games, inlining functions help a lot especially for linear algebra math operations. It's much more idiomatic to use inlined functions than macros for performance. It's not always true, however, that inlining a function will give you better performance, in fact, it can give you worse depending on the function if it's long + complex. A macro would be no better here.
I'm doing this myself now and it works just as good as any macro would; however, there are a few outstanding issues with struct param types with inlined functions, but I have a slightly edited compiler that fixes that.


#### Comment by Richard Minerich on 3/25/2014 10:27:00 AM ####
I could see something similar to template haskell being useful, one example of use would be generating lenses.


#### Comment by Bryan Edds on 3/25/2014 11:02:00 PM ####
Macro use case for the day #2 -
Implement F# features outside the compiler so that even idiomatic F# code can be back-ported to OCaml.


#### Comment by Jon Harrop on 3/26/2014 5:57:00 AM ####
@Tomas: Macros are used to customise syntax. For example, you might want to replace the pattern "| Add(f, g) -> d f + d g" with "| f+g -> d f + d g".


#### Comment by Bryan Edds on 3/27/2014 9:28:00 PM ####
Macro use case of the day #3 -
Let the community take more of a role in prototyping new F# language features with macros instead of forcing them to hack their own private compiler branch and thereby losing all portability.


#### Comment by Bryan Edds on 3/31/2014 10:14:00 AM ####
Macro use case of the day -
If we can allow macros to be imported based on a containing namespace / module, various DSL contexts could be opened separately, without clashing.


#### Comment by Mastr Mastic on 4/2/2014 11:01:00 AM ####
Fully seconded, and Bryan you're a hero for initiating this.
Macros are so underrated and to be fully honest, in my opinion this is a must!
I'll even go as far to say that imo every programming language should have macro support.
For instance, I can't begin to describe how much I dislike GUI development just because you have to manually raise events and legit repeat yourself again and again and again, which just results in filthy messy code.


#### Comment by Mastr Mastic on 4/2/2014 11:06:00 AM ####
Also if I may add another macro use case:
More aliasing functionality.
for instance, I highly dislike having to re-type this again and again:
[<CompilationRepresentationAttribute(CompilationRepresentationFlags.ModuleSuffix)>])
Type aliasing can't deal with this since the result is not a type.
Inheritance is not an option since the attribute is sealed.
Only option I can think of to deal with these kind of cases (this is merely an example) is macros.


#### Comment by Will Smith on 4/3/2014 3:02:00 PM ####
If F# has proper macros, this means you would be able to create another language inside F#. Do we really want that?
---
"Implement F# features outside the compiler so that even idiomatic F# code can be back-ported to OCaml."
Why would you want to use macros as a means of back-porting? Arn't there better ways that don't infect the language itself?
"Macros are used to customise syntax. For example, you might want to replace the pattern "| Add(f, g) -> d f + d g" with "| f+g -> d f + d g"."
Couldn't we find a way to extend the F# language that makes something like this possible without relying on macros?
"Let the community take more of a role in prototyping new F# language features with macros instead of forcing them to hack their own private compiler branch and thereby losing all portability."
A true prototype of a language feature is to have a modified version of the compiler. That is the proper way. Using macros for a prototype do not tell you what is involved in actually implementing a language feature.
"If we can allow macros to be imported based on a containing namespace / module, various DSL contexts could be opened separately, without clashing"
How is this a use case for a need to use macros?
"I can't begin to describe how much I dislike GUI development just because you have to manually raise events and legit repeat yourself again and again and again, which just results in filthy messy code."
You can create abstractions already, or even use type providers to generate all the mess so you don't have to.
"for instance, I highly dislike having to re-type this again and again:
[<CompilationRepresentationAttribute(CompilationRepresentationFlags.ModuleSuffix)>])"
So we can use macros for anyone to call what this behavior does anything they want? I agree that I dislike typing that again and again; but, I feel like we could figure out a simple language feature that could solve this in an idiomatic way.


#### Comment by Mauricio Scheffer on 4/4/2014 7:23:00 PM ####
Other than lenses, lots of things could be derived for a type with a macro: functor, applicative, monad, a serializer. None of the current metaprogramming facilities can do that as far as I know, and you can't build all of that into the language (for example deriving a serializer depends on a specific serialization library).


#### Comment by Bryan Edds on 4/4/2014 7:43:00 PM ####
Sorry I haven't been posting the use cases for macros like I promised - I've been in the hospital for 4 days now (obviously unrelated).
Will, if macros are only able to be enabled via a compiler-switch, it will not effectively change the language for the typical user, so there are no direct down sides there.
For people who need to program at the language level (such as framework developers), macros are a must (at least in a black-box language like F#). For those who have only ever consumed those types of services (as opposed to writing them properly), they will only see macros through the the Blub Paradox - http://paulgraham.com/avg.html .
Therefore, only programmers who write at the language level will ever turn on the feature, but those who blithely consume our work will keep the feature off - if they even know it exists in the first place.
* Yes, F# is a black-box language. Just because the compiler is open source does not mean it is white box. If you want to see a white box language, look at AML here - https://github.com/bryanedds/OmniBlade


#### Comment by Mastr Mastic on 4/7/2014 10:35:00 AM ####
@Will Smith
There is mess with abstractions as-well.
As for the attribute, I'll mention again that this is merely an example.
Sure, the F# team could introduce a ModuleSuffixAttribute as a shortcut, and maybe even have an optional Boolean parameter for RequireQualifiedAccess, and I was even about to suggest this but then the idea of macros came up and swiped it away because with macros you could do that + more + a lot more!


#### Comment by Bryan Edds on 4/8/2014 8:48:00 AM ####
* Just for clarification *
The compiler switch for enabling macros should allow new macros to be defined. Using existing macros should not require a compiler flag. This way, library developer can opt-in to access macro implementation syntax, and consumers can use library macros more transparently (either as if they were an ambient language feature, or a custom syntax imported from an F# namespace / module).


#### Comment by Will Smith on 4/13/2014 1:38:00 PM ####
That stinks you were in the hospital Bryan! I hope you are feeling better!
If macros were going to be implemented, a compiler directive or switch would be the least of all evils. That is my opinion and I could live with it.
This feature currently has the most votes, so it is clear that a lot of people want this for a good reason.
I want to be convinced that macros would really benefit F#; because I really fear this feature a lot. I'm looking for the bigger picture here, but so far all I see is syntactic sugar. I read there is the framework side, but I don't have a clear understanding of the problems devs are facing when developing a framework.
Could anyone show some example problems that macros would truly help resolve? Syntactic sugar is not one of them.


#### Comment by Mastr Mastic on 4/14/2014 6:02:00 PM ####
Will, personally I can't think of any (at least atm); I also can't think what more they need to do, because after all that is their purpose.
But how about share your thoughts and let us know what's daunting about macros.
I mean, yeah, it can definitely be misused like any other feature, but the good thing about macros is that you can simply choose not to use them.
They will not invade your work, but only be there for you to use when the trade-offs worth it in your opinion.
And perhaps if macros will be implemented (fingers crossed) they could also be removed from a certain point (very much like #undefine in C & C++).
That being said, I'd like to point out (to everyone) that all in all, macros allow you to make code more compact, shorter, succinct, readable, simpler, etc.
That's their point (syntactic sugar).
Now just notice how about any best practice you read in a book, online, hear from a friend will have the same reasons for usage. That's what we need, simple compact code.
So my viewpoint is: Program with care, play nice, have macro support, and the result is a maintainable code, that is a pleasure for the eyes to see.


#### Comment by Mauricio Scheffer on 4/14/2014 6:16:00 PM ####
Will, a lot of use cases have been mentioned in this thread that are not about syntactic sugar: lenses, serialization, derivation of functor/applicative/monad. Also derive curried constructors for records, which would help a lot with applicative functors.
All of these are about reducing boilerplate by generating code at compile-time.


#### Comment by Bryan Edds on 4/15/2014 12:06:00 AM ####
I'm starting to wonder if there is a bit of confusion between textual macros (like those found in C and C++) and my suggestion of syntactic macros.
For surefire clarification, here are links describing each -
Textual Macros - http://en.wikipedia.org/wiki/Macro_%28computer_science%29#Text_substitution_macros
Syntactic Macros - http://en.wikipedia.org/wiki/Macro_%28computer_science%29#Syntactic_macros
The difference between the two is very big, and I too would object to any suggestion of putting textual macros in F#! :)


#### Comment by Dave Thomas on 4/24/2014 3:37:00 AM ####
I think I would prefer expanded quotation and Type Provider support. The language is at a very stable base and Im not sure you could convince me that macros are necessary.


#### Comment by Bryan Edds on 4/24/2014 6:54:00 AM ####
Hi Dave!
Could you elaborate on what you mean by 'expanded' in these cases, and perhaps give examples where they would obviate macros?


#### Comment by Bryan Edds on 4/24/2014 7:13:00 AM ####
Dave and all,
Here's a super nice macro use case; Making FSCL more syntactically elegant. FSCL is amazing, but the amount of attributes and <@code quotation symbols@> flying around in its usage code makes it much harder to read and write than it should be, as well as error prone -
"Ah, why doesn't this work?! Did I leave out an attribute or parameter again?"
Imagine all that encapsulated behind a DSL that looks like first-class F# syntax - all just by opening the appropriate module.
Could expanded code quotations and / or type providers really obviate macros in cases like this?


#### Comment by mavnn on 4/25/2014 10:04:00 AM ####
@Bryan I don't know if this is what Dave was thinking, but a lot of type kind like functionality could be implemented by type providers that could be parameterized by type or by quotation.
Combined with better quotation evaluation out of the box, it would cover most of the use cases I've seen so far, especially Mauricio's lens et al.


#### Comment by Bryan Edds on 4/25/2014 10:25:00 AM ####
Hi mavnn!
It would be interesting to see some explanation of what the semantics of better / expanded type providers and quotations would entail, along with a couple of examples demonstrating how they would obviate macros.
Would you or Dave mind writing something like that up as an F# user voice suggestion so we can study upon and vote for it?


#### Comment by Suminda Sirinath Salpitikorala Dharmasena on 5/6/2014 8:33:00 AM ####
I think the following related concepts might be relevant:
1) Metaprogramming
2) Dilecting - Syntax mutation is dilecting
3) Extensible programming
4) Higher Order Abstract Syntax - http://en.wikipedia.org/wiki/Higher-order_abstract_syntax, http://www.cs.cmu.edu/~fp/papers/pldi88.pdf
5) Staging


#### Comment by mavnn on 5/7/2014 4:41:00 AM ####
@Bryan sorry for the slow response. Type providers that could take a type would allow you to generate things like lenses on the fly. Having said that...
... I actually very much like the idea of syntactic macros and have voted for this idea. So I'm not going to spend too long disagreeing with you!
It does have to said that a lot of very similar functionality could be provided by better support for evaluating quotations and that may be the more practical solution in the short term.


#### Comment by Suminda Sirinath Salpitikorala Dharmasena on 5/7/2014 10:55:00 PM ####
There are 3 ways to do this
1) Quasi Quotes (QQ)
2) Macros
3) GADT
Why not have all 3. F# is very well capable of doing this. If you use QQ you are dealing with concrete syntax. In other ways you can deal with it at the AST level also.


#### Comment by Suminda Sirinath Salpitikorala Dharmasena on 5/7/2014 10:58:00 PM ####
MetaOCaml, PPX, Camlp4/5 can be a good starting reference to explore the possibilities. Especially MetaOCaml. Love the concepts in this.


#### Comment by Suminda Sirinath Salpitikorala Dharmasena on 5/8/2014 12:07:00 AM ####
Also it would be very cool if you can use the meta programming facility to have projectional editors within the language.


#### Comment by Suminda Sirinath Salpitikorala Dharmasena on 5/8/2014 3:35:00 AM ####
Also MetaML and Template Haskell would be good starting points to flesh out a strawman speck for this feature.


#### Comment by Suminda Sirinath Salpitikorala Dharmasena on 5/10/2014 1:09:00 AM ####
Something interesting I stumbled across. Some of this research could be taken into consideration http://ltamer.sourceforge.net/


#### Comment by Kurt on 7/6/2015 5:46:00 AM ####
Here's how Boo does it: https://github.com/bamboo/boo/wiki/Syntactic-Macros


#### Comment by Yaar Hever on 3/13/2016 10:31:00 PM ####
I think macros would make it much easier to implement the missing functionalities of type providers (like creating F# specific types) and to have a functional way of writing type providers.


#### Comment by Anonymous on 3/14/2016 8:08:00 AM ####
Having a proper macro system would probably make type providers obsolete, the current mechanism (putting it politely) is a crap fest.


#### Comment by Kurren Nischal on 3/19/2016 5:02:00 AM ####
This would be a dream come true


#### Comment by Yemi Bedu on 5/29/2016 4:03:00 AM ####
/archive/suggestion-5975797-allow-implicit-quotation-of-expressions-used-as-a
Hello,
So I would recommend that the above be extended to work with general methods (functions)
The definition of it could look like:
def nameof (q:'T) = match q with
| Quotations.Patterns.ValueWithName(o, ty, n) -> n
| Quotations.Patterns.Let(v, e1,e2) -> v.Name | expr -> expr.ToString()
which is shorthand for writing:
let nameof ([<ReflectedDefinition>] q:Quotations.Expr<'T>) : string = match q with
| Quotations.Patterns.ValueWithName(o, ty, n) -> n
| Quotations.Patterns.Let(v, e1,e2) -> v.Name | expr -> expr.ToString()
let y = 1
printfn "%s" (nameof y)
Thank you. Good day.

