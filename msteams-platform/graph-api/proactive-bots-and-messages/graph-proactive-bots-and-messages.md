---
title: Использование Microsoft Graph для включения активной установки и обмена мгновенными сообщениями в Teams
description: Описание упреждающего обмена сообщениями в Teams и способов их реализации.
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: установочный график чата активных сообщений в Teams
ms.openlocfilehash: f1d2c51957eefbc548918210b843e408eb1107c8
ms.sourcegitcommit: 7a2da3b65246a125d441a971e7e6a6418355adbe
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "46587743"
---
# <a name="enable-proactive-bot-installation-and-proactive-messaging-in-teams-with-microsoft-graph-public-preview"></a>Включение активной установки и упреждающего обмена сообщениями в Teams с помощью Microsoft Graph (общедоступная Предварительная версия)

>[!IMPORTANT]
> Общедоступные предварительные обзоры Microsoft Graph доступны для раннего доступа и обратной связи. Несмотря на то что этот выпуск протестировался, он не предназначен для использования в рабочей среде.

## <a name="proactive-messaging-in-teams"></a>Активная система обмена сообщениями в Teams

Активные сообщения инициируются Боты, чтобы начать беседу с пользователем. Они позволяют выполнять различные задачи, включая отправку приветственных сообщений, проведение опросов и опросов, а также трансляцию уведомлений в масштабах Организации.  Интерактивные сообщения в Teams могут доставляться как беседы на основе **специальных** или **диалоговых окон** .

|Тип сообщения | Описание |
|----------------|-------------- |
|Прямое упреждающее сообщение| Элемент Bot интержектс сообщение, не прерывая потоки бесед.|
|Упреждающее сообщение на основе диалоговых окон | Bot создает новый поток диалоговых окон, получает Управление беседами, доставляет упреждающее сообщение, закрывает и возвращает управление предыдущему диалоговому окну.|

*Просмотр*, [Отправка упреждающего уведомления пользователям пакет SDK v4](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp)

## <a name="proactive-app-installation-in-teams"></a>Упреждающее установка приложений в Teams

Прежде чем приступить к отправку сообщений пользователю Bot, его необходимо установить либо в качестве личного приложения, либо в группу, в которую входит пользователь. Иногда может потребоваться упреждающее сообщение о том, что приложение не было установлено или _не_ было взаимодействовать с ним ранее. Например, необходимо получить важную информацию для всех пользователей в Организации. Для таких сценариев можно использовать API Microsoft Graph для профилактической установки программы-робота для пользователей.

## <a name="permissions"></a>Разрешения

Разрешения [типа ресурса](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0) Microsoft Graph теамсаппинсталлатион позволяют управлять жизненным циклом установки приложения для всех областей пользователя (персональных) или группы (каналов) на платформе Microsoft teams:

|Разрешение приложения | Описание|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|Позволяет приложению Teams читать, устанавливать, обновлять и удалять себя для любого **пользователя**без предварительного входа или использования.|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|Позволяет приложению Teams читать, устанавливать, обновлять и удалять себя в любой **команде**без предварительного входа или использования.|

Чтобы использовать эти разрешения, необходимо добавить в манифест приложения ключ [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) со следующими значениями:
> [!div class="checklist"]
> [!div class="checklist"]
>
> * **ID** — идентификатор приложения Azure AD.
> * **ресурс** — URL-адрес ресурса для приложения.
>

