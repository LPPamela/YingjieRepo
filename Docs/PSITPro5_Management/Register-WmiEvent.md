﻿# Register-WmiEvent

## SYNOPSIS
Subscribes to a Windows Management Instrumentation (WMI) event.

## DESCRIPTION
The Register-WmiEvent cmdlet subscribes to WMI events on the local computer or on a remote computer.

When the subscribed WMI event is raised, it is added to the event queue in your local session even if the event occurs on a remote computer.
To get events in the event queue, use the Get-Event cmdlet.

You can use the parameters of Register-WmiEvent to subscribe to events on remote computers and to specify the property values of the events that can help you to identify the event in the queue.
You can also use the Action parameter to specify actions to take when a subscribed event is raised.

When you subscribe to an event, an event subscriber is added to your session.
To get the event subscribers in the session, use the Get-EventSubscriber cmdlet.
To cancel the subscription, use the Unregister-Event cmdlet, which deletes the event subscriber from the session.

New CIM cmdlets, introduced Windows PowerShell 3.0, perform the same tasks as the WMI cmdlets.
The CIM cmdlets comply with WS-Management (WSMan) standards and with the Common Information Model (CIM) standard, which enables the cmdlets to use the same techniques to manage Windows computers and those running other operating systems.
Instead of using Register-WmiEvent, consider using the [Register-CimIndicationEvent]() cmdlet.

## PARAMETERS

### Action [ScriptBlock]

```powershell
[Parameter(Position = 102)]
```

Specifies commands that handle the events.
The commands in the Action parameter run when an event is raised instead of sending the event to the event queue.
Enclose the commands in braces ( { } ) to create a script block.

The value of the Action parameter can include the $Event, $EventSubscriber, $Sender, $EventArgs, and $Args automatic variables, which provide information about the event to the Action script block.
For more information, see about_Automatic_Variables.

When you specify an action, Register-WmiEvent returns an event job object that represents that action.
You can use the cmdlets that contain the Job noun (the Job cmdlets) to manage the event job.


### Class [String]

```powershell
[Parameter(
  Mandatory = $true,
  Position = 1,
  ParameterSetName = 'Set 1')]
```

Specifies the event to which you are subscribing.
Enter the WMI class that generates the events.
A Class or Query parameter is required in every command.


### ComputerName [String]

Runs the command on the specified computer.
The default is the local computer.

Type the NetBIOS name, an IP address, or a fully qualified domain name of the computer.
To specify the local computer, type the computer name, a dot (.), or "localhost".

This parameter does not rely on Windows PowerShell remoting.
You can use the ComputerName parameter even if your computer is not configured to run remote commands.


### Credential [PSCredential]

Specifies a user account that has permission to perform this action.
Type a user name, such as "User01" or "Domain01\User01".
Or, enter a PSCredential object, such as one from the Get-Credential cmdlet.
If you type a user name, you will be prompted for a password.


### Forward [switch]

Sends events for this subscription to the session on the local computer.
Use this parameter when you are registering for events on a remote computer or in a remote session.


### InformationAction [System.Management.Automation.ActionPreference]

```powershell
[ValidateSet(
  'SilentlyContinue',
  'Stop',
  'Continue',
  'Inquire',
  'Ignore',
  'Suspend')]
```


The value of the Action parameter can include the $Event, $EventSubscriber, $Sender, $EventArgs, and $Args automatic variables, which provide information about the event to the Action script block.
For more information, see about_Automatic_Variables.

When you specify an action, Register-WmiEvent returns an event job object that represents that action.
You can use the cmdlets that contain the Job noun (the Job cmdlets) to manage the event job.


### InformationVariable [System.String]


The value of the Action parameter can include the $Event, $EventSubscriber, $Sender, $EventArgs, and $Args automatic variables, which provide information about the event to the Action script block.
For more information, see about_Automatic_Variables.

When you specify an action, Register-WmiEvent returns an event job object that represents that action.
You can use the cmdlets that contain the Job noun (the Job cmdlets) to manage the event job.


### MaxTriggerCount [System.Int32]


The value of the Action parameter can include the $Event, $EventSubscriber, $Sender, $EventArgs, and $Args automatic variables, which provide information about the event to the Action script block.
For more information, see about_Automatic_Variables.

