---
title: Поддержка единого входа для ботов
description: Описывает, как получить маркер пользователя. В настоящее время разработчик ботов может использовать карточку для входов или службу ботов Azure с поддержкой карты OAuth.
keywords: маркер, маркер пользователя, поддержка службы SSO для ботов
ms.topic: conceptual
ms.openlocfilehash: 8669e00fcfcfb69844c4d63c9e7aa06b47567705
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014497"
---
# <a name="single-sign-on-sso-support-for-bots"></a>Поддержка единого входов (SSO) для ботов

Проверка подлинности с единым входом в Azure Active Directory (AAD) сводит к минимуму количество случаев, когда пользователям необходимо вводить свои учетные данные путем обновления маркера проверки подлинности автоматически. Если пользователи соглашаются использовать ваше приложение, им не нужно повторно предоставлять согласие на другом устройстве и они могут автоматически входить в приложение. Поток похож на тот, который поддерживается службой [SSO](../../../tabs/how-to/authentication/auth-aad-sso.md)для вкладок Microsoft [](#request-a-bot-token) Teams, однако разница заключается в протоколе запроса маркеров и получения ответов [ботом.](#receive-the-bot-token)

>[!NOTE]
> OAuth 2.0 — это открытый стандарт проверки подлинности и авторизации, используемый AAD и многими другими поставщиками удостоверений. Базовое понимание OAuth 2.0 является необходимым условием для работы с проверкой подлинности в Teams.

## <a name="bot-sso-at-runtime"></a>Бот SSO во время работы

![Схема SSO бота во время работы](../../../assets/images/bots/bots-sso-diagram.png)

Выполните следующие действия, чтобы получить аутентификацию и маркеры приложения-бота:

1. Бот отправляет сообщение со свойством OAuthCard. `tokenExchangeResource` Он сообщает Teams, что необходимо получить маркер проверки подлинности для приложения-бота. Пользователь получает сообщения на всех активных конечных точках пользователя.

    > [!NOTE]
    >* Пользователь может иметь несколько активных конечных точек одновременно.
    >* Маркер бота получается от каждой активной конечной точки пользователя.
    >* Приложение должно быть установлено в личной области для поддержки SSO.

2. Если текущий пользователь использует ваше приложение-бот в первый раз, появится запрос с запросом на одно из следующих этапов:
    * Предоставление согласия при необходимости.
    * Обработка проверки подлинности с пошаговой проверкой подлинности, например двух факторов.

3. Teams запрашивает маркер приложения-бота из конечной точки AAD для текущего пользователя.

4. AAD отправляет маркер приложения-бота в приложение Teams.

5. Teams отправляет маркер боту как часть объекта значения, возвращаемого действием вызова с именем **sign-in/tokenExchange.**
  
6. Разноравневый маркер в приложении-боте предоставляет необходимые сведения, например адрес электронной почты пользователя.
  
## <a name="develop-an-sso-teams-bot"></a>Разработка бота SSO Teams
  
Выполните следующие действия, чтобы разработать бот Для SSO Teams:

1. [Зарегистрируйте свое приложение на портале AAD.](#register-your-app-through-the-aad-portal)
2. [Обновите манифест приложения Teams для бота.](#update-your-teams-application-manifest-for-your-bot)
3. [Добавьте код для запроса и получения маркера бота.](#add-the-code-to-request-and-receive-a-bot-token)

### <a name="register-your-app-through-the-aad-portal"></a>Регистрация приложения на портале AAD

Действия для регистрации приложения на портале AAD похожи на поток [SSO табули.](../../../tabs/how-to/authentication/auth-aad-sso.md) Чтобы зарегистрировать приложение, выполните следующие действия:

1. Зарегистрируйте новое приложение на [портале Регистрации приложений Azure Active Directory.](https://go.microsoft.com/fwlink/?linkid=2083908)
2. Выберите **новую регистрацию.** Появится **страница "Регистрация** приложения".
3. На странице **"Регистрация приложения"** введите следующие значения:
    1. Введите **имя** приложения.
    2. Выберите **поддерживаемые типы учетных записей,** выберите один клиент или тип мультитенантной учетной записи.

        > [!NOTE]
        >
        > Пользователи не запрашивают согласие и сразу им ируются маркеры доступа, если приложение AAD зарегистрировано в том же клиенте, где они делают запрос на проверку подлинности в Teams. Однако пользователи должны предоставить согласие на предоставление разрешений, если приложение AAD зарегистрировано в другом клиенте.

    3. Нажмите кнопку **Зарегистрировать**.
4. На странице обзора скопируйте и сохраните ИД приложения **(клиента).** Оно потребуется позже при обновлении манифеста приложения Teams.
5. В разделе **Управление** выберите **Предоставление API**. 

   > [!IMPORTANT]
    > * Если вы строите автономный бот, введите URI ИД приложения как `api://botid-{YourBotId}` . Здесь **YourBotId** — ваш ИД приложения AAD.
    > * Если вы строите приложение с помощью бота и вкладки, введите URI ИД приложения как `api://fully-qualified-domain-name.com/botid-{YourBotId}` .

5. Выберите разрешения, необходимые приложению для конечной точки AAD и (при желании) для Microsoft Graph.
6. [Предоставление разрешений для](/azure/active-directory/develop/v2-permissions-and-consent) классических, веб-и мобильных приложений Teams.
7. Выберите **"Добавить область".**
8. На открываемой панели добавьте клиентские приложения, введите `access_as_user` имя **области.**

    >[!NOTE]
    > Область "access_as_user", используемая для добавления клиентского приложения, — "Администраторы и пользователи".
    >
    > Необходимо помнить о следующих важных ограничениях:
    >
    > * Поддерживаются только разрешения API Microsoft Graph на уровне пользователя, такие как электронная почта, профиль, offline_access и OpenId. Если вам нужен доступ к другим областьм Microsoft Graph, например или, см. `User.Read` `Mail.Read` [рекомендуемое решение.](../../../tabs/how-to/authentication/auth-aad-sso.md#apps-that-require-additional-microsoft-graph-scopes)
    > * Доменное имя приложения должно быть таким же, как и доменное имя, зарегистрированное для приложения AAD.
    > * Несколько доменов на приложение в настоящее время не поддерживаются.
    > * Приложения, которые используют домен, не поддерживаются, так как они являются общими и `azurewebsites.net` могут быть угрозой безопасности.

#### <a name="update-the-azure-portal-with-the-oauth-connection"></a>Обновление портала Azure с помощью подключения OAuth

Выполните следующие действия, чтобы обновить портал Azure с подключением OAuth:

1. На портале Azure перейдите к **регистрации приложений.**

2. Перейдите **к разрешениям API.** Выберите **"Добавить разрешения microsoft**  >  **Graph**  >  **Delegated permissions",** а затем добавьте следующие разрешения из API Microsoft Graph:
    * User.Read (включен по умолчанию)
    * email
    * offline_access
    * OpenId
    * profile

3. На портале Azure перейдите к процедуре **регистрации каналов ботов.**

4. Выберите **"Параметры"** в левой области и выберите **"Добавить параметр"** в разделе "Параметры подключения **OAuth".**

    ![Представление SSOBotHandle2](../../../assets/images/bots/bots-vuSSOBotHandle2-settings.png)

5. Выполните следующие действия, чтобы завершить создание формы **"Параметры подключения":**

    >[!NOTE]
    > **В приложении** AAD может потребоваться неявное предоставление.

    1. Введите **имя на** странице **"Новый параметр подключения".** Это имя, на которое ссылается код службы ботов в *шаге 5* bot [SSO во время работы.](#bot-sso-at-runtime)
    2. В **выпадаемом** каталоге "Поставщик услуг" выберите **Azure Active Directory 2.**
    3. Введите учетные данные клиента, такие как **ид клиента** и **секрет** клиента для приложения AAD.
    4. Для **URL-адреса Exchange маркера** используйте значение области, определенное в манифесте приложения [Teams для бота.](#update-your-teams-application-manifest-for-your-bot) URL-адрес Exchange маркеров указывает SDK, что это приложение AAD настроено для SSO.
    5. В поле **"ИД клиента"** *введите общий.*
    6. Добавьте все **области, настроенные** при указании разрешений для нисходящего API для приложения AAD. При условии, что в хранилище маркеров предоставлены ИД клиента и секрет клиента, он обменивается маркером на маркер графа с определенными разрешениями.
    7. Нажмите кнопку **Сохранить**.

    ![Представление Параметров VuSSOBotConnection](../../../assets/images/bots/bots-vuSSOBotConnection-settings.png)

### <a name="update-your-teams-application-manifest-for-your-bot"></a>Обновление манифеста приложения Teams для бота

Если приложение содержит автономный бот, используйте следующий код для добавления новых свойств в манифест приложения Teams:

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://botid-00000000-0000-0000-0000-000000000000"
        }
```
Если приложение содержит бота и вкладку, используйте следующий код для добавления новых свойств в манифест приложения Teams:

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://subdomain.example.com/botid-00000000-0000-0000-0000-000000000000"
        }
```

**webApplicationInfo является** родительским элементом следующих элементов:

* **id** — ИД клиента приложения. Это ИД приложения, полученный при регистрации приложения в AAD.
* **resource** — домен и поддомен приложения. Это тот же URI, включая протокол, зарегистрированный при создании приложения на портале `api://` `scope` [AAD.](#register-your-app-through-the-aad-portal) Не следует включать `access_as_user` путь в ресурс. Доменная часть этого URI должна соответствовать домену и поддоменам, используемым в URL-адресах манифеста приложения Teams.

### <a name="add-the-code-to-request-and-receive-a-bot-token"></a>Добавление кода для запроса и получения маркера бота

#### <a name="request-a-bot-token"></a>Запрос маркера бота

Запрос на токен — это обычный запрос post с использованием существующей схемы сообщения. Он включается во вложения OAuthCard. Схема для класса OAuthCard определена в [microsoft Bot Schema 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) и аналогична карточке для входов. Teams обрабатывает этот запрос как получение маркера в тихом режиме, если свойство заполнено `TokenExchangeResource` на карточке. Для канала Teams засчитано только свойство, уникальным образом идентифицирует запрос `Id` маркера.

>[!NOTE]
> Microsoft Bot Framework или microsoft Bot Framework `OAuthPrompt` `MultiProviderAuthDialog` поддерживают проверку подлинности SSO.

Если пользователь использует приложение в первый раз и требуется согласие пользователя, отображается следующее диалоговое окно для продолжения работы с согласием:

![Диалоговое окно "Согласие"](../../../assets/images/bots/bots-consent-dialogbox.png)

Когда пользователь выбирает **"Продолжить",** происходят следующие события:

* Если бот определяет кнопку для входов, запускается поток входов для ботов, аналогичный потоку входов из кнопки карточки OAuth в потоке сообщений. Разработчик должен решить, какие разрешения требуют согласия пользователя. Этот подход рекомендуется, если вам требуется маркер с разрешениями, которые выходят за `openId` рамки. Например, если вы хотите обменять маркер на ресурсы graph.

* Если бот не предоставляет кнопку для регистрации на карте OAuth, для минимального набора разрешений требуется согласие пользователя. Этот маркер полезен для базовой проверки подлинности и получения адреса электронной почты пользователя.

##### <a name="c-token-request-without-a-sign-in-button"></a>Запрос маркера C# без кнопки для регистрации

```csharp
    var attachment = new Attachment
            {
                Content = new OAuthCard
                {
                    TokenExchangeResource = new TokenExchangeResource
                    {
                        Id = requestId
                    }
                },
                ContentType = OAuthCard.ContentType,
            };
            var activity = MessageFactory.Attachment(attachment);

            // NOTE: This activity needs to be sent in the 1:1 conversation between the bot and the user. 
            // If the bot supports group and channel scope, this code should be updated to send the request to the 1:1 chat. 

       await turnContext.SendActivityAsync(activity, cancellationToken);
```

#### <a name="receive-the-bot-token"></a>Получение маркера бота

Ответ с маркером отправляется с помощью действия вызова с той же схемой, что и другие действия вызова, которые боты получают сегодня. Единственное отличие состоит в имени вызова, **входе/маркереExchange** и **поле значения.** Поле **значения** содержит **ID**, строку исходного запроса  для получения маркера и поля маркера, строку, включаемую маркер.

>[!NOTE]
> Если у пользователя несколько активных конечных точек, вы можете получить несколько ответов на заданный запрос. Необходимо отлагонять ответы с помощью маркера.

##### <a name="c-code-to-handle-the-invoke-activity"></a>Код C# для обработки действия вызова

```csharp
    protected override async Task<InvokeResponse> OnInvokeActivityAsync
    (ITurnContext<IInvokeActivity> turnContext, CancellationToken cancellationToken)
            {
                try
                {
                    if (turnContext.Activity.Name == SignInConstants.TokenExchangeOperationName && turnContext.Activity.ChannelId == Channels.Msteams)
                    {
                        await OnTokenResponseEventAsync(turnContext, cancellationToken);
                        return new InvokeResponse() { Status = 200 };
                    }
                    else
                    {
                        return await base.OnInvokeActivityAsync(turnContext, cancellationToken);
                    }
                }
                catch (InvokeResponseException e)
                {
                    return e.CreateInvokeResponse();
                }
            }
```

Тип `turnContext.activity.value` [TokenExchangeInvokeRequest](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true) содержит маркер, который может дополнительно использоваться ботом. Для повышения производительности маркеры необходимо хранить и обновлять.

### <a name="update-the-auth-sample"></a>Обновление примера auth

Откройте [пример auth Teams](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) и выполните следующие действия, чтобы обновить его:

1. Обновив TeamsBot для обработки отладки входящих запросов, включив следующий код:

    ```csharp
        protected override async Task OnSignInInvokeAsync(ITurnContext<IInvokeActivity> turnContext, CancellationToken cancellationToken)
            {
                await Dialog.RunAsync(turnContext, ConversationState.CreateProperty<DialogState>(nameof(DialogState)), cancellationToken);
            }
        protected override async Task OnTokenResponseEventAsync(ITurnContext<IEventActivity> turnContext, CancellationToken cancellationToken)
            {
                await Dialog.RunAsync(turnContext, ConversationState.CreateProperty<DialogState>(nameof(DialogState)), cancellationToken);
            }
    ```
  
2. Обновление с использованием пароля и имени подключения, определенного на портале Azure с подключением `appsettings.json` `botId` [OAuth.](#update-the-azure-portal-with-the-oauth-connection)
3. Обновим манифест и `token.botframework.com` убедитесь, что он находится в допустимом списке доменов. Дополнительные сведения см. в [примере auth Teams.](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth)
4. Замейте манифест изображениями профилей и установите его в Teams.

#### <a name="additional-code-samples"></a>Дополнительные примеры кода

* [Пример C# с использованием bot Framework SDK.](https://github.com/microsoft/BotBuilder-Samples/tree/main/experimental/teams-sso/csharp_dotnetcore)
