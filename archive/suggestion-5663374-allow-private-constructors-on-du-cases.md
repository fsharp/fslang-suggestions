# Allow private constructors on DU cases [5663374] #

**Submitted by Richard Gibson on 3/21/2014 12:00:00 AM**  
**6 votes on UserVoice prior to migration**  

Currently we can use DUs to represent several possible states. So if I want to I can have:
type EmailAddress =
| ValidEmail of string
| InvalidEmail of string with
static member Create email =
if Regex(".+@.+\..+").IsMatch email
then ValidEmail email
else InvalidEmail email

But the problem with this is that anyone can create either of my cases. There's nothing to stop someone calling one of the constructors directly like so:

let email = ValidEmail "wubwubwub"
I would like to be able to "hide" the constructors for the individual cases and have a constructor for the parent type.
Could perhaps be combined with active patterns?



## Response ##
** by fslang-admin on 7/18/2015 12:00:00 AM **

Many thanks for this suggestion. It is being marked as declined – for discussion see the comments.
Further discussion welcome
Don Syme, F# Language and Core Library Evolution.


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5663374)**


## Comments ##


#### Comment by Gustavo Guerra on 3/21/2014 9:07:00 AM ####
That's already possible currently:
type EmailAddress =
private | ValidEmail of string
| InvalidEmail of string
static member Create email =
if Regex(".+@.+\..+").IsMatch email
then ValidEmail email
else InvalidEmail email


#### Comment by Andrew Cherry on 3/21/2014 10:35:00 AM ####
It's possible as Gustavo points out, but then anybody else can't match on that DU as the cases aren't accessible. Very useful for providing "immutably safe" arguments to an API perhaps, but maybe there's a more general solution? Essentially I think you'd want the DU constructors to be publicly read only, but I can't think of anything that's very close to that conceptually in current F# or ML...


#### Comment by Daniel Fabian on 3/22/2014 3:27:00 AM ####
I think, this is one of the original use cases for Active Patterns, isn't it?. Make the constructors private and provide an active pattern to read it.


#### Comment by Jack Pappas on 3/23/2014 3:06:00 PM ####
I've suggested a feature to allow implementing "smart constructors" for DU cases. This feature would probably fill your needs as well, without the potential drawbacks of hiding some of the union cases.
/archive/suggestion-5671087-smart-constructors-for-du-cases


#### Comment by Richard Gibson on 3/24/2014 5:44:00 AM ####
The problem with ActivePatterns are that the Union they generate is anonymous, so you can't use them as a type on a function parameter, for example:
let (|ValidEmail|InvalidEmail|) email =
if Regex(".+@.+\..+").IsMatch email
then ValidEmail
else InvalidEmail

let sendEmail (validEmail: ???) =
printfn "Sending email to %s" email
What can I put as the type for validEmail?


#### Comment by Daniel Fabian on 3/24/2014 6:02:00 AM ####
You still put EmailAddress as your type. You just cannot access ValidEmail or InvalidEmail from outside of the DU, if you make the constructors private. The whole DU, however, is still accessible.


#### Comment by Don Syme on 7/18/2015 1:37:00 PM ####
From the discussion below, I think there are adequate existing alternatives available to address this problem.

