---
title: Что такое веб-окки и соединители?
author: surbhigupta
description: Понимание того, как веб-окки и соединители могут подключать веб-службы к Teams клиенту.
localization_priority: Normal
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 3e8105c9f069428bf93fb9bc2533895878f5ded1
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069042"
---
# <a name="what-are-webhooks-and-connectors"></a><span data-ttu-id="06e0d-103">Что такое веб-окки и соединители?</span><span class="sxs-lookup"><span data-stu-id="06e0d-103">What are webhooks and connectors?</span></span>

<span data-ttu-id="06e0d-104">С помощью веб-перехватчиков и соединителей можно легко подключить веб-службы к каналам и командам в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="06e0d-104">Webhooks and connectors are a simple way to connect your web services to channels and teams inside Microsoft Teams.</span></span> 

## <a name="outgoing-webhooks"></a><span data-ttu-id="06e0d-105">Исходящие веб-перехватчики</span><span class="sxs-lookup"><span data-stu-id="06e0d-105">Outgoing webhooks</span></span>

<span data-ttu-id="06e0d-106">Исходящие веб-перехватчики позволяют пользователям отправлять текстовые сообщения из канала в веб-службы.</span><span class="sxs-lookup"><span data-stu-id="06e0d-106">Outgoing webhooks allow your users to send text messages from a channel to your web services.</span></span> <span data-ttu-id="06e0d-107">После настройки пользователи смогут @mention исходяющий веб-сайт и отправить сообщение в службу.</span><span class="sxs-lookup"><span data-stu-id="06e0d-107">Once configured, your users will be able to @mention your outgoing webhook and send a message to your service.</span></span> <span data-ttu-id="06e0d-108">У службы будет пять секунд, чтобы отправить ответ на сообщение, потенциально содержащее текст или карточку.</span><span class="sxs-lookup"><span data-stu-id="06e0d-108">Your service will have five seconds to send a response to the message, potentially containing text or a card.</span></span>

<span data-ttu-id="06e0d-109">Исходяющие веб-окки настраиваются на основе одной команды, не могут быть включены как часть обычного Teams приложения.</span><span class="sxs-lookup"><span data-stu-id="06e0d-109">Outgoing webhooks are configured on a per-team basis, cannot be included as part of a normal Teams app.</span></span> <span data-ttu-id="06e0d-110">Они лучше всего подходят для выполнения рабочих нагрузок, которые не требуют сбора или обмена большими объемами информации.</span><span class="sxs-lookup"><span data-stu-id="06e0d-110">They are best suited for completing team-specific workloads that don't require large amounts of information to be collected or exchanged.</span></span>

<span data-ttu-id="06e0d-111">Дополнительные сведения см. [в странице Create an outgoing webhook.](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)</span><span class="sxs-lookup"><span data-stu-id="06e0d-111">For more information, see [Create an outgoing webhook](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md).</span></span>

## <a name="connectors"></a><span data-ttu-id="06e0d-112">Соединители</span><span class="sxs-lookup"><span data-stu-id="06e0d-112">Connectors</span></span>

<span data-ttu-id="06e0d-113">Соединители позволяют пользователям подписаться на получение уведомлений и сообщений от веб-служб.</span><span class="sxs-lookup"><span data-stu-id="06e0d-113">Connectors allow users to subscribe to receive notifications and messages from your web services.</span></span> <span data-ttu-id="06e0d-114">Они раскрывают конечную точку HTTPS для службы для публикации сообщений , как правило, в виде карт.</span><span class="sxs-lookup"><span data-stu-id="06e0d-114">They expose an HTTPS endpoint for your service to post messages to - typically in the form of cards.</span></span>

### <a name="incoming-webhooks"></a><span data-ttu-id="06e0d-115">Входящие веб-окки</span><span class="sxs-lookup"><span data-stu-id="06e0d-115">Incoming webhooks</span></span>

