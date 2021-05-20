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
# <a name="single-sign-on-sso-support-for-messaging-extensions"></a><span data-ttu-id="6e6a2-103">Поддержка единого ва-г действия (SSO) для расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="6e6a2-103">Single sign-on (SSO) support for messaging extensions</span></span>
 
<span data-ttu-id="6e6a2-104">Единая поддержка вовсяка теперь доступна для расширения обмена сообщениями и разворачивания ссылок.</span><span class="sxs-lookup"><span data-stu-id="6e6a2-104">Single sign-on support is now available for messaging extensions and link unfurling.</span></span> <span data-ttu-id="6e6a2-105">Включение единого входа (SSO) для расширения обмена сообщениями безмолвно обновляет маркер аутентификации, что сводит к минимуму количество раз, необходимое для вобщения в учетные данные Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="6e6a2-105">Enabling Single sign-on (SSO) for messaging extensions silently refreshes the authentication token, which minimizes the number of times you need to enter your sign in credentials for Microsoft Teams.</span></span>

<span data-ttu-id="6e6a2-106">Этот документ поможет вам включить SSO и при необходимости хранить токен аутентификации.</span><span class="sxs-lookup"><span data-stu-id="6e6a2-106">This document guides you on how to enable the SSO and store your authentication token, if required.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6e6a2-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6e6a2-107">Prerequisites</span></span>

