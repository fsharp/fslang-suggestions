# Allow Extension properties setters in initializers [6200089] #

**Submitted by Paul on 7/21/2014 12:00:00 AM**  
**6 votes on UserVoice prior to migration**  

I suggest we consider allowing ExtensionProperty=expr property setters in initializers.
For example
C(ExtensionProperty = [1;2;3])
Or for example to provide c# “add” pattern like support
type StackLayout with
member x.ChildrenInitializer with set (values : UIElement seq)=
values |> Seq.iter x.Children.Add
let layout = StackLayout (Orientation = StackOrientation.Horizonta,
ChildrenInitializer = [Entry(Placeholder = “Username”);Entry()])



## Response ##
** by fslang-admin on 1/21/2015 12:00:00 AM **

This has now been completed for F# 4.0+, see https://github.com/Microsoft/visualfsharp/pull/17 and https://github.com/fsharp/FSharpLangDesign/blob/master/FSharp-4.0/ExtensionPropertyInitializersDesignAndSpec.md


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6200089)**


## Comments ##


#### Comment by Paul on 7/22/2014 7:03:00 PM ####
An initial implementation of this feature has now been submitted here:
https://visualfsharp.codeplex.com/SourceControl/network/forks/EdwardPaul/PropertyInitializationExperiments


#### Comment by Don Syme on 9/6/2014 11:20:00 AM ####
I very much like this proposal, especially as i comes with a trial implementation that appears sound on a quick review.
However, it would be great to get more eyes on this and get more votes for the featue. If you are on twitter, could you advocate for this feature using the #fsharp tag please.


#### Comment by Don Syme on 11/10/2014 8:13:00 AM ####
Hi Paul,
There's a problem with your submission, could you take a look? Also you will need to sign the CLA for submitting to http://visualfsharp.codeplex.com
Otherwise I think it's ready to go.
Thanks
Don


#### Comment by Don Syme on 1/16/2015 10:49:00 AM ####
A speclet for this feature is here: https://github.com/fsharp/FSharpLangDesign/blob/master/FSharp-4.0/ExtensionPropertyInitializers.md


#### Comment by Don Syme on 1/21/2015 6:10:00 AM ####
Speclet is now here: https://github.com/fsharp/FSharpLangDesign/blob/master/FSharp-4.0/ExtensionPropertyInitializersDesignAndSpec.md

