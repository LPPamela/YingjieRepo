﻿# Test-ComputerSecureChannel

## SYNOPSIS
Tests and repairs the secure channel between the local computer and its domain.

## DESCRIPTION
The Test-ComputerSecureChannel cmdlet verifies that the secure channel between the local computer and its domain is working correctly by checking the status of its trust relationships.
If a connection fails, you can use the Repair parameter to try to restore it.

Test-ComputerSecureChannel returns "True" if the secure channel is working correctly and "False" if it is not.
This result lets you use the cmdlet in conditional statements in functions and scripts.
To get more detailed test results, use the Verbose parameter.

This cmdlet works much like NetDom.exe.
Both NetDom and Test-ComputerSecureChannel use the NetLogon service to perform the actions.

## PARAMETERS

### InformationAction [System.Management.Automation.ActionPreference]

```powershell
[Parameter(ParameterSetName = 'Set 1')]
[ValidateSet(
  'SilentlyContinue',
  'Stop',
  'Continue',
  'Inquire',
  'Ignore',
  'Suspend')]
```


To use this parameter, the current user must be a member of the Administrators group on the local computer.


### InformationVariable [System.String]

```powershell
[Parameter(ParameterSetName = 'Set 1')]
```


To use this parameter, the current user must be a member of the Administrators group on the local computer.


### Repair [switch]

```powershell
[Parameter(ParameterSetName = 'Set 1')]
```

Removes and then rebuilds the secure channel established by the NetLogon service.
Use this parameter to try to restore a connection that has failed the test (returned "False".)

To use this parameter, the current user must be a member of the Administrators group on the local computer.


### Server [String]

```powershell
[Parameter(ParameterSetName = 'Set 1')]
```

Uses the specified domain controller to run the command.
If this parameter is omitted, Test-ComputerSecureChannel selects a default domain controller for the operation.


### Credential [PSCredential]

```powershell
[Parameter(ParameterSetName = 'Set 1')]
```

Runs the command with the permissions of the specified user.
Type a user-name, such as "User01" or "Domain01\User01", or enter a PSCredential object, such as one that the Get-Credential cmdlet returns.
By default, the cmdlet uses the credentials of the current user.

The Credential parameter is designed for use in commands that use the Repair parameter to repair the secure channel between the computer and the domain.


### Confirm [switch]

```powershell
[Parameter(ParameterSetName = 'Set 1')]
```

Prompts you for confirmation before running the cmdlet.Prompts you for confirmation before running the cmdlet.


### WhatIf [switch]

```powershell
[Parameter(ParameterSetName = 'Set 1')]
```

Shows what would happen if the cmdlet runs.
The cmdlet is not run.Shows what would happen if the cmdlet runs.
The cmdlet is not run.



## INPUTS
### None

You cannot pipe input to this cmdlet.

## OUTPUTS
### System.Boolean

The cmdlet returns "True" when the connection is working correctly and "False" when it is not.

## NOTES
To run a Test-ComputerSecureChannel command on Windows Vista and later versions of Windows, open Windows PowerShell with the "Run as administrator" option.

Test-ComputerSecureChannel is implemented by using the  I_NetLogonControl2 function, which controls various aspects of the Netlogon service.


## EXAMPLES
### -------------------------- EXAMPLE 1 --------------------------

```powershell
PS C:\>test-computersecurechannel
True

```
This command tests the secure channel between the local computer and the domain to which it is joined.






### -------------------------- EXAMPLE 2 --------------------------

```powershell
PS C:\>test-computersecurechannel -server DCName.fabrikam.com
True

```
This command specifies a preferred domain controller for the test.






### -------------------------- EXAMPLE 3 --------------------------

```powershell
PS C:\>Test-ComputerSecureChannel -repair
True

```
This command resets the secure channel between the local computer and its domain.






### -------------------------- EXAMPLE 4 --------------------------

```powershell
PS C:\>test-computerSecureChannel -verbose
VERBOSE: Performing operation "Test-ComputerSecureChannel" on Target "SERVER01".
True
VERBOSE: "The secure channel between 'SERVER01' and 'net.fabrikam.com' is alive and working correctly."

```
This command uses the Verbose common parameter to request detailed messages about the operation.
For more information about the Verbose parameter, see about_CommonParameters.






### -------------------------- EXAMPLE 5 --------------------------

```powershell
PS C:\>set-alias tcsc test-computersecurechannel
if (!(tcsc))
{write-host "Connection failed. Reconnect and retry."}
else { &(.\get-servers.ps1) }

```
This example shows how to use Test-ComputerSecureChannel to test a connection before running a script that requires the connection.

The first command uses the Set-Alias cmdlet to create an alias for the cmdlet name.
This saves space and prevents typing errors.

The If statement checks the value that Test-ComputerSecureChannel returns before running a script.







## RELATED LINKS

[Online Version:](http://go.microsoft.com/fwlink/p/?linkid=293925)

[Checkpoint-Computer]()

[Reset-ComputerMachinePassword]()

[Restart-Computer]()

[Stop-Computer]()

