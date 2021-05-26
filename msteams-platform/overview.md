---
title: Создание приложений для Microsoft Teams платформы
author: heath-hamilton
description: Сведения о том, как разработчики могут расширять Microsoft Teams с помощью настраиваемого приложения.
ms.topic: overview
localization_priority: Normal
ms.author: lajanuar
ms.date: 05/24/2021
ms.openlocfilehash: 796353a4c556794a518a451e8a45989351729eb9
ms.sourcegitcommit: 9cabeaed9baf96c8caeb1497f0bc37abdb787d22
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/25/2021
ms.locfileid: "52646539"
---
# <a name="build-apps-for-microsoft-teams"></a><span data-ttu-id="74670-103">Создание приложений для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="74670-103">Build apps for Microsoft Teams</span></span>

<span data-ttu-id="74670-104">Microsoft Teams приложения приносят ключевые сведения, общие инструменты и доверенные процессы в места, где люди все чаще собираются, учатся и работают.</span><span class="sxs-lookup"><span data-stu-id="74670-104">Microsoft Teams apps bring key information, common tools, and trusted processes to where people increasingly gather, learn, and work.</span></span>

<span data-ttu-id="74670-105">Приложения — это то, как Teams, чтобы соответствовать вашим потребностям.</span><span class="sxs-lookup"><span data-stu-id="74670-105">Apps are how you extend Teams to fit your needs.</span></span> <span data-ttu-id="74670-106">Создайте что-то новое для Teams или интегрируете существующее приложение.</span><span class="sxs-lookup"><span data-stu-id="74670-106">Create something brand new for Teams or integrate an existing app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="74670-107">Начните отсюда</span><span class="sxs-lookup"><span data-stu-id="74670-107">Start here</span></span>](get-started/prerequisites.md)

## <a name="what-are-teams-apps"></a><span data-ttu-id="74670-108">Что такое Teams приложения?</span><span class="sxs-lookup"><span data-stu-id="74670-108">What are Teams apps?</span></span>

<span data-ttu-id="74670-109">Teams приложения — это сочетание [возможностей.](concepts/capabilities-overview.md)</span><span class="sxs-lookup"><span data-stu-id="74670-109">Teams apps are a combination of [capabilities](concepts/capabilities-overview.md).</span></span> <span data-ttu-id="74670-110">Некоторые приложения просты (отправка уведомлений), а другие сложны (управление записями пациентов).</span><span class="sxs-lookup"><span data-stu-id="74670-110">Some apps are simple (send notifications), while others are complex (manage patient records).</span></span> <span data-ttu-id="74670-111">При планировании приложения помните, что Teams является концентратором совместной работы.</span><span class="sxs-lookup"><span data-stu-id="74670-111">When planning your app, remember that Teams is a collaboration hub.</span></span> <span data-ttu-id="74670-112">Лучшие Teams помогают людям лучше выражать себя и работать вместе.</span><span class="sxs-lookup"><span data-stu-id="74670-112">The best Teams apps help people express themselves and work better together.</span></span>

### <a name="personal-apps"></a><span data-ttu-id="74670-113">Персональные приложения</span><span class="sxs-lookup"><span data-stu-id="74670-113">Personal apps</span></span>

:::row:::
   :::column span="1":::

<span data-ttu-id="74670-114">**Помощь людям в фокусе:** [личное](concepts/design/personal-apps.md) приложение — это выделенное пространство или бот, чтобы помочь пользователям сосредоточиться на своих задачах или просмотреть важные для них действия.</span><span class="sxs-lookup"><span data-stu-id="74670-114">**Help people focus**: A [personal app](concepts/design/personal-apps.md) is a dedicated space or bot to help users focus on their own tasks or view activities important to them.</span></span>

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-personal-apps-2021.png" alt-text="Концептуальное представление того, как личные приложения выглядят в Teams клиенте." border="false":::

   :::column-end:::

:::row-end:::

### <a name="tabs"></a><span data-ttu-id="74670-116">Вкладки</span><span class="sxs-lookup"><span data-stu-id="74670-116">Tabs</span></span>

:::row:::
   :::column span="1":::

<span data-ttu-id="74670-117">**Совместное взаимодействие более удобно:** отображение веб-контента на вкладке, на которой пользователи могут совместно обсуждать и работать над ними. [](tabs/what-are-tabs.md)</span><span class="sxs-lookup"><span data-stu-id="74670-117">**Collaborate more conveniently**: Display your web-based content in a [tab](tabs/what-are-tabs.md) where people can discuss and work on it together.</span></span>

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-channel-chat-apps-2021.png" alt-text="Концептуальное представление того, как выглядят вкладки в Teams клиенте." border="false":::

   :::column-end:::

:::row-end:::

### <a name="bots"></a><span data-ttu-id="74670-119">Боты</span><span class="sxs-lookup"><span data-stu-id="74670-119">Bots</span></span>

