---
title: Изменения API-интерфейса Bot для участников группы или чата (обновление 2020)
author: ojasvichoudhary
description: Описание предстоящих и выполняемых изменений API-интерфейсов Bot, используемых для получения участников команд и сеансов
keywords: Список членов группы API-интерфейсов Bot Framework
ms.topic: reference
ms.author: ojchoudh
ms.openlocfilehash: 926e4e39e4b5c3f1ba34a4458cf6f17612d86841
ms.sourcegitcommit: b13b38a104946c32cd5245a7af706070e534927d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/28/2020
ms.locfileid: "44801293"
---
# <a name="changes-to-teams-bot-apis-for-fetching-teamchat-members"></a>Изменения в API-интерфейсах ленты Teams для извлечения участников группы или чата

В настоящее время разработчики-роботы, желающие получить информацию для одного или нескольких участников беседы или команды, используют API Microsoft Teams Bot `TeamsInfo.GetMembersAsync` (для C#) или `TeamsInfo.getMembers` (для TypeScript/Node.js), [описанные здесь](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetching-the-roster-or-user-profile). В настоящее время эти API имеют несколько недостатков:

* **В крупных командах производительность снижается, и время ожидания может быть больше.** Максимальный размер команды значительно увеличился с момента выпуска Microsoft Teams на ранних 2017. Так как `GetMembersAsync` / `getMembers` возвращает весь список элементов, он занимает много времени, чтобы вызов API возвращался для крупных команд, и вы можете попробовать еще раз.
* **Получить сведения о профиле для отдельного пользователя очень трудоемко.** Чтобы получить сведения о профиле для одного пользователя, необходимо извлечь весь список участников, а затем выполнить поиск нужного пользователя. True, существует вспомогательная функция в пакете SDK Bot для упрощения, но в этом случае она неэффективна.

Как и в случае с введением групп по всей Организации, мы осознали, что имелось время для более точного выравнивания этих API с помощью Office 365: Боты, используемые в крупных командах, могут получать основные сведения о профиле, аналогичные `User.ReadBasic.All` разрешениям Microsoft Graph. Администраторы клиентов имеют большой контроль над тем, какие приложения и боты можно использовать в клиенте, но эти параметры отличаются от тех, которые управляют Microsoft Graph.

Ниже показан пример представления JSON, который возвращается этими API на сегодняшний день. Ниже приведены некоторые из этих полей.

```json
[{
    "id": "29:1GcS4EyB_oSI8A88XmWBN7NJFyMqe3QGnJdgLfFGkJnVelzRGos0bPbpsfJjcbAD22bmKc4GMbrY2g4JDrrA8vM06X1-cHHle4zOE6U4ttcc",
    "objectId": "9d3e08f9-a7ae-43aa-a4d3-de3f319a8a9c",
    "givenName": "Larry",
    "surname": "Brown",
    "email": "Larry.Brown@fabrikam.com",
    "userPrincipalName": "labrown@fabrikam.com"
}, {
    "id": "29:1bSnHZ7Js2STWrgk6ScEErLk1Lp2zQuD5H2qQ960rtvstKp8tKLl-3r8b6DoW0QxZimuTxk_kupZ1DBMpvIQQUAZL-PNj0EORDvRZXy8kvWk",
    "objectId": "76b0b09f-d410-48fd-993e-84da521a597b",
    "givenName": "John",
    "surname": "Patterson",
    "email": "johnp@fabrikam.com",
    "userPrincipalName": "johnp@fabrikam.com"
}, {
    "id": "29:1URzNQM1x1PNMr1D7L5_lFe6qF6gEfAbkdG8_BUxOW2mTKryQqEZtBTqDt10-MghkzjYDuUj4KG6nvg5lFAyjOLiGJ4jzhb99WrnI7XKriCs",
    "objectId": "6b7b3b2a-2c4b-4175-8582-41c9e685c1b5",
    "givenName": "Rick",
    "surname": "Stevens",
    "email": "Rick.Stevens@fabrikam.com",
    "userPrincipalName": "rstevens@fabrikam.com"
}]
```

## <a name="api-changes"></a>Изменения API
Ниже приведены будущие изменения API:

* Мы создали новый API [`TeamsInfo.GetPagedMembersAsync`](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetching-the-roster-or-user-profile) для получения сведений о профиле участников беседы или команды. Этот API теперь доступен в пакете SDK для Bot Framework 4,8. Для разработки во всех остальных версиях используется [`GetConversationPagedMembers`](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.conversationsextensions.getconversationpagedmembersasync?view=botbuilder-dotnet-stable) метод. **Примечание**: в V3 или v4 лучше всего выполнить обновление до последней версии пункта (3.30.2 или 4,8 соответственно). 
* Мы создали новый API [`TeamsInfo.GetMemberAsync`](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#get-single-member-details) для получения сведений о профиле для одного пользователя. Он принимает идентификатор группы или чата, а также [имя участника-пользователя](https://docs.microsoft.com/windows/win32/ad/naming-properties#userprincipalname) ( `userPrincipalName` , см. *выше*), идентификатор объекта Azure Active Directory (, см. выше) `objectId` или идентификатор пользователя Teams (см *see above* `id` . *выше*) в качестве параметров и возвращает сведения о профиле для этого пользователя. **Примечание**: мы изменим в соответствии с тем, `objectId` `aadObjectId` что вызывается в `Activity` объекте сообщения Bot Framework. Новый API доступен в версии 4,8 с пакетом SDK для Bot. Он скоро будет доступен в версии пакета SDK для Teams (Bot) для Team Framework 3. x, а также в то же время вы можете использовать конечную точку [REST](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#get-single-member-details) .
* `TeamsInfo.GetMembersAsync`(C#) и `TeamsInfo.getMembers` (TypeScript/Node.js) формально формально и больше не работает в поздних 2021. Мы будем объявлять о конкретном расписание в 2020 мая, основываясь на отзывах разработчиков. После того, как новые постраничные API будут доступны, разработчикам следует обновить свои Боты, чтобы использовать ее. (Это также относится к [базовым API REST, которые используются этими API](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#tabpanel_CeZOj-G++Q_json)).
* С опозданием 2021 Боты не сможет получить доступ к `userPrincipalName` `email` свойствам участников разговора или рабочей группы и будет использовать Microsoft Graph для их извлечения. В частности, `userPrincipalName` и `email` свойства не будут возвращены из нового `GetConversationPagedMembers` API, начиная с позднего 2021. Для получения этих сведений Боты должен использовать Microsoft Graph с маркером доступа. Очевидно, что это существенное изменение: мы должны упростить, чтобы Боты получить маркер доступа, и мы должны упростить и упростить процесс разрешения конечных пользователей.

## <a name="feedback-and-more-information"></a>Отзывы и дополнительные сведения
Мы будем использовать эту страницу для предоставления актуальной информации об этих изменениях. Если у вас возникнут вопросы, используйте "Отправить Отзывы > на этой странице" в разделе **отзывов** , приведенном ниже. 
