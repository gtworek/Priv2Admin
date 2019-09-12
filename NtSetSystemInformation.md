List of privileges required for `NtSetSystemInformation()` calls:

| SystemInformationClass | Privilege | Remarks |
| --- | --- | --- |
|SystemFlagsInformation|SeDebug||
|SystemFlags2Information|SeDebug||
|SystemLeapSecondInformation|SeSystemtime||
|SystemTimeAdjustmentInformation|SeSystemtime||
|SystemTimeSlipNotification|SeSystemtime||
|SystemTimeZoneInformation|SeTimeZone||
|SystemDynamicTimeZoneInformation|SeTimeZone||
|SystemRegistryQuotaInformation|SeIncreaseQuota||
|SystemPrioritySeperation|SeTcb||
|SystemExtendServiceTableInformation|SeLoadDriver||
|SystemWin32WerStartCallout|SeTcb||
|SystemFileCacheInformation|SeIncreaseQuota||
|SystemFileCacheInformationEx|SeIncreaseQuota||
|SystemDpcBehaviorInformation|SeLoadDriver||
|SystemCrashDumpStateInformation|SeDebug||
|SystemVerifierInformation|SeDebug||
|SystemVerifierInformationEx|SeDebug||
|SystemVerifierAddDriverInformation|SeDebug||
|SystemVerifierRemoveDriverInformation|SeDebug||
|SystemThreadPriorityClientIdInformation|SeIncreaseBasePriority||
|SystemSpecialPoolInformation|SeDebug||
|SystemErrorPortInformation|SeTcb||
|SystemImageFileExecutionOptionsInformation|SeTcb||
|SystemCoverageInformation|SeDebug||
|SystemVerifierFaultsInformation|SeDebug||
|SystemAitSamplingValue|SeProfileSingleProcess||
|SystemScrubPhysicalMemoryInformation|SeProfileSingleProcess||
|SystemCombinePhysicalMemoryInformation|SeProfileSingleProcess||
|SystemConsoleInformation|SeLoadDriver||
|SystemBootMetadataInformation|SeTcb||
|SystemSoftRebootInformation|SeShutdown, SeTcb||
|SystemCriticalProcessErrorLogInformation|SeShutdown||
|SystemInterruptCpuSetsInformation|SeIncreaseBasePriority||
|SystemIntegrityQuotaInformation|SeDebug||
|SystemSecureDumpEncryptionInformation|SeTcb||
|SystemAffinitizedInterruptProcessorInformation|SeIncreaseBasePriority||
|SystemAllowedCpuSetsInformation|SeIncreaseBasePriority||
|SystemCpuSetTagInformation|SeIncreaseBasePriority||
|SystemWorkloadAllowedCpuSetsInformation|SeIncreaseBasePriority||
