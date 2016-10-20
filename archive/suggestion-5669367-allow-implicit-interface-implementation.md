# Allow Implicit Interface Implementation [5669367] #

**Submitted by Mastr Mastic on 3/23/2014 12:00:00 AM**  
**133 votes on UserVoice prior to migration**  

F# only supports explicit interface implementation with the price of unnecessary and excessive casting (also causes readability issues), potential confusion when working with other languages, and causes limitation with F#'s OOP that could be resolved without any major language change.
To expand on this, this post by Mauricio Scheffer describes the issue very well: http://bugsquash.blogspot.co.il/2009/01/implementing-interfaces-in-f.html
In addition, I'm sure I could argue that people would prefer to just write `identifier.Member` rather than `(identifier :> Type).Member` whenever the member is a signature provided by an interface.
This repeats quite a bit on average and it is messy, to say the least.
It should also be pointed out that even though F# is primarily functional (and interfaces are less of an issue), F# code is still being used from other languages, and also some domains and tasks could be easier to take on from an OO approach.
(I am also finding very high limitations with using WPF & XAML with some MVVM approaches)
Currently the workaround would be to copy-paste the signatures for every member of an interface.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5669367)**


## Comments ##


#### Comment by Jack Pappas on 3/23/2014 7:45:00 AM ####
I personally prefer the requirement for explicit interface implementation and would like to continue to enforce that requirement in my own codebase, so if this feature were implemented I would like to have a compiler option to disable it (or perhaps, it should be disabled by default and activated by a compiler flag).


#### Comment by Mastr Mastic on 3/23/2014 8:20:00 AM ####
I'd like to expand a bit further on what I've mentioned about WPF and MVVM.
This issue makes F# not reliable for your view-models because other than being cumbersome and tedious (`{Binding Property}` becomes {`Binding Path=(namespace:InterfaceType.Property)}` for each property.
(You have to type `Path=` to avoid an exception)) it also introduces limitations.
For instance, one limitation that shows up frequently is that WPF DataTemplates do not support interfaces, yet passing an interface is your only way to expose your members because they are explicit.
(See: http://stackoverflow.com/a/327993/825637)


#### Comment by Mastr Mastic on 3/23/2014 11:17:00 AM ####
@Jack Pappas No worries there I think, this pretty much has to stay as default for the language so not to break existing-code (which I'm sure is one primary concern for the F# team).
I do like the idea of the compiler flag very much and also I think attributes, keywords, or different syntax would be required to get more specific from one instance to another within the same compilation.
Thanks for your input.


#### Comment by Jack Pappas on 3/23/2014 11:44:00 AM ####
@Mastr Mastic Admittedly, I do very little GUI programming, so I haven't run into the situation you described. The additional explanation you added makes a lot of sense, and I think you've made some good arguments for why this feature *should* be implemented. This would be a big change to the language though, and might also pose some challenges w.r.t. to type inference, so the more examples you can provide where the current behavior (explicit interface implementations only) is holding you back, the better.


#### Comment by Reed Copsey, Jr. on 8/4/2014 7:30:00 PM ####
I'd very much like this - and have run into this issue with WPF myself.
My preference would to allow this via an attribute like many other features - something like:
interface [<ImplicitInterface>] ISomeInterface with
member __.Foo = 42
This would align with how [<AbstractClass>] and similar are handled.


#### Comment by Paul on 9/9/2014 5:38:00 PM ####
I personally prefer the requirement for explicit interface implementation. But if you’re using WPF and not providing a proxy to allow WPF to access to a chosen interface an attribute like CLIMutableAttribute would be better. This would cause the decorated interface to additionally be compiled to Common Language Infrastructure (CLI) representation implicitly (but not exposed to f# code), allowing WPF binding to work. CLIMutableAttribute was added to F# 3.0 and adding this related attribute (called something like CLIImplicitInterface) to F# 4.0 would be a great addition, which would ease GUI development with F#.
http://msdn.microsoft.com/en-us/library/hh289724(v=VS.110).aspx
http://blogs.msdn.com/b/fsharpteam/archive/2012/07/19/more-about-fsharp-3.0-language-features.aspx
interface [<CLIImplicitInterface>] ISomeInterface with
member __.Foo = 42


#### Comment by Saagar Ahluwalia on 6/15/2015 5:36:00 PM ####
This is not much of an issue as any methods one needs to expose implicitly can just be redefined outside.


#### Comment by Kasey Speakman on 9/11/2015 11:28:00 AM ####
@Saagar Ahluwalia. This is a large issue, depending on your use. Try creating a class which implements IDictionary<'k,'v>. Maintaining ~15 alias methods on the base class is an issue.
I ran into this when creating a circular dictionary. Things I've tried:
- Inherit Dictionary<'k,'v>. Problem: existing functions like Add and Remove can't be overridden, and using them will circumvent the circular buffer. (You can hide them, but there's no "new" keyword in F# to suppress the compiler warning.)
- Implement IDictionary<'k,'v>. Problem: when you new up the class, none of the IDictionary methods are there. It's plain weird/unexpected to new up the class and immediately cast it to IDictionary. A static method could be created to do this for the user, but that suffers the same lack of obvious usage.
- Create alias methods on the class which do the interface cast for the user. Problem: this introduces a lot of superfluous alias methods (15ish for IDictionary) which must be maintained (and tested depending on the strictness of your testing policy).
All of these alternatives are bad.


#### Comment by Alexander Batishchev on 10/4/2015 12:31:00 AM ####
This is a HUGE ISSUE. The worst thing about F#. Clearly indicates its immaturity.


#### Comment by Anonymous on 1/16/2016 7:46:00 AM ####
Pls allow to use implicit interfaces. It is pain when creating an AST model and working with it.

