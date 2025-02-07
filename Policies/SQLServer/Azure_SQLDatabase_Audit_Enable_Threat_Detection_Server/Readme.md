## Azure_SQLDatabase_Audit_Enable_Threat_Detection_Server

### DisplayName 
[Enable advanced data security on your SQL servers](../../../Control%20coverage/Feature/SQLServer.md#azure_sqldatabase_audit_enable_threat_detection_server)

### Required Policies
Control can be covered with Azure policies mentioned below:
- Policy to enable Microsoft Defender with Standard tier for SQL servers at Subscription level (if not enabled).
- Policy to configure email address in Microsoft Defender security contacts (if security contacts not setup as per requirements).
- Policy to enable Advanced Threat Protection (ATP) for each non-compliant SQL server.
- Policy to enable SQL auditing for each non-compliant SQL server.

___ 

#### Policy Details

Following policy will enable Microsoft Defender with Standard tier for SQL servers at Subscription scope. This will help in creation of protected resources.

#### Policy Definition
[Security - Subscription - EnableMicrosoftDefenderForSQL](Security%20-%20Subscription%20-%20EnableMicrosoftDefenderForSQL.json)

#### Parameter details

|Param Name|Description|Default Value|Mandatory?
|----|----|----|----|
| Effect | Enable or disable the execution of the policy | DeployIfNotExists |No |

___ 

#### Policy Details

Following policy will configure security contacts (email) at Subscription scope.

#### Policy Definition
[Security - Subscription - UpdateSecurityContacts](Security%20-%20Subscription%20-%20UpdateSecurityContacts.json)

#### Parameter details

|Param Name|Description|Default Value|Mandatory?
|----|----|----|----|
| Effect | Enable or disable the execution of the policy | DeployIfNotExists |No |
| EmailAddress | Email address for security contact | NA |Yes|

___ 

#### Policy Details

Following policy will enable Advanced Threat Protection (ATP) for each non-compliant SQL server.

    > **Important**: Two different policy definitions are required to cover both general SQL servers and SQL servers which are part of Synapse Workspace as policy aliases are different.  

#### Policy Definition
[Security - SQL Server - DeploySqlServerThreatDetection](Security%20-%20SQL%20Server%20-%20DeploySqlServerThreatDetection.json)

[Security - SQL Server - Synapse SQL pools - DeploySqlServerThreatDetection](Security%20-%20SQL%20Server%20-%20Synapse%20SQL%20pools%20-%20DeploySqlServerThreatDetection.json)

#### Parameter details

|Param Name|Description|Default Value|Mandatory?
|----|----|----|----|
| Effect | Enable or disable the execution of the policy | DeployIfNotExists |No |

___ 

#### Policy Details

Following policy will enable SQL auditing for each non-compliant SQL server.

    > **Important**: 
    1. Two different policy definitions are required to cover both general SQL servers and SQL servers which are part of Synapse Workspace as policy aliases are different.  
    2. In the provided resource group, Storage account will be created in each region where a SQL Server is created that will be shared by all servers in that region.
    3. Provided resource group should pre-exist in all the subscriptions (in scope), otherwise remediation will fail. 

#### Policy Definition
[Security - SQL Server - DeploySqlServerAuditSettings](Security%20-%20SQL%20Server%20-%20DeploySqlServerAuditSettings.json)

[Security - SQL Server - Synapse SQL pools - DeploySqlServerAuditSettings](Security%20-%20SQL%20Server%20-%20Synapse%20SQL%20pools%20-%20DeploySqlServerAuditSettings.json)

#### Parameter details

|Param Name|Description|Default Value|Mandatory?
|----|----|----|----|
| Effect | Enable or disable the execution of the policy | DeployIfNotExists |No |
| RetentionDays | The value in days of the retention period (0 indicates unlimited retention) | 365 |No |
| StorageAccountsResourceGroup | Resource group name for storage accounts | NA |Yes |

___ 


### Notes
1. It is recommended to assign policy to setup MDC security contacts at Subscription scope (or Management group with subscriptions managed by same team) as it will configure same email address for all subscriptions in scope.
2. It is recommended to assign policy to enable SQL auditing at Subscription scope (or Management group with subscriptions managed by same team) as it will require one existing resource group (in all subscriptions in scope) at the time of policy assignment and a Storage account will be created in each region where a SQL Server is created that will be shared by all servers (in the subscription) in that region.