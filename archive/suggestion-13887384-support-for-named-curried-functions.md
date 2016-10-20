# Support for named curried functions [13887384] #

**Submitted by Bartosz Sypytkowski on 5/18/2016 12:00:00 AM**  
**25 votes on UserVoice prior to migration**  

The idea here is to add support for labeled arguments in curried functions. This could allow to extend things like partial application to depend not only on arguments order, and also to introduce default argument values in curried functions (now it's possible only in F# type methods).
This feature is supported already in ML languages like OCaml or FB Reason.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/13887384)**


## Comments ##


#### Comment by Alexei Odeychuk on 5/21/2016 5:03:00 AM ####
Bartosz, please clarify your suggestion by introducing an example of new syntax in a comment


#### Comment by Richard Minerich on 5/27/2016 4:38:00 PM ####
This could be neat, but I think it would at the very least require a new non-conflicting operator something like:
let f x y = x + y
let f' = f (y ~ 1)
or a whole new spin on partial application, you could make it look kind of like records
let f' = (f with y = 1)
Not really in love with any of this syntax, just throwing it out there.


#### Comment by Jared Hester on 6/27/2016 3:56:00 AM ####
OCaml does this like
-------
let rec range ~first:a ~last:b =
if a > b then []
else a :: range ~last:b ~first:(a+1)
-------
and with the shorthand
-------
let rec range ~first ~last =
if first > last then []
else first :: range ~first:(first+1) ~last
-------
~first is short for ~first:first
~last is short for ~last:last
This is also tied into optional labeled curried args that support default values [1]
------
let rec range2 ?(step=1) a b =
if a > b then []
else a :: range ~step (a+step) b
> range2 1 10;;
val it: int list = [1; 2; 3; 4; 5; 6; 7; 8; 9; 10]
> range2 1 10 ~step:2;;
val it: int list = [1; 3; 5; 7; 9]
- : int list = [1; 3; 5; 7; 9]
------
?(step=1) means ~step is an optional argument which defaults to 1
also when a function only has optional args the last arg has to be unit
------
let open_window ?title ?width ?height ()
------
======
Reason's approach is
------
let add = fun first::f second::s => f + s;
let result = add second::20 first::10;
------
Reason also uses this feature to supply default values to curried functions [2]
------
let increment = fun by::by=0 num => num + by;
let two = increment by::1 1;
let four = increment 4;
------
When a curried function takes optional args it's probably best to require the label always
be used for the optional arg.
Intellisense could also aid in making it clear which argument a value is being used to satisfy
[1] https://ocaml.org/learn/tutorials/labels.html#Usingfooinafunctioncall
[2] https://facebook.github.io/reason/#diving-deeper-curried-functions

