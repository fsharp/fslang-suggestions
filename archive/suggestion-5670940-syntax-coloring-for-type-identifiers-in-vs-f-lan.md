# Syntax coloring for type identifiers in VS F# language service [5670940] #

**Submitted by Jack Pappas on 3/23/2014 12:00:00 AM**  
**9 votes on UserVoice prior to migration**  

Visual Studio supports the ability for a language service to 'tag' tokens representing type identifiers so they can be assigned custom colors by the user. C# and VB.NET both support custom coloring, which makes it trivial to tell the difference between structs and classes (for example). VB.NET supports custom colors for some other identifiers as well.
It would be nice for F# to at least support the basic coloring types (classes, delegates, interfaces, enums, generic parameters); if possible, it would be useful to add DU and record types and modules. Type abbreviations would 'inherit' the coloration of whatever type they're abbreviating.
You can see the color options in Visual Studio by going to Tools -> Options -> General -> Fonts and Colors. F# Interactive currently has it's own settings (under the "Show Settings For" drop-down), but personally I'd prefer it used the same font/color scheme as the rest of my F# code in Visual Studio. The only thing that really makes much sense to override for F# Interactive is the font size, e.g., when demonstrating on a projector.



## Response ##
** by fslang-admin on 3/27/2014 12:00:00 AM **

This suggestion belongs in Visual Studio user voice (for the Visual F# Tools) or the github issues for the Visual F# Power Tools. This user voice is for the F# language itself.


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5670940)**


## Comments ##

