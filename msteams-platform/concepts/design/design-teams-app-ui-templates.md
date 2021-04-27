---
title: Проектирование приложения с помощью шаблонов пользовательского интерфейса
author: heath-hamilton
description: Быстрее разработать приложение с помощью стандартизированных компонентов пользовательского интерфейса, макетов и шаблонов, распространенных в Microsoft Teams.
ms.author: lajanuar
localization_priority: Normal
ms.topic: reference
ms.openlocfilehash: d627ce3b29ffa071d0d7e238c572c7cb69fa4cd9
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020767"
---
# <a name="designing-your-microsoft-teams-app-with-ui-templates"></a><span data-ttu-id="47be2-103">Разработка приложения Microsoft Teams с помощью шаблонов пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="47be2-103">Designing your Microsoft Teams app with UI templates</span></span>

<span data-ttu-id="47be2-104">Быстрее разработать приложение Microsoft Teams с помощью шаблонов пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="47be2-104">Design your Microsoft Teams app faster with UI templates.</span></span> <span data-ttu-id="47be2-105">Шаблоны — это коллекция компонентов на основе пользовательского интерфейса Fluent, которые работают в общих случаях использования Teams, что дает вам больше времени, чтобы узнать, как лучше работать с пользователями.</span><span class="sxs-lookup"><span data-stu-id="47be2-105">The templates are a collection of Fluent UI-based components that work across common Teams use cases, giving you more time to figure out the best experience for your users.</span></span>

## <a name="getting-started-with-tools-and-samples"></a><span data-ttu-id="47be2-106">Начало работы с инструментами и примерами</span><span class="sxs-lookup"><span data-stu-id="47be2-106">Getting started with tools and samples</span></span>

<span data-ttu-id="47be2-107">Следующие ресурсы помогут вам разработать и разработать приложение с помощью шаблонов пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="47be2-107">The following resources can help you design and develop your app using UI templates.</span></span>

### <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="47be2-108">Комплект разработчика для пользовательского интерфейса Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="47be2-108">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="47be2-109">Захватите шаблоны пользовательского интерфейса для разработки приложения из набора пользовательского интерфейса Microsoft Teams, который также содержит обширные сведения об использовании, анатомии, доступности и практических методиках.</span><span class="sxs-lookup"><span data-stu-id="47be2-109">Grab UI templates for your app design from the Microsoft Teams UI Kit, which also includes extensive information about usage, anatomy, accessibility, and best practices.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="47be2-110">Получите набор пользовательского интерфейса (Figma)</span><span class="sxs-lookup"><span data-stu-id="47be2-110">Get the UI kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a><span data-ttu-id="47be2-111">Библиотека пользовательского интерфейса Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="47be2-111">Microsoft Teams UI Library</span></span>

