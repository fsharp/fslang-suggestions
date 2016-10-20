# Hide Obsolete warnings on record initializer not using the obsolete field. [12826233] #

**Submitted by Matthias Dittrich on 3/6/2016 12:00:00 AM**  
**3 votes on UserVoice prior to migration**  

Basically the compiler emits a warning even when a obsolete field is not used directly in the source code. Here is a code example showing what I mean:
// def version 1
type TestRecordV1 =
{ Field1 : string
Feild2 : string }
static member Emtpy =
{ Field1 = null
Feild2 = null }
// usage
let v1var1 = { TestRecordV1.Emtpy with Field1 = "field1" }
let v1var2 = { TestRecordV1.Emtpy with Feild2 = "field2" }
let v1var3 = { TestRecordV1.Field1 = "field1"; Feild2 = "field2" }
let v1access1 = v1var1.Field1
let v1access2 = v1var1.Feild2
// def version 2
type TestRecordV2 =
{ Field1 : string
[<Obsolete("Use Field2 instead")>]
Feild2 : string }
static member Emtpy =
{ Field1 = null
Feild2 = null } // can we somehow hide the warning here
// (as it is obvious that we need to address it)
// usage
let v2var1 = { TestRecordV2.Emtpy with Field1 = "field1" } // why?
let v2var2 = { TestRecordV2.Emtpy with Feild2 = "field2" }
let v2var3 = { TestRecordV2.Field1 = "field1"; Feild2 = "field2" }
let v2access1 = v2var1.Field1
let v2access2 = v2var1.Feild2
// def version 3
type TestRecordV3 =
{ Field1 : string
Field2 : string }
static member Emtpy =
{ Field1 = null
Field2 = null } // was broken
[<Obsolete("Use Field2 instead")>]
member x.Feild2 = x.Field2
// usage
let v3var1 = { TestRecordV3.Emtpy with Field1 = "field1" } // not broken (yes, old compiled versions are still broken)
//let v3var2 = { TestRecordV3.Emtpy with Feild2 = "field2" } // broken
let v3var2 = { TestRecordV3.Emtpy with Field2 = "field2" }
//let v3var3 = { TestRecordV3.Field1 = "field1"; Feild2 = "field2" } // broken
let v3var3 = { TestRecordV3.Field1 = "field1"; Field2 = "field2" }
let v3access1 = v3var1.Field1
let v3access2 = v3var1.Feild2 // obsolete, OK
I'm pretty sure this is because the code will still break (and use the obsolete field behind the scenes). So even if the suggestion can not be accepted in general (but I think still worth the discussion) we should consider this is in scripting contexts (where binary compatibility is not really a problem). Scripting is the place where I realized this, so currently there really is no good way to use Obsolete on records at all (besides using constructor functions, but then I think the compiler should generate them for me behind the scenes).



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/12826233)**


## Comments ##


#### Comment by Matthias Dittrich on 3/6/2016 4:31:00 AM ####
As the formatting was completely broken: http://fssnip.net/7OE
The line with "// Why?" is triggering an obsolete compiler warning!


#### Comment by Matthias Dittrich on 3/6/2016 4:46:00 AM ####
I noticed one more thing: The complete record initializer is triggering the obsolete warning instead of the line accessing the obsoleted field (updated the fssnip version)


#### Comment by Alexei Odeychuk on 3/6/2016 5:47:00 AM ####
I support the idea shared by Matthias Dittrich.

