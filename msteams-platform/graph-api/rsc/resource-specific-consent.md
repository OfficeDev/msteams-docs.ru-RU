---
title: Согласие для определенных ресурсов в Teams
description: В этой статье описывается согласие на определенные ресурсы в Teams и его преимущества.
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: reference
keywords: RSC-граф AAD для авторизации OAuth
ms.openlocfilehash: 97f642b203a1f7fb4cd9332b61265c0b27788e2b
ms.sourcegitcommit: 6caf503de5544fb8b9c8c6bef8eff4ff5a46068c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/17/2021
ms.locfileid: "50270800"
---
# <a name="resource-specific-consent-rsc"></a>Согласие для определенных ресурсов (RSC)

Согласие для определенных ресурсов (RSC) — это интеграция Microsoft Teams и API Microsoft Graph, которая позволяет приложению использовать конечные точки API для управления определенными командами в организации. Модель разрешений на предоставление разрешений для определенных ресурсов (RSC) позволяет владельцам команд предоставлять приложению согласие на доступ к данным команды и(или) изменение их данных.  Детализированное разрешение RSC для Teams определяет, что приложение может делать в определенной команде:

## <a name="resource-specific-permissions"></a>Разрешения для определенных ресурсов

|Разрешение приложения| Action |
| ----- | ----- |
|TeamSettings.Read.Group | Получите параметры для этой команды.|
|TeamSettings.ReadWrite.Group|Обновление параметров для команды.|
|ChannelSettings.Read.Group|Получите имена каналов, описания каналов и параметры канала для этой команды.|
|ChannelSettings.ReadWrite.Group|Обновление имен каналов, описаний каналов и параметров каналов для этой команды.|
|Channel.Create.Group|Создание каналов в этой команде.|
|Channel.Delete.Group|Удалите каналы в этой команде.|
|ChannelMessage.Read.Group |Получите сообщения канала этой команды.|
|TeamsAppInstallation.Read.Group|Получите список установленных приложений этой команды.|
|TeamsTab.Read.Group|Получите список вкладок команды.|
|TeamsTab.Create.Group|Создание вкладок в этой команде.|
|TeamsTab.ReadWrite.Group|Обновление вкладок этой команды.|
|TeamsTab.Delete.Group|Удаление вкладок этой команды.|
|TeamMember.Read.Group|Получите участников этой команды.|

>[!NOTE]
>Разрешения для определенных ресурсов доступны только приложениям Teams, установленным в клиенте Teams и в настоящее время не являются частью портала Azure Active Directory.

## <a name="enable-resource-specific-consent-in-your-application"></a>Включить согласие для определенных ресурсов в приложении

Для включения RSC в приложении выполните следующие действия.

