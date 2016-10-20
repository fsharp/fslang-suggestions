# Allow more flexible layout for constraint syntax [12546456] #

**Submitted by George on 3/1/2016 12:00:00 AM**  
**1 votes on UserVoice prior to migration**  

The following layout of constraints for a sample class should be possible.
GroupedFixtures<'A, 'B
when
'A :> Remote.RemoteWebDriver and
'A : (new: unit -> 'A) and
'B :> ServerFixture
>() as this =
Presently it almost was but the `new()` constraint use of parenthesis caused problems. currently all the constraints layout forces them on the same line which is not as clear or convenient (note the text, that `>() as this`, is allowed on a separate line):
GroupedFixtures<'A, 'B when 'A :> Remote.RemoteWebDriver and 'A : (new: unit -> 'A) and 'B :> ServerFixture
>() as this =



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/12546456)**


## Comments ##

