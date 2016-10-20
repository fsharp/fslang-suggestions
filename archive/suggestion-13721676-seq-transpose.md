# Seq.transpose [13721676] #

**Submitted by James Ashwell on 5/3/2016 12:00:00 AM**  
**14 votes on UserVoice prior to migration**  

It would be nice to have a function that transposes sequences:
[ [ 00; 01; 02;... ]; [ 10; 11; 12;... ]; [ 20; 21; 22;... ];... ]
to
[ [ 00; 10; 20;... ]; [ 01; 11; 21;... ]; [02; 12; 22;... ];... ]
This is particularly useful when dealing with infinite x infinite sequences, where you want to iterate over the 'outer group' first.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/13721676)**


## Comments ##


#### Comment by Yaar Hever on 5/9/2016 7:57:00 AM ####
I took a stab at an implementation:
module Seq =
(**)
(**)let transpose s =
(****)seq {
(******)let cachedOuter =
(********)s |> Seq.map (fun inner -> (Seq.cast inner).GetEnumerator())
(**********)|> Seq.cache
(**)
(******)let firstInner = Seq.head cachedOuter
(**)
(******)while firstInner.MoveNext() do
(********)yield seq {
(**********)yield firstInner.Current
(**********)yield! cachedOuter
(*****************)|> Seq.skip 1
(*****************)|> Seq.map (fun inner ->
(**********************)inner.MoveNext() |> ignore
(**********************)inner.Current) } }


#### Comment by Reed Adams on 6/20/2016 3:56:00 PM ####
I'm quite the sucker for code golf. My solution:
// implementation:
let transposeInfinite seqs = Seq.initInfinite(fun i -> seqs |> Seq.map (Seq.item i))
// verify:
// (inf x inf) set, each starting 10 off
let orig = Seq.initInfinite(fun i -> Seq.initInfinite((+) (i * 10)))
printfn "orig: %A\n\ntrans: %A" orig (transposeInfinite orig)

