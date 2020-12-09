---
title: Разработка настраиваемого приложения
author: heath-hamilton
description: Узнайте, как проектировать приложения Microsoft Teams. Ресурсы включают набор элементов пользовательского интерфейса Microsoft Teams, рекомендации, примеры и многое другое.
ms.author: lajanuar
ms.topic: overview
ms.openlocfilehash: 0160a59ed4ebc51e900acbb5d74735ccae0b6083
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/09/2020
ms.locfileid: "49606270"
---
# <a name="designing-your-microsoft-teams-app"></a><span data-ttu-id="ce3b2-104">Разработка приложения Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="ce3b2-104">Designing your Microsoft Teams app</span></span>

:::image type="content" source="../../assets/images/design-guidelines-overview.png" alt-text="Концептуальное изображение содержит рекомендации по проектированию Microsoft Teams.":::

<span data-ttu-id="ce3b2-106">Независимо от того, являетесь ли вы дизайнером, менеджером по продуктам, разработчиком или производителем с помощью инструментов с небольшим кодом, эти рекомендации помогут вам быстро принять решение для вашего приложения Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="ce3b2-106">Whether you're a designer, product manager, developer, or maker using low-code tools, these guidelines can help you quickly make the right design decisions for your Microsoft Teams app.</span></span>

## <a name="teams-app-design-principles"></a><span data-ttu-id="ce3b2-107">Принципы разработки приложений Teams</span><span class="sxs-lookup"><span data-stu-id="ce3b2-107">Teams app design principles</span></span>

<span data-ttu-id="ce3b2-108">Приложения Teams помогают пользователям совместно присоединяться друг к другу.</span><span class="sxs-lookup"><span data-stu-id="ce3b2-108">Teams apps help people achieve more together.</span></span> <span data-ttu-id="ce3b2-109">Используйте эти принципы для создания руководства.</span><span class="sxs-lookup"><span data-stu-id="ce3b2-109">Use these principles to guide your design.</span></span>

:::row:::
   :::column span="":::

### <a name="collaborative"></a><span data-ttu-id="ce3b2-110">Совместной работы</span><span class="sxs-lookup"><span data-stu-id="ce3b2-110">Collaborative</span></span>

<span data-ttu-id="ce3b2-111">Приложения Teams помогают пользователям совместно присоединяться друг к другу.</span><span class="sxs-lookup"><span data-stu-id="ce3b2-111">Teams apps help people achieve more together.</span></span> <span data-ttu-id="ce3b2-112">Используйте эти принципы для создания руководства.</span><span class="sxs-lookup"><span data-stu-id="ce3b2-112">Use these principles to guide your design.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="trustworthy"></a><span data-ttu-id="ce3b2-113">Заслужив</span><span class="sxs-lookup"><span data-stu-id="ce3b2-113">Trustworthy</span></span>

<span data-ttu-id="ce3b2-114">Приложение является безопасным и соответствующим требованиям.</span><span class="sxs-lookup"><span data-stu-id="ce3b2-114">The app is secure and compliant.</span></span> <span data-ttu-id="ce3b2-115">Пользователи могут легко найти сведения о конфиденциальности.</span><span class="sxs-lookup"><span data-stu-id="ce3b2-115">Users can easily find information about privacy.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="globally-inclusive"></a><span data-ttu-id="ce3b2-116">Глобально включительно</span><span class="sxs-lookup"><span data-stu-id="ce3b2-116">Globally inclusive</span></span>

<span data-ttu-id="ce3b2-117">Люди со всеми фоновыми рисунками, скиллсетс и дисциплинами могут использовать приложение.</span><span class="sxs-lookup"><span data-stu-id="ce3b2-117">People of all backgrounds, skillsets, and disciplines can use the app.</span></span> <span data-ttu-id="ce3b2-118">Он культурно, раЦиалли и соЦиалли.</span><span class="sxs-lookup"><span data-stu-id="ce3b2-118">It’s culturally, racially, and socially aware.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="light"></a><span data-ttu-id="ce3b2-119">Легкие</span><span class="sxs-lookup"><span data-stu-id="ce3b2-119">Light</span></span>

