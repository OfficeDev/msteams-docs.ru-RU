---
title: Проектирование пользовательского приложения
author: heath-hamilton
description: Узнайте, как Microsoft Teams приложений. Ресурсы включают в Microsoft Teams набор пользовательского интерфейса, лучшие практики, примеры и многое другое.
localization_priority: Normal
ms.author: lajanuar
ms.topic: overview
ms.openlocfilehash: 2f21872bd8c37026528ff6fde282e8c433d5e052
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565118"
---
# <a name="designing-your-microsoft-teams-app"></a><span data-ttu-id="aa550-104">Проектирование приложения Microsoft Teams для веб-Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="aa550-104">Designing your Microsoft Teams app</span></span>

:::image type="content" source="../../assets/images/design-guidelines-overview.png" alt-text="Концептуальное изображение, вводя Microsoft Teams принципы проектирования.":::

<span data-ttu-id="aa550-106">Независимо от того, являете ли вы дизайнером, менеджером по продуктам, разработчиком или создателем инструментов с низким кодом, эти рекомендации помогут вам быстро принять правильные дизайнерские решения для вашего Microsoft Teams приложения.</span><span class="sxs-lookup"><span data-stu-id="aa550-106">Whether you're a designer, product manager, developer, or maker using low-code tools, these guidelines can help you quickly make the right design decisions for your Microsoft Teams app.</span></span>

## <a name="teams-app-design-principles"></a><span data-ttu-id="aa550-107">Teams принципы проектирования приложений</span><span class="sxs-lookup"><span data-stu-id="aa550-107">Teams app design principles</span></span>

<span data-ttu-id="aa550-108">Teams приложения помогают людям достичь большего вместе.</span><span class="sxs-lookup"><span data-stu-id="aa550-108">Teams apps help people achieve more together.</span></span> <span data-ttu-id="aa550-109">Используйте эти принципы, чтобы направлять ваш дизайн.</span><span class="sxs-lookup"><span data-stu-id="aa550-109">Use these principles to guide your design.</span></span>

:::row:::
   :::column span="":::

### <a name="collaborative"></a><span data-ttu-id="aa550-110">Совместных</span><span class="sxs-lookup"><span data-stu-id="aa550-110">Collaborative</span></span>

<span data-ttu-id="aa550-111">Teams приложения помогают людям достичь большего вместе.</span><span class="sxs-lookup"><span data-stu-id="aa550-111">Teams apps help people achieve more together.</span></span> <span data-ttu-id="aa550-112">Используйте эти принципы, чтобы направлять ваш дизайн.</span><span class="sxs-lookup"><span data-stu-id="aa550-112">Use these principles to guide your design.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="trustworthy"></a><span data-ttu-id="aa550-113">заслуживающий доверия</span><span class="sxs-lookup"><span data-stu-id="aa550-113">Trustworthy</span></span>

<span data-ttu-id="aa550-114">Приложение является безопасным и совместимым.</span><span class="sxs-lookup"><span data-stu-id="aa550-114">The app is secure and compliant.</span></span> <span data-ttu-id="aa550-115">Пользователи могут легко найти информацию о конфиденциальности.</span><span class="sxs-lookup"><span data-stu-id="aa550-115">Users can easily find information about privacy.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="globally-inclusive"></a><span data-ttu-id="aa550-116">Глобально инклюзивный</span><span class="sxs-lookup"><span data-stu-id="aa550-116">Globally inclusive</span></span>

<span data-ttu-id="aa550-117">С приложением могут пользоваться люди всех слоев общества, навыки и дисциплины.</span><span class="sxs-lookup"><span data-stu-id="aa550-117">People of all backgrounds, skillsets, and disciplines can use the app.</span></span> <span data-ttu-id="aa550-118">Это культурно, расово и социально известно.</span><span class="sxs-lookup"><span data-stu-id="aa550-118">It’s culturally, racially, and socially aware.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="light"></a><span data-ttu-id="aa550-119">Легкие</span><span class="sxs-lookup"><span data-stu-id="aa550-119">Light</span></span>

