---
title: Расширение приложения табуляции с помощью разрешений Microsoft Graph
description: Сведения о настройке разрешений API с помощью Microsoft Graph
ms.topic: how-to
ms.localizationpriority: medium
keywords: Вкладки проверки подлинности teams Microsoft Azure Active Directory (Azure AD) API Graph области маркера делегированного доступа к разрешениям
ms.openlocfilehash: 474d02c5b5f90e58bfc57f72ab6ce095a0323b62
ms.sourcegitcommit: c398dfdae9ed96f12e1401ac7c8d0228ff9c0a2b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/30/2022
ms.locfileid: "66558256"
---
# <a name="extend-tab-app-with-microsoft-graph-permissions-and-scope"></a>Расширение приложения табуляции с помощью разрешений и области Microsoft Graph

Вы можете расширить приложение вкладки с помощью Microsoft Graph, чтобы предоставить пользователям дополнительные разрешения, такие как просмотр профиля пользователя приложения, чтение почты и т. д. Ваше приложение должно запрашивать определенные области разрешений для получения маркеров доступа на согласие пользователя приложения.

Области графа, например `User.Read` или `Mail.Read`, позволяют указать, как приложение получает доступ к учетной записи пользователя Teams. Необходимо указать области в запросе авторизации.

В этом разделе вы научитесь:

