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
# <a name="using-azure-bot-service-for-authentication-in-teams"></a>Использование службы Azure Bot для проверки подлинности в Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Без OAuthCard службы microsoft Bot службы Azure сложно реализовать проверку подлинности в боте. Это задача полного стека, связанная с созданием веб-опыта, интеграцией с внешними поставщиками OAuth, управлением маркерами и обработкой вызовов API между серверами и серверами для безопасного завершения потока проверки подлинности. Это может привести к неуклюжим опытом, требующим ввода "магических чисел".

С помощью OAuthCard службы ботов Azure для вашего Teams-бота проще войти в пользователей и получить доступ к внешним поставщикам данных. Если вы уже внедрили auth и хотите перейти на что-то более простое, или если вы хотите добавить проверку подлинности в службу ботов впервые, OAuthCard может упростить ее.

Другие темы в проверке подлинности описывают проверку подлинности без использования OAuthCard, поэтому если вы хотите более глубоко разобраться в проверке подлинности в Teams или иметь ситуацию, в которой нельзя использовать OAuthCard, вы все равно можете ссылаться на эти темы. [](~/resources/bot-v3/bot-authentication/auth-flow-bot.md)

## <a name="support-for-the-oauthcard"></a>Поддержка OAuthCard

В настоящее время существует ряд ограничений на использование OAuthCard. Они включают:

* Карта не будет работать с [гостевим доступом](/MicrosoftTeams/guest-access)
* Он не будет работать с [Microsoft Teams бесплатно](https://products.office.com/microsoft-teams/free)
* Его можно использовать только для проверки подлинности ботов
* Он работает только для ботов, зарегистрированных в [службе Azure Bot](https://azure.microsoft.com/services/bot-service/)

## <a name="how-does-the-azure-bot-service-help-me-do-authentication"></a>Как служба Azure Bot помогает мне делать проверку подлинности?

Полная документация с помощью OAuthCard доступна в разделе: Добавление проверки подлинности в бот [через службу Azure Bot.](/azure/bot-service/bot-builder-tutorial-authentication?view=azure-bot-service-3.0&preserve-view=true) Обратите внимание, что эта тема находится в наборе документации Azure Bot Framework и не является конкретной для Teams.

В следующих разделах повеяно, как использовать OAuthCard в Teams.

## <a name="main-benefits-for-teams-developers"></a>Основные преимущества для Teams разработчиков

OAuthCard помогает с проверкой подлинности следующими способами:

* Обеспечивает поток веб-проверки подлинности на основе интернета: вам больше не нужно писать и хост-страницу, чтобы направлять внешние опытом входа или предоставлять перенаправление.
* Является бесшовным для конечных пользователей: выполните полный вход в опытом прямо в Teams.
* Включает простой процесс управления маркерами: вам больше не нужно внедрять систему хранения маркеров, вместо этого служба ботов заботится о кэширования маркеров и предоставляет безопасный механизм для получения этих маркеров.
* Поддерживается полными SDKs: легко интегрировать и потреблять из бот-службы.
* Поддерживает множество популярных поставщиков OAuth, таких как Azure AD/MSA, Facebook и Google.

## <a name="when-should-i-implement-my-own-solution"></a>Когда следует реализовать собственное решение?

Так как маркеры доступа являются конфиденциальной информацией, вы можете не хранить их во внешней службе. В этом случае вы можете реализовать собственную систему управления маркерами и войти в систему Teams, как описано [](~/resources/bot-v3/bot-authentication/auth-flow-bot.md) в остальных Teams проверки подлинности.

## <a name="getting-started-with-oauthcard-in-teams"></a>Начало работы с OAuthCard в Teams

> [!NOTE]
> В этом руководстве используется SDK Bot Framework v3. Реализацию v4 можно найти [здесь.](/azure/bot-service/bot-builder-authentication?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) Вам все равно потребуется создать манифест и включить token.botframework.com в раздел, так как в противном случае кнопка Вход не откроет окно проверки `validDomains` подлинности. Для создания [манифеста используйте app Studio.](~/concepts/build-and-test/app-studio-overview.md)

Сначала необходимо настроить службу ботов Azure для настройки внешних поставщиков проверки подлинности. Ознакомьтесь [с настройками поставщиков удостоверений для](~/concepts/authentication/configure-identity-provider.md) подробных действий.

Чтобы включить проверку подлинности с помощью службы Azure Bot, необходимо внести эти дополнения в код:

1. Включите token.botframework.com в раздел манифеста приложения, Teams встраить страницу входа в `validDomains` службу ботов.
2. Извлеките маркер из службы ботов всякий раз, когда боту необходимо получить доступ к ресурсам с проверкой подлинности. Если маркер не доступен, отправьте сообщение с OAuthCard пользователю с просьбой войти во внешнюю службу.
3. Обработка действий по завершению входа. Это гарантирует, что запрос на проверку подлинности и маркер связаны с пользователем, который в настоящее время взаимодействует с вашим ботом.
4. Извлечение маркера при выполнении действий с проверкой подлинности, таких как вызов внешних API REST.

В диалоговом коде необходимо добавить этот фрагмент (C#), который проверяет наличие существующего маркера доступа:

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

Если маркера доступа не существует, код отправляет пользователю сообщение с OAuthCard:

```CSharp
private async Task SendOAuthCardAsync(IDialogContext context, Activity activity)
{
    await context.PostAsync($"To do this, you'll first need to sign in.");

    var reply = await context.Activity.CreateOAuthReplyAsync(_connectionName, _signInMessage, _buttonLabel).ConfigureAwait(false);
    await context.PostAsync(reply);

    context.Wait(WaitForToken);
}
```

Чтобы выполнить полное действие входа, необходимо обработать этот вызов:

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

В диалоговом коде вы можете получить маркер из службы проверки подлинности Bot:

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

## <a name="using-oauthcard-with-messaging-extensions"></a>Использование OAuthCard с расширениями обмена сообщениями

Вы также можете использовать службу Azure Bot для подключения сторонних поставщиков к расширению обмена сообщениями. Поток такой же, как и у бота, но вместо возврата OAuthCard служба возвращает запрос входа.

Следующий фрагмент (C#) иллюстрирует, как создать ответ входа:

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

Обратите внимание, что в примере выше необходимо сделать вызов непосредственно `GetSignInLinkAsync` против `client.OAuthApi` свойства.

Когда пользователь успешно завершит последовательность входа, служба получит еще один запрос Вызов, содержащий исходный запрос пользователя, а также строку параметров состояния, содержащую "волшебный код". Теперь вы можете получить маркер с помощью этой строки, а также имя пользователя и имя подключения.

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
