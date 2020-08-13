---
title: Платформа для разработчиков Teams
author: clearab
description: Общие сведения о том, как разработчики могут расширять и настраивать функции Microsoft Teams с помощью платформы Teams.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: d127acb33212f23dff9cf0dd83a1936044c10d5e
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/12/2020
ms.locfileid: "46652119"
---
# <a name="building-for-microsoft-teams"></a><span data-ttu-id="1662d-103">Создание для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="1662d-103">Building for Microsoft Teams</span></span>

<span data-ttu-id="1662d-104">Приложения Microsoft Teams обеспечивают ключевые сведения, общие инструменты и надежные процессы, где люди все еще собирают, изученируют и работают.</span><span class="sxs-lookup"><span data-stu-id="1662d-104">Microsoft Teams apps bring key information, common tools, and trusted processes to where people increasingly gather, learn, and work.</span></span>

<span data-ttu-id="1662d-105">Приложения — это то, как вы расширяете Teams в соответствии со своими потребностями.</span><span class="sxs-lookup"><span data-stu-id="1662d-105">Apps are how you extend Teams to fit your needs.</span></span> <span data-ttu-id="1662d-106">Вы можете создать новую фирменную символику для Teams или просто интегрировать функции в избранные приложения и службы.</span><span class="sxs-lookup"><span data-stu-id="1662d-106">You can create something brand new for Teams or simply integrate features in your favorite apps and services.</span></span>

## <a name="what-can-teams-apps-do"></a><span data-ttu-id="1662d-107">Что могут делать приложения Teams?</span><span class="sxs-lookup"><span data-stu-id="1662d-107">What can Teams apps do?</span></span>

<span data-ttu-id="1662d-108">Люди обнаруживают и используют приложения Teams через набор [возможностей](capabilities-overview.md)платформы.</span><span class="sxs-lookup"><span data-stu-id="1662d-108">People discover and use Teams apps through a set of platform [capabilities](capabilities-overview.md).</span></span>

<span data-ttu-id="1662d-109">Некоторые приложения просты (уведомления об отправке), а другие — сложным (Просмотр записей пациента).</span><span class="sxs-lookup"><span data-stu-id="1662d-109">Some apps are simple (send notifications), while others are complex (view patient records).</span></span> <span data-ttu-id="1662d-110">При планировании приложения помните, что Teams — это центр для совместной работы.</span><span class="sxs-lookup"><span data-stu-id="1662d-110">When planning your app, remember that Teams is a collaboration hub.</span></span> <span data-ttu-id="1662d-111">Лучшие приложения Teams помогают людям выразить себя и лучше работают вместе.</span><span class="sxs-lookup"><span data-stu-id="1662d-111">The best Teams apps help people express themselves and work better together.</span></span>

### <a name="get-information-more-conveniently"></a><span data-ttu-id="1662d-112">Более удобное получение информации</span><span class="sxs-lookup"><span data-stu-id="1662d-112">Get information more conveniently</span></span>

<span data-ttu-id="1662d-113">Иногда вам нужно просто упростить поиск.</span><span class="sxs-lookup"><span data-stu-id="1662d-113">Sometimes you just need to make things easier to find.</span></span> <span data-ttu-id="1662d-114">Отображение важной веб-страницы на [вкладке](doc-links/what-are-tabs.md), которая предоставляет полноэкранный веб-интерфейс для статического и динамического контента в Teams.</span><span class="sxs-lookup"><span data-stu-id="1662d-114">Display an important webpage in a [tab](doc-links/what-are-tabs.md), which provides a full-screen web experience for static and dynamic content in Teams.</span></span>

![Концептуальное представление вкладок, которые выглядят как в клиенте Teams.](doc-links/images/overview-tabs.png)

### <a name="share-links-without-switching-context"></a><span data-ttu-id="1662d-116">Совместное использование ссылок без переключения контекста</span><span class="sxs-lookup"><span data-stu-id="1662d-116">Share links without switching context</span></span>

