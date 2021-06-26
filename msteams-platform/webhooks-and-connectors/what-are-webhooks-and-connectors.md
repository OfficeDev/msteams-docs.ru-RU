---
title: Веб-перехватчики и соединительные линии
author: clearab
description: Понимание того, как веб-окки и соединители могут подключать веб-службы к Teams клиенту.
localization_priority: Normal
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 2cb763a6637abd3faa500de871119f0b829871bf
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140056"
---
# <a name="webhooks-and-connectors"></a><span data-ttu-id="5e819-103">Веб-перехватчики и соединительные линии</span><span class="sxs-lookup"><span data-stu-id="5e819-103">Webhooks and connectors</span></span>

<span data-ttu-id="5e819-104">Веб-окки и соединители помогают подключать веб-службы к каналам и группам в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="5e819-104">Webhooks and connectors help to connect the web services to channels and teams in Microsoft Teams.</span></span> <span data-ttu-id="5e819-105">Веб-окки — это пользовательский http-вызов, который сообщает пользователям о любых действиях, которые произошли в Microsoft Teams канале.</span><span class="sxs-lookup"><span data-stu-id="5e819-105">Webhooks are user defined HTTP callback that notifies users about any action that has taken place in the Microsoft Teams channel.</span></span> <span data-ttu-id="5e819-106">Это способ получения данных в режиме реального времени для приложения.</span><span class="sxs-lookup"><span data-stu-id="5e819-106">It is a way for an app to get real time data.</span></span> <span data-ttu-id="5e819-107">Соединители позволяют пользователям подписаться на получение уведомлений и сообщений от веб-служб.</span><span class="sxs-lookup"><span data-stu-id="5e819-107">Connectors allow users to subscribe to receive notifications and messages from your web services.</span></span> <span data-ttu-id="5e819-108">Они раскрывают конечную точку HTTPS для службы для публикации сообщений в виде карт.</span><span class="sxs-lookup"><span data-stu-id="5e819-108">They expose an HTTPS endpoint for your service to post messages in the form of cards.</span></span>

## <a name="outgoing-webhooks"></a><span data-ttu-id="5e819-109">Исходяние веб-ок</span><span class="sxs-lookup"><span data-stu-id="5e819-109">Outgoing Webhooks</span></span>

<span data-ttu-id="5e819-110">Веб-сайты помогают Teams интеграции с внешними приложениями.</span><span class="sxs-lookup"><span data-stu-id="5e819-110">Webhooks help Teams to integrate with external apps.</span></span> <span data-ttu-id="5e819-111">Исходя из webhooks можно отправлять текстовые сообщения из канала в веб-службы.</span><span class="sxs-lookup"><span data-stu-id="5e819-111">With Outgoing Webhooks, you can send text messages from a channel to the web services.</span></span> <span data-ttu-id="5e819-112">После настройки исходяющих веб-ок пользователи могут @mention исходяющий веб-сайт и отправлять сообщение в веб-службы.</span><span class="sxs-lookup"><span data-stu-id="5e819-112">After configuring the Outgoing Webhooks, users can @mention Outgoing Webhook and send a message to web services.</span></span> <span data-ttu-id="5e819-113">Служба отвечает в течение десяти секунд на сообщение текстом или картой.</span><span class="sxs-lookup"><span data-stu-id="5e819-113">The service responds within ten seconds to the message with a text or a card.</span></span>

> [!NOTE]
> <span data-ttu-id="5e819-114">Исходяющие веб-окки настраиваются на основе группы и не могут быть включены как часть обычного Teams приложения.</span><span class="sxs-lookup"><span data-stu-id="5e819-114">Outgoing Webhooks are configured on a per team basis and cannot be included as part of a normal Teams app.</span></span>

## <a name="connectors"></a><span data-ttu-id="5e819-115">Соединители</span><span class="sxs-lookup"><span data-stu-id="5e819-115">Connectors</span></span>

<span data-ttu-id="5e819-116">Соединители позволяют пользователям подписываться на получение уведомлений и сообщений от веб-служб.</span><span class="sxs-lookup"><span data-stu-id="5e819-116">Connectors allow users to subscribe to receive notifications and messages from the web services.</span></span> <span data-ttu-id="5e819-117">Они раскрывают конечную точку HTTPS для службы для Teams каналов, как правило, в виде карт.</span><span class="sxs-lookup"><span data-stu-id="5e819-117">They expose the HTTPS endpoint for the service to post messages to Teams channels, typically in the form of cards.</span></span>

### <a name="incoming-webhooks"></a><span data-ttu-id="5e819-118">Входящие веб-окки</span><span class="sxs-lookup"><span data-stu-id="5e819-118">Incoming Webhooks</span></span>

