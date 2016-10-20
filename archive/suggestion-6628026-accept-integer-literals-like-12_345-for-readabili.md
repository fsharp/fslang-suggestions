# Accept integer literals like 12_345 for readability [6628026] #

**Submitted by Kai Noda on 10/28/2014 12:00:00 AM**  
**21 votes on UserVoice prior to migration**  

Simple modification to lex.fsl should suffice.
Other languages with a similar feature:
Perl
http://perldoc.perl.org/perldata.html#Scalar-value-constructors
Ruby
http://www.ruby-doc.org/core-2.1.3/doc/syntax/literals_rdoc.html#label-Numbers
Java 7
http://docs.oracle.com/javase/7/docs/technotes/guides/language/underscores-literals.html
C++11 (use single quote)
http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2013/n3781.pdf
just to name a few...



## Response ##
** by fslang-admin on 6/17/2016 12:00:00 AM **

Approved in principle, this should be simple for someone to implement
RFC is here: https://github.com/fsharp/FSharpLangDesign/blob/master/RFCs/FS-1005-underscores-in-numeric-literals.md
Don Syme
F# Language and Core Library Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6628026)**


## Comments ##


#### Comment by Vasily Kirichenko on 10/29/2014 2:26:00 PM ####
It's supported in D language as well.


#### Comment by Alexei Odeychuk on 11/10/2014 4:58:00 AM ####
I believe that Kai Noda's suggestion is good, but should be extended. F# compiler has to accept all numeric (both integer and floating-point with an optional suffix) literals with underscores between their digits like the Ada 2012 compiler does. In other words, the use of underscores between digits of numeric literals has to be supported for all numeric types: byte, sbyte, int16, uint16, int (int32), uint32, int64, uint64, float, float32, etc.
It also has to be supported not only for decimal base numeric literals, but also for binary, octal and hexadecimal base numeric literals like in Ada 2012, the world's premier language for engineering mission-critical, safety-critical and security-critical real-time software (in Ada this feature has existed since 1980).
For instance, the following numeric literals have to be accepted by the F# compiler:
12_345
123_456.01
123_456.789_345f
0xFFFF_FFFF
0b00_10_10_10y
0o_77_71_L
0x40_1E_00_00_00_00_00_00_LF
The suggested feature will improve program readability, safety, security and reliability. For instance, it can help improve the F# position in the financial application development domain where numeric literals with accidental typos in a high-frequency trading algorithm can incur huge financial losses.
Moreover, adding underscores between digits in numeric literals for better readability has to be optional, not mandatory feature of F#. So, it will have no adverse impact on the existing codebase and, therefore, does not constitute a breaking change in the programming language.
Finally, I believe the suggested feature is closely associated with non-breaking changes in the printf format string syntax, namely with the introduction of new flags in format placeholders enabling to display underscores between digits for numeric literals. They will be especially useful for debugging purposes. For instance, printf("%3_3d", 12345) has to result in " 12_345", while printf("%03_03d", 12345) has to result in "012_345".


#### Comment by Greg Sieranski on 11/15/2014 9:55:00 PM ####
Going to take a crack at this. Are there some references I can utilize?


#### Comment by Marc Sigrist on 11/17/2014 11:26:00 AM ####
This feature is also considered for C# 6.0 (see "Additional Numeric Literal Formats" at http://msdn.microsoft.com/en-us/magazine/dn683793.aspx).


#### Comment by exercitus vir on 6/16/2015 12:03:00 PM ####
While we are at it, it would be very useful to be able to specify metric prefixes for orders of magnitude:
centi = 10^(-2)
milli = 10^(-3)
micro = 10^(-6)
nano = 10^(-9)
pico = 10^(-12)
hecto = 10^2
kilo = 10^3
mega = 10^6
giga = 10^9
tera = 10^12
which could be used like this:
let number = 5_kilo = 5000


#### Comment by Alexei Odeychuk on 6/19/2016 8:16:00 AM ####
Great accomplishment! This feature is in great demand. Thank you!

