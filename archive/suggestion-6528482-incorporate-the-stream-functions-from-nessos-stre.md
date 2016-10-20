# Incorporate the Stream functions from Nessos/Streams into Core collections [6528482] #

**Submitted by Jack Fox on 10/6/2014 12:00:00 AM**  
**28 votes on UserVoice prior to migration**  

Efficient functional-style pipelines on streams of data. The main design behind Streams is inspired by Java 8 Streams and is based on the observation that many functional pipelines follow the pattern
source/generator |> lazy |> lazy |> lazy |> eager/reduce
Source/generator are functions that create Streams like Stream.ofArray/Stream.init.
Lazy functions take in streams and return streams like Stream.map/Stream.filter, these operations are fused together for efficient iteration.
Eager/reduce are functions like Stream.iter/Stream.sum that force the Stream to evaluate up to that point.
See https://github.com/nessos/Streams
and http://arxiv.org/abs/1406.6631



## Response ##
** by fslang-admin on 7/18/2015 12:00:00 AM **

Declining this because AFAIK Stream can’t be used as a replacement for Seq without either some semantic or performance changes. I think it is better we promote the use of Stream as a high-quality add-on library and continue to improve it.
More comments and input welcome though – perhaps Java 8 will gradually lead people to expect this in the core. But equally we have to be training people to select from available extra libraries.


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6528482)**


## Comments ##


#### Comment by Jack Fox on 10/6/2014 9:42:00 AM ####
I'm making the perhaps Naive assumption that replacing the current Core.Collections module functions with their Streams equivalents is technically feasible. This may potentially be a breaking change for some users. There is nothing preventing you from putting a side effect into the Map function, for instance. Some behavior of that side effect could change. Therefore from the point of view of semantic versioning, F# 4.0 is the right time to do this.


#### Comment by Nick Palladinos on 10/6/2014 10:38:00 AM ####
Stream has different design center than Seq but they are complementary. Seq is based on a pull model (external iteration) and Stream is based on a push model (internal iteration). As an example Seq.zip cannot be implemented in Stream as an "intermediate" combinator but it can be implemented as a producer.


#### Comment by Don Syme on 7/18/2015 11:31:00 AM ####
I don't think just replacing Seq by Stream is possible (Nick, tell me if I'm wrong), so it's unlikely we'll bring this into FSharp.Core. However I strongly encourage the use of the Nessos Stream library where appropriate.

