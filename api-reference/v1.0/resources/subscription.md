---
title: "subscription resource type"
description: "A subscription allows a client app to receive notifications about changes to data in Microsoft Graph. Currently, subscriptions are enabled for the following resources:"
localization_priority: Priority
author: "baywet"
ms.prod: ""
doc_type: resourcePageType
---

# subscription resource type

A subscription allows a client app to receive notifications about changes to data in Microsoft Graph. Currently, subscriptions are enabled for the following resources:

- A [message][], [event][], or [contact][] in Outlook
- A [conversation][] of an Office 365 group
- Content in the hierarchy of a root folder [driveItem][] in OneDrive for Business, or of a root folder or subfolder [driveItem][] in a user's personal OneDrive
- A [user][] or [group][] in Azure Active Directory
- An [alert][] from the Microsoft Graph Security API

## Methods

| Method | Return Type | Description |
|:-------|:------------|:------------|
| [Create subscription](../api/subscription-post-subscriptions.md) | [subscription](subscription.md) | Subscribes a listener application to receive notifications when Microsoft Graph data changes. |
| [Update subscription](../api/subscription-update.md) | [subscription](subscription.md) | Renews a subscription by updating its expiration time. |
| [List subscriptions](../api/subscription-list.md) | [subscription](subscription.md) | Lists active subscriptions. |
| [Get subscription](../api/subscription-get.md) | [subscription](subscription.md) | Reads properties and relationships of subscription object. |
| [Delete subscription](../api/subscription-delete.md) | None | Deletes a subscription object. |

## Properties

| Property | Type | Description |
|:---------|:-----|:------------|
| changeType | string | Required. Indicates the type of change in the subscribed resource that will raise a notification. The supported values are: `created`, `updated`, `deleted`. Multiple values can be combined using a comma-separated list.<br><br>Note: Drive root item notifications support only the `updated` changeType. User and group notifications support `updated` and `deleted` changeType. |
| notificationUrl | string | Required. The URL of the endpoint that will receive the notifications. This URL must make use of the HTTPS protocol. |
| resource | string | Required. Specifies the resource that will be monitored for changes. Do not include the base URL (`https://graph.microsoft.com/v1.0/`). |
| expirationDateTime | [dateTime](https://tools.ietf.org/html/rfc3339) | Required. Specifies the date and time when the webhook subscription expires. The time is in UTC, and can be an amount of time from subscription creation that varies for the resource subscribed to.  See the table below for maximum supported subscription length of time. |
| clientState | string | Optional. Specifies the value of the `clientState` property sent by the service in each notification. The maximum length is 128 characters. The client can check that the notification came from the service by comparing the value of the `clientState` property sent with the subscription with the value of the `clientState` property received with each notification. |
| id | string | Unique identifier for the subscription. Read-only. |
| applicationId | string | Identifier of the application used to create the subscription. Read-only. |
| creatorId | string | Identifier of the user or service principal that created the subscription. If the app used delegated permissions to create the subscription, this field contains the id of the signed-in user the app called on behalf of. If the app used application permissions, this field contains the id of the service principal corresponding to the app. Read-only. |
| latestSupportedTlsVersion | String | Specifies the latest TLS version that the notification endpoint supports. Allows subscribers to use a deprecated version of TLS for a limited period. Possible values: **v1_0**, **v1_1**, **v1_2**, **v1_3**. Optional, defaults to v1_2. If the client endpoint supports TLS 1.2 or above this property is not needed. If the client endpoint supports only TLS 1.0 or 1.1, this property should be set to the corresponding version or the operation will fail. |

### Maximum length of subscription per resource type

| Resource            | Maximum expiration time  |
|:--------------------|:-------------------------|
| User, group, other directory resources   | 4230 minutes (under 3 days)    |
| Mail                | 4230 minutes (under 3 days)    |
| Calendar            | 4230 minutes (under 3 days)    |
| Contacts            | 4230 minutes (under 3 days)    |
| Group conversations | 4230 minutes (under 3 days)    |
| Drive root items    | 4230 minutes (under 3 days)    |
| Security alerts     | 43200 minutes (under 30 days)  |

> **Note:** Existing applications and new applications should not exceed the supported value. In the future, any requests to create or renew a subscription beyond the maximum value will fail.

## Relationships

None

## JSON representation

Here is a JSON representation of the resource.

<!--{
  "blockType": "resource",
  "optionalProperties": [],
  "baseType": "microsoft.graph.entity",
  "@odata.type": "microsoft.graph.subscription",
  "@odata.annotations": [
    {
      "capabilities": {
        "skippable": false,
        "toppable": false,
        "countable": false,
        "expandable": false,
        "filterable": false,
        "referenceable": false,
        "selectable": false,
        "sortable": false
      }
    }
  ]
}-->

```json
{
  "changeType": "string",
  "notificationUrl": "string",
  "resource": "string",
  "applicationId" : "string",
  "expirationDateTime": "String (timestamp)",
  "id": "string (identifier)",
  "clientState": "string",
  "creatorId": "string",
  "latestSupportedTlsVersion": "string"
}
```

[contact]: ./contact.md
[conversation]: ./conversation.md
[driveItem]: ./driveitem.md
[event]: ./event.md
[group]: ./group.md
[message]: ./message.md
[user]: ./user.md
[alert]: ./alert.md

<!-- uuid: 8fcb5dbc-d5aa-4681-8e31-b001d5168d79
2015-10-25 14:57:30 UTC -->
<!-- {
  "type": "#page.annotation",
  "description": "subscription resource",
  "keywords": "",
  "section": "documentation",
  "tocPath": ""
}-->
