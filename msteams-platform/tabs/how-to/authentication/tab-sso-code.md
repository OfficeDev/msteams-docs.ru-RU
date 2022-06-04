---
title: Настройка кода для включения единого входа для вкладок
description: Описание конфигурации кода для включения единого входа для вкладок
ms.topic: how-to
ms.localizationpriority: medium
keywords: Вкладки проверки подлинности teams API Graph Microsoft Azure Active Directory (Azure AD)
ms.openlocfilehash: 3f095f3e2b0737b7afcdfe3bdcc96bd36d2f3847
ms.sourcegitcommit: e16b51a49756e0fe4eaf239898e28d3021f552da
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/04/2022
ms.locfileid: "65888131"
---
# <a name="add-code-to-enable-sso"></a>Добавление кода для включения единого входа

Перед добавлением кода для включения единого входа убедитесь, что вы зарегистрировали приложение в Azure AD.

> [!div class="nextstepaction"]
> [Регистрация в Azure AD](tab-sso-register-aad.md)

Чтобы получить маркер доступа из Azure AD, необходимо настроить клиентский код приложения табуляции. Маркер доступа выдан от имени приложения вкладки. Если приложению вкладки требуются дополнительные разрешения Microsoft Graph, необходимо передать маркер доступа на стороне сервера и обменять его на маркер Microsoft Graph.

:::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/sso-config-code.png" alt-text="настройка кода для обработки маркера доступа" border="false":::

Содержание раздела:

