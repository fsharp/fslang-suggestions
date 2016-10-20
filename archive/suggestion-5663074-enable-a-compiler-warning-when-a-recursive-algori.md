# Enable a compiler-warning when a recursive algorithm is not tail-recursive [5663074] #

**Submitted by knocte on 3/21/2014 12:00:00 AM**  
**311 votes on UserVoice prior to migration**  

Add an TailRecursiveAttribute to enable a compiler-warning when a recursive algorithm is not tail-recursive. This should ideally also cover recursive seq { .. } and async { ... } expressions.



## Response ##
** by fslang-admin on 8/3/2015 12:00:00 AM **

I am generally in favour of addressing this in F# 4.x+. I would want seq { .. } and async { … } tailcalls to also be addressed.
A more detailed design is needed and some trialling would be great. Jack’s work is a great start. However, this is not an easy piece of work to do in a non-invasive way and my own experiments in this area have not yet led to something I feel confident to include in the F# language design.
An implementation and testing would need to be provided by someone in the F# community (possibly including Microsoft or Microsoft Research, though not limited to them).
Currently, initial implementations of approved language design can be submitted as pull requests to the appropriate branch of https://github.com/Microsoft/visualfsharp. See http://fsharp.github.io/2014/06/18/fsharp-contributions.html for info on how to contribute to the F# language/core library design
I encourage you to consider continue working towards a detailed proposal and a proposed implementation. I will gladly help.
Don Syme, F# Language and Core Library Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5663074)**


## Comments ##


#### Comment by Phillip Trelford on 3/21/2014 7:30:00 AM ####
A compiler warning/error would be useful when you require your function to be tail recursive but it is not, perhaps a tailrec keyword could be used in this case, i.e.
let tailrec myfunc = // ...


#### Comment by knocte on 3/21/2014 7:42:00 AM ####
@Phillip: as far as I understand, it's always desirable to be tail-call-friendly, otherwise you might get StackOverflowExceptions if there are many iterations, right?


#### Comment by Phillip Trelford on 3/21/2014 7:46:00 AM ####
@Anonymous it's desirable to be tail recursive but not always necessary, a blanket warning on all existing code might be a bit harsh. An attribute or keyword where you explicitly expect tail recursion might be more forgiving.


#### Comment by Andrew Khmylov on 3/21/2014 9:54:00 AM ####
Philip, introducing another `tailrec` keyword doesn't sound like a good idea. It would make the code a lot more verbose IMO. I would rather get rid of `rec` keyword at all. I think the compiler is smart enough to figure out that the function is actually recursive, why should I type it myself?


#### Comment by Jon Harrop on 3/21/2014 10:02:00 AM ####
@Andrew: "I think the compiler is smart enough"
Consider:
let f n = n+1
let f n = f(n-1)
is the latter definition of "f" recursive? Obviously it is impossible to tell. Hence the existence of the "rec" keyword.
The alternative is to make everything recursive but then you must pollute your namespaces with, for example, "f1" and "f2" because you cannot supercede previous definitions.


#### Comment by Jon Harrop on 3/21/2014 10:05:00 AM ####
How would we handle mutual recursion or recursion via a function that was passed in?
For example:
let rec even n =
odd(n-1)
and odd n =
even(n-1)
or:
let evenOne odd n = odd(n-1)
let oddOne even n = even(n-1)
let rec even n = evenOne (oddOne even) n
Could we put this attribute on an entire module to check that all loops within the module require bounded stack space?


#### Comment by knocte on 3/21/2014 2:56:00 PM ####
@Philip, aha I understand. But I think if such keyword is proposed, I think it would be better if it's for opting-out the warning than opting-in.


#### Comment by Mastr Mastic on 3/23/2014 2:46:00 AM ####
@Andrew Khmylov I cannot agree because imo `rec` is not for the compiler, it is for us, and to me very necessary.
For instance when you re-bind a symbol for a function, to a function that uses it, how would you express yourself without using `rec` if you intend to call the previous binding or the new (recursive) one?


#### Comment by Mastr Mastic on 3/23/2014 2:50:00 AM ####
I agree with Philip on the keyword, it seems much more cleaner than an attribute.


#### Comment by Jack Pappas on 3/29/2014 9:14:00 AM ####
Requiring the compiler to warn you when an entire algorithm is not tail-recursive poses a significant challenge, as Jon and others have pointed out.
If you relax the definition of this feature request to something like "emit a compiler warning for non-tail-recursive call sites within a 'rec' function", this becomes fairly simple to implement. In addition, you don't need additional keywords or functions to implement this -- it could be a standard compiler warning which is on by default, which means it'd be easy to turn off for those who wanted to do so.


