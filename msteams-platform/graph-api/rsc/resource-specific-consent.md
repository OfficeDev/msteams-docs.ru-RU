---
title: В Teams
description: Описывает согласие на конкретные ресурсы в Teams и как использовать его.
localization_priority: Normal
author: akjo
ms.author: lajanuar
ms.topic: reference
keywords: команды авторизации OAuth SSO AAD rsc Graph
ms.openlocfilehash: 4573140e33bffb0daafbdc9f929b5afd49231af8
ms.sourcegitcommit: 6e4d2c8e99426125f7b72b9640ee4a4b4f374401
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/24/2021
ms.locfileid: "53114422"
---
# <a name="resource-specific-consent"></a>Согласие для определенных ресурсов

> [!NOTE]
> Согласие на доступ к области чата с конкретными ресурсами доступно только для [предварительного просмотра общедоступных](../../resources/dev-preview/developer-preview-intro.md) разработчиков.

Согласие для конкретного ресурса (RSC) — это интеграция API Microsoft Teams и Microsoft Graph, которая позволяет приложению использовать конечные точки API для управления определенными ресурсами, группами или чатами, в организации. Модель разрешений RSC  позволяет владельцам  команд и владельцам чатов предоставлять согласие приложению на доступ и изменение данных группы и данных чата соответственно.

## <a name="resource-specific-permissions"></a>Разрешения, определенные для ресурсов

Разрешения RSC, Teams, определяют, что приложение может сделать в определенном ресурсе.

### <a name="resource-specific-permissions-for-a-team"></a>Разрешения на использование ресурсов для группы

|Разрешение приложения| Действие |
| ----- | ----- |
|TeamSettings.Read.Group | Получите параметры этой группы.|
|TeamSettings.ReadWrite.Group|Обновление параметров этой группы.|
|ChannelSettings.Read.Group|Получите имена каналов этой группы, описания каналов и параметры канала.|
|ChannelSettings.ReadWrite.Group|Обновим имена каналов этой группы, описания каналов и параметры канала.|
|Channel.Create.Group|Создание каналов в этой команде. |
|Channel.Delete.Group|Удаление каналов в этой группе. |
|ChannelMessage.Read.Group |Получите сообщения канала этой группы. |
|TeamsAppInstallation.Read.Group|Получите список установленных приложений этой группы.|
|TeamsTab.Read.Group|Получите список вкладок этой группы.|
|TeamsTab.Create.Group|Создание вкладок в этой команде. |
|TeamsTab.ReadWrite.Group|Обновление вкладок этой команды. |
|TeamsTab.Delete.Group|Удаление вкладок этой команды. |
|TeamMember.Read.Group|Получите членов этой группы. |

