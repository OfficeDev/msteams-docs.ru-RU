---
title: Разработка приложения с помощью шаблонов пользовательского интерфейса
author: heath-hamilton
description: Ускоряется проектирование приложения со стандартизованными компонентами пользовательского интерфейса, макетами и шаблонами, которые обычно отображаются в Microsoft Teams.
ms.author: lajanuar
ms.topic: reference
ms.openlocfilehash: 144c18ab03d76e442a4de64a5c61af76cb2b8b5f
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/09/2020
ms.locfileid: "49606333"
---
# <a name="designing-your-microsoft-teams-app-with-ui-templates"></a><span data-ttu-id="c0700-103">Разработка приложения Microsoft Teams с помощью шаблонов пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="c0700-103">Designing your Microsoft Teams app with UI templates</span></span>

<span data-ttu-id="c0700-104">Быстрое проектирование приложения Microsoft Teams с помощью шаблонов пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="c0700-104">Design your Microsoft Teams app faster with UI templates.</span></span> <span data-ttu-id="c0700-105">Шаблоны представляют собой набор компонентов на основе пользовательского интерфейса Fluent, которые работают в стандартных случаях использования Teams, что позволяет вам больше времени для того, чтобы определить оптимальное взаимодействие с пользователями.</span><span class="sxs-lookup"><span data-stu-id="c0700-105">The templates are a collection of Fluent UI-based components that work across common Teams use cases, giving you more time to figure out the best experience for your users.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="c0700-106">Набор элементов пользовательского интерфейса Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="c0700-106">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="c0700-107">Шаблоны пользовательского интерфейса можно взять из набора UI Microsoft Teams, который также включает в себя подробные сведения об использовании, анатомии, специальных возможностях и рекомендациях.</span><span class="sxs-lookup"><span data-stu-id="c0700-107">You can grab UI templates from the Microsoft Teams UI Kit, which also includes extensive information about usage, anatomy, accessibility, and best practices.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c0700-108">Получение набора элементов пользовательского интерфейса Microsoft Teams (фигма)</span><span class="sxs-lookup"><span data-stu-id="c0700-108">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="list"></a><span data-ttu-id="c0700-109">Список</span><span class="sxs-lookup"><span data-stu-id="c0700-109">List</span></span>

<span data-ttu-id="c0700-110">Вы можете использовать список, чтобы отображать связанные элементы в формате с возможностью записи и разрешить пользователям выполнять действия для всего списка или отдельных элементов.</span><span class="sxs-lookup"><span data-stu-id="c0700-110">You can use a list to display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>

:::image type="content" source="../../assets/images/ui-templates/list.png" alt-text="Пример показывает шаблон пользовательского интерфейса списка." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="c0700-112">Основные варианты использования</span><span class="sxs-lookup"><span data-stu-id="c0700-112">Top use cases</span></span>

* <span data-ttu-id="c0700-113">Отображение данных</span><span class="sxs-lookup"><span data-stu-id="c0700-113">Display data</span></span>
* <span data-ttu-id="c0700-114">Контекстные действия для контента приложения</span><span class="sxs-lookup"><span data-stu-id="c0700-114">Contextual actions on app content</span></span>

## <a name="dashboard"></a><span data-ttu-id="c0700-115">Информационная панель</span><span class="sxs-lookup"><span data-stu-id="c0700-115">Dashboard</span></span>

<span data-ttu-id="c0700-116">Панель мониторинга отображает различные типы контента в центральном расположении (личное приложение Teams или вкладка).</span><span class="sxs-lookup"><span data-stu-id="c0700-116">A dashboard displays different types of content in a central location (Teams personal app or tab).</span></span> <span data-ttu-id="c0700-117">Пользователи должны иметь возможность настраивать по крайней мере некоторые из них на панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="c0700-117">Users should be able to customize at least some of what they see on a dashboard.</span></span>

:::image type="content" source="../../assets/images/ui-templates/dashboard.png" alt-text="Пример показывает шаблон пользовательского интерфейса панели мониторинга." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="c0700-119">Основные варианты использования</span><span class="sxs-lookup"><span data-stu-id="c0700-119">Top use cases</span></span>

* <span data-ttu-id="c0700-120">Анализ данных</span><span class="sxs-lookup"><span data-stu-id="c0700-120">Analyze data</span></span>
* <span data-ttu-id="c0700-121">Показатели отчетов</span><span class="sxs-lookup"><span data-stu-id="c0700-121">Report metrics</span></span>
* <span data-ttu-id="c0700-122">Организация разных сведений в одном месте</span><span class="sxs-lookup"><span data-stu-id="c0700-122">Organize different information in one place</span></span>

