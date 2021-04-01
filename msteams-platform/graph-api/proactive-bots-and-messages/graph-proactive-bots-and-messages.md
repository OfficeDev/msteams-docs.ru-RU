---
title: Использование Microsoft Graph для авторизации активной установки ботов и обмена сообщениями в Teams
description: Описывает активную передачу сообщений в Teams и ее реализацию.
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: teams proactive messaging chat installation Graph
ms.openlocfilehash: 4f9c1c2e73fc89d37792e59153affc398bb87044
ms.sourcegitcommit: 3bd2627b7a334568f61ccc606395e3d89aa521d9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/31/2021
ms.locfileid: "51475937"
---
# <a name="proactive-installation-of-apps-using-graph-api-and-send-messages"></a>Упреждающая установку приложений с помощью API Graph и отправка сообщений

>[!IMPORTANT]
> Общедоступные предварительные просмотры Microsoft Graph и Microsoft Teams доступны для раннего доступа и отзывов. Хотя этот выпуск прошел широкое тестирование, он не предназначен для использования в производстве.

## <a name="proactive-messaging-in-teams"></a>Активный обмен сообщениями в Teams

Активные сообщения инициировали боты, чтобы начать беседы с пользователем. Они служат многим целям, включая отправку приветствия, проведение опросов или опросов, а также уведомления для всей организации вещания. Активные сообщения в Teams могут доставляться в качестве бесед на основе **ad-hoc** или **диалогов:**

|Тип сообщения | Описание |
|----------------|-------------- |
|Ad-hoc proactive message| Бот перенабивает сообщение, не прерывая поток беседы.|
|Упреждающие сообщения на основе диалогов | Бот создает новый диалоговое нить, контролирует беседу, доставляет проактивное сообщение, закрывает и возвращает контроль в предыдущий диалог.|

См. в [рубрике Отправка упреждающих уведомлений пользователям SDK v4](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true).

## <a name="proactive-app-installation-in-teams"></a>Активная установка приложений в Teams

Прежде чем ваш бот сможет активно отправлять сообщения пользователю, он должен быть установлен как личное приложение или в команде, в которой пользователь является участником. Иногда необходимо заблаговременно отправлять сообщения пользователям, которые не установили или ранее не взаимодействовали с вашим приложением. Например, необходимо отправлять жизненно важные сведения всем в вашей организации. Для таких сценариев можно использовать API Microsoft Graph для активной установки бота для пользователей.

## <a name="permissions"></a>Разрешения

Разрешения типа ресурсов Microsoft Graph [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) помогают управлять жизненным циклом установки приложения для всех областей пользовательского (личного) или командного (канала) в платформе Microsoft Teams:

|Разрешение приложения | Описание|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|Позволяет приложению Teams читать, устанавливать, обновлять и удалить себя для любого пользователя **без** предварительного входе или использования.|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|Позволяет приложению Teams читать, устанавливать, обновлять и удалить себя в любой команде **без** предварительного входе или использования.|

