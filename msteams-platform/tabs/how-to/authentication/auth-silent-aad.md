---
title: Автоматическая проверка подлинности
description: Описание проверки подлинности без проверки подлинности
ms.topic: conceptual
keywords: AAD для проверки подлинности teams без проверки подлинности
ms.openlocfilehash: e55e415aba08fdedf4409abf39115838c3a5faf0
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014098"
---
# <a name="silent-authentication"></a>Автоматическая проверка подлинности

> [!NOTE]
> Чтобы проверка подлинности работала для вашей вкладки на мобильных клиентах, необходимо убедиться, что вы используете по крайней мере версию 1.4.1 SDK JavaScript для Teams.

Автоматический режим проверки подлинности в Azure Active Directory (Azure AD) сводит к минимуму количество случаев, когда пользователю необходимо ввести свои учетные данные для входа, автоматически обновив маркер проверки подлинности. (Для поддержки единого входов см. документацию по [единому входу)](~/tabs/how-to/authentication/auth-aad-sso.md)

Если вы хотите сохранить код полностью на стороне клиента, вы можете использовать библиотеку проверки подлинности [Azure Active Directory](/azure/active-directory/develop/active-directory-authentication-libraries) для JavaScript, чтобы попытаться получить маркер доступа Azure AD в тихом режиме. Это означает, что пользователь может никогда не видеть всплывающее диалоговое окно, если он недавно вступ в нее.

Хотя библиотека ADAL.js оптимизирована для приложений AngularJS, она также работает с одно page-приложениями JavaScript.

> [!NOTE]
> В настоящее время проверка подлинности без проверки подлинности работает только для вкладок. Он пока не работает при входе от бота.

## <a name="how-silent-authentication-works"></a>Как работает проверка подлинности без проверки подлинности

Библиотека ADAL.js создает скрытый iframe для неявного потока предоставления OAuth 2.0, но указывает, что Azure AD никогда не отображает страницу `prompt=none` входа. Если требуется взаимодействие с пользователем, так как пользователю необходимо войти в приложение или предоставить доступ к нему, Azure AD немедленно возвратит ошибку, ADAL.js затем сообщает приложению. На этом этапе ваше приложение может при необходимости показать кнопку входа.

## <a name="how-to-do-silent-authentication"></a>Как сделать проверку подлинности без проверки подлинности

Код в этой статье взят из примера приложения [Microsoft Teams Authentication Sample (Node).](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)

### <a name="include-and-configure-adal"></a>включить и настроить ADAL

Включите библиотеку ADAL.js на страницах вкладок и настройте ADAL с помощью своего ИД клиента и URL-адреса перенаправления:

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

### <a name="get-the-user-context"></a>Получить контекст пользователя

На странице содержимого вкладки вызовите, чтобы получить подсказку для входа `microsoftTeams.getContext()` для текущего пользователя. Он будет использоваться в качестве login_hint в вызове Azure AD.

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

Если В ADAL для пользователя кэшировали неиспользваваемый маркер, используйте его. В противном случае попытайтесь получить маркер без `acquireToken(resource, callback)` вызова. ADAL.js вызов функции вызова с помощью запрашиваемого маркера или ошибку при сбойе проверки подлинности.

Если в функции обратного вызова произошла ошибка, откажите кнопку входа и вернемся к явному входу.

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

### <a name="process-the-return-value"></a>Обработка возвращаемой стоимости

Let ADAL.js take care of parsing the result from Azure AD by calling `AuthenticationContext.handleWindowCallback(hash)` in the login callback page.

Убедитесь, что у нас есть допустимый пользователь, и позвоните или вернем отчет о состоянии на `microsoftTeams.authentication.notifySuccess()` `microsoftTeams.authentication.notifyFailure()` главную страницу содержимого вкладки.

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
