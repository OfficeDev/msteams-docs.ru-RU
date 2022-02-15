---
title: Тестирование разрешений на согласие для определенных ресурсов в Teams
description: Подробные сведения о тестировании согласия на использование ресурсов в Teams с использованием Почтальон с примерами кода
ms.localizationpriority: medium
author: akjo
ms.author: lajanuar
ms.topic: tutorial
keywords: команды авторизации OAuth SSO Microsoft Azure Active Directory (Azure AD) rsc postman Graph
ms.openlocfilehash: 4e8affcc75682390f403be5b2c0ebb99029dbe19
ms.sourcegitcommit: b9af51e24c9befcf46945400789e750c34723e56
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/15/2022
ms.locfileid: "62821628"
---
# <a name="test-resource-specific-consent-permissions-in-teams"></a>Тестирование разрешений на согласие для определенных ресурсов в Teams

> [!NOTE]
> Согласие на доступ к области чата с конкретными ресурсами доступно только для [предварительного просмотра общедоступных](../../resources/dev-preview/developer-preview-intro.md) разработчиков.

Согласие на использование ресурсов — это интеграция Microsoft Teams и Graph API, которая позволяет приложению использовать конечные точки API для управления определенными ресурсами — группами или чатами — в организации. Дополнительные сведения см. [в специальном для ресурса согласии (RSC) — Microsoft Teams Graph API](resource-specific-consent.md).

## <a name="prerequisites"></a>Предварительные условия

Убедитесь, что перед тестированием убедитесь, что перед тестированием вы убедитесь в следующих изменениях манифеста приложения для согласия, определенного для ресурсов:

<br>

<details>

<summary><b>Разрешения RSC для манифеста приложения версии 1.12</b></summary>

Добавьте ключ [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) в манифест приложения со следующими значениями:

|Имя| Тип | Описание|
|---|---|---|
|`id` |String |ID приложения Azure AD. Дополнительные сведения см. в [приложении зарегистрировать на портале Azure AD](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-using-the-azure-ad-portal).|
|`resource`|Строка| Это поле не имеет операции в RSC, но должно быть добавлено и иметь значение, чтобы избежать ответа на ошибку; любая строка будет делать.|

Укажите разрешения, необходимые приложению.