1. [Настройка параметров согласия владельца группы на портале Azure Active Directory.](#configure-group-owner-consent-settings-in-the-azure-ad-portal)
1. [Зарегистрируйте свое приложение с помощью платформы удостоверений Майкрософт на портале Azure AD.](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)
1. [Просмотрите разрешения приложений на портале Azure AD.](#review-your-application-permissions-in-the-azure-ad-portal)
1. [Получите маркер доступа от платформы удостоверений Майкрософт.](#obtain-an-access-token-from-the-microsoft-identity-platform)
1. [Обновите манифест приложения Teams.](#update-your-teams-app-manifest)
1. [Установите приложение непосредственно в Teams.](#install-your-app-directly-in-teams)
1. [Проверьте, нет ли в приложении дополнительных разрешений RSC.](#check-your-app-for-added-rsc-permissions)

## <a name="configure-group-owner-consent-settings-in-the-azure-ad-portal"></a>Настройка параметров согласия владельца группы на портале Azure AD

Вы можете включить или отключить [согласие владельца группы](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal) непосредственно на портале Azure:

> [!div class="checklist"]
>
>- Во sign in to the [Azure portal](https://portal.azure.com) as a [Global Administrator/Company Administrator](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator).  
 > - [Выберите](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings) **для корпоративных приложений Azure Active Directory** параметры согласия пользователя и  =>    =>    =>  **разрешения.**
> - Включать, отключать или ограничивать согласие пользователя с согласия владельца группы с меткой на управление для приложений, которые имеют доступ к данным **(по** умолчанию разрешается согласие владельца группы для **всех владельцев группы).** Чтобы владелец группы устанавливал приложение с помощью RSC, для этого пользователя должно быть включено согласие владельца группы.

![Конфигурация azure rsc](../../assets/images/azure-rsc-configuration.png)

Чтобы включить или отключить согласие владельца группы с помощью PowerShell, выполните действия, описанные в описании настройки согласия владельца группы [с помощью PowerShell.](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell)

## <a name="register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal"></a>Регистрация приложения с помощью платформы удостоверений Майкрософт на портале Azure AD

Портал Azure Active Directory предоставляет центральную платформу для регистрации и настройки приложений. Ваше приложение должно быть зарегистрировано на портале Azure AD для интеграции с платформой удостоверений Майкрософт и вызова API Microsoft Graph. *См.* [статью "Регистрация приложения с помощью платформы удостоверений Майкрософт".](/graph/auth-register-app-v2)

>[!WARNING]
>Не регистрируйте несколько приложений Teams в одном и том же ИД приложения Azure AD. ИД приложения должен быть уникальным для каждого приложения. Попытки установить несколько приложений с одинаковым ид приложения не удастся.

## <a name="review-your-application-permissions-in-the-azure-ad-portal"></a>Просмотр разрешений приложения на портале Azure AD

Перейдите на **страницу**  =>  **регистрации домашнего** приложения и выберите приложение RSC. Выберите **разрешения API** на левой панели nav и изучите список настроенных разрешений для вашего приложения. Если ваше приложение будет делать только вызовы API Graph RSC, удалите все разрешения на этой странице. Если ваше приложение также будет делать вызовы без RSC, при необходимости оохраните эти разрешения.

>[!IMPORTANT]
>Портал Azure AD нельзя использовать для запроса разрешений RSC. В настоящее время разрешения RSC являются монопольными для приложений Teams, установленных в клиенте Teams, и объявляются в файле манифеста приложения (JSON).

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a>Получение маркера доступа от платформы удостоверений Майкрософт

Чтобы сделать вызовы API Graph, необходимо получить маркер доступа для приложения из платформы удостоверений. Прежде чем приложение сможет получить маркер от платформы удостоверений Майкрософт, оно должно быть зарегистрировано на портале Azure AD. Маркер доступа содержит сведения о приложении и его разрешениях на доступ к ресурсам и API, доступным через Microsoft Graph.

Для получения маркера доступа с платформы удостоверений вам потребуется получить следующие значения из процесса регистрации Azure AD:

- ИД **приложения,** присвоенный порталом регистрации приложений. Если ваше приложение поддерживает единый вход( SSO), следует использовать тот же ИД приложения для вашего приложения и SSO.
- Секрет **клиента или пароль или** пара открытых и закрытых ключей **(сертификат).** Это необязательно для нативных приложений;
- URI **перенаправления** (или URL-адрес ответа) для вашего приложения, чтобы получать ответы от Azure AD.

 *См.* ["Получить доступ от имени пользователя"](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true) и ["Получить доступ без пользователя"](/graph/auth-v2-service)

## <a name="update-your-teams-app-manifest"></a>Обновление манифеста приложения Teams

Разрешения RSC объявляются в файле манифеста приложения (JSON).  Добавьте ключ [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) в манифест приложения со следующими значениями:

> [!div class="checklist"]
>
> - **id** — ваш ид приложения Azure AD. *Зарегистрируйте* свое [приложение на портале Azure AD.](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)
> - **ресурс**  — любая строка. Это поле не имеет операции в RSC, но его необходимо добавить и иметь значение, чтобы избежать ошибки; любая строка будет делать.
> - **разрешения приложения —** RSC-разрешения для вашего приложения. *См.* ["Разрешения для определенных ресурсов".](resource-specific-consent.md#resource-specific-permissions)

>
>[!IMPORTANT]
> Не RSC-разрешения хранятся на портале Azure. Не добавляйте их в манифест приложения.
>

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

## <a name="install-your-app-directly-in-teams"></a>Установка приложения непосредственно в Teams

После создания приложения вы можете [](../../concepts/deploy-and-publish/apps-upload.md#upload-your-package-into-a-team-using-the-apps-tab) отправить пакет приложения непосредственно определенной команде.  Для этого необходимо включить **параметр** политики отправки настраиваемого приложения в рамках настраиваемой политики установки приложений. *См.* [параметры настраиваемой политики приложений.](/microsoftteams/teams-custom-app-policies-and-settings#custom-app-policy-and-settings)

## <a name="check-your-app-for-added-rsc-permissions"></a>Проверка добавленных разрешений RSC в приложении

>[!IMPORTANT]
>Разрешения RSC не связаны с пользователем. Вызовы веются с разрешениями приложения, а не делегными разрешениями пользователя. Таким образом, приложению может быть разрешено выполнять действия, которые пользователь не может выполнять, например создание канала или удаление вкладки. Перед вызовами API RSC вам следует проанализировать намерение владельца команды в отношении вашего случая использования. *См.* [обзор API Microsoft Teams.](/graph/teams-concept-overview)

После установки приложения в команде вы можете использовать [проводник Graph](https://developer.microsoft.com/graph/graph-explorer)  для просмотра разрешений, предоставленных приложению в команде:

> [!div class="checklist"]
>
>- Получите **groupId** команды из клиента Teams.
> - В клиенте Teams выберите **Teams** на левой панели.
> - Выберите команду, в которой установлено приложение, в выпадаемом меню.
> - Выберите **значок "Дополнительные параметры"** (&#8943;).
> - Выберите **"Получить ссылку на команду".**
> - Скопируйте и **сохраните значение groupId** из строки.
> - Войдите в **обозреватель Graph.**
> - Сделайте **вызов GET** для следующей конечной точки: `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants` . Поле clientAppId в отклике со картой appId, указанным в манифесте приложения Teams.
  ![Ответ обозревателя Graph на вызов GET.](../../assets/images/graph-permissions.png)

## <a name="code-sample"></a>Пример кода
| **Имя примера** | **Описание** | **C#** |
|-----------------|-----------------|----------------|
| Согласие для конкретного ресурса (RSC) | Используйте RSC для вызова API Graph. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/csharp)|

## <a name="test-resource-specific-consent"></a>Проверка согласия для определенных ресурсов
 
> [!div class="nextstepaction"]
> [**Проверка разрешений на согласие для определенных ресурсов в Teams**](test-resource-specific-consent.md)
 
## <a name="related-topic-for-teams-administrators"></a>Связанный раздел для администраторов Teams

> [!div class="nextstepaction"]
> [**Согласие администраторов в Microsoft Teams для определенных ресурсов**](/MicrosoftTeams/resource-specific-consent)
> 

