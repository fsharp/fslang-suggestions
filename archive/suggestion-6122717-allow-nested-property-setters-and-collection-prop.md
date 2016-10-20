# Allow nested property setters and collection property setters in initializers [6122717] #

**Submitted by Don Syme on 7/1/2014 12:00:00 AM**  
**12 votes on UserVoice prior to migration**  

I suggest we consider allowing A.B=expr property setters in initializers, e.g.

UIButton(UIButtonType.Custom, Layer.BorderWidth = 1.0, Layer.BorderColor=UIColor.Gray.CGColor, Radius = size / 2.0)
cf. https://github.com/dvdsgl/shallow/blob/master/Shallow/RoundButton.fs#L6
Also, we should consider allowing collection setters, e.g.
C(CollectionProperty = [ 1;2;3 ])
where CollectionProperty has the "Add" pattern of C#. One design would make it tht any IEnumerable<T> would be assignable, where T corresponds to the type of an Add method, though that may not be fully compatible with the C# mechanism.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6122717)**


## Comments ##


#### Comment by Dave Thomas on 7/6/2014 3:37:00 AM ####
Having an IList<_>.Add mechanism as mentioned would make interop with lots of C# more palatable as extra create methods would ordinarily have to be added or assign an intermediate type.


#### Comment by Paul on 7/21/2014 7:29:00 PM ####
It might be more readable to explicitly specify the property setter to distinguish it from a standard setter with something like
let init values f = values |> Seq.iter f
C(CollectionProperty.Add |> init [1;2;3])
Or use a property setter extension which adds the items to given collection.
C(InitializingCollectionPropertyExtension = [1;2;3])


#### Comment by Paul on 10/19/2014 1:52:00 PM ####
An initial implementation of this feature has now been submitted here: https://visualfsharp.codeplex.com/SourceControl/network/forks/EdwardPaul/AllowNestedAndColllectionPropSetters


#### Comment by Don Syme on 10/20/2014 9:35:00 AM ####
Hi Paul,
That's great news! I'll definitely be taking a look at this.
Could you submit a pull request for that branch so we can see the overall changes more easily? (You may need to rebase the branch) Also could you write up a description of what is and isn't allowed (this should also match your testing)
Thanks
Don


#### Comment by Don Syme on 10/20/2014 10:08:00 AM ####
(BTW I now see the implementation in the "master" branch of https://visualfsharp.codeplex.com/SourceControl/network/forks/EdwardPaul/AllowNestedAndColllectionPropSetters)


#### Comment by Don Syme on 10/20/2014 10:09:00 AM ####
(Also, for those wondering, the design is summarized in this commit: https://visualfsharp.codeplex.com/SourceControl/network/forks/EdwardPaul/AllowNestedAndColllectionPropSetters/changeset/147eff4c8542fd5d5f1e351c831da7d653d679f3)


#### Comment by Don Syme on 10/20/2014 10:09:00 AM ####
(That's the proposed, experimental design)


#### Comment by Paul on 10/21/2014 11:28:00 AM ####
A pull request has now been submitted.