:::row:::
   :::column span="1":::

<span data-ttu-id="74670-120">**Превратите** слова в действия: беседы часто приводит к необходимости что-то делать (создать заказ, просмотреть код, проверить состояние билета и так далее).</span><span class="sxs-lookup"><span data-stu-id="74670-120">**Turn words into actions**: Conversations often result in the need to do something (generate an order, review my code, check ticket status, and so on).</span></span> <span data-ttu-id="74670-121">Бот [может](bots/what-are-bots.md) скинуть эти типы рабочего процесса прямо внутри Teams.</span><span class="sxs-lookup"><span data-stu-id="74670-121">A [bot](bots/what-are-bots.md) can kick off these kinds of workflows right inside Teams.</span></span>

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-bots-2021.png" alt-text="Концептуальное представление того, как выглядят боты в Teams клиенте." border="false":::

   :::column-end:::

:::row-end:::

### <a name="messaging-extensions"></a><span data-ttu-id="74670-123">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="74670-123">Messaging extensions</span></span>

:::row:::

   :::column span="1":::

<span data-ttu-id="74670-124">**Упростите многозадачную** работу. [С](messaging-extensions/what-are-messaging-extensions.md)помощью расширений обмена сообщениями можно быстро обмениваться внешней информацией в беседе.</span><span class="sxs-lookup"><span data-stu-id="74670-124">**Make it easier to multitask**: With [messaging extensions](messaging-extensions/what-are-messaging-extensions.md), you can quickly share external information in a conversation.</span></span> <span data-ttu-id="74670-125">Вы также можете действовать по сообщению, например, создать билет справки на основе контента сообщения канала.</span><span class="sxs-lookup"><span data-stu-id="74670-125">You also can act on a message, such as creating a help ticket based on the content of a channel post.</span></span>

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-messaging-extensions-2021.png" alt-text="Концептуальное представление о том, как выглядят расширения обмена сообщениями в Teams клиенте." border="false":::

   :::column-end:::
:::row-end:::

### <a name="meeting-extensions"></a><span data-ttu-id="74670-127">Расширения для собраний</span><span class="sxs-lookup"><span data-stu-id="74670-127">Meeting extensions</span></span>

:::row:::

   :::column span="1":::

<span data-ttu-id="74670-128">**Создание приложений для собраний.** Существует несколько вариантов включения приложения в Teams [звонков.](apps-in-teams-meetings/design/designing-apps-in-meetings.md)</span><span class="sxs-lookup"><span data-stu-id="74670-128">**Create apps for meetings**: There are a few options for [incorporating your app into the Teams calling experience](apps-in-teams-meetings/design/designing-apps-in-meetings.md).</span></span>

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-meeting-extensions-2021.png" alt-text="Концептуальное представление о том, как выглядят расширения собраний в Teams клиенте." border="false":::

   :::column-end:::
:::row-end:::

### <a name="webhooks-and-connectors"></a><span data-ttu-id="74670-130">Веб-перехватчики и соединительные линии</span><span class="sxs-lookup"><span data-stu-id="74670-130">Webhooks and connectors</span></span>

:::row:::

   :::column span="":::

<span data-ttu-id="74670-131">**Связь с внешними** приложениями. [Входящие веб-сайты](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) — это простой способ автоматической отправки уведомлений из другого приложения на Teams канал.</span><span class="sxs-lookup"><span data-stu-id="74670-131">**Communicate with external apps**: [Incoming webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) are a simple way to automatically send notifications from another app to a Teams channel.</span></span> <span data-ttu-id="74670-132">В [исходяющих веб-сайтах](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks)сообщение веб-службы с помощью @mention.</span><span class="sxs-lookup"><span data-stu-id="74670-132">With [outgoing webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks), message your web service with an @mention.</span></span>

   :::column-end:::

   :::column span="":::

:::image type="content" source="assets/images/overview-connectors.png" alt-text="Концептуальное представление о том, как выглядят соединители в Teams клиенте." border="false":::

   :::column-end:::
:::row-end:::

### <a name="microsoft-graph-for-teams"></a><span data-ttu-id="74670-134">Microsoft Graph для Teams</span><span class="sxs-lookup"><span data-stu-id="74670-134">Microsoft Graph for Teams</span></span>

:::row:::

   :::column span="":::

<span data-ttu-id="74670-135">**Использование Teams** данных. [API microsoft Graph](/graph/teams-concept-overview) для Teams предоставляет доступ к сведениям о командах, каналах, пользователях и сообщениях, которые помогут вам создать или улучшить функции для вашего приложения (например, богатые уведомления).</span><span class="sxs-lookup"><span data-stu-id="74670-135">**Utilize Teams data**: The [Microsoft Graph API for Teams](/graph/teams-concept-overview) provides access to information about teams, channels, users, and messages that can help you create or enhance features for your app (such as rich notifications).</span></span>

   :::column-end:::

   :::column span="":::

