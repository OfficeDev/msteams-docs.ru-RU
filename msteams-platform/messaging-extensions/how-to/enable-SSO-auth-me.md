---
title: Поддержка SSO в расширениях для сообщений
author: KirtiPereira
description: Узнайте, как включить поддержку SSO расширениям для обмена сообщениями с помощью примеров кода.
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: bba2a8a225a75c21c46a242dec8acc55dcc0e8b5
ms.sourcegitcommit: 430bf416bb8d1b74f926c8b5d5ffd3dbb0782286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/10/2022
ms.locfileid: "65296947"
---
# <a name="single-sign-on-support-for-message-extensions"></a>Поддержка единого входов у расширений для сообщений

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

4. Вы получаете маркер в обработчике `OnTeamsMessagingExtensionQueryAsync` в полезных данных `turnContext.Activity.Value` или в `OnTeamsAppBasedLinkQueryAsync`, в зависимости от того, для какого сценария вы включаете SSO.

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

## <a name="see-also"></a>Дополнительные ресурсы

* [Добавление проверки подлинности в расширения для сообщений](add-authentication.md)
* [Использование SSO для ботов](../../bots/how-to/authentication/auth-aad-sso-bots.md)
* [Развертывание ссылки](link-unfurling.md)
