# What do you think to add F# atom data type as it's used in Erlang? [5691666] #

**Submitted by Martin Bodocky on 3/28/2014 12:00:00 AM**  
**4 votes on UserVoice prior to migration**  

I think to implement Erlang like atoms can add language more readability more precise pattern matching. More here http://www.erlang.org/doc/reference_manual/data_types.html#id66445.



## Response ##
** by fslang-admin on 7/18/2015 12:00:00 AM **

Many thanks for this suggestion. It is being marked as declined – for discussion see the comments.
Further comments, use cases, information and discussion welcome
Don Syme, F# Language and Core Library Evolution.


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5691666)**


## Comments ##


#### Comment by Daniel Fabian on 3/28/2014 5:29:00 AM ####
What is the difference between atoms and DU cases without annotated data?


#### Comment by Martin Bodocky on 3/28/2014 5:43:00 AM ####
Atom is represent as value it self, for example atom is 'request' is just request is not string is atom. It should be differentiate from other variables, in Erlang should start by lower case or '.
Let's imagine we have atom in F# and we decide atoms in F# should start with one single quote like 'atom.
The reall example can be in pattern matching like :
let receive request =
match request with
| 'remove, Value -> action()
| 'add, Value -> action()
The atom 'remove is static, the variable request is tuple if atom and another data value type.
DU defines data by data value types, atoms are valueless in this sense.
I hope this helps you, if no I will try explain again, I don't know your level of Erlang :)


#### Comment by Daniel Fabian on 3/28/2014 5:48:00 AM ####
I meant, in what is it diffent from a DU like:
type RequestType = Remove | Add
let receive request =
match request with
| Remove, value -> action()
| Add, value -> anotherAction()
in this case the DU RequestType is reeally either Remove or Add but both cases have no value associated with them. The "Remove" or "Add" are the values themselves.


#### Comment by Martin Bodocky on 3/28/2014 6:15:00 AM ####
Daniel, your approach is right! I really cannot argue, you convinced me I don't need atoms in pattern matching also I see advantage when I upgrade RequestType compiler will push me to update my code. You see that's why I love F# I learn new thing every day.

