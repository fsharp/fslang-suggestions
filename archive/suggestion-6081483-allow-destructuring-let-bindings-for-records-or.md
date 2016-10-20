# Allow destructuring let bindings for records (or tuples with named values) [6081483] #

**Submitted by Eamon Nerbonne on 6/21/2014 12:00:00 AM**  
**5 votes on UserVoice prior to migration**  

Tuples are often bug-prone and hard to read because the ordering of members is critical. However, their use is so convenient that they're often used where they're inappropriate. "Tuples" with named members would be a huge improvement, and records are almost that.
In a similar vein, it would be helpful if this record or named-value tuple were as easy to construct as a tuple: in particular, there's no reason to require an explicitly defined type; all the relevant information about the type is present at the construction site - just like with tuples.



## Response ##
** by fslang-admin on 6/24/2014 12:00:00 AM **

Closing this as it looks very close to being a duplicate of /archive/suggestion-5673015-support-c-like-anonymous-types-in-f -
At least close enough that it can’t be treated independently.
Please reassign the votes there.


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6081483)**


## Comments ##


#### Comment by Eamon Nerbonne on 6/21/2014 3:21:00 AM ####
This would go particularly well with /archive/suggestion-5673015-support-c-like-anonymous-types-in-f - support for anonymous records. The combination would make records as well supported as tuples.


#### Comment by Eamon Nerbonne on 6/25/2014 8:15:00 AM ####
Even without anonymous types, I'd like to have destructuring let bindings; destructuring let bindings make API returning records much more practical. Of course there's synergy with anonymous types, but I don't see how they're the same thing - anonymous types don't necessarily imply destructuring let bindings nor do destructuring let bindings necessarily imply anonymous types (though they'd go well together). In particularly, even with anonymous types and even if they support destructuring let bindings, I'd still want that for records too...
I probably should have left out the "in a similar vein" bit. I get the feeling I misphrased the suggestion. Would it be useful to add a suggestion about just the destructuring and not confuse it with the anonymous types, or do you still think the distinction isn't worth making?

