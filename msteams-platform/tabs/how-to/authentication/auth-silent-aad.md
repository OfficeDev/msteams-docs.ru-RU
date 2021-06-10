---
title: Автоматическая проверка подлинности
description: Описание бесшумной проверки подлинности
ms.topic: conceptual
localization_priority: Normal
keywords: группы проверки подлинности SSO silent AAD
ms.openlocfilehash: 0c75c6d50fd1191b6ea8548d65c9df4ce8453898
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019603"
---
# <a name="silent-authentication"></a><span data-ttu-id="3abe9-104">Автоматическая проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="3abe9-104">Silent authentication</span></span>

> [!NOTE]
> <span data-ttu-id="3abe9-105">Для проверки подлинности для работы вкладки на мобильных клиентах убедитесь, что вы используете по крайней мере 1.4.1 версию Teams JavaScript SDK.</span><span class="sxs-lookup"><span data-stu-id="3abe9-105">For authentication to work for your tab on mobile clients, ensure you are using at least 1.4.1 version of the Teams JavaScript SDK.</span></span>

<span data-ttu-id="3abe9-106">Бесшумная проверка подлинности в Azure Active Directory (AAD) минимизирует количество случаев, когда пользователь вводит свой вход в учетные данные, молча освежая маркер проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="3abe9-106">Silent authentication in Azure Active Directory (AAD) minimizes the number of times a user enters their sign in credentials by silently refreshing the authentication token.</span></span> <span data-ttu-id="3abe9-107">Для верной поддержки единого входного знака см. [документацию по SSO.](~/tabs/how-to/authentication/auth-aad-sso.md)</span><span class="sxs-lookup"><span data-stu-id="3abe9-107">For true single sign-on support, see [SSO documentation](~/tabs/how-to/authentication/auth-aad-sso.md).</span></span>

<span data-ttu-id="3abe9-108">Если вы хотите сохранить код полностью клиентской стороной, вы можете использовать библиотеку проверки подлинности [AAD](/azure/active-directory/develop/active-directory-authentication-libraries) для JavaScript, чтобы получить маркер доступа AAD безмолвно.</span><span class="sxs-lookup"><span data-stu-id="3abe9-108">If you want to keep your code completely client-side, you can use the [AAD authentication library](/azure/active-directory/develop/active-directory-authentication-libraries) for JavaScript to get an AAD access token silently.</span></span> <span data-ttu-id="3abe9-109">Если пользователь недавно подписался, он никогда не увидит диалоговое окно всплывающее окно.</span><span class="sxs-lookup"><span data-stu-id="3abe9-109">If the user has signed in recently, they never see a popup dialog box.</span></span>

<span data-ttu-id="3abe9-110">Несмотря на тоADAL.js что библиотека оптимизирована для приложений AngularJS, она также работает с чистыми одно-страницами JavaScript.</span><span class="sxs-lookup"><span data-stu-id="3abe9-110">Even though the ADAL.js library is optimized for AngularJS applications, it also works with pure JavaScript single-page applications.</span></span>

> [!NOTE]
> <span data-ttu-id="3abe9-111">В настоящее время бесшумная проверка подлинности работает только для вкладок.</span><span class="sxs-lookup"><span data-stu-id="3abe9-111">Currently, silent authentication only works for tabs.</span></span> <span data-ttu-id="3abe9-112">Он не работает при входе с бота.</span><span class="sxs-lookup"><span data-stu-id="3abe9-112">It does not work when signing in from a bot.</span></span>

## <a name="how-silent-authentication-works"></a><span data-ttu-id="3abe9-113">Как работает бесшумная проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="3abe9-113">How silent authentication works</span></span>

<span data-ttu-id="3abe9-114">Библиотека ADAL.js создает скрытый поток неявных грантов для OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="3abe9-114">The ADAL.js library creates a hidden iframe for OAuth 2.0 implicit grant flow.</span></span> <span data-ttu-id="3abe9-115">Но библиотека указывает, поэтому Azure AD никогда `prompt=none` не показывает знак на странице.</span><span class="sxs-lookup"><span data-stu-id="3abe9-115">But the library specifies `prompt=none`, so Azure AD never shows the sign in page.</span></span> <span data-ttu-id="3abe9-116">Если требуется взаимодействие с пользователем, так как пользователю необходимо войти или предоставить доступ к приложению, AAD немедленно возвращает ошибку, ADAL.js отчеты в ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="3abe9-116">If user interaction is required because the user needs to sign in or grant access to the application, AAD immediately returns an error that ADAL.js reports to your app.</span></span> <span data-ttu-id="3abe9-117">На этом этапе приложение может при необходимости показать вход в кнопку.</span><span class="sxs-lookup"><span data-stu-id="3abe9-117">At this point your app can show a sign in button if required.</span></span>

## <a name="how-to-do-silent-authentication"></a><span data-ttu-id="3abe9-118">Как сделать бесшумную проверку подлинности</span><span class="sxs-lookup"><span data-stu-id="3abe9-118">How to do silent authentication</span></span>

<span data-ttu-id="3abe9-119">Код в этой статье поступает из Teams, которое является Teams проверки [подлинности.](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/app-auth/nodejs/src/views/tab/silent/silent.hbs)</span><span class="sxs-lookup"><span data-stu-id="3abe9-119">The code in this article comes from the Teams sample app that is [Teams authentication sample node](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/app-auth/nodejs/src/views/tab/silent/silent.hbs).</span></span>

