---
title: Поддержка SSO для расширений обмена сообщениями
author: KirtiPereira
description: Узнайте, как включить SSO-поддержку расширений обмена сообщениями с помощью примеров кода.
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: a0aaae8637a80dd2e6f48cf9ae3081b4e796824f
ms.sourcegitcommit: c66da76fb766df6270095265e1da8c49a3afd195
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/07/2022
ms.locfileid: "62435700"
---
# <a name="single-sign-on-support-for-messaging-extensions"></a>Поддержка единого входного знака для расширений обмена сообщениями
 
Поддержка единого входного (SSO) теперь доступна для расширений обмена сообщениями и разгрузки ссылок. Включение единого входа для расширений обмена сообщениями по умолчанию обновляет маркер проверки подлинности, что минимизирует количество раз, необходимых для ввода входа в учетные данные для Microsoft Teams.

В этом документе вы можете узнать, как включить SSO и при необходимости сохранить маркер проверки подлинности.

## <a name="prerequisites"></a>Предварительные требования

Необходимое условие, чтобы включить SSO для расширения обмена сообщениями и разгрузки ссылок:

* У вас должна быть [учетная запись Azure](https://azure.microsoft.com/free/) .
* Необходимо настроить приложение на портале Azure AD и обновить Teams, как определено в регистрации приложения на [портале Azure AD](../../bots/how-to/authentication/auth-aad-sso-bots.md#register-your-app-through-the-azure-ad-portal).

> [!NOTE]
> Дополнительные сведения о создании учетной записи Azure и обновлении манифеста приложения см. в документе Поддержка единого входного знака [(SSO) для ботов](../../bots/how-to/authentication/auth-aad-sso-bots.md).

## <a name="enable-sso-for-messaging-extensions-and-link-unfurling"></a>Включить SSO для расширения обмена сообщениями и разгрузки ссылок

После завершения необходимых условий можно включить SSO для расширения сообщений и разгрузку ссылок.

**Чтобы включить SSO**
1. Обновите сведения о подключении [ботов к OAuth](../../bots/how-to/authentication/auth-aad-sso-bots.md#update-the-azure-portal-with-the-oauth-connection) на Microsoft Azure портале.
2. Скачайте [пример расширений обмена сообщениями](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config) и следуйте инструкциям по настройке, предоставленным мастером.
   > [!NOTE]
   > Использование подключения OAuth для ботов при настройке расширений обмена сообщениями.
3. В [файле TeamsMessagingExtensionsSearchAuthConfigBot.cs](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config/Bots/TeamsMessagingExtensionsSearchAuthConfigBot.cs) обновите значение от *auth* до *silentAuth* `OnTeamsMessagingExtensionQueryAsync` в файле and/or `OnTeamsAppBasedLinkQueryAsync`.  

    > [!NOTE]
    > Мы не поддерживаем другие обработчики SSO, `OnTeamsMessagingExtensionQueryAsync` `OnTeamsAppBasedLinkQueryAsync` за исключением файла TeamsMessagingExtensionsSearchAuthConfigBot.cs.
   
4. Вы получаете маркер в `OnTeamsMessagingExtensionQueryAsync` обработнике `turnContext.Activity.Value` `OnTeamsAppBasedLinkQueryAsync`в полезной нагрузке или в зависимости от того, в какой сценарий вы включаете SSO для:

    ```json
    JObject valueObject=JObject.FromObject(turnContext.Activity.Value);
    if(valueObject["authentication"] !=null)
     {
        JObject authenticationObject=JObject.FromObject(valueObject["authentication"]);
        if(authenticationObject["token"] !=null)
     }
    
     ```
  
    Если вы используете подключение OAuth, добавьте следующий код в файл TeamsMessagingExtensionsSearchAuthConfigBot.cs для обновления или добавления маркера в магазине:
    
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

## <a name="see-also"></a>См. также

* [Добавление проверки подлинности в расширения обмена сообщениями](add-authentication.md)
* [Использование SSO для ботов](../../bots/how-to/authentication/auth-aad-sso-bots.md)
* [Развертывание ссылки](link-unfurling.md)
