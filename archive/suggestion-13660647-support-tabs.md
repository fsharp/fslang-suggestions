# Support Tabs [13660647] #

**Submitted by Anonymous on 4/29/2016 12:00:00 AM**  
**11 votes on UserVoice prior to migration**  

Don't force a code style upon users. Tabs can work perfectly well in whitespace-sensitive languages - see python or haskell - and many people prefer them.
Forcing users to use your style just comes across as petty and picky: not the impression you should be giving. Disappointing to see a promising language hamstrung by narrow-minded design decisions.



## Response ##
** by fslang-admin on 6/2/2016 12:00:00 AM **

Declined, per comments below. F# is a whitespace sensitive language and the general consensus is that TABs are not a good iddea in whitespace sensitive languages given the current status of editors
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/13660647)**


## Comments ##


#### Comment by Anonymous on 5/8/2016 10:53:00 AM ####
Can I downvote this suggestion?


#### Comment by Me on 5/8/2016 3:19:00 PM ####
Have you ever kissed a girl?


#### Comment by TeaDrivenDev _ on 5/8/2016 3:27:00 PM ####
The language once and for all deciding that for all F# code is a *good* thing. The indentation is part of the syntax, not a question of style.


#### Comment by Jerold Haas on 5/8/2016 3:40:00 PM ####
There are far more important things to concern over rather than whitespace.
If you'd like a history lesson on F#'s rules on white space I suggest you look at: https://www.seas.upenn.edu/~cis341/current/programming_style.shtml#3


#### Comment by Anonymous on 5/10/2016 7:13:00 AM ####
If you use Visual Studio, may be TabSanity is what you need: https://visualstudiogallery.msdn.microsoft.com/ac4d4d6b-b017-4a42-8f72-55f0ffe850d7


#### Comment by Robin Munn on 5/17/2016 11:34:00 PM ####
If the UserVoice system allowed downvotes, I would spend 2 votes on downvoting this suggestion.
Tabs for indentation work well when used consistently, e.g. when you will ALWAYS indent by some multiple of N (where N varies according to your preference: 4, or 2, or 8...). However, if you EVER want to line up an indented line with something on the previous line (e.g., lining up |> operators), then tabs will cause you problems. The example given at https://msdn.microsoft.com/visualfsharpdocs/conceptual/code-formatting-guidelines-%5bfsharp%5d is a simple case that would cause tab problems:
let function1 arg1 arg2 arg3 arg4 =
....arg1 + arg2
..+ arg3 + arg4
(Here a . represents a space). If you are coding with tabs for indentation, and use 4-space tabs (the most common setting, and IMHO the most sensible one for coding), then that would become:
let function1 arg1 arg2 arg3 arg4 =
>---arg1 + arg2
..+ arg3 + arg4
(Here >--- represents a 4-space tab). Now the main benefit of tabs (that other coders can adjust them to their preferred indentation level) has been lost! A coder who works with 8-space tabs will see:
let function1 arg1 arg2 arg3 arg4 =
>-------arg1 + arg2
..+ arg3 + arg4
And that doesn't line up at all.
No. Tabs can be nice when your indentation will always be a multiple of N (whatever N may be). But because F# lets you adjust indentation by the width of an operator (plus one space), and that width may vary, tabs are unsuitable for this language.


#### Comment by Stefano Pian on 5/24/2016 7:17:00 AM ####
I agree that the suggestion is bad, or at best an inefficient use of contributors' efforts.
However, I want to disagree with Robin Munn's objection. There *is* one straightforward and well-known solution to the problems he presents:
Use tabs for semantic indentation, and then if necessary add spaces for visual alignment.
In this style, the provided example should be typed as:
let function1 arg1 arg2 arg3 arg4 =
>---..arg1 + arg2
>---+ arg3 + arg4
You can now add as many tabs as you like (if you need to change the semantic indentation of the function) and the alignment will be preserved.


#### Comment by Robin Munn on 5/25/2016 9:25:00 AM ####
Stefano Pian's comment is entirely correct in that this is the one and only correct way to mix tabs and spaces -- tabs for indendation and spaces for alignment. And good editors do support this, sometimes with a little help:
Emacs: https://www.emacswiki.org/emacs/TabsAreEvil#SmartTabs
Vim: http://www.vim.org/scripts/script.php?script_id=231
Resharper: https://www.jetbrains.com/help/resharper/2016.1/Reference__Options__General_Formatter_Style.html
However, there are plenty of "dumb" editors out there that will ruin that perfect mix of tabs and spaces, and turn >---......foo (one tab plus six spaces) into >--->---..foo (two tabs plus two spaces). And that brings me to my main objection to tabs, which is that:
**I shouldn't have to care about the whitespace in my code!**
Mixing tabs and spaces *makes* me care about the whitespace in my code, because I usually can't trust the editor to get it right. And the time and mental energy I have to spend turning on "Show Invisibles" and peering at whitespace, to make sure that the tabs and spaces in my whitespace are being mixed correctly, is time and mental energy that I could have been spending on actual, productive improvements to my code.
So while Stefano's suggestion is entirely correct as far as it goes, it does not change my firm belief that worrying about whitespace is unproductive. And since tab characters in code *unavoidably* leads to worrying about whitespace, I much prefer to avoid them entirely.


#### Comment by Don Syme on 6/2/2016 1:52:00 PM ####
It's fair to say we're not planning to support TABs. After 8 years since F# 1.0 this is, AFAICR, the first time I've heard this suggestion, and there are lots of downvotes for it.

