---
title: Проверка подлинности для вкладок с помощью Azure Active Directory
description: Описание проверки подлинности в Teams и ее использования на вкладках
keywords: вкладки проверки подлинности Teams AAD
ms.openlocfilehash: 211c08ce1a51a8f0f13e622856a808661dc97b39
ms.sourcegitcommit: fdcd91b270d4c2e98ab2b2c1029c76c49bb807fa
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/13/2020
ms.locfileid: "44801264"
---
# <a name="authenticate-a-user-in-a-microsoft-teams-tab"></a>Проверка подлинности пользователя на вкладке Microsoft Teams

> [!Note]
> Чтобы проверка подлинности работала для вкладки на мобильных клиентах, необходимо убедиться, что используется версия 1.4.1 или более поздняя версия пакета SDK для Teams SDK.

Существует множество служб, которые вы можете использовать в приложении Teams, а большинство этих служб требуют проверки подлинности и авторизации для получения доступа к службе. Службы включают в себя Facebook, Twitter и учебные группы. Сведения о профилях пользователей в Teams хранятся в Azure Active Directory (Azure AD) с помощью Microsoft Graph, и эта статья посвящена проверке подлинности с помощью Azure AD для получения доступа к этой информации.

OAuth 2,0 — это открытый стандарт проверки подлинности, используемый Azure AD, и многие другие поставщики услуг. Общие сведения о OAuth 2,0 является необходимым условием для работы с проверкой подлинности в Teams и Azure AD. В приведенных ниже примерах используется неявный поток предоставления OAuth 2,0 с целью последующего считывания сведений профиля пользователя из Azure AD и Microsoft Graph.

