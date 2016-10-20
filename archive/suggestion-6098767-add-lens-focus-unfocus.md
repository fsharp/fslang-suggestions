# Add Lens focus unfocus [6098767] #

**Submitted by Craig Stuntz on 6/25/2014 12:00:00 AM**  
**11 votes on UserVoice prior to migration**  

Lenses allow you to read/write fields in a clean, generic, and extensible way. Here are a few before/after cases using made-up syntax. I'm not sure what the ideal syntax for F# would be.
I'm deserializing XML into F# records. For application-specific reasons, I can't use an off-the-shelf framework. My code contains this:
let private readRatebookServiceDataNode (ratebook : RawRatebook) (reader: XmlReader) =
let serviceDataType, serviceData = readElementAndReturnContentAsServiceData reader
match serviceDataType with
| "AccidentViolationOrder" -> { ratebook with AccidentViolationOrder = serviceData }
| "AdditionalInterest" -> { ratebook with AdditionalInterest = serviceData }
| "AntiTheft" -> { ratebook with AntiTheft = serviceData }
...and so on, for many more, mostly duplicated lines. If I had a dictionary of lenses, I could write this long function in one line:
ratebookLenses.[serviceDataType].Set serviceData
Also, lenses allow composition of record fields when setting values. See the worked out example here:
http://bugsquash.blogspot.com/2011/11/lenses-in-f.html
There's an implementation in FSharpX:
https://github.com/fsprojects/fsharpx/blob/master/src/FSharpx.Core/Lens.fs
Lenses in F# today have a major drawback, however. You must write them out explicitly for every label on a record. If you only use the lens once, it's usually more code with the lens than without.
Ideally I'd like to be able to focus and unfocus labels similar to the Haskell examples here:
http://www.scs.stanford.edu/14sp-cs240h/slides/lenses.html
So in more F# terms I'd write something like:
let labelALens = Lens.focus <@ myRecord.labelA @>
Or, with implicit quotation ( /archive/suggestion-5975797-allow-implicit-quotation-of-expressions-used-as-a )
let labelALens = Lens.focus myRecord.labelA
Mauricio's code goes from:
type Car with
static member mileage =
{ Get = fun (c: Car) -> c.Mileage
Set = fun v (x: Car) -> { x with Mileage = v } }
...to something like:
type Car with
member mileage = Lens.focus c.Mileage
Worth noting: If F# gets hygenic macros ( /archive/suggestion-5674940-implement-syntactic-macros ) then you could implement lenses that way and no special feature would be necessary. But I'd like lens support even if F# never gets macros!



## Response ##
** by fslang-admin on 2/5/2016 12:00:00 AM **

Closing as duplicate of /archive/suggestion-6906132-implement-first-class-lensing-lenses-in-f, or close enough, please see my comment
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6098767)**


## Comments ##


#### Comment by Craig Stuntz on 6/25/2014 3:53:00 PM ####
Also related: "Syntax for turning properties into functions" /archive/suggestion-5663326-syntax-for-turning-properties-into-functions


#### Comment by Don Syme on 2/5/2016 4:07:00 AM ####
Close enough to /archive/suggestion-6906132-implement-first-class-lensing-lenses-in-f that I will close as a duplicate

