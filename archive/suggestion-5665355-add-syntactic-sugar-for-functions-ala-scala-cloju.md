# Add syntactic sugar for functions ala Scala/Clojure [5665355] #

**Submitted by Khan Thompson on 3/21/2014 12:00:00 AM**  
**37 votes on UserVoice prior to migration**  

Add in shorthand syntax for anonymous functions, even if it is only for single argument functions.
For example:
[1; 2; 3; 4] |> List.map (_ + 1)
As opposed to
[1; 2; 3; 4] |> List.map (fun i -> i + 1)
It would be great to have this shorthand so that our anonymous functions are shorter than the C#ers' :).



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5665355)**


## Comments ##


#### Comment by Gustavo Guerra on 3/21/2014 6:13:00 PM ####
This is the same as this one: /archive/suggestion-5663326-syntax-for-turning-properties-into-functions
(your tittle is actually better, but there's already a bunch of votes there)


#### Comment by Jon Harrop on 3/26/2014 9:50:00 AM ####
@Gustavo: I think this is a separate idea. That idea was just a shorthand for a lambda that just invokes a property like (fun foo -> foo.Name) could be #Name. This idea is more general. You could do (_.Name) but with this you can also do (_ + 1) as a shorthand for ((+) 1).
FWIW, Mathematica has the shorthand notation #+1& for this where # is an anonymous argument in an anonymous function that ends with &. The syntax really is quite hideous!


#### Comment by Jon Harrop on 3/26/2014 9:52:00 AM ####
Mathematica can also do multivariate anonymous parameters in anonymous functions. So (fun (x, y, z) -> x*y+z) can be written #1*#2+#3& in Mathematica.


#### Comment by Bryan Edds on 3/27/2014 10:03:00 PM ####
This is silly. You have many alternative options -
[1; 2; 3; 4] |> List.map ((+) 1)
[1; 2; 3; 4] |> List.map (add 1) // where add = (+)
[1; 2; 3; 4] |> List.map incr // where incr n = n + 1
These are all equivalent and good enough.

