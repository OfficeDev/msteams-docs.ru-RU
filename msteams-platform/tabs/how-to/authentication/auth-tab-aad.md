---
title: Проверка подлинности для вкладок с Azure Active Directory
description: Описывает проверку подлинности в Teams и ее использование на вкладке
ms.topic: how-to
ms.localizationpriority: medium
keywords: группы проверки подлинности вкладок AAD
ms.openlocfilehash: 6bd963a0ff6eee8b239693904fdf30798fd192d0
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/12/2021
ms.locfileid: "59156096"
---
# <a name="authenticate-a-user-in-a-microsoft-teams-tab"></a>Проверка подлинности пользователя на вкладке Microsoft Teams

> [!Note]
> Для проверки подлинности для работы вкладки на мобильных клиентах необходимо убедиться, что вы используете версию 1.4.1 или более поздней версии Teams JavaScript SDK.

Существует множество служб, которые можно использовать в приложении Teams, и большинство из них требуют проверки подлинности и авторизации для получения доступа к службе. Службы включают Facebook, Twitter и, конечно, Teams. Пользователи Teams имеют сведения о профиле пользователей в Azure Active Directory (Azure AD) с помощью Microsoft Graph и в этой статье основное внимание будет уделялось проверке подлинности с помощью Azure AD для получения доступа к этой информации.

OAuth 2.0 — это открытый стандарт проверки подлинности, используемый Azure AD и многими другими поставщиками услуг. Понимание OAuth 2.0 является обязательным условием для работы с проверкой подлинности в Teams Azure AD. В примерах ниже используется поток неявных грантов OAuth 2.0 с целью в конечном итоге прочитать сведения о профиле пользователя из Azure AD и Microsoft Graph.

