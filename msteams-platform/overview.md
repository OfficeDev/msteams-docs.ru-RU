---
title: Создание приложений для платформы Microsoft Teams
author: heath-hamilton
description: Получите обзор того, как разработчики могут расширить возможности Microsoft Teams с помощью пользовательских приложений.
ms.topic: overview
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 9f043fd5bab441ce88b0e04b4254b925aff25aad
ms.sourcegitcommit: 00c657e3bf57d3b92aca7da941cde47a2eeff4d0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/20/2021
ms.locfileid: "49911886"
---
# <a name="build-apps-for-microsoft-teams"></a><span data-ttu-id="35a78-103">Создание приложений для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="35a78-103">Build apps for Microsoft Teams</span></span>

<span data-ttu-id="35a78-104">Приложения Microsoft Teams используют ключевую информацию, общие инструменты и доверенные процессы, в которые все чаще собираются, учитесь и работают люди.</span><span class="sxs-lookup"><span data-stu-id="35a78-104">Microsoft Teams apps bring key information, common tools, and trusted processes to where people increasingly gather, learn, and work.</span></span>

<span data-ttu-id="35a78-105">Приложения — это то, как вы расширяете Teams в своих потребностях.</span><span class="sxs-lookup"><span data-stu-id="35a78-105">Apps are how you extend Teams to fit your needs.</span></span> <span data-ttu-id="35a78-106">Создайте что-то совершенно новое для Teams или интегрируем существующее приложение.</span><span class="sxs-lookup"><span data-stu-id="35a78-106">Create something brand new for Teams or integrate an existing app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="35a78-107">Начните отсюда</span><span class="sxs-lookup"><span data-stu-id="35a78-107">Start here</span></span>](build-your-first-app/build-first-app-overview.md)

## <a name="what-are-teams-apps"></a><span data-ttu-id="35a78-108">Что такое приложения Teams?</span><span class="sxs-lookup"><span data-stu-id="35a78-108">What are Teams apps?</span></span>

<span data-ttu-id="35a78-109">Приложения Teams — это сочетание [возможностей и](concepts/capabilities-overview.md) [точек входа.](concepts/extensibility-points.md)</span><span class="sxs-lookup"><span data-stu-id="35a78-109">Teams apps are a combination of [capabilities](concepts/capabilities-overview.md) and [entry points](concepts/extensibility-points.md).</span></span> <span data-ttu-id="35a78-110">Например, люди могут общаться в  чате с ботом (возможностью) вашего приложения в *канале* (точке входа).</span><span class="sxs-lookup"><span data-stu-id="35a78-110">For example, people can chat with your app's *bot* (capability) in a *channel* (entry point).</span></span>

<span data-ttu-id="35a78-111">Некоторые приложения простые (отправка уведомлений), а другие сложные (управление записями пациентов).</span><span class="sxs-lookup"><span data-stu-id="35a78-111">Some apps are simple (send notifications), while others are complex (manage patient records).</span></span> <span data-ttu-id="35a78-112">При планировании приложения помните, что Teams — это центр совместной работы.</span><span class="sxs-lookup"><span data-stu-id="35a78-112">When planning your app, remember that Teams is a collaboration hub.</span></span> <span data-ttu-id="35a78-113">Лучшие приложения Teams помогают людям самовыражаться и работать вместе.</span><span class="sxs-lookup"><span data-stu-id="35a78-113">The best Teams apps help people express themselves and work better together.</span></span>

:::row:::
   :::column span="":::

### <a name="tabs"></a><span data-ttu-id="35a78-114">Вкладки</span><span class="sxs-lookup"><span data-stu-id="35a78-114">Tabs</span></span>

<span data-ttu-id="35a78-115">**Более удобный способ получения** информации: иногда требуется упростить поиск.</span><span class="sxs-lookup"><span data-stu-id="35a78-115">**Get information more conveniently**: Sometimes you just need to make things easier to find.</span></span> <span data-ttu-id="35a78-116">Отображение важной веб-страницы [](tabs/what-are-tabs.md)на вкладке, которая обеспечивает полноэкранное веб-изображение для статического и динамического содержимого в Teams.</span><span class="sxs-lookup"><span data-stu-id="35a78-116">Display an important webpage in a [tab](tabs/what-are-tabs.md), which provides a full-screen web experience for static and dynamic content in Teams.</span></span>

