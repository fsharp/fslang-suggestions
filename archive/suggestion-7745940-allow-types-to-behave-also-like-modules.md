# Allow types to behave also like modules. [7745940] #

**Submitted by Brad Phelan on 4/29/2015 12:00:00 AM**  
**1 votes on UserVoice prior to migration**  

I find this kind of coding annoying
module Foo =
type T = { a:int, b:int }
let xxx t = t.a
let yyy t = t.b

it would be much more compact and have less noise in the type system to allow
type Foo =
{ a:int, b:int }
with
let xxx t = t.a
let yyy t = t.b
So you can do
{ a = 10; b = 20 } | Foo.xxx



## Response ##
** by fslang-admin on 7/17/2015 12:00:00 AM **

Many thanks for this suggestion. It is being marked as declined – for discussion see the comments above.
Don Syme, F# Language and Core Library Evolution.


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/7745940)**


## Comments ##


#### Comment by Anonymous on 4/30/2015 8:23:00 AM ####
The following works:
type Foo =
{ a:int; b:int }
with
static member xxx t = t.a
static member yyy t = t.b


#### Comment by Don Syme on 7/17/2015 7:10:00 AM ####
As pointed out below, adding static members to types is close to what you want.