Код в этой статье происходит из примера Teams приложения Microsoft Teams проверки подлинности [вкладок (Node).](https://github.com/OfficeDev/microsoft-teams-sample-complete-node) Она содержит статическую вкладку, которая запрашивает маркер доступа для Microsoft Graph и отображает основные сведения о профиле текущего пользователя из Azure AD.

Общий обзор потока проверки подлинности для вкладок см. в разделе Поток проверки подлинности [на вкладке](~/tabs/how-to/authentication/auth-flow-tab.md).

Поток проверки подлинности на вкладке немного отличается от потока проверки подлинности в ботах.

## <a name="configuring-identity-providers"></a>Настройка поставщиков удостоверений

См. [](~/concepts/authentication/configure-identity-provider.md) в разделе Настройка поставщиков удостоверений для подробных действий по настройке URL-адреса перенаправления вызовов OAuth 2.0 при использовании Azure Active Directory в качестве поставщика удостоверений.

## <a name="initiate-authentication-flow"></a>Начало потока проверки подлинности

Поток проверки подлинности должен быть вызван действием пользователя. Не следует автоматически открывать всплывающее всплывающее окна проверки подлинности, так как это, скорее всего, вызовет блокировку всплывающее окна браузера, а также запутает пользователя.

Добавьте кнопку на страницу конфигурации или контента, чтобы пользователь в случае необходимости вход в нее входит. Это можно сделать на странице конфигурации [вкладок](~/tabs/how-to/create-tab-pages/configuration-page.md) или на любой [странице контента.](~/tabs/how-to/create-tab-pages/content-page.md)

Azure AD, как и большинство поставщиков удостоверений, не позволяет размещать содержимое в iframe. Это означает, что для хозяйского поставщика удостоверений необходимо добавить всплывающее всплывающее лицо. В следующем примере эта страница `/tab-auth/simple-start` . Используйте функцию SDK Microsoft Teams клиента, чтобы запустить эту страницу при выборе `microsoftTeams.authenticate()` кнопки.

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

### <a name="notes"></a>Примечания

* URL-адрес, на который `microsoftTeams.authentication.authenticate()` вы передаете, является началом потока проверки подлинности. В этом примере это `/tab-auth/simple-start` . Это должно совпадать с тем, что вы зарегистрировали на портале регистрации приложений [Azure AD.](https://apps.dev.microsoft.com)

* Поток проверки подлинности должен начинаться на странице, которая на вашем домене. Этот домен также должен быть указан в [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) разделе манифеста. Если этого не сделать, будет пустое всплывающее всплывающее место.

* Отказ от использования приведет к проблеме с всплывающее всплывающее не закрывающееся в `microsoftTeams.authentication.authenticate()` конце входного знака в процессе.

## <a name="navigate-to-the-authorization-page-from-your-popup-page"></a>Перейдите на страницу авторизации со всплываемой страницы

При показе всплываемой страницы () будет отображаться `/tab-auth/simple-start` следующий код. Основной целью этой страницы является перенаправление на поставщика удостоверений, чтобы пользователь может войти. Это перенаправление может быть сделано на стороне сервера с помощью HTTP 302, но в этом случае это делается на стороне клиента с помощью вызова `window.location.assign()` . Это также позволяет использовать для получения подсказок, которые можно передать `microsoftTeams.getContext()` в Azure AD.

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

После завершения авторизации пользователь перенаправляется на страницу вызова, указанную для вашего `/tab-auth/simple-end` приложения.

### <a name="notes"></a>Примечания

* Сведения [о контексте пользователя см.](~/tabs/how-to/access-teams-context.md) в справке о создании запросов на проверку подлинности и URL-адресов. Например, имя входа пользователя можно использовать в качестве значения для входа в Azure AD, что означает, что пользователю может потребоваться ввести `login_hint` меньше. Помните, что этот контекст не следует использовать непосредственно в качестве доказательства удостоверения, так как злоумышленник может загрузить страницу в вредоносный браузер и предоставить ему любую информацию, которую он хочет.
* Хотя контекст вкладки предоставляет полезную информацию о пользователе, не используйте эти сведения для проверки подлинности пользователя, независимо от того, получаете ли вы его в качестве параметров URL-адреса на URL-адрес контента вкладки или вызываете функцию в `microsoftTeams.getContext()` SDK клиента Microsoft Teams клиента. Злоумышленник может вызвать URL-адрес контента вкладки со своими параметрами, а веб-страница, Microsoft Teams может загрузить URL-адрес контента вкладки в iframe и вернуть собственные данные в `getContext()` функцию. Необходимо рассматривать сведения, связанные с удостоверениями, в контексте вкладок просто как подсказки и проверять их перед использованием.
* Этот параметр используется для подтверждения того, что служба, вызываемая службой URI для вызова вызова, `state` является вызываемой службой. Если параметр обратного вызова не совпадает с параметром, отправленным во время вызова, ответный вызов не проверяется и `state` должен быть прекращен.
* Нет необходимости включать домен поставщика удостоверений в список в файле manifest.js`validDomains` приложения.

## <a name="the-callback-page"></a>Страница вызова

В последнем разделе вы вызвали службу авторизации Azure AD и передали сведения о пользователях и приложениях, чтобы Azure AD мог представить пользователю собственный монолитный интерфейс авторизации. Ваше приложение не имеет контроля над тем, что происходит в этом опытом. Все, что он знает, это то, что возвращается, когда Azure AD вызывает предоставленную страницу обратного вызова ( `/tab-auth/simple-end` ).

На этой странице необходимо определить успешность или сбой на основе информации, возвращаемой Azure AD и вызова `microsoftTeams.authentication.notifySuccess()` или `microsoftTeams.authentication.notifyFailure()` . Если вход был успешным, у вас будет доступ к ресурсам службы.

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

Этот код разберет пары значений ключей, полученные от Azure AD с `window.location.hash` помощью `getHashParameters()` функции помощника. Если он находит и значение такое же, как и то, что было предоставлено в начале потока проверки подлинности, он возвращает маркер доступа на вкладку по вызову; в противном случае он сообщает об ошибке с `access_token` `state` `notifySuccess()` `notifyFailure()` .

### <a name="notes"></a>Примечания

`NotifyFailure()` имеет следующие предопределяемы причины сбоя:

* `CancelledByUser` пользователь закрыл всплывающее окно перед завершением потока проверки подлинности.
* `FailedToOpenWindow` окно всплывающих окон не удалось открыть. При Microsoft Teams в браузере это обычно означает, что окно было заблокировано блокатором всплывающих окон.

В случае успешной работы вы можете обновить или перезагрузить страницу и показать содержимое, релевантные пользователю, который сейчас имеет проверку подлинности. Если проверка подлинности не удается, отобразить сообщение об ошибке.

Ваше приложение может настроить свое собственное cookie сеанса, чтобы пользователю не нужно было снова входить, когда он возвращается на вкладку на текущем устройстве.

> [!NOTE]
> Chrome 80, запланированный на выпуск в начале 2020 г., вводит новые значения cookie и по умолчанию вводит политики cookie. Рекомендуется установить предназначенное использование для файлов cookie, а не полагаться на поведение браузера по умолчанию. *См.* [атрибут cookie SameSite (обновление 2020 г.).](../../../resources/samesite-cookie-update.md)

>[!NOTE]
>Чтобы получить правильный маркер для Microsoft Teams и гостевых пользователей, важно, чтобы приложения использовали конечную точку `https://login.microsoftonline.com/**{tenantId}**` клиента. Вы можете получить tenantId из сообщения бота или контекста вкладок. Если приложения используют, пользователи получат неправильные маркеры и войдите в "домашний" клиент вместо клиента, в который они в настоящее время `https://login.microsoftonline.com/common` подписаны.

Дополнительные сведения о едином Sign-On (SSO) см. в статье [Silent authentication](~/tabs/how-to/authentication/auth-silent-AAD.md).

## <a name="code-sample"></a>Пример кода

Пример кода, показывающий процесс проверки подлинности вкладок с помощью Azure AD:

| **Название примера** | **description** | **.NET** | **Node.js** |
|-----------------|-----------------|-------------|
| Microsoft Teams проверки подлинности вкладок | Процесс проверки подлинности вкладок с помощью Azure AD. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group-config-page-auth/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-auth/nodejs) |