|Имя| Тип | Описание|
|---|---|---|
|`authorization`|Object|Список разрешений, необходимых приложению для работы. Дополнительные сведения см. в [авторизации](../../resources/schema/manifest-schema.md#authorization).|

Пример RSC в команде

```json
"webApplicationInfo": {
    "id": "XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
    "resource": "https://RscBasedStoreApp"
    },
"authorization": {
    "permissions": {
        "resourceSpecific": [
            {
                "name": "TeamSettings.Read.Group",
                "type": "Application"
            },
            {
                "name": "TeamSettings.ReadWrite.Group",
                "type": "Application"
            },
            {
                "name": "ChannelSettings.Read.Group",
                "type": "Application"
            },
            {
                "name": "ChannelSettings.ReadWrite.Group",
                "type": "Application"
            },
            {
                "name": "Channel.Create.Group",
                "type": "Application"
            },
            {
                "name": "Channel.Delete.Group",
                "type": "Application"
            },
            {
                "name": "ChannelMessage.Read.Group",
                "type": "Application"
            },
            {
                "name": "TeamsAppInstallation.Read.Group",
                "type": "Application"
            },
            {
                "name": "TeamsTab.Read.Group",
                "type": "Application"
            },
            {
                "name": "TeamsTab.Create.Group",
                "type": "Application"
            },
            {
                "name": "TeamsTab.ReadWrite.Group",
                "type": "Application"
            },
            {
                "name": "TeamsTab.Delete.Group",
                "type": "Application"
            },
            {
                "name": "TeamMember.Read.Group",
                "type": "Application"
            },
            {
                "name": "TeamsActivity.Send.Group",
                "type": "Application"
            }
        ]    
    }
}
```

Пример RSC в чате

```json
"webApplicationInfo": {
    "id": "XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
    "resource": "https://RscBasedStoreApp"
    },
"authorization": {
    "permissions": {
        "resourceSpecific": [
            {
                "name": "ChatSettings.Read.Chat",
                "type": "Application"
            },
            {
                "name": "ChatSettings.ReadWrite.Chat",
                "type": "Application"
            },
            {
                "name": "ChatMessage.Read.Chat",
                "type": "Application"
            },
            {
                "name": "ChatMember.Read.Chat",
                "type": "Application"
            },
            {
                "name": "Chat.Manage.Chat",
                "type": "Application"
            },
            {
                "name": "TeamsTab.Read.Chat",
                "type": "Application"
            },
            {
                "name": "TeamsTab.Create.Chat",
                "type": "Application"
            },
            {
                "name": "TeamsTab.Delete.Chat",
                "type": "Application"
            },
            {
                "name": "TeamsTab.ReadWrite.Chat",
                "type": "Application"
            },
            {
                "name": "TeamsAppInstallation.Read.Chat",
                "type": "Application"
            },
            {
                "name": "OnlineMeeting.ReadBasic.Chat",
                "type": "Application"
            },
            {
                "name": "Calls.AccessMedia.Chat",
                "type": "Application"
            },
            {
                "name": "Calls.JoinGroupCalls.Chat",
                "type": "Application"
            },
            {
                "name": "TeamsActivity.Send.Chat",
                "type": "Application"
            }
        ]    
    }
}
```
    
> [!NOTE]
> Если приложение предназначено для поддержки установки в командных и чатных сферах, в одном манифесте могут быть указаны разрешения как группы, так и чата `authorization`.

</details>

<br>

<details>

<summary><b>Разрешения RSC для манифеста приложения версии 1.11 или более ранней версии</b></summary>

Добавьте ключ [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) в манифест приложения со следующими значениями:

|Имя| Тип | Описание|
|---|---|---|
|`id` |String |ID приложения Azure AD. Дополнительные сведения см. в [приложении зарегистрировать на портале Azure AD](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-using-the-azure-ad-portal).|
|`resource`|Строка| Это поле не имеет операции в RSC, но должно быть добавлено и иметь значение, чтобы избежать ответа на ошибку; любая строка будет делать.|
|`applicationPermissions`|Массив строк|Разрешения RSC для вашего приложения. Дополнительные сведения см. [в дополнительных сведениях о разрешениях, определенных для ресурсов](resource-specific-consent.md#resource-specific-permissions).|

Пример RSC в команде

```json
"webApplicationInfo": {
    "id": "XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
    "resource": "https://RscBasedStoreApp",
    "applicationPermissions": [
        "TeamSettings.Read.Group",
        "TeamSettings.ReadWrite.Group",
        "ChannelSettings.Read.Group",
        "ChannelSettings.ReadWrite.Group",
        "Channel.Create.Group",
        "Channel.Delete.Group",
        "ChannelMessage.Read.Group",
        "TeamsAppInstallation.Read.Group",
        "TeamsTab.Read.Group",
        "TeamsTab.Create.Group",
        "TeamsTab.ReadWrite.Group",
        "TeamsTab.Delete.Group",
        "TeamMember.Read.Group",
        "TeamsActivity.Send.Group"
    ]
  }
```

Пример RSC в чате

```json
"webApplicationInfo": {
    "id": "XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
    "resource": "https://RscBasedStoreApp",
    "applicationPermissions": [
        "ChatSettings.Read.Chat",
        "ChatSettings.ReadWrite.Chat",
        "ChatMessage.Read.Chat",
        "ChatMember.Read.Chat",
        "Chat.Manage.Chat",
        "TeamsTab.Read.Chat",
        "TeamsTab.Create.Chat",
        "TeamsTab.Delete.Chat",
        "TeamsTab.ReadWrite.Chat",
        "TeamsAppInstallation.Read.Chat",
        "OnlineMeeting.ReadBasic.Chat",
        "Calls.AccessMedia.Chat",
        "Calls.JoinGroupCalls.Chat",
        "TeamsActivity.Send.Chat"
    ]
  }
```

<br>

> [!NOTE]
> Если приложение предназначено для поддержки установки в командных и чатных сферах, в одном манифесте могут быть указаны разрешения как группы, так и чата `applicationPermissions`.
    
</details>

> [!IMPORTANT]
> В манифесте приложения включите только разрешения RSC, которые необходимо иметь вашему приложению.

> [!NOTE]
> Если приложение предназначено для доступа к API вызовов и мультимедиа, `webApplicationInfo.Id` то должен быть ИД приложения Azure AD [службы Azure Bot](/graph/cloud-communications-get-started#register-a-bot).

## <a name="test-added-rsc-permissions-to-a-team-using-the-postman-app"></a>Test added RSC permissions to a team using the Postman app

Чтобы проверить, чтят ли разрешения RSC полезной нагрузкой запроса API, необходимо скопировать тестовый код [RSC JSON](test-team-rsc-json-file.md) для группы в локальной среде и обновить следующие значения:

* `azureADAppId`: ID приложения Azure AD в вашем приложении.
* `azureADAppSecret`Пароль приложения Azure AD.
* `token_scope`. Область требуется для получения маркера. установите значение https://graph.microsoft.com/.default.
* `teamGroupId`: Вы можете получить id группы группы от клиента Teams следующим образом:

    1. В клиенте Teams **выберите Teams из** левой панели навигации.
    2. Выберите команду, в которой установлено приложение из отсевного меню.
    3. Выберите **значок Дополнительные** параметры (&#8943;).
    4. Выберите **Получить ссылку на команду**. 
    5. Скопируйте и сохраните **значение groupId** из строки.

## <a name="test-added-rsc-permissions-to-a-chat-using-the-postman-app"></a>Test added RSC permissions to a chat using the Postman app

Чтобы проверить, чтят ли разрешения RSC полезной нагрузкой запроса API, необходимо скопировать тестовый код [RSC JSON](test-chat-rsc-json-file.md) для чатов в локальной среде и обновить следующие значения:

* `azureADAppId`: ID приложения Azure AD в вашем приложении.
* `azureADAppSecret`Пароль приложения Azure AD.
* `token_scope`. Область требуется для получения маркера. установите значение https://graph.microsoft.com/.default.
* `tenantId`: Имя или ID объекта Azure AD клиента.
* `chatId`: Вы можете получить id потока чата из Teams *веб-клиента* следующим образом:

    1. В веб Teams клиенте выберите **Чат из** левой панели навигации.
    2. Выберите чат, в котором установлено приложение из меню отсев.
    3. Скопируйте веб-URL-адрес и сохраните id потока чата из строки.
![ID потока чата с веб-URL-адреса.](../../assets/images/chat-thread-id.png)

### <a name="use-postman"></a>Использование Postman

1. Откройте [приложение Postman](https://www.postman.com) .
2. Выберите **файл** **FileImportImport** >  > **,** чтобы загрузить обновленный JSON-файл из среды.  
3. Выберите **вкладку Collections** . 
4. Выберите шеврон **>** рядом с **тестом RSC** , чтобы расширить представление сведений и просмотреть запросы API.

Выполните всю коллекцию разрешений для каждого вызова API. Разрешения, указанные в манифесте приложения, должны быть успешными, а те, которые не указаны, должны не работать с кодом состояния HTTP 403. Проверьте все коды состояния отклика, чтобы подтвердить, что поведение разрешений RSC в вашем приложении соответствует ожиданиям.

> [!NOTE]
> Чтобы протестировать конкретные вызовы DELETE и READ API, добавьте эти сценарии экземпляров в файл JSON.

## <a name="test-revoked-rsc-permissions-using-postman"></a>Тестирование отозванных разрешений RSC с помощью [Postman](https://www.postman.com/)

1. Удалить приложение из определенного ресурса.
2. Выполните действия для чата или группы: 
    1. [Тест добавил разрешения RSC в команду с помощью Postman](#test-added-rsc-permissions-to-a-team-using-the-postman-app).
    2. [Test added RSC permissions to a chat using Postman](#test-added-rsc-permissions-to-a-chat-using-the-postman-app).
3. Проверьте все коды состояния отклика, чтобы подтвердить, что конкретные вызовы API сбой с **кодом состояния HTTP 403**.

## <a name="see-also"></a>См. также

* [Microsoft Graph API и Teams](/graph/api/resources/teams-api-overview?view=graph-rest-1.0&preserve-view=true)
* [Согласие для определенных ресурсов](~/graph-api/rsc/resource-specific-consent.md)