## <a name="form"></a><span data-ttu-id="c0700-123">Form</span><span class="sxs-lookup"><span data-stu-id="c0700-123">Form</span></span>

<span data-ttu-id="c0700-124">Формы используются для сбора, проверки и отсылки данных, вводимых пользователем, в структурированном виде.</span><span class="sxs-lookup"><span data-stu-id="c0700-124">Forms are used to collect, validate, and submit user input in a structured way.</span></span> <span data-ttu-id="c0700-125">Удаление меток и логических групп полей ввода является критически важным для хорошего взаимодействия с пользователем.</span><span class="sxs-lookup"><span data-stu-id="c0700-125">Clear labeling and logical groupings of input fields are critical for a good user experience.</span></span>

:::image type="content" source="../../assets/images/ui-templates/form.png" alt-text="Пример показывает шаблон пользовательского интерфейса формы." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="c0700-127">Основные варианты использования</span><span class="sxs-lookup"><span data-stu-id="c0700-127">Top use cases</span></span>

* <span data-ttu-id="c0700-128">Вход</span><span class="sxs-lookup"><span data-stu-id="c0700-128">Sign in</span></span>
* <span data-ttu-id="c0700-129">Профили пользователей</span><span class="sxs-lookup"><span data-stu-id="c0700-129">User profiles</span></span>
* <span data-ttu-id="c0700-130">Параметры</span><span class="sxs-lookup"><span data-stu-id="c0700-130">Settings</span></span>
* <span data-ttu-id="c0700-131">Коллекция вводимых пользователем данных</span><span class="sxs-lookup"><span data-stu-id="c0700-131">User input collection</span></span>

## <a name="sign-in"></a><span data-ttu-id="c0700-132">Вход</span><span class="sxs-lookup"><span data-stu-id="c0700-132">Sign in</span></span>

<span data-ttu-id="c0700-133">Вы можете проектировать потоки входа в приложение для различных контекстов команд и поставщиков удостоверений.</span><span class="sxs-lookup"><span data-stu-id="c0700-133">You can design app sign-in flows for different Teams contexts and identity providers.</span></span> <span data-ttu-id="c0700-134">В приведенном ниже примере используется единый вход (SSO), который мы рекомендуем использовать простейший способ проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="c0700-134">The following example includes single sign-on (SSO), which we recommend for the simplest authentication experience.</span></span>

:::image type="content" source="../../assets/images/ui-templates/sign-in.png" alt-text="Пример показывает шаблон пользовательского интерфейса входа." border="false":::

### <a name="top-use-case"></a><span data-ttu-id="c0700-136">Верхний вариант использования</span><span class="sxs-lookup"><span data-stu-id="c0700-136">Top use case</span></span>

* <span data-ttu-id="c0700-137">Проверка подлинности пользователей</span><span class="sxs-lookup"><span data-stu-id="c0700-137">Authenticate users</span></span>

## <a name="task-board"></a><span data-ttu-id="c0700-138">Доска задач</span><span class="sxs-lookup"><span data-stu-id="c0700-138">Task board</span></span>

<span data-ttu-id="c0700-139">Доска задач, иногда называемая доской Канбан или свим желобами, представляет собой коллекцию карточек, часто используемых для отслеживания состояния рабочих элементов или билетов.</span><span class="sxs-lookup"><span data-stu-id="c0700-139">A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span> <span data-ttu-id="c0700-140">Он также может использоваться для сортировки любого типа контента по категориям.</span><span class="sxs-lookup"><span data-stu-id="c0700-140">It can also be used to sort any type of content into categories.</span></span> <span data-ttu-id="c0700-141">Вы можете редактировать и перемещать карты между столбцами.</span><span class="sxs-lookup"><span data-stu-id="c0700-141">You can edit and move the cards between columns.</span></span>

:::image type="content" source="../../assets/images/ui-templates/task-board.png" alt-text="В примере показан шаблон пользовательского интерфейса доски задач." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="c0700-143">Основные варианты использования</span><span class="sxs-lookup"><span data-stu-id="c0700-143">Top use cases</span></span>

