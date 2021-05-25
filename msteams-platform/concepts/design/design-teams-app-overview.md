---
title: Разработка настраиваемой приложения
author: heath-hamilton
description: Узнайте, как создать Microsoft Teams приложения. Ресурсы включают набор Microsoft Teams пользовательского интерфейса, лучшие практики, примеры и другие.
localization_priority: Normal
ms.author: surbhigupta
ms.topic: overview
ms.openlocfilehash: 19b8f8cbcbc52aa02ccd5d94f5bc4c088f2ae28a
ms.sourcegitcommit: 4224c44d169b1a289cbf1d3353de6bc6de7c7ea8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/25/2021
ms.locfileid: "52644877"
---
# <a name="designing-your-microsoft-teams-app"></a><span data-ttu-id="765eb-104">Проектирование Microsoft Teams приложения</span><span class="sxs-lookup"><span data-stu-id="765eb-104">Designing your Microsoft Teams app</span></span>

:::image type="content" source="../../assets/images/design-guidelines-overview.png" alt-text="Концептуальное изображение, Microsoft Teams рекомендации по разработке.":::

<span data-ttu-id="765eb-106">Независимо от того, являетесь ли вы дизайнером, менеджером по продуктам, разработчиком или создателем с помощью инструментов с низким кодом, эти рекомендации помогут вам быстро принять правильные решения по разработке для Microsoft Teams приложения.</span><span class="sxs-lookup"><span data-stu-id="765eb-106">Whether you're a designer, product manager, developer, or maker using low-code tools, these guidelines can help you quickly make the right design decisions for your Microsoft Teams app.</span></span>

## <a name="creating-a-cohesive-experience"></a><span data-ttu-id="765eb-107">Создание сплоченного опыта</span><span class="sxs-lookup"><span data-stu-id="765eb-107">Creating a cohesive experience</span></span>

<span data-ttu-id="765eb-108">Проектирование приложения Teams похоже на разработку обычного веб-приложения, но также немного отличается.</span><span class="sxs-lookup"><span data-stu-id="765eb-108">Designing a Teams app is like designing a conventional web app—but also a little different.</span></span> <span data-ttu-id="765eb-109">Эффективный дизайн подчеркивает уникальные атрибуты вашего приложения, при этом естественно примыкает к Teams и контекстам.</span><span class="sxs-lookup"><span data-stu-id="765eb-109">An effective design highlights your app's unique attributes while fitting naturally with Teams features and contexts.</span></span>

<span data-ttu-id="765eb-110">Эти рекомендации и ресурсы помогут вам найти баланс.</span><span class="sxs-lookup"><span data-stu-id="765eb-110">These guidelines and resources can help you strike that balance.</span></span> <span data-ttu-id="765eb-111">Вы узнаете, что делать и чего следует избегать при разработке Teams приложения (например, многоуровневой навигации на вкладке).</span><span class="sxs-lookup"><span data-stu-id="765eb-111">You'll know what to do and what to avoid when designing your Teams app (such as multi-level navigation in a tab).</span></span>

## <a name="teams-app-design-principles"></a><span data-ttu-id="765eb-112">Teams принципы разработки приложений</span><span class="sxs-lookup"><span data-stu-id="765eb-112">Teams app design principles</span></span>

<span data-ttu-id="765eb-113">Teams приложения помогают людям добиться большего вместе.</span><span class="sxs-lookup"><span data-stu-id="765eb-113">Teams apps help people achieve more together.</span></span> <span data-ttu-id="765eb-114">Используйте эти принципы для руководства разработкой.</span><span class="sxs-lookup"><span data-stu-id="765eb-114">Use these principles to guide your design.</span></span>

:::row:::
   :::column span="":::

### <a name="collaborative"></a><span data-ttu-id="765eb-115">Совместная работа</span><span class="sxs-lookup"><span data-stu-id="765eb-115">Collaborative</span></span>

