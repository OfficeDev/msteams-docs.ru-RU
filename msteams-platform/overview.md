---
title: Создание приложений для платформы Microsoft Teams
author: heath-hamilton
description: Общие сведения о том, как разработчики могут расширять и настраивать функции Microsoft Teams с помощью настраиваемых приложений.
ms.topic: overview
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 6f5f3454885320669ef42383529d39fcfcfdfee8
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/09/2020
ms.locfileid: "49604789"
---
# <a name="build-apps-for-microsoft-teams"></a><span data-ttu-id="3a88b-103">Создание приложений для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="3a88b-103">Build apps for Microsoft Teams</span></span>

<span data-ttu-id="3a88b-104">Приложения Microsoft Teams обеспечивают ключевые сведения, общие инструменты и надежные процессы, где люди все еще собирают, изученируют и работают.</span><span class="sxs-lookup"><span data-stu-id="3a88b-104">Microsoft Teams apps bring key information, common tools, and trusted processes to where people increasingly gather, learn, and work.</span></span>

<span data-ttu-id="3a88b-105">Приложения — это то, как вы расширяете Teams в соответствии со своими потребностями.</span><span class="sxs-lookup"><span data-stu-id="3a88b-105">Apps are how you extend Teams to fit your needs.</span></span> <span data-ttu-id="3a88b-106">Создание новой фирменной символики для Teams или интеграция существующего приложения.</span><span class="sxs-lookup"><span data-stu-id="3a88b-106">Create something brand new for Teams or integrate an existing app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3a88b-107">Начните отсюда</span><span class="sxs-lookup"><span data-stu-id="3a88b-107">Start here</span></span>](build-your-first-app/build-first-app-overview.md)

## <a name="what-are-teams-apps"></a><span data-ttu-id="3a88b-108">Что такое приложения Teams?</span><span class="sxs-lookup"><span data-stu-id="3a88b-108">What are Teams apps?</span></span>

<span data-ttu-id="3a88b-109">Приложения Teams представляют собой сочетание [возможностей](concepts/capabilities-overview.md) и [точек входа](concepts/extensibility-points.md).</span><span class="sxs-lookup"><span data-stu-id="3a88b-109">Teams apps are a combination of [capabilities](concepts/capabilities-overview.md) and [entry points](concepts/extensibility-points.md).</span></span> <span data-ttu-id="3a88b-110">Например, люди могут общаться с *роботом* приложения (возможностями) в *канале* (точке входа).</span><span class="sxs-lookup"><span data-stu-id="3a88b-110">For example, people can chat with your app's *bot* (capability) in a *channel* (entry point).</span></span>

<span data-ttu-id="3a88b-111">Некоторые приложения просты (уведомления об отправке), а другие — сложными (Управление записями пациента).</span><span class="sxs-lookup"><span data-stu-id="3a88b-111">Some apps are simple (send notifications), while others are complex (manage patient records).</span></span> <span data-ttu-id="3a88b-112">При планировании приложения помните, что Teams — это центр для совместной работы.</span><span class="sxs-lookup"><span data-stu-id="3a88b-112">When planning your app, remember that Teams is a collaboration hub.</span></span> <span data-ttu-id="3a88b-113">Лучшие приложения Teams помогают людям выразить себя и лучше работают вместе.</span><span class="sxs-lookup"><span data-stu-id="3a88b-113">The best Teams apps help people express themselves and work better together.</span></span>

:::row:::
   :::column span="":::

### <a name="tabs"></a><span data-ttu-id="3a88b-114">Вкладки</span><span class="sxs-lookup"><span data-stu-id="3a88b-114">Tabs</span></span>

<span data-ttu-id="3a88b-115">**Более удобное для получения сведений**: иногда вам нужно просто упростить поиск.</span><span class="sxs-lookup"><span data-stu-id="3a88b-115">**Get information more conveniently**: Sometimes you just need to make things easier to find.</span></span> <span data-ttu-id="3a88b-116">Отображение важной веб-страницы на [вкладке](tabs/what-are-tabs.md), которая предоставляет полноэкранный веб-интерфейс для статического и динамического контента в Teams.</span><span class="sxs-lookup"><span data-stu-id="3a88b-116">Display an important webpage in a [tab](tabs/what-are-tabs.md), which provides a full-screen web experience for static and dynamic content in Teams.</span></span>

