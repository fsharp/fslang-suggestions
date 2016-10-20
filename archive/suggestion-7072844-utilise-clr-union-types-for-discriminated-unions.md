# Utilise CLR union types for discriminated unions [7072844] #

**Submitted by Isaac Abraham on 2/9/2015 12:00:00 AM**  
**6 votes on UserVoice prior to migration**  

CLR has native support for union types; these could provide optimization and performance opportunities for F# discriminated unions.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/7072844)**


## Comments ##


#### Comment by David Taylor-Fuller on 2/16/2015 5:31:00 PM ####
Would love to know why this wasnt done in the initial implementation.


#### Comment by exercitus vir on 5/21/2015 6:09:00 PM ####
Also interested. Does anyone have more information on native union types in the CLR?


#### Comment by Sam Isaacson on 7/14/2015 4:58:00 AM ####
When you say "native support for union types" do you mean the usage of attributes <StructLayout( LayoutKind.Explicit )> or something else?
I currently have a need for a DU type that is not heap allocated - this is causing performance problems via the "JIT_new" operation being expensive.


#### Comment by Don Syme on 7/17/2015 8:24:00 AM ####
It would be good to have some mock-up code with performance comparisons for this.


#### Comment by Zoltan Podlovics on 12/30/2015 7:55:00 AM ####
A proof of concept explicit structlayout based demo available at:
https://github.com/Microsoft/visualfsharp/pull/620
https://gist.github.com/zpodlovics/80e12e2de35cf73e6e03
However, it limited only to blittable types. Combine it with blittable type constraint and you can have stack allocated DU.

