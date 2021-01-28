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
# <a name="silent-authentication"></a><span data-ttu-id="f49df-104">Автоматическая проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="f49df-104">Silent authentication</span></span>

> [!NOTE]
> <span data-ttu-id="f49df-105">Чтобы проверка подлинности работала для вашей вкладки на мобильных клиентах, необходимо убедиться, что вы используете по крайней мере версию 1.4.1 SDK JavaScript для Teams.</span><span class="sxs-lookup"><span data-stu-id="f49df-105">For authentication to work for your tab on mobile clients, you need to ensure you're using at least the 1.4.1 version of the Teams JavaScript SDK.</span></span>

<span data-ttu-id="f49df-106">Автоматический режим проверки подлинности в Azure Active Directory (Azure AD) сводит к минимуму количество случаев, когда пользователю необходимо ввести свои учетные данные для входа, автоматически обновив маркер проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="f49df-106">Silent authentication in Azure Active Directory (Azure AD) minimizes the number of times a user needs to enter their login credentials by silently refreshing the authentication token.</span></span> <span data-ttu-id="f49df-107">(Для поддержки единого входов см. документацию по [единому входу)](~/tabs/how-to/authentication/auth-aad-sso.md)</span><span class="sxs-lookup"><span data-stu-id="f49df-107">(For true single sign-on support, view our [SSO Documentation](~/tabs/how-to/authentication/auth-aad-sso.md))</span></span>

<span data-ttu-id="f49df-108">Если вы хотите сохранить код полностью на стороне клиента, вы можете использовать библиотеку проверки подлинности [Azure Active Directory](/azure/active-directory/develop/active-directory-authentication-libraries) для JavaScript, чтобы попытаться получить маркер доступа Azure AD в тихом режиме.</span><span class="sxs-lookup"><span data-stu-id="f49df-108">If you want to keep your code completely client-side, you can use the [Azure Active Directory Authentication Library](/azure/active-directory/develop/active-directory-authentication-libraries) for JavaScript to attempt to acquire an Azure AD access token silently.</span></span> <span data-ttu-id="f49df-109">Это означает, что пользователь может никогда не видеть всплывающее диалоговое окно, если он недавно вступ в нее.</span><span class="sxs-lookup"><span data-stu-id="f49df-109">This means that the user may never see a popup dialog if they have signed in recently.</span></span>

<span data-ttu-id="f49df-110">Хотя библиотека ADAL.js оптимизирована для приложений AngularJS, она также работает с одно page-приложениями JavaScript.</span><span class="sxs-lookup"><span data-stu-id="f49df-110">Even though the ADAL.js library is optimized for AngularJS applications, it also works with pure JavaScript single-page applications.</span></span>

> [!NOTE]
> <span data-ttu-id="f49df-111">В настоящее время проверка подлинности без проверки подлинности работает только для вкладок.</span><span class="sxs-lookup"><span data-stu-id="f49df-111">Currently, silent authentication only works for tabs.</span></span> <span data-ttu-id="f49df-112">Он пока не работает при входе от бота.</span><span class="sxs-lookup"><span data-stu-id="f49df-112">It does not yet work when signing in from a bot.</span></span>

## <a name="how-silent-authentication-works"></a><span data-ttu-id="f49df-113">Как работает проверка подлинности без проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="f49df-113">How silent authentication works</span></span>

<span data-ttu-id="f49df-114">Библиотека ADAL.js создает скрытый iframe для неявного потока предоставления OAuth 2.0, но указывает, что Azure AD никогда не отображает страницу `prompt=none` входа.</span><span class="sxs-lookup"><span data-stu-id="f49df-114">The ADAL.js library creates a hidden iframe for OAuth 2.0 implicit grant flow, but it specifies `prompt=none` so that Azure AD never shows the login page.</span></span> <span data-ttu-id="f49df-115">Если требуется взаимодействие с пользователем, так как пользователю необходимо войти в приложение или предоставить доступ к нему, Azure AD немедленно возвратит ошибку, ADAL.js затем сообщает приложению.</span><span class="sxs-lookup"><span data-stu-id="f49df-115">If user interaction is required because the user needs to log in or grant access to the application, Azure AD will immediately return an error that ADAL.js then reports to your app.</span></span> <span data-ttu-id="f49df-116">На этом этапе ваше приложение может при необходимости показать кнопку входа.</span><span class="sxs-lookup"><span data-stu-id="f49df-116">At this point your app can show a login button if needed.</span></span>

