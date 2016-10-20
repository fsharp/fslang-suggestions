# Allow all declarations to be mutually referential and the compiler takes files in any order [10276974] #

**Submitted by Kevin Ransom on 10/19/2015 12:00:00 AM**  
**39 votes on UserVoice prior to migration**  

With F# becoming more and more multi-editor and cross-platform, it is becoming increasingly difficult to teach all build/edit tools about F#'s file order. The F# community are currently struggling to "update" each new build/edit tool to understand that F# actually needs a file order.
Part of the problem is that there is no standard textual way to specify this file order except as command line arguments, and these are not stored in an editable form. There is no standard way to specify the F# file order. We need an (optional) solution to this problem that is closer to home and doesn't involve modifying build/edit tools.
This proposal is one of three alternatives to deal with this problem in the F# language/compiler itself.
The specific proposal covered by this UV entry is to just change F# to use no file order at all, allowing all declarations in an assembly to be mutually referential with other declarations.
Related alternative: Keep a file order, but infer it from #load/#require declarations. This is covered by /archive/suggestion-6323146-syntactically-describe-dependencies-between-files
Related alternative: Keep a file order, but optionally have it specified by a fileorder.fsx or fileorder.txt or fileorder.json: /archive/suggestion-13394442-optionally-specify-file-order-by-a-fileorder-fsx



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/10276974)**


## Comments ##


#### Comment by Daniel Robinson on 10/19/2015 1:55:00 PM ####
I'm confused. Isn't being able to view file dependencies at a glance, based on file order, a good thing for the same reason types are required to be defined in order?


#### Comment by Daniel Robinson on 10/19/2015 1:59:00 PM ####
If we go the #include/#load route, I hope VS will still require dependency order. My 2 cents.


#### Comment by Mark Seemann on 10/19/2015 2:00:00 PM ####
Like Daniel Robinson, I think that since the order matters, being able to view that order at a glance is valuable.
If that feature is removed, I suspect we'll see files named 010Foo.fs, 050Bar.fs, etc. That's not a place I'd like to go.


#### Comment by Colin Bull on 10/19/2015 2:16:00 PM ####
Personally, having the enforced order of the files is a big win for me. It allows me to pick up a project and instantly know where to start figuring out how things work. This is especially useful for libraries which do not have such an obvious entry point as is available in console apps; also since the compiler enforces it is the same across all projects, no matter the developer. I realise that this can be somewhat of a hurdle for beginners, but for maintainability of a code base it is invaluable.


#### Comment by Onorio Catenacci on 10/19/2015 2:16:00 PM ####
Can someone vote against an idea? This is a bad idea.
F#'s enforced compilation order is a _good_thing_.


#### Comment by DK on 10/19/2015 2:22:00 PM ####
I think this is a brilliant idea! And the best part is -- it doesn't cancel out the enforced file order.
Having a tool deduce file order (and for example, update file order in solution explorer automatically) will let us keep the best of both worlds.


#### Comment by Radek Micek on 10/19/2015 2:37:00 PM ####
@DK Unfortunately this is not so simple. Different file orders may result in different behaviours (eg. when a type is in referenced assembly and a type with the same name is also in current assembly).


#### Comment by Jack Fox on 10/19/2015 3:48:00 PM ####
Unless this is a win in some area I do not understand (like tooling) I too would down-vote this idea.


#### Comment by Yaar Hever on 10/19/2015 3:56:00 PM ####
I'm also against it. Letting the compiler figure out the order of dependency only postpones the problem and eventually leads to spaghetti code and cyclic dependencies.
I find that this constraint + the fact that mutually recursive functions and types require the "let/type ... and ..." syntax actually help in reasoning about the structure of the code.
See also this article (and the references at its end): http://fsharpforfunandprofit.com/posts/recipe-part3/


#### Comment by Daniel Robinson on 10/19/2015 5:08:00 PM ####
Kevin, would the files in Solution Explorer re-order automatically based on #load's?


#### Comment by x on 10/19/2015 5:19:00 PM ####
Do this in external tooling to sort your files in the solution, and not in the compiler! As it is, its a great feature for keeping the architecture clean.


#### Comment by Anonymous on 10/20/2015 3:44:00 AM ####
As already commented on Twitter: Please don't break compilation order. It's what makes my code sane.


#### Comment by mavnn on 10/20/2015 7:57:00 AM ####
I'd also like to go on record as not wanting this as a feature; I say this dispite having written build scripts that *do* use #load statements in fsx files to feed the compiler source in the correct order.
It works, but it's ugly and it's not an improvement; optionally moving this information out of fsproj files might be helpful, but I'd rather see a dedicated file for this (like fsi files for signature information).


#### Comment by Shawn Martin on 10/21/2015 12:47:00 PM ####
Since there's no downvote button, I guess I'll pile on with many of the other commenters. I like the existing enforcement of an explicit, user-specified order.


