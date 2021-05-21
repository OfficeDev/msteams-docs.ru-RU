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
# <a name="single-sign-on-sso-support-for-messaging-extensions"></a><span data-ttu-id="4525b-103">Поддержка единой системы регистрации (SSO) для расширений обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="4525b-103">Single sign-on (SSO) support for messaging extensions</span></span>
 
<span data-ttu-id="4525b-104">Единая поддержка входов теперь доступна для расширения обмена сообщениями и разгрузки ссылок.</span><span class="sxs-lookup"><span data-stu-id="4525b-104">Single sign-on support is now available for messaging extensions and link unfurling.</span></span> <span data-ttu-id="4525b-105">Включение единого входа (SSO) для расширений обмена сообщениями безмолвно обновляет маркер проверки подлинности, что сводит к минимуму количество раз, необходимых для ввода входа в учетные данные для Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="4525b-105">Enabling Single sign-on (SSO) for messaging extensions silently refreshes the authentication token, which minimizes the number of times you need to enter your sign in credentials for Microsoft Teams.</span></span>

<span data-ttu-id="4525b-106">В этом документе вы можете узнать, как включить SSO и при необходимости сохранить маркер проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="4525b-106">This document guides you on how to enable the SSO and store your authentication token, if required.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4525b-107">Предварительные условия</span><span class="sxs-lookup"><span data-stu-id="4525b-107">Prerequisites</span></span>

