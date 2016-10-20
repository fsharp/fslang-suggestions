# Code clarity: Dot notation for casting objects to interfaces [13056630] #

**Submitted by Alexei Odeychuk on 3/21/2016 12:00:00 AM**  
**5 votes on UserVoice prior to migration**  

I suggest introducing the dot notation syntax for casting an object to an interface.
It would be great to write, for example:
this.InterfaceName.methodName(param1, param2, ..., paramN)
myObject.InterfaceName.methodName(param1, ..., paramN)
instead of:
(this :> InterfaceName).methodName(param1, param2, ..., paramN)
(myObject :> InterfaceName).methodName(param1, ..., paramN)
I think the use of one symbol "." instead of four symbols "(", ":", ">", ")" to convey the same idea can improve F# code clarity.
The syntax suggested would be especially useful in the body of methods of classes that implement multiple interfaces.
P.S. My suggestion does not mean a breaking change in the F# language. I think the existing syntax and the dot notation syntax for casts to interfaces can be used interchangeably.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/13056630)**


## Comments ##