Дополнительные сведения см. в дополнительных сведениях о разрешениях на [согласие, определенных ресурсами группы.](/graph/permissions-reference#teams-resource-specific-consent-permissions)

### <a name="resource-specific-permissions-for-a-chat"></a>Разрешения на доступ к ресурсам для чата

В следующей таблице вы можете получить разрешения на доступ к ресурсам для чата:

|Разрешение приложения| Действие |
| ----- | ----- |
| ChatSettings.Read.Chat         | Получите параметры этого чата.                                    |
| ChatSettings.ReadWrite.Chat    | Обновление параметров этого чата.                          |
| ChatMessage.Read.Chat          | Получите сообщения этого чата.                                    |
| ChatMember.Read.Chat           | Получите участников этого чата.                                     |
| Chat.Manage.Chat               | Управление чатом.                                             |
| TeamsTab.Read.Chat             | Получите вкладки этого чата.                                        |
| TeamsTab.Create.Chat           | Создание вкладок в чате.                                     |
| TeamsTab.Delete.Chat           | Удаление вкладок чата.                                      |
| TeamsTab.ReadWrite.Chat        | Управление вкладками чата.                                      |
| TeamsAppInstallation.Read.Chat | Получите, какие приложения установлены в этом чате.                   |
| OnlineMeeting.ReadBasic.Chat   | Получите основные свойства, такие как имя, расписание, организатор и соедините ссылку на собрание, связанное с этим чатом. |

Дополнительные сведения см. в [материале Chat Resource-specific consent permissions.](/graph/permissions-reference#chat-resource-specific-consent-permissions)

> [!NOTE]
> Разрешения на использование ресурсов доступны только Teams приложениям, установленным на Teams клиенте, и в настоящее время не являются частью портала Azure Active Directory (AAD).

## <a name="enable-rsc-in-your-application"></a>Включить RSC в приложении

1. [Настройка параметров согласия на портале AAD.](#configure-consent-settings-in-the-aad-portal)
    1. Настройка параметров согласия владельца группы [для RSC в команде.](#configure-group-owner-consent-settings-for-rsc-in-a-team)
    1. [Настройка параметров согласия пользователей для RSC в чате.](#configure-user-consent-settings-for-rsc-in-a-chat)
1. [Зарегистрируйте свое приложение платформа удостоверений Майкрософт с помощью портала AAD.](#register-your-app-with-microsoft-identity-platform-using-the-aad-portal)
1. [Просмотрите разрешения приложения на портале AAD.](#review-your-application-permissions-in-the-aad-portal)
1. [Получение маркера доступа с платформы удостоверений.](#obtain-an-access-token-from-the-microsoft-identity-platform)
1. [Обновление манифеста Teams приложения](#update-your-teams-app-manifest).
1. [Установите приложение непосредственно в Teams.](#sideload-your-app-in-teams)
1. [Проверьте приложение для дополнительных разрешений RSC](#check-your-app-for-added-rsc-permissions).
    1. [Проверьте приложение для добавленных разрешений RSC в команде.](#check-your-app-for-added-rsc-permissions-in-a-team)
    1. [Проверьте приложение для добавленных разрешений RSC в чате.](#check-your-app-for-added-rsc-permissions-in-a-chat)

## <a name="configure-consent-settings-in-the-aad-portal"></a>Настройка параметров согласия на портале AAD

### <a name="configure-group-owner-consent-settings-for-rsc-in-a-team"></a>Настройка параметров согласия владельца группы для RSC в команде

Вы можете включить или отключить согласие владельца [группы](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal) непосредственно на портале Azure:

1. Во входе на портал [Azure](https://portal.azure.com) в качестве [глобального администратора или администратора компании.](/azure/active-directory/roles/permissions-reference#global-administrator&preserve-view=true)
1. Выберите **Azure Active Directory**  >  **Enterprise приложений** Согласие и  >  **разрешения** параметров согласия  >  [**пользователя.**](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings)
1. Включить, отключить или ограничить согласие пользователя с согласия владельца группы с меткой управления для **доступа к данным приложений.** По умолчанию **разрешается согласие владельца группы для всех владельцев групп.** Чтобы владелец группы устанавливал приложение с помощью RSC, для этого пользователя необходимо включить согласие владельца группы.

    ![Конфигурация команды Azure RSC](../../assets/images/azure-rsc-team-configuration.png)

Кроме того, вы можете включить или отключить согласие владельца группы с помощью PowerShell, следуйте шагам, описанным в настройке согласия владельца группы [с помощью PowerShell.](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell)

### <a name="configure-user-consent-settings-for-rsc-in-a-chat"></a>Настройка параметров согласия пользователя для RSC в чате

Вы можете включить или отключить [согласие пользователя непосредственно](/azure/active-directory/manage-apps/configure-user-consent?tabs=azure-portal) на портале Azure:

1. Во входе на портал [Azure](https://portal.azure.com) в качестве [глобального администратора или администратора компании.](/azure/active-directory/roles/permissions-reference#global-administrator&preserve-view=true)
1. Выберите **Azure Active Directory**  >  **Enterprise приложений** Согласие и  >  **разрешения** параметров согласия  >  [**пользователя.**](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings)
1. Включить, отключить или ограничить согласие пользователя с разрешением пользователя с меткой управления **для приложений.** По умолчанию **разрешается согласие пользователя для приложений.** Чтобы участник чата устанавливал приложение с помощью RSC, для этого пользователя необходимо включить согласие пользователя.

    ![Конфигурация чата Azure RSC](../../assets/images/azure-rsc-chat-configuration.png)

Кроме того, вы можете включить или отключить согласие пользователя с помощью PowerShell, следуйте шагам, описанным в настройке согласия пользователя [с помощью PowerShell.](/azure/active-directory/manage-apps/configure-user-consent?tabs=azure-powershell)

## <a name="register-your-app-with-microsoft-identity-platform-using-the-aad-portal"></a>Регистрация приложения с помощью платформа удостоверений Майкрософт с помощью портала AAD

Портал AAD предоставляет центральную платформу для регистрации и настройки приложений. Ваше приложение должно быть зарегистрировано на портале AAD для интеграции с платформой удостоверений и вызова API microsoft Graph API. Дополнительные сведения см. [в примере зарегистрировать приложение с помощью платформы удостоверений.](/graph/auth-register-app-v2)

> [!WARNING]
> ID приложения AAD не должен быть общим для нескольких Teams приложений. Должно быть сопоставление 1:1 между приложением Teams и приложением AAD. Попытки установки нескольких Teams приложений, связанных с тем же ID приложения AAD, приводят к сбоям установки или запуска.

## <a name="review-your-application-permissions-in-the-aad-portal"></a>Просмотр разрешений приложения на портале AAD

1. Перейдите на **страницу**  >  **регистрации домашнего приложения** и выберите приложение RSC.
1. Выберите **разрешения API** с левой области и перейдите по списку настроенных разрешений **для** вашего приложения. Если приложение делает вызовы API Graph RSC, удалите все разрешения на этой странице. Если ваше приложение также вызывает не RSC, храните эти разрешения по мере необходимости.

> [!IMPORTANT]
> Портал AAD не может использоваться для запроса разрешений RSC. Разрешения RSC в настоящее время являются исключительными для Teams приложений, установленных в клиенте Teams и объявляются в файле манифеста Teams приложения (JSON).

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a>Получение маркера доступа из платформа удостоверений Майкрософт

Чтобы сделать Graph API, необходимо получить маркер доступа для приложения с платформы удостоверений. Прежде чем приложение сможет получить маркер с платформы удостоверений, его необходимо зарегистрировать на портале AAD. Маркер доступа содержит сведения о приложении и его разрешениях на доступ к ресурсам и API, доступным через Microsoft Graph.

Чтобы получить маркер доступа с платформы удостоверений, необходимо иметь следующие значения из процесса регистрации AAD:

- ID **приложения,** присвоенный порталом регистрации приложений. Если приложение поддерживает один вход (SSO), необходимо использовать тот же ИД приложения для приложения и SSO.
- Секрет **клиента/пароль или** пара ключей общего или частного доступа, которая является **сертификатом.** Это необязательно для нативных приложений;
- **URL-адрес URI** перенаправления или ответ для вашего приложения для получения ответов от AAD.

Дополнительные сведения см. [в статью Получить](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true) доступ от имени пользователя и [получить доступ без пользователя.](/graph/auth-v2-service)

## <a name="update-your-teams-app-manifest"></a>Обновление манифеста Teams приложения

Разрешения RSC объявляются в файле JSON манифеста приложения. Добавьте ключ [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) в манифест приложения со следующими значениями:

|Имя| Тип | Описание|
|---|---|---|
|`id` |String |ID приложения AAD. Дополнительные сведения см. [в приложении на портале AAD.](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-using-the-aad-portal)|
|`resource`|String| Это поле не имеет операции в RSC, но должно быть добавлено и иметь значение, чтобы избежать ответа на ошибку; любая строка будет делать.|
|`applicationPermissions`|Массив строк|Разрешения RSC для вашего приложения. Дополнительные сведения см. [в ресурсных разрешениях.](resource-specific-consent.md#resource-specific-permissions)|

>
> [!IMPORTANT]
> Разрешения не RSC хранятся на портале Azure. Не добавляйте их в манифест приложения.
>

### <a name="example-for-rsc-in-a-team"></a>Пример RSC в команде

```json
"webApplicationInfo": {
    "id": "XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
    "resource": "https://RscBasedStoreApp",
    "applicationPermissions": [
      "TeamSettings.Read.Group",
      "ChannelMessage.Read.Group",
      "TeamSettings.Edit.Group",
      "ChannelSettings.ReadWrite.Group",
      "Channel.Create.Group",
      "Channel.Delete.Group",
      "TeamsApp.Read.Group",
      "TeamsTab.Read.Group",
      "TeamsTab.Create.Group",
      "TeamsTab.ReadWrite.Group",
      "TeamsTab.Delete.Group",
      "Member.Read.Group",
      "Owner.Read.Group"
    ]
  }
```

### <a name="example-for-rsc-in-a-chat"></a>Пример RSC в чате

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
      "OnlineMeeting.ReadBasic.Chat"
    ]
  }
```

> [!NOTE]
> Если приложение предназначено для поддержки установки в командных и чатных сферах, в одном манифесте могут быть указаны разрешения как группы, так и `applicationPermissions` чата.

## <a name="sideload-your-app-in-teams"></a>Sideload ваше приложение в Teams

Если администратор Teams позволяет настраивать загрузки приложений, [](~/concepts/deploy-and-publish/apps-upload.md) вы можете загрузить приложение непосредственно в определенную группу или чат.

## <a name="check-your-app-for-added-rsc-permissions"></a>Проверьте приложение на дополнительные разрешения RSC

> [!IMPORTANT]
> Разрешения RSC не приписываются пользователю. Вызовы сделаны с разрешениями приложения, а не с делегированием разрешений пользователя. Приложению может быть разрешено выполнять действия, которые пользователь не может выполнять, например удаление вкладки. Перед вызовами API RSC необходимо просмотреть намерения владельца группы или владельца чата. Дополнительные сведения [см. в Microsoft Teams API.](/graph/teams-concept-overview)

После установки приложения на ресурс можно использовать [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) для просмотра разрешений, предоставленных приложению на ресурсе.

### <a name="check-your-app-for-added-rsc-permissions-in-a-team"></a>Проверьте приложение на дополнительные разрешения RSC в команде

1. Получите **группуId** группы из Teams.
1. В Teams выберите **Teams** из левой области.
1. Выберите команду, в которой будет установлено приложение.
1. Выберите эллипсы, &#x25CF;&#x25CF;&#x25CF; для этой группы.
1. Выберите **Получить ссылку на команду** из выпадаемого меню команды.
1. Скопируйте и сохраните **значение groupId** из ссылки на диалоговое окно **всплывающее** окно группы.
1. Во входе **в Graph Explorer**.
1. Сделайте **вызов GET** в эту конечную точку: `https://graph.microsoft.com/beta/teams/{teamGroupId}/permissionGrants` . Поле `clientAppId` в ответе будет соедино указанному в `webApplicationInfo.id` манифесте Teams приложения.

    ![Graph ответа обозревателя на вызов GET для разрешений RSC группы](../../assets/images/team-graph-permissions.png)

Дополнительные сведения о том, как получить сведения о приложениях, установленных в определенной группе, см. в материале "Имена и другие сведения о приложениях, установленных в [указанной группе".](/graph/api/team-list-installedapps#example-2-get-the-names-and-other-details-of-installed-apps)

### <a name="check-your-app-for-added-rsc-permissions-in-a-chat"></a>Проверьте приложение на дополнительные разрешения RSC в чате

1. Получите ID потока чата из веб Teams *клиента.*
1. В веб Teams клиенте выберите **Чат** с левой области.
1. Выберите чат, в котором установлено приложение из выпадаемого меню.
1. Скопируйте веб-URL-адрес и сохраните ID потока чата из строки.

    ![ID потока чата с веб-URL-адреса](../../assets/images/chat-thread-id.png)

1. Во входе **в Graph Explorer**.
1. Вызов **GET на** следующую конечную точку: `https://graph.microsoft.com/beta/chats/{chatId}/permissionGrants` . Поле `clientAppId` в ответе будет соедино указанному в `webApplicationInfo.id` манифесте Teams приложения.

    ![Graph исследователя на вызов GET для разрешений RSC чата](../../assets/images/chat-graph-permissions.png)

Дополнительные сведения о том, как получить сведения о приложениях, установленных в определенном чате, см. в материале "Имена и другие сведения о приложениях, установленных в [указанном чате".](/graph/api/chat-list-installedapps#example-2-get-the-names-and-other-details-of-apps-installed-in-the-specified-chat)

## <a name="code-sample"></a>Пример кода

| **Пример имени** | **Описание** | **.NET** |**Node.js** |
|-----------------|-----------------|----------------|----------------|
| Resource-Specific согласия (RSC) | Используйте RSC для вызова Graph API. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/nodeJs)|

## <a name="see-also"></a>См. также
 
* [Тестирование разрешений на согласие для определенных ресурсов в Teams](test-resource-specific-consent.md)
* [Согласие на определенные ресурсы в Microsoft Teams для администраторов](/MicrosoftTeams/resource-specific-consent)
