---
title: Автоматическая проверка подлинности
description: Описание неавтоматической проверки подлинности
keywords: Служба единого входа для проверки подлинности в Teams AAD
ms.openlocfilehash: b8a5b8cb9328635f5730ca089da29140d0a17ac4
ms.sourcegitcommit: 3fc7ad33e2693f07170c3cb1a0d396261fc5c619
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/29/2020
ms.locfileid: "48796367"
---
# <a name="silent-authentication"></a>Автоматическая проверка подлинности

> [!NOTE]
> Чтобы проверка подлинности работала для вкладки на мобильных клиентах, необходимо убедиться, что используется по крайней мере версия 1.4.1 SDK Teams SDK для Teams.

Автоматическая проверка подлинности в Azure Active Directory (Azure AD) минимизирует число попыток пользователя ввести свои учетные данные для входа, обновляя маркер проверки подлинности без уведомления. (Для поддержки единого входа) ознакомьтесь с [документацией по SSO](~/tabs/how-to/authentication/auth-aad-sso.md).

Если вы хотите, чтобы код полностью оставался на стороне клиента, вы можете использовать [библиотеку проверки подлинности Azure Active Directory](/azure/active-directory/develop/active-directory-authentication-libraries) для JavaScript, чтобы попытаться получить маркер доступа Azure AD. Это означает, что пользователь не видит всплывающее диалоговое окно, если они вошли в последнее время.

Несмотря на то, что библиотека ADAL.js оптимизирована для приложений AngularJS, она также работает с одностраничными приложениями для чистого кода JavaScript.

> [!NOTE]
> В настоящее время автоматическая проверка подлинности работает только для вкладок. Он пока не работает при входе с ленты.

## <a name="how-silent-authentication-works"></a>Как работает автоматическая проверка подлинности

Библиотека ADAL.js создает скрытый элемент iframe для неявного процесса предоставления OAuth 2,0, но он указывает `prompt=none` , что Azure AD никогда не отображает страницу входа. Если требуется вмешательство пользователя, так как пользователь должен войти в приложение или предоставить ему доступ, Azure AD немедленно возвратит ошибку, ADAL.js затем отправит отчет в ваше приложение. На этом шаге приложение может отображать кнопку входа, если это необходимо.

## <a name="how-to-do-silent-authentication"></a>Как выполнять автоматическую проверку подлинности

Код, приведенный в этой статье, взят из примера приложения Microsoft Teams, посвященного [проверке подлинности Microsoft Teams (узел)](https://github.com/OfficeDev/microsoft-teams-sample-complete-node).

### <a name="include-and-configure-adal"></a>Включение и настройка ADAL

Включите библиотеку ADAL.js на вкладки и настройте ADAL с помощью идентификатора клиента и URL-адреса перенаправления:

```html
<script src="https://secure.aadcdn.microsoftonline-p.com/lib/1.0.15/js/adal.min.js" integrity="sha384-lIk8T3uMxKqXQVVfFbiw0K/Nq+kt1P3NtGt/pNexiDby2rKU6xnDY8p16gIwKqgI" crossorigin="anonymous"></script>
<script type="text/javascript">
    // ADAL.js configuration
    let config = {
        clientId: "YOUR_APP_ID_HERE",
        // redirectUri must be in the list of redirect URLs for the Azure AD app
        redirectUri: window.location.origin + "/tab-auth/silent-end",
        cacheLocation: "localStorage",
        navigateToLoginRequestUrl: false,
    };
</script>
```

### <a name="get-the-user-context"></a>Получение контекста пользователя

На странице содержимого вкладки вызовите, `microsoftTeams.getContext()` чтобы получить подсказку о входе для текущего пользователя. Он будет использоваться в качестве login_hint при вызове Azure AD.

```javascript
// Set up extra query parameters for ADAL
// - openid and profile scope adds profile information to the id_token
// - login_hint provides the expected user name
if (loginHint) {
    config.extraQueryParameter = "scope=openid+profile&login_hint=" + encodeURIComponent(loginHint);
} else {
    config.extraQueryParameter = "scope=openid+profile";
}
```

### <a name="authenticate"></a>Проверка подлинности

Если для пользователя ADAL существует кэшированный маркер с истекшим сроком действия, используйте его. В противном случае попытайтесь получить маркер в автоматическом режиме, вызвав метод `acquireToken(resource, callback)` . ADAL.js вызовет функцию обратного вызова с запрошенным маркером или ошибкой в случае сбоя проверки подлинности.

При возникновении ошибки в функции обратного вызова показывать кнопку входа и возвращаться к явному имени входа.

```javascript
let authContext = new AuthenticationContext(config); // from the ADAL.js library
// See if there's a cached user and it matches the expected user
let user = authContext.getCachedUser();
if (user) {
    if (user.profile.oid !== userObjectId) {
        // User doesn't match, clear the cache
        authContext.clearCache();
    }
}

// In this example we are getting an id token (which ADAL.js returns if we ask for resource = clientId)
authContext.acquireToken(config.clientId, function (errDesc, token, err, tokenType) {
    if (token) {
        // Make sure ADAL gave us an id token
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

Разрешите ADAL.js проанализировать результаты из Azure AD, вызвав `AuthenticationContext.handleWindowCallback(hash)` страницу обратного вызова входа.

Убедитесь, что у нас есть действительный пользователь, Звонок `microsoftTeams.authentication.notifySuccess()` или `microsoftTeams.authentication.notifyFailure()` отчет о состоянии, чтобы вернуться на основную страницу содержимого вкладки.

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
