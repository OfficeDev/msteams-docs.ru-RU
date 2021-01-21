---
title: Проектирование приложения с помощью шаблонов пользовательского интерфейса
author: heath-hamilton
description: Быстрее проектируйте приложение с помощью стандартизированных компонентов пользовательского интерфейса, макетов и шаблонов, которые часто встречается в Microsoft Teams.
ms.author: lajanuar
ms.topic: reference
ms.openlocfilehash: b4d244bbf78ac85042d5caf8ec84afe42e79b3c7
ms.sourcegitcommit: 00c657e3bf57d3b92aca7da941cde47a2eeff4d0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/20/2021
ms.locfileid: "49911928"
---
# <a name="designing-your-microsoft-teams-app-with-ui-templates"></a><span data-ttu-id="164d0-103">Проектирование приложения Microsoft Teams с помощью шаблонов пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="164d0-103">Designing your Microsoft Teams app with UI templates</span></span>

<span data-ttu-id="164d0-104">Быстрее проектировать приложение Microsoft Teams с помощью шаблонов пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="164d0-104">Design your Microsoft Teams app faster with UI templates.</span></span> <span data-ttu-id="164d0-105">Шаблоны — это коллекция компонентов на основе пользовательского интерфейса Fluent, которые работают в распространенных случаях использования Teams, что дает вам больше времени, чтобы найти оптимальный интерфейс для пользователей.</span><span class="sxs-lookup"><span data-stu-id="164d0-105">The templates are a collection of Fluent UI-based components that work across common Teams use cases, giving you more time to figure out the best experience for your users.</span></span>

## <a name="getting-started-with-tools-and-samples"></a><span data-ttu-id="164d0-106">Начало работы со средствами и примерами</span><span class="sxs-lookup"><span data-stu-id="164d0-106">Getting started with tools and samples</span></span>

<span data-ttu-id="164d0-107">Следующие ресурсы помогут вам разработать и разработать приложение с помощью шаблонов пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="164d0-107">The following resources can help you design and develop your app using UI templates.</span></span>

### <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="164d0-108">Пакет пользовательского интерфейса Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="164d0-108">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="164d0-109">Получите шаблоны пользовательского интерфейса для разработки приложения из комплекта пользовательского интерфейса Microsoft Teams, который также содержит подробную информацию об использовании, анатомии, возможностях и практических методиках.</span><span class="sxs-lookup"><span data-stu-id="164d0-109">Grab UI templates for your app design from the Microsoft Teams UI Kit, which also includes extensive information about usage, anatomy, accessibility, and best practices.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="164d0-110">Get the UI kit (Figma)</span><span class="sxs-lookup"><span data-stu-id="164d0-110">Get the UI kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a><span data-ttu-id="164d0-111">Библиотека пользовательского интерфейса Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="164d0-111">Microsoft Teams UI Library</span></span>