<span data-ttu-id="ce3b2-120">Приложение фокусируется на основных сценариях, которые смешиваются с рабочими процессами Teams.</span><span class="sxs-lookup"><span data-stu-id="ce3b2-120">The app focuses on core scenarios that blend with Teams workflows.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="native-or-distinct"></a><span data-ttu-id="ce3b2-121">Native или DISTINCT</span><span class="sxs-lookup"><span data-stu-id="ce3b2-121">Native or distinct</span></span>

<span data-ttu-id="ce3b2-122">Приложение использует собственные компоненты для разработки Teams или свои собственные.</span><span class="sxs-lookup"><span data-stu-id="ce3b2-122">The app uses native Teams design components or your own.</span></span> <span data-ttu-id="ce3b2-123">Не существует смешения цветовых схем, элементов управления и т. д.</span><span class="sxs-lookup"><span data-stu-id="ce3b2-123">There’s no blend of color schemes, controls, etc.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="useful"></a><span data-ttu-id="ce3b2-124">Полезные</span><span class="sxs-lookup"><span data-stu-id="ce3b2-124">Useful</span></span>

<span data-ttu-id="ce3b2-125">Приложение основано на сценариях, необходимых пользователям в Teams.</span><span class="sxs-lookup"><span data-stu-id="ce3b2-125">The app is based on a scenario people need to do in Teams.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="easy-to-use"></a><span data-ttu-id="ce3b2-126">Простота использования</span><span class="sxs-lookup"><span data-stu-id="ce3b2-126">Easy to use</span></span>

<span data-ttu-id="ce3b2-127">Пользовательский интерфейс легко распознается, плеасант на внешнем виде и тона и повышает продуктивность работы пользователей.</span><span class="sxs-lookup"><span data-stu-id="ce3b2-127">The UI is easy to understand, pleasant in look and tone, and makes people more productive.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="responsive"></a><span data-ttu-id="ce3b2-128">Оперативно</span><span class="sxs-lookup"><span data-stu-id="ce3b2-128">Responsive</span></span>

<span data-ttu-id="ce3b2-129">Приложение не зависит от устройства и экрана.</span><span class="sxs-lookup"><span data-stu-id="ce3b2-129">The app is device and screen agnostic.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="accessible"></a><span data-ttu-id="ce3b2-130">Доступные</span><span class="sxs-lookup"><span data-stu-id="ce3b2-130">Accessible</span></span>

<span data-ttu-id="ce3b2-131">Приложение отвечает требованиям к специальным возможностям Teams с точки зрения цветовой контрастности, альтернативы навигации и т. д.</span><span class="sxs-lookup"><span data-stu-id="ce3b2-131">The app meets Teams accessibility requirements in terms of color contrast, navigation alternatives, and more.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="well-described"></a><span data-ttu-id="ce3b2-132">Хорошо сказано</span><span class="sxs-lookup"><span data-stu-id="ce3b2-132">Well described</span></span>

<span data-ttu-id="ce3b2-133">Текст, значки и изображения позволяют ясно понять, что такое приложение и как его использовать.</span><span class="sxs-lookup"><span data-stu-id="ce3b2-133">Text, icons, and images make it clear what the app is for and how to use it.</span></span>

   :::column-end:::
:::row-end:::

## <a name="creating-a-cohesive-experience"></a><span data-ttu-id="ce3b2-134">Создание взаимосвязных интерфейсов</span><span class="sxs-lookup"><span data-stu-id="ce3b2-134">Creating a cohesive experience</span></span>

<span data-ttu-id="ce3b2-135">Разработка приложения Teams аналогична разработке обычного веб-приложения, но и немного другой.</span><span class="sxs-lookup"><span data-stu-id="ce3b2-135">Designing a Teams app is like designing a conventional web app—but also a little different.</span></span> <span data-ttu-id="ce3b2-136">Эффективный проект выделяет уникальные атрибуты приложения, в то же время поддерживая их в соответствии с функциями и контекстами Teams.</span><span class="sxs-lookup"><span data-stu-id="ce3b2-136">An effective design highlights your app's unique attributes while fitting naturally with Teams features and contexts.</span></span>

