---
title: Поддержка единого входа для ботов
description: Описание единого входа (SSO)
ms.topic: how-to
ms.localizationpriority: high
keywords: группы проверки подлинности SSO Microsoft Azure Active Directory (Azure AD) единого api для входов
ms.openlocfilehash: 24b9465e8400660fb0f271d20e3922679c43663e
ms.sourcegitcommit: 90587b1ec04bf20d716ed6feb8ccca4313e87f8c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/10/2022
ms.locfileid: "62518102"
---
# <a name="single-sign-on-sso-support-for-tabs"></a>Поддержка единого входа (SSO) для вкладок

Пользователи, которые входят в Microsoft Teams с помощью учетной записи Office 365, Outlook или учебной учетной записи Майкрософт, могут воспользоваться преимуществами, разрешив единый вход для авторизации вкладок Teams или модуля задачи в настольных или мобильных клиентах. Если пользователь входит один раз, уже не нужно повторно входить на другом устройстве, так как вход осуществляется автоматически. Кроме того, маркер доступа предварительно загружается для повышения производительности и времени загрузки.

> [!NOTE]
> **Версии мобильных клиентов Teams, поддерживающие SSO**  
>
> ✔Teams для Android (1416/1.0.0.2020073101 и более поздние версии)
>
> ✔Teams для iOS (_Версия_: 2.0.18 и более поздние версии)  
> 
> ✔SDK JavaScript Teams (_Версия_: 1.10 и более поздние версии) для работы единого входа на боковой панели собрания. 
>
> Для лучшего взаимодействия с Teams используйте последнюю версию iOS и Android.

> [!NOTE]
> **Быстрый запуск**  
>
> Самый простой способ начала работы с единым входом для вкладок — это набор средств Teams для Microsoft Visual Studio Code. Дополнительные сведения см. в статье [Единый вход с помощью набора инструментов Teams и Visual Studio Code для вкладок](../../../toolkit/visual-studio-code-tab-sso.md)

## <a name="how-sso-works-at-runtime"></a>Принцип работы единого входа во время выполнения

На приведенном ниже изображении показано, как работает единый вход.

<!-- markdownlint-disable MD033 -->
<img src="~/assets/images/tabs/tabs-sso-diagram.png" alt="Tab single sign-on SSO diagram" width="75%"/>

1. На вкладке выполняется вызов JavaScript в `getAuthToken()`. `getAuthToken()` сообщает Teams, что нужно получить маркер доступа для приложения на вкладке.
2. Если текущий пользователь использует приложение на вкладке в первый раз, будет предложено дать согласие, если оно требуется. Кроме того, появляется запрос на обработку пошаговой проверки подлинности, например, двухфакторную проверку подлинности.
3. Teams запрашивает маркер доступа к вкладке из конечной точки Microsoft Azure Active Directory (Microsoft Azure Active Directory (Azure AD)) для текущего пользователя.
4. Microsoft Azure Active Directory (Microsoft Azure Active Directory (Azure AD)) отправляет маркер доступа вкладке в приложение Teams.
5. Teams отправляет маркер доступа вкладки на вкладку как часть объекта результата, возвращаемого вызовом `getAuthToken()`.
6. Маркер анализируется в приложении вкладки с помощью JavaScript для извлечения необходимых сведений, например адреса электронной почты пользователя.

