# add possibility to use custom hash code generation for types [6697507] #

**Submitted by Hodza Nassredin on 11/11/2014 12:00:00 AM**  
**5 votes on UserVoice prior to migration**  

Current implementation has some probems with collisions rate but fr backwards-compat reasons it couldn't be changed. https://github.com/fsharp/fsharp/issues/343
We need some way to use custom generatior and change it at compile time.



## Response ##
** by fslang-admin on 2/5/2016 12:00:00 AM **

Declined per Paul’s comment: just use a custom IEqualityComparer or Equals/GetHashCode
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6697507)**


## Comments ##


#### Comment by Paul Westcott on 7/29/2015 2:21:00 PM ####
Not really addressing your issue, but with https://github.com/Microsoft/visualfsharp/pull/513 changes the performance profile of your issue a bit.
32-bit run
------------
good keys
struct custom 1.336040 sec 0.000000 collisions
struct auto 2.028021 sec 0.776863 collisions
struct auto explicit 1.245075 sec 0.776863 collisions
bad keys
struct custom 3.273634 sec 0.061892 collisions
struct auto 7.006841 sec 0.777033 collisions
struct auto explicit 5.811893 sec 0.777033 collisions
64-bit run
------------
good keys
struct custom 1.370548 sec 0.000000 collisions
struct auto 2.040873 sec 0.776863 collisions
struct auto explicit 1.242726 sec 0.776863 collisions
bad keys
struct custom 3.380021 sec 0.061840 collisions
struct auto 7.008352 sec 0.777050 collisions
struct auto explicit 5.819077 sec 0.777050 collisions
And I don't really understand your issue anyway. i.e. you can already create an IEqualityComparer to use, or alternatively you can use the [<CustomEquality>] attribute like
[<CustomEquality; NoComparison>]
type StructTuple<'T,'T2> =
struct
val fst: 'T
val snd : 'T2
new(fst: 'T, snd : 'T2) = {fst = fst; snd = snd}
interface IEquatable<StructTuple<'T,'T2>> with
member a.Equals (b:StructTuple<'T,'T2>) =
EqualityComparer<'T>.Default.Equals(a.fst, b.fst) && EqualityComparer<'T2>.Default.Equals(a.snd, b.snd)
override x.GetHashCode () =
CmpHelpers.combine (EqualityComparer<'T>.Default.GetHashCode(x.fst)) (EqualityComparer<'T2>.Default.GetHashCode(x.snd))
override x.Equals (other:obj) =
match other with
| :? StructTuple<'T,'T2> as other -> LanguagePrimitives.GenericEqualityER x other
| _ -> false
end


#### Comment by Don Syme on 2/5/2016 9:04:00 AM ####
The way to do this is to manually implement GetHashCode and Equals on your key type. That's just how you do it.

