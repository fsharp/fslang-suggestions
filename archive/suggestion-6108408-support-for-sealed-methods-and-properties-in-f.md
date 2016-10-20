# Support for sealed methods and properties in F# [6108408] #

**Submitted by Expandable on 6/27/2014 12:00:00 AM**  
**15 votes on UserVoice prior to migration**  

I've recently noticed that F# doesn't support the definition of sealed overriding methods and properties. When you seal an overriding method or property in C#, only that method or property can no longer be overridden in deriving classes while other methods or properties still can be (in contrast to sealing the entire class, where the entire class can no longer be inherited).
F# honors sealed classes defined in both C# and F# as well as sealed methods and properties defined in C# code in the sense that it does not allow deriving from such a type or overriding such a method or property. However, while it is possible to seal a class defined in F# using the [<Sealed>] attribute, it is currently not possible to seal an overriding method or property.
I suggest to add this feature, as it is occasionally useful and shouldn't be that hard to implement, given that the compiler already rejects all attempts to override a sealed method or property. Implementing this feature would require the following changes, as far as I can see:
- The F# core library must be updated so that the [<Sealed>] attribute can also be used on methods and properties. That change is trivial.
- The F# compiler must emit the required IL metadata for properties and methods marked with the [<Sealed>] attribute.
- The F# compiler should raise an error if the [<Sealed>] attribute is applied to a non-overriding method or property (i.e., methods/properties that are not virtual at all as well as for definitions of virtual methods and properties, just like you can't use both the sealed and virtual keywords in C#).
Do you think that would be worth doing? Sure it's only a small change with very limited impact, but it would bring F# closer to feature parity with C# when it comes to object-oriented constructs. If you think it's worth implementing, I'll be happy to do it, although I have to admit that I've never modified the F# compiler before.
I'm looking forward to hearing your opinions on that suggestion!



## Response ##
** by fslang-admin on 2/5/2016 12:00:00 AM **

Thanks for the suggestion!
I’ve marked it declined per my comment. I’m not 100% opposed to the feature and appreciate it being noted. However I’ve given the explanation in the comment
That said, we may implement this feature one day as part of some overall “feature parity with C# implementation inheritance” work. But that day seems a fair way off for now.
Best wishes
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6108408)**


## Comments ##


#### Comment by Don Syme on 2/5/2016 6:25:00 AM ####
My inclination is not to implement this feature. I understand its utility, but we don't aim for 100% feature parity with C# OO. Specifically the F# emphasis is more to hide the implementation of object types rather than creating object inheritance hierarchies based on implementation inheritance. So we tend to strongly de-emphasize features related to supporting implementation inheritance as a technique - we allow basic implementation inheritance but not every bell-and-whistle of C#.