> [!NOTE]
> Метод `getAuthToken()` является допустимым только для согласия на ограниченный набор API на уровне пользователя, а именно email, profile, offline_access и OpenId. Он не используется для дополнительных областей Graph, таких как `User.Read` или `Mail.Read`. Рекомендуемые обходные пути см. в статье [Получение маркера доступа с помощью разрешений Graph](#get-an-access-token-with-graph-permissions).

API единого входа также работает в [модулях задач](../../../task-modules-and-cards/what-are-task-modules.md), которые встраивают веб-содержимое.

## <a name="develop-an-sso-microsoft-teams-tab"></a>Разработка вкладки Microsoft Teams с единым входом

В этом разделе описаны задачи, необходимые для создания вкладки Teams с единым входом. Эти задачи не зависит от языка и структуры.

### <a name="1-create-your-microsoft-azure-active-directory-azure-ad-application"></a>1. Создание приложения Microsoft Azure Active Directory (Azure AD)

> [!NOTE]
> Необходимо знать о некоторых важных ограничениях.
>
> * Поддерживаются только разрешения API Graph на уровне пользователя, а именно email, profile, offline_access и OpenId.. Если вам требуется доступ к другим областям Graph, таким как `User.Read` или `Mail.Read`, см. статью [Получение маркера доступа с помощью разрешений Graph](#get-an-access-token-with-graph-permissions).
> * Важно, чтобы доменное имя вашего приложения совпадало с доменным именем, которое вы зарегистрировали для приложения Microsoft Azure Active Directory (Azure AD).
> * В настоящее время несколько доменов для приложения не поддерживаются.
> * Пользователь должен установить для `accessTokenAcceptedVersion` нового приложения значение `2`.

**Регистрация приложения на портале Microsoft Azure Active Directory (Azure AD)**

1. Регистрация нового приложения на [портале регистрации Microsoft Azure Active Directory (Azure AD)](https://go.microsoft.com/fwlink/?linkid=2083908).
1. Выберите **Новая регистрация**. Появится страница **Регистрация приложения**.
1. На странице **Регистрация приложения** задайте следующие значения параметров.
    1. Введите **Название** приложения.
    2. Выберите **Поддерживаемые типы учетных записей**, выберите тип учетной записи одного клиента или нескольких клиентов. ¹
    * Оставьте поле **URI перенаправления** пустым.
    3. Нажмите кнопку **Зарегистрировать**.
1. На странице обзора скопируйте и сохраните **идентификатор приложения (клиента)**. Он потребуется вам позже при обновлении манифеста приложения Teams.
1. В разделе **Управление** выберите **Предоставление API**.

    > [!NOTE]
    > Если вы создаете приложение с ботом и вкладкой, введите URI идентификатора приложения в качестве `api://fully-qualified-domain-name.com/botid-{YourBotId}`.

1. Щелкните ссылку **Задать**, чтобы создать URI идентификатора приложения в следующем формате: "`api://{AppID}`". Вставьте свое полное доменное имя с косой чертой "/" в конце между двойной косой чертой и GUID. Весь идентификатор должен иметь следующий формат: "`api://fully-qualified-domain-name.com/{AppID}`". ² Например, `api://subdomain.example.com/00000000-0000-0000-0000-000000000000`. Полное доменное имя — это понятно человеку имя домена, из которого обслуживается ваше приложение. Если вы используете службу туннелирования, например ngrok, это значение необходимо обновлять при изменениях поддомена ngrok.
1. Нажмите **Добавить область**. В открывшейся панели введите **access_as_user** в качестве параметра **Имя области**.
1. В поле **Кто может давать согласие?** укажите **Администраторы и пользователи**.
1. Введите сведения в поля для настройки запроса согласия у администраторов и пользователей со значениями, подходящими для области `access_as_user`.
    * **Название согласия администратора:** Teams может получить доступ к профилю пользователя.
    * **Описание согласия администратора**: Teams может вызывать веб-API приложения в качестве текущего пользователя.
    * **Название согласия пользователя**: Teams может получать доступ к вашему профилю и делать запросы от вашего имени.
    * **Описание согласия пользователя:** Teams может вызывать API этого приложения с вашими правами.
1. Убедитесь, что параметру **Состояние** присвоено значение **Включено**.
1. Выберите **Добавить область**, чтобы сохранить сведения. Доменная часть параметра **Имя области**, отображаемая под текстовым полем, должна автоматически соответствовать URI **идентификатора приложения**, заданного на предыдущем шаге, с добавлением `/access_as_user` в конце `api://subdomain.example.com/00000000-0000-0000-0000-000000000000/access_as_user`.
1. В разделе **Авторизованные клиентские приложения** укажите приложения, которые необходимо авторизовать для веб-приложения вашего приложения. Выберите **Добавить клиентское приложение**. Введите каждый из следующих идентификаторов клиента и выберите авторизованную область, созданную на предыдущем шаге.
    * `1fec8e78-bce4-4aaf-ab1b-5451cc387264` для мобильного или настольного приложения Teams.
    * `5e3ce6c0-2b1f-4285-8d4b-75ee78787346` для веб-приложения Teams.
1. Перейдите в **Разрешения API**. Выберите **Добавить разрешение** > **Microsoft Graph** > **Делегированные разрешения**, затем добавьте следующие разрешения из API Graph:
    * User.Read, включенное по умолчанию
    * email
    * offline_access
    * OpenId
    * profile

1. Перейдите к параметру **Аутентификация**.

    > [!IMPORTANT]
    > Если приложению не предоставлено согласие ИТ-администратора, пользователи должны дать согласие при первом использовании приложения.

    Чтобы ввести URI перенаправления, сделайте следующее.
    * Выберите **Добавить платформу**.
    * Выберите **web**.
    * Введите **URI перенаправления** для вашего приложения. Этот URI — это полное доменное имя, которое вы ввели на шаге 5. За ним также следует маршрут API, на который отправляется ответ проверки подлинности. Если вы следуете любому из примеров Teams, URI будет `https://subdomain.example.com/auth-end`. Дополнительные сведения см. в статье [Поток кода авторизации OAuth 2.0](/azure/active-directory/develop/v2-oauth2-auth-code-flow).

    > [!NOTE]
    > Неявное предоставление разрешения не требуется для единого входа вкладки.

Поздравляем! Вы выполнили необходимые условия для регистрации приложения, чтобы продолжить работу с приложением для единого входа на вкладке.

> [!NOTE]
>
> * ¹ Если приложение Microsoft Azure Active Directory (Azure AD) зарегистрировано в том же клиенте, где вы делаете запрос на проверку подлинности в Teams, пользователю не предлагают дать согласие, а сразу предоставляют маркер доступа. Пользователи соглашаются на эти разрешения только в том случае, Microsoft Azure Active Directory приложение Azure AD зарегистрировано в другом клиенте.
> * ² Если настраиваемый домен не добавлен в Microsoft Azure Active Directory (Azure AD), вы получите ошибку - сообщение, что имя хоста не должно быть основано на домене, который вам уже принадлежит. Чтобы добавить настраиваемый домен Microsoft Azure Active Directory (Azure AD) и зарегистрировать его, выполните процедуру [добавления настраиваемого доменного имени Microsoft Azure Active Directory (Azure AD)](/azure/active-directory/fundamentals/add-custom-domain), а затем повторите шаг 5. Эту ошибку также можно получить, если вы не вошли в область клиента Office 365 с помощью учетных данных администратора.
> * Если вы не получили имя субъекта-пользователя (UPN) в возвращенном маркере доступа, вы можете добавить его в качестве [необязательной заявки](/azure/active-directory/develop/active-directory-optional-claims) в Microsoft Azure Active Directory (Azure AD).

### <a name="2-update-your-teams-application-manifest"></a>2. Обновите манифест приложения Teams

Чтобы добавить новые свойства в манифест Teams, используйте следующий код.

```json
"webApplicationInfo": {
  "id": "00000000-0000-0000-0000-000000000000",
  "resource": "api://subdomain.example.com/00000000-0000-0000-0000-000000000000"
}
```

* **WebApplicationInfo** — родительский элемент для указанных ниже элементов.

> [!div class="checklist"]
> * **id** — это идентификатор клиента приложения. Это ID приложения, полученный в процессе регистрации приложения в Microsoft Azure Active Directory (Azure AD).
>* **resource** — домен и поддомен вашего приложения. Это тот же URI (включая протокол `api://`), который вы зарегистрировали при создании `scope` на шаге 6. Не следует включать в ресурс путь к `access_as_user`. Доменная часть этого URI должна соответствовать домену, включая все поддомены, используемые в URL-адресах манифеста приложения Teams.

> [!NOTE]
>
>* Ресурс приложения Microsoft Azure Active Directory (Azure AD) обычно является корнем URL-адреса сайта и ИД приложения (например`api://subdomain.example.com/00000000-0000-0000-0000-000000000000`). Это значение также используется для обеспечения получения запроса из того же домена. Убедитесь, что `contentURL` для вкладки использует те же домены, что и свойство ресурса.
>* Для реализации поля `webApplicationInfo` необходимо использовать манифест версии 1.5 или более новой версии.

### <a name="3-get-an-access-token-from-your-client-side-code"></a>3. Получите маркер доступа из клиентского кода

Используйте следующий API проверки подлинности.

```javascript
var authTokenRequest = {
  successCallback: function(result) { console.log("Success: " + result); },
  failureCallback: function(error) { console.log("Failure: " + error); }
};
microsoftTeams.authentication.getAuthToken(authTokenRequest);
```

Когда вы вызываете `getAuthToken` и для разрешений на уровне пользователя требуется согласие пользователя, пользователю отображается диалоговое окно для предоставления согласия.

Получив маркер доступа при успешном обратном вызове, расшифруйте маркер доступа, чтобы просмотреть утверждения для этого маркера. При желании вручную скопируйте и вставьте маркер доступа в средство, например [jwt.ms](https://jwt.ms/). Если вы не получили имя субъекта-пользователя (UPN) в возвращенном маркере доступа, добавьте его в качестве [необязательной заявки](/azure/active-directory/develop/active-directory-optional-claims) в Microsoft Azure Active Directory (Azure AD).. Дополнительные сведения см. в разделе о [маркерах доступа](/azure/active-directory/develop/access-tokens).

<p>
    <img src="~/assets/images/tabs/tabs-sso-prompt.png" alt="Tab single sign-on SSO dialog prompt" width="75%"/>
</p>

## <a name="code-snippets"></a>Фрагменты кода

В следующем коде приводится пример потока On-Behalf-Of для получения маркера доступа с помощью библиотеки MSAL:

### <a name="c"></a>[C#](#tab/dotnet)

```csharp

IConfidentialClientApplication app = ConfidentialClientApplicationBuilder.Create(<"Client id">)
                                                .WithClientSecret(<"Client secret">)
                                                .WithAuthority($"https://login.microsoftonline.com/<"Tenant id">")
                                                .Build();
 
            try
            {
                var idToken = <"Client side token">;
                UserAssertion assert = new UserAssertion(idToken);
                List<string> scopes = new List<string>();
                scopes.Add("https://graph.microsoft.com/User.Read");
                var responseToken = await app.AcquireTokenOnBehalfOf(scopes, assert).ExecuteAsync();
                return responseToken.AccessToken.ToString();
            }
            catch (Exception ex)
            {
                return ex.Message;
            }
        }
```

### <a name="nodejs"></a>[Node.js](#tab/nodejs)

```javascript

// Exchange cliend side token with server token
  app.post('/getProfileOnBehalfOf', function(req, res) {
        var tid = < "Tenand id" >
    var token = < "Client side token" >
    var scopes = ["https://graph.microsoft.com/User.Read"];

        // Creating MSAL client
        const msalClient = new msal.ConfidentialClientApplication({
            auth: {
                clientId: < "Client ID" >,
                clientSecret: < "Client Secret" >
      }
        });

        var oboPromise = new Promise((resolve, reject) => {
            msalClient.acquireTokenOnBehalfOf({
                authority: `https://login.microsoftonline.com/${tid}`,
                oboAssertion: token,
                scopes: scopes,
                skipCache: true
            }).then(result => {
                console.log("Token is: " + result.accessToken);
            }).catch(error => {
                reject({ "error": error.errorCode });
            });
        });
