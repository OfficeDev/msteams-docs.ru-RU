---
title: Создание приложений для платформы Microsoft Teams
author: heath-hamilton
description: Сведения о том, как разработчики могут расширять функции Microsoft Teams с помощью настраиваемого приложения.
ms.topic: overview
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: e40d2b0d8b0d12e6275b97f79d103310d22f9720
ms.sourcegitcommit: 3bd2627b7a334568f61ccc606395e3d89aa521d9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/31/2021
ms.locfileid: "51475930"
---
# <a name="build-apps-for-microsoft-teams"></a><span data-ttu-id="5d698-103">Создание приложений для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="5d698-103">Build apps for Microsoft Teams</span></span>

<span data-ttu-id="5d698-104">Приложения Microsoft Teams приносят ключевые сведения, общие инструменты и доверенные процессы в места, где люди все чаще собираются, учатся и работают.</span><span class="sxs-lookup"><span data-stu-id="5d698-104">Microsoft Teams apps bring key information, common tools, and trusted processes to where people increasingly gather, learn, and work.</span></span>

<span data-ttu-id="5d698-105">Приложения — это то, как вы расширяете Teams, чтобы соответствовать вашим потребностям.</span><span class="sxs-lookup"><span data-stu-id="5d698-105">Apps are how you extend Teams to fit your needs.</span></span> <span data-ttu-id="5d698-106">Создайте что-то совершенно новое для Teams или интегрируете существующее приложение.</span><span class="sxs-lookup"><span data-stu-id="5d698-106">Create something brand new for Teams or integrate an existing app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5d698-107">Начните отсюда</span><span class="sxs-lookup"><span data-stu-id="5d698-107">Start here</span></span>](build-your-first-app/build-first-app-overview.md)

## <a name="what-are-teams-apps"></a><span data-ttu-id="5d698-108">Что такое приложения Teams?</span><span class="sxs-lookup"><span data-stu-id="5d698-108">What are Teams apps?</span></span>

<span data-ttu-id="5d698-109">Приложения teams — это сочетание [возможностей и](concepts/capabilities-overview.md) [точек входа.](concepts/extensibility-points.md)</span><span class="sxs-lookup"><span data-stu-id="5d698-109">Teams apps are a combination of [capabilities](concepts/capabilities-overview.md) and [entry points](concepts/extensibility-points.md).</span></span> <span data-ttu-id="5d698-110">Например, люди могут общаться с  ботом (возможностью) вашего приложения в *канале* (точка входа).</span><span class="sxs-lookup"><span data-stu-id="5d698-110">For example, people can chat with your app's *bot* (capability) in a *channel* (entry point).</span></span>

<span data-ttu-id="5d698-111">Некоторые приложения просты (отправка уведомлений), а другие сложны (управление записями пациентов).</span><span class="sxs-lookup"><span data-stu-id="5d698-111">Some apps are simple (send notifications), while others are complex (manage patient records).</span></span> <span data-ttu-id="5d698-112">При планировании приложения помните, что Teams — это центр совместной работы.</span><span class="sxs-lookup"><span data-stu-id="5d698-112">When planning your app, remember that Teams is a collaboration hub.</span></span> <span data-ttu-id="5d698-113">Лучшие приложения Teams помогают людям лучше выражать себя и работать вместе.</span><span class="sxs-lookup"><span data-stu-id="5d698-113">The best Teams apps help people express themselves and work better together.</span></span>

:::row:::
   :::column span="":::

### <a name="tabs"></a><span data-ttu-id="5d698-114">Вкладки</span><span class="sxs-lookup"><span data-stu-id="5d698-114">Tabs</span></span>

<span data-ttu-id="5d698-115">**Получите сведения более удобно.** Иногда вам просто нужно упростить поиск.</span><span class="sxs-lookup"><span data-stu-id="5d698-115">**Get information more conveniently**: Sometimes you just need to make things easier to find.</span></span> <span data-ttu-id="5d698-116">Отображение важной веб-страницы [](tabs/what-are-tabs.md)на вкладке, которая обеспечивает полноэкранный веб-опыт для статического и динамического контента в Teams.</span><span class="sxs-lookup"><span data-stu-id="5d698-116">Display an important webpage in a [tab](tabs/what-are-tabs.md), which provides a full-screen web experience for static and dynamic content in Teams.</span></span>

:::image type="content" source="assets/images/overview-tabs.png" alt-text="Концептуальное представление о том, как выглядят вкладки в клиенте Teams." border="false":::

   :::column-end:::

   :::column span="":::

### <a name="bots"></a><span data-ttu-id="5d698-118">Боты</span><span class="sxs-lookup"><span data-stu-id="5d698-118">Bots</span></span>