:::image type="content" source="assets/images/overview-tabs.png" alt-text="Концептуальное представление вкладок, которые выглядят как в клиенте Teams." border="false":::

   :::column-end:::
   :::column span="":::

### <a name="messaging-extensions"></a><span data-ttu-id="3a88b-118">расширения для обмена сообщениями;</span><span class="sxs-lookup"><span data-stu-id="3a88b-118">Messaging extensions</span></span>

<span data-ttu-id="3a88b-119">**Упрощение задач**: благодаря [расширениям обмена сообщениями](messaging-extensions/what-are-messaging-extensions.md)вы можете быстро поделиться внешними сведениями в беседе.</span><span class="sxs-lookup"><span data-stu-id="3a88b-119">**Make it easier to multitask**: With [messaging extensions](messaging-extensions/what-are-messaging-extensions.md), you can quickly share external information in a conversation.</span></span> <span data-ttu-id="3a88b-120">Кроме того, можно выполнить действия с сообщением, например создать билет справки на основе контента канала POST.</span><span class="sxs-lookup"><span data-stu-id="3a88b-120">You also can act on a message, such as creating a help ticket based on the content of a channel post.</span></span>

:::image type="content" source="assets\images\overview-messaging.png" alt-text="Концептуальное представление расширений обмена сообщениями в клиенте Teams выглядит как." border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="bots"></a><span data-ttu-id="3a88b-122">Боты</span><span class="sxs-lookup"><span data-stu-id="3a88b-122">Bots</span></span>

<span data-ttu-id="3a88b-123">**Включение слов в действия**: беседы часто приводят к необходимости выполнять какие-либо действия (создание заказа, просмотр кода, проверка состояния билета и т. д.).</span><span class="sxs-lookup"><span data-stu-id="3a88b-123">**Turn words into actions**: Conversations often result in the need to do something (generate an order, review my code, check ticket status, etc.).</span></span> <span data-ttu-id="3a88b-124">С помощью [Bot](bots/what-are-bots.md) можно запускать эти рабочие процессы прямо в Teams.</span><span class="sxs-lookup"><span data-stu-id="3a88b-124">A [bot](bots/what-are-bots.md) can kick off these kinds of workflows right inside Teams.</span></span>

:::image type="content" source="assets/images/overview-bots.png" alt-text="Концептуальное представление того, как боты выглядит в клиенте Teams." border="false":::

   :::column-end:::
   :::column span="":::

### <a name="webhooks"></a><span data-ttu-id="3a88b-126">веб-перехватчики</span><span class="sxs-lookup"><span data-stu-id="3a88b-126">Webhooks</span></span>

<span data-ttu-id="3a88b-127">**Обмен данными с внешними приложениями**: [Входящие веб-перехватчики](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) это простой способ автоматически отправлять уведомления из другого приложения в канал Teams.</span><span class="sxs-lookup"><span data-stu-id="3a88b-127">**Communicate with external apps**: [Incoming webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) are a simple way to automatically send notifications from another app to a Teams channel.</span></span> <span data-ttu-id="3a88b-128">С [исходящими веб-перехватчиками](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks)запросите у веб-службы @mention.</span><span class="sxs-lookup"><span data-stu-id="3a88b-128">With [outgoing webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks), message your web service with an @mention.</span></span>

:::image type="content" source="assets/images/overview-connectors.png" alt-text="Концептуальное представление соединителей, имеющих вид в клиенте Teams." border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="microsoft-graph-for-teams"></a><span data-ttu-id="3a88b-130">Microsoft Graph для Teams</span><span class="sxs-lookup"><span data-stu-id="3a88b-130">Microsoft Graph for Teams</span></span>