```
---

## <a name="code-sample"></a>Пример кода

|**Название примера**|**Описание**|**C#**|**Node.js**|
|---------------|---------------|------|--------------|
| Единый вход на вкладке |Пример приложения Microsoft Teams для единого входа Microsoft Azure Active Directory (Azure AD)| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-sso/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/tab-sso/nodejs), </br>[Набор средств Teams](../../../toolkit/visual-studio-code-tab-sso.md)|

## <a name="known-limitations"></a>Известные ограничения

### <a name="get-an-access-token-with-graph-permissions"></a>Получение маркера доступа с разрешениями Graph

Текущая реализация для единого входа дает согласие только на разрешения на уровне пользователя, которые нельзя использовать для выполнения вызовов Graph. Чтобы получить разрешения (области), необходимые для вызова Graph, решения для SSO должны реализовать настраиваемую веб-службу для обмена маркера, полученного из SDK JavaScript Teams, на маркер, который включает необходимые области. Это можно сделать с помощью Microsoft Azure Active Directory (Azure AD) [от имени потока](/azure/active-directory/develop/v1-oauth2-on-behalf-of-flow).

### <a name="tenant-admin-consent"></a>Согласие администратора клиента

Простой способ получения согласия от имени организации в качестве администратора клиента — обратиться к `https://login.microsoftonline.com/common/adminconsent?client_id=<AAD_App_ID>`.

