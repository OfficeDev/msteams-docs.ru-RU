---
title: Использование Microsoft Graph для включения упреждающие установки и обмена сообщениями ботов в Teams
description: Описывает упреждающие сообщения в Teams и как реализовать их.
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: графический клиент, применяемый в упреждающем сообщении teams
ms.openlocfilehash: b601c5858e5141ce81985dca62968b1713e1d2ba
ms.sourcegitcommit: 9fd61042e8be513c2b2bd8a33ab5e9e6498d65c5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/20/2020
ms.locfileid: "46819163"
---
# <a name="enable-proactive-bot-installation-and-proactive-messaging-in-teams-with-microsoft-graph-public-preview"></a>Включение упреждающей установки бота и упреждающие сообщения в Teams с помощью Microsoft Graph (общедоступная предварительная версия)

>[!IMPORTANT]
> Для раннего доступа и получения отзывов доступны общедоступные предварительные версии Microsoft Graph и Microsoft Teams. Хотя в этом выпуске прошло обширное тестирование, он не предназначен для использования в рабочей среде.

## <a name="proactive-messaging-in-teams"></a>Заранее обмен сообщениями в Teams

Заблаговременное сообщение инициируется ботами для начала беседы с пользователем. Они служат многими целями, в том числе отправка приветственных сообщений, проведение опросов или опросов, а также трансформация уведомлений для всей организации.  Заранее упреждающие сообщения в Teams можно доставлять в виде **нерегламентированных** или **диалоговых** бесед.

|Тип сообщения | Description |
|----------------|-------------- |
|Нерегулярное сообщение| Бот интерпретирует сообщение, не прерывая поток беседы.|
|Заблаговорное сообщение на основе диалогового окна | Бот создает новую цепочку диалоговых окон, получает управление беседой, превращает заблаговремяное сообщение, закрывает и возвращает управление в предыдущее диалоговое окно.|

*Просмотр:* [отправка упреждающие уведомлений SDK 4](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp)

## <a name="proactive-app-installation-in-teams"></a>Упреждающая установка приложений в Teams

Прежде чем ваш бот сможет заблагоена отдать сообщение о пользователе, его необходимо установить в виде личного приложения или в команде, в которой пользователь является участником. Иногда может потребоваться заблаговременно профилактиковать пользователей, _которые_ не работали или ранее не взаимодействовали с вашим приложением. Например, необходимость сообщения о пользователе сообщения о пользователе всех пользователей в организации. В таких случаях можно использовать API Microsoft Graph, чтобы заблагообразовать свой бот для пользователей.

## <a name="permissions"></a>Разрешения

Разрешения [типа ресурса teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0) в Microsoft Graph позволяют управлять жизненным циклом установки приложения для всех пользователей (личных) или областей команд (канала) в платформе Microsoft Teams:

|Разрешение приложения | Description|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|Позволяет приложению Teams читать, устанавливать, обновлять и удалить себя для **любого пользователя,** не предыдущие вход или использование.|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|Позволяет приложению Teams читать, устанавливать, обновлять и удалить себя в любой **команде**без предварительного входа или использования.|

Чтобы использовать эти разрешения, добавьте ключ [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) в манифест приложения со следующими значениями:
> [!div class="checklist"]
> [!div class="checklist"]
>
> * **id**  — идентификатор приложения Azure AD.
> * **resource** — URL-адрес ресурса для приложения.
>

