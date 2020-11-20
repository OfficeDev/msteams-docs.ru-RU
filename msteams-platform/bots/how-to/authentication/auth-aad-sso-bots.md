---
title: Поддержка единого входа для ботов
description: Описывается получение маркера пользователя. В настоящее время для самостоятельного разработчика можно использовать карточку входа или службу Azure Bot с поддержкой карточки OAuth.
keywords: маркер, маркер пользователя, поддержка единого входа для Боты
ms.openlocfilehash: a056ce1a8bf0e59c9f4f30392df3bce7e8c63e00
ms.sourcegitcommit: 64acd30eee8af5fe151e9866c13226ed3f337c72
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/18/2020
ms.locfileid: "49346856"
---
# <a name="single-sign-on-sso-support-for-bots"></a>Поддержка единого входа (SSO) для Боты

Проверка подлинности с единым входом в Azure Active Directory (Azure AD) сводит к минимуму число попыток ввода учетных данных для входа пользователями, обновляя маркер проверки подлинности без уведомления. Если пользователи согласились использовать ваше приложение, им не нужно будет согласиться на другое устройство и автоматически выполнить вход в систему. Этот процесс очень похож на [поддержку единого входа для вкладки Teams]( ../../../tabs/how-to/authentication/auth-aad-sso.md). Разница — это протокол, который используется для получения маркеров запросов Bot и получения ответов.

OAuth 2,0 — это открытый стандарт проверки подлинности и авторизации, используемый Azure Active Directory (Azure AD) и многими другими поставщиками удостоверений. Базовое понимание OAuth 2,0 является необходимым условием для работы с проверкой подлинности в Teams.

## <a name="bot-sso-at-runtime"></a>SSO SSO во время выполнения

![Схема SSO SSO во время выполнения](../../../assets/images/bots/bots-sso-diagram.png)

1. Bot отправляет сообщение с Оаускард, которое содержит `tokenExchangeResource` свойство. Он указывает Teams на получение маркера проверки подлинности для приложения Bot. Пользователь получает сообщения во всех активных конечных точках пользователя.

> [!NOTE]
>* Пользователь может одновременно иметь более одной активной конечной точки.  
>* Маркер Bot получен от каждой активной конечной точки пользователя.
>* В настоящее время для поддержки единого входа приложение должно быть установлено в личной области.

2. Если в первый раз текущий пользователь использует приложение Bot, будет выдаваться запрос на согласие (если требуется согласие) или обрабатывать проверку подлинности (например, двухфакторная проверка подлинности).

3. Microsoft Teams запрашивает маркер приложения Bot из конечной точки Azure AD для текущего пользователя.

4. Azure AD отправляет маркер приложения Bot в приложение Teams.

5. Microsoft Teams отправляет маркер участнику Bot как часть объекта value, возвращаемого действием Invoke, с именем Sign-in/Токенексчанже.
  
6. Маркер будет проанализирован в приложении Bot для извлечения необходимой информации, например, адреса электронной почты пользователя.
  
## <a name="develop-a-single-sign-on-microsoft-teams-bot"></a>Разработка ленты единого входа Microsoft Teams
  
Следующие действия: необходимы для разработки единого входа Microsoft Teams Bot:

