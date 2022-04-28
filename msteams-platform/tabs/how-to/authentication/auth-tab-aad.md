---
title: Проверка подлинности для вкладок с помощью Azure Active Directory
description: Описывает проверку подлинности в Teams и способы ее использования на вкладке
ms.topic: how-to
ms.localizationpriority: medium
keywords: вкладки проверки подлинности teams Microsoft Azure Active Directory (Azure AD)
ms.openlocfilehash: 41d2a3f0cb9d05acfe879654c255e1d012c1f874
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104058"
---
# <a name="authenticate-a-user-in-a-microsoft-teams-tab"></a>Проверка подлинности пользователя на вкладке Microsoft Teams

> [!Note]
> Для работы проверки подлинности на вкладке на мобильных клиентах необходимо убедиться, что вы используете версию 1.4.1 или более позднюю версию пакета SDK Teams JavaScript.

Существует множество служб, которые можно использовать в приложении Teams, и большинство из них требуют проверки подлинности и авторизации для получения доступа к службе. К службам относятся Facebook, Twitter и Teams. Teams сведения о профиле пользователя хранятся в Azure AD с помощью Microsoft Graph и в этой статье основное внимание уделяется проверке подлинности с помощью Azure AD для получения доступа к этой информации.

OAuth 2.0 — это открытый стандарт для проверки подлинности, используемый Azure AD и многими другими поставщиками услуг. Понимание OAuth 2.0 является необходимым условием для работы с проверкой подлинности в Teams и Azure AD. В приведенных ниже примерах используется поток неявного предоставления OAuth 2.0 с целью в конечном итоге считывания сведений о профиле пользователя из Azure AD и Microsoft Graph.

Код, приведенный в этой статье, Teams примере приложения Microsoft Teams проверки подлинности на вкладке [(Node).](https://github.com/OfficeDev/microsoft-teams-sample-complete-node) Она содержит статическую вкладку, которая запрашивает маркер доступа для Microsoft Graph и отображает основные сведения о профиле текущего пользователя из Azure AD.

Общие сведения о потоке проверки подлинности для вкладок см. на вкладке "Поток [проверки подлинности"](~/tabs/how-to/authentication/auth-flow-tab.md).

Поток проверки подлинности на вкладке немного отличается от потока проверки подлинности в ботах.

## <a name="configuring-identity-providers"></a>Настройка поставщиков удостоверений

Подробные инструкции по настройке URL-адресов перенаправления обратного вызова OAuth 2.0 при использовании Azure AD в качестве поставщика удостоверений см. в разделе "Настройка поставщиков удостоверений".[](~/concepts/authentication/configure-identity-provider.md)

## <a name="initiate-authentication-flow"></a>Запуск потока проверки подлинности

Поток проверки подлинности должен активироваться действием пользователя. Не следует открывать всплывающее окно проверки подлинности автоматически, так как это, скорее всего, активирует блокировку всплывающих элементов браузера, а также путает пользователя.

Добавьте кнопку на страницу конфигурации или содержимого, чтобы пользователь при необходимости входить в систему. Это можно сделать на странице конфигурации [вкладки](~/tabs/how-to/create-tab-pages/configuration-page.md) или на любой [странице](~/tabs/how-to/create-tab-pages/content-page.md) содержимого.

Azure AD, как и большинство поставщиков удостоверений, не разрешает помещать его содержимое в iframe. Это означает, что для размещения поставщика удостоверений потребуется добавить всплывающее окно. В следующем примере эта страница имеет значение `/tab-auth/simple-start`. Используйте функцию `microsoftTeams.authenticate()` пакета SDK Microsoft Teams клиента, чтобы запустить эту страницу при нажатии кнопки.

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