>[!NOTE]
>
> * Для работы с Bot требуются _приложения_ , не являющиеся _делегированными пользователями_ , так как установка не предназначена для других пользователей.
>
> * Администратор клиента Azure AD должен [явным образом предоставить разрешения приложению](/graph/security-authorization#grant-permissions-to-an-application). После получения разрешений для приложения _все_ участники клиента Azure AD получат предоставленные разрешения.

## <a name="enable-proactive-app-installation-and-messaging"></a>Включение упреждающего установки и обмена сообщениями для приложения

 > [!IMPORTANT]
>Microsoft Graph будет устанавливать только приложения, опубликованные в [каталоге приложений](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) вашей организации или в [AppSource](https://appsource.microsoft.com/).

### <a name="-create-and-publish-your-proactive-messaging-bot-for-teams"></a>✔ Создания и публикации робота для работы с системой обмена сообщениями для Teams

Чтобы приступить к работе, вам потребуются [Bot для Teams](../../bots/how-to/create-a-bot-for-teams.md) с возможностями [упреждающего обмена сообщениями](../../concepts/bots/bot-conversations/bots-conv-proactive.md) и [опубликованы](../../concepts/deploy-and-publish/overview.md) в [каталоге приложений](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) организации или в [AppSource](https://appsource.microsoft.com/).

>[!TIP]
> Шаблон приложения [**Communicator компании Communicator**](../..//samples/app-templates.md#company-communicator) включает обмен сообщениями и является хорошим фундаментом для создания упреждающего приложения-Bot.

### <a name="-get-the-teamsappid-for-your-app"></a>✔ Получить `teamsAppId` ваше приложение

**1.** вам потребуется выполнить `teamsAppId` дальнейшие действия.

`teamsAppId`Можно получить из каталога приложений вашей организации:

**Справочник по страницам Microsoft Graph:** [тип ресурса teamsApp](/graph/api/resources/teamsapp?view=graph-rest-1.0)

**Http-запрос Get** :

```http
GET https://graph.microsoft.com/beta/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
```

Запрос возвратит `teamsApp` объект. Возвращаемый объект `id` — это идентификатор приложения, создаваемый каталогом приложения, который отличается от идентификатора "ID:", указанного в манифесте приложения teams:

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

**2.** если ваше приложение уже было отправлено или неопубликованные для пользователя в личной области, вы можете получить `teamsAppId` следующее:

**Справочник по страницам Microsoft Graph:** [список приложений, установленных для пользователя](/graph/api/user-list-teamsappinstallation?view=graph-rest-beta&tabs=http)

**Http-запрос Get** :

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

**3.** если ваше приложение уже было отправлено или неопубликованные для канала в области группы, вы можете получить `teamsAppId` следующее:

**Справочник по страницам Microsoft Graph:** [список приложений в команде](/graph/api/teamsappinstallation-list?view=graph-rest-beta&tabs=http)

**Http-запрос Get** :

```http
GET https://graph.microsoft.com/beta/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{manifestId}'
```

>[!TIP]
> Для сужения списка результатов можно выполнить фильтрацию по любому из полей объекта [**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0) .

### <a name="-determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a>✔ Определить, установлен ли в данный момент ваш Bot для получателя сообщения

**Справочник по страницам Microsoft Graph:** [список приложений, установленных для пользователя](/graph/api/user-list-teamsappinstallation?view=graph-rest-beta&tabs=http)

**Http-запрос Get** :

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

Этот запрос возвратит пустой массив, если приложение не установлено, или массив с одним объектом [теамсаппинсталлатион](/graph/api/resources/teamsappinstallation?view=graph-rest-beta) , если он был установлен.

### <a name="-install-your-app"></a>✔ Установить приложение

**Справка по Microsoft Graph:** [Установка приложения для пользователя](/graph/api/user-add-teamsappinstallation?view=graph-rest-beta&tabs=http)

**Http-запрос POST** :

```http
POST https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps
{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/beta/appCatalogs/teamsApps/{teamsAppId}"
}
```

Если у пользователя установлена служба Microsoft Teams, вы можете сразу же увидеть установку приложения. Кроме того, для просмотра установленного приложения может потребоваться перезагрузка.

### <a name="-retrieve-the-conversation-chatid"></a>✔ Получить **чатид** беседы

Когда приложение устанавливается для пользователя, Bot получит `conversationUpdate` [уведомление о событии](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) , в котором будут содержаться необходимые сведения для отправки упреждающего сообщения.

`chatId`Кроме того, можно получить следующие значения:

**Справка по Microsoft Graph:** [Получение чата](/graph/api/chat-get?view=graph-rest-beta&tabs=http)

**1.** вам потребуются приложения `{teamsAppInstallationId}` . Если у вас его нет, выполните указанные ниже действия.

**Http-запрос Get** :

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

Свойство **ID** ответа имеет значение `teamsAppInstallationId` .

**2.** сделайте следующий запрос для получения `chatId` :

**Http-запрос Get** (разрешение `TeamsAppInstallation.ReadWriteSelfForUser.All` ):  

```http
 GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
```

Свойство **ID** ответа имеет значение `chatId` .

Кроме того, вы можете получить `chatId` запрос с запросом ниже, но для этого потребуется более широкое `Chat.Read.All` разрешение:

**Http-запрос Get** (разрешение `Chat.Read.All` ):

```http
GET https://graph.microsoft.com/beta/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
```

### <a name="-send-proactive-messages"></a>✔ Отправки упреждающих сообщений

После добавления ленты для пользователя или группы и получения необходимых сведений о пользователе он может начать [отправку активных сообщений](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp).

# <a name="c--net"></a>[C#/.NET](#tab/csharp)

Приведенный ниже фрагмент кода относится к [примерам Microsoft Bot Framework для C#.](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/16.proactive-messages)

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

Приведенный ниже фрагмент кода относится к [примерам Microsoft Bot Framework для JavaScript](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/16.proactive-messages).

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

## <a name="related-topic-for-teams-administrators"></a>Раздел, посвященный администраторам Teams
>
> [!div class="nextstepaction"]
> [**Управление политиками установки приложений в Microsoft Teams**](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)

## <a name="view-additional-code-samples"></a>Просмотр дополнительных примеров кода
>
> [!div class="nextstepaction"]
> [**Примеры кода для активных сообщений Teams**](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>
