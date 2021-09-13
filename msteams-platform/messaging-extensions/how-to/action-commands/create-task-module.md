---
title: Создание и отправка модуля задач
author: surbhigupta
description: Обработка начального действия вызова и реагирование с помощью модуля задач из команды расширения обмена сообщениями действий
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 891608b2346e09570ba88ee2b868177e1aca619c
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/12/2021
ms.locfileid: "59156043"
---
# <a name="create-and-send-the-task-module"></a>Создание и отправка модуля задач

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

Модуль задач можно создать с помощью адаптивной карты или встроенного веб-представления. Чтобы создать модуль задач, необходимо выполнить процесс, называемый начальным запросом на вызов. Этот документ охватывает начальный запрос на вызов, свойства активности полезной нагрузки при вызове модуля задачи из чата 1:1, группового чата, канала (новая должность), канала (ответ на поток) и командного окна. 
> [!NOTE]
> Если вы не заполняете модуль задач параметрами, определенными в манифесте приложения, необходимо создать модуль задач для пользователей с помощью адаптивной карты или встроенного веб-представления.

## <a name="the-initial-invoke-request"></a>Начальный запрос на вызов

В процессе первоначального запроса на вызов служба получает объект типа, и необходимо ответить объектом, содержащим адаптивную карту или URL-адрес встроенного `Activity` `composeExtension/fetchTask` `task` веб-представления. Наряду со стандартными свойствами активности бота, начальная загрузка ссылок содержит следующие метаданные запроса:

|Имя свойства|Назначение|
|---|---|
|`type`| Тип запроса. Это должно быть `invoke` . |
|`name`| Тип команды, выданной службе. Это должно быть `composeExtension/fetchTask` . |
|`from.id`| ID пользователя, отправив запрос. |
|`from.name`| Имя пользователя, отправив запрос. |
|`from.aadObjectId`| Azure Active Directory объекта пользователя, отправив запрос. |
|`channelData.tenant.id`| Идентификатор клиента Azure Active Directory. |
|`channelData.channel.id`| ID канала (если запрос был сделан в канале). |
|`channelData.team.id`| Team ID (если запрос был сделан в канале). |
|`value.commandId` | Содержит ID вызываемой команды. |
|`value.commandContext` | Контекст, который вызвал событие. Это должно быть `compose` . |
|`value.context.theme` | Клиентская тема пользователя, полезная для встраиваемого форматирования веб-просмотра. Он должен быть `default` или `contrast` `dark` . |

### <a name="example"></a>Пример

Код начального запроса на вызов приводится в следующем примере:

```json
{
  "type": "invoke",
  "id": "f:bc319b1d-571a-194d-9ffb-11d7ab37c9ff",
  "from": {
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  }
  "channelData": {
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "Test",
    "commandContext": "compose",
    "requestId": "fe50f49e5c74440bb2ebf07f49e9553c",
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
```

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-11-chat"></a>Свойства активности полезной нагрузки при вызове модуля задач из чата 1:1 

Свойства активности полезной нагрузки при вызове модуля задач из чата 1:1 перечислены следующим образом:

|Имя свойства|Назначение|
|---|---|
|`type`| Тип запроса. Это должно быть `invoke` . |
|`name`| Тип команды, выданной службе. Это должно быть `composeExtension/fetchTask` . |
|`from.id`| ID пользователя, отправив запрос. |
|`from.name`| Имя пользователя, отправив запрос. |
|`from.aadObjectId`| Azure Active Directory объекта пользователя, отправив запрос. |
|`channelData.tenant.id`| Идентификатор клиента Azure Active Directory. |
|`channelData.source.name`| Имя источника, из которого вызывается модуль задач. |
|`ChannelData.legacy. replyToId`| Получает или задает ID сообщения, на которое это сообщение является ответом. |
|`value.commandId` | Содержит ID вызываемой команды. |
|`value.commandContext` | Контекст, который вызвал событие. Это должно быть `compose` . |
|`value.context.theme` | Клиентская тема пользователя, полезная для встраиваемого форматирования веб-просмотра. Он должен быть `default` или `contrast` `dark` . |

### <a name="example"></a>Пример

Свойства активности полезной нагрузки при вызове модуля задач из чата 1:1 приводятся в следующем примере:

