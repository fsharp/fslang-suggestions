# Add support for default values in record types [6272047] #

**Submitted by Ted P on 8/8/2014 12:00:00 AM**  
**16 votes on UserVoice prior to migration**  

It would be able to define default values for fields in a record type definition so that those fields don't need to be set unless they differ from the default values.
Simple example:
type TransactionLogEntry = {
timeStamp: DateTime;
state: string = "Initial state"
}
let a:TransactionLogEntry = {timeStamp = DateTime.Now}
Here by explicitly saying which record type we mean, we would not need to set the 'state' field since the default value is what we want in most cases. Yes, this could be accomplished through a factory method on the record type but this a nicer approach I think.



## Response ##
** by fslang-admin on 2/10/2016 12:00:00 AM **

Thanks for the suggestion. It is quite a reasonable one. However I have marked it as declined for the reason listed below.
Don Syme
F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6272047)**


## Comments ##


#### Comment by Loic Denuziere on 8/8/2014 8:03:00 AM ####
This would be particularly useful for compilation to JavaScript (via WebSharper or TypeScript, although I can only speak for the former) when using external JS libraries. A very common pattern in JavaScript is the "configuration object", to pass named arguments as an object:
myLibrary.someFunction({arg1: 'test', arg2: 12})
Right now the way we make this work in WebSharper is using a class with mutable properties:
MyLibrary.SomeFunction(MyLibrary.SomeFunctionConfig(Arg1 = "test", Arg2 = 12))
But it's quite verbose. Records with optional or default values would allow us to be as succint as javascript:
MyLibrary.SomeFunction({Arg1 = "test"; Arg2 = 12})


#### Comment by Richard Gibson on 8/20/2014 10:10:00 AM ####
I know it's more verbose than what you've got, but at the moment I do this which isn't too bad:
type TransactionLogEntry = {
timeStamp: DateTime;
state: string
} with
static member Default = {
timeStamp = DateTime.MinValue
state = "Initial state"
}
let a:TransactionLogEntry = { TransactionLogEntry.Default with timeStamp = DateTime.Now }
Unfortunately it requires that you give default values for all fields in order to keep the compiler happy.


#### Comment by Loic Denuziere on 8/21/2014 8:07:00 AM ####
@Richard Gibson: Another inconvenient of your method is that every time you recreate the Default record, and then create another record with the updated fields. That's twice as many memory allocations as necessary. I guess you could do something like:
type TransactionLogEntry = { timeStamp: DateTime; state: string }
[<CompilationRepresentation(CompilationRepresentationFlags.ModuleSuffix)>]
module TransactionLogEntry =
let Default = { timeStamp = DateTime.MinValue; state = "Initial state" }
But it gets really verbose.


#### Comment by Alfonso Garcia-Caro on 9/7/2014 10:32:00 AM ####
I agree with Loic, this would be very helpful when writing F# to be compiled to JavaScript in FunScript too.


#### Comment by Ted P on 9/14/2014 2:59:00 AM ####
An alternate syntax for instantiation which reads nicer could be:
let a = { TransactionLogEntry with timeStamp = DateTime.Now }
with the type name instead of an instance before the 'with' keyword.


#### Comment by Gauthier Segay on 2/28/2015 7:40:00 AM ####
Would be better handled at library level if we had type class support:
https://github.com/mauke/data-default


#### Comment by Don Syme on 2/10/2016 11:15:00 AM ####
The F# approach is that once you cross the boundary of needing record-type-invariants, or defaults, or extra internal state computed stored in hidden fields and so on, then you should switch to a class type. I think this also applies here: rather than trying to load more features into record types, we would say "ok, if you want default, it's time to switch to a class type, and use optional named arguments in the class constructor".


#### Comment by Don Syme on 2/10/2016 11:16:00 AM ####
For that reason we've always taken the approach not to add bells-and-whistles to the record type mechanism in F#. So I will apply a rule of consistency and mark this as declined.


#### Comment by Vasily Kirichenko on 3/17/2016 6:33:00 AM ####
I disagree. I don't see why adding default values are bad for records.
Instead of:
type R =
{ A: int = 0
B: string = "foo"
C: float }
we currently have to write:

type C(c: float, ?a: int, ?b: string) =
let a = defaultArg a 0
let b = defaultArg b "foo"
member __.A = a
member __.B = b
member __.C = c
and we don't get record's `{ x with ... }` syntax and pattern matching.
So we have very primitive functional records and very OOP classes, so when we cannot fit what we want into the record concept we fall down to full blown C#-slyle boilerplate.


#### Comment by Jared Hester on 3/17/2016 6:37:00 AM ####
"default" records are incredibly common across F# codebases, it hardly seems worth it to switch to a class and lose the pattern matching benefits of records just to use optional named arguments in the constructor.

