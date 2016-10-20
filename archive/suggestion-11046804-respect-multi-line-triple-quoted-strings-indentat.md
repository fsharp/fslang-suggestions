# respect multi-line triple quoted strings indentation [11046804] #

**Submitted by George on 12/10/2015 12:00:00 AM**  
**1 votes on UserVoice prior to migration**  

It would be useful if the starting position of a multi-line triple quoted string could set the starting position of the content when it is the first non-whitespace character on it's source line. Additionally, when it is followed only by source level whitespace character, then the content is presume to actually start on the next line, indented of course. If non-whitespace characters occur prior to the indent point, then it may be flagged as a syntax error, however, EOL characters would be retained to capture lines.
Perhaps a new symbol could be used other than triple quotes...perhaps quadruple quotes: """"



## Response ##
** by fslang-admin on 12/15/2015 12:00:00 AM **

This would be a breaking change
A new symbol may be possible.
Don Syme
F# Language and Core Library Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/11046804)**


## Comments ##

