---
title: Проектирование приложения с помощью шаблонов пользовательского интерфейса
author: heath-hamilton
description: Быстрее проектировать приложение с помощью стандартизированных компонентов пользовательского интерфейса, макетов и шаблонов, обычно встречающихся Microsoft Teams.
ms.author: lajanuar
localization_priority: Normal
ms.topic: reference
ms.openlocfilehash: 0cd5c6c4525e340f9aa53a78749211783880225a
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566021"
---
# <a name="designing-your-microsoft-teams-app-with-ui-templates"></a><span data-ttu-id="55f71-103">Проектирование приложения Microsoft Teams с помощью шаблонов пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="55f71-103">Designing your Microsoft Teams app with UI templates</span></span>

<span data-ttu-id="55f71-104">Быстрее создайте Microsoft Teams с помощью шаблонов пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="55f71-104">Design your Microsoft Teams app faster with UI templates.</span></span> <span data-ttu-id="55f71-105">Шаблоны представляет собой набор компонентов на основе пользовательского интерфейса Fluent, которые работают в обычных случаях Teams использования, что дает вам больше времени, чтобы выяснить лучший опыт для ваших пользователей.</span><span class="sxs-lookup"><span data-stu-id="55f71-105">The templates are a collection of Fluent UI-based components that work across common Teams use cases, giving you more time to figure out the best experience for your users.</span></span>

## <a name="getting-started-with-tools-and-samples"></a><span data-ttu-id="55f71-106">Начало работы с инструментами и образцами</span><span class="sxs-lookup"><span data-stu-id="55f71-106">Getting started with tools and samples</span></span>

<span data-ttu-id="55f71-107">Следующие ресурсы помогут вам спроектировать и разработать приложение с помощью шаблонов пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="55f71-107">The following resources can help you design and develop your app using UI templates.</span></span>

### <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="55f71-108">Комплект разработчика для пользовательского интерфейса Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="55f71-108">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="55f71-109">Захватите шаблоны пользовательского интерфейса для дизайна приложения из набора пользовательского интерфейса Microsoft Teams, который также включает обширную информацию об использовании, анатомии, доступности и передовом опыте.</span><span class="sxs-lookup"><span data-stu-id="55f71-109">Grab UI templates for your app design from the Microsoft Teams UI Kit, which also includes extensive information about usage, anatomy, accessibility, and best practices.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="55f71-110">Получить комплект пользовательского интерфейса (Фигма)</span><span class="sxs-lookup"><span data-stu-id="55f71-110">Get the UI kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a><span data-ttu-id="55f71-111">Microsoft Teams Библиотека пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="55f71-111">Microsoft Teams UI Library</span></span>

