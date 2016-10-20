# Allow Unicode symbols to be used as operators [5688398] #

**Submitted by Jerold Haas on 3/27/2014 12:00:00 AM**  
**76 votes on UserVoice prior to migration**  

Suggestion moved from https://visualstudio.uservoice.com/forums/121579-visual-studio/suggestions/2314078-allow-unicode-symbols-to-be-used-as-operators
It would be great to define mathematical operators (e.g. ∀, ∑, ∩) in F#, and be able to use other Unicode symbols (such as arrows) in operators as well. So instead of saying
let inline (!++) xs = xs |> Seq.sum
you could say
let inline (~∑) xs = xs |> Seq.sum
Writing "∑myList" is much, much easier on the eyes and brain than trying to figure out what "!++myList" does.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5688398)**


## Comments ##


#### Comment by Daniel Fabian on 3/27/2014 12:19:00 PM ####
There used to be an addon like that. http://apollo13cn.blogspot.ch/2012/09/math-unicode-symbol-add-on-for-f.html
And what stops you right now from using unicode symbols in source code (apart from being rather exotic, that is)


#### Comment by Jerold Haas on 3/27/2014 1:07:00 PM ####
That add-on is simply text substitution: There's no actual Unicode characters in the source files using that method:
"This add-on only changes the visual of the string and the source code is untouched. So if you open it in a notepad, the code won't contain any math (Unicode) symbol."


#### Comment by Mastr Mastic on 3/27/2014 8:33:00 PM ####
It makes perfect sense that this should be supported, especially for a functional language.


#### Comment by Jack Pappas on 3/28/2014 5:58:00 PM ####
This is an often-requested feature for F#, usually from people doing heavy mathematical or algorithmic work, and can see how having code which more closely adheres to the underlying math could be helpful.
However, I have to say -- I don't think it would be good for F# to add this feature. My chief concern is that you'd be forcing consumers of your code to use these symbols as well. This would be annoying at best (I prefer the identifiers as they are now, and would probably end up implementing my own library instead of one that forced me into using Unicode symbols as operators); at worst, code with Unicode operators is much less approachable for newcomers to F# -- especially those who don't come from a math/science-heavy background -- and I worry it would keep people away from F# who might otherwise be quite happy with the language.
Another drawback -- a number of mainstream development tools (including parts of VS) weren't designed with Unicode symbols in mind, and won't work properly when code or compiled assemblies use them in type/field/method names. You can make a good argument that these tools should be fixed to properly handle Unicode symbols (and I would agree with you); but if having Unicode operators means that many of the common .NET development tools couldn't be used with F# due to such issues, I think that would be a serious problem. Even well-known C# libraries have removed the uses of Unicode characters from their method names due to this issue: http://rx.codeplex.com/releases/view/114891
What's the downside of having an IDE plugin (like F# Power Tools), or the add-on Daniel linked to, that could recognize naming conventions for variables and convert them to Unicode characters in the IDE (but not in the actual code)? Proof General (an Emacs package) does this for Isar (a proof language for the Isabelle theorem prover) and it seems to work quite well: http://proofgeneral.inf.ed.ac.uk/releases/ProofGeneral-3.7/isar/isar-unicode-tokens.el


#### Comment by Steve Gilham on 4/6/2014 3:16:00 PM ####
As code like `let (<+>) = ...` compiles to an all-ASCII function name `op_LessPlusGreater` I would expect code like `let (∪) = ...` to compile to a similarly all-ASCII function name like `op_U222A` in the IL. And just as one can invoke the <+> function by ASCII name (just not as an infix), so too op_U222A could be invoked by that name if input for the mathematical symbol was difficult.
Ideally, this change would be coupled with a more general facility to define infix operators -- along the lines of ML's `infix` keyword -- but lacking a suitable reserved keyword some other syntax, maybe like `let (Union) = ...` compiling to `op_Union` would be required. Or maybe a compiler directive that when switched on made functions defined as explicitly as `op_<whatever>` invokable as infix `<whatever>`


#### Comment by Robert Nielsen on 6/22/2014 11:04:00 AM ####
Daniel Fabian the main thing that is stopping us from using unicode in the source code is the need for double-backtick marks (`` ``) to make F# understand the meaning, and even then a lot of the language constructs simply refuse to use non-normal names.


#### Comment by Don Syme on 7/18/2015 11:22:00 AM ####
I tend agree with Jack Pappas that this would not be a good thing for F#, for the reasons he describes.


#### Comment by Jared Hester on 9/26/2015 3:56:00 PM ####
What if it required a `#nowarn` and the Unicode characters supported for operators were limited to specific blocks, e.g. Mathematical Operators[1], Supplemental Mathematical Operators[2], and maybe even some of Miscellaneous Technical[3] ;)
[1] http://www.fileformat.info/info/unicode/block/mathematical_operators/utf8test.htm
[2] http://www.fileformat.info/info/unicode/block/supplemental_mathematical_operators/utf8test.htm
[3] http://www.fileformat.info/info/unicode/block/miscellaneous_technical/utf8test.htm


