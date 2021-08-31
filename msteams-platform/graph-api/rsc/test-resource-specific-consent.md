---
title: Тестирование разрешений на согласие для определенных ресурсов в Teams
description: Подробные сведения о тестировании согласия на использование ресурсов в Teams с помощью Postman
localization_priority: Normal
author: akjo
ms.author: lajanuar
ms.topic: tutorial
keywords: команды авторизации OAuth SSO AAD rsc postman Graph
ms.openlocfilehash: 629d798e600a3a9a9ba1cbd7fd75bdc8de13a507
ms.sourcegitcommit: 95e0c767ca0f2a51c4a7ca87700ce50b7b154b7c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/25/2021
ms.locfileid: "58528945"
---
# <a name="test-resource-specific-consent-permissions-in-teams"></a>Тестирование разрешений на согласие для определенных ресурсов в Teams

> [!NOTE]
> Согласие на доступ к области чата с конкретными ресурсами доступно только для [предварительного просмотра общедоступных](../../resources/dev-preview/developer-preview-intro.md) разработчиков.

Согласие на использование ресурсов — это интеграция Microsoft Teams и Graph API, которая позволяет приложению использовать конечные точки API для управления определенными ресурсами — группами или чатами — в организации. Дополнительные сведения см. в [специальном для ресурса согласии (RSC) — Microsoft Teams Graph API.](resource-specific-consent.md)

> [!NOTE]
> Чтобы проверить разрешения RSC, Teams манифест приложения должен включать ключ **webApplicationInfo,** населённый следующими полями:
>
> - **id.** ID приложения Azure AD см. в приложении [Register your app in the Azure AD portal](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-using-the-aad-portal).
> - **ресурс**. Любая строка, см. примечание в [обновлении манифеста Teams приложения](resource-specific-consent.md#update-your-teams-app-manifest).
> - **Разрешения приложения:** разрешения RSC для вашего приложения см. в [приложении Resource-specific Permissions.](resource-specific-consent.md#resource-specific-permissions)

## <a name="example-for-a-team"></a>Пример для группы
```json
"webApplicationInfo":{
    "id":"XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
    "resource":"https://AnyString",
    "applicationPermissions":[
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
        "TeamMember.Read.Group"
    ]
   }
```

## <a name="example-for-a-chat"></a>Пример для чата
```json
"webApplicationInfo":{
    "id":"XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
    "resource":"https://AnyString",
    "applicationPermissions":[
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
        "Calls.JoinGroupCalls.Chat"
    ]
   }
```

> [!IMPORTANT]
> В манифесте приложения включите только разрешения RSC, которые необходимо иметь вашему приложению.

>[!NOTE]
>Если приложение предназначено для поддержки установки в командных и чатных сферах, в одном манифесте могут быть указаны разрешения как группы, так и `applicationPermissions` чата.

>Если приложение предназначено для доступа к API вызовов и мультимедиа, то должен быть `webApplicationInfo.Id` AAD-Id приложения [службы Azure Bot.](/graph/cloud-communications-get-started#register-a-bot)

## <a name="test-added-rsc-permissions-to-a-team-using-the-postman-app"></a>Test added RSC permissions to a team using the Postman app

Чтобы проверить, чтят ли разрешения RSC полезной нагрузкой запроса API, необходимо скопировать тестовый код [RSC JSON](test-team-rsc-json-file.md) для группы в локальной среде и обновить следующие значения:

* `azureADAppId`: ID приложения Azure AD в вашем приложении.
* `azureADAppSecret`Пароль приложения Azure AD.
* `token_scope`. Область требуется для получения маркера. установите значение https://graph.microsoft.com/.default .
* `teamGroupId`: Вы можете получить id группы группы от клиента Teams следующим образом:

    1. В клиенте Teams выберите **Teams** из левой панели навигации.
    2. Выберите команду, в которой установлено приложение из отсевного меню.
    3. Выберите **значок Дополнительные** параметры (&#8943;).
    4. Выберите **Получить ссылку на команду**. 
    5. Скопируйте и сохраните **значение groupId** из строки.

## <a name="test-added-rsc-permissions-to-a-chat-using-the-postman-app"></a>Test added RSC permissions to a chat using the Postman app

Чтобы проверить, чтят ли разрешения RSC полезной нагрузкой запроса API, необходимо скопировать тестовый код [RSC JSON](test-chat-rsc-json-file.md) для чатов в локальной среде и обновить следующие значения:

* `azureADAppId`: ID приложения Azure AD в вашем приложении.
* `azureADAppSecret`Пароль приложения Azure AD.
* `token_scope`. Область требуется для получения маркера. установите значение https://graph.microsoft.com/.default .
* `tenantId`: Имя или ID объекта AAD клиента.
* `chatId`: Вы можете получить id потока чата из Teams *веб-клиента* следующим образом:

    1. В веб Teams клиенте выберите **Чат из** левой панели навигации.
    2. Выберите чат, в котором установлено приложение из меню отсев.
    3. Скопируйте веб-URL-адрес и сохраните id потока чата из строки.
![ID потока чата с веб-URL-адреса.](../../assets/images/chat-thread-id.png)

### <a name="use-postman"></a>Использование Postman

1. Откройте [приложение Postman.](https://www.postman.com)
2. Выберите **файл импорта**  >    >  **файлов,** чтобы загрузить обновленный JSON-файл из среды.  
3. Выберите **вкладку Collections.** 
4. Выберите шеврон **>** рядом с **тестом RSC,** чтобы расширить представление сведений и просмотреть запросы API.

Выполните всю коллекцию разрешений для каждого вызова API. Разрешения, указанные в манифесте приложения, должны быть успешными, а те, которые не указаны, должны не работать с кодом состояния HTTP 403. Проверьте все коды состояния отклика, чтобы подтвердить, что поведение разрешений RSC в вашем приложении соответствует ожиданиям.

> [!NOTE]
> Чтобы протестировать конкретные вызовы DELETE и READ API, добавьте эти сценарии экземпляров в файл JSON.

## <a name="test-revoked-rsc-permissions-using-postman"></a>Тестирование отозванных разрешений RSC с помощью [Postman](https://www.postman.com/)

1. Удалить приложение из определенного ресурса.
2. Выполните действия для чата или группы: 
    1. [Test added RSC permissions to a team using Postman.](#test-added-rsc-permissions-to-a-team-using-the-postman-app)
    2. [Test added RSC permissions to a chat using Postman.](#test-added-rsc-permissions-to-a-chat-using-the-postman-app)
3. Проверьте все коды состояния отклика, чтобы подтвердить, что конкретные вызовы API сбой с **кодом состояния HTTP 403**.

## <a name="see-also"></a>См. также

[Microsoft Graph API и Teams](/graph/api/resources/teams-api-overview?view=graph-rest-1.0&preserve-view=true)

