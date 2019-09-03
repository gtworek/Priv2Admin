The idea is to "translate" Windows OS privileges to a path leading to:
1. administrator,
2. integrity and/or confidentiality threat,
3. availability threat,
4. just a mess.

Privileges are listed and explained at: https://docs.microsoft.com/en-us/windows/win32/secauthz/privilege-constants

If the goal can be achived multiple ways, the priority is
1. Using built-in commands
2. Using PowerShell (only if a working script exists)
3. Using non-OS tools
4. Using any other method

You can check your own privileges with `whoami /priv`. Disabled privileges are as good as enabled ones. The only important thing is if you have the privilege on the list or not.

Feel free to contribute and/or discuss presented ideas.

| Privilege | Impact | Tool | Execution path | Remarks |
| --- | --- | --- | --- | --- |
|`SeAssignPrimaryToken`| ? | ? | ? ||
|`SeAudit`| **Threat** | 3rd party tool | Write events to the Security event log to fool auditing or to overwrite old events. |Writing own events is possible with [`AuthzReportSecurityEvent`](https://docs.microsoft.com/en-us/windows/win32/api/authz/nf-authz-authzreportsecurityevent) API. |
|`SeBackup`| **Threat** | ***Built-in commands*** | Read sensitve files with `robocopy /b` |- May be more interesting if you can read %WINDIR%\MEMORY.DMP<br> <br>- `SeBackupPrivilege` (and robocopy) is not helpful when it comes to open files.<br> <br>- Robocopy requires both SeBackup and SeRestore to work with /b parameter. |
|`SeChangeNotify`| - | - | - | Privilege held by everyone. Revoking it may make the OS (Windows Server 2019) unbootable. |
|`SeCreateGlobal`| ? | ? | ? ||
|`SeCreatePagefile`| ? | ? | ? ||
|`SeCreatePermanent`| ? | ? | ? ||
|`SeCreateSymbolicLink`| ? | ? | ? ||
|`SeCreateToken`| ***Admin*** | 3rd party tool | Create arbitrary token including local admin rights with `NtCreateToken`, use it to start a new process and take control over OS. ||
|`SeDebug`| ***Admin*** | **PowerShell** | Duplicate the `lsass.exe` token.  | Script to be found at [FuzzySecurity](https://github.com/FuzzySecurity/PowerShell-Suite/blob/master/Conjure-LSASS.ps1) |
|`SeDelegateSession-`<br>`UserImpersonate`| ? | ? | ? | Privilege name broken to make the column narrow. |
|`SeEnableDelegation`| ? | ? | ? ||
|`SeImpersonate`| ? | ? | ? ||
|`SeIncreaseBasePriority`| ? | ? | ? ||
|`SeIncreaseQuota`| ? | ? | ? ||
|`SeIncreaseWorkingSet`| ? | ? | ? ||
|`SeLoadDriver`| ? | ? | ? ||
|`SeLockMemory`| ? | ? | ? ||
|`SeMachineAccount`| ? | ? | ? ||
|`SeManageVolume`| **Threat** | 3rd party tool | Create large file and manipulate the valid data length with [`SetFileValidData()`](https://docs.microsoft.com/en-us/windows/win32/api/fileapi/nf-fileapi-setfilevaliddata). Effectively the data from deleted files should be visible inside the file. |- Files smaller than ~700B fit entirely within MFT entries and will not expose the content with such method.<br>- It looks like the privilege allows to manipulate with mbr, which may lead to some availability issues. To be investigated.|
|`SeProfileSingleProcess`| ? | ? | ? ||
|`SeRelabel`| **Threat** | 3rd party tool | Modification of system files by a legitimate administrator? | See: [MIC documentation](https://docs.microsoft.com/en-us/windows/win32/secauthz/mandatory-integrity-control)<br> <br> Integrity labels are infrequently used and work only on top of standard ACLs. Two main scenarios include:<br>- protection against attacks using exploitable applications such as browsers, PDF readers etc.<br>- protection of OS files.<br> <br>Attacks with SeRelabel must obey access rules defined by ACLs, which makes them significantly less useful in practice.|
|`SeRemoteShutdown`| Availability | ***Built-in commands*** | `shutdown /s /f /m \\server1 /d P:5:19` |The privilege is verified when shutdown/restart request comes from the network. 127.0.0.1 scenario to be investigated.|
|`SeRestore`| ***Admin*** | 3rd party tool | Critical OS file replacement. | To be investigated. Fully reproductible path needs to be tested, but I did it.|
|`SeSecurity`| **Threat** | ***Built-in commands*** |- Clear Security event log: `wevtutil cl Security`<br> <br>- Shrink the Security log to 20MB to make events flushed soon: `wevtutil sl Security /ms:0`<br> <br>- Read Security event log to have knowledge about processes, access and actions of other users within the system.<br> <br>- Knowing what is logged to act under the radar.<br> <br>- Knowing what is logged to generate large number of events effectively purging old ones without leaving obvious evidence of cleaning. ||
|`SeShutdown`| Availability | ***Built-in commands*** | `shutdown.exe /s /f /t 1` |May be more interesting on servers.|
|`SeSyncAgent`| ? | ? | ? ||
|`SeSystemEnvironment`| _Unknown_ | 3rd party tool | The privilege permits to use `NtSetSystemEnvironmentValue`, `NtModifyDriverEntry` and some other syscalls to manipulate UEFI variables. |- Firmware environment variables were commonly used on non-Intel platforms in the past, and now slowly return to UEFI world. <br>- The area is highly undocumented.<br>- The potential may be huge (i.e. breaking Secure Boot) but raising the impact level requires at least PoC. |
|`SeSystemProfile`| ? | ? | ? ||
|`SeSystemtime`| ? | ? | ? ||
|`SeTakeOwnership`| ? | ? | ? ||
|`SeTcb`| ***Admin*** | 3rd party tool | Manipulate tokens to have local admin rights included, start new process with such token and take control over OS. ||
|`SeTimeZone`| Mess | ***Built-in commands*** | Change the timezone. `tzutil /s "Chatham Islands Standard Time"` ||
|`SeTrustedCredManAccess`| ? | ? | ? ||
|`SeUndock`| ? | ? | ? ||
|`SeUnsolicitedInput`| ? | ? | ? ||
