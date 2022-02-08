---
title: Обработчики действий ботов
author: surbhigupta
description: Понимание обработчиков действий бота в Teams.
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: anclear
keywords: Событие канала согласия на согласие бот-карты обработить обработник действий
ms.openlocfilehash: af6823a0a1395c5f33af9d914c3199d76854a050
ms.sourcegitcommit: c66da76fb766df6270095265e1da8c49a3afd195
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/07/2022
ms.locfileid: "62435798"
---
# <a name="bot-activity-handlers"></a>Обработчики действий ботов

Этот документ строится на статье о работе [ботов в](https://aka.ms/how-bots-work) основной документации [Bot Framework](https://aka.ms/azure-bot-service-docs). Основное различие между ботами, разработанными для Microsoft Teams и основной инфраструктурой ботов, заключается в функции, предоставляемые в Teams.

Для организации разговорной логики для бота используется обработок действий. Действия обрабатываются двумя способами с помощью обработчиков Teams действий и логики ботов. Обработник Teams добавляет поддержку для Microsoft Teams событий и взаимодействий. Объект бота содержит разговорное рассуждение или логику поворота и предоставляет обработщик поворота, который является методом, который может принимать входящие действия из адаптер бота.

## <a name="teams-activity-handlers"></a>Teams обработчики действий

Teams обработок действий получен Microsoft Bot Framework обработить действия Microsoft Bot Framework. Он передает все Teams, прежде чем разрешить обработку Teams определенных действий.

Когда бот для Teams получает действие, он передается обработчику действий. Все действия проходят через один базовый обработатель, называемый обработивель поворота. Обработник поворота вызывает обработник необходимых действий для управления любыми полученными действиями. Бот Teams происходит из `TeamsActivityHandler` класса, который является производным от класса `ActivityHandler` Bot Framework.

# <a name="c"></a>[C#](#tab/csharp)

Боты создаются с помощью bot Framework. Если боты получают сообщение, обработник поворота получает уведомление о входящих действиях. Обработитель поворота отправляет `OnMessageActivityAsync` входящие действия обработнику действий. В Teams эта функция остается той же. Если бот получает действие обновления беседы, обработитель поворота получает уведомление о входящих действиях и отправляет входящие действия `OnConversationUpdateActivityAsync`в . Обработ Teams действий сначала проверяет все Teams события. Если события не найдены, он передает их обработнику действий Bot Framework.

В классе обработчиков Teams действий есть два основных обработчиков Teams действий и `OnConversationUpdateActivityAsync` `OnInvokeActivityAsync`. `OnConversationUpdateActivityAsync`маршруты всех действий обновления беседы `OnInvokeActivityAsync` и маршруты всех Teams вызывают действия.

Чтобы реализовать логику Teams обработчиков действий, необходимо переопредить методы в боте, как показано в разделе [логика](#bot-logic) бота. Для этих обработчиков не существует базовой реализации, поэтому в переопределяемой логике необходимо добавить логику.

Фрагменты кода для обработчиков Teams действий:

`OnTeamsChannelCreatedAsync`

```csharp

protected override Task OnTeamsChannelCreatedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
        {
            // Code logic here
        }
```

`OnTeamsChannelDeletedAsync`

```csharp

protected override Task OnTeamsChannelDeletedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
        {
            // Code logic here
        }
```

`OnTeamsChannelRenamedAsync`

```csharp

protected override Task OnTeamsChannelRenamedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
        {
            // Code logic here
        }
```

`OnTeamsTeamRenamedAsync`

```csharp

protected override Task OnTeamsTeamRenamedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
        {
            // Code logic here
        }
```

`OnTeamsMembersAddedAsync`

```csharp

protected override Task OnTeamsMembersAddedAsync(IList<TeamsChannelAccount> teamsMembersAdded, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
        {
            // Code logic here
        }
```

`OnTeamsMembersRemovedAsync`

```csharp

protected override Task OnTeamsMembersRemovedAsync(IList<TeamsChannelAccount> teamsMembersRemoved, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken);
        {
            // Code logic here
        }
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

Боты создаются с помощью bot Framework. Если боты получают сообщение, обработник поворота получает уведомление о входящих действиях. Обработитель поворота отправляет `onMessage` входящие действия обработнику действий. В Teams эта функция остается той же. Если бот получает действие обновления беседы, обработитель поворота получает уведомление о входящих действиях и отправляет входящие действия `dispatchConversationUpdateActivity`в . Обработ Teams действий сначала проверяет все Teams события. Если события не найдены, он передает их обработнику действий Bot Framework.

В классе обработчиков Teams действий есть два основных обработчиков Teams действий и `dispatchConversationUpdateActivity` `onInvokeActivity`. `dispatchConversationUpdateActivity`маршруты всех действий обновления беседы `onInvokeActivity` и маршруты всех Teams вызывают действия.

Чтобы реализовать логику Teams обработчиков действий, необходимо переопредить методы в боте, как показано в разделе [логика](#bot-logic) бота. Определите логику бота для этих обработчиков, а затем обязательно позвоните `next()` в конце. Позвонив `next()` , убедитесь, что следующий обработок выполняется.

Фрагменты кода для обработчиков Teams действий:

`OnTeamsChannelCreatedAsync`

```javascript

onTeamsChannelCreated(async (channelInfo, teamInfo, context, next) => {
       // code for handling
        await next()
    });
```

`OnTeamsChannelDeletedAsync`

```javascript

onTeamsChannelDeleted(async (channelInfo, teamInfo, context, next) => {
       // code for handling
       await next()
    });
```

`OnTeamsChannelRenamedAsync`

```javascript

onTeamsChannelRenamed(async (channelInfo, teamInfo, context, next) => {
       // code for handling
       await next()
    });
```

`OnTeamsTeamRenamedAsync`

```javascript

onTeamsTeamRenamedAsync(async (teamInfo, context, next) => {
       // code for handling
       await next()
    });
```

`OnTeamsMembersAddedAsync`

```javascript

onTeamsMembersAdded(async (membersAdded, teamInfo, context, next) => {
       // code for handling
       await next();
    });
```

`OnTeamsMembersRemovedAsync`

```javascript

onTeamsMembersRemoved(async (membersRemoved, teamInfo, context, next) => {
       // code for handling
       await next();
    });
```

# <a name="python"></a>[Python](#tab/python)

Боты создаются с помощью bot Framework. Если боты получают сообщение, обработник поворота получает уведомление о входящих действиях. Обработитель поворота отправляет `on_message_activity` входящие действия обработнику действий. В Teams эта функция остается той же. Если бот получает действие обновления беседы, обработитель поворота получает уведомление о входящих действиях и отправляет входящие действия `on_conversation_update_activity`в . Обработ Teams действий сначала проверяет все Teams события. Если события не найдены, он передает их обработнику действий Bot Framework.

В классе обработчиков Teams действий есть два основных обработчиков Teams действий и `on_conversation_update_activity` `on_invoke_activity`. `on_conversation_update_activity`маршруты всех действий обновления беседы `on_invoke_activity` и маршруты всех Teams вызывают действия.

Чтобы реализовать логику Teams обработчиков действий, необходимо переопредить методы в боте, как показано в разделе [логика](#bot-logic) бота. Для этих обработчиков не существует базовой реализации, поэтому в переопределяемой логике необходимо добавить логику.

---

## <a name="bot-logic"></a>Логика бота

Логика бота обрабатывает входящие действия из одного или более каналов бота и в ответ создает исходящую деятельность. Это по-прежнему относится к ботам, полученным Teams обработить действия, которые сначала проверяют Teams действий. После проверки Teams действий он передает все другие действия обработивею действий Bot Framework.

# <a name="c"></a>[C#](#tab/csharp)

#### <a name="core-bot-framework-handlers"></a>Обработчики Core Bot Framework

>[!NOTE]
> За **исключением** действий  добавленных и удаленых участников, все обработчики действий, описанные в этом разделе, продолжают работать так же, как и с Teams ботом.

Обработчики действий отличаются в контексте группы, где новый член добавляется в команду вместо потока сообщений.

В список обработчиков, определенных в списке `ActivityHandler` , входят следующие:

| Событие | Обработник | Описание |
| :-- | :-- | :-- |
| Любой полученный тип действий | `OnTurnAsync` | Этот метод вызывает один из других обработчиков в зависимости от типа полученной активности. |
| Полученная активность сообщений | `OnMessageActivityAsync` | Этот метод может быть переопределен для обработки `Message` действий. |
| Получена активность обновления беседы | `OnConversationUpdateActivityAsync` | Этот метод вызывает обработник, если участники, помимо бота, присоединились или покинули беседу, в `ConversationUpdate` действии. |
| Участники, не вступив в бот, присоединились к беседе | `OnMembersAddedAsync` | Этот метод может быть переопределен для обработки участников, присоединявшихся к беседе. |
| Участники, не вносяые в боты, покинули беседу | `OnMembersRemovedAsync` | Этот метод может быть переопределен для обработки участников, покидая беседу. |
| Полученная активность событий | `OnEventActivityAsync` | Этот метод вызывает обработок, определенный типу события, в `Event` действии. |
| Полученная активность событий token-response | `OnTokenResponseEventAsync` | Этот метод может быть переопределен для обработки событий отклика маркеров. |
| Получена активность событий, не относяка к маркерам | `OnEventAsync` | Этот метод может быть переопределен для обработки других типов событий. |
| Другой полученный тип действий | `OnUnrecognizedActivityTypeAsync` | Этот метод может быть переопределен для обработки любого типа действий в противном случае без рукой. |

#### <a name="teams-specific-activity-handlers"></a>Teams обработчики действий

Список `TeamsActivityHandler` обработчиков в разделе обработчики core Bot Framework расширяется, чтобы включить следующие:

| Событие | Обработник | Описание |
| :-- | :-- | :-- |
| channelCreated | `OnTeamsChannelCreatedAsync` | Этот метод может быть переопределен для обработки создаемого Teams канала. Дополнительные сведения см. в [канале, созданном в](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created) [событиях обновления беседы](https://aka.ms/azure-bot-subscribe-to-conversation-events). |
| channelDeleted | `OnTeamsChannelDeletedAsync` | Этот метод может быть переопределен для обработки удаленного Teams канала. Дополнительные сведения см. в [ссылке на канал, удаленный в](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted) [событиях обновления беседы](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| ChannelRenamed | `OnTeamsChannelRenamedAsync` | Этот метод может быть переопределен для обработки Teams переименования канала. Дополнительные сведения см. в [ссылке на канал, переименованный](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed) в [событиях обновления беседы](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| переименованная команда | `OnTeamsTeamRenamedAsync` | `return Task.CompletedTask;`Этот метод может быть переопределен для обработки Teams переименованной группы. Дополнительные сведения см. в [группе, переименованной в](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) [событиях обновления беседы](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| MembersAdded | `OnTeamsMembersAddedAsync` | Этот метод вызывает метод `OnMembersAddedAsync` в `ActivityHandler`. Метод может быть переопределен для обработки участников, присоединявшихся к команде. Дополнительные сведения см. в [дополнительных сведениях, добавленных участниками группы](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added) в [событиях обновления беседы](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| MembersRemoved | `OnTeamsMembersRemovedAsync` | Этот метод вызывает метод `OnMembersRemovedAsync` в `ActivityHandler`. Метод может быть переопределен для обработки участников, покидая команду. Дополнительные сведения см. в [дополнительных сведениях о членах группы, удаленых в](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed) [событиях обновления беседы](https://aka.ms/azure-bot-subscribe-to-conversation-events).|

#### <a name="teams-invoke-activities"></a>Teams действия

Список обработчиков Teams, `OnInvokeActivityAsync` которые вызваны из обработчика Teams действий, включает следующие:

| Типы ссылок                    | Обработник                              | Описание                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `OnTeamsCardActionInvokeAsync`       | Этот метод вызывается при вызове действия карты из соединитетеля. |
| fileConsent/invoke              | `OnTeamsFileConsentAcceptAsync`      | Этот метод вызывается при приеме пользователем карточки согласия на файл. |
| fileConsent/invoke              | `OnTeamsFileConsentAsync`            | Этот метод вызывается, когда действие карточки согласия на файл получается из соединитетеля. |
| fileConsent/invoke              | `OnTeamsFileConsentDeclineAsync`     | Этот метод вызывается при отклонении пользователем карточки согласия на файл. |
| actionableMessage/executeAction | `OnTeamsO365ConnectorCardActionAsync` | Этот метод вызывается при Office 365 действия карты соединиттеля, полученной из соединитетеля. |
| signin/verifyState              | `OnTeamsSigninVerifyStateAsync`      | Этот метод вызывается при проверке действия signIn состояния, полученного из соединитетеля. |
| task/fetch                      | `OnTeamsTaskModuleFetchAsync`        | Этот метод может быть переопределен в производных классах, чтобы обеспечить логику при извлечении модуля задач. |
| task/submit                     | `OnTeamsTaskModuleSubmitAsync`       | Этот метод может быть переопределен в производных классах, чтобы обеспечить логику при отправке модуля задач. |

Действия вызова, перечисленные в этом разделе, для разговорных ботов в Teams. SDK Bot Framework также поддерживает вызов действий, определенных для расширений обмена сообщениями. Дополнительные сведения см. [в дополнительных сведениях о расширении обмена сообщениями](https://aka.ms/azure-bot-what-are-messaging-extensions).

# <a name="javascript"></a>[JavaScript](#tab/javascript)

#### <a name="core-bot-framework-handlers"></a>Обработчики Core Bot Framework

>[!NOTE]
> За **исключением** действий  добавленных и удаленых участников, все обработчики действий, описанные в этом разделе, продолжают работать так же, как и с Teams ботом.

Обработчики действий отличаются в контексте группы, где новый член добавляется в команду вместо потока сообщений.

В список обработчиков, определенных в списке `ActivityHandler` , входят следующие:

| Событие | Обработник | Описание |
| :-- | :-- | :-- |
| Любой полученный тип действий | `onTurn` | Этот метод вызывает один из других обработчиков в зависимости от типа полученной активности. |
| Полученная активность сообщений | `onMessage` | Этот метод помогает обрабатывать `Message` действия. |
| Получена активность обновления беседы | `onConversationUpdate` | Этот метод вызывает обработник, если участники, помимо бота, присоединились или покинули беседу, в `ConversationUpdate` действии. |
| Участники, не вступив в бот, присоединились к беседе | `onMembersAdded` | Этот метод помогает обрабатывать присоединение участников к беседе. |
| Участники, не вносяые в боты, покинули беседу | `onMembersRemoved` | Этот метод помогает обрабатывать участников, покидая беседу. |
| Полученная активность событий | `onEvent` | Этот метод вызывает обработок, определенный типу события, в `Event` действии. |
| Полученная активность событий token-response | `onTokenResponseEvent` | Этот метод помогает обрабатывать события отклика маркеров. |
| Другой полученный тип действий | `onUnrecognizedActivityType` | Этот метод помогает обрабатывать любые типы действий в противном случае без проблем. |

#### <a name="teams-specific-activity-handlers"></a>Teams обработчики действий

Список `TeamsActivityHandler` обработчиков в разделе обработчики core Bot Framework расширяется, чтобы включить следующие:

| Событие | Обработник | Описание |
| :-- | :-- | :-- |
| channelCreated | `OnTeamsChannelCreatedAsync` | Этот метод может быть переопределен для обработки создаемого Teams канала. Дополнительные сведения см. в [канале, созданном в](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created) [событиях обновления беседы](https://aka.ms/azure-bot-subscribe-to-conversation-events). |
| channelDeleted | `OnTeamsChannelDeletedAsync` | Этот метод может быть переопределен для обработки удаленного Teams канала. Дополнительные сведения см. в [ссылке на канал, удаленный в](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted) [событиях обновления беседы](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| ChannelRenamed | `OnTeamsChannelRenamedAsync` | Этот метод может быть переопределен для обработки Teams переименования канала. Дополнительные сведения см. в [ссылке на канал, переименованный](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed) в [событиях обновления беседы](https://aka.ms/azure-bot-subscribe-to-conversation-events). |
| переименованная команда | `OnTeamsTeamRenamedAsync` | `return Task.CompletedTask;`Этот метод может быть переопределен для обработки Teams переименованной группы. Дополнительные сведения см. в [группе, переименованной в](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) [событиях обновления беседы](https://aka.ms/azure-bot-subscribe-to-conversation-events). |
| MembersAdded | `OnTeamsMembersAddedAsync` | Этот метод вызывает метод `OnMembersAddedAsync` в `ActivityHandler`. Метод может быть переопределен для обработки участников, присоединявшихся к команде. Дополнительные сведения см. в [дополнительных сведениях, добавленных участниками группы](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added) в [событиях обновления беседы](https://aka.ms/azure-bot-subscribe-to-conversation-events). |
| MembersRemoved | `OnTeamsMembersRemovedAsync` | Этот метод вызывает метод `OnMembersRemovedAsync` в `ActivityHandler`. Метод может быть переопределен для обработки участников, покидая команду. Дополнительные сведения см. в [дополнительных сведениях о членах группы, удаленых в](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed) [событиях обновления беседы](https://aka.ms/azure-bot-subscribe-to-conversation-events). |

#### <a name="teams-invoke-activities"></a>Teams действия

Список обработчиков Teams, `onInvokeActivity` которые вызваны из обработчика Teams действий, включает следующие:

| Типы ссылок                    | Обработник                              | Описание                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `handleTeamsCardActionInvoke`       | Этот метод вызывается при вызове действия карты из соединитетеля. |
| fileConsent/invoke              | `handleTeamsFileConsentAccept`      | Этот метод вызывается при приеме пользователем карточки согласия на файл. |
| fileConsent/invoke              | `handleTeamsFileConsent`            | Этот метод вызывается, когда действие карточки согласия на файл получается из соединитетеля. |
| fileConsent/invoke              | `handleTeamsFileConsentDecline`     | Этот метод вызывается при отклонении пользователем карточки согласия на файл. |
| actionableMessage/executeAction | `handleTeamsO365ConnectorCardAction` | Этот метод вызывается при Office 365 действия карты соединиттеля, полученной из соединитетеля. |
| signin/verifyState              | `handleTeamsSigninVerifyState`      | Этот метод вызывается при проверке действия signIn состояния, полученного из соединитетеля. |
| task/fetch                      | `handleTeamsTaskModuleFetch`        | Этот метод может быть переопределен в производных классах, чтобы обеспечить логику при извлечении модуля задач. |
| task/submit                     | `handleTeamsTaskModuleSubmit`       | Этот метод может быть переопределен в производных классах, чтобы обеспечить логику при отправке модуля задач. |

Действия вызова, перечисленные в этом разделе, для разговорных ботов в Teams. SDK Bot Framework также поддерживает вызов действий, определенных для расширений обмена сообщениями. Дополнительные сведения см. [в дополнительных сведениях о расширении обмена сообщениями](https://aka.ms/azure-bot-what-are-messaging-extensions).

# <a name="python"></a>[Python](#tab/python)

#### <a name="core-bot-framework-handlers"></a>Обработчики Core Bot Framework

>[!NOTE]
> За **исключением** действий  добавленных и удаленых участников, все обработчики действий, описанные в этом разделе, продолжают работать так же, как и с Teams ботом.

Обработчики действий отличаются в контексте группы, где новый член добавляется в команду вместо потока сообщений.

В список обработчиков, определенных в списке `ActivityHandler` , входят следующие:

| Событие | Обработник | Описание |
| :-- | :-- | :-- |
| Любой полученный тип действий | `on_turn` | Этот метод вызывает один из других обработчиков в зависимости от типа полученной активности. |
| Полученная активность сообщений | `on_message_activity` | Этот метод может быть переопределен для обработки `Message` действий. |
| Получена активность обновления беседы | `on_conversation_update_activity` | Этот метод вызывает обработник, если участники, кроме бота, присоединяются или покидают беседу. |
| Участники, не вступив в бот, присоединились к беседе | `on_members_added_activity` | Этот метод может быть переопределен для обработки участников, присоединявшихся к беседе. |
| Участники, не вносяые в боты, покинули беседу | `on_members_removed_activity` | Этот метод может быть переопределен для обработки участников, покидая беседу. |
| Полученная активность событий | `on_event_activity` | Этот метод вызывает обработник, определенный типу события. |
| Полученная активность событий token-response | `on_token_response_event` | Этот метод может быть переопределен для обработки событий отклика маркеров. |
| Получена активность событий, не относяка к маркерам | `on_event` | Этот метод может быть переопределен для обработки других типов событий. |
| Другие полученные типы действий | `on_unrecognized_activity_type` | Этот метод может быть переопределен для обработки любого типа действий, которые не обрабатываются. |

#### <a name="teams-specific-activity-handlers"></a>Teams обработчики действий

Список `TeamsActivityHandler` обработчиков из основного раздела обработчиков Bot Framework расширяется, включив в него следующие:

| Событие | Обработник | Описание |
| :-- | :-- | :-- |
| channelCreated | `on_teams_channel_created` | Этот метод может быть переопределен для обработки создаемого Teams канала. Дополнительные сведения см. в [канале, созданном в](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created) [событиях обновления беседы](https://aka.ms/azure-bot-subscribe-to-conversation-events). |
| channelDeleted | `on_teams_channel_deleted` | Этот метод может быть переопределен для обработки удаленного Teams канала. Дополнительные сведения см. в [ссылке на канал, удаленный в](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted) [событиях обновления беседы](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| ChannelRenamed | `on_teams_channel_renamed` | Этот метод может быть переопределен для обработки Teams переименования канала. Дополнительные сведения см. в [ссылке на канал, переименованный](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed) в [событиях обновления беседы](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| переименованная команда | `on_teams_team_renamed` | `return Task.CompletedTask;`Этот метод может быть переопределен для обработки Teams переименованной группы. Дополнительные сведения см. в [группе, переименованной в](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) [событиях обновления беседы](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| MembersAdded | `on_teams_members_added` | Этот метод вызывает метод `OnMembersAddedAsync` в `ActivityHandler`. Метод может быть переопределен для обработки участников, присоединявшихся к команде. Дополнительные сведения см. в [дополнительных сведениях, добавленных участниками группы](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added) в [событиях обновления беседы](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| MembersRemoved | `on_teams_members_removed` | Этот метод вызывает метод `OnMembersRemovedAsync` в `ActivityHandler`. Метод может быть переопределен для обработки участников, покидая команду. Дополнительные сведения см. в [дополнительных сведениях о членах группы, удаленых в](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed) [событиях обновления беседы](https://aka.ms/azure-bot-subscribe-to-conversation-events).|

#### <a name="teams-invoke-activities"></a>Teams действия

Список обработчиков Teams, `on_invoke_activity` которые вызваны из обработчика Teams действий, включает следующие:

| Типы ссылок                    | Обработник                              | Описание                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `on_teams_card_action_invoke`       | Этот метод вызывается при вызове действия карты из соединитетеля. |
| fileConsent/invoke              | `on_teams_file_consent_accept`      | Этот метод вызывается при приеме пользователем карточки согласия на файл. |
| fileConsent/invoke              | `on_teams_file_consent`            | Этот метод вызывается, когда действие карточки согласия на файл получается из соединитетеля. |
| fileConsent/invoke              | `on_teams_file_consent_decline`     | Этот метод вызывается при отклонении пользователем карточки согласия на файл. |
| actionableMessage/executeAction | `on_teams_o365_connector_card_action` | Этот метод вызывается при Office 365 действия карты соединиттеля, полученной из соединитетеля. |
| signin/verifyState              | `on_teams_signin_verify_state`      | Этот метод вызывается при проверке действия signIn состояния, полученного из соединитетеля. |
| task/fetch                      | `on_teams_task_module_fetch`        | Этот метод может быть переопределен в производных классах, чтобы обеспечить логику при извлечении модуля задач. |
| task/submit                     | `on_teams_task_module_submit`       | Этот метод может быть переопределен в производных классах, чтобы обеспечить логику при отправке модуля задач. |

Действия вызова, перечисленные в этом разделе, для разговорных ботов в Teams. SDK Bot Framework также поддерживает вызов действий, определенных для расширений обмена сообщениями. Дополнительные сведения см. [в дополнительных сведениях о расширении обмена сообщениями](https://aka.ms/azure-bot-what-are-messaging-extensions).

---

* * *

Теперь, когда вы ознакомились с обработчиками действий ботов, давайте посмотрим, как боты ведут себя по-разному в зависимости от беседы и сообщений, которые они получают или отправляют.

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Основы разговора](~/bots/how-to/conversations/conversation-basics.md)
