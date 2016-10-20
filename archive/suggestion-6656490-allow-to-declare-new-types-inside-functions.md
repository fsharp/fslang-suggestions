# Allow to declare new types inside functions [6656490] #

**Submitted by Vasily Kirichenko on 11/3/2014 12:00:00 AM**  
**23 votes on UserVoice prior to migration**  

The idea is inspired by "Voldemont" typed from D language http://wiki.dlang.org/Voldemort_types
In short, you are allowed to define types inside function scope and return instances of such types from the functions. The proposing syntax is as following:
let func x =
type Nested = { Value: int }
{ Value = x }
let nested = func 1
let v = nested.Value
The type of the nested type is inferred as "func.Nested". You cannot add type annotations anywhere in code though:
let func x: func.Nested = // not allowed
type Nested = { Value: int }
{ Value = x }
let nested: func.Nested = func 1 // not allowed
Nested types cannot be used as types of arguments, however it's possible to write function with statically resolved type parameters to safely deal with such types.
In D you can use nested types as types for template function arguments like this:
auto getVoldemont() {
struct Voldemont {
int Value;
}
return Voldemont(1);
}
int func(T)(T voldemont) {
return voldemont.Value;
}
auto voldemont = getVoldemont();
auto value = func(voldemont); // template func instantiation
As for me, the main usecase for nested types is replacement for tuples as return types which would hugely increase code readability.



## Response ##
** by fslang-admin on 7/18/2015 12:00:00 AM **

Duplicate of /archive/suggestion-5663202-allow-to-define-types-at-expression-scopes


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6656490)**


## Comments ##


#### Comment by Alexei Odeychuk on 11/8/2014 5:57:00 AM ####
I think it is a very useful idea that is able to add more expressiveness to the language and flexibility to F# programmers in implementing their algorithms.


#### Comment by Isaac Abraham on 1/20/2015 8:50:00 AM ####
So this is kind of like anonymous types (albeit nested types) except they can escape function scope?


#### Comment by Don Syme on 7/18/2015 11:43:00 AM ####
This is a duplicate of this one (which has more votes so will be treated as the canonical one): /archive/suggestion-5663202-allow-to-define-types-at-expression-scopes