Чтобы использовать эти разрешения, необходимо добавить ключ [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) в манифест приложения со следующими значениями:
> [!div class="checklist"]
> [!div class="checklist"]
>
> * **id** — ваш ID приложения Azure AD.
> * **ресурс** — URL-адрес ресурса для приложения.
>
>[!NOTE]
>
> * Боту требуется приложение, а не делегированная пользователем разрешения, так как установка для других пользователей.
>
> * Администратор клиента Azure AD должен явно предоставлять разрешения [приложению.](/graph/security-authorization#grant-permissions-to-an-application) После получения разрешений все члены клиента Azure AD получают предоставленные разрешения.

## <a name="enable-proactive-app-installation-and-messaging"></a>Включить активную установку приложений и обмен сообщениями

 > [!IMPORTANT]
>Microsoft Graph может устанавливать приложения, опубликованные [](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) только в каталоге приложений организации или [в AppSource.](https://appsource.microsoft.com/)

### <a name="-create-and-publish-your-proactive-messaging-bot-for-teams"></a>✔ создание и публикация вашего активного бота обмена сообщениями для Teams

Чтобы начать работу, вам нужен бот для [Teams](../../bots/how-to/create-a-bot-for-teams.md) [с](../../concepts/bots/bot-conversations/bots-conv-proactive.md) возможностями активного [](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) обмена сообщениями, который публикуется в каталоге приложений организации или [в AppSource.](https://appsource.microsoft.com/) [](../../concepts/deploy-and-publish/overview.md)

>[!TIP]
> Готовый к производству [**шаблон Communicator**](../..//samples/app-templates.md#company-communicator) позволяет транслировать сообщения и является хорошей основой для создания вашего активного приложения-бота.

### <a name="-get-the-teamsappid-for-your-app"></a>✔ Получить для `teamsAppId` вашего приложения

**1.** Необходимы `teamsAppId` следующие действия.

Можно извлечь из каталога приложений `teamsAppId` организации:

**Ссылка на страницу Microsoft Graph:** [тип ресурсов teamsApp](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)

**ЗАПРОС HTTP GET:**

```http
GET https://graph.microsoft.com/v1.0/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
```

Запрос должен вернуть `teamsApp` объект. Возвращаемый объект — это созданный каталог приложения ИД приложения, который отличается от ID, который вы предоставили в манифесте `id` приложения Teams:

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

**2.**  Если ваше приложение уже загружено или загружено для пользователя в личной области, вы можете получить следующим `teamsAppId` образом:

**Ссылка на страницу Microsoft Graph: список** [приложений, установленных для пользователя](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**ЗАПРОС HTTP GET:**

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

**3.** Если ваше приложение было загружено или загружено для канала в области группы, вы можете получить следующим `teamsAppId` образом:

**Ссылка на страницу Microsoft Graph:** [Список приложений в команде](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**ЗАПРОС HTTP GET:**

```http
GET https://graph.microsoft.com/v1.0/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

>[!TIP]
> Чтобы сузить список результатов, можно фильтровать любой из полей [**объекта teamsApp.**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)

### <a name="-determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a>✔ определите, установлен ли ваш бот для получателя сообщения

**Ссылка на страницу Microsoft Graph: список** [приложений, установленных для пользователя](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**ЗАПРОС HTTP GET:**

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

В этом запросе возвращается пустой массив, если приложение не установлено, и массив с одним объектом [teamsAppInstallation,](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) если приложение установлено.

### <a name="-install-your-app"></a>✔ Установите приложение

**Ссылка на страницу Microsoft Graph:** [Установка приложения для пользователя](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**ЗАПРОС HTTP POST:**

```http
POST https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps
Content-Type: application/json

{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/v1.0/appCatalogs/teamsApps/{teamsAppId}"
}
```

Если у пользователя запущена Microsoft Teams, сразу же будет видна установка приложения. Для просмотра установленного приложения может потребоваться перезапуск.

### <a name="-retrieve-the-conversation-chatid"></a>✔ диалог **chatId**

Когда приложение установлено для пользователя, бот получает уведомление о событии, содержа которое содержит необходимые сведения для `conversationUpdate` [](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) отправки проактивного сообщения.

Можно `chatId` также извлечь следующим образом:

**Ссылка на страницу Microsoft Graph:** [получить чат](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)

**1.** Вам необходимо ваше приложение `{teamsAppInstallationId}` . Если у вас его нет, используйте следующие:

**ЗАПРОС HTTP GET:**

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

Свойство **id** ответа — `teamsAppInstallationId` .

**2.** Сделайте следующий запрос, чтобы получить `chatId` :

**HTTP GET** request (permission — `TeamsAppInstallation.ReadWriteSelfForUser.All` ):  

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
```

Свойство **id** ответа — `chatId` .

Вы также можете получить следующий запрос, но для этого требуется `chatId` более широкое `Chat.Read.All` разрешение:

**HTTP GET** request (permission — `Chat.Read.All` ):

```http
GET https://graph.microsoft.com/beta/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
```

### <a name="-send-proactive-messages"></a>✔ Отправка проактивных сообщений

Ваш бот может [отправлять упреждающие](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) сообщения после того, как бот был добавлен для пользователя или группы и получил всю информацию о пользователе.

## <a name="related-topic-for-teams-administrators"></a>Связанная тема для администраторов Teams
>
> [!div class="nextstepaction"]
> [**Управление политиками настройки приложений в Microsoft Teams**](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)

## <a name="view-additional-code-samples"></a>Просмотр дополнительных примеров кода
>
> [!div class="nextstepaction"]
> [**Teams proactive messaging code samples**](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>
