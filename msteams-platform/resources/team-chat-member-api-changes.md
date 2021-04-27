---
title: Изменения API-интерфейса бота для участников группы или чата
author: ojasvichoudhary
description: Описывает предстоящие и происходящие изменения API ботов, используемых для искания членов групп и чатов
keywords: Список участников группы apis для базы ботов
localization_priority: Normal
ms.topic: reference
ms.author: ojchoudh
ms.openlocfilehash: ad03d14ca1c38eb810d43027e901e01199858992
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019680"
---
# <a name="teams-bot-api-changes-to-fetch-team-or-chat-members"></a>Изменения API бота teams для получения участников группы или чата

>[!NOTE]
> Начался процесс амортизации `TeamsInfo.getMembers` и `TeamsInfo.GetMembersAsync` API. Первоначально они в значительной степени перенастраиваются до пяти запросов в минуту и возвращают не более 10 000 участников в каждой команде. В результате полный список не возвращается по мере увеличения размера группы.
> Необходимо обновить до версии 4.10 или выше SDK Bot Framework и перейти на paginated конечные точки API или API одного `TeamsInfo.GetMemberAsync` пользователя. Это также относится к вашему боту, даже если вы не используете эти API напрямую, так как более старые SDKs называют эти API во время [событий membersAdded.](../bots/how-to/conversations/subscribe-to-conversation-events.md#team-members-added) Чтобы просмотреть список предстоящих изменений, см. изменения [API.](team-chat-member-api-changes.md#api-changes) 

В настоящее время разработчики ботов, которые хотят получить сведения для одного или более членов чата или группы, используют API бота Microsoft Teams для C# или для `TeamsInfo.GetMembersAsync` `TeamsInfo.getMembers` API typeScript Node.js или Node.js API. Дополнительные сведения см. в [дополнительных сведениях о реестре или профиле пользователя.](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile) Эти API имеют несколько недостатков.

В настоящее время, если вы хотите получить сведения для одного или более членов чата или группы, вы можете использовать API [бота Microsoft Teams](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile) для C# или для `TeamsInfo.GetMembersAsync` `TeamsInfo.getMembers` typeScript или Node.js API. Эти API имеют следующие недостатки:

* Для больших групп производительность является низкой, а время ото дня более вероятно: максимальный размер группы значительно вырос с момента выпуска Teams в начале 2017 г. При возвращении или возвращении всего списка участников для вызова API для больших групп требуется много времени, и для вызова обычно требуется время ожидания, и вам придется попробовать `GetMembersAsync` `getMembers` еще раз.
* Получение сведений о профиле для одного пользователя затруднено: чтобы получить сведения о профиле для одного пользователя, необходимо получить весь список участников, а затем найти нужный. Существует функция помощника в SDK Bot Framework, чтобы упростерить ее, но она неэффективна.

С введением широкой группы организаций необходимо лучше согласовать эти API с управлением конфиденциальностью Office 365. Боты, используемые в больших группах, могут получать основные сведения о профиле, аналогичные `User.ReadBasic.All` разрешению Microsoft Graph. Администраторы клиентов имеют большой контроль над тем, какие приложения и боты можно использовать в клиенте, но эти параметры отличаются от Microsoft Graph.

В следующем коде представлен пример представления JSON того, что возвращается API бота Teams:

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

* Для получения сведений о профиле для участников чата или группы создается новый [`TeamsInfo.GetPagedMembersAsync`](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile) API. Этот API теперь доступен с SDK Bot Framework 4.8. Для разработки во всех других версиях используйте [`GetConversationPagedMembers`](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.conversationsextensions.getconversationpagedmembersasync?view=botbuilder-dotnet-stable&preserve-view=true) метод.

    > [!NOTE]
    > В v3 или v4 лучшим действием является обновление до последней версии точки, которая будет 3.30.2 или 4.8 соответственно.

* Для получения сведений о профиле для одного пользователя создается новый [`TeamsInfo.GetMemberAsync`](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#get-single-member-details) API. В качестве параметров принимается ID группы или чата и [upN,](https://docs.microsoft.com/windows/win32/ad/naming-properties#userprincipalname) то есть `userPrincipalName` , Azure Active Directory Object ID или ID пользователя Teams, который возвращает сведения о профиле для этого `objectId` `id` пользователя.

    > [!NOTE]
    > `objectId` изменен в `aadObjectId` соответствие с тем, что называется в `Activity` объекте сообщения Bot Framework. Новый API доступен с версией 4.8 SDK Bot Framework. Он также доступен в расширении Команд SDK Bot Framework 3.x. Между тем можно использовать конечную [точку REST.](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#get-single-member-details)

* `TeamsInfo.GetMembersAsync` в C# и `TeamsInfo.getMembers` в TypeScript или Node.js формально отстает. После того как новый API будет доступен, необходимо обновить боты, чтобы использовать его. Это также относится к основному [API REST, который используют эти API.](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#tabpanel_CeZOj-G++Q_json)
* К концу 2021 г. боты не смогут активно извлекать свойства для членов чата `userPrincipalName` `email` или группы. Для их получения боты должны использовать Graph. Свойства `userPrincipalName` `email` и свойства не возвращаются из нового `GetConversationPagedMembers` API, начиная с конца 2021 г. Боты должны использовать Graph с маркером доступа для получения информации. Ботам необходимо упростить процедуру получения маркера доступа, упростить и упростить процесс согласия конечных пользователей.
