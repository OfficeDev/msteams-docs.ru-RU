---
title: Использование Microsoft Graph для упреждающих установок ботов и обмена сообщениями в Teams
description: Описание упреждающего обмена сообщениями в Teams и реализации.
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: Teams proactive messaging chat installation Graph
ms.openlocfilehash: ee1620c8fdcaeeecf0e8b0992017bf6f2fbacbf9
ms.sourcegitcommit: d0e71ea63af2f67eba75ba283ec46cc7cdf87d75
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/24/2020
ms.locfileid: "49731974"
---
# <a name="enable-proactive-bot-installation-and-proactive-messaging-in-teams-with-microsoft-graph-public-preview"></a>Включить упреждающие установки ботов и упреждающие сообщения в Teams с помощью Microsoft Graph (public Preview)

>[!IMPORTANT]
> Общедоступные предварительные версии Microsoft Graph и Microsoft Teams доступны для раннего доступа и отзывов. Хотя этот выпуск прошел тщательное тестирование, он не предназначен для использования в производственной версии.

## <a name="proactive-messaging-in-teams"></a>Упреждающий обмен сообщениями в Teams

Боты инициировали упреждающие сообщения, чтобы начать беседы с пользователем. Они служат для многих целей, включая отправку приветствия, проведение опросов и трансляцию уведомлений на всей организации.  Упреждающие сообщения в Teams  могут доставляться как в качестве неучетных, так и в **диалоговые** беседы:

|Тип сообщения | Описание |
|----------------|-------------- |
|Нечеткие упреждающие сообщения| Бот перемеивает сообщение, не прерывая поток беседы.|
|Упреждающие сообщения на основе диалогов | Бот создает новый диалоговое окно, управляет беседой, доставляет упреждающие сообщения, закрывает и возвращает контроль предыдущему диалогову.|

*См.*" [Отправка упреждающих уведомлений пользователям SDK v4](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)

## <a name="proactive-app-installation-in-teams"></a>Упреждающие установки приложений в Teams

Прежде чем бот сможет заблаговременно отправить сообщение пользователю, его необходимо установить как личное приложение или в команде, участником которой является пользователь. Иногда может потребоваться заблаговременное сообщение пользователям, которые _не_ установили или ранее не взаимодействовали с вашим приложением. Например, необходимо отправлять важные сведения всем в организации. В таких сценариях вы можете использовать API Microsoft Graph для упреждающего установки бота для пользователей.

## <a name="permissions"></a>Разрешения

Разрешения типа ресурса [TeamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) Microsoft Graph позволяют управлять жизненным циклом установки приложения для всех областей пользователей (личных) или команд (каналов) в платформе Microsoft Teams:

|Разрешение приложения | Описание|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|Позволяет приложению Teams считывать, устанавливать, обновлять и удалить себя для любого пользователя без предварительного вход и использования.|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|Позволяет приложению Teams считывать, устанавливать, обновлять и удалить себя в любой команде **без** предварительного вход и использования.|

Чтобы использовать эти разрешения, необходимо добавить ключ [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) в манифест приложения со следующими значениями:
> [!div class="checklist"]
> [!div class="checklist"]
>
> * **id**  — ид приложения Azure AD.
> * **ресурс** — URL-адрес ресурса для приложения.
>

