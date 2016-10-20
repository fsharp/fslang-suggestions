# Nonconstant arguments for type providers [9626979] #

**Submitted by Semyon Grigorev on 9/4/2015 12:00:00 AM**  
**0 votes on UserVoice prior to migration**  

An idea is allow developers to use not string constants only but string expressions which can be statically calculated to regular set. It may be useful to improve sql type provider flexibility.
An example:
let getPersons maleOnly =
let s = “select mane, id from persons ”
let filter =
if maleOnly
then “where gender = ‘m’”
else “”
use cmd = new SqlCommandProvider<s + filter, connectionString>()
cmd.Executre()
The set of query expression values can be statically calculated. It can be described with regexp {"select mane, id from persons" ("where gender = ‘m’"|"")}. So, syntax correctness can be checked, parsing can be performed (there are some works on regular set parsing: http://link.springer.com/chapter/10.1007%2F978-3-642-17164-2_10, http://www.easychair.org/smart-program/PSI2015/2015-08-26.html#talk:10362 "Relaxed Parsing of Regular Approximations of String-Embedded Languages"). So it is not necessary to parse each element of the set and parsing can be implemented effectively. This way we can check query correctness and get information for typed result generation. Seems that we have enough information for type provider creation.
Short demo of string-embedded SQL support in MS VS: https://youtu.be/P3FFg02-edc



## Response ##
** by fslang-admin on 2/3/2016 12:00:00 AM **

Declining as now at zero votes.


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/9626979)**


## Comments ##