```json
{
  "type": "invoke",
  "id": "f:bc319b1d-571a-194d-9ffb-11d7ab37c9ff",
  "from": {
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  }
  "channelData": {
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "Test",
    "commandContext": "compose",
    "requestId": "fe50f49e5c74440bb2ebf07f49e9553c",
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
}
```

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-group-chat"></a>Свойства активности полезной нагрузки при вызове модуля задач из группового чата 

Свойства активности полезной нагрузки при вызове модуля задач из группового чата перечислены следующим образом:

|Имя свойства|Назначение|
|---|---|
|`type`| Тип запроса. Это должно быть `invoke` . |
|`name`| Тип команды, выданной службе. Это должно быть `composeExtension/fetchTask` . |
|`from.id`| ID пользователя, отправив запрос. |
|`from.name`| Имя пользователя, отправив запрос. |
|`from.aadObjectId`| Azure Active Directory объекта пользователя, отправив запрос. |
|`channelData.tenant.id`| Идентификатор клиента Azure Active Directory. |
|`channelData.source.name`| Имя источника, из которого вызывается модуль задач. |
|`ChannelData.legacy. replyToId`| Получает или задает ID сообщения, на которое это сообщение является ответом. |
|`value.commandId` | Содержит ID вызываемой команды. |
|`value.commandContext` | Контекст, который вызвал событие. Это должно быть `compose` . |
|`value.context.theme` | Клиентская тема пользователя, полезная для встраиваемого форматирования веб-просмотра. Он должен быть `default` или `contrast` `dark` . |

### <a name="example"></a>Пример

Свойства активности полезной нагрузки при вызове модуля задач из группового чата приводятся в следующем примере:

```json
{
  "type": "invoke",
  "id": "f:bf72031f-a17e-f99c-48dc-5c0714950d87",
  "from": {
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "groupChat",
    "id": "19:d77be72390a1416e9644261e9064fa00@thread.skype",
    "tenantId": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
  },
  "channelData": {
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "Test",
    "commandContext": "compose",
    "requestId": "213167a1e3b6428b93e186ea5407c759",
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
}
```

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-meeting-chat"></a>Свойства активности полезной нагрузки при вызове модуля задач из чата собраний

Свойства активности полезной нагрузки при вызове модуля задач из чата собраний приводятся в следующем примере:

```json
{
   "type": "invoke",
   "id": "f:4d271f11-4eed-622f-e820-6d82bf91692f",
   "channelId": "msteams",
   "from": {
      "id": "29:1yLsdbTM1UjxqqD8cjduNUCI1jm8xZaH3lx9u5JQ04t2bknuTCkP45TXdfROTOWk1LzN1AqTgFZUEqHIVGn_qUA",
      "name": "MOD Administrator",
      "aadObjectId": "ef16aa89-5b26-4a2c-aebb-761b551577c0"
   },
   "conversation": {
      "tenantId": "c9f9aafd-64ac-4f38-8e05-12feba3fb090",
      "id": "19:meeting_NTk4ZDY4ZmYtOWEzZS00OTRkLThhY2EtZmUzZmUzMDQyM2M0@thread.v2",
      "name": "Test meeting"
   },   
   "channelData": {
      "tenant": {
         "id": "c9f9aafd-64ac-4f38-8e05-12feba3fb090"
      },
      "source": {
         "name": "compose"
      },
      "meeting": {
         "id": "MCMxOTptZWV0aW5nX05UazRaRFk0Wm1ZdE9XRXpaUzAwT1RSa0xUaGhZMkV0Wm1VelptVXpNRFF5TTJNMEB0aHJlYWQudjIjMA=="
      }
   },
   "value": {
      "commandId": "Test",
      "commandContext": "compose",
      "requestId": "c46a6b53573f42b5bc801716e5ccc960",
      "context": {
         "theme": "default"
      }
   },
   "name": "composeExtension/fetchTask",
}
```

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-channel-new-post"></a>Свойства активности полезной нагрузки при вызове модуля задач из канала (новая публикация) 

Свойства активности полезной нагрузки при вызове модуля задач из канала (новая должность) перечислены следующим образом:

