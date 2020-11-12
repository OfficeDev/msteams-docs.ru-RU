---
title: Согласие с определенными ресурсами в Teams
description: В этой статье описывается согласие с определенным ресурсом в Teams и его преимущества.
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: reference
keywords: Авторизация в Teams единого входа OAuth RSC Graph
ms.openlocfilehash: cbeb1069f7f80608ec3a65710543b429e6f2908b
ms.sourcegitcommit: f6029c8ff0c5315613a3efcd86777aa4cede39e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/11/2020
ms.locfileid: "48995025"
---
# <a name="resource-specific-consent-rsc"></a>Согласие с конкретным ресурсом (RSC)

>[!IMPORTANT]
> Эти API доступны в https://graph.microsoft.com/beta конечной точке.  Конечная точка [версии бета-версии](/graph/versioning-and-support#beta-version) включает API, которые в настоящее время находятся в режиме предварительной версии и еще не доступны. API в конечной точке бета-версии могут быть изменены, и их не рекомендуется использовать в рабочих приложениях. 

Согласие с конкретными ресурсами (RSC) — это интеграция Microsoft Teams и Graph API, которая позволяет приложению использовать конечные точки API для управления определенными командами в Организации. Модель разрешений согласия для определенных ресурсов (RSC) позволяет *владельцам групп* предоставлять согласие на доступ к данным приложения и/или изменять их. Детализация, зависящие от Teams, разрешения RSC определяют, что приложение может выполнять в определенной команде:

## <a name="resource-specific-permissions"></a>Разрешения для определенных ресурсов

|Разрешение приложения| Действие |
| ----- | ----- |
|TeamSettings.Read.Group | Получение параметров для этой команды.|
|TeamSettings.ReadWrite.Group|Обновление параметров для команды.|
|ChannelSettings.Read.Group|Получите имена каналов, описания каналов и параметры канала для этой команды.|
|ChannelSettings.ReadWrite.Group|Обновите имена каналов, описания каналов и параметры канала для этой команды.|
|Channel.Create.Group|Создание каналов в этой команде.|
|Channel.Delete.Group|Удаление каналов в этой команде.|
|ChannelMessage.Read.Group |Получение сообщений о каналах этой группы.|
|TeamsAppInstallation.Read.Group|Получение списка установленных приложений этой группы.|
|TeamsTab.Read.Group|Получение списка вкладок этой группы.|
|TeamsTab.Create.Group|Создание вкладок в этой команде.|
|TeamsTab.ReadWrite.Group|Обновление вкладок этой команды.|
|TeamsTab.Delete.Group|Удаление вкладок этой команды.|
|TeamMember.Read.Group|Получение сведений о членах этой группы.|

>[!NOTE]
>Разрешения, связанные с ресурсами, доступны только для приложений Teams, установленных в клиенте Teams и в настоящее время не входят в состав портала Azure Active Directory.

## <a name="enable-resource-specific-consent-in-your-application"></a>Включение согласия, зависящей от ресурса, в приложении

Ниже приведены действия по включению RSC в приложении.

