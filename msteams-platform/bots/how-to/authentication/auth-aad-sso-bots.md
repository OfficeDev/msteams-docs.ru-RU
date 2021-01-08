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
# <a name="single-sign-on-sso-support-for-bots"></a><span data-ttu-id="478c6-105">Поддержка единого входов (SSO) для ботов</span><span class="sxs-lookup"><span data-stu-id="478c6-105">Single sign-on (SSO) support for bots</span></span>

<span data-ttu-id="478c6-106">Проверка подлинности с единым входом в Azure Active Directory (Azure AD) минимизирует количество случаев, когда пользователям нужно вводить свои учетные данные для входа, автоматически обновив маркер проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="478c6-106">Single sign-on authentication in Azure Active Directory (Azure AD) minimizes the number of times users need to enter their login credentials by silently refreshing the authentication token.</span></span> <span data-ttu-id="478c6-107">Если пользователи соглашаются использовать ваше приложение, им не придется повторно соглашаться на другом устройстве и они будут автоматически входить в нее.</span><span class="sxs-lookup"><span data-stu-id="478c6-107">If users agree to use your app, they will not have to consent again on another device and will be signed in automatically.</span></span> <span data-ttu-id="478c6-108">Поток очень похож на поддержку [SSO вкладки Teams.]( ../../../tabs/how-to/authentication/auth-aad-sso.md)</span><span class="sxs-lookup"><span data-stu-id="478c6-108">The flow is very similar to the [Teams tab SSO support]( ../../../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="478c6-109">Разница заключается в протоколе запроса маркеров и получения ответов ботом.</span><span class="sxs-lookup"><span data-stu-id="478c6-109">The difference is the protocol for how a bot requests tokens and receives responses.</span></span>

<span data-ttu-id="478c6-110">OAuth 2.0 — это открытый стандарт проверки подлинности и авторизации, используемый Azure Active Directory (Azure AD) и многими другими поставщиками удостоверений.</span><span class="sxs-lookup"><span data-stu-id="478c6-110">OAuth 2.0 is an open standard for authentication and authorization used by Azure Active Directory (Azure AD) and many other identity providers.</span></span> <span data-ttu-id="478c6-111">Базовое понимание OAuth 2.0 является необходимым условием для работы с проверкой подлинности в Teams.</span><span class="sxs-lookup"><span data-stu-id="478c6-111">A basic understanding of OAuth 2.0 is a prerequisite for working with authentication in Teams.</span></span>

## <a name="bot-sso-at-runtime"></a><span data-ttu-id="478c6-112">Бот SSO во время работы</span><span class="sxs-lookup"><span data-stu-id="478c6-112">Bot SSO at runtime</span></span>

![Схема SSO бота во время работы](../../../assets/images/bots/bots-sso-diagram.png)

1. <span data-ttu-id="478c6-114">Бот отправляет сообщение со свойством OAuthCard. `tokenExchangeResource`</span><span class="sxs-lookup"><span data-stu-id="478c6-114">The bot sends a message with an OAuthCard that contains the `tokenExchangeResource` property.</span></span> <span data-ttu-id="478c6-115">Он сообщает Teams, что необходимо получить маркер проверки подлинности для приложения-бота.</span><span class="sxs-lookup"><span data-stu-id="478c6-115">It tells Teams to obtain an authentication token for the bot application.</span></span> <span data-ttu-id="478c6-116">Пользователь получает сообщения во всех активных конечных точках пользователя.</span><span class="sxs-lookup"><span data-stu-id="478c6-116">The user receives messages at all the active endpoints of the user.</span></span>

    > [!NOTE]
    >* <span data-ttu-id="478c6-117">Пользователь может одновременно иметь несколько активных конечных точек.</span><span class="sxs-lookup"><span data-stu-id="478c6-117">A user can have more than one active endpoint at a time.</span></span>  
    >* <span data-ttu-id="478c6-118">Маркер бота получается от каждой активной конечной точки пользователя.</span><span class="sxs-lookup"><span data-stu-id="478c6-118">The bot token is received from every active endpoint of the user.</span></span>
    >* <span data-ttu-id="478c6-119">В настоящее время для поддержки единого входов требуется, чтобы приложение было установлено в личной области.</span><span class="sxs-lookup"><span data-stu-id="478c6-119">Single sign-on support currently requires the app to be installed in personal scope.</span></span>

2. <span data-ttu-id="478c6-120">Если текущий пользователь впервые использовал ваше приложение-бот, будет предложено согласиться (если требуется согласие) или обработать пошаговую проверку подлинности (например, двух-факторную проверку подлинности).</span><span class="sxs-lookup"><span data-stu-id="478c6-120">If it is the first time the current user has used your bot application, there will be a request prompt to consent (if consent is required) or to handle step-up authentication (such as two-factor authentication).</span></span>

3. <span data-ttu-id="478c6-121">Microsoft Teams запрашивает маркер приложения-бота из конечной точки Azure AD для текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="478c6-121">Microsoft Teams requests the bot application token from the Azure AD endpoint for the current user.</span></span>

4. <span data-ttu-id="478c6-122">Azure AD отправляет маркер приложения-бота в приложение Teams.</span><span class="sxs-lookup"><span data-stu-id="478c6-122">Azure AD sends the bot application token to the Teams application.</span></span>

5. <span data-ttu-id="478c6-123">Microsoft Teams отправляет маркер боту как часть объекта значения, возвращаемого действием вызова с именем sign-in/tokenExchange.</span><span class="sxs-lookup"><span data-stu-id="478c6-123">Microsoft Teams sends the token to the bot as part of the value object returned by the invoke activity with the name sign-in/tokenExchange.</span></span>
  
6. <span data-ttu-id="478c6-124">Маркер будет разлиться в бот-приложении для извлечения необходимых сведений, например адреса электронной почты пользователя.</span><span class="sxs-lookup"><span data-stu-id="478c6-124">The token will be parsed in the bot application to extract the needed information, such as the user's email address.</span></span>
  
## <a name="develop-a-single-sign-on-microsoft-teams-bot"></a><span data-ttu-id="478c6-125">Разработка бота единого вход в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="478c6-125">Develop a Single sign-on Microsoft Teams bot</span></span>
  
<span data-ttu-id="478c6-126">Для разработки бота Microsoft Teams с SSO необходимо сделать следующее:</span><span class="sxs-lookup"><span data-stu-id="478c6-126">The following steps are required to develop an SSO Microsoft Teams bot:</span></span>

1. [<span data-ttu-id="478c6-127">Создание бесплатной учетной записи Azure</span><span class="sxs-lookup"><span data-stu-id="478c6-127">Create an Azure free account</span></span>](#create-an-azure-account)
2. [<span data-ttu-id="478c6-128">Обновление манифеста приложения Teams</span><span class="sxs-lookup"><span data-stu-id="478c6-128">Update your Teams app manifest</span></span>](#update-your-app-manifest)
3. [<span data-ttu-id="478c6-129">Добавление кода для запроса и получения маркера бота</span><span class="sxs-lookup"><span data-stu-id="478c6-129">Add the code to request and receive the bot token</span></span>](#request-a-bot-token)

### <a name="create-an-azure-account"></a><span data-ttu-id="478c6-130">Создание учетной записи Azure</span><span class="sxs-lookup"><span data-stu-id="478c6-130">Create an Azure account</span></span>

<span data-ttu-id="478c6-131">Этот шаг похож на поток [SSO табули:](../../../tabs/how-to/authentication/auth-aad-sso.md)</span><span class="sxs-lookup"><span data-stu-id="478c6-131">This step is similar to the [tab SSO flow](../../../tabs/how-to/authentication/auth-aad-sso.md):</span></span>

1. <span data-ttu-id="478c6-132">Получите свой [ИД приложения Azure AD](/graph/concepts/auth-register-app-v2) для настольного, веб-клиента Или мобильного клиента Teams.</span><span class="sxs-lookup"><span data-stu-id="478c6-132">Get your [Azure AD Application ID](/graph/concepts/auth-register-app-v2) for Teams desktop, web, or mobile client.</span></span>
2. <span data-ttu-id="478c6-133">Укажите разрешения, необходимые приложению для конечной точки Azure AD и,при желании, Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="478c6-133">Specify the permissions that your application needs for the Azure AD endpoint and, optionally, Microsoft Graph.</span></span>
3. <span data-ttu-id="478c6-134">[Предоставление разрешений для](/azure/active-directory/develop/v2-permissions-and-consent) классических, веб-и мобильных приложений Teams.</span><span class="sxs-lookup"><span data-stu-id="478c6-134">[Grant permissions](/azure/active-directory/develop/v2-permissions-and-consent) for Teams desktop, web, and mobile applications.</span></span>
4. <span data-ttu-id="478c6-135">Выберите **"Добавить область".**</span><span class="sxs-lookup"><span data-stu-id="478c6-135">Select **Add a scope**.</span></span>
5. <span data-ttu-id="478c6-136">На открываемой панели добавьте клиентские приложения, введите `access_as_user` имя **области.**</span><span class="sxs-lookup"><span data-stu-id="478c6-136">In the panel that opens, add a client app by entering `access_as_user` as the **Scope name**.</span></span>

    >[!NOTE]
    > <span data-ttu-id="478c6-137">Область "access_as_user", используемая для добавления клиентского приложения, — "Администраторы и пользователи".</span><span class="sxs-lookup"><span data-stu-id="478c6-137">The "access_as_user" scope used to add a client app is for "Administrators and users".</span></span>

    > [!IMPORTANT]
    > * <span data-ttu-id="478c6-138">Если вы строите автономный бот, задайте для URI ИД приложения URI `api://botid-{YourBotId}` здесь, **ВашBotId** ссылается на ваш ИД приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="478c6-138">If you are building a standalone bot, set the Application ID URI to `api://botid-{YourBotId}` Here, **YourBotId** refers to your Azure AD application ID.</span></span>
    > * <span data-ttu-id="478c6-139">Если вы строите приложение с помощью бота и вкладки, установите для URI ИД приложения задав `api://fully-qualified-domain-name.com/botid-{YourBotId}` его.</span><span class="sxs-lookup"><span data-stu-id="478c6-139">If you are building an app with a bot and a tab, set the Application ID URI to `api://fully-qualified-domain-name.com/botid-{YourBotId}`.</span></span>

### <a name="update-your-app-manifest"></a><span data-ttu-id="478c6-140">Обновление манифеста приложения</span><span class="sxs-lookup"><span data-stu-id="478c6-140">Update your app manifest</span></span>

<span data-ttu-id="478c6-141">Добавьте новые свойства в манифест Microsoft Teams:</span><span class="sxs-lookup"><span data-stu-id="478c6-141">Add new properties to your Microsoft Teams manifest:</span></span>

<span data-ttu-id="478c6-142">**WebApplicationInfo —** родительский элемент следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="478c6-142">**WebApplicationInfo** - The parent of the following elements:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="478c6-143">**id** — ИД клиента приложения.</span><span class="sxs-lookup"><span data-stu-id="478c6-143">**id** - The client ID of the application.</span></span> <span data-ttu-id="478c6-144">Это ИД приложения, полученный при регистрации приложения в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="478c6-144">This is the application ID that you obtained as part of registering the application with Azure AD.</span></span>
>* <span data-ttu-id="478c6-145">**resource** — домен и поддомен приложения.</span><span class="sxs-lookup"><span data-stu-id="478c6-145">**resource** - The domain and subdomain of your application.</span></span> <span data-ttu-id="478c6-146">Это тот же URI (включая протокол), который вы зарегистрировали при создании на `api://` `scope` шаге 6 выше.</span><span class="sxs-lookup"><span data-stu-id="478c6-146">This is the same URI (including the `api://` protocol) that you registered when creating your `scope` in step 6 above.</span></span> <span data-ttu-id="478c6-147">Не следует включать путь `access_as_user` в ресурс.</span><span class="sxs-lookup"><span data-stu-id="478c6-147">You shouldn't include the `access_as_user` path in your resource.</span></span> <span data-ttu-id="478c6-148">Доменная часть этого URI должна соответствовать домену, в том числе поддоменам, используемым в URL-адресах манифеста приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="478c6-148">The domain part of this URI should match the domain, including any subdomains, used in the URLs of your Teams application manifest.</span></span>

```json
"webApplicationInfo": {
  "id": "00000000-0000-0000-0000-000000000000",
  "resource": "api://subdomain.example.com/00000000-0000-0000-0000-000000000000"
}
```

### <a name="request-a-bot-token"></a><span data-ttu-id="478c6-149">Запрос маркера бота</span><span class="sxs-lookup"><span data-stu-id="478c6-149">Request a bot token</span></span>

<span data-ttu-id="478c6-150">Запрос на получения маркера является обычным запросом post сообщения (с использованием существующей схемы сообщения).</span><span class="sxs-lookup"><span data-stu-id="478c6-150">The request to get the token is a normal POST message request (using the existing message schema).</span></span> <span data-ttu-id="478c6-151">Он включается во вложения OAuthCard.</span><span class="sxs-lookup"><span data-stu-id="478c6-151">It is included in the attachments of an OAuthCard.</span></span> <span data-ttu-id="478c6-152">Схема для класса OAuthCard определена в [microsoft Bot Schema 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) и очень похожа на карточку для входов.</span><span class="sxs-lookup"><span data-stu-id="478c6-152">The schema for the OAuthCard class is defined in [Microsoft Bot Schema 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) and it is very similar to a sign-in card.</span></span> <span data-ttu-id="478c6-153">Teams будет рассматривать этот запрос как получение маркера в тихом режиме, если свойство заполнено `TokenExchangeResource` на карточке.</span><span class="sxs-lookup"><span data-stu-id="478c6-153">Teams will treat this request as a silent token acquisition if the `TokenExchangeResource` property is populated on the card.</span></span> <span data-ttu-id="478c6-154">Для канала Teams мы считаем только свойство, которое уникальным образом идентифицирует `Id` запрос маркера.</span><span class="sxs-lookup"><span data-stu-id="478c6-154">For the Teams channel, we honor only the `Id` property, which uniquely identifies a token request.</span></span>

>[!NOTE]
> <span data-ttu-id="478c6-155">Bot Framework или поддерживается для проверки подлинности с единым `OAuthPrompt` `MultiProviderAuthDialog` входом.</span><span class="sxs-lookup"><span data-stu-id="478c6-155">The Bot Framework `OAuthPrompt` or the `MultiProviderAuthDialog` is supported for single sign-on (SSO) authentication.</span></span>

<span data-ttu-id="478c6-156">Если это первый раз, когда пользователь использует ваше приложение и требуется согласие пользователя, пользователю будет показано диалоговое окно для продолжения работы с согласием, аналогичное приведенному ниже.</span><span class="sxs-lookup"><span data-stu-id="478c6-156">If this is the first time the user is using your application and the user consent is required, the user will be shown a dialog to continue with the consent experience similar to the one below.</span></span> <span data-ttu-id="478c6-157">Когда пользователь выбирает **"Продолжить",** в зависимости от того, определен бот или нет, и кнопки для входов в OAuthCard происходят две разные вещи.</span><span class="sxs-lookup"><span data-stu-id="478c6-157">When the user selects **Continue**, two different things occur depending on whether the bot is defined or not and a sign-in button on the OAuthCard.</span></span>

![Диалоговое окно "Согласие"](../../../assets/images/bots/bots-consent-dialogbox.png)

<span data-ttu-id="478c6-159">Если бот определяет кнопку для входов, поток входов для ботов будет активен аналогично потоку входов с кнопки карточки в потоке сообщений.</span><span class="sxs-lookup"><span data-stu-id="478c6-159">If the bot defines a sign-in button, the sign-in flow for bots will be triggered similarly to the sign-in flow from a card button in a message stream.</span></span> <span data-ttu-id="478c6-160">Разработчик решает, какие разрешения нужно запросить у пользователя.</span><span class="sxs-lookup"><span data-stu-id="478c6-160">It is up to the developer to decide which permissions to ask for the user to consent.</span></span> <span data-ttu-id="478c6-161">Этот подход рекомендуется, если вам нужен маркер с разрешениями за пределами , например, если вы хотите обменять маркер для `openId` ресурсов graph.</span><span class="sxs-lookup"><span data-stu-id="478c6-161">This approach is recommended if you need a token with permissions beyond `openId`, for example, if you want to exchange the token for graph resources.</span></span>

<span data-ttu-id="478c6-162">Если бот не предоставляет кнопку для регистрации на карточке, он инициирует согласие пользователя на минимальный набор разрешений.</span><span class="sxs-lookup"><span data-stu-id="478c6-162">If the bot is not providing a sign-in button on the card, it triggers user consent for a minimal set of permissions.</span></span> <span data-ttu-id="478c6-163">Этот маркер полезен для базовой проверки подлинности и получения адреса электронной почты пользователя.</span><span class="sxs-lookup"><span data-stu-id="478c6-163">This token is useful for basic authentication and getting the user's email address.</span></span>

<span data-ttu-id="478c6-164">**Запрос маркера C# без кнопки для регистрации:**</span><span class="sxs-lookup"><span data-stu-id="478c6-164">**C# token request without a sign-in button**:</span></span>

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

#### <a name="receiving-the-token"></a><span data-ttu-id="478c6-165">Получение маркера</span><span class="sxs-lookup"><span data-stu-id="478c6-165">Receiving the token</span></span>

<span data-ttu-id="478c6-166">Ответ с маркером отправляется с помощью действия вызова с той же схемой, что и другие, вызываемой действиями, которые боты получают сегодня.</span><span class="sxs-lookup"><span data-stu-id="478c6-166">The response with the token is sent through an invoke activity with the same schema as others invoke activities the bots receive today.</span></span> <span data-ttu-id="478c6-167">Единственное отличие состоит в имени вызова,  входе/маркереExchange и поле значения, которое будет содержать ИД (строку) исходного запроса для получения маркера и поля маркера (строка, включаемая маркер).   </span><span class="sxs-lookup"><span data-stu-id="478c6-167">The only difference is the invoke name, **sign-in/tokenExchange** and the **value** field which will contain the **Id** (a string) of the initial request to get the token and the **token** field (a string value including the token).</span></span> <span data-ttu-id="478c6-168">Обратите внимание, что вы можете получить несколько ответов на заданный запрос, если у пользователя несколько активных конечных точек.</span><span class="sxs-lookup"><span data-stu-id="478c6-168">Please note that you might receive multiple responses for a given request if the user has multiple active endpoints.</span></span> <span data-ttu-id="478c6-169">Вы можете отреагировать на ответы с помощью маркера.</span><span class="sxs-lookup"><span data-stu-id="478c6-169">It is up to you to deduplicate the responses with the token.</span></span>

<span data-ttu-id="478c6-170">**Код C#, реагируя на обработку действия вызова:**</span><span class="sxs-lookup"><span data-stu-id="478c6-170">**C# code to respond to handle the invoke activity**:</span></span>

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

<span data-ttu-id="478c6-171">Тип `turnContext.activity.value` [TokenExchangeInvokeRequest](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true) содержит маркер, который может дополнительно использоваться ботом.</span><span class="sxs-lookup"><span data-stu-id="478c6-171">The `turnContext.activity.value` is of type [TokenExchangeInvokeRequest](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true) and contains the token that can be further used by your bot.</span></span> <span data-ttu-id="478c6-172">Храните маркеры безопасно из соображений производительности и обновляйте их.</span><span class="sxs-lookup"><span data-stu-id="478c6-172">Store the tokens securely for performance reasons and refresh them.</span></span>

### <a name="update-the-azure-portal-with-the-oauth-connection"></a><span data-ttu-id="478c6-173">Обновление портала Azure с помощью подключения OAuth</span><span class="sxs-lookup"><span data-stu-id="478c6-173">Update the Azure portal with the OAuth connection</span></span>

1. <span data-ttu-id="478c6-174">На портале Azure перейдите к регистрации каналов **ботов.**</span><span class="sxs-lookup"><span data-stu-id="478c6-174">In the Azure Portal, navigate back to the **Bot Channels Registration**.</span></span>

2. <span data-ttu-id="478c6-175">Переключение в **раздел "Параметры"** и выберите **"Добавить параметр"** в разделе "Параметры подключения OAuth".</span><span class="sxs-lookup"><span data-stu-id="478c6-175">Switch to the **Settings** blade and choose **Add Setting** under the OAuth Connection Settings section.</span></span>

    ![Представление SSOBotHandle2](../../../assets/images/bots/bots-vuSSOBotHandle2-settings.png)

3. <span data-ttu-id="478c6-177">**Заполнять форму параметра** подключения:</span><span class="sxs-lookup"><span data-stu-id="478c6-177">Complete the **Connection Setting** form:</span></span>

    > [!div class="checklist"]
    >
    > * <span data-ttu-id="478c6-178">Введите имя нового параметра подключения.</span><span class="sxs-lookup"><span data-stu-id="478c6-178">Enter a name for your new Connection Setting.</span></span> <span data-ttu-id="478c6-179">Это имя, на которое будет ссылаться код службы ботов на **шаге 5.**</span><span class="sxs-lookup"><span data-stu-id="478c6-179">This will be the name that gets referenced inside the settings of your bot service code in **step 5**.</span></span>
    > * <span data-ttu-id="478c6-180">В выпадаемом каталоге "Поставщик услуг" выберите **Azure Active Directory V2.**</span><span class="sxs-lookup"><span data-stu-id="478c6-180">In the Service Provider dropdown, select **Azure Active Directory V2**.</span></span>
    >* <span data-ttu-id="478c6-181">Введите учетные данные клиента для приложения AAD.</span><span class="sxs-lookup"><span data-stu-id="478c6-181">Enter the client credentials for the AAD application.</span></span>

    >[!NOTE]
    > <span data-ttu-id="478c6-182">**В приложении** AAD может потребоваться неявное предоставление.</span><span class="sxs-lookup"><span data-stu-id="478c6-182">**Implicit grant** may be required in the AAD application.</span></span>

    >* <span data-ttu-id="478c6-183">Для URL-адреса Exchange маркера используйте значение области, определенное на предыдущем шаге приложения AAD.</span><span class="sxs-lookup"><span data-stu-id="478c6-183">For the Token Exchange URL, use the scope value defined in the previous step of your AAD application.</span></span> <span data-ttu-id="478c6-184">Наличие URL-адреса Exchange маркера указывает SDK, что это приложение AAD настроено для SSO.</span><span class="sxs-lookup"><span data-stu-id="478c6-184">The presence of the Token Exchange URL is indicating to the SDK that this AAD application is configured for SSO.</span></span>
    >* <span data-ttu-id="478c6-185">Укажите "common" в **качестве ИД клиента.**</span><span class="sxs-lookup"><span data-stu-id="478c6-185">Specify "common" as the **Tenant ID**.</span></span>
    >* <span data-ttu-id="478c6-186">Добавьте все области, настроенные при указании разрешений для нисходящего API для приложения AAD.</span><span class="sxs-lookup"><span data-stu-id="478c6-186">Add all the scopes configured when specifying permissions to downstream APIs for your AAD application.</span></span> <span data-ttu-id="478c6-187">Если у вас есть ИД клиента и секрет клиента, хранилище маркеров будет обмениваться маркером на маркер графа с определенными разрешениями.</span><span class="sxs-lookup"><span data-stu-id="478c6-187">With the client id and client secret provided, the token store will exchange the token for a graph token with defined permissions for you.</span></span>
    >* <span data-ttu-id="478c6-188">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="478c6-188">Select **Save**.</span></span>

    ![Представление Параметров VuSSOBotConnection](../../../assets/images/bots/bots-vuSSOBotConnection-settings.png)

### <a name="update-the-auth-sample"></a><span data-ttu-id="478c6-190">Обновление примера auth</span><span class="sxs-lookup"><span data-stu-id="478c6-190">Update the auth sample</span></span>

<span data-ttu-id="478c6-191">Начните с примера [auth teams](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth).</span><span class="sxs-lookup"><span data-stu-id="478c6-191">Start with the [teams auth sample](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth).</span></span>

1. <span data-ttu-id="478c6-192">Обновив TeamsBot, включив в него следующее.</span><span class="sxs-lookup"><span data-stu-id="478c6-192">Update the TeamsBot to include the following.</span></span> <span data-ttu-id="478c6-193">Чтобы обработать deduping входящих запросов, см. ниже:</span><span class="sxs-lookup"><span data-stu-id="478c6-193">To handle the deduping of the incoming request, see below:</span></span>

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
  
2. <span data-ttu-id="478c6-194">`appsettings.json`Обновим имя, чтобы включить `botId` пароль и имя подключения, определенное выше.</span><span class="sxs-lookup"><span data-stu-id="478c6-194">Update the `appsettings.json` to include the `botId`, password, and the connection name defined above.</span></span>
3. <span data-ttu-id="478c6-195">Обновим манифест и `token.botframework.com` убедитесь, что он находится в разделе "Допустимые домены".</span><span class="sxs-lookup"><span data-stu-id="478c6-195">Update the manifest and ensure that `token.botframework.com` is in the valid domains section.</span></span>
4. <span data-ttu-id="478c6-196">Замейте манифест изображениями профилей и установите его в Teams.</span><span class="sxs-lookup"><span data-stu-id="478c6-196">Zip the manifest with the profile images and install it in Teams.</span></span>

#### <a name="additional-code-samples"></a><span data-ttu-id="478c6-197">Дополнительные примеры кода</span><span class="sxs-lookup"><span data-stu-id="478c6-197">Additional code samples</span></span>

* <span data-ttu-id="478c6-198">[Пример C# с использованием bot Framework SDK.](https://github.com/microsoft/BotBuilder-Samples/tree/main/experimental/teams-sso/csharp_dotnetcore)</span><span class="sxs-lookup"><span data-stu-id="478c6-198">[C# sample using the Bot Framework SDK](https://github.com/microsoft/BotBuilder-Samples/tree/main/experimental/teams-sso/csharp_dotnetcore).</span></span>

* <span data-ttu-id="478c6-199">[Пример C# с помощью SDK Bot Framework для дедипликации запроса маркера.](https://microsoft.sharepoint.com/:u:/t/ExtensibilityandFundamentals/Ea36rUGiN1BGt1RiLOb-mY8BGMF8NwPtronYGym0sCGOTw?e=4bB682)</span><span class="sxs-lookup"><span data-stu-id="478c6-199">[C# sample using the Bot Framework SDK to deduplicate the token request](https://microsoft.sharepoint.com/:u:/t/ExtensibilityandFundamentals/Ea36rUGiN1BGt1RiLOb-mY8BGMF8NwPtronYGym0sCGOTw?e=4bB682).</span></span>

* <span data-ttu-id="478c6-200">Пример на C# без использования магазина маркеров [SDK Bot Framework.](https://microsoft-my.sharepoint-df.com/:u:/p/tac/EceKDXrkMn5AuGbh6iGid8ABKEVQ6hkxArxK1y7-M8OVPw)</span><span class="sxs-lookup"><span data-stu-id="478c6-200">[C# sample without using the Bot Framework SDK token store](https://microsoft-my.sharepoint-df.com/:u:/p/tac/EceKDXrkMn5AuGbh6iGid8ABKEVQ6hkxArxK1y7-M8OVPw).</span></span>
