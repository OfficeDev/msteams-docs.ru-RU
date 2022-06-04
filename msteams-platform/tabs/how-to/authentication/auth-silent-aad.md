---
title: Автоматическая проверка подлинности
description: Описывает автоматическую проверку подлинности, процедуру единого входа и Azure AD для вкладок
ms.topic: conceptual
ms.localizationpriority: medium
keywords: Вкладка Azure AD "Единый вход для автоматической проверки подлинности Teams"
ms.openlocfilehash: 8cac439b73884703324d45506bce3600f3084031
ms.sourcegitcommit: e16b51a49756e0fe4eaf239898e28d3021f552da
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/04/2022
ms.locfileid: "65887795"
---
# <a name="silent-authentication"></a>Автоматическая проверка подлинности

> [!IMPORTANT]
> Поддержка и разработка библиотек проверки подлинности Active Directory (ADAL) со стороны Майкрософт, включая исправления в области безопасности, заканчивается **30 июня 2022 г**. Обновите приложения для использования библиотеки проверки подлинности Майкрософт (MSAL), чтобы продолжить получать поддержку. См. [Перенос приложений в библиотеку проверки подлинности Майкрософт (MSAL)](/azure/active-directory/develop/msal-migration).

> [!NOTE]
> Для проверки подлинности на вкладке на мобильных клиентах убедитесь, что вы используете пакет SDK для JavaScript Teams версии 1.4.1 или более поздней.

Автоматическая проверка подлинности в Azure AD минимизирует количество вводов учетных данных пользователем путем незаметного обновления маркера проверки подлинности. Сведения о поддержке единого входа см. в [документации по единому входу](~/tabs/how-to/authentication/tab-sso-overview.md).

Чтобы сохранить код на стороне клиента, используйте [библиотеку проверки подлинности Azure AD](/azure/active-directory/develop/active-directory-authentication-libraries) для JavaScript, чтобы автоматически получить маркер доступа Microsoft Azure Active Directory (Azure AD). Если пользователь недавно выполнил вход, всплывающее диалоговое окно не отображается.

Хотя библиотека проверки подлинности Active Directory оптимизирована для приложений AngularJS, она также работает с одностраничными приложениями (SPA) JavaScript.

> [!NOTE]
> В настоящее время автоматическая проверка подлинности работает только для вкладок. Она не работает при входе из бота.

## <a name="how-silent-authentication-works"></a>Принцип работы автоматической проверки подлинности

Библиотека проверки подлинности Active Directory создает скрытый iframe для потока неявного предоставления OAuth 2.0. При этом библиотека указывает `prompt=none`, так что Azure AD не отображает страницу входа. Взаимодействие с пользователем может потребоваться, если пользователю необходимо войти или предоставить доступ к приложению. Если требуется взаимодействие с пользователем, Azure AD возвращает ошибку, которую библиотека сообщает приложению. При необходимости в приложении теперь можно отобразить параметр входа.

## <a name="how-to-do-silent-authentication"></a>Как выполнить автоматическую проверку подлинности

Код, приведенный в этой статье, получен из примера приложения Teams, которое представляет собой [пример узла проверки подлинности Teams](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/app-auth/nodejs/src/views/tab/silent/silent.hbs).

[Инициируйте автоматическую и простую настраиваемую вкладку проверки подлинности с помощью Azure AD](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group-config-page-auth/csharp) и следуйте инструкциям по запуску примера на вашем локальном компьютере.

### <a name="include-and-configure-active-directory-authentication-library"></a>Включение и настройка библиотеки проверки подлинности Active Directory

Включите библиотеку проверки подлинности Active Directory на страницах вкладок и настройте ее с помощью идентификатора клиента и URL-адреса перенаправления:

```html
<script src="https://secure.aadcdn.microsoftonline-p.com/lib/1.0.15/js/adal.min.js" integrity="sha384-lIk8T3uMxKqXQVVfFbiw0K/Nq+kt1P3NtGt/pNexiDby2rKU6xnDY8p16gIwKqgI" crossorigin="anonymous"></script>
<script type="text/javascript">
    // Active Directory Authentication Library configuration
    let config = {
        clientId: "YOUR_APP_ID_HERE",
        // redirectUri must be in the list of redirect URLs for the Azure AD app
        redirectUri: window.location.origin + "/tab-auth/silent-end",
        cacheLocation: "localStorage",
        navigateToLoginRequestUrl: false,
    };
</script>
```

