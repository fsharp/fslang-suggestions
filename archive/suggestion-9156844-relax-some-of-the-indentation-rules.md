# Relax some of the indentation rules [9156844] #

**Submitted by Tomas Petricek on 8/3/2015 12:00:00 AM**  
**54 votes on UserVoice prior to migration**  

Currently, the general rules for indentation in F# is that the code on the next line should be indented further than the thing that determines its starting point on the previous line.
There are a number of cases where this quite annoyingly means that you have to indent things very far (or, to avoid that, add lots of unnecessary line breaks). One example is when you have nesting in a method call. For example:
Chart.Geo(growth)
|> Chart.WithOptions(Options(colorAxis=ColorAxis(values=[| -100;0;100;200;1000 |], colors=[| "#77D53D";"#D1C855";"#E8A958";"#EA4C41";"#930700" |])))
Now, there is almost no way to make this code snippet look decent. I would want to write something like this:
Chart.Geo(growth)
|> Chart.WithOptions(Options(colorAxis=ColorAxis(values=[| -100;0;100;200;1000 |],
colors=[| "#77D53D";"#D1C855";"#E8A958";"#EA4C41";"#930700" |])))
But this is not allowed, because "colors" should start after the opening parenthesis of ColorAxis, so I would need 50 spaces! To make the number of spaces smaller, you can add additional newline (to get the "ColorAxis" more to the left), but this looks pretty bad:
Chart.Geo(growth)
|> Chart.WithOptions
(Options
(colorAxis =
ColorAxis
(values=[| -100;0;100;200;1000 |],
colors=[| "#77D53D";"#D1C855";"#E8A958";"#EA4C41";"#930700" |])))
Another example is very similar, but with list expressions. I want to write:
let pop2010 = series [ for c in wb.Countries ->
c.Name => c.Indicators.``CO2 emissions (kt)``.[2010]]
This actually works, but it gives warning. Again, it wants me to indent the second line so that it is after "for", but then I'm not saving pretty much anything by the newline. Or, I can introduce lots of additional newlines and write:
let pop2010 =
series
[ for c in wb.Countries ->
c.Name => c.Indicators.``CO2 emissions (kt)``.[2010]]
I think that in situations like these, the rules should be relaxed. In particular, we should not require new line to be intended further than the "starting thing" on the previous line. Just further than the previous line.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/9156844)**


## Comments ##


#### Comment by Tomas Petricek on 8/3/2015 7:09:00 PM ####
Posted to F# Snippets, which actually *shows* the indentation! http://fssnip.net/rZ


#### Comment by DK on 8/4/2015 6:36:00 AM ####
As a matter of fact, I don't find the solution to the problem that you've posted to be that bad. I do however prefer it in a slightly different style: http://fssnip.net/s0
Given enough complexity even this would start becoming too unwieldy, and would require extracting values out into let bindings. But for this example, I personally think this is more than sufficient.


#### Comment by Fredrik Forssen on 8/4/2015 8:18:00 AM ####
What annoys me most is the records. I would prefer to be able to use something looking like the K&R bracing for records, but the F# compiler wants me to either write oneliners or indenting a lot (or putting the braces on their own lines, heresy!)
I'd love to be able to do this (. instead of space since uservoice hates whitespace)
type Person = {
....Name : string
....Age : int
}
let calvin = {
....Name = "Calvin
....Age = 8
}


#### Comment by Anonymous on 8/4/2015 4:17:00 PM ####
+1000 if I could. Constantly annoyed by this while writing F#.


#### Comment by Alexandre Szymocha on 12/7/2015 2:37:00 AM ####
I LOVE this proposition!
I’m currently using
#nowarn "62"
#light "off"
at the top of every file. This removes the pythonic indentation and allows me to write my code shapelessly, but it’s tedious.


#### Comment by Don Syme on 2/3/2016 1:09:00 PM ####
See also /archive/suggestion-7813977-indentation-of-new-lines-should-be-dependent-on-th


#### Comment by Robin Munn on 9/27/2016 11:54:00 PM ####
BTW, records have been mentioned in a separate suggestion: /archive/suggestion-15696774-relax-indentation-rules-on-records
I feel the records idea is a subset of this one, which would also cover lists and arrays (and so on). So although I'm 100% in favor of the records suggestion, I've put my limited votes on this one instead.
Also, I'd like to mention one thing that I haven't seen mentioned yet. I'd like to be able to put the closing delimiter on a line of its own, indented at the same level as the following code. E.g.,
let myFunction () =
....let someList = [
........"foo"
........"bar"
........"baz"
....]
....let otherList = [1; 2; 3]
....// Other code follows

