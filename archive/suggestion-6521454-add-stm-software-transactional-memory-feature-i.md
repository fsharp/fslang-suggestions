# Add STM (Software Transactional Memory) feature into F# as language feature and into compiler as well [6521454] #

**Submitted by Eriawan Kusumawardhono on 10/4/2014 12:00:00 AM**  
**3 votes on UserVoice prior to migration**  

STM, Software Transactional Memory is becoming not just relevant, but it's also for handling concurrency problems. Also to provide atomicity and also provide modularity in a sense of chaining functions of operations.eazily.
Also compositional operations is easier to create and it's transparent to reason the code.
Sample in Haskell:
module Main where
import Control.Monad
import Control.Concurrent
import Control.Concurrent.STM

main = do shared <- atomically $ newTVar 0
before <- atomRead shared
putStrLn $ "Before: " ++ show before
forkIO $ 25 `timesDo` (dispVar shared >> milliSleep 20)
forkIO $ 10 `timesDo` (appV ((+) 2) shared >> milliSleep 50)
forkIO $ 20 `timesDo` (appV pred shared >> milliSleep 25)
milliSleep 800
after <- atomRead shared
putStrLn $ "After: " ++ show after
where timesDo = replicateM_
milliSleep = threadDelay . (*) 1000

atomRead = atomically . readTVar
dispVar x = atomRead x >>= print
appV fn x = atomically $ readTVar x >>= writeTVar x . fn
I gave this feedback to have 2 votes because this is very important but I understand this feature will require lots of sample cases and prototypes in the language.



## Response ##
** by fslang-admin on 10/15/2014 12:00:00 AM **

As Vasily (Basil) indicates, this is approachable as a library in F#. There is no need to add anything to the F# language (though arguably some things could be added to the .NET runtime implementations, though that’s a different matter).
Don Syme, BDFL F# Language/Core Library Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6521454)**


## Comments ##


#### Comment by Vasily Kirichenko on 10/5/2014 2:32:00 AM ####
It's approachable with computation expressions, no need for language support.
FSharpx library contains an implementation here https://github.com/fsprojects/fsharpx/blob/43400739ac8957318f256dc9f669d0276de2499a/src/FSharpx.Core/Stm.fs and the famous Santa kata ported from Haskell here https://github.com/fsprojects/fsharpx/blob/b356a656c9c718fc2ff066d3fe2207fcca552de7/docs/content/Santa.fsx