>[!NOTE]
>
> * Боту требуются  _не_ делегированные пользователем разрешения, а разрешения приложения, так как установка не для вас, а для других пользователей.
>
> * Администратор клиента Azure AD должен явно предоставить разрешения [для приложения.](/graph/security-authorization#grant-permissions-to-an-application) После того как приложению будут предоставлены _разрешения,_ все участники клиента Azure AD получат предоставленные разрешения.

## <a name="enable-proactive-app-installation-and-messaging"></a>Включить упреждающие установки приложений и обмен сообщениями

 > [!IMPORTANT]
>Microsoft Graph будет устанавливать только приложения, опубликованные в каталоге приложений вашей организации [или](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) [в AppSource.](https://appsource.microsoft.com/)

### <a name="-create-and-publish-your-proactive-messaging-bot-for-teams"></a>✔ создание и публикация бота упреждающего обмена сообщениями для Teams

Для начала вам потребуется бот для [](../../concepts/bots/bot-conversations/bots-conv-proactive.md) [Teams](../../bots/how-to/create-a-bot-for-teams.md) с профилактическими возможностями обмена [](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) сообщениями и опубликованными в каталоге приложений вашей организации или [в AppSource.](https://appsource.microsoft.com/) [](../../concepts/deploy-and-publish/overview.md)

>[!TIP]
> Готовый [**к**](../..//samples/app-templates.md#company-communicator) Communicator шаблон приложения компании обеспечивает широковещательный обмен сообщениями и является хорошей основой для создания вашего упреждающего приложения-бота.

### <a name="-get-the-teamsappid-for-your-app"></a>✔ Получите `teamsAppId` приложение

**1.** Вам потребуется сделать `teamsAppId`  следующее.

Его `teamsAppId` можно извлечь из каталога приложений организации:

**Справка по странице Microsoft Graph:** [тип ресурса teamsApp](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)

**HTTP-запрос GET:**

```http
GET https://graph.microsoft.com/beta/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
```

Запрос возвращает `teamsApp`  объект. Возвращенный объект — это созданный каталогом приложения и отличается от "id:", который вы предоставили в манифесте `id`  приложения Teams:

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

**2.** Если ваше приложение уже загружено или загружено неогруженным пользователем в личной области, вы можете получить: `teamsAppId`

**Справка по странице Microsoft Graph:** [список приложений, установленных для пользователя](/graph/api/userteamwork-list-installedapps?view=graph-rest-beta&tabs=http&preserve-view=true)

**HTTP-запрос GET:**

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

**3.** Если ваше приложение уже загружено или загружено неогруженным для канала в области команды, можно получить: `teamsAppId`

**Справка по странице Microsoft Graph:** [список приложений в команде](/graph/api/team-list-installedapps?view=graph-rest-beta&tabs=http&preserve-view=true)

**HTTP-запрос GET:**

```http
GET https://graph.microsoft.com/beta/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

>[!TIP]
> Можно отфильтровать любые поля объекта [**teamsApp,**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true) чтобы сузить список результатов.

### <a name="-determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a>✔ определить, установлен ли бот для получателя сообщения

**Справка по странице Microsoft Graph:** [список приложений, установленных для пользователя](/graph/api/userteamwork-list-installedapps?view=graph-rest-beta&tabs=http&preserve-view=true)

**HTTP-запрос GET:**

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

Этот запрос возвращает пустой массив, если приложение не установлено, или массив с одним объектом [teamsAppInstallation,](/graph/api/resources/teamsappinstallation?view=graph-rest-beta&preserve-view=true) если он был установлен.

### <a name="-install-your-app"></a>✔ установки приложения

**Справка по странице Microsoft Graph:** [установка приложения для пользователя](/graph/api/userteamwork-post-installedapps?view=graph-rest-beta&tabs=http&preserve-view=true)

**HTTP-запрос POST:**

```http
POST https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps
{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/beta/appCatalogs/teamsApps/{teamsAppId}"
}
```

Если у пользователя запущен Microsoft Teams, он может сразу увидеть установку приложения. Кроме того, может потребоваться перезапуск, чтобы увидеть установленное приложение.

### <a name="-retrieve-the-conversation-chatid"></a>✔ извлечения **chatId беседы**

Когда приложение установлено для пользователя, бот получит уведомление о событии, которое будет содержать необходимые сведения для `conversationUpdate` [](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) отправки упреждающего сообщения.

Кроме `chatId` того, его можно получить следующим образом:

**Справка по странице Microsoft Graph: получить** [чат](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)

**1.** Вам потребуется ваше `{teamsAppInstallationId}` приложение. Если у вас его нет, используйте следующее:

**HTTP-запрос GET:**

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

Свойство **id** ответа — `teamsAppInstallationId` .

**2.** Сделайте следующий запрос, чтобы `chatId` получить:

**HTTP-запрос GET** (разрешение — `TeamsAppInstallation.ReadWriteSelfForUser.All` ):  

```http
 GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
```

Свойство **id** ответа — `chatId` .

Кроме того, вы можете получить запрос с помощью приведенного ниже запроса, но для него `chatId`  потребуется более широкое `Chat.Read.All` разрешение:

**HTTP-запрос GET** (разрешение — `Chat.Read.All` ):

```http
GET https://graph.microsoft.com/beta/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
```

### <a name="-send-proactive-messages"></a>✔ отправки упреждающих сообщений

После того как бот был добавлен для пользователя или команды и получил необходимую информацию о пользователе, он может начать отправлять упреждающие [сообщения.](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)

# <a name="c--net"></a>[C# / .NET](#tab/csharp)

Следующий фрагмент кода взят из примеров [Microsoft Bot Framework для C#.](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/16.proactive-messages)

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

Следующий фрагмент кода взят из примеров [Microsoft Bot Framework для JavaScript.](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/16.proactive-messages)

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

## <a name="related-topic-for-teams-administrators"></a>Связанный раздел для администраторов Teams
>
> [!div class="nextstepaction"]
> [**Управление политиками настройки приложений в Microsoft Teams**](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)

## <a name="view-additional-code-samples"></a>Просмотр дополнительных примеров кода
>
> [!div class="nextstepaction"]
> [**Примеры кода упреждающих сообщений Teams**](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>
