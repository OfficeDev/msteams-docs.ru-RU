---
title: Используйте Microsoft Graph для авторизации упреждающей установки бота и обмена сообщениями в Teams.
description: В этой статье описывается упреждающий обмен сообщениями в Teams и способы его реализации. Узнайте, как включить упреждающую установку приложений и обмен сообщениями, используя образец кода.
ms.localizationpriority: medium
author: akjo
ms.author: lajanuar
ms.topic: Overview
ms.openlocfilehash: 832dfe6ddce7710d506c480fc1195c426b8da0df
ms.sourcegitcommit: 7bbb7caf729a00b267ceb8af7defffc91903d945
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/21/2022
ms.locfileid: "66189586"
---
# <a name="proactive-installation-of-apps-using-graph-api-to-send-messages"></a>Упреждающая установку приложений с помощью API Graph для отправки сообщений

## <a name="proactive-messaging-in-teams"></a>Упреждающий обмен сообщениями в Teams

Упреждающие сообщения инициируются ботами для начала разговора с пользователем. Они служат многим целям, включая отправку приветственных сообщений, проведение опросов или исследований, а также рассылку уведомлений широкого охвата по всей организации. Упреждающие сообщения в Teams могут быть доставлены в виде **ситуативных** или **диалоговых бесед**:

|Тип сообщения | Описание |
|----------------|-------------- |
|Ситуативное упреждающее сообщение| Бот вставляет сообщение, не прерывая поток беседы.|
|Диалоговое упреждающее сообщение | Бот создает новую ветку диалога, берет на себя управление беседой, доставляет упреждающее сообщение, закрывает и возвращает управление предыдущему диалогу.|

## <a name="proactive-app-installation-in-teams"></a>Упреждающая установка приложений в Teams

Прежде чем бот сможет активно отправлять сообщения пользователю, его необходимо установить либо как личное приложение, либо в команде, участником которой является пользователь. Иногда необходимо заблаговременно отправлять сообщения пользователям, которые еще не установили или ранее взаимодействовали с вашим приложением. Например, если вам нужно отправлять важные сведения всем пользователям в организации, вы можете использовать microsoft API Graph для упреждающего установки бота для пользователей.

## <a name="permissions"></a>Разрешения

Разрешения Microsoft Graph [типа ресурса teamAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) помогают управлять жизненным циклом установки приложения для всех пользовательских (личных) или групповых (канальных) областей на платформе Microsoft Teams:

|Разрешение приложения | Описание|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|Позволяет приложению Teams читать, устанавливать, обновлять и удалять себя для любого *пользователя* без предварительного входа или использования.|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|Позволяет приложению Teams читать, устанавливать, обновлять и удалять себя в любой *команде* без предварительного входа или использования.|

Чтобы использовать эти разрешения, необходимо добавить в манифест приложения ключ [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) со следующими значениями:

* **id**: идентификатор приложения Azure Active Directory.
* **ресурс**: URL-адрес ресурса для приложения.

