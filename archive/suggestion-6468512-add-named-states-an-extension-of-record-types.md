# Add Named States (an extension of record types) [6468512] #

**Submitted by Alex Baggett on 9/21/2014 12:00:00 AM**  
**13 votes on UserVoice prior to migration**  

Essentially it would let you add a name to specific set of values in a record. and reuse that set when initializing something to a specific state or configuration.
It would look something like this:
type Permissions = { clientServices: bool ; ManagesUsers:bool; InternalContact:bool;}
|ProjectManager = {clientServices = true; ManagesUsers = false; IneralContact:true; }
|Administrator = {clientServices = false; ManagesUsers = true; IneralContact:false; }
|Recruiter = {ClientServices = false; ManagesUsers= true; InternalContact:true;}
type User = {FirstName :string; LastName; permissions:Permissions; }
let Stevo = {FirstName = "Stephen"; LastName = "Rogers"; permissions = Permissions.ProjectManager }



## Response ##
** by fslang-admin on 10/15/2014 12:00:00 AM **

Thanks for the suggestion! See comment above by me.
Don Syme, BDFL for F# Language/Core Library evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6468512)**


## Comments ##


#### Comment by exercitus vir on 9/22/2014 11:50:00 AM ####
How is this different from defining values in a module? Definition and usage would be almost unchanged. E.g.
type Permissions = { clientServices: bool ; ManagesUsers:bool; InternalContact:bool;}
module Permissions =
projectManager = {clientServices = true; ManagesUsers = false; InternalContact:true; }
administrator = {clientServices = false; ManagesUsers = true; InternalContact:false; }
recruiter = {clientServices = false; ManagesUsers= true; InternalContact:true;}
type User = {FirstName :string; LastName; permissions:Permissions; }
let Stevo = {FirstName = "Stephen"; LastName = "Rogers"; permissions = Permissions.projectManager }


#### Comment by Max Malook on 9/25/2014 1:03:00 PM ####
Sure it's something more concise that
type Permissions = { clientServices: bool ; ManagesUsers:bool; InternalContact:bool;} with
static member ProjectManager = {clientServices = true; ManagesUsers = false; InternalContact=true; }
static member Administrator = {clientServices = false; ManagesUsers = true; InternalContact=false; }
static member Recruiter = {clientServices = false; ManagesUsers= true; InternalContact=true;}
So why this extended syntax?


#### Comment by Vasily Kirichenko on 10/5/2014 2:46:00 AM ####
Agree with Max and exercitus vir - no need for this, just use let bindings in a module.


#### Comment by Don Syme on 10/15/2014 7:34:00 AM ####
There are a number of proposals aroundn to extend the support for records in F# in ways that can fairly easily be programmed today by using either
(a) object members on record types; or
(b) a module of functionality related to the record type; or
(c) an object type instead of a record type
All seem sufficiently good solutions and more general. Because of this, I agree with the comments below.

