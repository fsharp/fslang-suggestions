# Richer literals: TimeSpan/DateTime/Char array/UTF8 [11109258] #

**Submitted by Tom Rathbone on 12/16/2015 12:00:00 AM**  
**4 votes on UserVoice prior to migration**  

Combining several suggestions for richer literals
- New literals for TimeSpan and DateTime. e.g.
"01:02:03"T --> new TimeSpan(1,2,3)
"2015-01-02 10:30:00"D -> new DateTime(2015,01,02,10,30,00)
- Char[] e.g
"abcd"C
- UTF8 encoded strings "abc££def"U
and indeed perhaps the whole mechanism should be extensible like QZRING literals



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/11109258)**


## Comments ##


#### Comment by Sergey Tihon on 12/20/2015 1:17:00 AM ####
F# allow you to define your own behavior for suffixes Q, R, Z, I, N & G - https://sergeytihon.wordpress.com/2014/01/11/f-kung-fu-2-custom-numeric-literals/

