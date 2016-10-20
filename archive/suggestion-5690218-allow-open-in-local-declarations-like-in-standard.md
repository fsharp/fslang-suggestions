# Allow open in local declarations like in Standard ML and O'Caml (>= 3.12) [5690218] #

**Submitted by Anonymous on 3/27/2014 12:00:00 AM**  
**67 votes on UserVoice prior to migration**  

See e.g. http://www.mpi-sws.org/~rossberg/sml-vs-ocaml.html#localdecs



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5690218)**


## Comments ##


#### Comment by Bryan Edds on 3/27/2014 9:30:00 PM ####
I like this, though I don't know what the downsides might be.


#### Comment by Anonymous on 3/28/2014 7:00:00 PM ####
I don't think there are any downsides to this. An "open Module" declaration has no run-time effects nor does it generate new types so there are no major semantic issues to worry about. It merely allows finer grained scoping of existing bindings.


#### Comment by Paul on 11/13/2014 6:36:00 PM ####
A prototype is available here.
https://visualfsharp.codeplex.com/SourceControl/network/forks/EdwardPaul/AllowOpenInExpressions/contribution/7691


#### Comment by Don Syme on 7/18/2015 6:41:00 AM ####
Paul, could you please bring the PR across to http://github.com/Microsoft/visualfsharp? It is of definite interest (though no commitment about including the feature as yet)

