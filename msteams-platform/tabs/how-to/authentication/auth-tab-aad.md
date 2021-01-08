---
title: Проверка подлинности вкладок с помощью Azure Active Directory
description: Описание проверки подлинности в Teams и ее использования на вкладке
keywords: Вкладки проверки подлинности teams AAD
ms.openlocfilehash: f6df2dbf84583488ddc0c57798d423b6288af16d
ms.sourcegitcommit: 23ceb25d07a76f03ffe92cf1ac578b7c50b0bafc
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/07/2021
ms.locfileid: "49777933"
---
# <a name="authenticate-a-user-in-a-microsoft-teams-tab"></a><span data-ttu-id="c9f49-104">Проверка подлинности пользователя на вкладке Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="c9f49-104">Authenticate a user in a Microsoft Teams tab</span></span>

> [!Note]
> <span data-ttu-id="c9f49-105">Чтобы проверка подлинности работала для вашей вкладки на мобильных клиентах, необходимо убедиться, что вы используете версию 1.4.1 или более поздней версии SDK JavaScript для Teams.</span><span class="sxs-lookup"><span data-stu-id="c9f49-105">For authentication to work for your tab on mobile clients, you need to ensure you're using version 1.4.1 or later of the Teams JavaScript SDK.</span></span>

<span data-ttu-id="c9f49-106">Существует множество служб, которые можно использовать в приложении Teams, и большинству из них требуется проверка подлинности и авторизация для получения доступа к службе.</span><span class="sxs-lookup"><span data-stu-id="c9f49-106">There are many services that you may wish to consume inside your Teams app, and most of those services require authentication and authorization to get access to the service.</span></span> <span data-ttu-id="c9f49-107">К службам относятся Facebook, Twitter и, конечно, Teams.</span><span class="sxs-lookup"><span data-stu-id="c9f49-107">Services include Facebook, Twitter, and of course Teams.</span></span> <span data-ttu-id="c9f49-108">Данные профилей пользователей Teams хранятся в Azure Active Directory (Azure AD) с помощью Microsoft Graph, и эта статья посвящена проверке подлинности с помощью Azure AD для получения доступа к этой информации.</span><span class="sxs-lookup"><span data-stu-id="c9f49-108">Users of Teams have user profile information stored in Azure Active Directory (Azure AD) using Microsoft Graph and this article will focus on authentication using Azure AD to get access to this information.</span></span>

<span data-ttu-id="c9f49-109">OAuth 2.0 — это открытый стандарт проверки подлинности, используемый Azure AD и многими другими поставщиками услуг.</span><span class="sxs-lookup"><span data-stu-id="c9f49-109">OAuth 2.0 is an open standard for authentication used by Azure AD and many other service providers.</span></span> <span data-ttu-id="c9f49-110">Понимание OAuth 2.0 является необходимым условием для работы с проверкой подлинности в Teams и Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c9f49-110">Understanding OAuth 2.0 is a prerequisite for working with authentication in Teams and Azure AD.</span></span> <span data-ttu-id="c9f49-111">В примерах ниже используется неявный поток предоставления OAuth 2.0 с целью постепенного чтения сведений профиля пользователя из Azure AD и Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="c9f49-111">The examples below use the OAuth 2.0 Implicit Grant flow with the goal of eventually reading the user's profile information from Azure AD and Microsoft Graph.</span></span>

<span data-ttu-id="c9f49-112">Код в этой статье взят из примера приложения Microsoft Teams пример проверки подлинности вкладок [(Node).](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)</span><span class="sxs-lookup"><span data-stu-id="c9f49-112">The code in this article comes from the Teams sample app [Microsoft Teams tab authentication sample (Node)](https://github.com/OfficeDev/microsoft-teams-sample-complete-node).</span></span> <span data-ttu-id="c9f49-113">Она содержит статическую вкладку, которая запрашивает маркер доступа для Microsoft Graph и отображает базовые данные профиля текущего пользователя из Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c9f49-113">It contains a static tab that requests an access token for Microsoft Graph and shows the current user's basic profile information from Azure AD.</span></span>

<span data-ttu-id="c9f49-114">Общие сведения о потоке проверки подлинности для вкладок см. в разделе "Поток проверки [подлинности на вкладке".](~/tabs/how-to/authentication/auth-flow-tab.md)</span><span class="sxs-lookup"><span data-stu-id="c9f49-114">For a general overview of authentication flow for tabs see the topic [Authentication flow in tabs](~/tabs/how-to/authentication/auth-flow-tab.md).</span></span>

