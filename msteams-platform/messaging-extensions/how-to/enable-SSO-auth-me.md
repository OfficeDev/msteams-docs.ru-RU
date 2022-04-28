---
title: Поддержка единого входа для расширений сообщений
author: KirtiPereira
description: Узнайте, как включить поддержку единого входа для расширений сообщений с помощью примеров кода.
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: 4ee49b349d287325bb029aa155a61219a8656e22
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104394"
---
# <a name="single-sign-on-support-for-message-extensions"></a>Поддержка единого входа для расширений сообщений

Поддержка единого входа (SSO) теперь доступна для расширений сообщений и удаления ссылок. При включении единого входа для расширений сообщений по умолчанию обновляется маркер проверки подлинности, что сводит к минимуму количество попыток ввода учетных данных для входа Microsoft Teams.

В этом документе описывается, как включить единый вход и при необходимости сохранить маркер проверки подлинности.

## <a name="prerequisites"></a>Предварительные требования

Ниже приведены предварительные требования для включения единого входа для расширений сообщений и отмены ссылок.

* У вас должна быть [учетная запись Azure](https://azure.microsoft.com/free/) .
* Необходимо настроить приложение с помощью портала Azure AD и обновить Teams манифест приложения, как определено при регистрации приложения на [портале Azure AD](../../bots/how-to/authentication/auth-aad-sso-bots.md#register-your-app-through-the-azure-ad-portal).

> [!NOTE]
> Дополнительные сведения о создании учетной записи Azure и обновлении манифеста приложения см. в разделе о поддержке единого входа [для ботов](../../bots/how-to/authentication/auth-aad-sso-bots.md).

## <a name="enable-sso-for-message-extensions-and-link-unfurling"></a>Включение единого входа для расширений сообщений и отмена ссылки

После выполнения предварительных условий можно включить единый вход для расширений сообщений и удалить ссылку.

Чтобы включить единый вход:

1. Обновите сведения о подключении [OAuth](../../bots/how-to/authentication/auth-aad-sso-bots.md#update-the-azure-portal-with-the-oauth-connection) ботов на Microsoft Azure портале.
2. Скачайте [пример расширений сообщений](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config) и следуйте инструкциям по настройке, предоставленным мастером.
   > [!NOTE]
   > Используйте подключение OAuth ботов при настройке расширений сообщений.
3. В [файле TeamsMessagingExtensionsSearchAuthConfigBot.cs](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config/Bots/TeamsMessagingExtensionsSearchAuthConfigBot.cs) измените значение с проверки подлинности на *silentAuth* `OnTeamsMessagingExtensionQueryAsync` в и /или `OnTeamsAppBasedLinkQueryAsync`.  

    > [!NOTE]
    > Мы не поддерживаем единый вход других обработчиков, `OnTeamsMessagingExtensionQueryAsync` `OnTeamsAppBasedLinkQueryAsync` за исключением файла TeamsMessagingExtensionsSearchAuthConfigBot.cs и из файла TeamsMessagingExtensionsAuthConfigBot.cs.

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

## <a name="see-also"></a>См. также

* [Добавление проверки подлинности в расширения сообщений](add-authentication.md)
* [Использование единого входа для ботов](../../bots/how-to/authentication/auth-aad-sso-bots.md)
* [Развертывание ссылки](link-unfurling.md)