|Имя свойства|Назначение|
|---|---|
|`type`| Тип запроса. Это должно быть `invoke` . |
|`name`| Тип команды, выданной службе. Это должно быть `composeExtension/fetchTask` . |
|`from.id`| ID пользователя, отправив запрос. |
|`from.name`| Имя пользователя, отправив запрос. |
|`from.aadObjectId`| Azure Active Directory объекта пользователя, отправив запрос. |
|`channelData.tenant.id`| Идентификатор клиента Azure Active Directory. |
|`channelData.channel.id`| ID канала (если запрос был сделан в канале). |
|`channelData.team.id`| Team ID (если запрос был сделан в канале). |
|`channelData.source.name`| Имя источника, из которого вызывается модуль задач. |
|`ChannelData.legacy. replyToId`| Получает или задает ID сообщения, на которое это сообщение является ответом. |
|`value.commandId` | Содержит ID вызываемой команды. |
|`value.commandContext` | Контекст, который вызвал событие. Это должно быть `compose` . |
|`value.context.theme` | Клиентская тема пользователя, полезная для встраиваемого форматирования веб-просмотра. Он должен быть `default` `contrast` , или `dark` . |

### <a name="example"></a>Пример

Свойства активности полезной нагрузки при вызове модуля задач из канала (новая должность) приводятся в следующем примере:

```json
{
  "type": "invoke",
  "id": "f:a5fbb109-c989-c449-ee83-71ac99919d4b",
  "from": {
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "channel",
    "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype",
    "name": "parsable",
    "tenantId": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
  },
  "channelData": {
    "channel": {
      "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype"
    },
    "team": {
      "id": "19:acca514e83cb497e960e0b014d405336@thread.skype"
    },
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "Test",
    "commandContext": "compose",
    "requestId": "5336640edc7748b28ce2df43f5b45963",
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
}
```

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-channel-reply-to-thread"></a>Свойства активности полезной нагрузки при вызове модуля задач из канала (ответ на поток) 

Свойства активности полезной нагрузки при вызове модуля задач из канала (ответ на поток) перечислены следующим образом:

|Имя свойства|Назначение|
|---|---|
|`type`| Тип запроса. Это должно быть `invoke` . |
|`name`| Тип команды, выданной службе. Это должно быть `composeExtension/fetchTask` . |
|`from.id`| ID пользователя, отправив запрос. |
|`from.name`| Имя пользователя, отправив запрос. |
|`from.aadObjectId`| Azure Active Directory объекта пользователя, отправив запрос. |
|`channelData.tenant.id`| Идентификатор клиента Azure Active Directory. |
|`channelData.channel.id`| ID канала (если запрос был сделан в канале). |
|`channelData.team.id`| Team ID (если запрос был сделан в канале). |
|`channelData.source.name`| Имя источника, из которого вызывается модуль задач. |
|`ChannelData.legacy. replyToId`| Получает или задает ID сообщения, на которое это сообщение является ответом. |
|`value.commandId` | Содержит ID вызываемой команды. |
|`value.commandContext` | Контекст, который вызвал событие. Это должно быть `compose` . |
|`value.context.theme` | Клиентская тема пользователя, полезная для встраиваемого форматирования веб-просмотра. Он должен быть `default` или `contrast` `dark` . |

### <a name="example"></a>Пример

Свойства активности полезной нагрузки при вызове модуля задач из канала (ответ на поток) приводятся в следующем примере:

```json
{
  "type": "invoke",
  "id": "f:19ccc884-c792-35ef-2f40-d0ff43dcca71",
  "from": {
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "channel",
    "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype;messageid=1611060744833",
    "name": "parsable",
    "tenantId": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
  },
  "channelData": {
    "channel": {
      "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype"
    },
    "team": {
      "id": "19:acca514e83cb497e960e0b014d405336@thread.skype"
    },
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "TEst",
    "commandContext": "message",
    "requestId": "7f7d22efe5414818becebcec649a7912",
    "messagePayload": {
      "linkToMessage": "https://teams.microsoft.com/l/message/19:6decf54d86d945e4b3924b63a9161a78@thread.skype/1611060744833",
      "id": "1611060744833",
      "replyToId": null,
      "createdDateTime": "2021-01-19T12:52:24.833Z",
      "lastModifiedDateTime": null,
      "deleted": false,
      "summary": null,
      "importance": "normal",
      "locale": "en-us",
      "body": {
        "contentType": "html",
        "content": "<div><div><at id=\"0\">Testing outgoing Webhook-Nikitha</at> - Hi</div>\n</div>"
      },
      "from": {
        "device": null,
        "conversation": null,
        "user": {
          "userIdentityType": "aadUser",
          "id": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc",
          "displayName": "Olo Brockhouse"
        },
        "application": null
      },
      "reactions": [],
      "mentions": [
        {
          "id": 0,
          "mentionText": "Testing outgoing Webhook-Nikitha",
          "mentioned": {
            "device": null,
            "conversation": null,
            "user": null,
            "application": {
              "applicationIdentityType": "webhook",
              "id": "b8c1c68c-e290-4bdd-81c3-266f310751dc",
              "displayName": "Testing outgoing Webhook-Nikitha"
            }
          }
        }
      ],
      "attachments": []
    },
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
}
```

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-command-box"></a>Свойства активности полезной нагрузки при вызове модуля задач из командного окна 

