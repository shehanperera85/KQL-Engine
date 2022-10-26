//Hunt a Specific Policy for Group Assignment Changes
//Set the<Policy Name>
IntuneAuditLogs
| where OperationName contains “Assignment”
| parse Properties with * ‘”TargetDisplayNames”:[“‘IntuneProperty'”‘ * ‘Target.GroupId”,”‘ GroupAssignmentChanges ‘(‘ *
| where IntuneProperty == “<Policy_Name>”
| parse GroupAssignmentChanges with * ‘New”:”‘ Change
| project TimeGenerated, Identity, Policy=IntuneProperty, Operation=OperationName, Change