* <span data-ttu-id="c0700-144">управление проектами;</span><span class="sxs-lookup"><span data-stu-id="c0700-144">Project management.</span></span> <span data-ttu-id="c0700-145">Назначение задач и состояния отслеживания</span><span class="sxs-lookup"><span data-stu-id="c0700-145">Assigning tasks and tracking status</span></span>
* <span data-ttu-id="c0700-146">Мозговой штурм.</span><span class="sxs-lookup"><span data-stu-id="c0700-146">Brainstorming.</span></span> <span data-ttu-id="c0700-147">Добавление идей в разные категории</span><span class="sxs-lookup"><span data-stu-id="c0700-147">Adding ideas in different categories</span></span>
* <span data-ttu-id="c0700-148">Упражнения по сортировке.</span><span class="sxs-lookup"><span data-stu-id="c0700-148">Sorting exercises.</span></span> <span data-ttu-id="c0700-149">Организация любого вида информации в сегменты</span><span class="sxs-lookup"><span data-stu-id="c0700-149">Organizing any kind of information into buckets</span></span>

## <a name="data-visualization"></a><span data-ttu-id="c0700-150">Визуализация данных</span><span class="sxs-lookup"><span data-stu-id="c0700-150">Data visualization</span></span>

<span data-ttu-id="c0700-151">Вы можете использовать различные размеры карт (Single, Double и Full) для стеков и систематизации визуализаций данных на одной странице.</span><span class="sxs-lookup"><span data-stu-id="c0700-151">You can use different card sizes (single, double, and full) to stack and organize data visualizations on the same page.</span></span> <span data-ttu-id="c0700-152">Карты масштабируются в соответствии с разметкой столбцов и заполнение пробелами.</span><span class="sxs-lookup"><span data-stu-id="c0700-152">The cards scale to fit the column layout and fill in blank spaces.</span></span>

:::image type="content" source="../../assets/images/ui-templates/data-viz.png" alt-text="Пример показывает шаблон пользовательского интерфейса визуализации данных." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="c0700-154">Основные варианты использования</span><span class="sxs-lookup"><span data-stu-id="c0700-154">Top use cases</span></span>

* <span data-ttu-id="c0700-155">Отображение сложной информации</span><span class="sxs-lookup"><span data-stu-id="c0700-155">Display complex information</span></span>
* <span data-ttu-id="c0700-156">Создание панели мониторинга</span><span class="sxs-lookup"><span data-stu-id="c0700-156">Create a dashboard</span></span>

## <a name="wizard"></a><span data-ttu-id="c0700-157">Мастер</span><span class="sxs-lookup"><span data-stu-id="c0700-157">Wizard</span></span>

<span data-ttu-id="c0700-158">Мастер помогает пользователю выполнить задачу (например, процесс установки) с помощью нескольких экранов.</span><span class="sxs-lookup"><span data-stu-id="c0700-158">A wizard guides a user through several screens to complete a task (such as a setup process).</span></span>

:::image type="content" source="../../assets/images/ui-templates/wizard.png" alt-text="В примере показан шаблон пользовательского интерфейса мастера." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="c0700-160">Основные варианты использования</span><span class="sxs-lookup"><span data-stu-id="c0700-160">Top use cases</span></span>

* <span data-ttu-id="c0700-161">Настройка</span><span class="sxs-lookup"><span data-stu-id="c0700-161">Setup</span></span>
* <span data-ttu-id="c0700-162">Адаптация</span><span class="sxs-lookup"><span data-stu-id="c0700-162">Onboarding</span></span>
* <span data-ttu-id="c0700-163">Интерфейс первого запуска</span><span class="sxs-lookup"><span data-stu-id="c0700-163">First-run experiences</span></span>

## <a name="empty-state"></a><span data-ttu-id="c0700-164">Пустое состояние</span><span class="sxs-lookup"><span data-stu-id="c0700-164">Empty state</span></span>

<span data-ttu-id="c0700-165">Шаблон пустое состояние можно использовать для многих сценариев, в том числе входа, первого запуска, сообщений об ошибках и многого другого.</span><span class="sxs-lookup"><span data-stu-id="c0700-165">The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span> <span data-ttu-id="c0700-166">Он обладает широкими возможностями, адаптируя его к использованию одного, нескольких или всех компонентов в приведенном ниже проекте.</span><span class="sxs-lookup"><span data-stu-id="c0700-166">It’s highly flexible⁠—adapt it to use one, a few, or all of the components in the following design.</span></span>

:::image type="content" source="../../assets/images/ui-templates/empty-state.png" alt-text="В примере показан шаблон пользовательского интерфейса мастера." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="c0700-168">Основные варианты использования</span><span class="sxs-lookup"><span data-stu-id="c0700-168">Top use cases</span></span>

