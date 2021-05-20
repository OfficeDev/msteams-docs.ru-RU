---
title: Поддержка единого входа для ботов
description: Описывает, как получить токен пользователя. В настоящее время разработчик ботов может использовать знак в карте или службу лазурного бота с поддержкой карты OAuth.
keywords: токен, токен пользователя, поддержка SSO для ботов
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: a43c2a46561149ff97d039a3ba8fe9f4472e2073
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566096"
---
# <a name="single-sign-on-sso-support-for-bots"></a>Поддержка ботов с одним ва-пом (SSO)

Одноэтажная аутентификация в Azure Active Directory (AAD) сводит к минимуму количество случаев, когда пользователи должны вводить свой знак в учетные данные, молча обновляя маркер аутентификации. Если пользователи соглашаются использовать ваше приложение, им не нужно снова предоставлять согласие на другом устройстве и они могут войти в приложение автоматически. Поток похож на поток поддержки [Microsoft Teams SSO,](../../../tabs/how-to/authentication/auth-aad-sso.md)однако, разница в протоколе о том, как бот запрашивает [токены](#request-a-bot-token) [и получает ответы.](#receive-the-bot-token)

>[!NOTE]
> OAuth 2.0 является открытым стандартом для проверки подлинности и авторизации, используемой AAD и многими другими поставщиками идентификации. Базовое понимание OAuth 2.0 является необходимым условием для работы с аутентификацией в Teams.

## <a name="bot-sso-at-runtime"></a>Бот SSO во время выполнения

![Bot SSO на диаграмме времени выполнения](../../../assets/images/bots/bots-sso-diagram.png)

Выполните следующие шаги, чтобы получить токены аутентификации и бот-приложений:

1. Бот отправляет сообщение с OAuthCard, которая содержит `tokenExchangeResource` свойство. В нем Teams, чтобы получить токен аутентификации для приложения бота. Пользователь получает сообщения во всех конечных точках активных пользователей.

    > [!NOTE]
    >* Пользователь может иметь более одной активной конечной точки за один раз.
    >* Токен бота получен из каждой активной конечной точки пользователя.
    >* Приложение должно быть установлено в личном прицеле для поддержки SSO.

1. Если текущий пользователь использует приложение бота в первый раз, появляется запрос, запрашивающий пользователя сделать одно из следующих:
    * При необходимости предоставьте согласие.
    * Обработать проверку проверки подлинности, например двухфакторную аутентификацию.

1. Teams запрашивает токен приложения бота из конечной точки AAD для текущего пользователя.

1. AAD отправляет токен приложения бота в Teams приложение.

1. Teams отправляет токен боту как часть объекта значения, возвращенного действием вызова с **именем войти/tokenExchange.**
  
1. Разобраный маркер в приложении бота предоставляет необходимую информацию, такую как адрес электронной почты пользователя.
  
## <a name="develop-an-sso-teams-bot"></a>Разработка SSO Teams бота
  
Выполните следующие шаги по разработке SSO Teams бота:

1. [Зарегистрируйте приложение через портал AAD.](#register-your-app-through-the-aad-portal)
1. [Обновите Teams приложение для вашего бота.](#update-your-teams-application-manifest-for-your-bot)
1. [Добавьте код для запроса и получения токена бота.](#add-the-code-to-request-and-receive-a-bot-token)

### <a name="register-your-app-through-the-aad-portal"></a>Зарегистрируйте приложение через портал AAD

Шаги по регистрации приложения через портал AAD аналогичны потоку [вкладок SSO.](../../../tabs/how-to/authentication/auth-aad-sso.md) Выполните следующие шаги для регистрации приложения:

1. Зарегистрируйте новое приложение в Azure Active Directory [- портал App Registrations.](https://go.microsoft.com/fwlink/?linkid=2083908)
2. Выберите **новую регистрацию**. В **Регистре отображается** страница заявки.
3. На странице **регистрации приложения** введите следующие значения:
    1. **Введите имя** для приложения.
    2. Выберите **типы поддерживаемых счетов,** выберите одного арендатора или тип многотенантной учетной записи.

        > [!NOTE]
        >
        > Пользователи не запрашиваются для согласия и получают токены доступа сразу, если приложение AAD зарегистрировано в том же арендаторе, где они делают запрос на аутентификацию в Teams. Однако пользователи должны дать согласие на получение разрешений, если приложение AAD зарегистрировано в другом арендаторе.

    3. Нажмите кнопку **Зарегистрировать**.
4. На странице обзора скопировать и сохранить **идентификатор приложения (клиента).** Вы нуждаетеся в нем позже при обновлении Teams приложения манифест.
5. В разделе **Управление** выберите **Предоставление API**. 

   > [!IMPORTANT]
    > * Если вы строите автономный бот, введите идентификатор приложения URI как `api://botid-{YourBotId}` . Здесь **YourBotId** ваш идентификатор приложения AAD.
    > * Если вы строите приложение с ботом и вкладкой, введите идентификатор приложения URI как `api://fully-qualified-domain-name.com/botid-{YourBotId}` .

5. Выберите разрешения, которые нужны вашему приложению для конечной точки AAD, и, по желанию, для microsoft Graph.
6. [Предоставление разрешений на](/azure/active-directory/develop/v2-permissions-and-consent) Teams настольных, веб- и мобильных приложений.
7. Выберите **Добавить область**.
8. В панели, которая открывается, добавьте клиентское приложение, `access_as_user` введя в качестве **имени область.**

    >[!NOTE]
    > Область "access_as_user", используемая для добавления клиент-приложения, предназначена для "Администраторов и пользователей".
    >
    > Вы должны знать о следующих важных ограничениях:
    >
    > * Поддерживаются только разрешения microsoft Graph уровня пользователя, такие как электронная почта, профиль, offline_access и OpenId. Если вам нужен доступ к другим Graph, например, `User.Read` `Mail.Read` или, [см.](../../../tabs/how-to/authentication/auth-aad-sso.md#apps-that-require-additional-graph-scopes)
    > * Доменное имя вашего приложения должно быть таким же, как доменное имя, которое вы зарегистрировали для вашего приложения AAD.
    > * Несколько доменов на приложение в настоящее время не поддерживаются.
    > * Приложения, которые используют `azurewebsites.net` домен, не поддерживаются, поскольку он является общим и может быть угрозой безопасности.

#### <a name="update-the-azure-portal-with-the-oauth-connection"></a>Обновление портала Azure с подключением OAuth

Выполните следующие шаги по обновлению портала Azure с подключением OAuth:

1. На портале Azure перейдите на **регистрацию приложений.**

2. Перейдите **на разрешения API**. Выберите **Добавить разрешение**  >  **Microsoft**  >  **Graph, а затем** добавить следующие разрешения от Microsoft Graph API:
    * User.Read (включен по умолчанию)
    * email
    * offline_access
    * OpenId
    * profile

3. На портале Azure перейдите на **регистрацию бот-каналов.**

4. Выберите **Параметры** на левом стекле и **выберите Настройку добавления** **в разделе OAuth Connection Параметры** разделе.

    ![Вид SSOBotHandle2](../../../assets/images/bots/bots-vuSSOBotHandle2-settings.png)

5. Выполните следующие шаги для завершения **формы «Новая настройка** соединения»:

    >[!NOTE]
    > **В заявке** AAD может потребоваться неявный грант.

    1. **Введите имя** на **странице Настройка нового** соединения. Это имя, которое упоминается в настройках кода службы бота в *шаге 5* [Bot SSO во время выполнения.](#bot-sso-at-runtime)
    2. Из **сервиса-поставщика** высадки, выберите **Azure Active Directory v2**.
    3. Введите учетные данные клиента, **такие как идентификатор** **клиента и секрет** клиента для приложения AAD.
    4. Для **URL-адреса Exchange, используйте** значение сферы, определенное [в обновлении вашего Teams приложения для вашего бота.](#update-your-teams-application-manifest-for-your-bot) URL-Exchange Token указывает SDK, что это приложение AAD настроено для SSO.
    5. В поле **идентификатора арендатора** введите *общий*.
    6. Добавьте все **области, настроенные** при указании разрешений в API для приложения AAD. При условии, что идентификатор Клиента и Клиент секрет, токен-магазин обменивает токен на графический токен с определенными разрешениями.
    7. Нажмите **Сохранить**.

    ![Представление настроек VuSSOBotConnection](../../../assets/images/bots/bots-vuSSOBotConnection-settings.png)

### <a name="update-your-teams-application-manifest-for-your-bot"></a>Обновите Teams приложение для вашего бота

Если приложение содержит автономного бота, то используйте следующий код, чтобы добавить новые свойства в Teams приложения:

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://botid-00000000-0000-0000-0000-000000000000"
        }
```
Если приложение содержит бота и вкладку, то используйте следующий код, чтобы добавить новые свойства в Teams приложения:

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://subdomain.example.com/botid-00000000-0000-0000-0000-000000000000"
        }
```

**webApplicationInfo** является родителем следующих элементов:

* **id** - Идентификатор клиента приложения. Это идентификатор приложения, который вы получили в рамках регистрации приложения с AAD.
* **ресурс** - домен и поддомен вашего приложения. Это тот же URI, включая протокол, `api://` который вы зарегистрировали при `scope` создании вашего приложения в [Регистре через портал AAD.](#register-your-app-through-the-aad-portal) Вы не должны включать `access_as_user` путь в свой ресурс. Доменная часть этого URI должна соответствовать домену и субдоменам, используемым в URL-адресах вашего Teams приложения.

### <a name="add-the-code-to-request-and-receive-a-bot-token"></a>Добавить код для запроса и получения токена бота

#### <a name="request-a-bot-token"></a>Запрос токена бота

Запрос на токен является обычным запросом сообщений POST с использованием существующей схемы сообщения. Он включен в приложения OAuthCard. Схема для класса OAuthCard определена в [Microsoft Bot Schema 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) и похожа на карту. Teams рассматривает этот запрос как тихое приобретение токенов, `TokenExchangeResource` если недвижимость заполнена на карте. Для Teams канал, только `Id` свойство, которое однозначно идентифицирует запрос токенов, выполнено.

>[!NOTE]
> Данные Microsoft Bot Framework `OAuthPrompt` или `MultiProviderAuthDialog` поддерживаются для проверки подлинности SSO.

Если пользователь использует приложение в первый раз и требуется согласие пользователя, следующее диалоговое окно, как представляется, продолжается с опытом согласия:

![Согласие диалоговое окно](../../../assets/images/bots/bots-consent-dialogbox.png)

Когда пользователь выбирает **Продолжить ,** происходят следующие события:

* Если бот определяет кнопку в записи, знак потока для ботов срабатывает аналогично знаку потока из кнопки карты OAuth в потоке сообщений. Разработчик должен решить, какие разрешения требуют согласия пользователя. Этот подход рекомендуется, если вам требуется токен с разрешениями за пределами `openId` . Например, если вы хотите обменять токен на ресурсы графика.

* Если бот не предоставляет кнопку в записи на карту OAuth, для минимального набора разрешений требуется согласие пользователя. Этот маркер полезен для базовой аутентификации и получения адреса электронной почты пользователя.

##### <a name="c-token-request-without-a-sign-in-button"></a>Запрос токенов на C'a без кнопки ва-подвок

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

#### <a name="receive-the-bot-token"></a>Получение токена бота

Ответ с маркером отправляется через действие вызова с той же схемой, что и другие действия вызова, которые боты получают сегодня. Разница лишь в имени вызова, **ввименеле/токене и** поле **значения.** Поле **значения** содержит Id , **строку** первоначального запроса на получить токен и поле **токена,** значение строки, включая токен.

>[!NOTE]
> Вы можете получить несколько ответов на данный запрос, если пользователь имеет несколько активных конечных точек. Вы должны вывести ответы с маркером.

##### <a name="c-code-to-handle-the-invoke-activity"></a>Код C-кода для обработки действия вызова

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

Тип `turnContext.activity.value` [TokenExchangeInvokeRequest и содержит токен,](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true) который может быть использован вашим ботом. Вы должны хранить токены по причинам производительности и обновлять их.

### <a name="token-exchange-failure"></a>Сбой обмена токенов

В случае сбоя обмена токенов используйте следующий код:

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

Чтобы понять, что делает бот, когда обмен токенов не может вызвать запрос согласия, см.

>[!NOTE]
> Никакие действия пользователя не должны быть приняты, поскольку бот выполняет действия, когда обмен токенов терпит неудачу.

1. Клиент начинает разговор с ботом, запуская сценарий OAuth.
2. Бот отправляет клиенту карту OAuth.
3. Клиент перехватывает карту OAuth перед отображением ее пользователю и проверяет, содержит ли она `TokenExchangeResource` свойство.
4. Если свойство существует, клиент отправляет `TokenExchangeInvokeRequest` бота. Клиент должен иметь обмениваемый токен для пользователя, который должен быть токеном Azure AD v2 и чья аудитория должна быть такой же, как `TokenExchangeResource.Uri` собственность. Клиент отправляет действие вызова боту со следующим кодом:

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

6. Если `TokenExchangeInvokeResponse` имеет a , то клиент не показывает карту `status` `200` OAuth. Посмотреть [нормальное изображение потока.](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true) Для любого `status` другого или `TokenExchangeInvokeResponse` если не получено, то клиент показывает карту OAuth пользователю. Посмотреть [изображение обратного потока.](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true) Это гарантирует, что поток SSO возвращается к нормальному потоку OAuthCard в случае каких-либо ошибок или неудовлетворенных зависимостей, таких как согласие пользователя.


### <a name="update-the-auth-sample"></a>Обновление образца аута

Откройте [Teams, а затем](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) выполните следующие шаги, чтобы обновить его:

1. Обновление TeamsBot для обработки deduping входящего запроса, включив следующий код:

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
  
2. Обновление, `appsettings.json` чтобы включить пароль и `botId` имя соединения, определенное [в обновлении портала Azure с подключением OAuth.](#update-the-azure-portal-with-the-oauth-connection)
3. Обновите манифест и `token.botframework.com` убедитесь, что он находится в списке действительных доменов. Для получения дополнительной [информации, Teams образца аута](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth).
4. Завехайте манифест с изображениями профиля и установите его в Teams.

## <a name="code-sample"></a>Пример кода
|**Название образца** | **Описание** |**.NET** | 
|----------------|-----------------|--------------|
|Бот фреймвок SDK | Пример для использования бота фреймворка SDK. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/experimental/teams-sso/csharp_dotnetcore)|
