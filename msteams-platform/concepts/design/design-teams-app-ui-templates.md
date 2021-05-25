---
title: Проектирование приложения с помощью шаблонов пользовательского интерфейса
author: heath-hamilton
description: Быстрее разработать приложение с помощью стандартизированных компонентов пользовательского интерфейса, макетов и шаблонов, часто Microsoft Teams.
ms.author: lajanuar
localization_priority: Normal
ms.topic: reference
ms.openlocfilehash: 5026554070396dcc55390496b6754961e8e037bc
ms.sourcegitcommit: 4224c44d169b1a289cbf1d3353de6bc6de7c7ea8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/25/2021
ms.locfileid: "52644857"
---
# <a name="designing-your-microsoft-teams-app-with-ui-templates"></a><span data-ttu-id="f2599-103">Разработка приложения Microsoft Teams с помощью шаблонов пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="f2599-103">Designing your Microsoft Teams app with UI templates</span></span>

<span data-ttu-id="f2599-104">Быстрее Microsoft Teams приложение с помощью шаблонов пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="f2599-104">Design your Microsoft Teams app faster with UI templates.</span></span> <span data-ttu-id="f2599-105">Шаблоны — это коллекция компонентов на основе пользовательского интерфейса fluent, которые работают в общих Teams случаях использования, что дает вам больше времени, чтобы выяснить, как лучше работать с пользователями.</span><span class="sxs-lookup"><span data-stu-id="f2599-105">The templates are a collection of Fluent UI-based components that work across common Teams use cases, giving you more time to figure out the best experience for your users.</span></span>

## <a name="getting-started-with-tools-and-samples"></a><span data-ttu-id="f2599-106">Начало работы с инструментами и примерами</span><span class="sxs-lookup"><span data-stu-id="f2599-106">Getting started with tools and samples</span></span>

<span data-ttu-id="f2599-107">Следующие ресурсы помогут вам разработать и разработать приложение с помощью шаблонов пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="f2599-107">The following resources can help you design and develop your app using UI templates.</span></span>

### <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="f2599-108">Комплект разработчика для пользовательского интерфейса Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="f2599-108">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="f2599-109">Захватите шаблоны пользовательского интерфейса для разработки приложения из Microsoft Teams пользовательского интерфейса, который также содержит обширные сведения об использовании, анатомии, доступности и лучших практиках.</span><span class="sxs-lookup"><span data-stu-id="f2599-109">Grab UI templates for your app design from the Microsoft Teams UI Kit, which also includes extensive information about usage, anatomy, accessibility, and best practices.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f2599-110">Получите набор пользовательского интерфейса (Figma)</span><span class="sxs-lookup"><span data-stu-id="f2599-110">Get the UI kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a><span data-ttu-id="f2599-111">Microsoft Teams Библиотека пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="f2599-111">Microsoft Teams UI Library</span></span>

<span data-ttu-id="f2599-112">Просмотр и тестирование отдельных Teams шаблонов пользовательского интерфейса и связанных компонентов в браузере.</span><span class="sxs-lookup"><span data-stu-id="f2599-112">View and test individual Teams UI templates and related components in your browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f2599-113">Попробуйте библиотеку пользовательского интерфейса (детская площадка)</span><span class="sxs-lookup"><span data-stu-id="f2599-113">Try the UI library (playground)</span></span>](https://dev-int.teams.microsoft.com/storybook/main/index.html)

<span data-ttu-id="f2599-114">Импорт этих шаблонов и связанных компонентов непосредственно в проект Teams приложения.</span><span class="sxs-lookup"><span data-stu-id="f2599-114">Import these templates and related components directly into your Teams app project.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f2599-115">Получить библиотеку пользовательского интерфейса (GitHub)</span><span class="sxs-lookup"><span data-stu-id="f2599-115">Get the UI library (GitHub)</span></span>](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a><span data-ttu-id="f2599-116">Пример приложения</span><span class="sxs-lookup"><span data-stu-id="f2599-116">Sample app</span></span>

<span data-ttu-id="f2599-117">Установите пример приложения, чтобы увидеть, как выглядят и ведут себя шаблоны пользовательского интерфейса в Teams контекстах.</span><span class="sxs-lookup"><span data-stu-id="f2599-117">Install a sample app to see how UI templates look and behave within Teams contexts.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f2599-118">Получить пример приложения (GitHub)</span><span class="sxs-lookup"><span data-stu-id="f2599-118">Get the sample app (GitHub)</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="dashboard"></a><span data-ttu-id="f2599-119">Информационная панель</span><span class="sxs-lookup"><span data-stu-id="f2599-119">Dashboard</span></span>

