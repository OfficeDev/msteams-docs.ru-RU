---
title: Использование службы Azure Bot для проверки подлинности в Teams
description: Описание службы Azure Bot Оаускард и ее использования для проверки подлинности
keywords: Проверка подлинности Teams Оаускард OAuth Card OAuth Service Azure
ms.openlocfilehash: 0397c45b39470d97c1158b2681462038de618a39
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675474"
---
# <a name="using-azure-bot-service-for-authentication-in-teams"></a><span data-ttu-id="bea8b-104">Использование службы Azure Bot для проверки подлинности в Teams</span><span class="sxs-lookup"><span data-stu-id="bea8b-104">Using Azure Bot Service for Authentication in Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="bea8b-105">Без Оаускард службы Azure Bot это усложняет реализацию проверки подлинности в Bot.</span><span class="sxs-lookup"><span data-stu-id="bea8b-105">Without the Azure Bot Service’s OAuthCard it is complicated to implement authentication in a bot.</span></span> <span data-ttu-id="bea8b-106">Это полная стопка стека, включающая создание веб-интерфейсов, интеграцию с внешними поставщиками OAuth, управление маркерами и обработку правильных вызовов API "сервер-сервер" для безопасного процесса проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="bea8b-106">It is a full-stack challenge that involving building a web experience, integrating with external OAuth providers, token management, and handling the right server-to-server API calls to complete authentication flow securely.</span></span> <span data-ttu-id="bea8b-107">Это может привести к клунки, для которых требуется ввод "магическых номеров".</span><span class="sxs-lookup"><span data-stu-id="bea8b-107">This can result in clunky experiences requiring the entry of “magic numbers”.</span></span>

<span data-ttu-id="bea8b-108">С Оаускард службы Azure Bot упрощается вход пользователей и доступ к поставщикам внешних данных.</span><span class="sxs-lookup"><span data-stu-id="bea8b-108">With Azure Bot Service’s OAuthCard, it is easier for your Teams bot to sign in your users and access external data providers.</span></span> <span data-ttu-id="bea8b-109">Если вы уже реализовали проверку подлинности и хотите переключиться на что-то проще, или если вы хотите добавить проверку подлинности в службу Bot в первый раз, Оаускард может сделать это проще.</span><span class="sxs-lookup"><span data-stu-id="bea8b-109">Whether you’ve already implemented auth and you want to switch over to something simpler, or if you are looking to add authentication to your bot service for the first time, the OAuthCard can make it easier.</span></span>

<span data-ttu-id="bea8b-110">В других разделах, посвященных [проверке](~/resources/bot-v3/bot-authentication/auth-flow-bot.md) подлинности, описывается проверка подлинности без использования оаускард, поэтому если вы хотите более глубоко изучить проверку подлинности в Teams или в ситуации, когда вы не можете использовать оаускард, вы по-прежнему можете ссылаться на эти темы.</span><span class="sxs-lookup"><span data-stu-id="bea8b-110">Other topics in [Authentication](~/resources/bot-v3/bot-authentication/auth-flow-bot.md) describe authentication without using the OAuthCard, so if you want to understand authentication in Teams more deeply, or have a situation where you can not use the OAuthCard, you can still refer to those topics.</span></span>

## <a name="support-for-the-oauthcard"></a><span data-ttu-id="bea8b-111">Поддержка Оаускард</span><span class="sxs-lookup"><span data-stu-id="bea8b-111">Support for the OAuthCard</span></span>

<span data-ttu-id="bea8b-112">В настоящее время существуют некоторые ограничения, которые можно использовать в Оаускард.</span><span class="sxs-lookup"><span data-stu-id="bea8b-112">There are currently some restrictions to where you can use the OAuthCard.</span></span> <span data-ttu-id="bea8b-113">Эти решения перечислены ниже.</span><span class="sxs-lookup"><span data-stu-id="bea8b-113">These include:</span></span>

