---
title: Проверка подлинности для вкладок с помощью Azure Active Directory
description: Описывает проверку подлинности в Teams и способы ее использования на вкладке
ms.topic: how-to
ms.localizationpriority: high
keywords: вкладки проверка подлинности Teams Microsoft Azure Active Directory (Azure AD)
ms.openlocfilehash: 3341c7235e3fdbfeb401e6d22abf0869c1e9b181
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111677"
---
# <a name="authenticate-a-user-in-a-microsoft-teams-tab"></a>Проверка подлинности пользователя на вкладке Microsoft Teams

> [!Note]
> Для работы проверки подлинности на вкладке на мобильных клиентах сначала убедитесь, что вы используете версию 1.4.1 или более позднюю версию пакета SDK Teams JavaScript.

Существует множество служб, которые можно использовать в приложении Teams, и большинство из них требуют проверки подлинности и авторизации для получения доступа к службе. К службам относятся Facebook, Twitter и Teams. Профиль пользователя Teams хранится в Azure AD с помощью Microsoft Graph. В этой статье основное внимание уделяется проверке подлинности с помощью Azure AD для получения доступа к этой информации.

OAuth 2.0 — это открытый стандарт проверки подлинности и авторизации, используемый Azure Active Directory (Azure AD) и многими другими поставщиками удостоверений. Понимание механизма OAuth 2.0 необходимо для работы с проверкой подлинности в Teams и Azure AD. В приведенных ниже примерах используется поток неявного предоставления OAuth 2.0 с конечной целью считывания сведений о профиле пользователя из Azure AD и Microsoft Graph.

