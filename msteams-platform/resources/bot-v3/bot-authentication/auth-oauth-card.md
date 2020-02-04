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
# <a name="using-azure-bot-service-for-authentication-in-teams"></a>Использование службы Azure Bot для проверки подлинности в Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Без Оаускард службы Azure Bot это усложняет реализацию проверки подлинности в Bot. Это полная стопка стека, включающая создание веб-интерфейсов, интеграцию с внешними поставщиками OAuth, управление маркерами и обработку правильных вызовов API "сервер-сервер" для безопасного процесса проверки подлинности. Это может привести к клунки, для которых требуется ввод "магическых номеров".

С Оаускард службы Azure Bot упрощается вход пользователей и доступ к поставщикам внешних данных. Если вы уже реализовали проверку подлинности и хотите переключиться на что-то проще, или если вы хотите добавить проверку подлинности в службу Bot в первый раз, Оаускард может сделать это проще.

В других разделах, посвященных [проверке](~/resources/bot-v3/bot-authentication/auth-flow-bot.md) подлинности, описывается проверка подлинности без использования оаускард, поэтому если вы хотите более глубоко изучить проверку подлинности в Teams или в ситуации, когда вы не можете использовать оаускард, вы по-прежнему можете ссылаться на эти темы.

## <a name="support-for-the-oauthcard"></a>Поддержка Оаускард

В настоящее время существуют некоторые ограничения, которые можно использовать в Оаускард. Эти решения перечислены ниже.

* Карточка не будет работать с [гостевым доступом](/MicrosoftTeams/guest-access)
* Он не будет работать с [Microsoft Teams бесплатно](https://products.office.com/microsoft-teams/free)
* Его можно использовать только для проверки подлинности с помощью Bot
* Он работает только для Боты, зарегистрированных в [службе Azure Bot](https://azure.microsoft.com/services/bot-service/)

## <a name="how-does-the-azure-bot-service-help-me-do-authentication"></a>Как служба Azure Bot помогает выполнять проверку подлинности?

Полная документация по Оаускард доступна в разделе: [Добавление проверки подлинности в Bot через службу робота Azure](/azure/bot-service/bot-builder-tutorial-authentication?view=azure-bot-service-3.0). Обратите внимание, что этот раздел входит в набор документации по Azure Bot Framework и не относится к Teams.

В следующих разделах рассказывается, как использовать Оаускард в Teams.

## <a name="main-benefits-for-teams-developers"></a>Основные преимущества разработчиков Teams

Оаускард помогает с проверкой подлинности следующими способами:

* Обеспечивает сквозной веб-процесс проверки подлинности: вам больше не нужно создавать и размещать веб-страницы для направления внешнего входа или для перенаправления.
* Неэффективно для конечных пользователей: полный вход в Teams.
* Включает удобные средства управления маркерами: вам больше не нужно реализовывать систему хранения маркеров — вместо этого, служба Bot позаботится о кэшировании маркеров и предоставляет безопасный механизм для извлечения этих маркеров.
* Поддерживается полным комплектом SDK: простота интеграции и использования в службе Bot.
* Имеет встроенную поддержку многих популярных поставщиков OAuth, таких как Azure AD/MSA, Facebook и Google.

## <a name="when-should-i-implement-my-own-solution"></a>Когда следует реализовывать собственное решение?

Так как маркеры доступа являются конфиденциальными сведениями, их не следует хранить во внешней службе. В этом случае вы можете по-прежнему реализовать собственную систему управления маркерами и вход в систему в Teams, как описано в разделах, посвященных [проверке подлинности](~/resources/bot-v3/bot-authentication/auth-flow-bot.md) Teams.

## <a name="getting-started-with-oauthcard-in-teams"></a>Начало работы с Оаускард в Teams

> [!NOTE]
> В этом руководстве используется пакет SDK для Bot Framework версии 3. [Здесь](/azure/bot-service/bot-builder-authentication?view=azure-bot-service-4.0&tabs=csharp)вы можете найти реализацию v4. Вам все равно потребуется создать манифест и включить token.botframework.com в `validDomains` раздел, так как в противном случае кнопка входа не будет открывать окно проверки подлинности. Используйте [app Studio](~/concepts/build-and-test/app-studio-overview.md) для создания манифеста.

Сначала необходимо настроить службу Azure Bot, чтобы настроить внешние поставщики проверки подлинности. Сведения о [настройке поставщиков удостоверений](~/concepts/authentication/configure-identity-provider.md) для подробной процедуры.

Чтобы включить проверку подлинности с помощью службы Azure Bot, необходимо внести следующие дополнения в код:

1. Включите token.botframework.com в `validDomains` раздел манифеста приложения, так как teams внедряет страницу входа в службу Bot.
2. Получение маркера из службы Bot, когда необходимо получить доступ к ресурсам, прошедшим проверку подлинности. Если маркер недоступен, отправьте сообщение с Оаускард пользователю, который запрашивает вход в внешнюю службу.
3. Обработка действия по завершению входа. Это гарантирует, что запрос и маркер проверки подлинности связываются с пользователем, в настоящее время взаимодействующим с роботом Bot.
4. Извлеките маркер, когда он должен выполнять действия, прошедшие проверку подлинности, например, вызов внешних интерфейсов API REST.

В коде диалогового окна необходимо добавить этот фрагмент кода (C#), который проверяет наличие существующего маркера доступа:

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

Если маркер доступа не существует, код отправит ему сообщение с Оаускард:

```CSharp
private async Task SendOAuthCardAsync(IDialogContext context, Activity activity)
{
    await context.PostAsync($"To do this, you'll first need to sign in.");

    var reply = await context.Activity.CreateOAuthReplyAsync(_connectionName, _signInMessage, _buttonLabel).ConfigureAwait(false);
    await context.PostAsync(reply);

    context.Wait(WaitForToken);
}
```

Чтобы обработать действие "завершение входа", необходимо обработать следующий вызов:

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

В коде диалогового окна вы можете получить маркер из службы проверки подлинности Bot:

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

## <a name="using-oauthcard-with-messaging-extensions"></a>Использование Оаускард с расширениями обмена сообщениями

Вы также можете использовать службу Azure Bot для подключения сторонних поставщиков к своему расширению обмена сообщениями. Это то же, что и для Bot, за исключением того, что вместо возврата Оаускард служба возвращает запрос на вход.

В следующем фрагменте кода (C#) показано, как создавать ответ на вход:

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

Обратите внимание, что в приведенном выше примере необходимо сделать вызов `GetSignInLinkAsync` напрямую для `client.OAuthApi` свойства.

Когда пользователь успешно завершает последовательность входа, служба получает другой запрос на вызов, содержащий исходный запрос пользователя, а также строку с параметром State, содержащую "код Magic". Теперь вы можете получить маркер, используя эту строку, а также идентификатор пользователя и имя подключения.

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
