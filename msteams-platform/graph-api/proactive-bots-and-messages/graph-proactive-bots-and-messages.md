---
title: Используйте Microsoft Graph для авторизации упреждающей установки ботов и обмена сообщениями в Teams
description: Описывает упреждающие сообщения в Teams и как реализовать.
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: команды проактивной установки чата обмена сообщениями Graph
ms.openlocfilehash: 06b50e5ab8594c257959430383bab5e355af4e06
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566154"
---
# <a name="proactive-installation-of-apps-using-graph-api-and-send-messages"></a>Упреждающая установку приложений с помощью API Graph и отправка сообщений

>[!IMPORTANT]
> Microsoft Graph и Microsoft Teams предварительные просмотры доступны для раннего доступа и обратной связи. Хотя этот релиз прошел обширное тестирование, он не предназначен для использования в производстве.

## <a name="proactive-messaging-in-teams"></a>Проактивные сообщения в Teams

Проактивные сообщения ими ими ими ими ими и начинаются с пользователем. Они служат многим целям, включая отправку приветственных сообщений, проведение опросов или опросов, а также трансляцию уведомлений по всей организации. Проактивные сообщения Teams могут быть доставлены как **специальные, так** **и диалоговые:**

|Тип сообщения | Описание |
|----------------|-------------- |
|Специальное упреждающее сообщение| Бот вставляет сообщение, не прерывая поток разговора.|
|Упреждающее сообщение на основе Dialog | Бот создает новый диалоговый поток, берет под контроль разговор, доставляет упреждающее сообщение, закрывает и возвращает контроль к предыдущему диалогу.|

## <a name="proactive-app-installation-in-teams"></a>Проактивная установка приложений в Teams

Прежде чем ваш бот сможет активно отправить сообщение пользователю, он должен быть установлен либо в качестве личного приложения, либо в команде, в которой пользователь является участником. Иногда необходимо активно сообщения пользователям, которые не установили или ранее взаимодействовали с вашим приложением. Например, необходимость сообщения жизненно важной информации всем в вашей организации. Для таких сценариев можно использовать API Microsoft Graph для упреждающей установки бота для пользователей.

## <a name="permissions"></a>Разрешения

Разрешения Graph [группы Microsoft, в том](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) есть разрешения на установку ресурсов для всех областей пользователей (личных) или командных (каналов) в рамках Microsoft Teams платформы:

|Разрешение приложения | Описание|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|Позволяет Teams для чтения, установки, обновления и удаления себя для любого **пользователя,** без предварительного вовсяка или использования.|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|Позволяет Teams читать, устанавливать, модернизировать и удалять себя в любой **команде, без** предварительного вовсяка или использования.|