<span data-ttu-id="c9f49-115">Поток проверки подлинности на вкладке немного отличается от потока проверки подлинности в ботах.</span><span class="sxs-lookup"><span data-stu-id="c9f49-115">Authentication flow in tabs differs slightly from authentication flow in bots.</span></span>

## <a name="configuring-identity-providers"></a><span data-ttu-id="c9f49-116">Настройка поставщиков удостоверений</span><span class="sxs-lookup"><span data-stu-id="c9f49-116">Configuring identity providers</span></span>

<span data-ttu-id="c9f49-117">Подробные [](~/concepts/authentication/configure-identity-provider.md) инструкции по настройке URL-адресов перенаправления вызовов OAuth 2.0 при использовании Azure Active Directory в качестве поставщика удостоверений см. в разделе "Настройка поставщиков удостоверений".</span><span class="sxs-lookup"><span data-stu-id="c9f49-117">See the topic [Configure identity providers](~/concepts/authentication/configure-identity-provider.md) for detailed steps on configuring OAuth 2.0 callback redirect URL(s) when using Azure Active Directory as an identity provider.</span></span>

## <a name="initiate-authentication-flow"></a><span data-ttu-id="c9f49-118">Инициализация потока проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="c9f49-118">Initiate authentication flow</span></span>

<span data-ttu-id="c9f49-119">Поток проверки подлинности должен запускаться действием пользователя.</span><span class="sxs-lookup"><span data-stu-id="c9f49-119">Authentication flow should be triggered by a user action.</span></span> <span data-ttu-id="c9f49-120">Не следует открывать всплывающее окна проверки подлинности автоматически, так как это, скорее всего, вызовет блокирование всплывающих блоков браузера, а также запутает пользователя.</span><span class="sxs-lookup"><span data-stu-id="c9f49-120">You should not open the authentication pop-up automatically because this is likely to trigger the browser's pop-up blocker as well as confuse the user.</span></span>

<span data-ttu-id="c9f49-121">Добавьте кнопку на страницу конфигурации или содержимого, чтобы пользователь при необходимости в нее влся.</span><span class="sxs-lookup"><span data-stu-id="c9f49-121">Add a button to your configuration or content page to enable the user to sign in when needed.</span></span> <span data-ttu-id="c9f49-122">Это можно сделать на странице конфигурации [вкладки](~/tabs/how-to/create-tab-pages/configuration-page.md) или на любой [странице содержимого.](~/tabs/how-to/create-tab-pages/content-page.md)</span><span class="sxs-lookup"><span data-stu-id="c9f49-122">This can be done in the tab [configuration](~/tabs/how-to/create-tab-pages/configuration-page.md) page or any [content](~/tabs/how-to/create-tab-pages/content-page.md) page.</span></span>

<span data-ttu-id="c9f49-123">Azure AD, как и большинство поставщиков удостоверений, не позволяет размещать его содержимое в iframe.</span><span class="sxs-lookup"><span data-stu-id="c9f49-123">Azure AD, like most identity providers, does not allow its content to be placed in an iframe.</span></span> <span data-ttu-id="c9f49-124">Это означает, что вам потребуется добавить всплывающее лицо для поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="c9f49-124">This means that you will need to add a pop-up page to host the identity provider.</span></span> <span data-ttu-id="c9f49-125">В следующем примере эта страница `/tab-auth/simple-start` .</span><span class="sxs-lookup"><span data-stu-id="c9f49-125">In the following example this page is `/tab-auth/simple-start`.</span></span> <span data-ttu-id="c9f49-126">Используйте `microsoftTeams.authenticate()` функцию клиентского SDK Microsoft Teams, чтобы запустить эту страницу при нажатии кнопки.</span><span class="sxs-lookup"><span data-stu-id="c9f49-126">Use the `microsoftTeams.authenticate()` function of the Microsoft Teams client SDK to launch this page when your button is selected.</span></span>

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

