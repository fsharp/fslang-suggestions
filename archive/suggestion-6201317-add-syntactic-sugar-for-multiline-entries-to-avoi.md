# Add syntactic sugar for multiline entries to avoid hanging brackets [6201317] #

**Submitted by Dmítrij Jevgénijevič Ačkásov on 7/22/2014 12:00:00 AM**  
**1 votes on UserVoice prior to migration**  

Hanging brackets are bad why don't we replace those with initial opening bracket in multiline implementations and drop the closing one? The same way we use | and |> for multiline statements for the sake of symmetry? :)
From this:
type ComplexNumber =
{
real: float;
imaginary: float
}
let array = [|
{real = 3.0; imaginary = 0.0};
{real = 2.0; imaginary = 0.1};
{real = 1.0; imaginary = 0.2};
{real = 0.0; imaginary = 0.3};|]

To this:
type ComplexNumber =
{ real: float
{ imaginary: float
let array =
[| {real = 3.0; imaginary = 0.0}
[| {real = 2.0; imaginary = 0.1}
[| {real = 1.0; imaginary = 0.2}
[| {real = 0.0; imaginary = 0.3}



## Response ##
** by fslang-admin on 9/16/2014 12:00:00 AM **

Interesting suggestion, but removing closing brackets would be a radical departure for F# syntax. Declining for now.
Don Syme, current BDFL F# Language/Library Evolution.


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6201317)**


## Comments ##

