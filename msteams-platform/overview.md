---
title: Создание приложений для платформы Microsoft Teams
author: heath-hamilton
description: Сведения о том, как разработчики могут расширять функции Microsoft Teams с помощью настраиваемого приложения.
ms.topic: overview
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: b4f5d5fa3014d2acc5e4178a89c84ddb5a250132
ms.sourcegitcommit: f5ee3fa5ef6126d9bf845948d27d9067b3bbb994
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2021
ms.locfileid: "51596212"
---
# <a name="build-apps-for-microsoft-teams"></a><span data-ttu-id="3cc07-103">Создание приложений для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="3cc07-103">Build apps for Microsoft Teams</span></span>

<span data-ttu-id="3cc07-104">Приложения Microsoft Teams приносят ключевые сведения, общие инструменты и доверенные процессы в места, где люди все чаще собираются, учатся и работают.</span><span class="sxs-lookup"><span data-stu-id="3cc07-104">Microsoft Teams apps bring key information, common tools, and trusted processes to where people increasingly gather, learn, and work.</span></span>

<span data-ttu-id="3cc07-105">Приложения — это то, как вы расширяете Teams, чтобы соответствовать вашим потребностям.</span><span class="sxs-lookup"><span data-stu-id="3cc07-105">Apps are how you extend Teams to fit your needs.</span></span> <span data-ttu-id="3cc07-106">Создайте что-то совершенно новое для Teams или интегрируете существующее приложение.</span><span class="sxs-lookup"><span data-stu-id="3cc07-106">Create something brand new for Teams or integrate an existing app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3cc07-107">Начните отсюда</span><span class="sxs-lookup"><span data-stu-id="3cc07-107">Start here</span></span>](build-your-first-app/build-first-app-overview.md)

## <a name="what-are-teams-apps"></a><span data-ttu-id="3cc07-108">Что такое приложения Teams?</span><span class="sxs-lookup"><span data-stu-id="3cc07-108">What are Teams apps?</span></span>

<span data-ttu-id="3cc07-109">Приложения teams — это сочетание [возможностей и](concepts/capabilities-overview.md) [точек входа.](concepts/extensibility-points.md)</span><span class="sxs-lookup"><span data-stu-id="3cc07-109">Teams apps are a combination of [capabilities](concepts/capabilities-overview.md) and [entry points](concepts/extensibility-points.md).</span></span> <span data-ttu-id="3cc07-110">Например, люди могут общаться с  ботом (возможностью) вашего приложения в *канале* (точка входа).</span><span class="sxs-lookup"><span data-stu-id="3cc07-110">For example, people can chat with your app's *bot* (capability) in a *channel* (entry point).</span></span>

<span data-ttu-id="3cc07-111">Некоторые приложения просты (отправка уведомлений), а другие сложны (управление записями пациентов).</span><span class="sxs-lookup"><span data-stu-id="3cc07-111">Some apps are simple (send notifications), while others are complex (manage patient records).</span></span> <span data-ttu-id="3cc07-112">При планировании приложения помните, что Teams — это центр совместной работы.</span><span class="sxs-lookup"><span data-stu-id="3cc07-112">When planning your app, remember that Teams is a collaboration hub.</span></span> <span data-ttu-id="3cc07-113">Лучшие приложения Teams помогают людям лучше выражать себя и работать вместе.</span><span class="sxs-lookup"><span data-stu-id="3cc07-113">The best Teams apps help people express themselves and work better together.</span></span>

:::row:::
   :::column span="":::

### <a name="tabs"></a><span data-ttu-id="3cc07-114">Вкладки</span><span class="sxs-lookup"><span data-stu-id="3cc07-114">Tabs</span></span>

<span data-ttu-id="3cc07-115">**Получите сведения более удобно.** Иногда вам просто нужно упростить поиск.</span><span class="sxs-lookup"><span data-stu-id="3cc07-115">**Get information more conveniently**: Sometimes you just need to make things easier to find.</span></span> <span data-ttu-id="3cc07-116">Отображение важной веб-страницы [](tabs/what-are-tabs.md)на вкладке, которая обеспечивает полноэкранный веб-опыт для статического и динамического контента в Teams.</span><span class="sxs-lookup"><span data-stu-id="3cc07-116">Display an important webpage in a [tab](tabs/what-are-tabs.md), which provides a full-screen web experience for static and dynamic content in Teams.</span></span>

:::image type="content" source="assets/images/overview-tabs.png" alt-text="Концептуальное представление о том, как выглядят вкладки в клиенте Teams." border="false":::

   :::column-end:::

   :::column span="":::

