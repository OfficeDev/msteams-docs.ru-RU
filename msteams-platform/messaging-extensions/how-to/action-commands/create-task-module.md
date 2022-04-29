---
title: Создание и отправка модуля задач
author: surbhigupta
description: Узнайте, как обрабатывать действие начального вызова и отвечать с помощью модуля задач из команды расширения для сообщений о действиях с использованием примеров кода и образцов.
ms.localizationpriority: high
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 5daf262bfad3c88477ec0a1104e45b7cb9848aac
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2022
ms.locfileid: "65110353"
---
# <a name="create-and-send-the-task-module"></a>Создание и отправка модуля задач

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

Модуль задач можно создать с помощью адаптивной карточки или внедренного веб-представления. Чтобы создать модуль задач, необходимо выполнить процесс, называемый запросом начального вызова. В этом документе описываются запрос начального вызова, свойства действий полезных данных при вызове модуля задач из индивидуального чата, группового чата, канала (новая публикация), канала (ответ в беседе) и командного поля.
> [!NOTE]
> Если модуль задач не заполняется параметрами, определенными в манифесте приложения, необходимо создать модуль задач для пользователей с помощью адаптивной карточки или внедренного веб-представления.

## <a name="the-initial-invoke-request"></a>Запрос начального вызова

В процессе запроса начального вызова ваша служба получает объект `Activity` типа `composeExtension/fetchTask`, и вы должны ответить с использованием объекта `task`, содержащего адаптивную карточку или URL-адрес внедренного веб-представления. Вместе со стандартными свойствами действий бота полезные данные начального вызова содержат следующие метаданные запроса.

|Имя свойства|Назначение|
|---|---|
|`type`| Тип запроса. Должно применяться значение `invoke`. |
|`name`| Тип команды, выпущенной для вашей службы. Должно применяться значение `composeExtension/fetchTask`. |
|`from.id`| Идентификатор пользователя, отправившего запрос. |
|`from.name`| Имя пользователя, отправившего запрос. |
|`from.aadObjectId`| Идентификатор объекта Azure Active Directory пользователя, отправившего запрос. |
|`channelData.tenant.id`| Идентификатор клиента Azure Active Directory. |
|`channelData.channel.id`| Идентификатор канала (если запрос был выполнен в канале). |
|`channelData.team.id`| Идентификатор команды (если запрос был выполнен в канале). |
|`value.commandId` | Содержит идентификатор вызванной команды. |
|`value.commandContext` | Контекст, инициировавший событие. Должно применяться значение `compose`. |
|`value.context.theme` | Тема клиента пользователя. Удобно при форматировании внедренного веб-представления. Должно применяться значение `default`, `contrast` или `dark`. |

### <a name="example"></a>Пример

Код запроса начального вызова приведен в следующем примере.

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

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-11-chat"></a>Свойства действий полезных данных при вызове модуля задач из индивидуального чата

Свойства действий полезных данных при вызове модуля задач из индивидуального чата перечислены ниже.

|Имя свойства|Назначение|
|---|---|
|`type`| Тип запроса. Должно применяться значение `invoke`. |
|`name`| Тип команды, выпущенной для вашей службы. Должно применяться значение `composeExtension/fetchTask`. |
|`from.id`| Идентификатор пользователя, отправившего запрос. |
|`from.name`| Имя пользователя, отправившего запрос. |
|`from.aadObjectId`| Идентификатор объекта Azure Active Directory пользователя, отправившего запрос. |
|`channelData.tenant.id`| Идентификатор клиента Azure Active Directory. |
|`channelData.source.name`| Имя источника, из которого вызывается модуль задач. |
|`ChannelData.legacy. replyToId`| Возвращает или устанавливает идентификатор сообщения, ответом на которое является данное сообщение. |
|`value.commandId` | Содержит идентификатор вызванной команды. |
|`value.commandContext` | Контекст, инициировавший событие. Должно применяться значение `compose`. |
|`value.context.theme` | Тема клиента пользователя. Удобно при форматировании внедренного веб-представления. Должно применяться значение `default`, `contrast` или `dark`. |

### <a name="example"></a>Пример

Свойства действий полезных данных при вызове модуля задач из индивидуального чата указаны в примере ниже.

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

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-group-chat"></a>Свойства действий полезных данных при вызове модуля задач из группового чата

Свойства действий полезных данных при вызове модуля задач из группового чата перечислены ниже.

|Имя свойства|Назначение|
|---|---|
|`type`| Тип запроса. Должно применяться значение `invoke`. |
|`name`| Тип команды, выпущенной для вашей службы. Должно применяться значение `composeExtension/fetchTask`. |
|`from.id`| Идентификатор пользователя, отправившего запрос. |
|`from.name`| Имя пользователя, отправившего запрос. |
|`from.aadObjectId`| Идентификатор объекта Azure Active Directory пользователя, отправившего запрос. |
|`channelData.tenant.id`| Идентификатор клиента Azure Active Directory. |
|`channelData.source.name`| Имя источника, из которого вызывается модуль задач. |
|`ChannelData.legacy. replyToId`| Возвращает или устанавливает идентификатор сообщения, ответом на которое является данное сообщение. |
|`value.commandId` | Содержит идентификатор вызванной команды. |
|`value.commandContext` | Контекст, инициировавший событие. Должно применяться значение `compose`. |
|`value.context.theme` | Тема клиента пользователя. Удобно при форматировании внедренного веб-представления. Должно применяться значение `default`, `contrast` или `dark`. |

