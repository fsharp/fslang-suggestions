# Support for type classes or implicits [5762135] #

**Submitted by exercitus vir on 4/12/2014 12:00:00 AM**  
**392 votes on UserVoice prior to migration**  

(Updated the suggestion to "type classes or implicits", and edited it)
Please add support for type classes or implicits.
Currently, it's possible to hack type classes into F# using statically resolved type parameters and operators, but it is really ugly and not easily extensible.
I'd like to see something similar to an interface declaration:
class Mappable =
abstract map : ('a -> 'b) -> 'm<'a> -> 'm<'b>
Existing types could then be made instances of a type classes by writing them as type extensions:
type Seq with
class Mappable with
member map = Seq.map
type Option with
class Mappable with
member map = Option.map
I know that the 'class' keyword could be confusing for OO-folks but I could not come up with a better keyword for a type class but since 'class' is not used in F# anyway, this is probably less of a problem.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5762135)**


## Comments ##


#### Comment by Will Smith on 4/13/2014 1:13:00 PM ####
I wouldn't say it's currently a hack; it's just how it's done. But, I think something like this would have potential if we can figure out what the actual benefits are and how do to design it in a way without confusing anyone.
More info: http://www.infoq.com/interviews/F-Sharp-Don-Syme
Number 6 shows Don talking about type classes.


#### Comment by exercitus vir on 4/15/2014 6:35:00 AM ####
Currently, it's definitely a hack. It's not extensible, you need to overload unused operators and F# Interactive has problems with scripts that depend on type classes (requires a restart of the session each time its run). Check this for more information on hacking type classes in F#: http://www.nut-cracker.com.ar/index.php/typeclasses-for-fsharp


#### Comment by Will Smith on 4/15/2014 4:07:00 PM ####
Really good post about it. Thanks for the link.
It definitely feels like a hack if you try to make it behave exactly like Haskell.


#### Comment by Daniel Fabian on 4/18/2014 3:10:00 AM ####
Whilst, I would love to see this, I think for it be actually useful, we need higher-kinded polymorphism. As it stands now, even if you were able to define type classes, your Mappable would not compile, because 'm<'a> cannot be expressed with the .net type system.
The technique to simulate type classes has actually evolved somewhat and is _slightly_ less hacky now. E.g. you no longer need a special operator, etc. https://github.com/gmpl/FsControl


#### Comment by Gusty on 5/13/2014 4:43:00 AM ####
"...It's not extensible" It is extensible, just orphan instances are not supported.
"...you need to overload unused operators" this was due to a bug in F# parser, since the introduction of F# 3.0 this is not longer required.
Regarding the script issue, I really don't get it, could you possible open an issue in https://github.com/gmpl/FsControl/issues describing this problem?
I personally think F# can add Typeclass support requiring inline functions instead of support at the CLR Level. The same applies to Higher Kinds.
So the argument "this is a suggestion for the CLR team" is not valid, at least that's not what I'm suggesting.
To avoid the problem Don Syme mentions in the video, just keep ignoring extensions methods in overload resolution and create a "prelude" for existing types (that's the goal of FsControl).


#### Comment by exercitus vir on 6/23/2014 10:30:00 AM ####
Daniel and Gusty,
I was not talking about FsControl and I have not tried FsControl. The script issue occurs when you use the solution presented in http://www.nut-cracker.com.ar/index.php/typeclasses-for-fsharp
I personally do not care about support at the CLR level. It would already be great if it was an F#-only solution like units of measure and statically resolved type parameters.


#### Comment by Craig Stuntz on 6/25/2014 12:32:00 PM ####
One possible keyword might be
type class Mappable = ...
That reads well and doesn't introduce any new reserved words. It does introduce ambiguity into the grammar, though.


#### Comment by Don Syme on 9/7/2014 6:22:00 AM ####
I'd like to point people to the two talks about implicits at the ML workshop to get a feeling for implicits and type classes in a mixed OO/FP language, or in an ML-class language.
Any design for implicits in F# would differ substantially from these though.
http://www.youtube.com/watch?v=3wVUXTd4WNc
http://www.youtube.com/watch?v=--mrQSd6eas


#### Comment by David Ellis on 10/27/2014 4:13:00 PM ####
I think this is the biggest missing piece to F#. F# needs some kind of support for ad-hoc polymorphism. Haskell has type classes and clojure has protocols. F# needs type classes. If I could use all my votes on this, I would.


#### Comment by exercitus vir on 11/7/2014 5:50:00 AM ####
I was not asking for implicits originally because I am not a big fan of implicits. Implicits can be abused to make code less type safe (e.g. converting floats to ints). They also feel hacky to me if you only want is type classes. Adapting types (implicits in Skala) is also less efficient that calling the functions directly (type classes in Haskell).
I would prefer pure type classes and you could leverage the member constraints implementation of F# for a clean implementation of type classes in F#.


#### Comment by Gusty on 11/19/2014 4:26:00 PM ####
I know you were not talking about FsControl (http://github.com/gmpl/FsControl) but in the post you mentioned (now moved to http://nut-cracker.azurewebsites.net/typeclasses-for-fsharp) I described a technique which inspired me later to develop FsControl, which runs in F# 3.0 so you don't need to use operators at all. Support for this technique (or similar) at the language level (not CLR) will be nice.


#### Comment by Radek Micek on 6/7/2015 5:47:00 AM ####
What about implementation similar to type providers? For each parameter annotated with [<Witness>] attribute where the argument is not given explicitly in the code the compiler would call all witness providers in the scope to generate the argument. If only single witness is generated then this witness becomes the argument otherwise it's an error.
Additionally if there is a single value in the scope which can be used as the argument then it is used as the argument and witness providers are not used.


#### Comment by Kurt on 7/6/2015 2:58:00 AM ####
I haven't given this any votes because what I've missed is some sort of retro-active interface implementation, like is possible with protocols in Clojure and recently swift. So I voted for this one instead:
/archive/suggestion-5665042-allow-extension-interfaces
because it is more focused.
Typeclasses solve that problem but protocols seems to me like a solution that is closer to the existing design space of F# (i.e. a functional first language with OO concepts like subtyping). Typeclasses have many extensions - functional dependencies, overlapping instances, etc that are essentially research problems. What happens if you use two libraries that each instantiate the same typeclass for the same type in a different way? And how do typeclasses work with subtyping?
Finally proposing an idea for A or B (even if A and B are related) draws votes away from more focused suggestions. (e.g. this suggestion has something for everyone so it's not clear what I'm voting for here. Even the original poster commented they don't really want implicits...)


#### Comment by Radek Micek on 10/19/2015 4:15:00 PM ####
> What happens if you use two libraries that each instantiate the same typeclass for the same type in a different way?
@Kurt Doesn't this problem exist with protocols too? What should happen when two different assemblies implement the same protocol for the same type in a different way?
AFAIK in Haskell this leads to failure when linking. In Scala this is resolved by scoping rules for implicits (which is IMO better than Haskell).
> And how do typeclasses work with subtyping?
This could be derived from implicits.


#### Comment by Don Syme on 2/3/2016 1:45:00 PM ####
See also
/archive/suggestion-8509687-add-constraints-as-a-language-construct
/archive/suggestion-8393964-interfaces-as-simple-reusable-and-named-sets-of-m
/archive/suggestion-6343928-allow-naming-of-member-constraints
These various features tug in different incompatible directions.


#### Comment by bleis-tift on 3/2/2016 6:18:00 PM ####
OCaml way: http://www.lpw25.net/ml2014.pdf

