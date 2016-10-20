# Provide property on base Discriminated Union type if all the case constructors have the same paramater [14595360] #

**Submitted by Андрей Чебукин on 6/3/2016 12:00:00 AM**  
**27 votes on UserVoice prior to migration**  

If an each case constructor of Discriminated Union has a parameter with the same name and the same type than allow to implement a property on Discriminated Union base type to access to this parameter value.
Now I have to write a match on every case
type Physical =
| OneToOne of Data : ModuleData * Line : ModuleList
| OneOnOne of Data : ModuleData * Line1 : ModuleList * Line2 : ModuleList
| OneByOne of Data : ModuleData * Line1 : ModuleList * Line2 : ModuleList
| Vertical of Data : ModuleData * Line1 : ModuleList * Line2 : ModuleList
* Line3 : ModuleList * Line4 : ModuleList
member this.Data : ModuleData = match this with
| OneToOne(data, _) -> data
| OneOnOne(data, _, _) -> data
| OneByOne(data, _, _) -> data
| Vertical(data, _, _, _, _) -> data
Implement this same parameter as a field on base class and allow me to write
member this.Data : ModuleData = base.Data
Or automatic property implementation would also be a perfect option



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/14595360)**


## Comments ##


#### Comment by exercitus vir on 7/9/2016 1:53:00 PM ####
This is too much magic for my taste. If I saw `base.Data` I would look for such a field or member, but would need to remember that F# magically transforms cases of tuples with common components to this.


#### Comment by Abel on 9/22/2016 3:55:00 PM ####
You can already do generalization:
type Test =
    | Foo of string
    | Bar of string
static member getString x =
    match x with
    | Foo s
    | Bar s -> s // both conditions wrapped in a single continuation
It would, however, be nice if this is generalized further into something like:
static member getString x =
    match x with
    | _ s -> s
But that doesn't work well with tuples as in your original example. You'd still have to iterate them over, even though you'd need only one continuation.

