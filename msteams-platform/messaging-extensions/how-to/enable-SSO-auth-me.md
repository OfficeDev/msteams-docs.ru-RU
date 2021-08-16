---
title: Поддержка SSO для расширений обмена сообщениями
author: KirtiPereira
description: Как включить поддержку SSO для расширений обмена сообщениями
localization_priority: Normal
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: 656c17612c74ee55b870fd2e7e13dea60e6ed2f8
ms.sourcegitcommit: 2c4c77dc8344f2fab8ed7a3f7155f15f0dd6a5ce
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/13/2021
ms.locfileid: "58345243"
---
# <a name="single-sign-on-sso-support-for-messaging-extensions"></a>Поддержка единой системы регистрации (SSO) для расширений обмена сообщениями
 
Единая поддержка входов теперь доступна для расширения обмена сообщениями и разгрузки ссылок. Включение единого входа (SSO) для расширений обмена сообщениями безмолвно обновляет маркер проверки подлинности, что сводит к минимуму количество раз, необходимых для ввода входа в учетные данные для Microsoft Teams.

В этом документе вы можете узнать, как включить SSO и при необходимости сохранить маркер проверки подлинности.

## <a name="prerequisites"></a>Требования

Необходимое условие, чтобы включить SSO для расширения обмена сообщениями и разгрузки ссылок:
* У вас должна быть [учетная запись Azure.](https://azure.microsoft.com/free/)
* Необходимо настроить приложение через портал AAD и обновить манифест Teams для бота, как определено в регистрации приложения на портале [AAD.](../../bots/how-to/authentication/auth-aad-sso-bots.md#register-your-app-through-the-aad-portal)

> [!NOTE]
> Дополнительные сведения о создании учетной записи Azure и обновлении манифеста приложения см. в документе Поддержка единого входного знака [(SSO) для ботов.](../../bots/how-to/authentication/auth-aad-sso-bots.md)

## <a name="enable-sso-for-messaging-extensions-and-link-unfurling"></a>Включить SSO для расширения обмена сообщениями и разгрузки ссылок

После завершения необходимых условий можно включить SSO для расширения сообщений и разгрузку ссылок.

**Чтобы включить SSO**
1. Обновите сведения о подключении [ботов к OAuth](../../bots/how-to/authentication/auth-aad-sso-bots.md#update-the-azure-portal-with-the-oauth-connection) на портале Azure.
2. Скачайте [пример расширений обмена сообщениями](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config) и следуйте инструкциям по настройке, предоставленным мастером.
   > [!NOTE]
   > Использование подключения OAuth для ботов при настройке расширений обмена сообщениями.
3. В [файле TeamsMessagingExtensionsSearchAuthConfigBot.cs](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config/Bots/TeamsMessagingExtensionsSearchAuthConfigBot.cs) обновите значение от *auth* до *silentAuth* в `OnTeamsMessagingExtensionQueryAsync` файле and/or `OnTeamsAppBasedLinkQueryAsync` .  

    > [!NOTE]
    > Мы не поддерживаем другие обработчики SSO, за исключением файла `OnTeamsMessagingExtensionQueryAsync` `OnTeamsAppBasedLinkQueryAsync` TeamsMessagingExtensionsSearchAuthConfigBot.cs.
   
4. Вы получаете маркер в обработнике в полезной нагрузке или в зависимости от того, в какой сценарий вы включаете `OnTeamsMessagingExtensionQueryAsync` `turnContext.Activity.Value` `OnTeamsAppBasedLinkQueryAsync` SSO для:

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

* [Добавление проверки подлинности в расширения обмена сообщениями](add-authentication.md)
* [Использование SSO для ботов](../../bots/how-to/authentication/auth-aad-sso-bots.md)
* [Развертывание ссылки](link-unfurling.md)

