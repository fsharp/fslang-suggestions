# Support partial record prototypes [12902226] #

**Submitted by Matthew Orlando on 3/11/2016 12:00:00 AM**  
**1 votes on UserVoice prior to migration**  

I have a case where I have several related types (categories of parameter sets for an analytics API). I want to create a set of new types such that every category is required in exactly one of the new types, and all of the other categories are optional.
This is fairly easy to express in a variety of ways in F#, but enforcement becomes difficult. I'd prefer to use record types with a default prototype, but there are no good defaults for the required parameters. I either have to clutter up my types with bona fide classes with constructors, or use a module with a create function (as seems common in cases like this).
So I propose something like the following:
type Foo = Foo of string
type Bar = Bar of int
type Baz = Baz of Guid
type Foo' = { Foo : Foo ; Bar : Bar option ; Baz : Baz option }
let defaultFoo' = { Bar = None; Baz = None } : Foo' partial
Alternatively, I'll accept any comments that help point out something I've missed in F#... I'm still only about knee deep in the waters around here.
Now that I think about it a bit more, I wonder if the way I used "partial" in my example can be implemented with reflection... Still, I think language support would give a better developer experience.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/12902226)**


## Comments ##

