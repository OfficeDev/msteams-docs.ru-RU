---
title: Проектирование пользовательского приложения
author: heath-hamilton
description: Узнайте, как проектировать приложения Microsoft Teams. Ресурсы включают набор пользовательского интерфейса Microsoft Teams, лучшие методики, примеры и другие.
ms.author: lajanuar
ms.topic: overview
ms.openlocfilehash: 0c791b1e4733cd2a015e443ca5c4d0c433dd4d31
ms.sourcegitcommit: 00c657e3bf57d3b92aca7da941cde47a2eeff4d0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/20/2021
ms.locfileid: "49911907"
---
# <a name="designing-your-microsoft-teams-app"></a><span data-ttu-id="4ad32-104">Проектирование приложения Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="4ad32-104">Designing your Microsoft Teams app</span></span>

:::image type="content" source="../../assets/images/design-guidelines-overview.png" alt-text="Концептуальный образ с рекомендациями по проектированию Microsoft Teams.":::

<span data-ttu-id="4ad32-106">Независимо от того, являетесь ли вы дизайнером, менеджером по продуктам, разработчиком или создателем с помощью средств с низким кодом, эти рекомендации помогут вам быстро принять правильные решения по проектированию для вашего приложения Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="4ad32-106">Whether you're a designer, product manager, developer, or maker using low-code tools, these guidelines can help you quickly make the right design decisions for your Microsoft Teams app.</span></span>

## <a name="teams-app-design-principles"></a><span data-ttu-id="4ad32-107">Принципы проектирования приложений Teams</span><span class="sxs-lookup"><span data-stu-id="4ad32-107">Teams app design principles</span></span>

<span data-ttu-id="4ad32-108">Приложения Teams помогают людям добиться большего вместе.</span><span class="sxs-lookup"><span data-stu-id="4ad32-108">Teams apps help people achieve more together.</span></span> <span data-ttu-id="4ad32-109">Используйте эти принципы для разработки.</span><span class="sxs-lookup"><span data-stu-id="4ad32-109">Use these principles to guide your design.</span></span>

:::row:::
   :::column span="":::

### <a name="collaborative"></a><span data-ttu-id="4ad32-110">Совместная работа</span><span class="sxs-lookup"><span data-stu-id="4ad32-110">Collaborative</span></span>

<span data-ttu-id="4ad32-111">Приложения Teams помогают людям добиться большего вместе.</span><span class="sxs-lookup"><span data-stu-id="4ad32-111">Teams apps help people achieve more together.</span></span> <span data-ttu-id="4ad32-112">Используйте эти принципы для разработки.</span><span class="sxs-lookup"><span data-stu-id="4ad32-112">Use these principles to guide your design.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="trustworthy"></a><span data-ttu-id="4ad32-113">Надежность</span><span class="sxs-lookup"><span data-stu-id="4ad32-113">Trustworthy</span></span>

<span data-ttu-id="4ad32-114">Приложение защищено и соответствует требованиям.</span><span class="sxs-lookup"><span data-stu-id="4ad32-114">The app is secure and compliant.</span></span> <span data-ttu-id="4ad32-115">Пользователи могут легко находить сведения о конфиденциальности.</span><span class="sxs-lookup"><span data-stu-id="4ad32-115">Users can easily find information about privacy.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="globally-inclusive"></a><span data-ttu-id="4ad32-116">Глобальный инклюзивный</span><span class="sxs-lookup"><span data-stu-id="4ad32-116">Globally inclusive</span></span>

<span data-ttu-id="4ad32-117">Приложение могут использовать люди всех фонов, навыков и навыков.</span><span class="sxs-lookup"><span data-stu-id="4ad32-117">People of all backgrounds, skillsets, and disciplines can use the app.</span></span> <span data-ttu-id="4ad32-118">Это культурная, расовая и социальная интеграция.</span><span class="sxs-lookup"><span data-stu-id="4ad32-118">It’s culturally, racially, and socially aware.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="light"></a><span data-ttu-id="4ad32-119">Легкие</span><span class="sxs-lookup"><span data-stu-id="4ad32-119">Light</span></span>

<span data-ttu-id="4ad32-120">Приложение фокусируется на основных сценариях, которые смешиваются с рабочего процесса Teams.</span><span class="sxs-lookup"><span data-stu-id="4ad32-120">The app focuses on core scenarios that blend with Teams workflows.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="native-or-distinct"></a><span data-ttu-id="4ad32-121">Native или distinct</span><span class="sxs-lookup"><span data-stu-id="4ad32-121">Native or distinct</span></span>

