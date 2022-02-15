---
title: Автоматическая проверка подлинности
description: Описывает бесшумную проверку подлинности, одно-вход, Azure AD для вкладок
ms.topic: conceptual
ms.localizationpriority: medium
keywords: Командная проверка подлинности SSO безмолвная вкладка Azure AD
ms.openlocfilehash: e59b7ff30a0659b670796c56b97eda437f907739
ms.sourcegitcommit: b9af51e24c9befcf46945400789e750c34723e56
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/15/2022
ms.locfileid: "62821572"
---
# <a name="silent-authentication"></a>Автоматическая проверка подлинности

> [!IMPORTANT]
> Поддержка и разработка Microsoft для библиотеки проверки подлинности Active Directory (ADAL), включая исправления безопасности, заканчивается **30 июня 2022 г**. Обновите приложения, чтобы использовать Библиотеку проверки подлинности Microsoft (MSAL), чтобы продолжить получать поддержку. См [. в приложении Migrate to the Microsoft Authentication Library (MSAL)](/azure/active-directory/develop/msal-migration).

> [!NOTE]
> Чтобы проверка подлинности работала для вкладки на мобильных клиентах, убедитесь, что вы используете Teams версии JavaScript SDK 1.4.1 или более поздней версии.

Бесшумная проверка подлинности в Azure AD минимизирует количество случаев ввода учетных данных пользователем путем тихого обновления маркера проверки подлинности. Для верной поддержки единого входного знака см. [документацию по SSO](~/tabs/how-to/authentication/auth-aad-sso.md).

Чтобы сохранить клиентскую сторону кода, используйте библиотеку проверки подлинности [Azure AD](/azure/active-directory/develop/active-directory-authentication-libraries) для JavaScript для получения маркера доступа Microsoft Azure Active Directory Azure AD. Если пользователь недавно подписался, он не видит диалоговое окно всплывающее окно.

Хотя библиотека проверки подлинности Active Directory оптимизирована для приложений AngularJS, она также работает с одно-страницными приложениями JavaScript (SPA).

> [!NOTE]
> В настоящее время бесшумная проверка подлинности работает только для вкладок. Он не работает при входе с бота.

## <a name="how-silent-authentication-works"></a>Как работает бесшумная проверка подлинности

Библиотека проверки подлинности Active Directory создает скрытый поток неявных грантов для OAuth 2.0. Но библиотека указывает, поэтому `prompt=none`Azure AD не отображает страницу входного знака. Взаимодействие с пользователем может потребоваться, если пользователю необходимо войти или предоставить доступ к приложению. При необходимости взаимодействия с пользователем Azure AD возвращает ошибку, которую библиотека сообщает вашему приложению. При необходимости приложение теперь может отображать параметр входной знак.

## <a name="how-to-do-silent-authentication"></a>Как сделать бесшумную проверку подлинности

Код в этой статье поступает из Teams, которое является [Teams проверки подлинности](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/app-auth/nodejs/src/views/tab/silent/silent.hbs).

[Инициализуйте](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group-config-page-auth/csharp) настраиваемую вкладку бесшумной и простой проверки подлинности с помощью Azure AD и выполните инструкции по запуску образца на локальном компьютере.

### <a name="include-and-configure-active-directory-authentication-library"></a>Включить и настроить библиотеку проверки подлинности Active Directory

Включите библиотеку проверки подлинности Active Directory на страницах вкладок и настройте библиотеку с помощью идентификации клиента и URL-адрес перенаправления:

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

На странице контента вкладки позвоните `microsoftTeams.getContext()` , чтобы получить подсказку для текущего пользователя. Подсказка используется в качестве вызова `loginHint` в Azure AD.

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

Если в библиотеке проверки подлинности Active Directory имеется кэширование неиспользваемой маркерной символики для пользователя, используйте маркер. Поочередно вызов `acquireToken(resource, callback)` для получения маркера. Библиотека вызывает функцию вызова с запрашиваемого маркера или создает ошибку в случае сбой проверки подлинности.

Если вы получаете ошибку в функции вызова, отобразить и использовать явный параметр вход.

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

### <a name="process-the-return-value"></a>Обработка возвращаемой стоимости

Библиотека проверки подлинности Active Directory сравниет результат Azure AD `AuthenticationContext.handleWindowCallback(hash)` с помощью вызова на странице вызова для входов.

Убедитесь, что у вас есть допустимый пользователь и позвоните `microsoftTeams.authentication.notifySuccess()` `microsoftTeams.authentication.notifyFailure()` или сообщить о состоянии на главную страницу контента вкладки.

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

### <a name="handle-the-sign-out-flow"></a>Обработка потока регистрации

Используйте следующий код для обработки потока регистрации в проверке подлинности Azure AD:

> [!NOTE]
> При входе из Teams или бота текущий сеанс очищается.

```javascript
function logout() {
localStorage.clear();
window.location.href = "@Url.Action("<<Action Name>>", "<<Controller Name>>")";
}
```

## <a name="see-also"></a>См. также

* [Настройка поставщиков удостоверений для использования Azure AD](../../../concepts/authentication/configure-identity-provider.md)
* [Знать о Библиотеке проверки подлинности Майкрософт (MSAL)](/azure/active-directory/develop/msal-overview)
