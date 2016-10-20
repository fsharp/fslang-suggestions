# Close User Voice in favor of GitHub issues. [16529041] #

**Submitted by Krzysztof Cieslak on 10/6/2016 12:00:00 AM**  
**299 votes on UserVoice prior to migration**  

I really believe we should close UserVoice in favor of using GitHub issues (maybe separate repository for it? ). Here are few reasons for it:
* Bad UX
* Need to monitor and maintain separate communication channel
* No comment editing
* No markup for code samples
* No markdown
* Can't embed images
* No mentions and notifications
* Only 10 votes which reduce people ability to vote (especially in so old project as F# - many people already used all their votes over the years)
* No more fake accounts to workaround votes limit
* God damn this text editor (writing long message [like this] i terrible in editor showing 5 lines)
* GitHub issues can be labeled, milestones can be added, new projects feature can be used
Similar move was done by VSCode Team - https://code.visualstudio.com/blogs/2016/08/19/goodbyeuservoice - and I strongly believe we should do the same.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/16529041)**


## Comments ##


#### Comment by Anonymous on 10/6/2016 3:48:00 PM ####
+1M


#### Comment by Don Syme on 10/6/2016 3:57:00 PM ####
Well, someone would need to move all the items, votes, history, discussion and start to chase down incoming links. I don't think it's simple. Having done it once (when extracting F# User Voice from the Microsoft-specific Visual Studio user voice) I don't fancy doing it again, it was a huge job.


#### Comment by Reed Copsey, Jr. on 10/6/2016 3:59:00 PM ####
Don - I suspect that, with your blessing, we could coordinate that and make most of that happen.
The largest roadblock would be moving votes, since people can't add votes from other accounts. To be honest, I question the value of the votes on here in general, though, as the way voting works on user voice is incredibly problematic anyways.


#### Comment by Krzysztof Cieslak on 10/6/2016 4:01:00 PM ####
I'm pretty sure we can create script using cannopy or HTML TP to get all info from UserVoice and then add it to GitHub using their API :)


#### Comment by Jared Hester on 10/6/2016 4:10:00 PM ####
There are literally no advantages (at least from our perspective) to using uservoice over github.
Another advantage of github that wasn't mentioned is the ability to link directly to a specific comment in the thread.
Another small github advantage is that the comments are listed oldest -> newest, unlike uservoice where you have to go to the end of the thread and read backwards. If your post ends up exceeding the length limit on uservoice you need to split it up and post it backwards so it reads sensibly to other users.
This site is a wellspring of frustration; the lengths we need to go through (e.g. using (****) to replace whitespace so code examples can be copied and pasted without tons of tedious indenting) distracts from focusing on the content of posts.
I don't think the suggestions should be moved over to the visualfsharp or the fsharplangdesign repo. A new FSharpLangSuggestions or FSharpLangEvolution repository should be dedicated to this role.
I'll even do the grunt work of copying over all of the planned, under review, and started issues if that makes it easier to switch over.


#### Comment by Don Syme on 10/6/2016 5:19:00 PM ####
@JaredHester - We would use "FSharpLangSuggestions" or ("fsharp-lang-suggestions" to use more modern repo casing - we should probably rename FSharpLangDesign to fsharp-lang-design assuming the redirects work as expected). This collection is deliberately informal: suggestions, and _not_ actual RFCs. I want that distinction.
@JaredHester Closed suggestions would need to be copied over as well. Also the text giving the resolution.
@ReedCopsey - the vote counts are definitely valuable. The voting is only indicative anyway.


#### Comment by Robin Munn on 10/7/2016 2:57:00 AM ####
A suggestion posted today mentions "No more fake accounts to workaround votes limit" and has 142 votes. Nice practical illustration of why UserVoice votes aren't *actually* all that reliable. :-)
And I would throw 3 votes at this too, except my 10 votes are all used up -- on features I do care about, so I don't want to move them.


#### Comment by Robin Munn on 10/7/2016 2:58:00 AM ####
And since I can't edit my previous comment to add what I forgot to mention, I'll add a new comment to mention it:
I also am 100% in favor of moving to GitHub, and I don't mind re-creating my votes on the issues I've already voted on.


#### Comment by cs mr on 10/9/2016 6:18:00 PM ####
Does github issues require a github account to vote or comment? That could restrict voting and get less engagement.


#### Comment by Robin Munn on 10/9/2016 10:19:00 PM ####
GitHub issues does require you to be signed in to an account in order to vote or comment, but you can create a GitHub account for free. So there's no reason why that should restrict voting any more than UserVoice, which also requires you to be signed in. In fact, it's far MORE likely that using UserVoice would restrict voting, because far more people have GitHub accounts than UserVoice accounts, so using GitHub voting means less of a barrier to entry for new contributors to be able to offer suggestings and vote.


#### Comment by Jared Hester on 10/13/2016 4:26:00 PM ####
This is a sample of what the migration would look like, i didn't transfer everything because github rate limiting makes the process really slow.
https://github.com/cloudRoutine/issueCommRepo/issues


#### Comment by Chet Husk on 10/13/2016 11:30:00 PM ####
We're discussing remaining work over here: https://github.com/baronfel/fsharp-lang-suggestions/issues
Please drop by and raise issues if you feel we're missing anything.

