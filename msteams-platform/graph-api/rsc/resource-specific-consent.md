---
title: Включение согласия для конкретного ресурса в Teams
description: Сведения о поддерживаемых детальных разрешениях на согласие для конкретного ресурса (RSC), которые позволяют владельцам команд и владельцам чатов предоставлять согласие для приложения.
ms.localizationpriority: medium
author: akjo
ms.author: lajanuar
ms.topic: reference
ms.openlocfilehash: 558ddd3603c9545781a3ebe06b7878df48b1333c
ms.sourcegitcommit: 75d0072c021609af33ce584d671f610d78b3aaef
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/28/2022
ms.locfileid: "68100891"
---
# <a name="resource-specific-consent"></a>Согласие для определенных ресурсов

> [!NOTE]
> Согласие для конкретного ресурса для области чата доступно только в [общедоступной предварительной версии для разработчиков](../../resources/dev-preview/developer-preview-intro.md).

Согласие для конкретного ресурса (RSC) — это интеграция Microsoft Teams и Microsoft Graph API, которая позволяет приложению использовать конечные точки API для управления определенными ресурсами, командами или чатами, внутри организации. Модель разрешений RSC позволяет *владельцам команд* и *владельцам чатов* давать приложению согласие на доступ и изменение данных группы и данных чата соответственно.

**Примечание:** Если с чатом связана встреча или звонок, соответствующие разрешения RSC также применяются к этим ресурсам.

## <a name="resource-specific-permissions"></a>Разрешения для определенных ресурсов

Детализированные разрешения RSC для Teams определяют, что приложение может делать в пределах определенного ресурса.

### <a name="resource-specific-permissions-for-a-team"></a>Разрешения для определенных ресурсов Teams

|Разрешение приложения| Действие |
| ----- | ----- |
|TeamSettings.Read.Group | Получить параметры этой команды.|
|TeamSettings.ReadWrite.Group|Обновить параметры этой команды|
|ChannelSettings.Read.Group|Получите имена каналов этой команды, описания каналов и настройки каналов.|
|ChannelSettings.ReadWrite.Group|Обновить имена каналов этой команды, описания каналов и настройки каналов.|
|Channel.Create.Group|Создание каналов в этой команде. |
|Channel.Delete.Group|Удаление каналов в этой команде. |
|ChannelMessage.Read.Group |Получать сообщения канала этой команды |
|TeamsAppInstallation.Read.Group|Получить список установленных приложений этой команды.|
|TeamsTab.Read.Group|Получить список вкладок этой команды|
|TeamsTab.Create.Group|Создание вкладок в этой команде. |
|TeamsTab.ReadWrite.Group|Обновление вкладок этой команды. |
|TeamsTab.Delete.Group|Удаление вкладок этой команды. |
|TeamMember.Read.Group|Получить участников этой команды |
|TeamsActivity.Send.Group|Создавайте новые уведомления в лентах активности пользователей этой команды. |

