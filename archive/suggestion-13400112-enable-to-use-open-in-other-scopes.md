# Enable to use open in other scopes [13400112] #

**Submitted by Gauthier Segay on 4/12/2016 12:00:00 AM**  
**29 votes on UserVoice prior to migration**  

It would be nice to be able to use open in function scope and maybe other places where it currently is illegal.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/13400112)**


## Comments ##


#### Comment by Richard Minerich on 4/12/2016 3:07:00 PM ####
I would love to be able to open modules in let scopes, this would be especially useful given the way that things like unchecked arithmetic is done in F#.


#### Comment by Alexei Odeychuk on 4/13/2016 1:17:00 AM ####
I eagerly support Gauthier and Richard


#### Comment by Loic Denuziere on 4/13/2016 3:20:00 AM ####
Agreed, this would be great. Just for context, here are the two syntaxes to do this in OCaml:
let open Module in xyz
Module.(xyz)


#### Comment by Alexei Odeychuk on 4/13/2016 9:07:00 AM ####
Loic, I think F# needs and deserves more simple and succinct syntax than that of OCaml; something like this:
let someWrapperFunction x =
(* .. indentation .. *) open ModuleName
(* .. indentation .. *) y(x) // instead of: ModuleName.y(x)
let x =
(* .... *) open ModuleName1
(* .... *) open ModuleName2
// instead of: ModuleName1.someConstant1 + ModuleName2.someConstant2
(* .... *) someConstant1 + someConstant2


#### Comment by Gauthier Segay on 4/13/2016 9:13:00 AM ####
agree with Alexei to have fsharp-y syntax (although I'm not familiar with OCaml, I'm sure there are advantages in the way they open modules), I should have put more details in the suggestion but can't edit it.
I'm also considering if having "partial" open (to bring only select symbols in scope) is something which would be valuable.


#### Comment by Alexei Odeychuk on 4/13/2016 4:17:00 PM ####
As to the partial open syntax.
Gauthier, I think it would be nice to use the open keyword not only to open entire modules, namespaces in the let scope, but also to introduce a member of another module or namespace (I mean a type or class and its fields, case identifiers, methods, properties) into the current let block in order to prevent ambiguity in code (if the same identifier is in two different modules and we have an open clause for both), obscurity (you can't find the declaration of an identifier) and possibly a maintenance headache (another module is added which duplicates some identifiers).
The partial open clause should have the effect that members, properties, fields, case identifiers of the type (class) specified are directly visible from the module, namespace specified within the current let block (of course, if access modifiers of such members, properties, fields etc. allow them to be visible in client code).
For example,
module Zoo =
(* .. *) type Animal =
(* ….... *) | Cat
(* ….... *) | Dog
(* ….... *) | Mouse
(* ….... *) | Hamster
(* ….... *) member this.Age = match this with Dog | Cat -> 2 | _ -> 1
(* ….... *) static member StaticAge (animal : Animal) = animal.Age
// another file and module: client code.
let myAnimalWithAge =
(* ... *) open Zoo.Animal // introduce the type specified from module Zoo into the let block
(* … *) let animal = Cat // instead of: let animal = Zoo.Animal.Cat
(* … *) let animal = Animal.Dog // intentional shadowing; Animal.Dog and Dog are equally legal
(* … *) let age = StaticAge animal // instead of: Zoo.Animal.StaticAge animal, or: Animal.StaticAge animal
(* … *) (animal, age) // return a tuple
Moreover, I believe that the partial open clause can be widely used not only in the let blocks (definitions of values, functions), but also in the bodies of members, properties of classes and types, in namespaces and modules.
The syntax suggested would be an equivalent to the using syntax in C++, and the use type, use all type syntax in Ada 2012.
I think the above-mentioned syntax would improve the convenience of writing F# code and boost the F# completive strengths.


#### Comment by Alexei Odeychuk on 4/20/2016 4:24:00 AM ####
I think it would be great to use the open keyword:
a) in implicit constructors and explicit constructors, in bodies of methods or properties of classes,
b) in branches of the if expressions (if, elif, else branches),
c) in branches of the match expressions,
d) in the do blocks,
e) in loop bodies
AS WELL in order:
a) to open entire modules, namespaces (please see an example of the syntax suggested in my message on April 13, 2016 5:07 PM), or
b) to introduce a member of another module or namespace, namely a type or class and its fields, case identifiers, methods, properties whose access modifiers allow them to be visible in client code (please see an example of the syntax suggested in my message on April 14, 2016 12:17 AM).
c) to refer to a single object or class, type, structure from the same module or namespace so that the expressions can use a simplified syntax when accessing members of the object or structure, class, type (like a With...End With statement in VB.NET), for example:
let customer = new Customer()
open customer
// beginning in VB.NET with: .Name
// I think the leading "." is unneeded in F#
Name <- "Coho Vineyard"
City <- "Redmond"
open customer.Comments
Add("First comment.") // .Add("First comment.") in VB.NET
Add("Second comment.")


#### Comment by Paul on 9/15/2016 7:53:00 AM ####
There is some historic work in this area with a POC implementation here /archive/suggestion-5690218-allow-open-in-local-declarations-like-in-standard
Implementation allowed
let x = 
(* .... *) open ModuleName1 
(* .... *) open ModuleName2 

