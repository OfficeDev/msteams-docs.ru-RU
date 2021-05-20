---
title: Изменения API-интерфейса бота для участников группы или чата
author: ojasvichoudhary
description: Описывает предстоящие и в процессе изменения API Bot, используемые для извлечения членов групп и чатов
keywords: бот фреймвек apis список членов команды
localization_priority: Normal
ms.topic: reference
ms.author: ojchoudh
ms.openlocfilehash: 333a29664f0d60e89039f906fce77e71054d486f
ms.sourcegitcommit: 9ef3b415cbba484c2201abe9c6927e08d974388e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52555439"
---
# <a name="teams-bot-api-changes-to-fetch-team-or-chat-members"></a>Teams API-бота для извлечения членов команды или чата

>[!NOTE]
> Начался процесс амортизации `TeamsInfo.getMembers` `TeamsInfo.GetMembersAsync` и API. Первоначально они сильно задушены до пяти запросов в минуту и возвращают максимум 10K членов на команду. Это приводит к том, что полный список не возвращается по мере увеличения размера команды.
> Необходимо обновить версию 4.10 или выше Bot Framework SDK и переключиться на paginated конечные точки API или `TeamsInfo.GetMemberAsync` API одного пользователя. Это также относится и к вашему боту, даже если вы непосредственно не используете эти API, так как старые SDKs называют эти API во [время событий, связанных с использованием членов.](../bots/how-to/conversations/subscribe-to-conversation-events.md#team-members-added) Чтобы просмотреть список предстоящих изменений, [см.](team-chat-member-api-changes.md#api-changes) 

В настоящее время разработчики ботов, которые хотят получить информацию для одного или нескольких членов чата или команды, используют API-Microsoft Teams ботов `TeamsInfo.GetMembersAsync` для `TeamsInfo.getMembers` C-е или для TypeScript или Node.js API. Для получения дополнительной информации [см.](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile) Эти API имеют ряд недостатков.

В настоящее время, если вы хотите получить информацию для одного или нескольких членов чата или команды, [вы можете использовать API-файлы Microsoft Teams бота](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile) `TeamsInfo.GetMembersAsync` для `TeamsInfo.getMembers` C-е или для TypeScript или Node.js API. Эти API имеют следующие недостатки:

* Для больших команд производительность низкая, а тайм-ауты более вероятны: максимальный размер команды значительно вырос с момента Teams выпущен в начале 2017 года. По мере того как или возвращает весь список члена, оно принимает долгое время для звонока API для того чтобы возвратить для больших команд, и оно общее для `GetMembersAsync` `getMembers` звонока к тайм-ауту и вы должны попробовать снова.
* Получение информации о профиле для одного пользователя трудно: чтобы получить информацию о профиле для одного пользователя, вы должны получить весь список участников, а затем искать тот, который вы хотите. Существует функция помощник в Bot Framework SDK, чтобы сделать его проще, но это не эффективно.

С введением широких групп организации существует требование лучше согласовывать эти API с Office 365 конфиденциальности. Боты, используемые в больших группах, могут получать базовую информацию о профиле, аналогичную `User.ReadBasic.All` разрешению Graph Майкрософт. Администраторы арендаторов имеют большой контроль над тем, какие приложения и боты могут быть использованы в их арендатора, но эти настройки отличаются от Microsoft Graph.

Следующий код содержит пример JSON, в который возвращается Teams БОТ API:

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

* Создается новый API для [`TeamsInfo.GetPagedMembersAsync`](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile) получения информации о профиле для членов чата или команды. Этот API теперь доступен с bot Framework версией 4.8 или более поздней версией SDK. Для разработки во всех других версиях используйте [`GetConversationPagedMembers`](/dotnet/api/microsoft.bot.connector.conversationsextensions.getconversationpagedmembersasync?view=botbuilder-dotnet-stable&preserve-view=true) этот метод.

    > [!NOTE]
    > В v3 или v4, лучшее действие заключается в обновлении до последней точки релиза, который 3.30.2 или 4.8 или позже соответственно.

* Для получения информации [`TeamsInfo.GetMemberAsync`](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#get-single-member-details) о профиле для одного пользователя создается новый API. Он принимает ID команды или чата и [UPN,](/windows/win32/ad/naming-properties#userprincipalname) `userPrincipalName` который, Azure Active Directory Object ID , или идентификатор пользователя Teams в качестве `objectId` `id` параметров и возвращает информацию профиля для этого пользователя.

    > [!NOTE]
    > `objectId` изменен в чтобы `aadObjectId` соответствовать тому, что называется `Activity` в объекте сообщения Bot Framework. Новый API доступен с версией 4.8 или позже Bot Framework SDK. Он также доступен в Teams расширения Bot Framework 3.x. Между тем, вы можете использовать конечную точку [REST.](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#get-single-member-details)

* `TeamsInfo.GetMembersAsync` в C и `TeamsInfo.getMembers` в TypeScript или Node.js официально уничежен. Как только новый API доступен, вы должны обновить ваши боты, чтобы использовать его. Это также относится к [базовому API REST, который используют эти API.](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#tabpanel_CeZOj-G++Q_json)
* К концу 2021 года боты не смогла активно `userPrincipalName` получить свойства для членов `email` чата или команды. Боты должны использовать Graph, чтобы получить их. Свойства `userPrincipalName` и свойства не `email` возвращаются из нового `GetConversationPagedMembers` API, начиная с конца 2021 года. Боты должны использовать Graph с маркером доступа для получения информации. Ботам необходимо упростить получение токена доступа, упорядочить и упростить процесс согласия конечных пользователей.
