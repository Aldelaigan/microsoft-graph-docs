﻿# mobileAppTroubleshootingAppStateHistory resource type

> **Important:** APIs under the / beta version in Microsoft Graph are in preview and are subject to change. Use of these APIs in production applications is not supported.

> **Note:** Using the Microsoft Graph APIs to configure Intune controls and policies still requires that the Intune service is [correctly licensed](https://go.microsoft.com/fwlink/?linkid=839381) by the customer.

History Item contained in the Mobile App Troubleshooting Event.

Inherits from [mobileAppTroubleshootingHistoryItem](../resources/intune_troubleshooting_mobileapptroubleshootinghistoryitem.md)

## Properties
|Property|Type|Description|
|:---|:---|:---|
|occurrenceDateTime|DateTimeOffset|Time when the history item occurred. Inherited from [mobileAppTroubleshootingHistoryItem](../resources/intune_troubleshooting_mobileapptroubleshootinghistoryitem.md)|
|actionType|[mobileAppActionType](../resources/intune_troubleshooting_mobileappactiontype.md)|AAD security group id to which it was targeted. Possible values are: `unknown`, `installCommandSent`, `installed`, `uninstalled`, `userRequestedInstall`.|
|runState|[runState](../resources/intune_shared_runstate.md)|Status of the item. Possible values are: `unknown`, `success`, `fail`.|
|errorCode|String|Error code for the failure, empty if no failure.|

## Relationships
None
## JSON Representation
Here is a JSON representation of the resource.
<!-- {
  "blockType": "resource",
  "@odata.type": "microsoft.graph.mobileAppTroubleshootingAppStateHistory"
}
-->
``` json
{
  "@odata.type": "#microsoft.graph.mobileAppTroubleshootingAppStateHistory",
  "occurrenceDateTime": "String (timestamp)",
  "actionType": "String",
  "runState": "String",
  "errorCode": "String"
}
```