#### Comment by Anonymous on 10/21/2015 3:53:00 PM ####
If I could spend votes to down vote this suggestion I would.
This is a feature not a bug. It's a small bit of pain to start with that improves the overall quality / understandability later.


#### Comment by Bent Tranberg on 10/31/2015 3:01:00 PM ####
I'd also like to go on record as not wanting this. Colin Bull and others has already explained why it should stay the way it is.


#### Comment by Anonymous on 11/4/2015 9:43:00 PM ####
Please don't do this.


#### Comment by Semyon Grigorev on 12/8/2015 9:01:00 AM ####
Bad idea. Fixed compilation order is a good feature.


#### Comment by Siro Mateos on 12/11/2015 10:13:00 AM ####
Add another "downvote", for NOT doing this.


#### Comment by Joakim on 12/23/2015 6:12:00 PM ####
Semantic file order and lack of cyclic dependencies makes it so much easier to figure out what's going on in a project. Consider this a downvote.


#### Comment by Harald Steinlechner on 2/3/2016 6:20:00 AM ####
Another downvote. although it seems nice, we'd increase complexity in f# libraries, .e.g. see http://fsharpforfunandprofit.com/posts/cycles-and-modularity-in-the-wild/


#### Comment by Don Syme on 2/3/2016 2:53:00 PM ####
See also /archive/suggestion-10276974-allow-the-compiler-to-take-source-code-files-in-an which suggests
open "Helpers.fs"
or
#requires "Helpers.fs"
or
#load "Helpers.fs" (which already describes dependencies in scripts)
Note that F# scripts already have syntactic description of non-cyclic dependencies through #load. So a file ordering inferred from syntax is already part of the F# programming model, at least for scripting.


#### Comment by Don Syme on 2/5/2016 5:32:00 AM ####
Jus to mention that I don't see anything fundamentally "non-F#" about optionally describing file dependencies explicitly within files - indeed we already do this for F# scripting using ``#load``. The file ordering would still exist.
See /archive/suggestion-10276974-allow-the-compiler-to-take-source-code-files-in-an for example


#### Comment by Kurren Nischal on 4/14/2016 3:23:00 AM ####
Downvote. The ability to open a project and immediately see the dependency hierarchy is a major reason why we use F#.


#### Comment by Stefano Pian on 4/18/2016 3:37:00 AM ####
Downvote. The compilation order has been a huge blessing for me whenever I need to pick up a moderate-sized or bigger F# project.
I agree that the F# compilation should become editor-agnostic, but either of the related alternatives would solve the problem without sacrificing F#'s excellent enforced code structure.


#### Comment by Jason Ritchie on 6/28/2016 6:49:00 AM ####
Downvote. Having circular dependencies be impossible helps me fall into a 'pit of success' in my designs.


#### Comment by Gauthier Segay on 6/28/2016 6:58:00 AM ####
It is unfortunate that this suggestion mixes 2 concerns:
* declarations to be mutually referential (which most people don't want as seen in comments)
* have the compiler figure out the order rather than have to specify it manually
I think the later point would be a great thing for end-users, and that doesn't circumvent at all file ordering being there and necessary, only it would be figured out by the compiler.


#### Comment by Loic Denuziere on 7/1/2016 8:51:00 AM ####
100% agree with Gauthier. It would be quite good if the compiler could figure out the order of the files, but total circular dependency is way too error-prone.


#### Comment by Alex Yakunin on 9/24/2016 2:09:00 AM ####
Upvote.
There were many points saying that explicit file order is one of core F# features, and it's crucial. It lets you immediately see the order of dependencies, and thus it prevents possible issues with circular / spaghetti dependencies.
I am fully disagree with this:
a) Dependencies aren't simply chained in most of projects -- usually there is a good amount of flexibility in how to order them. And it's not fully clear why a specific order is preferable over others.
b) This also means that actually order doesn't show the dependencies: on contrary, it shows which dependencies do not exist. The only relationship it exposes is: "if A is above B, A definitely does not depend on B". Though the same doesn't mean "B definitely depends on A".
c) Finally, dependency graph is a graph, not a sequence. So I don't understand why it's good to force developers to model it as a sequence. Especially assuming that almost any modern compiler is smart enough to figure out both dependencies and compilation sequence.
d) Nevertheless, I see a value in having an ability to display the dependencies of your F# files. But "display" is not what compilers do -- this is what IDEs and other tools do. So I totally support to have this feature in IDE, but I don't see a single reason to have it baked into the compiler -- at least in such a way.
Moreover, if I'd be building a feature allowing me to see these dependencies, I'd prefer to show differently -- one of good ways is to show it as a tree listing the most independent files on the first level, their dependencies -- on the second, and so on. The opposite order (from the mostly dependent components to their deepest dependencies) is totally valid too. Any profiler is capable of showing a similar structure for your call tree.
And I don't think I'd prefer this dependency graph to be shown simply as an ordered sequence.
Please consider all these arguments before downvoting this feature.