* ПЕРЕДАВАЕМЫЙ URL-адрес `microsoftTeams.authentication.authenticate()` является начальной страницей потока проверки подлинности. В этом примере это `/tab-auth/simple-start`. Это должно совпадать с тем, что вы зарегистрировали на портале регистрации [приложений Azure AD](https://apps.dev.microsoft.com).

* Поток проверки подлинности должен начинаться на странице, которая в вашем домене. Этот домен также должен быть указан в [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) разделе манифеста. Если этого не сделать, вы увидите пустое всплывающее окно.

* В противном случае `microsoftTeams.authentication.authenticate()` возникает проблема с закрытием всплывающего окна в конце процесса входа.

## <a name="navigate-to-the-authorization-page-from-your-pop-up-page"></a>Перейдите на страницу авторизации со всплывающей страницы

При отображении всплывающей страницы (`/tab-auth/simple-start`) выполняется следующий код. Основная цель этой страницы — перенаправление к поставщику удостоверений, чтобы пользователь может войти в систему. Это перенаправление может быть выполнено на стороне сервера с помощью HTTP 302, но в этом случае это делается на стороне клиента с помощью вызова .`window.location.assign()` Это также позволяет получать `microsoftTeams.getContext()` подсказки, которые можно передать в Azure AD.

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

После завершения авторизации пользователь перенаправляется на страницу обратного вызова, указанную для вашего приложения `/tab-auth/simple-end`.

### <a name="notes"></a>Примечания

* [Дополнительные сведения о создании](~/tabs/how-to/access-teams-context.md) запросов на проверку подлинности и URL-адресов см. в статье "Получение сведений о контексте пользователя". Например, можно `login_hint` использовать имя входа пользователя в качестве значения для входа в Azure AD, что означает, что пользователю может потребоваться ввести меньше. Помните, что этот контекст не следует использовать непосредственно в качестве подтверждения личности, так как злоумышленник может загрузить вашу страницу в вредоносный браузер и предоставить ему любую информацию, которую он хочет.
* Хотя контекст вкладки предоставляет полезные сведения о пользователе, не используйте эти сведения для проверки подлинности пользователя независимо от того, получаете ли вы его в качестве параметров URL-адреса для URL-адреса `microsoftTeams.getContext()` содержимого вкладки или путем вызова функции в клиентском пакете SDK Microsoft Teams. Злоумышленник может вызвать URL-адрес содержимого вкладки с собственными параметрами, а веб-страница, олицетворяемая Microsoft Teams может загрузить URL-адрес содержимого вкладки в iframe `getContext()` и вернуть функции собственные данные. Сведения, связанные с удостоверениями, следует рассматривать в контексте вкладки просто как подсказки и проверять их перед использованием.
* Этот `state` параметр используется для подтверждения того, что служба, вызываемая URI обратного вызова, является вызываемой службой. Если параметр `state` в обратном вызове не совпадает с параметром, отправленным во время вызова, обратный вызов не проверяется и должен быть завершен.
* Нет необходимости включать домен поставщика удостоверений `validDomains` в список в файле manifest.json приложения.

## <a name="the-callback-page"></a>Страница обратного вызова

В последнем разделе вы вызвали службу авторизации Azure AD и передали сведения о пользователе и приложении, чтобы Azure AD мог предоставлять пользователю собственный монолитный интерфейс авторизации. Ваше приложение не контролирует, что происходит в этом интерфейсе. Все, что известно, — это то, что возвращается, когда Azure AD вызывает предоставленную вами страницу обратного вызова (`/tab-auth/simple-end`).

На этой странице необходимо определить успешность или сбой на основе сведений, возвращаемых Azure AD и звонка или `microsoftTeams.authentication.notifySuccess()` `microsoftTeams.authentication.notifyFailure()`. Если вход выполнен успешно, у вас будет доступ к ресурсам службы.

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

Этот код анализирует пары "ключ-значение", полученные из Azure AD, `window.location.hash` с помощью вспомогательной `getHashParameters()` функции. `access_token``state` Если он находит и значение совпадает со значением, указанным в начале потока проверки подлинности, `notifySuccess()`он возвращает маркер доступа на вкладку путем вызова; `notifyFailure()`в противном случае он сообщает об ошибке с .

### <a name="notes"></a>Примечания

`NotifyFailure()` имеет следующие предопределенные причины сбоя:

* `CancelledByUser` пользователь закрыл всплывающее окно перед завершением потока проверки подлинности.
* `FailedToOpenWindow` Не удалось открыть всплывающее окно. При запуске Microsoft Teams в браузере это обычно означает, что окно было заблокировано блокированием всплывающих окон.

В случае успешного выполнения можно обновить или перезагрузить страницу и отобразить содержимое, относятивное к пользователю, прошедшему проверку подлинности. В случае сбоя проверки подлинности отображается сообщение об ошибке.

Приложение может задать собственный файл cookie сеанса, чтобы пользователю больше не нужно входить в систему при возврате на вкладку на текущем устройстве.

> [!NOTE]
>
> * Chrome 80, запланированный на выпуск в начале 2020 г., вводит новые значения файлов cookie и по умолчанию налагает политики файлов cookie. Рекомендуется задать предполагаемое использование файлов cookie, а не полагаться на поведение браузера по умолчанию. *См*[. атрибут cookie SameSite (обновление до 2020 г.).](../../../resources/samesite-cookie-update.md)
> * Чтобы получить правильный токен для Microsoft Teams и гостевых пользователей, приложения должны использовать конечную точку конкретного клиента`https://login.microsoftonline.com/**{tenantId}**`. Идентификатор клиента можно получить из сообщения бота или контекста вкладки. Если используются приложения `https://login.microsoftonline.com/common`, пользователи получают неправильные маркеры и будут выполнять вход в "домашний" клиент, а не в клиент, в который они вошли в данный момент.

Дополнительные сведения о едином Sign-On (SSO) см. в статье "Автоматическая [проверка подлинности"](~/tabs/how-to/authentication/auth-silent-AAD.md).

## <a name="code-sample"></a>Пример кода

Пример кода, показывающий процесс проверки подлинности вкладок с помощью Azure AD:

| **Название примера** | **description** | **.NET** | **Node.js** |
|-----------------|-----------------|-------------|
| Microsoft Teams проверки подлинности на вкладке | Процесс проверки подлинности на вкладке с помощью Azure AD. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group-config-page-auth/csharp) | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-auth/nodejs) |

## <a name="see-also"></a>Дополнительные ресурсы

* [Планирование проверки подлинности пользователей](../../../concepts/design/understand-use-cases.md)
* [Разработка вкладки для Microsoft Teams](~/tabs/design/tabs.md)
* [Автоматическая проверка подлинности](~/tabs/how-to/authentication/auth-silent-aad.md)
* [Добавление проверки подлинности в расширение сообщения](~/messaging-extensions/how-to/add-authentication.md)
* [Поддержка единого входа для ботов](~/bots/how-to/authentication/auth-aad-sso-bots.md)