<span data-ttu-id="1662d-117">Извлекать информацию в беседу и никогда не оставлять Teams.</span><span class="sxs-lookup"><span data-stu-id="1662d-117">Pull information into a conversation and never leave Teams.</span></span> <span data-ttu-id="1662d-118">Например, с [расширениями обмена сообщениями](doc-links/what-are-messaging-extensions.md) вы можете поделиться богатыми и легко дижестибле контентом из внешней системы с помощью поля "Создание сообщения".</span><span class="sxs-lookup"><span data-stu-id="1662d-118">For example, with [messaging extensions](doc-links/what-are-messaging-extensions.md) you can share rich, easily digestible content from an external system using the message compose box.</span></span>

![Концептуальное представление расширений обмена сообщениями, которые выглядят как в клиенте Teams](doc-links\images\overview-messaging.png)

### <a name="turn-words-into-actions"></a><span data-ttu-id="1662d-120">Включение слов в действия</span><span class="sxs-lookup"><span data-stu-id="1662d-120">Turn words into actions</span></span>

<span data-ttu-id="1662d-121">Беседы часто приводят к необходимости выполнения каких-либо действий (создание заказа, просмотр кода и т. д.).</span><span class="sxs-lookup"><span data-stu-id="1662d-121">Conversations often result in the need to do something (create an order, review my code, etc.).</span></span> <span data-ttu-id="1662d-122">С помощью [Bot](doc-links/what-are-bots.md) можно запускать эти рабочие процессы прямо в Teams.</span><span class="sxs-lookup"><span data-stu-id="1662d-122">A [bot](doc-links/what-are-bots.md) can kick off these kinds of workflows right inside Teams.</span></span>

![Концептуальное представление того, как боты выглядит в клиенте Teams](doc-links/images/overview-bots.png)

### <a name="communicate-with-external-apps-and-services"></a><span data-ttu-id="1662d-124">Обмен данными с внешними приложениями и службами</span><span class="sxs-lookup"><span data-stu-id="1662d-124">Communicate with external apps and services</span></span>

