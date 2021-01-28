---
title: Проверка подлинности вкладок с помощью Azure Active Directory
description: Описание проверки подлинности в Teams и ее использования на вкладке
ms.topic: how-to
keywords: Вкладки проверки подлинности teams AAD
ms.openlocfilehash: 1502d2634b39230e0428863383bf97ada0be0359
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014567"
---
# <a name="authenticate-a-user-in-a-microsoft-teams-tab"></a>Проверка подлинности пользователя на вкладке Microsoft Teams

> [!Note]
> Чтобы проверка подлинности работала для вашей вкладки на мобильных клиентах, необходимо убедиться, что вы используете версию 1.4.1 или более поздней версии SDK JavaScript для Teams.

Существует множество служб, которые можно использовать в приложении Teams, и большинство из них требуют проверки подлинности и авторизации для получения доступа к службе. К службам относятся Facebook, Twitter и, конечно, Teams. Данные профилей пользователей Teams хранятся в Azure Active Directory (Azure AD) с помощью Microsoft Graph, и эта статья посвящена проверке подлинности с помощью Azure AD для получения доступа к этой информации.

OAuth 2.0 — это открытый стандарт проверки подлинности, используемый Azure AD и многими другими поставщиками услуг. Понимание OAuth 2.0 является необходимым условием для работы с проверкой подлинности в Teams и Azure AD. В примерах ниже используется неявный поток предоставления OAuth 2.0 с целью постепенного чтения сведений профиля пользователя из Azure AD и Microsoft Graph.

Код в этой статье взят из примера приложения Microsoft Teams пример проверки подлинности вкладок [(Node).](https://github.com/OfficeDev/microsoft-teams-sample-complete-node) Она содержит статическую вкладку, которая запрашивает маркер доступа для Microsoft Graph и отображает базовые данные профиля текущего пользователя из Azure AD.

Общие сведения о потоке проверки подлинности для вкладок см. в разделе "Поток проверки [подлинности на вкладке".](~/tabs/how-to/authentication/auth-flow-tab.md)

Поток проверки подлинности на вкладке немного отличается от потока проверки подлинности в ботах.

## <a name="configuring-identity-providers"></a>Настройка поставщиков удостоверений

Подробные [](~/concepts/authentication/configure-identity-provider.md) инструкции по настройке URL-адресов перенаправления вызовов OAuth 2.0 при использовании Azure Active Directory в качестве поставщика удостоверений см. в разделе "Настройка поставщиков удостоверений".

## <a name="initiate-authentication-flow"></a>Инициализация потока проверки подлинности

Поток проверки подлинности должен запускаться действием пользователя. Не следует открывать всплывающее окна проверки подлинности автоматически, так как это, скорее всего, вызовет блокирование всплывающих блоков браузера, а также запутает пользователя.

Добавьте кнопку на страницу конфигурации или содержимого, чтобы пользователь при необходимости в нее влся. Это можно сделать на странице конфигурации [вкладок](~/tabs/how-to/create-tab-pages/configuration-page.md) или на любой [странице содержимого.](~/tabs/how-to/create-tab-pages/content-page.md)

Azure AD, как и большинство поставщиков удостоверений, не позволяет размещать его содержимое в iframe. Это означает, что вам потребуется добавить всплывающее лицо для поставщика удостоверений. В следующем примере эта страница `/tab-auth/simple-start` . Используйте `microsoftTeams.authenticate()` функцию клиентского SDK Microsoft Teams, чтобы запустить эту страницу при нажатии кнопки.

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