<span data-ttu-id="4ad32-122">Приложение использует собственные компоненты проектирования Teams или ваши собственные.</span><span class="sxs-lookup"><span data-stu-id="4ad32-122">The app uses native Teams design components or your own.</span></span> <span data-ttu-id="4ad32-123">Не существует смешения цветовых схем, элементов управления и т. д.</span><span class="sxs-lookup"><span data-stu-id="4ad32-123">There’s no blend of color schemes, controls, etc.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="useful"></a><span data-ttu-id="4ad32-124">Полезно</span><span class="sxs-lookup"><span data-stu-id="4ad32-124">Useful</span></span>

<span data-ttu-id="4ad32-125">Приложение основано на сценарии, который необходимо сделать в Teams.</span><span class="sxs-lookup"><span data-stu-id="4ad32-125">The app is based on a scenario people need to do in Teams.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="easy-to-use"></a><span data-ttu-id="4ad32-126">Простой в использовании</span><span class="sxs-lookup"><span data-stu-id="4ad32-126">Easy to use</span></span>

<span data-ttu-id="4ad32-127">Пользовательский интерфейс прост в понятии, прекрасно выглядит и тон, а также повышает продуктивность работы людей.</span><span class="sxs-lookup"><span data-stu-id="4ad32-127">The UI is easy to understand, pleasant in look and tone, and makes people more productive.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="responsive"></a><span data-ttu-id="4ad32-128">Оперативно</span><span class="sxs-lookup"><span data-stu-id="4ad32-128">Responsive</span></span>

<span data-ttu-id="4ad32-129">Приложение не зависит от устройства и экрана.</span><span class="sxs-lookup"><span data-stu-id="4ad32-129">The app is device and screen agnostic.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="accessible"></a><span data-ttu-id="4ad32-130">Доступные</span><span class="sxs-lookup"><span data-stu-id="4ad32-130">Accessible</span></span>

<span data-ttu-id="4ad32-131">Приложение соответствует требованиям к специальным требованиям Teams с точки зрения цветовой контрастности, альтернативных вариантов навигации и других возможностей.</span><span class="sxs-lookup"><span data-stu-id="4ad32-131">The app meets Teams accessibility requirements in terms of color contrast, navigation alternatives, and more.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="well-described"></a><span data-ttu-id="4ad32-132">Хорошо описано</span><span class="sxs-lookup"><span data-stu-id="4ad32-132">Well described</span></span>

<span data-ttu-id="4ad32-133">Текст, значки и изображения четко понять, для чего нужно приложение и как его использовать.</span><span class="sxs-lookup"><span data-stu-id="4ad32-133">Text, icons, and images make it clear what the app is for and how to use it.</span></span>

   :::column-end:::
:::row-end:::

## <a name="creating-a-cohesive-experience"></a><span data-ttu-id="4ad32-134">Создание единого и согласованного опыта</span><span class="sxs-lookup"><span data-stu-id="4ad32-134">Creating a cohesive experience</span></span>

<span data-ttu-id="4ad32-135">Проектирование приложения Teams похоже на разработку обычного веб-приложения, но также немного отличается.</span><span class="sxs-lookup"><span data-stu-id="4ad32-135">Designing a Teams app is like designing a conventional web app—but also a little different.</span></span> <span data-ttu-id="4ad32-136">Эффективная разработка выделяет уникальные атрибуты вашего приложения, при этом естественным образом вписываясь в функции и контексты Teams.</span><span class="sxs-lookup"><span data-stu-id="4ad32-136">An effective design highlights your app's unique attributes while fitting naturally with Teams features and contexts.</span></span>

<span data-ttu-id="4ad32-137">Эти рекомендации и ресурсы помогут вам найти баланс.</span><span class="sxs-lookup"><span data-stu-id="4ad32-137">These guidelines and resources can help you strike that balance.</span></span> <span data-ttu-id="4ad32-138">Вы узнаете, что делать и чего избегать при разработке приложения Teams (например, многоуровневая навигация на вкладке).</span><span class="sxs-lookup"><span data-stu-id="4ad32-138">You'll know what to do and what to avoid when designing your Teams app (such as multi-level navigation in a tab).</span></span>

## <a name="planning-your-app"></a><span data-ttu-id="4ad32-139">Планирование приложения</span><span class="sxs-lookup"><span data-stu-id="4ad32-139">Planning your app</span></span>

