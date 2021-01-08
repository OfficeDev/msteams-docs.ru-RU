---
title: Поддержка единого входа для ботов
description: Описывает, как получить маркер пользователя. В настоящее время разработчик ботов может использовать карточку для входов или службу ботов Azure с поддержкой карты OAuth.
keywords: маркер, маркер пользователя, поддержка службы SSO для ботов
ms.openlocfilehash: ee9dbee063acf90f5596fc95d002caf53f88a08a
ms.sourcegitcommit: 0a9e91c65d88512eda895c21371b3cd4051dca0d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/23/2020
ms.locfileid: "49729082"
---
# <a name="single-sign-on-sso-support-for-bots"></a>Поддержка единого входов (SSO) для ботов

Проверка подлинности с единым входом в Azure Active Directory (Azure AD) минимизирует количество случаев, когда пользователям нужно вводить свои учетные данные для входа, автоматически обновив маркер проверки подлинности. Если пользователи соглашаются использовать ваше приложение, им не придется повторно соглашаться на другом устройстве и они будут автоматически входить в нее. Поток очень похож на поддержку [SSO вкладки Teams.]( ../../../tabs/how-to/authentication/auth-aad-sso.md) Разница заключается в протоколе запроса маркеров и получения ответов ботом.

OAuth 2.0 — это открытый стандарт проверки подлинности и авторизации, используемый Azure Active Directory (Azure AD) и многими другими поставщиками удостоверений. Базовое понимание OAuth 2.0 является необходимым условием для работы с проверкой подлинности в Teams.

## <a name="bot-sso-at-runtime"></a>Бот SSO во время работы

![Схема SSO бота во время работы](../../../assets/images/bots/bots-sso-diagram.png)

1. Бот отправляет сообщение со свойством OAuthCard. `tokenExchangeResource` Он сообщает Teams, что необходимо получить маркер проверки подлинности для приложения-бота. Пользователь получает сообщения во всех активных конечных точках пользователя.

    > [!NOTE]
    >* Пользователь может одновременно иметь несколько активных конечных точек.  
    >* Маркер бота получается от каждой активной конечной точки пользователя.
    >* В настоящее время для поддержки единого входов требуется, чтобы приложение было установлено в личной области.

2. Если текущий пользователь впервые использовал ваше приложение-бот, будет предложено согласиться (если требуется согласие) или обработать пошаговую проверку подлинности (например, двух-факторную проверку подлинности).

3. Microsoft Teams запрашивает маркер приложения-бота из конечной точки Azure AD для текущего пользователя.

4. Azure AD отправляет маркер приложения-бота в приложение Teams.

5. Microsoft Teams отправляет маркер боту как часть объекта значения, возвращаемого действием вызова с именем sign-in/tokenExchange.
  
6. Маркер будет разлиться в бот-приложении для извлечения необходимых сведений, например адреса электронной почты пользователя.
  
## <a name="develop-a-single-sign-on-microsoft-teams-bot"></a>Разработка бота единого вход в Microsoft Teams
  
Для разработки бота Microsoft Teams с SSO необходимо сделать следующее:

