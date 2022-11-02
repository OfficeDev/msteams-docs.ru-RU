---
title: Создание приложений для анонимного пользователя
author: v-sdhakshina
description: Узнайте, как создавать приложения для анонимных пользователей и тестировать взаимодействие с анонимными пользователями в приложениях для собраний со всеми параметрами администратора.
ms.topic: conceptual
ms.author: v-sdhakshina
ms.localizationpriority: medium
ms.openlocfilehash: ff897c5135740557e12898e7e5d231557b2e2823
ms.sourcegitcommit: 40d4bde10b6820c62e49e2400b10ab3569c8c815
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/20/2022
ms.locfileid: "68615476"
---
# <a name="build-apps-for-anonymous-users"></a>Создание приложений для анонимных пользователей

Вы можете создавать боты, расширения для обмена сообщениями, карточки и модули задач в приложении для взаимодействия с анонимными участниками собрания.

Чтобы протестировать работу приложения для анонимных пользователей, выберите URL-адрес в приглашении на собрание и присоединитесь к собранию в закрытом окне браузера.

## <a name="admin-setting-for-anonymous-user-app-interaction"></a>Администратор параметра для анонимного взаимодействия с приложением пользователя

Администраторы Teams могут использовать портал администрирования для включения или отключения анонимного взаимодействия с пользователем в приложении для всего клиента. Этот параметр по умолчанию включен. Дополнительные сведения см. в [статье о разрешении анонимным пользователям взаимодействовать с приложениями на собраниях](/microsoftteams/meeting-settings-in-teams).

## <a name="in-meeting-getcontext-from-teams-client-sdk"></a>In-Meeting getContext из клиентского пакета SDK teams

Приложения получают следующие сведения для анонимного пользователя при вызове `getContext` API из этапа общего приложения. Вы можете распознать анонимных пользователей, проверив значение `userLicenseType` **Unknown**.

```csharp
"userObjectId": "8:anon:<GUID1>",
"userLicenseType": "Unknown",
"loginHint": "8:teamsvisitor:<ID>",
"userPrincipalName": "8:teamsvisitor:<ID>",
"tid": "<meeting organizer tenant ID>"
```

| **Имя свойства** | **Описание** |
| --- | --- |
| `userObjectId` | Уникальное созданное значение для анонимного пользователя. Это значение нельзя использовать в вызовах API Graph. |
| `userLicenseType` | `Unknown`, представляет анонимного пользователя. |
| `loginHint` | Уникальное созданное значение. Это значение нельзя использовать в качестве указания в потоках входа. |
| `userPrincipalName` | Уникальное созданное значение. Это значение нельзя использовать в вызовах API Graph. |
| `tid` | Идентификатор клиента организатора собрания. |

> [!NOTE]
> Когда анонимный пользователь присоединяется к собранию, создается новый идентификатор пользователя. Каждый раз, когда анонимный пользователь повторно присоединяется к собранию, создается другой идентификатор пользователя.

## <a name="bot-activities-and-apis"></a>Действия бота и API

С несколькими отличиями действия, отправляемые боту, и ответы, получаемые от API бота, согласованы между анонимными и неанимными участниками собрания. Ниже приводится краткое описание этих операций.

* Идентификатор пользователя — это созданное значение, которое отличается при каждом присоединении анонимного пользователя к собранию.
* Свойство `aadObjectId` опущено.
* Для `userRole` свойства задано **анонимное значение**.
* Указанный идентификатор клиента задается идентификатором клиента организатора собрания.

### <a name="get-members-and-get-single-member-apis"></a>Получение членов и получение одноэлементных API