<span data-ttu-id="4ad32-140">Чтобы разработать высококачественное приложение Teams, необходимо сначала понять, что должно делать ваше приложение и как вы думаете, что его будут использовать люди.</span><span class="sxs-lookup"><span data-stu-id="4ad32-140">To design a high-quality Teams app, you must first understand what you want your app to do and how you think people will use it.</span></span> <span data-ttu-id="4ad32-141">Если вы еще не сделали этого, у вас есть некоторое время, чтобы правильно [спланировать приложение.](../../concepts/extensibility-points.md)</span><span class="sxs-lookup"><span data-stu-id="4ad32-141">If you haven't already, take some time to properly [plan your app](../../concepts/extensibility-points.md).</span></span>

## <a name="design-fundamentals"></a><span data-ttu-id="4ad32-142">Основные сведения о дизайне</span><span class="sxs-lookup"><span data-stu-id="4ad32-142">Design fundamentals</span></span>

<span data-ttu-id="4ad32-143">Изучите [основы проектирования приложений Teams,](design-teams-app-fundamentals.md)включая макет, цветовые схемы и т. д.</span><span class="sxs-lookup"><span data-stu-id="4ad32-143">Learn the [fundamentals of Teams app design](design-teams-app-fundamentals.md), including layout, color schemes, and more.</span></span>

## <a name="basic-fluent-ui-components-for-teams"></a><span data-ttu-id="4ad32-144">Основные компоненты пользовательского интерфейса Fluent для Teams</span><span class="sxs-lookup"><span data-stu-id="4ad32-144">Basic Fluent UI components for Teams</span></span>

<span data-ttu-id="4ad32-145">На основе пользовательского интерфейса Fluent это основные элементы для [создания знакомых интерфейсов Teams.](design-teams-app-basic-ui-components.md)</span><span class="sxs-lookup"><span data-stu-id="4ad32-145">Based on Fluent UI, these are the [core elements for creating familiar Teams interfaces](design-teams-app-basic-ui-components.md).</span></span>

## <a name="ui-templates"></a><span data-ttu-id="4ad32-146">Шаблоны пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="4ad32-146">UI templates</span></span>

<span data-ttu-id="4ad32-147">Быстро создавайте сложные высококачественные макеты с шаблонами для распространенных случаев использования Teams и [рабочих процессов.](design-teams-app-ui-templates.md)</span><span class="sxs-lookup"><span data-stu-id="4ad32-147">Quickly create complex, high-fidelity designs with [templates for common Teams use cases and workflows](design-teams-app-ui-templates.md).</span></span>

## <a name="app-capabilities"></a><span data-ttu-id="4ad32-148">Возможности приложений</span><span class="sxs-lookup"><span data-stu-id="4ad32-148">App capabilities</span></span>

<span data-ttu-id="4ad32-149">Понять, как люди добавляют, используют и управляют приложениями Teams, чтобы использовать все возможности в вашем дизайне.</span><span class="sxs-lookup"><span data-stu-id="4ad32-149">Understand how people add, use, and manage Teams apps to make the most of each capability in your design.</span></span>

