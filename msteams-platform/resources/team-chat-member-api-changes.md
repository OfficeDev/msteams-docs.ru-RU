---
title: Изменения API-интерфейса бота для участников группы или чата
author: ojasvichoudhary
description: Описывает предстоящие и происходящие изменения API ботов, используемых для искания членов групп и чатов
keywords: Список участников группы apis для базы ботов
ms.topic: reference
ms.author: ojchoudh
ms.openlocfilehash: ee90c9c324f11e191cf596bcf8e27cd2bef41240
ms.sourcegitcommit: f5ee3fa5ef6126d9bf845948d27d9067b3bbb994
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2021
ms.locfileid: "51596184"
---
# <a name="changes-to-teams-bot-apis-for-fetching-team-and-chat-members"></a>Изменения API-API бота Teams для получения участников группы и чата

>[!NOTE]
> Мы начали с процесса амортизации и `TeamsInfo.getMembers` `TeamsInfo.GetMembersAsync` API. Вначале они будут строго перенастраиваться до 5 запросов в минуту и будут возвращать не более 10 000 участников на каждую команду. В результате полный список не возвращается по мере увеличения размера группы. 
> 
> Необходимо обновить до **версии 4.10** или выше SDK Bot Framework и перейти на paginated конечные точки API или API одного `TeamsInfo.GetMemberAsync` пользователя. Это также относится к вашему боту, даже если вы не используете эти API напрямую, так как более старые SDKs называют эти API во время [событий membersAdded.](../bots/how-to/conversations/subscribe-to-conversation-events.md#team-members-added) Чтобы просмотреть список предстоящих изменений, см. изменения [API.](team-chat-member-api-changes.md#api-changes) 

В настоящее время разработчики ботов, которые хотят получить сведения для одного или более членов чата или группы, используют API бота Microsoft Teams `TeamsInfo.GetMembersAsync` (для C#) или `TeamsInfo.getMembers` (для TypeScript/Node.js) [API (см. здесь).](../bots/how-to/get-teams-context.md#fetching-the-roster-or-user-profile) Эти API имеют несколько недостатков на сегодняшний день:

* **Для больших групп производительность является низкой, а время выполнения более вероятно.** Максимальный размер группы значительно вырос с момента выпуска Microsoft Teams в начале 2017 г. Так как возвращается весь список участников, вызов API возвращается для больших групп, и это не редкость для вызова до времени ожидания, и вам придется попробовать `GetMembersAsync` / `getMembers` еще раз.
* **Получение сведений о профиле для одного пользователя является громоздким.** Чтобы получить сведения о профиле для одного пользователя, необходимо получить весь список участников, а затем искать нужный. Правда, в SDK Bot Framework есть функция помощника, чтобы упростерить ее, но под крышками она неэффективна.

Кроме того, с введением групп для всех организаций мы поняли, что пришло время лучше согласовать эти API с управлением конфиденциальности Office 365: боты, используемые в больших группах, могут получать основные сведения о профиле, аналогичные разрешению `User.ReadBasic.All` Microsoft Graph. Администраторы клиентов имеют большой контроль над тем, какие приложения и боты можно использовать в клиенте, но эти параметры отличаются от параметров, управляющих Microsoft Graph.

Вот пример представления JSON о том, что возвращается этими API сегодня. Я сослаться на некоторые из полей ниже.

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

Вот предстоящие изменения API:

* Мы создали новый API для получения сведений о профиле для членов [`TeamsInfo.GetPagedMembersAsync`](~/bots/how-to/get-teams-context.md?tabs=dotnet#fetching-the-roster-or-user-profile) чата или группы. Этот API теперь доступен с SDK Bot Framework 4.10. Для разработки во всех других версиях используйте [`GetConversationPagedMembers`](/dotnet/api/microsoft.bot.connector.conversationsextensions.getconversationpagedmembersasync?view=botbuilder-dotnet-stable&preserve-view=true) метод.
  > [!NOTE]
  > В v3 или v4 лучшим действием является обновление до последней точки выпуска.
* Мы создали новый API для получения сведений о профиле [`TeamsInfo.GetMemberAsync`](~/bots/how-to/get-teams-context.md?tabs=dotnet#get-single-member-details) для одного пользователя. Он принимает ID команды/чата и [upN](https://docs.microsoft.com/windows/win32/ad/naming-properties#userprincipalname) (см. `userPrincipalName` выше), Azure Active Directory Object ID (см. выше), или ID пользователя Teams  `objectId`  `id` (см. выше) в качестве параметров и возвращает сведения о профиле для этого пользователя.
  > [!NOTE]
  > Мы меняемся в соответствие с тем, что оно называется в объекте сообщения `objectId` Bot `aadObjectId` `Activity` Framework. Новый API доступен с версией 4.10 SDK Bot Framework. Вскоре он будет доступен и в расширении Bot Framework 3.x teams SDK; между тем вы можете использовать конечную [точку REST.](~/bots/how-to/get-teams-context.md?tabs=json#get-single-member-details)
* `TeamsInfo.GetMembersAsync` (C#) и (TypeScript/Node.js) формально обесценились и перестанут работать в `TeamsInfo.getMembers` конце 2021 г. Обновите боты, чтобы использовать API на странице. (Это также относится к основному [API REST, который используют](~/bots/how-to/get-teams-context.md?tabs=json)эти API.)
* К концу 2021 г. боты не смогут активно извлекать свойства для участников чата или группы, и для их получения потребуется использовать `userPrincipalName` `email` Microsoft Graph. В частности, свойства не будут возвращены из нового `userPrincipalName` `email` `GetConversationPagedMembers` API с конца 2021 г. Для получения этих сведений ботам придется использовать Microsoft Graph с маркером доступа. Очевидно, что это серьезное изменение: мы должны упростить для ботов процесс получения маркера доступа, а также упростить процесс согласия конечного пользователя.

## <a name="feedback-and-more-information"></a>Отзывы и дополнительные сведения

Мы будем использовать эту страницу для предоставления сведений об этих изменениях. Если у вас есть вопросы, используйте раздел "Отправка отзывов > на эту страницу" в разделе **Обратная** связь ниже.