#### <a name="ask-for-consent-using-the-auth-api"></a>Запрос согласия с помощью API Auth

Другой подход для получения областей Graph - вывести диалоговое окно с запросом согласия, используя существующий [метод проверки подлинности Microsoft Azure Active Directory (Azure AD) через Интернет](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-pop-up-page). Этот подход включает в себя показ диалогового окна с запросом согласия Microsoft Azure Active Directory (Azure AD).

**Запрос дополнительного согласия с помощью API Auth**

1. Маркер, полученный с помощью `getAuthToken()`, должен быть обменен Microsoft Azure Active Directory (Azure AD)[ на стороне сервера от](/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow) имени потока, чтобы получить доступ к другим Graph API. Убедитесь, что для этого обмена вы используете конечную точку Graph v2.
2. Если выполнить обмен не удается, Microsoft Azure Active Directory (Azure AD) возвращает исключение "не удалось предоставить права". Обычно появляется одно из двух сообщений об ошибке, `invalid_grant` или `interaction_required`.
3. В случае сбоя обмена необходимо запросить согласие. Отобразите пользовательский интерфейс с просьбой предоставить другое согласие. Этот пользовательский интерфейс должен содержать кнопку, которая запускает диалоговое окно согласия Microsoft Azure Active Directory (Azure AD) с помощью нашего [API проверки подлинности Microsoft Azure Active Directory (Azure AD)](~/concepts/authentication/auth-silent-aad.md).
4. При запросе последующего согласия Microsoft Azure Active Directory (Azure AD) необходимо включить `prompt=consent` в [параметр строки запроса](~/tabs/how-to/authentication/auth-silent-aad.md#get-the-user-context) Microsoft Azure Active Directory (Azure AD), в противном случае Microsoft Azure Active Directory (Azure AD) не будет запрашивать другие области.
    * Вместо `?scope={scopes}`
    * Используйте `?prompt=consent&scope={scopes}`
    * Убедитесь, что `{scopes}` включает все области, которые вы запросили у пользователя, например Mail.Read или User.Read.
5. После того как пользователь предоставил больше разрешений, попробуйте повторно применить поток on-behalf-of, чтобы получить доступ к другим API.

### <a name="non-microsoft-azure-active-directory-azure-ad-authentication"></a>Проверка подлинности способом, отличным от способа Microsoft Azure Active Directory (Azure AD)

Вышеуказанное решение проверки подлинности работает только для приложений и служб, поддерживающих Microsoft Azure Active Directory (Azure AD) в качестве поставщика удостоверений. Приложения, которые хотят проверять подлинность служб, не основанных на Microsoft Azure Active Directory (Azure AD), должны по-прежнему использовать [поток проверки подлинности в Интернете](~/concepts/authentication.md) на основе всплывающего окна.

> [!NOTE]
> Единый вход поддерживается для приложений, принадлежащих заказчикам, на клиентах B2C Microsoft Azure Active Directory (Azure AD).

## <a name="step-by-step-guides"></a>Пошаговые руководства

* Следуйте [инструкциям в руководстве](../../../sbs-tabs-and-messaging-extensions-with-sso.yml) для проверки подлинности вкладок и расширений обмена сообщениями.
* Следуйте [инструкциям в руководстве](../../../sbs-tab-with-adaptive-cards.yml) для создания вкладки с адаптивными карточками.

## <a name="see-also"></a>См. также
[Бот Teams с единым входом](../../../sbs-bots-with-sso.yml)
