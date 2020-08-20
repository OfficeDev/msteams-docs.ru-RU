---
title: Согласие на ресурсы в Teams
description: Описание согласия на ресурсы в Teams и способы его использования.
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: Teams Authorization OAuth SSO AAD rsc Graph
ms.openlocfilehash: 7e3fc3faa111f4ba982c1c79e6b5b873b8773aef
ms.sourcegitcommit: 9fd61042e8be513c2b2bd8a33ab5e9e6498d65c5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/20/2020
ms.locfileid: "46819184"
---
# <a name="resource-specific-consent-rsc"></a>Согласие на ресурсы (RSC)

>[!IMPORTANT]
> Эти API доступны в конечной https://graph.microsoft.com/beta точке.  Конечная [точка версии бета-версии](/graph/versioning-and-support#beta-version) включает API-интерфейсы, которые в настоящий момент находятся в предварительной версии и не являются общедоступными. API-интерфейсы в конечной точке бета-версий могут меняться, и мы не рекомендуем использовать их в рабочих приложениях. 

Согласие на ресурсы (RSC) — это интеграция API Microsoft Teams и Graph, позволяющая приложению использовать конечные точки API для управления определенными командами в организации. Модель разрешений RSC позволяет владельцам *группы* дать приложению разрешение на доступ к его данным и/или изменение. Детальные разрешения RSC для Teams определяют возможности приложения в конкретной команде:

## <a name="resource-specific-permissions"></a>Разрешения для конкретных ресурсов

|Разрешение приложения| Действие |
| ----- | ----- |
|TeamSettings.Read.Group | Получение параметров для команды.|
|TeamSettings.Edit.Group|Обновите параметры для этой команды.|
|ChannelSettings.Read.Group|Получение имен каналов, описаний каналов и параметров каналов для этой команды.|
|ChannelSettings.ReadWrite.Group|Обновите имена каналов, описания каналов и параметры каналов для этой команды.|
|Channel.Create.Group|Создание каналов в этой команде.|
|Channel.Delete.Group|Удаление каналов в команде.|
|ChannelMessage.Read.Group |Получение сообщений канала этой команды.|
|TeamsApp.Read.Group|Получение списка установленных приложений этой команды.|
|TeamsTab.Read.Group|Получение списка вкладок этой группы.|
|TeamsTab.Create.Group|Создание вкладок в этой команде.|
|TeamsTab.ReadWrite.Group|Обновляйте вкладки этой команды.|
|TeamsTab.Delete.Group|Удаление вкладок этой команды.|
|Member.Read.Group|Получение участников команды.|
|Owner.Read.Group|Получение владельцев команды.|

>[!NOTE]
>Разрешения для конкретных ресурсов доступны только приложениям Teams, установленным в клиенте Teams и в настоящее время не являются частью портала Azure Active Directory.

## <a name="enable-resource-specific-consent-in-your-application"></a>Включение согласия для ресурсов в приложении

Для включения RSC в приложении выполните следующие действия.

