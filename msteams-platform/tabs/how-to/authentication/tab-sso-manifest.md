---
title: Обновление манифеста для включения единого входа для вкладок
description: Описание манифеста обновления для включения единого входа для вкладок
ms.topic: how-to
ms.localizationpriority: medium
keywords: вкладки проверки подлинности teams Microsoft Azure Active Directory (Azure AD) API Graph
ms.openlocfilehash: 90a1ac781ef521f4b236bdf26f50d44533fa815a
ms.sourcegitcommit: c398dfdae9ed96f12e1401ac7c8d0228ff9c0a2b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/30/2022
ms.locfileid: "66558739"
---
# <a name="update-manifest-for-sso-and-preview-app"></a>Обновление манифеста для единого входа и приложения предварительной версии

Перед обновлением манифеста приложения Teams убедитесь, что вы настроите код для включения единого входа в приложении вкладки.

> [!div class="nextstepaction"]
> [Настройка кода](tab-sso-code.md)

Вы зарегистрировали приложение вкладки в Azure AD и получили идентификатор приложения. Вы также настроите код для вызова и `getAuthToken()` обработки маркера доступа. Теперь необходимо обновить манифест приложения Teams, чтобы включить единый вход для приложения вкладки. Манифест приложения Teams описывает, как приложение интегрируется в Teams.

## <a name="webapplicationinfo-property"></a>Свойство webApplicationInfo

Настройте свойство `webApplicationInfo` в файле манифеста приложения Teams. Это свойство позволяет приложению использовать единый вход, чтобы пользователи приложения могли легко получать доступ к приложению вкладки.

&nbsp;&nbsp;:::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/sso-manifest.png" alt-text="Конфигурация манифеста приложения Teams":::

`webApplicationInfo` имеет два элемента и `id` `resource`.

| Элемент | Описание |
| --- | --- |
| id | Введите идентификатор приложения (GUID), созданный в Azure AD. |
| resource | Введите URI поддомена приложения и URI идентификатора приложения, созданный в Azure AD при создании области. Его можно скопировать из раздела **Azure AD** >  **Expose a API**. |

> [!NOTE]
> Используйте манифест версии 1.5 или более поздней для реализации `webApplicationInfo` свойства.

Универсальный код ресурса (URI) идентификатора приложения, зарегистрированный в Azure AD, настраивается в области предоставляемого API. Настройте URI `resource` `getAuthToken()` поддомена приложения, чтобы убедиться, что запрос на проверку подлинности, используемый, выполняется из домена, указанного в манифесте приложения Teams.

