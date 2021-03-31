---
title: Автоматическая проверка подлинности
description: Описание бесшумной проверки подлинности
ms.topic: conceptual
keywords: группы проверки подлинности SSO silent AAD
ms.openlocfilehash: 7a68c532cadf181b15c16d6bc4d4ab861d5c9922
ms.sourcegitcommit: 2bf651dfbaf5dbab6d466788f668e7a6c5d69c36
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/30/2021
ms.locfileid: "51421610"
---
# <a name="silent-authentication"></a>Автоматическая проверка подлинности

> [!NOTE]
> Чтобы проверка подлинности работала для вкладки на мобильных клиентах, убедитесь, что вы используете по крайней мере версию 1.4.1 SDK Teams JavaScript.

Бесшумная проверка подлинности в Azure Active Directory (AAD) минимизирует количество случаев, когда пользователь вводит свой вход в учетные данные, молча освежая маркер проверки подлинности. Для верной поддержки единого входного знака см. [документацию по SSO.](~/tabs/how-to/authentication/auth-aad-sso.md)

Если вы хотите сохранить код полностью клиентской стороной, вы можете использовать библиотеку проверки подлинности [AAD](/azure/active-directory/develop/active-directory-authentication-libraries) для JavaScript, чтобы получить маркер доступа AAD безмолвно. Если пользователь недавно подписался, он никогда не увидит диалоговое окно всплывающее окно.

Несмотря на тоADAL.js что библиотека оптимизирована для приложений AngularJS, она также работает с чистыми одно-страницами JavaScript.

> [!NOTE]
> В настоящее время бесшумная проверка подлинности работает только для вкладок. Он не работает при входе с бота.

## <a name="how-silent-authentication-works"></a>Как работает бесшумная проверка подлинности

Библиотека ADAL.js создает скрытый поток неявных грантов для OAuth 2.0. Но библиотека указывает, поэтому Azure AD никогда `prompt=none` не показывает знак на странице. Если требуется взаимодействие с пользователем, так как пользователю необходимо войти или предоставить доступ к приложению, AAD немедленно возвращает ошибку, ADAL.js отчеты в ваше приложение. На этом этапе приложение может при необходимости показать вход в кнопку.

## <a name="how-to-do-silent-authentication"></a>Как сделать бесшумную проверку подлинности

Код в этой статье происходит из примера приложения Teams, которое является узлом [проверки подлинности Teams.](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/app-auth/nodejs/src/views/tab/silent/silent.hbs)

[Инициировать бесшумную](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group-config-page-auth/csharp) и простую настраиваемую вкладку проверки подлинности с помощью AAD и следуйте инструкциям по запуску образца на локальном компьютере.

### <a name="include-and-configure-adal"></a>Включить и настроить ADAL

Включите библиотеку ADAL.js на страницах вкладок и настройте ADAL с вашим клиентом ИД и URL-адресом перенаправления:

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

### <a name="get-the-user-context"></a>Получить пользовательский контекст

На странице контента вкладки позвоните, чтобы получить подсказку `microsoftTeams.getContext()` для текущего пользователя. Это используется в качестве входаHint в вызове в AAD.

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

Если ADAL кэшировали маркер для пользователя, срок действия которого не истек, используйте этот маркер. Кроме того, попытаться получить маркер молча, позвонив `acquireToken(resource, callback)` . ADAL.js вызывает функцию вызова с запрашиваемого маркера или дает ошибку в случае сбой проверки подлинности.

Если вы получаете ошибку в функции обратного вызова, покажите вход в кнопку и откажитесь от явного входного знака.

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

ADAL.js для размыва результатов AAD путем вызова в `AuthenticationContext.handleWindowCallback(hash)` знаке на странице вызова.

Убедитесь, что у вас есть допустимый пользователь и позвоните или сообщить о состоянии на главную страницу `microsoftTeams.authentication.notifySuccess()` `microsoftTeams.authentication.notifyFailure()` контента вкладки.

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

### <a name="handle-sign-out-flow"></a>Обработка потока регистрации

Используйте следующий код для обработки потока регистрации в AAD Auth:

> [!NOTE]
> Несмотря на то, что вход для вкладки или бота Teams будет сделан, текущий сеанс также очищается.

```javascript
function logout() {
localStorage.clear();
window.location.href = "@Url.Action("<<Action Name>>", "<<Controller Name>>")";
}
```
