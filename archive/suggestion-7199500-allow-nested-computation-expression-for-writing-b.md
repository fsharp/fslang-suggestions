# Allow nested Computation Expression for writing Builder Like DSLs [7199500] #

**Submitted by Robert Kuzelj on 3/12/2015 12:00:00 AM**  
**5 votes on UserVoice prior to migration**  

type DirectionBuilder() =
member self.Yield(()) = []
[<CustomOperation("left")>]
member self.Left (acc, degree) = somefn degree
[<CustomOperation("right")>]
member self.Right (acc, degree) = somefn degree
[<CustomOperation("velocity")>]
member self.Velocity (acc, ()) = new VelocityBuilder()
and VelocityBuilder() =
member self.Yield(()) = []
[<CustomOperation("accelerate")>]
member self.Accesslarate (acc, v) = somefn v
[<CustomOperation("decelerate")>]
member self.Decelerate (acc, v) = somefn v
let direction () = new DirectionBuilder()
direction() {
right 90
left 30
velocity() {
accelerate 1
}
}



## Response ##
** by fslang-admin on 7/18/2015 12:00:00 AM **

Many thanks for this suggestion. It is being marked as declined – for discussion see the comments.
Further discussion welcome
Don Syme, F# Language and Core Library Evolution.


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/7199500)**


## Comments ##


#### Comment by Don Syme on 7/18/2015 1:43:00 PM ####
More design detail, use-cases and motivation would be needed here. This would be a pretty substantial feature - what's the killer app for this? The above case is not convincing enough for me.

