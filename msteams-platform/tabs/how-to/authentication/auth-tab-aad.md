---
title: Проверка подлинности для вкладок с Azure Active Directory
description: Описывает проверку подлинности в Teams и ее использование на вкладке
ms.topic: how-to
ms.localizationpriority: medium
keywords: вкладки проверки подлинности Microsoft Azure Active Directory групп (Azure AD)
ms.openlocfilehash: 65020b91931782b985243a410792a4f7aab3b01e
ms.sourcegitcommit: 90587b1ec04bf20d716ed6feb8ccca4313e87f8c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/10/2022
ms.locfileid: "62518557"
---
# <a name="authenticate-a-user-in-a-microsoft-teams-tab"></a>Проверка подлинности пользователя на вкладке Microsoft Teams

> [!Note]
> Для проверки подлинности для работы вкладки на мобильных клиентах необходимо убедиться, что вы используете версию 1.4.1 или более поздней версии Teams JavaScript SDK.

Существует множество служб, которые можно использовать в приложении Teams, и большинство из них требуют проверки подлинности и авторизации для получения доступа к службе. Службы включают Facebook, Twitter и Teams. Teams сведения о профиле пользователя хранятся в Microsoft Azure Active Directory (Azure AD) с помощью Microsoft Graph и в этой статье основное внимание будет уделяться проверке подлинности с помощью Microsoft Azure Active Directory (Azure AD), чтобы получить доступ к этой информации.

OAuth 2.0 — это открытый стандарт проверки подлинности, используемый Microsoft Azure Active Directory (Azure AD) и многими другими поставщиками услуг. Понимание OAuth 2.0 является обязательным условием для работы с проверкой подлинности в Teams и Microsoft Azure Active Directory (Azure AD). В приведенных ниже примерах используется поток неявных грантов OAuth 2.0 с целью в конечном итоге считыть сведения о профиле пользователя из Microsoft Azure Active Directory (Azure AD) и Microsoft Graph.