<span data-ttu-id="765eb-116">Teams приложения помогают людям добиться большего вместе.</span><span class="sxs-lookup"><span data-stu-id="765eb-116">Teams apps help people achieve more together.</span></span> <span data-ttu-id="765eb-117">Используйте эти принципы для руководства разработкой.</span><span class="sxs-lookup"><span data-stu-id="765eb-117">Use these principles to guide your design.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="trustworthy"></a><span data-ttu-id="765eb-118">Надежность</span><span class="sxs-lookup"><span data-stu-id="765eb-118">Trustworthy</span></span>

<span data-ttu-id="765eb-119">Приложение является безопасным и совместимым.</span><span class="sxs-lookup"><span data-stu-id="765eb-119">The app is secure and compliant.</span></span> <span data-ttu-id="765eb-120">Пользователи могут легко найти сведения о конфиденциальности.</span><span class="sxs-lookup"><span data-stu-id="765eb-120">Users can easily find information about privacy.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="globally-inclusive"></a><span data-ttu-id="765eb-121">Глобальный инклюзивный</span><span class="sxs-lookup"><span data-stu-id="765eb-121">Globally inclusive</span></span>

<span data-ttu-id="765eb-122">В приложении могут использоваться люди всех слоев, навыков и дисциплин.</span><span class="sxs-lookup"><span data-stu-id="765eb-122">People of all backgrounds, skillsets, and disciplines can use the app.</span></span> <span data-ttu-id="765eb-123">Это культурно, расово и социально известно.</span><span class="sxs-lookup"><span data-stu-id="765eb-123">It’s culturally, racially, and socially aware.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="light"></a><span data-ttu-id="765eb-124">Легкие</span><span class="sxs-lookup"><span data-stu-id="765eb-124">Light</span></span>

<span data-ttu-id="765eb-125">Приложение фокусируется на основных сценариях, которые сочетаются с Teams процессами.</span><span class="sxs-lookup"><span data-stu-id="765eb-125">The app focuses on core scenarios that blend with Teams workflows.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="native-or-distinct"></a><span data-ttu-id="765eb-126">Native или distinct</span><span class="sxs-lookup"><span data-stu-id="765eb-126">Native or distinct</span></span>

<span data-ttu-id="765eb-127">Приложение использует собственные компоненты Teams или собственные.</span><span class="sxs-lookup"><span data-stu-id="765eb-127">The app uses native Teams design components or your own.</span></span> <span data-ttu-id="765eb-128">Нет смеси цветовой схемы, элементов управления и так далее.</span><span class="sxs-lookup"><span data-stu-id="765eb-128">There’s no blend of color schemes, controls, and so on.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="useful"></a><span data-ttu-id="765eb-129">Полезные</span><span class="sxs-lookup"><span data-stu-id="765eb-129">Useful</span></span>

<span data-ttu-id="765eb-130">Приложение основано на сценарии, который необходимо сделать в Teams.</span><span class="sxs-lookup"><span data-stu-id="765eb-130">The app is based on a scenario people need to do in Teams.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="easy-to-use"></a><span data-ttu-id="765eb-131">Простой в использовании</span><span class="sxs-lookup"><span data-stu-id="765eb-131">Easy to use</span></span>

<span data-ttu-id="765eb-132">Пользовательский интерфейс прост в понятном, приятном в взгляде и тоне и делает людей более продуктивными.</span><span class="sxs-lookup"><span data-stu-id="765eb-132">The UI is easy to understand, pleasant in look and tone, and makes people more productive.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="responsive"></a><span data-ttu-id="765eb-133">Оперативно</span><span class="sxs-lookup"><span data-stu-id="765eb-133">Responsive</span></span>

<span data-ttu-id="765eb-134">Приложение является агностиком устройства и экрана.</span><span class="sxs-lookup"><span data-stu-id="765eb-134">The app is device and screen agnostic.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="accessible"></a><span data-ttu-id="765eb-135">Доступные</span><span class="sxs-lookup"><span data-stu-id="765eb-135">Accessible</span></span>

<span data-ttu-id="765eb-136">Приложение отвечает Teams доступности с точки зрения контрастности цвета, альтернатив навигации и других.</span><span class="sxs-lookup"><span data-stu-id="765eb-136">The app meets Teams accessibility requirements in terms of color contrast, navigation alternatives, and more.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="well-described"></a><span data-ttu-id="765eb-137">Хорошо описано</span><span class="sxs-lookup"><span data-stu-id="765eb-137">Well described</span></span>