<span data-ttu-id="ce3b2-137">Эти рекомендации и ресурсы могут помочь вам в этом балансе.</span><span class="sxs-lookup"><span data-stu-id="ce3b2-137">These guidelines and resources can help you strike that balance.</span></span> <span data-ttu-id="ce3b2-138">Вы узнаете, что делать и что следует избегать при проектировании приложения Teams (например, многоуровневая навигация на вкладке).</span><span class="sxs-lookup"><span data-stu-id="ce3b2-138">You'll know what to do and what to avoid when designing your Teams app (such as multi-level navigation in a tab).</span></span>

## <a name="planning-your-app"></a><span data-ttu-id="ce3b2-139">Планирование приложения</span><span class="sxs-lookup"><span data-stu-id="ce3b2-139">Planning your app</span></span>

<span data-ttu-id="ce3b2-140">Чтобы разработать высококачественное приложение для работы с Teams, необходимо сначала разодумать, что должно делать ваше приложение, а также как вы считаете, что он будет использоваться пользователями.</span><span class="sxs-lookup"><span data-stu-id="ce3b2-140">To design a high-quality Teams app, you must first understand what you want your app to do and how you think people will use it.</span></span> <span data-ttu-id="ce3b2-141">Если вы еще не сделали этого, [запланируйте приложение](../../concepts/extensibility-points.md)должным образом.</span><span class="sxs-lookup"><span data-stu-id="ce3b2-141">If you haven't already, take some time to properly [plan your app](../../concepts/extensibility-points.md).</span></span>

## <a name="design-fundamentals"></a><span data-ttu-id="ce3b2-142">Основы дизайна</span><span class="sxs-lookup"><span data-stu-id="ce3b2-142">Design fundamentals</span></span>

<span data-ttu-id="ce3b2-143">Изучите [основы разработки приложений Teams](design-teams-app-fundamentals.md), включая макет, цветовые схемы и многое другое.</span><span class="sxs-lookup"><span data-stu-id="ce3b2-143">Learn the [fundamentals of Teams app design](design-teams-app-fundamentals.md), including layout, color schemes, and more.</span></span>

## <a name="basic-fluent-ui-components-for-teams"></a><span data-ttu-id="ce3b2-144">Основные компоненты пользовательского интерфейса Fluent для Teams</span><span class="sxs-lookup"><span data-stu-id="ce3b2-144">Basic Fluent UI components for Teams</span></span>

<span data-ttu-id="ce3b2-145">В зависимости от пользовательского интерфейса Fluent они являются [основными элементами для создания привычных интерфейсов Teams](design-teams-app-basic-ui-components.md).</span><span class="sxs-lookup"><span data-stu-id="ce3b2-145">Based on Fluent UI, these are the [core elements for creating familiar Teams interfaces](design-teams-app-basic-ui-components.md).</span></span>

## <a name="app-capabilities"></a><span data-ttu-id="ce3b2-146">Возможности приложений</span><span class="sxs-lookup"><span data-stu-id="ce3b2-146">App capabilities</span></span>

<span data-ttu-id="ce3b2-147">Узнайте, как пользователи могут добавлять, использовать и управлять приложениями Teams, чтобы максимально использовать все возможности в вашем проекте.</span><span class="sxs-lookup"><span data-stu-id="ce3b2-147">Understand how people add, use, and manage Teams apps to make the most of each capability in your design.</span></span>