<span data-ttu-id="1662d-125">[Входящие веб-перехватчики](doc-links/what-are-webhooks-and-connectors.md#incoming-webhooks) это простой способ автоматически отправлять оповещения из другого приложения в канал команд или чат.</span><span class="sxs-lookup"><span data-stu-id="1662d-125">[Incoming webhooks](doc-links/what-are-webhooks-and-connectors.md#incoming-webhooks) are a simple way to automatically send alerts from another app to a Teams channel or chat.</span></span> <span data-ttu-id="1662d-126">С помощью [исходящих веб-перехватчиков](doc-links/what-are-webhooks-and-connectors.md#outgoing-webhooks)вы можете отправить сообщение в веб-службу с помощью @mention.</span><span class="sxs-lookup"><span data-stu-id="1662d-126">With [outgoing webhooks](doc-links/what-are-webhooks-and-connectors.md#outgoing-webhooks), you can send a message to your web service with an @mention.</span></span>

![Концептуальное представление соединителей, имеющих вид в клиенте Teams.](doc-links/images/overview-connectors.png)

### <a name="utilize-teams-data"></a><span data-ttu-id="1662d-128">Использование данных Teams</span><span class="sxs-lookup"><span data-stu-id="1662d-128">Utilize Teams data</span></span>

<span data-ttu-id="1662d-129">[REST API Microsoft Graph для Teams](https://docs.microsoft.com/graph/teams-concept-overview) предоставляет доступ к сведениям о командах, каналах, пользователях и сообщениях, которые помогут вам создать или улучшить возможности приложения.</span><span class="sxs-lookup"><span data-stu-id="1662d-129">The [Microsoft Graph REST API for Teams](https://docs.microsoft.com/graph/teams-concept-overview) provides access to information about teams, channels, users, and messages that can help you create or enhance features for your app.</span></span>

!["Концептуальное представление REST API Microsoft Graph для Teams](doc-links/images/overview-graph.png)
  
## <a name="start-building"></a><span data-ttu-id="1662d-131">Начало создания</span><span class="sxs-lookup"><span data-stu-id="1662d-131">Start building</span></span>

   <span data-ttu-id="1662d-132">Быстро ознакомьтесь со сборкой для Teams, создав простое приложение и добавив пару часто используемых возможностей.</span><span class="sxs-lookup"><span data-stu-id="1662d-132">Quickly familiarize yourself with building for Teams by creating a simple app and adding a couple commonly used capabilities.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="1662d-133">Создайте свое первое приложение сейчас</span><span class="sxs-lookup"><span data-stu-id="1662d-133">Build your first app now</span></span>](build-your-first-app/build-real-world-app.md)

### <a name="bring-it-all-together"></a><span data-ttu-id="1662d-134">Совместное объединение</span><span class="sxs-lookup"><span data-stu-id="1662d-134">Bring it all together</span></span>

   <span data-ttu-id="1662d-135">Упрощение процессов и рабочих процессов для пользователей путем перехода к избранным веб-приложениям, службам и системам Организации с помощью функций совместной работы в Teams.</span><span class="sxs-lookup"><span data-stu-id="1662d-135">Simplify processes and workflows for users by blending your organization's favorite web apps, services, and systems with Teams collaborative features.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="1662d-136">Интеграция существующего приложения</span><span class="sxs-lookup"><span data-stu-id="1662d-136">Integrate an existing app</span></span>](doc-links/integrating-web-apps.md)

### <a name="trust-the-process"></a><span data-ttu-id="1662d-137">Доверие процессу</span><span class="sxs-lookup"><span data-stu-id="1662d-137">Trust the process</span></span>

   <span data-ttu-id="1662d-138">Узнайте, как весь процесс разработки платформы Teams для эффективного планирования, проектирования, построения и публикации приложения для вашей организации или для любого пользователя.</span><span class="sxs-lookup"><span data-stu-id="1662d-138">Understand the entire Teams platform development process to effectively plan, design, build, and publish an app for your organization or anyone.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="1662d-139">Начало планирования приложения</span><span class="sxs-lookup"><span data-stu-id="1662d-139">Start planning your app</span></span>](doc-links/extensibility-points.md)

### <a name="no-code-no-worries"></a><span data-ttu-id="1662d-140">Нет кода, нет проблем</span><span class="sxs-lookup"><span data-stu-id="1662d-140">No code, no worries</span></span>

   <span data-ttu-id="1662d-141">Вам не нужно быть программистом, чтобы создать отличное приложение.</span><span class="sxs-lookup"><span data-stu-id="1662d-141">You don't need to be a programmer to build a great app.</span></span> <span data-ttu-id="1662d-142">Создайте приложение Teams с минимальным количеством кода, используя платформу Microsoft Power.</span><span class="sxs-lookup"><span data-stu-id="1662d-142">Create a Teams app with little to no code using the Microsoft Power Platform.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="1662d-143">Импорт приложения Power Platform</span><span class="sxs-lookup"><span data-stu-id="1662d-143">Import a Power Platform app</span></span>](doc-links/importing-custom-microsoft-apps.md)

## <a name="resources"></a><span data-ttu-id="1662d-144">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="1662d-144">Resources</span></span>

* [<span data-ttu-id="1662d-145">Добавление на веб-сайт кнопки "общий доступ" в Teams</span><span class="sxs-lookup"><span data-stu-id="1662d-145">Add a Share to Teams button to your website</span></span>](doc-links/share-to-teams.md)
* [<span data-ttu-id="1662d-146">Создание приложения с использованием рекомендуемых рекомендаций</span><span class="sxs-lookup"><span data-stu-id="1662d-146">Design your app using recommended guidelines</span></span>](doc-links/designing-overview.md)
* [<span data-ttu-id="1662d-147">Система дизайна пользовательского интерфейса Fluent</span><span class="sxs-lookup"><span data-stu-id="1662d-147">Fluent UI Design System</span></span>](https://fluentsite.z22.web.core.windows.net/)
* [<span data-ttu-id="1662d-148">Пакет SDK для клиента Microsoft Teams JavaScript</span><span class="sxs-lookup"><span data-stu-id="1662d-148">Microsoft Teams JavaScript client SDK</span></span>](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest)
* <span data-ttu-id="1662d-149">[Пакет SDK Bot Framework для JavaScript](https://github.com/Microsoft/botbuilder-js) и [пакет SDK для Bot Framework для .NET](https://github.com/Microsoft/botbuilder-dotnet/)</span><span class="sxs-lookup"><span data-stu-id="1662d-149">[Bot Framework SDK for JavaScript](https://github.com/Microsoft/botbuilder-js) and [Bot Framework SDK for .NET](https://github.com/Microsoft/botbuilder-dotnet/)</span></span>
