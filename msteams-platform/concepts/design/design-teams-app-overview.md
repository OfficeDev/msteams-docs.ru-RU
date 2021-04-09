---
title: Разработка настраиваемой приложения
author: heath-hamilton
description: Узнайте, как создать приложения Microsoft Teams. Ресурсы включают набор пользовательского интерфейса Microsoft Teams, лучшие практики, примеры и другие.
ms.author: lajanuar
ms.topic: overview
ms.openlocfilehash: 7a6786cdf9091b04f89ebd6c8bb03799eb7d127a
ms.sourcegitcommit: b50f6d68482cad43a60642a9947d1be17809a7df
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/08/2021
ms.locfileid: "51634497"
---
# <a name="designing-your-microsoft-teams-app"></a><span data-ttu-id="94dea-104">Разработка приложения Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="94dea-104">Designing your Microsoft Teams app</span></span>

:::image type="content" source="../../assets/images/design-guidelines-overview.png" alt-text="Концептуальное изображение с рекомендациями по разработке Microsoft Teams.":::

<span data-ttu-id="94dea-106">Независимо от того, являетесь ли вы дизайнером, менеджером продукта, разработчиком или создателем с использованием инструментов с низким кодом, эти рекомендации помогут вам быстро принять правильные решения по проектированию для приложения Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="94dea-106">Whether you're a designer, product manager, developer, or maker using low-code tools, these guidelines can help you quickly make the right design decisions for your Microsoft Teams app.</span></span>

## <a name="teams-app-design-principles"></a><span data-ttu-id="94dea-107">Принципы проектирования приложений Teams</span><span class="sxs-lookup"><span data-stu-id="94dea-107">Teams app design principles</span></span>

<span data-ttu-id="94dea-108">Приложения teams помогают людям добиться большего вместе.</span><span class="sxs-lookup"><span data-stu-id="94dea-108">Teams apps help people achieve more together.</span></span> <span data-ttu-id="94dea-109">Используйте эти принципы для руководства разработкой.</span><span class="sxs-lookup"><span data-stu-id="94dea-109">Use these principles to guide your design.</span></span>

:::row:::
   :::column span="":::

### <a name="collaborative"></a><span data-ttu-id="94dea-110">Совместная работа</span><span class="sxs-lookup"><span data-stu-id="94dea-110">Collaborative</span></span>

<span data-ttu-id="94dea-111">Приложения teams помогают людям добиться большего вместе.</span><span class="sxs-lookup"><span data-stu-id="94dea-111">Teams apps help people achieve more together.</span></span> <span data-ttu-id="94dea-112">Используйте эти принципы для руководства разработкой.</span><span class="sxs-lookup"><span data-stu-id="94dea-112">Use these principles to guide your design.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="trustworthy"></a><span data-ttu-id="94dea-113">Надежность</span><span class="sxs-lookup"><span data-stu-id="94dea-113">Trustworthy</span></span>

<span data-ttu-id="94dea-114">Приложение является безопасным и совместимым.</span><span class="sxs-lookup"><span data-stu-id="94dea-114">The app is secure and compliant.</span></span> <span data-ttu-id="94dea-115">Пользователи могут легко найти сведения о конфиденциальности.</span><span class="sxs-lookup"><span data-stu-id="94dea-115">Users can easily find information about privacy.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="globally-inclusive"></a><span data-ttu-id="94dea-116">Глобальный инклюзивный</span><span class="sxs-lookup"><span data-stu-id="94dea-116">Globally inclusive</span></span>

<span data-ttu-id="94dea-117">В приложении могут использоваться люди всех слоев, навыков и дисциплин.</span><span class="sxs-lookup"><span data-stu-id="94dea-117">People of all backgrounds, skillsets, and disciplines can use the app.</span></span> <span data-ttu-id="94dea-118">Это культурно, расово и социально известно.</span><span class="sxs-lookup"><span data-stu-id="94dea-118">It’s culturally, racially, and socially aware.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="light"></a><span data-ttu-id="94dea-119">Легкие</span><span class="sxs-lookup"><span data-stu-id="94dea-119">Light</span></span>

