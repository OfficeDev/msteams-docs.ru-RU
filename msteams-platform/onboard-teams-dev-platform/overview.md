---
title: Платформа для разработчиков Microsoft Teams
author: clearab
description: Общие сведения о том, как разработчики могут расширять и настраивать функции Microsoft Teams с помощью платформы Teams.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 73cbd4f68d8878872147bd412972495de1b5de6e
ms.sourcegitcommit: d3bb4bbcdff9545c9869647dcdbe563a2db868be
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/18/2020
ms.locfileid: "47964573"
---
# <a name="building-for-microsoft-teams"></a><span data-ttu-id="cbdc1-103">Создание для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="cbdc1-103">Building for Microsoft Teams</span></span>

<span data-ttu-id="cbdc1-104">Приложения Microsoft Teams обеспечивают ключевые сведения, общие инструменты и надежные процессы, где люди все еще собирают, изученируют и работают.</span><span class="sxs-lookup"><span data-stu-id="cbdc1-104">Microsoft Teams apps bring key information, common tools, and trusted processes to where people increasingly gather, learn, and work.</span></span>

<span data-ttu-id="cbdc1-105">Приложения — это то, как вы расширяете Teams в соответствии со своими потребностями.</span><span class="sxs-lookup"><span data-stu-id="cbdc1-105">Apps are how you extend Teams to fit your needs.</span></span> <span data-ttu-id="cbdc1-106">Создание новой фирменной символики для Teams или интеграция существующего приложения.</span><span class="sxs-lookup"><span data-stu-id="cbdc1-106">Create something brand new for Teams or integrate an existing app.</span></span>

## <a name="what-are-teams-apps"></a><span data-ttu-id="cbdc1-107">Что такое приложения Teams?</span><span class="sxs-lookup"><span data-stu-id="cbdc1-107">What are Teams apps?</span></span>

<span data-ttu-id="cbdc1-108">Люди обнаруживают и используют приложения Teams через набор [возможностей](capabilities-overview.md)платформы.</span><span class="sxs-lookup"><span data-stu-id="cbdc1-108">People discover and use Teams apps through a set of platform [capabilities](capabilities-overview.md).</span></span>

<span data-ttu-id="cbdc1-109">Некоторые приложения просты (уведомления об отправке), а другие — сложным (Просмотр записей пациента).</span><span class="sxs-lookup"><span data-stu-id="cbdc1-109">Some apps are simple (send notifications), while others are complex (view patient records).</span></span> <span data-ttu-id="cbdc1-110">При планировании приложения помните, что Teams — это центр для совместной работы.</span><span class="sxs-lookup"><span data-stu-id="cbdc1-110">When planning your app, remember that Teams is a collaboration hub.</span></span> <span data-ttu-id="cbdc1-111">Лучшие приложения Teams помогают людям выразить себя и лучше работают вместе.</span><span class="sxs-lookup"><span data-stu-id="cbdc1-111">The best Teams apps help people express themselves and work better together.</span></span>

:::row:::
   :::column span="":::

### <a name="tabs"></a><span data-ttu-id="cbdc1-112">Вкладки</span><span class="sxs-lookup"><span data-stu-id="cbdc1-112">Tabs</span></span>

<span data-ttu-id="cbdc1-113">**Более удобное для получения сведений**: иногда вам нужно просто упростить поиск.</span><span class="sxs-lookup"><span data-stu-id="cbdc1-113">**Get information more conveniently**: Sometimes you just need to make things easier to find.</span></span> <span data-ttu-id="cbdc1-114">Отображение важной веб-страницы на [вкладке](../tabs/what-are-tabs.md), которая предоставляет полноэкранный веб-интерфейс для статического и динамического контента в Teams.</span><span class="sxs-lookup"><span data-stu-id="cbdc1-114">Display an important webpage in a [tab](../tabs/what-are-tabs.md), which provides a full-screen web experience for static and dynamic content in Teams.</span></span>

:::image type="content" source="doc-links/images/overview-tabs.png" alt-text="Концептуальное представление вкладок, которые выглядят как в клиенте Teams." border="false":::

   :::column-end:::
   :::column span="":::

### <a name="messaging-extensions"></a><span data-ttu-id="cbdc1-116">расширения для обмена сообщениями;</span><span class="sxs-lookup"><span data-stu-id="cbdc1-116">Messaging extensions</span></span>