<span data-ttu-id="4525b-108">Необходимое условие, чтобы включить SSO для расширения обмена сообщениями и разгрузки ссылок:</span><span class="sxs-lookup"><span data-stu-id="4525b-108">The prerequisite to enable SSO for messaging extensions and link unfurling are as follows:</span></span>
* <span data-ttu-id="4525b-109">У вас должна быть [учетная запись Azure.](https://azure.microsoft.com/en-us/free/)</span><span class="sxs-lookup"><span data-stu-id="4525b-109">You must have an [Azure](https://azure.microsoft.com/en-us/free/) account.</span></span>
* <span data-ttu-id="4525b-110">Необходимо настроить приложение через портал AAD и обновить манифест Teams для бота, как определено в регистрации приложения на портале [AAD.](../../bots/how-to/authentication/auth-aad-sso-bots.md#register-your-app-through-the-aad-portal)</span><span class="sxs-lookup"><span data-stu-id="4525b-110">You must configure your app through the AAD portal, and update your Teams application manifest for your bot as defined in [register your app through the AAD portal](../../bots/how-to/authentication/auth-aad-sso-bots.md#register-your-app-through-the-aad-portal).</span></span>

> [!NOTE]
> <span data-ttu-id="4525b-111">Дополнительные сведения о создании учетной записи Azure и обновлении манифеста приложения см. в документе Поддержка единого входного знака [(SSO) для ботов.](../../bots/how-to/authentication/auth-aad-sso-bots.md)</span><span class="sxs-lookup"><span data-stu-id="4525b-111">For more information on creating an Azure account and updating your app manifest, see [Single sign-on (SSO) support for bots](../../bots/how-to/authentication/auth-aad-sso-bots.md).</span></span>

## <a name="enable-sso-for-messaging-extensions-and-link-unfurling"></a><span data-ttu-id="4525b-112">Включить SSO для расширения обмена сообщениями и разгрузки ссылок</span><span class="sxs-lookup"><span data-stu-id="4525b-112">Enable SSO for messaging extensions and link unfurling</span></span>

<span data-ttu-id="4525b-113">После завершения необходимых условий можно включить SSO для расширения сообщений и разгрузку ссылок.</span><span class="sxs-lookup"><span data-stu-id="4525b-113">After the prerequisites are completed, you can enable SSO for messaging extensions and link unfurling.</span></span>

<span data-ttu-id="4525b-114">**Чтобы включить SSO**</span><span class="sxs-lookup"><span data-stu-id="4525b-114">**To enable SSO**</span></span>
1. <span data-ttu-id="4525b-115">Обновите сведения о подключении [ботов к OAuth](../../bots/how-to/authentication/auth-aad-sso-bots.md#update-the-azure-portal-with-the-oauth-connection) на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="4525b-115">Update your bots [OAuth connection](../../bots/how-to/authentication/auth-aad-sso-bots.md#update-the-azure-portal-with-the-oauth-connection) details in the Azure portal.</span></span>
2. <span data-ttu-id="4525b-116">Скачайте [пример расширений обмена сообщениями](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config) и следуйте инструкциям по настройке, предоставленным мастером.</span><span class="sxs-lookup"><span data-stu-id="4525b-116">Download the [messaging extensions sample](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config) and follow the setup instructions provided by the wizard.</span></span>
   > [!NOTE]
   > <span data-ttu-id="4525b-117">Использование подключения OAuth для ботов при настройке расширений обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="4525b-117">Use your bots OAuth connection when setting up your messaging extensions.</span></span>
3. <span data-ttu-id="4525b-118">В [файле TeamsMessagingExtensionsSearchAuthConfigBot.cs](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config/Bots/TeamsMessagingExtensionsSearchAuthConfigBot.cs) обновите значение от *auth* до *silentAuth* в `OnTeamsMessagingExtensionQueryAsync` файле and/or `OnTeamsAppBasedLinkQueryAsync` .</span><span class="sxs-lookup"><span data-stu-id="4525b-118">In the [TeamsMessagingExtensionsSearchAuthConfigBot.cs](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config/Bots/TeamsMessagingExtensionsSearchAuthConfigBot.cs) file, update the value from *auth* to *silentAuth* in the `OnTeamsMessagingExtensionQueryAsync` and / or `OnTeamsAppBasedLinkQueryAsync`.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="4525b-119">Мы не поддерживаем другие обработчики SSO, за исключением файла `OnTeamsMessagingExtensionQueryAsync` `OnTeamsAppBasedLinkQueryAsync` TeamsMessagingExtensionsSearchAuthConfigBot.cs.</span><span class="sxs-lookup"><span data-stu-id="4525b-119">We do not support other handlers SSO, except `OnTeamsMessagingExtensionQueryAsync` and `OnTeamsAppBasedLinkQueryAsync` from the TeamsMessagingExtensionsSearchAuthConfigBot.cs file.</span></span>
   
4. <span data-ttu-id="4525b-120">Вы получаете маркер в обработнике в полезной нагрузке или в зависимости от того, в какой сценарий вы включаете `OnTeamsMessagingExtensionQueryAsync` `turnContext.Activity.Value` `OnTeamsAppBasedLinkQueryAsync` SSO для:</span><span class="sxs-lookup"><span data-stu-id="4525b-120">You receive the token in `OnTeamsMessagingExtensionQueryAsync` handler in the `turnContext.Activity.Value` payload or in the `OnTeamsAppBasedLinkQueryAsync`, depending on which scenario you are enabling the SSO for:</span></span>

    ```json
    JObject valueObject=JObject.FromObject(turnContext.Activity.Value);
    if(valueObject["authentication"] !=null)
     {
        JObject authenticationObject=JObject.FromObject(valueObject["authentication"]);
        if(authenticationObject["token"] !=null)
     }
    
     ```
  
    <span data-ttu-id="4525b-121">Если вы используете подключение OAuth, добавьте следующий код в файл TeamsMessagingExtensionsSearchAuthConfigBot.cs для обновления или добавления маркера в магазине:</span><span class="sxs-lookup"><span data-stu-id="4525b-121">If you are using the OAuth connection, add the following code to the TeamsMessagingExtensionsSearchAuthConfigBot.cs file to update or add the token in the store:</span></span>
    
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

## <a name="see-also"></a><span data-ttu-id="4525b-122">См. также</span><span class="sxs-lookup"><span data-stu-id="4525b-122">See also</span></span>

* [<span data-ttu-id="4525b-123">Добавление проверки подлинности в расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="4525b-123">Add authentication to your messaging extensions</span></span>](add-authentication.md)
* [<span data-ttu-id="4525b-124">Использование SSO для ботов</span><span class="sxs-lookup"><span data-stu-id="4525b-124">Use SSO for bots</span></span>](../../bots/how-to/authentication/auth-aad-sso-bots.md)
* [<span data-ttu-id="4525b-125">Развертывание ссылки</span><span class="sxs-lookup"><span data-stu-id="4525b-125">Link unfurling</span></span>](link-unfurling.md)

