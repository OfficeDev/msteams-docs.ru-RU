---
title: Использование службы Azure Bot для проверки подлинности в Teams
description: Описывает OAuthCard службы Azure Bot и ее использование для проверки подлинности
ms.topic: conceptual
localization_priority: Normal
keywords: группы проверки подлинности OAuthCard OAuth card Azure Bot Service
ms.openlocfilehash: 3d0df4f04625c5be3468d12319b54096ae06de90
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020683"
---
# <a name="using-azure-bot-service-for-authentication-in-teams"></a><span data-ttu-id="537e1-104">Использование службы Azure Bot для проверки подлинности в Teams</span><span class="sxs-lookup"><span data-stu-id="537e1-104">Using Azure Bot Service for Authentication in Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="537e1-105">Без OAuthCard службы microsoft Bot службы Azure сложно реализовать проверку подлинности в боте.</span><span class="sxs-lookup"><span data-stu-id="537e1-105">Without the Azure Bot Service’s OAuthCard it is complicated to implement authentication in a bot.</span></span> <span data-ttu-id="537e1-106">Это задача полного стека, связанная с созданием веб-опыта, интеграцией с внешними поставщиками OAuth, управлением маркерами и обработкой вызовов API между серверами и серверами для безопасного завершения потока проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="537e1-106">It is a full-stack challenge that involving building a web experience, integrating with external OAuth providers, token management, and handling the right server-to-server API calls to complete authentication flow securely.</span></span> <span data-ttu-id="537e1-107">Это может привести к неуклюжим опытом, требующим ввода "магических чисел".</span><span class="sxs-lookup"><span data-stu-id="537e1-107">This can result in clunky experiences requiring the entry of “magic numbers”.</span></span>

<span data-ttu-id="537e1-108">С помощью OAuthCard службы ботов Azure для вашего Teams-бота проще войти в пользователей и получить доступ к внешним поставщикам данных.</span><span class="sxs-lookup"><span data-stu-id="537e1-108">With Azure Bot Service’s OAuthCard, it is easier for your Teams bot to sign in your users and access external data providers.</span></span> <span data-ttu-id="537e1-109">Если вы уже внедрили auth и хотите перейти на что-то более простое, или если вы хотите добавить проверку подлинности в службу ботов впервые, OAuthCard может упростить ее.</span><span class="sxs-lookup"><span data-stu-id="537e1-109">Whether you’ve already implemented auth and you want to switch over to something simpler, or if you are looking to add authentication to your bot service for the first time, the OAuthCard can make it easier.</span></span>

<span data-ttu-id="537e1-110">Другие темы в проверке подлинности описывают проверку подлинности без использования OAuthCard, поэтому если вы хотите более глубоко разобраться в проверке подлинности в Teams или иметь ситуацию, в которой нельзя использовать OAuthCard, вы все равно можете ссылаться на эти темы. [](~/resources/bot-v3/bot-authentication/auth-flow-bot.md)</span><span class="sxs-lookup"><span data-stu-id="537e1-110">Other topics in [Authentication](~/resources/bot-v3/bot-authentication/auth-flow-bot.md) describe authentication without using the OAuthCard, so if you want to understand authentication in Teams more deeply, or have a situation where you can not use the OAuthCard, you can still refer to those topics.</span></span>

## <a name="support-for-the-oauthcard"></a><span data-ttu-id="537e1-111">Поддержка OAuthCard</span><span class="sxs-lookup"><span data-stu-id="537e1-111">Support for the OAuthCard</span></span>

<span data-ttu-id="537e1-112">В настоящее время существует ряд ограничений на использование OAuthCard.</span><span class="sxs-lookup"><span data-stu-id="537e1-112">There are currently some restrictions to where you can use the OAuthCard.</span></span> <span data-ttu-id="537e1-113">Они включают:</span><span class="sxs-lookup"><span data-stu-id="537e1-113">These include:</span></span>

