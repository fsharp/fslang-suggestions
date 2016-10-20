# Have TypeProviderConfig.IsHostedExecution = true for type providers instantiated in *.fsx files [15462291] #

**Submitted by Dmitry Morozov on 7/29/2016 12:00:00 AM**  
**7 votes on UserVoice prior to migration**  

Have TypeProviderConfig.IsHostedExecution = true for type providers instantiated in *.fsx files
This came up in my work on FSharp.Data.SqlClient library.
Up until version 1.8.2 version of the library SqlCommandProvider provided command types with two constructors of following signatures:
new: connectionString: string, ?commandTimeout: int
new: ?connection: SqlConnection, ?transaction: SqlTransactoin, ?commandTimeout: int
Keep in mind that above are not normal F# type signatures but rather signature as suggested by Intellisense otherwise parameters with default values won’t show as optional.
It allowed to write following code:
do
use cmd = new SqlCommandProvider<"SELECT 42", "Server=.;Integrated Security=true">()
cmd.Execute()
It resolves to second constructor invocation where all parameters have default value e.g. optional.
At runtime this code reuses design time connection string to connect to a database. This is typical coding style for F# scripting (*.fsx + FSI).
For production-like scenarios connection string is read from some sort of configuration.
One way to archived that is to use connection string name from config file app.config/web.config. In that case type provider reads connection string from config file both at design time and runtime which allows to have different connection string at runtime by overriding *.config file
Pattern #1
do
use cmd = new SqlCommandProvider<"SELECT 42", " name=AdventureWorks">()
cmd.Execute()
app.config
<configuration>
<connectionStrings>
<add name="AdventureWorks" connectionString="Data Source=.;Initial Catalog=AdventureWorks2012;Integrated Security=True" />
</connectionStrings>
…
Pattern #2
The other way is override connection string or connection object at runtime
type Get42 = SqlCommandProvider<"select 42", "server=.;trusted_connection=yes">
…
Do
let connStr = readConnectionStringFromConfig()
use cmd = new SqlCommandProvider<"SELECT 42", "Server=.;Integrated Security=true">( connStr)
cmd.Execute()
Note that will resolve to invocation of first constructor.
That how it worked until 1.8.2
I got a complaint from one of the library users - Jet.com. They use pattern #2. They said the biggest source of mistakes is that developers forget to provide runtime override for connection string and it fails at runtime.
An issue was opened to reflect that
https://github.com/fsprojects/FSharp.Data.SqlClient/issues/195
And it was fixed and deployed as part of 1.8.2
To sum up the change is following: if literal connection string was used at design time, at runtime either connection string or connection object is mandatory parameter. I believe it was right change to support production quality code but it made scripting counterpart ugly and I actually received complaints from customers.
[<Literal>]
let connection = "Server=.;Integrated Security=true"
do
use cmd = new SqlCommandProvider<"SELECT 42", connection>(connection)
//connection mentioned twice. Not elegant
cmd.Execute()
It would be nice if the type provider can generate slightly different constructor signature for scripting e.g. allowing to create provided command with parameter-less ctor invocation.
I already do something similar in response to
https://github.com/fsprojects/FSharp.Data.SqlClient/issues/185
It relies on IsHostedExecution property TypeProviderConfig
https://github.com/fsprojects/FSharp.Data.SqlClient/blob/v1.8.1/src/SqlClient/Configuration.fs#L67
But it works only when a type generated within FSI. This was enough to resolve issue 185 but not sufficient to generated diff ctors signatures.
Here is my proposal:
*.fsx files mostly meant to be executed from FSI. Why not to have TypeProviderConfig.IsHostedExecution = true for type providers instantiated in *.fsx files
So type provider will able to generate diff types depending on IsHostedExecution value



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/15462291)**


## Comments ##