<span data-ttu-id="f2599-120">Панель мониторинга отображает различные типы контента в центре расположения (Teams личного приложения или вкладки).</span><span class="sxs-lookup"><span data-stu-id="f2599-120">A dashboard displays different types of content in a central location (Teams personal app or tab).</span></span> <span data-ttu-id="f2599-121">Пользователи должны иметь возможность настраивать хотя бы некоторые из того, что они видят на панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="f2599-121">Users should be able to customize at least some of what they see on a dashboard.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="f2599-122">Верхние случаи использования</span><span class="sxs-lookup"><span data-stu-id="f2599-122">Top use cases</span></span>

* <span data-ttu-id="f2599-123">Анализ данных</span><span class="sxs-lookup"><span data-stu-id="f2599-123">Analyze data</span></span>
* <span data-ttu-id="f2599-124">Показатели отчета</span><span class="sxs-lookup"><span data-stu-id="f2599-124">Report metrics</span></span>
* <span data-ttu-id="f2599-125">Организация различных сведений в одном месте</span><span class="sxs-lookup"><span data-stu-id="f2599-125">Organize different information in one place</span></span>

# <a name="desktop"></a>[<span data-ttu-id="f2599-126">Desktop</span><span class="sxs-lookup"><span data-stu-id="f2599-126">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/dashboard.png" alt-text="В примере показан шаблон пользовательского интерфейса панели мониторинга на рабочем столе." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="f2599-128">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="f2599-128">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-dashboard.png" alt-text="В примере показан шаблон пользовательского интерфейса панели мониторинга на мобильных устройствах." border="false":::

---

## <a name="data-visualization"></a><span data-ttu-id="f2599-130">Визуализация данных</span><span class="sxs-lookup"><span data-stu-id="f2599-130">Data visualization</span></span>

<span data-ttu-id="f2599-131">Для стека и организации визуализации данных на одной странице можно использовать различные размеры карт (одноместные, двойные и полные).</span><span class="sxs-lookup"><span data-stu-id="f2599-131">You can use different card sizes (single, double, and full) to stack and organize data visualizations on the same page.</span></span> <span data-ttu-id="f2599-132">Шкала карт, чтобы соответствовать макету столбца и заполнять пустые пробелы.</span><span class="sxs-lookup"><span data-stu-id="f2599-132">The cards scale to fit the column layout and fill in blank spaces.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="f2599-133">Верхние случаи использования</span><span class="sxs-lookup"><span data-stu-id="f2599-133">Top use cases</span></span>

* <span data-ttu-id="f2599-134">Отображение сложной информации</span><span class="sxs-lookup"><span data-stu-id="f2599-134">Display complex information</span></span>
* <span data-ttu-id="f2599-135">Создание панели мониторинга</span><span class="sxs-lookup"><span data-stu-id="f2599-135">Create a dashboard</span></span>

# <a name="desktop"></a>[<span data-ttu-id="f2599-136">Desktop</span><span class="sxs-lookup"><span data-stu-id="f2599-136">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/data-viz.png" alt-text="В примере показан шаблон пользовательского интерфейса визуализации данных на рабочем столе." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="f2599-138">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="f2599-138">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-data-viz.png" alt-text="В примере показан шаблон пользовательского интерфейса визуализации данных на мобильных устройствах." border="false":::

---

## <a name="empty-state"></a><span data-ttu-id="f2599-140">Пустое состояние</span><span class="sxs-lookup"><span data-stu-id="f2599-140">Empty state</span></span>

<span data-ttu-id="f2599-141">Пустой шаблон состояния можно использовать для многих сценариев, включая вход, первый запуск, сообщения об ошибках и многое другое.</span><span class="sxs-lookup"><span data-stu-id="f2599-141">The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span> <span data-ttu-id="f2599-142">Он очень гибкий и адаптируется к использованию одного, нескольких или всех компонентов в следующем дизайне.</span><span class="sxs-lookup"><span data-stu-id="f2599-142">It’s highly flexible⁠—adapt it to use one, a few, or all of the components in the following design.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="f2599-143">Верхние случаи использования</span><span class="sxs-lookup"><span data-stu-id="f2599-143">Top use cases</span></span>

