---
title: Конфигурация кода для включения единого входа для вкладок
description: Обновите код в приложении вкладки для запроса и получения маркера доступа с помощью удостоверения Teams пользователя приложения для включения единого входа.
ms.topic: how-to
ms.localizationpriority: high
keywords: вкладки проверки подлинности команд Microsoft Azure Active Directory (Azure AD) API Graph
ms.openlocfilehash: 20b11032227a08d057a6cdae8e46154004bfdb02
ms.sourcegitcommit: bb15ce26cd65bec90991b703069424ab4b4e1a61
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/28/2022
ms.locfileid: "68772267"
---
# <a name="add-code-to-enable-sso"></a>Добавление кода для включения единого входа

Прежде чем добавлять код для включения единого входа, зарегистрируйте свое приложение в Azure AD.

> [!div class="nextstepaction"]
> [Регистрация в Azure AD](tab-sso-register-aad.md)

Чтобы получить маркер доступа из Azure AD, необходимо настроить клиентский код приложения вкладки. Маркер доступа выдается от имени приложения вкладки. Если для вашего приложения вкладки требуются дополнительные разрешения Microsoft Graph, вам будет нужно передать маркер доступа на сервер и обменять его на маркер Microsoft Graph.

:::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/sso-config-code.png" alt-text="настройка кода для обработки маркера доступа":::

Содержание раздела:

