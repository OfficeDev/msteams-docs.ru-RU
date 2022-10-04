---
title: Обновление манифеста для включения единого входа для вкладок
description: Обновите манифест Teams для включения единого входа (SSO) для вкладок и перезагрузите его в клиент Teams для тестирования проверки подлинности единого входа.
ms.topic: how-to
ms.localizationpriority: high
keywords: вкладки проверки подлинности команд Microsoft Azure Active Directory (Azure AD) API Graph
ms.openlocfilehash: bd5b7257a131a11e861b94221c533d8364b6bb54
ms.sourcegitcommit: 176bbca74ba46b7ac298899d19a2d75087fb37c1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/04/2022
ms.locfileid: "68376587"
---
# <a name="update-manifest-for-sso-and-preview-app"></a>Обновление манифеста для системы единого входа и предварительного просмотра приложения

Перед обновлением манифеста приложения Teams убедитесь, что вы настроили код для включения единого входа в приложении на вкладке.

> [!div class="nextstepaction"]
> [Настройка кода](tab-sso-code.md)

Вы зарегистрировали приложение с вкладками в Azure AD и получили идентификатор приложения. Вы также настроили свой код для вызова `getAuthToken()` и обработки маркера доступа. Теперь необходимо обновить манифест приложения Teams для включения единого входа для приложения с вкладками. Манифест приложения Teams описывает, как приложение интегрируется в Teams.

## <a name="webapplicationinfo-property"></a>Свойство webApplicationInfo

Настройте свойство `webApplicationInfo` в файле манифеста приложения Teams. Это свойство включает единый вход для вашего приложения и помогает вашим пользователям беспрепятственно получать доступ к вашему приложению с вкладками.

&nbsp;&nbsp;:::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/sso-manifest.png" alt-text="Настройка манифеста приложения Teams":::

У `webApplicationInfo` есть два элемента: `id` и `resource`.

| Элемент | Описание |
| --- | --- |
| id | Введите идентификатор приложения (GUID), созданный в Azure AD. |
| resource | Введите URI поддомена вашего приложения и URI идентификатора приложения, созданного в Azure AD при создании области. Вы можете скопировать его из раздела **Azure AD** > **Предоставление API**. |

> [!NOTE]
> Для реализации свойства `webApplicationInfo` необходимо использовать манифест версии 1.5 или более новой версии.

URI идентификатора приложения, зарегистрированного вами в Azure AD, настроен в соответствии с областью предоставляемого вами API. Настройте URI поддомена приложения в `resource` чтобы убедиться, что запрос проверки подлинности с использованием `getAuthToken()` исходит из домена, заданного в манифесте приложения Teams.

Дополнительные сведения см. в [webApplicationInfo](../../../resources/schema/manifest-schema.md#webapplicationinfo).

## <a name="to-configure-teams-app-manifest"></a>Чтобы настроить манифест приложения Teams

1. Откройте вкладку проекта приложения.
2. Откройте папку манифеста.

  > [!NOTE]
  >
  > - Папка манифеста должна находиться в корне вашего проекта. Дополнительные сведения см. в статье [Создание пакета приложения Microsoft Teams](../../../concepts/build-and-test/apps-package.md).
  > - Дополнительные сведения о том, как создать файл manifest.json, см. в разделе [Справочник: схема манифеста для Microsoft Teams](../../../resources/schema/manifest-schema.md).

1. Откройте файл manifest.json.
1. Добавьте следующий фрагмент кода в файл манифеста, чтобы добавить новое свойство:

    ```json
    "webApplicationInfo": {
    "id": "{Azure AD AppId}",
    "resource": "api://{Subdomain}.example.com/{Azure AD AppId}"
    }
    ```

    где
    - {Azure AD AppId} — это идентификатор приложения, созданный вами при регистрации приложения в Azure AD. Это GUID.
    - {{Subdomain}.app ID URI} — это URI идентификатора приложения, который вы зарегистрировали при создании области в Azure AD.

4. Обновите идентификатор приложения из Azure AD в свойстве **id**.
5. Обновите URL субдомена в следующих свойствах:
   1. `contentUrl`
   2. `configurationUrl`
   3. `validDomains`
6. Сохраните файл манифеста приложения Teams.

<br>
<details>
<summary>Вот пример манифеста приложения после его обновления.</summary>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.11/MicrosoftTeams.schema.json",
  "manifestVersion": "1.11",
  "version": "1.0.0",
  "id": "bccfbe67-e08b-4ec1-a7fd-e0aaf41a097c",
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
> Во время отладки вы можете использовать ngrok для тестирования своего приложения в Azure AD. В этом случае вам нужно заменить поддомен в `api://subdomain.example.com/00000000-0000-0000-0000-000000000000` на URL-адрес ngrok. Вам нужно будет обновлять URL всякий раз, когда изменяется ваш поддомен ngrok. Например, api://23c3-103-50-148-128.ngrok.io/bccfbe67-e08b-4ec1-a7fd-e0aaf41a097c.

## <a name="sideload-and-preview-in-teams"></a>Неопубликованная загрузка и предварительный просмотр в Teams

Вы настроили приложение вкладки, чтобы включить единый вход в Azure AD, в коде приложения и в файле манифеста Teams. Теперь вы можете загрузить неопубликованное приложение с вкладками в Teams и просмотреть его в среде Teams.

:::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/sso-flow.png" alt-text="Приложение единого входа":::

Чтобы предварительно просмотреть приложение с вкладками в Teams:

1. Создайте пакет приложения.

   Пакет приложения представляет собой ZIP-файл, содержащий файл манифеста приложения и значки приложений.

1. Откройте Teams.

1. Выберите **Приложения** > **Управление приложениями** > **Отправка приложения**.

    Появятся варианты отправки приложения.

1. Выберите **Отправить пользовательское приложение** чтобы отправить неопубликованное приложение вкладки в Teams.

1. Выберите ZIP-файл пакета приложения, а затем нажмите кнопку **Добавить**.

    Приложение вкладки загружено, и появляется диалоговое окно со сведениями о дополнительных разрешениях, которые могут потребоваться.

1. Нажмите **Продолжить**.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/teams-sso-consent.png" alt-text="Диалоговое окно Teams со сведениями о необходимых дополнительных разрешениях":::

    Появится диалоговое окно согласия Azure AD.

1. Выберите **Принять**, чтобы дать согласие на использование областей с открытым идентификатором.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/aad-sso-consent.png" alt-text="Диалоговое окно согласия Azure AD":::

    Teams открывает приложение на вкладке, и вы можете его использовать.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/teams-sso-app.png" alt-text="Пример приложения на вкладке &quot;Команды&quot; с включенным единым входом":::

    Поздравляем! Вы включили систему единого входа для своего приложения вкладки.

## <a name="see-also"></a>См. также

- [Схема манифеста для Microsoft Teams](../../../resources/schema/manifest-schema.md)
- [Формат схемы манифеста](https://developer.microsoft.com/json-schemas/teams/v1.12/MicrosoftTeams.schema.json)
- [Создание манифеста приложения в Microsoft Teams](../../../concepts/build-and-test/apps-package.md)