#### Comment by Jared Hester on 1/9/2016 3:36:00 PM ####
[ Part 2 of 2 ]
> What's the downside of having an IDE plugin (like F# Power Tools), or the add-on Daniel linked to, that could recognize naming conventions for variables and convert them to Unicode characters in the IDE (but not in the actual code)?
This downside is that this does nothing for operators. Operators are what are in question, and converting variable names does nothing to help the fact that the set of possible operators that can be created is fairly constricted and most of them are part of the language already. Not to mention between Suave, FParsec, and Freya there aren't many you can define or use without colliding fairly quickly under 3 characters. The built in precedence rules of F# only further compound these issues `^` is going to start any operator that you want to have right associativity. Swift gets this right[1], when declaring a custom operator you declare whether it's prefix, infix, or postfix; you pick whether the associativity is left, right, or none; and you set an associativity level between 0 and 255. And operators can be created from Unicode Math, Symbol, Arrow, Dingbat, line/box drawing and Unicode combining characters.[2] One additional feature that they should have included is the ability to give your operator a named
alias to use during autocomplete.
Furthermore there's not reason to create a naming convention for variables so they can be disguised as Unicode characters while rendered, because we can just use those those characters already.
These are all valid binding names:
ʀ ʁ ʂ ʃ ʄ ʅ ʆ ʇ ʈ ʉ ʊ ʋ ʌ ʍ ʎ ʏ ʐ ʑ ʒ ʓ ʔ ʕ ʖ ʗ ʘ ʙ ʚ ʛ ʜ ʝ ʞ ʟ
ɀ Ɂ ɂ Ƀ Ʉ Ʌ Ɇ ɇ Ɉ ɉ Ɋ ɋ Ɍ ɍ Ɏ ɏ ɐ ɑ ɒ ɓ ɔ ɕ ɖ ɗ ɘ ə ɚ ɛ ɜ ɝ ɞ ɟ
ɠ ɡ ɢ ɣ ɤ ɥ ɦ ɧ ɨ ɩ ɪ ɫ ɬ ɭ ɮ ɯ ɰ ɱ ɲ ɳ ɴ ɵ ɶ ɷ ɸ ɹ ɺ ɻ ɼ ɽ ɾ ɿ
ʀ ʁ ʂ ʃ ʄ ʅ ʆ ʇ ʈ ʉ ʊ ʋ ʌ ʍ ʎ ʏ ʐ ʑ ʒ ʓ ʔ ʕ ʖ ʗ ʘ ʙ ʚ ʛ ʜ ʝ ʞ ʟ
π ρ ς σ τ υ φ χ ψ ω ϊ ϋ ό ύ ώ Ϗ ϐ ϑ ϒ ϓ ϔ ϕ ϖ ϗ Ϙ ϙ Ϛ ϛ Ϝ ϝ Ϟ ϟ
Ϡ ϡ Ϣ ϣ Ϥ ϥ Ϧ ϧ Ϩ ϩ Ϫ ϫ Ϭ ϭ Ϯ ϯ ϰ ϱ ϲ ϳ ϴ ϵ
ڀ ځ ڂ ڃ ڄ څ چ ڇ ڈ ډ ڊ ڋ ڌ ڍ ڎ ڏ ڐ ڑ ڒ ړ ڔ ڕ ږ ڗ ژ ڙ ښ ڛ ڜ ڝ ڞ ڟ
ᐁ ᐂ ᐃ ᐄ ᐅ ᐆ ᐇ ᐈ ᐉ ᐊ ᐋ ᐌ ᐍ ᐎ ᐏ ᐐ ᐑ ᐒ ᐓ ᐔ ᐕ ᐖ ᐗ ᐘ ᐙ ᐚ ᐛ ᐜ ᐝ ᐞ ᐟ
Ⅰ Ⅱ Ⅲ Ⅳ Ⅴ Ⅵ Ⅶ Ⅷ Ⅸ Ⅹ Ⅺ Ⅻ Ⅼ Ⅽ Ⅾ Ⅿ ⅰ ⅱ ⅲ ⅳ ⅴ ⅵ ⅶ ⅷ ⅸ ⅹ ⅺ ⅻ ⅼ ⅽ ⅾ ⅿ
ↀ ↁ ↂ Ↄ ↄ ↅ ↆ ↇ ↈ
And for the wide swath of glyphs and characters that cause compiler errors due to unrecognized characters if you include them in your source, all you need are some backticks
``∠`` ``∡`` ``∢`` ``∣`` ``∤`` ``∥`` ``∦`` ``∧`` ``∨`` ``∩`` ``∪`` ``∫`` ``∬`` ``∭`` ``∮`` ``∯`` ``∰`` ``∱`` ``∲`` ``∳``
and you're free to use and abuse them as much as you please.
It's almost as though people fear F# will turn into APL if the operator system is improved, but it won't, because people don't want that. This is a feature that will be very beneficial to some people, and for the most part it'll have little to no effect on everyone else. But there's a still decent chance that most people will reach a point in time, maybe a few times, where having these extra capabilities was essential and incredibly useful, just like with Units Of Measure.
Let me be clear I don't want to use operators all the time, and I think that most of the time it's better and easier to understand code by using well named functions over glyph jumbles. My biggest issue with the current state of F# on this issue is it's very easy to make the worst kind code that fulfills and embodies all of the concerns people have brought up already. But there's no way to make and employ the symbols that would actually be useful.
[1] https://developer.apple.com/library/ios/documentation/Swift/Conceptual/Swift_Programming_Language/AdvancedOperators.html
[2] https://developer.apple.com/library/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/doc/uid/TP40014097-CH30-ID418