:::image type="content" source="assets/images/overview-tabs.png" alt-text="Концептуальное представление вкладки в клиенте Teams." border="false":::

   :::column-end:::

   :::column span="":::

### <a name="bots"></a><span data-ttu-id="35a78-118">Боты</span><span class="sxs-lookup"><span data-stu-id="35a78-118">Bots</span></span>

<span data-ttu-id="35a78-119">**Превратить слова в действия:** беседы часто приводит к необходимости что-то делать (создать заказ, просмотреть мой код, проверить состояние билета и т. д.).</span><span class="sxs-lookup"><span data-stu-id="35a78-119">**Turn words into actions**: Conversations often result in the need to do something (generate an order, review my code, check ticket status, etc.).</span></span> <span data-ttu-id="35a78-120">Бот [может](bots/what-are-bots.md) прикатить эти типы рабочего процесса прямо в Teams.</span><span class="sxs-lookup"><span data-stu-id="35a78-120">A [bot](bots/what-are-bots.md) can kick off these kinds of workflows right inside Teams.</span></span>

:::image type="content" source="assets/images/overview-bots.png" alt-text="Концептуальное представление того, как боты выглядят в клиенте Teams." border="false":::

   :::column-end:::

:::row-end:::

:::row:::

   :::column span="":::

### <a name="messaging-extensions"></a><span data-ttu-id="35a78-122">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="35a78-122">Messaging extensions</span></span>

<span data-ttu-id="35a78-123">**Упростить** многозадачи: с [](messaging-extensions/what-are-messaging-extensions.md)помощью расширений обмена сообщениями можно быстро обмениваться внешней информацией в беседе.</span><span class="sxs-lookup"><span data-stu-id="35a78-123">**Make it easier to multitask**: With [messaging extensions](messaging-extensions/what-are-messaging-extensions.md), you can quickly share external information in a conversation.</span></span> <span data-ttu-id="35a78-124">Вы также можете действовать над сообщением, например создавать обращение в справку на основе содержимого публикации в канале.</span><span class="sxs-lookup"><span data-stu-id="35a78-124">You also can act on a message, such as creating a help ticket based on the content of a channel post.</span></span>

:::image type="content" source="assets\images\overview-messaging.png" alt-text="Концептуальное представление расширений обмена сообщениями в клиенте Teams." border="false":::

   :::column-end:::

   :::column span="":::

### <a name="webhooks"></a><span data-ttu-id="35a78-126">веб-перехватчики</span><span class="sxs-lookup"><span data-stu-id="35a78-126">Webhooks</span></span>

<span data-ttu-id="35a78-127">**Общение с внешними приложениями:** [входящие](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) веб-ookы — это простой способ автоматической отправки уведомлений из другого приложения в канал Teams.</span><span class="sxs-lookup"><span data-stu-id="35a78-127">**Communicate with external apps**: [Incoming webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) are a simple way to automatically send notifications from another app to a Teams channel.</span></span> <span data-ttu-id="35a78-128">С [помощью исходяющих веб-hooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks)сообщение веб-службы с помощью @mention.</span><span class="sxs-lookup"><span data-stu-id="35a78-128">With [outgoing webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks), message your web service with an @mention.</span></span>

:::image type="content" source="assets/images/overview-connectors.png" alt-text="Концептуальное представление того, как выглядят соединители в клиенте Teams." border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="microsoft-graph-for-teams"></a><span data-ttu-id="35a78-130">Microsoft Graph для Teams</span><span class="sxs-lookup"><span data-stu-id="35a78-130">Microsoft Graph for Teams</span></span>

