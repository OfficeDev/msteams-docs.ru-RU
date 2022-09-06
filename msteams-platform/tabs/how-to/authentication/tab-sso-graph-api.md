---
title: Расширение приложения вкладки с использованием разрешений Microsoft Graph
description: Настройка дополнительных разрешений и областей с помощью Microsoft Graph для включения единого входа (SSO).
ms.topic: how-to
ms.localizationpriority: high
keywords: teams проверка подлинности вкладки Microsoft Azure Active Directory (Azure AD) API Graph делегированное разрешение маркер доступа область
ms.openlocfilehash: 3232d1104a715b8c50f39b1e70d58fa18d970b7c
ms.sourcegitcommit: d92e14fad6567fe91fd52ee6c213836740316683
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/06/2022
ms.locfileid: "67605091"
---
# <a name="extend-tab-app-with-microsoft-graph-permissions-and-scope"></a>Расширение приложения вкладки с использованием разрешений и областей Microsoft Graph

Вы можете расширить приложение вкладки с помощью Microsoft Graph, чтобы предоставить пользователям дополнительные разрешения, например разрешения на просмотр профиля пользователя приложения, чтение почты и т. д. Приложение должно запросить определенные области разрешений, чтобы получить маркеры доступа при согласии пользователя приложения.

Области Graph, например `User.Read` или `Mail.Read`, позволяют указать, как приложение получает доступ к учетной записи пользователя Teams. Необходимо указать области в запросе на авторизацию.

Из этого раздела вы узнаете, как:

