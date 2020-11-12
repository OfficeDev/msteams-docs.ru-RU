---
title: Поддержка единого входа для Боты
description: Описывается получение маркера пользователя. В настоящее время для самостоятельного разработчика можно использовать карточку входа или службу Azure Bot с поддержкой карточки OAuth.
keywords: маркер, маркер пользователя, поддержка единого входа для Боты
ms.openlocfilehash: 0b896f7e13847f529075b5562a6c3eb2542482bf
ms.sourcegitcommit: df9448681d2a81f1029aad5a5e1989cd438d1ae0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/03/2020
ms.locfileid: "48877866"
---
# <a name="single-sign-on-sso-support-for-bots"></a><span data-ttu-id="72fbd-105">Поддержка единого входа (SSO) для Боты</span><span class="sxs-lookup"><span data-stu-id="72fbd-105">Single sign-on (SSO) support for bots</span></span>

<span data-ttu-id="72fbd-106">Проверка подлинности с единым входом в Azure Active Directory (Azure AD) сводит к минимуму число попыток ввода учетных данных для входа пользователями, обновляя маркер проверки подлинности без уведомления.</span><span class="sxs-lookup"><span data-stu-id="72fbd-106">Single sign-on authentication in Azure Active Directory (Azure AD) minimizes the number of times users need to enter their login credentials by silently refreshing the authentication token.</span></span> <span data-ttu-id="72fbd-107">Если пользователи согласились использовать ваше приложение, им не нужно будет согласиться на другое устройство и автоматически выполнить вход в систему.</span><span class="sxs-lookup"><span data-stu-id="72fbd-107">If users agrees to use your app, they will not have to consent again on another device and will be signed in automatically.</span></span> <span data-ttu-id="72fbd-108">Этот процесс очень похож на [поддержку единого входа для вкладки Teams]( ../../../tabs/how-to/authentication/auth-aad-sso.md).</span><span class="sxs-lookup"><span data-stu-id="72fbd-108">The flow is very similar to the [Teams tab SSO support]( ../../../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="72fbd-109">Разница — это протокол, который используется для получения маркеров запросов Bot и получения ответов.</span><span class="sxs-lookup"><span data-stu-id="72fbd-109">The difference is the protocol for how a bot requests tokens and receives responses.</span></span>

<span data-ttu-id="72fbd-110">OAuth 2,0 — это открытый стандарт проверки подлинности и авторизации, используемый Azure Active Directory (Azure AD) и многими другими поставщиками удостоверений.</span><span class="sxs-lookup"><span data-stu-id="72fbd-110">OAuth 2.0 is an open standard for authentication and authorization used by Azure Active Directory (Azure AD) and many other identity providers.</span></span> <span data-ttu-id="72fbd-111">Базовое понимание OAuth 2,0 является необходимым условием для работы с проверкой подлинности в Teams.</span><span class="sxs-lookup"><span data-stu-id="72fbd-111">A basic understanding of OAuth 2.0 is a prerequisite for working with authentication in Teams.</span></span>

## <a name="bot-sso-at-runtime"></a><span data-ttu-id="72fbd-112">SSO SSO во время выполнения</span><span class="sxs-lookup"><span data-stu-id="72fbd-112">Bot SSO at runtime</span></span>

![Схема SSO SSO во время выполнения](../../../assets/images/bots/bots-sso-diagram.png)

1. <span data-ttu-id="72fbd-114">Bot отправляет сообщение с Оаускард, которое содержит `tokenExchangeResource` свойство.</span><span class="sxs-lookup"><span data-stu-id="72fbd-114">The bot sends a message with an OAuthCard that contains the `tokenExchangeResource` property.</span></span> <span data-ttu-id="72fbd-115">Он указывает Teams на получение маркера проверки подлинности для приложения Bot.</span><span class="sxs-lookup"><span data-stu-id="72fbd-115">It tells Teams to obtain an authentication token for the bot application.</span></span> <span data-ttu-id="72fbd-116">Пользователь получает сообщения во всех активных конечных точках пользователя.</span><span class="sxs-lookup"><span data-stu-id="72fbd-116">The user receives messages at all the active endpoints of the user.</span></span>

> [!NOTE]
> <span data-ttu-id="72fbd-117">✔ Пользователь может одновременно иметь более одной активной конечной точки.</span><span class="sxs-lookup"><span data-stu-id="72fbd-117">✔ A user can have more than one active endpoint at a time.</span></span>  
> <span data-ttu-id="72fbd-118">✔ Маркер Bot получен от каждой активной конечной точки пользователя.</span><span class="sxs-lookup"><span data-stu-id="72fbd-118">✔ The bot token is received from every active endpoint of the user.</span></span>
> <span data-ttu-id="72fbd-119">В настоящее время для ✔ поддержки единого входа приложение должно устанавливаться в личной области.</span><span class="sxs-lookup"><span data-stu-id="72fbd-119">✔ Single sign-on support currently requires the app to be installed in personal scope.</span></span>

2. <span data-ttu-id="72fbd-120">Если в первый раз текущий пользователь использует приложение Bot, будет выдаваться запрос на согласие (если требуется согласие) или обрабатывать проверку подлинности (например, двухфакторная проверка подлинности).</span><span class="sxs-lookup"><span data-stu-id="72fbd-120">If it is the first time the current user has used your bot application, there will be a request prompt to consent (if consent is required) or to handle step-up authentication (such as two-factor authentication).</span></span>

3. <span data-ttu-id="72fbd-121">Microsoft Teams запрашивает маркер приложения Bot из конечной точки Azure AD для текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="72fbd-121">Microsoft Teams requests the bot application token from the Azure AD endpoint for the current user.</span></span>

4. <span data-ttu-id="72fbd-122">Azure AD отправляет маркер приложения Bot в приложение Teams.</span><span class="sxs-lookup"><span data-stu-id="72fbd-122">Azure AD sends the bot application token to the Teams application.</span></span>

5. <span data-ttu-id="72fbd-123">Microsoft Teams отправляет маркер участнику Bot как часть объекта value, возвращаемого действием Invoke, с именем Sign-in/Токенексчанже.</span><span class="sxs-lookup"><span data-stu-id="72fbd-123">Microsoft Teams sends the token to the bot as part of the value object returned by the invoke activity with the name sign-in/tokenExchange.</span></span>
  
6. <span data-ttu-id="72fbd-124">Маркер будет проанализирован в приложении Bot для извлечения необходимой информации, например, адреса электронной почты пользователя.</span><span class="sxs-lookup"><span data-stu-id="72fbd-124">The token will be parsed in the bot application to extract the needed information, such as the user's email address.</span></span>
  
## <a name="develop-an-single-sign-on-microsoft-teams-bot"></a><span data-ttu-id="72fbd-125">Разработка ленты единого входа Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="72fbd-125">Develop an Single sign-on Microsoft Teams bot</span></span>
  
<span data-ttu-id="72fbd-126">Следующие действия: необходимы для разработки единого входа Microsoft Teams Bot:</span><span class="sxs-lookup"><span data-stu-id="72fbd-126">The following steps: are required to develop an SSO Microsoft Teams bot:</span></span>

1. [<span data-ttu-id="72fbd-127">Создание бесплатной учетной записи Azure</span><span class="sxs-lookup"><span data-stu-id="72fbd-127">Create a Azure free account</span></span>](#create-an-azure-account)
2. [<span data-ttu-id="72fbd-128">Обновление манифеста приложения Teams</span><span class="sxs-lookup"><span data-stu-id="72fbd-128">Update your Teams app manifest</span></span>](#update-your-app-manifest)
3. [<span data-ttu-id="72fbd-129">Добавление кода для запроса и получения маркера Bot</span><span class="sxs-lookup"><span data-stu-id="72fbd-129">Add the code to request and receive the bot token</span></span>](#request-a-bot-token)

### <a name="create-an-azure-account"></a><span data-ttu-id="72fbd-130">Создание учетной записи Azure</span><span class="sxs-lookup"><span data-stu-id="72fbd-130">Create an Azure account</span></span>

<span data-ttu-id="72fbd-131">Этот шаг похож на процесс обработки [последовательности входа в Tab](../../../tabs/how-to/authentication/auth-aad-sso.md) :</span><span class="sxs-lookup"><span data-stu-id="72fbd-131">This step is similar to the [tab SSO flow](../../../tabs/how-to/authentication/auth-aad-sso.md) flow:</span></span>

1. <span data-ttu-id="72fbd-132">Получение [идентификатора приложения Azure AD](/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in).</span><span class="sxs-lookup"><span data-stu-id="72fbd-132">Get your [Azure AD Application ID](/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in).</span></span>
2. <span data-ttu-id="72fbd-133">Укажите разрешения, необходимые вашему приложению для конечной точки Azure AD, и (при необходимости) Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="72fbd-133">Specify the permissions that your application needs for the Azure AD endpoint and, optionally, Microsoft Graph.</span></span>
3. <span data-ttu-id="72fbd-134">[Предоставление разрешений](/azure/active-directory/develop/howto-create-service-principal-portal#configure-access-policies-on-resources) для настольных приложений, веб-приложений и мобильных приложений Teams.</span><span class="sxs-lookup"><span data-stu-id="72fbd-134">[Grant permissions](/azure/active-directory/develop/howto-create-service-principal-portal#configure-access-policies-on-resources) for Teams desktop, web, and mobile applications.</span></span>
4. <span data-ttu-id="72fbd-135">Предварительная авторизация Teams, нажав кнопку **Добавить область** и на открывшейся панели, введите `access_as_user` **имя области**.</span><span class="sxs-lookup"><span data-stu-id="72fbd-135">Pre-authorize Teams by selecting the **Add a scope** button and in the panel that opens, enter `access_as_user` as the **Scope name**.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="72fbd-136">При создании автономной программы Bot задайте для идентификатора URI идентификатор приложения `api://botid-{YourBotId}` .</span><span class="sxs-lookup"><span data-stu-id="72fbd-136">If you are building a standalone bot, set the Application ID URI to `api://botid-{YourBotId}` .</span></span>
> * <span data-ttu-id="72fbd-137">Если вы создаете приложение с помощью ленты и вкладки, задайте для идентификатора URI идентификатор приложения `api://fully-qualified-domain-name.com/botid-{YourBotId}` .</span><span class="sxs-lookup"><span data-stu-id="72fbd-137">If you are building an app with a bot and a tab, set the Application ID URI to `api://fully-qualified-domain-name.com/botid-{YourBotId}`.</span></span>

### <a name="update-your-app-manifest"></a><span data-ttu-id="72fbd-138">Обновление манифеста приложения</span><span class="sxs-lookup"><span data-stu-id="72fbd-138">Update your app manifest</span></span>

<span data-ttu-id="72fbd-139">Добавьте новые свойства в манифест Microsoft teams:</span><span class="sxs-lookup"><span data-stu-id="72fbd-139">Add new properties to your Microsoft Teams manifest:</span></span>

<span data-ttu-id="72fbd-140">**WebApplicationInfo** — родительский элемент следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="72fbd-140">**WebApplicationInfo** - The parent of the following elements:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="72fbd-141">**ID** — идентификатор клиента приложения.</span><span class="sxs-lookup"><span data-stu-id="72fbd-141">**id** - The client ID of the application.</span></span> <span data-ttu-id="72fbd-142">Это идентификатор приложения, полученный в ходе регистрации приложения с помощью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="72fbd-142">This is the application ID that you obtained as part of registering the application with Azure AD.</span></span>
>* <span data-ttu-id="72fbd-143">**Resource** — домен и поддомен приложения.</span><span class="sxs-lookup"><span data-stu-id="72fbd-143">**resource** - The domain and subdomain of your application.</span></span> <span data-ttu-id="72fbd-144">Это тот же URI (включая `api://` протокол), который вы зарегистрировали при создании `scope` на шаге 6.</span><span class="sxs-lookup"><span data-stu-id="72fbd-144">This is the same URI (including the `api://` protocol) that you registered when creating your `scope` in step 6 above.</span></span> <span data-ttu-id="72fbd-145">Не следует включать `access_as_user` путь в ресурс.</span><span class="sxs-lookup"><span data-stu-id="72fbd-145">You shouldn't include the `access_as_user` path in your resource.</span></span> <span data-ttu-id="72fbd-146">Доменная часть этого URI должна быть соотнесена с доменом, включая все поддомены, используемые в URL-адресах манифеста приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="72fbd-146">The domain part of this URI should match the domain, including any subdomains, used in the URLs of your Teams application manifest.</span></span>

```json
"webApplicationInfo": {
  "id": "00000000-0000-0000-0000-000000000000",
  "resource": "api://subdomain.example.com/00000000-0000-0000-0000-000000000000"
}
```

### <a name="request-a-bot-token"></a><span data-ttu-id="72fbd-147">Запрос маркера Bot</span><span class="sxs-lookup"><span data-stu-id="72fbd-147">Request a bot token</span></span>

<span data-ttu-id="72fbd-148">Запрос на получение маркера является обычным запросом POST Message (с использованием существующей схемы сообщения).</span><span class="sxs-lookup"><span data-stu-id="72fbd-148">The request to get the token is a normal POST message request (using the existing message schema).</span></span> <span data-ttu-id="72fbd-149">Он включен в вложения объекта Оаускард.</span><span class="sxs-lookup"><span data-stu-id="72fbd-149">It is included in the attachments of an OAuthCard.</span></span> <span data-ttu-id="72fbd-150">Схема для класса Оаускард определена в [схеме Microsoft Bot 4,0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) , и она очень похожа на карточку входа.</span><span class="sxs-lookup"><span data-stu-id="72fbd-150">The schema for the OAuthCard class is defined in [Microsoft Bot Schema 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) and it is very similar to a sign-in card.</span></span> <span data-ttu-id="72fbd-151">Если `TokenExchangeResource` свойство заполнено на карточке, Teams будет обрабатывать этот запрос как необъявляемый токен.</span><span class="sxs-lookup"><span data-stu-id="72fbd-151">Teams will treat this request as a silent token acquisition if the `TokenExchangeResource` property is populated on the card.</span></span> <span data-ttu-id="72fbd-152">Для канала Teams мы соблюдаем только `Id` свойство, которое уникально идентифицирует запрос маркера.</span><span class="sxs-lookup"><span data-stu-id="72fbd-152">For the Teams channel we honor only the `Id` property, which uniquely identifies a token request.</span></span>

<span data-ttu-id="72fbd-153">Если вы впервые используете приложение, а пользователь не дойдет согласие пользователя, в диалоговом окне будет отображаться диалоговое окно, в котором будет выполняться согласие, аналогичный приведенному ниже.</span><span class="sxs-lookup"><span data-stu-id="72fbd-153">If this is the first time the user is using your application and the user consent is required, the user will be shown a dialog to continue with the consent experience similar to the one below.</span></span> <span data-ttu-id="72fbd-154">Когда пользователь выбирает **Continue (продолжить** ), выполняются два различных действия в зависимости от того, определен ли Bot или нет, и кнопку входа на оаускард.</span><span class="sxs-lookup"><span data-stu-id="72fbd-154">When the user selects **Continue** , two different things occur depending on whether the bot is defined or not and a sign-in button on the OAuthCard.</span></span>

![Диалоговое окно "согласие"](../../../assets/images/bots/bots-consent-dialogbox.png)

<span data-ttu-id="72fbd-156">Если элемент Bot определяет кнопку входа, то поток входа для Боты будет срабатывать аналогично потоку входа с помощью кнопки карточки в потоке сообщений.</span><span class="sxs-lookup"><span data-stu-id="72fbd-156">If the bot defines a sign-in button, the sign-in flow for bots will be triggered similarly to the sign-in flow from a card button in a message stream.</span></span> <span data-ttu-id="72fbd-157">Разработчик должен принять решение о том, какие разрешения необходимо запросить у пользователя.</span><span class="sxs-lookup"><span data-stu-id="72fbd-157">It is up to the developer to decide which permissions to ask for the user to consent.</span></span> <span data-ttu-id="72fbd-158">Этот подход рекомендуется в тех случаях, когда вам нужен маркер с разрешениями `openId` , например, если вы хотите обмениваться маркером для ресурсов Graph.</span><span class="sxs-lookup"><span data-stu-id="72fbd-158">This approach is recommended if you need a token with permissions beyond `openId`, for example, if you want to exchange the token for graph resources.</span></span>

<span data-ttu-id="72fbd-159">Если на карточке ленты не предоставляется кнопка входа, она инициирует согласие пользователя на минимальный набор разрешений.</span><span class="sxs-lookup"><span data-stu-id="72fbd-159">If the bot is not providing a sign-in button on the card, it triggers user consent for a minimal set of permissions.</span></span> <span data-ttu-id="72fbd-160">Этот маркер полезен для обычной проверки подлинности и считывания адреса электронной почты пользователя.</span><span class="sxs-lookup"><span data-stu-id="72fbd-160">This token is useful for basic authentication and getting the user email address.</span></span>

<span data-ttu-id="72fbd-161">**Запрос маркера C# без кнопки входа** :</span><span class="sxs-lookup"><span data-stu-id="72fbd-161">**C# token request without a sign-in button** :</span></span>

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

#### <a name="receiving-the-token"></a><span data-ttu-id="72fbd-162">Получение маркера</span><span class="sxs-lookup"><span data-stu-id="72fbd-162">Receiving the token</span></span>

<span data-ttu-id="72fbd-163">Ответ с маркером отправляется через действие Invoke с той же схемой, что и другие вызовы, которые Боты получать сегодня.</span><span class="sxs-lookup"><span data-stu-id="72fbd-163">The response with the token is sent through an invoke activity with the same schema as others invoke activities the bots receive today.</span></span> <span data-ttu-id="72fbd-164">Единственное отличие заключается в том, что имя Invoke, **Sign-in/токенексчанже** и поле **value** , которое будет содержать **идентификатор** (строку) начального запроса для получения маркера, и поле **маркер** (строковое значение, включая маркер).</span><span class="sxs-lookup"><span data-stu-id="72fbd-164">The only difference is the invoke name, **sign-in/tokenExchange** and the **value** field which will contain the **Id** (a string) of the initial request to get the token and the **token** field (a string value including the token).</span></span> <span data-ttu-id="72fbd-165">Обратите внимание, что вы можете получить несколько ответов для данного запроса, если у пользователя есть несколько активных конечных точек.</span><span class="sxs-lookup"><span data-stu-id="72fbd-165">Please note that you might receive multiple responses for a given request if the user has multiple active endpoints.</span></span> <span data-ttu-id="72fbd-166">Вы можете подублировать ответы с маркером.</span><span class="sxs-lookup"><span data-stu-id="72fbd-166">It is up to you to deduplicate the responses with the token.</span></span>

<span data-ttu-id="72fbd-167">**Код C#, реагирующий на обработку действия Invoke** :</span><span class="sxs-lookup"><span data-stu-id="72fbd-167">**C# code to respond to handle the invoke activity** :</span></span>

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

<span data-ttu-id="72fbd-168">`turnContext.activity.value`Тип относится к типу [токенексчанжеинвокерекуест](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true) и содержит маркер, который можно использовать для работы с роботом.</span><span class="sxs-lookup"><span data-stu-id="72fbd-168">The `turnContext.activity.value` is of type [TokenExchangeInvokeRequest](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true) and contains the token that can be further used by your bot.</span></span> <span data-ttu-id="72fbd-169">Безопасное хранение маркеров по соображениям производительности и их обновление.</span><span class="sxs-lookup"><span data-stu-id="72fbd-169">Store the tokens securely for performance reasons and refresh them.</span></span>

### <a name="update-the-azure-portal-with-the-oauth-connection"></a><span data-ttu-id="72fbd-170">Обновление портала Azure с подключением OAuth</span><span class="sxs-lookup"><span data-stu-id="72fbd-170">Update the Azure portal with the OAuth connection</span></span>

1. <span data-ttu-id="72fbd-171">На портале Azure вернитесь к **регистрации каналов ленты**.</span><span class="sxs-lookup"><span data-stu-id="72fbd-171">In the Azure Portal, navigate back to the **Bot Channels Registration**.</span></span>

2. <span data-ttu-id="72fbd-172">Перейдите к колонке **Параметры** и выберите пункт **Добавить параметр** в разделе Параметры подключения OAuth.</span><span class="sxs-lookup"><span data-stu-id="72fbd-172">Switch to the **Settings** blade and choose **Add Setting** under the OAuth Connection Settings section.</span></span>

![Представление SSOBotHandle2](../../../assets/images/bots/bots-vuSSOBotHandle2-settings.png)

3. <span data-ttu-id="72fbd-174">Заполните форму **параметров подключения** .</span><span class="sxs-lookup"><span data-stu-id="72fbd-174">Complete the **Connection Setting** form:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="72fbd-175">Введите имя для нового параметра подключения.</span><span class="sxs-lookup"><span data-stu-id="72fbd-175">Enter a name for your new Connection Setting.</span></span> <span data-ttu-id="72fbd-176">Это имя, которое будет указываться в ссылках внутри параметров кода службы Bot в **действии 5**.</span><span class="sxs-lookup"><span data-stu-id="72fbd-176">This will be the name that gets referenced inside the settings of your bot service code in **step 5**.</span></span>
> * <span data-ttu-id="72fbd-177">В раскрывающемся списке Поставщик услуг выберите **Azure Active Directory v2**.</span><span class="sxs-lookup"><span data-stu-id="72fbd-177">In the Service Provider dropdown, select **Azure Active Directory V2**.</span></span>
>* <span data-ttu-id="72fbd-178">Введите учетные данные клиента для приложения AAD.</span><span class="sxs-lookup"><span data-stu-id="72fbd-178">Enter the client credentials for the AAD application.</span></span>
>* <span data-ttu-id="72fbd-179">Для URL-адреса обмена маркерами используйте значение Scope, определенное на предыдущем шаге приложения AAD.</span><span class="sxs-lookup"><span data-stu-id="72fbd-179">For the Token Exchange URL, use the scope value defined in the previous step of your AAD application.</span></span> <span data-ttu-id="72fbd-180">Присутствие URL-адреса Exchange маркера указывает пакету SDK, что это приложение AAD настроено для единого входа.</span><span class="sxs-lookup"><span data-stu-id="72fbd-180">The presence of the Token Exchange URL is indicating to the SDK that this AAD application is configured for SSO.</span></span>
>* <span data-ttu-id="72fbd-181">Укажите "Common" в качестве **идентификатора клиента**.</span><span class="sxs-lookup"><span data-stu-id="72fbd-181">Specify "common" as the **Tenant ID**.</span></span>
>* <span data-ttu-id="72fbd-182">Добавьте все области, настроенные при указании разрешений на доступ к подчиненным API для приложения AAD.</span><span class="sxs-lookup"><span data-stu-id="72fbd-182">Add all the scopes configured when specifying permissions to downstream APIs for your AAD application.</span></span> <span data-ttu-id="72fbd-183">Если указан идентификатор клиента и секрет клиента, хранилище маркеров будет обмениваться маркером для маркера графа с определенными разрешениями.</span><span class="sxs-lookup"><span data-stu-id="72fbd-183">With the client id and client secret provided, token store will exchange the token for a graph token with defined permissions for you.</span></span>
>* <span data-ttu-id="72fbd-184">Выберите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="72fbd-184">Select **Save**.</span></span>

![Представление параметра Вуссоботконнектион](../../../assets/images/bots/bots-vuSSOBotConnection-settings.png)

### <a name="update-the-auth-sample"></a><span data-ttu-id="72fbd-186">Обновление примера проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="72fbd-186">Update the auth sample</span></span>

<span data-ttu-id="72fbd-187">Начните с [примера проверки подлинности Teams](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth).</span><span class="sxs-lookup"><span data-stu-id="72fbd-187">Start with the [teams auth sample](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth).</span></span>

1. <span data-ttu-id="72fbd-188">Обновите Теамсбот, чтобы включить следующие функции.</span><span class="sxs-lookup"><span data-stu-id="72fbd-188">Update the TeamsBot to include the following.</span></span> <span data-ttu-id="72fbd-189">Чтобы обработать дедупинг входящего запроса, см.</span><span class="sxs-lookup"><span data-stu-id="72fbd-189">To handle the deduping of the incoming request, see below:</span></span>

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
  
2. <span data-ttu-id="72fbd-190">Обновите, `appsettings.json` чтобы включить `botId` , пароль и имя подключения, указанные выше.</span><span class="sxs-lookup"><span data-stu-id="72fbd-190">Update the `appsettings.json` to include the `botId`, password, and the connection name defined above.</span></span>
3. <span data-ttu-id="72fbd-191">Обновите манифест и убедитесь, что `token.botframework.com` он находится в разделе Допустимые домены.</span><span class="sxs-lookup"><span data-stu-id="72fbd-191">Update the manifest and ensure that `token.botframework.com` is in the valid domains section.</span></span>
4. <span data-ttu-id="72fbd-192">Поzip-файл манифеста с изображениями профиля и установите его в Teams.</span><span class="sxs-lookup"><span data-stu-id="72fbd-192">Zip the manifest with the profile images and install it in Teams.</span></span>

#### <a name="additional-code-samples"></a><span data-ttu-id="72fbd-193">Дополнительные примеры кода</span><span class="sxs-lookup"><span data-stu-id="72fbd-193">Additional code samples</span></span>

* <span data-ttu-id="72fbd-194">[Пример кода на языке C# с помощью пакета SDK для Bot Framework](https://microsoft-my.sharepoint-df.com/:u:/p/vul/ETZQfeTViDlCv-frjgTIincB7dvk2HOnma1TLvcoeGGIxg?e=uPq62c).</span><span class="sxs-lookup"><span data-stu-id="72fbd-194">[C# sample using the Bot Framework SDK](https://microsoft-my.sharepoint-df.com/:u:/p/vul/ETZQfeTViDlCv-frjgTIincB7dvk2HOnma1TLvcoeGGIxg?e=uPq62c).</span></span>

* <span data-ttu-id="72fbd-195">[Пример кода на C# с помощью пакета SDK Bot Framework для дедупликации запроса маркера](https://microsoft.sharepoint.com/:u:/t/ExtensibilityandFundamentals/Ea36rUGiN1BGt1RiLOb-mY8BGMF8NwPtronYGym0sCGOTw?e=4bB682).</span><span class="sxs-lookup"><span data-stu-id="72fbd-195">[C# sample using the Bot Framework SDK to deduplicate the token request](https://microsoft.sharepoint.com/:u:/t/ExtensibilityandFundamentals/Ea36rUGiN1BGt1RiLOb-mY8BGMF8NwPtronYGym0sCGOTw?e=4bB682).</span></span>

* [<span data-ttu-id="72fbd-196">Пример кода на языке C# без использования хранилища маркеров пакета SDK Bot Framework</span><span class="sxs-lookup"><span data-stu-id="72fbd-196">C# sample without using the Bot Framework SDK token store</span></span>](https://microsoft-my.sharepoint-df.com/:u:/p/tac/EceKDXrkMn5AuGbh6iGid8ABKEVQ6hkxArxK1y7-M8OVPw)