Код, приведенный в этой статье, взят из примера приложения [Microsoft Teams с проверкой подлинности с помощью вкладки Microsoft Teams (узел)](https://github.com/OfficeDev/microsoft-teams-sample-complete-node). Он содержит статическую вкладку, которая запрашивает маркер доступа для Microsoft Graph и показывает сведения о базовом профиле текущего пользователя из Azure AD.

Общий обзор процесса проверки подлинности для вкладок представлен в разделе [последовательность проверки подлинности на вкладках](~/tabs/how-to/authentication/auth-flow-tab.md).

Процесс проверки подлинности на вкладках немного отличается от процесса проверки подлинности в Боты.

## <a name="configuring-identity-providers"></a>Настройка поставщиков удостоверений

В разделе [Настройка поставщиков удостоверений](~/concepts/authentication/configure-identity-provider.md) подробные указания по настройке URL-адресов перенаправления для обратного вызова OAuth 2,0 при использовании Azure Active Directory в качестве поставщика удостоверений.

## <a name="initiate-authentication-flow"></a>Запуск процесса проверки подлинности

Процесс проверки подлинности должен инициироваться действием пользователя. Не следует открывать всплывающую подсказку проверки подлинности автоматически, так как это может вызвать блокирование всплывающих окон в браузере, а также запутать пользователя.

Добавьте кнопку на страницу конфигурации или содержимого, чтобы разрешить пользователю выполнять вход при необходимости. Это можно сделать на странице [Настройка](~/tabs/how-to/create-tab-pages/configuration-page.md) вкладки или на любой странице [содержимого](~/tabs/how-to/create-tab-pages/content-page.md) .

Azure AD, как и большинство поставщиков удостоверений, не допускают помещение его содержимого в IFRAME. Это означает, что вам потребуется добавить всплывающую страницу для размещения поставщика удостоверений. В следующем примере это страница `/tab-auth/simple-start` . Используйте `microsoftTeams.authenticate()` функцию пакета SDK клиента Microsoft Teams, чтобы открыть эту страницу при выборе кнопки.

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

* URL-адрес, на который вы передается, `microsoftTeams.authentication.authenticate()` является начальной страницей процесса проверки подлинности. В этом примере `/tab-auth/simple-start` . Это должно быть согласовано с тем, что вы зарегистрировались на [портале регистрации приложений Azure AD](https://apps.dev.microsoft.com).

* Процесс проверки подлинности должен начинаться на странице, которая находится в вашем домене. Этот домен также должен быть указан в [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) разделе манифеста. В противном случае произойдет пустое всплывающее окно.

* Отработка отказа приведет к проблеме, когда `microsoftTeams.authentication.authenticate()` всплывающее окно не закрывается в конце процесса входа.

## <a name="navigate-to-the-authorization-page-from-your-popup-page"></a>Переход на страницу авторизации из всплывающей страницы

Когда откроется всплывающая страница ( `/tab-auth/simple-start` ), выполняется следующий код. Основной целью этой страницы является перенаправление на поставщика удостоверений, чтобы пользователь мог выполнить вход. Это перенаправление можно выполнить на стороне сервера с помощью HTTP 302, но в этом случае она выполняется на клиентской стороне с помощью вызова `window.location.assign()` . Кроме того, можно `microsoftTeams.getContext()` использовать для получения сведений о подсказках, которые можно передать в Azure AD.

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

После того как пользователь завершит авторизацию, пользователь перенаправляется на страницу обратного вызова, указанную для вашего приложения `/tab-auth/simple-end` .

### <a name="notes"></a>Примечания

* Для создания запросов проверки подлинности и URL-адресов ознакомьтесь со [статьей получение сведений о контексте пользователя](~/tabs/how-to/access-teams-context.md) . Например, вы можете использовать имя пользователя для входа в качестве `login_hint` значения для входа в Azure AD, что означает, что пользователю может потребоваться ввести меньше. Помните, что этот контекст не следует использовать непосредственно в качестве подтверждения личности, так как злоумышленник может загрузить страницу в вредоносном браузере и предоставить ей любую нужную информацию.
* Несмотря на то, что контекст вкладки предоставляет полезную информацию для пользователя, не используйте эти сведения для проверки подлинности пользователя о том, является ли он параметрами URL-адреса для контента вкладки, или вызывая `microsoftTeams.getContext()` функцию в клиенте SDK Microsoft Teams. Вредоносный субъект может вызывать URL-адрес содержимого вкладки с собственными параметрами, а веб-страница, олицетворяющая Microsoft Teams, может загрузить URL-адрес содержимого вкладки в IFRAME и вернуть собственные данные в `getContext()` функцию. Информация, связанная с удостоверением, должна рассматриваться в контексте вкладки просто как подсказки и проверять их перед использованием.
* `state`Параметр используется для подтверждения того, что служба, вызывающая URI обратного вызова, является вызываемой службой. Если `state` параметр в обратном вызове не соответствует параметру, отправленному во время вызова, возвращенный вызов не проверяется и должен быть завершен.
* Нет необходимости включать домен поставщика удостоверений в `validDomains` список в manifest.jsприложения в файле.

## <a name="the-callback-page"></a>Страница обратного вызова

В последнем разделе, на котором вы позвонили в службу авторизации Azure AD и переданы сведения о пользователях и приложениях, чтобы Azure AD мог представить пользователю собственную систему авторизации. Ваше приложение не контролирует то, что происходит в этом интерфейсе. Все знают, что возвращается, когда Azure AD вызывает указанную страницу обратного вызова ( `/tab-auth/simple-end` ).

На этой странице необходимо определить успешность или сбой на основе сведений, возвращенных службой Azure AD, а `microsoftTeams.authentication.notifySuccess()` также вызвать или `microsoftTeams.authentication.notifyFailure()` . Если вход выполнен успешно, вы получите доступ к ресурсам службы.

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

Этот код анализирует пары "ключ — значение", полученные из Azure AD `window.location.hash` , с помощью `getHashParameters()` вспомогательной функции. Если обнаруживается `access_token` , и значение совпадает с параметром, `state` предоставленным в начале процесса проверки подлинности, он возвращает маркер доступа на вкладку с помощью вызова `notifySuccess()` ; в противном случае сообщает об ошибке `notifyFailure()` .

### <a name="notes"></a>Примечания

`NotifyFailure()`имеет следующие предопределенные причины ошибки:

* `CancelledByUser`пользователь закрыл всплывающее окно перед завершением процесса проверки подлинности.
* `FailedToOpenWindow`не удается открыть всплывающее окно. При работе с Microsoft Teams в браузере обычно это означает, что окно заблокировано с помощью средства блокирования всплывающих окон.

В случае успешного выполнения можно обновить или перезагрузить страницу, а также Показать контент, относящийся к пользователю, прошедшему проверку подлинности. Если не удается выполнить проверку подлинности, отобразится сообщение об ошибке.

Ваше приложение может задать свой файл cookie для сеанса, чтобы пользователь не мог войти в систему при возврате на вкладку на текущем устройстве.

> [!NOTE]
> Хром 80, запланированный на выпуск ранних 2020, содержит новые значения файлов cookie и по умолчанию накладывает политики файлов cookie. Рекомендуется задавать предполагаемый способ использования файлов cookie, а не полагаться на поведение браузера по умолчанию. *Просмотрите* [атрибут самесите cookie (обновление 2020)](../../../resources/samesite-cookie-update.md).

Дополнительные сведения о службе единого входа (SSO) можно найти в статье [Автоматическая проверка подлинности](~/tabs/how-to/authentication/auth-silent-AAD.md).

## <a name="samples"></a>Примеры

Пример кода, иллюстрирующий процесс проверки подлинности с помощью вкладок с помощью Azure AD, приведен ниже.

* [Пример проверки подлинности с помощью вкладки Microsoft Teams (узел)](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)
