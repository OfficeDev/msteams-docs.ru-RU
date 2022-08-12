---
title: Использование Azure Служба Bot для проверки подлинности в Teams
description: Описание azure Служба Bot OAuthCard и его использования для проверки подлинности
ms.topic: conceptual
localization_priority: Normal
keywords: Проверка подлинности teams OAuthCard OAuth card Azure Служба Bot
ms.openlocfilehash: efe05320fc6a0b03b530349b5498fa29d36b47b6
ms.sourcegitcommit: 69a45722c5c09477bbff3ba1520e6c81d2d2d997
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/11/2022
ms.locfileid: "67312235"
---
# <a name="using-azure-bot-service-for-authentication-in-teams"></a>Использование Azure Служба Bot для проверки подлинности в Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Без OAuthCard Служба Bot azure сложно реализовать проверку подлинности в боте. Это задача с полным стеком, которая включает создание веб-интерфейса, интеграцию с внешними поставщиками OAuth, управление маркерами и обработку вызовов API между серверами для безопасного завершения потока проверки подлинности. Это может привести к нестрогому опыту, требуя ввода "магических чисел".

С помощью Служба Bot Azure OAuthCard боту Teams проще входить в систему пользователей и получать доступ к внешним поставщикам данных. Если вы уже реализовали проверку подлинности и хотите переключиться на что-то более простое или если вы хотите добавить проверку подлинности в службу бота в первый раз, OAuthCard может упростить эту задачу.

Другие разделы[](~/resources/bot-v3/bot-authentication/auth-flow-bot.md), посвященные проверке подлинности, описывают проверку подлинности без использования OAuthCard, поэтому, если вы хотите более подробно разобраться в проверке подлинности в Teams или в ситуации, когда вы не можете использовать OAuthCard, вы по-прежнему можете ссылаться на эти темы.

## <a name="support-for-the-oauthcard"></a>Поддержка OAuthCard

В настоящее время существуют некоторые ограничения на использование OAuthCard. В том числе:

* Карточка не будет работать с [гостевым доступом](/MicrosoftTeams/guest-access).
* Он не будет [работать с Бесплатная версия Microsoft Teams](https://products.office.com/microsoft-teams/free).
* Его можно использовать только для проверки подлинности бота.
* Он работает только для ботов, зарегистрированных в [azure Служба Bot](https://azure.microsoft.com/services/bot-service/).

## <a name="how-does-the-azure-bot-service-help-me-do-authentication"></a>Как azure Служба Bot аутентификацию?

Полная документация по OAuthCard доступна в разделе " Добавление проверки подлинности в бот [с помощью Azure Служба Bot](/azure/bot-service/bot-builder-tutorial-authentication?view=azure-bot-service-3.0&preserve-view=true). Обратите внимание, что этот раздел находится в наборе документации по Azure Bot Framework и не относится к Teams.

В следующих разделах показано, как использовать OAuthCard в Teams.

## <a name="main-benefits-for-teams-developers"></a>Основные преимущества для разработчиков Teams

OAuthCard помогает выполнить проверку подлинности следующими способами:

* Предоставляет встроенный веб-поток проверки подлинности: вам больше не нужно писать и разместить веб-страницу для направления к внешним интерфейсам входа или предоставления перенаправления.
* Это удобно для конечных пользователей: выполните полный вход прямо в Teams.
* Включает простое управление маркерами: вам больше не нужно реализовывать систему хранения маркеров. Вместо этого Служба Bot выполняет кэширование маркеров и предоставляет безопасный механизм для получения этих маркеров.
* Поддерживается полными пакетами SDK: простота интеграции и использования из службы бота.
* Поддерживает множество популярных поставщиков OAuth, таких как Azure AD/MSA, Facebook и Google.

## <a name="when-should-i-implement-my-own-solution"></a>Когда следует реализовать собственное решение?

Так как маркеры доступа являются конфиденциальной информацией, вы можете не хранить их во внешней службе. В этом случае вы можете реализовать собственную систему управления маркерами и функцию входа в Teams, как описано в остальных разделах проверки [подлинности](~/resources/bot-v3/bot-authentication/auth-flow-bot.md) Teams.

## <a name="getting-started-with-oauthcard-in-teams"></a>Начало работы с OAuthCard в Teams

> [!NOTE]
> В этом руководстве используется пакет SDK Bot Framework версии 3. Реализацию версии 4 можно найти [здесь](/azure/bot-service/bot-builder-authentication?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true). Вам по-прежнему `validDomains` потребуется создать манифест и включить token.botframework.com в раздел, так как в противном случае кнопка входа не откроет окно проверки подлинности. Используйте портал [разработчика для](~/concepts/build-and-test/teams-developer-portal.md) создания манифеста.

Сначала необходимо настроить службу ботов Azure для настройки внешних поставщиков проверки подлинности. [Подробные инструкции см. в](~/concepts/authentication/configure-identity-provider.md) статье "Настройка поставщиков удостоверений".

Чтобы включить проверку подлинности с Служба Bot Azure, необходимо внести следующие дополнения в код:

1. Включите token.botframework.com в `validDomains` раздел манифеста приложения, так как Teams Служба Bot страницу входа пользователя.
2. Извлеките маркер из Служба Bot каждый раз, когда боту требуется доступ к ресурсам, прошедшим проверку подлинности. Если маркер недоступен, отправьте сообщение с OAuthCard пользователю с запросом на вход во внешнюю службу.
3. Обработка действия завершения входа. Это гарантирует, что запрос проверки подлинности и маркер связаны с пользователем, который в настоящее время взаимодействует с ботом.
4. Извлеките маркер всякий раз, когда боту необходимо выполнить действия, прошедшие проверку подлинности, например вызов внешних REST API.

В код диалогового окна необходимо добавить этот фрагмент кода (C#), который проверяет наличие существующего маркера доступа:

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

Если маркер доступа не существует, код отправит пользователю сообщение с OAuthCard:

```CSharp
private async Task SendOAuthCardAsync(IDialogContext context, Activity activity)
{
    await context.PostAsync($"To do this, you'll first need to sign in.");

    var reply = await context.Activity.CreateOAuthReplyAsync(_connectionName, _signInMessage, _buttonLabel).ConfigureAwait(false);
    await context.PostAsync(reply);

    context.Wait(WaitForToken);
}
```

Чтобы обработать действие входа в систему, необходимо обработать этот вызов:

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

Затем в коде диалогового окна можно получить маркер из службы проверки подлинности Бота:

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

Вы также можете использовать Azure Служба Bot для подключения сторонних поставщиков к расширению обмена сообщениями. Поток такой же, как и для бота, за исключением того, что вместо возврата OAuthCard служба вернет запрос на вход.

В следующем фрагменте кода (C#) показано, как создать ответ для входа:

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

Обратите внимание, что в приведенном выше примере необходимо `GetSignInLinkAsync` выполнить вызов непосредственно к свойству `client.OAuthApi` .

Когда пользователь успешно завершит последовательность входа, служба получит еще один запрос Invoke, содержащий исходный запрос пользователя, а также строку параметра состояния, содержащую "магический код". Теперь вы можете получить маркер с помощью этой строки, а также идентификатор пользователя и имя подключения.

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