1. [Настройте параметры разрешения владельца группы на портале Azure Active Directory](#configure-group-owner-consent-settings-in-the-azure-ad-portal).
1. [Зарегистрируйте свое приложение с помощью платформы удостоверений Майкрософт через портал Azure AD](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).
1. [Просмотр разрешений приложения на портале Azure AD](#review-your-application-permissions-in-the-azure-ad-portal)
1. [Получите маркер доступа от платформы идентификации Майкрософт](#obtain-an-access-token-from-the-microsoft-identity-platform).
1. [Обновите манифест приложения Teams](#update-your-teams-app-manifest).
1. [Установка приложения непосредственно в Teams](#install-your-app-directly-in-teams).
1. [Проверьте приложение на наличие добавленных разрешений RSC](#check-your-app-for-added-rsc-permissions).

## <a name="configure-group-owner-consent-settings-in-the-azure-ad-portal"></a>Настройка параметров согласия владельца группы на портале Azure AD

Вы можете включать и отключать [согласие владельца группы](/azure/active-directory/manage-apps/configure-user-consent#configure-group-owner-consent-to-apps-accessing-group-data) непосредственно на портале Azure:

> [!div class="checklist"]
>
>- Войдите на [портал Azure](https://portal.azure.com) в качестве [глобального администратора или администратора компании](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator).  
 > - [Выберите](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings) параметры разрешения пользователей для корпоративных приложений **Azure Active Directory**  =>  **Enterprise applications**  =>  **и соответствующие разрешения**  =>  **User consent settings**.
> - Разрешите, запретите или ограничьте согласие пользователя с помощью элемента управления " **согласие владельца группы" для приложений, обращающихся к данным** (по умолчанию **разрешено согласие владельца группы всем владельцам группы** ). Чтобы владелец команды установил приложение с помощью RSC, для него должно быть включено согласие владельца группы.

![Конфигурация Azure RSC](../../assets/images/azure-rsc-configuration.png)

Чтобы включить или отключить согласие владельца группы на портале Azure с помощью PowerShell, выполните действия, описанные в разделе [Настройка разрешения владельца группы с помощью PowerShell](/azure/active-directory/manage-apps/configure-user-consent#configure-group-owner-consent-using-powershell).

## <a name="register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal"></a>Регистрация приложения с помощью платформы удостоверений Майкрософт через портал Azure AD

Портал Azure Active Directory предоставляет центральную платформу для регистрации и настройки приложений. Ваше приложение должно быть зарегистрировано на портале Azure AD для интеграции с API Microsoft Identity Platform и Graph Calls. В *разделе* [Регистрация приложения с помощью платформы удостоверений Майкрософт](/graph/auth-register-app-v2).

>[!WARNING]
>Не регистрировать несколько приложений Teams в одном идентификаторе приложения Azure AD. Идентификатор приложения должен быть уникальным для каждого приложения. Попытки установить несколько приложений для одного идентификатора приложения завершатся неудачей.

## <a name="review-your-application-permissions-in-the-azure-ad-portal"></a>Просмотр разрешений приложения на портале Azure AD

Перейдите на страницу **Home**  =>  **регистрации домашнего приложения** и выберите приложение RSC. Выберите **разрешения API** в левой панели навигации и просмотрите список настроенных разрешений для вашего приложения. Если ваше приложение будет выполнять только вызовы для графа RSC, удалите все разрешения на этой странице. Если ваше приложение также сделает вызовы, не входящие в RSC,, не будут иметь соответствующих разрешений.

>[!IMPORTANT]
>Портал Azure AD не может использоваться для запроса разрешений RSC. Разрешения RSC в настоящее время являются эксклюзивными для приложений Teams, установленных в клиенте Teams, и объявляются в файле манифеста приложения (JSON).

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a>Получение маркера доступа от платформы удостоверений Майкрософт

Чтобы сделать вызовы API Graph, необходимо получить маркер доступа для приложения из платформы удостоверений. Прежде чем приложение сможет получить маркер от платформы удостоверений Майкрософт, его необходимо зарегистрировать на портале Azure AD. Маркер доступа содержит сведения о приложении и его разрешениях на доступ к ресурсам и API, доступным через Microsoft Graph.

Для получения маркера доступа от платформы удостоверений необходимо иметь следующие значения из процесса регистрации Azure AD:

- **Идентификатор приложения** , назначенный порталом регистрации приложений. Если ваше приложение поддерживает единый вход (SSO), необходимо использовать тот же идентификатор приложения для приложения и единого входа.
- **Секрет и пароль клиента** или открытый/закрытый ключ ( **сертификат** ). Это необязательно для нативных приложений;
- **URI перенаправления** (или URL-адрес ответа) для приложения на получение ответов от Azure AD.

 В *разделе* [Получение доступа от имени пользователя](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token) и [Получение доступа без пользователя](/graph/auth-v2-service)

## <a name="update-your-teams-app-manifest"></a>Обновление манифеста приложения Teams

Разрешения RSC объявляются в файле манифеста приложения (JSON).  Добавьте в манифест приложения ключ [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) со следующими значениями:

> [!div class="checklist"]
>
> - **ID**  — идентификатор приложения Azure AD. *см* . [Регистрация приложения на портале Azure AD](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).
> - **ресурс**  — любая строка. Это поле не содержит операции в RSC, но должно быть добавлено и иметь значение, чтобы избежать ошибки. выполняется любая строка.
> - **разрешения приложения** — сведения о разрешениях RSC для вашего приложения. *See* [Разрешения для определенных ресурсов](resource-specific-consent.md#resource-specific-permissions).

>
>[!IMPORTANT]
> Разрешения, отличные от RSC, хранятся на портале Azure. Не добавляйте их в манифест приложения.
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

После создания приложения вы можете [отправить пакет приложения](../../concepts/deploy-and-publish/apps-upload.md#upload-your-package-into-a-team-using-the-apps-tab) непосредственно определенной команде.  Для этого необходимо включить параметр " **Отправить настраиваемые политики приложений** " в рамках настраиваемых политик установки приложений. *Просмотрите* [Настраиваемые параметры политики приложений](/microsoftteams/teams-custom-app-policies-and-settings#custom-app-policy-and-settings).

## <a name="check-your-app-for-added-rsc-permissions"></a>Проверка приложения на наличие добавленных разрешений RSC

>[!IMPORTANT]
>Разрешения RSC не заносятся в атрибуты пользователя. Звонки выполняются с разрешениями приложения, а не делегированными разрешениями пользователя. Таким образом, приложению может быть разрешено выполнять действия, которые пользователь не может выполнить, например создание канала или удаление вкладки. Перед выполнением вызовов API RSC необходимо проанализировать назначение владельца команды для вашего варианта использования. *Ознакомьтесь* с [обзором API Microsoft Teams](/graph/teams-concept-overview).

После установки приложения в команду можно использовать [проводник диаграмм](https://developer.microsoft.com/graph/graph-explorer)  для просмотра разрешений, предоставленных приложению в команде:

> [!div class="checklist"]
>
>- Получение группы клиентов группы **из клиента** Teams.
> - В клиенте Teams выберите **Teams (Teams** ) в крайней левой панели навигации.
> - В раскрывающемся меню выберите команду, в которой установлено приложение.
> - Выберите значок **Дополнительные параметры** (&#8943;).
> - Выберите команду **получить ссылку на команду**.
> - Скопируйте и сохраните значение **groupId** из строки.
> - Войдите в **проводник Graph**.
> - Выполните вызов **Get** для следующей конечной точки: `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants` . Поле Клиентаппид в отклике будет сопоставляться с appId, указанным в манифесте приложения Teams.
  ![Ответ в проводнике Graph для получения вызова.](../../assets/images/graph-permissions.png)
 
## <a name="test-resource-specific-consent"></a>Проверка согласия, зависящей от ресурса
 
> [!div class="nextstepaction"]
> [**Проверка разрешений согласия для определенных ресурсов в Teams**](test-resource-specific-consent.md)
 
## <a name="related-topic-for-teams-administrators"></a>Раздел, посвященный администраторам Teams

> [!div class="nextstepaction"]
> [**Согласие с определенными ресурсами в Microsoft Teams для администраторов**](/MicrosoftTeams/resource-specific-consent)
> 
