---
title: Проверка подлинности для вкладок с помощью Azure Active Directory
description: Описание проверки подлинности в Teams и ее использования на вкладках
keywords: вкладки проверки подлинности Teams AAD
ms.openlocfilehash: a1d3a96e23706012b643b5827701b49e2306d847
ms.sourcegitcommit: f9a2f5cedc9d30ef7a9cf78a47d01cfd277e150d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/23/2020
ms.locfileid: "48237785"
---
# <a name="authenticate-a-user-in-a-microsoft-teams-tab"></a><span data-ttu-id="c67ae-104">Проверка подлинности пользователя на вкладке Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="c67ae-104">Authenticate a user in a Microsoft Teams tab</span></span>

> [!Note]
> <span data-ttu-id="c67ae-105">Чтобы проверка подлинности работала для вкладки на мобильных клиентах, необходимо убедиться, что используется версия 1.4.1 или более поздняя версия пакета SDK для Teams SDK.</span><span class="sxs-lookup"><span data-stu-id="c67ae-105">For authentication to work for your tab on mobile clients, you need to ensure you're using version 1.4.1 or later of the Teams JavaScript SDK.</span></span>

<span data-ttu-id="c67ae-106">Существует множество служб, которые вы можете использовать в приложении Teams, а большинство этих служб требуют проверки подлинности и авторизации для получения доступа к службе.</span><span class="sxs-lookup"><span data-stu-id="c67ae-106">There are many services that you may wish to consume inside your Teams app, and most of those services require authentication and authorization to get access to the service.</span></span> <span data-ttu-id="c67ae-107">Службы включают в себя Facebook, Twitter и учебные группы.</span><span class="sxs-lookup"><span data-stu-id="c67ae-107">Services include Facebook, Twitter, and of course Teams.</span></span> <span data-ttu-id="c67ae-108">Сведения о профилях пользователей в Teams хранятся в Azure Active Directory (Azure AD) с помощью Microsoft Graph, и эта статья посвящена проверке подлинности с помощью Azure AD для получения доступа к этой информации.</span><span class="sxs-lookup"><span data-stu-id="c67ae-108">Users of Teams have user profile information stored in Azure Active Directory (Azure AD) using Microsoft Graph and this article will focus on authentication using Azure AD to get access to this information.</span></span>

<span data-ttu-id="c67ae-109">OAuth 2,0 — это открытый стандарт проверки подлинности, используемый Azure AD, и многие другие поставщики услуг.</span><span class="sxs-lookup"><span data-stu-id="c67ae-109">OAuth 2.0 is an open standard for authentication used by Azure AD and many other service providers.</span></span> <span data-ttu-id="c67ae-110">Общие сведения о OAuth 2,0 является необходимым условием для работы с проверкой подлинности в Teams и Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c67ae-110">Understanding OAuth 2.0 is a prerequisite for working with authentication in Teams and Azure AD.</span></span> <span data-ttu-id="c67ae-111">В приведенных ниже примерах используется неявный поток предоставления OAuth 2,0 с целью последующего считывания сведений профиля пользователя из Azure AD и Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="c67ae-111">The examples below use the OAuth 2.0 Implicit Grant flow with the goal of eventually reading the user's profile information from Azure AD and Microsoft Graph.</span></span>