### <a name="bots"></a><span data-ttu-id="3cc07-118">Боты</span><span class="sxs-lookup"><span data-stu-id="3cc07-118">Bots</span></span>

<span data-ttu-id="3cc07-119">**Превратите** слова в действия: беседы часто приводит к необходимости что-то делать (создать заказ, просмотреть код, проверить состояние билета и т.д.).</span><span class="sxs-lookup"><span data-stu-id="3cc07-119">**Turn words into actions**: Conversations often result in the need to do something (generate an order, review my code, check ticket status, etc.).</span></span> <span data-ttu-id="3cc07-120">Бот [может](bots/what-are-bots.md) скинуть эти типы рабочего процесса прямо внутри Teams.</span><span class="sxs-lookup"><span data-stu-id="3cc07-120">A [bot](bots/what-are-bots.md) can kick off these kinds of workflows right inside Teams.</span></span>

:::image type="content" source="assets/images/overview-bots.png" alt-text="Концептуальное представление того, как выглядят боты в клиенте Teams." border="false":::

   :::column-end:::

:::row-end:::

:::row:::

   :::column span="":::

### <a name="messaging-extensions"></a><span data-ttu-id="3cc07-122">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="3cc07-122">Messaging extensions</span></span>

<span data-ttu-id="3cc07-123">**Упростите многозадачную** работу. [С](messaging-extensions/what-are-messaging-extensions.md)помощью расширений обмена сообщениями можно быстро обмениваться внешней информацией в беседе.</span><span class="sxs-lookup"><span data-stu-id="3cc07-123">**Make it easier to multitask**: With [messaging extensions](messaging-extensions/what-are-messaging-extensions.md), you can quickly share external information in a conversation.</span></span> <span data-ttu-id="3cc07-124">Вы также можете действовать по сообщению, например, создать билет справки на основе контента сообщения канала.</span><span class="sxs-lookup"><span data-stu-id="3cc07-124">You also can act on a message, such as creating a help ticket based on the content of a channel post.</span></span>

:::image type="content" source="assets\images\overview-messaging.png" alt-text="Концептуальное представление о том, как выглядят расширения обмена сообщениями в клиенте Teams." border="false":::

   :::column-end:::

   :::column span="":::

### <a name="webhooks"></a><span data-ttu-id="3cc07-126">веб-перехватчики</span><span class="sxs-lookup"><span data-stu-id="3cc07-126">Webhooks</span></span>

<span data-ttu-id="3cc07-127">**Связь с внешними приложениями.** [Входящие веб-сайты](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) — это простой способ автоматической отправки уведомлений из другого приложения в канал Teams.</span><span class="sxs-lookup"><span data-stu-id="3cc07-127">**Communicate with external apps**: [Incoming webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) are a simple way to automatically send notifications from another app to a Teams channel.</span></span> <span data-ttu-id="3cc07-128">В [исходяющих веб-сайтах](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks)сообщение веб-службы с помощью @mention.</span><span class="sxs-lookup"><span data-stu-id="3cc07-128">With [outgoing webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks), message your web service with an @mention.</span></span>

:::image type="content" source="assets/images/overview-connectors.png" alt-text="Концептуальное представление того, как выглядят соединители в клиенте Teams." border="false":::

   :::column-end:::
:::row-end:::

:::row:::

   :::column span="":::

### <a name="microsoft-graph-for-teams"></a><span data-ttu-id="3cc07-130">Microsoft Graph для teams</span><span class="sxs-lookup"><span data-stu-id="3cc07-130">Microsoft Graph for Teams</span></span>

