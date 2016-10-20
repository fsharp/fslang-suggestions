# Optionally relax signatures of -X, sin X, cos X to allow use w.r.t. subtyping [11356425] #

**Submitted by Don Syme on 1/8/2016 12:00:00 AM**  
**3 votes on UserVoice prior to migration**  

See https://github.com/Microsoft/visualfsharp/issues/799
type Base(x : int) =
member self.X = x
static member (~-) (a : Base) = Base(-a.X)
static member (+) (a : Base, b : Base) = Base(a.X + b.X)
static member Cos(a : Base) = Base(2*a.X)
type Derived(x : int) =
inherit Base(x)
let a = Base(1)
let minusa = -a // OK
let cosa = cos a // OK
let twoa = a + a // OK
let b = Derived(1)
let minusb = -b // Compile error
let cosb = cos b // Compile error
let twob = b + b // OK



## Response ##
** by fslang-admin on 2/4/2016 12:00:00 AM **

Marking as approved-in-principle per my comment below
We will post an RFC for it in due course.
Don Syme, F# Language and Core Library Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/11356425)**


## Comments ##


#### Comment by Don Syme on 2/4/2016 3:56:00 PM ####
This is a reasonable request and we should accommodate this somehow. Unfortunately we will likely only be able to do it by having the user open a new module.

