# Return untyped syntax tree from ITypeProvider [15202209] #

**Submitted by Isak Sky on 7/13/2016 12:00:00 AM**  
**27 votes on UserVoice prior to migration**  

Add the ability to *opt in* to send back an untyped syntax tree from ITypeProviders. The current type provider mechanism is good for simple data exploration use cases, but otherwise extremely limited, and will soon allow for less metaprogramming than Roslyn in some ways. Currently, some types of type providers not possible to create, because unbound generics, records, discriminated unions, and other normal language features are not supported.
With the ability to opt in to just returning an untyped syntax tree, it would enable the creation of just about any type provider. It would also effectively give F# macros, though through an API rather than syntax.
These new kind of type providers would be hard to create initially, but the community would be empowered to create libraries to wrap the untyped syntax tree to make it easier to use, and it would soon be an extremely effective and powerful way to do metaprogramming.
Another benefit is that there wouldn't really be much of a design to experiment with to get right - it is just the untyped syntax tree of the language, which we already have a version of.
The F# community has very limited resources, and this would be an extremely leveraged way to utilize them.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/15202209)**


## Comments ##


#### Comment by Alexei Odeychuk on 7/17/2016 4:15:00 PM ####
One of the F# strengths is its strong typing. It is not a dynamic typed language. Strong typing helps spotting bugs in code early and produce safe, secure and high-performance code. Maybe it would be better to address the core problem: to develop support at the compiler level for creating unbound generics, records, discriminated unions, and other normal language features in type providers that lack support as of today, preserving F# as a strongly typed language.


#### Comment by Isak Sky on 7/18/2016 12:22:00 AM ####
Alexei Odeychuk: I agree it would be nice, but we also have to think about how to best utilize our very limited resources. Remember that type providers have been out for many years, and we still don't have anywhere close to full language support. I think we have to be open to the possibility that the current design is too difficult to implement.
Thinking of good abstractions for meta programming is incredibly hard, and there are a lot of big issues with the current approach F# takes, as anyone who has written a type provider can tell you. That is why I think it is better to expose a lower level API, and let the community build on this instead.


#### Comment by Dave Thomas on 7/18/2016 8:11:00 AM ####
The big problem with TP's is a lot of errors come during running the second instance of your dev environment during quotation splicing, so they are not well typed enough during development.