- [Настраивать разрешения API в Azure AD](#configure-api-permissions-in-azure-ad)
- [Настраивать проверку подлинности для разных платформ](#configure-authentication-for-different-platforms)
- [Получать маркер доступа для MS Graph](#acquire-access-token-for-ms-graph)

## <a name="configure-api-permissions-in-azure-ad"></a>Настройка разрешений API в Azure AD

Вы можете настроить дополнительные области Graph в Azure AD для приложения. Это делегированные разрешения, используемые приложениями, которым требуется доступ для входа. Пользователю или администратору приложения, выполнившему вход, следует предоставить свое согласие. Приложение вкладки может предоставить согласие от имени вошедшего пользователя при вызове Microsoft Graph.

### <a name="to-configure-api-permissions"></a>Чтобы настроить разрешения API:

1. Откройте приложение, зарегистрированное на [портале Azure](https://ms.portal.azure.com/).

2. Выберите **Управление** > **Разрешение API** на панели слева.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/api-permission-menu.png" alt-text="Параметр меню разрешений приложения.":::

    Появится страница **Разрешения API**.

3. Выберите **+ Добавить разрешения**, чтобы добавить разрешения API Microsoft Graph

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/app-permission.png" alt-text="Страница &quot;Разрешения приложения&quot;.":::

    Появится страница **Запрос разрешений API**.

4. Выберите **Microsoft Graph**.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/request-api-permission.png" alt-text="Страница &quot;Запрос разрешений API&quot;.":::

    Отобразятся параметры разрешений Graph.

5. Выберите **Делегированные разрешения**, чтобы просмотреть список разрешений.

   :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/delegated-permission.png" alt-text="Делегированные разрешения.":::

6. Выберите соответствующие разрешения для приложения, а затем щелкните **Добавить разрешения**.

   :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/select-permission.png" alt-text="Выбор разрешений.":::

    Вы также можете ввести имя разрешения в поле поиска, чтобы найти его.

    В браузере появится сообщение о том, что разрешения обновлены.

   :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/updated-permission-msg.png" alt-text="Сообщение об обновлении разрешений.":::

    Добавленные разрешения отображаются на странице **Разрешения API**.

   :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/configured-permissions.png" alt-text="Разрешения API настроены.":::

    Вы настроили приложение с использованием разрешений Microsoft Graph.

## <a name="configure-authentication-for-different-platforms"></a>Настройка проверки подлинности для разных платформ

В зависимости от платформы или устройства, для которых предназначено приложение, может потребоваться дополнительная настройка, например перенаправление URI, определенные параметры проверки подлинности или сведения, относящиеся к платформе.

> [!NOTE]
>
> - Если приложению вкладки не предоставлено согласие ИТ-администратора, пользователям следует дать согласие при первом использовании приложения на другой платформе.
> - Неявное предоставление разрешения не требуется, если в приложении вкладки включен единый вход.

Вы можете настроить проверку подлинности для нескольких платформ, если URL-адрес уникален.

### <a name="to-configure-authentication-for-a-platform"></a>Чтобы настроить проверку подлинности для платформы:

1. Откройте приложение, зарегистрированное на [портале Azure](https://ms.portal.azure.com/).

1. Выберите **Управление** > **Проверка подлинности** на панели слева.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/azure-portal-platform.png" alt-text="Проверка подлинности для платформ":::

    Появится страница **Конфигурации платформ**.

1. Выберите **+ Добавить платформу**.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/add-platform.png" alt-text="Добавление платформы":::

    Появится страница **Настройка платформ**.

1. Выберите платформу, которую нужно настроить для приложения вкладки. Вы можете выбрать тип платформы в Интернете или SPA.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/configure-platform.png" alt-text="Выбор веб-платформы":::

    Можно настроить несколько платформ определенного типа. Убедитесь, что URI перенаправления уникален для каждой настраиваемой платформы.

    Появится страница "Настройка веб-платформы".

    > [!NOTE]
    > Конфигурации будут отличаться в зависимости от выбранной платформы.

1. Введите сведения о конфигурации платформы.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/config-web-platform.png" alt-text="Настройка веб-платформы":::

    1. Введите URI перенаправления. URI должен быть уникальным.
    2. Введите URL-адрес выхода из внешнего канала.
    3. Выберите маркеры, которые Azure AD отправит для вашего приложения.

1. Нажмите **Настроить**.

    Платформа настраивается и отображается на странице **Конфигурации платформ**.

## <a name="acquire-access-token-for-ms-graph"></a>Получение маркера доступа для MS Graph

Вам нужно получить маркер доступа для Microsoft Graph. Это можно сделать с помощью потока OBO в Azure AD.

Текущая реализация для единого входа обеспечивает разрешения только на уровне пользователя, и их невозможно использовать для выполнения вызовов Graph. Чтобы получить разрешения (области), необходимые для выполнения вызова Graph, приложения единого входа реализуют настраиваемую веб-службу для обмена маркера, полученного из пакета SDK Teams для JavaScript, на маркер, который включает необходимые области. Для получения маркера со стороны клиента можно использовать библиотеку проверки подлинности Майкрософт (MSAL).

После настройки разрешений Graph в Azure AD:

- [Настройка клиентского кода для получения маркера доступа с помощью MSAL](#configure-code-to-fetch-access-token-using-msal)
- [Передача маркера доступа серверному коду](#pass-the-access-token-to-server-side-code)

### <a name="configure-code-to-fetch-access-token-using-msal"></a>Настройка кода для получения маркера доступа с помощью MSAL

В следующем коде приводится пример потока OBO для получения маркера доступа из клиента Teams с помощью MSAL.

### <a name="c"></a>[C#](#tab/dotnet)

```csharp

IConfidentialClientApplication app = ConfidentialClientApplicationBuilder.Create(<"Client id">)
                                                .WithClientSecret(<"Client secret">)
                                                .WithAuthority($"https://login.microsoftonline.com/<"Tenant id">")
                                                .Build();
 
            try
            {
                var idToken = <"Client side token">;
                UserAssertion assert = new UserAssertion(idToken);
                List<string> scopes = new List<string>();
                scopes.Add("https://graph.microsoft.com/User.Read");
                var responseToken = await app.AcquireTokenOnBehalfOf(scopes, assert).ExecuteAsync();
                return responseToken.AccessToken.ToString();
            }
            catch (Exception ex)
            {
                return ex.Message;
            }
        }
```

### <a name="nodejs"></a>[Node.js](#tab/nodejs)

```Node.js

// Exchange client Id side token with server token
  app.post('/getProfileOnBehalfOf', function(req, res) {
        var tid = < "Tenant id" >
    var token = < "Client side token" >
    var scopes = ["https://graph.microsoft.com/User.Read"];

        // Creating MSAL client
        const msalClient = new msal.ConfidentialClientApplication({
            auth: {
                clientId: < "Client ID" >,
                clientSecret: < "Client Secret" >
      }
        });

        var oboPromise = new Promise((resolve, reject) => {
            msalClient.acquireTokenOnBehalfOf({
                authority: `https://login.microsoftonline.com/${tid}`,
                oboAssertion: token,
                scopes: scopes,
                skipCache: true
            }).then(result => {
                console.log("Token is: " + result.accessToken);
            }).catch(error => {
                reject({ "error": error.errorCode });
            });
        });
```

---

### <a name="pass-the-access-token-to-server-side-code"></a>Передача маркера доступа серверному коду

Если необходим доступ к данным Microsoft Graph, настройте серверный код следующим образом:

1. Проверка маркера доступа. Дополнительные сведения см. в разделе [Проверка маркера доступа](tab-sso-code.md#validate-the-access-token);
1. Инициирование потока OBO OAuth 2.0 с вызовом платформы удостоверений Майкрософт, которая включает маркер доступа, некоторые метаданные о пользователе и учетные данные приложения вкладки (идентификатор приложения и секрет клиента). Платформа удостоверений Майкрософт вернет новый маркер доступа, который можно использовать для доступа к Microsoft Graph.
1. Получение данных из Microsoft Graph с помощью нового маркера.
1. Используйте сериализацию кэша маркеров в MSAL.NET, чтобы при необходимости кэшировать новый маркер доступа для нескольких вызовов.

> [!IMPORTANT]
> В целях безопасности рекомендуется всегда использовать серверный код для выполнения вызовов Microsoft Graph или других вызовов, требующих передачи маркера доступа. Никогда не возвращайте маркер OBO клиенту, чтобы клиент мог выполнять прямые вызовы в Microsoft Graph. Это помогает защитить маркер от перехвата или утечки.

## <a name="known-limitations"></a>Известные ограничения

Согласие администратора клиента. Простой способ [предоставления согласия от имени организации в качестве администратора клиента](/azure/active-directory/manage-apps/consent-and-permissions-overview#admin-consent) — получить [согласие от администратора](/azure/active-directory/manage-apps/grant-admin-consent).

Вы можете запросить согласие с помощью API проверки подлинности. Другой способ получения областей Graph — представить диалоговое окно согласия, используя существующий [метод проверки подлинности стороннего поставщика OAuth](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-pop-up-page). Этот подход включает в себя отображение всплывающего диалогового окна Azure AD для получения согласия.

<details>
<summary>Чтобы запросить дополнительное согласие с помощью API Auth, выполните следующие действия.</summary>

1. Маркер, полученный с помощью `getAuthToken()`, следует обменять на стороне сервера, используя [поток On-Behalf-Of](/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow) в Azure AD, чтобы получить доступ к другим API Graph. Убедитесь, что для этого обмена вы используете конечную точку Graph v2.
2. В случае ошибки обмена Azure AD возвращает исключение недопустимого предоставления. Обычно направляется одно из двух сообщений об ошибке, `invalid_grant` или `interaction_required`.
3. В случае сбоя обмена необходимо запросить согласие. Используйте пользовательский интерфейс, чтобы попросить пользователя приложения предоставить дополнительное согласие. Пользовательский интерфейс должен включать кнопку, которая запускает диалоговое окно согласия Azure AD с помощью [автоматической проверки подлинности](~/concepts/authentication/auth-silent-aad.md).
4. При запросе дополнительного согласия от Azure AD следует включить `prompt=consent` в [query-string-parameter](~/tabs/how-to/authentication/auth-silent-aad.md#get-the-user-context) в Azure AD, иначе Azure AD не запросит другие области.
    - Использование `?prompt=consent&scope={scopes}` вместо `?scope={scopes}`
    - Убедитесь, что `{scopes}` включает все области, которые вы запросили у пользователя, например `Mail.Read` или `User.Read`.
5. После того как пользователь предоставит дополнительные разрешения, попробуйте повторно запустить поток OBO, чтобы получить доступ к другим API.

    </details>

## <a name="see-also"></a>См. также

- [Поток On-Behalf-Of OAuth 2.0](/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow)
- [Получение доступа к MS Graph](/graph/auth-v2-user)
- [Сериализация кэша маркеров в MSAL.NET](/azure/active-directory/develop/msal-net-token-cache-serialization?tabs=aspnet)
- [Поставщик MSAL2 в Microsoft Teams](/graph/toolkit/providers/teams-msal2)