<span data-ttu-id="cbdc1-117">**Упрощение задач**: благодаря [расширениям обмена сообщениями](../messaging-extensions/what-are-messaging-extensions.md)вы можете быстро поделиться внешними сведениями в беседе.</span><span class="sxs-lookup"><span data-stu-id="cbdc1-117">**Make it easier to multitask**: With [messaging extensions](../messaging-extensions/what-are-messaging-extensions.md), you can quickly share external information in a conversation.</span></span> <span data-ttu-id="cbdc1-118">Кроме того, можно выполнить действия с сообщением, например создать билет справки на основе контента канала POST.</span><span class="sxs-lookup"><span data-stu-id="cbdc1-118">You also can act on a message, such as creating a help ticket based on the content of a channel post.</span></span>

:::image type="content" source="doc-links/images/overview-messaging.png" alt-text="Концептуальное представление расширений обмена сообщениями в клиенте Teams выглядит как." border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="bots"></a><span data-ttu-id="cbdc1-120">Боты</span><span class="sxs-lookup"><span data-stu-id="cbdc1-120">Bots</span></span>

<span data-ttu-id="cbdc1-121">**Включение слов в действия**: беседы часто приводят к необходимости выполнять какие-либо действия (создание заказа, просмотр кода, проверка состояния билета и т. д.).</span><span class="sxs-lookup"><span data-stu-id="cbdc1-121">**Turn words into actions**: Conversations often result in the need to do something (generate an order, review my code, check ticket status, etc.).</span></span> <span data-ttu-id="cbdc1-122">С помощью [Bot](../bots/what-are-bots.md) можно запускать эти рабочие процессы прямо в Teams.</span><span class="sxs-lookup"><span data-stu-id="cbdc1-122">A [bot](../bots/what-are-bots.md) can kick off these kinds of workflows right inside Teams.</span></span>

:::image type="content" source="doc-links/images/overview-bots.png" alt-text="Концептуальное представление того, как боты выглядит в клиенте Teams." border="false":::

   :::column-end:::
   :::column span="":::

### <a name="webhooks"></a><span data-ttu-id="cbdc1-124">веб-перехватчики</span><span class="sxs-lookup"><span data-stu-id="cbdc1-124">Webhooks</span></span>

<span data-ttu-id="cbdc1-125">**Обмен данными с внешними приложениями**: [Входящие веб-перехватчики](../webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) это простой способ автоматически отправлять уведомления из другого приложения в канал Teams.</span><span class="sxs-lookup"><span data-stu-id="cbdc1-125">**Communicate with external apps**: [Incoming webhooks](../webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) are a simple way to automatically send notifications from another app to a Teams channel.</span></span> <span data-ttu-id="cbdc1-126">С [исходящими веб-перехватчиками](../webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks)запросите у веб-службы @mention.</span><span class="sxs-lookup"><span data-stu-id="cbdc1-126">With [outgoing webhooks](../webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks), message your web service with an @mention.</span></span>

:::image type="content" source="doc-links/images/overview-connectors.png" alt-text="Концептуальное представление соединителей, имеющих вид в клиенте Teams." border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="microsoft-graph-for-teams"></a><span data-ttu-id="cbdc1-128">Microsoft Graph для Teams</span><span class="sxs-lookup"><span data-stu-id="cbdc1-128">Microsoft Graph for Teams</span></span>