Подробности в статье [Разрешения на согласие для конкретных ресурсов группы](/graph/permissions-reference#team-resource-specific-consent-permissions).

### <a name="resource-specific-permissions-for-a-chat"></a>Разрешения для определенных ресурсов для чата

В следующей таблице представлены разрешения для чата для определенных ресурсов:

|Разрешение приложения| Действие |
| ----- | ----- |
| ChatSettings.Read.Chat         | Получить параметры этого чата                                    |
| ChatSettings.ReadWrite.Chat    | Обновить параметры этого чата                          |
| ChatMessage.Read.Chat          | Получить сообщения этого чата                                    |
| ChatMember.Read.Chat           | Получить участников этого чата                                     |
| Chat.Manage.Chat               | Управление чатом.                                             |
| TeamsTab.Read.Chat             | Получить вкладки этого чата                                        |
| TeamsTab.Create.Chat           | Создание вкладок в чате.                                     |
| TeamsTab.Delete.Chat           | Удаление вкладок чата.                                      |
| TeamsTab.ReadWrite.Chat        | Управление вкладками чата.                                      |
| TeamsAppInstallation.Read.Chat | Узнать, какие приложения установлены в этом чате.                   |
| OnlineMeeting.ReadBasic.Chat   | Чтение основных свойств, таких как имя, расписание, организатор, ссылка для присоединения и уведомления о начале/конце встречи, связанной с этим чатом. |
| Calls.AccessMedia.Chat         | Доступ к мультимедийным потокам в звонках, связанных с этим чатом или собранием.                                    |
| Calls.JoinGroupCalls.Chat         | Присоединение к звонкам, связанным с этим чатом или собранием.                                    |
| TeamsActivity.Send.Chat         | Создавайте новые уведомления в лентах активности пользователей в этом чате. |
| OnlineMeetingTranscript.Read.Chat | Прочитайте расшифровки собрания, связанного с этим чатом. |

Подробности в статье [Разрешения на согласие для конкретных ресурсов чата](/graph/permissions-reference#chat-resource-specific-consent-permissions).

> [!NOTE]
> Разрешения для конкретных ресурсов доступны только для приложений Teams, установленных на клиенте Teams, и сейчас не являются частью портала Azure Active Directory (AAD).

## <a name="enable-rsc-in-your-application"></a>Включить RSC в приложении

1. [Настройка параметров согласия](#configure-consent-settings).
    1. [Настройте параметры согласия владельца группы для RSC в команде с помощью Azure AD портала](#configure-group-owner-consent-settings-for-rsc-in-a-team-using-the-azure-ad-portal).
    1. [Настройка параметров согласия владельца чата для RSC в чате с помощью API Microsoft Graph](#configure-chat-owner-consent-settings-for-rsc-in-a-chat-using-the-microsoft-graph-apis).
1. [Зарегистрируйте приложение на платформе Microsoft Identity с помощью портала Azure AD.](#register-your-app-with-microsoft-identity-platform-using-the-azure-ad-portal).
1. [ Просмотрите разрешения приложения на портале Azure AD](#review-your-application-permissions-in-the-azure-ad-portal).
1. [Получите токен доступа от платформы идентификации.](#obtain-an-access-token-from-the-microsoft-identity-platform).
1. [Обновите манифест приложения Teams](#update-your-teams-app-manifest).
1. [Установите приложение прямо в Teams](#sideload-your-app-in-teams).
1. [Проверьте приложение на наличие добавленных разрешений RSC.](#check-your-app-for-added-rsc-permissions).
    1. [Проверьте приложение на наличие добавленных разрешений RSC в команде.](#check-your-app-for-added-rsc-permissions-in-a-team).
    1. [Проверьте приложение на наличие добавленных разрешений RSC в чате](#check-your-app-for-added-rsc-permissions-in-a-chat).

## <a name="configure-consent-settings"></a>Настройка параметров согласия

### <a name="configure-group-owner-consent-settings-for-rsc-in-a-team-using-the-azure-ad-portal"></a>Настройка параметров согласия владельца группы для RSC в команде с помощью портала Azure AD

Вы можете включить или отключить [согласие владельца группы](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal) непосредственно на портале Microsoft Azure:

1. Войдите на [Портал Azure](https://portal.azure.com) как [Глобальный администратор или администратор компании](/azure/active-directory/roles/permissions-reference#global-administrator&preserve-view=true).
1. Выберите **Azure Active Directory** > **Корпоративные приложения** > **Согласия и разрешения** > [**Параметры согласия пользователя**](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings).
1. Включайте, отключайте или ограничивайте согласие пользователя с помощью элемента управления **Согласие владельца группы на доступ приложений к данным**. По умолчанию установлено значение **Разрешить согласие владельца группы для всех владельцев группы**. Чтобы владелец группы мог установить приложение с помощью RSC, для этого пользователя должно быть включено согласие владельца группы.

    ![Конфигурация команды Azure RSC](../../assets/images/azure-rsc-team-configuration.png)

Кроме того, вы можете включить или отключить согласие владельца группы с помощью PowerShell, следуя инструкциям, описанным в разделе [Настройка согласия владельца группы с помощью PowerShell](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell).

### <a name="configure-chat-owner-consent-settings-for-rsc-in-a-chat-using-the-microsoft-graph-apis"></a>Настройка параметров согласия владельца чата для RSC в чате с помощью API Microsoft Graph

Вы можете включить или отключить RSC для чатов с помощью Graph API. Свойство в `isChatResourceSpecificConsentEnabled` [**teamsAppSettings**](/graph/api/teamsappsettings-update#example-1-enable-installation-of-apps-that-require-resource-specific-consent-in-chats-meetings) определяет, включен ли RSC чата в клиенте.

   ![Конфигурация команды RSC Graph](../../assets/images/rsc/graph-rsc-chat-configuration.png)

> Значение свойства по умолчанию **—ChatResourceSpecificConsentEnabled** зависит от того, включены или отключены параметры согласия пользователя в клиенте при первом использовании RSC для чатов.[](/azure/active-directory/manage-apps/configure-user-consent?tabs=azure-portal) Это может быть первый раз, когда a) получение [**teamsAppSettings**](/graph/api/teamsappsettings-get) или б) установка приложения Teams с разрешениями для конкретных ресурсов в чате или собрании.

## <a name="register-your-app-with-microsoft-identity-platform-using-the-azure-ad-portal"></a>Зарегистрируйте приложение на платформе Microsoft Identity с помощью портала Azure AD.

Портал Azure AD предоставляет центральную платформу для регистрации и настройки приложений. Приложение должно быть зарегистрировано на портале Azure AD для интеграции с платформой идентификации и вызова API Microsoft Graph. Подробности в разделе [Регистрация приложения на платформе идентификации](/graph/auth-register-app-v2).

> [!WARNING]
> Идентификатор приложения Azure AD не должен использоваться в нескольких приложениях Teams. Между приложением Teams и приложением Azure AD должно быть сопоставление 1:1. Попытки установить несколько приложений Teams, связанных с одним и тем же идентификатором приложения Azure AD, приведут к сбоям установки или выполнения.

## <a name="review-your-application-permissions-in-the-azure-ad-portal"></a>Проверьте разрешения приложения на портале Azure AD.

1. Перейдите на **Главную** > **страницу регистрации приложений** и выберите приложение RSC.
1. Выберите **API permissions** в левой области и пройдите по списку **Настройки разрешений** для приложения. Если приложение совершает только вызовы API Graph RSC, удалите все разрешения на этой странице. Если приложение также совершает вызовы, не относясь к RSC, оохраняйте эти разрешения по мере необходимости.

> [!IMPORTANT]
> Портал Azure AD нельзя использовать для запроса разрешений RSC. Разрешения RSC сейчас являются эксклюзивными для приложений Teams, установленных в клиенте Teams, и объявляются в файле манифеста приложения Teams (JSON).

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a>Получите токен доступа от платформы удостоверений Майкрософт.

Чтобы совершать вызовы Graph API, вы должны получить токен доступа для своего приложения на платформе идентификации. Прежде чем ваше приложение сможет получить токен с платформы удостоверений, оно должно быть зарегистрировано на портале Azure AD. Маркер доступа содержит сведения о приложении и его разрешениях на доступ к ресурсам и API, доступным через Microsoft Graph.

Чтобы получить токен доступа с платформы удостоверений, у вас должны быть следующие значения из процесса регистрации Azure AD:

* **Идентификатор приложения**, назначенный порталом регистрации приложений. Если приложение поддерживает единый вход (SSO), необходимо использовать один и тот же ИД приложения для приложения и единого вход.
* **Секрет или пароль клиента** или пара открытого или закрытого ключа, которая является **Сертификатом**. Это необязательно для нативных приложений;
* **URI перенаправления** или URL-адрес отклика для вашего приложения, чтобы получать отклики от Azure AD.

Подробности в разделе [Получение доступа от имени пользователя](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true) и [Получение доступа без пользователя](/graph/auth-v2-service).

## <a name="update-your-teams-app-manifest"></a>Обновите манифест приложения Teams

Разрешения RSC объявляются в JSON-файле манифеста приложения.

> [!IMPORTANT]
> Разрешения, отличные от RSC, хранятся на портале Azure. Не добавляйте их в манифест приложения.

### <a name="manifest-changes-for-resource-specific-consent"></a>Манифест изменений для согласия конкретного ресурса

<br>

<details>

<summary><b>Разрешения RSC для манифеста приложения версии 1.12</b></summary>

Добавьте в манифест приложения ключ [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) со следующими значениями:

|Имя| Тип | Описание|
|---|---|---|
|`id` |String |Идентификатор приложения Azure AD Подробнее см. в статье [Регистрация приложения на портале Azure AD.](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-using-the-azure-ad-portal).|
|`resource`|String| Это поле не используется в RSC, но должно быть добавлено и иметь значение, чтобы избежать ответа об ошибке; подойдет любая строка.|

Укажите разрешения, необходимые приложению.

|Имя| Тип | Описание|
|---|---|---|
|`authorization`|Object|Список разрешений, необходимых приложению для работы. Для получения дополнительной информации см. [заполнитель для авторизации ссылки в манифесте]

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
> Если приложение предназначено для поддержки установки как для группы, так и для чата, то разрешения для группы и чата можно указать в одном и том же манифесте в разделе`authorization`.

<br>

</details>

<br>

<details>

<summary><b>Разрешения RSC для манифеста приложения версии 1.11 или более ранней</b></summary>

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

> [!NOTE]
> Если приложение предназначено для поддержки установки как для группы, так и для чата, то разрешения для группы и чата можно указать в одном и том же манифесте в разделе `applicationPermissions`.

<br>

</details>

## <a name="sideload-your-app-in-teams"></a>Загрузка неопубликованного приложения в Teams

Если ваш администратор Teams разрешает загрузку пользовательских приложений, вы можете [загрузить неопубликованное приложение](~/concepts/deploy-and-publish/apps-upload.md) непосредственно в определенную команду или чат.

## <a name="check-your-app-for-added-rsc-permissions"></a>Проверьте, нет ли в приложении добавленных разрешений RSC.

> [!IMPORTANT]
> Разрешения RSC не присваиваются пользователю. Вызовы выполняются с разрешениями приложений, а не делегированными пользователями разрешениями. Приложению можно разрешить выполнять действия, недоступные пользователю, например удаление вкладки. Прежде чем совершать вызовы RSC API, вы должны проверить намерение владельца группы или владельца чата относительно вашего использования. Подробности в статье [Обзор API Microsoft Teams](/graph/teams-concept-overview).

После установки приложения в ресурс вы можете использовать [Обозреватель Graph](https://developer.microsoft.com/graph/graph-explorer) для просмотра разрешений, предоставленных приложению в ресурсе.

### <a name="check-your-app-for-added-rsc-permissions-in-a-team"></a>Проверьте, есть ли у приложения добавленные разрешения RSC в команде

1. Получите **groupId** команды из Teams.
1. В Teams выберите **Teams** на крайней левой панели.
1. Выберите команду, в которую нужно установить приложение.
1. Выберите многоточия &#x25CF;&#x25CF;&#x25CF; для этой команды.
1. Выберите **Получить ссылку на команду** в раскрывающемся меню команды.
1. Скопируйте и сохраните значение **groupId** из всплывающего диалогового окна **Получить ссылку на команду**.
1. Войдите в **Обозреватель Graph**
1. Вызовите **GET** для этой конечной точки: `https://graph.microsoft.com/beta/teams/{teamGroupId}/permissionGrants`. Поле `clientAppId` в отклике будет сопоставлено с `webApplicationInfo.id` указанным в манифесте приложения Teams.

    ![Отклик обозревателя Graph на вызов GET для разрешений команды RSC](../../assets/images/team-graph-permissions.png)

Подробнее о том, как получить сведения о приложениях, установленных в определенной группе, см. в статье [Получение имен и других сведений о приложениях, установленных в указанной группе](/graph/api/team-list-installedapps#example-2-get-the-names-and-other-details-of-installed-apps).

### <a name="check-your-app-for-added-rsc-permissions-in-a-chat"></a>Проверьте свое приложение на добавленные разрешения RSC в чате

1. Получите идентификатор потока чата из *веб*-клиента Teams.
1. В веб-клиенте Teams выберите **Чат** в крайней левой области.
1. Выберите чат, в котором установлено приложение, из выпадающего меню.
1. Скопируйте веб-URL и сохраните идентификатор цепочки чата из строки.

    ![Идентификатор темы чата из веб-URL](../../assets/images/chat-thread-id.png)

1. Войдите в **Обозреватель Graph**
1. Вызовите **GET** для следующей конечной точки: `https://graph.microsoft.com/beta/chats/{chatId}/permissionGrants`. Поле `clientAppId` в отклике будет сопоставлено с `webApplicationInfo.id` указанным в манифесте приложения Teams.

    ![Отклик обозревателя Graph на вызов GET для разрешений RSC для чата](../../assets/images/chat-graph-permissions.png)

Подробнее о том, как получить сведения о приложениях, установленных в определенном чате, см. в статье [Получение имен и других сведений о приложениях, установленных в указанном чате](/graph/api/chat-list-installedapps#example-2-get-the-names-and-other-details-of-apps-installed-in-the-specified-chat).

## <a name="code-sample"></a>Пример кода

| **Название примера** | **Описание** | **.NET** |**Node.js** |
|-----------------|-----------------|----------------|----------------|
| Согласие для определенного ресурса (RSC) | Используйте RSC для вызова API-интерфейсов Graph. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/csharp)|[Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/nodeJs)|

## <a name="see-also"></a>Дополнительные ресурсы

* [Проверка разрешений согласия для определенных ресурсов в Teams](test-resource-specific-consent.md)
* [Согласие для определенного ресурса в Microsoft Teams для администраторов](/MicrosoftTeams/resource-specific-consent)