> [!NOTE]
>
> * Боту требуются приложения, а не делегированные пользователем разрешения, поскольку установка предназначена для других.
>
> * Администратор арендатора Azure AD должен [явным образом предоставить разрешения приложению](/graph/security-authorization#grant-permissions-to-an-application). После того как приложению будут предоставлены разрешения, все члены арендатора Azure AD получат предоставленные разрешения.

## <a name="enable-proactive-app-installation-and-messaging"></a>Включить упреждающую установку приложений и обмен сообщениями

> [!IMPORTANT]
> Microsoft Graph может устанавливать только приложения, опубликованные в хранилище приложений организации или в Teams Store.

### <a name="create-and-publish-your-proactive-messaging-bot-for-teams"></a>Создайте и опубликуйте бот для активного обмена сообщениями для Teams

Для начала вам понадобится [бот для Teams](../../bots/how-to/create-a-bot-for-teams.md) с [возможностями упреждающего обмена сообщениями](../../concepts/bots/bot-conversations/bots-conv-proactive.md), который находится в [хранилище приложений организации](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-your-org) или в [Teams Store](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-the-teams-store).

> [!TIP]
> Готовый к работе шаблон приложения [*Company Communicator*](../..//samples/app-templates.md#company-communicator) позволяет осуществлять широковещательную рассылку сообщений и является хорошим началом для создания упреждающего приложения-бота.

### <a name="get-the-teamsappid-for-your-app"></a>Получите `teamsAppId` для приложения

Вы можете получить `teamsAppId` следующими способами:

* Из каталога приложений организации:

    **Справочник по странице Microsoft Graph:** [тип ресурса teamApp](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)

    Запрос **HTTP GET**:

    ```http
    GET https://graph.microsoft.com/v1.0/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
    ```

    Запрос должен возвращать `teamsApp`объект`id`, который представляет собой идентификатор приложения, сгенерированный каталогом приложения. Он отличается от идентификатора, который вы указали в манифесте приложения Teams:

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

* Если ваше приложение уже было отправлено или загружено как неопубликованное приложение для пользователя в индивидуальном объеме:

    **Справочник по странице Microsoft Graph:** [Список приложений, установленных для пользователя](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

    Запрос **HTTP GET**:

    ```http
    GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
    ```

* Если ваше приложение уже отправлено или загружено как неопубликованное приложение для канала в Teams в масштабе команды:

    **Справочник по странице Microsoft Graph:** [Список приложений в команде](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

    Запрос **HTTP GET**:

    ```http
    GET https://graph.microsoft.com/v1.0/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
    ```

    > [!TIP]
    > Чтобы сузить список результатов, вы можете отфильтровать любое из полей объекта [**teamApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true).

### <a name="determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a>Определите, установлен ли ваш бот в настоящее время для получателя сообщения

Вы можете определить, установлен ли ваш бот для получателя сообщения, следующим образом:

**Справочник по странице Microsoft Graph:** [Список приложений, установленных для пользователя](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

Запрос **HTTP GET**:

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

Запрос возвращает:

* Пустой массив, если приложение не установлено.
* Массив с одним объектом [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true), если приложение установлено.

### <a name="install-your-app"></a>Установите приложение

Вы можете установить приложение следующим образом:

**Ссылка на страницу Microsoft Graph:** [Установить приложение для пользователя](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

Запрос **HTTP POST**

```http
POST https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps
Content-Type: application/json

{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/v1.0/appCatalogs/teamsApps/{teamsAppId}"
}
```

Если у пользователя запущены Microsoft Teams, установка приложения происходит немедленно. Для просмотра установленного приложения может потребоваться перезагрузка.

### <a name="retrieve-the-conversation-chatid"></a>Получить беседу `chatId`

Когда ваше приложение установлено для пользователя, бот получает `conversationUpdate` [уведомление о событии](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition), содержащее необходимую информацию для отправки упреждающего сообщения.

**Справочник по странице Microsoft Graph:** [Получить чат](/graph/api/chat-get?view=graph-rest-v1.0&tabs=http&preserve-view=true)

1. У вас должен быть `{teamsAppInstallationId}` приложения. Если у вас ее нет, используйте следующую команду:

    Запрос **HTTP GET**:

    ```http
    GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
    ```

    Свойство **id** отклика — `teamsAppInstallationId`.

1. Отправьте следующий запрос, чтобы получить `chatId`:

    **HTTP-запрос GET** (разрешение—`TeamsAppInstallation.ReadWriteSelfForUser.All` ):  

    ```http
    GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
    ```

    Свойство **id** отклика — `chatId`.

    Вы также можете получить `chatId` с помощью следующего запроса, но для этого требуется более широкое `Chat.Read.All` разрешение:

    **HTTP-запрос GET** (разрешение—`Chat.Read.All` ):

    ```http
    GET https://graph.microsoft.com/v1.0/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
    ```

### <a name="send-proactive-messages"></a>Отправка упреждающих сообщений

Бот может [отправлять упреждающие сообщения](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) после добавления бота для пользователя или команды и получения им всех сведений о пользователе.

## <a name="code-snippets"></a>Фрагменты кода

Следующий код представляет собой пример отправки упреждающих сообщений:

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
public async Task<int> SendNotificationToAllUsersAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
   int msgSentCount = 0;

   // Send notification to all the members
   foreach (var conversationReference in _conversationReferences.Values)
   {
       await turnContext.Adapter.ContinueConversationAsync(_configuration["MicrosoftAppId"], conversationReference, BotCallback, cancellationToken);
       msgSentCount++;
   }

   return msgSentCount;
}

private async Task BotCallback(ITurnContext turnContext, CancellationToken cancellationToken)
{
   await turnContext.SendActivityAsync("Proactive hello.");
}
```

# <a name="nodejs"></a>[Node.js](#tab/nodejs)

```javascript
server.get('/api/notify', async (req, res) => {
    for (const conversationReference of Object.values(conversationReferences)) {
        await adapter.continueConversationAsync(process.env.MicrosoftAppId, conversationReference, async context => {
            await context.sendActivity('proactive hello');
        });
    }

    res.setHeader('Content-Type', 'text/html');
    res.writeHead(200);
    res.write('<html><body><h1>Proactive messages have been sent.</h1></body></html>');
    res.end();
});
```

---

## <a name="code-sample"></a>Пример кода

| **Название примера** | **Описание** | **.NET** | **Node.js** |
|---------------|--------------|--------|-------------|
| Упреждающая установка приложений и отправка упреждающих уведомлений | В этом примере показано, как использовать упреждающую установку приложений для пользователей и отправлять упреждающие уведомления, вызывая API Microsoft Graph. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-proactive-installation/csharp) | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-proactive-installation/nodejs) |

## <a name="additional-code-samples"></a>Дополнительный образец кода
>
> [!div class="nextstepaction"]
> [**Примеры кода упреждающих сообщений в Teams**](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-proactive-messaging/csharp)

## <a name="see-also"></a>Дополнительные ресурсы

* [Управление политиками настройки приложений в Microsoft Teams](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)
* [Отправка упреждающих уведомлений пользователям SDK v4](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)