<span data-ttu-id="cbdc1-129">**Использование данных Teams**: [REST API Microsoft Graph для Teams](https://docs.microsoft.com/graph/teams-concept-overview) предоставляет доступ к сведениям о Teams, каналах, пользователях и сообщениях, которые помогут вам создать или улучшить возможности приложения.</span><span class="sxs-lookup"><span data-stu-id="cbdc1-129">**Utilize Teams data**: The [Microsoft Graph REST API for Teams](https://docs.microsoft.com/graph/teams-concept-overview) provides access to information about teams, channels, users, and messages that can help you create or enhance features for your app.</span></span>

:::image type="content" source="doc-links/images/overview-graph.png" alt-text="Концептуальное представление REST API Microsoft Graph для Teams." border="false":::

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="get-started"></a><span data-ttu-id="cbdc1-131">Начало работы</span><span class="sxs-lookup"><span data-stu-id="cbdc1-131">Get started</span></span>

<span data-ttu-id="cbdc1-132">Вы можете перейти непосредственно к нашим первым руководствам по приложениям, узнать, как интегрировать и импортировать существующие приложения, или познакомиться со временем жизненного цикла разработки приложений Teams.</span><span class="sxs-lookup"><span data-stu-id="cbdc1-132">Jump right in with our first app tutorials, find out how to integrate and import existing apps, or take your time to learn about the Teams app development lifecycle.</span></span>

:::row:::
   :::column span="2":::

### <a name="start-building"></a><span data-ttu-id="cbdc1-133">Начало создания</span><span class="sxs-lookup"><span data-stu-id="cbdc1-133">Start building</span></span>

   <span data-ttu-id="cbdc1-134">Быстро ознакомьтесь со сборкой для Teams, создав простое приложение и добавив некоторые часто используемые возможности.</span><span class="sxs-lookup"><span data-stu-id="cbdc1-134">Quickly familiarize yourself with building for Teams by creating a simple app and adding some commonly used capabilities.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="cbdc1-135">Создайте свое первое приложение сейчас</span><span class="sxs-lookup"><span data-stu-id="cbdc1-135">Build your first app now</span></span>](build-your-first-app/building-real-world-app.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

### <a name="integrate-with-teams"></a><span data-ttu-id="cbdc1-136">Интеграция с Teams</span><span class="sxs-lookup"><span data-stu-id="cbdc1-136">Integrate with Teams</span></span>

   <span data-ttu-id="cbdc1-137">Функция смешения пользователи любовь о существующем веб-приложении, службе или системе с функциями совместной работы Teams.</span><span class="sxs-lookup"><span data-stu-id="cbdc1-137">Blend the features users love about an existing web app, service, or system with the collaborative features of Teams.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="cbdc1-138">Интеграция существующего приложения</span><span class="sxs-lookup"><span data-stu-id="cbdc1-138">Integrate an existing app</span></span>](migrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

### <a name="a-little-code-goes-a-long-way"></a><span data-ttu-id="cbdc1-139">Небольшой код проходит много времени</span><span class="sxs-lookup"><span data-stu-id="cbdc1-139">A little code goes a long way</span></span>

   <span data-ttu-id="cbdc1-140">Вам не нужно быть экспертным программистом, чтобы создать удобное приложение Teams.</span><span class="sxs-lookup"><span data-stu-id="cbdc1-140">You don't need to be an expert programmer to build a great Teams app.</span></span> <span data-ttu-id="cbdc1-141">Попробуйте одно из нескольких решений с небольшим кодом.</span><span class="sxs-lookup"><span data-stu-id="cbdc1-141">Try one of several low-code solutions.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="cbdc1-142">Создание приложения с небольшим кодом</span><span class="sxs-lookup"><span data-stu-id="cbdc1-142">Create a low-code app</span></span>](low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

### <a name="trust-the-process"></a><span data-ttu-id="cbdc1-143">Доверие процессу</span><span class="sxs-lookup"><span data-stu-id="cbdc1-143">Trust the process</span></span>

   <span data-ttu-id="cbdc1-144">Узнайте, как весь процесс разработки платформы Teams для эффективного планирования, проектирования, построения и публикации приложения для вашей организации или для любого пользователя.</span><span class="sxs-lookup"><span data-stu-id="cbdc1-144">Learn the entire Teams platform development process to effectively plan, design, build, and publish an app for your organization or anyone.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="cbdc1-145">Начало планирования приложения</span><span class="sxs-lookup"><span data-stu-id="cbdc1-145">Start planning your app</span></span>](../concepts/extensibility-points.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="resources"></a><span data-ttu-id="cbdc1-146">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="cbdc1-146">Resources</span></span>

* [<span data-ttu-id="cbdc1-147">Добавление на веб-сайт кнопки "общий доступ" в Teams</span><span class="sxs-lookup"><span data-stu-id="cbdc1-147">Add a Share to Teams button to your website</span></span>](../concepts/build-and-test/share-to-teams.md)
* [<span data-ttu-id="cbdc1-148">Система дизайна Fluent</span><span class="sxs-lookup"><span data-stu-id="cbdc1-148">Fluent Design System</span></span>](https://fluentsite.z22.web.core.windows.net/)
* [<span data-ttu-id="cbdc1-149">Пакет SDK для JavaScript Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="cbdc1-149">Microsoft Teams JavaScript SDK</span></span>](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* <span data-ttu-id="cbdc1-150">[Пакет SDK Bot Framework для JavaScript](https://github.com/Microsoft/botbuilder-js) и [пакет SDK для Bot Framework для .NET](https://github.com/Microsoft/botbuilder-dotnet/)</span><span class="sxs-lookup"><span data-stu-id="cbdc1-150">[Bot Framework SDK for JavaScript](https://github.com/Microsoft/botbuilder-js) and [Bot Framework SDK for .NET](https://github.com/Microsoft/botbuilder-dotnet/)</span></span>
* [<span data-ttu-id="cbdc1-151">Публикация приложения в организации или AppSource</span><span class="sxs-lookup"><span data-stu-id="cbdc1-151">Publish your app to an organization or AppSource</span></span>](../concepts/deploy-and-publish/overview.md)
