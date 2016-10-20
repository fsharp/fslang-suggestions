# Consider implementing static mixins to make the functional style more convenient in F# [6699130] #

**Submitted by Bryan Edds on 11/11/2014 12:00:00 AM**  
**6 votes on UserVoice prior to migration**  

Here is a conversation from stackoverflow chat that provide context for this language feature idea -
AshtonKJ -
Does anyone else occassionally want to have inheritance with records?
I mean I hate inheritance from a behaviour point of view. But I like it from a data inheritance point of view.

Vandroiy -
Hmh. I guess it could be useful in rare cases, but I never felt a real need.

AshtonKJ -
I guess I can use a DU for what I want to do. Thinking about things in terms of unions still isn't second nature for me yet

Vandroiy -
Huh... okay, I don't get how these two topics relate here, but good if you solved it :)

AshtonKJ -
Esentially I want something that has data only inheritance.
Which I can do with a DU and some trickery.
I think.
Or not.
Damn
Sigh
OOP it is in this case :(

Vandroiy -
What are you trying to do?

AshtonKJ -
Ideally what I would like is a DU, with properties that exist on the base type.
But it doesn't seem like I can do that.

Vandroiy -
I have the impression that inheritance is mostly good if the base class is small. Otherwise, I prefer composing of smaller types and then making helper functions to shorten common cases.

AshtonKJ -
Yeah. My thing is data inheritance is fine. I don't like behavioural inheritance

Vandroiy -
What do you mean by data in this case? A good argument against inheritance is that people like to think in clusters; thus it is hard to think about types that are comprised of lots of fine-grained components. This argument works for heterogeneous data as well. (For homogeneous data, I'd guess that either collections apply or you've ended up with a case that asks for a type provider.)

AshtonKJ -
By data in this case I mean something like
(An example close to what I am doing)
I have tasks of various types. All the tasks have certain shared characteristics. The different sub tasks have their own unique additions
And they will be handled differently (which is why I like the DU idea)
Because the matching would make my life much easier.

weismat -
I would strongly recommend to read "Practical Object-Oriented Design in Ruby: An Agile Primer " - most OO stuff is done poorly, if done properly OO is first about responsibility and exchanging messages, not about inheritance - the inheritance debacle comes frequently from dependency injection/testing

AshtonKJ -
I don't really like the OO way of doing things, but it is still what I am most familiar with. And yes, OO SHOULD be about messaging / responsibility. But mostly it isn't
;)

Vandroiy -
@AshtonKJ Is it much too verbose to just go with standard composition? Like this: fssnip.net/om

AshtonKJ -
Not too verbose. Just was hoping that I would find a better way.
So, a musician's parent's died and he was given the chance to take over the family business. He refused. He favoured composition over inheritance.

Vandroiy -
lol

AshtonKJ -
I can't remember where I saw that one. But it made me snicker
Anyways, done pretending to work for today. I think I am now going to play some games

Vandroiy -
Have fun!

Bryan Edds -
@AshtonKJ, I would recommend trying to make composition work rather than OOP.
Yes, it is more inconvenient.\
Ultimately, what I think you really want is mixins for data types.
Not inheritance per se.
With mixins, data composition would act more like inheritance in that you wouldn't need to write forwarding functions for each 'subtype'.
It might be high time someone recommended mixins as an F# language feature.
It really would be very useful generally as i've hit the same problem you have several times as well.
and while I've solved it well enough with data composition and forwarding, it feels like a missing piece in the F# ecosystem
and the last thing we want is people resorting to OO too early, thus infeecting their architectures with the unfortunately self-propagating property of OO.

AshtonKJ -
@BryanEdds How would you envision it working?

Bryan Edds -
Basically, a mixin in this case would generate a bunch of forwarding functions from type A to B along with compositing A's data fields into type B.
There would be no actual 'subtyping' (EG - casting B to A)

Ibasa -
is forwarding even necessary in that case

Bryan Edds -
for convenience, yes

Ibasa -
compiler could just plain copy paste the method and fields

Bryan Edds -
well, technically, maybe not
this form of mixin without subtyping would work well with F#'s compile-time duck typing (structural 'subtyping')
I really think F# is ripe for this feature.

Ibasa -
doesn't play nice with C# interop though

Bryan Edds -
neither does F#'s type extensions

Ibasa -
but still if there was a clean way of doing it that kept interop nice that would be good

Bryan Edds -
don't hold yer breath on that
it's just not there

Ibasa -
yeh it would be pretty merg to express in CIL metadata
I guess maybe mixins as interfaces, + extension methods

Bryan Edds -
maybe bits and pieces of the implementation could be made more .net-ish here and there

Ibasa -
but then you still have the issue of fields

Bryan Edds -
but overall, you'll have to deemphasize .netness
now, maybe if .net did mixins, then there'd be something to talk about in terms of idiomaticy

AshtonKJ -
Ok, so that game doesn't do it for me. Le sigh

Bryan Edds -
but it doesn't at all, so we're on our own
The original conversation is also linked here - http://chat.stackoverflow.com/transcript/message/19890630#19890630



## Response ##
** by fslang-admin on 2/5/2016 12:00:00 AM **

Closing as this suggestion needs to be more concrete (not just a chat log)
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6699130)**


## Comments ##


#### Comment by Isaac Abraham on 11/11/2014 9:31:00 AM ####
Agree with this in principle - there are times where you want to share fields across records. The only way to do it now is by making a separate record type and making that a child field of the two top-level record types (so a sort of composition approach). It would be nice to have the ability to share those properties in a more lightweight fashion (even if this was erased away).


#### Comment by Daniel Robinson on 11/11/2014 9:33:00 AM ####
Posting a chat log instead of clearly and concisely stating your suggestion doesn't bode well for gathering support from the community.


#### Comment by Bryan Edds on 11/11/2014 9:44:00 AM ####
Danial Rocinson, please feel free to do your part and write a summary. I have some other pressing stuff I have to do today, so I can't polish this as much as we would both like. And on the other hand, a chat context can be extremely illuminating in its own way if one is willing to spend the time on it.


#### Comment by Bryan Edds on 11/11/2014 10:33:00 AM ####
Here's a link to the extended chat log -
http://chat.stackoverflow.com/rooms/51909/conversation/data-type-composition-via-mixins


#### Comment by Suminda Sirinath Salpitikorala Dharmasena on 11/13/2014 1:16:00 AM ####
The details are lost in the chat. Can someone summarise.


#### Comment by Vasily Kirichenko on 11/15/2014 9:14:00 AM ####
+1. What's this all about?


#### Comment by Frank Joppe on 11/16/2014 9:12:00 AM ####
I'm casting a vote for the feature of Record inheritance. And honestly, I would like Record to be even a bit more like a class, having a constructor (with parameters), but keeping the current Record advantages with the equality comparison.


#### Comment by Isaac Abraham on 1/9/2016 6:06:00 AM ####
Frank: If it's just a constructor that takes in all the fields, how is this any different from the current native syntax e.g. { Field = value; Field 2 = value2 } etc. aside from possibly saving a tiny bit of text at the cost of readability e.g. new Record(value, value2) ?

