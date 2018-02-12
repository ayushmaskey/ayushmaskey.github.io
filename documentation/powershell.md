<#commands#>

$host - get host information

ls - same as dir
Host |get-member | more -  method and property of host and more give it on pages
"Hello World" | get-member | more - method and property of string
Get-Verb - all the verb available
Get-Verb | Out-GridView - in separate window
man Get-Member | more -  gets manual of properties and method of an object. Here the object is Get-Member
update-help -  update help file. need to run as admin
Get-Process - all the process running in windows
Get-Process | Stop-Process - whatif | more - what happens if you use the given commands
Get-Process *Chrome* - all the process for chrome

function simple one helloworld.ps1
to run it
.\helloworld.ps1 or h and then tab. need path to the file

Get-ExecutionPolicy - default is restricted mode
get-Help about_Execution_Policies
Set-ExecutionPolicy -ExecutionPolicy Restricted - change execution policy