<span data-ttu-id="3cc07-131">**Использование данных Teams.** [API Microsoft Graph для Teams](https://docs.microsoft.com/graph/teams-concept-overview) предоставляет доступ к сведениям о командах, каналах, пользователях и сообщениях, которые помогут вам создать или улучшить функции для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="3cc07-131">**Utilize Teams data**: The [Microsoft Graph API for Teams](https://docs.microsoft.com/graph/teams-concept-overview) provides access to information about teams, channels, users, and messages that can help you create or enhance features for your app.</span></span>

:::image type="content" source="assets/images/overview-graph.png" alt-text="Концептуальное представление API Microsoft Graph для Teams." border="false":::

   :::column-end:::

   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="start-building"></a><span data-ttu-id="3cc07-133">Начало создания</span><span class="sxs-lookup"><span data-stu-id="3cc07-133">Start building</span></span>

<span data-ttu-id="3cc07-134">Быстро ознакомьтесь со зданием для Teams, настроив среду и создав простое приложение.</span><span class="sxs-lookup"><span data-stu-id="3cc07-134">Quickly familiarize yourself with building for Teams by setting up your environment and creating a simple app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3cc07-135">Создание первого приложения</span><span class="sxs-lookup"><span data-stu-id="3cc07-135">Build your first app</span></span>](build-your-first-app/build-first-app-overview.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="integrate-with-teams"></a><span data-ttu-id="3cc07-136">Интеграция с Teams</span><span class="sxs-lookup"><span data-stu-id="3cc07-136">Integrate with Teams</span></span>

<span data-ttu-id="3cc07-137">Сочетание функций, которые пользователи любят в существующем веб-приложении, службе или системе, с функциями совместной работы Teams.</span><span class="sxs-lookup"><span data-stu-id="3cc07-137">Blend the features users love about an existing web app, service, or system with the collaborative features of Teams.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3cc07-138">Интеграция существующего приложения</span><span class="sxs-lookup"><span data-stu-id="3cc07-138">Integrate an existing app</span></span>](samples/integrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="a-little-code-goes-a-long-way"></a><span data-ttu-id="3cc07-139">Маленький код проходит долгий путь</span><span class="sxs-lookup"><span data-stu-id="3cc07-139">A little code goes a long way</span></span>

<span data-ttu-id="3cc07-140">Вам не нужно быть программистом-экспертом, чтобы создать отличное приложение Teams.</span><span class="sxs-lookup"><span data-stu-id="3cc07-140">You don't need to be an expert programmer to build a great Teams app.</span></span> <span data-ttu-id="3cc07-141">Попробуйте одно из нескольких решений с низким кодом.</span><span class="sxs-lookup"><span data-stu-id="3cc07-141">Try one of several low-code solutions.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3cc07-142">Создание приложения с низким кодом</span><span class="sxs-lookup"><span data-stu-id="3cc07-142">Create a low-code app</span></span>](samples/teams-low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="get-ideas-for-your-app"></a><span data-ttu-id="3cc07-143">Получить идеи для приложения</span><span class="sxs-lookup"><span data-stu-id="3cc07-143">Get ideas for your app</span></span>

<span data-ttu-id="3cc07-144">Ищете вдохновение для разработки приложений?</span><span class="sxs-lookup"><span data-stu-id="3cc07-144">Looking for app development inspiration?</span></span> <span data-ttu-id="3cc07-145">Просмотрите список реальных сценариев и отраслевых решений с помощью макетов концепции высокой верности, чтобы понять различные способы, которыми приложения Teams могут помочь пользователям.</span><span class="sxs-lookup"><span data-stu-id="3cc07-145">Browse our list of real-world scenarios and industry solutions with high fidelity concept mocks to understand the various ways Teams apps can help your users.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3cc07-146">См. сценарии приложений</span><span class="sxs-lookup"><span data-stu-id="3cc07-146">See app scenarios</span></span>](https://adoption.microsoft.com/extensibility-look-book/scenarios/)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="see-also"></a><span data-ttu-id="3cc07-147">См. также</span><span class="sxs-lookup"><span data-stu-id="3cc07-147">See also</span></span>

* [<span data-ttu-id="3cc07-148">Добавление кнопки Share-to-Teams на веб-сайт</span><span class="sxs-lookup"><span data-stu-id="3cc07-148">Add a Share-to-Teams button to your website</span></span>](concepts/build-and-test/share-to-teams.md)
* [<span data-ttu-id="3cc07-149">Разработка приложения Teams</span><span class="sxs-lookup"><span data-stu-id="3cc07-149">Design your Teams app</span></span>](concepts/design/design-teams-app-overview.md)
* [<span data-ttu-id="3cc07-150">Клиент Microsoft Teams JavaScript SDK</span><span class="sxs-lookup"><span data-stu-id="3cc07-150">Microsoft Teams JavaScript client SDK</span></span>](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* <span data-ttu-id="3cc07-151">Bot Framework SDK для [JavaScript](https://github.com/Microsoft/botbuilder-js) и [.NET](https://github.com/Microsoft/botbuilder-dotnet/)</span><span class="sxs-lookup"><span data-stu-id="3cc07-151">Bot Framework SDK for [JavaScript](https://github.com/Microsoft/botbuilder-js) and [.NET](https://github.com/Microsoft/botbuilder-dotnet/)</span></span>
* [<span data-ttu-id="3cc07-152">Публикация приложения Teams</span><span class="sxs-lookup"><span data-stu-id="3cc07-152">Publish your Teams app</span></span>](concepts/deploy-and-publish/overview.md)
