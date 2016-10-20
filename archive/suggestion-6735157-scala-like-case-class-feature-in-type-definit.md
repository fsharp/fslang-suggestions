# Scala like 'case class' feature in 'type' definition [6735157] #

**Submitted by M Sheik Uduman Ali on 11/18/2014 12:00:00 AM**  
**1 votes on UserVoice prior to migration**  

I would like to have Scala like 'case class' feature in 'type' definition. In F# 3.0, type definition is too verbose



## Response ##
** by fslang-admin on 2/14/2015 12:00:00 AM **

F# discriminated unions play this role
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6735157)**


## Comments ##


#### Comment by Sergey Tihon on 11/23/2014 4:28:00 PM ####
Could you please provide an example of syntax?
I think that F# Discriminated Unions are more elegant than Scala case classes http://msdn.microsoft.com/en-us/library/dd233226.aspx


#### Comment by Vasily Kirichenko on 11/26/2014 2:52:00 AM ####
sealed abstract class DU
case class Case1(field1: Int, field2: String) extends DU
case class Case1(field3: List[DU]) extends DU
vs
type DU =
| Case1 of field1: int * field2: string
| Case1 of field3: DU list
So who is verbose now?

