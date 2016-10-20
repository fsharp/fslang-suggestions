# Optional and named parameters on let bindings on modules [5663215] #

**Submitted by Gustavo Guerra on 3/21/2014 12:00:00 AM**  
**131 votes on UserVoice prior to migration**  

Optional and named parameters are supported in static methods, but not in let bindings on modules. This many times forces you to use a static class instead of a module, which has some inconvenients. Ocaml has this, so I'm guessing is doable.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5663215)**


## Comments ##


#### Comment by Gustavo Guerra on 3/21/2014 8:26:00 AM ####
Original item: http://visualstudio.uservoice.com/forums/121579-visual-studio/suggestions/5592336-optional-parameters-on-let-bindings-on-modules


#### Comment by Andrew Cherry on 3/21/2014 9:42:00 AM ####
A fairly similar syntax of let functionName ?(parameterName: [type]) () = [...] seems like it would work if parameterName became type option? That would seem like it would fit with defaultArg still, etc...


#### Comment by Jon Harrop on 3/21/2014 10:07:00 AM ####
OCaml is rather grim in this respect. They got too fancy and let you have optional curried arguments that support partial specialization which leads to all kinds of inconveniences.
I would like optional non-curried arguments to let-bound functions though.


#### Comment by Jack Pappas on 3/22/2014 8:13:00 AM ####
OCaml does have this, so it is possible -- but as Jon H. pointed out, it's very easy to make this feature "too powerful" and ultimately cause more problems than it solves.
+1 for Jon's suggestion that if this were implemented, it should only be for let-bound functions using the tupled argument style. I think that would provide a good compromise because you'd be able to write let-bound functions in modules in exactly the same way you're writing methods in static classes now (sans overloading), without introducing the complexity of optional curried arguments or type inference when using named arguments.


#### Comment by trek42 on 9/8/2014 4:44:00 PM ####
Does named parameters have similar drawbacks as optional parameters (mentioned by Jon)? If not, would definitely see named parameters supported for curried let-bound functions.
This would remove a fairly common annoying case in pipelines, where I find myself having to use lambda expression (e.g. "... |> fun param -> someFunc a b param c) instead of partial application ("... |> someFunc a b c"), because the pipelined variable isn't the last argument of the function. With named parameter I can use the parameter name to override the parameter order, at the same time increases clarity of code.


#### Comment by Richard Minerich on 3/12/2015 4:04:00 PM ####
It seems like this might ruin the symmetry between tupled function parameters and actual tuples, unless it could be that when you create tuples you can do the same thing, and that seems to come with a host of other problems. What if you could describe function parameters more like records and extend records to allow optional construction parameters?


#### Comment by Richard Minerich on 3/12/2015 4:40:00 PM ####
Also, would we allow overloading in the context of these special module functions? If not it's still not a replacement for actual static classes.


#### Comment by Eric Stokes on 12/24/2015 1:26:00 PM ####
Coming from OCaml this is by far the thing I most want in F#. I am often forced into using a static class when what I really want is a module containing a type and some operations on that type. I'm not sure I agree that OCaml's optional/labeled implementation is "too powerful", for example curried optional arguments could be very useful in a pipeline, it seemed if we forced them to be tupled we'd mostly lose that.


#### Comment by Alfonso Garcia-Caro on 5/18/2016 7:38:00 AM ####
Having this will be tremendously beneficial when parsing TypeScript files to be used by Fable. Currently an extra type must be created to translate module functions in TypeScript with optional or ParamArray arguments.


#### Comment by Dave Thomas on 5/27/2016 10:11:00 AM ####
This would be an excellent addition to the language, using the tupled argument style.


#### Comment by Jared Hester on 6/28/2016 12:41:00 AM ####
related - /archive/suggestion-13887384-support-for-named-curried-functions