* <span data-ttu-id="537e1-114">Карта не будет работать с [гостевим доступом](/MicrosoftTeams/guest-access)</span><span class="sxs-lookup"><span data-stu-id="537e1-114">The card will not work with [guest access](/MicrosoftTeams/guest-access)</span></span>
* <span data-ttu-id="537e1-115">Он не будет работать с [Microsoft Teams бесплатно](https://products.office.com/microsoft-teams/free)</span><span class="sxs-lookup"><span data-stu-id="537e1-115">It will not work with [Microsoft Teams free](https://products.office.com/microsoft-teams/free)</span></span>
* <span data-ttu-id="537e1-116">Его можно использовать только для проверки подлинности ботов</span><span class="sxs-lookup"><span data-stu-id="537e1-116">It can only be used for bot authentication</span></span>
* <span data-ttu-id="537e1-117">Он работает только для ботов, зарегистрированных в [службе Azure Bot](https://azure.microsoft.com/services/bot-service/)</span><span class="sxs-lookup"><span data-stu-id="537e1-117">It only works for bots registered in the [Azure Bot Service](https://azure.microsoft.com/services/bot-service/)</span></span>

## <a name="how-does-the-azure-bot-service-help-me-do-authentication"></a><span data-ttu-id="537e1-118">Как служба Azure Bot помогает мне делать проверку подлинности?</span><span class="sxs-lookup"><span data-stu-id="537e1-118">How does the Azure Bot Service help me do authentication?</span></span>

<span data-ttu-id="537e1-119">Полная документация с помощью OAuthCard доступна в разделе: Добавление проверки подлинности в бот [через службу Azure Bot.](/azure/bot-service/bot-builder-tutorial-authentication?view=azure-bot-service-3.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="537e1-119">Full documentation using the OAuthCard is available in the topic: [Add authentication to your bot via Azure Bot Service](/azure/bot-service/bot-builder-tutorial-authentication?view=azure-bot-service-3.0&preserve-view=true).</span></span> <span data-ttu-id="537e1-120">Обратите внимание, что эта тема находится в наборе документации Azure Bot Framework и не является конкретной для Teams.</span><span class="sxs-lookup"><span data-stu-id="537e1-120">Note that this topic is in the Azure Bot Framework documentation set, and is not specific to Teams.</span></span>

<span data-ttu-id="537e1-121">В следующих разделах повеяно, как использовать OAuthCard в Teams.</span><span class="sxs-lookup"><span data-stu-id="537e1-121">The following sections tell how to use the OAuthCard in Teams.</span></span>

## <a name="main-benefits-for-teams-developers"></a><span data-ttu-id="537e1-122">Основные преимущества для Teams разработчиков</span><span class="sxs-lookup"><span data-stu-id="537e1-122">Main benefits for Teams developers</span></span>

<span data-ttu-id="537e1-123">OAuthCard помогает с проверкой подлинности следующими способами:</span><span class="sxs-lookup"><span data-stu-id="537e1-123">The OAuthCard helps with authentication in the following ways:</span></span>

* <span data-ttu-id="537e1-124">Обеспечивает поток веб-проверки подлинности на основе интернета: вам больше не нужно писать и хост-страницу, чтобы направлять внешние опытом входа или предоставлять перенаправление.</span><span class="sxs-lookup"><span data-stu-id="537e1-124">Provides an out-of-box web-based authentication flow: you no longer have to write and host a web page to direct to external login experiences or provide a redirect.</span></span>
* <span data-ttu-id="537e1-125">Является бесшовным для конечных пользователей: выполните полный вход в опытом прямо в Teams.</span><span class="sxs-lookup"><span data-stu-id="537e1-125">Is seamless for end users: complete the full sign in experience right within Teams.</span></span>
* <span data-ttu-id="537e1-126">Включает простой процесс управления маркерами: вам больше не нужно внедрять систему хранения маркеров, вместо этого служба ботов заботится о кэширования маркеров и предоставляет безопасный механизм для получения этих маркеров.</span><span class="sxs-lookup"><span data-stu-id="537e1-126">Includes easy token management: you no longer have to implement a token storage system – instead, the Bot Service takes care of token caching and provides a secure mechanism for fetching those tokens.</span></span>
* <span data-ttu-id="537e1-127">Поддерживается полными SDKs: легко интегрировать и потреблять из бот-службы.</span><span class="sxs-lookup"><span data-stu-id="537e1-127">Is supported by complete SDKs: easy to integrate and consume from your bot service.</span></span>
* <span data-ttu-id="537e1-128">Поддерживает множество популярных поставщиков OAuth, таких как Azure AD/MSA, Facebook и Google.</span><span class="sxs-lookup"><span data-stu-id="537e1-128">Has out-of-box support for many popular OAuth providers, such as Azure AD/MSA, Facebook, and Google.</span></span>

## <a name="when-should-i-implement-my-own-solution"></a><span data-ttu-id="537e1-129">Когда следует реализовать собственное решение?</span><span class="sxs-lookup"><span data-stu-id="537e1-129">When should I implement my own solution?</span></span>

<span data-ttu-id="537e1-130">Так как маркеры доступа являются конфиденциальной информацией, вы можете не хранить их во внешней службе.</span><span class="sxs-lookup"><span data-stu-id="537e1-130">Because access tokens are sensitive information, you may not wish to have them stored in an external service.</span></span> <span data-ttu-id="537e1-131">В этом случае вы можете реализовать собственную систему управления маркерами и войти в систему Teams, как описано [](~/resources/bot-v3/bot-authentication/auth-flow-bot.md) в остальных Teams проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="537e1-131">In this case, you may choose to still implement your own token management system and login experience within Teams, as described in the rest of the Teams [Authentication](~/resources/bot-v3/bot-authentication/auth-flow-bot.md) topics.</span></span>

## <a name="getting-started-with-oauthcard-in-teams"></a><span data-ttu-id="537e1-132">Начало работы с OAuthCard в Teams</span><span class="sxs-lookup"><span data-stu-id="537e1-132">Getting started with OAuthCard in Teams</span></span>

> [!NOTE]
> <span data-ttu-id="537e1-133">В этом руководстве используется SDK Bot Framework v3.</span><span class="sxs-lookup"><span data-stu-id="537e1-133">This guide is using the Bot Framework v3 SDK.</span></span> <span data-ttu-id="537e1-134">Реализацию v4 можно найти [здесь.](/azure/bot-service/bot-builder-authentication?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="537e1-134">You can find the v4 implementation [here](/azure/bot-service/bot-builder-authentication?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true).</span></span> <span data-ttu-id="537e1-135">Вам все равно потребуется создать манифест и включить token.botframework.com в раздел, так как в противном случае кнопка Вход не откроет окно проверки `validDomains` подлинности.</span><span class="sxs-lookup"><span data-stu-id="537e1-135">You will still need to create a manifest and include token.botframework.com in the `validDomains` section, because otherwise the Sign in button will not open the authentication window.</span></span> <span data-ttu-id="537e1-136">Для создания [манифеста используйте app Studio.](~/concepts/build-and-test/app-studio-overview.md)</span><span class="sxs-lookup"><span data-stu-id="537e1-136">Use the [App Studio](~/concepts/build-and-test/app-studio-overview.md) to generate your manifest.</span></span>

<span data-ttu-id="537e1-137">Сначала необходимо настроить службу ботов Azure для настройки внешних поставщиков проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="537e1-137">You’ll first need to configure your Azure bot service to set up external authentication providers.</span></span> <span data-ttu-id="537e1-138">Ознакомьтесь [с настройками поставщиков удостоверений для](~/concepts/authentication/configure-identity-provider.md) подробных действий.</span><span class="sxs-lookup"><span data-stu-id="537e1-138">Read [Configuring identity providers](~/concepts/authentication/configure-identity-provider.md) for detailed steps.</span></span>

<span data-ttu-id="537e1-139">Чтобы включить проверку подлинности с помощью службы Azure Bot, необходимо внести эти дополнения в код:</span><span class="sxs-lookup"><span data-stu-id="537e1-139">To enable authentication using the Azure Bot Service, you need to make these additions to your code:</span></span>

1. <span data-ttu-id="537e1-140">Включите token.botframework.com в раздел манифеста приложения, Teams встраить страницу входа в `validDomains` службу ботов.</span><span class="sxs-lookup"><span data-stu-id="537e1-140">Include token.botframework.com in the `validDomains` section of your app manifest because Teams will embed the Bot Service’s login page.</span></span>
2. <span data-ttu-id="537e1-141">Извлеките маркер из службы ботов всякий раз, когда боту необходимо получить доступ к ресурсам с проверкой подлинности.</span><span class="sxs-lookup"><span data-stu-id="537e1-141">Fetch the token from the Bot Service whenever your bot needs to access authenticated resources.</span></span> <span data-ttu-id="537e1-142">Если маркер не доступен, отправьте сообщение с OAuthCard пользователю с просьбой войти во внешнюю службу.</span><span class="sxs-lookup"><span data-stu-id="537e1-142">If no token is available, send a message with an OAuthCard to the user requesting them to log into the external service.</span></span>
3. <span data-ttu-id="537e1-143">Обработка действий по завершению входа.</span><span class="sxs-lookup"><span data-stu-id="537e1-143">Handle the login completion activity.</span></span> <span data-ttu-id="537e1-144">Это гарантирует, что запрос на проверку подлинности и маркер связаны с пользователем, который в настоящее время взаимодействует с вашим ботом.</span><span class="sxs-lookup"><span data-stu-id="537e1-144">This ensures that the authentication request and the token are associated with the user currently interacting with your bot.</span></span>
4. <span data-ttu-id="537e1-145">Извлечение маркера при выполнении действий с проверкой подлинности, таких как вызов внешних API REST.</span><span class="sxs-lookup"><span data-stu-id="537e1-145">Retrieve the token whenever your bot needs to perform authenticated actions, such as calling external REST APIs.</span></span>

<span data-ttu-id="537e1-146">В диалоговом коде необходимо добавить этот фрагмент (C#), который проверяет наличие существующего маркера доступа:</span><span class="sxs-lookup"><span data-stu-id="537e1-146">In your dialog code, you’ll need to add this snippet (C#), which checks for an existing access token:</span></span>

```CSharp
// First ask Bot Service if it already has a token for this user
var token = await context.GetUserTokenAsync(ConnectionName).ConfigureAwait(false);
if (token != null)
{
    // use the token to do exciting things!
}
else
{
    // If Bot Service does not have a token, send an OAuth card to sign in 
    await SendOAuthCardAsync(context, (Activity)context.Activity);
}
```

<span data-ttu-id="537e1-147">Если маркера доступа не существует, код отправляет пользователю сообщение с OAuthCard:</span><span class="sxs-lookup"><span data-stu-id="537e1-147">If an access token doesn’t exist, your code will then send a message with an OAuthCard to the user:</span></span>

```CSharp
private async Task SendOAuthCardAsync(IDialogContext context, Activity activity)
{
    await context.PostAsync($"To do this, you'll first need to sign in.");

    var reply = await context.Activity.CreateOAuthReplyAsync(_connectionName, _signInMessage, _buttonLabel).ConfigureAwait(false);
    await context.PostAsync(reply);

    context.Wait(WaitForToken);
}
```

<span data-ttu-id="537e1-148">Чтобы выполнить полное действие входа, необходимо обработать этот вызов:</span><span class="sxs-lookup"><span data-stu-id="537e1-148">To handle the login complete activity, you’ll need to process this Invoke:</span></span>

```CSharp
if (activity.Name == "signin/verifyState")
{
  // We do this so that we can pass handling to the right logic in the dialog. You can
  // set this to be whatever string you want.
  activity.Text = "loginComplete";
  await Conversation.SendAsync(activity, () => new Dialogs.RootDialog());

  return Request.CreateResponse(HttpStatusCode.OK);
}
```

<span data-ttu-id="537e1-149">В диалоговом коде вы можете получить маркер из службы проверки подлинности Bot:</span><span class="sxs-lookup"><span data-stu-id="537e1-149">In your dialog code, you can then retrieve the token from the Bot authentication service:</span></span>

```CSharp
if (text.Contains("loginComplete"))
  {
    // Handle login completion event.
    JObject ctx = activity.Value as JObject;

    if (ctx != null)
    {
      string code = ctx["state"].ToString();

      var oauthClient = activity.GetOAuthClient();
      var token = await oauthClient.OAuthApi.GetUserTokenAsync(activity.From.Id, ConnectionName, magicCode: code).ConfigureAwait(false);
      if (token != null)
      {
        // Make whatever API calls here you want
        await context.PostAsync($"Success! You are now signed in.");
      }
    }
  // Need to respond to the Invoke.
  return;
}
```

## <a name="using-oauthcard-with-messaging-extensions"></a><span data-ttu-id="537e1-150">Использование OAuthCard с расширениями обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="537e1-150">Using OAuthCard with messaging extensions</span></span>

<span data-ttu-id="537e1-151">Вы также можете использовать службу Azure Bot для подключения сторонних поставщиков к расширению обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="537e1-151">You can also use Azure Bot Service to connect third-party providers to your messaging extension.</span></span> <span data-ttu-id="537e1-152">Поток такой же, как и у бота, но вместо возврата OAuthCard служба возвращает запрос входа.</span><span class="sxs-lookup"><span data-stu-id="537e1-152">The flow is the same as with a bot, except instead of returning an OAuthCard, your service will return a login prompt.</span></span>

<span data-ttu-id="537e1-153">Следующий фрагмент (C#) иллюстрирует, как создать ответ входа:</span><span class="sxs-lookup"><span data-stu-id="537e1-153">The following snippet (C#) illustrates how to craft the login response:</span></span>

```CSharp
var token = await client.OAuthApi.GetUserTokenAsync(activity.From.Id, ConnectionName).ConfigureAwait(false);

if (token == null)
{
  // Send the login response with the auth link.
  string link = await client.OAuthApi.GetSignInLinkAsync(activity, ConnectionName);

  response = new ComposeExtensionResponse()
  {
    ComposeExtension = new ComposeExtensionResult()
  };
  response.ComposeExtension.Type = "auth";
  response.ComposeExtension.SuggestedActions = new ComposeExtensionSuggestedAction()
  {
    Actions = new List<CardAction>()
      {
        new CardAction(ActionTypes.OpenUrl, title: "Sign into this app", value: link)
      }
    };
  return response;
}
```

<span data-ttu-id="537e1-154">Обратите внимание, что в примере выше необходимо сделать вызов непосредственно `GetSignInLinkAsync` против `client.OAuthApi` свойства.</span><span class="sxs-lookup"><span data-stu-id="537e1-154">Note that in the example above you need to make the call to `GetSignInLinkAsync` directly against the `client.OAuthApi` property.</span></span>

<span data-ttu-id="537e1-155">Когда пользователь успешно завершит последовательность входа, служба получит еще один запрос Вызов, содержащий исходный запрос пользователя, а также строку параметров состояния, содержащую "волшебный код".</span><span class="sxs-lookup"><span data-stu-id="537e1-155">When the user successfully completes the login sequence, your service will receive another Invoke request containing the original user query, along with a state parameter string containing the “magic code”.</span></span> <span data-ttu-id="537e1-156">Теперь вы можете получить маркер с помощью этой строки, а также имя пользователя и имя подключения.</span><span class="sxs-lookup"><span data-stu-id="537e1-156">You can now fetch the token using this string, along with the user ID and connection name.</span></span>

```CSharp
var query = activity.GetComposeExtensionQueryData();
JObject data = activity.Value as JObject;

var client = activity.GetOAuthClient();

// Check if the request comes with login state
if (data != null && data["state"] != null)
{
  var token = await client.OAuthApi.GetUserTokenAsync(activity.From.Id, ConnectionName, data["state"].ToString());

  // Do stuff with the token here.

}
```