- [Добавьте код для клиента](#add-client-side-code)
- [Передача маркера доступа серверному коду](#pass-the-access-token-to-server-side-code)
- [Проверка маркера доступа](#validate-the-access-token)

## <a name="add-client-side-code"></a>Добавьте код для клиента

Чтобы получить доступ к приложению для текущего пользователя приложения, клиентский код должен вызвать Teams для получения маркера доступа. Для запуска процесса `getAuthToken()` проверки необходимо обновить код на стороне клиента.

<br>
<details>
<summary>Дополнительные сведения о getAuthToken()</summary>
<br>
`getAuthToken()` — это метод в пакете SDK JavaScript для Microsoft Teams. Он запрашивает выдачу маркера доступа Azure AD от имени приложения. Маркер будет получен из кэша, если срок его действия не истек. Если срок действия истек, в Azure AD отправляется запрос на получение нового маркера доступа.

 Дополнительные сведения см. в [разделе getAuthToken](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-authentication-getauthtoken&preserve-view=true).
</details>

### <a name="when-to-call-getauthtoken"></a>Когда следует вызывать getAuthToken

Используйте `getAuthToken()` в момент, когда требуется маркер доступа для текущего пользователя приложения:

| Если требуется маркер доступа... | Вызовите метод getAuthToken()... |
| --- | --- |
| Когда пользователь приложения имеет доступ к приложению | Изнутри `microsoftTeams.initialize()`. |
| Использование определенной функциональности приложения | Когда пользователь приложения выполняет действие, требующее входа. |

### <a name="add-code-for-getauthtoken"></a>Добавление кода для getAuthToken

Добавьте фрагмент кода JavaScript в приложение вкладки, чтобы:

- вызова метода `getAuthToken()`;
- Проанализировать маркер доступа или передать его в код на стороне сервера.

В следующем фрагменте кода показан пример вызова `getAuthToken()`.

```javascript
microsoftTeams.initialize();
var authTokenRequest = {
  successCallback: function(result) { console.log("Success: " + result); },
  failureCallback: function(error) { console.log("Error getting token: " + error); }
};
microsoftTeams.authentication.getAuthToken(authTokenRequest);
```

Можно добавить вызовы ко `getAuthToken()` всем функциям и обработчикам, которые инициируют действие, в котором требуется маркер.

<br>
<details>
<summary>Ниже приведен пример кода на стороне клиента.</summary>

:::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/config-client-code.png" alt-text="Настройка клиентского кода" lightbox="../../../assets/images/authentication/teams-sso-tabs/config-client-code.png":::

</details>

Когда Teams получает маркер доступа, он кэшируется и используется повторно по мере необходимости. Этот токен можно использовать при каждом `getAuthToken()` вызове, пока не истечет срок его действия, без выполнения другого вызова Azure AD.

> [!IMPORTANT]
> Для обеспечения безопасности маркера доступа рекомендуется:
>
> - Всегда вызывайте `getAuthToken()` только в том случае, если вам нужен маркер доступа.
> - Teams будет кэшировать маркер доступа. Не кэшировать и не сохранять его в коде приложения.

### <a name="consent-dialog-for-getting-access-token"></a>Диалоговое окно согласия для получения маркера доступа

Когда вы вызываете `getAuthToken()` и требуется согласие пользователя приложения для разрешений на уровне пользователя, пользователю приложения, который в настоящее время выполнил вход, отображается диалоговое окно Azure AD.

:::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/tabs-sso-prompt.png" alt-text="Диалоговое окно &quot;Вкладка единого входа&quot;":::

Откроется диалоговое окно согласия для областей с открытым идентификатором, определенных в Azure AD. Пользователь приложения должен дать согласие только один раз. После предоставления согласия пользователь приложения может получить доступ к приложению табуляции и использовать его для предоставленных разрешений и областей.

> [!IMPORTANT]
> Сценарии, в которых диалоги согласия не требуются:
>
> - Если администратор клиента предоставил согласие от имени клиента, пользователям приложения не нужно запрашивать согласие. Это означает, что пользователи приложения не видят диалоги согласия и могут легко получить доступ к приложению.
> - Если приложение Azure AD зарегистрировано в том же клиенте, из которого вы запрашиваете проверку подлинности в Teams, пользователю приложения не может быть предложено дать согласие, и ему сразу же предоставляется маркер доступа. Пользователи приложения соглашаются на эти разрешения только в том случае, если приложение Azure AD зарегистрировано в другом клиенте.

Если у вас возникли ошибки, см. раздел "Устранение неполадок проверки [подлинности единого входа" в Teams](tab-sso-troubleshooting.md).

### <a name="use-the-access-token-as-an-identity-token"></a>Использование маркера доступа в качестве маркера удостоверений

Маркер, возвращаемый приложению табуляции, является маркером доступа и маркером идентификатора. Приложение вкладки может использовать маркер в качестве маркера доступа для выполнения HTTPS-запросов, прошедших проверку подлинности, к API на стороне сервера.

Возвращаемый маркер доступа `getAuthToken()` можно использовать для установления удостоверения пользователя приложения с помощью следующих утверждений в маркере:

- `name`: отображаемое имя пользователя приложения.
- `preferred_username`: адрес электронной почты пользователя приложения.
- `oid`: GUID, представляющий идентификатор пользователя приложения.
- `tid`: GUID, представляющий клиент, в который выполняет вход пользователь приложения.

Teams может кэшировать эти сведения, связанные с удостоверением пользователя приложения, например настройки пользователя.

> [!NOTE]
> Если необходимо создать уникальный идентификатор для представления пользователя приложения в системе, см. раздел "Использование утверждений для надежной [идентификации пользователя"](/azure/active-directory/develop/id-tokens#using-claims-to-reliably-identify-a-user-subject-and-object-id).

## <a name="pass-the-access-token-to-server-side-code"></a>Передача маркера доступа серверному коду

Если вам нужен доступ к веб-API на сервере, необходимо передать маркер доступа в код на стороне сервера. Веб-API должны декодировать маркер доступа для просмотра утверждений для этого маркера.

> [!NOTE]
> Если вы не получили имя участника-пользователя (UPN) в возвращенном маркере доступа, добавьте его в качестве необязательного [утверждения в Azure](/azure/active-directory/develop/active-directory-optional-claims) AD.
> Дополнительные сведения см. в разделе [маркеров доступа](/azure/active-directory/develop/access-tokens).

Маркер доступа, полученный при успешном `getAuthToken()` обратном вызове, предоставляет доступ (для пользователя приложения, прошедшего проверку подлинности) к веб-API. При необходимости серверный код также может анализировать [маркер для](#use-the-access-token-as-an-identity-token) сведений об удостоверении.

Если вам нужно передать маркер доступа для получения данных Microsoft Graph, см. раздел "Расширение приложения [вкладки с помощью разрешений Microsoft Graph"](tab-sso-graph-api.md).

### <a name="code-for-passing-access-token-to-server-side"></a>Код для передачи маркера доступа на стороне сервера

В следующем коде показан пример передачи маркера доступа на сервер. Маркер передается в `Authorization`заголовке при отправке запроса в серверный веб-API. В этом примере отправляются данные JSON, поэтому используется `POST` метод. Этого `GET` достаточно для отправки маркера доступа, если вы не выполняете запись на сервер.

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

Веб-API на сервере должны декодировать маркер доступа и проверять, отправлен ли он от клиента. Это маркер JSON Web Token (JWT), то есть его проверка выполняется так же, как и в большинстве стандартных потоков OAuth. Веб-API должны декодировать маркер доступа. При необходимости можно вручную скопировать и вставить маркер доступа в средство, например jwt.ms.

Существует ряд библиотек, которые могут обрабатывать проверку JWT. Базовая проверка включает в себя:

- проверяют правильность формата маркера;
- проверяют, выдан ли маркер нужным центром сертификации;
- Проверка того, что маркер предназначен для веб-API

При проверке маркера учитывайте приведенные ниже рекомендации.

- Допустимые маркеры единого входа выданы Azure AD. Утверждение `iss` в маркере должно начинаться с этого значения.
- Для параметра токена `aud1` будет задано значение идентификатора приложения, созданного во время регистрации приложения Azure AD.
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
- [Общие сведения о библиотеке проверки подлинности Майкрософт (MSAL)](/azure/active-directory/develop/msal-overview)
- [Маркеры идентификаторов платформы удостоверений Майкрософт](/azure/active-directory/develop/id-tokens)
- [Маркеры доступа платформы удостоверений Майкрософт](/azure/active-directory/develop/access-tokens#validating-tokens)