* <span data-ttu-id="f2599-144">Вход</span><span class="sxs-lookup"><span data-stu-id="f2599-144">Sign in</span></span>
* <span data-ttu-id="f2599-145">Приветствие сообщений и первый запуск</span><span class="sxs-lookup"><span data-stu-id="f2599-145">Welcome messages and first-run experiences</span></span>
* <span data-ttu-id="f2599-146">Сообщения об успехе</span><span class="sxs-lookup"><span data-stu-id="f2599-146">Success messages</span></span>
* <span data-ttu-id="f2599-147">Сообщения об ошибках</span><span class="sxs-lookup"><span data-stu-id="f2599-147">Error messages</span></span>

# <a name="desktop"></a>[<span data-ttu-id="f2599-148">Desktop</span><span class="sxs-lookup"><span data-stu-id="f2599-148">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/empty-state.png" alt-text="В примере показан пустой шаблон пользовательского интерфейса состояния на рабочем столе." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="f2599-150">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="f2599-150">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-empty-state.png" alt-text="В примере показан пустой шаблон пользовательского интерфейса состояния на мобильных устройствах." border="false":::

---

## <a name="filter"></a><span data-ttu-id="f2599-152">Фильтр</span><span class="sxs-lookup"><span data-stu-id="f2599-152">Filter</span></span>

<span data-ttu-id="f2599-153">Фильтр позволяет уменьшить сведения, которые вы видите, в зависимости от выбранных критериев.</span><span class="sxs-lookup"><span data-stu-id="f2599-153">A filter allows you to reduce the information you see based on the criteria selected.</span></span> <span data-ttu-id="f2599-154">Можно включить фильтры со таблицами, списками, картами и другими компонентами, которые организуют контент.</span><span class="sxs-lookup"><span data-stu-id="f2599-154">You can include filters with tables, lists, cards, and other components that organize content.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="f2599-155">Верхние случаи использования</span><span class="sxs-lookup"><span data-stu-id="f2599-155">Top use cases</span></span>

<span data-ttu-id="f2599-156">Организация контента в:</span><span class="sxs-lookup"><span data-stu-id="f2599-156">Organizing content in:</span></span>

* <span data-ttu-id="f2599-157">Списки</span><span class="sxs-lookup"><span data-stu-id="f2599-157">Lists</span></span>
* <span data-ttu-id="f2599-158">Таблицы</span><span class="sxs-lookup"><span data-stu-id="f2599-158">Tables</span></span>
* <span data-ttu-id="f2599-159">Панели мониторинга</span><span class="sxs-lookup"><span data-stu-id="f2599-159">Dashboards</span></span>
* <span data-ttu-id="f2599-160">Визуализация данных</span><span class="sxs-lookup"><span data-stu-id="f2599-160">Data visualization</span></span>

:::image type="content" source="../../assets/images/ui-templates/filter.png" alt-text="В примере показан шаблон фильтра." border="false":::

## <a name="form"></a><span data-ttu-id="f2599-162">Form</span><span class="sxs-lookup"><span data-stu-id="f2599-162">Form</span></span>

<span data-ttu-id="f2599-163">Формы используются для сбора, проверки и отправки пользовательского ввода структурированным способом.</span><span class="sxs-lookup"><span data-stu-id="f2599-163">Forms are used to collect, validate, and submit user input in a structured way.</span></span> <span data-ttu-id="f2599-164">Четкая маркировка и логические группировки полей ввода имеют решающее значение для хорошего пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="f2599-164">Clear labeling and logical groupings of input fields are critical for a good user experience.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="f2599-165">Верхние случаи использования</span><span class="sxs-lookup"><span data-stu-id="f2599-165">Top use cases</span></span>

* <span data-ttu-id="f2599-166">Вход</span><span class="sxs-lookup"><span data-stu-id="f2599-166">Sign in</span></span>
* <span data-ttu-id="f2599-167">Профили пользователей</span><span class="sxs-lookup"><span data-stu-id="f2599-167">User profiles</span></span>
* <span data-ttu-id="f2599-168">Параметры</span><span class="sxs-lookup"><span data-stu-id="f2599-168">Settings</span></span>
* <span data-ttu-id="f2599-169">Коллекция входных данных пользователей</span><span class="sxs-lookup"><span data-stu-id="f2599-169">User input collection</span></span>

