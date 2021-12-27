---
title: Поддержка единого входа для ботов
description: Описывает, как получить маркер пользователя. В настоящее время разработчик ботов может использовать входную карту или службу ботов Azure с поддержкой карты OAuth.
keywords: маркер, маркер пользователя, поддержка SSO для ботов, разрешения, Microsoft Graph, AAD
ms.localizationpriority: medium
ms.topic: conceptual
ms.openlocfilehash: f9934d29b9c340b7e3543420a212ae9304ba22e6
ms.sourcegitcommit: 4892d8d0fa38a472edab047754ef85b1a85be495
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/27/2021
ms.locfileid: "61608449"
---
# <a name="single-sign-on-sso-support-for-bots"></a>Поддержка единого входного знака (SSO) для ботов

Единая проверка подлинности в Azure Active Directory (AAD) безмолвно обновляет маркер проверки подлинности, чтобы свести к минимуму количество случаев, когда пользователям необходимо вводить учетные данные входа. Если пользователи соглашаются использовать ваше приложение, они не должны предоставлять согласие снова на другом устройстве, так как они подписаны автоматически. Вкладки и боты имеют аналогичный поток для поддержки SSO. Но бот [запрашивает маркеры](#request-a-bot-token) и [получает ответы](#receive-the-bot-token) с другим протоколом.

>[!NOTE]
> OAuth 2.0 — это открытый стандарт проверки подлинности и авторизации, используемый AAD и многими другими поставщиками удостоверений. Базовое понимание OAuth 2.0 является обязательным условием для работы с проверкой подлинности в Teams.

## <a name="bot-sso-at-runtime"></a>Bot SSO во время запуска

На следующем изображении иллюстрируется поток SSO в ботах:

![Bot SSO на схеме времени запуска](../../../assets/images/bots/bots-sso-diagram.png)

Следующие действия помогают вам с проверкой подлинности и маркерами бот-приложений:

1. Бот отправляет сообщение в Teams с OAuthCard, который содержит для получения маркера проверки подлинности `tokenExchangeResource` для приложения-бота. Пользователь получает сообщения во всех активных конечных точках пользователя.

   > [!NOTE]
   >
   > * Пользователь может иметь несколько активных конечных точек одновременно.
   > * Маркер бота получается от каждой активной конечной точки пользователя.
   > * Приложение должно быть установлено в личной области для поддержки единого входа.


1. Если текущий пользователь впервые использует приложение-бот, пользователю появляется запрос на одно из следующих действий:
    * При необходимости предоставить согласие.
    * Обработать пошаговую проверки подлинности, например двухфакторную проверку подлинности.

1. Teams запрашивает маркер приложения-бота из конечной точки AAD для текущего пользователя.

1. AAD отправляет маркер приложения-бота в Teams приложение.

1. Teams отправляет маркер боту в составе объекта значения, возвращаемого путем наводки с помощью **входных и tokenExchange.**
  
1. Анализируемый токен в приложении бота предоставляет необходимые сведения, например адрес электронной почты пользователя.
  
## <a name="develop-an-sso-teams-bot"></a>Разработка SSO-Teams бота
  
Следующие действия по разработке SSO-Teams бота:

1. [Регистрация приложения на портале AAD.](#register-your-app-through-the-aad-portal)
1. [Обновите манифест Teams приложения для бота.](#update-your-teams-application-manifest-for-your-bot)
1. [Добавьте код для запроса и получения маркера бота.](#add-the-code-to-request-and-receive-a-bot-token)

### <a name="register-your-app-through-the-aad-portal"></a>Регистрация приложения на портале AAD

Действия для регистрации приложения через портал AAD похожи на поток [SSO вкладки.](../../../tabs/how-to/authentication/auth-aad-sso.md) Следующие действия повеяют вас о регистрации приложения:

1. Зарегистрируйте новое приложение на [портале Azure Active Directory App Registrations.](https://go.microsoft.com/fwlink/?linkid=2083908)

1. Выберите **новую регистрацию.** Появится **страница "Регистрация** приложения".

    ![Новая регистрация](~/assets/images/authentication/SSO-bots-auth/app-registration.png)

1. В **приложении Register сделайте** следующие действия:

   > [!NOTE]
   >
   > Пользователи не запрашиваются для получения согласия и им сразу же выдают маркеры доступа, если приложение AAD зарегистрировано в том же клиенте, где они делают запрос на проверку подлинности в Teams. Однако пользователи должны предоставить согласие на разрешения, если приложение AAD зарегистрировано в другом клиенте.

    * Введите **имя** приложения.
    * Выберите **поддерживаемые типы учетных** записей, например один клиент или мультитенант.
    * Нажмите **Зарегистрировать**.

    ![Регистрация приложения](~/assets/images/authentication/SSO-bots-auth/register-application.png)

1. Перейдите на страницу обзор.
1. Скопируйте значение ID приложения **(клиента).**
1. В **статье Управление**, перейдите к **обналичить API**


   > [!TIP] 
   > Чтобы обновить манифест приложения позже, сохраните значение **ID приложения (клиента).**


   > [!IMPORTANT]
   > * Если вы строите автономный бот, введите URI приложения ID как `api://botid-{YourBotId}` . Здесь **YourBotId** — это AAD ID приложения.
   > * Если вы строите приложение с помощью бота и вкладки, введите URI ID приложения как `api://fully-qualified-domain-name.com/botid-{YourBotId}` .

1. Выберите разрешения, необходимые вашему приложению для конечной точки AAD и, необязательно, для Microsoft Graph.
1. [Предоставление разрешений](/azure/active-directory/develop/v2-permissions-and-consent) для Teams, веб-приложений и мобильных приложений.
1. Нажмите **Добавить область**.
1. В панели, которая подсказок, `access_as_user` введите в качестве **имени Область**.

   >[!NOTE]
   > Область "access_as_user" для добавления клиентского приложения для "Администраторы и пользователи".
   >
   > Необходимо помнить о следующих важных ограничениях:
   >
   > * Поддерживаются только разрешения Graph API на уровне пользователей, такие как электронная почта, профиль, offline_access и OpenId. Если вам необходим доступ к другим Graph Microsoft, например или , см. статью `User.Read` Get an access token with Graph `Mail.Read` [разрешений.](../../../tabs/how-to/authentication/auth-aad-sso.md#get-an-access-token-with-graph-permissions)
   > * Доменное имя приложения должно быть таким же, как доменное имя, которое вы зарегистрировали для AAD приложения.
   > * Несколько доменов в приложении в настоящее время не поддерживаются.
   > * Приложения, которые используют домен, не поддерживаются, так как они являются распространенными и `azurewebsites.net` могут быть угрозой безопасности.

1. В Кто **может согласиться?**, введите **администраторов и пользователей**.
1. Введите следующие сведения, чтобы настроить запросы на согласие администратора и пользователя со значениями, подходящими для `access_as_user` области.
    * **Имя отображения** согласия администратора: Teams можно получить доступ к профилю пользователя.
    * **Описание согласия администратора:** Teams может вызывать веб-API приложения в качестве текущего пользователя.
    * **Имя отображения согласия** пользователя: Teams получить доступ к вашему профилю и сделать запросы от вашего имени.
    * **Описание согласия пользователя:** Teams может вызывать API этого приложения с тем же правам, что и у вас.

    ![администратор и пользователи](~/assets/images/authentication/SSO-bots-auth/add-a-scope.png)

1. Убедитесь, что состояние **включено.**

    ![Состояние](~/assets/images/authentication/SSO-bots-auth/enabled-state.png)

1. Выберите **Добавить область,** чтобы сохранить сведения. Отображаемая доменная часть имени **Scope** должна автоматически соответствовать набору URI **ID** приложения на предыдущем шаге с приложением `/access_as_user` до `api://subdomain.example.com/00000000-0000-0000-0000-000000000000/access_as_user` конца.

1. В **уполномоченных клиентских приложениях** определите приложения, которые необходимо авторизировать для веб-приложения вашего приложения.
1. Выберите **Добавление клиентского приложения.**

    ![клиентская заявка](~/assets/images/authentication/SSO-bots-auth/add-client-application.png)

1. Введите каждый из следующих клиентских ИД и выберите авторизованную область, созданную на предыдущем шаге:
    * `1fec8e78-bce4-4aaf-ab1b-5451cc387264`для Teams или настольного приложения.
    * `5e3ce6c0-2b1f-4285-8d4b-75ee78787346`для Teams веб-приложения.

    ![id клиента](~/assets/images/authentication/SSO-bots-auth/add-client-id.png)

1. Перейдите к **проверке подлинности.**
1. В **конфигурациях платформы** выберите **Добавить платформу.**

    ![платформа](~/assets/images/authentication/SSO-bots-auth/platform-configuration.png)

1. Выберите платформу **Веб**.

    ![Настройка платформы](~/assets/images/authentication/SSO-bots-auth/configure-platform.png)

1. Введите **URL-адреса перенаправления** для приложения.

   >[!NOTE]
   > Этот URI должен быть полностью квалифицированным доменным именем. Далее следует маршрут API, куда отправляется ответ на проверку подлинности. Если вы следуете любому из Teams, URI `https://token.botframework.com/.auth/web/redirect` — это . Дополнительные сведения см. в потоке кода авторизации [OAuth 2.0.](/azure/active-directory/develop/v2-oauth2-auth-code-flow)

    ![Перенаправление uris](~/assets/images/authentication/SSO-bots-auth/configure-web.png)

1. Добавление **необходимых разрешений API.**
    * Выберите **разрешения API из** левой плоскости.
    * Выберите **Добавить платформу, чтобы** добавить все разрешения, делегированные пользователем, необходимые приложению для API вниз по течению, например User.Read.

1. Следующие действия помогут включить неявный грант:
    * Выберите **проверку подлинности** с левой области.
    * Выберите **контрольные ящики** маркеров Доступа и маркеров **ID.**
    
    ![Поток грантов](~/assets/images/authentication/SSO-bots-auth/grant-flow.png)
    
    * Выберите **Сохранить,** чтобы сохранить изменения.

#### <a name="update-manifest-in-azure-portal"></a>Манифест обновления на портале Azure

Следующие действия повеяют об обновлении манифеста бота на портале Azure:

1. Выберите **Манифест** с левой области.
1. Убедитесь, что для элемента config **установлено "accessTokenAcceptedVersion": 2**. Если нет, измените его значение на **2**.

    ![Манифест обновления](~/assets/images/bots/update-manifest.png)


   >[!NOTE]
   > Если вы уже тестируете бота в Teams, необходимо выйти из этого приложения и выйти из Teams. Затем снова впишитесь, чтобы увидеть это изменение.

1. Нажмите **Сохранить**.

#### <a name="update-the-azure-portal-with-the-oauth-connection"></a>Обновление портала Azure с подключением OAuth

В следующих действиях вы сможете обновить портал Azure с подключением OAuth:

1. На портале Azure перейдите в [ **AzureBot**](https://ms.portal.azure.com/#create/Microsoft.AzureBot)
1. Перейдите **к конфигурации** на левой области.
1. Выберите **Добавить подключение OAuth Параметры**.

    ![Параметр конфигурации](~/assets/images/authentication/SSO-bots-auth/auth-setting2.png)

1. Следующие действия повеяют о том, как заполнить форму **Параметры подключения:**

   >[!NOTE]
   > **Неявный** грант может потребоваться в AAD приложении.

    * Введите **имя** на странице **Параметр подключения.**

    >[!NOTE]
    > Имя **ссылается** на параметры кода службы бота в *шаге 5* [bot SSO во время запуска.](#bot-sso-at-runtime)

    * От **сброса поставщика** услуг выберите Azure Active Directory **v2**.
    * Введите учетные данные клиента, такие как **client Id** и **Client secret** для AAD приложения.
    * Для **URL-Exchange маркера** используйте значение области, определенное в обновлении манифеста Teams приложения [для бота.](#update-your-teams-application-manifest-for-your-bot) URL-Exchange маркера указывает SDK, что AAD настроено для SSO.
    * В **ID клиента** *введите* общие .
    * Добавьте все **области,** настроенные при указании разрешений на API ниже по течению для AAD приложения. С помощью секрета client ID и Client магазин маркеров обменивается маркером для маркера графа с определенными разрешениями.
    * Нажмите **Сохранить**.
    * Нажмите **Применить**.
   
    ![Параметр подключения](~/assets/images/authentication/Bot-connection-setting.png)

### <a name="update-your-teams-application-manifest-for-your-bot"></a>Обновление манифеста Teams приложения для бота

Если приложение содержит автономный бот, используйте следующий код, чтобы добавить новые свойства в манифест Teams приложения:

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://botid-00000000-0000-0000-0000-000000000000"
        }
```
Если приложение содержит бот и вкладку, используйте следующий код, чтобы добавить новые свойства в манифест Teams приложения:

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://subdomain.example.com/botid-00000000-0000-0000-0000-000000000000"
        }
```

**webApplicationInfo** является родителем следующих элементов:

* **id** — ID клиента приложения. Это ID приложения, полученный в рамках регистрации приложения в AAD. Не делитесь этим ID приложениями с несколькими Teams приложениями. Создайте новое приложение AAD для каждого манифеста приложения, которое использует `webApplicationInfo` .
* **ресурс** — домен и поддомен приложения. Это тот же URI, в том числе протокол, который вы зарегистрировали при создании приложения в Регистре приложения через `api://` `scope` портал [AAD.](#register-your-app-through-the-aad-portal) Не включите `access_as_user` путь в ресурс. Доменная часть этого URI должна соответствовать домену и поддоменам, используемым в URL-адресах манифеста Teams приложения.

### <a name="add-the-code-to-request-and-receive-a-bot-token"></a>Добавление кода для запроса и получения маркера бота

#### <a name="request-a-bot-token"></a>Запрос маркера бота

Запрос на токен — это обычный запрос сообщения POST с помощью существующей схемы сообщений. Он включен в вложения OAuthCard. Схема для класса OAuthCard определена в [Microsoft Bot Schema 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) и похожа на карточку входной записи. Teams рассматривает этот запрос как бесшумное приобретение маркера, если свойство `TokenExchangeResource` заполнено на карте. Для канала Teams только свойство, которое уникально определяет запрос `Id` маркера, имеет честь.

>[!NOTE]
> Поддержка Microsoft Bot Framework или поддержка `OAuthPrompt` `MultiProviderAuthDialog` проверки подлинности SSO.

Если пользователь использует приложение в первый раз и требуется согласие пользователя, следующий диалоговое окно, как представляется, продолжится с опытом согласия:

![Диалоговое окно Согласия](~/assets/images/authentication/SSO-bots-auth/bot-consent-box.png)

Когда пользователь выбирает **Продолжить**, происходят следующие события:

* Если бот определяет кнопку вход, активируется поток входных данных для ботов, аналогичный потоку входов с кнопки карточки OAuth в потоке сообщений. Разработчик должен решить, какие разрешения требуют согласия пользователя. Этот подход рекомендуется, если требуется маркер с разрешениями за пределами `openId` . Например, если вы хотите обменять маркер на ресурсы графа.

* Если бот не предоставляет кнопку входа на карточке OAuth, для получения минимального набора разрешений требуется согласие пользователя. Этот маркер полезен для базовой проверки подлинности и получения адреса электронной почты пользователя.

##### <a name="c-token-request-without-a-sign-in-button"></a>C# маркера без кнопки вход

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

Ответ с маркером отправляется с помощью действия вызова с той же схемой, что и другие действия вызова, которые получают сегодня боты. Единственным отличием является имя вызова, **вход в/tokenExchange** и **поле значений.** Поле **значений** содержит **Id**, строку начального запроса  на токен и поле маркера, строковую величину, включая маркер.

>[!NOTE]
> Вы можете получить несколько ответов на заданный запрос, если у пользователя есть несколько активных конечных точек. Необходимо оттапликировать ответы с помощью маркера.

##### <a name="c-code-to-handle-the-invoke-activity"></a>C# для обработки действия вызова

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

Имеет `turnContext.activity.value` тип [TokenExchangeInvokeRequest](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true) и содержит маркер, который может быть дополнительно использован вашим ботом. Вы должны хранить маркеры из соображений производительности и обновлять их.

### <a name="token-exchange-failure"></a>Сбой обмена маркерами

При сбое обмена маркерами используйте следующий код:

```json
{ 
    "status": "<response code>", 
    "body": 
    { 
        "id":"<unique Id>", 
        "connectionName": "<connection Name on the bot (from the OAuth card)>", 
        "failureDetail": "<failure reason if status code is not 200, null otherwise>" 
    } 
}
```

Чтобы понять, что делает бот, если биржа маркеров не запускает запрос на согласие, см. следующие действия:

>[!NOTE]
> Никаких действий пользователя не требуется, так как бот принимает действия при сбой обмена маркерами.

1. Клиент начинает беседу с ботом, запускающий сценарий OAuth.
2. Бот отправляет клиенту карту OAuth.
3. Клиент перехватывает карту OAuth перед ее отображением пользователю и проверяет, содержит ли она `TokenExchangeResource` свойство.
4. Если свойство существует, клиент отправляет `TokenExchangeInvokeRequest` боту. Клиент должен иметь обменяемый маркер для пользователя, который должен быть маркером Azure AD v2 и аудитория которого должна быть такой же, как `TokenExchangeResource.Uri` свойство. Клиент отправляет боту действие вызова со следующим кодом:

    ```json
    {
        "type": "Invoke",
        "name": "signin/tokenExchange",
        "value": 
        {
            "id": "<any unique Id>",
            "connectionName": "<connection Name on the skill bot (from the OAuth card)>",
            "token": "<exchangeable token>"
        }
    }
    ```

5. Бот обрабатывает и `TokenExchangeInvokeRequest` возвращает обратно `TokenExchangeInvokeResponse` клиенту. Клиент должен подождать, пока он не получит `TokenExchangeInvokeResponse` .

    ```json
    {
        "status": "<response code>",
        "body": 
        {
            "id":"<unique Id>",
            "connectionName": "<connection Name on the skill bot (from the OAuth card)>",
            "failureDetail": "<failure reason if status code is not 200, null otherwise>"
        }
    }
    ```

6. Если `TokenExchangeInvokeResponse` у клиента есть, клиент не показывает карту `status` `200` OAuth. См. [изображение нормального потока.](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true) Для любого другого или если не получено, клиент показывает пользователю карточку `status` `TokenExchangeInvokeResponse` OAuth. См. [изображение потока отката.](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true) Если есть какие-либо ошибки или недоставка зависимостей, таких как согласие пользователя, это действие гарантирует, что поток SSO возвращается к нормальному потоку OAuthCard.


### <a name="update-the-auth-sample"></a>Обновление примера auth

Откройте [Teams пример auth,](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) а затем выполните следующие действия, чтобы обновить его:

1. Обнови команду TeamsBot для обработки отработки входящих запросов, включив в нее следующий код:

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
  
2. Обновление, включив пароль и имя подключения, определенное в обновлении портала Azure с подключением `appsettings.json` `botId` [OAuth.](#update-the-azure-portal-with-the-oauth-connection)
3. Обнови манифест и `token.botframework.com` убедитесь, что он находится в допустимом списке доменов. Дополнительные сведения см. [в Teams примере auth.](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth)
4. Zip манифест с изображениями профиля и установить его в Teams.

## <a name="code-sample"></a>Пример кода
|**Название примера** | **Описание** |**.NET** | 
|----------------|-----------------|--------------|
|SDK для базы ботов | Пример для использования SDK-базы ботов. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/46.teams-auth)|

## <a name="step-by-step-guide"></a>Пошаговые инструкции

Следуйте [пошаговом](../../../sbs-bots-with-sso.yml)руководстве, которое поможет создать бот с включенной проверкой подлинности SSO.
