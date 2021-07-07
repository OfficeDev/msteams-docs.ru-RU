---
title: Использование microsoft Graph для авторизации активной установки ботов и обмена сообщениями в Teams
description: Описывает активный обмен сообщениями в Teams и как реализовать.
localization_priority: Normal
author: akjo
ms.author: lajanuar
ms.topic: Overview
keywords: группы проактивной установки чата Graph
ms.openlocfilehash: 0f59a74cc24b7d80dd3afd4aa4369a47d56e4d59
ms.sourcegitcommit: a6253e89cb8c8c34d45b06e08c9668daeebc30a3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/06/2021
ms.locfileid: "53300307"
---
# <a name="proactive-installation-of-apps-using-graph-api-to-send-messages"></a>Упреждающая установку приложений с помощью API Graph для отправки сообщений

>[!IMPORTANT]
> Предварительные Graph и Microsoft Teams доступны для раннего доступа и отзывов. Хотя этот выпуск прошел широкое тестирование, он не предназначен для использования в производстве.

## <a name="proactive-messaging-in-teams"></a>Активный обмен сообщениями в Teams

Активные сообщения инициировали боты, чтобы начать беседы с пользователем. Они служат многим целям, включая отправку приветствия, проведение опросов или опросов, а также уведомления для всей организации вещания. Активные сообщения в Teams могут быть доставлены в качестве бесед на основе **ad-hoc** или **диалогов:**

|Тип сообщения | Описание |
|----------------|-------------- |
|Ad-hoc proactive message| Бот перенабивает сообщение, не прерывая поток беседы.|
|Упреждающие сообщения на основе диалогов | Бот создает новый диалоговое нить, контролирует беседу, доставляет проактивное сообщение, закрывает и возвращает контроль в предыдущий диалог.|

## <a name="proactive-app-installation-in-teams"></a>Активная установка приложения в Teams

Прежде чем ваш бот сможет активно отправлять сообщения пользователю, он должен быть установлен как личное приложение или в команде, в которой пользователь является участником. Иногда необходимо заблаговременно отправлять сообщения пользователям, которые не установили или ранее не взаимодействовали с вашим приложением. Например, необходимо отправлять важные сведения всем в вашей организации. Для таких сценариев можно использовать API microsoft Graph для активной установки бота для пользователей.

## <a name="permissions"></a>Разрешения

Разрешения типа ресурсов Microsoft Graph [TeamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) помогают управлять жизненным циклом установки приложения для всех областей пользовательского (личного) или командного (канала) в Microsoft Teams платформе:

|Разрешение приложения | Описание|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|Позволяет приложению Teams чтение, установку, обновление и самоустановку для любого пользователя без предварительного входе или использования.|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|Позволяет приложению Teams читать, устанавливать, обновлять и удалить себя в любой команде без предварительного входе или использования.|

Чтобы использовать эти разрешения, необходимо добавить ключ [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) в манифест приложения со следующими значениями:

* **id:** ID Azure Active Directory (AAD).
* **ресурс.** URL-адрес ресурса для приложения.