1. [Создание бесплатной учетной записи Azure](#create-an-azure-account)
2. [Обновление манифеста приложения Teams](#update-your-app-manifest)
3. [Добавление кода для запроса и получения маркера бота](#request-a-bot-token)

### <a name="create-an-azure-account"></a>Создание учетной записи Azure

Этот шаг похож на поток [SSO табули:](../../../tabs/how-to/authentication/auth-aad-sso.md)

1. Получите свой [ИД приложения Azure AD](/graph/concepts/auth-register-app-v2) для настольного, веб-клиента Или мобильного клиента Teams.
2. Укажите разрешения, необходимые приложению для конечной точки Azure AD и,при желании, Microsoft Graph.
3. [Предоставление разрешений для](/azure/active-directory/develop/v2-permissions-and-consent) классических, веб-и мобильных приложений Teams.
4. Выберите **"Добавить область".**
5. На открываемой панели добавьте клиентские приложения, введите `access_as_user` имя **области.**

    >[!NOTE]
    > Область "access_as_user", используемая для добавления клиентского приложения, — "Администраторы и пользователи".

    > [!IMPORTANT]
    > * Если вы строите автономный бот, задайте для URI ИД приложения URI `api://botid-{YourBotId}` здесь, **ВашBotId** ссылается на ваш ИД приложения Azure AD.
    > * Если вы строите приложение с помощью бота и вкладки, установите для URI ИД приложения задав `api://fully-qualified-domain-name.com/botid-{YourBotId}` его.

### <a name="update-your-app-manifest"></a>Обновление манифеста приложения

Добавьте новые свойства в манифест Microsoft Teams:

**WebApplicationInfo —** родительский элемент следующих элементов:

> [!div class="checklist"]
>
> * **id** — ИД клиента приложения. Это ИД приложения, полученный при регистрации приложения в Azure AD.
>* **resource** — домен и поддомен приложения. Это тот же URI (включая протокол), который вы зарегистрировали при создании на `api://` `scope` шаге 6 выше. Не следует включать путь `access_as_user` в ресурс. Доменная часть этого URI должна соответствовать домену, в том числе поддоменам, используемым в URL-адресах манифеста приложения Teams.

```json
"webApplicationInfo": {
  "id": "00000000-0000-0000-0000-000000000000",
  "resource": "api://subdomain.example.com/00000000-0000-0000-0000-000000000000"
}
```

### <a name="request-a-bot-token"></a>Запрос маркера бота

Запрос на получения маркера является обычным запросом post сообщения (с использованием существующей схемы сообщения). Он включается во вложения OAuthCard. Схема для класса OAuthCard определена в [microsoft Bot Schema 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) и очень похожа на карточку для входов. Teams будет рассматривать этот запрос как получение маркера в тихом режиме, если свойство заполнено `TokenExchangeResource` на карточке. Для канала Teams мы считаем только свойство, которое уникальным образом идентифицирует `Id` запрос маркера.

>[!NOTE]
> Bot Framework или поддерживается для проверки подлинности с единым `OAuthPrompt` `MultiProviderAuthDialog` входом.

Если это первый раз, когда пользователь использует ваше приложение и требуется согласие пользователя, пользователю будет показано диалоговое окно для продолжения работы с согласием, аналогичное приведенному ниже. Когда пользователь выбирает **"Продолжить",** в зависимости от того, определен бот или нет, и кнопки для входов в OAuthCard происходят две разные вещи.

![Диалоговое окно "Согласие"](../../../assets/images/bots/bots-consent-dialogbox.png)

Если бот определяет кнопку для входов, поток входов для ботов будет активен аналогично потоку входов с кнопки карточки в потоке сообщений. Разработчик решает, какие разрешения нужно запросить у пользователя. Этот подход рекомендуется, если вам нужен маркер с разрешениями за пределами , например, если вы хотите обменять маркер для `openId` ресурсов graph.

Если бот не предоставляет кнопку для регистрации на карточке, он инициирует согласие пользователя на минимальный набор разрешений. Этот маркер полезен для базовой проверки подлинности и получения адреса электронной почты пользователя.

**Запрос маркера C# без кнопки для регистрации:**

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

#### <a name="receiving-the-token"></a>Получение маркера

Ответ с маркером отправляется с помощью действия вызова с той же схемой, что и другие, вызываемой действиями, которые боты получают сегодня. Единственное отличие состоит в имени вызова,  входе/маркереExchange и поле значения, которое будет содержать ИД (строку) исходного запроса для получения маркера и поля маркера (строка, включаемая маркер).    Обратите внимание, что вы можете получить несколько ответов на заданный запрос, если у пользователя несколько активных конечных точек. Вы можете отреагировать на ответы с помощью маркера.

**Код C#, реагируя на обработку действия вызова:**

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

Тип `turnContext.activity.value` [TokenExchangeInvokeRequest](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true) содержит маркер, который может дополнительно использоваться ботом. Храните маркеры безопасно из соображений производительности и обновляйте их.

### <a name="update-the-azure-portal-with-the-oauth-connection"></a>Обновление портала Azure с помощью подключения OAuth

1. На портале Azure перейдите к регистрации каналов **ботов.**

2. Переключение в **раздел "Параметры"** и выберите **"Добавить параметр"** в разделе "Параметры подключения OAuth".

    ![Представление SSOBotHandle2](../../../assets/images/bots/bots-vuSSOBotHandle2-settings.png)

3. **Заполнять форму параметра** подключения:

    > [!div class="checklist"]
    >
    > * Введите имя нового параметра подключения. Это имя, на которое будет ссылаться код службы ботов на **шаге 5.**
    > * В выпадаемом каталоге "Поставщик услуг" выберите **Azure Active Directory V2.**
    >* Введите учетные данные клиента для приложения AAD.

    >[!NOTE]
    > **В приложении** AAD может потребоваться неявное предоставление.

    >* Для URL-адреса Exchange маркера используйте значение области, определенное на предыдущем шаге приложения AAD. Наличие URL-адреса Exchange маркера указывает SDK, что это приложение AAD настроено для SSO.
    >* Укажите "common" в **качестве ИД клиента.**
    >* Добавьте все области, настроенные при указании разрешений для нисходящего API для приложения AAD. Если у вас есть ИД клиента и секрет клиента, хранилище маркеров будет обмениваться маркером на маркер графа с определенными разрешениями.
    >* Нажмите кнопку **Сохранить**.

    ![Представление Параметров VuSSOBotConnection](../../../assets/images/bots/bots-vuSSOBotConnection-settings.png)

### <a name="update-the-auth-sample"></a>Обновление примера auth

Начните с примера [auth teams](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth).

1. Обновив TeamsBot, включив в него следующее. Чтобы обработать deduping входящих запросов, см. ниже:

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
  
2. `appsettings.json`Обновим имя, чтобы включить `botId` пароль и имя подключения, определенное выше.
3. Обновим манифест и `token.botframework.com` убедитесь, что он находится в разделе "Допустимые домены".
4. Замейте манифест изображениями профилей и установите его в Teams.

#### <a name="additional-code-samples"></a>Дополнительные примеры кода

* [Пример C# с использованием bot Framework SDK.](https://github.com/microsoft/BotBuilder-Samples/tree/main/experimental/teams-sso/csharp_dotnetcore)

* [Пример C# с помощью SDK Bot Framework для дедипликации запроса маркера.](https://microsoft.sharepoint.com/:u:/t/ExtensibilityandFundamentals/Ea36rUGiN1BGt1RiLOb-mY8BGMF8NwPtronYGym0sCGOTw?e=4bB682)

* Пример на C# без использования магазина маркеров [SDK Bot Framework.](https://microsoft-my.sharepoint-df.com/:u:/p/tac/EceKDXrkMn5AuGbh6iGid8ABKEVQ6hkxArxK1y7-M8OVPw)