### <a name="example"></a>Пример

Свойства действий полезных данных при вызове модуля задач из группового чата указаны в примере ниже.

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

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-meeting-chat"></a>Свойства действий полезных данных при вызове модуля задач из чата собрания

Свойства действий полезных данных при вызове модуля задач из чата собрания указаны в примере ниже.

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

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-channel-new-post"></a>Свойства действий полезных данных при вызове модуля задач из канала (новая публикация)

Свойства действий полезных данных при вызове модуля задач из канала (новая публикация) перечислены ниже.

|Имя свойства|Назначение|
|---|---|
|`type`| Тип запроса. Должно применяться значение `invoke`. |
|`name`| Тип команды, выпущенной для вашей службы. Должно применяться значение `composeExtension/fetchTask`. |
|`from.id`| Идентификатор пользователя, отправившего запрос. |
|`from.name`| Имя пользователя, отправившего запрос. |
|`from.aadObjectId`| Идентификатор объекта Azure Active Directory пользователя, отправившего запрос. |
|`channelData.tenant.id`| Идентификатор клиента Azure Active Directory. |
|`channelData.channel.id`| Идентификатор канала (если запрос был выполнен в канале). |
|`channelData.team.id`| Идентификатор команды (если запрос был выполнен в канале). |
|`channelData.source.name`| Имя источника, из которого вызывается модуль задач. |
|`ChannelData.legacy. replyToId`| Возвращает или устанавливает идентификатор сообщения, ответом на которое является данное сообщение. |
|`value.commandId` | Содержит идентификатор вызванной команды. |
|`value.commandContext` | Контекст, инициировавший событие. Должно применяться значение `compose`. |
|`value.context.theme` | Тема клиента пользователя. Удобно при форматировании внедренного веб-представления. Должно применяться значение `default`, `contrast` или `dark`. |

### <a name="example"></a>Пример

Свойства действий полезных данных при вызове модуля задач из канала (новая публикация) указаны в примере ниже.

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

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-channel-reply-to-thread"></a>Свойства действий полезных данных при вызове модуля задач из канала (ответ в беседе)

Свойства действий полезных данных при вызове модуля задач из канала (ответ в беседе) перечислены ниже.

|Имя свойства|Назначение|
|---|---|
|`type`| Тип запроса. Должно применяться значение `invoke`. |
|`name`| Тип команды, выпущенной для вашей службы. Должно применяться значение `composeExtension/fetchTask`. |
|`from.id`| Идентификатор пользователя, отправившего запрос. |
|`from.name`| Имя пользователя, отправившего запрос. |
|`from.aadObjectId`| Идентификатор объекта Azure Active Directory пользователя, отправившего запрос. |
|`channelData.tenant.id`| Идентификатор клиента Azure Active Directory. |
|`channelData.channel.id`| Идентификатор канала (если запрос был выполнен в канале). |
|`channelData.team.id`| Идентификатор команды (если запрос был выполнен в канале). |
|`channelData.source.name`| Имя источника, из которого вызывается модуль задач. |
|`ChannelData.legacy. replyToId`| Возвращает или устанавливает идентификатор сообщения, ответом на которое является данное сообщение. |
|`value.commandId` | Содержит идентификатор вызванной команды. |
|`value.commandContext` | Контекст, инициировавший событие. Должно применяться значение `compose`. |
|`value.context.theme` | Тема клиента пользователя. Удобно при форматировании внедренного веб-представления. Должно применяться значение `default`, `contrast` или `dark`. |

### <a name="example"></a>Пример

Свойства действий полезных данных при вызове модуля задач из канала (ответ в беседе) указаны в примере ниже.

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

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-command-box"></a>Свойства действий полезных данных при вызове модуля задач из командного поля

Свойства действий полезных данных при вызове модуля задач из командного поля перечислены ниже.

|Имя свойства|Назначение|
|---|---|
|`type`| Тип запроса. Должно применяться значение `invoke`. |
|`name`| Тип команды, выпущенной для вашей службы. Должно применяться значение `composeExtension/fetchTask`. |
|`from.id`| Идентификатор пользователя, отправившего запрос. |
|`from.name`| Имя пользователя, отправившего запрос. |
|`from.aadObjectId`| Идентификатор объекта Azure Active Directory пользователя, отправившего запрос. |
|`channelData.tenant.id`| Идентификатор клиента Azure Active Directory. |
|`channelData.source.name`| Имя источника, из которого вызывается модуль задач. |
|`value.commandId` | Содержит идентификатор вызванной команды. |
|`value.commandContext` | Контекст, инициировавший событие. Должно применяться значение `compose`. |
|`value.context.theme` | Тема клиента пользователя. Удобно при форматировании внедренного веб-представления. Должно применяться значение `default`, `contrast` или `dark`. |