<span data-ttu-id="765eb-138">Текст, значки и изображения четко поймют, для чего приложение и как его использовать.</span><span class="sxs-lookup"><span data-stu-id="765eb-138">Text, icons, and images make it clear what the app is for and how to use it.</span></span>

   :::column-end:::
:::row-end:::

## <a name="teams-design-system"></a><span data-ttu-id="765eb-139">Teams системы проектирования</span><span class="sxs-lookup"><span data-stu-id="765eb-139">Teams design system</span></span>

<span data-ttu-id="765eb-140">Узнайте основы [разработки Teams,](design-teams-app-fundamentals.md)включая макет, цветовые схемы и другие.</span><span class="sxs-lookup"><span data-stu-id="765eb-140">Learn the [fundamentals of Teams app design](design-teams-app-fundamentals.md), including layout, color schemes, and more.</span></span>

## <a name="app-capabilities"></a><span data-ttu-id="765eb-141">Возможности приложений</span><span class="sxs-lookup"><span data-stu-id="765eb-141">App capabilities</span></span>

<span data-ttu-id="765eb-142">Понимание того, как люди добавляют, используют и Teams приложения, чтобы использовать все возможности в вашем дизайне.</span><span class="sxs-lookup"><span data-stu-id="765eb-142">Understand how people add, use, and manage Teams apps to make the most of each capability in your design.</span></span>

* [<span data-ttu-id="765eb-143">Персональные приложения</span><span class="sxs-lookup"><span data-stu-id="765eb-143">Personal apps</span></span>](../../concepts/design/personal-apps.md)
* [<span data-ttu-id="765eb-144">Вкладки</span><span class="sxs-lookup"><span data-stu-id="765eb-144">Tabs</span></span>](../../tabs/design/tabs.md)
* [<span data-ttu-id="765eb-145">Расширения для системы обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="765eb-145">Messaging extensions</span></span>](../../messaging-extensions/design/messaging-extension-design.md)
* [<span data-ttu-id="765eb-146">Боты</span><span class="sxs-lookup"><span data-stu-id="765eb-146">Bots</span></span>](../../bots/design/bots.md)
* [<span data-ttu-id="765eb-147">Расширения для собраний</span><span class="sxs-lookup"><span data-stu-id="765eb-147">Meeting extensions</span></span>](../../apps-in-teams-meetings/design/designing-apps-in-meetings.md)

## <a name="ui-templates"></a><span data-ttu-id="765eb-148">Шаблоны пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="765eb-148">UI templates</span></span>

<span data-ttu-id="765eb-149">Быстро создайте сложные и высококачественные проекты с шаблонами для общих Teams и [рабочих процессов.](design-teams-app-ui-templates.md)</span><span class="sxs-lookup"><span data-stu-id="765eb-149">Quickly create complex, high-fidelity designs with [templates for common Teams use cases and workflows](design-teams-app-ui-templates.md).</span></span>

## <a name="basic-ui-components"></a><span data-ttu-id="765eb-150">Основные компоненты пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="765eb-150">Basic UI components</span></span>

<span data-ttu-id="765eb-151">На основе пользовательского интерфейса [](design-teams-app-basic-ui-components.md) Fluent эти основные элементы можно использовать для создания Teams с нуля.</span><span class="sxs-lookup"><span data-stu-id="765eb-151">Based on Fluent UI, these are the [core elements](design-teams-app-basic-ui-components.md) you can use to create Teams experiences from scratch.</span></span>

## <a name="tools-and-samples"></a><span data-ttu-id="765eb-152">Инструменты и примеры</span><span class="sxs-lookup"><span data-stu-id="765eb-152">Tools and samples</span></span>

<span data-ttu-id="765eb-153">Следующие средства помогут дизайнерам и разработчикам начать работу:</span><span class="sxs-lookup"><span data-stu-id="765eb-153">The following tools can help designers and developers get started:</span></span>

