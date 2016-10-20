# Allow [<DefaultValue>] on member val auto-properties [13584294] #

**Submitted by Reed Adams on 4/25/2016 12:00:00 AM**  
**6 votes on UserVoice prior to migration**  

This is specifically motivated by my issues with using Entity Framework and how it initializes DbSet<'T> elements. There might be other applications.
In order to correctly interact with EF in C# I may use:
public DbSet<RecType> Records { get; set }
To accomplish the same thing in F# I must;
[<DefaultValue>]
let mutable private _Records: DbSet<RecType>
member x.Records with get() = x._Records and set value = x._Records <- value
Not doing so causes the EF wire-ups to be lost when the regular member init-assign is called.
I believe that it would be beneficial to allow the following:
[<DefaultValue>]
member val Records: DbSet<RecType> with get, set
This would remove a good deal of boilerplate code and more expressively describe what's going on.
Thank you for your consideration.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/13584294)**


## Comments ##


#### Comment by Daniel Robinson on 5/2/2016 9:10:00 AM ####
Reed, an equivalent translation of your C# to F# would be:
member val Records = Unchecked.defaultof<_> with get, set


#### Comment by Reed Adams on 5/3/2016 9:33:00 AM ####
Unfortunately, this doesn't solve the problem. That changes the type away from the required EF DbSet<> to an IQueryable<QuerySource<,>> as well as not solving the underlying issue of late-assigning the initializer value, which is overwriting property hook wire-ups used by EF.
The code you posted isn't really equivalent since C# doesn't require property initializers. When the GC allocates memory for the (C#) class it's zero-set for the size of the class and then no further action is taken. F# does this, but then additionally sets the init-value during construction. This is an extra value-set step that C# lacks, and in this case kills the work EF has already done. This is why [<Defaultvalue>] on an F# field prevents the need for an explicit initializer value and prevents the described problem, at the cost of much additional code to facilitate the solution.
I was hopeful for it to work, but it just wasn't so.


#### Comment by Don Syme on 6/13/2016 5:45:00 AM ####
I'm not certain, but does this work?
type C() =
[<DefaultValue>]
val mutable Records: DbSet<RecType>
??


#### Comment by Reed Adams on 6/17/2016 5:05:00 PM ####
Hello, Don. Thank you for reviewing my request.
The suggestion you've given is already among my personal attempts at limiting the verbosity, but this approach too does not solve the issue.
The problem in your suggested case is that the target is no longer a property (EF uses DbSet<> properties as injection markers) but has been demoted to a regular field, which can be DefaultValue'd, but isn't a property, and so EF ignores this element.
To date, the only way that I have managed to avoid this problem is with an explicit backing store (your suggestion is suitable for that purpose) that is DefaultValue'd accompanied by the manual property machinery for get and set. It seems that in all cases of F# property use, the value initializer for the property is happening after EF has setup all of its hooks into the object, effectively wiping them out. Bummer :/
If there is anything else you would like me to test I'm happy to do so.
Thank you again for your time.

