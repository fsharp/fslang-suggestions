# Allow custom equality on record types. [5663332] #

**Submitted by Isaac Abraham on 3/21/2014 12:00:00 AM**  
**4 votes on UserVoice prior to migration**  

Record Types current support structural equality on all fields of the record, or none at all. There is no "easy" way to say "make this record structurally equal using just the ID field" etc. - you have to go back to implementing GetHashCode etc. etc. yourself.
You should have an option of decorating fields on the Record to explicitly state which fields you want structural equality on.



## Response ##
** by fslang-admin on 2/5/2016 12:00:00 AM **

Thanks for the suggestion. Declined per my comment below, please take a look
Best regards
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5663332)**


## Comments ##


#### Comment by Thomas Clarke on 8/24/2015 5:40:00 AM ####
Just a slight modification. Given any ID field that allows equality, comparison is equally possible, and equality and comparison are needed for use of a record in maps and sets - a very common use case for me at any rate!
So the most useful (and fairly painless?) enhancement would be a (record) type attribute say AutoCompareAndEqualityAndHash which referenced a function (restriction to method would be Ok I think):
idf: R -> I
Where R is the record type so annotated and I is any type implementing IComparable and IEquatable.
Typical usage would be for idf to reference an integer id field in the record.


#### Comment by Don Syme on 2/4/2016 5:31:00 AM ####
See also /archive/suggestion-11645070-exclude-mutable-fields-from-gethashcode-in-record


#### Comment by Don Syme on 2/5/2016 9:08:00 AM ####
The F# way to do custom equality and hashing is to implement your own Equals and GetHashCode.
It's hard to find an intermediate point (e.g. just use this field, skip that field, etc.), so we decided in F# 1.0 to only support being explicit. Since that decision was made nothing has really changed, so I don't think we should change the decision and venture into the intermediate ground.
I will mark this as declined for this reason. It's not a bad suggestion, it's just that there is an existing general-purpose way to customize the Equals/GetHashCode.

