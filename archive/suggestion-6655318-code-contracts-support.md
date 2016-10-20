# Code Contracts support [6655318] #

**Submitted by Onur on 11/3/2014 12:00:00 AM**  
**24 votes on UserVoice prior to migration**  

This has been discussed but I believe it should be F# that can fix it.
F# compiler does a lot of magic. Especially if we put Contract.Requires to the beginning of a method or a constructor, F# can (if it is a constructor it will) put additional code.
There is nothing code contract team can do anything about this because this is about how F# compiler works. It basically adds code to the prologue methods and ctors. What compiler can do is to respect System.Diagnostics.Contract class and don't put any code above it.
Example:
Suppose you have this code:
type RationalEx =
val numerator : int

new(num : int) as this =
{ numerator = num }
then
Contract.Requires(this.numerator>0)
this.Check(this.numerator)

member this.Check(num:int)=
Contract.Requires(num > 0 )
()
When it is compiled and checked from reflector what you will see is
For the constructor:
public RationalEx(int num)
{
FSharpRef<Program.RationalEx> this = new FSharpRef<Program.RationalEx>(null);
base();
this.numerator@ = num;
this.contents = this;
this.init@5 = 1;
Contract.Requires(LanguagePrimitives.IntrinsicFunctions.CheckThis<Program.RationalEx>(this.contents).numerator@ > 0);
LanguagePrimitives.IntrinsicFunctions.CheckThis<Program.RationalEx>(this.contents).Check(LanguagePrimitives.IntrinsicFunctions.CheckThis<Program.RationalEx>(this.contents).numerator@);
}
and for the method
public void Check(int num)
{
if (this.init@5 < 1)
{
LanguagePrimitives.IntrinsicFunctions.FailInit();
}
Contract.Requires(num > 0);
}
as you see it adds some magic code on top of the contract code by magic. And this causes contract checker and rewriter to fail



## Response ##
** by fslang-admin on 7/18/2015 12:00:00 AM **

Declining this because it is the remit of the code contracts tool. I think they should make a fix in this case, or simply ignore the added F# initialization checking code.
Further discussion and input welcome.
Don Syme, F# Language and Core Library evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6655318)**


## Comments ##


#### Comment by Don Syme on 7/18/2015 11:39:00 AM ####
Why doe this require a fix in F# rather than in the Code Contracts tool?

