---
title: Что такое веб-перехватчики и соединители?
author: clearab
description: Узнайте, как веб-перехватчики и соединители могут подключаться к веб-службам в клиенте Teams.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 740806e43af94d5a5da876affec2070a5a461b11
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/12/2020
ms.locfileid: "46652120"
---
# <a name="what-are-webhooks-and-connectors"></a><span data-ttu-id="281fc-103">Что такое веб-перехватчики и соединители?</span><span class="sxs-lookup"><span data-stu-id="281fc-103">What are webhooks and connectors?</span></span>

<span data-ttu-id="281fc-104">Веб-перехватчики и соединители — это простые способы подключения внешних систем и служб к каналам и разговорам Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="281fc-104">Webhooks and connectors are straightforward ways to connect external systems and services with Microsoft Teams channels and chats.</span></span>

<span data-ttu-id="281fc-105">Пользователи могут, например, подписываться на уведомления из другого приложения (как правило, в форме карточек).</span><span class="sxs-lookup"><span data-stu-id="281fc-105">Users can, for example, subscribe to notifications from another app (typically in the form of cards).</span></span>

## <a name="incoming-webhooks"></a><span data-ttu-id="281fc-106">Входящие веб-перехватчики</span><span class="sxs-lookup"><span data-stu-id="281fc-106">Incoming webhooks</span></span>

<span data-ttu-id="281fc-107">Входящие веб-перехватчики это самый простой тип соединителя и быстрый и простой способ подключения канала группы к внешней службе.</span><span class="sxs-lookup"><span data-stu-id="281fc-107">Incoming webhooks are the simplest type of connector and a quick and easy way to connect a team's channel to an external service.</span></span> <span data-ttu-id="281fc-108">Для любого канала (если он включен для этой команды) можно предоставить конечную точку HTTPS, которая принимает правильно отформатированный формат JSON и вставит сообщения в канал.</span><span class="sxs-lookup"><span data-stu-id="281fc-108">For any channel (if enabled for that team), you can expose an HTTPS endpoint that accepts correctly formatted JSON and insert messages into the channel.</span></span>

