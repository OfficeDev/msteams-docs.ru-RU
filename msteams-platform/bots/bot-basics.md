---
title: Основы бота
author: clearab
description: Основные принципы работы ботов в Teams.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 3c4e707fa4677c2441f348e8d09ecf4428ef1296
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014504"
---
# <a name="bot-basics"></a>Основы бота

В этом документе содержится введение в боты в Microsoft Teams, которое построено на статье о том, как боты [работают](https://aka.ms/how-bots-work) в основной документации [Bot Framework.](https://aka.ms/azure-bot-service-docs) Основное различие между ботами, разработанными для Microsoft Teams, и основной bot Framework заключается в функции, предоставляемые в Teams.

## <a name="teams-activity-handlers"></a>Обработчики действий Teams

Обработник действий Teams является производным от обработера действий Microsoft Bot Framework. Он маршрутит все действия Teams, прежде чем разрешит обработку любых других действий.

Когда бот для Teams получает действие, он направляется в *обработчики действий.* Все действия перенаправлются через один базовый обработатель, называемый *обработом поворота.* *Обработник поверки* вызывает требуемую обработрику действий для управления любыми полученными действиями. Бот Teams является производным от класса, производного от класса `TeamsActivityHandler` Bot `ActivityHandler` Framework.

# <a name="c"></a>[C#](#tab/csharp)

Боты создаются с помощью Bot Framework. Если боты получают сообщение о действии, то обработник поворота получает уведомление о том, что входящие действия. Затем обработитель поворота отправляет входящие действия в `OnMessageActivityAsync` обработитель действий. В Teams эта функция остается такой же. Если бот получает действие обновления беседы, обработитель поворота получает уведомление о входящих действиях и отправляет входящие действия в `OnConversationUpdateActivityAsync` . Обработник действий Teams сначала проверяет наличие определенных событий Teams. Если события не найдены, они затем перенаправят их в обработок действий Bot Framework.

В классе обработчиков действий Teams есть два основных обработчиков действий Teams и `OnConversationUpdateActivityAsync` `OnInvokeActivityAsync` . `OnConversationUpdateActivityAsync` Маршруты всех действий по обновлению бесед `OnInvokeActivityAsync` и маршруты всех действий, вызываемой Teams.

Чтобы реализовать логику для конкретных обработчиков действий Teams, необходимо переопредить методы в боте, как показано в разделе [логики](#bot-logic) бота. Базовая реализация этих обработчиков не существует, поэтому необходимо добавить логику, которая должна быть переопределяема.

# <a name="javascript"></a>[JavaScript](#tab/javascript)

Боты создаются с помощью Bot Framework. Если боты получают действие с сообщением, то обработник поворота получает уведомление о том, что входящие действия. Затем обработитель поворота отправляет входящие действия в `onMessage` обработитель действий. В Teams эта функция остается такой же. Если бот получает действие обновления беседы, обработитель поворота получает уведомление о входящих действиях и отправляет входящие действия в `dispatchConversationUpdateActivity` . Обработник действий Teams сначала проверяет наличие определенных событий Teams. Если события не найдены, они затем перенаправят их в обработок действий Bot Framework.

В классе обработчиков действий Teams есть два основных обработчиков действий Teams и `dispatchConversationUpdateActivity` `onInvokeActivity` . `dispatchConversationUpdateActivity` Маршруты всех действий по обновлению бесед `onInvokeActivity` и маршруты всех действий, вызываемой Teams.

Чтобы реализовать логику для конкретных обработчиков действий Teams, необходимо переопредить методы в боте, как показано в разделе [логики](#bot-logic) бота. Определите логику бота для этих обработчиков, а затем обязательно **`next()` вызовите их в конце.** Вызов позволяет `next()` убедиться, что выполняется следующий обработок.

# <a name="python"></a>[Python](#tab/python)

Боты создаются с помощью Bot Framework. Если боты получают действие с сообщением, то обработник поворота получает уведомление о том, что входящие действия. Затем обработитель поворота отправляет входящие действия в `on_message_activity` обработитель действий. В Teams эта функция остается такой же. Если бот получает действие обновления беседы, обработитель поворота получает уведомление о входящих действиях и отправляет входящие действия в `on_conversation_update_activity` . Обработник действий Teams сначала проверяет наличие определенных событий Teams. Если события не найдены, они затем перенаправят их в обработок действий Bot Framework.

В классе обработчиков действий Teams есть два основных обработчиков действий Teams и `on_conversation_update_activity` `on_invoke_activity` . `on_conversation_update_activity` Маршруты всех действий по обновлению бесед `on_invoke_activity` и маршруты всех действий, вызываемой Teams.

Чтобы реализовать логику для конкретных обработчиков действий Teams, необходимо переопредить методы в боте, как показано в разделе [логики](#bot-logic) бота. Базовая реализация этих обработчиков не существует, поэтому необходимо добавить логику, которая должна быть переопределяема.

---

## <a name="bot-logic"></a>Логика бота

Логика бота обрабатывает входящие действия из одного или более каналов ботов и в ответ создает исходящую активность. Это по-прежнему относится к ботам, производным от класса обработвода действий Teams, который сначала проверяет действия Teams. После проверки действий Teams он передает все остальные действия в обработник действий Bot Framework.

# <a name="c"></a>[C#](#tab/csharp)

#### <a name="core-bot-framework-handlers"></a>Обработчики Core Bot Framework

>[!NOTE]
> За *исключением*  действий добавленных и удаленных участников, все обработчики действий, описанные в этом разделе, продолжают работать так же, как и боты, не в том числе Teams.

Обработчики действий отличаются в контексте команды, в которой новый участник добавляется в команду вместо потока сообщений.

В список обработчиков, определенных в списке, `ActivityHandler` входят следующие:

| Event | Обработник | Описание |
| :-- | :-- | :-- |
| Любой полученный тип действия | `OnTurnAsync` | Этот метод вызывает один из других обработчиков в зависимости от типа полученного действия. |
| Полученная активность сообщения | `OnMessageActivityAsync` | Этот метод может быть переопределен для обработки `Message` действия. |
| Получена информация об обновлении беседы | `OnConversationUpdateActivityAsync` | Этот метод вызывает обработок, если участники, кроме бота, присоединились к беседе или покидали ее в `ConversationUpdate` действии. |
| К беседе присоединились не боты | `OnMembersAddedAsync` | Этот метод может быть переопределен для обработки участников, присоединявшихся к беседе. |
| Участники, не относякие к ботам, покинули беседу | `OnMembersRemovedAsync` | Этот метод может быть переопределен для обработки участников беседы. |
| Полученная активность события | `OnEventActivityAsync` | Этот метод вызывает обработок, специфический для типа события, для `Event` действия. |
| Полученные действия событий с маркерами | `OnTokenResponseEventAsync` | Этот метод может быть переопределен для обработки событий отклика маркера. |
| Получена активность событий, не относяхся к маркерам | `OnEventAsync` | Этот метод может быть переопределен для обработки других типов событий. |
| Получен другой тип действия | `OnUnrecognizedActivityTypeAsync` | Этот метод может быть переопределен для обработки любого типа действий в противном случае без обработки. |

#### <a name="teams-specific-activity-handlers"></a>Обработчики определенных действий Teams

Список обработчиков в разделе "Обработчики Core Bot Framework" расширяется, включив в него `TeamsActivityHandler` следующие:

| Event | Обработник | Описание |
| :-- | :-- | :-- |
| channelCreated | `OnTeamsChannelCreatedAsync` | Этот метод может быть переопределен для обработки создаемого канала Teams. Дополнительные сведения см. в [канале, созданном](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created) в [событиях обновления беседы.](https://aka.ms/azure-bot-subscribe-to-conversation-events) |
| channelDeleted | `OnTeamsChannelDeletedAsync` | Этот метод может быть переопределен для обработки удаления канала Teams. Дополнительные сведения см. в [канале, удаленном](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted) в [событиях обновления беседы.](https://aka.ms/azure-bot-subscribe-to-conversation-events)|
| channelRenamed | `OnTeamsChannelRenamedAsync` | Этот метод может быть переопределен для обработки переименования канала Teams. Дополнительные сведения см. в [канале, переименованном](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed) в [событиях обновления беседы.](https://aka.ms/azure-bot-subscribe-to-conversation-events)|
| teamRenamed | `OnTeamsTeamRenamedAsync` | `return Task.CompletedTask;` Этот метод может быть переопределен для обработки переименования команды Teams. Дополнительные сведения см. в [переименовывной команде](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) в [событиях обновления беседы.](https://aka.ms/azure-bot-subscribe-to-conversation-events)|
| MembersAdded | `OnTeamsMembersAddedAsync` | Этот метод вызывает `OnMembersAddedAsync` метод в `ActivityHandler` . Метод может быть переопределен для обработки участников, присоединявшихся к команде. Дополнительные сведения см. [в сведениях, добавленных участниками команды](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added) в [событиях обновления беседы.](https://aka.ms/azure-bot-subscribe-to-conversation-events)|
| MembersRemoved | `OnTeamsMembersRemovedAsync` | Этот метод вызывает `OnMembersRemovedAsync` метод в `ActivityHandler` . Этот метод может быть переопределен для обработки членов команды. Дополнительные сведения см. в [сведениях, которые участники команды удалили](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed) в [событиях обновления беседы.](https://aka.ms/azure-bot-subscribe-to-conversation-events)|

#### <a name="teams-invoke-activities"></a>Вызов действий в Teams

Список обработчиков действий Teams, которые вызваны обработчиком действий `OnInvokeActivityAsync` Teams, включает следующие:

| Типы вызовов                    | Обработник                              | Описание                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `OnTeamsCardActionInvokeAsync`       | Этот метод вызывается, когда действие вызова действия карточки получается от соединители. |
| fileConsent/invoke              | `OnTeamsFileConsentAcceptAsync`      | Этот метод вызывается, когда пользователь принимает карточку согласия на файл. |
| fileConsent/invoke              | `OnTeamsFileConsentAsync`            | Этот метод вызывается, когда действие карточки согласия с файлом получено от соединители. |
| fileConsent/invoke              | `OnTeamsFileConsentDeclineAsync`     | Этот метод вызывается при отклонении пользователем карточки согласия на файл. |
| actionableMessage/executeAction | `OnTeamsO365ConnectorCardActionAsync` | Этот метод вызывается при получении действия карточки соединитела O365 от соединитела. |
| signin/verifyState              | `OnTeamsSigninVerifyStateAsync`      | Этот метод вызывается при проверке получения действия состояния signIn от соединители. |
| task/fetch                      | `OnTeamsTaskModuleFetchAsync`        | Этот метод может быть переопределен в производном классе для предоставления логики при извлечении модуля задачи. |
| task/submit                     | `OnTeamsTaskModuleSubmitAsync`       | Этот метод может быть переопределен в производном классе для предоставления логики при отправке модуля задачи. |

Действия по вызову, перечисленные в этом разделе, посвящены ботам для бесед в Teams. SDK Bot Framework также поддерживает вызов действий, характерных для расширений обмена сообщениями. Дополнительные сведения см. в дополнительных сведениях [о расширениях обмена сообщениями.](https://aka.ms/azure-bot-what-are-messaging-extensions)

# <a name="javascript"></a>[JavaScript](#tab/javascript)

#### <a name="core-bot-framework-handlers"></a>Обработчики Core Bot Framework

>[!NOTE]
> За *исключением*  действий добавленных и удаленных участников, все обработчики действий, описанные в этом разделе, продолжают работать так же, как и боты, не в том числе Teams.

Обработчики действий отличаются в контексте команды, в которой новый участник добавляется в команду вместо потока сообщений.

В список обработчиков, определенных в списке, `ActivityHandler` входят следующие:

| Event | Обработник | Описание |
| :-- | :-- | :-- |
| Любой полученный тип действия | `onTurn` | Этот метод вызывает один из других обработчиков в зависимости от типа полученного действия. |
| Полученная активность сообщения | `onMessage` | Этот метод помогает обрабатывать `Message` действия. |
| Получена информация об обновлении беседы | `onConversationUpdate` | Этот метод вызывает обработок, если участники, кроме бота, присоединились к беседе или покидали ее в `ConversationUpdate` действии. |
| К беседе присоединились не боты | `onMembersAdded` | Этот метод помогает обрабатывать участников, присоединявшихся к беседе. |
| Участники, не относякие к ботам, покинули беседу | `onMembersRemoved` | Этот метод помогает обрабатывать участников, покидая беседу. |
| Полученная активность события | `onEvent` | Этот метод вызывает обработок, специфический для типа события, для `Event` действия. |
| Полученное действие события токена | `onTokenResponseEvent` | Этот метод помогает обрабатывать события отклика маркера. |
| Получен другой тип действия | `onUnrecognizedActivityType` | Этот метод помогает обрабатывать любые типы действий в противном случае без обработки. |

#### <a name="teams-specific-activity-handlers"></a>Обработчики определенных действий Teams

Список обработчиков в разделе "Обработчики Core Bot Framework" расширяется, включив в него `TeamsActivityHandler` следующие:

| Event | Обработник | Описание |
| :-- | :-- | :-- |
| channelCreated | `OnTeamsChannelCreatedAsync` | Этот метод может быть переопределен для обработки создаемого канала Teams. Дополнительные сведения см. в [канале, созданном](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created) в [событиях обновления беседы.](https://aka.ms/azure-bot-subscribe-to-conversation-events) |
| channelDeleted | `OnTeamsChannelDeletedAsync` | Этот метод может быть переопределен для обработки удаления канала Teams. Дополнительные сведения см. в [канале, удаленном](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted) в [событиях обновления беседы.](https://aka.ms/azure-bot-subscribe-to-conversation-events)|
| channelRenamed | `OnTeamsChannelRenamedAsync` | Этот метод может быть переопределен для обработки переименования канала Teams. Дополнительные сведения см. в [канале, переименованном](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed) в [событиях обновления беседы.](https://aka.ms/azure-bot-subscribe-to-conversation-events) |
| teamRenamed | `OnTeamsTeamRenamedAsync` | `return Task.CompletedTask;` Этот метод может быть переопределен для обработки переименования команды Teams. Дополнительные сведения см. в [переименовывной команде](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) в [событиях обновления беседы.](https://aka.ms/azure-bot-subscribe-to-conversation-events) |
| MembersAdded | `OnTeamsMembersAddedAsync` | Этот метод вызывает `OnMembersAddedAsync` метод в `ActivityHandler` . Метод может быть переопределен для обработки участников, присоединявшихся к команде. Дополнительные сведения см. [в сведениях, добавленных участниками команды](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added) в [событиях обновления беседы.](https://aka.ms/azure-bot-subscribe-to-conversation-events) |
| MembersRemoved | `OnTeamsMembersRemovedAsync` | Этот метод вызывает `OnMembersRemovedAsync` метод в `ActivityHandler` . Этот метод может быть переопределен для обработки членов команды. Дополнительные сведения см. в [сведениях, которые участники команды удалили](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed) в [событиях обновления беседы.](https://aka.ms/azure-bot-subscribe-to-conversation-events) |

#### <a name="teams-invoke-activities"></a>Вызов действий в Teams

Список обработчиков действий Teams, которые вызваны обработчиком действий `onInvokeActivity` Teams, включает следующие:

| Типы вызовов                    | Обработник                              | Описание                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `handleTeamsCardActionInvoke`       | Этот метод вызывается, когда действие вызова действия карточки получается от соединители. |
| fileConsent/invoke              | `handleTeamsFileConsentAccept`      | Этот метод вызывается, когда пользователь принимает карточку согласия на файл. |
| fileConsent/invoke              | `handleTeamsFileConsent`            | Этот метод вызывается, когда действие карточки согласия с файлом получено от соединители. |
| fileConsent/invoke              | `handleTeamsFileConsentDecline`     | Этот метод вызывается при отклонении пользователем карточки согласия на файл. |
| actionableMessage/executeAction | `handleTeamsO365ConnectorCardAction` | Этот метод вызывается при получении действия карточки соединитела O365 от соединитела. |
| signin/verifyState              | `handleTeamsSigninVerifyState`      | Этот метод вызывается при проверке получения действия состояния signIn от соединители. |
| task/fetch                      | `handleTeamsTaskModuleFetch`        | Этот метод может быть переопределен в производном классе для предоставления логики при извлечении модуля задачи. |
| task/submit                     | `handleTeamsTaskModuleSubmit`       | Этот метод может быть переопределен в производном классе для предоставления логики при отправке модуля задачи. |

Действия по вызову, перечисленные в этом разделе, посвящены ботам бесед в Teams. SDK Bot Framework также поддерживает вызов действий, характерных для расширений обмена сообщениями. Дополнительные сведения см. в дополнительных сведениях [о расширениях обмена сообщениями.](https://aka.ms/azure-bot-what-are-messaging-extensions)

# <a name="python"></a>[Python](#tab/python)

#### <a name="core-bot-framework-handlers"></a>Обработчики Core Bot Framework

>[!NOTE]
> За *исключением*  действий добавленных и удаленных участников, все обработчики действий, описанные в этом разделе, продолжают работать так же, как и боты, не в том числе Teams.

Обработчики действий отличаются в контексте команды, в которой новый участник добавляется в команду вместо потока сообщений.

В список обработчиков, определенных в списке, `ActivityHandler` входят следующие:

| Event | Обработник | Описание |
| :-- | :-- | :-- |
| Любой полученный тип действия | `on_turn` | Этот метод вызывает один из других обработчиков в зависимости от типа полученного действия. |
| Полученная активность сообщения | `on_message_activity` | Этот метод может быть переопределен для обработки `Message` действия. |
| Получена информация об обновлении беседы | `on_conversation_update_activity` | Этот метод вызывает обработок, если участники, кроме бота, присоединяются к беседе или покидают ее. |
| К беседе присоединились не боты | `on_members_added_activity` | Этот метод может быть переопределен для обработки участников, присоединявшихся к беседе. |
| Участники, не относякие к ботам, покинули беседу | `on_members_removed_activity` | Этот метод может быть переопределен для обработки участников беседы. |
| Полученная активность события | `on_event_activity` | Этот метод вызывает обработок, специфический для типа события. |
| Полученные действия событий с маркерами | `on_token_response_event` | Этот метод может быть переопределен для обработки событий отклика маркера. |
| Получена активность события, не относяка к маркеру | `on_event` | Этот метод может быть переопределен для обработки других типов событий. |
| Другие типы полученных действий | `on_unrecognized_activity_type` | Этот метод может быть переопределен для обработки любых типов действий, которые не обрабатываются. |

#### <a name="teams-specific-activity-handlers"></a>Обработчики определенных действий Teams

Список обработчиков из раздела Core Bot Framework расширяется, включив в него `TeamsActivityHandler` следующие:

| Event | Обработник | Описание |
| :-- | :-- | :-- |
| channelCreated | `on_teams_channel_created` | Этот метод может быть переопределен для обработки создания канала Teams. Дополнительные сведения см. в [канале, созданном](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created) в [событиях обновления беседы.](https://aka.ms/azure-bot-subscribe-to-conversation-events) |
| channelDeleted | `on_teams_channel_deleted` | Этот метод может быть переопределен для обработки удаления канала Teams. Дополнительные сведения см. в [канале, удаленном](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted) в [событиях обновления беседы.](https://aka.ms/azure-bot-subscribe-to-conversation-events)|
| channelRenamed | `on_teams_channel_renamed` | Этот метод может быть переопределен для обработки переименования канала Teams. Дополнительные сведения см. в [канале, переименованном](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed) в [событиях обновления беседы.](https://aka.ms/azure-bot-subscribe-to-conversation-events)|
| teamRenamed | `on_teams_team_renamed` | `return Task.CompletedTask;` Этот метод может быть переопределен для обработки переименования команды Teams. Дополнительные сведения см. в [переименовывной команде](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) в [событиях обновления беседы.](https://aka.ms/azure-bot-subscribe-to-conversation-events)|
| MembersAdded | `on_teams_members_added` | Этот метод вызывает `OnMembersAddedAsync` метод в `ActivityHandler` . Метод может быть переопределен для обработки участников, присоединявшихся к команде. Дополнительные сведения см. [в сведениях, добавленных участниками команды](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added) в [событиях обновления беседы.](https://aka.ms/azure-bot-subscribe-to-conversation-events)|
| MembersRemoved | `on_teams_members_removed` | Этот метод вызывает `OnMembersRemovedAsync` метод в `ActivityHandler` . Этот метод может быть переопределен для обработки членов команды. Дополнительные сведения см. в [сведениях, которые участники команды удалили](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed) в [событиях обновления беседы.](https://aka.ms/azure-bot-subscribe-to-conversation-events)|

#### <a name="teams-invoke-activities"></a>Вызов действий в Teams

Список обработчиков действий Teams, которые вызваны обработчиком действий `on_invoke_activity` Teams, включает следующие:

| Типы вызовов                    | Обработник                              | Описание                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `on_teams_card_action_invoke`       | Этот метод вызывается, когда действие вызова действия карточки получается от соединители. |
| fileConsent/invoke              | `on_teams_file_consent_accept`      | Этот метод вызывается, когда пользователь принимает карточку согласия на файл. |
| fileConsent/invoke              | `on_teams_file_consent`            | Этот метод вызывается, когда действие карточки согласия с файлом получено от соединители. |
| fileConsent/invoke              | `on_teams_file_consent_decline`     | Этот метод вызывается при отклонении пользователем карточки согласия на файл. |
| actionableMessage/executeAction | `on_teams_o365_connector_card_action` | Этот метод вызывается при получении действия карточки соединитела O365 от соединитела. |
| signin/verifyState              | `on_teams_signin_verify_state`      | Этот метод вызывается при проверке получения действия состояния signIn от соединители. |
| task/fetch                      | `on_teams_task_module_fetch`        | Этот метод может быть переопределен в производном классе для предоставления логики при извлечении модуля задачи. |
| task/submit                     | `on_teams_task_module_submit`       | Этот метод может быть переопределен в производном классе для предоставления логики при отправке модуля задачи. |

Действия по вызову, перечисленные в этом разделе, посвящены ботам бесед в Teams. SDK Bot Framework также поддерживает вызов действий, характерных для расширений обмена сообщениями. Дополнительные сведения см. в дополнительных сведениях [о расширениях обмена сообщениями.](https://aka.ms/azure-bot-what-are-messaging-extensions)

---