When you specify an action, Register-WmiEvent returns an event job object that represents that action.
You can use the cmdlets that contain the Job noun (the Job cmdlets) to manage the event job.


### MessageData [PSObject]

Specifies any additional data to be associated with this event subscription.
The value of this parameter appears in the MessageData property of all events associated with this subscription.


### Namespace [String]

Specifies the namespace of the WMI class.


### Query [String]

```powershell
[Parameter(
  Mandatory = $true,
  Position = 1,
  ParameterSetName = 'Set 2')]
```

Specifies a query in WMI Query Language (WQL) that identifies the WMI event class, such as "select * from __InstanceDeletionEvent".


### SourceIdentifier [String]

```powershell
[Parameter(Position = 101)]
```

Specifies a name that you select for the subscription.
The name that you select must be unique in the current session.
The default value is the GUID that Windows PowerShell assigns.

The value of this parameter appears in the value of the SourceIdentifier property of the subscriber object and of all event objects associated with this subscription.


### SupportEvent [switch]

Hides the event subscription.
Use this parameter when the current subscription is part of a more complex event registration mechanism and it should not be discovered independently.

To view or cancel a subscription that was created with the SupportEvent parameter, use the Force parameter of the Get-EventSubscriber and Unregister-Event cmdlets.


### Timeout [Int64]

Determines how long Windows PowerShell waits for this command to complete.

The default value, 0 (zero), means that there is no time-out, and it causes Windows PowerShell to wait indefinitely.



## INPUTS
### None

You cannot pipe objects to Register-WmiEvent.

## OUTPUTS
### None

This cmdlet does not generate any output.

## NOTES
To use this cmdlet in Windows Vista or a later version of Windows, start Windows PowerShell with the "Run as administrator" option.

Events, event subscriptions, and the event queue exist only in the current session.
If you close the current session, the event queue is discarded and the event subscription is canceled.


## EXAMPLES
### -------------------------- EXAMPLE 1 --------------------------

```powershell
PS C:\>register-wmiEvent -class 'Win32_ProcessStartTrace' -sourceIdentifier "ProcessStarted"

```
This command subscribes to the events generated by the Win32_ProcessStartTrace class.
This class raises an event whenever a process starts.






### -------------------------- EXAMPLE 2 --------------------------

```powershell
PS C:\>register-wmiEvent -query "select * from __instancecreationevent within 5 where targetinstance isa 'win32_process'" -sourceIdentifier "WMIProcess" -messageData "Test 01" -timeout 500

```
This command uses a query to subscribe to Win32_process instance creation events.






### -------------------------- EXAMPLE 3 --------------------------

```powershell
PS C:\>$action = { get-history | where { $_.commandline -like "*start-process*" } | export-cliXml "commandHistory.clixml" }
PS C:\>register-wmiEvent -class 'Win32_ProcessStartTrace' -sourceIdentifier "ProcessStarted" -action $action

Id    Name            State      HasMoreData   Location  Command
--    ----            -----      -----------   --------  -------
1     ProcessStarted  NotStarted False                   get-history | where {...

```
This example shows how to use an action to respond to an event.
In this case, when a process starts, any Start-Process commands in the current session are written to an XML file.

When you use the Action parameter, Register-WmiEvent returns a background job that represents the event action.
You can use the Job cmdlets, such as Get-Job and Receive-Job, to manage the event job.

For more information, see about_Jobs.






### -------------------------- EXAMPLE 4 --------------------------

```powershell
PS C:\>register-wmiEvent -class 'Win32_ProcessStartTrace' -sourceIdentifier "Start" -computername Server01
PS C:\>get-event -sourceIdentifier "Start"

```
This example registers for events on the Server01 remote computer.

WMI returns the events to the local computer and stores them in the event queue in the current session.
To retrieve the events, run a local Get-Event command.







## RELATED LINKS

[Online Version:](http://go.microsoft.com/fwlink/p/?linkid=293893)

[Get-Event]()

[New-Event]()

[Register-EngineEvent]()

[Register-ObjectEvent]()

[Remove-Event]()

[Unregister-Event]()

[Wait-Event]()