<span data-ttu-id="aa550-120">Приложение фокусируется на основных сценариях, которые сочетаются с Teams процессами.</span><span class="sxs-lookup"><span data-stu-id="aa550-120">The app focuses on core scenarios that blend with Teams workflows.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="native-or-distinct"></a><span data-ttu-id="aa550-121">Родные или различные</span><span class="sxs-lookup"><span data-stu-id="aa550-121">Native or distinct</span></span>

<span data-ttu-id="aa550-122">Приложение использует родные Teams компоненты дизайна или свои собственные.</span><span class="sxs-lookup"><span data-stu-id="aa550-122">The app uses native Teams design components or your own.</span></span> <span data-ttu-id="aa550-123">Там нет смеси цветовых схем, элементов управления, и так далее.</span><span class="sxs-lookup"><span data-stu-id="aa550-123">There’s no blend of color schemes, controls, and so on.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="useful"></a><span data-ttu-id="aa550-124">полезный</span><span class="sxs-lookup"><span data-stu-id="aa550-124">Useful</span></span>

<span data-ttu-id="aa550-125">Приложение основано на сценарии, который люди должны делать в Teams.</span><span class="sxs-lookup"><span data-stu-id="aa550-125">The app is based on a scenario people need to do in Teams.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="easy-to-use"></a><span data-ttu-id="aa550-126">Простой в использовании</span><span class="sxs-lookup"><span data-stu-id="aa550-126">Easy to use</span></span>

<span data-ttu-id="aa550-127">Пользовательский интерфейс прост в пониманиях, приятен по своему вкусу и тону и делает людей более продуктивными.</span><span class="sxs-lookup"><span data-stu-id="aa550-127">The UI is easy to understand, pleasant in look and tone, and makes people more productive.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="responsive"></a><span data-ttu-id="aa550-128">Оперативно</span><span class="sxs-lookup"><span data-stu-id="aa550-128">Responsive</span></span>

<span data-ttu-id="aa550-129">Приложение является устройством и экраном агностик.</span><span class="sxs-lookup"><span data-stu-id="aa550-129">The app is device and screen agnostic.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="accessible"></a><span data-ttu-id="aa550-130">Доступные</span><span class="sxs-lookup"><span data-stu-id="aa550-130">Accessible</span></span>

<span data-ttu-id="aa550-131">Приложение отвечает требованиям Teams с точки зрения контрастности цвета, навигации альтернативы, и многое другое.</span><span class="sxs-lookup"><span data-stu-id="aa550-131">The app meets Teams accessibility requirements in terms of color contrast, navigation alternatives, and more.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="well-described"></a><span data-ttu-id="aa550-132">Хорошо описано</span><span class="sxs-lookup"><span data-stu-id="aa550-132">Well described</span></span>

<span data-ttu-id="aa550-133">Текст, значки и изображения ясно показывают, для чего предназначено приложение и как его использовать.</span><span class="sxs-lookup"><span data-stu-id="aa550-133">Text, icons, and images make it clear what the app is for and how to use it.</span></span>

   :::column-end:::
:::row-end:::

## <a name="creating-a-cohesive-experience"></a><span data-ttu-id="aa550-134">Создание сплоченного опыта</span><span class="sxs-lookup"><span data-stu-id="aa550-134">Creating a cohesive experience</span></span>

<span data-ttu-id="aa550-135">Проектирование Teams приложения, как проектирование обычного веб-приложения, но и немного отличается.</span><span class="sxs-lookup"><span data-stu-id="aa550-135">Designing a Teams app is like designing a conventional web app—but also a little different.</span></span> <span data-ttu-id="aa550-136">Эффективный дизайн подчеркивает уникальные атрибуты вашего приложения, при этом естественным образом вписываясь в Teams функции и контексты.</span><span class="sxs-lookup"><span data-stu-id="aa550-136">An effective design highlights your app's unique attributes while fitting naturally with Teams features and contexts.</span></span>

<span data-ttu-id="aa550-137">Эти руководящие принципы и ресурсы могут помочь вам найти этот баланс.</span><span class="sxs-lookup"><span data-stu-id="aa550-137">These guidelines and resources can help you strike that balance.</span></span> <span data-ttu-id="aa550-138">Вы будете знать, что делать и чего следует избегать при проектировании Teams приложения (например, многоуровневая навигация во вкладке).</span><span class="sxs-lookup"><span data-stu-id="aa550-138">You'll know what to do and what to avoid when designing your Teams app (such as multi-level navigation in a tab).</span></span>

