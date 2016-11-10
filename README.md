# Welcome to F# Language and Core Library Suggestions!

This site is for suggestions about the future evolution of the F# Language and Core Library. Please read about [the F# Language and Core Library RFC Process](http://fsharp.github.io/2016/09/26/fsharp-rfc-process.html). For discussions about tooling (editor support, compiler services etc.) please see http://fsharp.org/guides/engineering/issues.

**Voting is by giving :thumbsup: reactions to an issue.** 

The items marked [approved-in-principle](https://github.com/fsharp/fslang-suggestions/labels/approved%20in%20principle) for F# 4.x or beyond, are eligible to be taken to an RFC. You can contribute detailed designs, implementation and testing for these items. See http://fsharp.github.io/2014/06/18/fsharp-contributions.html for information on contributing to the evolution of the F# Language Design and Core Library.

**Please search for an existing suggestion before opening a new one.** Just use GitHub search over the issues in this repository.

### [View all suggestions](https://github.com/fsharp/fslang-suggestions/issues?utf8=%E2%9C%93&q=is%3Aissue%20)

### [View popular suggestions (votes by :thumbsup:)](https://github.com/fsharp/fslang-suggestions/issues?q=is%3Aissue+is%3Aopen+sort%3Areactions-%2B1-desc)

### [View newest suggestions](https://github.com/fsharp/fslang-suggestions/issues?q=is%3Aissue+is%3Aopen+sort%3Acreated-desc)

### [View approved-in-principle suggestions](https://github.com/fsharp/fslang-suggestions/labels/approved%20in%20principle)

### [View started suggestions](https://github.com/fsharp/fslang-suggestions/labels/started)

### [View open suggestions (language)](https://github.com/fsharp/fslang-suggestions/issues?utf8=%E2%9C%93&q=is%3Aissue%20is%3Aopen%20-label%3A%22approved%20in%20principle%22%20-label%3Astarted%20-label%3A%22area%3A%20library%22)

### [View open suggestions (core library)](https://github.com/fsharp/fslang-suggestions/issues?utf8=%E2%9C%93&q=is%3Aissue%20is%3Aopen%20-label%3A%22approved%20in%20principle%22%20-label%3Astarted%20label%3A%22area%3A%20library%22%20)

### [View completed suggestions](https://github.com/fsharp/fslang-suggestions/issues?q=is%3Aissue+label%3Acompleted)

### [View declined suggestions](https://github.com/fsharp/fslang-suggestions/issues?q=is%3Aissue+label%3Adeclined)

### [Create a new suggestion](https://github.com/fsharp/fslang-suggestions/issues/new)  (have you searched for existing similar suggestions?)

## Notes on the Design Process

We do not in general revisit design decisions that have already been decided. In particular there is a distinction between

1. things we have previousy decided "not to do"
2. things where we decided to do X, considered Y, and by doing X implicitly decided not to do Y
3. things we thought about doing andd left open the future possibility of doing them
4. things we never thought of before

Most of the existing open suggestions are in category 3 or 4. In general things in categories 1 and 2 won't be reconsidered unless there is a really very strong case, e.g. because of a change in circumstance. Many suggestions will thus be closed with responses like "we considered this in F# 2.0 and decided against this".  The design notes for F# 2.0-3.0 are only available in email form, we will gradually try to make them available from our archives.

The decisions about moving things to "approved in principle" (and thus RFC stage) are up to the language designer ("BDFL"), Don Syme. The votes are just used as an indicator. A huge range of factors go into the decision to "approve in principle", including:

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

Also we have a large queue of relatively small-cost "approved in principle" items, and a large (and occasionally growing) number of bugs/issues in http://github.com/Microsoft/visualfsharp. Getting through these is also a priority.

## When are new features a good thing?

Adding endless new language features in every version has major downsides.  Here are some observations on why adding features is not necessarily a good thing:

1. Stability is a virtue
2. _Gradual_ evolution is good
3. Adding new language features on every version is not a necessarily a sign of strength.  Many languages have spread very widely while remaining very stable (e.g. Java in 2000-2013)
4. The addition of new features on every version can be a sign that language implementors are being incentivized (e.g. getting paid) for feature-completion rather than overall simplicity and utility.
5. New features add learning costs to every user of the language

In contrast, features which make the language more orthogonal, simpler and easier to use are generally a very good thing.

## How do I get my favourite feature approved?

First make sure the issue for your feature is really clear and addresses all major concerns.

Probably the best thing you can do to get a feature promoted is to draft an RFC on it, even if it has not yet been marked "approved". A prototype implementation of high quality, with tests, can also help convince. 