### <a name="example"></a>Пример

Свойства действий полезных данных при вызове модуля задач из командного поля указаны в примере ниже.

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

Следующий раздел кода является примером запроса `fetchTask`.

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

## <a name="initial-invoke-request-from-a-message"></a>Запрос начального вызова из сообщения

При вызове бота из сообщения объект `value` в запросе начального вызова должен содержать сведения о сообщении, из которого вызывается ваше расширение для сообщений. Массивы `reactions` и `mentions` являются необязательными. Они отсутствуют, если в исходном сообщении нет реакций или упоминаний.
В следующем разделе представлен пример объекта `value`.

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

## <a name="respond-to-the-fetchtask"></a>Отклик на fetchTask

Отвечайте на запрос вызова с использованием объекта `task`, который содержит либо объект `taskInfo` с адаптивной карточкой или URL-адресом веб-страницы, либо простое строковое сообщение.

|Имя свойства|Назначение|
|---|---|
|`type`| Может иметь значение `continue` для представления формы или `message` для простого всплывающего окна. |
|`value`| Объект `taskInfo` для формы или `string` для сообщения. |

Схема для объекта taskInfo:

|Имя свойства|Назначение|
|---|---|
|`title`| Название модуля задач.|
|`height`| Должно быть целым числом (в пикселях) или иметь значение `small`, `medium`, `large`.|
|`width`| Должно быть целым числом (в пикселях) или иметь значение `small`, `medium`, `large`.|
|`card`| Адаптивная карточка, определяющая форму (если она используется).
|`url`| URL-адрес, который должен открываться внутри модуля задач в виде внедренного веб-представления.|
|`fallbackUrl`| Если клиент не поддерживает модули задач, этот URL-адрес открывается во вкладке браузера. |

### <a name="respond-to-the-fetchtask-with-an-adaptive-card"></a>Отклик на fetchTask с помощью адаптивной карточки

При использовании адаптивной карточки необходимо ответить объектом `task` с объектом `value`, содержащим адаптивную карточку.

#### <a name="example"></a>Пример

Следующий раздел кода является примером отклика на `fetchTask` с помощью адаптивной карточки.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

В этом примере в дополнение к пакету SDK Bot Framework используется [пакет NuGet AdaptiveCards](https://www.nuget.org/packages/AdaptiveCards).

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

При использовании внедренного веб-представления необходимо ответить объектом `task` с объектом `value`, содержащим URL-адрес веб-формы, которую требуется загрузить. Домены любого URL-адреса, который нужно загрузить, требуется включить в массив `validDomains` манифеста приложения. Дополнительные сведения о создании внедренного веб-представления см. в [документации по модулям задач](~/task-modules-and-cards/what-are-task-modules.md).

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

### <a name="request-to-install-your-conversational-bot"></a>Запрос на установку бота для бесед

Если приложение содержит бот для бесед, установите бота в беседе, а затем загрузите модуль задач. Бот удобен для получения дополнительного контекста для модуля задач. Примером этого сценария является получение состава для заполнения элемента выбора людей или списка каналов в команде.

Когда расширение для сообщений получит вызов `composeExtension/fetchTask`, проверьте, установлен ли бот в текущем контексте, чтобы упростить поток. Например, проверьте поток с помощью вызова получения состава. Если бот не установлен, верните адаптивную карточку с действием, которое запрашивает у пользователя установку бота. У пользователя должно быть разрешение на установку приложений в этом расположении для проверки. Если установка приложения завершается неудачно, пользователь получает сообщение, предлагающее ему связаться с администратором.

#### <a name="example"></a>Пример

Следующий раздел кода является примером отклика.

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

После установки бота для бесед он получает еще одно сообщение вызова с `name = composeExtension/submitAction` и `value.data.msteams.justInTimeInstall = true`.

#### <a name="example"></a>Пример

Следующий раздел кода является примером отклика задачи на вызов.

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

Отклик задачи на вызов должен быть аналогичен отклику установленного бота.

#### <a name="example"></a>Пример

Следующий раздел кода является примером JIT-установки приложения с адаптивной карточкой.

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

| Название примера           | Описание | .NET    | Node.js   |
|:---------------------|:--------------|:---------|:--------|
|Действие расширения для сообщений Teams| Описывает, как определить команды действий, создать модуль задач и отвечать на действие отправки модуля задач. |[Просмотр](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[Просмотр](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) |
|Поиск в расширении для сообщений Teams   |  Описывает, как определить команды поиска и отвечать на поисковые запросы.        |[Просмотр](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[Просмотр](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Отклик на команды действий](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)

## <a name="see-also"></a>Дополнительные ресурсы

[Определение команд действий](~/messaging-extensions/how-to/action-commands/define-action-command.md)
