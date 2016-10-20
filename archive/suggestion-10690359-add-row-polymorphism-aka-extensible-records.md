# Add "row polymorphism" aka "extensible records" [10690359] #

**Submitted by Joris Morger on 11/13/2015 12:00:00 AM**  
**16 votes on UserVoice prior to migration**  

In F# there is no way to write a function that can work on similar records.
If I have two records
type Organisation = { Name: string, Country: string }
type User = { Name: string, Profession: Profession }
and would like to write a function that operates on the common (name: string) fields I need to rewrite my records.
What I would like is a way to write a function that can work with all records that have a field (Name: string)
Here is an example with pseudocode.
Note: I do not propose this exact syntax.
// Named takes a record with at least a name field
// but can have many more in addition to that, denoted by the 'a
type 'a Named = { Name: string | 'a }
let printName (a : 'a Named) : string =
sprintf "Name: %s" a.Name
It's already possible to simulate this, but you'd have to replace your records, see here: http://stackoverflow.com/questions/29531852/does-f-have-row-polymorphism-or-something-similar
This feature is implemented in PureScript and Elm.
Elm uses the Name "Extensible Records", see: http://elm-lang.org/docs/records#record-types
Purescript: https://leanpub.com/purescript/read#leanpub-auto-record-patterns-and-row-polymorphism



## Response ##
** by fslang-admin on 1/23/2016 12:00:00 AM **

Duplicate of /archive/suggestion-9633858-structural-extensible-records-like-elm-concrete
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/10690359)**


## Comments ##


#### Comment by Radek Micek on 11/15/2015 10:05:00 AM ####
Note that this is same as
/archive/suggestion-9633858-structural-extensible-records-like-elm-concrete
and similar to
/archive/suggestion-6181848-provide-better-support-for-structural-typing


#### Comment by Nathan Schultz on 11/17/2015 8:59:00 PM ####
It might be worth noting that Elm is removing Extensible Record support as of version 0.16.
https://github.com/elm-lang/elm-compiler/issues/985

