# An CLIVirtual attribute [6672675] #

**Submitted by Remko Boschker on 11/6/2014 12:00:00 AM**  
**22 votes on UserVoice prior to migration**  

Just as you can use CLIMutable to store records using Entity Framework wouldn't is be nice to be able to set an CLIVirtual attribute on a record field of an ICollection type so that Entity Framework can do lazy loading. See also http://stackoverflow.com/questions/26775760/how-to-create-a-virtual-record-field-for-entity-framework-lazy-loading



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6672675)**


## Comments ##


#### Comment by luketopia on 11/10/2014 5:40:00 PM ####
In addition to making the property virtual, you would also have to make the record type non-sealed since EF creates dynamic proxy types that inherit from the base entity to override the virtual properties. Right now, all record types are sealed.