<span data-ttu-id="94dea-120">Основное внимание приложение уделяет основным сценариям, которые сочетаются с рабочего процессами Teams.</span><span class="sxs-lookup"><span data-stu-id="94dea-120">The app focuses on core scenarios that blend with Teams workflows.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="native-or-distinct"></a><span data-ttu-id="94dea-121">Native или distinct</span><span class="sxs-lookup"><span data-stu-id="94dea-121">Native or distinct</span></span>

<span data-ttu-id="94dea-122">Приложение использует собственные компоненты проектирования Teams или собственные.</span><span class="sxs-lookup"><span data-stu-id="94dea-122">The app uses native Teams design components or your own.</span></span> <span data-ttu-id="94dea-123">Нет смеси цветов, элементов управления и т.д.</span><span class="sxs-lookup"><span data-stu-id="94dea-123">There’s no blend of color schemes, controls, etc.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="useful"></a><span data-ttu-id="94dea-124">Полезные</span><span class="sxs-lookup"><span data-stu-id="94dea-124">Useful</span></span>

<span data-ttu-id="94dea-125">Приложение основано на сценарии, который необходимо сделать людям в Teams.</span><span class="sxs-lookup"><span data-stu-id="94dea-125">The app is based on a scenario people need to do in Teams.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="easy-to-use"></a><span data-ttu-id="94dea-126">Простой в использовании</span><span class="sxs-lookup"><span data-stu-id="94dea-126">Easy to use</span></span>

<span data-ttu-id="94dea-127">Пользовательский интерфейс прост в понятном, приятном в взгляде и тоне и делает людей более продуктивными.</span><span class="sxs-lookup"><span data-stu-id="94dea-127">The UI is easy to understand, pleasant in look and tone, and makes people more productive.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="responsive"></a><span data-ttu-id="94dea-128">Оперативно</span><span class="sxs-lookup"><span data-stu-id="94dea-128">Responsive</span></span>

<span data-ttu-id="94dea-129">Приложение является агностиком устройства и экрана.</span><span class="sxs-lookup"><span data-stu-id="94dea-129">The app is device and screen agnostic.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="accessible"></a><span data-ttu-id="94dea-130">Доступные</span><span class="sxs-lookup"><span data-stu-id="94dea-130">Accessible</span></span>

<span data-ttu-id="94dea-131">Приложение отвечает требованиям к доступности Teams с точки зрения контрастности цвета, альтернатив навигации и других.</span><span class="sxs-lookup"><span data-stu-id="94dea-131">The app meets Teams accessibility requirements in terms of color contrast, navigation alternatives, and more.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="well-described"></a><span data-ttu-id="94dea-132">Хорошо описано</span><span class="sxs-lookup"><span data-stu-id="94dea-132">Well described</span></span>

<span data-ttu-id="94dea-133">Текст, значки и изображения четко поймют, для чего приложение и как его использовать.</span><span class="sxs-lookup"><span data-stu-id="94dea-133">Text, icons, and images make it clear what the app is for and how to use it.</span></span>

   :::column-end:::
:::row-end:::

## <a name="creating-a-cohesive-experience"></a><span data-ttu-id="94dea-134">Создание сплоченного опыта</span><span class="sxs-lookup"><span data-stu-id="94dea-134">Creating a cohesive experience</span></span>

<span data-ttu-id="94dea-135">Разработка приложения Teams — это как проектирование обычного веб-приложения, но и немного другое.</span><span class="sxs-lookup"><span data-stu-id="94dea-135">Designing a Teams app is like designing a conventional web app—but also a little different.</span></span> <span data-ttu-id="94dea-136">Эффективный дизайн подчеркивает уникальные атрибуты вашего приложения, при этом он естественно вписывается в функции и контексты Teams.</span><span class="sxs-lookup"><span data-stu-id="94dea-136">An effective design highlights your app's unique attributes while fitting naturally with Teams features and contexts.</span></span>

<span data-ttu-id="94dea-137">Эти рекомендации и ресурсы помогут вам найти баланс.</span><span class="sxs-lookup"><span data-stu-id="94dea-137">These guidelines and resources can help you strike that balance.</span></span> <span data-ttu-id="94dea-138">Вы узнаете, что делать и чего следует избегать при разработке приложения Teams (например, многоуровневой навигации на вкладке).</span><span class="sxs-lookup"><span data-stu-id="94dea-138">You'll know what to do and what to avoid when designing your Teams app (such as multi-level navigation in a tab).</span></span>

