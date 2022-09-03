---
title: Поддержка SSO в расширениях для сообщений
author: KirtiPereira
description: Включите единый вход (SSO) в приложении расширения сообщений Teams, используя Azure AD и пример кода.
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: 999094e1649008e6d0528c8ac44c21a3f5f2f7a4
ms.sourcegitcommit: 82c585d287d61924ce3a3bba3e9caeff35c9a27a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/02/2022
ms.locfileid: "67586849"
---
# <a name="enable-sso-for-message-extensions"></a>Включение единого входа в расширениях для сообщений

Поддержка единого входа (SSO) теперь доступна для расширений сообщений и развертывания ссылок. Включение единого входа для расширений сообщений по умолчанию обновляет токен проверки подлинности, что сводит к минимуму количество раз, необходимое для ввода учетных данных для входа в Microsoft Teams.

В этом документе приводится инструкция о том, как включить SSO и при необходимости сохранить маркер проверки подлинности.

## <a name="prerequisites"></a>Предварительные условия

Необходимое условие для активации SSO расширений для сообщений и развертывания ссылок:

* Необходимо иметь учетную запись [Azure](https://azure.microsoft.com/free/).
* Необходимо настроить приложение на портале Azure AD и обновить манифест приложения Teams, как определено в статье [Регистрация приложения на портале Azure AD](../../bots/how-to/authentication/auth-aad-sso-bots.md#register-your-app-through-the-azure-ad-portal).

> [!NOTE]
> Дополнительные сведения о создании учетной записи Azure и обновлении манифеста приложения см. в статье [Поддержка единого входа (SSO) для ботов](../../bots/how-to/authentication/auth-aad-sso-bots.md).

## <a name="enable-sso-for-message-extensions-and-link-unfurling"></a>Включить SSO для расширений сообщений и развертывания ссылок

После завершения необходимых условий можно включить SSO расширений для сообщений и развернуть ссылки.

Чтобы включить SSO, выполните следующие действия.

1. Обновите боты [подключения OAuth](../../bots/how-to/authentication/auth-aad-sso-bots.md#update-the-azure-portal-with-the-oauth-connection) на портале Microsoft Azure.
2. Скачайте [образец расширения для сообщений](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config) и следуйте инструкциям мастера установки.
   > [!NOTE]
   > Используйте подключение OAuth ботов при настройке расширений сообщений.
3. В файле [TeamsMessagingExtensionsSearchAuthConfigBot.cs](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config/Bots/TeamsMessagingExtensionsSearchAuthConfigBot.cs) обновите значение с *auth* до *silentAuth* в `OnTeamsMessagingExtensionQueryAsync` и/или `OnTeamsAppBasedLinkQueryAsync`.  

    > [!NOTE]
    > Мы не поддерживаем другие обработчики SSO, за исключением `OnTeamsMessagingExtensionQueryAsync` и `OnTeamsAppBasedLinkQueryAsync` из файла TeamsMessagingExtensionsSearchAuthConfigBot.cs.

4. Маркер вы получаете в обработчике `OnTeamsMessagingExtensionQueryAsync` `turnContext.Activity.Value` `OnTeamsAppBasedLinkQueryAsync`в полезных данных или в зависимости от сценария, для которого вы включите единый вход:

    ```json
    JObject valueObject=JObject.FromObject(turnContext.Activity.Value);
    if(valueObject["authentication"] !=null)
     {
        JObject authenticationObject=JObject.FromObject(valueObject["authentication"]);
        if(authenticationObject["token"] !=null)
     }
    
     ```
  
    Если вы используете подключение OAuth, добавьте следующий код в файл TeamsMessagingExtensionsSearchAuthConfigBot.cs, чтобы обновить или добавить маркер в хранилище:

   ```C#
   protected override async Task<InvokeResponse> OnInvokeActivityAsync(ITurnContext<IInvokeActivity> turnContext, CancellationToken cancellationToken)
        {
            JObject valueObject = JObject.FromObject(turnContext.Activity.Value);
            if (valueObject["authentication"] != null)
            {
                JObject authenticationObject = JObject.FromObject(valueObject["authentication"]);
                if (authenticationObject["token"] != null)
                {
                    //If the token is NOT exchangeable, then return 412 to require user consent
                    if (await TokenIsExchangeable(turnContext, cancellationToken))
                    {
                        return await base.OnInvokeActivityAsync(turnContext, cancellationToken).ConfigureAwait(false);
                    }
                    else
                    {
                        var response = new InvokeResponse();
                        response.Status = 412;
                        return response;
                    }
                }
            }
            return await base.OnInvokeActivityAsync(turnContext, cancellationToken).ConfigureAwait(false);
        }
        private async Task<bool> TokenIsExchangeable(ITurnContext turnContext, CancellationToken cancellationToken)
        {
            TokenResponse tokenExchangeResponse = null;
            try
            {
                JObject valueObject = JObject.FromObject(turnContext.Activity.Value);
                var tokenExchangeRequest =
                ((JObject)valueObject["authentication"])?.ToObject<TokenExchangeInvokeRequest>();
                var userTokenClient = turnContext.TurnState.Get<UserTokenClient>();
                tokenExchangeResponse = await userTokenClient.ExchangeTokenAsync(
                                turnContext.Activity.From.Id,
                                 _connectionName,
                                 turnContext.Activity.ChannelId,
                                 new TokenExchangeRequest
                 {
                     Token = tokenExchangeRequest.Token,
                 },
                  cancellationToken).ConfigureAwait(false);
            }
    #pragma warning disable CA1031 //Do not catch general exception types (ignoring, see comment below)
            catch
    #pragma warning restore CA1031 //Do not catch general exception types
            {
                //ignore exceptions
                //if token exchange failed for any reason, tokenExchangeResponse above remains null, and a failure invoke response is sent to the caller.
                //This ensures the caller knows that the invoke has failed.
            }
            if (tokenExchangeResponse == null || string.IsNullOrEmpty(tokenExchangeResponse.Token))
            {
                return false;
            }
            return true;
        }
    
    ```

## <a name="code-sample"></a>Пример кода

В этом разделе приведен пример пакета SDK для проверки подлинности бота версии 3.

| **Название примера** | **Описание** | **.NET** | **Node.js** | **Python** |
|---------------|------------|------------|-------------|---------------|
| Проверка подлинности бота | В этом примере показано, как начать работу с проверкой подлинности в боте для Teams. | [Просмотр](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) | [Просмотр](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/46.teams-auth) |
| Вкладка, бот и расширение сообщений (ME) SSO | В этом примере показан единый вход для tab, Bot и ME — поиск, действие, распакуйте ссылку. |  [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/csharp) | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/nodejs) | Н/Д |
|Расширение Tab, Bot и Message| В этом примере показано, как проверить проверку подлинности в расширениях Bot, Tab и Message с помощью единого входа. | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-complete-auth/csharp) | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-complete-auth/nodejs) | Недоступно |

## <a name="see-also"></a>См. также

* [Добавление проверки подлинности в расширения для сообщений](add-authentication.md)
* [Использование SSO для ботов](../../bots/how-to/authentication/auth-aad-sso-bots.md)
* [Развертывание ссылки](link-unfurling.md)