## <a name="how-to-do-silent-authentication"></a><span data-ttu-id="f49df-117">Как сделать проверку подлинности без проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="f49df-117">How to do silent authentication</span></span>

<span data-ttu-id="f49df-118">Код в этой статье взят из примера приложения [Microsoft Teams Authentication Sample (Node).](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)</span><span class="sxs-lookup"><span data-stu-id="f49df-118">The code in this article comes from the Teams sample app [Microsoft Teams Authentication Sample (Node)](https://github.com/OfficeDev/microsoft-teams-sample-complete-node).</span></span>

### <a name="include-and-configure-adal"></a><span data-ttu-id="f49df-119">включить и настроить ADAL</span><span class="sxs-lookup"><span data-stu-id="f49df-119">include and configure ADAL</span></span>

<span data-ttu-id="f49df-120">Включите библиотеку ADAL.js на страницах вкладок и настройте ADAL с помощью своего ИД клиента и URL-адреса перенаправления:</span><span class="sxs-lookup"><span data-stu-id="f49df-120">Include the ADAL.js library in your tab pages and configure ADAL with your client ID and redirect URL:</span></span>

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

### <a name="get-the-user-context"></a><span data-ttu-id="f49df-121">Получить контекст пользователя</span><span class="sxs-lookup"><span data-stu-id="f49df-121">Get the user context</span></span>

<span data-ttu-id="f49df-122">На странице содержимого вкладки вызовите, чтобы получить подсказку для входа `microsoftTeams.getContext()` для текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="f49df-122">In the tab's content page, call `microsoftTeams.getContext()` to get a login hint for the current user.</span></span> <span data-ttu-id="f49df-123">Он будет использоваться в качестве login_hint в вызове Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f49df-123">This will be used as a login_hint in the call to Azure AD.</span></span>

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

### <a name="authenticate"></a><span data-ttu-id="f49df-124">Проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="f49df-124">Authenticate</span></span>

<span data-ttu-id="f49df-125">Если В ADAL для пользователя кэшировали неиспользваваемый маркер, используйте его.</span><span class="sxs-lookup"><span data-stu-id="f49df-125">If ADAL has an unexpired token cached for the user, use that.</span></span> <span data-ttu-id="f49df-126">В противном случае попытайтесь получить маркер без `acquireToken(resource, callback)` вызова.</span><span class="sxs-lookup"><span data-stu-id="f49df-126">Otherwise, attempt to get a token silently by calling `acquireToken(resource, callback)`.</span></span> <span data-ttu-id="f49df-127">ADAL.js вызов функции вызова с помощью запрашиваемого маркера или ошибку при сбойе проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="f49df-127">ADAL.js will call your callback function with the requested token, or an error if authentication fails.</span></span>

<span data-ttu-id="f49df-128">Если в функции обратного вызова произошла ошибка, откажите кнопку входа и вернемся к явному входу.</span><span class="sxs-lookup"><span data-stu-id="f49df-128">If you get an error in the callback function, show a login button and fall back to an explicit login.</span></span>

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

### <a name="process-the-return-value"></a><span data-ttu-id="f49df-129">Обработка возвращаемой стоимости</span><span class="sxs-lookup"><span data-stu-id="f49df-129">Process the return value</span></span>

<span data-ttu-id="f49df-130">Let ADAL.js take care of parsing the result from Azure AD by calling `AuthenticationContext.handleWindowCallback(hash)` in the login callback page.</span><span class="sxs-lookup"><span data-stu-id="f49df-130">Let ADAL.js take care of parsing the result from Azure AD by calling `AuthenticationContext.handleWindowCallback(hash)` in the login callback page.</span></span>

<span data-ttu-id="f49df-131">Убедитесь, что у нас есть допустимый пользователь, и позвоните или вернем отчет о состоянии на `microsoftTeams.authentication.notifySuccess()` `microsoftTeams.authentication.notifyFailure()` главную страницу содержимого вкладки.</span><span class="sxs-lookup"><span data-stu-id="f49df-131">Check that we have a valid user and call `microsoftTeams.authentication.notifySuccess()` or `microsoftTeams.authentication.notifyFailure()` to report status back to your main tab content page.</span></span>

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