<span data-ttu-id="55f71-112">Просмотр и тестирование отдельных Teams пользовательского интерфейса и связанных с ними компонентов в браузере.</span><span class="sxs-lookup"><span data-stu-id="55f71-112">View and test individual Teams UI templates and related components in your browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="55f71-113">Попробуйте библиотеку пользовательского интерфейса (площадка)</span><span class="sxs-lookup"><span data-stu-id="55f71-113">Try the UI library (playground)</span></span>](https://dev-int.teams.microsoft.com/storybook/main/index.html)

<span data-ttu-id="55f71-114">Импорт этих шаблонов и связанных с ними компонентов непосредственно в ваш Teams проекта приложения.</span><span class="sxs-lookup"><span data-stu-id="55f71-114">Import these templates and related components directly into your Teams app project.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="55f71-115">Получить библиотеку пользовательского интерфейса (GitHub)</span><span class="sxs-lookup"><span data-stu-id="55f71-115">Get the UI library (GitHub)</span></span>](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a><span data-ttu-id="55f71-116">Пример приложения</span><span class="sxs-lookup"><span data-stu-id="55f71-116">Sample app</span></span>

<span data-ttu-id="55f71-117">Установите пример приложения, чтобы увидеть, как выглядят и ведут себя шаблоны пользовательского интерфейса Teams контексте.</span><span class="sxs-lookup"><span data-stu-id="55f71-117">Install a sample app to see how UI templates look and behave within Teams contexts.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="55f71-118">Получить образец приложения (GitHub)</span><span class="sxs-lookup"><span data-stu-id="55f71-118">Get the sample app (GitHub)</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="list"></a><span data-ttu-id="55f71-119">List</span><span class="sxs-lookup"><span data-stu-id="55f71-119">List</span></span>

<span data-ttu-id="55f71-120">Вы можете использовать список для отображения связанных элементов в сканируемом формате и позволить пользователям принимать меры по всему списку или отдельным элементам.</span><span class="sxs-lookup"><span data-stu-id="55f71-120">You can use a list to display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>

:::image type="content" source="../../assets/images/ui-templates/list.png" alt-text="Пример показывает шаблон пользовательского интерфейса списка." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="55f71-122">Лучшие случаи использования</span><span class="sxs-lookup"><span data-stu-id="55f71-122">Top use cases</span></span>

* <span data-ttu-id="55f71-123">Отображение данных</span><span class="sxs-lookup"><span data-stu-id="55f71-123">Display data</span></span>
* <span data-ttu-id="55f71-124">Контекстные действия на содержимом приложения</span><span class="sxs-lookup"><span data-stu-id="55f71-124">Contextual actions on app content</span></span>

## <a name="dashboard"></a><span data-ttu-id="55f71-125">Информационная панель</span><span class="sxs-lookup"><span data-stu-id="55f71-125">Dashboard</span></span>

<span data-ttu-id="55f71-126">Панель мониторинга отображает различные типы содержимого в центральном месте (Teams приложение или вкладка).</span><span class="sxs-lookup"><span data-stu-id="55f71-126">A dashboard displays different types of content in a central location (Teams personal app or tab).</span></span> <span data-ttu-id="55f71-127">Пользователи должны иметь возможность настроить по крайней мере некоторые из того, что они видят на панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="55f71-127">Users should be able to customize at least some of what they see on a dashboard.</span></span>

:::image type="content" source="../../assets/images/ui-templates/dashboard.png" alt-text="Пример показывает шаблон пользовательского интерфейса панели мониторинга." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="55f71-129">Лучшие случаи использования</span><span class="sxs-lookup"><span data-stu-id="55f71-129">Top use cases</span></span>

* <span data-ttu-id="55f71-130">Анализ данных</span><span class="sxs-lookup"><span data-stu-id="55f71-130">Analyze data</span></span>
* <span data-ttu-id="55f71-131">Отчетные метрики</span><span class="sxs-lookup"><span data-stu-id="55f71-131">Report metrics</span></span>
* <span data-ttu-id="55f71-132">Организация различной информации в одном месте</span><span class="sxs-lookup"><span data-stu-id="55f71-132">Organize different information in one place</span></span>

## <a name="form"></a><span data-ttu-id="55f71-133">Form</span><span class="sxs-lookup"><span data-stu-id="55f71-133">Form</span></span>

<span data-ttu-id="55f71-134">Формы используются для сбора, проверки и отправки пользовательского ввода структурированным способом.</span><span class="sxs-lookup"><span data-stu-id="55f71-134">Forms are used to collect, validate, and submit user input in a structured way.</span></span> <span data-ttu-id="55f71-135">Четкая маркировка и логические группировки входных полей имеют решающее значение для хорошего пользовательского опыта.</span><span class="sxs-lookup"><span data-stu-id="55f71-135">Clear labeling and logical groupings of input fields are critical for a good user experience.</span></span>

:::image type="content" source="../../assets/images/ui-templates/form.png" alt-text="Пример показывает шаблон пользовательского интерфейса формы." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="55f71-137">Лучшие случаи использования</span><span class="sxs-lookup"><span data-stu-id="55f71-137">Top use cases</span></span>

* <span data-ttu-id="55f71-138">Вход</span><span class="sxs-lookup"><span data-stu-id="55f71-138">Sign in</span></span>
* <span data-ttu-id="55f71-139">Профили пользователей</span><span class="sxs-lookup"><span data-stu-id="55f71-139">User profiles</span></span>
* <span data-ttu-id="55f71-140">Параметры</span><span class="sxs-lookup"><span data-stu-id="55f71-140">Settings</span></span>
* <span data-ttu-id="55f71-141">Сбор пользовательских входных данных</span><span class="sxs-lookup"><span data-stu-id="55f71-141">User input collection</span></span>

## <a name="sign-in"></a><span data-ttu-id="55f71-142">Вход</span><span class="sxs-lookup"><span data-stu-id="55f71-142">Sign in</span></span>

<span data-ttu-id="55f71-143">Вы можете проектировать потоки вовсяки приложений для различных Teams контекстов и поставщиков идентификации.</span><span class="sxs-lookup"><span data-stu-id="55f71-143">You can design app sign-in flows for different Teams contexts and identity providers.</span></span> <span data-ttu-id="55f71-144">Следующий пример включает в себя один знак -на (SSO), который мы рекомендуем для простейшего опыта проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="55f71-144">The following example includes single sign-on (SSO), which we recommend for the simplest authentication experience.</span></span>

:::image type="content" source="../../assets/images/ui-templates/sign-in.png" alt-text="Пример показывает знак в шаблоне пользовательского интерфейса." border="false":::

### <a name="top-use-case"></a><span data-ttu-id="55f71-146">Верхний случай использования</span><span class="sxs-lookup"><span data-stu-id="55f71-146">Top use case</span></span>

* <span data-ttu-id="55f71-147">Аутентичность пользователей</span><span class="sxs-lookup"><span data-stu-id="55f71-147">Authenticate users</span></span>

## <a name="task-board"></a><span data-ttu-id="55f71-148">Целевая доска</span><span class="sxs-lookup"><span data-stu-id="55f71-148">Task board</span></span>

<span data-ttu-id="55f71-149">Доска задач, иногда называемая доска kanban или swim lanes, представляет собой набор карт, часто используемых для отслеживания состояния рабочих предметов или билетов.</span><span class="sxs-lookup"><span data-stu-id="55f71-149">A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span> <span data-ttu-id="55f71-150">Он также может быть использован для сортировки любого типа контента по категориям.</span><span class="sxs-lookup"><span data-stu-id="55f71-150">It can also be used to sort any type of content into categories.</span></span> <span data-ttu-id="55f71-151">Вы можете редактировать и перемещать карты между столбцами.</span><span class="sxs-lookup"><span data-stu-id="55f71-151">You can edit and move the cards between columns.</span></span>

:::image type="content" source="../../assets/images/ui-templates/task-board.png" alt-text="Пример показывает шаблон пользовательского интерфейса доски задач." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="55f71-153">Лучшие случаи использования</span><span class="sxs-lookup"><span data-stu-id="55f71-153">Top use cases</span></span>

* <span data-ttu-id="55f71-154">Project: Назначение задач и отслеживание статуса.</span><span class="sxs-lookup"><span data-stu-id="55f71-154">Project management: Assigning tasks and tracking status.</span></span>
* <span data-ttu-id="55f71-155">Мозговой штурм: Добавление идей в разных категориях.</span><span class="sxs-lookup"><span data-stu-id="55f71-155">Brainstorming: Adding ideas in different categories.</span></span>
* <span data-ttu-id="55f71-156">Сортировка упражнения: Организация любой информации в ведра.</span><span class="sxs-lookup"><span data-stu-id="55f71-156">Sorting exercises: Organizing any kind of information into buckets.</span></span>

## <a name="data-visualization"></a><span data-ttu-id="55f71-157">Визуализация данных</span><span class="sxs-lookup"><span data-stu-id="55f71-157">Data visualization</span></span>

<span data-ttu-id="55f71-158">Вы можете использовать различные размеры карт (одиночные, двойные и полные) для укладки и организации визуализации данных на одной странице.</span><span class="sxs-lookup"><span data-stu-id="55f71-158">You can use different card sizes (single, double, and full) to stack and organize data visualizations on the same page.</span></span> <span data-ttu-id="55f71-159">Масштаб карт соответствует макету столбца и заполняет пробелы.</span><span class="sxs-lookup"><span data-stu-id="55f71-159">The cards scale to fit the column layout and fill in blank spaces.</span></span>

:::image type="content" source="../../assets/images/ui-templates/data-viz.png" alt-text="Пример показывает шаблон визуализации данных пользовательского интерфейса." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="55f71-161">Лучшие случаи использования</span><span class="sxs-lookup"><span data-stu-id="55f71-161">Top use cases</span></span>

* <span data-ttu-id="55f71-162">Отображение сложной информации</span><span class="sxs-lookup"><span data-stu-id="55f71-162">Display complex information</span></span>
* <span data-ttu-id="55f71-163">Создание панели мониторинга</span><span class="sxs-lookup"><span data-stu-id="55f71-163">Create a dashboard</span></span>

## <a name="wizard"></a><span data-ttu-id="55f71-164">Мастер</span><span class="sxs-lookup"><span data-stu-id="55f71-164">Wizard</span></span>

<span data-ttu-id="55f71-165">Мастер направляет пользователя через несколько экранов для выполнения задачи (например, процесса настройки).</span><span class="sxs-lookup"><span data-stu-id="55f71-165">A wizard guides a user through several screens to complete a task (such as a setup process).</span></span>

:::image type="content" source="../../assets/images/ui-templates/wizard.png" alt-text="Пример показывает шаблон пользовательского интерфейса мастера." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="55f71-167">Лучшие случаи использования</span><span class="sxs-lookup"><span data-stu-id="55f71-167">Top use cases</span></span>

* <span data-ttu-id="55f71-168">Настройка</span><span class="sxs-lookup"><span data-stu-id="55f71-168">Setup</span></span>
* <span data-ttu-id="55f71-169">Адаптация</span><span class="sxs-lookup"><span data-stu-id="55f71-169">Onboarding</span></span>
* <span data-ttu-id="55f71-170">Первый опыт работы</span><span class="sxs-lookup"><span data-stu-id="55f71-170">First-run experiences</span></span>

## <a name="empty-state"></a><span data-ttu-id="55f71-171">Пустое состояние</span><span class="sxs-lookup"><span data-stu-id="55f71-171">Empty state</span></span>

<span data-ttu-id="55f71-172">Пустой шаблон состояния может быть использован для многих сценариев, включая войти в первый запуск, сообщения об ошибках и многое другое.</span><span class="sxs-lookup"><span data-stu-id="55f71-172">The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span> <span data-ttu-id="55f71-173">Он очень гибкий – адаптируем его к использованию одного, нескольких или всех компонентов в следующем дизайне.</span><span class="sxs-lookup"><span data-stu-id="55f71-173">It’s highly flexible⁠—adapt it to use one, a few, or all of the components in the following design.</span></span>

:::image type="content" source="../../assets/images/ui-templates/empty-state.png" alt-text="Пример показывает пустой шаблон пользовательского интерфейса состояния." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="55f71-175">Лучшие случаи использования</span><span class="sxs-lookup"><span data-stu-id="55f71-175">Top use cases</span></span>

* <span data-ttu-id="55f71-176">Вход</span><span class="sxs-lookup"><span data-stu-id="55f71-176">Sign in</span></span>
* <span data-ttu-id="55f71-177">Приветственные сообщения и первый запуск</span><span class="sxs-lookup"><span data-stu-id="55f71-177">Welcome messages and first-run experiences</span></span>
* <span data-ttu-id="55f71-178">Сообщения об успехе</span><span class="sxs-lookup"><span data-stu-id="55f71-178">Success messages</span></span>
* <span data-ttu-id="55f71-179">Сообщения об ошибках</span><span class="sxs-lookup"><span data-stu-id="55f71-179">Error messages</span></span>

## <a name="notification-bar"></a><span data-ttu-id="55f71-180">Панель уведомлений</span><span class="sxs-lookup"><span data-stu-id="55f71-180">Notification bar</span></span>

<span data-ttu-id="55f71-181">Бар уведомлений является выделенной областью для отображения кратких, важных сообщений, которые не требуют от пользователя принятия незамедлительных мер.</span><span class="sxs-lookup"><span data-stu-id="55f71-181">A notification bar is a dedicated area for displaying a brief, important messages that do not require the user to take immediate action.</span></span> <span data-ttu-id="55f71-182">Конкретные цвета фона и значки связаны с определенными типами сообщений (см. ниже).</span><span class="sxs-lookup"><span data-stu-id="55f71-182">Specific background colors and icons are associated with specific types of messages (see below).</span></span>

:::image type="content" source="../../assets/images/ui-templates/notification-bar.png" alt-text="Пример показывает шаблоны баров уведомлений." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="55f71-184">Лучшие случаи использования</span><span class="sxs-lookup"><span data-stu-id="55f71-184">Top use cases</span></span>

* <span data-ttu-id="55f71-185">Критические сообщения, ошибки и предупреждения</span><span class="sxs-lookup"><span data-stu-id="55f71-185">Critical messages, errors, and warnings</span></span>
* <span data-ttu-id="55f71-186">Сообщения об успехе</span><span class="sxs-lookup"><span data-stu-id="55f71-186">Success messages</span></span>
* <span data-ttu-id="55f71-187">Информационные или рекламные сообщения</span><span class="sxs-lookup"><span data-stu-id="55f71-187">Informational or promotional messages</span></span>

## <a name="left-nav"></a><span data-ttu-id="55f71-188">Левый навигатор</span><span class="sxs-lookup"><span data-stu-id="55f71-188">Left nav</span></span>

<span data-ttu-id="55f71-189">Используйте левый навигатор для просмотра нескольких страниц в вашей Teams вкладке. В следующем примере левый навигатор находится между списком каналов и содержанием вкладок.</span><span class="sxs-lookup"><span data-stu-id="55f71-189">Use the left nav to browse multiple pages within your Teams tab. In the following example, the left nav is between the channel list and tab content.</span></span>

:::image type="content" source="../../assets/images/ui-templates/left-nav.png" alt-text="Пример показывает левый шаблон навигации." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="55f71-191">Лучшие случаи использования</span><span class="sxs-lookup"><span data-stu-id="55f71-191">Top use cases</span></span>

* <span data-ttu-id="55f71-192">Просматривайте несколько страниц в Teams вкладке.</span><span class="sxs-lookup"><span data-stu-id="55f71-192">Browse multiple pages within a Teams tab.</span></span>
* <span data-ttu-id="55f71-193">Разбей сложные приложения на несколько страниц.</span><span class="sxs-lookup"><span data-stu-id="55f71-193">Break down complex apps into multiple pages.</span></span>

## <a name="breadcrumb"></a><span data-ttu-id="55f71-194">Breadcrumb</span><span class="sxs-lookup"><span data-stu-id="55f71-194">Breadcrumb</span></span>

<span data-ttu-id="55f71-195">Breadcrumbs являются навигационным помощником, который передает иерархию вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="55f71-195">Breadcrumbs are a navigational aid that convey your app’s hierarchy.</span></span> <span data-ttu-id="55f71-196">Они помогают пользователям понять, как страница, которую они просматривают, вписывается в общий опыт и позволить себе доступ одним щелчком мыши к более высоким уровням в этой иерархии.</span><span class="sxs-lookup"><span data-stu-id="55f71-196">They help users understand how the page they’re viewing fits into the overall experience and afford one-click access to higher levels in that hierarchy.</span></span>

:::image type="content" source="../../assets/images/ui-templates/breadcrumb.png" alt-text="Пример показывает шаблон панировочных сухарей." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="55f71-198">Лучшие случаи использования</span><span class="sxs-lookup"><span data-stu-id="55f71-198">Top use cases</span></span>

* <span data-ttu-id="55f71-199">Иерархия общения</span><span class="sxs-lookup"><span data-stu-id="55f71-199">Communicate hierarchy</span></span>
* <span data-ttu-id="55f71-200">Навигация</span><span class="sxs-lookup"><span data-stu-id="55f71-200">Navigation</span></span>

## <a name="toolbar"></a><span data-ttu-id="55f71-201">Панель инструментов</span><span class="sxs-lookup"><span data-stu-id="55f71-201">Toolbar</span></span>

<span data-ttu-id="55f71-202">Панель инструментов является контейнером для группировки набора элементов управления.</span><span class="sxs-lookup"><span data-stu-id="55f71-202">A toolbar is a container for grouping a set of controls.</span></span>

:::image type="content" source="../../assets/images/ui-templates/toolbar.png" alt-text="Пример показывает шаблон панели инструментов." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="55f71-204">Лучшие случаи использования</span><span class="sxs-lookup"><span data-stu-id="55f71-204">Top use cases</span></span>

* <span data-ttu-id="55f71-205">Контекстные действия на содержимом приложения</span><span class="sxs-lookup"><span data-stu-id="55f71-205">Contextual actions on app content</span></span>
* <span data-ttu-id="55f71-206">Контекстный фильтр и найти</span><span class="sxs-lookup"><span data-stu-id="55f71-206">Contextual filter and find</span></span>
* <span data-ttu-id="55f71-207">Навигация и панировочные сухари</span><span class="sxs-lookup"><span data-stu-id="55f71-207">Navigation and breadcrumbs</span></span>

## <a name="stage"></a><span data-ttu-id="55f71-208">Этап</span><span class="sxs-lookup"><span data-stu-id="55f71-208">Stage</span></span>

<span data-ttu-id="55f71-209">Stage предлагает пользователям способ открыть объект, например изображение, файл или веб-сайт, в Teams вместо того, чтобы открывать его в другом приложении или браузере.</span><span class="sxs-lookup"><span data-stu-id="55f71-209">Stage offers a way for users to open an entity—like an image, file, or website—in Teams instead of opening it in another app or browser.</span></span> <span data-ttu-id="55f71-210">Основным примером использования этапа является просмотр; поверхность не должна использоваться для сложных взаимодействий.</span><span class="sxs-lookup"><span data-stu-id="55f71-210">The primary use case of stage is viewing; the surface should not be used for complex interactions.</span></span>

<span data-ttu-id="55f71-211">(Примечание к реализации: Создайте свой этап с помощью [большого модуля задач](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).)</span><span class="sxs-lookup"><span data-stu-id="55f71-211">(Implementation note: Build your stage using a large [task module](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).)</span></span>

:::image type="content" source="../../assets/images/ui-templates/stage.png" alt-text="Пример показывает шаблон сцены." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="55f71-213">Лучшие случаи использования</span><span class="sxs-lookup"><span data-stu-id="55f71-213">Top use cases</span></span>

* <span data-ttu-id="55f71-214">Откройте объект в Teams вместо другого приложения или браузера.</span><span class="sxs-lookup"><span data-stu-id="55f71-214">Open an entity in Teams instead of another app or browser.</span></span>
* <span data-ttu-id="55f71-215">Средства массовой информации или другой контент.</span><span class="sxs-lookup"><span data-stu-id="55f71-215">Spotlight media or other content.</span></span>