### <a name="notes"></a><span data-ttu-id="c9f49-127">Примечания</span><span class="sxs-lookup"><span data-stu-id="c9f49-127">Notes</span></span>

* <span data-ttu-id="c9f49-128">URL-адрес, на который вы передаете, является `microsoftTeams.authentication.authenticate()` первой страницей потока проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="c9f49-128">The URL you pass to `microsoftTeams.authentication.authenticate()` is the start page of the authentication flow.</span></span> <span data-ttu-id="c9f49-129">В этом примере это `/tab-auth/simple-start` .</span><span class="sxs-lookup"><span data-stu-id="c9f49-129">In this example that is `/tab-auth/simple-start`.</span></span> <span data-ttu-id="c9f49-130">Это должно соответствовать зарегистрированным на портале регистрации приложений [Azure AD.](https://apps.dev.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="c9f49-130">This should match what you registered in the [Azure AD Application Registration Portal](https://apps.dev.microsoft.com).</span></span>

* <span data-ttu-id="c9f49-131">Поток проверки подлинности должен начинаться на странице, которая в вашем домене.</span><span class="sxs-lookup"><span data-stu-id="c9f49-131">Authentication flow must start on a page that's on your domain.</span></span> <span data-ttu-id="c9f49-132">Этот домен также должен быть указан в [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) разделе манифеста.</span><span class="sxs-lookup"><span data-stu-id="c9f49-132">This domain should also be listed in the [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) section of the manifest.</span></span> <span data-ttu-id="c9f49-133">Если этого не сделать, будет выявить пустое всплывающее ок.</span><span class="sxs-lookup"><span data-stu-id="c9f49-133">Failure to do so will result in an empty pop-up.</span></span>

* <span data-ttu-id="c9f49-134">В противном случае возникает проблема, из-за чего всплывающее не закрывающееся в `microsoftTeams.authentication.authenticate()` конце процесса регистрации.</span><span class="sxs-lookup"><span data-stu-id="c9f49-134">Failing to use `microsoftTeams.authentication.authenticate()` will cause a problem with the popup not closing at the end of the sign in process.</span></span>

## <a name="navigate-to-the-authorization-page-from-your-popup-page"></a><span data-ttu-id="c9f49-135">Перейдите на страницу авторизации со всплываемой страницы</span><span class="sxs-lookup"><span data-stu-id="c9f49-135">Navigate to the authorization page from your popup page</span></span>

<span data-ttu-id="c9f49-136">После отображения всплываемой страницы () будет запускаться `/tab-auth/simple-start` следующий код.</span><span class="sxs-lookup"><span data-stu-id="c9f49-136">When your popup page (`/tab-auth/simple-start`) is displayed the following code is run.</span></span> <span data-ttu-id="c9f49-137">Основная цель этой страницы — перенаправить пользователя к поставщику удостоверений.</span><span class="sxs-lookup"><span data-stu-id="c9f49-137">The main goal of this page is to redirect to your identity provider so the user can sign in.</span></span> <span data-ttu-id="c9f49-138">Это перенаправление может быть сделано на стороне сервера с помощью HTTP 302, но в этом случае это делается на стороне клиента с помощью вызова `window.location.assign()` .</span><span class="sxs-lookup"><span data-stu-id="c9f49-138">This redirection could be done on the server side using HTTP 302, but in this case it is done on the client side using with a call to `window.location.assign()`.</span></span> <span data-ttu-id="c9f49-139">Это также позволяет получать подсказки, которые можно передать `microsoftTeams.getContext()` в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c9f49-139">This also allows `microsoftTeams.getContext()` to be used to retrieve hinting information which can be passed to Azure AD.</span></span>

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
        scope: "https://graph.microsoft.com/User.Read openid",
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

<span data-ttu-id="c9f49-140">После авторизации пользователь перенаправляется на страницу вызова, указанную для вашего `/tab-auth/simple-end` приложения.</span><span class="sxs-lookup"><span data-stu-id="c9f49-140">After the user completes authorization, the user is redirected to the callback page you specified for your app at `/tab-auth/simple-end`.</span></span>

### <a name="notes"></a><span data-ttu-id="c9f49-141">Примечания</span><span class="sxs-lookup"><span data-stu-id="c9f49-141">Notes</span></span>

* <span data-ttu-id="c9f49-142">Сведения [о контексте пользователя см.](~/tabs/how-to/access-teams-context.md) в справке по построению запросов на проверку подлинности и URL-адресов.</span><span class="sxs-lookup"><span data-stu-id="c9f49-142">See [get user context information](~/tabs/how-to/access-teams-context.md) for help building authentication requests and URLs.</span></span> <span data-ttu-id="c9f49-143">Например, можно использовать имя для входа пользователя в качестве значения для входа в Azure AD, что означает, что пользователю может потребоваться `login_hint` ввести меньше.</span><span class="sxs-lookup"><span data-stu-id="c9f49-143">For example, you can use the user's login name as the `login_hint` value for Azure AD sign-in, which means the user might need to type less.</span></span> <span data-ttu-id="c9f49-144">Помните, что не следует использовать этот контекст непосредственно в качестве подтверждения личности, так как злоумышленник может загрузить страницу в вредоносный браузер и предоставить ему любую информацию.</span><span class="sxs-lookup"><span data-stu-id="c9f49-144">Remember that you should not use this context directly as proof of identity since an attacker could load your page in a malicious browser and provide it with any information they want.</span></span>
* <span data-ttu-id="c9f49-145">Хотя контекст вкладки предоставляет полезную информацию о пользователе, не используйте эти сведения для проверки подлинности пользователя независимо от того, получаете ли вы его в качестве параметров URL-адреса URL-адреса содержимого вкладки или путем вызова функции в клиентском `microsoftTeams.getContext()` SDK Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="c9f49-145">Although the tab context provides useful information regarding the user, don't use this information to authenticate the user whether you get it as URL parameters to your tab content URL or by calling the `microsoftTeams.getContext()` function in the Microsoft Teams client SDK.</span></span> <span data-ttu-id="c9f49-146">Злоумышленник может вызвать URL-адрес содержимого вкладки с собственными параметрами, а веб-страница, под названием Microsoft Teams, загрузит URL-адрес содержимого вкладки в iframe и возвратит свои данные в `getContext()` функцию.</span><span class="sxs-lookup"><span data-stu-id="c9f49-146">A malicious actor could invoke your tab content URL with its own parameters, and a web page impersonating Microsoft Teams could load your tab content URL in an iframe and return its own data to the `getContext()` function.</span></span> <span data-ttu-id="c9f49-147">Данные, связанные с удостоверениями, следует рассматривать в контексте вкладки просто как подсказки и проверять их перед использованием.</span><span class="sxs-lookup"><span data-stu-id="c9f49-147">You should treat the identity-related information in the tab context simply as hints and validate them before use.</span></span>
* <span data-ttu-id="c9f49-148">Этот параметр используется для подтверждения того, что служба, вызываемая URI вызова, `state` является вызываемой службой.</span><span class="sxs-lookup"><span data-stu-id="c9f49-148">The `state` parameter is used to confirm that the service calling the callback URI is the service you called.</span></span> <span data-ttu-id="c9f49-149">Если параметр в обратном вызове не совпадает с параметром, отправленным во время вызова, ответный вызов не проверяется и должен `state` быть завершен.</span><span class="sxs-lookup"><span data-stu-id="c9f49-149">If the `state` parameter in the callback does not match the parameter you sent during the call the return call is not verified and should be terminated.</span></span>
* <span data-ttu-id="c9f49-150">Нет необходимости включать домен поставщика удостоверений в список в файле manifest.js`validDomains` приложения.</span><span class="sxs-lookup"><span data-stu-id="c9f49-150">It is not necessary to include the identity provider's domain in the `validDomains` list in the app's manifest.json file.</span></span>

## <a name="the-callback-page"></a><span data-ttu-id="c9f49-151">Страница вызова</span><span class="sxs-lookup"><span data-stu-id="c9f49-151">The callback page</span></span>

<span data-ttu-id="c9f49-152">В последнем разделе вы вызвали службу авторизации Azure AD и передали сведения о пользователе и приложении, чтобы Azure AD мог представить пользователю собственный монолитный интерфейс авторизации.</span><span class="sxs-lookup"><span data-stu-id="c9f49-152">In the last section you called the Azure AD authorization service and passed in user and app information so that Azure AD could present the user with its own monolithic authorization experience.</span></span> <span data-ttu-id="c9f49-153">Ваше приложение не может контролировать, что происходит в этом случае.</span><span class="sxs-lookup"><span data-stu-id="c9f49-153">Your app has no control over what happens in this experience.</span></span> <span data-ttu-id="c9f49-154">Он знает только то, что возвращается, когда Azure AD вызывает предоставленную страницу обратного вызова ( `/tab-auth/simple-end` ).</span><span class="sxs-lookup"><span data-stu-id="c9f49-154">All it knows is what is returned when Azure AD calls the  callback page that you provided (`/tab-auth/simple-end`).</span></span>

<span data-ttu-id="c9f49-155">На этой странице необходимо определить успешность или сбой на основе информации, возвращаемой Azure AD и `microsoftTeams.authentication.notifySuccess()` вызовом или `microsoftTeams.authentication.notifyFailure()` .</span><span class="sxs-lookup"><span data-stu-id="c9f49-155">In this page you need to determine success or failure based on the information returned by Azure AD and call `microsoftTeams.authentication.notifySuccess()` or `microsoftTeams.authentication.notifyFailure()`.</span></span> <span data-ttu-id="c9f49-156">В случае успешного входа у вас будет доступ к ресурсам службы.</span><span class="sxs-lookup"><span data-stu-id="c9f49-156">If the login was successful you will have access to service resources.</span></span>

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

<span data-ttu-id="c9f49-157">Этот код разберет пары "ключ-значение", полученные из Azure AD, с `window.location.hash` помощью `getHashParameters()` функции-помощника.</span><span class="sxs-lookup"><span data-stu-id="c9f49-157">This code parses the key-value pairs received from Azure AD in `window.location.hash` using the `getHashParameters()` helper function.</span></span> <span data-ttu-id="c9f49-158">Если он находит и значение такое же, как в начале потока проверки подлинности, он возвращает маркер доступа на вкладку путем вызова; в противном случае сообщает об ошибке `access_token` `state` с `notifySuccess()` `notifyFailure()` .</span><span class="sxs-lookup"><span data-stu-id="c9f49-158">If it finds an `access_token`, and the `state` value is the same as the one provided at the start of the authentication flow, it returns the access token to the tab by calling `notifySuccess()`; otherwise it reports an error with `notifyFailure()`.</span></span>

### <a name="notes"></a><span data-ttu-id="c9f49-159">Примечания</span><span class="sxs-lookup"><span data-stu-id="c9f49-159">Notes</span></span>

<span data-ttu-id="c9f49-160">`NotifyFailure()` имеет следующие предопределяемы причины сбоя:</span><span class="sxs-lookup"><span data-stu-id="c9f49-160">`NotifyFailure()` has the following predefined failure reasons:</span></span>

* <span data-ttu-id="c9f49-161">`CancelledByUser` пользователь закрыл всплывающее окно перед завершением потока проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="c9f49-161">`CancelledByUser` the user closed the popup window before completing the authentication flow.</span></span>
* <span data-ttu-id="c9f49-162">`FailedToOpenWindow` Не удалось открыть всплывающее окно.</span><span class="sxs-lookup"><span data-stu-id="c9f49-162">`FailedToOpenWindow` the popup window could not be opened.</span></span> <span data-ttu-id="c9f49-163">При запуске Microsoft Teams в браузере это обычно означает, что окно было заблокировано блокатором всплывающих окон.</span><span class="sxs-lookup"><span data-stu-id="c9f49-163">When running Microsoft Teams in a browser, this typically means that the window was blocked by a popup blocker.</span></span>

<span data-ttu-id="c9f49-164">В случае успеха вы можете обновить или перезагрузить страницу и отдемонстрировать содержимое, релевантные для пользователя, который в настоящее время имеет проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="c9f49-164">If successful, you can refresh or reload the page and show content relevant to the now-authenticated user.</span></span> <span data-ttu-id="c9f49-165">Если не удается проверить подлинность, отобразить сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="c9f49-165">If authentication fails, display an error message.</span></span>

<span data-ttu-id="c9f49-166">Ваше приложение может настроить собственный файл cookie сеанса, чтобы пользователю не нужно было повторно входить при возвращении на вкладку на текущем устройстве.</span><span class="sxs-lookup"><span data-stu-id="c9f49-166">Your app can set its own session cookie so that the user need not sign in again when they return to your tab on the current device.</span></span>

> [!NOTE]
> <span data-ttu-id="c9f49-167">Chrome 80, запланированный на выпуск в начале 2020 г., представляет новые значения файлов cookie и по умолчанию налагает политики файлов cookie.</span><span class="sxs-lookup"><span data-stu-id="c9f49-167">Chrome 80, scheduled for release in early 2020, introduces new cookie values and imposes cookie policies by default.</span></span> <span data-ttu-id="c9f49-168">Рекомендуется устанавливать предназначенное для файлов cookie использование, а не полагаться на поведение браузера по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c9f49-168">It's recommended that you set the intended use for your cookies rather than rely on default browser behavior.</span></span> <span data-ttu-id="c9f49-169">*См.* [атрибут cookie SameSite (обновление 2020).](../../../resources/samesite-cookie-update.md)</span><span class="sxs-lookup"><span data-stu-id="c9f49-169">*See* [SameSite cookie attribute (2020 update)](../../../resources/samesite-cookie-update.md).</span></span>

>[!NOTE]
><span data-ttu-id="c9f49-170">Чтобы получить правильный маркер для бесплатных и гостевых пользователей Microsoft Teams, важно, чтобы приложения использовали конечную точку https://login.microsoftonline.com/ **{tenantId} для определенного клиента.**</span><span class="sxs-lookup"><span data-stu-id="c9f49-170">To get the correct token for Microsoft Teams Free and guest users, it is important that the apps use tenant specific endpoint https://login.microsoftonline.com/**{tenantId}**.</span></span> <span data-ttu-id="c9f49-171">Вы можете получить tenantId из сообщения бота или контекста вкладки.</span><span class="sxs-lookup"><span data-stu-id="c9f49-171">You can get tenantId from the bot message or tab context.</span></span> <span data-ttu-id="c9f49-172">Если используются приложения, пользователи получают неправильные маркеры и будут входить в "домашний" клиент, а не в клиент, в который они уже https://login.microsoftonline.com/common вписались.</span><span class="sxs-lookup"><span data-stu-id="c9f49-172">If the apps use https://login.microsoftonline.com/common, the users will get incorrect tokens and will log on to the "home" tenant instead of the tenant that they are currently signed into.</span></span>

<span data-ttu-id="c9f49-173">Дополнительные сведения о едином Sign-On (SSO) см. в статье "Проверка подлинности [без проверки подлинности".](~/tabs/how-to/authentication/auth-silent-AAD.md)</span><span class="sxs-lookup"><span data-stu-id="c9f49-173">For more information on Single Sign-On (SSO) see the article [Silent authentication](~/tabs/how-to/authentication/auth-silent-AAD.md).</span></span>

## <a name="samples"></a><span data-ttu-id="c9f49-174">Примеры</span><span class="sxs-lookup"><span data-stu-id="c9f49-174">Samples</span></span>

<span data-ttu-id="c9f49-175">Пример кода, показывающий процесс проверки подлинности вкладок с помощью Azure AD, см. в:</span><span class="sxs-lookup"><span data-stu-id="c9f49-175">For sample code showing the tab authentication process using Azure AD see:</span></span>

* [<span data-ttu-id="c9f49-176">Пример проверки подлинности на вкладке Microsoft Teams (узел)</span><span class="sxs-lookup"><span data-stu-id="c9f49-176">Microsoft Teams tab authentication sample (Node)</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)
