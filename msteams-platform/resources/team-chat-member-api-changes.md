---
title: Изменения API-интерфейса бота для участников группы или чата
author: ojasvichoudhary
description: Описывает предстоящие и происходящие изменения API ботов, используемых для искания членов групп и чатов
keywords: Список участников группы apis для базы ботов
localization_priority: Normal
ms.topic: reference
ms.author: ojchoudh
ms.openlocfilehash: 9c6444967d330d27a415ac596a3858c05c49236e
ms.sourcegitcommit: b1f9162a0bbcd276064ae9e4f1e8bccc06cb7035
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/07/2021
ms.locfileid: "53328067"
---
# <a name="teams-bot-api-changes-to-fetch-team-or-chat-members"></a>Teams API бота для получения участников группы или чата

>[!NOTE]
> Начался процесс амортизации `TeamsInfo.getMembers` и `TeamsInfo.GetMembersAsync` API. Первоначально они в значительной степени перенастраиваются до пяти запросов в минуту и возвращают не более 10 000 участников в каждой команде. В результате полный список не возвращается по мере увеличения размера группы.
> Необходимо обновить до версии 4.10 или выше SDK Bot Framework и перейти на paginated конечные точки API или API одного `TeamsInfo.GetMemberAsync` пользователя. Это также относится к вашему боту, даже если вы не используете эти API напрямую, так как более старые SDKs называют эти API во время [событий membersAdded.](../bots/how-to/conversations/subscribe-to-conversation-events.md#team-members-added) Чтобы просмотреть список предстоящих изменений, см. изменения [API.](team-chat-member-api-changes.md#api-changes)

В настоящее время, если вы хотите получить сведения для одного или [](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile) более членов чата или группы, вы можете использовать API Microsoft Teams бота для C# или для `TeamsInfo.GetMembersAsync` `TeamsInfo.getMembers` API typeScript Node.js или Node.js. Дополнительные сведения см. в [дополнительных сведениях о реестре или профиле пользователя.](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile)

Эти API имеют следующие недостатки:

* Для больших групп производительность является низкой, а время выполнения более вероятно: максимальный размер группы значительно вырос с момента выпуска Teams в начале 2017 г. При возвращении или возвращении всего списка участников для вызова API для больших групп требуется много времени, и для вызова обычно требуется время ожидания, и вам придется попробовать `GetMembersAsync` `getMembers` еще раз.
* Получение сведений о профиле для одного пользователя затруднено: чтобы получить сведения о профиле для одного пользователя, необходимо получить весь список участников, а затем найти нужный. Существует функция помощника в SDK Bot Framework, чтобы упростерить ее, но она неэффективна.

С введением широкой группы организаций существует требование, чтобы лучше согласовать эти API с Office 365 конфиденциальности. Боты, используемые в больших группах, могут получать основные сведения о профиле, аналогичные разрешению `User.ReadBasic.All` Microsoft Graph. Администраторы клиентов имеют большой контроль над тем, какие приложения и боты можно использовать в клиенте, но эти параметры отличаются от microsoft Graph.

В следующем коде представлен пример представления JSON того, что возвращается Teams API бота:

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

Ниже следующую статью предстоящих изменений API:

* Для получения сведений о профиле для участников чата или группы создается новый [`TeamsInfo.GetPagedMembersAsync`](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile) API. Этот API теперь доступен с версией Bot Framework 4.8 или более поздней SDK. Для разработки во всех других версиях используйте [`GetConversationPagedMembers`](/dotnet/api/microsoft.bot.connector.conversationsextensions.getconversationpagedmembersasync?view=botbuilder-dotnet-stable&preserve-view=true) метод.

    > [!NOTE]
    > В v3 или v4 лучшим действием является обновление до последнего выпуска точки 3.30.2 или 4.8 или более поздней версии соответственно.

* Для получения сведений о профиле для одного пользователя создается новый [`TeamsInfo.GetMemberAsync`](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#get-single-member-details) API. В качестве параметров принимается ID группы или чата и [upN,](/windows/win32/ad/naming-properties#userprincipalname) то есть Azure Active Directory Object ID, или Teams пользователя в качестве параметров и возвращает сведения о профиле для этого `userPrincipalName` `objectId` `id` пользователя.

    > [!NOTE]
    > `objectId` изменен в `aadObjectId` соответствие с тем, что называется в `Activity` объекте сообщения Bot Framework. Новый API доступен с версией 4.8 или более поздней версией SDK bot Framework. Он также доступен в Teams SDK extension Bot Framework 3.x. Между тем можно использовать конечную [точку REST.](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#get-single-member-details)

* `TeamsInfo.GetMembersAsync` в C# и `TeamsInfo.getMembers` в TypeScript или Node.js формально отстает. После того как новый API будет доступен, необходимо обновить боты, чтобы использовать его. Это также относится к основному [API REST, который используют эти API.](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#tabpanel_CeZOj-G++Q_json)
* К концу 2022 г. боты не смогут активно извлекать свойства или свойства для членов `userPrincipalName` `email` чата или группы. Боты должны использовать Graph для их получения. Свойства `userPrincipalName` и свойства не `email` возвращаются из нового `GetConversationPagedMembers` API, начиная с конца 2022 г. Боты должны использовать Graph с маркером доступа для получения информации. Ботам необходимо упростить процедуру получения маркера доступа, упростить и упростить процесс согласия конечных пользователей.