<span data-ttu-id="3abe9-120">[Инициировать бесшумную](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group-config-page-auth/csharp) и простую настраиваемую вкладку проверки подлинности с помощью AAD и следуйте инструкциям по запуску образца на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="3abe9-120">[Initiate silent and simple authentication configurable tab using AAD](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group-config-page-auth/csharp) and follow the instructions to run the sample on your local machine.</span></span>

### <a name="include-and-configure-adal"></a><span data-ttu-id="3abe9-121">Включить и настроить ADAL</span><span class="sxs-lookup"><span data-stu-id="3abe9-121">Include and configure ADAL</span></span>

<span data-ttu-id="3abe9-122">Включите библиотеку ADAL.js на страницах вкладок и настройте ADAL с вашим клиентом ИД и URL-адресом перенаправления:</span><span class="sxs-lookup"><span data-stu-id="3abe9-122">Include the ADAL.js library in your tab pages and configure ADAL with your client ID and redirect URL:</span></span>

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

### <a name="get-the-user-context"></a><span data-ttu-id="3abe9-123">Получить пользовательский контекст</span><span class="sxs-lookup"><span data-stu-id="3abe9-123">Get the user context</span></span>

<span data-ttu-id="3abe9-124">На странице контента вкладки позвоните, чтобы получить подсказку `microsoftTeams.getContext()` для текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="3abe9-124">In the tab's content page, call `microsoftTeams.getContext()` to get a sign in hint for the current user.</span></span> <span data-ttu-id="3abe9-125">Это используется в качестве входаHint в вызове в AAD.</span><span class="sxs-lookup"><span data-stu-id="3abe9-125">This is used as a loginHint in the call to AAD.</span></span>

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

### <a name="authenticate"></a><span data-ttu-id="3abe9-126">Проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="3abe9-126">Authenticate</span></span>

<span data-ttu-id="3abe9-127">Если ADAL кэшировали маркер для пользователя, срок действия которого не истек, используйте этот маркер.</span><span class="sxs-lookup"><span data-stu-id="3abe9-127">If ADAL has a token cached for the user that has not expired, use that token.</span></span> <span data-ttu-id="3abe9-128">Кроме того, попытаться получить маркер молча, позвонив `acquireToken(resource, callback)` .</span><span class="sxs-lookup"><span data-stu-id="3abe9-128">Alternately, attempt to get a token silently by calling `acquireToken(resource, callback)`.</span></span> <span data-ttu-id="3abe9-129">ADAL.js вызывает функцию вызова с запрашиваемого маркера или дает ошибку в случае сбой проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="3abe9-129">ADAL.js calls the callback function with the requested token, or gives an error if authentication fails.</span></span>

<span data-ttu-id="3abe9-130">Если вы получаете ошибку в функции обратного вызова, покажите вход в кнопку и откажитесь от явного входного знака.</span><span class="sxs-lookup"><span data-stu-id="3abe9-130">If you get an error in the callback function, show a sign in button and fall back to an explicit sign in.</span></span>

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

### <a name="process-the-return-value"></a><span data-ttu-id="3abe9-131">Обработка возвращаемой стоимости</span><span class="sxs-lookup"><span data-stu-id="3abe9-131">Process the return value</span></span>

<span data-ttu-id="3abe9-132">ADAL.js для размыва результатов AAD путем вызова в `AuthenticationContext.handleWindowCallback(hash)` знаке на странице вызова.</span><span class="sxs-lookup"><span data-stu-id="3abe9-132">ADAL.js parses the result from AAD by calling `AuthenticationContext.handleWindowCallback(hash)` in the sign in callback page.</span></span>

<span data-ttu-id="3abe9-133">Убедитесь, что у вас есть допустимый пользователь и позвоните или сообщить о состоянии на главную страницу `microsoftTeams.authentication.notifySuccess()` `microsoftTeams.authentication.notifyFailure()` контента вкладки.</span><span class="sxs-lookup"><span data-stu-id="3abe9-133">Check that you have a valid user and call `microsoftTeams.authentication.notifySuccess()` or `microsoftTeams.authentication.notifyFailure()` to report the status to your main tab content page.</span></span>

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

### <a name="handle-sign-out-flow"></a><span data-ttu-id="3abe9-134">Обработка потока регистрации</span><span class="sxs-lookup"><span data-stu-id="3abe9-134">Handle sign out flow</span></span>

<span data-ttu-id="3abe9-135">Используйте следующий код для обработки потока регистрации в AAD Auth:</span><span class="sxs-lookup"><span data-stu-id="3abe9-135">Use the following code to handle sign out flow in AAD Auth:</span></span>

> [!NOTE]
> <span data-ttu-id="3abe9-136">Несмотря на то, что Teams для вкладки или бота, текущий сеанс также очищается.</span><span class="sxs-lookup"><span data-stu-id="3abe9-136">While logout for Teams tab or bot is done, the current session is also cleared.</span></span>

```javascript
function logout() {
localStorage.clear();
window.location.href = "@Url.Action("<<Action Name>>", "<<Controller Name>>")";
}
```
