# Attributes to help resolve type inference [7413124] #

**Submitted by Greg Rosenbaum on 4/1/2015 12:00:00 AM**  
**1 votes on UserVoice prior to migration**  

Sometimes, you want to have a main overload for a method and then some secondary overloads that take arguments in different forms. For example, if you're writing a dictionary, you might want to have:
AddRange (pairs : seq<'key * 'value>)
AddRange (pairs : seq<KeyValuePair<'key, 'value>>)

However, this would normally make type inference impossible, because writing `x.AddRange vs` would be ambiguous. Sometimes though, we really want one method to be inferred, and other overloads are provided for special cases, or for interoperability with other .NET languages.
In such cases, it could be possible to use a special attribute, `DefaultOverloadAttribute`, that specifies the overload the inference procedure should try first. A more powerful alternative would be an `OverloadPriorityAttribute` that accepts an `int`, and creates a sequence of methods to try one after the other.
The attribute should automatically generate some documentation that specifies it is the primary overload.



## Response ##
** by fslang-admin on 2/3/2016 12:00:00 AM **

Declined: see my comment below


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/7413124)**


## Comments ##


#### Comment by Don Syme on 2/3/2016 12:38:00 PM ####
I understand the suggestion and can see the motivation
However my inclination is not to add more special cases to the overload resolution rules unless really critical for interoperability purposes. The F# programmer always has the option of avoiding the use of overloading