### <a name="get-the-user-context"></a>Получить пользовательский контекст

На странице содержимого вкладки вызовите `microsoftTeams.getContext()`, чтобы получить подсказку для входа для текущего пользователя. Подсказка используется в качестве `loginHint` в вызове Azure AD.

```javascript
// Set up extra query parameters for Active Directory Authentication Library
// - openid and profile scope adds profile information to the id_token
// - login_hint provides the expected user name
if (loginHint) {
    config.extraQueryParameter = "scope=openid+profile&login_hint=" + encodeURIComponent(loginHint);
} else {
    config.extraQueryParameter = "scope=openid+profile";
}
```

### <a name="authenticate"></a>Проверка подлинности

Если в библиотеке проверки подлинности Active Directory есть неиспользуемый маркер, кэшированный для пользователя, используйте этот маркер. Как вариант, вызовите `acquireToken(resource, callback)` для автоматического получения маркера. Библиотека вызывает функцию обратного вызова с запрошенным маркером или создает ошибку в случае сбоя проверки подлинности.

Если в функции обратного вызова возникает ошибка, отобразите и используйте параметр явного входа.

```javascript
let authContext = new AuthenticationContext(config); // from Active Directory Authentication Library
// See if there is a cached user and it matches the expected user
let user = authContext.getCachedUser();
if (user) {
    if (user.profile.oid !== userObjectId) {
        // User doesn't match, clear the cache
        authContext.clearCache();
    }
}

// In this example we are getting an id token (which Active Directory Authentication Library returns if we ask for resource = clientId)
authContext.acquireToken(config.clientId, function (errDesc, token, err, tokenType) {
    if (token) {
        // Make sure Active Directory Authentication Library gave us an ID token
        if (tokenType !== authContext.CONSTANTS.ID_TOKEN) {
            token = authContext.getCachedToken(config.clientId);
        }
        showProfileInformation(idToken);
    } else {
        console.log("Renewal failed: " + err);
        // Failed to get the token silently; show the login button
        showLoginButton();
        // You could attempt to launch the login popup here, but in browsers this could be blocked by
        // a popup blocker, in which case the login attempt will fail with the reason FailedToOpenWindow.
    }
});
```

### <a name="process-the-return-value"></a>Обработка возвращаемого значения

Библиотека проверки подлинности Active Directory анализирует результат Azure AD путем вызова `AuthenticationContext.handleWindowCallback(hash)` на странице обратного вызова для входа.

Убедитесь, что у вас есть подходящий пользователь, и вызовите `microsoftTeams.authentication.notifySuccess()` или `microsoftTeams.authentication.notifyFailure()`, чтобы сообщить о состоянии на главной странице содержимого вкладки.

```javascript
if (authContext.isCallback(window.location.hash)) {
    authContext.handleWindowCallback(window.location.hash);
    if (window.parent === window) {
        if (authContext.getCachedUser()) {
            microsoftTeams.authentication.notifySuccess();
        } else {
            microsoftTeams.authentication.notifyFailure(authContext.getLoginError());
        }
    }
}
```

### <a name="handle-the-sign-out-flow"></a>Обработка потока выходов

Используйте следующий код для обработки потока выходов при проверке подлинности Azure AD:

> [!NOTE]
> При выходе из вкладки Teams или из бота текущий сеанс сбрасывается.

```javascript
function logout() {
localStorage.clear();
window.location.href = "@Url.Action("<<Action Name>>", "<<Controller Name>>")";
}
```

## <a name="see-also"></a>Дополнительные ресурсы

* [Настройка поставщиков удостоверений для использования Azure AD](../../../concepts/authentication/configure-identity-provider.md)
* [Сведения о библиотеке проверки подлинности Майкрософт (MSAL)](/azure/active-directory/develop/msal-overview)