<span data-ttu-id="5e819-119">Входящие веб-окки помогают отправлять сообщения из приложений в Teams.</span><span class="sxs-lookup"><span data-stu-id="5e819-119">Incoming Webhooks help in posting messages from apps to Teams.</span></span> <span data-ttu-id="5e819-120">Если входящие веб-оки включены для группы в любом канале, она предоставляет конечную точку HTTPS, которая принимает правильно отформатированные JSON и вставляет сообщения в этот канал.</span><span class="sxs-lookup"><span data-stu-id="5e819-120">If Incoming Webhooks are enabled for a team in any channel, it exposes the HTTPS endpoint, which accepts correctly formatted JSON and inserts the messages into that channel.</span></span> <span data-ttu-id="5e819-121">Например, можно создать входящий веб DevOps канал, настроить сборку и одновременно развернуть и отслеживать службы для отправки оповещений.</span><span class="sxs-lookup"><span data-stu-id="5e819-121">For example, you can create an Incoming Webhook in your DevOps channel, configure your build, and simultaneously deploy and monitor services to send alerts.</span></span>

### <a name="office-365-connectors"></a><span data-ttu-id="5e819-122">Соединители Office 365</span><span class="sxs-lookup"><span data-stu-id="5e819-122">Office 365 Connectors</span></span>

<span data-ttu-id="5e819-123">Office 365 Соединители позволяют создавать настраиваемую страницу конфигурации для входящих веб-пользователей и упаковывать их в Teams приложения.</span><span class="sxs-lookup"><span data-stu-id="5e819-123">Office 365 Connectors allow you to create a custom configuration page for your Incoming Webhook and package them as part of a Teams app.</span></span> <span data-ttu-id="5e819-124">Вы отправляете сообщения в основном с Office 365 соединителю и имеете возможность добавлять в них ограниченный набор действий карт.</span><span class="sxs-lookup"><span data-stu-id="5e819-124">You send messages primarily using Office 365 Connector cards and have the ability to add a limited set of card actions to them.</span></span> <span data-ttu-id="5e819-125">Например, соединитетелем погоды, который позволяет пользователям выбирать местоположение и время суток, получать обновления о погоде завтрашнего дня.</span><span class="sxs-lookup"><span data-stu-id="5e819-125">For example, a weather connector that allows users to select a location and time of day, to receive updates about tomorrow's weather.</span></span> <span data-ttu-id="5e819-126">Они настроены на уровне канала, но устанавливаются на уровне группы.</span><span class="sxs-lookup"><span data-stu-id="5e819-126">They are configured on a channel level but are installed at a team level.</span></span>

> [!NOTE]
> <span data-ttu-id="5e819-127">Вы можете распространять приложение Office 365 соединители Teams в нашем AppStore.</span><span class="sxs-lookup"><span data-stu-id="5e819-127">You can distribute the Office 365 Connector Teams app to our AppStore.</span></span>

## <a name="create-and-send-messages"></a><span data-ttu-id="5e819-128">Создание и отправка сообщений</span><span class="sxs-lookup"><span data-stu-id="5e819-128">Create and send messages</span></span>

<span data-ttu-id="5e819-129">Actionable messages allow users to take action without leaving their email client, increasing user engagement.</span><span class="sxs-lookup"><span data-stu-id="5e819-129">Actionable messages allow users to take action without leaving their email client, increasing user engagement.</span></span> <span data-ttu-id="5e819-130">С Office 365 и входящих веб-ок можно отправлять сообщения, разместив полезной нагрузки JSON на URL-адрес веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="5e819-130">With Office 365 and Incoming Webhooks, you can send messages by posting a JSON payload to the webhook URL.</span></span>

## <a name="see-also"></a><span data-ttu-id="5e819-131">См. также</span><span class="sxs-lookup"><span data-stu-id="5e819-131">See also</span></span>

* [<span data-ttu-id="5e819-132">Создание входящих веб-ок</span><span class="sxs-lookup"><span data-stu-id="5e819-132">Create an Incoming Webhook</span></span>](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [<span data-ttu-id="5e819-133">Создание соединителя Office 365</span><span class="sxs-lookup"><span data-stu-id="5e819-133">Create an Office 365 Connector</span></span>](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [<span data-ttu-id="5e819-134">Создание и отправка сообщений</span><span class="sxs-lookup"><span data-stu-id="5e819-134">Create and send messages</span></span>](~/webhooks-and-connectors/how-to/connectors-using.md)

## <a name="next-step"></a><span data-ttu-id="5e819-135">Следующий этап</span><span class="sxs-lookup"><span data-stu-id="5e819-135">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5e819-136">Создание исходятого веб-окка</span><span class="sxs-lookup"><span data-stu-id="5e819-136">Create an Outgoing Webhook</span></span>](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)