# <a name="desktop"></a>[<span data-ttu-id="f2599-170">Desktop</span><span class="sxs-lookup"><span data-stu-id="f2599-170">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/form.png" alt-text="В примере показан шаблон пользовательского интерфейса форм на рабочем столе." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="f2599-172">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="f2599-172">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-form.png" alt-text="В примере показан шаблон пользовательского интерфейса формы на мобильных устройствах." border="false":::

---

## <a name="list"></a><span data-ttu-id="f2599-174">List</span><span class="sxs-lookup"><span data-stu-id="f2599-174">List</span></span>

<span data-ttu-id="f2599-175">Вы можете использовать список для отображения связанных элементов в формате сканируемых элементов и разрешить пользователям принимать меры по всему списку или отдельным пунктам.</span><span class="sxs-lookup"><span data-stu-id="f2599-175">You can use a list to display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="f2599-176">Верхние случаи использования</span><span class="sxs-lookup"><span data-stu-id="f2599-176">Top use cases</span></span>

* <span data-ttu-id="f2599-177">Отображение данных</span><span class="sxs-lookup"><span data-stu-id="f2599-177">Display data</span></span>
* <span data-ttu-id="f2599-178">Контекстные действия в контенте приложения</span><span class="sxs-lookup"><span data-stu-id="f2599-178">Contextual actions on app content</span></span>

# <a name="desktop"></a>[<span data-ttu-id="f2599-179">Desktop</span><span class="sxs-lookup"><span data-stu-id="f2599-179">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/list.png" alt-text="В примере показан шаблон пользовательского интерфейса списка на рабочем столе." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="f2599-181">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="f2599-181">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-list.png" alt-text="В примере показан шаблон пользовательского интерфейса списка на мобильных устройствах." border="false":::

---

## <a name="sign-in"></a><span data-ttu-id="f2599-183">Вход</span><span class="sxs-lookup"><span data-stu-id="f2599-183">Sign in</span></span>

<span data-ttu-id="f2599-184">Вы можете создать потоки регистрации приложений для различных Teams контекстов и поставщиков удостоверений.</span><span class="sxs-lookup"><span data-stu-id="f2599-184">You can design app sign-in flows for different Teams contexts and identity providers.</span></span> <span data-ttu-id="f2599-185">В следующем примере содержится один вход (SSO), который мы рекомендуем для простейшей проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="f2599-185">The following example includes single sign-on (SSO), which we recommend for the simplest authentication experience.</span></span>

### <a name="top-use-case"></a><span data-ttu-id="f2599-186">Пример верхнего использования</span><span class="sxs-lookup"><span data-stu-id="f2599-186">Top use case</span></span>

* <span data-ttu-id="f2599-187">Проверка подлинности пользователей</span><span class="sxs-lookup"><span data-stu-id="f2599-187">Authenticate users</span></span>

# <a name="desktop"></a>[<span data-ttu-id="f2599-188">Desktop</span><span class="sxs-lookup"><span data-stu-id="f2599-188">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/sign-in.png" alt-text="В примере показан знак в шаблоне пользовательского интерфейса на рабочем столе." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="f2599-190">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="f2599-190">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-sign-in.png" alt-text="В примере показан знак в шаблоне пользовательского интерфейса на мобильных устройствах." border="false":::

---

## <a name="settings"></a><span data-ttu-id="f2599-192">Параметры</span><span class="sxs-lookup"><span data-stu-id="f2599-192">Settings</span></span>

<span data-ttu-id="f2599-193">Параметры экраны, на которых пользователи могут настраивать свои предпочтения с помощью приложения.</span><span class="sxs-lookup"><span data-stu-id="f2599-193">Settings screens are where users can configure their preferences with your app.</span></span> <span data-ttu-id="f2599-194">(Примечание. Параметры является контейнером для [основных компонентов пользовательского интерфейса.)](~/concepts/design/design-teams-app-basic-ui-components.md)</span><span class="sxs-lookup"><span data-stu-id="f2599-194">(Note: Settings is a container for [basic UI components](~/concepts/design/design-teams-app-basic-ui-components.md).)</span></span>

### <a name="top-use-case"></a><span data-ttu-id="f2599-195">Пример верхнего использования</span><span class="sxs-lookup"><span data-stu-id="f2599-195">Top use case</span></span>

