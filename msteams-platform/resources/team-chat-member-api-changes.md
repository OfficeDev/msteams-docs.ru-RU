---
title: Изменения API-интерфейса бота для участников группы или чата
author: ojasvichoudhary
description: Описание предстоящих и предстоящих изменений в API-интерфейсах ботов, используемых для извлечения участников команд и чатов.
keywords: Список участников команды API bot Framework
ms.localizationpriority: medium
ms.topic: reference
ms.author: ojchoudh
ms.openlocfilehash: dfa85832fe8225b58e4566ba889c23d2696807e4
ms.sourcegitcommit: 61003a14e8a179e1268bbdbd9cf5e904c5259566
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2022
ms.locfileid: "64737207"
---
# <a name="teams-bot-api-changes-to-fetch-team-or-chat-members"></a>Teams API бота для получения участников команды или чата

>[!NOTE]
> Запущен процесс устаревания API `TeamsInfo.getMembers` `TeamsInfo.GetMembersAsync` и API. Изначально они сильно регулируются пятью запросами в минуту и возвращают не более 10 000 участников на команду. В результате полный список не возвращается по мере увеличения размера команды.
> Необходимо обновить пакет SDK Bot Framework до версии 4.10 или более поздней и переключиться на конечные точки API с разбивкой на страницы или `TeamsInfo.GetMemberAsync` API одного пользователя. Это также относится к боту, даже если вы не используете эти API напрямую, так как старые пакеты SDK вызывающие эти API во время [событий membersAdded](../bots/how-to/conversations/subscribe-to-conversation-events.md#team-members-added) . Список предстоящих изменений см. в [разделе об изменениях API](team-chat-member-api-changes.md#api-changes).

В настоящее время, если вы хотите получить сведения для одного или нескольких участников чата или команды, можно использовать [API](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile) `TeamsInfo.GetMembersAsync` бота Microsoft Teams для C#`TeamsInfo.getMembers`, TypeScript или Node.js API. Дополнительные сведения см. в [разделе fetch roster или user profile](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile).

Эти API имеют следующие недостатки:

* Для больших команд производительность низкая, а время ожидания более вероятно: максимальный размер команды значительно увеличивается с момента выпуска Teams в начале 2017 г. `getMembers` Так `GetMembersAsync` как вызов API возвращается или возвращается весь список участников, для возврата крупных команд требуется много времени, и обычно для вызова истекло время ожидания, и вам придется повторить попытку.
* Получить сведения о профиле для одного пользователя сложно: чтобы получить сведения о профиле для одного пользователя, необходимо получить весь список участников, а затем найти нужный. В пакете SDK Bot Framework есть вспомогательная функция, которая упрощает ее, но не является эффективной.

С появлением групп для всей организации необходимо лучше согласовать эти API с Office 365 конфиденциальности. Боты, используемые в больших командах`User.ReadBasic.All`, могут получать основные сведения о профиле, аналогичные разрешению microsoft Graph. Администраторы клиентов имеют большой контроль над тем, какие приложения и боты можно использовать в клиенте, но эти параметры отличаются от microsoft Graph.

Следующий код предоставляет пример JSON-представления того, что возвращается Teams API бота:

```json
[{
    "id": "29:1GcS4EyB_oSI8A88XmWBN7NJFyMqe3QGnJdgLfFGkJnVelzRGos0bPbpsfJjcbAD22bmKc4GMbrY2g4JDrrA8vM06X1-cHHle4zOE6U4ttcc",
    "name": "Anon1 (Guest)",
    "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47",
 "userRole": "anonymous"
}, {
    "id": "29:1bSnHZ7Js2STWrgk6ScEErLk1Lp2zQuD5H2qQ960rtvstKp8tKLl-3r8b6DoW0QxZimuTxk_kupZ1DBMpvIQQUAZL-PNj0EORDvRZXy8kvWk",
    "objectId": "76b0b09f-d410-48fd-993e-84da521a597b",
    "givenName": "John",
    "surname": "Patterson",
    "email": "johnp@fabrikam.com",
    "userPrincipalName": "johnp@fabrikam.com",
    "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47",
 "userRole": "user"
}, {
    "id": "29:1URzNQM1x1PNMr1D7L5_lFe6qF6gEfAbkdG8_BUxOW2mTKryQqEZtBTqDt10-MghkzjYDuUj4KG6nvg5lFAyjOLiGJ4jzhb99WrnI7XKriCs",
    "objectId": "6b7b3b2a-2c4b-4175-8582-41c9e685c1b5",
    "givenName": "Rick",
    "surname": "Stevens",
    "email": "Rick.Stevens@fabrikam.com",
    "userPrincipalName": "rstevens@fabrikam.com",
    "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47",
 "userRole": "user"
}]
```

## <a name="api-changes"></a>Изменения API

Ниже приведены предстоящие изменения API:

* Для получения сведений о [`TeamsInfo.GetPagedMembersAsync`](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile) профиле для участников чата или команды создается новый API. Этот API теперь доступен в пакете SDK Bot Framework версии 4.8 или более поздней. Для разработки во всех остальных версиях используйте этот [`GetConversationPagedMembers`](/dotnet/api/microsoft.bot.connector.conversationsextensions.getconversationpagedmembersasync?view=botbuilder-dotnet-stable&preserve-view=true) метод.

    > [!NOTE]
    > В версии 3 или 4 лучше всего выполнить обновление до последней версии 3.30.2 или 4.8 или более поздней версии соответственно.

* Для получения сведений [`TeamsInfo.GetMemberAsync`](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#get-single-member-details) о профиле для одного пользователя создается новый API. Он принимает идентификатор команды или чата и имя участника-пользователя[](/windows/win32/ad/naming-properties#userprincipalname), то есть идентификатор объекта Microsoft Azure Active Directory (Azure AD) `objectId``id` или идентификатор пользователя Teams в качестве параметров, и возвращает сведения о профиле для этого пользователя.`userPrincipalName`

    > [!NOTE]
    > `objectId` is changed to `aadObjectId` to match what is called in the `Activity` object of a Bot Framework message. Новый API доступен в версии 4.8 или более поздней версии пакета SDK Bot Framework. Он также доступен в расширении Teams Пакета SDK Bot Framework 3.x. В то же время можно использовать конечную [точку REST](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#get-single-member-details) .

* `TeamsInfo.GetMembersAsync` в C# и `TeamsInfo.getMembers` TypeScript или Node.js официально не рекомендуется. После того как новый API будет доступен, необходимо обновить боты, чтобы использовать его. Это также относится к базовому [REST API, который используются этими API](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#tabpanel_CeZOj-G++Q_json).
* К конце 2022 `userPrincipalName` `email` года боты не могут заранее получить свойства участников чата или команды. Боты должны использовать Graph API для получения необходимой формы. `GetConversationPagedMembers` Новый API не может вернуть свойства `userPrincipalName` `email` с позднего 2022 года. Боты должны использовать API Graph с маркером доступа для получения информации. 