* <span data-ttu-id="c0700-169">Вход</span><span class="sxs-lookup"><span data-stu-id="c0700-169">Sign in</span></span>
* <span data-ttu-id="c0700-170">Приветственные сообщения и интерфейс первого запуска</span><span class="sxs-lookup"><span data-stu-id="c0700-170">Welcome messages and first-run experiences</span></span>
* <span data-ttu-id="c0700-171">Сообщения об успешном выполнении</span><span class="sxs-lookup"><span data-stu-id="c0700-171">Success messages</span></span>
* <span data-ttu-id="c0700-172">Сообщения об ошибках</span><span class="sxs-lookup"><span data-stu-id="c0700-172">Error messages</span></span>

## <a name="notification-bar"></a><span data-ttu-id="c0700-173">Панель уведомлений</span><span class="sxs-lookup"><span data-stu-id="c0700-173">Notification bar</span></span>

<span data-ttu-id="c0700-174">Панель уведомлений — это выделенная область для отображения коротких, важных сообщений, не требующих от пользователя немедленного выполнения действия.</span><span class="sxs-lookup"><span data-stu-id="c0700-174">A notification bar is a dedicated area for displaying a brief, important messages that do not require the user to take immediate action.</span></span> <span data-ttu-id="c0700-175">Определенные цвета фона и значки связаны с определенными типами сообщений (см. ниже).</span><span class="sxs-lookup"><span data-stu-id="c0700-175">Specific background colors and icons are associated with specific types of messages (see below).</span></span>

:::image type="content" source="../../assets/images/ui-templates/notification-bar.png" alt-text="Пример показывает шаблоны панели уведомлений." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="c0700-177">Основные варианты использования</span><span class="sxs-lookup"><span data-stu-id="c0700-177">Top use cases</span></span>

* <span data-ttu-id="c0700-178">Критические сообщения, ошибки и предупреждения</span><span class="sxs-lookup"><span data-stu-id="c0700-178">Critical messages, errors, and warnings</span></span>
* <span data-ttu-id="c0700-179">Сообщения об успешном выполнении</span><span class="sxs-lookup"><span data-stu-id="c0700-179">Success messages</span></span>
* <span data-ttu-id="c0700-180">Информационные или рекламные сообщения</span><span class="sxs-lookup"><span data-stu-id="c0700-180">Informational or promotional messages</span></span>

## <a name="left-nav"></a><span data-ttu-id="c0700-181">Левая панель навигации</span><span class="sxs-lookup"><span data-stu-id="c0700-181">Left nav</span></span>

<span data-ttu-id="c0700-182">Используйте левую панель навигации для просмотра нескольких страниц на вкладке Teams (команды). В следующем примере левая панель навигации находится между списком канал и содержимым Tab.</span><span class="sxs-lookup"><span data-stu-id="c0700-182">Use the left nav to browse multiple pages within your Teams tab. In the following example, the left nav is between the channel list and tab content.</span></span>

:::image type="content" source="../../assets/images/ui-templates/left-nav.png" alt-text="Пример показывает левый шаблон навигации." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="c0700-184">Основные варианты использования</span><span class="sxs-lookup"><span data-stu-id="c0700-184">Top use cases</span></span>

* <span data-ttu-id="c0700-185">Обзор нескольких страниц на вкладке "команды"</span><span class="sxs-lookup"><span data-stu-id="c0700-185">Browse multiple pages within a Teams tab</span></span>
* <span data-ttu-id="c0700-186">Разделение сложных приложений на несколько страниц</span><span class="sxs-lookup"><span data-stu-id="c0700-186">Break down complex apps into multiple pages</span></span>

## <a name="breadcrumb"></a><span data-ttu-id="c0700-187">Строка навигации</span><span class="sxs-lookup"><span data-stu-id="c0700-187">Breadcrumb</span></span>

<span data-ttu-id="c0700-188">Иерархические пути — это помощь в навигации, которая передает иерархию вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="c0700-188">Breadcrumbs are a navigational aid that convey your app’s hierarchy.</span></span> <span data-ttu-id="c0700-189">Они помогают пользователям разослаться на просматриваемую страницу в общем интерфейсе и позволить одноэлементному доступу к более высоким уровням в этой иерархии.</span><span class="sxs-lookup"><span data-stu-id="c0700-189">They help users understand how the page they’re viewing fits into the overall experience and afford one-click access to higher levels in that hierarchy.</span></span>

