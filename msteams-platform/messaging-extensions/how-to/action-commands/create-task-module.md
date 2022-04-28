---
title: Создание и отправка модуля задач
author: surbhigupta
description: Узнайте, как обрабатывать начальное действие вызова и отвечать с помощью модуля задачи из команды расширения сообщения о действии с помощью примеров кода и примеров.
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: bea8358edfa11dd278bdbc8ea052c61612d6db71
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104471"
---
# <a name="create-and-send-the-task-module"></a>Создание и отправка модуля задач

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

Модуль задачи можно создать с помощью адаптивной карточки или внедренного веб-представления. Чтобы создать модуль задачи, необходимо выполнить процесс, называемый начальным запросом на вызов. В этом документе описываются начальный запрос на вызов, свойства действия полезных данных при вызове модуля задачи из чата 1:1, группового чата, канала (новая запись), канала (ответа на поток) и командного поля.
> [!NOTE]
> Если модуль задач не заполняется параметрами, определенными в манифесте приложения, необходимо создать модуль задач для пользователей с помощью адаптивной карточки или внедренного веб-представления.

## <a name="the-initial-invoke-request"></a>Начальный запрос на вызов

В процессе первоначального `Activity` `composeExtension/fetchTask`запроса на вызов служба получает объект типа, `task` и необходимо ответить объектом, содержащим адаптивную карточку или URL-адрес внедренного веб-представления. Вместе со стандартными свойствами действия бота полезные данные начального вызова содержат следующие метаданные запроса:

|Имя свойства|Назначение|
|---|---|
|`type`| Тип запроса. Это должно быть `invoke`. |
|`name`| Тип команды, выданной службе. Это должно быть `composeExtension/fetchTask`. |
|`from.id`| Идентификатор пользователя, отправив запрос. |
|`from.name`| Имя пользователя, отправив запрос. |
|`from.aadObjectId`| Azure Active Directory идентификатор объекта пользователя, отправив запрос. |
|`channelData.tenant.id`| Идентификатор клиента Azure Active Directory. |
|`channelData.channel.id`| Идентификатор канала (если запрос был выполнен в канале). |
|`channelData.team.id`| Идентификатор команды (если запрос был сделан в канале). |
|`value.commandId` | Содержит идентификатор вызванной команды. |
|`value.commandContext` | Контекст, который инициирует событие. Это должно быть `compose`. |
|`value.context.theme` | Тема клиента пользователя, полезная для форматирования внедренных веб-представлений. Оно должно быть `default`или `contrast` `dark`. |

### <a name="example"></a>Пример

Код начального запроса на вызов приведен в следующем примере:

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

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-11-chat"></a>Свойства действия полезных данных при вызове модуля задачи из чата 1:1

Свойства действия полезных данных при вызове модуля задачи из чата 1:1 перечислены следующим образом:

|Имя свойства|Назначение|
|---|---|
|`type`| Тип запроса. Это должно быть `invoke`. |
|`name`| Тип команды, выданной службе. Это должно быть `composeExtension/fetchTask`. |
|`from.id`| Идентификатор пользователя, отправив запрос. |
|`from.name`| Имя пользователя, отправив запрос. |
|`from.aadObjectId`| Azure Active Directory идентификатор объекта пользователя, отправив запрос. |
|`channelData.tenant.id`| Идентификатор клиента Azure Active Directory. |
|`channelData.source.name`| Имя источника, из которого вызывается модуль задачи. |
|`ChannelData.legacy. replyToId`| Возвращает или задает идентификатор сообщения, ответом на которое является данное сообщение. |
|`value.commandId` | Содержит идентификатор вызванной команды. |
|`value.commandContext` | Контекст, который инициирует событие. Это должно быть `compose`. |
|`value.context.theme` | Тема клиента пользователя, полезная для форматирования внедренных веб-представлений. Оно должно быть `default`или `contrast` `dark`. |

### <a name="example"></a>Пример

Свойства действия полезных данных при вызове модуля задачи из чата 1:1 приведены в следующем примере:

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

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-group-chat"></a>Свойства действия полезных данных при вызове модуля задачи из группового чата

Свойства действия полезных данных при вызове модуля задачи из группового чата перечислены следующим образом:

|Имя свойства|Назначение|
|---|---|
|`type`| Тип запроса. Это должно быть `invoke`. |
|`name`| Тип команды, выданной службе. Это должно быть `composeExtension/fetchTask`. |
|`from.id`| Идентификатор пользователя, отправив запрос. |
|`from.name`| Имя пользователя, отправив запрос. |
|`from.aadObjectId`| Azure Active Directory идентификатор объекта пользователя, отправив запрос. |
|`channelData.tenant.id`| Идентификатор клиента Azure Active Directory. |
|`channelData.source.name`| Имя источника, из которого вызывается модуль задачи. |
|`ChannelData.legacy. replyToId`| Возвращает или задает идентификатор сообщения, ответом на которое является данное сообщение. |
|`value.commandId` | Содержит идентификатор вызванной команды. |
|`value.commandContext` | Контекст, который инициирует событие. Это должно быть `compose`. |
|`value.context.theme` | Тема клиента пользователя, полезная для форматирования внедренных веб-представлений. Оно должно быть `default`или `contrast` `dark`. |