<span data-ttu-id="5d698-119">**Превратите** слова в действия: беседы часто приводит к необходимости что-то делать (создать заказ, просмотреть код, проверить состояние билета и т.д.).</span><span class="sxs-lookup"><span data-stu-id="5d698-119">**Turn words into actions**: Conversations often result in the need to do something (generate an order, review my code, check ticket status, etc.).</span></span> <span data-ttu-id="5d698-120">Бот [может](bots/what-are-bots.md) скинуть эти типы рабочего процесса прямо внутри Teams.</span><span class="sxs-lookup"><span data-stu-id="5d698-120">A [bot](bots/what-are-bots.md) can kick off these kinds of workflows right inside Teams.</span></span>

:::image type="content" source="assets/images/overview-bots.png" alt-text="Концептуальное представление того, как выглядят боты в клиенте Teams." border="false":::

   :::column-end:::

:::row-end:::

:::row:::

   :::column span="":::

### <a name="messaging-extensions"></a><span data-ttu-id="5d698-122">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="5d698-122">Messaging extensions</span></span>

<span data-ttu-id="5d698-123">**Упростите многозадачную** работу. [С](messaging-extensions/what-are-messaging-extensions.md)помощью расширений обмена сообщениями можно быстро обмениваться внешней информацией в беседе.</span><span class="sxs-lookup"><span data-stu-id="5d698-123">**Make it easier to multitask**: With [messaging extensions](messaging-extensions/what-are-messaging-extensions.md), you can quickly share external information in a conversation.</span></span> <span data-ttu-id="5d698-124">Вы также можете действовать по сообщению, например, создать билет справки на основе контента сообщения канала.</span><span class="sxs-lookup"><span data-stu-id="5d698-124">You also can act on a message, such as creating a help ticket based on the content of a channel post.</span></span>

:::image type="content" source="assets\images\overview-messaging.png" alt-text="Концептуальное представление о том, как выглядят расширения обмена сообщениями в клиенте Teams." border="false":::

   :::column-end:::

   :::column span="":::

### <a name="webhooks"></a><span data-ttu-id="5d698-126">Веб-перехватчики</span><span class="sxs-lookup"><span data-stu-id="5d698-126">Webhooks</span></span>

<span data-ttu-id="5d698-127">**Связь с внешними приложениями.** [Входящие веб-сайты](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) — это простой способ автоматической отправки уведомлений из другого приложения в канал Teams.</span><span class="sxs-lookup"><span data-stu-id="5d698-127">**Communicate with external apps**: [Incoming webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) are a simple way to automatically send notifications from another app to a Teams channel.</span></span> <span data-ttu-id="5d698-128">В [исходяющих веб-сайтах](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks)сообщение веб-службы с помощью @mention.</span><span class="sxs-lookup"><span data-stu-id="5d698-128">With [outgoing webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks), message your web service with an @mention.</span></span>

:::image type="content" source="assets/images/overview-connectors.png" alt-text="Концептуальное представление того, как выглядят соединители в клиенте Teams." border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
:::row-end:::

### <a name="microsoft-graph-for-teams"></a><span data-ttu-id="5d698-130">Microsoft Graph для teams</span><span class="sxs-lookup"><span data-stu-id="5d698-130">Microsoft Graph for Teams</span></span>