#### Comment by Jared Hester on 1/9/2016 3:37:00 PM ####
[ Part 1 of 2 ]
I disagree with the majority of Jack's points.
> My chief concern is that you'd be forcing consumers of your code to use these symbols as well.
That's the point, it's not a detrimental aspect. When working in a specialized domain the ability to use a common and familiar set of symbols is of great benefit to reducing the overall cognitive load applied to problem solving. If a developer is using these symbols in their code, the intended consumers probably want to use them as well.
> code with Unicode operators is much less approachable for newcomers to F# -- especially those who don't come from a math/science-heavy background -- and I worry it would keep people away from F# who might otherwise be quite happy with the language.
This is a completely unrealistic fear. The kinds of code it would most likely be used in are for highly domain specific math and science projects. These are not the kind of projects that newcomers to the language would be using in the first place. Even without the Unicode glyphs it'd still be unapproachable to newcomers. But that's fine, because it's not for them. We should want to have features in the language that make it more appealing to a wider group of people than it currently does, if a language as obtuse as Haskell can reach the level of popularity that it already has, I think F# will be fine with a few more options for operators.
> Another drawback -- a number of mainstream development tools (including parts of VS) weren't designed with Unicode symbols in mind, and won't work properly when code or compiled assemblies use them in type/field/method names.
Atom, Kate, Brackets, VsCode, Sublime, Vim, Emacs, XCode, Xamarin, these tools all work fine with Unicode Symbols. I use them all the time. I even added Unicode glyph support to Ionide for Atom to make it even easier to use them. Yes the tools should be fixed to handle them properly, but there's no impetus to do so if no one needs the functionality.


#### Comment by Matthew Orlando on 1/23/2016 2:49:00 PM ####
Everything Jared said. My browser (chrome on windows 10) doesn't even display all the characters he listed as valid binding names and yet... they're valid binding names. There is nothing but the fact that people are mostly sane keeping them from running amok with identifier names already. It's just certain sets of characters that seem arbitrarily excluded and would actually logically make sense in a functional language.
One of the biggest benefits of FP in general is that it's easy to make DSLs. Why would you want to artificially limit the expressiveness of those DSLs?
The structure of the arguments against adding math symbols as valid operators is identical to the arguments against allowing gay marriage. "I'm uncomfortable with it, therefore others shouldn't be allowed." "If we allow some people to start doing this, then everyone will start doing this and humanity (programmerity?) will be doomed"


#### Comment by Alan Ball on 7/29/2016 1:04:00 PM ####
Let's not forget that the link to this page already had 110 votes.


#### Comment by Alan Ball on 8/2/2016 12:57:00 PM ####
The opponents to this suggestion would have us believe that some random assortment of characters is better than a simple symbol that you can even copy and paste into google to find what it means. The idea of "substitution" where you can actually figure out what each thing is supposed to mean predictably ultimately leads to something where you have unicode names as functions, losing operator precedence.
u2211 mylist, or
set1 |> u2229 <| set2
is not easier than
∑mylist
and
set1 ∩ set2


#### Comment by Charles Roddie on 9/20/2016 4:50:00 PM ####
I think there are a few common operators which should be added to the F# spec.
≤, ≥ and ≠ are very common but quite ugly and hard to understand in F#. <= and >= are familiar to progammers but not to non-programmers, and a <= b looks more like a⇐b than a≤b. <> looks nothing like ≠ and is unintelligible to anyone who has not read the F# spec.
I think it would be close to no effort to include these as alternative syntax, and it would allow quantitative code to look a lot better.
← and → could also be treated as more concise and better looking versions of <- and ->
(Maybe ¬ ∧ ∨ for not, &&, ||, and ○ for <| too but these are less universally understood symbols.)
F# is a very expressive language. You can often write code that is basically intelligible to technical people without specific programming knowledge. For example in teaching/presenting maths you can write F# code that is universally understandable, like pseudocode, except that it actually runs. With some small tweaks to approve attractiveness, readability, and intelligibility it can be even better.


#### Comment by cj on 10/10/2016 4:10:00 PM ####
Emacs' prettify-symbols-mode partially addresses this feature request by changing the way [plain text] symbols are rendered (without touching the code) using regex substitutions. I've implemented a similar extension for vscode: https://marketplace.visualstudio.com/items?itemName=siegebell.prettify-symbols-mode.