### <a name="example"></a>Пример

Свойства действия полезных данных при вызове модуля задачи из группового чата приведены в следующем примере:

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

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-meeting-chat"></a>Свойства действия полезных данных при вызове модуля задачи из чата собрания

Свойства действия полезных данных при вызове модуля задачи из чата собрания приведены в следующем примере:

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

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-channel-new-post"></a>Свойства действия полезных данных при вызове модуля задачи из канала (новая запись)

Свойства действия полезных данных при вызове модуля задачи из канала (новой записи) перечислены следующим образом:

|Имя свойства|Назначение|
|---|---|
|`type`| Тип запроса. Это должно быть `invoke`. |
|`name`| Тип команды, выданной службе. Это должно быть `composeExtension/fetchTask`. |
|`from.id`| Идентификатор пользователя, отправив запрос. |
|`from.name`| Имя пользователя, отправив запрос. |
|`from.aadObjectId`| Azure Active Directory идентификатор объекта пользователя, отправив запрос. |
|`channelData.tenant.id`| Идентификатор клиента Azure Active Directory. |
|`channelData.channel.id`| Идентификатор канала (если запрос был выполнен в канале). |
|`channelData.team.id`| Идентификатор команды (если запрос был сделан в канале). |
|`channelData.source.name`| Имя источника, из которого вызывается модуль задачи. |
|`ChannelData.legacy. replyToId`| Возвращает или задает идентификатор сообщения, ответом на которое является данное сообщение. |
|`value.commandId` | Содержит идентификатор вызванной команды. |
|`value.commandContext` | Контекст, который инициирует событие. Это должно быть `compose`. |
|`value.context.theme` | Тема клиента пользователя, полезная для форматирования внедренных веб-представлений. Это должен быть `default`, `contrast`или `dark`. |

### <a name="example"></a>Пример

Свойства действия полезных данных при вызове модуля задачи из канала (новая запись) приведены в следующем примере:

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

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-channel-reply-to-thread"></a>Свойства действия полезных данных при вызове модуля задачи из канала (ответ на поток)

Свойства действия полезных данных при вызове модуля задачи из канала (ответ на поток) перечислены следующим образом:

|Имя свойства|Назначение|
|---|---|
|`type`| Тип запроса. Это должно быть `invoke`. |
|`name`| Тип команды, выданной службе. Это должно быть `composeExtension/fetchTask`. |
|`from.id`| Идентификатор пользователя, отправив запрос. |
|`from.name`| Имя пользователя, отправив запрос. |
|`from.aadObjectId`| Azure Active Directory идентификатор объекта пользователя, отправив запрос. |
|`channelData.tenant.id`| Идентификатор клиента Azure Active Directory. |
|`channelData.channel.id`| Идентификатор канала (если запрос был выполнен в канале). |
|`channelData.team.id`| Идентификатор команды (если запрос был сделан в канале). |
|`channelData.source.name`| Имя источника, из которого вызывается модуль задачи. |
|`ChannelData.legacy. replyToId`| Возвращает или задает идентификатор сообщения, ответом на которое является данное сообщение. |
|`value.commandId` | Содержит идентификатор вызванной команды. |
|`value.commandContext` | Контекст, который инициирует событие. Это должно быть `compose`. |
|`value.context.theme` | Тема клиента пользователя, полезная для форматирования внедренных веб-представлений. Оно должно быть `default`или `contrast` `dark`. |

### <a name="example"></a>Пример

Свойства действия полезных данных при вызове модуля задачи из канала (ответ на поток) приведены в следующем примере:

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

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-command-box"></a>Свойства действия полезных данных при вызове модуля задачи из командного поля

Свойства действия полезных данных при вызове модуля задачи из командного поля перечислены следующим образом:

|Имя свойства|Назначение|
|---|---|
|`type`| Тип запроса. Это должно быть `invoke`. |
|`name`| Тип команды, выданной службе. Это должно быть `composeExtension/fetchTask`. |
|`from.id`| Идентификатор пользователя, отправив запрос. |
|`from.name`| Имя пользователя, отправив запрос. |
|`from.aadObjectId`| Azure Active Directory идентификатор объекта пользователя, отправив запрос. |
|`channelData.tenant.id`| Идентификатор клиента Azure Active Directory. |
|`channelData.source.name`| Имя источника, из которого вызывается модуль задачи. |
|`value.commandId` | Содержит идентификатор вызванной команды. |
|`value.commandContext` | Контекст, который инициирует событие. Это должно быть `compose`. |
|`value.context.theme` | Тема клиента пользователя, полезная для форматирования внедренных веб-представлений. Это должен быть `default`, `contrast`или `dark`. |