>[!NOTE]
>
> * Вашему боту _требуются разрешения приложения,_ _которые не_ делегированы пользователям, поскольку установка предназначена не для себя, а для других.
>
> * Администратор клиента Azure AD должен [явным образом предоставить разрешения для приложения.](/graph/security-authorization#grant-permissions-to-an-application) После получения приложением разрешений _все члены_ клиента Azure AD полбадят предоставленные разрешения.

## <a name="enable-proactive-app-installation-and-messaging"></a>Включение упреждающие установки приложений и обмена сообщениями

 > [!IMPORTANT]
>Microsoft Graph устанавливает только приложения, опубликованные в каталоге [приложений организации](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) или [в AppSource.](https://appsource.microsoft.com/)

### <a name="-create-and-publish-your-proactive-messaging-bot-for-teams"></a>✔ и публикация бота для сообщений, упреждающем в Teams

Для начала вам потребуется [бот](../../bots/how-to/create-a-bot-for-teams.md) для Teams со возможностями [заблаговорного](../../concepts/bots/bot-conversations/bots-conv-proactive.md) обмена сообщениями, который [опубликован](../../concepts/deploy-and-publish/overview.md) в каталоге приложений вашей [организации](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) [или в AppSource.](https://appsource.microsoft.com/)

>[!TIP]
> Готовый для [**рабочей Communicator**](../..//samples/app-templates.md#company-communicator) шаблон приложения "Готово к работе" обеспечивает передачу сообщений и является хорошей основой для создания проактивного приложения бота.

### <a name="-get-the-teamsappid-for-your-app"></a>✔Получение `teamsAppId` приложения

**1.** Он `teamsAppId`  понадобится на последующих этапах.

Его `teamsAppId` можно получить из каталога приложений вашей организации:

**Справочник по страницам Microsoft Graph:** [тип ресурса teamsApp](/graph/api/resources/teamsapp?view=graph-rest-1.0)

**HTTP-запрос GET:**

```http
GET https://graph.microsoft.com/beta/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
```

Запрос возвратит `teamsApp`  объект. Возвращаемый объект — это идентификатор `id`  приложения, сгенерированный каталогом приложения и отличается от идентификатора "id:", который вы указали в манифесте приложения Teams.

```json
{
  "value": [
    {
      "id": "b1c5353a-7aca-41b3-830f-27d5218fe0e5",
      "externalId": "f31b1263-ba99-435a-a679-911d24850d7c",
      "name": "Test App",
      "version": "1.0.1",
      "distributionMethod": "Organization"
    }
  ]
}
```

**2.**  Если ваше приложение уже отправлено или неопубликовано для пользователя в личной области, вы можете получить `teamsAppId` следующие сведения:

**Справочник по страницам Microsoft Graph: список** [установленных для пользователя приложений](/graph/api/user-list-teamsappinstallation?view=graph-rest-beta&tabs=http)

**HTTP-запрос GET:**

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

**3.** Если ваше приложение уже отправлено или неопубликовано для канала в области действия команды, вы можете получить `teamsAppId` указанные ниже разрешения.

**Справочник по страницам Microsoft Graph: список** [приложений в команде](/graph/api/teamsappinstallation-list?view=graph-rest-beta&tabs=http)

**HTTP-запрос GET:**

```http
GET https://graph.microsoft.com/beta/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

>[!TIP]
> Вы можете фильтровать данные по любому из полей [**объекта teamsApp,**](/graph/api/resources/teamsapp?view=graph-rest-1.0) чтобы сузить список результатов.

### <a name="-determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a>✔ Определение того, установлен ли ваш бот для получателя сообщения

**Справочник по страницам Microsoft Graph: список** [установленных для пользователя приложений](/graph/api/user-list-teamsappinstallation?view=graph-rest-beta&tabs=http)

**HTTP-запрос GET:**

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

Если приложение не установлено, этот запрос вернет пустой массив или массив с одним объектом [teamsAppInstallation,](/graph/api/resources/teamsappinstallation?view=graph-rest-beta) если оно установлено.

### <a name="-install-your-app"></a>✔ установка приложения

**Справка по Microsoft Graph:** [установка приложения для пользователя](/graph/api/user-add-teamsappinstallation?view=graph-rest-beta&tabs=http)

**HTTP-запрос POST:**

```http
POST https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps
{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/beta/appCatalogs/teamsApps/{teamsAppId}"
}
```

Если пользователь работает под управлением Microsoft Teams, он может сразу увидеть установку приложения. Или же может потребоваться перезагрузка, чтобы увидеть установленное приложение.

### <a name="-retrieve-the-conversation-chatid"></a>✔ получение идентификатора **чата**

Если ваше приложение установлено для пользователя, бот получит уведомление о событии, которое будет содержать необходимые сведения `conversationUpdate` [event notification](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) для отправки проактивного сообщения.

Его `chatId` также можно получить следующим образом:

**Справка по Microsoft Graph: получение** [чатов](/graph/api/chat-get?view=graph-rest-beta&tabs=http)

**1.** Вам понадобится ваше `{teamsAppInstallationId}` приложение. Если это не так, используйте следующую команду:

**HTTP-запрос GET:**

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

Свойство **id** отклика — `teamsAppInstallationId` это.

**2.** Отправьте приведенный ниже запрос для `chatId` получения.

**HTTP-запрос GET** (разрешение `TeamsAppInstallation.ReadWriteSelfForUser.All` — ):  

```http
 GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
```

Свойство **id** отклика — `chatId` это.

Кроме того, запрос можно `chatId`  получить с помощью запроса ниже, но для него требуется более широкий `Chat.Read.All` уровень разрешений:

**HTTP-запрос GET** (разрешение `Chat.Read.All` — ):

```http
GET https://graph.microsoft.com/beta/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
```

### <a name="-send-proactive-messages"></a>✔ отправка упреждающих сообщений

После того как ваш бот будет добавлен для пользователя или группы и получить необходимые сведения, можно начинать [отправку заблагоприятных сообщений.](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp)

# <a name="c--net"></a>[C# / .NET](#tab/csharp)

Фрагмент кода ниже взят [из примеров Microsoft Bot Framework для C#.](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/16.proactive-messages)

```csharp
using System.Collections.Concurrent;
using System.Collections.Generic;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.Bot.Builder;
using Microsoft.Bot.Schema;

namespace Microsoft.BotBuilderSamples
{
    public class ProactiveBot : ActivityHandler
    {
        // Message to send to users when the bot receives a Conversation Update event
        private const string WelcomeMessage = "Welcome to the Proactive Bot sample.  Navigate to http://localhost:3978/api/notify to proactively message everyone who has previously messaged this bot.";

        // Dependency injected dictionary for storing ConversationReference objects used in NotifyController to proactively message users
        private readonly ConcurrentDictionary<string, ConversationReference> _conversationReferences;

        public ProactiveBot(ConcurrentDictionary<string, ConversationReference> conversationReferences)
        {
            _conversationReferences = conversationReferences;
        }

        private void AddConversationReference(Activity activity)
        {
            var conversationReference = activity.GetConversationReference();
            _conversationReferences.AddOrUpdate(conversationReference.User.Id, conversationReference, (key, newValue) => conversationReference);
        }

        protected override Task OnConversationUpdateActivityAsync(ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
        {
            AddConversationReference(turnContext.Activity as Activity);

            return base.OnConversationUpdateActivityAsync(turnContext, cancellationToken);
        }

        protected override async Task OnMembersAddedAsync(IList<ChannelAccount> membersAdded, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
        {
            foreach (var member in membersAdded)
            {
                // Greet anyone that was not the target (recipient) of this message.
                if (member.Id != turnContext.Activity.Recipient.Id)
                {
                    await turnContext.SendActivityAsync(MessageFactory.Text(WelcomeMessage), cancellationToken);
                }
            }
        }

        protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
        {
            AddConversationReference(turnContext.Activity as Activity);

            // Echo back what the user said
            await turnContext.SendActivityAsync(MessageFactory.Text($"You sent '{turnContext.Activity.Text}'"), cancellationToken);
        }
    }
}
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

Фрагмент кода приведен ниже в [примерах Microsoft Bot Framework для JavaScript.](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/16.proactive-messages)

```javascript
const { ActivityHandler, TurnContext } = require('botbuilder');

class ProactiveBot extends ActivityHandler {
    constructor(conversationReferences) {
        super();

        // Dependency injected dictionary for storing ConversationReference objects used in NotifyController to proactively message users
        this.conversationReferences = conversationReferences;

        this.onConversationUpdate(async (context, next) => {
            this.addConversationReference(context.activity);

            await next();
        });

        this.onMembersAdded(async (context, next) => {
            const membersAdded = context.activity.membersAdded;
            for (let cnt = 0; cnt < membersAdded.length; cnt++) {
                if (membersAdded[cnt].id !== context.activity.recipient.id) {
                    const welcomeMessage = 'Welcome to the Proactive Bot sample.  Navigate to http://localhost:3978/api/notify to proactively message everyone who has previously messaged this bot.';
                    await context.sendActivity(welcomeMessage);
                }
            }

            // By calling next() you ensure that the next BotHandler is run.
            await next();
        });

        this.onMessage(async (context, next) => {
            this.addConversationReference(context.activity);

            // Echo back what the user said
            await context.sendActivity(`You sent '${ context.activity.text }'`);
            await next();
        });
    }

    addConversationReference(activity) {
        const conversationReference = TurnContext.getConversationReference(activity);
        this.conversationReferences[conversationReference.conversation.id] = conversationReference;
    }
}

module.exports.ProactiveBot = ProactiveBot;

```
---

## <a name="related-topic-for-teams-administrators"></a>Статья по теме для администраторов Teams
>
> [!div class="nextstepaction"]
> [**Управление политиками настройки приложений в Microsoft Teams**](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)

## <a name="view-additional-code-samples"></a>Просмотр дополнительных примеров кода
>
> [!div class="nextstepaction"]
> [**Примеры упреждающего кода обмена сообщениями Teams**](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>
