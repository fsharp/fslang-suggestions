# Make the single-line use of [<Literal>] consistent [7090326] #

**Submitted by Don Syme on 2/13/2015 12:00:00 AM**  
**6 votes on UserVoice prior to migration**  

See https://github.com/Microsoft/visualfsharp/issues/229
Some declaration constructs allow attributes on the same line as the keyword for the declaration, e.g.
[<Measure>] type kg
[<Measure>] type m
However this doesn't work for "let" bindings, e.g.
https://cloud.githubusercontent.com/assets/445888/6168930/cd4fc538-b2c9-11e4-8961-6efa3f0e4080.png
Right now the consistent way to do things is always to use multiple lines, e.g.https://cloud.githubusercontent.com/assets/445888/6168957/07eb7688-b2ca-11e4-887e-97e8de7c90c9.png.
The suggestion is to make this consistent by allowing single-line use everywhere, if that is technically possible.



## Response ##
** by fslang-admin on 2/5/2016 12:00:00 AM **

Closing as this idea (listed by me) as it has little support


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/7090326)**


## Comments ##

