---
title: Уведомления о входящих звонках
description: Подробные технические сведения об обработке уведомлений от входящих вызовов
ms.topic: conceptual
localization_priority: Normal
keywords: близость области вызовов вызовов уведомлений о вызове
ms.date: 04/02/2019
ms.openlocfilehash: 06068c13d27598b9a7b5e70181c69f9efb2c0afb
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020178"
---
# <a name="incoming-call-notifications"></a><span data-ttu-id="86b7f-104">Уведомления о входящих звонках</span><span class="sxs-lookup"><span data-stu-id="86b7f-104">Incoming call notifications</span></span>

<span data-ttu-id="86b7f-105">При [регистрации бота](./registering-calling-bot.md#create-new-bot-or-add-calling-capabilities)вызовов и собраний для Microsoft Teams указан веб-сайт для вызова URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="86b7f-105">In [registering a calls and meetings bot for Microsoft Teams](./registering-calling-bot.md#create-new-bot-or-add-calling-capabilities), the Webhook for calling URL is mentioned.</span></span> <span data-ttu-id="86b7f-106">Этот URL-адрес является конечной точкой веб-адреса для всех входящих звонков в бот.</span><span class="sxs-lookup"><span data-stu-id="86b7f-106">This URL is the webhook endpoint for all incoming calls to your bot.</span></span>

## <a name="protocol-determination"></a><span data-ttu-id="86b7f-107">Определение протокола</span><span class="sxs-lookup"><span data-stu-id="86b7f-107">Protocol determination</span></span>

<span data-ttu-id="86b7f-108">Входящие уведомления предоставляются в устаревшем формате для совместимости с предыдущим протоколом [Skype.](/azure/bot-service/dotnet/bot-builder-dotnet-real-time-media-concepts?view=azure-bot-service-3.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="86b7f-108">The incoming notification is provided in a legacy format for compatibility with the previous [Skype protocol](/azure/bot-service/dotnet/bot-builder-dotnet-real-time-media-concepts?view=azure-bot-service-3.0&preserve-view=true).</span></span> <span data-ttu-id="86b7f-109">Чтобы преобразовать вызов в протокол Microsoft Graph, бот должен определить, находится ли уведомление в устаревшем формате, и предоставить следующий ответ:</span><span class="sxs-lookup"><span data-stu-id="86b7f-109">In order to convert the call to the Microsoft Graph protocol, your bot must determine whether the notification is in a legacy format and provide the following response:</span></span>

```http
HTTP/1.1 204 No Content
```

<span data-ttu-id="86b7f-110">Бот получает уведомление снова, но на этот раз в протоколе Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="86b7f-110">Your bot receives the notification again, but this time in the Microsoft Graph protocol.</span></span>

<span data-ttu-id="86b7f-111">В будущем выпуске медиаплатформы в режиме реального времени можно настроить протокол, поддерживаемый вашим приложением, чтобы избежать первоначального вызова в устаревшем формате.</span><span class="sxs-lookup"><span data-stu-id="86b7f-111">In a future release of the Real-time Media Platform, you can configure the protocol your application supports to avoid receiving the initial callback in the legacy format.</span></span>

<span data-ttu-id="86b7f-112">В следующем разделе приводится подробная информация о входящих уведомлениях о вызове, перенаправленных для сродства региона к развертыванию.</span><span class="sxs-lookup"><span data-stu-id="86b7f-112">The next section provides details on incoming call notifications redirected for region affinity to your deployment.</span></span>

## <a name="redirects-for-region-affinity"></a><span data-ttu-id="86b7f-113">Перенаправления для сродства регионов</span><span class="sxs-lookup"><span data-stu-id="86b7f-113">Redirects for region affinity</span></span>

<span data-ttu-id="86b7f-114">Вы звоните на веб-сайт из центра обработки данных, где размещен вызов.</span><span class="sxs-lookup"><span data-stu-id="86b7f-114">You call your webhook from the data-center hosting the call.</span></span> <span data-ttu-id="86b7f-115">Вызов запускается в любом центре обработки данных и не учитывает особенности региона.</span><span class="sxs-lookup"><span data-stu-id="86b7f-115">The call starts in any data center and does not take into account region affinities.</span></span> <span data-ttu-id="86b7f-116">Уведомление отправляется в развертывание в зависимости от разрешения GeoDNS.</span><span class="sxs-lookup"><span data-stu-id="86b7f-116">The notification is sent to your deployment depending on the GeoDNS resolution.</span></span> <span data-ttu-id="86b7f-117">Если ваше приложение определяет, проверяя начальную нагрузку уведомления или иным образом, что оно должно выполнить в другом развертывании, приложение предоставляет следующий ответ:</span><span class="sxs-lookup"><span data-stu-id="86b7f-117">If your application determines, by inspecting the initial notification payload or otherwise, that it needs to run in a different deployment, the application provides the following response:</span></span>

```http
HTTP/1.1 302 Found
Location: your-new-location
```

<span data-ttu-id="86b7f-118">Уделите боту ответ на входящий вызов с [помощью](https://developer.microsoft.com/graph/docs/api-reference/beta/api/call_answer) API ответа.</span><span class="sxs-lookup"><span data-stu-id="86b7f-118">Enable your bot to answer an incoming call using the [answer](https://developer.microsoft.com/graph/docs/api-reference/beta/api/call_answer) API.</span></span> <span data-ttu-id="86b7f-119">Вы можете указать `callbackUri` для обработки этого конкретного вызова.</span><span class="sxs-lookup"><span data-stu-id="86b7f-119">You can specify the `callbackUri` to handle this particular call.</span></span> <span data-ttu-id="86b7f-120">Это полезно для тех случаев, когда вызов обрабатывается определенным разделом, и эту информацию необходимо встраить в маршрутную маршрутику в `callbackUri` нужный экземпляр.</span><span class="sxs-lookup"><span data-stu-id="86b7f-120">This is useful for stateful instances where your call is handled by a particular partition, and you want to embed this information in the `callbackUri` for routing to the right instance.</span></span>

<span data-ttu-id="86b7f-121">В следующем разделе приводится подробная информация о проверке подлинности вызова путем проверки маркера, размещенного на веб-сайте.</span><span class="sxs-lookup"><span data-stu-id="86b7f-121">The next section provides details on authenticating the callback by inspecting the token posted to your webhook.</span></span>

## <a name="authenticate-the-callback"></a><span data-ttu-id="86b7f-122">Проверка подлинности вызова</span><span class="sxs-lookup"><span data-stu-id="86b7f-122">Authenticate the callback</span></span>

<span data-ttu-id="86b7f-123">Для проверки запроса бот должен проверить маркер, который был размещен на веб-сайте.</span><span class="sxs-lookup"><span data-stu-id="86b7f-123">Your bot must inspect the token posted to your webhook to validate the request.</span></span> <span data-ttu-id="86b7f-124">Каждый раз, когда API публикуется на веб-сайте, сообщение HTTP POST содержит маркер OAuth в заголовке авторизации в качестве маркера носители, а аудитория — в качестве ID приложения.</span><span class="sxs-lookup"><span data-stu-id="86b7f-124">Every time the API posts to the webhook, the HTTP POST message contains an OAuth token in the Authorization header as a bearer token, with the audience as your application's App ID.</span></span>

<span data-ttu-id="86b7f-125">Ваше приложение должно проверить этот маркер, прежде чем принимать запрос на вызов.</span><span class="sxs-lookup"><span data-stu-id="86b7f-125">Your application must validate this token before accepting the callback request.</span></span>

<span data-ttu-id="86b7f-126">Для проверки подлинности вызова используется следующий пример кода:</span><span class="sxs-lookup"><span data-stu-id="86b7f-126">The following sample code is used to authenticate the callback:</span></span>

```http
POST https://bot.contoso.com/api/calls
Content-Type: application/json
Authentication: Bearer <TOKEN>

"value": [
    "subscriptionId": "2887CEE8344B47C291F1AF628599A93C",
    "subscriptionExpirationDateTime": "2016-11-20T18:23:45.9356913Z",
    "changeType": "updated",
    "resource": "/app/calls/8A934F51F25B4EE19613D4049491857B",
    "resourceData": {
        "@odata.type": "#microsoft.graph.call",
        "state": "Established"
    }
]
```

<span data-ttu-id="86b7f-127">Маркер OAuth имеет следующие значения и подписывается Skype:</span><span class="sxs-lookup"><span data-stu-id="86b7f-127">The OAuth token has the following values, and is signed by Skype:</span></span>

```json
{
    "aud": "0efc74f7-41c3-47a4-8775-7259bfef4241",
    "iss": "https://api.botframework.com",
    "iat": 1466741440,
    "nbf": 1466741440,
    "exp": 1466745340,
    "tid": "1fdd12d0-4620-44ed-baec-459b611f84b2"
}
```

<span data-ttu-id="86b7f-128">Конфигурация OpenID, опубликованная на сайте, <https://api.aps.skype.com/v1/.well-known/OpenIdConfiguration> может использоваться для проверки маркера.</span><span class="sxs-lookup"><span data-stu-id="86b7f-128">The OpenID configuration published at <https://api.aps.skype.com/v1/.well-known/OpenIdConfiguration> can be used to verify the token.</span></span> <span data-ttu-id="86b7f-129">Каждое значение маркера OAuth используется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="86b7f-129">Each OAuth token value is used as follows:</span></span>

* <span data-ttu-id="86b7f-130">`aud` где аудитория — это URI ID приложения, заданный для приложения.</span><span class="sxs-lookup"><span data-stu-id="86b7f-130">`aud` where audience is the App ID URI specified for the application.</span></span>
* <span data-ttu-id="86b7f-131">`tid` является id клиента для Contoso.com.</span><span class="sxs-lookup"><span data-stu-id="86b7f-131">`tid` is the tenant id for Contoso.com.</span></span>
* <span data-ttu-id="86b7f-132">`iss` является эмитентом `https://api.botframework.com` маркеров.</span><span class="sxs-lookup"><span data-stu-id="86b7f-132">`iss` is the token issuer, `https://api.botframework.com`.</span></span>

<span data-ttu-id="86b7f-133">Для обработки кода веб-сайт должен проверить маркер, убедиться, что он не истек, и проверить, был ли он подписан опубликованной конфигурацией OpenID.</span><span class="sxs-lookup"><span data-stu-id="86b7f-133">For your code handling, the webhook must validate the token, ensure it has not expired, and check whether it has been signed by the published OpenID configuration.</span></span> <span data-ttu-id="86b7f-134">Кроме того, перед принятием запроса на вызов необходимо проверить, соответствует ли aud вашему ID приложения.</span><span class="sxs-lookup"><span data-stu-id="86b7f-134">You must also check whether aud matches your App ID before accepting the callback request.</span></span>

<span data-ttu-id="86b7f-135">Дополнительные сведения см. в [ссылке проверка входящие запросы.](https://github.com/microsoftgraph/microsoft-graph-comms-samples/blob/master/Samples/Common/Sample.Common/Authentication/AuthenticationProvider.cs)</span><span class="sxs-lookup"><span data-stu-id="86b7f-135">For more information, see [validate inbound requests](https://github.com/microsoftgraph/microsoft-graph-comms-samples/blob/master/Samples/Common/Sample.Common/Authentication/AuthenticationProvider.cs).</span></span>

## <a name="next-step"></a><span data-ttu-id="86b7f-136">Следующий этап</span><span class="sxs-lookup"><span data-stu-id="86b7f-136">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="86b7f-137">Требования и соображения к медийным ботам с хостингом приложений</span><span class="sxs-lookup"><span data-stu-id="86b7f-137">Requirements and considerations for application-hosted media bots</span></span>](~/bots/calls-and-meetings/requirements-considerations-application-hosted-media-bots.md)
