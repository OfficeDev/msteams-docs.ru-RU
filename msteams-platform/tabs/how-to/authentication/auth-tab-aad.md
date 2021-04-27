---
title: Проверка подлинности для вкладок с помощью Azure Active Directory
description: Описывает проверку подлинности в Teams и ее использование на вкладке
ms.topic: how-to
localization_priority: Normal
keywords: группы проверки подлинности вкладок AAD
ms.openlocfilehash: 2fdfc4448abb6980cca97e90951d7772611108da
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020389"
---
# <a name="authenticate-a-user-in-a-microsoft-teams-tab"></a><span data-ttu-id="60800-104">Проверка подлинности пользователя на вкладке Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="60800-104">Authenticate a user in a Microsoft Teams tab</span></span>

> [!Note]
> <span data-ttu-id="60800-105">Для проверки подлинности для вкладки на мобильных клиентах необходимо убедиться, что вы используете версию 1.4.1 или более поздний SDK Teams JavaScript.</span><span class="sxs-lookup"><span data-stu-id="60800-105">For authentication to work for your tab on mobile clients, you need to ensure you're using version 1.4.1 or later of the Teams JavaScript SDK.</span></span>

<span data-ttu-id="60800-106">Существует множество служб, которые можно использовать в приложении Teams, и большинство из них требуют проверки подлинности и авторизации для получения доступа к службе.</span><span class="sxs-lookup"><span data-stu-id="60800-106">There are many services that you may wish to consume inside your Teams app, and most of those services require authentication and authorization to get access to the service.</span></span> <span data-ttu-id="60800-107">Службы включают Facebook, Twitter и, конечно, Teams.</span><span class="sxs-lookup"><span data-stu-id="60800-107">Services include Facebook, Twitter, and of course Teams.</span></span> <span data-ttu-id="60800-108">У пользователей Teams есть сведения о профиле пользователей, хранимые в Azure Active Directory (Azure AD) с помощью Microsoft Graph, и в этой статье основное внимание будет уделялось проверке подлинности с помощью Azure AD для получения доступа к этой информации.</span><span class="sxs-lookup"><span data-stu-id="60800-108">Users of Teams have user profile information stored in Azure Active Directory (Azure AD) using Microsoft Graph and this article will focus on authentication using Azure AD to get access to this information.</span></span>

<span data-ttu-id="60800-109">OAuth 2.0 — это открытый стандарт проверки подлинности, используемый Azure AD и многими другими поставщиками услуг.</span><span class="sxs-lookup"><span data-stu-id="60800-109">OAuth 2.0 is an open standard for authentication used by Azure AD and many other service providers.</span></span> <span data-ttu-id="60800-110">Понимание OAuth 2.0 является обязательным условием для работы с проверкой подлинности в Teams и Azure AD.</span><span class="sxs-lookup"><span data-stu-id="60800-110">Understanding OAuth 2.0 is a prerequisite for working with authentication in Teams and Azure AD.</span></span> <span data-ttu-id="60800-111">В приведенных ниже примерах используется поток неявных грантов OAuth 2.0 с целью в конечном итоге считыть сведения о профиле пользователя из Azure AD и Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="60800-111">The examples below use the OAuth 2.0 Implicit Grant flow with the goal of eventually reading the user's profile information from Azure AD and Microsoft Graph.</span></span>

