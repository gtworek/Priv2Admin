List of privileges required for [`NtQuerySystemInformation()`](https://docs.microsoft.com/en-us/windows/win32/api/winternl/nf-winternl-ntquerysysteminformation) calls
| SystemInformationClass | Privilege | Remarks |
| --- | --- | --- |
|SystemPlatformBinaryInformation|SeTcb||
|SystemCoverageInformation|SeDebug||
|SystemBootMetadataInformation|SeTcb||
|SystemSecureKernelProfileInformation|SeSystemProfile||