## <a name="planning-your-app"></a><span data-ttu-id="aa550-139">Планирование приложения</span><span class="sxs-lookup"><span data-stu-id="aa550-139">Planning your app</span></span>

<span data-ttu-id="aa550-140">Чтобы разработать высококачественное приложение для Teams, вы должны сначала понять, что вы хотите, чтобы ваше приложение делать и как вы думаете, люди будут использовать его.</span><span class="sxs-lookup"><span data-stu-id="aa550-140">To design a high-quality Teams app, you must first understand what you want your app to do and how you think people will use it.</span></span> <span data-ttu-id="aa550-141">Если вы еще не сделали этого, на некоторое время нужно правильно [спланировать приложение.](../../concepts/extensibility-points.md)</span><span class="sxs-lookup"><span data-stu-id="aa550-141">If you haven't already, take some time to properly [plan your app](../../concepts/extensibility-points.md).</span></span>

## <a name="design-fundamentals"></a><span data-ttu-id="aa550-142">Основные сведения о дизайне</span><span class="sxs-lookup"><span data-stu-id="aa550-142">Design fundamentals</span></span>

<span data-ttu-id="aa550-143">Узнайте основы [дизайна Teams, включая макет,](design-teams-app-fundamentals.md)цветовые схемы и многое другое.</span><span class="sxs-lookup"><span data-stu-id="aa550-143">Learn the [fundamentals of Teams app design](design-teams-app-fundamentals.md), including layout, color schemes, and more.</span></span>

## <a name="basic-fluent-ui-components-for-teams"></a><span data-ttu-id="aa550-144">Основные компоненты пользовательского интерфейса Fluent для Teams</span><span class="sxs-lookup"><span data-stu-id="aa550-144">Basic Fluent UI components for Teams</span></span>

<span data-ttu-id="aa550-145">На основе Fluent пользовательского интерфейса, это [основные элементы для создания знакомых Teams интерфейсов](design-teams-app-basic-ui-components.md).</span><span class="sxs-lookup"><span data-stu-id="aa550-145">Based on Fluent UI, these are the [core elements for creating familiar Teams interfaces](design-teams-app-basic-ui-components.md).</span></span>

## <a name="ui-templates"></a><span data-ttu-id="aa550-146">Шаблоны пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="aa550-146">UI templates</span></span>

<span data-ttu-id="aa550-147">Быстро создавайте сложные, высококачественные проекты с [шаблонами для обычных Teams и рабочих процессов.](design-teams-app-ui-templates.md)</span><span class="sxs-lookup"><span data-stu-id="aa550-147">Quickly create complex, high-fidelity designs with [templates for common Teams use cases and workflows](design-teams-app-ui-templates.md).</span></span>

## <a name="app-capabilities"></a><span data-ttu-id="aa550-148">Возможности приложений</span><span class="sxs-lookup"><span data-stu-id="aa550-148">App capabilities</span></span>

<span data-ttu-id="aa550-149">Поймите, как люди добавляют, используют и управляют Teams приложениями, чтобы использовать каждую возможность в вашем дизайне.</span><span class="sxs-lookup"><span data-stu-id="aa550-149">Understand how people add, use, and manage Teams apps to make the most of each capability in your design.</span></span>

