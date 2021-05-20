---
title: Поддержка SSO для расширений обмена сообщениями
author: KirtiPereira
description: Как включить поддержку SSO для расширений обмена сообщениями
localization_priority: Normal
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: 02d08506a07e955693531908f4f3cf16573a02c0
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566203"
---
# <a name="single-sign-on-sso-support-for-messaging-extensions"></a>Поддержка единого ва-г действия (SSO) для расширения обмена сообщениями
 
Единая поддержка вовсяка теперь доступна для расширения обмена сообщениями и разворачивания ссылок. Включение единого входа (SSO) для расширения обмена сообщениями безмолвно обновляет маркер аутентификации, что сводит к минимуму количество раз, необходимое для вобщения в учетные данные Microsoft Teams.

Этот документ поможет вам включить SSO и при необходимости хранить токен аутентификации.

## <a name="prerequisites"></a>Предварительные требования

Предпосылкой для включения SSO для расширения сообщений и разворачивания ссылок являются следующие:
* У вас должна быть [учетная запись Azure.](https://azure.microsoft.com/en-us/free/)
* Вы должны настроить приложение через портал AAD и обновить манифест Teams приложения для бота, как это определено в [регистрации приложения через портал AAD.](../../bots/how-to/authentication/auth-aad-sso-bots.md#register-your-app-through-the-aad-portal)

> [!NOTE]
> Для получения дополнительной информации о создании учетной записи Azure и обновлении манифеста приложения [см.](../../bots/how-to/authentication/auth-aad-sso-bots.md)

## <a name="enable-sso-for-messaging-extensions-and-link-unfurling"></a>Включить SSO для расширения обмена сообщениями и разворачивания ссылок

После завершения предварительных условий можно включить SSO для расширения обмена сообщениями и разворачивания ссылок.

**Включить SSO**
1. Обновите [данные о подключении ботов OAuth](../../bots/how-to/authentication/auth-aad-sso-bots.md#update-the-azure-portal-with-the-oauth-connection) на портале Azure.
2. Загрузите [образец расширений обмена сообщениями](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config) и следуйте инструкциям по настройке, предоставленным мастером.
   > [!NOTE]
   > Используйте соединение OAuth ботов при настройке расширений обмена сообщениями.
3. В [TeamsMessagingExtensionsSearchAuthConfigBot.cs](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config/Bots/TeamsMessagingExtensionsSearchAuthConfigBot.cs) файл, обновить значение *от аута* *до silentAuth* `OnTeamsMessagingExtensionQueryAsync` в и / или `OnTeamsAppBasedLinkQueryAsync` .  

    > [!NOTE]
    > Мы не поддерживаем других обработчиков SSO, за `OnTeamsMessagingExtensionQueryAsync` `OnTeamsAppBasedLinkQueryAsync` исключением и из файла TeamsMessagingExtensionsSearchAuthConfigBot.cs файл.
   
4. Вы получаете токен в `OnTeamsMessagingExtensionQueryAsync` обработчике в `turnContext.Activity.Value` полезной нагрузке или `OnTeamsAppBasedLinkQueryAsync` в, в зависимости от того, какой сценарий вы позволяете SSO для:

    ```json
    JObject valueObject=JObject.FromObject(turnContext.Activity.Value);
    if(valueObject["authentication"] !=null)
     {
        JObject authenticationObject=JObject.FromObject(valueObject["authentication"]);
        if(authenticationObject["token"] !=null)
     }
    
     ```
  
    Если вы используете OAuth соединение, добавьте следующий код в файл TeamsMessagingExtensionsSearchAuthConfigBot.cs для обновления или добавления токена в магазине:
    
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
                tokenExchangeResponse = await (turnContext.Adapter as IExtendedUserTokenProvider).ExchangeTokenAsync(
                 turnContext,
                 _connectionName,
                 turnContext.Activity.From.Id,
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

* [Добавление аутентификации в расширения обмена сообщениями](add-authentication.md)
* [Используйте SSO для ботов](../../bots/how-to/authentication/auth-aad-sso-bots.md)
* [Развертывание ссылки](link-unfurling.md)