Свойства активности полезной нагрузки при вызове модуля задач из командного окна перечислены следующим образом:

|Имя свойства|Назначение|
|---|---|
|`type`| Тип запроса. Это должно быть `invoke` . |
|`name`| Тип команды, выданной службе. Это должно быть `composeExtension/fetchTask` . |
|`from.id`| ID пользователя, отправив запрос. |
|`from.name`| Имя пользователя, отправив запрос. |
|`from.aadObjectId`| Azure Active Directory объекта пользователя, отправив запрос. |
|`channelData.tenant.id`| Идентификатор клиента Azure Active Directory. |
|`channelData.source.name`| Имя источника, из которого вызывается модуль задач. |
|`value.commandId` | Содержит ID вызываемой команды. |
|`value.commandContext` | Контекст, который вызвал событие. Это должно быть `compose` . |
|`value.context.theme` | Клиентская тема пользователя, полезная для встраиваемого форматирования веб-просмотра. Он должен быть `default` `contrast` , или `dark` . |

### <a name="example"></a>Пример

Свойства активности полезной нагрузки при вызове модуля задач из командного окна приводятся в следующем примере:

```json
{
  "type": "invoke",
  "id": "f:172560f1-95f9-3189-edb2-b7612cd1a3cd",
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "channel",
    "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype",
    "name": "parsable",
    "tenantId": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
  },
  "channelData": {
    "channel": {
      "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype"
    },
    "team": {
      "id": "19:acca514e83cb497e960e0b014d405336@thread.skype"
    },
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "TEst",
    "commandContext": "compose",
    "requestId": "d2ce690cdc2b4920a538e75882610a30",
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
}
```

### <a name="example"></a>Пример 

