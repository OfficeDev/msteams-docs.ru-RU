---
title: Поддержка единого входа для ботов
description: Описывает, как получить маркер пользователя. В настоящее время разработчик бота может использовать вход в карточку или службу лазурного бота с поддержкой карты OAuth.
keywords: маркер, маркер пользователя, поддержка SSO для ботов
ms.topic: conceptual
ms.openlocfilehash: a023c232186ce855c0b262f8cb535ec9d05db95a
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449488"
---
# <a name="single-sign-on-sso-support-for-bots"></a>Поддержка единого входного знака (SSO) для ботов

Одновековая проверка подлинности в Azure Active Directory (AAD) минимизирует количество случаев, когда пользователям необходимо вводить свой знак в учетных данных, молча освежая маркер проверки подлинности. Если пользователи соглашаются использовать ваше приложение, они не должны предоставлять согласие снова на другом устройстве и могут войти автоматически. Поток похож на поток поддержки [SSO](../../../tabs/how-to/authentication/auth-aad-sso.md)вкладки Microsoft Teams, однако разница в [](#request-a-bot-token) протоколе заключается в том, как бот запрашивает маркеры и получает [ответы.](#receive-the-bot-token)

>[!NOTE]
> OAuth 2.0 — это открытый стандарт проверки подлинности и авторизации, используемый AAD и многими другими поставщиками удостоверений. Базовое понимание OAuth 2.0 является обязательным условием для работы с проверкой подлинности в Teams.

## <a name="bot-sso-at-runtime"></a>Bot SSO во время запуска

![Bot SSO на схеме времени запуска](../../../assets/images/bots/bots-sso-diagram.png)

Выполните следующие действия, чтобы получить маркеры проверки подлинности и бот-приложений:

1. Бот отправляет сообщение с помощью OAuthCard с `tokenExchangeResource` свойством. Он сообщает Teams, чтобы получить маркер проверки подлинности для приложения-бота. Пользователь получает сообщения на всех активных конечных точках пользователя.

    > [!NOTE]
    >* У пользователя одновременно может быть несколько активных конечных точек.
    >* Маркер бота получается с каждой конечной точки активного пользователя.
    >* Приложение должно быть установлено в личном поле для поддержки SSO.

2. Если текущий пользователь впервые использует приложение-бот, появляется запрос с просьбой сделать одно из следующих:
    * Предоставление согласия при необходимости.
    * Обработка этапной проверки подлинности, например двух факторов проверки подлинности.

3. Teams запрашивает маркер приложения-бота из конечной точки AAD для текущего пользователя.

4. AAD отправляет маркер приложения-бота в приложение Teams.

5. Teams отправляет маркер боту в составе объекта значения, возвращаемого в результате действия вызова с именем **sign-in/tokenExchange.**
  
6. Разбиванный маркер в бот-приложении предоставляет необходимые сведения, например адрес электронной почты пользователя.
  
## <a name="develop-an-sso-teams-bot"></a>Разработка бота SSO Teams
  
Выполните следующие действия по разработке бота SSO Teams:

1. [Регистрация приложения на портале AAD.](#register-your-app-through-the-aad-portal)
2. [Обновление манифеста приложения Teams для бота.](#update-your-teams-application-manifest-for-your-bot)
3. [Добавьте код для запроса и получения маркера бота.](#add-the-code-to-request-and-receive-a-bot-token)

### <a name="register-your-app-through-the-aad-portal"></a>Регистрация приложения на портале AAD

Действия по регистрации приложения через портал AAD похожи на поток [SSO вкладки.](../../../tabs/how-to/authentication/auth-aad-sso.md) Выполните следующие действия для регистрации приложения:

1. Регистрация нового приложения на [портале Регистрации приложений Azure Active Directory.](https://go.microsoft.com/fwlink/?linkid=2083908)
2. Выберите **новую регистрацию.** Появится **страница "Регистрация** приложения".
3. На странице **Регистрация приложения** введите следующие значения:
    1. Введите **имя** приложения.
    2. Выберите **поддерживаемые типы учетных записей,** выберите один клиент или многотенантный тип учетной записи.

        > [!NOTE]
        >
        > Пользователи не запрашиваются для получения согласия и им сразу же выдают маркеры доступа, если приложение AAD зарегистрировано в том же клиенте, где они делают запрос на проверку подлинности в Teams. Однако пользователи должны предоставить согласие на разрешения, если приложение AAD зарегистрировано в другом клиенте.

    3. Нажмите кнопку **Зарегистрировать**.
4. На странице обзор скопируйте и сохраните ID приложения **(клиента).** Это необходимо позднее при обновлении манифеста приложения Teams.
5. В разделе **Управление** выберите **Предоставление API**. 

   > [!IMPORTANT]
    > * Если вы строите автономный бот, введите URI приложения ID как `api://botid-{YourBotId}` . Здесь **YourBotId** — это ваш ID приложения AAD.
    > * Если вы строите приложение с помощью бота и вкладки, введите URI ID приложения как `api://fully-qualified-domain-name.com/botid-{YourBotId}` .

5. Выберите разрешения, необходимые приложению для конечной точки AAD и, необязательно, для Microsoft Graph.
6. [Предоставление разрешений](/azure/active-directory/develop/v2-permissions-and-consent) для настольных, веб-приложений и мобильных приложений Teams.
7. Выберите **Добавить область**.
8. На открываемой панели добавьте клиентские приложения, введите `access_as_user` имя **Scope.**

    >[!NOTE]
    > Область "access_as_user" для добавления клиентского приложения для "Администраторы и пользователи".
    >
    > Необходимо помнить о следующих важных ограничениях:
    >
    > * Поддерживаются только разрешения API Microsoft Graph на уровне пользователей, такие как электронная почта, профиль, offline_access и OpenId. Если вам нужен доступ к другим областьм Microsoft Graph, например или `User.Read` `Mail.Read` , см. [рекомендуемое обходное решение.](../../../tabs/how-to/authentication/auth-aad-sso.md#apps-that-require-additional-microsoft-graph-scopes)
    > * Доменное имя приложения должно быть таким же, как доменное имя, которое вы зарегистрировали для приложения AAD.
    > * Несколько доменов в приложении в настоящее время не поддерживаются.
    > * Приложения, которые используют домен, не поддерживаются, так как они являются распространенными и `azurewebsites.net` могут быть угрозой безопасности.

#### <a name="update-the-azure-portal-with-the-oauth-connection"></a>Обновление портала Azure с подключением OAuth

Выполните следующие действия по обновлению портала Azure с подключением OAuth:

1. На портале Azure перейдите к **регистрациям приложений.**

2. Перейдите **к разрешениям API.** Выберите **Добавить разрешения,** делегированные Microsoft Graph, а затем добавьте следующие разрешения из  >    >  API Microsoft Graph:
    * User.Read (включен по умолчанию)
    * рассылка
    * offline_access
    * OpenId
    * profile

3. На портале Azure перейдите к **регистрации бот-каналов.**

4. Выберите **Параметры** на левой области и выберите **параметр Добавить** в разделе Параметры подключения **OAuth.**

    ![Представление SSOBotHandle2](../../../assets/images/bots/bots-vuSSOBotHandle2-settings.png)

5. Выполните следующие действия для завершения **формы параметра "Новое подключение":**

    >[!NOTE]
    > **Неявный** грант может потребоваться в приложении AAD.

    1. Введите **имя** на странице **Параметр нового подключения.** Это имя, которое упоминается в параметрах кода службы бота в *шаге 5* bot [SSO во время запуска.](#bot-sso-at-runtime)
    2. Из **выпадаемого** поставщика услуг выберите **Azure Active Directory v2**.
    3. Введите учетные данные клиента, такие как **client id** и **client secret** для приложения AAD.
    4. Для **URL-адреса Exchange маркеров** используйте значение области, определенное в манифесте [приложения Update your Teams для бота.](#update-your-teams-application-manifest-for-your-bot) URL-адрес Exchange token указывает на SDK, что это приложение AAD настроено для SSO.
    5. В поле **"ID клиента"** введите *общие .*
    6. Добавьте все **области, настроенные** при указании разрешений на API ниже по течению для приложения AAD. С помощью секрета client id и Client, магазин маркеров обменивается маркером для маркера графа с определенными разрешениями.
    7. Нажмите **Сохранить**.

    ![Представление параметра VuSSOBotConnection](../../../assets/images/bots/bots-vuSSOBotConnection-settings.png)

### <a name="update-your-teams-application-manifest-for-your-bot"></a>Обновление манифеста приложения Teams для бота

Если приложение содержит автономный бот, используйте следующий код, чтобы добавить новые свойства в манифест приложений Teams:

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://botid-00000000-0000-0000-0000-000000000000"
        }
```
Если приложение содержит бот и вкладку, используйте следующий код, чтобы добавить новые свойства в манифест приложений Teams:

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://subdomain.example.com/botid-00000000-0000-0000-0000-000000000000"
        }
```

**webApplicationInfo** является родителем следующих элементов:

* **id** — ID клиента приложения. Это ID приложения, полученный в рамках регистрации приложения в AAD.
* **ресурс** — домен и поддомен приложения. Это тот же URI, в том числе протокол, зарегистрированный при создании приложения в Зарегистрировать приложение `api://` `scope` через портал [AAD.](#register-your-app-through-the-aad-portal) Не следует включать путь `access_as_user` в ресурс. Доменная часть этого URI должна соответствовать домену и поддоменам, используемым в URL-адресах манифеста приложения Teams.

### <a name="add-the-code-to-request-and-receive-a-bot-token"></a>Добавление кода для запроса и получения маркера бота

#### <a name="request-a-bot-token"></a>Запрос маркера бота

Запрос на токен — это обычный запрос сообщения POST с помощью существующей схемы сообщений. Он входит в вложения OAuthCard. Схема для класса OAuthCard определена в [Microsoft Bot Schema 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) и похожа на карточку для регистрации. Teams рассматривает этот запрос как бесшумное приобретение маркера, если свойство `TokenExchangeResource` заполнено на карте. В канале Teams зачтется только свойство, которое однозначно определяет запрос `Id` маркера.

>[!NOTE]
> Microsoft Bot Framework `OAuthPrompt` или `MultiProviderAuthDialog` поддерживается для проверки подлинности SSO.

Если пользователь использует приложение в первый раз и требуется согласие пользователя, следующий диалоговое окно, как представляется, продолжится с опытом согласия:

![Диалоговое окно Согласия](../../../assets/images/bots/bots-consent-dialogbox.png)

Когда пользователь выбирает **Продолжить,** происходят следующие события:

* Если бот определяет кнопку вход, запускается вход в поток ботов, аналогичный входу в потоке с кнопки карточки OAuth в потоке сообщений. Разработчик должен решить, какие разрешения требуют согласия пользователя. Этот подход рекомендуется, если требуется маркер с разрешениями за пределами `openId` . Например, если вы хотите обменять маркер на ресурсы графа.

* Если бот не предоставляет кнопку вход на карту OAuth, для минимального набора разрешений требуется согласие пользователя. Этот маркер полезен для базовой проверки подлинности и получения адреса электронной почты пользователя.

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

Ответ с маркером отправляется с помощью действия вызова с той же схемой, что и другие действия вызова, которые получают сегодня боты. Единственное отличие — это имя вызова, **вход/tokenExchange** и **поле значений.** Поле **значений** содержит **Id**, строку начального запроса  на токен и поле маркера, строковую величину, включая маркер.

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

В случае сбоя обмена маркерами используйте следующий код:

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

5. Бот обрабатывает и `TokenExchangeInvokeRequest` возвращает обратно `TokenExchangeInvokeResponse` клиенту. Клиент должен подождать, пока он получит `TokenExchangeInvokeResponse` .

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

6. Если `TokenExchangeInvokeResponse` у клиента есть a, клиент не показывает карту `status` `200` OAuth. См. [изображение нормального потока.](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true) Для любого другого или если не получено, клиент показывает пользователю карточку `status` `TokenExchangeInvokeResponse` OAuth. См. [изображение потока отката.](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true) Это гарантирует, что поток SSO возвращается к нормальному потоку OAuthCard в случае ошибок или невыполнения зависимостей, таких как согласие пользователя.


### <a name="update-the-auth-sample"></a>Обновление примера auth

Пример [auth Open Teams,](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) а затем выполните следующие действия, чтобы обновить его:

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
3. Обнови манифест и `token.botframework.com` убедитесь, что он находится в допустимом списке доменов. Дополнительные сведения см. в [примере teams auth](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth).
4. Zip манифест с изображениями профиля и установить его в Teams.

## <a name="code-sample"></a>Пример кода
|**Пример имени** | **Описание** |**.NET** | 
|----------------|-----------------|--------------|
|SDK для базы ботов | Пример для использования SDK-базы ботов. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/experimental/teams-sso/csharp_dotnetcore)|