<span data-ttu-id="c67ae-112">Код, приведенный в этой статье, взят из примера приложения [Microsoft Teams с проверкой подлинности с помощью вкладки Microsoft Teams (узел)](https://github.com/OfficeDev/microsoft-teams-sample-complete-node).</span><span class="sxs-lookup"><span data-stu-id="c67ae-112">The code in this article comes from the Teams sample app [Microsoft Teams tab authentication sample (Node)](https://github.com/OfficeDev/microsoft-teams-sample-complete-node).</span></span> <span data-ttu-id="c67ae-113">Он содержит статическую вкладку, которая запрашивает маркер доступа для Microsoft Graph и показывает сведения о базовом профиле текущего пользователя из Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c67ae-113">It contains a static tab that requests an access token for Microsoft Graph and shows the current user's basic profile information from Azure AD.</span></span>

<span data-ttu-id="c67ae-114">Общий обзор процесса проверки подлинности для вкладок представлен в разделе [последовательность проверки подлинности на вкладках](~/tabs/how-to/authentication/auth-flow-tab.md).</span><span class="sxs-lookup"><span data-stu-id="c67ae-114">For a general overview of authentication flow for tabs see the topic [Authentication flow in tabs](~/tabs/how-to/authentication/auth-flow-tab.md).</span></span>

<span data-ttu-id="c67ae-115">Процесс проверки подлинности на вкладках немного отличается от процесса проверки подлинности в Боты.</span><span class="sxs-lookup"><span data-stu-id="c67ae-115">Authentication flow in tabs differs slightly from authentication flow in bots.</span></span>

## <a name="configuring-identity-providers"></a><span data-ttu-id="c67ae-116">Настройка поставщиков удостоверений</span><span class="sxs-lookup"><span data-stu-id="c67ae-116">Configuring identity providers</span></span>

<span data-ttu-id="c67ae-117">В разделе [Настройка поставщиков удостоверений](~/concepts/authentication/configure-identity-provider.md) подробные указания по настройке URL-адресов перенаправления для обратного вызова OAuth 2,0 при использовании Azure Active Directory в качестве поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="c67ae-117">See the topic [Configure identity providers](~/concepts/authentication/configure-identity-provider.md) for detailed steps on configuring OAuth 2.0 callback redirect URL(s) when using Azure Active Directory as an identity provider.</span></span>

## <a name="initiate-authentication-flow"></a><span data-ttu-id="c67ae-118">Запуск процесса проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="c67ae-118">Initiate authentication flow</span></span>

<span data-ttu-id="c67ae-119">Процесс проверки подлинности должен инициироваться действием пользователя.</span><span class="sxs-lookup"><span data-stu-id="c67ae-119">Authentication flow should be triggered by a user action.</span></span> <span data-ttu-id="c67ae-120">Не следует открывать всплывающую подсказку проверки подлинности автоматически, так как это может вызвать блокирование всплывающих окон в браузере, а также запутать пользователя.</span><span class="sxs-lookup"><span data-stu-id="c67ae-120">You should not open the authentication pop-up automatically because this is likely to trigger the browser's pop-up blocker as well as confuse the user.</span></span>

<span data-ttu-id="c67ae-121">Добавьте кнопку на страницу конфигурации или содержимого, чтобы разрешить пользователю выполнять вход при необходимости.</span><span class="sxs-lookup"><span data-stu-id="c67ae-121">Add a button to your configuration or content page to enable the user to sign in when needed.</span></span> <span data-ttu-id="c67ae-122">Это можно сделать на странице [Настройка](~/tabs/how-to/create-tab-pages/configuration-page.md) вкладки или на любой странице [содержимого](~/tabs/how-to/create-tab-pages/content-page.md) .</span><span class="sxs-lookup"><span data-stu-id="c67ae-122">This can be done in the tab [configuration](~/tabs/how-to/create-tab-pages/configuration-page.md) page or any [content](~/tabs/how-to/create-tab-pages/content-page.md) page.</span></span>

<span data-ttu-id="c67ae-123">Azure AD, как и большинство поставщиков удостоверений, не допускают помещение его содержимого в IFRAME.</span><span class="sxs-lookup"><span data-stu-id="c67ae-123">Azure AD, like most identity providers, does not allow its content to be placed in an iframe.</span></span> <span data-ttu-id="c67ae-124">Это означает, что вам потребуется добавить всплывающую страницу для размещения поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="c67ae-124">This means that you will need to add a pop-up page to host the identity provider.</span></span> <span data-ttu-id="c67ae-125">В следующем примере это страница `/tab-auth/simple-start` .</span><span class="sxs-lookup"><span data-stu-id="c67ae-125">In the following example this page is `/tab-auth/simple-start`.</span></span> <span data-ttu-id="c67ae-126">Используйте `microsoftTeams.authenticate()` функцию пакета SDK клиента Microsoft Teams, чтобы открыть эту страницу при выборе кнопки.</span><span class="sxs-lookup"><span data-stu-id="c67ae-126">Use the `microsoftTeams.authenticate()` function of the Microsoft Teams client SDK to launch this page when your button is selected.</span></span>

```javascript
microsoftTeams.authentication.authenticate({
    url: window.location.origin + "/tab-auth/simple-start",
    width: 600,
    height: 535,
    successCallback: function (result) {
        getUserProfile(result.accessToken);
    },
    failureCallback: function (reason) {
        handleAuthError(reason);
    }
});
```

### <a name="notes"></a><span data-ttu-id="c67ae-127">Примечания</span><span class="sxs-lookup"><span data-stu-id="c67ae-127">Notes</span></span>

* <span data-ttu-id="c67ae-128">URL-адрес, на который вы передается, `microsoftTeams.authentication.authenticate()` является начальной страницей процесса проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="c67ae-128">The URL you pass to `microsoftTeams.authentication.authenticate()` is the start page of the authentication flow.</span></span> <span data-ttu-id="c67ae-129">В этом примере `/tab-auth/simple-start` .</span><span class="sxs-lookup"><span data-stu-id="c67ae-129">In this example that is `/tab-auth/simple-start`.</span></span> <span data-ttu-id="c67ae-130">Это должно быть согласовано с тем, что вы зарегистрировались на [портале регистрации приложений Azure AD](https://apps.dev.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="c67ae-130">This should match what you registered in the [Azure AD Application Registration Portal](https://apps.dev.microsoft.com).</span></span>

* <span data-ttu-id="c67ae-131">Процесс проверки подлинности должен начинаться на странице, которая находится в вашем домене.</span><span class="sxs-lookup"><span data-stu-id="c67ae-131">Authentication flow must start on a page that's on your domain.</span></span> <span data-ttu-id="c67ae-132">Этот домен также должен быть указан в [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) разделе манифеста.</span><span class="sxs-lookup"><span data-stu-id="c67ae-132">This domain should also be listed in the [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) section of the manifest.</span></span> <span data-ttu-id="c67ae-133">В противном случае произойдет пустое всплывающее окно.</span><span class="sxs-lookup"><span data-stu-id="c67ae-133">Failure to do so will result in an empty pop-up.</span></span>

* <span data-ttu-id="c67ae-134">Отработка отказа приведет к проблеме, когда `microsoftTeams.authentication.authenticate()` всплывающее окно не закрывается в конце процесса входа.</span><span class="sxs-lookup"><span data-stu-id="c67ae-134">Failing to use `microsoftTeams.authentication.authenticate()` will cause a problem with the popup not closing at the end of the sign in process.</span></span>

## <a name="navigate-to-the-authorization-page-from-your-popup-page"></a><span data-ttu-id="c67ae-135">Переход на страницу авторизации из всплывающей страницы</span><span class="sxs-lookup"><span data-stu-id="c67ae-135">Navigate to the authorization page from your popup page</span></span>

<span data-ttu-id="c67ae-136">Когда откроется всплывающая страница ( `/tab-auth/simple-start` ), выполняется следующий код.</span><span class="sxs-lookup"><span data-stu-id="c67ae-136">When your popup page (`/tab-auth/simple-start`) is displayed the following code is run.</span></span> <span data-ttu-id="c67ae-137">Основной целью этой страницы является перенаправление на поставщика удостоверений, чтобы пользователь мог выполнить вход.</span><span class="sxs-lookup"><span data-stu-id="c67ae-137">The main goal of this page is to redirect to your identity provider so the user can sign in.</span></span> <span data-ttu-id="c67ae-138">Это перенаправление можно выполнить на стороне сервера с помощью HTTP 302, но в этом случае она выполняется на клиентской стороне с помощью вызова `window.location.assign()` .</span><span class="sxs-lookup"><span data-stu-id="c67ae-138">This redirection could be done on the server side using HTTP 302, but in this case it is done on the client side using with a call to `window.location.assign()`.</span></span> <span data-ttu-id="c67ae-139">Кроме того, можно `microsoftTeams.getContext()` использовать для получения сведений о подсказках, которые можно передать в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c67ae-139">This also allows `microsoftTeams.getContext()` to be used to retrieve hinting information which can be passed to Azure AD.</span></span>

```javascript
microsoftTeams.getContext(function (context) {
    // Generate random state string and store it, so we can verify it in the callback
    let state = _guid(); // _guid() is a helper function in the sample
    localStorage.setItem("simple.state", state);
    localStorage.removeItem("simple.error");
    // Go to the Azure AD authorization endpoint
    let queryParams = {
        client_id: "YOUR_APP_ID_HERE",
        response_type: "id_token token",
        response_mode: "fragment",
        resource: "https://graph.microsoft.com/User.Read openid",
        redirect_uri: window.location.origin + "/tab-auth/simple-end",
        nonce: _guid(),
        state: state,
        // The context object is populated by Teams; the loginHint attribute
         // is used as hinting information
        login_hint: context.loginHint,
    };

    let authorizeEndpoint = "https://login.microsoftonline.com/" + context.tid + "/oauth2/v2.0/authorize?" + toQueryString(queryParams);
    window.location.assign(authorizeEndpoint);
});
```

<span data-ttu-id="c67ae-140">После того как пользователь завершит авторизацию, пользователь перенаправляется на страницу обратного вызова, указанную для вашего приложения `/tab-auth/simple-end` .</span><span class="sxs-lookup"><span data-stu-id="c67ae-140">After the user completes authorization, the user is redirected to the callback page you specified for your app at `/tab-auth/simple-end`.</span></span>

### <a name="notes"></a><span data-ttu-id="c67ae-141">Примечания</span><span class="sxs-lookup"><span data-stu-id="c67ae-141">Notes</span></span>

* <span data-ttu-id="c67ae-142">Для создания запросов проверки подлинности и URL-адресов ознакомьтесь со [статьей получение сведений о контексте пользователя](~/tabs/how-to/access-teams-context.md) .</span><span class="sxs-lookup"><span data-stu-id="c67ae-142">See [get user context information](~/tabs/how-to/access-teams-context.md) for help building authentication requests and URLs.</span></span> <span data-ttu-id="c67ae-143">Например, вы можете использовать имя пользователя для входа в качестве `login_hint` значения для входа в Azure AD, что означает, что пользователю может потребоваться ввести меньше.</span><span class="sxs-lookup"><span data-stu-id="c67ae-143">For example, you can use the user's login name as the `login_hint` value for Azure AD sign-in, which means the user might need to type less.</span></span> <span data-ttu-id="c67ae-144">Помните, что этот контекст не следует использовать непосредственно в качестве подтверждения личности, так как злоумышленник может загрузить страницу в вредоносном браузере и предоставить ей любую нужную информацию.</span><span class="sxs-lookup"><span data-stu-id="c67ae-144">Remember that you should not use this context directly as proof of identity since an attacker could load your page in a malicious browser and provide it with any information they want.</span></span>
* <span data-ttu-id="c67ae-145">Несмотря на то, что контекст вкладки предоставляет полезную информацию для пользователя, не используйте эти сведения для проверки подлинности пользователя о том, является ли он параметрами URL-адреса для контента вкладки, или вызывая `microsoftTeams.getContext()` функцию в клиенте SDK Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="c67ae-145">Although the tab context provides useful information regarding the user, don't use this information to authenticate the user whether you get it as URL parameters to your tab content URL or by calling the `microsoftTeams.getContext()` function in the Microsoft Teams client SDK.</span></span> <span data-ttu-id="c67ae-146">Вредоносный субъект может вызывать URL-адрес содержимого вкладки с собственными параметрами, а веб-страница, олицетворяющая Microsoft Teams, может загрузить URL-адрес содержимого вкладки в IFRAME и вернуть собственные данные в `getContext()` функцию.</span><span class="sxs-lookup"><span data-stu-id="c67ae-146">A malicious actor could invoke your tab content URL with its own parameters, and a web page impersonating Microsoft Teams could load your tab content URL in an iframe and return its own data to the `getContext()` function.</span></span> <span data-ttu-id="c67ae-147">Информация, связанная с удостоверением, должна рассматриваться в контексте вкладки просто как подсказки и проверять их перед использованием.</span><span class="sxs-lookup"><span data-stu-id="c67ae-147">You should treat the identity-related information in the tab context simply as hints and validate them before use.</span></span>
* <span data-ttu-id="c67ae-148">`state`Параметр используется для подтверждения того, что служба, вызывающая URI обратного вызова, является вызываемой службой.</span><span class="sxs-lookup"><span data-stu-id="c67ae-148">The `state` parameter is used to confirm that the service calling the callback URI is the service you called.</span></span> <span data-ttu-id="c67ae-149">Если `state` параметр в обратном вызове не соответствует параметру, отправленному во время вызова, возвращенный вызов не проверяется и должен быть завершен.</span><span class="sxs-lookup"><span data-stu-id="c67ae-149">If the `state` parameter in the callback does not match the parameter you sent during the call the return call is not verified and should be terminated.</span></span>
* <span data-ttu-id="c67ae-150">Нет необходимости включать домен поставщика удостоверений в `validDomains` список в manifest.jsприложения в файле.</span><span class="sxs-lookup"><span data-stu-id="c67ae-150">It is not necessary to include the identity provider's domain in the `validDomains` list in the app's manifest.json file.</span></span>

## <a name="the-callback-page"></a><span data-ttu-id="c67ae-151">Страница обратного вызова</span><span class="sxs-lookup"><span data-stu-id="c67ae-151">The callback page</span></span>

<span data-ttu-id="c67ae-152">В последнем разделе, на котором вы позвонили в службу авторизации Azure AD и переданы сведения о пользователях и приложениях, чтобы Azure AD мог представить пользователю собственную систему авторизации.</span><span class="sxs-lookup"><span data-stu-id="c67ae-152">In the last section you called the Azure AD authorization service and passed in user and app information so that Azure AD could present the user with its own monolithic authorization experience.</span></span> <span data-ttu-id="c67ae-153">Ваше приложение не контролирует то, что происходит в этом интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="c67ae-153">Your app has no control over what happens in this experience.</span></span> <span data-ttu-id="c67ae-154">Все знают, что возвращается, когда Azure AD вызывает указанную страницу обратного вызова ( `/tab-auth/simple-end` ).</span><span class="sxs-lookup"><span data-stu-id="c67ae-154">All it knows is what is returned when Azure AD calls the  callback page that you provided (`/tab-auth/simple-end`).</span></span>

<span data-ttu-id="c67ae-155">На этой странице необходимо определить успешность или сбой на основе сведений, возвращенных службой Azure AD, а `microsoftTeams.authentication.notifySuccess()` также вызвать или `microsoftTeams.authentication.notifyFailure()` .</span><span class="sxs-lookup"><span data-stu-id="c67ae-155">In this page you need to determine success or failure based on the information returned by Azure AD and call `microsoftTeams.authentication.notifySuccess()` or `microsoftTeams.authentication.notifyFailure()`.</span></span> <span data-ttu-id="c67ae-156">Если вход выполнен успешно, вы получите доступ к ресурсам службы.</span><span class="sxs-lookup"><span data-stu-id="c67ae-156">If the login was successful you will have access to service resources.</span></span>

````javascript
// Split the key-value pairs passed from Azure AD
// getHashParameters is a helper function that parses the arguments sent
// to the callback URL by Azure AD after the authorization call
let hashParams = getHashParameters();
if (hashParams["error"]) {
    // Authentication/authorization failed
    microsoftTeams.authentication.notifyFailure(hashParams["error"]);
} else if (hashParams["access_token"]) {
    // Get the stored state parameter and compare with incoming state
    // This validates that the data is coming from Azure AD
    let expectedState = localStorage.getItem("simple.state");
    if (expectedState !== hashParams["state"]) {
        // State does not match, report error
        microsoftTeams.authentication.notifyFailure("StateDoesNotMatch");
    } else {
        // Success: return token information to the tab
        microsoftTeams.authentication.notifySuccess({
            idToken: hashParams["id_token"],
            accessToken: hashParams["access_token"],
            tokenType: hashParams["token_type"],
            expiresIn: hashParams["expires_in"]
        })
    }
} else {
    // Unexpected condition: hash does not contain error or access_token parameter
    microsoftTeams.authentication.notifyFailure("UnexpectedFailure");
}
````

<span data-ttu-id="c67ae-157">Этот код анализирует пары "ключ — значение", полученные из Azure AD `window.location.hash` , с помощью `getHashParameters()` вспомогательной функции.</span><span class="sxs-lookup"><span data-stu-id="c67ae-157">This code parses the key-value pairs received from Azure AD in `window.location.hash` using the `getHashParameters()` helper function.</span></span> <span data-ttu-id="c67ae-158">Если обнаруживается `access_token` , и значение совпадает с параметром, `state` предоставленным в начале процесса проверки подлинности, он возвращает маркер доступа на вкладку с помощью вызова `notifySuccess()` ; в противном случае сообщает об ошибке `notifyFailure()` .</span><span class="sxs-lookup"><span data-stu-id="c67ae-158">If it finds an `access_token`, and the `state` value is the same as the one provided at the start of the authentication flow, it returns the access token to the tab by calling `notifySuccess()`; otherwise it reports an error with `notifyFailure()`.</span></span>

### <a name="notes"></a><span data-ttu-id="c67ae-159">Примечания</span><span class="sxs-lookup"><span data-stu-id="c67ae-159">Notes</span></span>

<span data-ttu-id="c67ae-160">`NotifyFailure()` имеет следующие предопределенные причины ошибки:</span><span class="sxs-lookup"><span data-stu-id="c67ae-160">`NotifyFailure()` has the following predefined failure reasons:</span></span>

* <span data-ttu-id="c67ae-161">`CancelledByUser` пользователь закрыл всплывающее окно перед завершением процесса проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="c67ae-161">`CancelledByUser` the user closed the popup window before completing the authentication flow.</span></span>
* <span data-ttu-id="c67ae-162">`FailedToOpenWindow` не удается открыть всплывающее окно.</span><span class="sxs-lookup"><span data-stu-id="c67ae-162">`FailedToOpenWindow` the popup window could not be opened.</span></span> <span data-ttu-id="c67ae-163">При работе с Microsoft Teams в браузере обычно это означает, что окно заблокировано с помощью средства блокирования всплывающих окон.</span><span class="sxs-lookup"><span data-stu-id="c67ae-163">When running Microsoft Teams in a browser, this typically means that the window was blocked by a popup blocker.</span></span>

<span data-ttu-id="c67ae-164">В случае успешного выполнения можно обновить или перезагрузить страницу, а также Показать контент, относящийся к пользователю, прошедшему проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="c67ae-164">If successful, you can refresh or reload the page and show content relevant to the now-authenticated user.</span></span> <span data-ttu-id="c67ae-165">Если не удается выполнить проверку подлинности, отобразится сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="c67ae-165">If authentication fails, display an error message.</span></span>

<span data-ttu-id="c67ae-166">Ваше приложение может задать свой файл cookie для сеанса, чтобы пользователь не мог войти в систему при возврате на вкладку на текущем устройстве.</span><span class="sxs-lookup"><span data-stu-id="c67ae-166">Your app can set its own session cookie so that the user need not sign in again when they return to your tab on the current device.</span></span>

> [!NOTE]
> <span data-ttu-id="c67ae-167">Хром 80, запланированный на выпуск ранних 2020, содержит новые значения файлов cookie и по умолчанию накладывает политики файлов cookie.</span><span class="sxs-lookup"><span data-stu-id="c67ae-167">Chrome 80, scheduled for release in early 2020, introduces new cookie values and imposes cookie policies by default.</span></span> <span data-ttu-id="c67ae-168">Рекомендуется задавать предполагаемый способ использования файлов cookie, а не полагаться на поведение браузера по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c67ae-168">It's recommended that you set the intended use for your cookies rather than rely on default browser behavior.</span></span> <span data-ttu-id="c67ae-169">*Просмотрите* [атрибут самесите cookie (обновление 2020)](../../../resources/samesite-cookie-update.md).</span><span class="sxs-lookup"><span data-stu-id="c67ae-169">*See* [SameSite cookie attribute (2020 update)](../../../resources/samesite-cookie-update.md).</span></span>

>[!NOTE]
><span data-ttu-id="c67ae-170">Чтобы получить правильный маркер для гостевых и гостевых пользователей Microsoft Teams, важно, чтобы в приложениях использовалась конечная точка клиента https://login.microsoftonline.com/ **{tenantId}**.</span><span class="sxs-lookup"><span data-stu-id="c67ae-170">To get the correct token for Microsoft Teams Free and guest users, it is important that the apps use tenant specific endpoint https://login.microsoftonline.com/**{tenantId}**.</span></span> <span data-ttu-id="c67ae-171">Значение tenantId можно получить из сообщения Bot или контекста Tab.</span><span class="sxs-lookup"><span data-stu-id="c67ae-171">You can get tenantId from the bot message or tab context.</span></span> <span data-ttu-id="c67ae-172">Если приложение использует приложения https://login.microsoftonline.com/common , пользователи получат неверные маркеры и войдет в "домашний" клиент, а не в клиент, на который в данный момент выполнен вход.</span><span class="sxs-lookup"><span data-stu-id="c67ae-172">If the apps use https://login.microsoftonline.com/common, the users will get incorrect tokens and will log on to the "home" tenant instead of the tenant that they are currently signed into.</span></span>

<span data-ttu-id="c67ae-173">Дополнительные сведения о службе единого входа (SSO) можно найти в статье [Автоматическая проверка подлинности](~/tabs/how-to/authentication/auth-silent-AAD.md).</span><span class="sxs-lookup"><span data-stu-id="c67ae-173">For more information on Single Sign-On (SSO) see the article [Silent authentication](~/tabs/how-to/authentication/auth-silent-AAD.md).</span></span>

## <a name="samples"></a><span data-ttu-id="c67ae-174">Примеры</span><span class="sxs-lookup"><span data-stu-id="c67ae-174">Samples</span></span>

<span data-ttu-id="c67ae-175">Пример кода, иллюстрирующий процесс проверки подлинности с помощью вкладок с помощью Azure AD, приведен ниже.</span><span class="sxs-lookup"><span data-stu-id="c67ae-175">For sample code showing the tab authentication process using Azure AD see:</span></span>

* [<span data-ttu-id="c67ae-176">Пример проверки подлинности с помощью вкладки Microsoft Teams (узел)</span><span class="sxs-lookup"><span data-stu-id="c67ae-176">Microsoft Teams tab authentication sample (Node)</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)