1. [Создание бесплатной учетной записи Azure](#create-an-azure-account)
2. [Обновление манифеста приложения Teams](#update-your-app-manifest)
3. [Добавление кода для запроса и получения маркера Bot](#request-a-bot-token)

### <a name="create-an-azure-account"></a>Создание учетной записи Azure

Этот шаг аналогичен последующему [входу в табуляцию](../../../tabs/how-to/authentication/auth-aad-sso.md):

1. Получение [идентификатора приложения Azure AD](/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in).
2. Укажите разрешения, необходимые вашему приложению для конечной точки Azure AD, и (при необходимости) Microsoft Graph.
3. [Предоставление разрешений](/azure/active-directory/develop/howto-create-service-principal-portal#configure-access-policies-on-resources) для настольных приложений, веб-приложений и мобильных приложений Teams.
4. Предварительная авторизация Teams, нажав кнопку **Добавить область** и на открывшейся панели, введите `access_as_user` **имя области**.

> [!IMPORTANT]
> * При создании автономной программы Bot задайте для идентификатора URI идентификатор приложения `api://botid-{YourBotId}` .
> * Если вы создаете приложение с помощью ленты и вкладки, задайте для идентификатора URI идентификатор приложения `api://fully-qualified-domain-name.com/botid-{YourBotId}` .

### <a name="update-your-app-manifest"></a>Обновление манифеста приложения

Добавьте новые свойства в манифест Microsoft teams:

**WebApplicationInfo** — родительский элемент следующих элементов:

> [!div class="checklist"]
>
> * **ID** — идентификатор клиента приложения. Это идентификатор приложения, полученный в ходе регистрации приложения с помощью Azure AD.
>* **Resource** — домен и поддомен приложения. Это тот же URI (включая `api://` протокол), который вы зарегистрировали при создании `scope` на шаге 6. Не следует включать `access_as_user` путь в ресурс. Доменная часть этого URI должна быть соотнесена с доменом, включая все поддомены, используемые в URL-адресах манифеста приложения Teams.

```json
"webApplicationInfo": {
  "id": "00000000-0000-0000-0000-000000000000",
  "resource": "api://subdomain.example.com/00000000-0000-0000-0000-000000000000"
}
```

### <a name="request-a-bot-token"></a>Запрос маркера Bot

Запрос на получение маркера является обычным запросом POST Message (с использованием существующей схемы сообщения). Он включен в вложения объекта Оаускард. Схема для класса Оаускард определена в [схеме Microsoft Bot 4,0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) , и она очень похожа на карточку входа. Если `TokenExchangeResource` свойство заполнено на карточке, Teams будет обрабатывать этот запрос как необъявляемый токен. Для канала Teams мы соблюдаем только `Id` свойство, которое уникально идентифицирует запрос маркера.

Если вы впервые используете приложение, а пользователь не дойдет согласие пользователя, в диалоговом окне будет отображаться диалоговое окно, в котором будет выполняться согласие, аналогичный приведенному ниже. Когда пользователь выбирает **Continue (продолжить**), выполняются два различных действия в зависимости от того, определен ли Bot или нет, и кнопку входа на оаускард.

![Диалоговое окно "согласие"](../../../assets/images/bots/bots-consent-dialogbox.png)

Если элемент Bot определяет кнопку входа, то поток входа для Боты будет срабатывать аналогично потоку входа с помощью кнопки карточки в потоке сообщений. Разработчик должен принять решение о том, какие разрешения необходимо запросить у пользователя. Этот подход рекомендуется в тех случаях, когда вам нужен маркер с разрешениями `openId` , например, если вы хотите обмениваться маркером для ресурсов Graph.

Если на карточке ленты не предоставляется кнопка входа, она инициирует согласие пользователя на минимальный набор разрешений. Этот маркер полезен для обычной проверки подлинности и считывания адреса электронной почты пользователя.

**Запрос маркера C# без кнопки входа**:

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

Ответ с маркером отправляется через действие Invoke с той же схемой, что и другие вызовы, которые Боты получать сегодня. Единственное отличие заключается в том, что имя Invoke, **Sign-in/токенексчанже** и поле **value** , которое будет содержать **идентификатор** (строку) начального запроса для получения маркера, и поле **маркер** (строковое значение, включая маркер). Обратите внимание, что вы можете получить несколько ответов для данного запроса, если у пользователя есть несколько активных конечных точек. Вы можете подублировать ответы с маркером.

**Код C#, реагирующий на обработку действия Invoke**:

```csharp
protected override async Task<InvokeResponse> OnInvokeActivity
  (ITurnContext<IInvokeActivity> turnContext, CancellationToken cancellationToken)
        {
            try
            {
                if (turnContext.Activity.Name == SignInConstants.TokenExchangeOperationName && turnContext.Activity.ChannelId == Channels.Msteams)
                {
                    await OnTokenResponse(turnContext, cancellationToken);
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

`turnContext.activity.value`Тип относится к типу [токенексчанжеинвокерекуест](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true) и содержит маркер, который можно использовать для работы с роботом. Безопасное хранение маркеров по соображениям производительности и их обновление.

### <a name="update-the-azure-portal-with-the-oauth-connection"></a>Обновление портала Azure с подключением OAuth

1. На портале Azure вернитесь к **регистрации каналов ленты**.

2. Перейдите к колонке **Параметры** и выберите пункт **Добавить параметр** в разделе Параметры подключения OAuth.

![Представление SSOBotHandle2](../../../assets/images/bots/bots-vuSSOBotHandle2-settings.png)

3. Заполните форму **параметров подключения** .

> [!div class="checklist"]
>
> * Введите имя для нового параметра подключения. Это имя, которое будет указываться в ссылках внутри параметров кода службы Bot в **действии 5**.
> * В раскрывающемся списке Поставщик услуг выберите **Azure Active Directory v2**.
>* Введите учетные данные клиента для приложения AAD.
>* Для URL-адреса обмена маркерами используйте значение Scope, определенное на предыдущем шаге приложения AAD. Присутствие URL-адреса Exchange маркера указывает пакету SDK, что это приложение AAD настроено для единого входа.
>* Укажите "Common" в качестве **идентификатора клиента**.
>* Добавьте все области, настроенные при указании разрешений на доступ к подчиненным API для приложения AAD. Если указан идентификатор клиента и секрет клиента, хранилище маркеров будет обмениваться маркером для маркера графа с определенными разрешениями.
>* Нажмите кнопку **Сохранить**.

![Представление параметра Вуссоботконнектион](../../../assets/images/bots/bots-vuSSOBotConnection-settings.png)

### <a name="update-the-auth-sample"></a>Обновление примера проверки подлинности

Начните с [примера проверки подлинности Teams](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth).

1. Обновите Теамсбот, чтобы включить следующие функции. Чтобы обработать дедупинг входящего запроса, см.

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
  
2. Обновите, `appsettings.json` чтобы включить `botId` , пароль и имя подключения, указанные выше.
3. Обновите манифест и убедитесь, что `token.botframework.com` он находится в разделе Допустимые домены.
4. Поzip-файл манифеста с изображениями профиля и установите его в Teams.

#### <a name="additional-code-samples"></a>Дополнительные примеры кода

* [Пример кода на языке C# с помощью пакета SDK для Bot Framework](https://microsoft-my.sharepoint-df.com/:u:/p/vul/ETZQfeTViDlCv-frjgTIincB7dvk2HOnma1TLvcoeGGIxg?e=uPq62c).

* [Пример кода на C# с помощью пакета SDK Bot Framework для дедупликации запроса маркера](https://microsoft.sharepoint.com/:u:/t/ExtensibilityandFundamentals/Ea36rUGiN1BGt1RiLOb-mY8BGMF8NwPtronYGym0sCGOTw?e=4bB682).

* [Пример кода на языке C# без использования хранилища маркеров пакета SDK Bot Framework](https://microsoft-my.sharepoint-df.com/:u:/p/tac/EceKDXrkMn5AuGbh6iGid8ABKEVQ6hkxArxK1y7-M8OVPw)
