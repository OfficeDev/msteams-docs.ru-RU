---
title: Согласие на определенные ресурсы в Teams
description: Описывает согласие на конкретные ресурсы в Teams и как использовать его.
localization_priority: Normal
author: akjo
ms.author: lajanuar
ms.topic: reference
keywords: команды авторизации OAuth SSO AAD rsc Graph
ms.openlocfilehash: f364371f7763235e64da71b91db9b16b41ddf389
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/22/2021
ms.locfileid: "53068550"
---
# <a name="resource-specific-consent-rsc"></a>Согласие на определенный ресурс (RSC)

> [!NOTE]
> Согласие на доступ к области чата с конкретными ресурсами доступно только для [предварительного просмотра общедоступных](../../resources/dev-preview/developer-preview-intro.md) разработчиков.

Согласие для конкретного ресурса (RSC) — это интеграция API Microsoft Teams и Microsoft Graph, которая позволяет приложению использовать конечные точки API для управления определенными ресурсами — группами или чатами — в организации. Модель разрешений, характерных для конкретных ресурсов,  позволяет  владельцам команд и владельцам чатов предоставлять согласие приложению на доступ и(или) изменять данные группы и данные чата соответственно. Разнонакладные разрешения RSC определяют, что приложение может сделать в определенном ресурсе:

## <a name="resource-specific-permissions"></a>Разрешения, определенные для ресурсов

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