* URL-адрес, на который вы передаете, является `microsoftTeams.authentication.authenticate()` первой страницей потока проверки подлинности. В этом примере это `/tab-auth/simple-start` . Это должно соответствовать зарегистрированным на портале регистрации приложений [Azure AD.](https://apps.dev.microsoft.com)

* Поток проверки подлинности должен начинаться на странице, которая в вашем домене. Этот домен также должен быть указан в [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) разделе манифеста. Если этого не сделать, будет выявить пустое всплывающее ок.

* В противном случае возникает проблема с не закрывающееся всплывающее всплывающее `microsoftTeams.authentication.authenticate()` ок.

## <a name="navigate-to-the-authorization-page-from-your-popup-page"></a>Перейдите на страницу авторизации со всплываемой страницы

После отображения всплываемой страницы () будет запускаться `/tab-auth/simple-start` следующий код. Основная цель этой страницы — перенаправить пользователя к поставщику удостоверений. Это перенаправление может быть сделано на стороне сервера с помощью HTTP 302, но в этом случае это делается на стороне клиента с помощью вызова `window.location.assign()` . Это также позволяет получать подсказки, которые можно передать `microsoftTeams.getContext()` в Azure AD.

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

После авторизации пользователь перенаправляется на страницу вызова, указанную для вашего `/tab-auth/simple-end` приложения.

### <a name="notes"></a>Примечания

* Сведения [о контексте пользователя см.](~/tabs/how-to/access-teams-context.md) в справке по построению запросов на проверку подлинности и URL-адресов. Например, можно использовать имя для входа пользователя в качестве значения для входа в Azure AD, что означает, что пользователю может потребоваться `login_hint` ввести меньше. Помните, что не следует использовать этот контекст непосредственно в качестве подтверждения личности, так как злоумышленник может загрузить страницу в вредоносный браузер и предоставить ему любую информацию.
* Хотя контекст вкладки содержит полезные сведения о пользователе, не используйте эти сведения для проверки подлинности пользователя независимо от того, получаете ли вы его в качестве параметров URL-адреса URL-адреса содержимого вкладки или путем вызова функции в клиентском `microsoftTeams.getContext()` SDK Microsoft Teams. Злоумышленник может вызвать URL-адрес содержимого вкладки с собственными параметрами, а веб-страница, под названием Microsoft Teams, загрузит URL-адрес содержимого вкладки в iframe и возвратит свои данные в `getContext()` функцию. Данные, связанные с удостоверениями, следует рассматривать в контексте вкладки просто как подсказки и проверять их перед использованием.
* Этот параметр используется для подтверждения того, что служба, вызываемая URI вызова, `state` является вызываемой службой. Если параметр в обратном вызове не совпадает с параметром, отправленным во время вызова, ответный вызов не проверяется и должен `state` быть завершен.
* Нет необходимости включать домен поставщика удостоверений в список в файле manifest.js`validDomains` приложения.

## <a name="the-callback-page"></a>Страница вызова

В последнем разделе вы вызвали службу авторизации Azure AD и передали сведения о пользователе и приложении, чтобы Azure AD мог представить пользователю собственный монолитный интерфейс авторизации. Ваше приложение не может контролировать, что происходит в этом случае. Он знает только то, что возвращается, когда Azure AD вызывает предоставленную страницу обратного вызова ( `/tab-auth/simple-end` ).

На этой странице необходимо определить успешность или сбой на основе информации, возвращаемой Azure AD и `microsoftTeams.authentication.notifySuccess()` вызовом или `microsoftTeams.authentication.notifyFailure()` . В случае успешного входа у вас будет доступ к ресурсам службы.

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

Этот код разберет пары "ключ-значение", полученные из Azure AD, с `window.location.hash` помощью `getHashParameters()` функции-помощника. Если он находит и значение такое же, как в начале потока проверки подлинности, он возвращает маркер доступа на вкладку путем вызова; в противном случае сообщает об ошибке `access_token` `state` с `notifySuccess()` `notifyFailure()` .

### <a name="notes"></a>Примечания

`NotifyFailure()` имеет следующие предопределяемы причины сбоя:

* `CancelledByUser` пользователь закрыл всплывающее окно перед завершением потока проверки подлинности.
* `FailedToOpenWindow` Не удалось открыть всплывающее окно. При запуске Microsoft Teams в браузере это обычно означает, что окно было заблокировано блокатором всплывающих окон.

В случае успеха вы можете обновить или перезагрузить страницу и отдемонстрировать содержимое, релевантные для пользователя, который в настоящее время имеет проверку подлинности. Если не удается проверить подлинность, отобразить сообщение об ошибке.

Ваше приложение может настроить собственный файл cookie сеанса, чтобы пользователю не нужно было повторно входить при возвращении на вкладку на текущем устройстве.

> [!NOTE]
> Chrome 80, запланированный на выпуск в начале 2020 г., представляет новые значения файлов cookie и по умолчанию налагает политики файлов cookie. Рекомендуется устанавливать предназначенное для файлов cookie использование, а не полагаться на поведение браузера по умолчанию. *См.* [атрибут cookie SameSite (обновление 2020).](../../../resources/samesite-cookie-update.md)

>[!NOTE]
>Чтобы получить правильный маркер для бесплатных и гостевых пользователей Microsoft Teams, важно, чтобы приложения использовали конечную точку https://login.microsoftonline.com/ **{tenantId} для определенного клиента.** Вы можете получить tenantId из сообщения бота или контекста вкладки. Если используются приложения, пользователи получают неправильные маркеры и будут входить в "домашний" клиент, а не в клиент, в который они уже https://login.microsoftonline.com/common вписались.

Дополнительные сведения о едином Sign-On (SSO) см. в статье "Проверка подлинности [без проверки подлинности".](~/tabs/how-to/authentication/auth-silent-AAD.md)

## <a name="samples"></a>Примеры

Пример кода, показывающий процесс проверки подлинности вкладок с помощью Azure AD, см. в:

* [Пример проверки подлинности на вкладке Microsoft Teams (узел)](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)