Чтобы использовать эти разрешения, необходимо добавить ключ [webApplicationInfo к манифесту](../../resources/schema/manifest-schema.md#webapplicationinfo) приложения со следующими значениями:
> [!div class="checklist"]
> [!div class="checklist"]
>
> * **ID** - идентификатор приложения Azure AD.
> * **ресурс** — URL-адрес ресурса для приложения.
>
>[!NOTE]
>
> * Ваш бот требует применения, а не пользовательских разрешений, потому что установка для других.
>
> * Администратор арендатора Azure AD [должен явно предоставлять разрешения на приложение.](/graph/security-authorization#grant-permissions-to-an-application) После получения разрешения на приложение все участники azure AD-арендатор получают предоставленные разрешения.

## <a name="enable-proactive-app-installation-and-messaging"></a>Включить проактивную установку приложений и обмен сообщениями

> [!IMPORTANT]
>Корпорация Graph может устанавливать только приложения, опубликованные в магазине приложений вашей организации или в магазине Teams магазине.

### <a name="-create-and-publish-your-proactive-messaging-bot-for-teams"></a>✔ создать и опубликовать свой упреждающий бот обмена сообщениями для Teams

Чтобы начать работу, вам нужен [бот для Teams с упреждающими](../../bots/how-to/create-a-bot-for-teams.md) [возможностями](../../concepts/bots/bot-conversations/bots-conv-proactive.md) обмена сообщениями, которые [есть в магазине приложений вашей](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-your-org) [организации или в магазине Teams магазина.](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-the-teams-store)

>[!TIP]
> Готовая к производству [**компания Communicator позволяет**](../..//samples/app-templates.md#company-communicator) транслировать сообщения и является хорошей основой для создания вашего активного приложения бота.

### <a name="-get-the-teamsappid-for-your-app"></a>✔ получите для `teamsAppId` вашего приложения

**1.** Вам нужно `teamsAppId` для следующих шагов.

Можно `teamsAppId` получить из каталога приложений вашей организации:

**Ссылка Graph microsoft на страницу:** [тип ресурса teamsApp](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)

**Запрос HTTP GET:**

```http
GET https://graph.microsoft.com/v1.0/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
```

Запрос должен вернуть `teamsApp` объект. Возвращенный объект `id` является идентификатором приложения, созданным в каталоге приложений, и отличается от идентификатора, предоставленного вами в Teams приложении:

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

**2.**  Если ваше приложение уже загружено или загружено для пользователя в личном прицеле, вы можете получить `teamsAppId` следующее:

**Ссылка Graph Microsoft: Список приложений,** [установленных для пользователя](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**Запрос HTTP GET:**

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

**3.** Если ваше приложение было загружено или загружено для канала в области команды, вы можете получить `teamsAppId` следующее:

**Ссылка Graph microsoft на странице:** [Список приложений в команде](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**Запрос HTTP GET:**

```http
GET https://graph.microsoft.com/v1.0/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

>[!TIP]
> Чтобы сузить список результатов, можно фильтровать на любом из полей [**объекта teamsApp.**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)

### <a name="-determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a>✔ определить, установлен ли ваш бот в настоящее время для получателя сообщения

**Ссылка Graph Microsoft: Список приложений,** [установленных для пользователя](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**Запрос HTTP GET:**

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

Этот запрос возвращает пустой массив, если приложение не установлено, и массив с одним [объектом teamsAppInstallation,](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) если приложение установлено.

### <a name="-install-your-app"></a>✔ Установите приложение

**Ссылка Graph microsoft на страницу:** [Установите приложение для пользователя](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**Запрос HTTP POST:**

```http
POST https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps
Content-Type: application/json

{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/v1.0/appCatalogs/teamsApps/{teamsAppId}"
}
```

Если пользователь не Microsoft Teams, установка приложения немедленно рассматривается. Для просмотра установленного приложения может потребоваться перезагрузка.

### <a name="-retrieve-the-conversation-chatid"></a>✔ Получить разговор **chatId**

Когда ваше приложение установлено для пользователя, бот получает уведомление о `conversationUpdate` [событии, которое содержит](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) необходимую информацию для отправки упреждающего сообщения.

Можно `chatId` также получить следующим образом:

**Ссылка Graph microsoft на страницу:** [Получить чат](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)

**1.** Вы должны нуждаться в вашем приложении `{teamsAppInstallationId}` . Если у вас его нет, используйте следующее:

**Запрос HTTP GET:**

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

**Идентификатором** свойства ответа является `teamsAppInstallationId` .

**2.** Сделайте следующий запрос, чтобы `chatId` получить:

**Запрос HTTP GET** (разрешение - `TeamsAppInstallation.ReadWriteSelfForUser.All` ):  

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
```

**Идентификатором** свойства ответа является `chatId` .

Вы также можете получить `chatId` следующий запрос, но он требует более широкого `Chat.Read.All` разрешения:

**Запрос HTTP GET** (разрешение - `Chat.Read.All` ):

```http
GET https://graph.microsoft.com/beta/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
```

### <a name="-send-proactive-messages"></a>✔ отправлять упреждающие сообщения

Ваш бот может [отправлять упреждающие сообщения](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) после того, как бот был добавлен для пользователя или команды и получил всю информацию о пользователе.

## <a name="see-also"></a>См. также

* [**Управление политиками настройки приложений в Microsoft Teams**](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)
* [Отправка упреждающих уведомлений пользователям SDK v4](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)

## <a name="view-additional-code-samples"></a>Просмотр дополнительных образцов кода
>
> [!div class="nextstepaction"]
> [**Teams упреждающие образцы кода обмена сообщениями**](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)