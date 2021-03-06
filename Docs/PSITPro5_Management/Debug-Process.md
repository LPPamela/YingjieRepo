﻿# Debug-Process

## SYNOPSIS
Debugs one or more processes running on the local computer.

## DESCRIPTION
The Debug-Process cmdlet attaches a debugger to one or more running processes on a local computer.
You can specify the processes by their process name or process ID (PID), or you can pipe process objects to Debug-Process.

Debug-Process attaches the debugger that is currently registered for the process.
Before using this cmdlet, verify that a debugger is downloaded and correctly configured.

## PARAMETERS

### Id [Int32[]]

```powershell
[Parameter(
  Mandatory = $true,
  Position = 1,
  ValueFromPipelineByPropertyName = $true,
  ParameterSetName = 'Set 2')]
```

Specifies the process IDs of the processes to be debugged.
The parameter name ("-Id") is optional.

To find the process ID of a process, type "get-process".


### InformationAction [System.Management.Automation.ActionPreference]]

```powershell
[ValidateSet(
  'SilentlyContinue',
  'Stop',
  'Continue',
  'Inquire',
  'Ignore',
  'Suspend')]
```


To find the process ID of a process, type "get-process".


### InformationVariable [System.String]]


To find the process ID of a process, type "get-process".


### InputObject [Process[]]

```powershell
[Parameter(
  Mandatory = $true,
  ValueFromPipeline = $true,
  ParameterSetName = 'Set 3')]
```

Specifies the process objects that represent processes to be debugged.
Enter a variable that contains the process objects or a command that gets the process objects, such as a Get-Process command.
You can also pipe process objects to Debug-Process.


### Name [String[]]

```powershell
[Parameter(
  Mandatory = $true,
  Position = 1,
  ValueFromPipelineByPropertyName = $true,
  ParameterSetName = 'Set 1')]
```

Specifies the names of the processes to be debugged.
If there is more than one process with the same name, Debug-Process attaches a debugger to all processes with that name.
The parameter name ("Name") is optional.


### Confirm [switch]

Prompts you for confirmation before running the cmdlet.Prompts you for confirmation before running the cmdlet.


### WhatIf [switch]

Shows what would happen if the cmdlet runs.
The cmdlet is not run.Shows what would happen if the cmdlet runs.
The cmdlet is not run.



## INPUTS
### System.Int32, System.Diagnostics.Process, System.String

You can pipe a process ID (Int32), a process object (System.Diagnostics.Process), or a process name (String) to Debug-Process.

## OUTPUTS
### None

This cmdlet does not generate any output.

## NOTES
This cmdlet uses the AttachDebugger method of the Windows Management Instrumentation (WMI) Win32_Process class.
For more information about this method, see "AttachDebugger Method" in the [MSDN library]() at http://go.microsoft.com/fwlink/?LinkId=143640.


## EXAMPLES
### -------------------------- EXAMPLE 1 --------------------------

```powershell
PS C:\>debug-process -name powershell

```
This command attaches a debugger to the PowerShell process on the computer.






### -------------------------- EXAMPLE 2 --------------------------

```powershell
PS C:\>debug-process -name sql*

```
This command attaches a debugger to all processes that have names that begin with "sql".






### -------------------------- EXAMPLE 3 --------------------------

```powershell
PS C:\>debug-process winlogon, explorer, outlook

```
This command attaches a debugger to the Winlogon, Explorer, and Outlook processes.






### -------------------------- EXAMPLE 4 --------------------------

```powershell
PS C:\>debug-process -id 1132, 2028

```
This command attaches a debugger to the processes that have process IDs 1132 and 2028.






### -------------------------- EXAMPLE 5 --------------------------

```powershell
PS C:\>get-process powershell | debug-process

```
This command attaches a debugger to the PowerShell processes on the computer.
It uses the Get-Process cmdlet to get the PowerShell processes on the computer, and it uses a pipeline operator (|) to send the processes to the Debug-Process cmdlet.

To specify a particular PowerShell process, use the ID parameter of Get-Process.






### -------------------------- EXAMPLE 6 --------------------------

```powershell
PS C:\>$pid | debug-process

```
This command attaches a debugger to the current PowerShell processes on the computer.

It uses the $pid automatic variable, which contains the process ID of the current PowerShell process.
Then, it uses a pipeline operator (|) to send the process ID to the Debug-Process cmdlet.

For more information about the $pid automatic variable, see about_Automatic_Variables.







### -------------------------- EXAMPLE 7 --------------------------

```powershell
PS C:\>get-process -computername Server01, Server02 -name MyApp | debug-process

```
This command attaches a debugger to the MyApp processes on the Server01 and Server02 computers.

It uses the Get-Process cmdlet to get the MyApp processes on the Server01 and Server02 computers.
It uses a pipeline operator to send the processes to the Debug-Process cmdlet, which attaches the debuggers.






### -------------------------- EXAMPLE 8 --------------------------

```powershell
PS C:\>$p = get-process powershell
PS C:\>debug-process -inputobject $p

```
This command attaches a debugger to the PowerShell processes on the local computer.

The first command uses the Get-Process cmdlet to get the PowerShell processes on the computer.
It saves the resulting process object in the $p variable.

The second command uses the InputObject parameter of Debug-Process to submit the process object in the $p variable to Debug-Process.







## RELATED LINKS

[Online Version:](http://go.microsoft.com/fwlink/p/?linkid=290485)

[Debug-Process]()

[Get-Process]()

[Start-Process]()

[Stop-Process]()

[Wait-Process]()