Программный код, приведенный в этой статье, взят из примера приложения Teams [Пример проверки подлинности Microsoft Teams на вкладке (Node)](https://github.com/OfficeDev/microsoft-teams-sample-complete-node). В примере используется статическая вкладка, которая запрашивает маркер доступа для Microsoft Graph и отображает основные сведения о профиле текущего пользователя из Azure AD.

Общие сведения о потоке проверки подлинности для вкладок см. в разделе [Поток проверки подлинности для вкладок](~/tabs/how-to/authentication/auth-flow-tab.md).

Поток проверки подлинности для вкладок немного отличается от потока проверки подлинности для ботов.

## <a name="configuring-identity-providers"></a>Настройка поставщиков удостоверений

Подробные инструкции по настройке URL-адресов перенаправления обратного вызова OAuth 2.0 при использовании Azure AD в качестве поставщика удостоверений см. в разделе [Настройка поставщиков удостоверений](~/concepts/authentication/configure-identity-provider.md).

## <a name="initiate-authentication-flow"></a>Запуск потока проверки подлинности

Поток проверки подлинности должен активироваться действием пользователя. Не следует открывать всплывающее окно проверки подлинности автоматически, так как это, скорее всего, активирует блокировку всплывающих элементов браузера, а также запутает пользователя.

Добавьте кнопку на страницу конфигурации или содержимого, чтобы пользователь при необходимости мог входить в систему. Это можно сделать на странице [конфигурации](~/tabs/how-to/create-tab-pages/configuration-page.md) вкладки или на любой странице [содержимого](~/tabs/how-to/create-tab-pages/content-page.md).

Azure AD, как и большинство поставщиков удостоверений, не позволяет помещать свое содержимое в iframe. Это означает, что для размещения поставщика удостоверений придется добавить всплывающее окно. В следующем примере эта страница - `/tab-auth/simple-start`. Используйте функцию `microsoftTeams.authenticate()` пакета SDK клиента Microsoft Teams, чтобы запустить эту страницу при нажатии кнопки.

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

* Передаваемый URL-адрес `microsoftTeams.authentication.authenticate()` является начальной страницей потока проверки подлинности. В данном примере это `/tab-auth/simple-start`. Он должен совпадать с адресом, который вы зарегистрировали на [портале регистрации приложений Azure AD](https://apps.dev.microsoft.com).

* Поток проверки подлинности должен начинаться на странице, которая находится в вашем домене. Этот домен также должен быть указан в [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) разделе манифеста. Если этого не сделать, вы увидите пустое всплывающее окно.

* Если вы не используете `microsoftTeams.authentication.authenticate()`, возникнет проблема: всплывающее окно не закроется по окончании процесса входа.

## <a name="navigate-to-the-authorization-page-from-your-pop-up-page"></a>Со всплывающей страницы перейдите на страницу авторизации

При показе всплывающей страницы (`/tab-auth/simple-start`) выполняется следующий код. Основная цель этой страницы — перенаправление к поставщику удостоверений, чтобы пользователь мог войти в систему. Это перенаправление может быть выполнено на стороне сервера с помощью HTTP 302, но в данном случае это делается на стороне клиента с помощью вызова `window.location.assign()`. Это также позволяет методу `microsoftTeams.getContext()` получать подсказки, которые можно передать в Azure AD.

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

После завершения авторизации пользователь перенаправляется на страницу обратного вызова для вашего приложения, указанную в `/tab-auth/simple-end`.

### <a name="notes"></a>Примечания

* Подробнее о создании запросов и URL-адресов проверки подлинности см. в статье [Получение сведений о контексте пользователя](~/tabs/how-to/access-teams-context.md). Например, можно использовать в качестве значения `login_hint` для входа в Azure AD имя пользователя: тогда пользователю придется вводить меньше информации вручную. Помните, что этот контекст не следует использовать непосредственно в качестве подтверждения личности, так как злоумышленник может загрузить вашу страницу во вредоносный браузер и подсунуть туда любые данные.
* Хотя контекст вкладки предоставляет полезные сведения о пользователе, не используйте эти сведения для проверки подлинности пользователя независимо от того, получаете ли вы его в качестве параметров для URL-адреса содержимого вкладки или путем вызова функции `microsoftTeams.getContext()` в пакете SDK клиента Microsoft Teams. Злоумышленник может вызвать URL-адрес содержимого вкладки с собственными параметрами, и веб-страница, мимикрирующая под Microsoft Teams, может загрузить URL-адрес содержимого вкладки в iframe и передать функции `getContext()` свои собственные данные. Сведения, связанные с удостоверениями, следует рассматривать в контексте вкладки просто как подсказки и проверять их перед использованием.
* Параметр `state` используется для подтверждения того, что служба, вызывающая URI обратного вызова - именно та, которую вызывали вы. Если параметр `state` в обратном вызове не совпадает с параметром, отправленным во время вызова, обратный вызов не прошел проверку, и его следует прервать.
* Нет необходимости включать домен поставщика удостоверений в список `validDomains` в файле manifest.json приложения.

## <a name="the-callback-page"></a>Страница обратного вызова

В последнем разделе вы вызвали службу авторизации Azure AD и передали сведения о пользователе и приложении, чтобы Azure AD могла предоставить пользователю собственный монолитный интерфейс авторизации. Ваше приложение не контролирует, что происходит в этом интерфейсе. Приложению известно только, что возвращается, когда Azure AD вызывает предоставленную вами страницу обратного вызова (`/tab-auth/simple-end`).

На этой странице вы должны определить, пройдена проверка или нет, на основе информации, возвращенной Azure AD, и вызвать `microsoftTeams.authentication.notifySuccess()` или `microsoftTeams.authentication.notifyFailure()`. Если вход выполнен успешно, у вас появится доступ к ресурсам службы.

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

В этом коде анализируются пары "ключ-значение", полученные от Azure AD в `window.location.hash`, с помощью вспомогательной функции `getHashParameters()`. Если найден `access_token` и значение `state` совпадает со значением, указанным в начале потока проверки подлинности, возвращается маркер доступа на вкладку путем вызова `notifySuccess()`; в противном случае генерируется сообщение об ошибке с помощью `notifyFailure()`.

### <a name="notes"></a>Примечания

Сообщение `NotifyFailure()` имеет следующие предопределенные причины:

* `CancelledByUser`: пользователь закрыл всплывающее окно до завершения потока проверки подлинности.
* `FailedToOpenWindow`: не удалось открыть всплывающее окно. При запуске Microsoft Teams в браузере эта ошибка указывает на то, что окно было заблокировано блокировщиком всплывающих окон браузера.

Если проверка подлинности пройдена успешно, вы можете обновить или перезагрузить страницу и показать содержимое, нужное пользователю, прошедшему проверку подлинности. Если проверка подлинности не пройдена, выдается сообщение об ошибке.

Приложение может задать собственный файл cookie сеанса, чтобы пользователю не нужно было заново входить в систему при возврате на вкладку на текущем устройстве.

> [!NOTE]
>
> * Chrome 80, запланированный на выпуск в начале 2020 г., вводит новые значения файлов cookie и по умолчанию реализует политики файлов cookie. Рекомендуем задать использование файлов cookie в явном виде, а не полагаться на поведение браузера по умолчанию. *См. статью*[ Атрибут cookie SameSite (обновление 2020)](../../../resources/samesite-cookie-update.md).
> * Чтобы получить правильный маркер для Microsoft Teams и гостевых пользователей, приложения должны использовать конечную точку конкретного клиента`https://login.microsoftonline.com/**{tenantId}**`. Идентификатор клиента можно получить из сообщения бота или контекста вкладки. Если приложения используют `https://login.microsoftonline.com/common`, пользователи получат неправильные маркеры и будет выполнен вход в "домашний" клиент, а не в тот, в который они входят в данный момент.

Дополнительные сведения о едином входе (SSO) см. в статье [Автоматическая проверка подлинности](~/tabs/how-to/authentication/auth-silent-AAD.md).

## <a name="code-sample"></a>Пример кода

Пример кода, показывающий процесс проверки подлинности с помощью Azure AD:

| **Название примера** | **description** | **.NET** | **Node.js** |
|-----------------|-----------------|-------------|
| Проверка подлинности для вкладок Microsoft Teams | Процесс проверки подлинности с помощью Azure AD. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group-config-page-auth/csharp) | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-auth/nodejs) |

## <a name="see-also"></a>Дополнительные ресурсы

* [Планирование проверки подлинности пользователей](../../../concepts/design/understand-use-cases.md)
* [Разработка вкладки для Microsoft Teams](~/tabs/design/tabs.md)
* [Автоматическая проверка подлинности](~/tabs/how-to/authentication/auth-silent-aad.md)
* [Добавление проверки подлинности в расширение для сообщений](~/messaging-extensions/how-to/add-authentication.md)
* [Поддержка единого входа (SSO) для ботов](~/bots/how-to/authentication/auth-aad-sso-bots.md)
