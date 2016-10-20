# Support constant values in Discriminated unions [14892927] #

**Submitted by Pedro Santos on 6/21/2016 12:00:00 AM**  
**6 votes on UserVoice prior to migration**  

Hi,
While trying to model a music domain I ended up with this code:
type Note = | C | CSharp | DFlat | D | DSharp | EFlat | E | F | FSharp
| GFlat | G | GSharp | AFlat | A | ASharp | BFlat | B

let noteName note =
match note with
| C -> "C" | CSharp -> "C#" | DFlat -> "Db" | D -> "D"
| DSharp -> "D#" | EFlat -> "Eb" | E -> "E" | F -> "F"
| FSharp -> "F#" | GFlat -> "Gb" | G -> "G" | GSharp -> "G#"
| AFlat -> "Ab" | A -> "A" | ASharp -> "A#" | BFlat -> "Bb"
| B -> "B"

let pitch note =
match note with
| C -> 0 | CSharp -> 1 | DFlat -> 1 | D -> 2
| DSharp -> 3 | EFlat -> 3 | E -> 4 | F -> 5
| FSharp -> 6 | GFlat -> 6 | G -> 7 | GSharp -> 8
| AFlat -> 8 | A -> 9 | ASharp -> 10 | BFlat -> 10
| B -> 11
The code I wish I could write looks like this:
type Note = | C of ("C", 0) | CSharp of ("C#", 1) and so on
let name = fst C
let pitch = sdn C
or
type Note = | C = {name="C"; pitch=0} | CSharp = {name="C#"; pitch=1} and so on
let name = C.name
let pitch = C.pitch
or
type Note = | C of {name="C"; pitch=0} | CSharp of {name="C#"; pitch=1} and so on
let name = C.name
let pitch = C.pitch



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/14892927)**


## Comments ##


#### Comment by exercitus vir on 7/9/2016 12:59:00 PM ####
You could instead just do this:
type Note = { name: string, pitch : uint }
module Note =
let C = { name = "C", pitch = 0 }
let CSharp = { name = "C#", pitch = 1 }
//etc.
let name = Note.C.name
let pitch = Note .C.pitch


#### Comment by Isak Sky on 7/29/2016 7:56:00 PM ####
You can do this:
type Cond = Foo | Bar | Baz
let (|SetV|) x _ = x
[<EntryPoint>]
let main argv =
let c = Cond.Foo
match c with
| Baz ->
printfn "Baz"
| Foo & SetV "and" kwd
| Bar & SetV "or" kwd ->
printfn "Keyword: %s" kwd
| Baz -> failwith "wat"
0 // return an integer exit code
But note this compiler bug:
https://github.com/Microsoft/visualfsharp/issues/1281
Credit @kevin in fp slack.


#### Comment by Abel on 9/22/2016 3:37:00 PM ####
It seems to me to make more sense to change the way you use DU for your problem domain. I am missing CFlat (C♭) and ESharp (E♯) etc, or things like DDoubleSharp (D