1. [Настройте параметры согласия владельца группы на портале Azure Active Directory.](#configure-group-owner-consent-settings-in-the-azure-ad-portal)
1. [Регистрация приложения с помощью платформы удостоверений Майкрософт на портале Azure AD.](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)
1. [Проверьте разрешения приложений на портале Azure AD](#review-your-application-permissions-in-the-azure-ad-portal)
1. [Получите маркер доступа с платформы удостоверений Майкрософт.](#obtain-an-access-token-from-the-microsoft-identity-platform)
1. [Обновите манифест приложения Teams.](#update-your-teams-app-manifest)
1. [Установите приложение непосредственно в Teams.](#install-your-app-directly-in-teams)
1. [Проверьте, как в вашем приложении предоставлены разрешения, предоставленные для RSC-каналов.](#check-your-app-for-added-rsc-permissions)

## <a name="configure-group-owner-consent-settings-in-the-azure-ad-portal"></a>Настройка параметров согласия владельца группы на портале Azure AD

Вы можете включать и  [отключать согласие](/azure/active-directory/manage-apps/configure-user-consent#configure-group-owner-consent-to-apps-accessing-group-data) владельцев группы непосредственно на портале Azure:

> [!div class="checklist"]
>
>- Войдите на портал [Azure под учетной](https://portal.azure.com) [записью глобального администратора или администратора организации.](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator)  
 > - Выберите **параметры пользователя для**  => **корпоративных приложений**Azure Active  => **User settings**Directory.
> - Разрешать, отключать или ограничивать согласие пользователя с помощью контролировщика "Пользователи могут разрешать" доступ к приложениям **для принадлежащих им групп** (эта возможность включена по умолчанию).

![Конфигурация azure rsc](../../assets/images/azure-rsc-configuration.svg)

| Значение | Описание|
|--- | --- |
|Да | Включение согласия для группы для всех владельцев групп.|
|Нет |Отключите согласие для группы для всех пользователей.| 
|Ограничено | Включение согласия для групп для участников выбранной группы.|

Чтобы включить или отключить согласие владельца группы на портале Azure с помощью PowerShell, выполните действия, описанные в разделе ["Настройка согласия владельца группы с помощью PowerShell".](/azure/active-directory/manage-apps/configure-user-consent#configure-group-owner-consent-using-powershell)

## <a name="register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal"></a>Регистрация приложения на платформе удостоверений Майкрософт на портале Azure AD

Портал Azure Active Directory представляет собой центральную платформу для регистрации и настройки приложений. Ваше приложение должно быть зарегистрировано на портале Azure AD, чтобы интегрироватьегоего его с платформой удостоверений Майкрософт и вызывать API Graph. *См.* [раздел "Регистрация приложения с помощью платформы удостоверений Майкрософт".](/graph/auth-register-app-v2)

>[!WARNING]
>Не регистрируйте несколько приложений Teams с одинаковым идентификатором приложения Azure AD. Идентификатор приложения должен быть уникальным для каждого приложения. Попытки установить несколько приложений с один и тем же идентификатором приложения завершится ошибкой.

## <a name="review-your-application-permissions-in-the-azure-ad-portal"></a>Проверьте разрешения приложений на портале Azure AD

Перейдите на **страницу**  =>  **регистрации домашнего приложения** и выберите свое RSC-приложение. Выберите **разрешения API** из левой панели навигации и проверьте список настроенных разрешений для приложения. Если ваше приложение будет выполнять только вызовы RSC Graph, удалите все разрешения на этой странице. Если ваше приложение также будет выполнять вызовы, не использующие поддержку RSC, не забудьте эти разрешения по мере необходимости.

>[!IMPORTANT]
>Невозможно использовать портал Azure AD для запроса разрешений RSC. Разрешения RSC в настоящее время используются только для приложений Teams, установленных в клиенте Teams и объявляются в файле манифеста приложения (JSON).

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a>Получите маркер доступа от платформы удостоверений Майкрософт

Для вызова API Graph необходимо получить маркер доступа для приложения с платформы идентификации. Чтобы приложение сможет получить маркер от платформы удостоверений Майкрософт, оно должно быть зарегистрировано на портале Azure AD. Маркер доступа содержит сведения о приложении и его разрешениях на доступ к ресурсам и API, доступным через Microsoft Graph.

Вам потребуются следующие значения из процесса регистрации Azure AD, чтобы получать маркер доступа из платформы удостоверений.

- Идентификатор **приложения,** назначенный порталом регистрации. Если ваше приложение поддерживает единый вход, следует использовать для приложения и единого входа один и тот же идентификатор приложения.
- **Секрет/пароль клиента** либо открытый и закрытый ключ (**сертификат).** Это необязательно для нативных приложений;
- **URI перенаправления** (или URL-адрес ответа), с помощью которого приложение будет получать отклики от Azure AD.

 *Просмотр* [сведений о доступе от имени пользователя и](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token) получение [доступа без пользователя](/graph/auth-v2-service)

## <a name="update-your-teams-app-manifest"></a>Обновление манифеста приложения Teams

Разрешения RSC объявляются в файле манифеста приложения (JSON).  Добавьте [ключ webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) в манифест приложения со следующими значениями:

> [!div class="checklist"]
>
> - **id** — идентификатор приложения Azure AD. *См.* ["Регистрация приложения" на портале Azure AD.](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)
> - **resource —**  любая строка. Это поле не имеет операций в RSC, но его необходимо добавить и значение, чтобы избежать отклика с ошибкой; любая строка выполнит это.
> - **разрешения приложений** — разрешения RSC для вашего приложения. *См.* [разрешения для конкретных ресурсов.](resource-specific-consent.md#resource-specific-permissions)

>
>[!IMPORTANT]
> Разрешения, не относящиеся к RSC, хранятся на портале Azure. Не добавляйте их в манифест приложения.
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

## <a name="install-your-app-directly-in-teams"></a>Установка приложения непосредственно в Microsoft Teams

После создания приложения можно отправить пакет [приложения непосредственно](../../concepts/deploy-and-publish/apps-upload.md#upload-your-package-into-a-team-using-the-apps-tab) определенной команде.  Для этого параметр **политики "Отправить пользовательские приложения"** должен быть включен в рамках настраиваемых политик настройки приложений. *См.* ["Настраиваемые параметры политики приложений".](/microsoftteams/teams-custom-app-policies-and-settings#custom-app-policy-and-settings)

## <a name="check-your-app-for-added-rsc-permissions"></a>Проверьте добавляемые разрешения для RSC в приложении

>[!IMPORTANT]
>Разрешения RSC не обращаются к пользователю. Вызовы касаются разрешений приложения, а не делегированных пользователем разрешений. Поэтому приложению может быть разрешено выполнять действия, которые не могут выполняться пользователю (например, создать канал или удалять вкладку). Перед вызовами API RSC следует просмотреть намерения владельца команды об вашем варианте использования. *Ознакомьтесь* [с обзором API Microsoft Teams.](/graph/teams-concept-overview)

После установки приложения в команде вы можете просматривать разрешения, предоставленные приложению в команде, с помощью песочницы [Graph.](https://developer.microsoft.com/graph/graph-explorer)

> [!div class="checklist"]
>
>- Получение идентификатора **группы команды** из клиента Teams.
> - В клиенте Teams выберите **Teams** на левой левой панели навигации.
> - Выберите команду, в которой устанавливается приложение, из раскрывающегося меню.
> - Щелкните **значок "Дополнительные** параметры" (&#8943;).
> - Выберите **"Получить ссылку на команду".**
> - Скопируйте и **сохраните значение groupId** из строки.
> - Войдите в **песочницу Graph.**
> - Выполните **вызов GET** к следующей конечной точке: `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants` Поле clientAppId в ответе будет сопоставлено с appId, указанным в манифесте приложения Teams.
  ![Ответ песочницы graph на вызов GET.](../../assets/images/graph-permissions.png)
 
## <a name="test-resource-specific-consent"></a>Проверка согласия для ресурса
 
> [!div class="nextstepaction"]
> [**Тестирование разрешений на согласие для конкретных ресурсов в Teams**](test-resource-specific-consent.md)
 
## <a name="related-topic-for-teams-administrators"></a>Статья по теме для администраторов Teams

> [!div class="nextstepaction"]
> [**Для администраторов согласие на ресурсы в Microsoft Teams**](/MicrosoftTeams/resource-specific-consent)
> 