<span data-ttu-id="281fc-109">Ознакомьтесь [со статьей Создание входящего веб-перехватчика](~/webhooks-and-connectors/how-to/add-incoming-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="281fc-109">See [Create an incoming webhook](~/webhooks-and-connectors/how-to/add-incoming-webhook.md).</span></span>

### <a name="user-scenarios"></a><span data-ttu-id="281fc-110">Пользовательские сценарии</span><span class="sxs-lookup"><span data-stu-id="281fc-110">User scenarios</span></span>

<span data-ttu-id="281fc-111">Входящие веб-перехватчики наилучшим образом подходят для сценариев, уникальных для конкретной команды.</span><span class="sxs-lookup"><span data-stu-id="281fc-111">Incoming webhooks are best for scenarios unique to a particular team.</span></span> <span data-ttu-id="281fc-112">Например, вы можете создать входящий веб-перехватчик в своем канале DevOps и настроить службы построения, развертывания и мониторинга для отправки оповещений.</span><span class="sxs-lookup"><span data-stu-id="281fc-112">For example, you could create an incoming webhook in your DevOps channel and configure your build, deployment, and monitoring services to send alerts.</span></span>

## <a name="office-365-connectors"></a><span data-ttu-id="281fc-113">Соединители Office 365</span><span class="sxs-lookup"><span data-stu-id="281fc-113">Office 365 Connectors</span></span>

<span data-ttu-id="281fc-114">Соединитель Office 365 позволяет создать настраиваемую страницу конфигурации для входящего веб-перехватчика и упаковать ее как часть приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="281fc-114">An Office 365 Connector allows you to create a custom configuration page for your incoming webhook and package it as part of a Teams app.</span></span> <span data-ttu-id="281fc-115">Затем вы можете распространить это приложение более широко или даже в наши хранилища приложений.</span><span class="sxs-lookup"><span data-stu-id="281fc-115">You can then distribute that app more broadly or even to our app store.</span></span> <span data-ttu-id="281fc-116">Сообщения отправляются в основном с помощью карт подключателя Office 365, которые также могут иметь ограниченный набор действий с картой.</span><span class="sxs-lookup"><span data-stu-id="281fc-116">You send messages primarily using Office 365 Connector cards that can also have a limited set of card actions.</span></span> <span data-ttu-id="281fc-117">Они настраиваются на уровне канала, но устанавливаются на уровне команды.</span><span class="sxs-lookup"><span data-stu-id="281fc-117">They are configured on the channel level but installed at the team level.</span></span>

<span data-ttu-id="281fc-118">В разделе Create a a [Office 365 Connector](~/webhooks-and-connectors/how-to/connectors-creating.md).</span><span class="sxs-lookup"><span data-stu-id="281fc-118">See [Create an Office 365 Connector](~/webhooks-and-connectors/how-to/connectors-creating.md).</span></span>

### <a name="user-scenarios"></a><span data-ttu-id="281fc-119">Пользовательские сценарии</span><span class="sxs-lookup"><span data-stu-id="281fc-119">User scenarios</span></span>

<span data-ttu-id="281fc-120">Соединитель погоды, позволяющий выбрать местоположение и время для получения обновлений по прогнозу завтрашнего дня.</span><span class="sxs-lookup"><span data-stu-id="281fc-120">A weather connector that lets you choose a location and time of day to receive updates about tomorrow's forecast.</span></span>

## <a name="outgoing-webhooks"></a><span data-ttu-id="281fc-121">Исходящие веб-перехватчики</span><span class="sxs-lookup"><span data-stu-id="281fc-121">Outgoing webhooks</span></span>

<span data-ttu-id="281fc-122">Исходящие веб-Перехватчики позволяют пользователям отправлять текстовые сообщения из канала в веб-службы.</span><span class="sxs-lookup"><span data-stu-id="281fc-122">Outgoing webhooks allow your users to send text messages from a channel to your web services.</span></span> <span data-ttu-id="281fc-123">После настройки пользователи могут @mention ваше приложение и отправлять сообщение во внешнюю службу.</span><span class="sxs-lookup"><span data-stu-id="281fc-123">Once configured, users can @mention your app and send a message to your external service.</span></span> <span data-ttu-id="281fc-124">В течение пяти секунд служба отправляет ответ на сообщение, потенциально содержащий текст или карточку.</span><span class="sxs-lookup"><span data-stu-id="281fc-124">Your service has five seconds to send a response to the message, potentially containing text or a card.</span></span>

<span data-ttu-id="281fc-125">Исходящие веб-перехватчики настраиваются отдельно для каждой группы и не могут быть включены в состав обычного приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="281fc-125">Outgoing webhooks are configured on a per-team basis and can't be included as part of a normal Teams app.</span></span>

<span data-ttu-id="281fc-126">Ознакомьтесь [со статьей Создание исходящего веб-перехватчика](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="281fc-126">See [Create an outgoing webhook](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md).</span></span>

### <a name="user-scenarios"></a><span data-ttu-id="281fc-127">Пользовательские сценарии</span><span class="sxs-lookup"><span data-stu-id="281fc-127">User scenarios</span></span>

<span data-ttu-id="281fc-128">Исходящие веб-перехватчики лучше всего подходят для выполнения рабочих процессов, связанных с группой, для которых не требуется собирать или обмениваться большим объемом информации.</span><span class="sxs-lookup"><span data-stu-id="281fc-128">Outgoing webhooks are best suited for completing team-specific workflows that don't require collecting or exchanging large amounts of information.</span></span>

## <a name="learn-more"></a><span data-ttu-id="281fc-129">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="281fc-129">Learn more</span></span>

* [<span data-ttu-id="281fc-130">Планирование приложения</span><span class="sxs-lookup"><span data-stu-id="281fc-130">Planning your app</span></span>](../../concepts/extensibility-points.md)
* [<span data-ttu-id="281fc-131">Создание приложения</span><span class="sxs-lookup"><span data-stu-id="281fc-131">Building your app</span></span>](../../concepts/building-an-app.md)
* [<span data-ttu-id="281fc-132">Публикация приложения</span><span class="sxs-lookup"><span data-stu-id="281fc-132">Publishing your app</span></span>](../../concepts/deploy-and-publish/overview.md)
