# Add the do .. while loops to the language (from Java, C, C++, C#) [13306077] #

**Submitted by Alexei Odeychuk on 4/4/2016 12:00:00 AM**  
**4 votes on UserVoice prior to migration**  

I suggest adding the do .. while loops to F#. This feature would improve the expressiveness of the language and facilitate the migration of large codebases to F# from imperative languages such as Java, C, C++, C#.
I suggest using time-tested and popular syntax from Java, C, C++, C# (TIOBE TOP 4 languages as of March 2016), but with F#-style indentation instead of {}:
do
(* indentation to indicate the body of the loop *) body-expression
while test-condition
The difference between the do .. while loop and the already existing in F# while .. do loop is that do .. while evaluates its test expression at the bottom of the loop instead of the top. Therefore, the body of the loop is always evaluated at least once before the condition is tested. If the test condition is true, the flow of control jumps back up to do, and the body of the loop evaluates again. This process repeats until the given test condition becomes false. Indentation indicates which expressions are in the loop, so code is clear and easy-to-understand.
It's good that F# is not pure functional language. I like that F# is a functional-imperative programming language suitable for writing real-world applications. So, it would be nice if F# would be fully developed language in terms of imperative programming features. It certainly would boost the F# popularity and facilitate the migration of existing code from C, C++, C#, Java.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/13306077)**


## Comments ##


#### Comment by Bent Tranberg on 4/10/2016 1:33:00 AM ####
I do not like that existing keywords - do, while - are used for this loop construct, especially since "while" is already used for another loop construct. In Pascal syntax this loop construct is called repeat-until. It tells you immediately on top of the loop what this is ("do" doesn't since it's used already), and to expect an "until" at the bottom.


#### Comment by Gauthier Segay on 4/10/2016 7:20:00 PM ####
I'm concerned that "do blocks" will be difficult to discern from "do while" blocks.
I'd appreciate this feature be brought to F# but it needs to not clash with do blocks IMHO.


#### Comment by Graham Sharp on 5/3/2016 12:55:00 PM ####
This can be accomplished with
while (
body-expression
test-condition
) do ()