### <a name="example"></a>Пример

Свойства действия полезных данных при вызове модуля задачи из командного поля приведены в следующем примере:

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

В следующем разделе кода приведен пример запроса `fetchTask` :

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

При вызове бота `value` из сообщения объект в первоначальном запросе на вызов должен содержать сведения о сообщении, из которого вызывается расширение сообщения. Массивы `reactions` `mentions` и массивы являются необязательными и отсутствуют, если в исходном сообщении нет реакций или упоминаний.
В следующем разделе приведен пример `value` объекта:

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

Ответ на запрос на вызов с помощью объекта `task` `taskInfo` , содержащего объект с адаптивной карточкой или URL-адресом веб-страницы, или простое строковое сообщение.

|Имя свойства|Назначение|
|---|---|
|`type`| Может быть либо для `continue` представления формы, либо `message` для простого всплывающего окна. |
|`value`| Объект для `taskInfo` формы или объект `string` для сообщения. |

Схема для объекта taskInfo:

|Имя свойства|Назначение|
|---|---|
|`title`| Заголовок модуля задачи.|
|`height`| Оно должно быть целым числом (в пикселях) или `small`, `medium`. `large`|
|`width`| Оно должно быть целым числом (в пикселях) или `small`, `medium`. `large`|
|`card`| Адаптивная карточка, определяющая форму (если она используется).
|`url`| URL-адрес, который должен быть открыт внутри модуля задачи в виде внедренного веб-представления.|
|`fallbackUrl`| Если клиент не поддерживает функцию модуля задач, этот URL-адрес открывается на вкладке браузера. |

### <a name="respond-to-the-fetchtask-with-an-adaptive-card"></a>Реагирование на fetchTask с помощью адаптивной карточки

При использовании адаптивной карточки необходимо `task` `value` ответить объектом, содержащим адаптивную карточку.

#### <a name="example"></a>Пример

В следующем разделе кода приведен пример ответа `fetchTask` с помощью адаптивной карточки:

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

В этом примере в дополнение к пакету SDK Bot Framework [NuGet adaptiveCards](https://www.nuget.org/packages/AdaptiveCards).

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

### <a name="create-a-task-module-with-an-embedded-web-view"></a>Создание модуля задач с внедренным веб-представлением

При использовании внедренного веб-представления `task` `value` необходимо ответить объектом, содержащим URL-адрес веб-формы, которую требуется загрузить. Домены любого URL-адреса `validDomains` , который требуется загрузить, должны быть включены в массив манифеста приложения. Дополнительные сведения о создании внедренного веб-представления см. в [документации по модулям задач](~/task-modules-and-cards/what-are-task-modules.md).

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

### <a name="request-to-install-your-conversational-bot"></a>Запрос на установку чат-бота

Если приложение содержит чат-бот, установите бот в беседе и загрузите модуль задачи. Бот полезен для получения дополнительного контекста для модуля задачи. Примером этого сценария является получение списка для заполнения элемента управления выбора людей или списка каналов в команде.

Когда расширение сообщения получит вызов `composeExtension/fetchTask` , проверьте, установлен ли бот в текущем контексте, чтобы упростить поток. Например, проверьте поток с помощью вызова get roster. Если бот не установлен, возвращает адаптивную карточку с действием, которое запрашивает у пользователя установку бота. Пользователь должен иметь разрешение на установку приложений в этом расположении для проверки. Если установка приложения завершается неудачно, пользователь получает сообщение для связи с администратором.

#### <a name="example"></a>Пример

В следующем разделе кода приведен пример ответа:

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

После установки чат-бота он получает еще одно сообщение вызова с и `name = composeExtension/submitAction``value.data.msteams.justInTimeInstall = true`.

#### <a name="example"></a>Пример

В следующем разделе кода приведен пример ответа задачи на вызов:

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

Ответ задачи на вызов должен быть аналогичен ответу установленного бота.

#### <a name="example"></a>Пример

В следующем разделе кода приведен пример JIT-установки приложения с адаптивной карточкой:

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
|Teams расширения сообщения| Описывает, как определить команды действий, создать модуль задач и реагировать на действие отправки модуля задачи. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) |
|Teams расширения сообщения   |  Описывает, как определить команды поиска и реагировать на поисковые запросы.        |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Ответ на команду действия](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)

## <a name="see-also"></a>См. также

[Определение команд действий](~/messaging-extensions/how-to/action-commands/define-action-command.md)