Дополнительные сведения см. в [материале Team resource-specific consent permissions.](/graph/permissions-reference#team-resource-specific-consent-permissions)

### <a name="resource-specific-permissions-for-a-chat"></a>Разрешения на доступ к ресурсам для чата
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
| OnlineMeeting.ReadBasic.Chat   | Получите основные свойства, такие как имя, расписание, организатор и ссылка на ссылку на собрание, связанное с этим чатом. |

Дополнительные сведения см. в [материале Chat resource-specific consent permissions.](/graph/permissions-reference#chat-resource-specific-consent-permissions)

>[!NOTE]
>Разрешения на использование ресурсов доступны только Teams приложениям, установленным на клиенте Teams и в настоящее время не являются частью Azure Active Directory портала.

## <a name="enable-resource-specific-consent-in-your-application"></a>Включить в приложении согласие, определенное для ресурсов

Действия для включения RSC в приложении следующие:

1. [Настройка параметров согласия на Azure Active Directory портале](#configure-consent-settings-in-the-azure-ad-portal).
    1. Настройка параметров согласия владельца группы [для RSC в команде.](#configure-group-owner-consent-settings-for-rsc-in-a-team)
    1. [Настройка параметров согласия пользователей для RSC в чате.](#configure-user-consent-settings-for-rsc-in-a-chat)
1. [Зарегистрируйте свое приложение платформа удостоверений Майкрософт с помощью портала Azure AD.](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)
1. [Просмотрите разрешения приложений на портале Azure AD.](#review-your-application-permissions-in-the-azure-ad-portal)
1. [Получение маркера доступа с платформы Microsoft Identity.](#obtain-an-access-token-from-the-microsoft-identity-platform)
1. [Обновление манифеста Teams приложения](#update-your-teams-app-manifest).
1. [Установите приложение непосредственно в Teams.](#sideload-your-app-in-teams)
1. [Проверьте приложение для дополнительных разрешений RSC](#check-your-app-for-added-rsc-permissions).
    1. [Проверьте приложение для добавленных разрешений RSC в команде.](#check-your-app-for-added-rsc-permissions-in-a-team)
    1. [Проверьте приложение для добавленных разрешений RSC в чате.](#check-your-app-for-added-rsc-permissions-in-a-chat)

## <a name="configure-consent-settings-in-the-azure-ad-portal"></a>Настройка параметров согласия на портале Azure AD

### <a name="configure-group-owner-consent-settings-for-rsc-in-a-team"></a>Настройка параметров согласия владельца группы для RSC в команде

Вы можете включить или отключить согласие владельца [группы](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal) непосредственно на портале Azure:

> [!div class="checklist"]
>
>- Во входе на [портал Azure](https://portal.azure.com) в качестве [глобального администратора или администратора компании.](/azure/active-directory/roles/permissions-reference#global-administrator&preserve-view=true)  
 > - [Выберите](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings) **Azure Active Directory**  =>  **Enterprise приложения** Consent и  =>  **permissions** User consent  =>  **settings.**
> - Включить, отключить или ограничить согласие пользователя с согласия владельца группы с меткой управления для доступа к данным **приложений** (по умолчанию разрешается согласие владельца группы для всех **владельцев групп).** Чтобы владелец группы устанавливал приложение с помощью RSC, для этого пользователя необходимо включить согласие владельца группы.

![конфигурация команды azure rsc](../../assets/images/azure-rsc-team-configuration.png)

Чтобы включить или отключить согласие владельца группы с помощью PowerShell, выполните действия, описанные в Настройка согласия владельца группы [с помощью PowerShell.](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell)

### <a name="configure-user-consent-settings-for-rsc-in-a-chat"></a>Настройка параметров согласия пользователя для RSC в чате

Вы можете включить или отключить [согласие пользователя непосредственно](/azure/active-directory/manage-apps/configure-user-consent?tabs=azure-portal) на портале Azure:

> [!div class="checklist"]
>
>- Во входе на [портал Azure](https://portal.azure.com) в качестве [глобального администратора или администратора компании.](/azure/active-directory/roles/permissions-reference#global-administrator&preserve-view=true)  
 > - [Выберите](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings) **Azure Active Directory**  =>  **Enterprise приложения** Consent и  =>  **permissions** User consent  =>  **settings.**
> - Включить, отключить или ограничить согласие пользователя с разрешением пользователя с меткой управления для приложений **(по** умолчанию разрешается согласие пользователя **для приложений).** Чтобы участник чата устанавливал приложение с помощью RSC, для этого пользователя необходимо включить согласие пользователя.

![конфигурация чата azure rsc](../../assets/images/azure-rsc-chat-configuration.png)

Чтобы включить или отключить согласие пользователя с помощью PowerShell, выполните действия, описанные в Настройка согласия пользователя [с помощью PowerShell.](/azure/active-directory/manage-apps/configure-user-consent?tabs=azure-powershell)


## <a name="register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal"></a>Регистрация приложения с помощью платформа удостоверений Майкрософт на портале Azure AD

Портал Azure Active Directory предоставляет центральную платформу для регистрации и настройки приложений. Ваше приложение должно быть зарегистрировано на портале Azure AD, чтобы интегрироваться с платформа удостоверений Майкрософт и вызвать API Graph Microsoft. Дополнительные сведения [см. в приложении Register with the платформа удостоверений Майкрософт.](/graph/auth-register-app-v2)

>[!WARNING]
>ID приложения Azure AD не должен быть общим для нескольких Teams приложений. Должно быть сопоставление 1:1 между приложением Teams и приложением Azure AD. Попытки установки нескольких Teams приложений, связанных с одинаковым ИД приложения Azure AD, приводят к сбоям установки и запуска.

## <a name="review-your-application-permissions-in-the-azure-ad-portal"></a>Просмотр разрешений приложения на портале Azure AD

Перейдите на **страницу**  =>  **регистрации домашнего приложения** и выберите приложение RSC. Выберите **разрешения API** из левой панели nav и изучите список настроенных разрешений для приложения. Если ваше приложение будет только делать вызовы API Graph RSC, удалите все разрешения на этой странице. Если ваше приложение также будет звонить не RSC, храните эти разрешения по мере необходимости.

>[!IMPORTANT]
>Портал Azure AD не может использоваться для запроса разрешений RSC. Разрешения RSC в настоящее время являются исключительными для Teams приложений, установленных в клиенте Teams и объявляются в файле манифеста Teams приложения (JSON).

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a>Получение маркера доступа из платформа удостоверений Майкрософт

Чтобы сделать Graph API, необходимо получить маркер доступа для приложения с платформы удостоверений. Прежде чем приложение сможет получить маркер из платформа удостоверений Майкрософт, его необходимо зарегистрировать на портале Azure AD. Маркер доступа содержит сведения о приложении и его разрешениях на доступ к ресурсам и API, доступным через Microsoft Graph.

Для получения маркера доступа с платформы удостоверений необходимо иметь следующие значения из процесса регистрации Azure AD:

- ID **приложения,** присвоенный порталом регистрации приложений. Если приложение поддерживает один вход (SSO), необходимо использовать тот же ID приложения для приложения и SSO.
- Секрет **клиента или пароль** или пара ключей общего и частного доступа **(сертификат).** Это необязательно для нативных приложений;
- URI **перенаправления** (или URL-адрес ответа) для вашего приложения для получения ответов из Azure AD.

 *См.* [статью Получить](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true) доступ от имени пользователя и [получить доступ без пользователя](/graph/auth-v2-service)

## <a name="update-your-teams-app-manifest"></a>Обновление манифеста Teams приложения

Разрешения RSC объявляются в файле манифеста приложения (JSON).  Добавьте ключ [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) в манифест приложения со следующими значениями:

> [!div class="checklist"]
>
> - **id**  — ваш ID приложения Azure AD. Дополнительные сведения см. в сайте [Регистрация приложения на портале Azure AD.](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)
> - **ресурс**  — любая строка. Это поле не имеет операции в RSC, но должно быть добавлено и иметь значение, чтобы избежать ответа на ошибку; любая строка будет делать.
> - **разрешения приложения** — разрешения RSC для вашего приложения. Дополнительные сведения см. [в специальном ресурсе Permissions.](resource-specific-consent.md#resource-specific-permissions)

>
>[!IMPORTANT]
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

>[!NOTE]
>Если приложение предназначено для поддержки установки в командных и чатных сферах, в одном манифесте могут быть указаны разрешения как группы, так и `applicationPermissions` чата.

## <a name="sideload-your-app-in-teams"></a>Sideload ваше приложение в Teams

Если администратор Teams позволяет настраивать загрузки приложений, [](~/concepts/deploy-and-publish/apps-upload.md) вы можете загрузить приложение непосредственно в определенную группу или чат.

## <a name="check-your-app-for-added-rsc-permissions"></a>Проверьте приложение на дополнительные разрешения RSC

>[!IMPORTANT]
>Разрешения RSC не приписываются пользователю. Вызовы сделаны с разрешениями приложения, а не с делегированием разрешений пользователя. Таким образом, приложению может быть разрешено выполнять действия, которые не могут выполняться пользователем, например удаление вкладки. Перед вызовами API RSC необходимо просмотреть намерения владельца группы или владельца чата для вашего случая использования. Дополнительные сведения [см. в Microsoft Teams API.](/graph/teams-concept-overview)

После установки приложения на ресурс можно использовать [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) для просмотра разрешений, предоставленных приложению на ресурсе:

### <a name="check-your-app-for-added-rsc-permissions-in-a-team"></a>Проверьте приложение на дополнительные разрешения RSC в команде

> [!div class="checklist"]
>
>- Получите **группуId** группы из Teams клиента.
> - В клиенте Teams выберите **Teams** из левого левого панели nav.
> - Выберите команду, в которой установлено приложение из выпадаемого меню.
> - Выберите **значок Дополнительные** параметры (&#8943;).
> - Выберите **Получить ссылку на команду**.
> - Скопируйте и сохраните **значение groupId** из строки.
> - Войдите **в Graph Explorer**.
> - Вызов **GET на** следующую конечную точку: `https://graph.microsoft.com/beta/teams/{teamGroupId}/permissionGrants` . Поле `clientAppId` в ответе будет соедино указанному в `webApplicationInfo.id` манифесте Teams приложения.
  ![Graph ответа исследователя на вызов GET для разрешений RSC группы.](../../assets/images/team-graph-permissions.png)

Сведения о том, как получить сведения о приложениях, установленных в определенной группе, см. в материале [Get the names and other details of apps installed in the specified team.](/graph/api/team-list-installedapps#example-2-get-the-names-and-other-details-of-installed-apps)

### <a name="check-your-app-for-added-rsc-permissions-in-a-chat"></a>Проверьте приложение на дополнительные разрешения RSC в чате

> [!div class="checklist"]
>
>- Получите ID потока чата из веб Teams *клиента.*
> - В веб Teams клиенте выберите **Чат из** левой панели nav.
> - Выберите чат, в котором установлено приложение из выпадаемого меню.
> - Скопируйте веб-URL-адрес и сохраните ID потока чата из строки.
![ID потока чата с веб-URL-адреса.](../../assets/images/chat-thread-id.png)
> - Войдите **в Graph Explorer**.
> - Вызов **GET на** следующую конечную точку: `https://graph.microsoft.com/beta/chats/{chatId}/permissionGrants` . Поле `clientAppId` в ответе будет соедино указанному в `webApplicationInfo.id` манифесте Teams приложения.
  ![Graph ответ обозревателя на вызов GET для разрешений RSC чата.](../../assets/images/chat-graph-permissions.png)

Сведения о том, как получить сведения о приложениях, установленных в определенном чате, см. в материале [Get the names and other details of apps installed in the specified chat.](/graph/api/chat-list-installedapps#example-2-get-the-names-and-other-details-of-apps-installed-in-the-specified-chat)

## <a name="code-sample"></a>Пример кода
| **Пример имени** | **Описание** | **.NET** |**Node.js** |
|-----------------|-----------------|----------------|----------------|
| Конкретное согласие ресурса (RSC) | Используйте RSC для вызова Graph API. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/nodeJs)|



## <a name="see-also"></a>Дополнительные материалы
 
* [Тестирование разрешений на согласие для определенных ресурсов в Teams](test-resource-specific-consent.md)
* [Согласие на определенные ресурсы в Microsoft Teams для администраторов](/MicrosoftTeams/resource-specific-consent)