* [<span data-ttu-id="4ad32-150">Персональные приложения</span><span class="sxs-lookup"><span data-stu-id="4ad32-150">Personal apps</span></span>](../../concepts/design/personal-apps.md)
* [<span data-ttu-id="4ad32-151">Вкладки</span><span class="sxs-lookup"><span data-stu-id="4ad32-151">Tabs</span></span>](../../tabs/design/tabs.md)
* [<span data-ttu-id="4ad32-152">Расширения для системы обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="4ad32-152">Messaging extensions</span></span>](../../messaging-extensions/design/messaging-extension-design.md)
* [<span data-ttu-id="4ad32-153">Боты</span><span class="sxs-lookup"><span data-stu-id="4ad32-153">Bots</span></span>](../../bots/design/bots.md)
* [<span data-ttu-id="4ad32-154">Расширения для собраний</span><span class="sxs-lookup"><span data-stu-id="4ad32-154">Meeting extensions</span></span>](../../apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [<span data-ttu-id="4ad32-155">Модули задач</span><span class="sxs-lookup"><span data-stu-id="4ad32-155">Task modules</span></span>](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)
* [<span data-ttu-id="4ad32-156">Адаптивные карточки</span><span class="sxs-lookup"><span data-stu-id="4ad32-156">Adaptive Cards</span></span>](../../task-modules-and-cards/cards/design-effective-cards.md)

## <a name="tools-and-samples"></a><span data-ttu-id="4ad32-157">Инструменты и примеры</span><span class="sxs-lookup"><span data-stu-id="4ad32-157">Tools and samples</span></span>

<span data-ttu-id="4ad32-158">С помощью следующих средств дизайнеры и разработчики могут начать работу.</span><span class="sxs-lookup"><span data-stu-id="4ad32-158">The following tools can help designers and developers get started.</span></span>

### <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="4ad32-159">Пакет пользовательского интерфейса Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="4ad32-159">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="4ad32-160">Разработка приложения Teams с помощью компонентов пользовательского интерфейса, шаблонов и примеров, которые можно перетаскивать, перетаскивать и изменять при необходимости.</span><span class="sxs-lookup"><span data-stu-id="4ad32-160">Design a Teams app with UI components, templates, and examples that you can drag, drop, and modify as needed.</span></span> <span data-ttu-id="4ad32-161">Комплект пользовательского интерфейса также содержит всесторонние сведения о том, как приложения должны выглядеть и вести себя в различных сценариях Teams.</span><span class="sxs-lookup"><span data-stu-id="4ad32-161">The UI kit also includes comprehensive information about how apps should look and behave in different Teams scenarios.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4ad32-162">Get the UI kit (Figma)</span><span class="sxs-lookup"><span data-stu-id="4ad32-162">Get the UI kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a><span data-ttu-id="4ad32-163">Библиотека пользовательского интерфейса Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="4ad32-163">Microsoft Teams UI Library</span></span>

<span data-ttu-id="4ad32-164">Просмотр и тестирование отдельных шаблонов пользовательского интерфейса Teams и связанных компонентов в браузере.</span><span class="sxs-lookup"><span data-stu-id="4ad32-164">View and test individual Teams UI templates and related components in your browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4ad32-165">Попробуйте библиотеку пользовательского интерфейса (игровая библиотека)</span><span class="sxs-lookup"><span data-stu-id="4ad32-165">Try the UI library (playground)</span></span>](https://dev-int.teams.microsoft.com/storybook/main/index.html)

<span data-ttu-id="4ad32-166">Импортировать эти шаблоны и связанные компоненты непосредственно в проект приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="4ad32-166">Import these templates and related components directly into your Teams app project.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4ad32-167">Получить библиотеку пользовательского интерфейса (GitHub)</span><span class="sxs-lookup"><span data-stu-id="4ad32-167">Get the UI library (GitHub)</span></span>](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a><span data-ttu-id="4ad32-168">Пример приложения</span><span class="sxs-lookup"><span data-stu-id="4ad32-168">Sample app</span></span>

<span data-ttu-id="4ad32-169">Установите пример приложения, чтобы увидеть, как шаблоны пользовательского интерфейса выглядят и работают в контекстах Teams.</span><span class="sxs-lookup"><span data-stu-id="4ad32-169">Install a sample app to see how UI templates look and behave within Teams contexts.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4ad32-170">Получить пример приложения (GitHub)</span><span class="sxs-lookup"><span data-stu-id="4ad32-170">Get the sample app (GitHub)</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="other-resources"></a><span data-ttu-id="4ad32-171">Другие ресурсы</span><span class="sxs-lookup"><span data-stu-id="4ad32-171">Other resources</span></span>

<span data-ttu-id="4ad32-172">Чтобы узнать больше, попробуйте один из следующих ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4ad32-172">To learn more, try one of the following resources.</span></span>

### <a name="fluent-ui-documentation"></a><span data-ttu-id="4ad32-173">Документация по пользовательскому интерфейсу Fluent</span><span class="sxs-lookup"><span data-stu-id="4ad32-173">Fluent UI documentation</span></span>

<span data-ttu-id="4ad32-174">Получите примеры кода и сведения о реализации компонентов на основе пользовательского интерфейса Fluent, используемых для создания интерфейсов Teams.</span><span class="sxs-lookup"><span data-stu-id="4ad32-174">Get code samples and implementation details for the Fluent UI-based components used to build Teams experiences.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4ad32-175">Попробуйте компоненты пользовательского интерфейса Teams (пользовательский интерфейс Fluent)</span><span class="sxs-lookup"><span data-stu-id="4ad32-175">Try Teams UI components (Fluent UI)</span></span>](https://fluentsite.z22.web.core.windows.net/)

### <a name="adaptive-cards-designer"></a><span data-ttu-id="4ad32-176">Конструктор адаптивных карточек</span><span class="sxs-lookup"><span data-stu-id="4ad32-176">Adaptive Cards designer</span></span>

<span data-ttu-id="4ad32-177">Разработка адаптивных карточек в веб-средстве.</span><span class="sxs-lookup"><span data-stu-id="4ad32-177">Design Adaptive Cards in our web-based tool.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4ad32-178">Попробуйте конструктор адаптивных карточек</span><span class="sxs-lookup"><span data-stu-id="4ad32-178">Try the Adaptive Cards designer</span></span>](https://adaptivecards.io/designer/)
