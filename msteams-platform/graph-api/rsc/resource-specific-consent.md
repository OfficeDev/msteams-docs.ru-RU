---
title: Согласие на конкретные ресурсы в Teams
description: Описывает согласие, специфичное для Teams и как им воспользоваться.
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: reference
keywords: команды авторизации OAuth SSO AAD rsc Graph
ms.openlocfilehash: dabe0c33013fbb398eee7bf00ac2881cd86e6bc5
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566135"
---
# <a name="resource-specific-consent-rsc"></a>Согласие на конкретные ресурсы (RSC)

Согласие с конкретными ресурсами (RSC) — это интеграция Microsoft Teams и Microsoft Graph API, которая позволяет приложению использовать конечные точки API для управления определенными группами в организации. Модель разрешений на согласие с конкретными  ресурсами (RSC) позволяет владельцам групп дать согласие на получение заявки на доступ и/или изменение данных группы. Детальные, Teams RSC определяют, что приложение может сделать в рамках конкретной группы:

## <a name="resource-specific-permissions"></a>Разрешения, специфичные для ресурсов

|Разрешение приложения| Действие |
| ----- | ----- |
|TeamSettings.Read.Group | Получите настройки для этой команды.|
|TeamSettings.ReadWrite.Group|Обновление параметров для команды.|
|ChannelSettings.Read.Group|Получите имена каналов, описания каналов и настройки каналов для этой команды.|
|ChannelSettings.ReadWrite.Group|Обновление имен каналов, описаний каналов и настроек каналов для этой команды.|
|Channel.Create.Group|Создание каналов в этой команде.|
|Channel.Delete.Group|Удалить каналы в этой команде.|
|ChannelMessage.Read.Group |Получите сообщения канала этой команды.|
|TeamsAppInstallation.Read.Group|Получить список установленных приложений этой команды.|
|TeamsTab.Read.Group|Получить список вкладок этой команды.|
|TeamsTab.Create.Group|Создание вкладок в этой команде.|
|TeamsTab.ReadWrite.Group|Обновление вкладок этой команды.|
|TeamsTab.Delete.Group|Удаление вкладок этой команды.|
|TeamMember.Read.Group|Возьми членов этой команды.|

>[!NOTE]
>Разрешения на использование ресурсов доступны только для Teams, установленных на Teams и в настоящее время не являются частью Azure Active Directory портала.

## <a name="enable-resource-specific-consent-in-your-application"></a>Включить согласие на использование ресурсов в приложении

Шаги для включения RSC в приложении следующие:

1. [Настройка настроек согласия владельца группы на Azure Active Directory портале.](#configure-group-owner-consent-settings-in-the-azure-ad-portal)
1. [Зарегистрируйте приложение на платформа удостоверений Майкрософт через портал Azure AD.](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)
1. [Просмотрите разрешения приложений на портале Azure AD.](#review-your-application-permissions-in-the-azure-ad-portal)
1. [Получить токен доступа с платформы Microsoft Identity.](#obtain-an-access-token-from-the-microsoft-identity-platform)
1. [Обновите манифест Teams приложения.](#update-your-teams-app-manifest)
1. [Установите приложение прямо в Teams](#sideload-your-app-in-teams).
1. [Проверьте приложение на наличие дополнительных разрешений RSC.](#check-your-app-for-added-rsc-permissions)

## <a name="configure-group-owner-consent-settings-in-the-azure-ad-portal"></a>Настройка параметров согласия владельца группы на портале Azure AD

Вы можете включить или отключить [согласие владельца группы](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal) непосредственно на портале Azure:

> [!div class="checklist"]
>
>- Войтись на [портал Azure в](https://portal.azure.com) качестве [глобального администратора/администратора компании.](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator)  
 > - [Выберите](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings) **Azure Active Directory** Enterprise  =>  **приложения Согласие** и разрешения  =>    =>  **Настройки согласия пользователя.**
> - Включить, отключить или ограничить согласие пользователя с согласия владельца группы, помеченного **как контроль, на доступ к данным** приложений (по умолчанию **разрешается согласие владельца группы для всех владельцев групп).** Для установки приложения с помощью RSC владелец группы должен быть включен для этого пользователя.

![лазурный rsc конфигурации](../../assets/images/azure-rsc-configuration.png)

Чтобы включить или отключить согласие владельца группы с помощью PowerShell, следуйте шагам, изложенным в [согласии владельца группы Configure с помощью PowerShell.](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell)

## <a name="register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal"></a>Зарегистрируйте приложение в платформа удостоверений Майкрософт через портал Azure AD

Портал Azure Active Directory предоставляет центральную платформу для регистрации и настройки приложений. Ваше приложение должно быть зарегистрировано на портале Azure AD для интеграции с платформа удостоверений Майкрософт вызова microsoft Graph API. Для получения дополнительной [информации, см Регистрация приложения с платформа удостоверений Майкрософт](/graph/auth-register-app-v2).

>[!WARNING]
>Не регистрировать несколько Teams на один и тот же идентификатор приложения Azure AD. Идентификатор приложения должен быть уникальным для каждого приложения. Попытки установить несколько приложений на один и тот же идентификатор приложения не увенчаются успехом.

## <a name="review-your-application-permissions-in-the-azure-ad-portal"></a>Просмотрите разрешения приложений на портале Azure AD

Перейдите на  =>  **страницу регистрации домашних** приложений и выберите приложение RSC. Выберите **разрешения API** из левой навигационной бара и изучите список настроенных разрешений для приложения. Если ваше приложение будет делать только RSC Graph API звонки, удалите все разрешения на этой странице. Если ваше приложение также будет делать вызовы, не в том числе RSC, сохраняйте эти разрешения по мере необходимости.

>[!IMPORTANT]
>Портал Azure AD не может использоваться для запроса разрешений RSC. Разрешения RSC в настоящее время Teams для приложений, Teams клиента и заявлены в файле манифеста приложения (JSON).

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a>Получить токен доступа от платформа удостоверений Майкрософт

Чтобы сделать Graph API, необходимо получить токен доступа для приложения с платформы идентификации. Прежде чем ваше приложение сможет получить токен от платформа удостоверений Майкрософт, оно должно быть зарегистрировано на портале Azure AD. Маркер доступа содержит сведения о приложении и его разрешениях на доступ к ресурсам и API, доступным через Microsoft Graph.

Для получения токена доступа с платформы идентификации необходимо иметь следующие значения из процесса регистрации Azure AD:

- Идентификатор **приложения,** присвоенный порталом регистрации приложений. Если ваше приложение поддерживает один ва-по (SSO), вы должны использовать тот же идентификатор приложения для вашего приложения и SSO.
- Секрет **клиента/пароль или** публичная/частная ключевая пара **(Сертификат).** Это необязательно для нативных приложений;
- **Перенаправление URI** (или ОТВЕТ URL) для вашего приложения для получения ответов от Azure AD.

 *Смотрите* [Получить доступ от имени пользователя](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true) и получить доступ без [пользователя](/graph/auth-v2-service)

## <a name="update-your-teams-app-manifest"></a>Обновление манифеста Teams приложения

Разрешения RSC объявлены в файле манифеста приложения (JSON).  Добавьте [ключ webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) к манифесту приложения со следующими значениями:

> [!div class="checklist"]
>
> - **ID** - идентификатор приложения Azure AD. Для получения дополнительной информации [см. Зарегистрируйте свое приложение на портале Azure AD.](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)
> - **ресурс**  - любая строка. Это поле не имеет работы в RSC, но должно быть добавлено и иметь значение, чтобы избежать ответа на ошибку; любая строка будет делать.
> - **разрешения приложений** - разрешения RSC для вашего приложения. Для получения дополнительной информации [см.](resource-specific-consent.md#resource-specific-permissions)

>
>[!IMPORTANT]
> Разрешения, не вносяные RSC, хранятся на портале Azure. Не добавляйте их в манифест приложения.
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

## <a name="sideload-your-app-in-teams"></a>Загрузка приложения в Teams

Если администратор Teams пользовательских загрузок приложений, вы [можете загрузить приложение непосредственно](~/concepts/deploy-and-publish/apps-upload.md) в конкретную группу.

## <a name="check-your-app-for-added-rsc-permissions"></a>Проверьте приложение на наличие дополнительных разрешений RSC

>[!IMPORTANT]
>Разрешения RSC не приписываются пользователю. Звонки будут сделаны с разрешениями приложений, а не с разрешениями, делегированным пользователями. Таким образом, приложению может быть разрешено выполнять действия, которые пользователь не может, такие как создание канала или удаление вкладки. Вы должны просмотреть намерения владельца команды для вашего использования случае до принятия RSC API звонки. Для получения дополнительной информации [см. Microsoft Teams обзор API](/graph/teams-concept-overview).

После установки приложения в группу можно [использовать Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) для просмотра разрешений, предоставленных приложению в команде:

> [!div class="checklist"]
>
>- Получите группу **командыId от** клиента Teams клиента.
> - В Teams, выберите **Teams из** крайне левого навигационной бара.
> - Выберите команду, в которой приложение установлено из выпадают из меню.
> - Выберите **значок больше** вариантов (&#8943;).
> - Выберите **Получить ссылку на команду**.
> - Копировать и сохранить **значение groupId** из строки.
> - Войдите **в Graph Explorer**.
> - Сделайте **get** вызов к следующей конечной точке: `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants` . Поле clientAppId в ответе будет картой к appId, указанному в Teams приложения.
  ![Graph explorer на вызов GET.](../../assets/images/graph-permissions.png)

## <a name="code-sample"></a>Пример кода
| **Название образца** | **Описание** | **.NET** |**Node.js** |
|-----------------|-----------------|----------------|----------------|
| Ресурсное конкретное согласие (RSC) | Используйте RSC для вызова Graph API. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/nodeJs)|



## <a name="see-also"></a>См. также
 
* [Тестирование разрешений на согласие с конкретными ресурсами в Teams](test-resource-specific-consent.md)
* [Согласие на использование ресурсов в Microsoft Teams для администраторов](/MicrosoftTeams/resource-specific-consent)