> [!NOTE]
>
> * Боту требуется приложение, а не делегированная пользователем разрешения, так как установка для других пользователей.
>
> * Администратор клиента AAD должен [явно предоставлять разрешения приложению.](/graph/security-authorization#grant-permissions-to-an-application) После получения разрешений все члены клиента AAD получают предоставленные разрешения.

## <a name="enable-proactive-app-installation-and-messaging"></a>Включить активную установку приложений и обмен сообщениями

> [!IMPORTANT]
> Microsoft Graph может устанавливать только приложения, опубликованные в магазине приложений организации или Teams магазине.

### <a name="create-and-publish-your-proactive-messaging-bot-for-teams"></a>Создание и публикация вашего активного бота обмена сообщениями для Teams

Чтобы начать работу, [](../../bots/how-to/create-a-bot-for-teams.md) вам нужен бот для [](../../concepts/bots/bot-conversations/bots-conv-proactive.md) Teams с проактивными [](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-your-org) возможностями обмена сообщениями, который находится в магазине приложений организации или [Teams магазине.](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-the-teams-store)

> [!TIP]
> Готовый к производству [*шаблон Communicator*](../..//samples/app-templates.md#company-communicator) позволяет транслировать сообщения и является хорошим началом для создания вашего проактивного приложения-бота.

### <a name="get-the-teamsappid-for-your-app"></a>Get the `teamsAppId` for your app

Вы можете получить `teamsAppId` следующие способы:

* Из каталога приложений организации:

    **Ссылка Graph Microsoft:** [тип ресурсов teamsApp](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)

    **ЗАПРОС HTTP GET:**

    ```http
        GET https://graph.microsoft.com/v1.0/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
    ```

    Запрос должен вернуть объект, который является созданным в каталоге приложения `teamsApp` `id` ИД приложения. Это отличается от ID, который вы предоставили в манифесте Teams приложения:

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

* Если приложение уже загружено или загружено для пользователя в личной области:

    **Ссылка Graph Microsoft: Список** [приложений, установленных для пользователя](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

    **ЗАПРОС HTTP GET:**

    ```http
    GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
    ```

* Если ваше приложение уже загружено или загружено для канала в области группы:

    **Ссылка Graph Microsoft: Список** [приложений в команде](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

    **ЗАПРОС HTTP GET:**

    ```http
    GET https://graph.microsoft.com/v1.0/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
    ```

    > [!TIP]
    > Чтобы сузить список результатов, можно отфильтровать любое из полей [**объекта teamsApp.**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)

### <a name="determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a>Определите, установлен ли в настоящее время бот для получателя сообщения

Вы можете определить, установлен ли ваш бот для получателя сообщений следующим образом:

**Ссылка Graph Microsoft: Список** [приложений, установленных для пользователя](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**ЗАПРОС HTTP GET:**

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

Возвращает запрос:

* Пустой массив, если приложение не установлено.
* Массив с одним [объектом teamsAppInstallation,](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) если приложение установлено.

### <a name="install-your-app"></a>Установка приложения

Вы можете установить приложение следующим образом:

**Ссылка Graph Microsoft:** [Установите приложение для пользователя](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**ЗАПРОС HTTP POST:**

```http
POST https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps
Content-Type: application/json

{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/v1.0/appCatalogs/teamsApps/{teamsAppId}"
}
```

Если у пользователя есть Microsoft Teams, установка приложения происходит немедленно. Для просмотра установленного приложения может потребоваться перезапуск.

### <a name="retrieve-the-conversation-chatid"></a>Извлечение беседы `chatId`

Когда приложение установлено для пользователя, бот получает уведомление о событии, содержа которое содержит необходимые сведения для `conversationUpdate` [](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) отправки проактивного сообщения.

**Ссылка Graph microsoft:** [получить чат](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)

1. Вы должны иметь приложение `{teamsAppInstallationId}` . Если у вас его нет, используйте следующие:

    **ЗАПРОС HTTP GET:**

    ```http
    GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
    ```

    Свойство **id** ответа — `teamsAppInstallationId` .

1. Сделайте следующий запрос, чтобы `chatId` получить:

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

### <a name="send-proactive-messages"></a>Отправка упреждающих сообщений

Ваш бот может [отправлять упреждающие](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) сообщения после того, как бот был добавлен для пользователя или группы и получил всю информацию о пользователе.

## <a name="code-sample"></a>Пример кода

| **Имя образца** | **Описание** | **.NET** | **Node.js** |
|---------------|--------------|--------|-------------|--------|
| Активная установка приложения и отправка упреждающих уведомлений | В этом примере показано, как можно использовать активную установку приложения для пользователей и отправлять упреждающие уведомления, вызывая API Graph Microsoft. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-proactive-installation/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-proactive-installation/nodejs) |

## <a name="see-also"></a>См. также

* [**Управление политиками установки приложений в Microsoft Teams**](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)
* [Отправка упреждающих уведомлений пользователям SDK v4](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)

## <a name="additional-code-samples"></a>Дополнительные примеры кода
>
> [!div class="nextstepaction"]
> [**Teams примеры кода проактивных сообщений**](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-proactive-messaging/csharp)