* <span data-ttu-id="f2599-196">Управление функциями приложения</span><span class="sxs-lookup"><span data-stu-id="f2599-196">Manage app features</span></span>

:::image type="content" source="../../assets/images/ui-templates/settings.png" alt-text="В примере показан шаблон параметров." border="false":::

## <a name="task-board"></a><span data-ttu-id="f2599-198">Доска задач</span><span class="sxs-lookup"><span data-stu-id="f2599-198">Task board</span></span>

<span data-ttu-id="f2599-199">Доска задач, иногда называемая канбанской или плавательные дорожки, — это коллекция карт, часто используемых для отслеживания состояния элементов или билетов.</span><span class="sxs-lookup"><span data-stu-id="f2599-199">A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span> <span data-ttu-id="f2599-200">Он также может использоваться для сортировки любого типа контента на категории.</span><span class="sxs-lookup"><span data-stu-id="f2599-200">It can also be used to sort any type of content into categories.</span></span> <span data-ttu-id="f2599-201">Вы можете изменить и переместить карты между столбцами.</span><span class="sxs-lookup"><span data-stu-id="f2599-201">You can edit and move the cards between columns.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="f2599-202">Верхние случаи использования</span><span class="sxs-lookup"><span data-stu-id="f2599-202">Top use cases</span></span>

* <span data-ttu-id="f2599-203">управление проектами;</span><span class="sxs-lookup"><span data-stu-id="f2599-203">Project management.</span></span> <span data-ttu-id="f2599-204">Назначение задач и состояние отслеживания</span><span class="sxs-lookup"><span data-stu-id="f2599-204">Assigning tasks and tracking status</span></span>
* <span data-ttu-id="f2599-205">Мозговой штурм.</span><span class="sxs-lookup"><span data-stu-id="f2599-205">Brainstorming.</span></span> <span data-ttu-id="f2599-206">Добавление идей в различных категориях</span><span class="sxs-lookup"><span data-stu-id="f2599-206">Adding ideas in different categories</span></span>
* <span data-ttu-id="f2599-207">Упражнения сортировки.</span><span class="sxs-lookup"><span data-stu-id="f2599-207">Sorting exercises.</span></span> <span data-ttu-id="f2599-208">Организация любых сведений в ведра</span><span class="sxs-lookup"><span data-stu-id="f2599-208">Organizing any kind of information into buckets</span></span>

# <a name="desktop"></a>[<span data-ttu-id="f2599-209">Desktop</span><span class="sxs-lookup"><span data-stu-id="f2599-209">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/task-board.png" alt-text="В примере показан шаблон пользовательского интерфейса доски задач на рабочем столе." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="f2599-211">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="f2599-211">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-task-board.png" alt-text="В примере показан шаблон пользовательского интерфейса доски задач на мобильных устройствах." border="false":::

---

## <a name="wizard"></a><span data-ttu-id="f2599-213">Мастер</span><span class="sxs-lookup"><span data-stu-id="f2599-213">Wizard</span></span>

<span data-ttu-id="f2599-214">Мастер направляет пользователя на несколько экранов для выполнения задачи (например, процесса настройки).</span><span class="sxs-lookup"><span data-stu-id="f2599-214">A wizard guides a user through several screens to complete a task (such as a setup process).</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="f2599-215">Верхние случаи использования</span><span class="sxs-lookup"><span data-stu-id="f2599-215">Top use cases</span></span>

* <span data-ttu-id="f2599-216">Настройка</span><span class="sxs-lookup"><span data-stu-id="f2599-216">Setup</span></span>
* <span data-ttu-id="f2599-217">Адаптация</span><span class="sxs-lookup"><span data-stu-id="f2599-217">Onboarding</span></span>
* <span data-ttu-id="f2599-218">Первый запуск</span><span class="sxs-lookup"><span data-stu-id="f2599-218">First-run experiences</span></span>

# <a name="desktop"></a>[<span data-ttu-id="f2599-219">Desktop</span><span class="sxs-lookup"><span data-stu-id="f2599-219">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/wizard.png" alt-text="В примере показан шаблон пользовательского интерфейса мастера на рабочем столе." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="f2599-221">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="f2599-221">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-wizard.png" alt-text="В примере показан шаблон пользовательского интерфейса мастера на мобильных устройствах." border="false":::

---