### <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="765eb-154">Комплект разработчика для пользовательского интерфейса Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="765eb-154">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="765eb-155">Разработать Teams с компонентами пользовательского интерфейса, шаблонами и примерами, которые можно перетаскивать, падать и изменять по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="765eb-155">Design a Teams app with UI components, templates, and examples that you can drag, drop, and modify as needed.</span></span> <span data-ttu-id="765eb-156">Набор пользовательского интерфейса также содержит всеобъемлющую информацию о том, как приложения должны выглядеть и вести себя в различных Teams сценариях.</span><span class="sxs-lookup"><span data-stu-id="765eb-156">The UI kit also includes comprehensive information about how apps should look and behave in different Teams scenarios.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="765eb-157">Получите набор пользовательского интерфейса (Figma)</span><span class="sxs-lookup"><span data-stu-id="765eb-157">Get the UI kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a><span data-ttu-id="765eb-158">Microsoft Teams Библиотека пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="765eb-158">Microsoft Teams UI Library</span></span>

<span data-ttu-id="765eb-159">Просмотр и тестирование отдельных Teams шаблонов пользовательского интерфейса и связанных компонентов в браузере.</span><span class="sxs-lookup"><span data-stu-id="765eb-159">View and test individual Teams UI templates and related components in your browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="765eb-160">Попробуйте библиотеку пользовательского интерфейса (детская площадка)</span><span class="sxs-lookup"><span data-stu-id="765eb-160">Try the UI library (playground)</span></span>](https://dev-int.teams.microsoft.com/storybook/main/index.html)

<span data-ttu-id="765eb-161">Импорт этих шаблонов и связанных компонентов непосредственно в проект Teams приложения.</span><span class="sxs-lookup"><span data-stu-id="765eb-161">Import these templates and related components directly into your Teams app project.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="765eb-162">Получить библиотеку пользовательского интерфейса (GitHub)</span><span class="sxs-lookup"><span data-stu-id="765eb-162">Get the UI library (GitHub)</span></span>](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a><span data-ttu-id="765eb-163">Пример приложения</span><span class="sxs-lookup"><span data-stu-id="765eb-163">Sample app</span></span>

<span data-ttu-id="765eb-164">Вы можете загрузить пример приложения, чтобы узнать, как приложения должны выглядеть и вести себя в Teams клиенте.</span><span class="sxs-lookup"><span data-stu-id="765eb-164">You can upload a sample app to see how apps should look and behave in the Teams client.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="765eb-165">Получить пример приложения (GitHub)</span><span class="sxs-lookup"><span data-stu-id="765eb-165">Get the sample app (GitHub)</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="other-resources"></a><span data-ttu-id="765eb-166">Другие ресурсы</span><span class="sxs-lookup"><span data-stu-id="765eb-166">Other resources</span></span>

<span data-ttu-id="765eb-167">Чтобы узнать больше, попробуйте один из следующих ресурсов:</span><span class="sxs-lookup"><span data-stu-id="765eb-167">To learn more, try one of the following resources:</span></span>

### <a name="fluent-ui-documentation"></a><span data-ttu-id="765eb-168">Документация по свободному пользовательскому интерфейсу</span><span class="sxs-lookup"><span data-stu-id="765eb-168">Fluent UI documentation</span></span>

<span data-ttu-id="765eb-169">Получите примеры кода и сведения о реализации базовых компонентов пользовательского интерфейса Fluent, используемых для создания Teams интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="765eb-169">Get code samples and implementation details for the basic Fluent UI components used to build Teams experiences.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="765eb-170">Попробуйте Teams компоненты пользовательского интерфейса (Fluent UI)</span><span class="sxs-lookup"><span data-stu-id="765eb-170">Try Teams UI components (Fluent UI)</span></span>](https://fluentsite.z22.web.core.windows.net/)

### <a name="adaptive-cards-designer"></a><span data-ttu-id="765eb-171">Конструктор адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="765eb-171">Adaptive Cards designer</span></span>

<span data-ttu-id="765eb-172">Разработка адаптивных карт в нашем веб-инструменте.</span><span class="sxs-lookup"><span data-stu-id="765eb-172">Design Adaptive Cards in our web-based tool.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="765eb-173">Попробуйте конструктор адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="765eb-173">Try the Adaptive Cards designer</span></span>](https://adaptivecards.io/designer/)