<span data-ttu-id="5d698-131">**Использование данных Teams.** [API Microsoft Graph для Teams](https://docs.microsoft.com/graph/teams-concept-overview) предоставляет доступ к сведениям о командах, каналах, пользователях и сообщениях, которые помогут вам создать или улучшить функции для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="5d698-131">**Utilize Teams data**: The [Microsoft Graph API for Teams](https://docs.microsoft.com/graph/teams-concept-overview) provides access to information about teams, channels, users, and messages that can help you create or enhance features for your app.</span></span>

:::image type="content" source="assets/images/overview-graph.png" alt-text="Концептуальное представление API Microsoft Graph для Teams." border="false":::

   :::column-end:::
   :::column span="":::

:::row:::
   :::column span="2":::
   :::column-end:::
:::row-end:::

## <a name="build-solutions-for-microsoft-teams-apps"></a><span data-ttu-id="5d698-133">Создание решений для приложений Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="5d698-133">Build solutions for Microsoft Teams apps</span></span>
 
<span data-ttu-id="5d698-134">Корпорация Майкрософт предлагает книгу extensibility look , библиотеку сценариев для приложений Teams, организованных промышленностью.</span><span class="sxs-lookup"><span data-stu-id="5d698-134">Microsoft offers an extensibility look book, a scenario library for Teams apps organized by industry.</span></span> <span data-ttu-id="5d698-135">Эта книга помогает создавать приложения на платформе Teams и понимать различные возможные сценарии с помощью различных возможностей платформы Teams.</span><span class="sxs-lookup"><span data-stu-id="5d698-135">This book helps you build apps on the Teams platform and understand different possible scenarios using various Teams platform capabilities.</span></span> <span data-ttu-id="5d698-136">Сценарии книги look начинаются с бизнес-проблемы, лиц, вовлеченных вместе со своими проблемами, и заканчиваются решением приложения Teams для решения бизнес-потребностей.</span><span class="sxs-lookup"><span data-stu-id="5d698-136">The look book scenarios start with a business problem, the personas involved along with their challenges, and end with a Teams app solution addressing the business needs.</span></span>

<span data-ttu-id="5d698-137">Каждый сценарий в этой библиотеке сопровождается набором макетов концепции проектирования высокой верности, которые могут служить вдохновением для разработки приложений и улучшения пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="5d698-137">Each scenario in this library is accompanied by a set of high-fidelity design concept mocks, which can serve as an inspiration for designing your apps and enhancing user experience.</span></span> <span data-ttu-id="5d698-138">Кроме того, в книге "Внешний вид" освещаются лучшие практики проектирования и архитектуры при создании каждого приложения.</span><span class="sxs-lookup"><span data-stu-id="5d698-138">In addition, the look book highlights the design and architecture best practices followed in building each app.</span></span> <span data-ttu-id="5d698-139">Дополнительные сведения см. в книге extensibility look.</span><span class="sxs-lookup"><span data-stu-id="5d698-139">For more information, see the extensibility look book.</span></span> <span data-ttu-id="5d698-140">Дополнительные сведения см. [в книге extensibility look book.](https://adoption.microsoft.com/extensibility-look-book/scenarios/)</span><span class="sxs-lookup"><span data-stu-id="5d698-140">For more information, see [extensibility look book](https://adoption.microsoft.com/extensibility-look-book/scenarios/).</span></span> 

## <a name="start-building"></a><span data-ttu-id="5d698-141">Начало создания</span><span class="sxs-lookup"><span data-stu-id="5d698-141">Start building</span></span>

<span data-ttu-id="5d698-142">Быстро ознакомьтесь со зданием для Teams, создав простое приложение и добавив некоторые часто используемые возможности.</span><span class="sxs-lookup"><span data-stu-id="5d698-142">Quickly familiarize yourself with building for Teams by creating a simple app and adding some commonly used capabilities.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5d698-143">Создайте свое первое приложение сейчас</span><span class="sxs-lookup"><span data-stu-id="5d698-143">Build your first app now</span></span>](build-your-first-app/build-first-app-overview.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="integrate-with-teams"></a><span data-ttu-id="5d698-144">Интеграция с Teams</span><span class="sxs-lookup"><span data-stu-id="5d698-144">Integrate with Teams</span></span>

<span data-ttu-id="5d698-145">Сочетание функций, которые пользователи любят в существующем веб-приложении, службе или системе, с функциями совместной работы Teams.</span><span class="sxs-lookup"><span data-stu-id="5d698-145">Blend the features users love about an existing web app, service, or system with the collaborative features of Teams.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5d698-146">Интеграция существующего приложения</span><span class="sxs-lookup"><span data-stu-id="5d698-146">Integrate an existing app</span></span>](samples/integrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="a-little-code-goes-a-long-way"></a><span data-ttu-id="5d698-147">Маленький код проходит долгий путь</span><span class="sxs-lookup"><span data-stu-id="5d698-147">A little code goes a long way</span></span>

<span data-ttu-id="5d698-148">Вам не нужно быть программистом-экспертом, чтобы создать отличное приложение Teams.</span><span class="sxs-lookup"><span data-stu-id="5d698-148">You don't need to be an expert programmer to build a great Teams app.</span></span> <span data-ttu-id="5d698-149">Попробуйте одно из нескольких решений с низким кодом.</span><span class="sxs-lookup"><span data-stu-id="5d698-149">Try one of several low-code solutions.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5d698-150">Создание приложения с низким кодом</span><span class="sxs-lookup"><span data-stu-id="5d698-150">Create a low-code app</span></span>](samples/teams-low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="resources"></a><span data-ttu-id="5d698-151">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="5d698-151">Resources</span></span>

* [<span data-ttu-id="5d698-152">Добавление кнопки Share-to-Teams на веб-сайт</span><span class="sxs-lookup"><span data-stu-id="5d698-152">Add a Share-to-Teams button to your website</span></span>](concepts/build-and-test/share-to-teams.md)
* [<span data-ttu-id="5d698-153">Разработка приложения Teams</span><span class="sxs-lookup"><span data-stu-id="5d698-153">Design your Teams app</span></span>](concepts/design/design-teams-app-overview.md)
* [<span data-ttu-id="5d698-154">Клиент Microsoft Teams JavaScript SDK</span><span class="sxs-lookup"><span data-stu-id="5d698-154">Microsoft Teams JavaScript client SDK</span></span>](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* <span data-ttu-id="5d698-155">Bot Framework SDK для [JavaScript](https://github.com/Microsoft/botbuilder-js) и [.NET](https://github.com/Microsoft/botbuilder-dotnet/)</span><span class="sxs-lookup"><span data-stu-id="5d698-155">Bot Framework SDK for [JavaScript](https://github.com/Microsoft/botbuilder-js) and [.NET](https://github.com/Microsoft/botbuilder-dotnet/)</span></span>
* [<span data-ttu-id="5d698-156">Публикация приложения Teams</span><span class="sxs-lookup"><span data-stu-id="5d698-156">Publish your Teams app</span></span>](concepts/deploy-and-publish/overview.md)