* [<span data-ttu-id="aa550-150">Персональные приложения</span><span class="sxs-lookup"><span data-stu-id="aa550-150">Personal apps</span></span>](../../concepts/design/personal-apps.md)
* [<span data-ttu-id="aa550-151">Вкладки</span><span class="sxs-lookup"><span data-stu-id="aa550-151">Tabs</span></span>](../../tabs/design/tabs.md)
* [<span data-ttu-id="aa550-152">Расширения для системы обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="aa550-152">Messaging extensions</span></span>](../../messaging-extensions/design/messaging-extension-design.md)
* [<span data-ttu-id="aa550-153">Боты</span><span class="sxs-lookup"><span data-stu-id="aa550-153">Bots</span></span>](../../bots/design/bots.md)
* [<span data-ttu-id="aa550-154">Расширения для собраний</span><span class="sxs-lookup"><span data-stu-id="aa550-154">Meeting extensions</span></span>](../../apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [<span data-ttu-id="aa550-155">Модули задач</span><span class="sxs-lookup"><span data-stu-id="aa550-155">Task modules</span></span>](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)
* [<span data-ttu-id="aa550-156">Адаптивные карточки</span><span class="sxs-lookup"><span data-stu-id="aa550-156">Adaptive Cards</span></span>](../../task-modules-and-cards/cards/design-effective-cards.md)

## <a name="app-customization"></a><span data-ttu-id="aa550-157">Настройка приложений</span><span class="sxs-lookup"><span data-stu-id="aa550-157">App customization</span></span>

<span data-ttu-id="aa550-158">Поймите, Teams администратор может настроить или ребрендинг приложения на основе необходимости организации.</span><span class="sxs-lookup"><span data-stu-id="aa550-158">Understand how the Teams admin can customize or rebrand the app based on the organization's need.</span></span> <span data-ttu-id="aa550-159">Эта настройка включена, если вы `configurableProperties` определяете схему манифеста.</span><span class="sxs-lookup"><span data-stu-id="aa550-159">This customization is enabled if you define the `configurableProperties` in the manifest schema.</span></span> <span data-ttu-id="aa550-160">Для получения дополнительной информации [см Microsoft Teams.](/MicrosoftTeams/customize-apps)</span><span class="sxs-lookup"><span data-stu-id="aa550-160">For more information, see [Customize apps in Microsoft Teams](/MicrosoftTeams/customize-apps).</span></span>

> [!NOTE]
> <span data-ttu-id="aa550-161">Настройка приложений позволяет администраторам изменять внешний вид приложений, загруженных через ботов, расширения обмена сообщениями, вкладки и разъемы.</span><span class="sxs-lookup"><span data-stu-id="aa550-161">App customization enables admins to change the look-and-feel of the apps loaded through bots, messaging extensions, tabs, and connectors.</span></span> <span data-ttu-id="aa550-162">Например, если администратор Teams настраивает имя приложения *от Contoso* до *Contoso Agent,* то приложение будет отображаться с новым *именем Contoso Agent* для пользователей.</span><span class="sxs-lookup"><span data-stu-id="aa550-162">For example, if the Teams admin customizes the name of an app from *Contoso* to *Contoso Agent*, then the app will appear with the new name *Contoso Agent* to users.</span></span> <span data-ttu-id="aa550-163">Однако, добавляя разъем в чат, в списке разъемы будут по-прежнему показывать название приложения как *Contoso*.</span><span class="sxs-lookup"><span data-stu-id="aa550-163">However, while adding a connector to a chat, in the list the connectors will still show the name of the app as *Contoso*.</span></span>
> 
> <span data-ttu-id="aa550-164">В качестве наилучшей практики необходимо предоставить рекомендации по настройке для пользователей и клиентов приложений, чтобы следовать при настройке приложения.</span><span class="sxs-lookup"><span data-stu-id="aa550-164">As a best practice, you must provide customization guidelines for app users and customers to follow when customizing your app.</span></span> <span data-ttu-id="aa550-165">Для получения дополнительной [информации, смотрите настроить приложения в Microsoft Teams](/MicrosoftTeams/customize-apps).</span><span class="sxs-lookup"><span data-stu-id="aa550-165">For more information, see [customize apps in Microsoft Teams](/MicrosoftTeams/customize-apps).</span></span>

## <a name="tools-and-samples"></a><span data-ttu-id="aa550-166">Инструменты и примеры</span><span class="sxs-lookup"><span data-stu-id="aa550-166">Tools and samples</span></span>

<span data-ttu-id="aa550-167">Следующие инструменты могут помочь дизайнерам и разработчикам начать работу:</span><span class="sxs-lookup"><span data-stu-id="aa550-167">The following tools can help designers and developers get started:</span></span>

### <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="aa550-168">Комплект разработчика для пользовательского интерфейса Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="aa550-168">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="aa550-169">Создать приложение Teams с компонентами пользовательского интерфейса, шаблонами и примерами, которые можно перетащить, сбросить и изменить по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="aa550-169">Design a Teams app with UI components, templates, and examples that you can drag, drop, and modify as needed.</span></span> <span data-ttu-id="aa550-170">Комплект пользовательского интерфейса также содержит полную информацию о том, как приложения должны выглядеть и вести себя в Teams сценариях.</span><span class="sxs-lookup"><span data-stu-id="aa550-170">The UI kit also includes comprehensive information about how apps should look and behave in different Teams scenarios.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="aa550-171">Получить комплект пользовательского интерфейса (Фигма)</span><span class="sxs-lookup"><span data-stu-id="aa550-171">Get the UI kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a><span data-ttu-id="aa550-172">Microsoft Teams Библиотека пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="aa550-172">Microsoft Teams UI Library</span></span>

<span data-ttu-id="aa550-173">Просмотр и тестирование отдельных Teams пользовательского интерфейса и связанных с ними компонентов в браузере.</span><span class="sxs-lookup"><span data-stu-id="aa550-173">View and test individual Teams UI templates and related components in your browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="aa550-174">Попробуйте библиотеку пользовательского интерфейса (площадка)</span><span class="sxs-lookup"><span data-stu-id="aa550-174">Try the UI library (playground)</span></span>](https://dev-int.teams.microsoft.com/storybook/main/index.html)

<span data-ttu-id="aa550-175">Импорт этих шаблонов и связанных с ними компонентов непосредственно в ваш Teams проекта приложения.</span><span class="sxs-lookup"><span data-stu-id="aa550-175">Import these templates and related components directly into your Teams app project.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="aa550-176">Получить библиотеку пользовательского интерфейса (GitHub)</span><span class="sxs-lookup"><span data-stu-id="aa550-176">Get the UI library (GitHub)</span></span>](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a><span data-ttu-id="aa550-177">Пример приложения</span><span class="sxs-lookup"><span data-stu-id="aa550-177">Sample app</span></span>

<span data-ttu-id="aa550-178">Установите пример приложения, чтобы увидеть, как выглядят и ведут себя шаблоны пользовательского интерфейса Teams контексте.</span><span class="sxs-lookup"><span data-stu-id="aa550-178">Install a sample app to see how UI templates look and behave within Teams contexts.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="aa550-179">Получить образец приложения (GitHub)</span><span class="sxs-lookup"><span data-stu-id="aa550-179">Get the sample app (GitHub)</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="other-resources"></a><span data-ttu-id="aa550-180">Другие ресурсы</span><span class="sxs-lookup"><span data-stu-id="aa550-180">Other resources</span></span>

<span data-ttu-id="aa550-181">Чтобы узнать больше, попробуйте один из следующих ресурсов:</span><span class="sxs-lookup"><span data-stu-id="aa550-181">To learn more, try one of the following resources:</span></span>

### <a name="fluent-ui-documentation"></a><span data-ttu-id="aa550-182">Документация свободного пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="aa550-182">Fluent UI documentation</span></span>

<span data-ttu-id="aa550-183">Получите образцы кода и детали реализации компонентов на основе пользовательского интерфейса Fluent, используемых для создания Teams интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="aa550-183">Get code samples and implementation details for the Fluent UI-based components used to build Teams experiences.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="aa550-184">Попробуйте Teams пользовательского интерфейса (Fluent UI)</span><span class="sxs-lookup"><span data-stu-id="aa550-184">Try Teams UI components (Fluent UI)</span></span>](https://fluentsite.z22.web.core.windows.net/)

### <a name="adaptive-cards-designer"></a><span data-ttu-id="aa550-185">Дизайнер адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="aa550-185">Adaptive Cards designer</span></span>

<span data-ttu-id="aa550-186">Дизайн адаптивных карт в нашем веб-инструменте.</span><span class="sxs-lookup"><span data-stu-id="aa550-186">Design Adaptive Cards in our web-based tool.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="aa550-187">Попробуйте дизайнер адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="aa550-187">Try the Adaptive Cards designer</span></span>](https://adaptivecards.io/designer/)
