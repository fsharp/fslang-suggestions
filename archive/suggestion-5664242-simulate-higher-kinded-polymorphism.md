# Simulate higher-kinded polymorphism [5664242] #

**Submitted by Daniel Fabian on 3/21/2014 12:00:00 AM**  
**492 votes on UserVoice prior to migration**  

F# already has to make trade-offs when doing interop, e.g. it is possible to create a null value for a DU from C#, erased type providers don't work from anywhere but F# etc. Maybe F# could allow for higher-kinded polymorphism within F# code and use dynamic casts at runtime or maybe statically resolved inlining to simulate higher-kinded polymorphism.



## Response ##
** by fslang-admin on 3/21/2014 12:00:00 AM **

removed “until the CLR fully supports it” from title


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5664242)**


## Comments ##


#### Comment by Don Syme on 3/21/2014 12:38:00 PM ####
I think "until the CLR finally supports it" should be deleted from the title. To my knowledge there is no prospect of the CLR supporting HK polymorphism in any timeframe that matters for the purposes of this discussion.


#### Comment by Lev Gorodinski on 3/24/2014 8:23:00 AM ####
This would be very useful for higher-order functional programming, along with, to a lesser extent, something like either Scala implicits or Haskell type classes. This can be a slipper slope though - should higher-kinded currying also be supported (aka partially applied type parameters)? If not part of the type system at the core, should F# resort to Scala type lambdas?


#### Comment by Mauricio Scheffer on 3/24/2014 9:24:00 PM ####
The best simulation of higher kinds I know is the technique explained in http://www.nut-cracker.com.ar/ . Work on this ended up in two libraries: FsControl ( https://github.com/gmpl/FsControl ) and FSharpPlus ( https://github.com/gmpl/FSharpPlus ), which builds on FsControl.
It's not perfect by any means (I need to finish a series of posts about it), but I'm already using it in production, and it works just fine (at least the parts I'm using).
Of course, it would be much better if F# had explicit support for this.


#### Comment by Hodza Nassredin on 6/27/2014 12:28:00 AM ####
We can emulate some restricted form of Higher-Rank Polymorphism in c# for single inheritance pattern. For example function with forall https://gist.github.com/hodzanassredin/4de8fc7bbfbf4bb7dfa7 more details and monad and monad transformers are here http://hodzanassredin.github.io/2014/06/21/yet-another-monad-guide.html


#### Comment by Hodza Nassredin on 6/27/2014 3:11:00 AM ####
Added some example how we can automatically translate code like this into c#:
public static List<A> Wrap(Func<A, List<A>> f, A val) forall A{
where A : IConstraint
return f(val);
}
https://gist.github.com/hodzanassredin/eb0aa76f48e37cbcc87f


#### Comment by John Azariah on 9/7/2014 7:37:00 AM ####
1) Even without higher-kinded currying, being able to abstract over Monads and Functors without losing type inference would be pretty helpful. Doing that kind of thing in Scala is pretty painful.
2) I'm not sure we need to include Scala-style implicits! I find them a way to reduce the transparency of the code and severely affect the ability to comprehend the code - although it may simply be my naivete!


#### Comment by Anonymous on 11/13/2014 1:04:00 AM ####
Since .Net is open-sourced, and they are open to PR, let us all push this request to https://github.com/dotnet/corefx and make this the most important feature for F# be realized.


#### Comment by Phylos on 1/6/2015 11:32:00 PM ####
In a recent Reddit post related to F# adoption, I saw a great comment from "TarMil" on higher kinds that I believe is worth repeating to illustrate their usefulness. Here is that comment in full ...
"Basically higher kinds are a type system for types: just like a value has a type, a type has a kind. And just like a function can take other values as arguments, a type variable can take other types as parameters. So where in F# you can have a parameterized type T<'a>, in Haskell the T part itself can be a type variable.
For an example of the usefulness, see how in F# we have a whole bunch of similar functions:
List.map : ('a -> 'b) -> list<'a> -> list<'b>
Array.map : ('a -> 'b) -> array<'a> -> array<'b>
Seq.map : ('a -> 'b) -> seq<'a> -> seq<'b>
Option.map : ('a -> 'b) -> option<'a> -> option<'b>
Event.map : ('a -> 'b) -> Event<'a> -> Event<'b>
// Not in the standard library, but easy to implement:
Async.map : ('a -> 'b) -> Async<'a> -> Async<'b>
// etc.
In Haskell, you can have a single function fmap, whose type (with an F#-like syntax) would be:
fmap : ('a -> 'b) -> 'T<'a> -> 'T<'b>
where (again in a hypothetic F#-like syntax):
'T : Type -> Type
// 'T takes a type as parameter and returns a type
and this function has different implementations for different 'Ts. You can then use this function to write your own functions that can be called on any "mappable" type, and will do the right thing according to the type of the value passed.
(I gave the example in Haskell because the way to do this in OCaml is more convoluted.)"


#### Comment by Greg Rosenbaum on 3/14/2015 5:57:00 PM ####
This can only be practically implemented using statically resolved inlining (or reflection) because of constraints in the IL type system (this is where reified generics bites you in the ass!). Here is what an fmap function (as described by phylos) might look like:
https://gist.github.com/Springwight/0368e8e7d7aec8b77e68
I really don't see it as a technical challenge though, considering how much effort has already gone into the inlining system. It's more like, "do we need to see this in the language?" It's something that's very unlikely to be used by anyone except library developers, but it will help those library developers a lot.


#### Comment by exercitus vir on 6/18/2015 2:43:00 PM ####
Any comment from Don Syme or the F# Software Foundation Language Group on the chances of simulating higher-kinded polymorphism in the near future?
I think this is a really important feature. Many expert functional programmers forego F# because they think can't take a language serious that does not have it. The F# community is losing a lot of potential expert functional programmers do to this.


#### Comment by Suminda Sirinath Salpitikorala Dharmasena on 7/13/2015 9:00:00 AM ####
Also a feature request with this many votes should not be ignored. Otherwise why go through all this Uservoice exercise.


#### Comment by Alexander Sidorenko on 8/3/2015 5:44:00 AM ####
CoreCLR is open-sourced, someday someone will do PL which adds HKT to CLR :) we just need to wait or do it yourself :)


#### Comment by George on 3/1/2016 12:00:00 PM ####
This may do the trick...
https://github.com/gmpl/FsControl


#### Comment by Tobias Burger on 4/12/2016 4:02:00 AM ####
For reference here is the discussion of HKP in the roslyn issue tracker: https://github.com/dotnet/roslyn/issues/2212


#### Comment by exercitus vir on 7/9/2016 9:47:00 AM ####
I just want to repeat my question from about one year ago, because I would really appreciate some comments (concerns, feasibility, effort) from the F# team on this:
"Any comment from Don Syme or the F# Software Foundation Language Group on the chances of simulating higher-kinded polymorphism in the near future?
I think this is a really important feature. Many expert functional programmers forego F# because they think can't take a language serious that does not have it. The F# community is losing a lot of potential expert functional programmers [because of this]."
This issue being more than 2 years old requires some kind of official response. Either decline it or approve it in principle, but not answering just keeps our hopes up and keeps our votes from being used for other feature requests.


#### Comment by Alexei Odeychuk on 10/18/2016 10:29:00 AM ####
I support exercitus vir. This issue really requires some kind of official response. Either decline it (and explain why) or approve it in principle, but not answering just keeps our votes from being used for other valuable suggestions.