В следующем разделе кода приводится пример `fetchTask` запроса:

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  //handle fetch task
}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreviewBot extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    //hand fetch task
  }
}
```

# <a name="json"></a>[JSON](#tab/json)

```json
{
  "name": "composeExtension/fetchTask",
  "type": "invoke",
  "timestamp": "2019-07-01T22:57:22.175Z",
  "localTimestamp": "2019-07-01T15:57:22.175-07:00",
  "id": "f:0123456878990178955",
  "channelId": "msteams",
  "serviceURL": "https://smba.trafficmanager.net/amer/",
  "from": {
    "id": "29:1test2GgHIa0DXzDT_OGwL5vSMZdAxDlGR7hYxZ6_JBVqHz2Zq9Nm44FUNWqHCdGBwHg8WrlFRsYrd0cCAS7dig",
    "name": "John Smith",
    "aadObjectId": "1234567d-1234-462a-8952-35b75f16f1e1"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "channel",
    "tenantId": "1234abcd-1234-12ab-12ab-35b75f16f1e1",
    "id": "19:83ed1d507cb5427c93495cf914326310@thread.skype"
  },
  "recipient": {
    "id": "28:049566e0-4401-4bcf-86a1-ce22082ce03a",
    "name": "mess"
  },
  "entities": [
    {
      "locale": "en-US",
      "country": "US",
      "platform": "Windows",
      "type": "clientInfo"
    }
  ],
  "channelData": {
    "channel": {
      "id": "19:83ab1d507cb5427c93495cf912345678@thread.skype"
    },
    "team": {
      "id": "19:83ab1d507cb5427c93495cf912345678@thread.skype"
    },
    "tenant": {
      "id": "1234abcd-1234-12ab-12ab-35b75f16f1e1"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "hello",
    "commandContext": "compose",
    "context": {
      "theme": "dark"
    }
  },
  "locale": "en-US"
}
```

* * *

## <a name="initial-invoke-request-from-a-message"></a>Начальный запрос на вызов из сообщения

Если бот вызывается из сообщения, объект в первоначальном запросе на вызов должен содержать сведения о сообщении, из которых вызывается расширение `value` обмена сообщениями. Массивы и массивы необязательны, и они не присутствуют, если в исходном сообщении нет реакций или `reactions` `mentions` упоминаний. В следующем разделе приводится пример `value` объекта:

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  var messageText = action.MessagePayload.Body.Content;
  var fromId = action.MessagePayload.From.User.Id;

  //finish handling the fetchTask
}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    const messageText = action.messagePayload.body.content;

    //finish handling the fetchTask
  }
}
```

# <a name="json"></a>[JSON](#tab/json)

```json
{
  "name": "composeExtension/submitAction",
  "type": "invoke",
...
  "value": {
    "commandId": "setReminder",
    "commandContext": "message",
    "messagePayload": {
      "id": "1111111111",
      "replyToId": null,
      "createdDateTime": "2019-02-25T21:29:36.065Z",
      "lastModifiedDateTime": null,
      "deleted": false,
      "subject": "Message subject",
      "summary": null,
      "importance": "normal",
      "locale": "en-us",
      "body": {
        "contentType": "html",
        "content": "This is the message the messaging extension was invoked from."
    },
      "from": {
        "device": null,
        "conversation": null,
        "user": {
          "userIdentityType": "aadUser",
          "id": "wxyz12ab8-ab12-cd34-ef56-098abc123876",
          "displayName": "Jamie Smythe"
        },
        "application": null
      },
      "reactions": [
        {
          "reactionType": "like",
          "createdDateTime": "2019-02-25T22:40:40.806Z",
          "user": {
            "device": null,
            "conversation": null,
            "user": {
              "userIdentityType": "aadUser",
              "id": "qrst12346-ab12-cd34-ef56-098abc123876",
              "displayName": "Jim Brown"
            },
            "application": null
          }
        }
      ],
      "mentions": [
        {
          "id": 0,
          "mentionText": "Sarah",
          "mentioned": {
            "device": null,
            "conversation": null,
            "user": {
              "userIdentityType": "aadUser",
              "id": "ab12345678-ab12-cd34-ef56-098abc123876",
              "displayName": "Sarah"
            },
            "application": null
          }
        }
      ]
    }
  ...
```

* * *

## <a name="respond-to-the-fetchtask"></a>Ответ на fetchTask

Откликнитесь на запрос на вызов с помощью объекта, который содержит объект с адаптивной картой или `task` `taskInfo` веб-URL-адресом, или простое строковом сообщении.

|Имя свойства|Назначение|
|---|---|
|`type`| Может быть либо `continue` представить форму, либо `message` простое всплывающее всплывающее. |
|`value`| Объект `taskInfo` для формы или для `string` сообщения. |

Схема объекта taskInfo заключается в:

|Имя свойства|Назначение|
|---|---|
|`title`| Название модуля задач.|
|`height`| Он должен быть либо integer (в пикселях), или `small` `medium` , , `large` .|
|`width`| Он должен быть либо integer (в пикселях), или `small` `medium` , , `large` .|
|`card`| Адаптивная карта, определяющая форму (при ее использовании).
|`url`| URL-адрес, открытый внутри модуля задач в качестве встроенного веб-представления.|
|`fallbackUrl`| Если клиент не поддерживает функцию модуля задач, этот URL-адрес открывается на вкладке браузера. |

### <a name="respond-to-the-fetchtask-with-an-adaptive-card"></a>Ответ на fetchTask с помощью адаптивной карты

При использовании адаптивной карты необходимо отвечать объектом с `task` `value` объектом, содержащим адаптивную карту.

#### <a name="example"></a>Пример

В следующем разделе кода приводится пример ответа `fetchTask` с помощью адаптивной карты:

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

В этом примере используется [пакет AdaptiveCards NuGet](https://www.nuget.org/packages/AdaptiveCards) в дополнение к SDK Bot Framework.

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  string placeholder = "Not invoked from message";

  if (action.MessagePayload != null)
  {
      var messageText = action.MessagePayload.Body.Content;
      var fromId = action.MessagePayload.From.User.Id;
      placeholder = "Invoked from message";
  }

  var response = new MessagingExtensionActionResponse()
  {
    Task = new TaskModuleContinueResponse()
    {
      Value = new TaskModuleTaskInfo()
      {
        Height = "small",
        Width = "small",
        Title = "Example task module",
        Card = new Attachment()
        {
          ContentType = AdaptiveCard.ContentType,
          Content = new AdaptiveCard("1.0")
          {
            Body = new List<AdaptiveElement>()
            {
              new AdaptiveTextInput() { Id = "FormField1", Placeholder = placeholder},
              new AdaptiveTextInput() { Id = "FormField2", Placeholder = "FormField2"},
              new AdaptiveTextInput() { Id = "FormField3", Placeholder = "FormField3"},
            },
            Actions = new List<AdaptiveAction>()
            {
              new AdaptiveSubmitAction()
              {
                Type = AdaptiveSubmitAction.TypeName,
                Title = "Submit",
              },
            },
          },
        },
      },
    },
  };
  return response;
}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
    handleTeamsMessagingExtensionFetchTask(context, action) {
      const adaptiveCard = CardFactory.adaptiveCard({
        actions: [{
          data: { submitLocation: 'messagingExtensionFetchTask'},
          title: 'Submit',
          type: 'Action.Submit'
        }],
        body: [
          { text: 'Task Module', type: 'TextBlock', weight: 'bolder'},
          { type: 'TextBlock', text: 'Enter text for Question:' },
          { id: 'Question', placeholder: 'Question text here', type: 'Input.Text', value: userText },
          { type: 'TextBlock', text: 'Options for Question:' },
          { type: 'TextBlock', text: 'Is Multi-Select:' },
          {
            choices: [{ title: 'True', value: 'true' }, { title: 'False', value: 'false' }],
            id: 'MultiSelect',
            isMultiSelect: false,
            style: 'expanded',
            type: 'Input.ChoiceSet',
            value: isMultiSelect ? 'true' : 'false'
          },
          { id: 'Option1', placeholder: 'Option 1 here', type: 'Input.Text', value: option1 },
          { id: 'Option2', placeholder: 'Option 2 here', type: 'Input.Text', value: option2 }
        ],
        type: 'AdaptiveCard',
        version: '1.0'
      });

      return {
        task: {
          type: 'continue',
          value: {
            card: adaptiveCard,
            height: 450,
            title: 'Task Module Fetch Example',
            url: null,
            width: 500
          }
        }
      };
    }
}
```

# <a name="json"></a>[JSON](#tab/json)

```json
 {
  "task": {
    "type": "continue",
    "value": {
      "title": "Task module title",
      "height": 500,
      "width": "medium",
      "card": {
        "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
        "type": "AdaptiveCard",
        "version": "1.0",
        "body": [
          {
            "type": "Input.Text",
            "placeholder": "FormField1",
            "id": "FormField1"
          },
          {
            "type": "Input.Text",
            "placeholder": "FormField2",
            "id": "FormField2"
          },
          {
            "type": "Input.Text",
            "placeholder": "FormField3",
            "id": "FormField3"
          },
          {
            "type": "ActionSet",
            "actions": [
              {
                "type": "Action.Submit",
                "title": "Action.Submit",
                "id": "submitAction"
              }
            ]
          }
        ]
      }
    }
  }
}
```

* * *

### <a name="create-a-task-module-with-an-embedded-web-view"></a>Создание модуля задач со встроенным веб-представлением

При использовании встроенного веб-представления необходимо отвечать объектом с объектом, содержащим URL-адрес, в веб-форму, которую необходимо `task` `value` загрузить. Домены любого URL-адреса, который необходимо загрузить, должны быть включены в массив `validDomains` манифеста приложения. Дополнительные сведения о создании встроенного веб-представления см. в [документации по модулям задач.](~/task-modules-and-cards/what-are-task-modules.md) 

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  string placeholder = "Not invoked from message";

  if (action.MessagePayload != null)
  {
      var messageText = action.MessagePayload.Body.Content;
      var fromId = action.MessagePayload.From.User.Id;
      placeholder = "Invoked from message";
  }

  var response = new MessagingExtensionActionResponse()
  {
    Task = new TaskModuleContinueResponse()
    {
      Value = new TaskModuleTaskInfo()
      {
        Height = "small",
        Width = "small",
        Title = "Example task module",
        Url = "https://contoso.com/msteams/taskmodules/newcustomer",
        },
      },
    },
  };
  return response;
}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    return {
      task: {
        type: 'continue',
        value: {
          width: 500,
          height: 450,
          title: 'Task Module Fetch Example',
          url: 'https://contoso.com/msteams/taskmodules/newcustomer',
          fallbackUrl: 'https://contoso.com/msteams/taskmodules/newcustomer'
        }
      }
    };
  }
}
```