#### Comment by Jack Pappas on 3/29/2014 2:07:00 PM ####
I put together a little code sample demonstrating my proposal (see previous comment): https://gist.github.com/jack-pappas/9860949
To elaborate a bit: the compiler would emit a warning at each call site to a function which shares the same stack frame as the current function -- in other words, when a function is calling itself, or some other function within a group of mutually-recursive functions.


#### Comment by knocte on 4/3/2014 3:45:00 PM ####
@Jack: awesome work!


#### Comment by bleis-tift on 4/3/2014 11:42:00 PM ####
F# has tailcall keyword as reserved-ident-keyword.
So I think that the keyword is better than tailrec.


#### Comment by Don Syme on 6/20/2014 12:18:00 PM ####
I am generally in favour of addressing this in F# 4.0. I would want seq { .. } and async { ... } tailcalls to also be addressed.
A more detailed design is needed and some trialling would be great. Jack's work is a great start.
An implementation and testing would need to be provided by someone in the F# community (possibly including Microsoft or Microsoft Research, though not limited to them).Currently, initial implementations of approved language design can be submitted as pull requests to the "fsharp4" branch of https://visualfsharp.codeplex.com/SourceControl/latest.
I encourage you to consider continue working towards a detailed proposal and a propopsed implementation. I will gladly help.

I would tend towards using an attribute rather than a keyword, despite the fact that "tailcall" is reserved, simply because that is how things like this are generally added to the F# language since F# 2.0.
[<TailCall>]
let rec f x = .... f (x-1)
[<TailCall>]
let rec f x = .seq { ... yield! f (x-1) }
[<TailCall>]
let rec g x = .async { ... return g (x-1) }
With regard to Jon's question - the checking would be much as described by Jack - i.e. only w.r.t. the control flow contructs that are syntactically present in the F# expression language (and hot combinator encodings of these).
All uses of an attributed function within its recursive scope would need to be in tail position. Thus passing the function as a higher-order argument would not be allowed.
This limts the utility of the method of course but it still remains useful, especially for beginners and teaching purposes.


#### Comment by Eriawan Kusumawardhono on 9/2/2014 10:29:00 PM ####
This tailcall CLR and recursive implementation should be transparent to the language, especially F#.
Meaning that not only adding keywords or IDE realtime warning, but also should be available in other languages other than F# as well to use if there's a need to optimize recursive function calls.
I vote +2 for this!


#### Comment by Alfonso Garcia-Caro on 9/7/2014 8:30:00 AM ####
I would be in favour of using the keyword, the attribute looks much more verbose...


#### Comment by Eriawan Kusumawardhono on 9/25/2014 11:16:00 PM ####
I agree to use the attribute. This will give different meaning and also context is more verbose than keyword.
This will also minimize confusion whether a rec function is actually tailcall optimized or not.


#### Comment by James Hugard on 11/6/2014 2:09:00 AM ####
I'm in agreement with Jack Pappas: use neither a keyword nor attribute; simply always issue a warning. In other words, relax the feature request to be:
"F# compiler emits a warning at each non-tail recursive call site where a function is calling itself or some other function defined within a group of mutually-recursive functions."
It is obviously bad practice, in general, to make non-tail calls to oneself or one's siblings due to the potential of a stack overflow. Therefore, such usage should be strongly discouraged by default and not only when a specific keyword modifier or attribute is supplied. Doubly so because beginners are more likely to make mistakes here and not even know to use a modifier or attribute as a compiler assist.
For cases where one accepts the risks, the warning could easily be disabled.
The documentation for that warning, though, would probably run to the long side; e.g., explaining how one could make the code tailcall friendly.


#### Comment by Don Syme on 11/6/2014 7:05:00 PM ####
James/Jack, there are many cases where non-tail recursive calls are required and normal, for example consider Map.add https://github.com/fsharp/fsharp/blob/master/src/fsharp/FSharp.Core/map.fs#L120
In this case the depth of recursion is bounded by log(n) on the size of the input.


#### Comment by Don Syme on 11/11/2014 1:22:00 PM ####
I have started prototyping this, https://visualfsharp.codeplex.com/SourceControl/network/forks/dsyme/cleanup?branch=tailcall-warning


#### Comment by exercitus vir on 6/19/2015 5:53:00 PM ####
I second the the idea of always issuing a warning. You can always disable it with an in-place compiler directive if you really don't require tail-recursion.


#### Comment by Anonymous on 5/10/2016 4:32:00 PM ####
It is really "#1 must be" all this recursive stuff got failed on a big data if not optimized, but some times it is nontrivial to check is it ok or not.

