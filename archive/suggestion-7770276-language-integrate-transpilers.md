# Language Integrate transpilers [7770276] #

**Submitted by Nick Cooper on 4/30/2015 12:00:00 AM**  
**7 votes on UserVoice prior to migration**  

Create a framework similar to computation expressions, but built using Roslyn or whatever compiler-like framework would be necessary so that subexpressions would be well-formed and type-safe.
XML Example:
let x1 = xml {%
<?xml version 1.0"?>
<PurchaseOrder OrderDate="1999-10-20">
<Items>
....
</Items>
</PurchaseOrder> %}
let v2 = x1.Root.Attribute("OrderDate").Value
SQL:
let x = sql {%
INSERT INTO TestTable([ID], [Name]) VALUES (@ID, @Name) %}
x.Parameters.AddWith("@ID", 3)
x.Parameters.AddWith("@Name", "My Name")
Or LaTeX, or C#, or CIL, or any other parser that one could imagine.



## Response ##
** by fslang-admin on 7/17/2015 12:00:00 AM **

Many thanks for this suggestion. It is being marked as declined – for discussion see the comments above.
The idea of allowing language embeddings is certainly not a bad one but given the success of things like embedded SQL processing in the SqlClient type provider it feels that any feature in this area would have to be based around evolving and extending the type provider mechanism. Perhaps a synthesis of ideas is what’s needed here.
Don Syme, F# Language and Core Library Evolution.


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/7770276)**


## Comments ##


#### Comment by Vasily Kirichenko on 5/4/2015 4:18:00 AM ####
Have you seen type providers? They are exactly what you want.


#### Comment by Anonymous on 5/7/2015 7:09:00 AM ####
Type providers do not invoke the compiler to work with the text. I'm talking about syntactic help (from an addition compiler) while inside the {% Escape Sequence %} that has Intellisense and such.


#### Comment by Anonymous on 5/7/2015 7:11:00 AM ####
I'll add an additional example:
let cs = CSharp {%
public class Person
{
public string Name { get; set; }
}
%}
As far as the XML version goes, VB supports this currently


#### Comment by Jack Fox on 5/9/2015 10:26:00 AM ####
For SQL Server (and any SQL DB linked database through SS) this already exists. http://fsprojects.github.io/FSharp.Data.SqlClient/ It is built out even further than the documentation suggests. A lot of features still not fully documented.


#### Comment by Don Syme on 7/17/2015 7:06:00 AM ####
This seems out of scope for F# given the existing features - instead we would extend the type provider mechanism to continue to allow processing of external languages to be offloaded to external compiler plugin components.

