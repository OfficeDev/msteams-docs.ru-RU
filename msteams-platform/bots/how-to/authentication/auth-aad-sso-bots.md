---
title: Поддержка единого входа для ботов
description: Описывается получение маркера пользователя. В настоящее время для самостоятельного разработчика можно использовать карточку входа или службу Azure Bot с поддержкой карточки OAuth.
keywords: маркер, маркер пользователя, поддержка единого входа для Боты
ms.openlocfilehash: f2f04cefdea874c42961404339f54b8eb581c7ee
ms.sourcegitcommit: aca9990e1f84b07b9e77c08bfeca4440eb4e64f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/25/2020
ms.locfileid: "49409101"
---
# <a name="single-sign-on-sso-support-for-bots"></a><span data-ttu-id="9ec94-105">Поддержка единого входа (SSO) для Боты</span><span class="sxs-lookup"><span data-stu-id="9ec94-105">Single sign-on (SSO) support for bots</span></span>

<span data-ttu-id="9ec94-106">Проверка подлинности с единым входом в Azure Active Directory (Azure AD) сводит к минимуму число попыток ввода учетных данных для входа пользователями, обновляя маркер проверки подлинности без уведомления.</span><span class="sxs-lookup"><span data-stu-id="9ec94-106">Single sign-on authentication in Azure Active Directory (Azure AD) minimizes the number of times users need to enter their login credentials by silently refreshing the authentication token.</span></span> <span data-ttu-id="9ec94-107">Если пользователи согласились использовать ваше приложение, им не нужно будет согласиться на другое устройство и автоматически выполнить вход в систему.</span><span class="sxs-lookup"><span data-stu-id="9ec94-107">If users agrees to use your app, they will not have to consent again on another device and will be signed in automatically.</span></span> <span data-ttu-id="9ec94-108">Этот процесс очень похож на [поддержку единого входа для вкладки Teams]( ../../../tabs/how-to/authentication/auth-aad-sso.md).</span><span class="sxs-lookup"><span data-stu-id="9ec94-108">The flow is very similar to the [Teams tab SSO support]( ../../../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="9ec94-109">Разница — это протокол, который используется для получения маркеров запросов Bot и получения ответов.</span><span class="sxs-lookup"><span data-stu-id="9ec94-109">The difference is the protocol for how a bot requests tokens and receives responses.</span></span>

<span data-ttu-id="9ec94-110">OAuth 2,0 — это открытый стандарт проверки подлинности и авторизации, используемый Azure Active Directory (Azure AD) и многими другими поставщиками удостоверений.</span><span class="sxs-lookup"><span data-stu-id="9ec94-110">OAuth 2.0 is an open standard for authentication and authorization used by Azure Active Directory (Azure AD) and many other identity providers.</span></span> <span data-ttu-id="9ec94-111">Базовое понимание OAuth 2,0 является необходимым условием для работы с проверкой подлинности в Teams.</span><span class="sxs-lookup"><span data-stu-id="9ec94-111">A basic understanding of OAuth 2.0 is a prerequisite for working with authentication in Teams.</span></span>

## <a name="bot-sso-at-runtime"></a><span data-ttu-id="9ec94-112">SSO SSO во время выполнения</span><span class="sxs-lookup"><span data-stu-id="9ec94-112">Bot SSO at runtime</span></span>

![Схема SSO SSO во время выполнения](../../../assets/images/bots/bots-sso-diagram.png)

1. <span data-ttu-id="9ec94-114">Bot отправляет сообщение с Оаускард, которое содержит `tokenExchangeResource` свойство.</span><span class="sxs-lookup"><span data-stu-id="9ec94-114">The bot sends a message with an OAuthCard that contains the `tokenExchangeResource` property.</span></span> <span data-ttu-id="9ec94-115">Он указывает Teams на получение маркера проверки подлинности для приложения Bot.</span><span class="sxs-lookup"><span data-stu-id="9ec94-115">It tells Teams to obtain an authentication token for the bot application.</span></span> <span data-ttu-id="9ec94-116">Пользователь получает сообщения во всех активных конечных точках пользователя.</span><span class="sxs-lookup"><span data-stu-id="9ec94-116">The user receives messages at all the active endpoints of the user.</span></span>

> [!NOTE]
>* <span data-ttu-id="9ec94-117">Пользователь может одновременно иметь более одной активной конечной точки.</span><span class="sxs-lookup"><span data-stu-id="9ec94-117">A user can have more than one active endpoint at a time.</span></span>  
>* <span data-ttu-id="9ec94-118">Маркер Bot получен от каждой активной конечной точки пользователя.</span><span class="sxs-lookup"><span data-stu-id="9ec94-118">The bot token is received from every active endpoint of the user.</span></span>
>* <span data-ttu-id="9ec94-119">В настоящее время для поддержки единого входа приложение должно быть установлено в личной области.</span><span class="sxs-lookup"><span data-stu-id="9ec94-119">Single sign-on support currently requires the app to be installed in personal scope.</span></span>

2. <span data-ttu-id="9ec94-120">Если в первый раз текущий пользователь использует приложение Bot, будет выдаваться запрос на согласие (если требуется согласие) или обрабатывать проверку подлинности (например, двухфакторная проверка подлинности).</span><span class="sxs-lookup"><span data-stu-id="9ec94-120">If it is the first time the current user has used your bot application, there will be a request prompt to consent (if consent is required) or to handle step-up authentication (such as two-factor authentication).</span></span>

3. <span data-ttu-id="9ec94-121">Microsoft Teams запрашивает маркер приложения Bot из конечной точки Azure AD для текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="9ec94-121">Microsoft Teams requests the bot application token from the Azure AD endpoint for the current user.</span></span>

4. <span data-ttu-id="9ec94-122">Azure AD отправляет маркер приложения Bot в приложение Teams.</span><span class="sxs-lookup"><span data-stu-id="9ec94-122">Azure AD sends the bot application token to the Teams application.</span></span>

5. <span data-ttu-id="9ec94-123">Microsoft Teams отправляет маркер участнику Bot как часть объекта value, возвращаемого действием Invoke, с именем Sign-in/Токенексчанже.</span><span class="sxs-lookup"><span data-stu-id="9ec94-123">Microsoft Teams sends the token to the bot as part of the value object returned by the invoke activity with the name sign-in/tokenExchange.</span></span>
  
6. <span data-ttu-id="9ec94-124">Маркер будет проанализирован в приложении Bot для извлечения необходимой информации, например, адреса электронной почты пользователя.</span><span class="sxs-lookup"><span data-stu-id="9ec94-124">The token will be parsed in the bot application to extract the needed information, such as the user's email address.</span></span>
  
## <a name="develop-a-single-sign-on-microsoft-teams-bot"></a><span data-ttu-id="9ec94-125">Разработка ленты единого входа Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="9ec94-125">Develop a Single sign-on Microsoft Teams bot</span></span>
  
<span data-ttu-id="9ec94-126">Следующие действия: необходимы для разработки единого входа Microsoft Teams Bot:</span><span class="sxs-lookup"><span data-stu-id="9ec94-126">The following steps: are required to develop an SSO Microsoft Teams bot:</span></span>

1. [<span data-ttu-id="9ec94-127">Создание бесплатной учетной записи Azure</span><span class="sxs-lookup"><span data-stu-id="9ec94-127">Create an Azure free account</span></span>](#create-an-azure-account)
2. [<span data-ttu-id="9ec94-128">Обновление манифеста приложения Teams</span><span class="sxs-lookup"><span data-stu-id="9ec94-128">Update your Teams app manifest</span></span>](#update-your-app-manifest)
3. [<span data-ttu-id="9ec94-129">Добавление кода для запроса и получения маркера Bot</span><span class="sxs-lookup"><span data-stu-id="9ec94-129">Add the code to request and receive the bot token</span></span>](#request-a-bot-token)

### <a name="create-an-azure-account"></a><span data-ttu-id="9ec94-130">Создание учетной записи Azure</span><span class="sxs-lookup"><span data-stu-id="9ec94-130">Create an Azure account</span></span>

<span data-ttu-id="9ec94-131">Этот шаг аналогичен последующему [входу в табуляцию](../../../tabs/how-to/authentication/auth-aad-sso.md):</span><span class="sxs-lookup"><span data-stu-id="9ec94-131">This step is similar to the [tab SSO flow](../../../tabs/how-to/authentication/auth-aad-sso.md):</span></span>

1. <span data-ttu-id="9ec94-132">Получение [идентификатора приложения Azure AD](/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in) для настольных, Интернет-и мобильных клиентов Teams.</span><span class="sxs-lookup"><span data-stu-id="9ec94-132">Get your [Azure AD Application ID](/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in) for Teams desktop, web, or mobile client.</span></span>
2. <span data-ttu-id="9ec94-133">Укажите разрешения, необходимые вашему приложению для конечной точки Azure AD, и (при необходимости) Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="9ec94-133">Specify the permissions that your application needs for the Azure AD endpoint and, optionally, Microsoft Graph.</span></span>
3. <span data-ttu-id="9ec94-134">[Предоставление разрешений](/azure/active-directory/develop/howto-create-service-principal-portal#configure-access-policies-on-resources) для настольных приложений, веб-приложений и мобильных приложений Teams.</span><span class="sxs-lookup"><span data-stu-id="9ec94-134">[Grant permissions](/azure/active-directory/develop/howto-create-service-principal-portal#configure-access-policies-on-resources) for Teams desktop, web, and mobile applications.</span></span>
4. <span data-ttu-id="9ec94-135">Добавьте клиентское приложение, нажав кнопку **Добавить область** и на открывшейся панели, введите `access_as_user` **имя области**.</span><span class="sxs-lookup"><span data-stu-id="9ec94-135">Add a client app by selecting the **Add a scope** button and in the panel that opens, enter `access_as_user` as the **Scope name**.</span></span>

>[!NOTE]
> <span data-ttu-id="9ec94-136">Область "access_as_user", используемая для добавления клиентского приложения, — "Администраторы и пользователи".</span><span class="sxs-lookup"><span data-stu-id="9ec94-136">The "access_as_user" scope used to add a client app is for "Administrators and users".</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="9ec94-137">Если вы создаете автономную программу Bot, задайте здесь идентификатор URI идентификатора приложения `api://botid-{YourBotId}` , **йоурботид** ссылается на идентификатор приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9ec94-137">If you are building a standalone bot, set the Application ID URI to `api://botid-{YourBotId}` Here, **YourBotId** refers to your Azure AD application ID.</span></span>
> * <span data-ttu-id="9ec94-138">Если вы создаете приложение с помощью ленты и вкладки, задайте для идентификатора URI идентификатор приложения `api://fully-qualified-domain-name.com/botid-{YourBotId}` .</span><span class="sxs-lookup"><span data-stu-id="9ec94-138">If you are building an app with a bot and a tab, set the Application ID URI to `api://fully-qualified-domain-name.com/botid-{YourBotId}`.</span></span>

### <a name="update-your-app-manifest"></a><span data-ttu-id="9ec94-139">Обновление манифеста приложения</span><span class="sxs-lookup"><span data-stu-id="9ec94-139">Update your app manifest</span></span>

<span data-ttu-id="9ec94-140">Добавьте новые свойства в манифест Microsoft teams:</span><span class="sxs-lookup"><span data-stu-id="9ec94-140">Add new properties to your Microsoft Teams manifest:</span></span>

<span data-ttu-id="9ec94-141">**WebApplicationInfo** — родительский элемент следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="9ec94-141">**WebApplicationInfo** - The parent of the following elements:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="9ec94-142">**ID** — идентификатор клиента приложения.</span><span class="sxs-lookup"><span data-stu-id="9ec94-142">**id** - The client ID of the application.</span></span> <span data-ttu-id="9ec94-143">Это идентификатор приложения, полученный в ходе регистрации приложения с помощью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9ec94-143">This is the application ID that you obtained as part of registering the application with Azure AD.</span></span>
>* <span data-ttu-id="9ec94-144">**Resource** — домен и поддомен приложения.</span><span class="sxs-lookup"><span data-stu-id="9ec94-144">**resource** - The domain and subdomain of your application.</span></span> <span data-ttu-id="9ec94-145">Это тот же URI (включая `api://` протокол), который вы зарегистрировали при создании `scope` на шаге 6.</span><span class="sxs-lookup"><span data-stu-id="9ec94-145">This is the same URI (including the `api://` protocol) that you registered when creating your `scope` in step 6 above.</span></span> <span data-ttu-id="9ec94-146">Не следует включать `access_as_user` путь в ресурс.</span><span class="sxs-lookup"><span data-stu-id="9ec94-146">You shouldn't include the `access_as_user` path in your resource.</span></span> <span data-ttu-id="9ec94-147">Доменная часть этого URI должна быть соотнесена с доменом, включая все поддомены, используемые в URL-адресах манифеста приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="9ec94-147">The domain part of this URI should match the domain, including any subdomains, used in the URLs of your Teams application manifest.</span></span>

```json
"webApplicationInfo": {
  "id": "00000000-0000-0000-0000-000000000000",
  "resource": "api://subdomain.example.com/00000000-0000-0000-0000-000000000000"
}
```

### <a name="request-a-bot-token"></a><span data-ttu-id="9ec94-148">Запрос маркера Bot</span><span class="sxs-lookup"><span data-stu-id="9ec94-148">Request a bot token</span></span>

<span data-ttu-id="9ec94-149">Запрос на получение маркера является обычным запросом POST Message (с использованием существующей схемы сообщения).</span><span class="sxs-lookup"><span data-stu-id="9ec94-149">The request to get the token is a normal POST message request (using the existing message schema).</span></span> <span data-ttu-id="9ec94-150">Он включен в вложения объекта Оаускард.</span><span class="sxs-lookup"><span data-stu-id="9ec94-150">It is included in the attachments of an OAuthCard.</span></span> <span data-ttu-id="9ec94-151">Схема для класса Оаускард определена в [схеме Microsoft Bot 4,0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) , и она очень похожа на карточку входа.</span><span class="sxs-lookup"><span data-stu-id="9ec94-151">The schema for the OAuthCard class is defined in [Microsoft Bot Schema 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) and it is very similar to a sign-in card.</span></span> <span data-ttu-id="9ec94-152">Если `TokenExchangeResource` свойство заполнено на карточке, Teams будет обрабатывать этот запрос как необъявляемый токен.</span><span class="sxs-lookup"><span data-stu-id="9ec94-152">Teams will treat this request as a silent token acquisition if the `TokenExchangeResource` property is populated on the card.</span></span> <span data-ttu-id="9ec94-153">Для канала Teams мы соблюдаем только `Id` свойство, которое уникально идентифицирует запрос маркера.</span><span class="sxs-lookup"><span data-stu-id="9ec94-153">For the Teams channel we honor only the `Id` property, which uniquely identifies a token request.</span></span>

>[!NOTE]
> <span data-ttu-id="9ec94-154">`OAuthPrompt` `MultiProviderAuthDialog` Для проверки подлинности с использованием единого входа (Bot) или платформы.</span><span class="sxs-lookup"><span data-stu-id="9ec94-154">The Bot Framework `OAuthPrompt` or the `MultiProviderAuthDialog` is supported for single sign-on (SSO) authentication.</span></span>

<span data-ttu-id="9ec94-155">Если вы впервые используете приложение, а пользователь не дойдет согласие пользователя, в диалоговом окне будет отображаться диалоговое окно, в котором будет выполняться согласие, аналогичный приведенному ниже.</span><span class="sxs-lookup"><span data-stu-id="9ec94-155">If this is the first time the user is using your application and the user consent is required, the user will be shown a dialog to continue with the consent experience similar to the one below.</span></span> <span data-ttu-id="9ec94-156">Когда пользователь выбирает **Continue (продолжить**), выполняются два различных действия в зависимости от того, определен ли Bot или нет, и кнопку входа на оаускард.</span><span class="sxs-lookup"><span data-stu-id="9ec94-156">When the user selects **Continue**, two different things occur depending on whether the bot is defined or not and a sign-in button on the OAuthCard.</span></span>

![Диалоговое окно "согласие"](../../../assets/images/bots/bots-consent-dialogbox.png)

<span data-ttu-id="9ec94-158">Если элемент Bot определяет кнопку входа, то поток входа для Боты будет срабатывать аналогично потоку входа с помощью кнопки карточки в потоке сообщений.</span><span class="sxs-lookup"><span data-stu-id="9ec94-158">If the bot defines a sign-in button, the sign-in flow for bots will be triggered similarly to the sign-in flow from a card button in a message stream.</span></span> <span data-ttu-id="9ec94-159">Разработчик должен принять решение о том, какие разрешения необходимо запросить у пользователя.</span><span class="sxs-lookup"><span data-stu-id="9ec94-159">It is up to the developer to decide which permissions to ask for the user to consent.</span></span> <span data-ttu-id="9ec94-160">Этот подход рекомендуется в тех случаях, когда вам нужен маркер с разрешениями `openId` , например, если вы хотите обмениваться маркером для ресурсов Graph.</span><span class="sxs-lookup"><span data-stu-id="9ec94-160">This approach is recommended if you need a token with permissions beyond `openId`, for example, if you want to exchange the token for graph resources.</span></span>

<span data-ttu-id="9ec94-161">Если на карточке ленты не предоставляется кнопка входа, она инициирует согласие пользователя на минимальный набор разрешений.</span><span class="sxs-lookup"><span data-stu-id="9ec94-161">If the bot is not providing a sign-in button on the card, it triggers user consent for a minimal set of permissions.</span></span> <span data-ttu-id="9ec94-162">Этот маркер полезен для обычной проверки подлинности и считывания адреса электронной почты пользователя.</span><span class="sxs-lookup"><span data-stu-id="9ec94-162">This token is useful for basic authentication and getting the user email address.</span></span>

<span data-ttu-id="9ec94-163">**Запрос маркера C# без кнопки входа**:</span><span class="sxs-lookup"><span data-stu-id="9ec94-163">**C# token request without a sign-in button**:</span></span>

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

#### <a name="receiving-the-token"></a><span data-ttu-id="9ec94-164">Получение маркера</span><span class="sxs-lookup"><span data-stu-id="9ec94-164">Receiving the token</span></span>

<span data-ttu-id="9ec94-165">Ответ с маркером отправляется через действие Invoke с той же схемой, что и другие вызовы, которые Боты получать сегодня.</span><span class="sxs-lookup"><span data-stu-id="9ec94-165">The response with the token is sent through an invoke activity with the same schema as others invoke activities the bots receive today.</span></span> <span data-ttu-id="9ec94-166">Единственное отличие заключается в том, что имя Invoke, **Sign-in/токенексчанже** и поле **value** , которое будет содержать **идентификатор** (строку) начального запроса для получения маркера, и поле **маркер** (строковое значение, включая маркер).</span><span class="sxs-lookup"><span data-stu-id="9ec94-166">The only difference is the invoke name, **sign-in/tokenExchange** and the **value** field which will contain the **Id** (a string) of the initial request to get the token and the **token** field (a string value including the token).</span></span> <span data-ttu-id="9ec94-167">Обратите внимание, что вы можете получить несколько ответов для данного запроса, если у пользователя есть несколько активных конечных точек.</span><span class="sxs-lookup"><span data-stu-id="9ec94-167">Please note that you might receive multiple responses for a given request if the user has multiple active endpoints.</span></span> <span data-ttu-id="9ec94-168">Вы можете подублировать ответы с маркером.</span><span class="sxs-lookup"><span data-stu-id="9ec94-168">It is up to you to deduplicate the responses with the token.</span></span>

<span data-ttu-id="9ec94-169">**Код C#, реагирующий на обработку действия Invoke**:</span><span class="sxs-lookup"><span data-stu-id="9ec94-169">**C# code to respond to handle the invoke activity**:</span></span>

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

<span data-ttu-id="9ec94-170">`turnContext.activity.value`Тип относится к типу [токенексчанжеинвокерекуест](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true) и содержит маркер, который можно использовать для работы с роботом.</span><span class="sxs-lookup"><span data-stu-id="9ec94-170">The `turnContext.activity.value` is of type [TokenExchangeInvokeRequest](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true) and contains the token that can be further used by your bot.</span></span> <span data-ttu-id="9ec94-171">Безопасное хранение маркеров по соображениям производительности и их обновление.</span><span class="sxs-lookup"><span data-stu-id="9ec94-171">Store the tokens securely for performance reasons and refresh them.</span></span>

### <a name="update-the-azure-portal-with-the-oauth-connection"></a><span data-ttu-id="9ec94-172">Обновление портала Azure с подключением OAuth</span><span class="sxs-lookup"><span data-stu-id="9ec94-172">Update the Azure portal with the OAuth connection</span></span>

1. <span data-ttu-id="9ec94-173">На портале Azure вернитесь к **регистрации каналов ленты**.</span><span class="sxs-lookup"><span data-stu-id="9ec94-173">In the Azure Portal, navigate back to the **Bot Channels Registration**.</span></span>

2. <span data-ttu-id="9ec94-174">Перейдите к колонке **Параметры** и выберите пункт **Добавить параметр** в разделе Параметры подключения OAuth.</span><span class="sxs-lookup"><span data-stu-id="9ec94-174">Switch to the **Settings** blade and choose **Add Setting** under the OAuth Connection Settings section.</span></span>

![Представление SSOBotHandle2](../../../assets/images/bots/bots-vuSSOBotHandle2-settings.png)

3. <span data-ttu-id="9ec94-176">Заполните форму **параметров подключения** .</span><span class="sxs-lookup"><span data-stu-id="9ec94-176">Complete the **Connection Setting** form:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="9ec94-177">Введите имя для нового параметра подключения.</span><span class="sxs-lookup"><span data-stu-id="9ec94-177">Enter a name for your new Connection Setting.</span></span> <span data-ttu-id="9ec94-178">Это имя, которое будет указываться в ссылках внутри параметров кода службы Bot в **действии 5**.</span><span class="sxs-lookup"><span data-stu-id="9ec94-178">This will be the name that gets referenced inside the settings of your bot service code in **step 5**.</span></span>
> * <span data-ttu-id="9ec94-179">В раскрывающемся списке Поставщик услуг выберите **Azure Active Directory v2**.</span><span class="sxs-lookup"><span data-stu-id="9ec94-179">In the Service Provider dropdown, select **Azure Active Directory V2**.</span></span>
>* <span data-ttu-id="9ec94-180">Введите учетные данные клиента для приложения AAD.</span><span class="sxs-lookup"><span data-stu-id="9ec94-180">Enter the client credentials for the AAD application.</span></span>

>[!NOTE]
> <span data-ttu-id="9ec94-181">В приложении AAD может потребоваться **неявное предоставление** .</span><span class="sxs-lookup"><span data-stu-id="9ec94-181">**Implicit grant** may be required in the AAD application.</span></span>

>* <span data-ttu-id="9ec94-182">Для URL-адреса обмена маркерами используйте значение Scope, определенное на предыдущем шаге приложения AAD.</span><span class="sxs-lookup"><span data-stu-id="9ec94-182">For the Token Exchange URL, use the scope value defined in the previous step of your AAD application.</span></span> <span data-ttu-id="9ec94-183">Присутствие URL-адреса Exchange маркера указывает пакету SDK, что это приложение AAD настроено для единого входа.</span><span class="sxs-lookup"><span data-stu-id="9ec94-183">The presence of the Token Exchange URL is indicating to the SDK that this AAD application is configured for SSO.</span></span>
>* <span data-ttu-id="9ec94-184">Укажите "Common" в качестве **идентификатора клиента**.</span><span class="sxs-lookup"><span data-stu-id="9ec94-184">Specify "common" as the **Tenant ID**.</span></span>
>* <span data-ttu-id="9ec94-185">Добавьте все области, настроенные при указании разрешений на доступ к подчиненным API для приложения AAD.</span><span class="sxs-lookup"><span data-stu-id="9ec94-185">Add all the scopes configured when specifying permissions to downstream APIs for your AAD application.</span></span> <span data-ttu-id="9ec94-186">Если указан идентификатор клиента и секрет клиента, хранилище маркеров будет обмениваться маркером для маркера графа с определенными разрешениями.</span><span class="sxs-lookup"><span data-stu-id="9ec94-186">With the client id and client secret provided, token store will exchange the token for a graph token with defined permissions for you.</span></span>
>* <span data-ttu-id="9ec94-187">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="9ec94-187">Select **Save**.</span></span>

![Представление параметра Вуссоботконнектион](../../../assets/images/bots/bots-vuSSOBotConnection-settings.png)

### <a name="update-the-auth-sample"></a><span data-ttu-id="9ec94-189">Обновление примера проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="9ec94-189">Update the auth sample</span></span>

<span data-ttu-id="9ec94-190">Начните с [примера проверки подлинности Teams](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth).</span><span class="sxs-lookup"><span data-stu-id="9ec94-190">Start with the [teams auth sample](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth).</span></span>

1. <span data-ttu-id="9ec94-191">Обновите Теамсбот, чтобы включить следующие функции.</span><span class="sxs-lookup"><span data-stu-id="9ec94-191">Update the TeamsBot to include the following.</span></span> <span data-ttu-id="9ec94-192">Чтобы обработать дедупинг входящего запроса, см.</span><span class="sxs-lookup"><span data-stu-id="9ec94-192">To handle the deduping of the incoming request, see below:</span></span>

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
  
2. <span data-ttu-id="9ec94-193">Обновите, `appsettings.json` чтобы включить `botId` , пароль и имя подключения, указанные выше.</span><span class="sxs-lookup"><span data-stu-id="9ec94-193">Update the `appsettings.json` to include the `botId`, password, and the connection name defined above.</span></span>
3. <span data-ttu-id="9ec94-194">Обновите манифест и убедитесь, что `token.botframework.com` он находится в разделе Допустимые домены.</span><span class="sxs-lookup"><span data-stu-id="9ec94-194">Update the manifest and ensure that `token.botframework.com` is in the valid domains section.</span></span>
4. <span data-ttu-id="9ec94-195">Поzip-файл манифеста с изображениями профиля и установите его в Teams.</span><span class="sxs-lookup"><span data-stu-id="9ec94-195">Zip the manifest with the profile images and install it in Teams.</span></span>

#### <a name="additional-code-samples"></a><span data-ttu-id="9ec94-196">Дополнительные примеры кода</span><span class="sxs-lookup"><span data-stu-id="9ec94-196">Additional code samples</span></span>

* <span data-ttu-id="9ec94-197">[Пример кода на языке C# с помощью пакета SDK для Bot Framework](https://microsoft-my.sharepoint-df.com/:u:/p/vul/ETZQfeTViDlCv-frjgTIincB7dvk2HOnma1TLvcoeGGIxg?e=uPq62c).</span><span class="sxs-lookup"><span data-stu-id="9ec94-197">[C# sample using the Bot Framework SDK](https://microsoft-my.sharepoint-df.com/:u:/p/vul/ETZQfeTViDlCv-frjgTIincB7dvk2HOnma1TLvcoeGGIxg?e=uPq62c).</span></span>

* <span data-ttu-id="9ec94-198">[Пример кода на C# с помощью пакета SDK Bot Framework для дедупликации запроса маркера](https://microsoft.sharepoint.com/:u:/t/ExtensibilityandFundamentals/Ea36rUGiN1BGt1RiLOb-mY8BGMF8NwPtronYGym0sCGOTw?e=4bB682).</span><span class="sxs-lookup"><span data-stu-id="9ec94-198">[C# sample using the Bot Framework SDK to deduplicate the token request](https://microsoft.sharepoint.com/:u:/t/ExtensibilityandFundamentals/Ea36rUGiN1BGt1RiLOb-mY8BGMF8NwPtronYGym0sCGOTw?e=4bB682).</span></span>

* [<span data-ttu-id="9ec94-199">Пример кода на языке C# без использования хранилища маркеров пакета SDK Bot Framework</span><span class="sxs-lookup"><span data-stu-id="9ec94-199">C# sample without using the Bot Framework SDK token store</span></span>](https://microsoft-my.sharepoint-df.com/:u:/p/tac/EceKDXrkMn5AuGbh6iGid8ABKEVQ6hkxArxK1y7-M8OVPw)
