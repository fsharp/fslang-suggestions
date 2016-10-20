# Please make a correct ‘modulus’ for F# [7156040] #

**Submitted by Alexei Odeychuk on 3/1/2015 12:00:00 AM**  
**13 votes on UserVoice prior to migration**  

Please fix a bug in the F# compiler. Everybody needs correct values for negative numbers. The algorithm calculating a modulo should respect the existing math rules. For example, 11 % 5 = 1 (correct), but -11 % 5 is -1 (bug), should be 4 (correct value).
For instance, m mod n: for integers m and n, m mod n is the integer for which 0 <= r < n and m-r is a multiple of n. For example, 11 mod 5 = 1, and -11 mod 5 = 4.
Details of discussion and suggested corrections to the algorithm of the % operator are here: 1) http://gettingsharper.de/2012/02/28/how-to-implement-a-mathematically-correct-modulus-operator-in-f/
2) Distinctions between rem and mod: http://mathcentral.uregina.ca/QQ/database/QQ.09.12/h/eric1.html



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/7156040)**


## Comments ##


#### Comment by Fraser Waters on 3/12/2015 7:11:00 AM ####
This matches the behavior of % in C# (and nearly every other language), it would also be a significant breaking change. But adding a new builtin function to do this would be a good idea.


#### Comment by Don Syme on 6/9/2015 2:06:00 PM ####
Just to confirm that our decision in F# 1.0 was to follow C#'s design here.
We would welcome a PR to github.com/Microsoft/visualfsharp/ to add a new operator.


#### Comment by Jared Hester on 6/22/2015 11:15:00 PM ####
` %. ` should be that operator


#### Comment by Jared Hester on 7/3/2016 1:49:00 PM ####
Another option would be to move `mod` from the set of keywords in "mlcompatibility" mode to the standard language keywords


#### Comment by Alexei Odeychuk on 7/5/2016 1:13:00 PM ####
I agree with Jared Hester (July 03, 2016 11:49). The "mod" operator would be a great addition to the F# language!
For example, the "mod" exists in Object Pascal (Delphi), No. 12 in TIOBE Language Popularity Index.
As to "%." operator suggested by Jared Hester (June 22, 2015 21:15), I believe it would add nothing to code readability. Programming is a human activitiy. The more readable and correct code, the better for programmers and language popularity.
I am strongly in favor of the "mod" operator.

