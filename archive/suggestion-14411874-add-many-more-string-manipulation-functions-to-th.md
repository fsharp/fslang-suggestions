# Add many more string manipulation functions to the Core.String module [14411874] #

**Submitted by TheInnerLight on 5/30/2016 12:00:00 AM**  
**53 votes on UserVoice prior to migration**  

The Core.String module does not provide nearly enough features at present, too often we have to revert to using the the standard .NET string class which both hinders tidy piping and stops us taking advantage of curried args / partial application.
I suggest that at least the following functions be added to the string module:
empty : string
isEmpty : string -> bool
isWhitespace : string -> bool
replace : string -> string -> string -> string
startsWith/endsWith : string -> bool
split : seq<char> -> string -> seq<string>
toUpper/toLower(Invariant) : string -> string
trim : string -> string
trimStart/trimEnd : string -> string
Obviously all of this can easily be achieved by writing simple wrappers to the methods in the .NET string class but if F# is going to have a String module, it ought to be a fully featured one.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/14411874)**


## Comments ##


#### Comment by Alexei Odeychuk on 5/31/2016 3:30:00 PM ####
I believe this suggestion is valueable and should be extended. There are three useful functions for string handling in Visual Basic: left, right, mid (please see: String Functions in Visual Basic. https://msdn.microsoft.com/en-us/library/dd789093.aspx).
It would be nice to add them to String module in F# as follows:
left: int -> string -> string
right: int -> string -> string
mid: startFrom: int -> int -> string -> string
Example:
let str = "123456789"
let x = str |> String.mid 2 2 // x = "23"
let y = str |> String.left 4 // y = "1234"
let z = str |> String.right 3 // z = "789"


#### Comment by Alexei Odeychuk on 6/1/2016 6:10:00 AM ####
In addition, it would be nice to add several useful functions from Cryptol, a language for programming cryptographic algorithms, to the F# String module:
drop: int -> string -> string
tail: string -> string // to drop the first symbol from a string
take: int -> string -> string
splitBy: int -> string -> string list
groupBy: int -> string -> string list
join: string list -> string
Example:
let str = "123456789"
let x1 = str |> String.drop 5 // x1 = "6789"
let x2 = str |> String.tail // x2 = "23456789"
let x3 = str |> String.take 2 // x3 = "12"
let str2 = "123456789012"
let x4 = str2 |> String.splitBy 3 // x4 = [ "1234"; "5678"; "9012" ]
let x5 = str2 |> String.groupBy 3 // x5 = [ "123"; "456"; "789"; "012" ]
let str3 = [ "123"; "456"; "789"; "012" ]
let x6 = str3 |> String.join // x6 = "123456789012"


#### Comment by Bent Tranberg on 6/5/2016 2:14:00 PM ####
I like the basic philosophy behind string functions in Delphi, and never understood why the same wasn't done in C#.
String functions in C# typically blow up with exceptions, while in Delphi they typically do the best they can, and typically can't blow up. Delphi string functions results in far less coding, because there's no need to check for index out of range or other possible causes of exceptions, and it's usually far easier to comprehend the possible outcomes of an expression.
For example, SubString in C# will blow up if any index is out of range, which frequently makes it necessary to do a lot of extra checking. Copy in Delphi is basically the same function, but will not blow up, and instead return whatever lies within the given subrange. Safe, logical, easy.
When programming in F#, I typically end up implementing a lot of string functions borrowed from Delphi.
Of course I only suggest this as one more source of inspiration, and of course it overlaps heavily with other suggestions.


#### Comment by Paul Westcott on 6/6/2016 4:06:00 PM ####
The following could be used for some inspiration:
https://gist.github.com/manofstick/37f243fedaae203104c7dcc81b221d4b
This is just my string library that I add to as I use different functions. It has some ideas that may be food for thought, such as:
- treating null as String.Empty (it is f# after all, otherwise use string option...)
- Culture stuff is split into submodules
- "format" uses statically resolved types to call "ToString : string->string" on any object
- silly naming for blank. Not sure what I was thinking. I should probably just rename to the String objects static function names, but without the "NullOr", as that is implied by the library.
But this is far from a complete surface area. as said, only populated as I need things, so should be taken for what it is, a WIP at glacial pace...

