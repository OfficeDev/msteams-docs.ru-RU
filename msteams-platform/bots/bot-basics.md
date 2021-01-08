---
title: Основы бота
author: clearab
description: Основные принципы работы ботов в Teams.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 43dd351b30fdba3435d39aca43aae0f2de00ed24
ms.sourcegitcommit: d0e71ea63af2f67eba75ba283ec46cc7cdf87d75
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/24/2020
ms.locfileid: "49731960"
---
# <a name="bot-basics"></a>Основы бота

Это введение, которое построено на статье о том, как [боты работают](https://aka.ms/how-bots-work) в основной документации [Bot Framework.](https://aka.ms/azure-bot-service-docs) Эта статья и другие статьи в разделе  "Понятия" могут оказаться полезными.

Основное различие в ботах, разработанных для Microsoft Teams, заключается в том, как обрабатываются действия. Обработок действий Microsoft Teams является на основе обработки действий Bot Framework, чтобы перенаправить все действия Teams, прежде чем разрешать обработку любых действий, не относяющихся к Teams.

## <a name="teams-activity-handlers"></a>Обработчики действий Teams

Когда бот для Microsoft Teams получает действие, он передает его обработчику *действий.* Под обложками имеется один базовый обработатель под названием обработок поворота, через который перенаправлются все действия. *Обработок поворота* вызывает требуемого обработка действий для обработки любого типа полученного действия. Бот, разработанный для Microsoft Teams, отличается тем, что он является производным от класса, производного от `TeamsActivityHandler` класса Bot `ActivityHandler` Framework.

# <a name="c"></a>[C#](#tab/csharp)

Как и любой бот, созданный с помощью Microsoft Bot Framework, если бот получает действие сообщения, обработитель поворота видит это входящие действия и отправляет его обработелю `OnMessageActivityAsync` действия. В Teams эта функция остается такой же. Если бот получает действие обновления беседы, обработитель поворота видит это входящие действия и отправляет его в `OnConversationUpdateActivityAsync` . Обработник действий *Teams,* который сначала проверяет все конкретные события Teams и передает его в обработок действий Bot Framework, если его не найти.

В классе обработчиков действий Teams есть два основных обработчиков действий Teams, которые маршрутизют все действия по обновлению бесед и маршрутизизют все действия, `OnConversationUpdateActivityAsync` `OnInvokeActivityAsync` вызываемые Teams.

Чтобы реализовать логику для конкретных обработчиков действий Teams, вы переопределите эти методы в боте, как показано в разделе логики [бота](#bot-logic) ниже. Для каждого из этих обработчиков не существует базовой реализации, поэтому просто добавьте логику, которая будет вам нужна в переопределе.

# <a name="javascript"></a>[JavaScript](#tab/javascript)

Как и любой бот, созданный с помощью Microsoft Bot Framework, если бот получает действие сообщения, обработитель поворота видит это входящие действия и отправляет его обработелю `onMessage` действия. В Teams эта функция остается такой же. Если бот получает действие обновления беседы, обработитель поворота видит это входящие действия и отправляет его в `dispatchConversationUpdateActivity` . Обработник действий *Teams,* который сначала проверяет все конкретные события Teams и передает его обработители действий на основе ботов, если они не найдены.

В классе обработчиков действий Teams есть два основных обработчиков действий Teams, которые маршрутизют все действия по обновлению бесед и маршрутизют все действия, `dispatchConversationUpdateActivity` `onInvokeActivity` вызываемые Teams.

Чтобы реализовать логику для конкретных обработчиков действий Teams, вы переопределите [](#bot-logic) эти методы в боте, как по видно из раздела логики бота. Для каждого из этих обработчиков определите логику бота, а затем обязательно **вызовите `next()` его в конце.** Вызов позволяет `next()` убедиться, что выполняется следующий обработок.

# <a name="python"></a>[Python](#tab/python)

Боты создаются с помощью Microsoft Bot Framework, если они получают сообщение, то обработник поворота получает уведомление о том, что входящие действия. Затем обработитель поворота отправляет входящие действия в `on_message_activity` обработитель действий. В Teams эта функция остается такой же. Если бот получает действие обновления беседы, обработитель поворота получает уведомление о входящих действиях и отправляет входящие действия в `on_conversation_update_activity` . Обработник действий Teams сначала проверяет все конкретные события Teams. Если события не найдены, они будут переданы в обработок действий Bot Framework.

В классе обработчиков действий Teams есть два основных обработчиков действий Teams и `on_conversation_update_activity` `on_invoke_activity` . `on_conversation_update_activity` Маршруты всех действий по обновлению бесед `on_invoke_activity` и маршруты всех действий, вызываемой Teams.

Чтобы реализовать логику для конкретных обработчиков действий Teams, необходимо переопредить эти методы в боте, как показано в разделе [логики](#bot-logic) бота. Базовая реализация этих обработчиков не существует, поэтому необходимо добавить логику, необходимую для переопределения.

---

## <a name="bot-logic"></a>Логика бота

Логика бота обрабатывает входящие действия из одного или более каналов ботов и создает исходящую активность в ответ.  Это по-прежнему относится к ботам, производным от класса обработвода действий Teams, который сначала проверяет действия Teams, а затем передает все остальные действия обработиму действий в рамках ботов.

# <a name="c"></a>[C#](#tab/csharp)

#### <a name="core-bot-framework-handlers"></a>Обработчики Core Bot Framework

Все описанные ниже обработчики действий продолжат работать так же, как и с  ботом,  не относястого к Teams, за исключением обработки добавленных членов и удалений участников, они будут разными в контексте команды, где новый участник добавляется в команду, а не поток сообщений.

Обработчики, определенные в `ActivityHandler` них, описаны ниже.

| Событие | Обработник | Описание |
| :-- | :-- | :-- |
| Любой полученный тип действия | `OnTurnAsync` | Вызывает один из других обработчиков в зависимости от типа полученного действия. |
| Полученная активность сообщения | `OnMessageActivityAsync` | Переопределять это для обработки `Message` действия. |
| Получена информация об обновлении беседы | `OnConversationUpdateActivityAsync` | В действии вызывается обработок, если участники, кроме бота, присоединились к беседе `ConversationUpdate` или покидали ее. |
| К беседе присоединились не боты | `OnMembersAddedAsync` | Переопределять это, чтобы обработать участников, присоединявшихся к беседе. |
| Участники, не относякие к ботам, покинули беседу | `OnMembersRemovedAsync` | Переопределять это, чтобы обрабатывать участников, покидая беседу. |
| Полученная активность события | `OnEventActivityAsync` | В `Event` действии вызывается обработок, специфический для типа события. |
| Полученное действие события токена | `OnTokenResponseEventAsync` | Переопределять это для обработки событий отклика маркера. |
| Получена активность события, не относяка к маркеру | `OnEventAsync` | Переопределять это для обработки событий других типов. |
| Получен другой тип действия | `OnUnrecognizedActivityTypeAsync` | Переопределять это действие для обработки любых типов действий в противном случае без обработки. |

#### <a name="teams-specific-handlers"></a>Обработчики для Teams

Список обработчиков выше расширяется, включив в него `TeamsActivityHandler` следующие:

| Событие | Обработник | Описание |
| :-- | :-- | :-- |
| channelCreated | `OnTeamsChannelCreatedAsync` | Переопределять это для обработки создания канала Teams. Дополнительные сведения см. в [канале, созданном](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created) в [событиях обновления беседы.](https://aka.ms/azure-bot-subscribe-to-conversation-events) |
| channelDeleted | `OnTeamsChannelDeletedAsync` | Переопределять это для обработки удаления канала Teams. Дополнительные сведения см. в [канале, удаленном](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted) в [событиях обновления беседы.](https://aka.ms/azure-bot-subscribe-to-conversation-events)|
| channelRenamed | `OnTeamsChannelRenamedAsync` | Переопределять это для обработки переименования канала Teams. Дополнительные сведения см. в [канале, переименованном](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed) в [событиях обновления беседы.](https://aka.ms/azure-bot-subscribe-to-conversation-events)|
| teamRenamed | `OnTeamsTeamRenamedAsync` | `return Task.CompletedTask;` Переопределять это для обработки переименования команды Teams. Дополнительные сведения см. в [переименованной команде](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) в [событиях обновления беседы.](https://aka.ms/azure-bot-subscribe-to-conversation-events)|
| MembersAdded | `OnTeamsMembersAddedAsync` | Вызывает метод `OnMembersAddedAsync` в `ActivityHandler` . Переопределять это, чтобы обрабатывать участников, присоединявшихся к команде. Дополнительные сведения [см. в сведениях, добавленных участниками команды](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added) в [событиях обновления беседы.](https://aka.ms/azure-bot-subscribe-to-conversation-events)|
| MembersRemoved | `OnTeamsMembersRemovedAsync` | Вызывает метод `OnMembersRemovedAsync` в `ActivityHandler` . Переопределять это, чтобы обрабатывать участников, покидая команду. Дополнительные сведения [см. в сведениях, которые участники команды удалили](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed) в [событиях обновления беседы.](https://aka.ms/azure-bot-subscribe-to-conversation-events)|

#### <a name="teams-invoke-activities"></a>Вызов действий в Teams

Вот список всех обработчиков действий Teams, которые вызваны из обработчиков `OnInvokeActivityAsync` действий _Teams:_

| Типы вызовов                    | Обработник                              | Описание                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `OnTeamsCardActionInvokeAsync`       | Вызов действия карточки Teams. |
| fileConsent/invoke              | `OnTeamsFileConsentAcceptAsync`      | Teams File Consent Accept. |
| fileConsent/invoke              | `OnTeamsFileConsentAsync`            | Согласие на файл Teams. |
| fileConsent/invoke              | `OnTeamsFileConsentDeclineAsync`     | Согласие на файл Teams. |
| actionableMessage/executeAction | `OnTeamsO365ConnectorCardActionAsync` | Действие карточки соединитела Teams O365. |
| signin/verifyState              | `OnTeamsSigninVerifyStateAsync`      | Teams Sign in Verify State. |
| task/fetch                      | `OnTeamsTaskModuleFetchAsync`        | Извлечение модуля задач Teams. |
| task/submit                     | `OnTeamsTaskModuleSubmitAsync`       | Отправка модуля задач Teams. |

Действия по вызову, перечисленные выше, для ботов бесед в Teams. SDK Bot Framework также поддерживает вызовы, специфичная для расширений обмена сообщениями. Дополнительные сведения см. [в дополнительных сведениях о расширениях обмена сообщениями](https://aka.ms/azure-bot-what-are-messaging-extensions)

# <a name="javascript"></a>[JavaScript](#tab/javascript)

Все описанные ниже обработчики действий продолжат работать так же, как и боты,  не  в том числе Teams, за исключением обработки действий, добавленных и удалимых участников, в контексте команды, в которой новый участник добавляется в команду, а не в потоке сообщений.

#### <a name="core-bot-framework-handlers"></a>Обработчики Core Bot Framework

Обработчики, определенные в `ActivityHandler` них, описаны ниже.

| Событие | Обработник | Описание |
| :-- | :-- | :-- |
| Любой полученный тип действия | `onTurn` | Вызывает один из других обработчиков в зависимости от типа полученного действия. |
| Полученная активность сообщения | `onMessage` | Предоставление функции для обработки `Message` действия. |
| Получена информация об обновлении беседы | `onConversationUpdate` | В действии вызывается обработок, если участники, кроме бота, присоединились к беседе `ConversationUpdate` или покидали ее. |
| К беседе присоединились не боты | `onMembersAdded` | Предоставление функции для этого для обработки участников, присоединявшихся к беседе. |
| Участники, не относякие к ботам, покинули беседу | `onMembersRemoved` | Предоставление функции для этого для обработки участников, покидая беседу. |
| Полученная активность события | `onEvent` | В `Event` действии вызывается обработок, специфический для типа события. |
| Полученное действие события токена | `onTokenResponseEvent` | Предоставление функции для обработки событий отклика маркера. |
| Получен другой тип действия | `onUnrecognizedActivityType` | Предодать функцию для обработки любого типа действия в противном случае без обработки. |
| Обработчики действий завершены | `onDialog` | Предо включите функцию для обработки любой обработки, которая должна быть выполнена в конце поворота после завершения остальных обработчиков действий. |

#### <a name="teams-specific-handlers"></a>Обработчики для Teams

Список обработчиков в разделе "Обработчики Core Bot Framework" расширяется, включив в него `TeamsActivityHandler` следующие:

| Событие | Обработник | Описание |
| :-- | :-- | :-- |
| channelCreated | `OnTeamsChannelCreatedAsync` | Переопределять это для обработки создания канала Teams. Дополнительные сведения см. в [канале, созданном](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created) в [событиях обновления беседы.](https://aka.ms/azure-bot-subscribe-to-conversation-events) |
| channelDeleted | `OnTeamsChannelDeletedAsync` | Переопределять это для обработки удаления канала Teams. Дополнительные сведения см. в [канале, удаленном](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted) в [событиях обновления беседы.](https://aka.ms/azure-bot-subscribe-to-conversation-events)|
| channelRenamed | `OnTeamsChannelRenamedAsync` | Переопределять это для обработки переименования канала Teams. Дополнительные сведения см. в [канале, переименованном](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed) в [событиях обновления беседы.](https://aka.ms/azure-bot-subscribe-to-conversation-events) |
| teamRenamed | `OnTeamsTeamRenamedAsync` | `return Task.CompletedTask;` Переопределять это для обработки переименования команды Teams. Дополнительные сведения см. в [переименованной команде](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) в [событиях обновления беседы.](https://aka.ms/azure-bot-subscribe-to-conversation-events) |
| MembersAdded | `OnTeamsMembersAddedAsync` | Вызывает метод `OnMembersAddedAsync` в `ActivityHandler` . Переопределять это, чтобы обрабатывать участников, присоединявшихся к команде. Дополнительные сведения [см. в сведениях, добавленных участниками команды](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added) в [событиях обновления беседы.](https://aka.ms/azure-bot-subscribe-to-conversation-events) |
| MembersRemoved | `OnTeamsMembersRemovedAsync` | Вызывает метод `OnMembersRemovedAsync` в `ActivityHandler` . Переопределять это, чтобы обрабатывать участников, покидая команду. Дополнительные сведения [см. в сведениях, которые участники команды удалили](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed) в [событиях обновления беседы.](https://aka.ms/azure-bot-subscribe-to-conversation-events) |

#### <a name="teams-invoke-activities"></a>Вызов действий в Teams

Вот список всех обработчиков действий Teams, которые вызваны из обработчиков `onInvokeActivity` действий Teams:

| Типы вызовов                    | Обработник                              | Описание                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `handleTeamsCardActionInvoke`       | Вызов действия карточки Teams. |
| fileConsent/invoke              | `handleTeamsFileConsentAccept`      | Согласие на файл Teams принимается. |
| fileConsent/invoke              | `handleTeamsFileConsent`            | Согласие на файл Teams. |
| fileConsent/invoke              | `handleTeamsFileConsentDecline`     | Согласие на файл Teams. |
| actionableMessage/executeAction | `handleTeamsO365ConnectorCardAction` | Действие карточки соединители Teams O365. |
| signin/verifyState              | `handleTeamsSigninVerifyState`      | Teams sign in verify state. |
| task/fetch                      | `handleTeamsTaskModuleFetch`        | Извлечение модуля задач Teams. |
| task/submit                     | `handleTeamsTaskModuleSubmit`       | Отправка модуля задач Teams. |

Действия по вызову, перечисленные в разделе "Действия по вызову Teams", посвящены ботам в беседах в Teams. SDK Bot Framework также поддерживает вызов действий, характерных для расширений обмена сообщениями. Дополнительные сведения см. в дополнительных сведениях [о расширениях обмена сообщениями.](https://aka.ms/azure-bot-what-are-messaging-extensions)

# <a name="python"></a>[Python](#tab/python)

#### <a name="core-bot-framework-handlers"></a>Обработчики Core Bot Framework

>[!NOTE]
> За исключением действий добавленных и удаленных участников, все обработчики действий, описанные в этом разделе, продолжают работать так же, как и боты, не в том числе Teams.

Обработчики действий отличаются в контексте команды, в которой новый участник добавляется в команду вместо потока сообщений.

В список обработчиков, определенных в списке, `ActivityHandler` входят следующие:

| Событие | Обработник | Описание |
| :-- | :-- | :-- |
| Любой полученный тип действия | `on_turn` | Вызывает один из других обработчиков в зависимости от типа полученного действия. |
| Полученная активность сообщения | `on_message_activity` | Переопределяет этот процесс для `Message` обработки действия. |
| Получена информация об обновлении беседы | `on_conversation_update_activity` | Вызывает обработ который, если участники, кроме бота, присоединяются к беседе или покидают ее. |
| К беседе присоединились не боты | `on_members_added_activity` | Переопределяется для обработки присоединения участников к беседе. |
| Участники, не относякие к ботам, покинули беседу | `on_members_removed_activity` | Переопределяется для обработки участников, покидая беседу. |
| Полученная активность события | `on_event_activity` | Вызывает обработок, относякся к типу события. |
| Полученное действие события токена | `on_token_response_event` | Переопределяет эту возможность для обработки событий отклика маркера. |
| Получена активность события, не относяка к маркеру | `on_event` | Переопределяет эту возможность для обработки событий других типов. |
| Другие типы полученных действий | `on_unrecognized_activity_type` | Переопределяется для обработки любых типов не обрабатываемого действия. |

#### <a name="teams-specific-handlers"></a>Обработчики для Teams

Список обработчиков из раздела Core Bot Framework расширяется, включив в него `TeamsActivityHandler` следующие:

| Событие | Обработник | Описание |
| :-- | :-- | :-- |
| channelCreated | `on_teams_channel_created` | Переопределяется для обработки создания канала Teams. Дополнительные сведения см. в [канале, созданном](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created) в [событиях обновления беседы.](https://aka.ms/azure-bot-subscribe-to-conversation-events) |
| channelDeleted | `on_teams_channel_deleted` | Переопределяется для обработки удаления канала Teams. Дополнительные сведения см. в [канале, удаленном](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted) в [событиях обновления беседы.](https://aka.ms/azure-bot-subscribe-to-conversation-events)|
| channelRenamed | `on_teams_channel_renamed` | Переопределяется для обработки переименования канала Teams. Дополнительные сведения см. в [переименовыв канале](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed) в [событиях обновления беседы.](https://aka.ms/azure-bot-subscribe-to-conversation-events)|
| teamRenamed | `on_teams_team_renamed` | `return Task.CompletedTask;` Переопределяется для обработки переименования команды Teams. Дополнительные сведения см. в [переименованной команде](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) в [событиях обновления беседы.](https://aka.ms/azure-bot-subscribe-to-conversation-events)|
| MembersAdded | `on_teams_members_added` | Вызывает метод `OnMembersAddedAsync` в `ActivityHandler` . Переопределяется для обработки присоединения участников к команде. Дополнительные сведения см. [в сведениях, добавленных участниками команды](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added) в [событиях обновления беседы.](https://aka.ms/azure-bot-subscribe-to-conversation-events)|
| MembersRemoved | `on_teams_members_removed` | Вызывает метод `OnMembersRemovedAsync` в `ActivityHandler` . Переопределяется для обработки выходных участников команды. Дополнительные сведения см. в [сведениях, которые участники команды удалили](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed) в [событиях обновления беседы.](https://aka.ms/azure-bot-subscribe-to-conversation-events)|

#### <a name="teams-invoke-activities"></a>Вызов действий в Teams

Список обработчиков действий Teams, которые вызваны обработчиком действий `on_invoke_activity` Teams, включает следующие:

| Типы вызовов                    | Обработник                              | Описание                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `on_teams_card_action_invoke`       | Вызов действия карточки Teams. |
| fileConsent/invoke              | `on_teams_file_consent_accept`      | Согласие на файл Teams принимается. |
| fileConsent/invoke              | `on_teams_file_consent`            | Согласие на файл Teams. |
| fileConsent/invoke              | `on_teams_file_consent_decline`     | Согласие на файл Teams отклонено. |
| actionableMessage/executeAction | `on_teams_o365_connector_card_action` | Действие карточки соединители Teams O365. |
| signin/verifyState              | `on_teams_signin_verify_state`      | Teams sign in verify state. |
| task/fetch                      | `on_teams_task_module_fetch`        | Извлечение модуля задач Teams. |
| task/submit                     | `on_teams_task_module_submit`       | Отправка модуля задач Teams. |

Действия по вызову, перечисленные в разделе "Действия по вызову Teams", посвящены ботам в беседах в Teams. SDK Bot Framework также поддерживает вызов действий, характерных для расширений обмена сообщениями. Дополнительные сведения см. в дополнительных сведениях [о расширениях обмена сообщениями.](https://aka.ms/azure-bot-what-are-messaging-extensions)

---