<span data-ttu-id="164d0-112">Просмотр и тестирование отдельных шаблонов пользовательского интерфейса Teams и связанных компонентов в браузере.</span><span class="sxs-lookup"><span data-stu-id="164d0-112">View and test individual Teams UI templates and related components in your browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="164d0-113">Попробуйте библиотеку пользовательского интерфейса (игровая библиотека)</span><span class="sxs-lookup"><span data-stu-id="164d0-113">Try the UI library (playground)</span></span>](https://dev-int.teams.microsoft.com/storybook/main/index.html)

<span data-ttu-id="164d0-114">Импортировать эти шаблоны и связанные компоненты непосредственно в проект приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="164d0-114">Import these templates and related components directly into your Teams app project.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="164d0-115">Получить библиотеку пользовательского интерфейса (GitHub)</span><span class="sxs-lookup"><span data-stu-id="164d0-115">Get the UI library (GitHub)</span></span>](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a><span data-ttu-id="164d0-116">Пример приложения</span><span class="sxs-lookup"><span data-stu-id="164d0-116">Sample app</span></span>

<span data-ttu-id="164d0-117">Установите пример приложения, чтобы увидеть, как шаблоны пользовательского интерфейса выглядят и работают в контекстах Teams.</span><span class="sxs-lookup"><span data-stu-id="164d0-117">Install a sample app to see how UI templates look and behave within Teams contexts.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="164d0-118">Получить пример приложения (GitHub)</span><span class="sxs-lookup"><span data-stu-id="164d0-118">Get the sample app (GitHub)</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="list"></a><span data-ttu-id="164d0-119">Перечисление</span><span class="sxs-lookup"><span data-stu-id="164d0-119">List</span></span>

<span data-ttu-id="164d0-120">Вы можете использовать список для отображения связанных элементов в сканируемый формат и разрешить пользователям действия над всем списком или отдельными элементами.</span><span class="sxs-lookup"><span data-stu-id="164d0-120">You can use a list to display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>

:::image type="content" source="../../assets/images/ui-templates/list.png" alt-text="В примере показан шаблон пользовательского интерфейса списка." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="164d0-122">Лучшие случаи использования</span><span class="sxs-lookup"><span data-stu-id="164d0-122">Top use cases</span></span>

* <span data-ttu-id="164d0-123">Отображение данных</span><span class="sxs-lookup"><span data-stu-id="164d0-123">Display data</span></span>
* <span data-ttu-id="164d0-124">Контекстные действия с содержимым приложения</span><span class="sxs-lookup"><span data-stu-id="164d0-124">Contextual actions on app content</span></span>

## <a name="dashboard"></a><span data-ttu-id="164d0-125">Информационная панель</span><span class="sxs-lookup"><span data-stu-id="164d0-125">Dashboard</span></span>

<span data-ttu-id="164d0-126">Панель мониторинга отображает различные типы содержимого в центральном расположении (личное приложение или вкладка Teams).</span><span class="sxs-lookup"><span data-stu-id="164d0-126">A dashboard displays different types of content in a central location (Teams personal app or tab).</span></span> <span data-ttu-id="164d0-127">Пользователи должны иметь возможность настраивать по крайней мере некоторые из того, что они видят на панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="164d0-127">Users should be able to customize at least some of what they see on a dashboard.</span></span>

:::image type="content" source="../../assets/images/ui-templates/dashboard.png" alt-text="В примере показан шаблон пользовательского интерфейса панели мониторинга." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="164d0-129">Лучшие случаи использования</span><span class="sxs-lookup"><span data-stu-id="164d0-129">Top use cases</span></span>

* <span data-ttu-id="164d0-130">Анализ данных</span><span class="sxs-lookup"><span data-stu-id="164d0-130">Analyze data</span></span>
* <span data-ttu-id="164d0-131">Показатели отчета</span><span class="sxs-lookup"><span data-stu-id="164d0-131">Report metrics</span></span>
* <span data-ttu-id="164d0-132">Организация разных сведений в одном месте</span><span class="sxs-lookup"><span data-stu-id="164d0-132">Organize different information in one place</span></span>

## <a name="form"></a><span data-ttu-id="164d0-133">Form</span><span class="sxs-lookup"><span data-stu-id="164d0-133">Form</span></span>

<span data-ttu-id="164d0-134">Формы используются для сбора, проверки и отправки входных данных пользователей структурированным образом.</span><span class="sxs-lookup"><span data-stu-id="164d0-134">Forms are used to collect, validate, and submit user input in a structured way.</span></span> <span data-ttu-id="164d0-135">Очистка меток и логические группировки полей ввода критически важны для хорошего пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="164d0-135">Clear labeling and logical groupings of input fields are critical for a good user experience.</span></span>

:::image type="content" source="../../assets/images/ui-templates/form.png" alt-text="В примере показан шаблон пользовательского интерфейса формы." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="164d0-137">Лучшие случаи использования</span><span class="sxs-lookup"><span data-stu-id="164d0-137">Top use cases</span></span>

* <span data-ttu-id="164d0-138">Вход</span><span class="sxs-lookup"><span data-stu-id="164d0-138">Sign in</span></span>
* <span data-ttu-id="164d0-139">Профили пользователей</span><span class="sxs-lookup"><span data-stu-id="164d0-139">User profiles</span></span>
* <span data-ttu-id="164d0-140">Параметры</span><span class="sxs-lookup"><span data-stu-id="164d0-140">Settings</span></span>
* <span data-ttu-id="164d0-141">Коллекция пользовательских входных данных</span><span class="sxs-lookup"><span data-stu-id="164d0-141">User input collection</span></span>

## <a name="sign-in"></a><span data-ttu-id="164d0-142">Вход</span><span class="sxs-lookup"><span data-stu-id="164d0-142">Sign in</span></span>

<span data-ttu-id="164d0-143">Вы можете разработать потоки входов в приложения для различных контекстов Teams и поставщиков удостоверений.</span><span class="sxs-lookup"><span data-stu-id="164d0-143">You can design app sign-in flows for different Teams contexts and identity providers.</span></span> <span data-ttu-id="164d0-144">В следующем примере включается единый вход ( SSO), который рекомендуется для простейшей проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="164d0-144">The following example includes single sign-on (SSO), which we recommend for the simplest authentication experience.</span></span>

:::image type="content" source="../../assets/images/ui-templates/sign-in.png" alt-text="В примере показан шаблон для входов в пользовательский интерфейс." border="false":::

### <a name="top-use-case"></a><span data-ttu-id="164d0-146">Пример использования</span><span class="sxs-lookup"><span data-stu-id="164d0-146">Top use case</span></span>

* <span data-ttu-id="164d0-147">Проверка подлинности пользователей</span><span class="sxs-lookup"><span data-stu-id="164d0-147">Authenticate users</span></span>

## <a name="task-board"></a><span data-ttu-id="164d0-148">Доска задач</span><span class="sxs-lookup"><span data-stu-id="164d0-148">Task board</span></span>

<span data-ttu-id="164d0-149">Доска задач, иногда называемая доской канан или плаваком, — это коллекция карточек, часто используемых для отслеживания состояния элементов или билетов.</span><span class="sxs-lookup"><span data-stu-id="164d0-149">A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span> <span data-ttu-id="164d0-150">Его также можно использовать для сортировки любого типа контента по категориям.</span><span class="sxs-lookup"><span data-stu-id="164d0-150">It can also be used to sort any type of content into categories.</span></span> <span data-ttu-id="164d0-151">Карточки можно редактировать и перемещать между столбцами.</span><span class="sxs-lookup"><span data-stu-id="164d0-151">You can edit and move the cards between columns.</span></span>

:::image type="content" source="../../assets/images/ui-templates/task-board.png" alt-text="В примере показан шаблон пользовательского интерфейса доски задач." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="164d0-153">Лучшие случаи использования</span><span class="sxs-lookup"><span data-stu-id="164d0-153">Top use cases</span></span>

* <span data-ttu-id="164d0-154">управление проектами;</span><span class="sxs-lookup"><span data-stu-id="164d0-154">Project management.</span></span> <span data-ttu-id="164d0-155">Назначение задач и состояние отслеживания</span><span class="sxs-lookup"><span data-stu-id="164d0-155">Assigning tasks and tracking status</span></span>
* <span data-ttu-id="164d0-156">Многая мягок.</span><span class="sxs-lookup"><span data-stu-id="164d0-156">Brainstorming.</span></span> <span data-ttu-id="164d0-157">Добавление идей в различных категориях</span><span class="sxs-lookup"><span data-stu-id="164d0-157">Adding ideas in different categories</span></span>
* <span data-ttu-id="164d0-158">Сортировка упражнений.</span><span class="sxs-lookup"><span data-stu-id="164d0-158">Sorting exercises.</span></span> <span data-ttu-id="164d0-159">Организация любых сведений по сегментам</span><span class="sxs-lookup"><span data-stu-id="164d0-159">Organizing any kind of information into buckets</span></span>

## <a name="data-visualization"></a><span data-ttu-id="164d0-160">Визуализация данных</span><span class="sxs-lookup"><span data-stu-id="164d0-160">Data visualization</span></span>

<span data-ttu-id="164d0-161">Для стека и организации визуализации данных на одной странице можно использовать разные размеры карт (один, двойной и полный).</span><span class="sxs-lookup"><span data-stu-id="164d0-161">You can use different card sizes (single, double, and full) to stack and organize data visualizations on the same page.</span></span> <span data-ttu-id="164d0-162">Карточки масштабются в форме макета столбца и заполняются пустыми пробелами.</span><span class="sxs-lookup"><span data-stu-id="164d0-162">The cards scale to fit the column layout and fill in blank spaces.</span></span>

:::image type="content" source="../../assets/images/ui-templates/data-viz.png" alt-text="В примере показан шаблон пользовательского интерфейса визуализации данных." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="164d0-164">Лучшие случаи использования</span><span class="sxs-lookup"><span data-stu-id="164d0-164">Top use cases</span></span>

* <span data-ttu-id="164d0-165">Отображение сложной информации</span><span class="sxs-lookup"><span data-stu-id="164d0-165">Display complex information</span></span>
* <span data-ttu-id="164d0-166">Создание панели мониторинга</span><span class="sxs-lookup"><span data-stu-id="164d0-166">Create a dashboard</span></span>

## <a name="wizard"></a><span data-ttu-id="164d0-167">Мастер</span><span class="sxs-lookup"><span data-stu-id="164d0-167">Wizard</span></span>

<span data-ttu-id="164d0-168">Мастер поможет пользователю выполнить задачу (например, выполнить настройку) на нескольких экранах.</span><span class="sxs-lookup"><span data-stu-id="164d0-168">A wizard guides a user through several screens to complete a task (such as a setup process).</span></span>

:::image type="content" source="../../assets/images/ui-templates/wizard.png" alt-text="В примере показан шаблон пользовательского интерфейса мастера." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="164d0-170">Лучшие случаи использования</span><span class="sxs-lookup"><span data-stu-id="164d0-170">Top use cases</span></span>

* <span data-ttu-id="164d0-171">Настройка</span><span class="sxs-lookup"><span data-stu-id="164d0-171">Setup</span></span>
* <span data-ttu-id="164d0-172">Адаптация</span><span class="sxs-lookup"><span data-stu-id="164d0-172">Onboarding</span></span>
* <span data-ttu-id="164d0-173">Первый запуск</span><span class="sxs-lookup"><span data-stu-id="164d0-173">First-run experiences</span></span>

## <a name="empty-state"></a><span data-ttu-id="164d0-174">Пустое состояние</span><span class="sxs-lookup"><span data-stu-id="164d0-174">Empty state</span></span>

<span data-ttu-id="164d0-175">Пустой шаблон состояния можно использовать для многих сценариев, включая вход, первый запуск, сообщения об ошибках и многое другое.</span><span class="sxs-lookup"><span data-stu-id="164d0-175">The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span> <span data-ttu-id="164d0-176">Он очень гибкий — адаптируется к использованию одного, нескольких или всех компонентов в следующем проекте.</span><span class="sxs-lookup"><span data-stu-id="164d0-176">It’s highly flexible⁠—adapt it to use one, a few, or all of the components in the following design.</span></span>

:::image type="content" source="../../assets/images/ui-templates/empty-state.png" alt-text="В примере показан пустой шаблон пользовательского интерфейса состояния." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="164d0-178">Лучшие случаи использования</span><span class="sxs-lookup"><span data-stu-id="164d0-178">Top use cases</span></span>

* <span data-ttu-id="164d0-179">Вход</span><span class="sxs-lookup"><span data-stu-id="164d0-179">Sign in</span></span>
* <span data-ttu-id="164d0-180">Приветствия и первый запуск</span><span class="sxs-lookup"><span data-stu-id="164d0-180">Welcome messages and first-run experiences</span></span>
* <span data-ttu-id="164d0-181">Сообщения об успешном успешном собраии</span><span class="sxs-lookup"><span data-stu-id="164d0-181">Success messages</span></span>
* <span data-ttu-id="164d0-182">Сообщения об ошибках</span><span class="sxs-lookup"><span data-stu-id="164d0-182">Error messages</span></span>

## <a name="notification-bar"></a><span data-ttu-id="164d0-183">Панель уведомлений</span><span class="sxs-lookup"><span data-stu-id="164d0-183">Notification bar</span></span>

<span data-ttu-id="164d0-184">Область уведомлений — это выделенная область для отображения кратких важных сообщений, которые не требуют немедленного действия пользователя.</span><span class="sxs-lookup"><span data-stu-id="164d0-184">A notification bar is a dedicated area for displaying a brief, important messages that do not require the user to take immediate action.</span></span> <span data-ttu-id="164d0-185">Определенные цвета фона и значки связаны с определенными типами сообщений (см. ниже).</span><span class="sxs-lookup"><span data-stu-id="164d0-185">Specific background colors and icons are associated with specific types of messages (see below).</span></span>

:::image type="content" source="../../assets/images/ui-templates/notification-bar.png" alt-text="В примере показаны шаблоны панели уведомлений." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="164d0-187">Лучшие случаи использования</span><span class="sxs-lookup"><span data-stu-id="164d0-187">Top use cases</span></span>

* <span data-ttu-id="164d0-188">Критические сообщения, ошибки и предупреждения</span><span class="sxs-lookup"><span data-stu-id="164d0-188">Critical messages, errors, and warnings</span></span>
* <span data-ttu-id="164d0-189">Сообщения об успешном успешном собраии</span><span class="sxs-lookup"><span data-stu-id="164d0-189">Success messages</span></span>
* <span data-ttu-id="164d0-190">Информационные или рекламные сообщения</span><span class="sxs-lookup"><span data-stu-id="164d0-190">Informational or promotional messages</span></span>

## <a name="left-nav"></a><span data-ttu-id="164d0-191">Левый nav</span><span class="sxs-lookup"><span data-stu-id="164d0-191">Left nav</span></span>

<span data-ttu-id="164d0-192">Используйте левую вкладку для просмотра нескольких страниц на вкладке Teams. В следующем примере левый канал находится между списком каналов и содержимым вкладок.</span><span class="sxs-lookup"><span data-stu-id="164d0-192">Use the left nav to browse multiple pages within your Teams tab. In the following example, the left nav is between the channel list and tab content.</span></span>

:::image type="content" source="../../assets/images/ui-templates/left-nav.png" alt-text="В примере показан левый шаблон nav." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="164d0-194">Лучшие случаи использования</span><span class="sxs-lookup"><span data-stu-id="164d0-194">Top use cases</span></span>

* <span data-ttu-id="164d0-195">Просмотр нескольких страниц на вкладке Teams</span><span class="sxs-lookup"><span data-stu-id="164d0-195">Browse multiple pages within a Teams tab</span></span>
* <span data-ttu-id="164d0-196">Разбитие сложных приложений на несколько страниц</span><span class="sxs-lookup"><span data-stu-id="164d0-196">Break down complex apps into multiple pages</span></span>

## <a name="breadcrumb"></a><span data-ttu-id="164d0-197">Строка навигации</span><span class="sxs-lookup"><span data-stu-id="164d0-197">Breadcrumb</span></span>

<span data-ttu-id="164d0-198">Навигационные переходы — это навигационный помощник, который передает иерархию приложения.</span><span class="sxs-lookup"><span data-stu-id="164d0-198">Breadcrumbs are a navigational aid that convey your app’s hierarchy.</span></span> <span data-ttu-id="164d0-199">Они помогают пользователям понять, как просматриваемая страница соответствует общему опыту, и помогают одним щелчком мыши получить доступ к более высоким уровням в этой иерархии.</span><span class="sxs-lookup"><span data-stu-id="164d0-199">They help users understand how the page they’re viewing fits into the overall experience and afford one-click access to higher levels in that hierarchy.</span></span>

:::image type="content" source="../../assets/images/ui-templates/breadcrumb.png" alt-text="В примере показан шаблон навигации." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="164d0-201">Лучшие случаи использования</span><span class="sxs-lookup"><span data-stu-id="164d0-201">Top use cases</span></span>

* <span data-ttu-id="164d0-202">Иерархия общения</span><span class="sxs-lookup"><span data-stu-id="164d0-202">Communicate hierarchy</span></span>
* <span data-ttu-id="164d0-203">Навигация</span><span class="sxs-lookup"><span data-stu-id="164d0-203">Navigation</span></span>

## <a name="toolbar"></a><span data-ttu-id="164d0-204">Панель инструментов</span><span class="sxs-lookup"><span data-stu-id="164d0-204">Toolbar</span></span>

<span data-ttu-id="164d0-205">Панель инструментов — это контейнер для группировки набора элементов управления.</span><span class="sxs-lookup"><span data-stu-id="164d0-205">A toolbar is a container for grouping a set of controls.</span></span>

:::image type="content" source="../../assets/images/ui-templates/toolbar.png" alt-text="В примере показан шаблон панели инструментов." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="164d0-207">Лучшие случаи использования</span><span class="sxs-lookup"><span data-stu-id="164d0-207">Top use cases</span></span>

* <span data-ttu-id="164d0-208">Контекстные действия с содержимым приложения</span><span class="sxs-lookup"><span data-stu-id="164d0-208">Contextual actions on app content</span></span>
* <span data-ttu-id="164d0-209">Контекстный фильтр и поиск</span><span class="sxs-lookup"><span data-stu-id="164d0-209">Contextual filter and find</span></span>
* <span data-ttu-id="164d0-210">Навигация и навигационные переходы</span><span class="sxs-lookup"><span data-stu-id="164d0-210">Navigation and breadcrumbs</span></span>

## <a name="stage"></a><span data-ttu-id="164d0-211">Стадия</span><span class="sxs-lookup"><span data-stu-id="164d0-211">Stage</span></span>

<span data-ttu-id="164d0-212">Этап позволяет пользователям открывать объект ( например, изображение, файл или веб-сайт) в Teams вместо открытия в другом приложении или браузере.</span><span class="sxs-lookup"><span data-stu-id="164d0-212">Stage offers a way for users to open an entity—like an image, file, or website—in Teams instead of opening it in another app or browser.</span></span> <span data-ttu-id="164d0-213">Основной пример использования стадии — просмотр; поверхность не должна использоваться для сложных взаимодействий.</span><span class="sxs-lookup"><span data-stu-id="164d0-213">The primary use case of stage is viewing; the surface should not be used for complex interactions.</span></span>

<span data-ttu-id="164d0-214">(Примечание по реализации. Создание стадии с помощью модуля больших [задач.)](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)</span><span class="sxs-lookup"><span data-stu-id="164d0-214">(Implementation note: Build your stage using a large [task module](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).)</span></span>

:::image type="content" source="../../assets/images/ui-templates/stage.png" alt-text="В примере показан шаблон стадии." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="164d0-216">Лучшие случаи использования</span><span class="sxs-lookup"><span data-stu-id="164d0-216">Top use cases</span></span>

* <span data-ttu-id="164d0-217">Открытие сущности в Teams вместо другого приложения или браузера</span><span class="sxs-lookup"><span data-stu-id="164d0-217">Open an entity in Teams instead of another app or browser</span></span>
* <span data-ttu-id="164d0-218">Мультимедиа в центре внимания или другое содержимое</span><span class="sxs-lookup"><span data-stu-id="164d0-218">Spotlight media or other content</span></span>