* [<span data-ttu-id="ce3b2-148">Персональные приложения</span><span class="sxs-lookup"><span data-stu-id="ce3b2-148">Personal apps</span></span>](../../concepts/design/personal-apps.md)
* [<span data-ttu-id="ce3b2-149">Вкладки</span><span class="sxs-lookup"><span data-stu-id="ce3b2-149">Tabs</span></span>](../../tabs/design/tabs.md)
* [<span data-ttu-id="ce3b2-150">Расширения для системы обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="ce3b2-150">Messaging extensions</span></span>](../../messaging-extensions/design/messaging-extension-design.md)
* [<span data-ttu-id="ce3b2-151">Боты</span><span class="sxs-lookup"><span data-stu-id="ce3b2-151">Bots</span></span>](../../bots/design/bots.md)
* [<span data-ttu-id="ce3b2-152">Расширения собраний</span><span class="sxs-lookup"><span data-stu-id="ce3b2-152">Meeting extensions</span></span>](../../apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [<span data-ttu-id="ce3b2-153">Модули задач</span><span class="sxs-lookup"><span data-stu-id="ce3b2-153">Task modules</span></span>](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)
* [<span data-ttu-id="ce3b2-154">Адаптивные карточки</span><span class="sxs-lookup"><span data-stu-id="ce3b2-154">Adaptive Cards</span></span>](../../task-modules-and-cards/cards/design-effective-cards.md)

## <a name="ui-templates"></a><span data-ttu-id="ce3b2-155">Шаблоны пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="ce3b2-155">UI templates</span></span>

<span data-ttu-id="ce3b2-156">Быстрое создание сложных высококачественных макетов с помощью [шаблонов для стандартных вариантов использования и рабочих процессов в Teams](design-teams-app-ui-templates.md).</span><span class="sxs-lookup"><span data-stu-id="ce3b2-156">Quickly create complex, high-fidelity designs with [templates for common Teams use cases and workflows](design-teams-app-ui-templates.md).</span></span>

## <a name="get-started-with-the-microsoft-teams-ui-kit"></a><span data-ttu-id="ce3b2-157">Начало работы с набором элементов пользовательского интерфейса Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="ce3b2-157">Get started with the Microsoft Teams UI Kit</span></span>

<span data-ttu-id="ce3b2-158">Набор элементов пользовательского интерфейса Microsoft Teams содержит компоненты пользовательского интерфейса, шаблоны и примеры, которые можно перетаскивать, удалять и изменять при необходимости.</span><span class="sxs-lookup"><span data-stu-id="ce3b2-158">The Microsoft Teams UI Kit has UI components, templates, and examples that you can drag, drop, and modify as needed.</span></span> <span data-ttu-id="ce3b2-159">Набор UI также содержит исчерпывающие сведения о том, как приложения должны выглядеть и работать в различных сценариях Teams.</span><span class="sxs-lookup"><span data-stu-id="ce3b2-159">The UI kit also includes comprehensive information about how apps should look and behave in different Teams scenarios.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ce3b2-160">Получение набора элементов пользовательского интерфейса Microsoft Teams (фигма)</span><span class="sxs-lookup"><span data-stu-id="ce3b2-160">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="other-resources"></a><span data-ttu-id="ce3b2-161">Другие ресурсы</span><span class="sxs-lookup"><span data-stu-id="ce3b2-161">Other resources</span></span>

<span data-ttu-id="ce3b2-162">Для получения дополнительных сведений попробуйте один из следующих ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ce3b2-162">To learn more, try one of the following resources.</span></span>

### <a name="fluent-ui"></a><span data-ttu-id="ce3b2-163">Пользовательский интерфейс Fluent</span><span class="sxs-lookup"><span data-stu-id="ce3b2-163">Fluent UI</span></span>

<span data-ttu-id="ce3b2-164">Получение примеров кода и сведений о реализации компонентов на основе пользовательского интерфейса Fluent, используемых для создания приложений Teams.</span><span class="sxs-lookup"><span data-stu-id="ce3b2-164">Get code samples and implementation details for the Fluent UI-based components used to build Teams experiences.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ce3b2-165">Испытать компоненты пользовательского интерфейса Teams (Fluent в пользовательском интерфейсе)</span><span class="sxs-lookup"><span data-stu-id="ce3b2-165">Try out Teams UI components (Fluent UI)</span></span>](https://fluentsite.z22.web.core.windows.net/)

### <a name="adaptive-cards-designer"></a><span data-ttu-id="ce3b2-166">Конструктор адаптивных карточек</span><span class="sxs-lookup"><span data-stu-id="ce3b2-166">Adaptive Cards designer</span></span>

<span data-ttu-id="ce3b2-167">Разработайте адаптивные карты в веб-инструменте.</span><span class="sxs-lookup"><span data-stu-id="ce3b2-167">Design Adaptive Cards in a web-based tool.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ce3b2-168">Попробуйте конструктор адаптивных карточек</span><span class="sxs-lookup"><span data-stu-id="ce3b2-168">Try the Adaptive Cards designer</span></span>](https://adaptivecards.io/designer/)
