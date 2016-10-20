# Inherit `StructuredFormatDisplayAttribute` specified on interface [8432340] #

**Submitted by exercitus vir on 6/16/2015 12:00:00 AM**  
**1 votes on UserVoice prior to migration**  

Annotating an interface with `StructuredFormatDisplayAttribute` should be inherited by types that implement that interface. This would safe a lot of repetitive code when an interface requires a property that is used by `StructuredFormatDisplayAttribute` is implemented by a type.
This suggestion would require the support of the following suggestion to work this way: /archive/suggestion-8431944-allow-to-specify-fully-qualified-name-of-property



## Response ##
** by fslang-admin on 2/3/2016 12:00:00 AM **

Declined per request


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/8432340)**


## Comments ##


#### Comment by Don Syme on 7/17/2015 6:35:00 AM ####
What would happen when multiple interfaces implement this attribute?


#### Comment by Don Syme on 7/17/2015 8:59:00 AM ####
Also, why would this require the fully qualified name? Wouldn't the attribute on the interface use the non-fully-qualified name?


#### Comment by exercitus vir on 7/17/2015 11:15:00 AM ####
Ah, thanks for the good questions. I did not think about multiple interfaces implementing the attribute. The fully qualified name would have been required for `StructuredFormatDisplayAttribute` to to see the member of the interface. But it seems that it is better if that is not possible since the member directly on the type guarantees that there is only one member with that name.
You can decline this request as I understand now that this would not be possible technically.

