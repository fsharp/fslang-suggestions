# Provide better support for structural typing [6181848] #

**Submitted by Isaac Abraham on 7/16/2014 12:00:00 AM**  
**17 votes on UserVoice prior to migration**  

In F#3 you can declare a function which can operate on e.g. records which has no relation aside from the fact that they share e.g. field name + type. This can occasionally be useful - however, the syntax for achieving this is somewhat awkward e.g. http://codebetter.com/matthewpodwysocki/2009/06/11/f-duck-typing-and-structural-typing/
If there were a more succinct way to achieve this, it could be a very powerful feature e.g.
decorating a function with [<StructuralTyping>] to automatically indicate to the compiler to infer the implicit structure of the type, or at least simplifying the syntax to not have to mess around with "'a member" etc..



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6181848)**


## Comments ##


#### Comment by trek42 on 8/27/2014 12:35:00 PM ####
structural typing is in general very useful, and can avoid using the OO-style inheritance in many places.
Would be nice if F# supports typeclass, and implements this particular type of structural typing in the framework of typeclass. Something like:
typeclass ClassName = { property_name: type; ... }
and every record type that has all the listed fields automatically becomes an instance of the typeclass.


#### Comment by Richard Gibson on 9/12/2014 5:47:00 AM ####
I really like the way Typescript does this. You can either use an interface (the object in question does not have to explicitly implement the interface to satisfy it, although it can) or you can declare the 'shape' of the object inline. Such as:
class Person
{
constructor(public name : string)
{}
}
var sayHello = function (named : { name : string })
{
return "Hello " + named.name;
}
sayHello(new Person("John"));


#### Comment by Tobias Burger on 12/12/2014 8:46:00 AM ####
Would be cool to have a structural type syntax like in TypeScript. Especially for interop scenarios, where often a type/class is needed for binding.
type PersonController() =
inherit ApiController()
member __.GetGreeting(person: { name: string; age: int }) =
sprintf "hello %s, you are %i years old" person.name person.age


#### Comment by Don Syme on 2/5/2016 6:20:00 AM ####
Strucutral subtyping is hard to implement within the constraints of the .NET type system. Any implementation would effectively have to erase to property bags at compile time. See the discussion here for example: /archive/suggestion-9633858-structural-extensible-records-like-elm-concrete. This representation would also not work particularly well with .NET reflection.
How bad is this? Well, for normal F# use it is quite bad. But for lower-performance information-representation scenarios it may not too bad.
I'll leave this open as a general placeholder for votes on "better structural subtyping"


#### Comment by Isaac Abraham on 8/12/2016 7:05:00 AM ####
Don - I'm not really sure if I'm thinking along the same lines here - I'm thinking for just syntactic sugar for either the duck-typing support that already exists in F#. I don't even know how this works internally (is the structural constraint erased at runtime? what's the signature of the method at runtime?).
This could even be something that was erased away at compile-time and resorted to something less than that at runtime (in a similar way to units of measure?). I don't know :-)

