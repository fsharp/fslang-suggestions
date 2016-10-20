# Remove fun keyword from lambda expressions [5663774] #

**Submitted by Jorge Fioranelli on 3/21/2014 12:00:00 AM**  
**271 votes on UserVoice prior to migration**  

Maybe make it optional?
Otherwise it is more verbose than C#.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5663774)**


## Comments ##


#### Comment by Vasily Kirichenko on 4/4/2014 1:39:00 AM ####
I personally like the current syntax.


#### Comment by Mastr Mastic on 4/9/2014 4:07:00 AM ####
Should be optional, not removed (otherwise code will break).
And I'm all for it.
It happens to me countless of times that I forget it because my mind just always expects better.


#### Comment by Brian on 7/6/2014 8:47:00 AM ####
Seems like it would complicate the language a lot to make it optional. If we were starting from scratch though I'd support it. I would like to hear about what the reasoning behind requiring "fun" for lambda's. Was it simply because it was in OCAML? or was there other technical reasons?


#### Comment by Tahir Hassan on 7/25/2014 5:59:00 AM ####
I agree, it looks horrible. C# has a much better lambda syntax, imho.
Potentially we could use Haskell's backslash:
[1;2;3] |> Seq.map (\x -> x * x)
Although it ain't as perfect like C#'s, it would work without making the language ambiguous.


#### Comment by Michael on 9/7/2014 6:34:00 PM ####
I really like the fun keyword.


#### Comment by Grant Crofton on 2/14/2015 12:09:00 PM ####
Would certainly improve our code golf scores a little! :-)


#### Comment by Filip Kopecký on 6/20/2015 5:49:00 PM ####
I think it would be nice if we could write anonymous functions like expressions. The compiler could tell it is a function based on undeclared variables being used.
(fun x y -> x + y)
(x + y)


#### Comment by Андрей Чебукин on 7/19/2015 6:33:00 PM ####
I agree that it is too long and actually moving to C# syntax would be reasonable.
However current syntax allows to introduce a snippet for lambda that looks natural
Type fun, press tab (or just space in case of CodeRush) and fun is almost ready for you.


#### Comment by Andreas Vilinski on 8/6/2015 12:45:00 AM ####
You wanna take the fun out of F#!
It is not always needed. Often you can write ((+) y) instead of (fun x -> x + y). For other cases I have a R# live template expansion, which just adds me an arrow and braces, defined like here:
fsfun ==> (fun x -> $END$)
However it would be nice to map list of pairs like in Scala: List.map (_ + _)


#### Comment by Anonymous on 1/16/2016 1:29:00 AM ####
I think we should preserve the fun keyword to be backward compatible, however
I really like the Elixir shorthand lambda expressions:
1..100_000 |> Enum.map(&(&1 * 3)) |> Enum.filter(odd?) |> Enum.sum
You can for example make
fun x y z -> x + y + z
into
&(&1 + &2 + &3)
it is not that much shorter, but it frees the programmer from thinking about what to name all those pesky variables.. just like the pipeline frees the programmer from making up a lot of variable names...


#### Comment by Maciej J. Bańkowski on 1/17/2016 9:42:00 AM ####
to some Anonymous: variable names are important
if you are lazy enough to name variables $1 $2 $3 then just name them a b c - it is even shorter.
Besides, names do matter for maintainability. 2-3 months from now, nobody will know what the original programmer indented to do - names help.
On topic: It would be so cool to get rid of the 'fun' keyword and make lambdas as sexy as those in C#. However, I doubt it is possible due to statement evaluation logic of F# and ambiguity that would arise without some arbitrary discriminator for lambda expression.
In C# lambdas are clear from the context and I am not sure F# context is rich enough to get by without the 'fun' keyword but maybe it is - would be awesome.


#### Comment by Will Smith on 2/11/2016 6:46:00 PM ####
I like what we currently have. It isn't that much more verbose than C#. In a way, it seems easier to spot out lambdas in a codebase when you see 'fun'.


#### Comment by Ideaflare on 4/11/2016 2:40:00 PM ####
I agree with Mastr Mastic, instead of removing it to make it optional.
Something else that could also be made optional is the let keyword.


#### Comment by Alan Ball on 8/8/2016 9:21:00 AM ####
In response to those who enjoy typing fun, and seeing fun, I do not think the language maintainers would break existing code. The reasonable way to interpret the requirement is to interpret it as optional. I personally think this might be nice. I'm sure there is a clean way to make this work. I would personally prefer the => syntax if possible, simply because many many languages currently use that, including C#.


#### Comment by Mohsin Syed on 9/15/2016 2:48:00 PM ####
looks verbose. Removing would make lambda looks cleaner.


#### Comment by Anonymous on 9/27/2016 10:02:00 PM ####
I think the optional use of the fun keyword would be the way to go as well. Just like in React in ES6 the function keyword is no longer necessary

