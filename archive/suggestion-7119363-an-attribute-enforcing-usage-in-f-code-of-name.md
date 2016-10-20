# An attribute enforcing usage (in F# code) of named parameters at callsite [7119363] #

**Submitted by Gauthier Segay on 2/19/2015 12:00:00 AM**  
**4 votes on UserVoice prior to migration**  

In some code, it's critical to have function/methods called with parameter names at call site, for readability reasons, but also for correctness.
I would like F# to enforce this using an attribute for example: [<EnforceNamedParametersAtCallSite>]
suppose we have this code (for sake of showing the idea):
type Foo() =
member x.Bar(b, a) = (a, b)
let foo = new Foo()
foo.Bar(1.00, 0.00)
foo.Bar(a = 1.00, b = 0.00)
now suppose we have this slight change in the code (just swapped the parameter names)
type Foo() =
member x.Bar(b, a) = (a, b)
this would not produce the expected result
foo.Bar(1.00, 0.00)
With the proposed feature:
type Foo() =
[<EnforceNamedParametersAtCallSite>]
member x.Bar(b, a) = (a, b)
foo.Bar(1.00, 0.00) // doesn't compile, expects usage of parameter names
Another example is with FSharp.Data.SqlClient's SqlCommandProvider, which defines methods taking parameters based on their order of appearance in the sql code.
samplesql1.sql
------------------------------------
declare @numerator float
declare @denominator float
set @numerator = @a
set @denominator = @b
select @numerator / @denominator
samplesql2.sql
------------------------------------
declare @numerator float
declare @denominator float
set @denominator = @b // swapped this line, didn't change anything else
set @numerator = @a
select @numerator / @denominator
sample1.fsx
------------------------------------
#r @"..\tools\nuget\packages\FSharp.Data.SqlClient\lib\net40\FSharp.Data.SqlClient.dll"
open FSharp.Data
type divideInSql = SqlCommandProvider< "sample1.sql", YourConnectionString>
let cmd = new divideInSql()
cmd.Execute(0.0, 1.0) // work but wait bellow (don't want that to compile)
cmd.Execute(a = 0.0, b = 1.0) // works
cmd.Execute(b = 1.0, a = 0.0) // works
sample2.fsx
------------------------------------
#r @"..\tools\nuget\packages\FSharp.Data.SqlClient\lib\net40\FSharp.Data.SqlClient.dll"
open FSharp.Data
type divideInSql = SqlCommandProvider< "sample2.sql", YourConnectionString>
let cmd = new divideInSql()
cmd.Execute(0.0, 1.0) // fails divide by 0 (don't want that to compile)
cmd.Execute(a = 0.0, b = 1.0) // works
cmd.Execute(b = 1.0, a = 0.0) // works
------------------------------------
We have seen by now that change of order in a sql file provokes havoc.
API design wise, some people might want to enforce that callsite will use named parameters to avoid those kind of misshaps.
I hope the description is clear enough.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/7119363)**


## Comments ##


#### Comment by Don Syme on 7/17/2015 8:04:00 AM ####
I can see the rationale.
It feels uncomfortable to add a bespoke attribute for this though I don't have specific better suggestions as yet. There's nothing quite like this in the F# language design, apart from the requirement to name record fields in the { a=1; b = 2} construction syntax, which is of course a related problem.

