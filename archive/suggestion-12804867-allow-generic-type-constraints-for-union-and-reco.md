# Allow generic type constraints for union and record [12804867] #

**Submitted by Huw Simpson on 3/4/2016 12:00:00 AM**  
**2 votes on UserVoice prior to migration**  

I suggest that the ability to express the following type constraints be added:
when 'T : union
when 'T : record
This would enable apis which use quotations or reflection over the supplied record or union to be safer.
The constraint could be enforced at runtime if unions or records implemented some sort of marker interface, perhaps there is a better way.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/12804867)**


## Comments ##