<span data-ttu-id="47be2-112">Просмотр и тестирование отдельных шаблонов пользовательского интерфейса Teams и связанных компонентов в браузере.</span><span class="sxs-lookup"><span data-stu-id="47be2-112">View and test individual Teams UI templates and related components in your browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="47be2-113">Попробуйте библиотеку пользовательского интерфейса (детская площадка)</span><span class="sxs-lookup"><span data-stu-id="47be2-113">Try the UI library (playground)</span></span>](https://dev-int.teams.microsoft.com/storybook/main/index.html)

<span data-ttu-id="47be2-114">Импорт этих шаблонов и связанных компонентов непосредственно в проект приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="47be2-114">Import these templates and related components directly into your Teams app project.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="47be2-115">Получить библиотеку пользовательского интерфейса (GitHub)</span><span class="sxs-lookup"><span data-stu-id="47be2-115">Get the UI library (GitHub)</span></span>](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a><span data-ttu-id="47be2-116">Пример приложения</span><span class="sxs-lookup"><span data-stu-id="47be2-116">Sample app</span></span>

<span data-ttu-id="47be2-117">Установите пример приложения, чтобы узнать, как выглядят и ведут себя шаблоны пользовательского интерфейса в контекстах Teams.</span><span class="sxs-lookup"><span data-stu-id="47be2-117">Install a sample app to see how UI templates look and behave within Teams contexts.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="47be2-118">Получить пример приложения (GitHub)</span><span class="sxs-lookup"><span data-stu-id="47be2-118">Get the sample app (GitHub)</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="list"></a><span data-ttu-id="47be2-119">List</span><span class="sxs-lookup"><span data-stu-id="47be2-119">List</span></span>

<span data-ttu-id="47be2-120">Вы можете использовать список для отображения связанных элементов в формате сканируемых элементов и разрешить пользователям принимать меры по всему списку или отдельным пунктам.</span><span class="sxs-lookup"><span data-stu-id="47be2-120">You can use a list to display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>

:::image type="content" source="../../assets/images/ui-templates/list.png" alt-text="В примере показан шаблон пользовательского интерфейса списка." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="47be2-122">Верхние случаи использования</span><span class="sxs-lookup"><span data-stu-id="47be2-122">Top use cases</span></span>

* <span data-ttu-id="47be2-123">Отображение данных</span><span class="sxs-lookup"><span data-stu-id="47be2-123">Display data</span></span>
* <span data-ttu-id="47be2-124">Контекстные действия в контенте приложения</span><span class="sxs-lookup"><span data-stu-id="47be2-124">Contextual actions on app content</span></span>

## <a name="dashboard"></a><span data-ttu-id="47be2-125">Информационная панель</span><span class="sxs-lookup"><span data-stu-id="47be2-125">Dashboard</span></span>

<span data-ttu-id="47be2-126">Панель мониторинга отображает различные типы контента в центре расположения (личное приложение teams или вкладка).</span><span class="sxs-lookup"><span data-stu-id="47be2-126">A dashboard displays different types of content in a central location (Teams personal app or tab).</span></span> <span data-ttu-id="47be2-127">Пользователи должны иметь возможность настраивать хотя бы некоторые из того, что они видят на панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="47be2-127">Users should be able to customize at least some of what they see on a dashboard.</span></span>

:::image type="content" source="../../assets/images/ui-templates/dashboard.png" alt-text="В примере показан шаблон пользовательского интерфейса панели мониторинга." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="47be2-129">Верхние случаи использования</span><span class="sxs-lookup"><span data-stu-id="47be2-129">Top use cases</span></span>

* <span data-ttu-id="47be2-130">Анализ данных</span><span class="sxs-lookup"><span data-stu-id="47be2-130">Analyze data</span></span>
* <span data-ttu-id="47be2-131">Показатели отчета</span><span class="sxs-lookup"><span data-stu-id="47be2-131">Report metrics</span></span>
* <span data-ttu-id="47be2-132">Организация различных сведений в одном месте</span><span class="sxs-lookup"><span data-stu-id="47be2-132">Organize different information in one place</span></span>

## <a name="form"></a><span data-ttu-id="47be2-133">Form</span><span class="sxs-lookup"><span data-stu-id="47be2-133">Form</span></span>

<span data-ttu-id="47be2-134">Формы используются для сбора, проверки и отправки пользовательского ввода структурированным способом.</span><span class="sxs-lookup"><span data-stu-id="47be2-134">Forms are used to collect, validate, and submit user input in a structured way.</span></span> <span data-ttu-id="47be2-135">Четкая маркировка и логические группировки полей ввода имеют решающее значение для хорошего пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="47be2-135">Clear labeling and logical groupings of input fields are critical for a good user experience.</span></span>

:::image type="content" source="../../assets/images/ui-templates/form.png" alt-text="В примере показан шаблон пользовательского интерфейса формы." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="47be2-137">Верхние случаи использования</span><span class="sxs-lookup"><span data-stu-id="47be2-137">Top use cases</span></span>

* <span data-ttu-id="47be2-138">Вход</span><span class="sxs-lookup"><span data-stu-id="47be2-138">Sign in</span></span>
* <span data-ttu-id="47be2-139">Профили пользователей</span><span class="sxs-lookup"><span data-stu-id="47be2-139">User profiles</span></span>
* <span data-ttu-id="47be2-140">Settings</span><span class="sxs-lookup"><span data-stu-id="47be2-140">Settings</span></span>
* <span data-ttu-id="47be2-141">Коллекция входных данных пользователей</span><span class="sxs-lookup"><span data-stu-id="47be2-141">User input collection</span></span>

## <a name="sign-in"></a><span data-ttu-id="47be2-142">Вход</span><span class="sxs-lookup"><span data-stu-id="47be2-142">Sign in</span></span>

<span data-ttu-id="47be2-143">Вы можете создать потоки входов в приложения для различных контекстов Teams и поставщиков удостоверений.</span><span class="sxs-lookup"><span data-stu-id="47be2-143">You can design app sign-in flows for different Teams contexts and identity providers.</span></span> <span data-ttu-id="47be2-144">В следующем примере содержится один вход (SSO), который мы рекомендуем для простейшей проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="47be2-144">The following example includes single sign-on (SSO), which we recommend for the simplest authentication experience.</span></span>

:::image type="content" source="../../assets/images/ui-templates/sign-in.png" alt-text="В примере показан знак в шаблоне пользовательского интерфейса." border="false":::

### <a name="top-use-case"></a><span data-ttu-id="47be2-146">Пример верхнего использования</span><span class="sxs-lookup"><span data-stu-id="47be2-146">Top use case</span></span>

* <span data-ttu-id="47be2-147">Проверка подлинности пользователей</span><span class="sxs-lookup"><span data-stu-id="47be2-147">Authenticate users</span></span>

## <a name="task-board"></a><span data-ttu-id="47be2-148">Доска задач</span><span class="sxs-lookup"><span data-stu-id="47be2-148">Task board</span></span>

<span data-ttu-id="47be2-149">Доска задач, иногда называемая канбанской или плавательные дорожки, — это коллекция карт, часто используемых для отслеживания состояния элементов или билетов.</span><span class="sxs-lookup"><span data-stu-id="47be2-149">A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span> <span data-ttu-id="47be2-150">Он также может использоваться для сортировки любого типа контента на категории.</span><span class="sxs-lookup"><span data-stu-id="47be2-150">It can also be used to sort any type of content into categories.</span></span> <span data-ttu-id="47be2-151">Вы можете изменить и переместить карты между столбцами.</span><span class="sxs-lookup"><span data-stu-id="47be2-151">You can edit and move the cards between columns.</span></span>

:::image type="content" source="../../assets/images/ui-templates/task-board.png" alt-text="В примере показан шаблон пользовательского интерфейса доски задач." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="47be2-153">Верхние случаи использования</span><span class="sxs-lookup"><span data-stu-id="47be2-153">Top use cases</span></span>

* <span data-ttu-id="47be2-154">управление проектами;</span><span class="sxs-lookup"><span data-stu-id="47be2-154">Project management.</span></span> <span data-ttu-id="47be2-155">Назначение задач и состояние отслеживания</span><span class="sxs-lookup"><span data-stu-id="47be2-155">Assigning tasks and tracking status</span></span>
* <span data-ttu-id="47be2-156">Мозговой штурм.</span><span class="sxs-lookup"><span data-stu-id="47be2-156">Brainstorming.</span></span> <span data-ttu-id="47be2-157">Добавление идей в различных категориях</span><span class="sxs-lookup"><span data-stu-id="47be2-157">Adding ideas in different categories</span></span>
* <span data-ttu-id="47be2-158">Упражнения сортировки.</span><span class="sxs-lookup"><span data-stu-id="47be2-158">Sorting exercises.</span></span> <span data-ttu-id="47be2-159">Организация любых сведений в ведра</span><span class="sxs-lookup"><span data-stu-id="47be2-159">Organizing any kind of information into buckets</span></span>

## <a name="data-visualization"></a><span data-ttu-id="47be2-160">Визуализация данных</span><span class="sxs-lookup"><span data-stu-id="47be2-160">Data visualization</span></span>

<span data-ttu-id="47be2-161">Для стека и организации визуализации данных на одной странице можно использовать различные размеры карт (одноместные, двойные и полные).</span><span class="sxs-lookup"><span data-stu-id="47be2-161">You can use different card sizes (single, double, and full) to stack and organize data visualizations on the same page.</span></span> <span data-ttu-id="47be2-162">Шкала карт, чтобы соответствовать макету столбца и заполнять пустые пробелы.</span><span class="sxs-lookup"><span data-stu-id="47be2-162">The cards scale to fit the column layout and fill in blank spaces.</span></span>

:::image type="content" source="../../assets/images/ui-templates/data-viz.png" alt-text="В примере показан шаблон пользовательского интерфейса визуализации данных." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="47be2-164">Верхние случаи использования</span><span class="sxs-lookup"><span data-stu-id="47be2-164">Top use cases</span></span>

* <span data-ttu-id="47be2-165">Отображение сложной информации</span><span class="sxs-lookup"><span data-stu-id="47be2-165">Display complex information</span></span>
* <span data-ttu-id="47be2-166">Создание панели мониторинга</span><span class="sxs-lookup"><span data-stu-id="47be2-166">Create a dashboard</span></span>

## <a name="wizard"></a><span data-ttu-id="47be2-167">Мастер</span><span class="sxs-lookup"><span data-stu-id="47be2-167">Wizard</span></span>

<span data-ttu-id="47be2-168">Мастер направляет пользователя на несколько экранов для выполнения задачи (например, процесса настройки).</span><span class="sxs-lookup"><span data-stu-id="47be2-168">A wizard guides a user through several screens to complete a task (such as a setup process).</span></span>

:::image type="content" source="../../assets/images/ui-templates/wizard.png" alt-text="В примере показан шаблон пользовательского интерфейса мастера." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="47be2-170">Верхние случаи использования</span><span class="sxs-lookup"><span data-stu-id="47be2-170">Top use cases</span></span>

* <span data-ttu-id="47be2-171">Настройка</span><span class="sxs-lookup"><span data-stu-id="47be2-171">Setup</span></span>
* <span data-ttu-id="47be2-172">Адаптация</span><span class="sxs-lookup"><span data-stu-id="47be2-172">Onboarding</span></span>
* <span data-ttu-id="47be2-173">Первый запуск</span><span class="sxs-lookup"><span data-stu-id="47be2-173">First-run experiences</span></span>

## <a name="empty-state"></a><span data-ttu-id="47be2-174">Пустое состояние</span><span class="sxs-lookup"><span data-stu-id="47be2-174">Empty state</span></span>

<span data-ttu-id="47be2-175">Пустой шаблон состояния можно использовать для многих сценариев, включая вход, первый запуск, сообщения об ошибках и многое другое.</span><span class="sxs-lookup"><span data-stu-id="47be2-175">The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span> <span data-ttu-id="47be2-176">Он очень гибкий и адаптируется к использованию одного, нескольких или всех компонентов в следующем дизайне.</span><span class="sxs-lookup"><span data-stu-id="47be2-176">It’s highly flexible⁠—adapt it to use one, a few, or all of the components in the following design.</span></span>

:::image type="content" source="../../assets/images/ui-templates/empty-state.png" alt-text="В примере показан пустой шаблон пользовательского интерфейса состояния." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="47be2-178">Верхние случаи использования</span><span class="sxs-lookup"><span data-stu-id="47be2-178">Top use cases</span></span>

* <span data-ttu-id="47be2-179">Вход</span><span class="sxs-lookup"><span data-stu-id="47be2-179">Sign in</span></span>
* <span data-ttu-id="47be2-180">Приветствие сообщений и первый запуск</span><span class="sxs-lookup"><span data-stu-id="47be2-180">Welcome messages and first-run experiences</span></span>
* <span data-ttu-id="47be2-181">Сообщения об успехе</span><span class="sxs-lookup"><span data-stu-id="47be2-181">Success messages</span></span>
* <span data-ttu-id="47be2-182">Сообщения об ошибках</span><span class="sxs-lookup"><span data-stu-id="47be2-182">Error messages</span></span>

## <a name="notification-bar"></a><span data-ttu-id="47be2-183">Панель уведомлений</span><span class="sxs-lookup"><span data-stu-id="47be2-183">Notification bar</span></span>

<span data-ttu-id="47be2-184">Панели уведомлений — это выделенная область для отображения кратких важных сообщений, не требующих от пользователя немедленных действий.</span><span class="sxs-lookup"><span data-stu-id="47be2-184">A notification bar is a dedicated area for displaying a brief, important messages that do not require the user to take immediate action.</span></span> <span data-ttu-id="47be2-185">Определенные фоновые цвета и значки связаны с определенными типами сообщений (см. ниже).</span><span class="sxs-lookup"><span data-stu-id="47be2-185">Specific background colors and icons are associated with specific types of messages (see below).</span></span>

:::image type="content" source="../../assets/images/ui-templates/notification-bar.png" alt-text="В примере показаны шаблоны панели уведомлений." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="47be2-187">Верхние случаи использования</span><span class="sxs-lookup"><span data-stu-id="47be2-187">Top use cases</span></span>

* <span data-ttu-id="47be2-188">Критически важные сообщения, ошибки и предупреждения</span><span class="sxs-lookup"><span data-stu-id="47be2-188">Critical messages, errors, and warnings</span></span>
* <span data-ttu-id="47be2-189">Сообщения об успехе</span><span class="sxs-lookup"><span data-stu-id="47be2-189">Success messages</span></span>
* <span data-ttu-id="47be2-190">Информационные или рекламные сообщения</span><span class="sxs-lookup"><span data-stu-id="47be2-190">Informational or promotional messages</span></span>

## <a name="left-nav"></a><span data-ttu-id="47be2-191">Левый nav</span><span class="sxs-lookup"><span data-stu-id="47be2-191">Left nav</span></span>

<span data-ttu-id="47be2-192">Используйте левый nav для просмотра нескольких страниц в вкладке Teams. В следующем примере левый nav находится между списком каналов и контентом вкладок.</span><span class="sxs-lookup"><span data-stu-id="47be2-192">Use the left nav to browse multiple pages within your Teams tab. In the following example, the left nav is between the channel list and tab content.</span></span>

:::image type="content" source="../../assets/images/ui-templates/left-nav.png" alt-text="В примере показан левый шаблон nav." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="47be2-194">Верхние случаи использования</span><span class="sxs-lookup"><span data-stu-id="47be2-194">Top use cases</span></span>

* <span data-ttu-id="47be2-195">Просмотр нескольких страниц в вкладке Teams</span><span class="sxs-lookup"><span data-stu-id="47be2-195">Browse multiple pages within a Teams tab</span></span>
* <span data-ttu-id="47be2-196">Разбить сложные приложения на несколько страниц</span><span class="sxs-lookup"><span data-stu-id="47be2-196">Break down complex apps into multiple pages</span></span>

## <a name="breadcrumb"></a><span data-ttu-id="47be2-197">Breadcrumb</span><span class="sxs-lookup"><span data-stu-id="47be2-197">Breadcrumb</span></span>

<span data-ttu-id="47be2-198">Breadcrumbs — это навигационный помощник, который передает иерархию приложения.</span><span class="sxs-lookup"><span data-stu-id="47be2-198">Breadcrumbs are a navigational aid that convey your app’s hierarchy.</span></span> <span data-ttu-id="47be2-199">Они помогают пользователям понять, как просматриваемая страница вписывается в общий опыт и позволяет одним щелчком мыши получить доступ к более высоким уровням в этой иерархии.</span><span class="sxs-lookup"><span data-stu-id="47be2-199">They help users understand how the page they’re viewing fits into the overall experience and afford one-click access to higher levels in that hierarchy.</span></span>

:::image type="content" source="../../assets/images/ui-templates/breadcrumb.png" alt-text="В примере показан шаблон breadcrumb." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="47be2-201">Верхние случаи использования</span><span class="sxs-lookup"><span data-stu-id="47be2-201">Top use cases</span></span>

* <span data-ttu-id="47be2-202">Иерархия связи</span><span class="sxs-lookup"><span data-stu-id="47be2-202">Communicate hierarchy</span></span>
* <span data-ttu-id="47be2-203">Навигация</span><span class="sxs-lookup"><span data-stu-id="47be2-203">Navigation</span></span>

## <a name="toolbar"></a><span data-ttu-id="47be2-204">Панель инструментов</span><span class="sxs-lookup"><span data-stu-id="47be2-204">Toolbar</span></span>

<span data-ttu-id="47be2-205">Панель инструментов — это контейнер для группировки набора элементов управления.</span><span class="sxs-lookup"><span data-stu-id="47be2-205">A toolbar is a container for grouping a set of controls.</span></span>

:::image type="content" source="../../assets/images/ui-templates/toolbar.png" alt-text="В примере показан шаблон панели инструментов." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="47be2-207">Верхние случаи использования</span><span class="sxs-lookup"><span data-stu-id="47be2-207">Top use cases</span></span>

* <span data-ttu-id="47be2-208">Контекстные действия в контенте приложения</span><span class="sxs-lookup"><span data-stu-id="47be2-208">Contextual actions on app content</span></span>
* <span data-ttu-id="47be2-209">Контекстный фильтр и поиск</span><span class="sxs-lookup"><span data-stu-id="47be2-209">Contextual filter and find</span></span>
* <span data-ttu-id="47be2-210">Навигация и сухари</span><span class="sxs-lookup"><span data-stu-id="47be2-210">Navigation and breadcrumbs</span></span>

## <a name="stage"></a><span data-ttu-id="47be2-211">Этап</span><span class="sxs-lookup"><span data-stu-id="47be2-211">Stage</span></span>

<span data-ttu-id="47be2-212">Stage предоставляет пользователям возможность открыть объект, например изображение, файл или веб-сайт, в Teams, а не открывать его в другом приложении или браузере.</span><span class="sxs-lookup"><span data-stu-id="47be2-212">Stage offers a way for users to open an entity—like an image, file, or website—in Teams instead of opening it in another app or browser.</span></span> <span data-ttu-id="47be2-213">Основной пример использования стадии — просмотр; поверхность не должна использоваться для сложных взаимодействий.</span><span class="sxs-lookup"><span data-stu-id="47be2-213">The primary use case of stage is viewing; the surface should not be used for complex interactions.</span></span>

<span data-ttu-id="47be2-214">(Примечание реализации. Создайте этап с помощью большого [модуля задач.)](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)</span><span class="sxs-lookup"><span data-stu-id="47be2-214">(Implementation note: Build your stage using a large [task module](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).)</span></span>

:::image type="content" source="../../assets/images/ui-templates/stage.png" alt-text="В примере показан шаблон стадии." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="47be2-216">Верхние случаи использования</span><span class="sxs-lookup"><span data-stu-id="47be2-216">Top use cases</span></span>

* <span data-ttu-id="47be2-217">Откройте объект в Teams вместо другого приложения или браузера</span><span class="sxs-lookup"><span data-stu-id="47be2-217">Open an entity in Teams instead of another app or browser</span></span>
* <span data-ttu-id="47be2-218">Прожектор мультимедиа или другой контент</span><span class="sxs-lookup"><span data-stu-id="47be2-218">Spotlight media or other content</span></span>
