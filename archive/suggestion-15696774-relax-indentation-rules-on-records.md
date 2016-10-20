# Relax indentation rules on Records [15696774] #

**Submitted by Mathias Brandewinder on 8/17/2016 12:00:00 AM**  
**9 votes on UserVoice prior to migration**  

The current indentation rules around records seem inconsistent, or at least counter-intuitive. Consider for instance:
type Foo = {
....Foo:int
....}
type Bar = {
....F:Foo
....}
let bar = {
....F = {
........Foo = 10
........}
....}
This is valid. But if you change F in Bar to VeryLongName:
type Baz = {
....VeryLongName:Foo
....}
let baz = {
....VeryLongName = {
........Foo = 10
........}
....}
We now get a warning:
warning FS0058: Possible incorrect indentation: this token is offside of context started at position (10:20). Try indenting this token further or using standard formatting conventions.
In a similar fashion, indentation rules around adding members to records seem inconsistent, or at least counter-intuitive.
The 2 examples below are valid:
type Foo1 =
....{
........data:int
....}
....member x.Data = x.data
type Foo2 = {
....data:int
....}
....with member x.Data = x.data
... but this one is not:
type Foo3 = {
....data:int
....}
....member x.Data = x.data
There is a workaround - systematically put the opening brace { on the second line - but the "shorter" syntax is quite nice, and allows to write compact and readable code. Given what is currently acceptable syntax, relaxing a bit the rules would be quite nice, and follow the principle of 'least surprise'.
Note: this is loosely related to /archive/suggestion-9156844-relax-some-of-the-indentation-rules ; that specific problem is brought up in the comments.
Note: sorry about the .... but this is the only way I could find to keep the code indentation preserved.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/15696774)**


## Comments ##

