---
title: Управление Azure Active Directory в Teams Toolkit
author: zyxiaoyuer
description: Описание управления приложениями Azure Active Directory в Teams Toolkit
ms.author: surbhigupta
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/20/2022
ms.openlocfilehash: 4067b86bc3a8de0ed891e84ceef68f5f95741479
ms.sourcegitcommit: 80edf3c964bb47a2ee13f9eda4334ad19e21f331
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/24/2022
ms.locfileid: "65655650"
---
# <a name="azure-ad-manifest"></a>Azure AD манифеста

Манифест [Azure Active Directory (Azure AD)](/azure/active-directory/develop/reference-app-manifest) содержит определения всех атрибутов объекта Azure AD в платформа удостоверений Майкрософт.

Teams Toolkit теперь управляет Azure AD с файлом манифеста в качестве источника истинности во время Teams разработки приложения.

## <a name="customize-azure-ad-manifest-template"></a>Настройка Azure AD манифеста

Вы можете настроить Azure AD манифеста для обновления Azure AD приложения.

1. Откройте `aad.template.json` в проекте.
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add template.png" alt-text="template":::

2. Обновите шаблон напрямую [или ссылочные значения из другого файла](https://github.com/OfficeDev/TeamsFx/wiki/Manage-AAD-application-in-Teams-Toolkit#Placeholders-in-AAD-manifest-template). Здесь можно увидеть несколько сценариев настройки:
  
* [Добавление разрешения приложения](#customize-requiredresourceaccess)
* [Предварительная авторизация клиентского приложения](#customize-preauthorizedapplications)
* [Обновление URL-адреса перенаправления для ответа на проверку подлинности](#customize-redirect-urls)

3. [Разверните Azure AD приложения для локальной среды](#deploy-azure-ad-application-changes-for-local-environment).
  
4. [Разверните Azure AD приложения для удаленной среды](#deploy-azure-ad-application-changes-for-remote-environment).

### <a name="customize-requiredresourceaccess"></a>Настройка requiredResourceAccess

Если приложению Teams требуются дополнительные разрешения для вызова API с дополнительными разрешениями, `requiredResourceAccess` необходимо обновить свойство в шаблоне Azure AD манифеста. Для этого свойства можно увидеть следующий пример:

```JSON

   "requiredResourceAccess": [
    {
        "resourceAppId": "Microsoft Graph",
        "resourceAccess": [
            {
                "id": "User.Read", // For Microsoft Graph API, you can also use uuid for permission id
                "type": "Scope" // Scope is for delegated permission
            },
            {
                "id": "User.Export.All",
                "type": "Role" // Role is for application permission
            }
        ]
    },
    {
        "resourceAppId": "Office 365 SharePoint Online",
        "resourceAccess": [
            {
                "id": "AllSites.Read",
                "type": "Scope"
            }
        ]
    }
]
```

* `resourceAppId` Свойство  предназначено для разных API, для `Microsoft Graph` `Office 365` `SharePoint Online`и , введите имя непосредственно вместо UUID, а для других API используйте UUID.

* `resourceAccess.id` свойство  предназначено для разных разрешений, `Microsoft Graph` `Office 365 SharePoint Online`для и , введите имя разрешения непосредственно вместо UUID, а для других API используйте UUID.

* `resourceAccess.type` Свойство  используется для делегированного разрешения или разрешения приложения. `Scope` означает делегированное разрешение и `Role` разрешение приложения.

### <a name="customize-preauthorizedapplications"></a>Настройка preAuthorizedApplications

Свойство можно использовать `preAuthorizedApplications` для авторизации клиентского приложения, чтобы указать, что API доверяет приложению, и пользователи не соглашают его при вызове клиентом предоставленного API. Для этого свойства можно увидеть следующий пример:

```JSON

    "preAuthorizedApplications": [
        {
            "appId": "1fec8e78-bce4-4aaf-ab1b-5451cc387264",
            "permissionIds": [
                "{{state.fx-resource-aad-app-for-teams.oauth2PermissionScopeId}}"
            ]
        }
        ...
    ]
```

`preAuthorizedApplications.appId` Свойство  используется для приложения, которое требуется авторизовать. Если вы не знаете идентификатор приложения, но знаете только его имя, перейдите к портал Azure и выполните действия по поиску в приложении, чтобы найти идентификатор:

1. Перейдите [портал Azure](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) и откройте регистрацию приложений.

1. Выберите **все приложения и** найдите имя приложения.

1. Выберите имя приложения и получите идентификатор приложения на странице обзора.

### <a name="customize-redirect-urls"></a>Настройка URL-адресов перенаправления

  URL-адреса перенаправления используются при возврате ответов проверки подлинности, таких как маркеры после успешной проверки подлинности. ВЫ можете настроить URL-адреса `replyUrlsWithType`перенаправления с помощью свойства, например, `https://www.examples.com/auth-end.html` чтобы добавить его в качестве URL-адреса перенаправления, можно добавить его в следующем примере:

``` JSON
"replyUrlsWithType": [
    ...
    {
        "url": "https://www.examples.com/auth-end.html",
        "type": "Spa"
    }
]
```

## <a name="azure-ad-manifest-template-placeholders"></a>Azure AD шаблона манифеста

Файл Azure AD манифеста содержит аргументы-заполнители с {{...}} Операторы  заменяются во время сборки для разных сред. Ссылки на файл конфигурации, файл состояния и переменные среды можно создавать с помощью аргументов заполнителя.

### <a name="reference-state-file-values-in-azure-ad-manifest-template"></a>Ссылочные значения файла состояния в Azure AD манифеста

Файл состояния находится в `.fx\states\state.xxx.json` (xxx представляет другую среду). В следующем примере показан типичный файл состояния:

``` JSON
{
    "solution": {
        "teamsAppTenantId": "uuid",
        ...
    },
    "fx-resource-aad-app-for-teams": {
        "applicationIdUris": "api://xxx.com/uuid",
        ...
    }
    ...
}
```

Этот аргумент-заполнитель можно использовать в манифесте Azure AD: `{{state.fx-resource-aad-app-for-teams.applicationIdUris}}` для ссылки на `applicationIdUris` значение в свойстве`fx-resource-aad-app-for-teams`.

### <a name="reference-config-file-values-in-azure-ad-manifest-template"></a>Ссылки на значения файла конфигурации в Azure AD манифеста

Файл конфигурации находится в `.fx\configs\config.xxx.json` папке (xxx представляет другую среду). В следующем примере показан файл конфигурации:

``` JSON
{
  "$schema": "https://aka.ms/teamsfx-env-config-schema",
  "description": "description.",
  "manifest": {
    "appName": {
      "short": "app",
      "full": "Full name for app"
    }
  }
}
```

Аргумент-заполнитель можно использовать в манифесте Azure AD: `{{config.manifest.appName.short}}` для ссылки на `short` значение.

### <a name="reference-environment-variable-in-azure-ad-manifest-template"></a>Эталонная переменная среды в Azure AD манифеста

Иногда не требуется жестко кодировать значения в шаблоне Azure AD манифеста. Например, если значение является секретом. Azure AD шаблона манифеста поддерживает значения переменных эталонной среды. Вы можете использовать синтаксис `{{env.YOUR_ENV_VARIABLE_NAME}}` в значениях параметров, чтобы указать инструментарию разрешить значение текущей переменной среды.

## <a name="author-and-preview-azure-ad-manifest-with-code-lens"></a>Создание и предварительный просмотр Azure AD с помощью code lens

Azure AD шаблона манифеста имеет линзы кода для просмотра и редактирования.

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/preview view.png" alt-text="previewview":::

### <a name="azure-ad-manifest-template-file"></a>Azure AD шаблона манифеста

В начале файла Azure AD манифеста есть начальный объект кода. Выберите линзу кода, чтобы создать Azure AD в зависимости от выбранной среды.

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/add codelens.png" alt-text="addcodelens":::

### <a name="placeholder-argument-code-lens"></a>Линза кода аргумента заполнителя

Линза кода аргумента заполнителя позволяет быстро просмотреть значения для локальной среды отладки и разработки. При наведении указателя мыши на аргумент заполнителя отображается поле подсказки для значений во всех средах.

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/add arguments.png" alt-text="addarguments":::

### <a name="required-resource-access-code-lens"></a>Необходимый код доступа к ресурсу

Она отличается от официальной схемы манифеста [Azure AD](/azure/active-directory/develop/reference-app-manifest) `resourceAppId` `resourceAccess` `requiredResourceAccess`, которая и идентификатор в свойстве поддерживают только UUID, шаблон манифеста Azure AD в Teams Toolkit `Microsoft Graph` `Office 365 SharePoint Online` также поддерживает удобочитаемые пользователем строки и разрешения. При вводе UUID в code lens отображаются удобочитаемые строки пользователя, в противном случае — UUID.

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/add resource.png" alt-text="addresource":::

### <a name="pre-authorized-applications-code-lens"></a>Объект кода предварительно авторизованных приложений

В объекте Code lens показано имя приложения для каждого авторизованного идентификатора приложения для `preAuthorizedApplications` свойства.

## <a name="deploy-azure-ad-application-changes-for-local-environment"></a>Развертывание Azure AD приложения для локальной среды

1. Выберите `Preview` линзы кода в `aad.template.json`.
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add deploy1.png" alt-text="deploy1":::

2. Выберите `local` среду.
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add deploy2.png" alt-text="deploy2":::

3. Выберите `Deploy Azure AD Manifest` линзы кода в `aad.local.json`.

     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add deploy3.png" alt-text="deploy3":::

4. Развертываются Azure AD приложения, используемого в локальной среде.
  
## <a name="deploy-azure-ad-application-changes-for-remote-environment"></a>Развертывание Azure AD приложений для удаленной среды

1. Откройте палитру команд и выберите: `Teams: Deploy Azure Active Directory application manifest`.
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add deploy4.png" alt-text="deploy4":::

2. Вы также можете щелкнуть правой кнопкой мыши контекстное `aad.template.json` `Deploy Azure Active Directory application manifest` меню и выбрать его.
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add deploy5.png" alt-text="deploy5":::

## <a name="view-azure-ad-application-on-the-azure-portal"></a>Просмотр Azure AD приложения на портал Azure

1. Скопируйте Azure AD `state.xxx.json` клиента приложения из (xxx — это имя среды, в котором развернут файл Azure AD) в свойстве`fx-resource-aad-app-for-teams`.
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add view1.png" alt-text="view1":::

2. Перейдите [портал Azure](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) и войдите в Microsoft 365 учетной записи.
  
> [!NOTE]
> Убедитесь, что учетные данные входа Teams приложения и учетной записи M365 одинаковы.

3. Откройте [страницу регистрации приложений](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) и выполните поиск Azure AD с помощью идентификатора клиента, скопированного ранее.
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add view2.png" alt-text="view2":::

4. Выберите Azure AD в результатах поиска, чтобы просмотреть подробные сведения.
  
5. На Azure AD страницы сведений о приложении выберите меню`Manifest`, чтобы просмотреть манифест этого приложения. Схема манифеста совпадает со схемой в файле `aad.template.json` . Дополнительные сведения о манифесте см[. Azure Active Directory манифеста приложения](/azure/active-directory/develop/reference-app-manifest).
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add view3.png" alt-text="view3":::

6. Вы можете выбрать **другое меню,** чтобы просмотреть или настроить Azure AD с помощью портала.
  
## <a name="use-an-existing-azure-ad-application"></a>Использование существующего Azure AD приложения

Вы можете использовать существующее приложение Azure AD для проекта Teams. Дополнительные сведения см. в статье "Использование существующего Azure AD приложения для Teams [приложения"](https://github.com/OfficeDev/TeamsFx/wiki/Customize-provision-behaviors#use-an-existing-aad-app-for-your-teams-app).

## <a name="azure-ad-application-in-teams-application-development-lifecycle"></a>Azure AD приложения в Teams разработки приложений

Необходимо взаимодействовать с приложением Azure AD на различных этапах Teams разработки приложения.

1. **Создание Project**

      Вы можете создать проект с Teams Toolkit, который поставляется с поддержкой единого входа по умолчанию, например `SSO-enabled tab`. Дополнительные сведения о создании нового приложения см. в Teams [с помощью Teams Toolkit](create-new-project.md). Автоматически создается Azure AD манифеста. `templates\appPackage\aad.template.json` Teams Toolkit создает или обновляет Azure AD во время локальной разработки или при перемещении приложения в облако.

2. **Добавление единого входа в бот или вкладку**

      После создания приложения Teams без встроенного единого входа Teams Toolkit пошагово помогает добавить единый вход для проекта. В результате автоматически создается Azure AD манифеста. `templates\appPackage\aad.template.json`

      Teams Toolkit создает или обновляет Azure AD во время следующего локального сеанса отладки или при перемещении приложения в облако.

3. **Локальное построение**

    Teams Toolkit выполняет следующие функции во время локальной разработки (известной как F5):

    * Прочитайте файл`state.local.json`, чтобы найти существующее Azure AD приложения. Если приложение Azure AD уже существует, Teams Toolkit повторно использует существующее приложение Azure AD `aad.template.json` в противном случае необходимо создать новое приложение с помощью файла.

    * Изначально игнорирует некоторые свойства в файле манифеста, для которых требуется дополнительный контекст (например, свойство replyUrls, требующее локальной конечной точки отладки) во время создания нового приложения Azure AD с файлом манифеста.

    * После успешного запуска локальной среды разработки идентификаторы Azure AD приложения, replyUrls и другие свойства, недоступные на этапе создания, обновляются соответствующим образом.

    * Изменения, внесенные в Azure AD приложения, загружаются во время следующего локального сеанса отладки. Вы можете [просмотреть Azure AD приложения для](https://github.com/OfficeDev/TeamsFx/wiki/) применения изменений вручную Azure AD изменения приложения.

4. **Подготовка облачных ресурсов**

      Необходимо подготовить облачные ресурсы и развернуть приложение при перемещении приложения в облако. На этапах, таких как локальная разработка, Teams Toolkit будет:

      * Прочитайте файл`state.{env}.json`, чтобы найти существующее Azure AD приложения. Если приложение Azure AD уже существует, Teams Toolkit повторно использует существующее приложение Azure AD `aad.template.json` в противном случае необходимо создать новое приложение с помощью файла.

      * Изначально игнорирует некоторые свойства в файле манифеста, для которых требуется дополнительный контекст (например, свойство replyUrls требует внешнего интерфейса или конечной точки бота) во время создания нового приложения Azure AD с файлом манифеста.

      * После завершения подготовки других ресурсов идентификаторы Azure AD и replyUrls приложения обновляются соответствующим образом в соответствии с правильными конечными точками.

5. **Создание приложения**

    * Команда развертывания в облаке развертывает приложение на подготовленных ресурсах. Он не включает развертывание Azure AD внесенных изменений приложения

    * Вы можете увидеть, [как Azure AD изменения приложения для](#deploy-azure-ad-application-changes-for-remote-environment) удаленной среды для развертывания Azure AD приложений для удаленной среды.

    * Teams Toolkit обновляет приложение Azure AD в соответствии с файлом шаблона Azure AD манифеста.

## <a name="limitations"></a>Ограничения

1. Teams Toolkit поддерживает не все свойства, перечисленные в схеме Azure AD манифеста.
  
      В следующей таблице перечислены свойства, которые не поддерживаются в расширении Teams Toolkit:

      |**Не поддерживаемые свойства**|**Причина**|
      |-----------|----------|
      |passwordCredentials|Не разрешено в манифесте|
      |createdDateTime|Только для чтения и не может изменить|
      |logoUrl|Только для чтения и не может изменить|
      |publisherDomain|Только для чтения и не может изменить|
      |oauth2RequirePostResponse|В API Graph|
      |oauth2AllowUrlPathMatching|В API Graph|
      |samlMetadataUrl|В API Graph|
      |orgRestrictions|В API Graph|
      |certification|В API Graph|

2. В `requiredResourceAccess` настоящее время свойство может использовать имя приложения ресурса для чтения или строки имени разрешения только для `Microsoft Graph` API и API `Office 365 SharePoint Online` . Для других API необходимо использовать UUID. Чтобы получить идентификаторы из портал Azure, выполните следующие действия.

    * Регистрация нового приложения Azure AD на [портал Azure](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps)
    * Выберите `API permissions` на странице Azure AD приложения
    * Выберите `add a permission` , чтобы добавить нужное разрешение
    * Выберите `Manifest`в свойстве `requiredResourceAccess` идентификаторы API и разрешения.

## <a name="see-also"></a>См. также

* [Настройка манифеста приложения в наборе средств](TeamsFx-manifest-customization.md)
* [Предварительный просмотр манифеста приложения в наборе средств](TeamsFx-manifest-preview.md)