<span data-ttu-id="06e0d-116">Входящие веб-окки являются простейшим типом соединители.</span><span class="sxs-lookup"><span data-stu-id="06e0d-116">Incoming webhooks are the simplest type of connector.</span></span> <span data-ttu-id="06e0d-117">Для любого канала в команде (если они включены для этой группы) можно выбрать конечную точку HTTPS, которая будет принимать правильно отформатированные JSON и вставлять сообщения в этот канал.</span><span class="sxs-lookup"><span data-stu-id="06e0d-117">For any channel in team (if they are enabled for that team) you can choose to expose an HTTPS endpoint that will accept correctly formatted JSON and insert messages into that channel.</span></span> <span data-ttu-id="06e0d-118">Это быстрый и простой способ подключения канала к службе, который лучше всего использовать для сценариев, уникальных для определенной группы.</span><span class="sxs-lookup"><span data-stu-id="06e0d-118">They are a quick and easy way to connect a channel to your service, and are best used for scenarios that are unique to a particular team.</span></span> <span data-ttu-id="06e0d-119">Например, можно создать входящий веб-DevOps канал и настроить службы сборки, развертывания и мониторинга для отправки оповещений.</span><span class="sxs-lookup"><span data-stu-id="06e0d-119">For example, you could create an incoming webhook in your DevOps channel and configure your build, deployment and monitoring services to send alerts.</span></span>

<span data-ttu-id="06e0d-120">Дополнительные сведения см. в [странице Create an incoming webhook.](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)</span><span class="sxs-lookup"><span data-stu-id="06e0d-120">For more information, see [Create an incoming webhook](~/webhooks-and-connectors/how-to/add-incoming-webhook.md).</span></span>

### <a name="office-365-connectors"></a><span data-ttu-id="06e0d-121">Соединители Office 365</span><span class="sxs-lookup"><span data-stu-id="06e0d-121">Office 365 Connectors</span></span>

<span data-ttu-id="06e0d-122">Office 365 Соединители позволяют создавать настраиваемую страницу конфигурации для входящих веб-пользователей и упаковывать их в Teams приложения.</span><span class="sxs-lookup"><span data-stu-id="06e0d-122">Office 365 Connectors allow you to create a custom configuration page for your incoming webhook, and package them as part of a Teams app.</span></span> <span data-ttu-id="06e0d-123">Затем вы можете распространить это приложение более широко или даже в наш магазин приложений.</span><span class="sxs-lookup"><span data-stu-id="06e0d-123">You can then distribute that app more broadly, or even to our app store.</span></span> <span data-ttu-id="06e0d-124">Вы отправляете сообщения в основном с Office 365 соединителю, а также имеете возможность добавлять в них ограниченный набор действий карт.</span><span class="sxs-lookup"><span data-stu-id="06e0d-124">You send messages primarily using Office 365 Connector cards, and have the ability to add a limited set of card actions to them as well.</span></span> <span data-ttu-id="06e0d-125">Хорошим примером этого является подключение к погоде, которое позволяет пользователям выбирать расположение и время суток для получения обновлений о погоде завтрашнего дня.</span><span class="sxs-lookup"><span data-stu-id="06e0d-125">A good example of this is a weather connector that allows users to choose a location and time of day to receive updates about tomorrow's weather.</span></span> <span data-ttu-id="06e0d-126">Они настроены на уровне канала, но устанавливаются на уровне группы.</span><span class="sxs-lookup"><span data-stu-id="06e0d-126">They are configured on a channel level, but are installed at a team level.</span></span>

<span data-ttu-id="06e0d-127">Дополнительные сведения см. в [Office 365 Connector.](~/webhooks-and-connectors/how-to/connectors-creating.md)</span><span class="sxs-lookup"><span data-stu-id="06e0d-127">For more information, see [Create an Office 365 Connector](~/webhooks-and-connectors/how-to/connectors-creating.md).</span></span>
