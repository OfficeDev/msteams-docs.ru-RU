---
title: Проверка разрешений согласия для конкретных ресурсов в Teams
description: Подробная информация о тестировании согласия для конкретного ресурса в Teams с использованием Postman с примерами кода
ms.localizationpriority: medium
author: akjo
ms.author: lajanuar
ms.topic: tutorial
keywords: авторизация teams OAuth SSO Microsoft Azure Active Directory (Azure AD) rsc Postman Graph
ms.openlocfilehash: d0eba34c8477c00e400e89adee7b9f09604918b7
ms.sourcegitcommit: 7bbb7caf729a00b267ceb8af7defffc91903d945
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/21/2022
ms.locfileid: "66189880"
---
# <a name="test-resource-specific-consent-permissions-in-teams"></a>Проверка разрешений согласия для конкретных ресурсов в Teams

> [!NOTE]
> Согласие для конкретного ресурса для области чата доступно только в [общедоступной предварительной версии для разработчиков](../../resources/dev-preview/developer-preview-intro.md).

Согласие для конкретного ресурса (RSC) — это интеграция Microsoft Teams и Graph API, которая позволяет приложению использовать конечные точки API для управления определенными ресурсами — командами или чатами — внутри организации. Подробнее см. в статье [Согласие для конкретного ресурса (RSC) — API Microsoft Teams Graph](resource-specific-consent.md).

## <a name="prerequisites"></a>Предварительные условия

Перед тестированием убедитесь, что вы проверили следующие изменения манифеста приложения для согласия конкретного ресурса:

<br>

<details>

<summary><b>Разрешения RSC для манифеста приложения версии 1.12 и более поздних</b></summary>

Добавьте в манифест приложения ключ [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) со следующими значениями:

|Имя| Тип | Описание|
|---|---|---|
|`id` |String |Идентификатор приложения Azure AD Подробнее см. в статье [Регистрация приложения на портале Azure AD.](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-using-the-azure-ad-portal).|
|`resource`|String| Это поле не используется в RSC, но должно быть добавлено и иметь значение, чтобы избежать ответа об ошибке; подойдет любая строка.|

Укажите разрешения, необходимые приложению.

