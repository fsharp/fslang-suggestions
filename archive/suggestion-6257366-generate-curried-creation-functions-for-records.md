# Generate curried creation functions for records [6257366] #

**Submitted by David Tchepak on 8/4/2014 12:00:00 AM**  
**7 votes on UserVoice prior to migration**  

This suggestion is along the lines of [1], but for records.
[1]: /archive/suggestion-5663317-allow-to-use-class-constructors-as-functions
It can be handy to have curried creation functions for records.
Say we have a record with a categoryId:
type Product = { categoryId : int; id : int; name : string }
And we want to create a number of records with the same categoryId. If we have a curried creation method we could do something like:
> type Product with static member create c i n = { categoryId = c; id = i; name = n };;
> let createPl = Product.create 432;;
val createPl : (int -> string -> Product)
> createPl 27 "F#", createPl 42 "Haskell", createPl 123 "C#";;
It would be great to have the compiler generate this. I don't really have a preference for the syntax (create a function with same name as type? So in this case we'd also get a function `Product : int -> int -> string`?)



## Response ##
** by fslang-admin on 9/16/2014 12:00:00 AM **

I’m declining this particular suggestion because of the comment below – “It seems the natural thing in F# would be to allow the record type name to be used as an uncurried constructor allowing named arguments…”
I will open a new suggestion for this.
Don Syme
Current BDFL F# Language/Library Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6257366)**


## Comments ##


#### Comment by Bartosz Przygoda on 8/20/2014 8:54:00 AM ####
WebSharper users would love this, as their formlets syntax suffer a bit from lack of such curried constructor (and you've got those fun x y z -> { ... } lambdas everywhere then).


#### Comment by Don Syme on 9/3/2014 3:51:00 AM ####
It seems the natural thing in F# would be to allow the record type name to be used as an uncurried constructor allowing named arguments, e.g.
Product(3, "three")
Product(categoryId=3, name="three")
[ (3, "4"); (5, "five") ] |> List.map Product


#### Comment by David Tchepak on 9/16/2014 8:33:00 PM ####
Hi Don,
Curried helps for code like this:
https://github.com/mausch/Fleece/blob/c8f7f59417d3b4c68b32a59fd45dd46a3778b977/Tests/Tests.fs#L26
Although we can always call `curryX` I guess.


#### Comment by Huw Simpson on 7/12/2016 5:45:00 AM ####
Anyone know where the suggestion for the non curried constructor is, which Don refers to?

