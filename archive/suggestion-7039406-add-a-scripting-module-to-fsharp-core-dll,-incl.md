# Add a "Scripting" module to FSharp.Core.dll, including a wget function [7039406] #

**Submitted by Don Syme on 2/1/2015 12:00:00 AM**  
**4 votes on UserVoice prior to migration**  

I suggest we add a "Scripting" module to FSharp.Core.dll (.NET Framework Version) that makes F# Interactive a more fluent and connected scripting environment
Minimally, I want enough that F# scripts can meaningfully bootstrap a connection to a package tool in a succinct header to a script. For example
open Scripting
cd __SOURCE_DIRECTORY__
if not (fileExists "paket.exe") then
wget "https://github.com/fsprojects/Paket/releases/download/0.26.2/paket.exe&quot;
;;
For example, this would enable very neat self-contained F# scripts to get and use packages: https://gist.github.com/dsyme/9c95a66a18b2c625b057
Some sample code is below - it is not complete or robust at all, and a considerable amount of discussion would be needed. Not all operations would necessarily be needed - as can be seen above, I only really feel the pain with regard to "wget". Further, the "wget" would need to be made robust with sensible defaults, e.g. See https://github.com/fsprojects/Paket/blob/master/src/Paket.Bootstrapper/Program.cs#L93-L115.
module Scripting =
let (++) a v = System.IO.Path.Combine(a, v)
let filename filePath = System.IO.Path.GetFileName(filePath)
let changext filePath ext = System.IO.Path.ChangeExtension(filePath,ext)
let extension filePath = System.IO.Path.GetExtension(filePath)
let fullpath filePath = System.IO.Path.GetFullPath(filePath)
let rootdir filePath = System.IO.Path.GetPathRoot(filePath)
let basename filePath = System.IO.Path.GetFileNameWithoutExtension(filePath)
let dirname filePath = System.IO.Path.GetDirectoryName(filePath)
let ls dirPath = System.IO.Directory.EnumerateFiles dirPath
let writeText filePath contents = System.IO.File.WriteAllText(filePath,contents)
let readText filePath = System.IO.File.ReadAllText(filePath)
let lines filePath = System.IO.File.ReadAllLines(filePath)
let linesAsSeq filePath = System.IO.File.ReadLines(filePath)
let (.>>) contents filePath = System.IO.File.AppendAllText(filePath, contents)
let (.>) contents filePath = System.IO.File.WriteAllText(filePath, contents)
let cat filePath = linesAsSeq filePath |> Seq.iter System.Console.Out.WriteLine
let echo (text:string) = System.Console.Out.WriteLine text
let wget (url:string) =
use wc = new System.Net.WebClient ()
let tmp = System.IO.Path.GetTempFileName()
wc.DownloadFile(url, tmp)
let target = filename url
System.IO.File.Move(tmp,target)

let fileExists filePath = try System.IO.File.Exists filePath with _ -> false
let cd dirPath = System.Environment.CurrentDirectory <- dirPath



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/7039406)**


## Comments ##


#### Comment by Don Syme on 2/1/2015 6:25:00 PM ####
Note, I'm not particularly attached to the Unix names and don't necessarily think we should add those to a "Scripting" module in FSharp.Core.dll. But I am attached to the idea that getting a file from the web robustly and reliably with sensible download defaults suitable for scripting should be much easier than this kind of thing: https://github.com/fsprojects/Paket/blob/master/src/Paket.Bootstrapper/Program.cs#L93-L115
That's especially because a single "web fetch" is an immensely powerful thing when it gets a .NET bootstrapping DLL which can be referenced later in the script. (In the example in the gist, initially the #r "paket.exe" reference is shown as unresolved. Once it has been downloaded by the user by executing the first part of the script the reference shows as resolved and can be evaluated).


#### Comment by Don Syme on 2/1/2015 6:40:00 PM ####
See also this sample, which shows how you can add a Paket.exe download to an F# script without needing "wget" - i.e. in a way that works today
https://gist.github.com/dsyme/9b18608b78dccf92ba33


#### Comment by Don Syme on 2/3/2016 3:02:00 PM ####
I'm closing this since few people have voted for it and it doesn't seem to be blocking people


#### Comment by Jared Hester on 6/25/2016 11:32:00 PM ####
I still think this would be really useful. Especially if it was built on top of the dotnetcore apis