|Имя| Тип | Описание|
|---|---|---|
|`authorization`|Object|Список разрешений, необходимых приложению для работы. Для получения дополнительных сведений см.[Авторизация](../../resources/schema/manifest-schema.md#authorization).|

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
> Если приложение предназначено для поддержки установки как для группы, так и для чата, то разрешения для группы и чата можно указать в одном манифесте в разделе `authorization`.

</details>

<br>

<details>

<summary><b>Разрешения RSC для манифеста приложения версии 1.11 и более ранних</b></summary>

Добавьте в манифест приложения ключ [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) со следующими значениями:

|Имя| Тип | Описание|
|---|---|---|
|`id` |String |Идентификатор приложения Azure AD Подробнее см. в статье [Регистрация приложения на портале Azure AD.](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-using-the-azure-ad-portal).|
|`resource`|String| Это поле не используется в RSC, но должно быть добавлено и иметь значение, чтобы избежать ответа об ошибке; подойдет любая строка.|
|`applicationPermissions`|Массив строк|Разрешения RSC для приложения. Подробнее см. в статье [Разрешения для определенных ресурсов](resource-specific-consent.md#resource-specific-permissions).|

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
> Если приложение предназначено для поддержки установки как для группы, так и для чата, то разрешения для группы и чата можно указать в одном манифесте в разделе `applicationPermissions`.

</details>

> [!IMPORTANT]
> В манифест приложения включите только разрешения RSC, которые должны быть у приложения.

> [!NOTE]
> Если приложение предназначено для доступа к API вызовам и мультимедиа, `webApplicationInfo.Id` должен быть идентификатором приложения [Azure AD службы Azure Bot](/graph/cloud-communications-get-started#register-a-bot).

## <a name="test-added-rsc-permissions-to-a-team-using-the-postman-app"></a>Протестируйте добавленные разрешения RSC для команды с помощью приложения Postman.

Чтобы проверить, соблюдаются ли разрешения RSC полезными данными запроса API, вам необходимо скопировать [тестовый код RSC JSON для команды](test-team-rsc-json-file.md) в локальную среду и обновить следующие значения:

* `azureADAppId`: : идентификатор приложения Azure AD для приложения.
* `azureADAppSecret`: пароль приложения Azure AD.
* `token_scope`: область необходима для получения токена.. Установить значение https://graph.microsoft.com/.default.
* `teamGroupId`: вы можете получить идентификатор группы команды из клиента Teams следующим образом:

    1. В клиенте Teams выберите **Teams** на крайней левой панели навигации.
    2. Из раскрывающегося меню выберите команду, в которой установлено приложение.
    3. Выберите значок **Дополнительные параметры** (&#8943;).
    4. Выберите **Получить ссылку на команду**.
    5. Скопируйте и сохраните значение **groupId** из строки.

## <a name="test-added-rsc-permissions-to-a-chat-using-the-postman-app"></a>Протестируйте добавленные разрешения RSC в чат с помощью приложения Postman.

Чтобы проверить, соблюдаются ли разрешения RSC полезными данными запроса API, вам необходимо скопировать[тестовый код RSC JSON для чатов](test-chat-rsc-json-file.md) в вашу локальную среду и обновить следующие значения:

* `azureADAppId`: : идентификатор приложения Azure AD для приложения.
* `azureADAppSecret`: пароль приложения Azure AD.
* `token_scope`: область необходима для получения токена.. Установить значение https://graph.microsoft.com/.default.
* `tenantId`: имя или идентификатор объекта Azure AD вашего клиента.
* `chatId`: : вы можете получить идентификатор потока чата из *веб-* клиента Teams следующим образом::

    1. В веб-клиенте Teams выберите **Чат** на крайней левой панели навигации.
    2. Из раскрывающегося меню выберите чат, в котором установлено приложение.
    3. Скопируйте веб-URL и сохраните идентификатор цепочки чата из строки.
![Идентификатор темы чата из веб-URL.](../../assets/images/chat-thread-id.png)

### <a name="use-postman"></a>Использование Postman

1. Откройте приложение [Postman](https://www.postman.com).
2. Выберите **Файл** > **Импорт** > **Импортировать файл**, чтобы загрузить обновленный файл JSON из вашей среды.  
3. Выберите вкладку **Коллекции**.
4. Щелкните шеврон **>** рядом с **Test RSC**, чтобы развернуть представление сведений и просмотреть запросы API.

Выполните всю коллекцию разрешений для каждого вызова API. Разрешения, которые вы указали в своем манифесте приложения, должны успешно выполняться, а те, которые не указаны, должны завершаться ошибкой с кодом состояния HTTP 403. Проверьте все коды состояния ответа, чтобы убедиться, что поведение разрешений RSC в приложении соответствует ожиданиям.

> [!NOTE]
> Чтобы протестировать определенные вызовы API DELETE и READ, добавьте эти сценарии экземпляров в файл JSON.

## <a name="test-revoked-rsc-permissions-using-postman"></a>Проверьте отозванные разрешения RSC с помощью[Postman](https://www.postman.com/)

1. Удаление приложения с определенного ресурса.
2. Следуйте инструкциям для чата или команды:
    1. [Протестируйте разрешения RSC, добавленные в команду с помощью Postman](#test-added-rsc-permissions-to-a-team-using-the-postman-app).
    2. [Протестируйте разрешения RSC, добавленные в чат с помощью Postman](#test-added-rsc-permissions-to-a-chat-using-the-postman-app).
3. Проверьте все коды состояния ответа, чтобы убедиться, что определенные вызовы API **завершились с ошибкой с кодом состояния HTTP 403**.

## <a name="see-also"></a>Дополнительные ресурсы

* [API Microsoft Graph и команды](/graph/api/resources/teams-api-overview?view=graph-rest-1.0&preserve-view=true)
* [Согласие для определенных ресурсов](~/graph-api/rsc/resource-specific-consent.md)