[API get members](/microsoftteams/platform/bots/how-to/get-teams-context#fetch-the-roster-or-user-profile) и [get single member](/microsoftteams/platform/bots/how-to/get-teams-context#get-single-member-details) возвращают ограниченную информацию для анонимных пользователей:

```json
{ 
  "id": "<GUID1>", 
  "name": "<AnonTest (Guest)>",  
  "tenantId": "<GUID2>", 
  "userRole": "anonymous" 
} 
```

| **Имя свойства** | **Описание** |
| --- | --- |
| `id` | Уникальное созданное значение для анонимного пользователя. |
| `name` | Имя, указанное анонимным пользователем при присоединении к собранию. |
| `tenantId` | Идентификатор клиента организатора собрания. |
| `userRole` | `anonymous`, представляет анонимного пользователя. |

> [!NOTE]
> Идентификатор, полученный от API бота и API клиентского пакета SDK Teams, не совпадает.

### <a name="conversationupdate-activity-membersadded-and-membersremoved"></a>Действия ConversationUpdate MembersAdded и MembersRemoved

```csharp
{ 
  "membersAdded": [ 
    { 
      "id": "<GUID1>" 
    } 
  ], 
  "type": "conversationUpdate", 
  "timestamp": "<timestamp>", 
  "id": "<event unique identifier>", 
  "channelId": "msteams", 
  "serviceUrl": "<serviceURL>", 
  "from": { 
    "id": "<GUID2>" 
  }, 
  "conversation": { 
    "isGroup": true, 
    "tenantId": "<tenant id>", 
    "id": "<conversation id>" 
  }, 
  "recipient": { 
    "id": "<bot id>", 
    "name": "<bot name>" 
  }, 
  "channelData": { 
    "tenant": { 
      "id": "<tenant id>" 
    }, 
    "source": null, 
    "meeting": { 
      "id": "<meeting id>" 
    } 
  } 
} 
```

| **Имя свойства** | **Описание** |
| --- | --- |
| `membersAdded.id` | Анонимный идентификатор пользователя. |
| `from.id` | Идентификатор организатора собрания. |
| `conversation.tenantId` | Идентификатор клиента организатора собрания. |
| `conversation.id` | Идентификатор беседы в чате собрания. |
| `tenant.id` | Идентификатор клиента организатора собрания. |

Аналогичные изменения применяются к полезным `membersRemoved` данным действия.

> [!NOTE]
>
> Когда анонимный пользователь присоединяется к собранию или покидает его, `from` объект в полезных данных всегда имеет идентификатор организатора собрания, даже если действие было выполнено другим пользователем.

### <a name="create-conversation-api"></a>Создание API беседы

Ботам не разрешено инициировать беседу "один на один" с анонимным пользователем. Если бот вызывает API создания беседы с идентификатором анонимного пользователя, `400` он получит код состояния "Недопустимый запрос" и следующий ответ об ошибке:

```csharp
{ 
  "error": {
    "code": "BadArgument",
    "message": "Bot cannot create a conversation with an anonymous user"
  }
} 
```

### <a name="adaptive-cards"></a>Адаптивные карточки

Анонимные пользователи могут просматривать адаптивные карточки и взаимодействовать с ними в чате собрания. Действия адаптивной карточки ведут себя одинаково для анонимных и неанимных пользователей. Дополнительные сведения см. в [разделе "Действия карточки"](/microsoftteams/platform/task-modules-and-cards/cards/cards-actions?tabs=json).

## <a name="known-issues-and-limitations"></a>Известные проблемы и ограничения

* Вкладки боковой панели и пузырьки содержимого недоступны анонимным пользователям. Анонимные пользователи по-прежнему могут видеть содержимое приложения, предоставленное на этапе собрания.

* Для анонимного пользователя идентификатор пользователя и идентификатор пользователя, `getContext` полученный ботом, отличаются. Коррелировать эти два элемента напрямую невозможно. Если необходимо отслеживать удостоверение пользователя между вкладкой и ботом, необходимо предложить пользователю выполнить проверку подлинности с помощью внешнего поставщика удостоверений.

* Анонимные пользователи будут видеть универсальный значок приложения в сообщениях бота и карточках вместо фактического значка приложения. Например:

    :::image type="content" source="../assets/images/apps-in-meetings/app-icon.png" alt-text="На этом снимке экрана показано, как отображается значок приложения для анонимного пользователя.":::

## <a name="see-also"></a>См. также

* [Этап сборки приложений для собраний Teams](build-apps-for-teams-meeting-stage.md)
* [API-интерфейсы приложений для собраний](meeting-apps-apis.md)
* [Как работают боты Microsoft Teams](/azure/bot-service/bot-builder-basics-teams)