<span data-ttu-id="60800-112">Код в этой статье происходит из образца образца приложения Microsoft Teams образца проверки подлинности вкладок [(Node).](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)</span><span class="sxs-lookup"><span data-stu-id="60800-112">The code in this article comes from the Teams sample app [Microsoft Teams tab authentication sample (Node)](https://github.com/OfficeDev/microsoft-teams-sample-complete-node).</span></span> <span data-ttu-id="60800-113">Она содержит статическую вкладку, которая запрашивает маркер доступа для Microsoft Graph и отображает основные сведения о профиле текущего пользователя из Azure AD.</span><span class="sxs-lookup"><span data-stu-id="60800-113">It contains a static tab that requests an access token for Microsoft Graph and shows the current user's basic profile information from Azure AD.</span></span>

<span data-ttu-id="60800-114">Общий обзор потока проверки подлинности для вкладок см. в разделе Поток проверки подлинности [на вкладке](~/tabs/how-to/authentication/auth-flow-tab.md).</span><span class="sxs-lookup"><span data-stu-id="60800-114">For a general overview of authentication flow for tabs see the topic [Authentication flow in tabs](~/tabs/how-to/authentication/auth-flow-tab.md).</span></span>

<span data-ttu-id="60800-115">Поток проверки подлинности на вкладке немного отличается от потока проверки подлинности в ботах.</span><span class="sxs-lookup"><span data-stu-id="60800-115">Authentication flow in tabs differs slightly from authentication flow in bots.</span></span>

## <a name="configuring-identity-providers"></a><span data-ttu-id="60800-116">Настройка поставщиков удостоверений</span><span class="sxs-lookup"><span data-stu-id="60800-116">Configuring identity providers</span></span>

<span data-ttu-id="60800-117">См. в разделе [Настройка](~/concepts/authentication/configure-identity-provider.md) поставщиков удостоверений для подробных действий по настройке URL-адреса перенаправления вызовов OAuth 2.0 при использовании Azure Active Directory в качестве поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="60800-117">See the topic [Configure identity providers](~/concepts/authentication/configure-identity-provider.md) for detailed steps on configuring OAuth 2.0 callback redirect URL(s) when using Azure Active Directory as an identity provider.</span></span>

## <a name="initiate-authentication-flow"></a><span data-ttu-id="60800-118">Начало потока проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="60800-118">Initiate authentication flow</span></span>

<span data-ttu-id="60800-119">Поток проверки подлинности должен быть вызван действием пользователя.</span><span class="sxs-lookup"><span data-stu-id="60800-119">Authentication flow should be triggered by a user action.</span></span> <span data-ttu-id="60800-120">Не следует автоматически открывать всплывающее всплывающее окна проверки подлинности, так как это, скорее всего, вызовет блокировку всплывающее окна браузера, а также запутает пользователя.</span><span class="sxs-lookup"><span data-stu-id="60800-120">You should not open the authentication pop-up automatically because this is likely to trigger the browser's pop-up blocker as well as confuse the user.</span></span>

<span data-ttu-id="60800-121">Добавьте кнопку на страницу конфигурации или контента, чтобы пользователь в случае необходимости вход в нее входит.</span><span class="sxs-lookup"><span data-stu-id="60800-121">Add a button to your configuration or content page to enable the user to sign in when needed.</span></span> <span data-ttu-id="60800-122">Это можно сделать на странице конфигурации [вкладок](~/tabs/how-to/create-tab-pages/configuration-page.md) или на любой [странице контента.](~/tabs/how-to/create-tab-pages/content-page.md)</span><span class="sxs-lookup"><span data-stu-id="60800-122">This can be done in the tab [configuration](~/tabs/how-to/create-tab-pages/configuration-page.md) page or any [content](~/tabs/how-to/create-tab-pages/content-page.md) page.</span></span>

<span data-ttu-id="60800-123">Azure AD, как и большинство поставщиков удостоверений, не позволяет размещать содержимое в iframe.</span><span class="sxs-lookup"><span data-stu-id="60800-123">Azure AD, like most identity providers, does not allow its content to be placed in an iframe.</span></span> <span data-ttu-id="60800-124">Это означает, что для хозяйского поставщика удостоверений необходимо добавить всплывающее всплывающее лицо.</span><span class="sxs-lookup"><span data-stu-id="60800-124">This means that you will need to add a pop-up page to host the identity provider.</span></span> <span data-ttu-id="60800-125">В следующем примере эта страница `/tab-auth/simple-start` .</span><span class="sxs-lookup"><span data-stu-id="60800-125">In the following example this page is `/tab-auth/simple-start`.</span></span> <span data-ttu-id="60800-126">Используйте функцию SDK клиента Microsoft Teams для запуска этой страницы при выборе `microsoftTeams.authenticate()` кнопки.</span><span class="sxs-lookup"><span data-stu-id="60800-126">Use the `microsoftTeams.authenticate()` function of the Microsoft Teams client SDK to launch this page when your button is selected.</span></span>

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

### <a name="notes"></a><span data-ttu-id="60800-127">Примечания</span><span class="sxs-lookup"><span data-stu-id="60800-127">Notes</span></span>

* <span data-ttu-id="60800-128">URL-адрес, на который `microsoftTeams.authentication.authenticate()` вы передаете, является началом потока проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="60800-128">The URL you pass to `microsoftTeams.authentication.authenticate()` is the start page of the authentication flow.</span></span> <span data-ttu-id="60800-129">В этом примере это `/tab-auth/simple-start` .</span><span class="sxs-lookup"><span data-stu-id="60800-129">In this example that is `/tab-auth/simple-start`.</span></span> <span data-ttu-id="60800-130">Это должно совпадать с тем, что вы зарегистрировали на портале регистрации приложений [Azure AD.](https://apps.dev.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="60800-130">This should match what you registered in the [Azure AD Application Registration Portal](https://apps.dev.microsoft.com).</span></span>

* <span data-ttu-id="60800-131">Поток проверки подлинности должен начинаться на странице, которая на вашем домене.</span><span class="sxs-lookup"><span data-stu-id="60800-131">Authentication flow must start on a page that's on your domain.</span></span> <span data-ttu-id="60800-132">Этот домен также должен быть указан в [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) разделе манифеста.</span><span class="sxs-lookup"><span data-stu-id="60800-132">This domain should also be listed in the [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) section of the manifest.</span></span> <span data-ttu-id="60800-133">Если этого не сделать, будет пустое всплывающее всплывающее место.</span><span class="sxs-lookup"><span data-stu-id="60800-133">Failure to do so will result in an empty pop-up.</span></span>

* <span data-ttu-id="60800-134">Отказ от использования приведет к проблеме с всплывающее всплывающее не закрывающееся в `microsoftTeams.authentication.authenticate()` конце входного знака в процессе.</span><span class="sxs-lookup"><span data-stu-id="60800-134">Failing to use `microsoftTeams.authentication.authenticate()` will cause a problem with the popup not closing at the end of the sign in process.</span></span>

## <a name="navigate-to-the-authorization-page-from-your-popup-page"></a><span data-ttu-id="60800-135">Перейдите на страницу авторизации со всплываемой страницы</span><span class="sxs-lookup"><span data-stu-id="60800-135">Navigate to the authorization page from your popup page</span></span>

<span data-ttu-id="60800-136">При показе всплываемой страницы () будет отображаться `/tab-auth/simple-start` следующий код.</span><span class="sxs-lookup"><span data-stu-id="60800-136">When your popup page (`/tab-auth/simple-start`) is displayed the following code is run.</span></span> <span data-ttu-id="60800-137">Основной целью этой страницы является перенаправление на поставщика удостоверений, чтобы пользователь может войти.</span><span class="sxs-lookup"><span data-stu-id="60800-137">The main goal of this page is to redirect to your identity provider so the user can sign in.</span></span> <span data-ttu-id="60800-138">Это перенаправление может быть сделано на стороне сервера с помощью HTTP 302, но в этом случае это делается на стороне клиента с помощью вызова `window.location.assign()` .</span><span class="sxs-lookup"><span data-stu-id="60800-138">This redirection could be done on the server side using HTTP 302, but in this case it is done on the client side using with a call to `window.location.assign()`.</span></span> <span data-ttu-id="60800-139">Это также позволяет использовать для получения подсказок, которые можно передать `microsoftTeams.getContext()` в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="60800-139">This also allows `microsoftTeams.getContext()` to be used to retrieve hinting information which can be passed to Azure AD.</span></span>

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

<span data-ttu-id="60800-140">После завершения авторизации пользователь перенаправляется на страницу вызова, указанную для вашего `/tab-auth/simple-end` приложения.</span><span class="sxs-lookup"><span data-stu-id="60800-140">After the user completes authorization, the user is redirected to the callback page you specified for your app at `/tab-auth/simple-end`.</span></span>

### <a name="notes"></a><span data-ttu-id="60800-141">Примечания</span><span class="sxs-lookup"><span data-stu-id="60800-141">Notes</span></span>

* <span data-ttu-id="60800-142">Сведения [о контексте пользователя см.](~/tabs/how-to/access-teams-context.md) в справке о создании запросов на проверку подлинности и URL-адресов.</span><span class="sxs-lookup"><span data-stu-id="60800-142">See [get user context information](~/tabs/how-to/access-teams-context.md) for help building authentication requests and URLs.</span></span> <span data-ttu-id="60800-143">Например, имя входа пользователя можно использовать в качестве значения для входа в Azure AD, что означает, что пользователю может потребоваться ввести `login_hint` меньше.</span><span class="sxs-lookup"><span data-stu-id="60800-143">For example, you can use the user's login name as the `login_hint` value for Azure AD sign-in, which means the user might need to type less.</span></span> <span data-ttu-id="60800-144">Помните, что этот контекст не следует использовать непосредственно в качестве доказательства удостоверения, так как злоумышленник может загрузить страницу в вредоносный браузер и предоставить ему любую информацию, которую он хочет.</span><span class="sxs-lookup"><span data-stu-id="60800-144">Remember that you should not use this context directly as proof of identity since an attacker could load your page in a malicious browser and provide it with any information they want.</span></span>
* <span data-ttu-id="60800-145">Хотя контекст вкладки содержит полезную информацию о пользователе, не используйте эти сведения для проверки подлинности пользователя, независимо от того, получаете ли вы его в качестве параметров URL-адреса url-адреса вкладки или вызывайте функцию в `microsoftTeams.getContext()` SDK клиента Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="60800-145">Although the tab context provides useful information regarding the user, don't use this information to authenticate the user whether you get it as URL parameters to your tab content URL or by calling the `microsoftTeams.getContext()` function in the Microsoft Teams client SDK.</span></span> <span data-ttu-id="60800-146">Злоумышленник может вызвать URL-адрес контента вкладок со своими параметрами, а веб-страница, вымышлев microsoft Teams, может загрузить URL-адрес контента вкладок в iframe и вернуть собственные данные в `getContext()` функцию.</span><span class="sxs-lookup"><span data-stu-id="60800-146">A malicious actor could invoke your tab content URL with its own parameters, and a web page impersonating Microsoft Teams could load your tab content URL in an iframe and return its own data to the `getContext()` function.</span></span> <span data-ttu-id="60800-147">Необходимо рассматривать сведения, связанные с удостоверениями, в контексте вкладок просто как подсказки и проверять их перед использованием.</span><span class="sxs-lookup"><span data-stu-id="60800-147">You should treat the identity-related information in the tab context simply as hints and validate them before use.</span></span>
* <span data-ttu-id="60800-148">Этот параметр используется для подтверждения того, что служба, вызываемая службой URI для вызова вызова, `state` является вызываемой службой.</span><span class="sxs-lookup"><span data-stu-id="60800-148">The `state` parameter is used to confirm that the service calling the callback URI is the service you called.</span></span> <span data-ttu-id="60800-149">Если параметр обратного вызова не совпадает с параметром, отправленным во время вызова, ответный вызов не проверяется и `state` должен быть прекращен.</span><span class="sxs-lookup"><span data-stu-id="60800-149">If the `state` parameter in the callback does not match the parameter you sent during the call the return call is not verified and should be terminated.</span></span>
* <span data-ttu-id="60800-150">Нет необходимости включать домен поставщика удостоверений в список в файле manifest.js`validDomains` приложения.</span><span class="sxs-lookup"><span data-stu-id="60800-150">It is not necessary to include the identity provider's domain in the `validDomains` list in the app's manifest.json file.</span></span>

## <a name="the-callback-page"></a><span data-ttu-id="60800-151">Страница вызова</span><span class="sxs-lookup"><span data-stu-id="60800-151">The callback page</span></span>

<span data-ttu-id="60800-152">В последнем разделе вы вызвали службу авторизации Azure AD и передали сведения о пользователях и приложениях, чтобы Azure AD мог представить пользователю собственный монолитный интерфейс авторизации.</span><span class="sxs-lookup"><span data-stu-id="60800-152">In the last section you called the Azure AD authorization service and passed in user and app information so that Azure AD could present the user with its own monolithic authorization experience.</span></span> <span data-ttu-id="60800-153">Ваше приложение не имеет контроля над тем, что происходит в этом опытом.</span><span class="sxs-lookup"><span data-stu-id="60800-153">Your app has no control over what happens in this experience.</span></span> <span data-ttu-id="60800-154">Все, что он знает, это то, что возвращается, когда Azure AD вызывает предоставленную страницу обратного вызова ( `/tab-auth/simple-end` ).</span><span class="sxs-lookup"><span data-stu-id="60800-154">All it knows is what is returned when Azure AD calls the  callback page that you provided (`/tab-auth/simple-end`).</span></span>

<span data-ttu-id="60800-155">На этой странице необходимо определить успешность или сбой на основе информации, возвращаемой Azure AD и вызова `microsoftTeams.authentication.notifySuccess()` или `microsoftTeams.authentication.notifyFailure()` .</span><span class="sxs-lookup"><span data-stu-id="60800-155">In this page you need to determine success or failure based on the information returned by Azure AD and call `microsoftTeams.authentication.notifySuccess()` or `microsoftTeams.authentication.notifyFailure()`.</span></span> <span data-ttu-id="60800-156">Если вход был успешным, у вас будет доступ к ресурсам службы.</span><span class="sxs-lookup"><span data-stu-id="60800-156">If the login was successful you will have access to service resources.</span></span>

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

<span data-ttu-id="60800-157">Этот код разберет пары значений ключей, полученные от Azure AD с `window.location.hash` помощью `getHashParameters()` функции помощника.</span><span class="sxs-lookup"><span data-stu-id="60800-157">This code parses the key-value pairs received from Azure AD in `window.location.hash` using the `getHashParameters()` helper function.</span></span> <span data-ttu-id="60800-158">Если он находит и значение такое же, как и то, что было предоставлено в начале потока проверки подлинности, он возвращает маркер доступа на вкладку по вызову; в противном случае он сообщает об ошибке с `access_token` `state` `notifySuccess()` `notifyFailure()` .</span><span class="sxs-lookup"><span data-stu-id="60800-158">If it finds an `access_token`, and the `state` value is the same as the one provided at the start of the authentication flow, it returns the access token to the tab by calling `notifySuccess()`; otherwise it reports an error with `notifyFailure()`.</span></span>

### <a name="notes"></a><span data-ttu-id="60800-159">Примечания</span><span class="sxs-lookup"><span data-stu-id="60800-159">Notes</span></span>

<span data-ttu-id="60800-160">`NotifyFailure()` имеет следующие предопределяемы причины сбоя:</span><span class="sxs-lookup"><span data-stu-id="60800-160">`NotifyFailure()` has the following predefined failure reasons:</span></span>

* <span data-ttu-id="60800-161">`CancelledByUser` пользователь закрыл всплывающее окно перед завершением потока проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="60800-161">`CancelledByUser` the user closed the popup window before completing the authentication flow.</span></span>
* <span data-ttu-id="60800-162">`FailedToOpenWindow` окно всплывающих окон не удалось открыть.</span><span class="sxs-lookup"><span data-stu-id="60800-162">`FailedToOpenWindow` the popup window could not be opened.</span></span> <span data-ttu-id="60800-163">При запуске Microsoft Teams в браузере это обычно означает, что окно было заблокировано блокатором всплывающих окон.</span><span class="sxs-lookup"><span data-stu-id="60800-163">When running Microsoft Teams in a browser, this typically means that the window was blocked by a popup blocker.</span></span>

<span data-ttu-id="60800-164">В случае успешной работы вы можете обновить или перезагрузить страницу и показать содержимое, релевантные пользователю, который сейчас имеет проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="60800-164">If successful, you can refresh or reload the page and show content relevant to the now-authenticated user.</span></span> <span data-ttu-id="60800-165">Если проверка подлинности не удается, отобразить сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="60800-165">If authentication fails, display an error message.</span></span>

<span data-ttu-id="60800-166">Ваше приложение может настроить свое собственное cookie сеанса, чтобы пользователю не нужно было снова входить, когда он возвращается на вкладку на текущем устройстве.</span><span class="sxs-lookup"><span data-stu-id="60800-166">Your app can set its own session cookie so that the user need not sign in again when they return to your tab on the current device.</span></span>

> [!NOTE]
> <span data-ttu-id="60800-167">Chrome 80, запланированный на выпуск в начале 2020 г., вводит новые значения cookie и по умолчанию вводит политики cookie.</span><span class="sxs-lookup"><span data-stu-id="60800-167">Chrome 80, scheduled for release in early 2020, introduces new cookie values and imposes cookie policies by default.</span></span> <span data-ttu-id="60800-168">Рекомендуется установить предназначенное использование для файлов cookie, а не полагаться на поведение браузера по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="60800-168">It's recommended that you set the intended use for your cookies rather than rely on default browser behavior.</span></span> <span data-ttu-id="60800-169">*См.* [атрибут cookie SameSite (обновление 2020 г.).](../../../resources/samesite-cookie-update.md)</span><span class="sxs-lookup"><span data-stu-id="60800-169">*See* [SameSite cookie attribute (2020 update)](../../../resources/samesite-cookie-update.md).</span></span>

>[!NOTE]
><span data-ttu-id="60800-170">Чтобы получить правильный маркер для бесплатных и гостевых пользователей Microsoft Teams, важно, чтобы приложения использовали конечную точку https://login.microsoftonline.com/ **клиента {tenantId}**.</span><span class="sxs-lookup"><span data-stu-id="60800-170">To get the correct token for Microsoft Teams Free and guest users, it is important that the apps use tenant specific endpoint https://login.microsoftonline.com/**{tenantId}**.</span></span> <span data-ttu-id="60800-171">Вы можете получить tenantId из сообщения бота или контекста вкладок.</span><span class="sxs-lookup"><span data-stu-id="60800-171">You can get tenantId from the bot message or tab context.</span></span> <span data-ttu-id="60800-172">Если приложения используют, пользователи получат неправильные маркеры и войдите в "домашний" клиент вместо клиента, в который они в настоящее время https://login.microsoftonline.com/common подписаны.</span><span class="sxs-lookup"><span data-stu-id="60800-172">If the apps use https://login.microsoftonline.com/common, the users will get incorrect tokens and will log on to the "home" tenant instead of the tenant that they are currently signed into.</span></span>

<span data-ttu-id="60800-173">Дополнительные сведения о едином Sign-On (SSO) см. в статье [Silent authentication](~/tabs/how-to/authentication/auth-silent-AAD.md).</span><span class="sxs-lookup"><span data-stu-id="60800-173">For more information on Single Sign-On (SSO) see the article [Silent authentication](~/tabs/how-to/authentication/auth-silent-AAD.md).</span></span>

## <a name="code-sample"></a><span data-ttu-id="60800-174">Пример кода</span><span class="sxs-lookup"><span data-stu-id="60800-174">Code sample</span></span>

<span data-ttu-id="60800-175">Пример кода, показывающий процесс проверки подлинности вкладок с помощью Azure AD:</span><span class="sxs-lookup"><span data-stu-id="60800-175">Sample code showing the tab authentication process using Azure AD:</span></span>

| <span data-ttu-id="60800-176">**Пример имени**</span><span class="sxs-lookup"><span data-stu-id="60800-176">**Sample name**</span></span> | <span data-ttu-id="60800-177">**description**</span><span class="sxs-lookup"><span data-stu-id="60800-177">**description**</span></span> | <span data-ttu-id="60800-178">**.NET**</span><span class="sxs-lookup"><span data-stu-id="60800-178">**.NET**</span></span> | <span data-ttu-id="60800-179">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="60800-179">**Node.js**</span></span> |
|-----------------|-----------------|-------------|
| <span data-ttu-id="60800-180">Проверка подлинности вкладок Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="60800-180">Microsoft Teams tab authentication</span></span> | <span data-ttu-id="60800-181">Процесс проверки подлинности вкладок с помощью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="60800-181">Tab authentication process using Azure AD.</span></span> | [<span data-ttu-id="60800-182">View</span><span class="sxs-lookup"><span data-stu-id="60800-182">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group-config-page-auth/csharp) | [<span data-ttu-id="60800-183">View</span><span class="sxs-lookup"><span data-stu-id="60800-183">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-auth/nodejs) |
