---
title: Изменения API-интерфейса бота для участников группы или чата
author: ojasvichoudhary
description: В этом модуле вы узнаете о предстоящих и предстоящих изменениях в API-интерфейсах ботов, используемых для извлечения участников команд и чатов.
ms.localizationpriority: medium
ms.topic: reference
ms.author: ojchoudh
ms.openlocfilehash: e3096b3a2201d1bc36824fb5bf726150522f679b
ms.sourcegitcommit: c7fbb789b9654e9b8238700460b7ae5b2a58f216
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/29/2022
ms.locfileid: "66485365"
---
# <a name="teams-bot-api-changes-to-fetch-team-or-chat-members"></a>Изменения API-интерфейса бота Teams для получения участников команды или чата

> [!NOTE]
> `TeamsInfo.getMembers` и `TeamsInfo.GetMembersAsync` API являются устаревшими. Они регулируются до пяти запросов в минуту и возвращают не более 10 тысяч участников на команду, а полный список не возвращается для больших команд. Необходимо обновить пакет SDK Bot Framework до версии 4.10 или более поздней, переключиться на конечные точки API с разбивкой на страницы или `TeamsInfo.GetMemberAsync` использовать их для извлечения отдельных пользователей.
>
> Это также относится к боту, даже если вы не используете эти API напрямую, так как старые пакеты SDK вызывающие эти API во время [событий membersAdded](../bots/how-to/conversations/subscribe-to-conversation-events.md#members-added) . Если вы используете пакет SDK более ранней версии до 4.10, обновите его до последней версии.
>
> Список предстоящих изменений см. в разделе об [изменениях API](team-chat-member-api-changes.md#api-changes).

В настоящее время, если вы хотите получить сведения для одного или нескольких участников чата или группы, можно использовать [API бота Microsoft Teams](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile)`TeamsInfo.GetMembersAsync` для C# или `TeamsInfo.getMembers` для API-интерфейсов TypeScript или Node.js. Дополнительные сведения см. в разделе [получение личного состава группы или пользовательского профиля](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile).

Эти API имеют следующие недостатки:

* Для больших групп их производительность низкая, а прерывание по истечении времени ожидания более вероятно. Максимальный размер рабочей группы значительно увеличился с момента выпуска Teams в начале 2017 г. `getMembers` Так `GetMembersAsync` как вызов API возвращается или возвращает весь список участников, для возврата крупных команд требуется много времени, и обычно для вызова истекло время ожидания, и вам придется повторить попытку.
* Получить сведения о профиле для одного пользователя сложно: чтобы получить сведения из профиля одного пользователя, необходимо получить весь список участников, а затем найти нужного. В пакете SDK Bot Framework есть вспомогательная функция, которая упрощает ее, но не является эффективной.

С появлением команд для всей организации необходимо лучше согласовать эти API с Office 365 конфиденциальности. Боты, используемые в больших группах, могут получать основные сведения о профиле пользователя аналогично разрешению `User.ReadBasic.All` Microsoft Graph. Администраторы клиентов имеют значительную степень контроля над тем, какие приложения и боты можно использовать в клиенте, но эти параметры отличаются от Microsoft Graph.

Этот фрагмент кода представляет собой пример JSON-представления того, что возвращают боты API Teams:

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

Ниже описаны предстоящие изменения API:

* Для получения сведений о профиле для участников чата или группы [`TeamsInfo.GetPagedMembersAsync`](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile) создается новый API. Этот API теперь доступен в пакете SDK Bot Framework начиная с версии 4.8. Для разработки во всех остальных версиях используйте метод [`GetConversationPagedMembers`](/dotnet/api/microsoft.bot.connector.conversationsextensions.getconversationpagedmembersasync?view=botbuilder-dotnet-stable&preserve-view=true).

    > [!NOTE]
    > При работе с версиями 3 или 4 лучше всего выполнить обновление до последней версии (не ниже 3.30.2 или не ниже 4.8 соответственно).

* Для получения сведений о профиле одного пользователя [`TeamsInfo.GetMemberAsync`](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#get-single-member-details) создается новый API. Он принимает в качестве параметров идентификатор группы или чата и [имя участника-пользователя](/windows/win32/ad/naming-properties#userprincipalname), то есть `userPrincipalName`идентификатор объекта Microsoft Azure Active Directory (Azure AD)`objectId` или идентификатор пользователя Teams `id` и возвращает сведения о профиле для этого пользователя.

    > [!NOTE]
    > `objectId` заменяется на `aadObjectId` в соответствии с тем, что вызывается в объекте сообщения `Activity` Bot Framework. Новый API доступен начиная с версии 4.8 пакета SDK Bot Framework. Он также доступен в расширении Пакета SDK Bot Framework Teams 3.x. Тем временем вы можете использовать конечную точку [REST](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#get-single-member-details).

* `TeamsInfo.GetMembersAsync` в C# и `TeamsInfo.getMembers` в TypeScript или Node.js официально не рекомендуется к использованию. После того как новый API станет доступен, вам придется обновить все боты, чтобы использовать его. Это также относится к [базовому REST API, который используется этими API](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#tabpanel_CeZOj-G++Q_json). 
