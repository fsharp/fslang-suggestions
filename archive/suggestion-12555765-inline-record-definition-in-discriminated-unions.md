# Inline Record Definition in Discriminated Unions [12555765] #

**Submitted by Jared Hester on 3/2/2016 12:00:00 AM**  
**30 votes on UserVoice prior to migration**  

type shape =
(**)| Circle of
(*....*) { centerX : float
(*......*) centerY : float
(*......*) radius : float
(*....*) }
| Rect of
(*....*) { x_lo : float
(*......*) y_lo : float
(*......*) x_hi : float
(*......*) y_hi : float
(*....*) }
Recently Added to OCaml
https://blogs.janestreet.com/ocaml-4-03-everything-else/



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/12555765)**


## Comments ##


#### Comment by Huw Simpson on 3/4/2016 7:29:00 AM ####
This feature already exists in the form:
type Shame =
| Circle of centerX: float * centerY:float * radius:float
| ...
It supports pattern matching by the order of the field as well as the name.


#### Comment by Alexei Odeychuk on 3/6/2016 4:27:00 AM ####
I believe that discriminated unions containing inline records in their declarations is a great idea. It would improve the F# expressiveness. It is good that the F# language supports tuples with named items as Huw Simpson mentioned, but inline records in declarations of discriminated union types would be a new way of expressing programmers' ideas in code. F# should remain competitive and be better than OCaml, I think.


#### Comment by Alexei Odeychuk on 3/7/2016 2:23:00 PM ####
I think inline records can be named as "record expressions" or "records of an anonymous type" for the sake of terminology consistency in F#. There are object expressions in F# that are useful when there is no need to define a class. I think a situation when a language user needs to use a record expression of a compiler-generated anonymous record type instead of a user-defined record type is quite possible in practice and it will be good if the language has a solution able to meet competition with other programming languages.


#### Comment by Bikal Gurung on 5/19/2016 5:34:00 AM ####
This feature is currently deprecated in F# 3.0 and above. It was available I believe until F# 2.0. Maybe we can change the title to 'Undeprecate inline record in DU'. I have also created a ticket/issue in github visual f# repo. https://github.com/Microsoft/visualfsharp/issues/1196#issuecomment-220172524


#### Comment by Demetrios Obenour on 7/7/2016 9:03:00 PM ####
For me, the big advantage is that it would allow mutable inline records. This can be huge for performance.