* <span data-ttu-id="bea8b-114">Карточка не будет работать с [гостевым доступом](/MicrosoftTeams/guest-access)</span><span class="sxs-lookup"><span data-stu-id="bea8b-114">The card will not work with [guest access](/MicrosoftTeams/guest-access)</span></span>
* <span data-ttu-id="bea8b-115">Он не будет работать с [Microsoft Teams бесплатно](https://products.office.com/microsoft-teams/free)</span><span class="sxs-lookup"><span data-stu-id="bea8b-115">It will not work with [Microsoft Teams free](https://products.office.com/microsoft-teams/free)</span></span>
* <span data-ttu-id="bea8b-116">Его можно использовать только для проверки подлинности с помощью Bot</span><span class="sxs-lookup"><span data-stu-id="bea8b-116">It can only be used for bot authentication</span></span>
* <span data-ttu-id="bea8b-117">Он работает только для Боты, зарегистрированных в [службе Azure Bot](https://azure.microsoft.com/services/bot-service/)</span><span class="sxs-lookup"><span data-stu-id="bea8b-117">It only works for bots registered in the [Azure Bot Service](https://azure.microsoft.com/services/bot-service/)</span></span>

## <a name="how-does-the-azure-bot-service-help-me-do-authentication"></a><span data-ttu-id="bea8b-118">Как служба Azure Bot помогает выполнять проверку подлинности?</span><span class="sxs-lookup"><span data-stu-id="bea8b-118">How does the Azure Bot Service help me do authentication?</span></span>

<span data-ttu-id="bea8b-119">Полная документация по Оаускард доступна в разделе: [Добавление проверки подлинности в Bot через службу робота Azure](/azure/bot-service/bot-builder-tutorial-authentication?view=azure-bot-service-3.0).</span><span class="sxs-lookup"><span data-stu-id="bea8b-119">Full documentation using the OAuthCard is available in the topic: [Add authentication to your bot via Azure Bot Service](/azure/bot-service/bot-builder-tutorial-authentication?view=azure-bot-service-3.0).</span></span> <span data-ttu-id="bea8b-120">Обратите внимание, что этот раздел входит в набор документации по Azure Bot Framework и не относится к Teams.</span><span class="sxs-lookup"><span data-stu-id="bea8b-120">Note that this topic is in the Azure Bot Framework documentation set, and is not specific to Teams.</span></span>

<span data-ttu-id="bea8b-121">В следующих разделах рассказывается, как использовать Оаускард в Teams.</span><span class="sxs-lookup"><span data-stu-id="bea8b-121">The following sections tell how to use the OAuthCard in Teams.</span></span>

## <a name="main-benefits-for-teams-developers"></a><span data-ttu-id="bea8b-122">Основные преимущества разработчиков Teams</span><span class="sxs-lookup"><span data-stu-id="bea8b-122">Main benefits for Teams developers</span></span>

<span data-ttu-id="bea8b-123">Оаускард помогает с проверкой подлинности следующими способами:</span><span class="sxs-lookup"><span data-stu-id="bea8b-123">The OAuthCard helps with authentication in the following ways:</span></span>

* <span data-ttu-id="bea8b-124">Обеспечивает сквозной веб-процесс проверки подлинности: вам больше не нужно создавать и размещать веб-страницы для направления внешнего входа или для перенаправления.</span><span class="sxs-lookup"><span data-stu-id="bea8b-124">Provides an out-of-box web-based authentication flow: you no longer have to write and host a web page to direct to external login experiences or provide a redirect.</span></span>
* <span data-ttu-id="bea8b-125">Неэффективно для конечных пользователей: полный вход в Teams.</span><span class="sxs-lookup"><span data-stu-id="bea8b-125">Is seamless for end users: complete the full sign in experience right within Teams.</span></span>
* <span data-ttu-id="bea8b-126">Включает удобные средства управления маркерами: вам больше не нужно реализовывать систему хранения маркеров — вместо этого, служба Bot позаботится о кэшировании маркеров и предоставляет безопасный механизм для извлечения этих маркеров.</span><span class="sxs-lookup"><span data-stu-id="bea8b-126">Includes easy token management: you no longer have to implement a token storage system – instead, the Bot Service takes care of token caching and provides a secure mechanism for fetching those tokens.</span></span>
* <span data-ttu-id="bea8b-127">Поддерживается полным комплектом SDK: простота интеграции и использования в службе Bot.</span><span class="sxs-lookup"><span data-stu-id="bea8b-127">Is supported by complete SDKs: easy to integrate and consume from your bot service.</span></span>
* <span data-ttu-id="bea8b-128">Имеет встроенную поддержку многих популярных поставщиков OAuth, таких как Azure AD/MSA, Facebook и Google.</span><span class="sxs-lookup"><span data-stu-id="bea8b-128">Has out-of-box support for many popular OAuth providers, such as Azure AD/MSA, Facebook, and Google.</span></span>

## <a name="when-should-i-implement-my-own-solution"></a><span data-ttu-id="bea8b-129">Когда следует реализовывать собственное решение?</span><span class="sxs-lookup"><span data-stu-id="bea8b-129">When should I implement my own solution?</span></span>

<span data-ttu-id="bea8b-130">Так как маркеры доступа являются конфиденциальными сведениями, их не следует хранить во внешней службе.</span><span class="sxs-lookup"><span data-stu-id="bea8b-130">Because access tokens are sensitive information, you may not wish to have them stored in an external service.</span></span> <span data-ttu-id="bea8b-131">В этом случае вы можете по-прежнему реализовать собственную систему управления маркерами и вход в систему в Teams, как описано в разделах, посвященных [проверке подлинности](~/resources/bot-v3/bot-authentication/auth-flow-bot.md) Teams.</span><span class="sxs-lookup"><span data-stu-id="bea8b-131">In this case, you may choose to still implement your own token management system and login experience within Teams, as described in the rest of the Teams [Authentication](~/resources/bot-v3/bot-authentication/auth-flow-bot.md) topics.</span></span>

## <a name="getting-started-with-oauthcard-in-teams"></a><span data-ttu-id="bea8b-132">Начало работы с Оаускард в Teams</span><span class="sxs-lookup"><span data-stu-id="bea8b-132">Getting started with OAuthCard in Teams</span></span>

> [!NOTE]
> <span data-ttu-id="bea8b-133">В этом руководстве используется пакет SDK для Bot Framework версии 3.</span><span class="sxs-lookup"><span data-stu-id="bea8b-133">This guide is using the Bot Framework v3 SDK.</span></span> <span data-ttu-id="bea8b-134">[Здесь](/azure/bot-service/bot-builder-authentication?view=azure-bot-service-4.0&tabs=csharp)вы можете найти реализацию v4.</span><span class="sxs-lookup"><span data-stu-id="bea8b-134">You can find the v4 implementation [here](/azure/bot-service/bot-builder-authentication?view=azure-bot-service-4.0&tabs=csharp).</span></span> <span data-ttu-id="bea8b-135">Вам все равно потребуется создать манифест и включить token.botframework.com в `validDomains` раздел, так как в противном случае кнопка входа не будет открывать окно проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="bea8b-135">You will still need to create a manifest and include token.botframework.com in the `validDomains` section, because otherwise the Sign in button will not open the authentication window.</span></span> <span data-ttu-id="bea8b-136">Используйте [app Studio](~/concepts/build-and-test/app-studio-overview.md) для создания манифеста.</span><span class="sxs-lookup"><span data-stu-id="bea8b-136">Use the [App Studio](~/concepts/build-and-test/app-studio-overview.md) to generate your manifest.</span></span>

<span data-ttu-id="bea8b-137">Сначала необходимо настроить службу Azure Bot, чтобы настроить внешние поставщики проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="bea8b-137">You’ll first need to configure your Azure bot service to set up external authentication providers.</span></span> <span data-ttu-id="bea8b-138">Сведения о [настройке поставщиков удостоверений](~/concepts/authentication/configure-identity-provider.md) для подробной процедуры.</span><span class="sxs-lookup"><span data-stu-id="bea8b-138">Read [Configuring identity providers](~/concepts/authentication/configure-identity-provider.md) for detailed steps.</span></span>

<span data-ttu-id="bea8b-139">Чтобы включить проверку подлинности с помощью службы Azure Bot, необходимо внести следующие дополнения в код:</span><span class="sxs-lookup"><span data-stu-id="bea8b-139">To enable authentication using the Azure Bot Service, you need to make these additions to your code:</span></span>

1. <span data-ttu-id="bea8b-140">Включите token.botframework.com в `validDomains` раздел манифеста приложения, так как teams внедряет страницу входа в службу Bot.</span><span class="sxs-lookup"><span data-stu-id="bea8b-140">Include token.botframework.com in the `validDomains` section of your app manifest because Teams will embed the Bot Service’s login page.</span></span>
2. <span data-ttu-id="bea8b-141">Получение маркера из службы Bot, когда необходимо получить доступ к ресурсам, прошедшим проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="bea8b-141">Fetch the token from the Bot Service whenever your bot needs to access authenticated resources.</span></span> <span data-ttu-id="bea8b-142">Если маркер недоступен, отправьте сообщение с Оаускард пользователю, который запрашивает вход в внешнюю службу.</span><span class="sxs-lookup"><span data-stu-id="bea8b-142">If no token is available, send a message with an OAuthCard to the user requesting them to log into the external service.</span></span>
3. <span data-ttu-id="bea8b-143">Обработка действия по завершению входа.</span><span class="sxs-lookup"><span data-stu-id="bea8b-143">Handle the login completion activity.</span></span> <span data-ttu-id="bea8b-144">Это гарантирует, что запрос и маркер проверки подлинности связываются с пользователем, в настоящее время взаимодействующим с роботом Bot.</span><span class="sxs-lookup"><span data-stu-id="bea8b-144">This ensures that the authentication request and the token are associated with the user currently interacting with your bot.</span></span>
4. <span data-ttu-id="bea8b-145">Извлеките маркер, когда он должен выполнять действия, прошедшие проверку подлинности, например, вызов внешних интерфейсов API REST.</span><span class="sxs-lookup"><span data-stu-id="bea8b-145">Retrieve the token whenever your bot needs to perform authenticated actions, such as calling external REST APIs.</span></span>

<span data-ttu-id="bea8b-146">В коде диалогового окна необходимо добавить этот фрагмент кода (C#), который проверяет наличие существующего маркера доступа:</span><span class="sxs-lookup"><span data-stu-id="bea8b-146">In your dialog code, you’ll need to add this snippet (C#), which checks for an existing access token:</span></span>

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

<span data-ttu-id="bea8b-147">Если маркер доступа не существует, код отправит ему сообщение с Оаускард:</span><span class="sxs-lookup"><span data-stu-id="bea8b-147">If an access token doesn’t exist, your code will then send a message with an OAuthCard to the user:</span></span>

```CSharp
private async Task SendOAuthCardAsync(IDialogContext context, Activity activity)
{
    await context.PostAsync($"To do this, you'll first need to sign in.");

    var reply = await context.Activity.CreateOAuthReplyAsync(_connectionName, _signInMessage, _buttonLabel).ConfigureAwait(false);
    await context.PostAsync(reply);

    context.Wait(WaitForToken);
}
```

<span data-ttu-id="bea8b-148">Чтобы обработать действие "завершение входа", необходимо обработать следующий вызов:</span><span class="sxs-lookup"><span data-stu-id="bea8b-148">To handle the login complete activity, you’ll need to process this Invoke:</span></span>

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

<span data-ttu-id="bea8b-149">В коде диалогового окна вы можете получить маркер из службы проверки подлинности Bot:</span><span class="sxs-lookup"><span data-stu-id="bea8b-149">In your dialog code, you can then retrieve the token from the Bot authentication service:</span></span>

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

## <a name="using-oauthcard-with-messaging-extensions"></a><span data-ttu-id="bea8b-150">Использование Оаускард с расширениями обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="bea8b-150">Using OAuthCard with messaging extensions</span></span>

<span data-ttu-id="bea8b-151">Вы также можете использовать службу Azure Bot для подключения сторонних поставщиков к своему расширению обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="bea8b-151">You can also use Azure Bot Service to connect third-party providers to your messaging extension.</span></span> <span data-ttu-id="bea8b-152">Это то же, что и для Bot, за исключением того, что вместо возврата Оаускард служба возвращает запрос на вход.</span><span class="sxs-lookup"><span data-stu-id="bea8b-152">The flow is the same as with a bot, except instead of returning an OAuthCard, your service will return a login prompt.</span></span>

<span data-ttu-id="bea8b-153">В следующем фрагменте кода (C#) показано, как создавать ответ на вход:</span><span class="sxs-lookup"><span data-stu-id="bea8b-153">The following snippet (C#) illustrates how to craft the login response:</span></span>

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

<span data-ttu-id="bea8b-154">Обратите внимание, что в приведенном выше примере необходимо сделать вызов `GetSignInLinkAsync` напрямую для `client.OAuthApi` свойства.</span><span class="sxs-lookup"><span data-stu-id="bea8b-154">Note that in the example above you need to make the call to `GetSignInLinkAsync` directly against the `client.OAuthApi` property.</span></span>

<span data-ttu-id="bea8b-155">Когда пользователь успешно завершает последовательность входа, служба получает другой запрос на вызов, содержащий исходный запрос пользователя, а также строку с параметром State, содержащую "код Magic".</span><span class="sxs-lookup"><span data-stu-id="bea8b-155">When the user successfully completes the login sequence, your service will receive another Invoke request containing the original user query, along with a state parameter string containing the “magic code”.</span></span> <span data-ttu-id="bea8b-156">Теперь вы можете получить маркер, используя эту строку, а также идентификатор пользователя и имя подключения.</span><span class="sxs-lookup"><span data-stu-id="bea8b-156">You can now fetch the token using this string, along with the user ID and connection name.</span></span>

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
