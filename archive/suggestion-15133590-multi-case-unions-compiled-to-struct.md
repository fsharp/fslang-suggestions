# Multi-case unions compiled to struct [15133590] #

**Submitted by exercitus vir on 7/9/2016 12:00:00 AM**  
**20 votes on UserVoice prior to migration**  

I am posting this idea to be able to track its status since it is already informally under consideration. Tuples, records, and single-cases unions are have already planned (implementation even nearing completoin) to be compilable to a struct:
struct tuples: /archive/suggestion-6148669-add-support-for-structtuple
struct records: /archive/suggestion-6547517-record-types-can-be-marked-with-the-struct-attribu
struct single-case unions: /archive/suggestion-6147144-allow-single-case-unions-to-be-compiled-as-structs
There is also already a proof of concept for unions of "blittable" types: /archive/suggestion-7072844-utilise-clr-union-types-for-discriminated-unions
There has also been a lot of discussion on the implementation of multi-case unions in the discussion of struct records: https://github.com/Microsoft/visualfsharp/pull/620
One great use of multi-case unions compiled to struct would be optional computations (e.g. Option<'T>) for value types that don't do heap-allocation at all.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/15133590)**


## Comments ##