# <a name="json"></a>[JSON](#tab/json)

```json
{
  "task": {
    "type": "continue",
    "value": {
      "title": "Task module title",
      "height": 500,
      "width": "medium",
      "url": "https://contoso.com/msteams/taskmodules/newcustomer",
      "fallbackUrl": "https://contoso.com/msteams/taskmodules/newcustomer"
    }
  }
}
```

* * *

### <a name="request-to-install-your-conversational-bot"></a>Запрос на установку разговорного бота

Если приложение содержит разговорный бот, установите бот в беседе и загрузив модуль задач. Бот полезен для получения дополнительного контекста для модуля задач. Примером этого сценария является извлечение списка для заполнения управления сборщиком людей или списка каналов в команде.

Когда расширение обмена сообщениями получает вызов, проверьте, установлен ли бот в текущем контексте для `composeExtension/fetchTask` облегчения потока. Например, проверьте поток с помощью вызова реестра получения. Если бот не установлен, верни адаптивную карту с действием, которое запрашивает у пользователя установку бота. Пользователь должен иметь разрешение на установку приложений в этом расположении для проверки. Если установка приложения не увенчается успехом, пользователь получает сообщение, чтобы связаться с администратором.

#### <a name="example"></a>Пример 

В следующем разделе кода приводится пример ответа:

```json
{
  "type": "AdaptiveCard",
  "body": [
    {
      "type": "TextBlock",
      "text": "Looks like you haven't used Disco in this team/chat"
    }
  ],
  "actions": [
    {
      "type": "Action.Submit",
      "title": "Continue",
      "data": {
        "msteams": {
          "justInTimeInstall": true
        }
      }
    }
  ],
  "version": "1.0"
}
```

После установки разговорного бота он получает еще одно сообщение с вызовом `name = composeExtension/submitAction` и `value.data.msteams.justInTimeInstall = true` .

#### <a name="example"></a>Пример 

В следующем разделе кода приводится пример ответа задачи на вызов:

```json
{
  "value": {
    "commandId": "giveKudos",
    "commandContext": "compose",
    "context": {
      "theme": "default"
    },
    "data": {
      "msteams": {
        "justInTimeInstall": true
      }
    }
  },
  "conversation": {
    "id": "19:7705841b240044b297123ad7f9c99217@thread.skype"
  },
  "name": "composeExtension/submitAction",
  "imdisplayname": "Bob Smith"
}
```

Ответ на вызов задачи должен быть похож на ответ установленного бота.

#### <a name="example"></a>Пример 

В следующем разделе кода приводится пример установки приложения с адаптивной картой вовремя: 

```csharp
private static Attachment GetAdaptiveCardAttachmentFromFile(string fileName)
  {
      //Read the card json and create attachment.
         string[] paths = { ".", "Resources", fileName };
         var adaptiveCardJson = File.ReadAllText(Path.Combine(paths));
         var adaptiveCardAttachment = new Attachment()
            {
                ContentType = "application/vnd.microsoft.card.adaptive",
                Content = JsonConvert.DeserializeObject(adaptiveCardJson),
            };
            return adaptiveCardAttachment;
        }
```

* * *

## <a name="code-sample"></a>Пример кода

| Имя образца           | Описание | .NET    | Node.js   |   
|:---------------------|:--------------|:---------|:--------|
|Teams расширения обмена сообщениями| Описывает, как определить команды действий, создать модуль задач и реагировать на отправку действия модуля задач. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | 
|Teams расширения обмена сообщениями   |  Описывает, как определить команды поиска и реагировать на поиски.        |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[Просмотр](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="see-also"></a>Дополнительные ресурсы

[Определение команд действий](~/messaging-extensions/how-to/action-commands/define-action-command.md)


## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"] 
> [Ответ на команду действий](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)

