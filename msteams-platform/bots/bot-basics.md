---
title: Обработчики действий ботов
author: surbhigupta
description: Общие сведения об обработчиках действий бота в Teams.
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: anclear
keywords: Событие канала согласия для карточки бота платформы обработчика действий
ms.openlocfilehash: 34dd5e8042b71f4e7cc78df7e7c543c86a53f58e
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104037"
---
# <a name="bot-activity-handlers"></a>Обработчики действий ботов

В этом документе показано, как [работают боты](https://aka.ms/how-bots-work) в основной [документации Bot Framework](https://aka.ms/azure-bot-service-docs). Основное различие между ботами, разработанными для Microsoft Teams и основной платформой Bot Framework, заключается в функциях, предоставляемых в Teams.

Для упорядочения логики общения для бота используется обработчик действий. Действия обрабатываются двумя способами с помощью Teams действий и логики бота. Обработчик Teams действия добавляет поддержку Microsoft Teams событий и взаимодействий. Объект бота содержит логику или логику диалога для шага и предоставляет обработчик шага, который является методом, который может принимать входящие действия из адаптера бота.

## <a name="teams-activity-handlers"></a>Teams действий

Teams обработчик действия является производным Microsoft Bot Framework обработчика действий пользователя. Он направляет все Teams, прежде чем разрешать обработку Teams действий, не связанных с конкретными действиями.

Когда бот для Teams получает действие, он направляется в обработчики действий. Все действия направляются через один базовый обработчик, называемый обработчиком шага. Обработчик шага вызывает обработчик требуемого действия для управления любым полученным действием. Бот Teams является производным от `TeamsActivityHandler` класса, который является производным от класса `ActivityHandler` Bot Framework.

# <a name="c"></a>[C#](#tab/csharp)

Боты создаются с помощью Bot Framework. Если боты получают действие сообщения, обработчик шага получает уведомление о входящем действии. Затем обработчик шага отправляет входящее действие обработчику `OnMessageActivityAsync` действий. В Teams эти функции остаются неизменными. Если бот получает действие обновления беседы, обработчик шага получает уведомление о входящем действии и отправляет входящее действие `OnConversationUpdateActivityAsync`в . Обработчик Teams действий сначала проверяет наличие Teams определенных событий. Если события не найдены, они передаются обработчику действий Bot Framework.

В классе Teams действий есть два основных Teams действий и `OnConversationUpdateActivityAsync` `OnInvokeActivityAsync`. `OnConversationUpdateActivityAsync`маршрутизирует все действия обновления беседы `OnInvokeActivityAsync` и направляет все Teams вызова.

Чтобы реализовать логику для Teams действий, необходимо переопределить методы в боте, как показано в разделе [логики](#bot-logic) бота. Для этих обработчиков нет базовой реализации, поэтому необходимо добавить логику, которую требуется переопределить.

Фрагменты кода для Teams действий:

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

Боты создаются с помощью Bot Framework. Если боты получают действие сообщения, обработчик шага получает уведомление о входящем действии. Затем обработчик шага отправляет входящее действие обработчику `onMessage` действий. В Teams эти функции остаются неизменными. Если бот получает действие обновления беседы, обработчик шага получает уведомление о входящем действии и отправляет входящее действие `dispatchConversationUpdateActivity`в . Обработчик Teams действий сначала проверяет наличие Teams определенных событий. Если события не найдены, они передаются обработчику действий Bot Framework.

В классе Teams действий есть два основных Teams действий и `dispatchConversationUpdateActivity` `onInvokeActivity`. `dispatchConversationUpdateActivity`маршрутизирует все действия обновления беседы `onInvokeActivity` и направляет все Teams вызова.

Чтобы реализовать логику для Teams действий, необходимо переопределить методы в боте, как показано в разделе [логики](#bot-logic) бота. Определите логику бота для этих обработчиков, а затем обязательно вызовите `next()` их в конце. Выполнив вызов `next()` , убедитесь, что выполняется следующий обработчик.

Фрагменты кода для Teams действий:

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

Боты создаются с помощью Bot Framework. Если боты получают действие сообщения, обработчик шага получает уведомление о входящем действии. Затем обработчик шага отправляет входящее действие обработчику `on_message_activity` действий. В Teams эти функции остаются неизменными. Если бот получает действие обновления беседы, обработчик шага получает уведомление о входящем действии и отправляет входящее действие `on_conversation_update_activity`в . Обработчик Teams действий сначала проверяет наличие Teams определенных событий. Если события не найдены, они передаются обработчику действий Bot Framework.

В классе Teams действий есть два основных Teams действий и `on_conversation_update_activity` `on_invoke_activity`. `on_conversation_update_activity`маршрутизирует все действия обновления беседы `on_invoke_activity` и направляет все Teams вызова.

Чтобы реализовать логику для Teams действий, необходимо переопределить методы в боте, как показано в разделе [логики](#bot-logic) бота. Для этих обработчиков нет базовой реализации, поэтому необходимо добавить логику, которую требуется переопределить.

---

## <a name="bot-logic"></a>Логика бота

Логика бота обрабатывает входящие действия из одного или нескольких каналов бота и в ответ создает исходящие действия. Это относится и к ботам, производным от класса обработчика Teams действий, который сначала проверяет наличие Teams действий. После проверки Teams все остальные действия передаются обработчику действий Bot Framework.

# <a name="c"></a>[C#](#tab/csharp)

#### <a name="core-bot-framework-handlers"></a>Обработчики Core Bot Framework

>[!NOTE]
>
>* За **исключением** действий  добавленных и удаленных членов, все обработчики действий, описанные в этом разделе, продолжают работать так же, как и с ботом, Teams другими пользователями.
>* `onInstallationUpdateActivityAsync()`Метод  используется для Teams языкового стандарта при добавлении бота в Teams.

Обработчики действий отличаются в контексте команды, где новый участник добавляется в команду вместо потока сообщений.

Список обработчиков, определенных в `ActivityHandler` следующем списке:

| Событие | Обработчик | Описание |
| :-- | :-- | :-- |
| Любой полученный тип действия | `OnTurnAsync` | Этот метод вызывает один из других обработчиков в зависимости от типа полученного действия. |
| Получено действие сообщения | `OnMessageActivityAsync` | Этот метод можно переопределить для обработки `Message` действия. |
| Получено действие обновления беседы | `OnConversationUpdateActivityAsync` | Этот метод вызывает обработчик, если участники, отличные от бота `ConversationUpdate` , присоединились к действию или покинули беседу. |
| Участники, не вносяые в бот, присоединились к беседе | `OnMembersAddedAsync` | Этот метод можно переопределить для обработки участников, присоединяющихся к беседе. |
| Участники, отличные от бота, покинули беседу | `OnMembersRemovedAsync` | Этот метод можно переопределить для обработки участников, покидаемых беседой. |
| Получено действие события | `OnEventActivityAsync` | Этот метод вызывает обработчик, относящиеся к типу события, для `Event` действия. |
| Получено действие события token-response | `OnTokenResponseEventAsync` | Этот метод можно переопределить для обработки событий ответа маркера. |
| Получено действие события без маркера и ответа | `OnEventAsync` | Этот метод можно переопределить для обработки других типов событий. |
| Получен другой тип действия | `OnUnrecognizedActivityTypeAsync` | Этот метод можно переопределить для обработки любого типа действия в противном случае необработанным. |

#### <a name="teams-specific-activity-handlers"></a>Teams обработчиков действий

Этот `TeamsActivityHandler` список расширяет список обработчиков в разделе основных обработчиков Bot Framework, включив в него следующее:

| Событие | Обработчик | Описание |
| :-- | :-- | :-- |
| channelCreated | `OnTeamsChannelCreatedAsync` | Этот метод можно переопределить для обработки Teams создаваемого канала. Дополнительные сведения см. в [статье о канале, созданном в](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created) [событиях обновления беседы](https://aka.ms/azure-bot-subscribe-to-conversation-events). |
| channelDeleted | `OnTeamsChannelDeletedAsync` | Этот метод можно переопределить для обработки удаленного Teams канала. Дополнительные сведения см. в [статье об удалении канала в](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted) [событиях обновления беседы](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| channelRenamed | `OnTeamsChannelRenamedAsync` | Этот метод можно переопределить для обработки переименовываемого Teams канала. Дополнительные сведения см. в [статье о переименовании канала](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed) в [событиях обновления беседы](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| teamRenamed | `OnTeamsTeamRenamedAsync` | `return Task.CompletedTask;`Этот метод можно переопределить для обработки переименования Teams группы. Дополнительные сведения см. в [статье о переименовании](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) команды в [событиях обновления бесед](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| MembersAdded | `OnTeamsMembersAddedAsync` | Этот метод вызывает метод `OnMembersAddedAsync` в `ActivityHandler`. Этот метод можно переопределить для обработки участников, присоединяющихся к команде. Дополнительные сведения см. [в статье о добавлении участников команды](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added) в [события обновления беседы](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| MembersRemoved | `OnTeamsMembersRemovedAsync` | Этот метод вызывает метод `OnMembersRemovedAsync` в `ActivityHandler`. Этот метод можно переопределить для обработки членов команды. Дополнительные сведения см. [в разделе "Участники команды, удаленные](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed) в [событиях обновления беседы"](https://aka.ms/azure-bot-subscribe-to-conversation-events).|

#### <a name="teams-invoke-activities"></a>Teams действий вызова

Список обработчиков Teams действий `OnInvokeActivityAsync` , вызываемый из Teams действий, включает следующее:

| Типы вызовов                    | Обработчик                              | Описание                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `OnTeamsCardActionInvokeAsync`       | Этот метод вызывается при получении действия вызова действия карточки от соединителя. |
| fileConsent/invoke              | `OnTeamsFileConsentAcceptAsync`      | Этот метод вызывается, когда пользователь принимает карточку согласия на доступ к файлу. |
| fileConsent/invoke              | `OnTeamsFileConsentAsync`            | Этот метод вызывается при получении действия карточки согласия файла от соединителя. |
| fileConsent/invoke              | `OnTeamsFileConsentDeclineAsync`     | Этот метод вызывается, когда пользователь отклоняет карточку согласия на доступ к файлу. |
| actionableMessage/executeAction | `OnTeamsO365ConnectorCardActionAsync` | Этот метод вызывается при получении действия Office 365 карточки соединителя от соединителя. |
| signin/verifyState              | `OnTeamsSigninVerifyStateAsync`      | Этот метод вызывается при получении действия проверки состояния signIn от соединителя. |
| задача/выборка                      | `OnTeamsTaskModuleFetchAsync`        | Этот метод можно переопределить в производном классе, чтобы предоставить логику при извлечении модуля задачи. |
| задача или отправка                     | `OnTeamsTaskModuleSubmitAsync`       | Этот метод можно переопределить в производном классе для предоставления логики при отправке модуля задачи. |

Действия вызова, перечисленные в этом разделе, предназначены для чат-ботов в Teams. Пакет SDK Bot Framework также поддерживает вызов действий, связанных с расширениями сообщений. Дополнительные сведения см. [в статье о расширениях сообщений](https://aka.ms/azure-bot-what-are-messaging-extensions).

# <a name="javascript"></a>[JavaScript](#tab/javascript)

#### <a name="core-bot-framework-handlers"></a>Обработчики Core Bot Framework

>[!NOTE]
> За **исключением** действий  добавленных и удаленных членов, все обработчики действий, описанные в этом разделе, продолжают работать так же, как и с ботом, Teams другими пользователями.

Обработчики действий отличаются в контексте команды, где новый участник добавляется в команду вместо потока сообщений.

Список обработчиков, определенных в `ActivityHandler` следующем списке:

| Событие | Обработчик | Описание |
| :-- | :-- | :-- |
| Любой полученный тип действия | `onTurn` | Этот метод вызывает один из других обработчиков в зависимости от типа полученного действия. |
| Получено действие сообщения | `onMessage` | Этот метод помогает обрабатывать `Message` действие. |
| Получено действие обновления беседы | `onConversationUpdate` | Этот метод вызывает обработчик, если участники, отличные от бота `ConversationUpdate` , присоединились к действию или покинули беседу. |
| Участники, не вносяые в бот, присоединились к беседе | `onMembersAdded` | Этот метод помогает обрабатывать участников, присоединяющихся к беседе. |
| Участники, отличные от бота, покинули беседу | `onMembersRemoved` | Этот метод помогает обрабатывать участников, покидая беседу. |
| Получено действие события | `onEvent` | Этот метод вызывает обработчик, относящиеся к типу события, для `Event` действия. |
| Получено действие события token-response | `onTokenResponseEvent` | Этот метод помогает обрабатывать события ответа маркера. |
| Получен другой тип действия | `onUnrecognizedActivityType` | Этот метод помогает обрабатывать любые типы действий в противном случае необработанными. |

#### <a name="teams-specific-activity-handlers"></a>Teams обработчиков действий

Этот `TeamsActivityHandler` список расширяет список обработчиков в разделе основных обработчиков Bot Framework, включив в него следующее:

| Событие | Обработчик | Описание |
| :-- | :-- | :-- |
| channelCreated | `OnTeamsChannelCreatedAsync` | Этот метод можно переопределить для обработки Teams создаваемого канала. Дополнительные сведения см. в [статье о канале, созданном в](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created) [событиях обновления беседы](https://aka.ms/azure-bot-subscribe-to-conversation-events). |
| channelDeleted | `OnTeamsChannelDeletedAsync` | Этот метод можно переопределить для обработки удаленного Teams канала. Дополнительные сведения см. в [статье об удалении канала в](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted) [событиях обновления беседы](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| channelRenamed | `OnTeamsChannelRenamedAsync` | Этот метод можно переопределить для обработки переименовываемого Teams канала. Дополнительные сведения см. в [статье о переименовании канала](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed) в [событиях обновления беседы](https://aka.ms/azure-bot-subscribe-to-conversation-events). |
| teamRenamed | `OnTeamsTeamRenamedAsync` | `return Task.CompletedTask;`Этот метод можно переопределить для обработки переименования Teams группы. Дополнительные сведения см. в [статье о переименовании](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) команды в [событиях обновления бесед](https://aka.ms/azure-bot-subscribe-to-conversation-events). |
| MembersAdded | `OnTeamsMembersAddedAsync` | Этот метод вызывает метод `OnMembersAddedAsync` в `ActivityHandler`. Этот метод можно переопределить для обработки участников, присоединяющихся к команде. Дополнительные сведения см. [в статье о добавлении участников команды](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added) в [события обновления беседы](https://aka.ms/azure-bot-subscribe-to-conversation-events). |
| MembersRemoved | `OnTeamsMembersRemovedAsync` | Этот метод вызывает метод `OnMembersRemovedAsync` в `ActivityHandler`. Этот метод можно переопределить для обработки членов команды. Дополнительные сведения см. [в разделе "Участники команды, удаленные](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed) в [событиях обновления беседы"](https://aka.ms/azure-bot-subscribe-to-conversation-events). |

#### <a name="teams-invoke-activities"></a>Teams действий вызова

Список обработчиков Teams действий `onInvokeActivity` , вызываемый из Teams действий, включает следующее:

| Типы вызовов                    | Обработчик                              | Описание                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `handleTeamsCardActionInvoke`       | Этот метод вызывается при получении действия вызова действия карточки от соединителя. |
| fileConsent/invoke              | `handleTeamsFileConsentAccept`      | Этот метод вызывается, когда пользователь принимает карточку согласия на доступ к файлу. |
| fileConsent/invoke              | `handleTeamsFileConsent`            | Этот метод вызывается при получении действия карточки согласия файла от соединителя. |
| fileConsent/invoke              | `handleTeamsFileConsentDecline`     | Этот метод вызывается, когда пользователь отклоняет карточку согласия на доступ к файлу. |
| actionableMessage/executeAction | `handleTeamsO365ConnectorCardAction` | Этот метод вызывается при получении действия Office 365 карточки соединителя от соединителя. |
| signin/verifyState              | `handleTeamsSigninVerifyState`      | Этот метод вызывается при получении действия проверки состояния signIn от соединителя. |
| задача/выборка                      | `handleTeamsTaskModuleFetch`        | Этот метод можно переопределить в производном классе, чтобы предоставить логику при извлечении модуля задачи. |
| задача или отправка                     | `handleTeamsTaskModuleSubmit`       | Этот метод можно переопределить в производном классе для предоставления логики при отправке модуля задачи. |

Действия вызова, перечисленные в этом разделе, предназначены для чат-ботов в Teams. Пакет SDK Bot Framework также поддерживает вызов действий, связанных с расширениями сообщений. Дополнительные сведения см. [в статье о расширениях сообщений](https://aka.ms/azure-bot-what-are-messaging-extensions).

# <a name="python"></a>[Python](#tab/python)

#### <a name="core-bot-framework-handlers"></a>Обработчики Core Bot Framework

>[!NOTE]
> За **исключением** действий  добавленных и удаленных членов, все обработчики действий, описанные в этом разделе, продолжают работать так же, как и с ботом, Teams другими пользователями.

Обработчики действий отличаются в контексте команды, где новый участник добавляется в команду вместо потока сообщений.

Список обработчиков, определенных в `ActivityHandler` следующем списке:

| Событие | Обработчик | Описание |
| :-- | :-- | :-- |
| Любой полученный тип действия | `on_turn` | Этот метод вызывает один из других обработчиков в зависимости от типа полученного действия. |
| Получено действие сообщения | `on_message_activity` | Этот метод можно переопределить для обработки `Message` действия. |
| Получено действие обновления беседы | `on_conversation_update_activity` | Этот метод вызывает обработчик, если участники, отличные от бота, присоединяются к беседе или покидают ее. |
| Участники, не вносяые в бот, присоединились к беседе | `on_members_added_activity` | Этот метод можно переопределить для обработки участников, присоединяющихся к беседе. |
| Участники, отличные от бота, покинули беседу | `on_members_removed_activity` | Этот метод можно переопределить для обработки участников, покидаемых беседой. |
| Получено действие события | `on_event_activity` | Этот метод вызывает обработчик, относяющийся к типу события. |
| Получено действие события token-response | `on_token_response_event` | Этот метод можно переопределить для обработки событий ответа маркера. |
| Получено действие события без маркера и ответа | `on_event` | Этот метод можно переопределить для обработки других типов событий. |
| Другие полученные типы действий | `on_unrecognized_activity_type` | Этот метод можно переопределить для обработки любого типа действия, которое не обрабатывается. |

#### <a name="teams-specific-activity-handlers"></a>Teams обработчиков действий

Этот `TeamsActivityHandler` список расширяет список обработчиков из раздела основных обработчиков Bot Framework, включив в него следующее:

| Событие | Обработчик | Описание |
| :-- | :-- | :-- |
| channelCreated | `on_teams_channel_created` | Этот метод можно переопределить для обработки Teams создаваемого канала. Дополнительные сведения см. в [статье о канале, созданном в](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created) [событиях обновления беседы](https://aka.ms/azure-bot-subscribe-to-conversation-events). |
| channelDeleted | `on_teams_channel_deleted` | Этот метод можно переопределить для обработки удаленного Teams канала. Дополнительные сведения см. в [статье об удалении канала в](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted) [событиях обновления беседы](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| channelRenamed | `on_teams_channel_renamed` | Этот метод можно переопределить для обработки переименовываемого Teams канала. Дополнительные сведения см. в [статье о переименовании канала](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed) в [событиях обновления беседы](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| teamRenamed | `on_teams_team_renamed` | `return Task.CompletedTask;`Этот метод можно переопределить для обработки переименования Teams группы. Дополнительные сведения см. в [статье о переименовании](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) команды в [событиях обновления бесед](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| MembersAdded | `on_teams_members_added` | Этот метод вызывает метод `OnMembersAddedAsync` в `ActivityHandler`. Этот метод можно переопределить для обработки участников, присоединяющихся к команде. Дополнительные сведения см. [в статье о добавлении участников команды](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added) в [события обновления беседы](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| MembersRemoved | `on_teams_members_removed` | Этот метод вызывает метод `OnMembersRemovedAsync` в `ActivityHandler`. Этот метод можно переопределить для обработки членов команды. Дополнительные сведения см. [в разделе "Участники команды, удаленные](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed) в [событиях обновления беседы"](https://aka.ms/azure-bot-subscribe-to-conversation-events).|

#### <a name="teams-invoke-activities"></a>Teams действий вызова

Список обработчиков Teams действий `on_invoke_activity` , вызываемый из Teams действий, включает следующее:

| Типы вызовов                    | Обработчик                              | Описание                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `on_teams_card_action_invoke`       | Этот метод вызывается при получении действия вызова действия карточки от соединителя. |
| fileConsent/invoke              | `on_teams_file_consent_accept`      | Этот метод вызывается, когда пользователь принимает карточку согласия на доступ к файлу. |
| fileConsent/invoke              | `on_teams_file_consent`            | Этот метод вызывается при получении действия карточки согласия файла от соединителя. |
| fileConsent/invoke              | `on_teams_file_consent_decline`     | Этот метод вызывается, когда пользователь отклоняет карточку согласия на доступ к файлу. |
| actionableMessage/executeAction | `on_teams_o365_connector_card_action` | Этот метод вызывается при получении действия Office 365 карточки соединителя от соединителя. |
| signin/verifyState              | `on_teams_signin_verify_state`      | Этот метод вызывается при получении действия проверки состояния signIn от соединителя. |
| задача/выборка                      | `on_teams_task_module_fetch`        | Этот метод можно переопределить в производном классе, чтобы предоставить логику при извлечении модуля задачи. |
| задача или отправка                     | `on_teams_task_module_submit`       | Этот метод можно переопределить в производном классе для предоставления логики при отправке модуля задачи. |

Действия вызова, перечисленные в этом разделе, предназначены для чат-ботов в Teams. Пакет SDK Bot Framework также поддерживает вызов действий, связанных с расширениями сообщений. Дополнительные сведения см. [в статье о расширениях сообщений](https://aka.ms/azure-bot-what-are-messaging-extensions).

---

---

Теперь, когда вы ознакомились с обработчиками действий бота, давайте посмотрим, как боты ведут себя по-разному в зависимости от беседы и получаемых или отправляемых сообщений.

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Основы разговора](~/bots/how-to/conversations/conversation-basics.md)
