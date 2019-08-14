The idea is to "translate" Windows OS privileges to a path leading to:
1. localadmin,
2. some other security threat,
3. just a mess.

Privileges are listed and explained at: https://docs.microsoft.com/en-us/windows/win32/secauthz/privilege-constants

If the goal can be achived multiple ways, the priority is
1. Using built-in commands
2. Using PowerShell
3. Using non-OS tools not reported by VirusTotal
4. Using any other method

Feel free to contribute and/or discuss presented ideas.

| Privilege | Impact | Tool | Execution path | Remarks |
| --- | --- | --- | --- | --- |
|`SeAssignPrimaryToken`| ? | ? | ? ||
|`SeAudit`| **Threat** | ***Built-in commands*** |- Clean Security event log: `wevtutil cl Security`<br> <br>- Shrink the Security log to 20MB to make events flushed soon: `wevtutil sl Security /ms:0` |Writing own events is possible with AuthzReportSecurityEvent API called from PowerShell|
|`SeBackup`| **Threat** | ***Built-in commands*** | Read sensitve files with `robocopy /b` |- May be more interesting if you can read %WINDIR%\MEMORY.DMP<br> <br>- SeBackupPrivilege (and robocopy) is not helpful when it comes to open files.|
|`SeChangeNotify`| ? | ? | ? ||
|`SeCreateGlobal`| ? | ? | ? ||
|`SeCreatePagefile`| ? | ? | ? ||
|`SeCreatePermanent`| ? | ? | ? ||
|`SeCreateSymbolicLink`| ? | ? | ? ||
|`SeCreateToken`| ? | ? | ? ||
|`SeDebug`| ? | ? | ? ||
|`SeDelegateSession-`<br>`UserImpersonate`| ? | ? | ? |Privilege name broken to make the column narrow.|
|`SeEnableDelegation`| ? | ? | ? ||
|`SeImpersonate`| ? | ? | ? ||
|`SeIncreaseBasePriority`| ? | ? | ? ||
|`SeIncreaseQuota`| ? | ? | ? ||
|`SeIncreaseWorkingSet`| ? | ? | ? ||
|`SeLoadDriver`| ? | ? | ? ||
|`SeLockMemory`| ? | ? | ? ||
|`SeMachineAccount`| ? | ? | ? ||
|`SeManageVolume`| ? | ? | ? ||
|`SeProfileSingleProcess`| ? | ? | ? ||
|`SeRelabel`| ? | ? | ? ||
|`SeRemoteShutdown`| ? | ? | ? ||
|`SeRestore`| ? | ? | ? ||
|`SeSecurity`| ? | ? | ? ||
|`SeShutdown`| ? | ? | ? ||
|`SeSyncAgent`| ? | ? | ? ||
|`SeSystemEnvironment`| ? | ? | ? ||
|`SeSystemProfile`| ? | ? | ? ||
|`SeSystemtime`| ? | ? | ? ||
|`SeTakeOwnership`| ? | ? | ? ||
|`SeTcb`| ? | ? | ? ||
|`SeTimeZone`| ? | ? | ? ||
|`SeTrustedCredManAccess`| ? | ? | ? ||
|`SeUndock`| ? | ? | ? ||
|`SeUnsolicitedInput`| ? | ? | ? ||