Код в этой статье происходит из примера Teams приложения Microsoft Teams [проверки подлинности вкладок (Node)](https://github.com/OfficeDev/microsoft-teams-sample-complete-node). Она содержит статическую вкладку, которая запрашивает маркер доступа для Microsoft Graph и отображает основные сведения о профиле текущего пользователя из Microsoft Azure Active Directory (Azure AD).

Общий обзор потока проверки подлинности для вкладок см. в вкладке [Поток проверки подлинности](~/tabs/how-to/authentication/auth-flow-tab.md).

Поток проверки подлинности на вкладке немного отличается от потока проверки подлинности в ботах.

## <a name="configuring-identity-providers"></a>Настройка поставщиков удостоверений

См. в [](~/concepts/authentication/configure-identity-provider.md) разделе Настройка поставщиков удостоверений для подробных действий по настройке URL-адреса перенаправления вызовов OAuth 2.0 при использовании Microsoft Azure Active Directory (Azure AD) в качестве поставщика удостоверений.

## <a name="initiate-authentication-flow"></a>Начало потока проверки подлинности

Поток проверки подлинности должен быть вызван действием пользователя. Не следует автоматически открывать всплывающее всплывающее окна проверки подлинности, так как это, скорее всего, вызовет блокировку всплывающее окна браузера, а также запутает пользователя.

Добавьте кнопку на страницу конфигурации или контента, чтобы пользователь в случае необходимости вход в нее входит. Это можно сделать на странице конфигурации [вкладок](~/tabs/how-to/create-tab-pages/configuration-page.md) или на любой [странице контента](~/tabs/how-to/create-tab-pages/content-page.md) .

Microsoft Azure Active Directory Azure AD, как и большинство поставщиков удостоверений, не позволяет размещать его содержимое в iframe. Это означает, что для хозяйского поставщика удостоверений необходимо добавить всплывающее всплывающее лицо. В следующем примере эта страница .`/tab-auth/simple-start` Используйте функцию `microsoftTeams.authenticate()` SDK Microsoft Teams клиента, чтобы запустить эту страницу при выборе кнопки.

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

* URL-адрес, на который вы передаете `microsoftTeams.authentication.authenticate()` , является началом потока проверки подлинности. В этом примере это `/tab-auth/simple-start`. Это должно совпадать с тем, что вы зарегистрировали на портале регистрации [Microsoft Azure Active Directory приложений (Azure AD](https://apps.dev.microsoft.com)).

* Поток проверки подлинности должен начинаться на странице, которая на вашем домене. Этот домен также должен быть указан в разделе [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) манифеста. Если этого не сделать, будет пустое всплывающее всплывающее место.

* Отказ от использования `microsoftTeams.authentication.authenticate()` приведет к проблеме с всплывающее всплывающее не закрывающееся в конце входного знака в процессе.

## <a name="navigate-to-the-authorization-page-from-your-pop-up-page"></a>Перейдите на страницу авторизации со всплываемой страницы

После отображения всплываемой страницы (`/tab-auth/simple-start`) будет запускаться следующий код. Основной целью этой страницы является перенаправление на поставщика удостоверений, чтобы пользователь может войти. Это перенаправление может быть сделано на стороне сервера с помощью HTTP 302, но в этом случае это делается на стороне клиента с помощью вызова `window.location.assign()`. Это также позволяет использовать `microsoftTeams.getContext()` для получения подсказок, которые можно передать в Microsoft Azure Active Directory Azure AD.

```javascript
microsoftTeams.getContext(function (context) {
    // Generate random state string and store it, so we can verify it in the callback
    let state = _guid(); // _guid() is a helper function in the sample
    localStorage.setItem("simple.state", state);
    localStorage.removeItem("simple.error");
    // Go to the Microsoft Azure Active Directory (Azure AD) authorization endpoint
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

После завершения авторизации пользователь перенаправляется на страницу вызова, указанную для вашего приложения `/tab-auth/simple-end`.

### <a name="notes"></a>Примечания

* Сведения [о контексте пользователя см](~/tabs/how-to/access-teams-context.md) . в справке о создании запросов на проверку подлинности и URL-адресов. Например, можно `login_hint` использовать имя входа пользователя в качестве значения для входа Microsoft Azure Active Directory Azure AD, что означает, что пользователю может потребоваться ввести меньше. Помните, что этот контекст не следует использовать непосредственно в качестве доказательства удостоверения, так как злоумышленник может загрузить страницу в вредоносный браузер и предоставить ему любую информацию, которую он хочет.
* Хотя контекст вкладки предоставляет полезную информацию о пользователе, `microsoftTeams.getContext()` не используйте эти сведения для проверки подлинности пользователя, независимо от того, получаете ли вы его в качестве параметров URL-адреса на URL-адрес контента вкладки или вызываете функцию в SDK клиента Microsoft Teams клиента. Злоумышленник может вызвать URL-адрес контента вкладки со своими параметрами, а веб-страница, Microsoft Teams может загрузить URL-адрес контента вкладки в iframe `getContext()` и вернуть собственные данные в функцию. Необходимо рассматривать сведения, связанные с удостоверениями, в контексте вкладок просто как подсказки и проверять их перед использованием.
* Этот `state` параметр используется для подтверждения того, что служба, вызываемая службой URI для вызова вызова, является вызываемой службой. Если параметр `state` обратного вызова не совпадает с параметром, отправленным во время вызова, ответный вызов не проверяется и должен быть прекращен.
* Нет необходимости включать домен поставщика удостоверений `validDomains` в список в файле manifest.json приложения.

## <a name="the-callback-page"></a>Страница вызова

В последнем разделе вы вызвали службу авторизации Microsoft Azure Active Directory Azure AD и передали сведения о пользователях и приложениях, чтобы Microsoft Azure Active Directory (Azure AD) могли представить пользователю собственный монолитный интерфейс авторизации. Ваше приложение не имеет контроля над тем, что происходит в этом опытом. Все, что он знает, возвращается, когда Microsoft Azure Active Directory (Azure AD) вызывает предоставленную страницу обратного вызова (`/tab-auth/simple-end`).

На этой странице необходимо определить успех или сбой на основе информации, возвращаемой Microsoft Azure Active Directory (Azure AD) и вызова `microsoftTeams.authentication.notifySuccess()` или `microsoftTeams.authentication.notifyFailure()`. Если вход был успешным, у вас будет доступ к ресурсам службы.

````javascript
// Split the key-value pairs passed from Microsoft Azure Active Directory (Azure AD)
// getHashParameters is a helper function that parses the arguments sent
// to the callback URL by Microsoft Azure Active Directory (Azure AD) after the authorization call
let hashParams = getHashParameters();
if (hashParams["error"]) {
    // Authentication/authorization failed
    microsoftTeams.authentication.notifyFailure(hashParams["error"]);
} else if (hashParams["access_token"]) {
    // Get the stored state parameter and compare with incoming state
    // This validates that the data is coming from Microsoft Azure Active Directory (Azure AD)
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

В этом коде размыкаются пары значений ключей, полученные от Microsoft Azure Active Directory Azure AD при `window.location.hash` `getHashParameters()` использовании функции помощника. `access_token``state` Если он находит и значение такое же, как и то, что было предоставлено в начале потока проверки подлинности, `notifySuccess()`он возвращает маркер доступа на вкладку по вызову; `notifyFailure()`в противном случае он сообщает об ошибке с .

### <a name="notes"></a>Примечания

`NotifyFailure()` имеет следующие предопределяемы причины сбоя:

* `CancelledByUser` пользователь закрыл всплывающее окно перед завершением потока проверки подлинности.
* `FailedToOpenWindow` всплывающее окно не удалось открыть. При Microsoft Teams браузере это обычно означает, что окно было заблокировано блокатором всплывающих окон.

В случае успешной работы вы можете обновить или перезагрузить страницу и показать содержимое, релевантные пользователю, который сейчас имеет проверку подлинности. Если проверка подлинности не удается, она отображает сообщение об ошибке.

Ваше приложение может настроить свое собственное cookie сеанса, чтобы пользователю не нужно было снова входить, когда он возвращается на вкладку на текущем устройстве.

> [!NOTE]
> Chrome 80, запланированный на выпуск в начале 2020 г., вводит новые значения cookie и по умолчанию вводит политики cookie. Рекомендуется установить предназначенное использование для файлов cookie, а не полагаться на поведение браузера по умолчанию. *См*[. атрибут cookie SameSite (обновление 2020 г.)](../../../resources/samesite-cookie-update.md).

>[!NOTE]
>Чтобы получить правильный маркер для Microsoft Teams и гостевых пользователей, важно, `https://login.microsoftonline.com/**{tenantId}**`чтобы приложения использовали конечную точку клиента. Вы можете получить tenantId из сообщения бота или контекста вкладок. Если приложения используют `https://login.microsoftonline.com/common`, пользователи получат неправильные маркеры и войдите в "домашний" клиент вместо клиента, в который они в настоящее время подписаны.

Дополнительные сведения о единой Sign-On (SSO) см. в статье [Silent authentication](~/tabs/how-to/authentication/auth-silent-AAD.md).

## <a name="code-sample"></a>Пример кода

Пример кода, показывающий процесс проверки подлинности вкладок с Microsoft Azure Active Directory (Azure AD):

| **Название примера** | **description** | **.NET** | **Node.js** |
|-----------------|-----------------|-------------|
| Microsoft Teams проверки подлинности вкладок | Процесс проверки подлинности вкладок с Microsoft Azure Active Directory (Azure AD). | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group-config-page-auth/csharp) | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-auth/nodejs) |

## <a name="see-also"></a>Дополнительные ресурсы

* [Планирование проверки подлинности пользователей](../../../concepts/design/understand-use-cases.md#provide-authentication)
* [Разработка вкладки для Microsoft Teams](~/tabs/design/tabs.md)
* [Бесшумная проверка подлинности](~/tabs/how-to/authentication/auth-silent-aad.md)
* [Добавление проверки подлинности в расширение для сообщений](~/messaging-extensions/how-to/add-authentication.md)
* [Поддержка единого входного знака (SSO) для ботов](~/bots/how-to/authentication/auth-aad-sso-bots.md)
