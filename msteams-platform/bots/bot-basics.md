---
title: Обработчики действий ботов
author: surbhigupta
description: Сведения о событиях и обработчиках действий Microsoft Teams для сообщений, каналов, команд, участников, упоминаний, проверки подлинности, действий с карточками с помощью Microsoft Bot Framework SDK.
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: 4780c4c2ca3965186411f7927f1fb5b555647004
ms.sourcegitcommit: b918181217995a47be34632e1051d0f4d4d481b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/12/2022
ms.locfileid: "67321210"
---
# <a name="bot-activity-handlers"></a>Обработчики действий ботов

Этот документ берет за основу статью о том, [как работают боты](https://aka.ms/how-bots-work): [Документация по платформе ботов](https://aka.ms/azure-bot-service-docs). Основное различие между ботами, разработанными для Microsoft Teams, и основной платформой Bot Framework заключается в функциях, предоставляемых в Teams.

Чтобы организовать логику беседы для вашего бота, используется обработчик действий. Действия обрабатываются двумя способами: с помощью обработчиков действий Teams и логики бота. Обработчик действий Teams добавляет поддержку событий и взаимодействий, относящихся к Teams. Объект бота содержит логику беседы для поворота и отображает обработчик поворота, который является методом, который может принимать входящие действия от адаптера бота.

## <a name="teams-activity-handlers"></a>Обработчики действий Teams

Обработчик действий Teams является производным от обработчика действий Microsoft Bot Framework. Он перенаправляет все действия Teams, прежде чем разрешит обработку любых действий, не относящихся к Teams.

Когда бот для Teams получает действие, оно направляется в обработчики действий. Все действия перенаправляются через один базовый обработчик, называемый обработчиком поворота. Обработчик поворота вызывает необходимый обработчик действий для управления полученными действиями. Бот Teams является производным от класса `TeamsActivityHandler`, который является производным от класса `ActivityHandler`.

> [!NOTE]
> Если обработка действия бота занимает более 15 секунд, Teams отправляет запрос на повторную попытку в конечную точку бота. Таким образом, в боте будут отображаться повторяющиеся запросы.

# <a name="c"></a>[C#](#tab/csharp)

Боты создаются с помощью Bot Framework. Если боты получают действие с сообщением, обработчик поворота получает уведомление об этом входящем действии. Затем обработчик поворота отправляет входящие действия обработчику действий `OnMessageActivityAsync`. В Teams эта функция остается той же. Если бот получает действие обновления беседы, обработчик поворота получает уведомление о входящих действиях и отправляет входящие действия в `OnConversationUpdateActivityAsync`. Обработчик действий Teams сначала проверяет наличие определенных событий Teams. Если события найдены, их передают в обработчик действий Bot Framework.

В классе обработчиков действий Teams есть два основных обработчика действий Teams: `OnConversationUpdateActivityAsync` и `OnInvokeActivityAsync`. `OnConversationUpdateActivityAsync` маршрутизирует все действия по обновлению беседы, а `OnInvokeActivityAsync` маршрутизирует все действия вызова Teams.

Чтобы реализовать логику для конкретных обработчиков действий Teams, необходимо переопределить методы в боте, как показано в разделе [Логика бота](#bot-logic). Базовая реализация этих обработчиков отсутствует. Поэтому добавьте логику, которую нужно переопределить.

Фрагменты кода для обработчиков действий Teams:

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

Боты создаются с помощью Bot Framework. Если боты получают действие с сообщением, обработчик поворота получает уведомление об этом входящем действии. Затем обработчик поворота отправляет входящие действия обработчику действий `onMessage`. В Teams эта функция остается той же. Если бот получает действие обновления беседы, обработчик поворота получает уведомление о входящих действиях и отправляет входящие действия в `dispatchConversationUpdateActivity`. Обработчик действий Teams сначала проверяет наличие определенных событий Teams. Если события найдены, их передают в обработчик действий Bot Framework.

В классе обработчиков действий Teams есть два основных обработчика действий Teams: `dispatchConversationUpdateActivity` и `onInvokeActivity`. `dispatchConversationUpdateActivity` маршрутизирует все действия по обновлению беседы, а `onInvokeActivity` маршрутизирует все действия вызова Teams.

Чтобы реализовать логику для конкретных обработчиков действий Teams, необходимо переопределить методы в боте, как показано в разделе [Логика бота](#bot-logic). Определите логику бота для этих обработчиков, а затем обязательно вызовите `next()` в конце. Выполнив вызов `next()`, убедитесь, что выполняется следующий обработчик.

Фрагменты кода для обработчиков действий Teams:

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

Боты создаются с помощью Bot Framework. Если боты получают действие с сообщением, обработчик поворота получает уведомление об этом входящем действии. Затем обработчик поворота отправляет входящие действия обработчику действий `on_message_activity`. В Teams эта функция остается той же. Если бот получает действие обновления беседы, обработчик поворота получает уведомление о входящих действиях и отправляет входящие действия в `on_conversation_update_activity`. Обработчик действий Teams сначала проверяет наличие определенных событий Teams. Если события найдены, их передают в обработчик действий Bot Framework.

В классе обработчиков действий Teams есть два основных обработчика действий Teams: `on_conversation_update_activity` и `on_invoke_activity`. `on_conversation_update_activity` маршрутизирует все действия по обновлению беседы, а `on_invoke_activity` маршрутизирует все действия вызова Teams.

Чтобы реализовать логику для конкретных обработчиков действий Teams, необходимо переопределить методы в боте, как показано в разделе [Логика бота](#bot-logic). Базовая реализация этих обработчиков отсутствует. Поэтому добавьте логику, которую нужно переопределить.

---

## <a name="bot-logic"></a>Логика бота

Логика бота обрабатывает входящие действия из одного или более каналов бота и в ответ создает исходящие действия. Это по-прежнему относится к ботам, производным от класса обработчика действий Teams, который сначала проверяет действия Teams. После проверки действий Teams все остальные действия передается в обработчик действий Bot Framework.

# <a name="c"></a>[C#](#tab/csharp)

#### <a name="core-bot-framework-handlers"></a>Основные обработчики Bot Framework

>[!NOTE]
>
>* За исключением **добавленных** и **удаленных** действий участников, все обработчики действий, описанные в этом разделе, продолжают работать так же, как и с ботом, не относящимся к Teams.
>* Метод `onInstallationUpdateActivityAsync()` используется для получения языкового стандарты Teams при добавлении бота в Teams.

Обработчики действий отличаются в контексте команды, где в команду добавляется новый участник, а не цепочка сообщений.

Список обработчиков, определенных в `ActivityHandler` списке, включает в себя следующее:

| Событие | Обработчик | Описание |
| :-- | :-- | :-- |
| Любой полученный тип действия | `OnTurnAsync` | Этот метод вызывает один из других обработчиков в зависимости от типа полученного действия. |
| Получено действий с сообщением | `OnMessageActivityAsync` | Этот метод может быть переопределен для обработки действия `Message`. |
| Получено действие обновления беседы | `OnConversationUpdateActivityAsync` | Этот метод вызывает обработчик для действия `ConversationUpdate`, если участники, кроме бота, присоединяются к беседе или выходят из нее. |
| К беседе присоединились участники, не являющиеся ботами | `OnMembersAddedAsync` | Этот метод может быть переопределен для обработки присоединения участников к беседе. |
| Участники, не боты, покинули беседу | `OnMembersRemovedAsync` | Этот метод может быть переопределен для обработки выхода участников из беседе. |
| Получено действие события | `OnEventActivityAsync` | Этот метод вызывает для действия `Event` определенный обработчик для типа события. |
| Получено действие события токена-ответа | `OnTokenResponseEventAsync` | Этот метод может быть переопределен для обработки событий ответа маркера. |
| Получено действие события, не относящегося к токену-ответу | `OnEventAsync` | Этот метод может быть переопределен для обработки других типов событий. |
| Получен другой тип действия | `OnUnrecognizedActivityTypeAsync` | Этот метод может быть переопределен для обработки любого типа действия, для которого в противном случае обработка была недоступна. |

#### <a name="teams-specific-activity-handlers"></a>Обработчики действий для Teams

Обработчик `TeamsActivityHandler` расширяет список обработчиков в разделе основных обработчиков Bot Framework, включая следующие:

| Событие | Обработчик | Описание |
| :-- | :-- | :-- |
| channelCreated | `OnTeamsChannelCreatedAsync` | Этот метод может быть переопределен для обработки создания канала Teams. Дополнительные сведения см. в разделе [создания канала](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created) в [событиях обновления беседы](https://aka.ms/azure-bot-subscribe-to-conversation-events). |
| ChannelDeleted | `OnTeamsChannelDeletedAsync` | Этот метод может быть переопределен для обработки удаления канала Teams. Дополнительные сведения см. в разделе [удаления канала](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted) в [событиях обновления беседы](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| channelRenamed | `OnTeamsChannelRenamedAsync` | Этот метод может быть переопределен для обработки переименования канала Teams. Дополнительные сведения см. в разделе [переименования канала](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed) в [событиях обновления беседы](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| teamRenamed | `OnTeamsTeamRenamedAsync` | `return Task.CompletedTask;` Этот метод может быть переопределен для обработки переименования команды Teams. Дополнительные сведения см. в разделе [переименования команды](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) в [событиях обновления беседы](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| MembersAdded | `OnTeamsMembersAddedAsync` | Этот метод вызывает метод `OnMembersAddedAsync` в `ActivityHandler`. Этот метод может быть переопределен для обработки присоединения участников к команде. Дополнительные сведения см. в разделе [добавления участников команды](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added) в [событиях обновления беседы](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| MembersRemoved | `OnTeamsMembersRemovedAsync` | Этот метод вызывает метод `OnMembersRemovedAsync` в `ActivityHandler`. Этот метод может быть переопределен для обработки выхода участников из команды. Дополнительные сведения см. в разделе [удаления участников команды](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed) в [событиях обновления беседы](https://aka.ms/azure-bot-subscribe-to-conversation-events).|

#### <a name="teams-invoke-activities"></a>Запуск действий Teams

Список обработчиков действий Teams, вызываемый `OnInvokeActivityAsync` из обработчика действий Teams, включает в себя следующее:

| Типы вызовов                    | Обработчик                              | Описание                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `OnTeamsCardActionInvokeAsync`       | Этот метод вызывается, когда от соединителя получено действие вызова действия карточки. |
| fileConsent/invoke              | `OnTeamsFileConsentAcceptAsync`      | Этот метод вызывается, когда пользователь принимает карточку согласия на файл. |
| fileConsent/invoke              | `OnTeamsFileConsentAsync`            | Этот метод вызывается, когда от соединителя получено действие карточки согласия на файл. |
| fileConsent/invoke              | `OnTeamsFileConsentDeclineAsync`     | Этот метод вызывается, когда пользователь отклоняет карточку согласия на файл. |
| actionableMessage/executeAction | `OnTeamsO365ConnectorCardActionAsync` | Этот метод вызывается при получении Office 365 действия карточки соединителя от соединителя. |
| signin/verifyState              | `OnTeamsSigninVerifyStateAsync`      | Этот метод вызывается, когда от соединителя получено действие проверки состояния входа. |
| task/fetch                      | `OnTeamsTaskModuleFetchAsync`        | Этот метод может быть переопределен в производном классе для предоставления логики при извлечении модуля задачи. |
| task/submit                     | `OnTeamsTaskModuleSubmitAsync`       | Этот метод может быть переопределен в производном классе для предоставления логики при отправке модуля задачи. |

Действия Invoke, перечисленные в этом разделе, предназначены для чат-ботов в Teams. Пакет SDK Bot Framework также поддерживает вызов действий, характерных для расширений для сообщений. Дополнительные сведения см. в статье о том, [что такое расширения для сообщений](https://aka.ms/azure-bot-what-are-messaging-extensions).

# <a name="javascript"></a>[JavaScript](#tab/javascript)

#### <a name="core-bot-framework-handlers"></a>Основные обработчики Bot Framework

>[!NOTE]
> За исключением **добавленных** и **удаленных** действий участников, все обработчики действий, описанные в этом разделе, продолжают работать так же, как и с ботом, не относящимся к Teams.

Обработчики действий отличаются в контексте команды, где в команду добавляется новый участник, а не цепочка сообщений.

Список обработчиков, определенных в `ActivityHandler` списке, включает в себя следующее:

| Событие | Обработчик | Описание |
| :-- | :-- | :-- |
| Любой полученный тип действия | `onTurn` | Этот метод вызывает один из других обработчиков в зависимости от типа полученного действия. |
| Получено действий с сообщением | `onMessage` | Этот метод помогает обрабатывать действия `Message`. |
| Получено действие обновления беседы | `onConversationUpdate` | Этот метод вызывает обработчик для действия `ConversationUpdate`, если участники, кроме бота, присоединяются к беседе или выходят из нее. |
| К беседе присоединились участники, не являющиеся ботами | `onMembersAdded` | Этот метод помогает обработать присоединение участников к беседе. |
| Участники, не боты, покинули беседу | `onMembersRemoved` | Этот метод помогает обработать выход участников из беседы. |
| Получено действие события | `onEvent` | Этот метод вызывает для действия `Event` определенный обработчик для типа события. |
| Получено действие события токена-ответа | `onTokenResponseEvent` | Этот метод помогает обрабатывать события ответа маркера. |
| Получен другой тип действия | `onUnrecognizedActivityType` | Этот метод помогает обрабатывать любой тип действия, для которого в противном случае обработка была недоступна. |

#### <a name="teams-specific-activity-handlers"></a>Обработчики действий для Teams

Обработчик `TeamsActivityHandler` расширяет список обработчиков в разделе основных обработчиков Bot Framework, включая следующие:

| Событие | Обработчик | Описание |
| :-- | :-- | :-- |
| channelCreated | `OnTeamsChannelCreatedAsync` | Этот метод может быть переопределен для обработки создания канала Teams. Дополнительные сведения см. в разделе [создания канала](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created) в [событиях обновления беседы](https://aka.ms/azure-bot-subscribe-to-conversation-events). |
| ChannelDeleted | `OnTeamsChannelDeletedAsync` | Этот метод может быть переопределен для обработки удаления канала Teams. Дополнительные сведения см. в разделе [удаления канала](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted) в [событиях обновления беседы](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| channelRenamed | `OnTeamsChannelRenamedAsync` | Этот метод может быть переопределен для обработки переименования канала Teams. Дополнительные сведения см. в разделе [переименования канала](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed) в [событиях обновления беседы](https://aka.ms/azure-bot-subscribe-to-conversation-events). |
| teamRenamed | `OnTeamsTeamRenamedAsync` | `return Task.CompletedTask;` Этот метод может быть переопределен для обработки переименования команды Teams. Дополнительные сведения см. в разделе [переименования команды](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) в [событиях обновления беседы](https://aka.ms/azure-bot-subscribe-to-conversation-events). |
| MembersAdded | `OnTeamsMembersAddedAsync` | Этот метод вызывает метод `OnMembersAddedAsync` в `ActivityHandler`. Этот метод может быть переопределен для обработки присоединения участников к команде. Дополнительные сведения см. в разделе [добавления участников команды](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added) в [событиях обновления беседы](https://aka.ms/azure-bot-subscribe-to-conversation-events). |
| MembersRemoved | `OnTeamsMembersRemovedAsync` | Этот метод вызывает метод `OnMembersRemovedAsync` в `ActivityHandler`. Этот метод может быть переопределен для обработки выхода участников из команды. Дополнительные сведения см. в разделе [удаления участников команды](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed) в [событиях обновления беседы](https://aka.ms/azure-bot-subscribe-to-conversation-events). |

#### <a name="teams-invoke-activities"></a>Запуск действий Teams

Список обработчиков действий Teams, вызываемый `onInvokeActivity` из обработчика действий Teams, включает в себя следующее:

| Типы вызовов                    | Обработчик                              | Описание                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `handleTeamsCardActionInvoke`       | Этот метод вызывается, когда от соединителя получено действие вызова действия карточки. |
| fileConsent/invoke              | `handleTeamsFileConsentAccept`      | Этот метод вызывается, когда пользователь принимает карточку согласия на файл. |
| fileConsent/invoke              | `handleTeamsFileConsent`            | Этот метод вызывается, когда от соединителя получено действие карточки согласия на файл. |
| fileConsent/invoke              | `handleTeamsFileConsentDecline`     | Этот метод вызывается, когда пользователь отклоняет карточку согласия на файл. |
| actionableMessage/executeAction | `handleTeamsO365ConnectorCardAction` | Этот метод вызывается при получении Office 365 действия карточки соединителя от соединителя. |
| signin/verifyState              | `handleTeamsSigninVerifyState`      | Этот метод вызывается, когда от соединителя получено действие проверки состояния входа. |
| task/fetch                      | `handleTeamsTaskModuleFetch`        | Этот метод может быть переопределен в производном классе для предоставления логики при извлечении модуля задачи. |
| task/submit                     | `handleTeamsTaskModuleSubmit`       | Этот метод может быть переопределен в производном классе для предоставления логики при отправке модуля задачи. |

Действия по вызову, перечисленные в этом разделе, посвящены ботам бесед в Teams. Пакет SDK Bot Framework также поддерживает вызов действий, характерных для расширений для сообщений. Дополнительные сведения см. в статье о том, [что такое расширения для сообщений](https://aka.ms/azure-bot-what-are-messaging-extensions).

# <a name="python"></a>[Python](#tab/python)

#### <a name="core-bot-framework-handlers"></a>Основные обработчики Bot Framework

>[!NOTE]
> За исключением **добавленных** и **удаленных** действий участников, все обработчики действий, описанные в этом разделе, продолжают работать так же, как и с ботом, не относящимся к Teams.

Обработчики действий отличаются в контексте команды, где в команду добавляется новый участник, а не цепочка сообщений.

Список обработчиков, определенных в `ActivityHandler` списке, включает в себя следующее:

| Событие | Обработчик | Описание |
| :-- | :-- | :-- |
| Любой полученный тип действия | `on_turn` | Этот метод вызывает один из других обработчиков в зависимости от типа полученного действия. |
| Получено действий с сообщением | `on_message_activity` | Этот метод может быть переопределен для обработки действия `Message`. |
| Получено действие обновления беседы | `on_conversation_update_activity` | Этот метод вызывает обработчик, если участники, кроме бота, присоединяются к беседе или выходят из нее. |
| К беседе присоединились участники, не являющиеся ботами | `on_members_added_activity` | Этот метод может быть переопределен для обработки присоединения участников к беседе. |
| Участники, не боты, покинули беседу | `on_members_removed_activity` | Этот метод может быть переопределен для обработки выхода участников из беседе. |
| Получено действие события | `on_event_activity` | Этот метод вызывает обработчик для определенного типа события. |
| Получено действие события токена-ответа | `on_token_response_event` | Этот метод может быть переопределен для обработки событий ответа маркера. |
| Получено действие события, не относящегося к токену-ответу | `on_event` | Этот метод может быть переопределен для обработки других типов событий. |
| Получены другие типы действий | `on_unrecognized_activity_type` | Этот метод можно переопределить для обработки любого типа действия, которое не обрабатывается. |

#### <a name="teams-specific-activity-handlers"></a>Обработчики действий для Teams

Обработчик `TeamsActivityHandler` расширяет список обработчиков из раздела основных обработчиков Bot Framework, включая следующие:

| Событие | Обработчик | Описание |
| :-- | :-- | :-- |
| channelCreated | `on_teams_channel_created` | Этот метод может быть переопределен для обработки создания канала Teams. Дополнительные сведения см. в разделе [создания канала](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created) в [событиях обновления беседы](https://aka.ms/azure-bot-subscribe-to-conversation-events). |
| ChannelDeleted | `on_teams_channel_deleted` | Этот метод может быть переопределен для обработки удаления канала Teams. Дополнительные сведения см. в разделе [удаления канала](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted) в [событиях обновления беседы](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| channelRenamed | `on_teams_channel_renamed` | Этот метод может быть переопределен для обработки переименования канала Teams. Дополнительные сведения см. в разделе [переименования канала](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed) в [событиях обновления беседы](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| teamRenamed | `on_teams_team_renamed` | `return Task.CompletedTask;` Этот метод может быть переопределен для обработки переименования команды Teams. Дополнительные сведения см. в разделе [переименования команды](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) в [событиях обновления беседы](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| MembersAdded | `on_teams_members_added` | Этот метод вызывает метод `OnMembersAddedAsync` в `ActivityHandler`. Этот метод может быть переопределен для обработки присоединения участников к команде. Дополнительные сведения см. в разделе [добавления участников команды](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added) в [событиях обновления беседы](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| MembersRemoved | `on_teams_members_removed` | Этот метод вызывает метод `OnMembersRemovedAsync` в `ActivityHandler`. Этот метод может быть переопределен для обработки выхода участников из команды. Дополнительные сведения см. в разделе [удаления участников команды](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed) в [событиях обновления беседы](https://aka.ms/azure-bot-subscribe-to-conversation-events).|

#### <a name="teams-invoke-activities"></a>Запуск действий Teams

Список обработчиков действий Teams, вызываемый `on_invoke_activity` из обработчика действий Teams, включает в себя следующее:

| Типы вызовов                    | Обработчик                              | Описание                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `on_teams_card_action_invoke`       | Этот метод вызывается, когда от соединителя получено действие вызова действия карточки. |
| fileConsent/invoke              | `on_teams_file_consent_accept`      | Этот метод вызывается, когда пользователь принимает карточку согласия на файл. |
| fileConsent/invoke              | `on_teams_file_consent`            | Этот метод вызывается, когда от соединителя получено действие карточки согласия на файл. |
| fileConsent/invoke              | `on_teams_file_consent_decline`     | Этот метод вызывается, когда пользователь отклоняет карточку согласия на файл. |
| actionableMessage/executeAction | `on_teams_o365_connector_card_action` | Этот метод вызывается при получении Office 365 действия карточки соединителя от соединителя. |
| signin/verifyState              | `on_teams_signin_verify_state`      | Этот метод вызывается, когда от соединителя получено действие проверки состояния входа. |
| task/fetch                      | `on_teams_task_module_fetch`        | Этот метод может быть переопределен в производном классе для предоставления логики при извлечении модуля задачи. |
| task/submit                     | `on_teams_task_module_submit`       | Этот метод может быть переопределен в производном классе для предоставления логики при отправке модуля задачи. |

Действия по вызову, перечисленные в этом разделе, посвящены ботам бесед в Teams. Пакет SDK Bot Framework также поддерживает вызов действий, характерных для расширений для сообщений. Дополнительные сведения см. в статье о том, [что такое расширения для сообщений](https://aka.ms/azure-bot-what-are-messaging-extensions).

---

---

Теперь, когда вы ознакомились с обработчиками действий бота, давайте посмотрим, как боты ведут себя по-разному в зависимости от беседы и получаемых или отправляемых сообщений.

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Основы разговора](~/bots/how-to/conversations/conversation-basics.md)