<span data-ttu-id="35a78-131">**Использование данных Teams:** [API Microsoft Graph](https://docs.microsoft.com/graph/teams-concept-overview) для Teams предоставляет доступ к сведениям о командах, каналах, пользователях и сообщениях, которые помогут вам создать или улучшить функции для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="35a78-131">**Utilize Teams data**: The [Microsoft Graph API for Teams](https://docs.microsoft.com/graph/teams-concept-overview) provides access to information about teams, channels, users, and messages that can help you create or enhance features for your app.</span></span>

:::image type="content" source="assets/images/overview-graph.png" alt-text="Концептуальное представление API Microsoft Graph для Teams." border="false":::

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="start-building"></a><span data-ttu-id="35a78-133">Начало построения</span><span class="sxs-lookup"><span data-stu-id="35a78-133">Start building</span></span>

   <span data-ttu-id="35a78-134">Быстро ознакомьтесь с процессом создания для Teams, создав простое приложение и добавив некоторые часто используемые возможности.</span><span class="sxs-lookup"><span data-stu-id="35a78-134">Quickly familiarize yourself with building for Teams by creating a simple app and adding some commonly used capabilities.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="35a78-135">Создайте свое первое приложение сейчас</span><span class="sxs-lookup"><span data-stu-id="35a78-135">Build your first app now</span></span>](build-your-first-app/build-first-app-overview.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="integrate-with-teams"></a><span data-ttu-id="35a78-136">Интеграция с Teams</span><span class="sxs-lookup"><span data-stu-id="35a78-136">Integrate with Teams</span></span>

   <span data-ttu-id="35a78-137">Смешивайте функции, которые нравится пользователям в существующем веб-приложении, службе или системе, с функциями teams для совместной работы.</span><span class="sxs-lookup"><span data-stu-id="35a78-137">Blend the features users love about an existing web app, service, or system with the collaborative features of Teams.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="35a78-138">Интеграция существующего приложения</span><span class="sxs-lookup"><span data-stu-id="35a78-138">Integrate an existing app</span></span>](samples/integrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="a-little-code-goes-a-long-way"></a><span data-ttu-id="35a78-139">Небольшой код проходит длинный путь</span><span class="sxs-lookup"><span data-stu-id="35a78-139">A little code goes a long way</span></span>

   <span data-ttu-id="35a78-140">Для создания отличного приложения Teams не требуется быть экспертом-программистом.</span><span class="sxs-lookup"><span data-stu-id="35a78-140">You don't need to be an expert programmer to build a great Teams app.</span></span> <span data-ttu-id="35a78-141">Попробуйте одно из нескольких решений с низким кодом.</span><span class="sxs-lookup"><span data-stu-id="35a78-141">Try one of several low-code solutions.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="35a78-142">Создание приложения с низким кодом</span><span class="sxs-lookup"><span data-stu-id="35a78-142">Create a low-code app</span></span>](samples/teams-low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="resources"></a><span data-ttu-id="35a78-143">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="35a78-143">Resources</span></span>

* [<span data-ttu-id="35a78-144">Добавление кнопки "Поделиться в Teams" на веб-сайт</span><span class="sxs-lookup"><span data-stu-id="35a78-144">Add a Share-to-Teams button to your website</span></span>](concepts/build-and-test/share-to-teams.md)
* [<span data-ttu-id="35a78-145">Проектирование приложения Teams</span><span class="sxs-lookup"><span data-stu-id="35a78-145">Design your Teams app</span></span>](concepts/design/design-teams-app-overview.md)
* [<span data-ttu-id="35a78-146">Microsoft Teams JavaScript client SDK</span><span class="sxs-lookup"><span data-stu-id="35a78-146">Microsoft Teams JavaScript client SDK</span></span>](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* <span data-ttu-id="35a78-147">Bot Framework SDK для [JavaScript](https://github.com/Microsoft/botbuilder-js) и [.NET](https://github.com/Microsoft/botbuilder-dotnet/)</span><span class="sxs-lookup"><span data-stu-id="35a78-147">Bot Framework SDK for [JavaScript](https://github.com/Microsoft/botbuilder-js) and [.NET](https://github.com/Microsoft/botbuilder-dotnet/)</span></span>
* [<span data-ttu-id="35a78-148">Публикация приложения Teams</span><span class="sxs-lookup"><span data-stu-id="35a78-148">Publish your Teams app</span></span>](concepts/deploy-and-publish/overview.md)
