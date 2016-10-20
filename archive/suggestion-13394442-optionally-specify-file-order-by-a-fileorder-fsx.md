# Optionally specify file order by a fileorder.fsx (or fileorder.txt or fileorder.json) file [13394442] #

**Submitted by Don Syme on 4/12/2016 12:00:00 AM**  
**20 votes on UserVoice prior to migration**  

With F# becoming more and more multi-editor and cross-platform, it is becoming increasingly difficult to teach all build/edit tools about F#'s file order. The F# community are currently struggling to "update" each new build/edit tool to understand that F# actually needs a file order.
Part of the problem is that there is no standard textual way to specify this file order except as command line arguments, and these are not stored in an editable form. There is no standard way to specify the F# file order. We need an (optional) solution to this problem that is closer to home and doesn't involve modifying build/edit tools.
This proposal is one of three alternatives to deal with this problem in the F# language/compiler itself.
The specific proposal covered by this UV entry is to allow the F# compiler to optionally take a special file, tentatively called fileorder.fsx, which specifies the file order E.g.
fileorder.fsx:
#load "Directory/a.fs"
#load "b.fs"
(We could instead use a fileorder.txt or fileorder.json – discuss).
This would be given to the F# compiler as a command-line input and otherwise everything would work as it does today.
Rules
- File references can be given in any order on the command-line.
- If present, the file order is taken from fileorder.fsx
- Using fileorder.fsx is optional
- fileorder.fsx would be hand-authored by the user
- An error would be given if fileorder.fsx doesn’t list all the files in the compilation.
Questions:
- Would we use a fileorder.fsx or fileorder.txt
- We need a way to refer to things like “obj/Debug/pars.fs” that are the intermediate outputs of other actions. I suggest wildcards
#load "obj/*/pars.fs"
Here the meaning of wildcards is “all the inputs that match” not “all the files on disk that match”.
Disadvantages:
- It’s at least as tasteless than “#load/#require”
- It requires manual editing
Advantages:
- Single place of reference for file order.
- Requires no changes to F# language, “it just works” with any editor
- We could augment the F# compiler to automatically write out a fileorder.fsx if one doesn’t exist, which would allow the user to gradually switch to this model.
Related alternative: Allow all declarations to be mutually referential and the compiler takes files in any order /archive/suggestion-10276974-allow-the-compiler-to-take-source-code-files-in-an
Related alternative: Keep a file order, but infer it from #load/#require declarations. This is covered by /archive/suggestion-6323146-syntactically-describe-dependencies-between-files



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/13394442)**


## Comments ##


#### Comment by Kevin Ransom on 4/12/2016 12:43:00 PM ####
I’m afraid this proposal does not resonate with me. It has a number of deficiencies in my opinion:
1. It repeats information stored elsewhere in every other build system:
• Fake specifies a source file ordering
• Msbuild projects specify source file ordering
• Project.json specifies a source file ordering
2. For a loose collection of F# files in a directory this ordering needs to be specified anyway and so the scenario we are trying to address is not really addressed, I think project.json is as good a way to specify it as an F# file as any
3. I agree with Jared that specifying a source files requirements is a more natural, and source code reuse friendly mechanism for specifying dependencies.
4. A project file can contain a file with the same name in two different directories and so the dependency will need to be path qualified again making the file less friendly in reuse scenarios
5. We already have a model for script files based on #load … this is not aligned with that approach.
• I actually prefer #requires “foo.fs”, and a topological sort, it certainly degenerates in to a form that satisfies this proposal, although there is a preprocessing step that requires opening and reading all of the files which will slow down builds a tad. We can also allow #requires to be a synonym for #load allowing script files to build correctly.
6. I also think that we can probably write a tool that integrates with the dotnet new that reads the source code for loose files and looks at type dependencies and open statements and performs a topological sort that will work. Because it is just a tool, it wouldn’t pollute the compiler and would only run on dotnet new, or when other tooling invoked it.
And so …
I think we need to either :
1. Do nothing … require developers to specify file ordering in project.json
a. Perhaps write a tool
2. Or add #requires “foo.fs” and do a topologival sort to specify dependencies.
Kevin


#### Comment by Gauthier Segay on 4/17/2016 8:02:00 PM ####
Don, have you considered that fsc now takes a response file?
I think the tooling issue is becoming manageable, for the widespread msbuild project files there is fsprojects/forge tool, and I think support for project.json will be added when it matures.
As for json file in your suggestion, I really don't think json is a human readable format, it is great when you have javascript on one side but that is about it, writing a json file by hand is tedious compared to a more human friendly format (see the file formats used by paket).
A precompiler directive solution (#require) seems also like a good way to have that made explicit in the source, I think this approach could be studied (with an extra tool as Kevin mentions), but would require some tooling or compiler support (we want error message if a file doesn't exist).


#### Comment by Jared Hester on 6/27/2016 11:28:00 PM ####
JSON presents several issues for use as a configuration file
- doesn't support comments
- no bare keys
- fussy commas
- the abundance of braces make nesting hard to read at a glance and files tedious to edit
- no multi-line strings
- no literal strings (fully escaped)
- only floats, no integers
- no dateTime standard
A much better choice would be TOML[1] (Rust's choice for Cargo[2]) which addresses all of the issues listed above and every vaild TOML file maps directly to a HashTable.
CSON[3] addresses most of JSON's issues, but it doesn't do it as well as TOML does.
YAML[4] is another option, although it's more sane to read and write than JSON, it's unnecessarily complex and much more than is necessary for a project config. A subset of yaml could be used, but that adds another set of issues, so whether it'd be better than JSON in any form is up for debate.
So really just use TOML or CSON and please not JSON
[1] https://github.com/toml-lang/toml
[2] http://doc.crates.io/manifest.html#the-project-layout
[3] https://github.com/bevry/cson#what-is-cson
[4] https://en.wikipedia.org/wiki/YAML#Sample_document


#### Comment by Nestor Demeure on 7/4/2016 11:51:00 AM ####
This post might interest you :
http://kcieslak.io/Creating-custom-project-file-for-F
As far as I know, that tool is currently being design :)