<span data-ttu-id="6e6a2-108">Предпосылкой для включения SSO для расширения сообщений и разворачивания ссылок являются следующие:</span><span class="sxs-lookup"><span data-stu-id="6e6a2-108">The prerequisite to enable SSO for messaging extensions and link unfurling are as follows:</span></span>
* <span data-ttu-id="6e6a2-109">У вас должна быть [учетная запись Azure.](https://azure.microsoft.com/en-us/free/)</span><span class="sxs-lookup"><span data-stu-id="6e6a2-109">You must have an [Azure](https://azure.microsoft.com/en-us/free/) account.</span></span>
* <span data-ttu-id="6e6a2-110">Вы должны настроить приложение через портал AAD и обновить манифест Teams приложения для бота, как это определено в [регистрации приложения через портал AAD.](../../bots/how-to/authentication/auth-aad-sso-bots.md#register-your-app-through-the-aad-portal)</span><span class="sxs-lookup"><span data-stu-id="6e6a2-110">You must configure your app through the AAD portal, and update your Teams application manifest for your bot as defined in [register your app through the AAD portal](../../bots/how-to/authentication/auth-aad-sso-bots.md#register-your-app-through-the-aad-portal).</span></span>

> [!NOTE]
> <span data-ttu-id="6e6a2-111">Для получения дополнительной информации о создании учетной записи Azure и обновлении манифеста приложения [см.](../../bots/how-to/authentication/auth-aad-sso-bots.md)</span><span class="sxs-lookup"><span data-stu-id="6e6a2-111">For more information on creating an Azure account and updating your app manifest, see [Single sign-on (SSO) support for bots](../../bots/how-to/authentication/auth-aad-sso-bots.md).</span></span>

## <a name="enable-sso-for-messaging-extensions-and-link-unfurling"></a><span data-ttu-id="6e6a2-112">Включить SSO для расширения обмена сообщениями и разворачивания ссылок</span><span class="sxs-lookup"><span data-stu-id="6e6a2-112">Enable SSO for messaging extensions and link unfurling</span></span>

<span data-ttu-id="6e6a2-113">После завершения предварительных условий можно включить SSO для расширения обмена сообщениями и разворачивания ссылок.</span><span class="sxs-lookup"><span data-stu-id="6e6a2-113">After the prerequisites are completed, you can enable SSO for messaging extensions and link unfurling.</span></span>

<span data-ttu-id="6e6a2-114">**Включить SSO**</span><span class="sxs-lookup"><span data-stu-id="6e6a2-114">**To enable SSO**</span></span>
1. <span data-ttu-id="6e6a2-115">Обновите [данные о подключении ботов OAuth](../../bots/how-to/authentication/auth-aad-sso-bots.md#update-the-azure-portal-with-the-oauth-connection) на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="6e6a2-115">Update your bots [OAuth connection](../../bots/how-to/authentication/auth-aad-sso-bots.md#update-the-azure-portal-with-the-oauth-connection) details in the Azure portal.</span></span>
2. <span data-ttu-id="6e6a2-116">Загрузите [образец расширений обмена сообщениями](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config) и следуйте инструкциям по настройке, предоставленным мастером.</span><span class="sxs-lookup"><span data-stu-id="6e6a2-116">Download the [messaging extensions sample](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config) and follow the setup instructions provided by the wizard.</span></span>
   > [!NOTE]
   > <span data-ttu-id="6e6a2-117">Используйте соединение OAuth ботов при настройке расширений обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="6e6a2-117">Use your bots OAuth connection when setting up your messaging extensions.</span></span>
3. <span data-ttu-id="6e6a2-118">В [TeamsMessagingExtensionsSearchAuthConfigBot.cs](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config/Bots/TeamsMessagingExtensionsSearchAuthConfigBot.cs) файл, обновить значение *от аута* *до silentAuth* `OnTeamsMessagingExtensionQueryAsync` в и / или `OnTeamsAppBasedLinkQueryAsync` .</span><span class="sxs-lookup"><span data-stu-id="6e6a2-118">In the [TeamsMessagingExtensionsSearchAuthConfigBot.cs](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config/Bots/TeamsMessagingExtensionsSearchAuthConfigBot.cs) file, update the value from *auth* to *silentAuth* in the `OnTeamsMessagingExtensionQueryAsync` and / or `OnTeamsAppBasedLinkQueryAsync`.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="6e6a2-119">Мы не поддерживаем других обработчиков SSO, за `OnTeamsMessagingExtensionQueryAsync` `OnTeamsAppBasedLinkQueryAsync` исключением и из файла TeamsMessagingExtensionsSearchAuthConfigBot.cs файл.</span><span class="sxs-lookup"><span data-stu-id="6e6a2-119">We do not support other handlers SSO, except `OnTeamsMessagingExtensionQueryAsync` and `OnTeamsAppBasedLinkQueryAsync` from the TeamsMessagingExtensionsSearchAuthConfigBot.cs file.</span></span>
   
4. <span data-ttu-id="6e6a2-120">Вы получаете токен в `OnTeamsMessagingExtensionQueryAsync` обработчике в `turnContext.Activity.Value` полезной нагрузке или `OnTeamsAppBasedLinkQueryAsync` в, в зависимости от того, какой сценарий вы позволяете SSO для:</span><span class="sxs-lookup"><span data-stu-id="6e6a2-120">You receive the token in `OnTeamsMessagingExtensionQueryAsync` handler in the `turnContext.Activity.Value` payload or in the `OnTeamsAppBasedLinkQueryAsync`, depending on which scenario you are enabling the SSO for:</span></span>

    ```json
    JObject valueObject=JObject.FromObject(turnContext.Activity.Value);
    if(valueObject["authentication"] !=null)
     {
        JObject authenticationObject=JObject.FromObject(valueObject["authentication"]);
        if(authenticationObject["token"] !=null)
     }
    
     ```
  
    <span data-ttu-id="6e6a2-121">Если вы используете OAuth соединение, добавьте следующий код в файл TeamsMessagingExtensionsSearchAuthConfigBot.cs для обновления или добавления токена в магазине:</span><span class="sxs-lookup"><span data-stu-id="6e6a2-121">If you are using the OAuth connection, add the following code to the TeamsMessagingExtensionsSearchAuthConfigBot.cs file to update or add the token in the store:</span></span>
    
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

## <a name="see-also"></a><span data-ttu-id="6e6a2-122">См. также</span><span class="sxs-lookup"><span data-stu-id="6e6a2-122">See also</span></span>

* [<span data-ttu-id="6e6a2-123">Добавление аутентификации в расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="6e6a2-123">Add authentication to your messaging extensions</span></span>](add-authentication.md)
* [<span data-ttu-id="6e6a2-124">Используйте SSO для ботов</span><span class="sxs-lookup"><span data-stu-id="6e6a2-124">Use SSO for bots</span></span>](../../bots/how-to/authentication/auth-aad-sso-bots.md)
* [<span data-ttu-id="6e6a2-125">Развертывание ссылки</span><span class="sxs-lookup"><span data-stu-id="6e6a2-125">Link unfurling</span></span>](link-unfurling.md)