Дополнительные сведения см. в [разделе webApplicationInfo](../../../resources/schema/manifest-schema.md#webapplicationinfo).

## <a name="to-configure-teams-app-manifest"></a>Настройка манифеста приложения Teams

1. Откройте проект приложения табуляции.
2. Откройте папку манифеста.

  > [!NOTE]
  >
  > - Папка манифеста должна находиться в корне проекта. Дополнительные сведения см. в [статье "Создание пакета приложения Microsoft Teams"](../../../concepts/build-and-test/apps-package.md).
  > - Дополнительные сведения о создании файла manifest.json см. в справочнике [по схеме манифеста для Microsoft Teams](../../../resources/schema/manifest-schema.md).

1. Открытие файла manifest.json
1. Добавьте следующий фрагмент кода в файл манифеста, чтобы добавить новое свойство:

    ```json
    "webApplicationInfo": {
    "id": "{Azure AD AppId}",
    "resource": "api://{Subdomain}.example.com/{Azure AD AppId}"
    }
    ```

    Где
    - {Azure AD AppId} — это идентификатор приложения, созданный при регистрации приложения в Azure AD. Это ИДЕНТИФИКАТОР GUID.
    - {{URI идентификатора приложения}.app} — это универсальный код ресурса (URI) идентификатора приложения, зарегистрированный при создании области в Azure AD.

4. Обновите идентификатор приложения из Azure AD в **свойстве id**.
5. Обновите URL-адрес поддомена в следующих свойствах:
   1. `contentUrl`
   2. `configurationUrl`
   3. `validDomains`
6. Сохраните файл манифеста приложения Teams.

<br>
<details>
<summary>Ниже приведен пример манифеста приложения после его обновления.</summary>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.11/MicrosoftTeams.schema.json",
  "manifestVersion": "1.11",
  "version": "1.0.0",
  "id": "bccfbe67-e08b-4ec1-a7fd-e0aaf41a097c",
  "packageName": "com.contoso.teamsauthsso",
  "developer": {
    "name": "Microsoft",
    "websiteUrl": "https://www.microsoft.com",
    "privacyUrl": "https://www.microsoft.com/privacy",
    "termsOfUseUrl": "https://www.microsoft.com/termsofuse"
  },
  "name": {
    "short": "Teams Auth SSO",
    "full": "Teams Auth SSO"
  },
  "description": {
    "short": "Teams Auth SSO app",
    "full": "The Teams Auth SSO app"
  },
  "icons": {
    "outline": "outline.png",
    "color": "color.png"
  },
  "accentColor": "#60A18E",
  "staticTabs": [
    {
      "entityId": "auth",
      "name": "Auth",
      "contentUrl": "https://contoso.com/Home/Index",
      "scopes": [ "personal" ]
    }
  ],
  "configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/Home/Configure",
      "canUpdateConfiguration": true,
      "scopes": [
        "team"
      ]
    }
  ],
  "permissions": [ "identity", "messageTeamMembers" ],
  "validDomains": [
    "contoso.com"
  ],
  "webApplicationInfo": {
    "id": "bccfbe67-e08b-4ec1-a7fd-e0aaf41a097c",
    "resource": "api://contoso.com/bccfbe67-e08b-4ec1-a7fd-e0aaf41a097c"
  }
}
```

</details>

> [!NOTE]
> Во время отладки можно использовать ngrok для тестирования приложения в Azure AD. В этом случае необходимо `api://subdomain.example.com/00000000-0000-0000-0000-000000000000` заменить поддомен url-адресом ngrok. Url-адрес необходимо обновлять при каждом изменении поддомена ngrok, например api://23c3-103-50-148-128.ngrok.io/bccfbe67-e08b-4ec1-a7fd-e0aaf41a097c.

## <a name="sideload-and-preview-in-teams"></a>Загрузка неопубликованных приложений и предварительный просмотр в Teams

Вы настроите приложение вкладки, чтобы включить единый вход в Azure AD, в коде приложения и в файле манифеста Teams. Теперь вы можете загрузить неопубликованную вкладку в Teams и просмотреть его в среде Teams.

:::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/sso-flow.png" alt-text="Приложение единого входа":::

Чтобы просмотреть приложение вкладки в Teams:

1. Создайте пакет приложения.

   Пакет приложения — это ZIP-файл, содержащий файл манифеста приложения и значки приложения.

1. Откройте Teams.

1. Выберите **"Управление** > **приложениями" для отправки** > **приложения**.

    Отобразятся параметры для отправки приложения.

1. Выберите **"Отправить пользовательское приложение" для** загрузки неопубликованного приложения табуляции в Teams.

1. Выберите ZIP-файл пакета приложения и нажмите кнопку **"Добавить"**.

    Приложение вкладки загружено неопубликованно, и появится диалоговое окно с уведомлением о дополнительных разрешениях, которые могут потребоваться.

1. Нажмите **Продолжить**.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/teams-sso-consent.png" alt-text="Диалоговое окно Teams с уведомлением о необходимых дополнительных разрешениях":::

    Появится Azure AD согласия.

1. Выберите **"Принять** ", чтобы предоставить согласие для областей с открытым идентификатором.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/aad-sso-consent.png" alt-text="Azure AD согласия":::

    Teams открывает приложение вкладки, и вы можете использовать его.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/teams-sso-app.png" alt-text="Пример приложения вкладки Teams с включенным единым входом":::

    Поздравляем! Вы включили единый вход для приложения вкладки.

## <a name="see-also"></a>См. также

- [Схема манифеста для Microsoft Teams](../../../resources/schema/manifest-schema.md)
- [Формат схемы манифеста](https://developer.microsoft.com/json-schemas/teams/v1.12/MicrosoftTeams.schema.json)
- [Создание манифеста приложения в Microsoft Teams](../../../concepts/build-and-test/apps-package.md)
