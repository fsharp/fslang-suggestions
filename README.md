# Welcome to F# Language and Core Library Suggestions!

This site is for suggestions about the future evolution of the F# Language and Core Library.

Please read about [the F# Language and Core Library RFC Process](http://fsharp.github.io/2016/09/26/fsharp-rfc-process.html)

For discussions about tooling (editor support, compiler services etc.) please see http://fsharp.org/guides/engineering/issues.

The items marked [approved-in-principle](https://github.com/fsharp/fslang-suggestions/labels/approved%20in%20principle) for F# 4.x or beyond, and are eligible to be taken to an RFC. You can contribute detailed designs, implementation and testing for these items. See http://fsharp.github.io/2014/06/18/fsharp-contributions.html for information on contributing to the evolution of the F# Language Design and Core Library.

**Please search for an existing suggestion before opening a new one.** Just use GitHub search over the issues in this repository.

### [View all suggestions](https://github.com/fsharp/fslang-suggestions/issues?utf8=%E2%9C%93&q=is%3Aissue%20)

### [View approved-in-principle suggestions](https://github.com/fsharp/fslang-suggestions/labels/approved%20in%20principle)

### [View open suggestions](https://github.com/fsharp/fslang-suggestions/issues?q=is%3Aissue+label%3Aopen)

### [View completed suggestions](https://github.com/fsharp/fslang-suggestions/issues?q=is%3Aissue+label%3Acompleted)

### [View declined suggestions](https://github.com/fsharp/fslang-suggestions/issues?q=is%3Aissue+label%3Adeclined)

### [View suggestions with more than 100 votes](https://github.com/fsharp/fslang-suggestions/issues?utf8=%E2%9C%93&q=is%3Aissue%20is%3Aopen%20-label%3Avotes%3A0-10%20-label%3Avotes%3A11-50%20-label%3Avotes%3A51-100)

### [Create a new suggestion](https://github.com/fsharp/fslang-suggestions/issues/new)  (have you searched for existing similar suggestions?)

The decisions about moving things to "approved in principle" (and thus RFC stage) are up to the language designer ("BDFL"), Don Syme. The votes are just used as an indicator. A huge range of factors go into the decision to "approve in principle", including

* estimated utility
* estimated cost of implementing
* completeness of proposed design (is this an "idea" or a concrete suggestion)
* availability of alterenatives
* education/learning paths and simplicity
* does this give multiple ways to achieve the same thing
* votes
* design coherence
* "less is more" design considerations
* likelihood of breaking change
* strategic importance
* usefulness (or otherwise) for interop with .NET and other languages
* risk of churn w.r.t. bugs
* cost of churn w.r.t. education materials (new editions of books etc.)
* is someone stepping up to the plate to write an RFC, implement the change and own it long term?

Also we have a large queue of relatively small-cost "approved in principle" items, and large (and occasionally growing) number of bugs/issues in http://github.com/Microsoft/visualfsharp. Getting through these is also a priority.

Probably the best thing you can do to get a feature promoted is to draft an RFC on it, even if it has not yet been marked "approved". A prototype implementation to high quality, with testing, can also help convince. 