- [Добавьте код для клиента](#add-client-side-code)
- [Передача маркера доступа серверному коду](#pass-the-access-token-to-server-side-code)
- [Проверка маркера доступа](#validate-the-access-token)

## <a name="add-client-side-code"></a>Добавьте код для клиента

Чтобы получить доступ к приложению для текущего пользователя приложения, код на стороне клиента должен выполнить вызов Teams для получения маркера доступа. Чтобы инициировать процесс проверки, вам необходимо обновить клиентский код для использования `getAuthToken()`.

<br>
<details>
<summary>Подробнее о getAuthToken()</summary>
<br>
`getAuthToken()` — это метод в Microsoft Teams JavaScript SDK. Он запрашивает маркер доступа Azure AD, который будет выдан от имени приложения. Маркер получается из кэша, если срок его действия истек. Если срок его действия истек, в Azure AD отправляется запрос на получение нового маркера доступа.

 Дополнительные сведения см. в разделе [getAuthToken](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-authentication-getauthtoken&preserve-view=true).
</details>

### <a name="when-to-call-getauthtoken"></a>Когда вызывать getAuthToken

Используйте `getAuthToken()`, если вам нужен маркер доступа для текущего пользователя приложения:

| Если требуется маркер доступа... | Вызовите getAuthToken()... |
| --- | --- |
| Когда пользователь приложения получает доступ к приложению | После `microsoftTeams.initialize()`. |
| Чтобы использовать определенные функции приложения | Когда пользователь приложения выполняет действие, требующее входа в систему. |

### <a name="add-code-for-getauthtoken"></a>Добавьте код для getAuthToken

Добавьте фрагмент кода JavaScript во вкладку приложения, чтобы:

- вызова метода `getAuthToken()`;
- Проанализируйте маркер доступа или передайте его коду на стороне сервера.

В следующем фрагменте кода показан пример вызова `getAuthToken()`.

```javascript
microsoftTeams.initialize();
var authTokenRequest = {
  successCallback: function(result) { console.log("Success: " + result); },
  failureCallback: function(error) { console.log("Error getting token: " + error); }
};
microsoftTeams.authentication.getAuthToken(authTokenRequest);
```

Вы можете добавить вызовы `getAuthToken()` ко всем функциям и обработчикам, инициирующим действие, где необходим маркер

<br>
<details>
<summary>Вот пример клиентского кода:</summary>

:::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/config-client-code.png" alt-text="Настройка клиентского кода" lightbox="../../../assets/images/authentication/teams-sso-tabs/config-client-code.png":::

</details>

Когда Teams получает маркер доступа, он кэшируется и повторно используется по мере необходимости. Этот маркер можно использовать при каждом вызове `getAuthToken()` до истечения срока его действия без повторного вызова Azure AD.

> [!IMPORTANT]
> В качестве наилучшей методики обеспечения безопасности маркера доступа:
>
> - Вызывайте `getAuthToken()` только тогда, когда вам нужен маркер доступа.
> - Teams кэшируют маркер доступа для вас. Не кэшируйте и не храните его в коде своего приложения.

### <a name="consent-dialog-for-getting-access-token"></a>Диалоговое окно согласия на получение маркера доступа

Когда вы вызываете `getAuthToken()` и для разрешений на уровне пользователя требуется согласие пользователя приложения, вошедшему пользователю приложения, отображается диалоговое окно Azure AD.

:::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/tabs-sso-prompt.png" alt-text="Диалоговое окно единого входа с вкладкой":::

Появится диалоговое окно согласия для областей с открытым идентификатором, определенных в Azure AD. Пользователь приложения должен дать согласие только один раз. После согласия пользователь приложения может получить доступ и использовать ваше приложение вкладки для предоставленных разрешений и областей.

> [!IMPORTANT]
> Сценарии, в которых диалоги согласия не нужны:
>
> - Если администратор клиента предоставил согласие от имени клиента, пользователям приложений вообще не нужно запрашивать согласие. Это означает, что пользователи приложения не видят диалоговые окна согласия и могут беспрепятственно получать доступ к приложению.
> - Если ваше приложение Azure AD зарегистрировано в том же клиенте, у которого вы запрашиваете проверку подлинности в Teams, пользователю приложения нельзя будет предложить согласие, и ему сразу же будет предоставлен маркер доступа. Пользователи приложения предоставляют согласие на эти разрешения, только если приложение Azure AD зарегистрировано в другом клиенте.

Если вы столкнулись с какими-либо ошибками, см. раздел [Устранение неполадок с проверкой подлинности единого входа в Teams](tab-sso-troubleshooting.md).

### <a name="use-the-access-token-as-an-identity-token"></a>Использование маркера доступа в качестве маркера удостоверений

Маркер, возвращенный в приложение вкладки, является одновременно маркером доступа и маркером идентификатора. Приложение вкладки может использовать маркер в качестве маркера доступа для выполнения HTTPS-запросов, прошедших проверку подлинности, к API на стороне сервера.

Токен доступа, возвращенный из `getAuthToken()`, можно использовать для установления личности пользователя приложения с помощью следующих утверждений в маркере:

- `name`: отображаемое имя пользователя приложения.
- `preferred_username`: адрес электронной почты пользователя приложения.
- `oid`: GUID, представляющий идентификатор пользователя приложения.
- `tid`: идентификатор GUID, представляющий клиент, в который входит пользователь приложения.

Teams могут кэшировать эти сведения, связанные с удостоверением пользователя приложения, например предпочтениями пользователя.

> [!NOTE]
> Если вам нужно создать уникальный идентификатор для представления пользователя приложения в вашей системе, см. раздел [Использование утверждений для надежной идентификации пользователя](/azure/active-directory/develop/id-tokens#using-claims-to-reliably-identify-a-user-subject-and-object-id).

## <a name="pass-the-access-token-to-server-side-code"></a>Передача маркера доступа серверному коду

Если вам нужен доступ к веб-API на вашем сервере, вам нужно будет передать маркер доступа в код на стороне сервера. Веб-API должны декодировать маркер доступа для просмотра утверждений для этого маркера.

> [!NOTE]
> Если вы не получили имя участника-пользователя (UPN) в возвращенном маркере доступа, добавьте его в качестве [необязательного утверждения](/azure/active-directory/develop/active-directory-optional-claims) в Azure AD.
> Дополнительные сведения см. в разделе [Маркеры доступа](/azure/active-directory/develop/access-tokens).

Маркер доступа, полученный при успешном обратном вызове `getAuthToken()`, предоставляет доступ (для пользователя приложения, прошедшего проверку подлинности) к вашим веб-API. Код на стороне сервера также может анализировать маркер на предмет [сведений об удостоверении](#use-the-access-token-as-an-identity-token), если это необходимо.

Если вам нужно передать маркер доступа для получения данных Microsoft Graph, см. [Расширение приложения вкладки с разрешениями Microsoft Graph](tab-sso-graph-api.md).

### <a name="code-for-passing-access-token-to-server-side"></a>Код для передачи маркера доступа на сервер

В следующем коде показан пример передачи маркера доступа на сервер. Маркер передается в `Authorization`заголовке при отправке запроса в серверный веб-API. В этом примере отправляются данные JSON, поэтому используется метод `POST`. `GET` достаточно для отправки маркера доступа, когда вы не пишете на сервер.

```javascript
$.ajax({
    type: "POST",
    url: "/api/DoSomething",
    headers: {
        "Authorization": "Bearer " + accessToken
    },
    data: { /* some JSON payload */ },
    contentType: "application/json; charset=utf-8"
}).done(function (data) {
    // Handle success
}).fail(function (error) {
    // Handle error
}).always(function () {
    // Cleanup
});
```

### <a name="validate-the-access-token"></a>Проверка маркера доступа

Веб-API на вашем сервере должны декодировать маркер доступа и проверять, отправлен ли он клиентом. Это маркер JSON Web Token (JWT), то есть его проверка выполняется так же, как и в большинстве стандартных потоков OAuth. Веб-API должны декодировать маркер доступа. При желании вы можете вручную скопировать и вставить маркер доступа в инструмент, например jwt.ms.

Доступно множество библиотек, которые могут выполнять проверку JWT. Базовая проверка включает в себя:

- проверяют правильность формата маркера;
- проверяют, выдан ли маркер нужным центром сертификации;
- Проверка того, предназначен ли маркер для веб-API.

При проверке маркера учитывайте приведенные ниже рекомендации.

- Допустимые маркеры единого входа выдаются Azure AD. Утверждение `iss` в маркере должно начинаться с этого значения.
- Параметр `aud1` маркера будет установлен на идентификатор приложения, созданный во время регистрации приложения Azure AD.
- Для параметра `scp` маркера будет задано значение `access_as_user`.

#### <a name="example-access-token"></a>Пример маркера доступа

Ниже приведен типичная раскодированная нагрузка маркера доступа.

```javascript
{
    aud: "2c3caa80-93f9-425e-8b85-0745f50c0d24",
    iss: "https://login.microsoftonline.com/fec4f964-8bc9-4fac-b972-1c1da35adbcd/v2.0",
    iat: 1521143967,
    nbf: 1521143967,
    exp: 1521147867,
    aio: "ATQAy/8GAAAA0agfnU4DTJUlEqGLisMtBk5q6z+6DB+sgiRjB/Ni73q83y0B86yBHU/WFJnlMQJ8",
    azp: "e4590ed6-62b3-5102-beff-bad2292ab01c",
    azpacr: "0",
    e_exp: 262800,
    name: "Mila Nikolova",
    oid: "6467882c-fdfd-4354-a1ed-4e13f064be25",
    preferred_username: "milan@contoso.com",
    scp: "access_as_user",
    sub: "XkjgWjdmaZ-_xDmhgN1BMP2vL2YOfeVxfPT_o8GRWaw",
    tid: "fec4f964-8bc9-4fac-b972-1c1da35adbcd",
    uti: "MICAQyhrH02ov54bCtIDAA",
    ver: "2.0"
}
```

## <a name="code-samples"></a>Примеры кода

| Название примера | Описание | C#/.NET| Node.js |
|---------------|---------------|------|--------------|
| Единый вход на вкладке |Пример приложения Microsoft Teams для единого входа на вкладках Azure AD| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-sso/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/tab-sso/nodejs), </br>[Набор средств Teams](../../../toolkit/visual-studio-code-tab-sso.md)|
| Вкладка, бот и расширение сообщений (ME) SSO | В этом примере показана система единого входа для Tab, Bot и ME — поиск, действие, linkunfurl. |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/csharp) | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/nodejs) |

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Обновление манифеста приложения Teams и предварительный просмотр приложения](tab-sso-manifest.md)

## <a name="see-also"></a>См. также

- [jwt.ms](https://jwt.ms/)
- [Необязательное утверждение Active Directory](/azure/active-directory/develop/active-directory-optional-claims)
- [Маркеры доступа](/azure/active-directory/develop/access-tokens)
- [Обзор библиотеки проверки подлинности Microsoft (MSAL)](/azure/active-directory/develop/msal-overview)
- [Маркеры идентификатора платформы Microsoft Identity](/azure/active-directory/develop/id-tokens)
- [Маркеры доступа платформы удостоверений Майкрософт](/azure/active-directory/develop/access-tokens#validating-tokens)