:::image type="content" source="../../assets/images/ui-templates/breadcrumb.png" alt-text="В примере показан пример иерархического шаблона." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="c0700-191">Основные варианты использования</span><span class="sxs-lookup"><span data-stu-id="c0700-191">Top use cases</span></span>

* <span data-ttu-id="c0700-192">Иерархия "обмен сообщениями"</span><span class="sxs-lookup"><span data-stu-id="c0700-192">Communicate hierarchy</span></span>
* <span data-ttu-id="c0700-193">Навигация</span><span class="sxs-lookup"><span data-stu-id="c0700-193">Navigation</span></span>

## <a name="toolbar"></a><span data-ttu-id="c0700-194">Панель инструментов</span><span class="sxs-lookup"><span data-stu-id="c0700-194">Toolbar</span></span>

<span data-ttu-id="c0700-195">Панель инструментов — это контейнер для группировки набора элементов управления.</span><span class="sxs-lookup"><span data-stu-id="c0700-195">A toolbar is a container for grouping a set of controls.</span></span>

:::image type="content" source="../../assets/images/ui-templates/toolbar.png" alt-text="Пример показывает шаблон панели инструментов." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="c0700-197">Основные варианты использования</span><span class="sxs-lookup"><span data-stu-id="c0700-197">Top use cases</span></span>

* <span data-ttu-id="c0700-198">Контекстные действия для контента приложения</span><span class="sxs-lookup"><span data-stu-id="c0700-198">Contextual actions on app content</span></span>
* <span data-ttu-id="c0700-199">Контекстный фильтр и поиск</span><span class="sxs-lookup"><span data-stu-id="c0700-199">Contextual filter and find</span></span>
* <span data-ttu-id="c0700-200">Навигация и иерархические строки</span><span class="sxs-lookup"><span data-stu-id="c0700-200">Navigation and breadcrumbs</span></span>

## <a name="stage"></a><span data-ttu-id="c0700-201">Этап</span><span class="sxs-lookup"><span data-stu-id="c0700-201">Stage</span></span>

<span data-ttu-id="c0700-202">Stage позволяет пользователям открывать сущности (например, изображение, файл или веб-сайт) в Teams, не открывая их в другом приложении или браузере.</span><span class="sxs-lookup"><span data-stu-id="c0700-202">Stage offers a way for users to open an entity—like an image, file, or website—in Teams instead of opening it in another app or browser.</span></span> <span data-ttu-id="c0700-203">Основным вариантом использования стадии является просмотр; поверхность не должна использоваться для сложных взаимодействий.</span><span class="sxs-lookup"><span data-stu-id="c0700-203">The primary use case of stage is viewing; the surface should not be used for complex interactions.</span></span>

<span data-ttu-id="c0700-204">(Примечание о реализации. Создание стадии с помощью большого [модуля задач](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).)</span><span class="sxs-lookup"><span data-stu-id="c0700-204">(Implementation note: Build your stage using a large [task module](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).)</span></span>

:::image type="content" source="../../assets/images/ui-templates/stage.png" alt-text="В примере показан шаблон Stage." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="c0700-206">Основные варианты использования</span><span class="sxs-lookup"><span data-stu-id="c0700-206">Top use cases</span></span>

* <span data-ttu-id="c0700-207">Открытие объекта в Teams вместо другого приложения или браузера</span><span class="sxs-lookup"><span data-stu-id="c0700-207">Open an entity in Teams instead of another app or browser</span></span>
* <span data-ttu-id="c0700-208">Важный носитель или другое содержимое</span><span class="sxs-lookup"><span data-stu-id="c0700-208">Spotlight media or other content</span></span>

## <a name="microsoft-teams-ui-library-coming-soon"></a><span data-ttu-id="c0700-209">Библиотека пользовательского интерфейса Microsoft Teams (ожидается в ближайшее время)</span><span class="sxs-lookup"><span data-stu-id="c0700-209">Microsoft Teams UI Library (coming soon)</span></span>

<span data-ttu-id="c0700-210">Библиотека пользовательского интерфейса Microsoft Teams позволит импортировать эти шаблоны готовых рабочих ИНТЕРФЕЙСов непосредственно в проект приложения.</span><span class="sxs-lookup"><span data-stu-id="c0700-210">The Microsoft Teams UI Library will allow you to import these production-ready UI templates directly into your app project.</span></span>