## <a name="planning-your-app"></a><span data-ttu-id="94dea-139">Планирование приложения</span><span class="sxs-lookup"><span data-stu-id="94dea-139">Planning your app</span></span>

<span data-ttu-id="94dea-140">Чтобы создать высококачественное приложение Teams, сначала необходимо понять, что нужно сделать вашему приложению и как его будут использовать люди.</span><span class="sxs-lookup"><span data-stu-id="94dea-140">To design a high-quality Teams app, you must first understand what you want your app to do and how you think people will use it.</span></span> <span data-ttu-id="94dea-141">Если вы еще не сделали этого, у вас есть некоторое время, чтобы правильно [спланировать свое приложение](../../concepts/extensibility-points.md).</span><span class="sxs-lookup"><span data-stu-id="94dea-141">If you haven't already, take some time to properly [plan your app](../../concepts/extensibility-points.md).</span></span>

## <a name="design-fundamentals"></a><span data-ttu-id="94dea-142">Основные сведения о дизайне</span><span class="sxs-lookup"><span data-stu-id="94dea-142">Design fundamentals</span></span>

<span data-ttu-id="94dea-143">Узнайте основы [разработки приложений Teams,](design-teams-app-fundamentals.md)включая макет, цветовую схему и другие.</span><span class="sxs-lookup"><span data-stu-id="94dea-143">Learn the [fundamentals of Teams app design](design-teams-app-fundamentals.md), including layout, color schemes, and more.</span></span>

## <a name="basic-fluent-ui-components-for-teams"></a><span data-ttu-id="94dea-144">Базовые компоненты пользовательского интерфейса Fluent для Teams</span><span class="sxs-lookup"><span data-stu-id="94dea-144">Basic Fluent UI components for Teams</span></span>

<span data-ttu-id="94dea-145">На основе пользовательского интерфейса Fluent это основные элементы для [создания знакомых интерфейсов Teams.](design-teams-app-basic-ui-components.md)</span><span class="sxs-lookup"><span data-stu-id="94dea-145">Based on Fluent UI, these are the [core elements for creating familiar Teams interfaces](design-teams-app-basic-ui-components.md).</span></span>

## <a name="ui-templates"></a><span data-ttu-id="94dea-146">Шаблоны пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="94dea-146">UI templates</span></span>

<span data-ttu-id="94dea-147">Быстро создайте сложные и высококачественные проекты с шаблонами для общих команд, которые используют кейсы и [рабочие процессы.](design-teams-app-ui-templates.md)</span><span class="sxs-lookup"><span data-stu-id="94dea-147">Quickly create complex, high-fidelity designs with [templates for common Teams use cases and workflows](design-teams-app-ui-templates.md).</span></span>

## <a name="app-capabilities"></a><span data-ttu-id="94dea-148">Возможности приложений</span><span class="sxs-lookup"><span data-stu-id="94dea-148">App capabilities</span></span>

<span data-ttu-id="94dea-149">Понимание того, как люди добавляют, используют и управляют приложениями Teams, чтобы использовать все возможности в вашем дизайне.</span><span class="sxs-lookup"><span data-stu-id="94dea-149">Understand how people add, use, and manage Teams apps to make the most of each capability in your design.</span></span>