:::image type="content" source="assets/images/overview-graph.png" alt-text="Концептуальное представление API microsoft Graph для Teams." border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="start-building"></a><span data-ttu-id="74670-137">Начало создания</span><span class="sxs-lookup"><span data-stu-id="74670-137">Start building</span></span>

<span data-ttu-id="74670-138">Быстро ознакомьтесь с созданием для Teams, настроив среду и создав простое приложение.</span><span class="sxs-lookup"><span data-stu-id="74670-138">Quickly familiarize yourself with building for Teams by setting up your environment and creating a simple app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="74670-139">Создание первого приложения</span><span class="sxs-lookup"><span data-stu-id="74670-139">Build your first app</span></span>](get-started/prerequisites.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="integrate-with-teams"></a><span data-ttu-id="74670-140">Интеграция с Teams</span><span class="sxs-lookup"><span data-stu-id="74670-140">Integrate with Teams</span></span>

<span data-ttu-id="74670-141">Смешайте функции, которые пользователи любят в существующем веб-приложении, службе или системе с функциями совместной работы Teams.</span><span class="sxs-lookup"><span data-stu-id="74670-141">Blend the features users love about an existing web app, service, or system with the collaborative features of Teams.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="74670-142">Интеграция существующего приложения</span><span class="sxs-lookup"><span data-stu-id="74670-142">Integrate an existing app</span></span>](samples/integrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="a-little-code-goes-a-long-way"></a><span data-ttu-id="74670-143">Маленький код проходит долгий путь</span><span class="sxs-lookup"><span data-stu-id="74670-143">A little code goes a long way</span></span>

<span data-ttu-id="74670-144">Вам не нужно быть программистом-экспертом, чтобы создать отличное Teams приложение.</span><span class="sxs-lookup"><span data-stu-id="74670-144">You don't need to be an expert programmer to build a great Teams app.</span></span> <span data-ttu-id="74670-145">Попробуйте одно из нескольких решений с низким кодом.</span><span class="sxs-lookup"><span data-stu-id="74670-145">Try one of several low-code solutions.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="74670-146">Создание приложения с низким кодом</span><span class="sxs-lookup"><span data-stu-id="74670-146">Create a low-code app</span></span>](samples/teams-low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="get-ideas-for-your-app"></a><span data-ttu-id="74670-147">Получить идеи для приложения</span><span class="sxs-lookup"><span data-stu-id="74670-147">Get ideas for your app</span></span>

<span data-ttu-id="74670-148">Ищете вдохновение для разработки приложений?</span><span class="sxs-lookup"><span data-stu-id="74670-148">Looking for app development inspiration?</span></span> <span data-ttu-id="74670-149">Просмотрите список реальных сценариев и отраслевых решений с помощью макетов концепции высокой верности, чтобы понять различные способы, Teams приложения могут помочь пользователям.</span><span class="sxs-lookup"><span data-stu-id="74670-149">Browse our list of real-world scenarios and industry solutions with high fidelity concept mocks to understand the various ways Teams apps can help your users.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="74670-150">См. сценарии приложений</span><span class="sxs-lookup"><span data-stu-id="74670-150">See app scenarios</span></span>](https://adoption.microsoft.com/extensibility-look-book/scenarios/)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="see-also"></a><span data-ttu-id="74670-151">См. также</span><span class="sxs-lookup"><span data-stu-id="74670-151">See also</span></span>

* [<span data-ttu-id="74670-152">Добавьте кнопку Share-to-Teams на веб-сайте</span><span class="sxs-lookup"><span data-stu-id="74670-152">Add a Share-to-Teams button to your website</span></span>](concepts/build-and-test/share-to-teams.md)
* [<span data-ttu-id="74670-153">Разработка Teams приложения</span><span class="sxs-lookup"><span data-stu-id="74670-153">Design your Teams app</span></span>](concepts/design/design-teams-app-overview.md)
* [<span data-ttu-id="74670-154">Microsoft Teams SDK клиента JavaScript</span><span class="sxs-lookup"><span data-stu-id="74670-154">Microsoft Teams JavaScript client SDK</span></span>](/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* <span data-ttu-id="74670-155">Bot Framework SDK для [JavaScript](https://github.com/Microsoft/botbuilder-js) и [.NET](https://github.com/Microsoft/botbuilder-dotnet/)</span><span class="sxs-lookup"><span data-stu-id="74670-155">Bot Framework SDK for [JavaScript](https://github.com/Microsoft/botbuilder-js) and [.NET](https://github.com/Microsoft/botbuilder-dotnet/)</span></span>
* [<span data-ttu-id="74670-156">Распространение приложения Teams</span><span class="sxs-lookup"><span data-stu-id="74670-156">Distribute your Teams app</span></span>](concepts/deploy-and-publish/apps-publish-overview.md)
