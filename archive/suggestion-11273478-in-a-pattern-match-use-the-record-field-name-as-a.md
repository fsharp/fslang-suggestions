# In a pattern match use the record field name as a default binding if none is provided [11273478] #

**Submitted by Eric Stokes on 12/31/2015 12:00:00 AM**  
**13 votes on UserVoice prior to migration**  

In OCaml we can do,
match somrecord with
| {foo; bar; baz} -> foo + bar + baz
If we don't provide a binding, then the field name is used as the default. In F# we still have to write,
match somerecord with
| {foo=foo;bar=bar;baz=baz} -> foo + bar + baz
This is quite a simple syntactic enhancement, however it's very nice to have. It also pushes us to use the (presumably) well chosen record field names for our variables instead of picking a single letter variable name.
Also, in OCaml we get a warning if we don't bind all the record fields in a pattern match, unless we include _. e.g. {foo;bar;_}. This would be a nice thing to have as well, because in a pattern match where we DO want to bind all the fields, we are now told when the record type changes that we need to consider the new field. This is very useful for large projects.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/11273478)**


## Comments ##