<span data-ttu-id="3a88b-131">**Использование данных Teams**: [API Microsoft Graph для Teams](https://docs.microsoft.com/graph/teams-concept-overview) предоставляет доступ к сведениям о командах, каналах, пользователях и сообщениях, которые помогут вам создать или улучшить возможности приложения.</span><span class="sxs-lookup"><span data-stu-id="3a88b-131">**Utilize Teams data**: The [Microsoft Graph API for Teams](https://docs.microsoft.com/graph/teams-concept-overview) provides access to information about teams, channels, users, and messages that can help you create or enhance features for your app.</span></span>

:::image type="content" source="assets/images/overview-graph.png" alt-text="Концептуальное представление API Microsoft Graph для Teams." border="false":::

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="get-started"></a><span data-ttu-id="3a88b-133">Начало работы</span><span class="sxs-lookup"><span data-stu-id="3a88b-133">Get started</span></span>

<span data-ttu-id="3a88b-134">Приступите к работе с нашими первыми приложениями и Узнайте, как интегрировать и импортировать существующие приложения.</span><span class="sxs-lookup"><span data-stu-id="3a88b-134">Jump right in with our first app tutorials or find out how to integrate and import existing apps.</span></span>

:::row:::
   :::column span="2":::

### <a name="start-building"></a><span data-ttu-id="3a88b-135">Начало создания</span><span class="sxs-lookup"><span data-stu-id="3a88b-135">Start building</span></span>

   <span data-ttu-id="3a88b-136">Быстро ознакомьтесь со сборкой для Teams, создав простое приложение и добавив некоторые часто используемые возможности.</span><span class="sxs-lookup"><span data-stu-id="3a88b-136">Quickly familiarize yourself with building for Teams by creating a simple app and adding some commonly used capabilities.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="3a88b-137">Создайте свое первое приложение сейчас</span><span class="sxs-lookup"><span data-stu-id="3a88b-137">Build your first app now</span></span>](build-your-first-app/build-first-app-overview.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

### <a name="integrate-with-teams"></a><span data-ttu-id="3a88b-138">Интеграция с Teams</span><span class="sxs-lookup"><span data-stu-id="3a88b-138">Integrate with Teams</span></span>

   <span data-ttu-id="3a88b-139">Функция смешения пользователи любовь о существующем веб-приложении, службе или системе с функциями совместной работы Teams.</span><span class="sxs-lookup"><span data-stu-id="3a88b-139">Blend the features users love about an existing web app, service, or system with the collaborative features of Teams.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="3a88b-140">Интеграция существующего приложения</span><span class="sxs-lookup"><span data-stu-id="3a88b-140">Integrate an existing app</span></span>](samples/integrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

### <a name="a-little-code-goes-a-long-way"></a><span data-ttu-id="3a88b-141">Небольшой код проходит много времени</span><span class="sxs-lookup"><span data-stu-id="3a88b-141">A little code goes a long way</span></span>

   <span data-ttu-id="3a88b-142">Вам не нужно быть экспертным программистом, чтобы создать удобное приложение Teams.</span><span class="sxs-lookup"><span data-stu-id="3a88b-142">You don't need to be an expert programmer to build a great Teams app.</span></span> <span data-ttu-id="3a88b-143">Попробуйте одно из нескольких решений с небольшим кодом.</span><span class="sxs-lookup"><span data-stu-id="3a88b-143">Try one of several low-code solutions.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="3a88b-144">Создание приложения с небольшим кодом</span><span class="sxs-lookup"><span data-stu-id="3a88b-144">Create a low-code app</span></span>](samples/teams-low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="resources"></a><span data-ttu-id="3a88b-145">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="3a88b-145">Resources</span></span>

* [<span data-ttu-id="3a88b-146">Добавление на веб-сайт кнопки "общий доступ" в Teams</span><span class="sxs-lookup"><span data-stu-id="3a88b-146">Add a Share to Teams button to your website</span></span>](concepts/build-and-test/share-to-teams.md)
* <span data-ttu-id="3a88b-147"><a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">Пользовательский интерфейс Fluent</a></span><span class="sxs-lookup"><span data-stu-id="3a88b-147"><a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">Fluent UI</a></span></span>
* [<span data-ttu-id="3a88b-148">Пакет SDK для клиента Microsoft Teams JavaScript</span><span class="sxs-lookup"><span data-stu-id="3a88b-148">Microsoft Teams JavaScript client SDK</span></span>](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* <span data-ttu-id="3a88b-149">[Пакет SDK Bot Framework для JavaScript](https://github.com/Microsoft/botbuilder-js) и [пакет SDK для Bot Framework для .NET](https://github.com/Microsoft/botbuilder-dotnet/)</span><span class="sxs-lookup"><span data-stu-id="3a88b-149">[Bot Framework SDK for JavaScript](https://github.com/Microsoft/botbuilder-js) and [Bot Framework SDK for .NET](https://github.com/Microsoft/botbuilder-dotnet/)</span></span>
* [<span data-ttu-id="3a88b-150">Публикация приложения в организации или AppSource</span><span class="sxs-lookup"><span data-stu-id="3a88b-150">Publish your app to an organization or AppSource</span></span>](concepts/deploy-and-publish/overview.md)