* [<span data-ttu-id="94dea-150">Персональные приложения</span><span class="sxs-lookup"><span data-stu-id="94dea-150">Personal apps</span></span>](../../concepts/design/personal-apps.md)
* [<span data-ttu-id="94dea-151">Tabs</span><span class="sxs-lookup"><span data-stu-id="94dea-151">Tabs</span></span>](../../tabs/design/tabs.md)
* [<span data-ttu-id="94dea-152">Расширения для системы обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="94dea-152">Messaging extensions</span></span>](../../messaging-extensions/design/messaging-extension-design.md)
* [<span data-ttu-id="94dea-153">Боты</span><span class="sxs-lookup"><span data-stu-id="94dea-153">Bots</span></span>](../../bots/design/bots.md)
* [<span data-ttu-id="94dea-154">Расширения для собраний</span><span class="sxs-lookup"><span data-stu-id="94dea-154">Meeting extensions</span></span>](../../apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [<span data-ttu-id="94dea-155">Модули задач</span><span class="sxs-lookup"><span data-stu-id="94dea-155">Task modules</span></span>](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)
* [<span data-ttu-id="94dea-156">Адаптивные карточки</span><span class="sxs-lookup"><span data-stu-id="94dea-156">Adaptive Cards</span></span>](../../task-modules-and-cards/cards/design-effective-cards.md)

## <a name="app-customization"></a><span data-ttu-id="94dea-157">Настройка приложения</span><span class="sxs-lookup"><span data-stu-id="94dea-157">App customization</span></span>

<span data-ttu-id="94dea-158">Понимание того, как администратор Teams может настраивать или ребрендировать приложение в зависимости от необходимости организации.</span><span class="sxs-lookup"><span data-stu-id="94dea-158">Understand how the Teams admin can customize or rebrand the app based on the organization's need.</span></span> <span data-ttu-id="94dea-159">Эта настройка включена, если вы определяете `configurableProperties` схему манифеста.</span><span class="sxs-lookup"><span data-stu-id="94dea-159">This customization is enabled if you define the `configurableProperties` in the manifest schema.</span></span> <span data-ttu-id="94dea-160">Дополнительные сведения см. [в перенастройке приложений в Microsoft Teams.](/MicrosoftTeams/customize-apps)</span><span class="sxs-lookup"><span data-stu-id="94dea-160">For more information, see [Customize apps in Microsoft Teams](/MicrosoftTeams/customize-apps).</span></span>

> [!NOTE]
> <span data-ttu-id="94dea-161">В настоящее время эта функция доступна только в предварительном просмотре разработчика.</span><span class="sxs-lookup"><span data-stu-id="94dea-161">This feature is currently available in developer preview only.</span></span>
> 
> <span data-ttu-id="94dea-162">Настройка приложения позволяет администраторам изменять внешний вид приложений, загружаемых через боты, расширения обмена сообщениями, вкладки и соединители.</span><span class="sxs-lookup"><span data-stu-id="94dea-162">App customization enables admins to change the look-and-feel of the apps loaded through bots, messaging extensions, tabs, and connectors.</span></span> <span data-ttu-id="94dea-163">Например, если администратор Teams настраивает имя приложения от *Contoso* до Агента *Contoso,* приложение появится с новым именем *Агент Contoso* для пользователей.</span><span class="sxs-lookup"><span data-stu-id="94dea-163">For example, if the Teams admin customizes the name of an app from *Contoso* to *Contoso Agent*, then the app will appear with the new name *Contoso Agent* to users.</span></span> <span data-ttu-id="94dea-164">Однако при добавлении соединитетеля в чат в списке соединители по-прежнему будут показывать имя приложения *как Contoso*.</span><span class="sxs-lookup"><span data-stu-id="94dea-164">However, while adding a connector to a chat, in the list the connectors will still show the name of the app as *Contoso*.</span></span>
> 
> <span data-ttu-id="94dea-165">В качестве наилучшей практики необходимо предоставить рекомендации по настройке для пользователей и клиентов приложений, которые следует соблюдать при настройке приложения.</span><span class="sxs-lookup"><span data-stu-id="94dea-165">As a best practice, you must provide customization guidelines for app users and customers to follow when customizing your app.</span></span> <span data-ttu-id="94dea-166">Дополнительные сведения см. [в дополнительных сведениях о настройке приложений в Microsoft Teams.](/MicrosoftTeams/customize-apps)</span><span class="sxs-lookup"><span data-stu-id="94dea-166">For more information, see [customize apps in Microsoft Teams](/MicrosoftTeams/customize-apps).</span></span>

## <a name="tools-and-samples"></a><span data-ttu-id="94dea-167">Инструменты и примеры</span><span class="sxs-lookup"><span data-stu-id="94dea-167">Tools and samples</span></span>

<span data-ttu-id="94dea-168">Следующие средства помогут дизайнерам и разработчикам начать работу:</span><span class="sxs-lookup"><span data-stu-id="94dea-168">The following tools can help designers and developers get started:</span></span>

### <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="94dea-169">Комплект разработчика для пользовательского интерфейса Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="94dea-169">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="94dea-170">Разработать приложение Teams с компонентами пользовательского интерфейса, шаблонами и примерами, которые можно перетаскивать, падать и изменять по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="94dea-170">Design a Teams app with UI components, templates, and examples that you can drag, drop, and modify as needed.</span></span> <span data-ttu-id="94dea-171">Набор пользовательского интерфейса также содержит всеобъемлющую информацию о том, как приложения должны выглядеть и вести себя в различных сценариях Teams.</span><span class="sxs-lookup"><span data-stu-id="94dea-171">The UI kit also includes comprehensive information about how apps should look and behave in different Teams scenarios.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="94dea-172">Получите набор пользовательского интерфейса (Figma)</span><span class="sxs-lookup"><span data-stu-id="94dea-172">Get the UI kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a><span data-ttu-id="94dea-173">Библиотека пользовательского интерфейса Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="94dea-173">Microsoft Teams UI Library</span></span>

<span data-ttu-id="94dea-174">Просмотр и тестирование отдельных шаблонов пользовательского интерфейса Teams и связанных компонентов в браузере.</span><span class="sxs-lookup"><span data-stu-id="94dea-174">View and test individual Teams UI templates and related components in your browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="94dea-175">Попробуйте библиотеку пользовательского интерфейса (детская площадка)</span><span class="sxs-lookup"><span data-stu-id="94dea-175">Try the UI library (playground)</span></span>](https://dev-int.teams.microsoft.com/storybook/main/index.html)

<span data-ttu-id="94dea-176">Импорт этих шаблонов и связанных компонентов непосредственно в проект приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="94dea-176">Import these templates and related components directly into your Teams app project.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="94dea-177">Получить библиотеку пользовательского интерфейса (GitHub)</span><span class="sxs-lookup"><span data-stu-id="94dea-177">Get the UI library (GitHub)</span></span>](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a><span data-ttu-id="94dea-178">Пример приложения</span><span class="sxs-lookup"><span data-stu-id="94dea-178">Sample app</span></span>

<span data-ttu-id="94dea-179">Установите пример приложения, чтобы узнать, как выглядят и ведут себя шаблоны пользовательского интерфейса в контекстах Teams.</span><span class="sxs-lookup"><span data-stu-id="94dea-179">Install a sample app to see how UI templates look and behave within Teams contexts.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="94dea-180">Получить пример приложения (GitHub)</span><span class="sxs-lookup"><span data-stu-id="94dea-180">Get the sample app (GitHub)</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="other-resources"></a><span data-ttu-id="94dea-181">Другие ресурсы</span><span class="sxs-lookup"><span data-stu-id="94dea-181">Other resources</span></span>

<span data-ttu-id="94dea-182">Чтобы узнать больше, попробуйте один из следующих ресурсов.</span><span class="sxs-lookup"><span data-stu-id="94dea-182">To learn more, try one of the following resources.</span></span>

### <a name="fluent-ui-documentation"></a><span data-ttu-id="94dea-183">Документация по свободному пользовательскому интерфейсу</span><span class="sxs-lookup"><span data-stu-id="94dea-183">Fluent UI documentation</span></span>

<span data-ttu-id="94dea-184">Получите примеры кода и сведения о реализации компонентов на основе пользовательского интерфейса Fluent, используемых для создания интерфейсов Teams.</span><span class="sxs-lookup"><span data-stu-id="94dea-184">Get code samples and implementation details for the Fluent UI-based components used to build Teams experiences.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="94dea-185">Попробуйте компоненты пользовательского интерфейса Teams (fluent UI)</span><span class="sxs-lookup"><span data-stu-id="94dea-185">Try Teams UI components (Fluent UI)</span></span>](https://fluentsite.z22.web.core.windows.net/)

### <a name="adaptive-cards-designer"></a><span data-ttu-id="94dea-186">Конструктор адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="94dea-186">Adaptive Cards designer</span></span>

<span data-ttu-id="94dea-187">Разработка адаптивных карт в нашем веб-инструменте.</span><span class="sxs-lookup"><span data-stu-id="94dea-187">Design Adaptive Cards in our web-based tool.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="94dea-188">Попробуйте конструктор адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="94dea-188">Try the Adaptive Cards designer</span></span>](https://adaptivecards.io/designer/)
