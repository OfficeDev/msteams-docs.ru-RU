---
title: Технические подробности об обработке уведомлений о входящем звонке
description: Подробная техническая информация об обработке уведомлений от входящих вызовов
keywords: сопоставление для уведомлений о вызовах в области обратного вызова
ms.date: 04/02/2019
ms.openlocfilehash: be8860ff70cd7dff4fd9599079ea7aab4f454174
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675587"
---
# <a name="incoming-call-notifications-technical-details"></a><span data-ttu-id="7f337-104">Уведомления о входящем звонке: технические сведения</span><span class="sxs-lookup"><span data-stu-id="7f337-104">Incoming call notifications: technical details</span></span>

<span data-ttu-id="7f337-105">В процессе [регистрации абонента и приглашения на собрание для Microsoft Teams](./registering-calling-bot.md#creating-a-new-bot-or-adding-calling-capabilities-to-an-existing-bot)мы упомянули URL-адрес веб-перехватчика **(для вызова)** — конечная точка веб-перехватчика для всех входящих вызовов в Bot.</span><span class="sxs-lookup"><span data-stu-id="7f337-105">In [Registering a calling and meeting bot for Microsoft Teams](./registering-calling-bot.md#creating-a-new-bot-or-adding-calling-capabilities-to-an-existing-bot), we mentioned the **Webhook (for calling)** URL — the webhook endpoint for all incoming calls to your bot.</span></span> <span data-ttu-id="7f337-106">В этом разделе обсуждаются технические сведения, которые необходимо ответить на эти уведомления.</span><span class="sxs-lookup"><span data-stu-id="7f337-106">This topic discusses the technical details you'll need to respond to these notifications.</span></span>

## <a name="protocol-determination"></a><span data-ttu-id="7f337-107">Определение протокола</span><span class="sxs-lookup"><span data-stu-id="7f337-107">Protocol determination</span></span>

<span data-ttu-id="7f337-108">Входящее уведомление предоставляется в устаревшем формате для совместимости с предыдущим [протоколом Skype](/azure/bot-service/dotnet/bot-builder-dotnet-real-time-media-concepts?view=azure-bot-service-3.0).</span><span class="sxs-lookup"><span data-stu-id="7f337-108">The incoming notification is provided in legacy format for compatibility with the previous [Skype protocol](/azure/bot-service/dotnet/bot-builder-dotnet-real-time-media-concepts?view=azure-bot-service-3.0).</span></span> <span data-ttu-id="7f337-109">Чтобы преобразовать вызов в протокол Microsoft Graph, ваш Bot должен определить, находится ли уведомление в устаревшем формате и ответить:</span><span class="sxs-lookup"><span data-stu-id="7f337-109">In order to convert the call to the Microsoft Graph protocol, your bot must determine whether the notification is in legacy format and reply with:</span></span>

```http
HTTP/1.1 204 No Content
```

<span data-ttu-id="7f337-110">Ваш робот снова получит уведомление, но на этот раз в протоколе Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="7f337-110">Your bot will receive the notification again, but this time in the Microsoft Graph protocol.</span></span>

<span data-ttu-id="7f337-111">В будущих выпусках мультимедийной платформы реального времени мы разберем, как настроить протокол, поддерживаемый приложением, чтобы избежать получения исходного обратного вызова в устаревшем формате.</span><span class="sxs-lookup"><span data-stu-id="7f337-111">In a future release of the Real-time Media Platform, we'll allow you to configure the protocol your application supports to avoid receiving the initial callback in the legacy format.</span></span>

## <a name="redirects-for-region-affinity"></a><span data-ttu-id="7f337-112">Перенаправление для сходства региона</span><span class="sxs-lookup"><span data-stu-id="7f337-112">Redirects for region affinity</span></span>

<span data-ttu-id="7f337-113">Вы назовите свой веб-перехватчик из центра обработки данных, в котором размещен вызов.</span><span class="sxs-lookup"><span data-stu-id="7f337-113">You'll call your webhook from the data-center hosting the call.</span></span> <span data-ttu-id="7f337-114">Вызов может начаться в любом центре обработки данных и не потребует сходства с областями счетов.</span><span class="sxs-lookup"><span data-stu-id="7f337-114">The call may start in any data center and doesn't take into account region affinities.</span></span> <span data-ttu-id="7f337-115">Уведомление будет отправлено в развертывание в зависимости от разрешения GeoDNS.</span><span class="sxs-lookup"><span data-stu-id="7f337-115">The notification will be sent to your deployment depending on the GeoDNS resolution.</span></span> <span data-ttu-id="7f337-116">Если приложение определяет, изменив полезные полезные данные уведомления или иным образом, оно должно выполняться в другом развертывании, приложение может ответить следующим образом:</span><span class="sxs-lookup"><span data-stu-id="7f337-116">If your application determines, by inspecting the initial notification payload or otherwise, that it needs to run in a different deployment, the application may reply with:</span></span>

```http
HTTP/1.1 302 Found
Location: your-new-location
```

<span data-ttu-id="7f337-117">Разрешить интерфейсу Bot отвечать на входящий вызов с помощью API [ответов](https://developer.microsoft.com/graph/docs/api-reference/beta/api/call_answer) .</span><span class="sxs-lookup"><span data-stu-id="7f337-117">Enable your bot to answer an incoming call using the [answer](https://developer.microsoft.com/graph/docs/api-reference/beta/api/call_answer) API.</span></span> <span data-ttu-id="7f337-118">Вы можете задать `callbackUri` обработку этого конкретного вызова.</span><span class="sxs-lookup"><span data-stu-id="7f337-118">You can specify the `callbackUri` to handle this particular call.</span></span> <span data-ttu-id="7f337-119">Это полезно для экземпляров с _ведением состояния_ , где вызов обрабатывается определенным разделом и необходимо внедрить эту информацию в маршрут `callbackUri` для маршрутизации в нужный экземпляр.</span><span class="sxs-lookup"><span data-stu-id="7f337-119">This is useful for _stateful_ instances where your call is handled by a particular partition and you want to embed this information in the `callbackUri` for routing to the right instance.</span></span>

## <a name="authenticating-the-callback"></a><span data-ttu-id="7f337-120">Проверка подлинности обратного вызова</span><span class="sxs-lookup"><span data-stu-id="7f337-120">Authenticating the callback</span></span>

<span data-ttu-id="7f337-121">Ваш робот должен проверить маркер, отправленный на веб-перехватчик, чтобы проверить запрос.</span><span class="sxs-lookup"><span data-stu-id="7f337-121">Your bot should inspect the token posted to your webhook to validate the request.</span></span> <span data-ttu-id="7f337-122">Когда API отправляется в веб-перехватчик, сообщение POST HTTP содержит маркер OAuth в заголовке авторизации в качестве маркера носителя с аудиторией в качестве идентификатора приложения.</span><span class="sxs-lookup"><span data-stu-id="7f337-122">Whenever the API posts to the webhook, the HTTP POST message contains an OAuth token in the Authorization header as a Bearer token, with audience as your application's App ID.</span></span>

<span data-ttu-id="7f337-123">Приложение должно проверить этот маркер, прежде чем принимать запрос обратного вызова.</span><span class="sxs-lookup"><span data-stu-id="7f337-123">Your application should validate this token before accepting the callback request.</span></span>

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

<span data-ttu-id="7f337-124">Маркер OAuth будет иметь значения, подобные приведенным ниже, и будет подписан Skype.</span><span class="sxs-lookup"><span data-stu-id="7f337-124">The OAuth token will have values like the following, and will be signed by Skype.</span></span> <span data-ttu-id="7f337-125">Конфигурацию OpenID, опубликованную <https://api.aps.skype.com/v1/.well-known/OpenIdConfiguration> в, можно использовать для проверки маркера.</span><span class="sxs-lookup"><span data-stu-id="7f337-125">The OpenID configuration published at <https://api.aps.skype.com/v1/.well-known/OpenIdConfiguration> can be used to verify the token.</span></span>

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

* <span data-ttu-id="7f337-126">**ауд** аудитория — это URI идентификатора приложения, указанный для приложения.</span><span class="sxs-lookup"><span data-stu-id="7f337-126">**aud** audience is the App ID URI specified for the application.</span></span>
* <span data-ttu-id="7f337-127">**tid** — идентификатор клиента для contoso.com.</span><span class="sxs-lookup"><span data-stu-id="7f337-127">**tid** is the tenant id for Contoso.com.</span></span>
* <span data-ttu-id="7f337-128">**ISS** — это поставщик маркеров, `https://api.botframework.com`.</span><span class="sxs-lookup"><span data-stu-id="7f337-128">**iss** is the token issuer, `https://api.botframework.com`.</span></span>

<span data-ttu-id="7f337-129">При обработке кода веб-перехватчику необходимо проверить маркер, убедиться, что срок его действия истек, и проверить, подписан ли он опубликованной конфигурацией OpenID.</span><span class="sxs-lookup"><span data-stu-id="7f337-129">Your code handling the webhook should validate the token, ensure it hasn't expired, and check whether it has been signed by our published OpenID configuration.</span></span> <span data-ttu-id="7f337-130">Кроме того, необходимо проверить, соответствует ли **ауд** идентификатору приложения, прежде чем принимать запрос обратного вызова.</span><span class="sxs-lookup"><span data-stu-id="7f337-130">You should also check whether **aud** matches your App ID before accepting the callback request.</span></span>

<span data-ttu-id="7f337-131">В [примере](https://github.com/microsoftgraph/microsoft-graph-comms-samples/blob/master/Samples/Common/Sample.Common/Authentication/AuthenticationProvider.cs) показано, как проверить входящие запросы.</span><span class="sxs-lookup"><span data-stu-id="7f337-131">[Sample](https://github.com/microsoftgraph/microsoft-graph-comms-samples/blob/master/Samples/Common/Sample.Common/Authentication/AuthenticationProvider.cs) shows how to validate inbound requests.</span></span>
