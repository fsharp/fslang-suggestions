# Add the (..<), (>..) half-open range operators and (>..<) open range operator (from Swift) [13307676] #

**Submitted by Alexei Odeychuk on 4/4/2016 12:00:00 AM**  
**1 votes on UserVoice prior to migration**  

I suggest adding the (..<) and (>..) half-open range operators and (>..<) open range operator to the language in order to reduce risks of introducing off-by-one errors in code.
There is the (..) closed range operator in F# to generate ranges of consecutive values, but now the language lacks the (..<) and (>..) half-open range operators to generate ranges of consecutive values without the first or last value specified respectively. Furthermore, there is no open range operator (>..<) to generate a range of consecutive values without both the first and last value.
Syntax suggested:
a) from Swift:
1 ..< 10 // means: 1 .. 9 in the already existing F# syntax
b) my suggestions:
0 >.. 5 // means: 1 .. 5, the first value (0) is excluded from the range
// means: 0 .. 3 .. 99; the operators (>..), (..), (..<) can be combined
0 .. 3 ..< 100
// means: 1 .. 9 in the existing F# syntax,
// 0 and 10 are excluded from the range
0 >..< 10
let lst = [ ... some list comprehension ... ]
for i in 0 ..< lst.Length do ... // instead of: for i in 0 .. lst.Length - 1 do
As Edsger W. Dijkstra said, programming is a human activity. The off-by-one errors are often introduced by human programmers because it's easier for them to read and write code like: 0 ..< lst.Length (range from 0 to lst.Length, the last value excluded) instead of: 0 .. lst.Length - 1 (range from 0 to the last value, and the last value is: subtract 1 from lst.Length). We see in life that human programmers often forget to write "- 1" in code.
The syntax suggested helps eliminate off-by-one errors in code.
It would improve F# code robustness and clarity.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/13307676)**


## Comments ##


#### Comment by Gauthier Segay on 4/10/2016 8:28:00 PM ####
Interesting, what about a notation that would bring closer to mathematical notation?
[0..lst.Length[
or
[0..lst.Length)

