//Find Settings Changes in Policies with in 30 days
IntuneAuditLogs
| where TimeGenerated >= ago (30d)
| where OperationName !contains “Assignment”
| parse Properties with * ‘,”TargetDisplayNames”:[“‘ Object ‘”],’ *
| parse Properties with * ‘”TargetDisplayNames”:[“‘IntuneProperty'”]’ * ‘,”Targets”:[{“ModifiedProperties”:[{“‘ ModifiedProperties ‘],’*
| project TimeGenerated, Identity, Object, OperationName, ModifiedProperties
