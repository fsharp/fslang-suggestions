# Allow extension interfaces [5665042] #

**Submitted by Ryan Riley on 3/21/2014 12:00:00 AM**  
**92 votes on UserVoice prior to migration**  

Rather than just supporting single methods or properties, provide a mechanism by which to implement interfaces on existing types. This could be similar to protocols in Clojure and Elixir.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5665042)**


## Comments ##


#### Comment by Richard Minerich on 3/21/2014 4:54:00 PM ####
If only I had more votes to give. This would be interop between various libraries a million times better.


#### Comment by Jack Pappas on 3/22/2014 9:08:00 AM ####
This is an interesting idea, and I can think of some times in the past where it would have been useful.
I could be mistaken, but after thinking it over a bit, it seems like this could only work for non-sealed classes; trying to extend sealed classes or value types would lead to issues when interoperating with non-F# code. Extending base classes or interfaces seems possible but very tricky to get right. For example, if you extended a base class which has some derived types, the F# compiler would have to create backing classes (in the compiled assembly) for the base class and any of the derived classes you used in your F# code, just to make sure the 'derives-from' and 'implements' relationships still hold correctly from the POV of any outside code.


#### Comment by Daniel Fabian on 3/22/2014 12:47:00 PM ####
In all fairness, don't object expressions already face pretty similar problems? This could be some sort of automatic implementation of object expressions using delegation.


#### Comment by Daniel Fabian on 3/23/2014 3:40:00 AM ####
I was thinking more about it a little more and I think, it could be done with some special object expression syntax. Something like
let myObj = MyClass() // does not implement the interface
let myAdoptedObj = { new IMyInterface on myObj } // if MyClass already has all the functions needed for the interface
let myAdoptedObj2 = { new IMyInterface on myObj with member x.MyAdditionalMemberOnlyPresentInTheInterface() = () } // if MyClass maybe implements half of the interface and we would like to add the second half. It is possible to use the existing object's methods as a default, but we can provide custom implementations for methods, that are missing or we can hide / override present methods on the object.
And because type inference probably would work (it works for object expressions for the generic argument at least), one might introduce a function
let adopt x = { new _ on x }
let result = adopt myObj |> funcThatWantsMyInterface
in this hypothetical syntax, { new IMyInterface on myObj } is a short-hand for
{ new IMyInterface with member x.method1 = myObj.method1; member x.method2 = myObj.method2 }
not unlike the record copy syntax.


#### Comment by Jack Pappas on 3/23/2014 12:07:00 PM ####
Daniel -- no, object expressions don't face the same problems, because they're only required to implement the interface. The problems with these proposed extension interfaces is that they need to have a type which matches both the class being extended and the interface(s) being added. This is the reason it's impossible for this to work with sealed classes and value types, or unsealed classes which have internal/protected constructors.
The only way I can think for this to work (unless I've misinterpreted Ryan's intentions) is that by extending existing types with these new interfaces, you'd basically just be making a shortcut for using object expressions somewhere else in your code. In other words, the compiler would not actually create a new type derived from the type being extended and the interfaces, but would in fact create a static method (in some module) which takes an instance of the type being extended and internally uses an object expression to produce an instance of the interface which was "added" to the type. It would then need to insert a call to this method into any call sites where instances of the interface were expected and you'd passed an instance of the type being extended.


#### Comment by Daniel Fabian on 3/23/2014 12:28:00 PM ####
Maybe I misunderstand the use-case here then. I thought the issue is, that you have a type that would be structurally compatible with an interface, but does not actually implement the interface.
Now if a function requires an in instance of said interface, you cannot pass the object in question, because it does not implement the interface.
So you either interface your type with the interface, or you need to create an object expression delegating all the methods to the underlaying object. The first option makes implementing the interface easy, but it has to be done beforehand and cannot be don't when retrofitting existing (library) types. Also in the latter case, you do not need to take into account a lot of complicated inheritance hierarchies, because, you are implementing the interface through delegation instead of inheritance.
If I misunderstood the use-case, maybe the idea with extending the object expression syntax should be moved into a separate freature request.


#### Comment by mavnn on 6/3/2014 10:06:00 AM ####
I'm out of votes, unfortunately. This would be pretty awesome, however. Alternatively, something similar to member constraints where you could say "anything that matches the signature of this interface" as a constraint.


#### Comment by Ryan Riley on 6/3/2014 10:35:00 AM ####
Here's a quick sample of the current problem: https://dotnetfiddle.net/vm2CJ6


#### Comment by Ryan Riley on 6/3/2014 10:50:00 AM ####
@mvann: Something like assembly neutral interfaces without the need for an actual interface implementation that also accepts type extensions would also satisfy me, though I would much prefer the stronger contract afforded by interfaces.


#### Comment by Mauricio Scheffer on 6/3/2014 11:04:00 AM ####
FsControl ( https://github.com/gmpl/FsControl ) is a workaround that does this *now* with the current F#.
@Ryan for your concrete problem, FsControl has the ToString "type method": https://github.com/gmpl/FsControl/blob/master/FsControl.Core/Converter.fs#L98
And it even does constraining for parametric types, i.e. like Haskell's Show a => Show (Maybe a)


#### Comment by Ryan Riley on 6/24/2014 10:48:00 AM ####
Thanks all for your comments. FsControl is pretty great, and I'm using it now. I don't think sealed classes are a complete blocker, though they probably make performance a pain. See https://groups.google.com/d/msg/fsharp-opensource/ar8-lbRlTwQ/JzFakHTt1dgJ for an example. As Paul discovered, you can actually use object expressions to append interfaces, though I'm quite certain this won't last long using persistent data structures without doing something to change the module or type functions of the persistent data structures themselves. Consider, for example, the list type.


#### Comment by Phil de Joux on 11/9/2014 3:34:00 PM ####
Here's a concrete example from https://github.com/ServiceStack/ServiceStack/wiki/Error-Handling
"In addition to the above options, you can override the serialization of ad-hoc exceptions by implementing the IResponseStatusConvertible.ToResponseStatus() method and have it return your own populated ResponseStatus instance instead."
type StatusResponse =
{mutable Status : ResponseStatus}
interface IHasResponseStatus with
member x.ResponseStatus
with get () = x.Status
and set (v) = x.Status <- v
exception StatusExn of StatusResponse
type StatusExn with
//interface IResponseStatusConvertible
member x.ToResponseStatus () : StatusResponse = x.Data0


#### Comment by Phil de Joux on 11/9/2014 3:42:00 PM ####
Classes derived from Exception declared using "exception of" are sealed.


#### Comment by exercitus vir on 6/13/2015 1:26:00 AM ####
Regarding this implementation I'd like to elaborate on what Jack Pappas said: Implementing an extension interface, would generate an adapter type and an adapter function that adapts the extended type to the same extension interface while making it appears identical to the extend type. This means that adapter type would need to inherit the extended type with all its interfaces in addition to implementing the new interface. IComparable must also be implemented to return the same result as the extended type. The only restriction is that this does not work with to-be-extended types that cannot be inherited from.


#### Comment by Kurt on 7/6/2015 2:39:00 AM ####
And now, protocols in Swift. https://developer.apple.com/library/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Protocols.html
They are a tasteful design of retro-active interface implementation in a language that seems to have much the same philosophy as F#.
Protocols are extremely powerful, not so much for apps but in library design I've missed them often.