- [Настройка разрешений API в Azure AD](#configure-api-permissions-in-azure-ad)
- [Настройка проверки подлинности для разных платформ](#configure-authentication-for-different-platforms)
- [Получение маркера доступа для MS Graph](#acquire-access-token-for-ms-graph)

## <a name="configure-api-permissions-in-azure-ad"></a>Настройка разрешений API в Azure AD

Вы можете настроить дополнительные области Graph в Azure AD приложения. Это делегированные разрешения, которые используются приложениями, которым требуется доступ для входа. Пользователь или администратор приложения, выполнившего вход, должен дать ему согласие. Приложение вкладки может дать согласие от имени вошедвшего пользователя при вызове Microsoft Graph.

### <a name="to-configure-api-permissions"></a>Настройка разрешений API

1. Откройте приложение, зарегистрированное [в портал Azure.](https://ms.portal.azure.com/)

2. Выберите **разрешение "** > **Управление API"** на левой панели.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/api-permission-menu.png" alt-text="Пункт меню разрешений приложения.":::

    **Появится страница разрешений API**.

3. Выберите **"+ Добавить разрешения"**, чтобы добавить API Graph Майкрософт.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/app-permission.png" alt-text="Страница разрешений приложения.":::

    **Появится страница разрешений API запросов**.

4. Выберите **Microsoft Graph**.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/request-api-permission.png" alt-text="Страница &quot;Запрос разрешений API&quot;.":::

    Отображаются параметры разрешений Graph.

5. Выберите **"Делегированные разрешения** ", чтобы просмотреть список разрешений.

   :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/delegated-permission.png" alt-text="Делегированные разрешения.":::

6. Выберите соответствующие разрешения для приложения, а затем нажмите кнопку **"Добавить разрешения"**.

   :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/select-permission.png" alt-text="Выберите разрешения.":::

    Вы также можете ввести имя разрешения в поле поиска, чтобы найти его.

    В браузере отображается сообщение об обновлении разрешений.

   :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/updated-permission-msg.png" alt-text="Обновленное сообщение о разрешениях.":::

    Добавленные разрешения отображаются на странице **разрешений API** .

   :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/configured-permissions.png" alt-text="Настроены разрешения API.":::

    Вы настроите приложение с разрешениями Microsoft Graph.

## <a name="configure-authentication-for-different-platforms"></a>Настройка проверки подлинности для разных платформ

В зависимости от платформы или устройства, на которых вы хотите нацелить приложение, может потребоваться дополнительная настройка, например URI перенаправления, определенные параметры проверки подлинности или сведения, относящиеся к платформе.

> [!NOTE]
>
> - Если приложению табуляции не предоставлено согласие ИТ-администратора, пользователи приложения должны предоставить согласие при первом использовании приложения на другой платформе.
> - Неявное предоставление не требуется, если единый вход включен в приложении табуляции.

Вы можете настроить проверку подлинности для нескольких платформ, если URL-адрес уникален.

### <a name="to-configure-authentication-for-a-platform"></a>Настройка проверки подлинности для платформы

1. Откройте приложение, зарегистрированное в [портал Azure.](https://ms.portal.azure.com/)

1. Выберите **"Управление** > **проверкой подлинности** " на левой панели.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/azure-portal-platform.png" alt-text="Проверка подлинности для платформ":::

    **Появится страница "Конфигурации платформы**".

1. Выберите **+Добавить платформу**.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/add-platform.png" alt-text="Добавление платформ":::

    **Появится страница "Настройка платформ**".

1. Выберите платформу, которую вы хотите настроить для приложения вкладки. Вы можете выбрать тип платформы в Интернете или SPA.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/configure-platform.png" alt-text="Выбор веб-платформы":::

    Можно настроить несколько платформ для определенного типа платформы. Убедитесь, что URI перенаправления уникален для каждой настраиваемой платформы.

    Появится веб-страница "Настройка".

    > [!NOTE]
    > Конфигурации будут отличаться в зависимости от выбранной платформы.

1. Введите сведения о конфигурации платформы.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/config-web-platform.png" alt-text="Настройка веб-платформы":::

    1. Введите URI перенаправления. Универсальный код ресурса (URI) должен быть уникальным.
    2. Введите URL-адрес выхода из внешнего канала.
    3. Выберите маркеры, которые Azure AD отправить для вашего приложения.

1. Нажмите **Настроить**.

    Платформа настраивается и отображается на странице **"Конфигурации платформы** ".

## <a name="acquire-access-token-for-ms-graph"></a>Получение маркера доступа для MS Graph

Вам потребуется получить маркер доступа для Microsoft Graph. Это можно сделать с помощью Azure AD OBO.

Текущая реализация единого входа предоставляет согласие только на разрешения на уровне пользователя, которые не могут использоваться для вызовов Graph. Чтобы получить разрешения (области), необходимые для вызова Graph, приложения единого входа должны реализовать пользовательскую веб-службу для обмена маркера, полученного из пакета SDK JavaScript для Teams, на маркер, который включает необходимые области. Для получения маркера со стороны клиента можно использовать библиотеку проверки подлинности Майкрософт (MSAL).

После настройки разрешений Graph в Azure AD:

- [Настройка клиентского кода для получения маркера доступа с помощью MSAL](#configure-code-to-fetch-access-token-using-msal)
- [Передача маркера доступа серверному коду](#pass-the-access-token-to-server-side-code)

### <a name="configure-code-to-fetch-access-token-using-msal"></a>Настройка кода для получения маркера доступа с помощью MSAL

В следующем коде приведен пример потока OBO для получения маркера доступа из клиента Teams с помощью MSAL.

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

Если вам нужен доступ к данным Microsoft Graph, настройте код на стороне сервера, чтобы:

1. Проверьте маркер доступа. Дополнительные сведения см. в разделе [Проверка маркера доступа](tab-sso-code.md#validate-the-access-token);
1. Инициируйте поток OBO OAuth 2.0 с помощью вызова платформа удостоверений Майкрософт, который включает маркер доступа, некоторые метаданные о пользователе и учетные данные приложения вкладки (идентификатор приложения и секрет клиента). Платформа удостоверений Майкрософт вернет новый маркер доступа, который можно использовать для доступа к Microsoft Graph.
1. Получение данных из Microsoft Graph с помощью нового маркера.
1. Используйте сериализацию кэша маркеров в MSAL.NET кэшировать новый маркер доступа для нескольких, если это необходимо.

> [!IMPORTANT]
> Для обеспечения безопасности всегда используйте серверный код для выполнения вызовов Microsoft Graph или других вызовов, которые требуют передачи маркера доступа. Никогда не возвращайте маркер OBO клиенту, чтобы клиент мог выполнять прямые вызовы в Microsoft Graph. Это помогает защитить маркер от перехвата или утечки.

## <a name="known-limitations"></a>Известные ограничения

Согласие администратора клиента. Простой способ предоставления [](/azure/active-directory/manage-apps/consent-and-permissions-overview#admin-consent) согласия от имени организации в качестве администратора клиента — получить [согласие от администратора](/azure/active-directory/manage-apps/grant-admin-consent).

Вы можете запросить согласие с помощью API проверки подлинности. Другой подход для получения областей Graph — предоставить диалоговое окно согласия с использованием существующего подхода проверки подлинности стороннего поставщика [OAuth](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-pop-up-page). Этот подход включает в себя отображение всплывающего диалогового окна Azure AD для получения согласия.

<details>
<summary>Чтобы запросить дополнительное согласие с помощью API Auth, выполните следующие действия.</summary>

1. Полученный с `getAuthToken()` помощью маркера маркер должен быть обменяться на стороне сервера с помощью Azure AD [](/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow) потока "от имени", чтобы получить доступ к этим другим API Graph. Убедитесь, что для этого обмена вы используете конечную точку Graph v2.
2. В случае ошибки обмена Azure AD возвращает исключение недопустимого предоставления. Обычно он отвечает одним из двух сообщений об ошибке или `invalid_grant` `interaction_required`.
3. В случае сбоя обмена необходимо запросить согласие. Используйте пользовательский интерфейс, чтобы попросить пользователя приложения предоставить другое согласие. Этот пользовательский интерфейс должен включать кнопку, которая активирует диалоговое окно Azure AD с использованием [автоматической проверки подлинности](~/concepts/authentication/auth-silent-aad.md).
4. При запросе `prompt=consent` дополнительного согласия от Azure AD необходимо включить в параметр [query-string для](~/tabs/how-to/authentication/auth-silent-aad.md#get-the-user-context) Azure AD, в противном случае Azure AD не будет запрашивать другие области.
    - Вместо этого используйте `?scope={scopes}``?prompt=consent&scope={scopes}`
    - Убедитесь `{scopes}` , что включены все области, для которых вы запрашиваете у пользователя, например, `Mail.Read` или `User.Read`.
5. После того как пользователь приложения предоставил дополнительные разрешения, повторите попытку потока OBO, чтобы получить доступ к этим другим API.

    </details>

## <a name="see-also"></a>См. также

- [Поток On-Behalf-Of OAuth 2.0](/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow)
- [Получение доступа для MS Graph](/graph/auth-v2-user)
- [Сериализация кэша маркеров в MSAL.NET](/azure/active-directory/develop/msal-net-token-cache-serialization?tabs=aspnet)
- [Поставщик Microsoft Teams MSAL2](/graph/toolkit/providers/teams-msal2)
