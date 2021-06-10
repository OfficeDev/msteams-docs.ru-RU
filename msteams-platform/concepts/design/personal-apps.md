---
title: Проектирование личного приложения
description: Узнайте, как создать Teams и получить Microsoft Teams пользовательского интерфейса.
author: heath-hamilton
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 83fad746d71dd196f6efa6526f5c6c28ceac9e20
ms.sourcegitcommit: 4224c44d169b1a289cbf1d3353de6bc6de7c7ea8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/25/2021
ms.locfileid: "52644897"
---
# <a name="designing-your-personal-app-for-microsoft-teams"></a><span data-ttu-id="724ff-103">Разработка личного приложения для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="724ff-103">Designing your personal app for Microsoft Teams</span></span>

<span data-ttu-id="724ff-104">Персональным приложением может быть бот, частное рабочее пространство или и то, и другое.</span><span class="sxs-lookup"><span data-stu-id="724ff-104">A personal app can be a bot, private workspace, or both.</span></span> <span data-ttu-id="724ff-105">Иногда он функционирует как место для создания или просмотра контента, в других случаях он предлагает пользователю вид с высоты птичьего полета на все, что у них, когда приложение было настроено как вкладка в нескольких каналах.</span><span class="sxs-lookup"><span data-stu-id="724ff-105">Sometimes it functions like a place to create or view content, other times it offers the user a bird’s eye view of everything that's theirs when the app has been configured as a tab in multiple channels.</span></span>

<span data-ttu-id="724ff-106">Для руководства разработкой приложения в следующих сведениях описывается и иллюстрируется, как люди могут добавлять, использовать и управлять личными приложениями в Teams.</span><span class="sxs-lookup"><span data-stu-id="724ff-106">To guide your app design, the following information describes and illustrates how people can add, use, and manage personal apps in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="724ff-107">Комплект разработчика для пользовательского интерфейса Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="724ff-107">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="724ff-108">В наборе пользовательского интерфейса можно найти исчерпывающие рекомендации по разработке персональных приложений Microsoft Teams, в том числе элементы, которые можно захватить и изменить по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="724ff-108">You can find comprehensive personal app design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="724ff-109">Набор пользовательского интерфейса также имеет важные темы, такие как доступность и размер отзывчивый, которые здесь не охватываются.</span><span class="sxs-lookup"><span data-stu-id="724ff-109">The UI kit also has essential topics such as accessibility and responsive sizing that aren't covered here.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="724ff-110">Получить комплект разработчика для пользовательского интерфейса Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="724ff-110">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-personal-app"></a><span data-ttu-id="724ff-111">Добавление личного приложения</span><span class="sxs-lookup"><span data-stu-id="724ff-111">Add a personal app</span></span>

<span data-ttu-id="724ff-112">Вы можете добавить личное приложение из Teams магазина (AppSource) или вылет  приложения, выбрав значок More слева от Teams (показано в следующем примере).</span><span class="sxs-lookup"><span data-stu-id="724ff-112">You can add a personal app from the Teams store (AppSource) or the app flyout by selecting the **More** icon on the left side of Teams (shown in the following example).</span></span>

:::image type="content" source="../../assets/images/personal-apps/add-from-app-flyout.png" alt-text="В примере показано, как добавить личное приложение из вылета приложения." border="false":::

## <a name="use-a-personal-app-private-workspace"></a><span data-ttu-id="724ff-114">Использование личного приложения (личное рабочее пространство)</span><span class="sxs-lookup"><span data-stu-id="724ff-114">Use a personal app (private workspace)</span></span>

<span data-ttu-id="724ff-115">С помощью частного рабочего пространства вы можете просматривать содержимое приложения, содержательное для вас в центре, не Teams.</span><span class="sxs-lookup"><span data-stu-id="724ff-115">With a private workspace, you can view app content that's meaningful to you in a central location without leaving Teams.</span></span>

<span data-ttu-id="724ff-116">(Примечание реализации. Личное рабочее пространство основано на возможностях [*личной*](../../build-your-first-app/build-personal-tab.md) вкладки.)</span><span class="sxs-lookup"><span data-stu-id="724ff-116">(Implementation note: The private workspace is based on the [*personal tab*](../../build-your-first-app/build-personal-tab.md) capability.)</span></span>

### <a name="anatomy-personal-app-private-workspace"></a><span data-ttu-id="724ff-117">Анатомия: Личное приложение (личное рабочее пространство)</span><span class="sxs-lookup"><span data-stu-id="724ff-117">Anatomy: Personal app (private workspace)</span></span>

# <a name="desktop"></a>[<span data-ttu-id="724ff-118">Desktop</span><span class="sxs-lookup"><span data-stu-id="724ff-118">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/personal-apps/personal-tab-component-anatomy.png" alt-text="В примере показана анатомия компонентов личной вкладки." border="false":::

|<span data-ttu-id="724ff-120">Счетчик</span><span class="sxs-lookup"><span data-stu-id="724ff-120">Counter</span></span>|<span data-ttu-id="724ff-121">Описание</span><span class="sxs-lookup"><span data-stu-id="724ff-121">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="724ff-122">A</span><span class="sxs-lookup"><span data-stu-id="724ff-122">A</span></span>|<span data-ttu-id="724ff-123">**Присвоение приложения:** логотип и имя приложения.</span><span class="sxs-lookup"><span data-stu-id="724ff-123">**App attribution**: Your app logo and name.</span></span>|
|<span data-ttu-id="724ff-124">B</span><span class="sxs-lookup"><span data-stu-id="724ff-124">B</span></span>|<span data-ttu-id="724ff-125">**Вкладки.** Обеспечивает навигацию для личного приложения.</span><span class="sxs-lookup"><span data-stu-id="724ff-125">**Tabs**: Provides navigation for your personal app.</span></span>|
|<span data-ttu-id="724ff-126">C</span><span class="sxs-lookup"><span data-stu-id="724ff-126">C</span></span>|<span data-ttu-id="724ff-127">**Представление всплывающих** окон: отодвигает содержимое приложения из родительского окна в автономный детский окне.</span><span class="sxs-lookup"><span data-stu-id="724ff-127">**Popout view**: Pushes your app content from a parent window to a standalone child window.</span></span>|
|<span data-ttu-id="724ff-128">D</span><span class="sxs-lookup"><span data-stu-id="724ff-128">D</span></span>|<span data-ttu-id="724ff-129">**Дополнительные меню.** Включает дополнительные параметры приложения и сведения.</span><span class="sxs-lookup"><span data-stu-id="724ff-129">**More menu**: Includes additional app options and information.</span></span> <span data-ttu-id="724ff-130">(Можно также сделать **Параметры** вкладку.)</span><span class="sxs-lookup"><span data-stu-id="724ff-130">(You could alternatively make **Settings** a tab.)</span></span>|

:::image type="content" source="../../assets/images/personal-apps/personal-tab-structural-anatomy.png" alt-text="В примере показана структурная анатомия личной вкладки." border="false":::

|<span data-ttu-id="724ff-132">Счетчик</span><span class="sxs-lookup"><span data-stu-id="724ff-132">Counter</span></span>|<span data-ttu-id="724ff-133">Описание</span><span class="sxs-lookup"><span data-stu-id="724ff-133">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="724ff-134">A</span><span class="sxs-lookup"><span data-stu-id="724ff-134">A</span></span>|<span data-ttu-id="724ff-135">**Вкладки.** Обеспечивает навигацию для личного приложения.</span><span class="sxs-lookup"><span data-stu-id="724ff-135">**Tabs**: Provides navigation for your personal app.</span></span>|
|<span data-ttu-id="724ff-136">1</span><span class="sxs-lookup"><span data-stu-id="724ff-136">1</span></span>|<span data-ttu-id="724ff-137">**iframe:** отображает содержимое приложения.</span><span class="sxs-lookup"><span data-stu-id="724ff-137">**iframe**: Displays your app content.</span></span>|

# <a name="mobile"></a>[<span data-ttu-id="724ff-138">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="724ff-138">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/personal-apps/mobile-personal-tab-component-anatomy.png" alt-text="В примере показана анатомия компонентов личной вкладки." border="false":::

|<span data-ttu-id="724ff-140">Счетчик</span><span class="sxs-lookup"><span data-stu-id="724ff-140">Counter</span></span>|<span data-ttu-id="724ff-141">Описание</span><span class="sxs-lookup"><span data-stu-id="724ff-141">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="724ff-142">A</span><span class="sxs-lookup"><span data-stu-id="724ff-142">A</span></span>|<span data-ttu-id="724ff-143">**Присвоение приложения:** имя приложения.</span><span class="sxs-lookup"><span data-stu-id="724ff-143">**App attribution**: Your app name.</span></span>|
|<span data-ttu-id="724ff-144">B</span><span class="sxs-lookup"><span data-stu-id="724ff-144">B</span></span>|<span data-ttu-id="724ff-145">**Вкладки.** Обеспечивает навигацию для личного приложения.</span><span class="sxs-lookup"><span data-stu-id="724ff-145">**Tabs**: Provides navigation for your personal app.</span></span>|
|<span data-ttu-id="724ff-146">C</span><span class="sxs-lookup"><span data-stu-id="724ff-146">C</span></span>|<span data-ttu-id="724ff-147">**Дополнительные меню.** Включает дополнительные параметры приложения и сведения.</span><span class="sxs-lookup"><span data-stu-id="724ff-147">**More menu**: Includes additional app options and information.</span></span>|
|<span data-ttu-id="724ff-148">D</span><span class="sxs-lookup"><span data-stu-id="724ff-148">D</span></span>|<span data-ttu-id="724ff-149">**Основная навигация.** Обеспечивает навигацию для приложения другими основными Teams функциями.</span><span class="sxs-lookup"><span data-stu-id="724ff-149">**Primary navigation**: Provides navigation to your app other main Teams features.</span></span>|

:::image type="content" source="../../assets/images/personal-apps/mobile-personal-tab-structural-anatomy.png" alt-text="В примере показана структурная анатомия личной вкладки." border="false":::

|<span data-ttu-id="724ff-151">Счетчик</span><span class="sxs-lookup"><span data-stu-id="724ff-151">Counter</span></span>|<span data-ttu-id="724ff-152">Описание</span><span class="sxs-lookup"><span data-stu-id="724ff-152">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="724ff-153">A</span><span class="sxs-lookup"><span data-stu-id="724ff-153">A</span></span>|<span data-ttu-id="724ff-154">**Вкладки.** Обеспечивает навигацию для личного приложения.</span><span class="sxs-lookup"><span data-stu-id="724ff-154">**Tabs**: Provides navigation for your personal app.</span></span>|
|<span data-ttu-id="724ff-155">1</span><span class="sxs-lookup"><span data-stu-id="724ff-155">1</span></span>|<span data-ttu-id="724ff-156">**веб-просмотр.** Отображает содержимое приложения.</span><span class="sxs-lookup"><span data-stu-id="724ff-156">**webview**: Displays your app content.</span></span>|

---

### <a name="designing-with-ui-templates-and-advanced-components"></a><span data-ttu-id="724ff-157">Проектирование с помощью шаблонов пользовательского интерфейса и расширенных компонентов</span><span class="sxs-lookup"><span data-stu-id="724ff-157">Designing with UI templates and advanced components</span></span>

<span data-ttu-id="724ff-158">Используйте один из следующих Teams и компонентов для разработки личной вкладки:</span><span class="sxs-lookup"><span data-stu-id="724ff-158">Use one of the following Teams templates and components to help design your personal tab:</span></span>

* <span data-ttu-id="724ff-159">[Список.](../../concepts/design/design-teams-app-ui-templates.md#list)Списки могут отображать связанные элементы в сканируемых форматах и позволяют пользователям принимать меры по всему списку или отдельным пунктам.</span><span class="sxs-lookup"><span data-stu-id="724ff-159">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="724ff-160">[Доска](../../concepts/design/design-teams-app-ui-templates.md#task-board)задач. Доска задач, иногда называемая канбанской или плавательные дорожки, — это коллекция карт, часто используемых для отслеживания состояния элементов или билетов.</span><span class="sxs-lookup"><span data-stu-id="724ff-160">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="724ff-161">[Панель](../../concepts/design/design-teams-app-ui-templates.md#dashboard)мониторинга: панель мониторинга — это холст, содержащий несколько карт, которые предоставляют обзор данных или контента.</span><span class="sxs-lookup"><span data-stu-id="724ff-161">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="724ff-162">[Form:](../../concepts/design/design-teams-app-ui-templates.md#form)Forms are for collecting, validating and submitting user input in a structured way.</span><span class="sxs-lookup"><span data-stu-id="724ff-162">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="724ff-163">[Пустое](../../concepts/design/design-teams-app-ui-templates.md#empty-state)состояние. Пустой шаблон состояния можно использовать для многих сценариев, включая вход, первый запуск, сообщения об ошибках и многое другое.</span><span class="sxs-lookup"><span data-stu-id="724ff-163">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="724ff-164">[Левый nav:](~/concepts/design/design-teams-app-advanced-ui-components.md#left-nav)компонент левого nav может помочь, если ваше личное приложение требует некоторой навигации.</span><span class="sxs-lookup"><span data-stu-id="724ff-164">[Left nav](~/concepts/design/design-teams-app-advanced-ui-components.md#left-nav): The left nav component can help if your personal app requires some navigation.</span></span> <span data-ttu-id="724ff-165">В общем, необходимо сохранить навигацию до минимума.</span><span class="sxs-lookup"><span data-stu-id="724ff-165">In general, you should keep navigation to a minimum.</span></span>

## <a name="use-a-personal-app-bot"></a><span data-ttu-id="724ff-166">Использование личного приложения (бота)</span><span class="sxs-lookup"><span data-stu-id="724ff-166">Use a personal app (bot)</span></span>

<span data-ttu-id="724ff-167">Личные приложения могут включать бот для индивидуальных бесед и частных уведомлений (например, когда коллега публикует комментарий на вашей доске).</span><span class="sxs-lookup"><span data-stu-id="724ff-167">Personal apps can include a bot for one-on-one conversations and private notifications (for instance, when a colleague posts a comment on your artboard).</span></span> <span data-ttu-id="724ff-168">Бот доступен на указанной вкладке.</span><span class="sxs-lookup"><span data-stu-id="724ff-168">The bot is available in a tab you specify.</span></span>

### <a name="anatomy-personal-app-bot"></a><span data-ttu-id="724ff-169">Анатомия: личное приложение (бот)</span><span class="sxs-lookup"><span data-stu-id="724ff-169">Anatomy: Personal app (bot)</span></span>

# <a name="desktop"></a>[<span data-ttu-id="724ff-170">Desktop</span><span class="sxs-lookup"><span data-stu-id="724ff-170">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/personal-apps/personal-bot-anatomy.png" alt-text="В примере показана анатомия компонентов персональных ботов." border="false":::

|<span data-ttu-id="724ff-172">Счетчик</span><span class="sxs-lookup"><span data-stu-id="724ff-172">Counter</span></span>|<span data-ttu-id="724ff-173">Описание</span><span class="sxs-lookup"><span data-stu-id="724ff-173">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="724ff-174">A</span><span class="sxs-lookup"><span data-stu-id="724ff-174">A</span></span>|<span data-ttu-id="724ff-175">**Вкладка Бот.** Например, включаем вкладку **Chat** для доступа к беседам и уведомлениям ботов.</span><span class="sxs-lookup"><span data-stu-id="724ff-175">**Bot tab**: For example, include a **Chat** tab to access bot conversations and notifications.</span></span>|
|<span data-ttu-id="724ff-176">B</span><span class="sxs-lookup"><span data-stu-id="724ff-176">B</span></span>|<span data-ttu-id="724ff-177">**Сообщение бота.** Боты часто отправляют сообщения и уведомления в виде карты (например, адаптивной карты).</span><span class="sxs-lookup"><span data-stu-id="724ff-177">**Bot message**: Bots often send messages and notifications in the form of a card (such as an Adaptive Card).</span></span>|
|<span data-ttu-id="724ff-178">C</span><span class="sxs-lookup"><span data-stu-id="724ff-178">C</span></span>|<span data-ttu-id="724ff-179">**Compose box**: Вводное поле для отправки сообщений боту.</span><span class="sxs-lookup"><span data-stu-id="724ff-179">**Compose box**: Input field for sending messages to the bot.</span></span>|

# <a name="mobile"></a>[<span data-ttu-id="724ff-180">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="724ff-180">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/personal-apps/mobile-personal-bot-anatomy.png" alt-text="В примере показана анатомия компонентов персональных ботов." border="false":::

|<span data-ttu-id="724ff-182">Счетчик</span><span class="sxs-lookup"><span data-stu-id="724ff-182">Counter</span></span>|<span data-ttu-id="724ff-183">Описание</span><span class="sxs-lookup"><span data-stu-id="724ff-183">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="724ff-184">A</span><span class="sxs-lookup"><span data-stu-id="724ff-184">A</span></span>|<span data-ttu-id="724ff-185">**Точка входа бота.** Точка входа для доступа пользователей к функции бота в личном приложении.</span><span class="sxs-lookup"><span data-stu-id="724ff-185">**Bot entry point**: Entry point for users to access the bot feature in your personal app.</span></span>|
|<span data-ttu-id="724ff-186">B</span><span class="sxs-lookup"><span data-stu-id="724ff-186">B</span></span>|<span data-ttu-id="724ff-187">**Кнопка**"Назад": возвращает пользователей в личное рабочее пространство.</span><span class="sxs-lookup"><span data-stu-id="724ff-187">**Back button**: Takes users back to the private workspace.</span></span>|
|<span data-ttu-id="724ff-188">C</span><span class="sxs-lookup"><span data-stu-id="724ff-188">C</span></span>|<span data-ttu-id="724ff-189">**Сообщение бота.** Боты часто отправляют сообщения и уведомления в виде карты (например, адаптивной карты).</span><span class="sxs-lookup"><span data-stu-id="724ff-189">**Bot message**: Bots often send messages and notifications in the form of a card (such as an Adaptive Card).</span></span>|
|<span data-ttu-id="724ff-190">D</span><span class="sxs-lookup"><span data-stu-id="724ff-190">D</span></span>|<span data-ttu-id="724ff-191">**Compose box**: Вводное поле для отправки сообщений боту.</span><span class="sxs-lookup"><span data-stu-id="724ff-191">**Compose box**: Input field for sending messages to the bot.</span></span>|

---

## <a name="manage-a-personal-tab"></a><span data-ttu-id="724ff-192">Управление личной вкладке</span><span class="sxs-lookup"><span data-stu-id="724ff-192">Manage a personal tab</span></span>

<span data-ttu-id="724ff-193">На левой стороне Teams пользователи могут правой кнопкой мыши личного приложения, чтобы закрепить, удалить и настроить другие параметры приложения.</span><span class="sxs-lookup"><span data-stu-id="724ff-193">On the left side of Teams, users can right click the personal app to pin, remove, and configure other app options.</span></span>

:::image type="content" source="../../assets/images/personal-apps/manage-personal-tab.png" alt-text="В примере показаны параметры управления личным приложением." border="false":::

## <a name="best-practices"></a><span data-ttu-id="724ff-195">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="724ff-195">Best practices</span></span>

<span data-ttu-id="724ff-196">Используйте эти рекомендации для создания качественного приложения.</span><span class="sxs-lookup"><span data-stu-id="724ff-196">Use these recommendations to create a quality app experience.</span></span>

### <a name="tab-priority"></a><span data-ttu-id="724ff-197">Приоритет tab</span><span class="sxs-lookup"><span data-stu-id="724ff-197">Tab priority</span></span>

#### <a name="do-show-the-most-relevant-content-in-the-first-tab"></a><span data-ttu-id="724ff-198">Do: Показать наиболее релевантный контент на первой вкладке</span><span class="sxs-lookup"><span data-stu-id="724ff-198">Do: Show the most relevant content in the first tab</span></span>

<span data-ttu-id="724ff-199">При гибком размере вкладки справа могут быть усечены или невещены.</span><span class="sxs-lookup"><span data-stu-id="724ff-199">With responsive sizing, tabs on the right may become truncated or out of view.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-do.png" alt-text="В примере показано, как личное приложение отображает наиболее релевантный контент на первой вкладке." border="false":::

#### <a name="dont-lead-with-secondary-content-or-metadata"></a><span data-ttu-id="724ff-201">Не: руководство со вторичным контентом или метаданными</span><span class="sxs-lookup"><span data-stu-id="724ff-201">Don’t: Lead with secondary content or metadata</span></span>

<span data-ttu-id="724ff-202">Как и стандартное веб-приложение, навигация вкладок должна развиваться в порядке, который помогает понять основные функции приложения.</span><span class="sxs-lookup"><span data-stu-id="724ff-202">Like a standard web app, tab navigation should progress in an order that helps make sense of your app’s primary features.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-dont.png" alt-text="В примере показано личное приложение, ведущее со вторичным контентом или метаданными." border="false":::

### <a name="tab-hierarchy"></a><span data-ttu-id="724ff-204">Иерархия вкладок</span><span class="sxs-lookup"><span data-stu-id="724ff-204">Tab hierarchy</span></span>

#### <a name="do-tabs-should-be-of-equal-hierarchy-and-represent-key-app-pages"></a><span data-ttu-id="724ff-205">Do: Tabs should be of equal hierarchy and represent key app pages</span><span class="sxs-lookup"><span data-stu-id="724ff-205">Do: Tabs should be of equal hierarchy and represent key app pages</span></span>

<span data-ttu-id="724ff-206">Ваши вкладки должны классифицировать основные функции и содержимое приложения.</span><span class="sxs-lookup"><span data-stu-id="724ff-206">Your tabs should categorize your app’s primary features and content.</span></span> <span data-ttu-id="724ff-207">При гибком размере содержимое справа может стать усеченным или невыясненным.</span><span class="sxs-lookup"><span data-stu-id="724ff-207">With responsive sizing, content on the right may become truncated or out of view.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-do.png" alt-text="В примере показано личное приложение с вкладками равной иерархии." border="false":::

#### <a name="dont-include-different-levels-of-hierarchy"></a><span data-ttu-id="724ff-209">Не: включайте различные уровни иерархии</span><span class="sxs-lookup"><span data-stu-id="724ff-209">Don't: Include different levels of hierarchy</span></span>

<span data-ttu-id="724ff-210">Ваше содержимое должно развиваться в логическом порядке, что помогает пользователям понять его.</span><span class="sxs-lookup"><span data-stu-id="724ff-210">Your content should progress in a logical order that helps users make sense of it.</span></span> <span data-ttu-id="724ff-211">Если у вас есть две вкладки, которые тесно связаны, рассмотрите возможность их объединения в одну вкладку.</span><span class="sxs-lookup"><span data-stu-id="724ff-211">If you have two tabs that are closely related, consider combining them into one tab.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-dont.png" alt-text="В примере показано личное приложение с различными уровнями иерархии." border="false":::

### <a name="first-run-experience"></a><span data-ttu-id="724ff-213">Интерфейс при первом запуске</span><span class="sxs-lookup"><span data-stu-id="724ff-213">First-run experience</span></span>

#### <a name="do-include-a-first-run-experience"></a><span data-ttu-id="724ff-214">Do: Включите первый запуск</span><span class="sxs-lookup"><span data-stu-id="724ff-214">Do: Include a first-run experience</span></span>

<span data-ttu-id="724ff-215">При первом использовании личного приложения должен быть по крайней мере приветственный экран.</span><span class="sxs-lookup"><span data-stu-id="724ff-215">There should be at least a welcome screen the first time you use a personal app.</span></span> <span data-ttu-id="724ff-216">Для ботов опишите, что может сделать ваш бот, и предопишите быстрые действия, например кнопку вход.</span><span class="sxs-lookup"><span data-stu-id="724ff-216">For bots, describe what your bot can do and provide quick actions, such as a sign-in button.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-do.png" alt-text="В примере показано, что нужно делать во время личного опыта запуска приложения." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-fre-do.png" alt-text="В другом примере показано, что нужно делать во время работы с личным приложением в первом запуске." border="false":::

#### <a name="dont-start-with-a-blank-screen"></a><span data-ttu-id="724ff-219">Не: начните с пустого экрана</span><span class="sxs-lookup"><span data-stu-id="724ff-219">Don't: Start with a blank screen</span></span>

<span data-ttu-id="724ff-220">Пользователи могут быть сбиты с толку, если при первом запуске приложения ничего не отображается.</span><span class="sxs-lookup"><span data-stu-id="724ff-220">Users might be confused if nothing displays the first time they run your app.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-dont.png" alt-text="В примере показано, что не нужно делать во время первого запуска личного приложения." border="false":::

### <a name="personalized-content"></a><span data-ttu-id="724ff-222">Персонализированный контент</span><span class="sxs-lookup"><span data-stu-id="724ff-222">Personalized content</span></span>

#### <a name="do-aggregate-app-content-relevant-to-a-user"></a><span data-ttu-id="724ff-223">Do: Совокупный контент приложения, релевантный пользователю</span><span class="sxs-lookup"><span data-stu-id="724ff-223">Do: Aggregate app content relevant to a user</span></span>

<span data-ttu-id="724ff-224">Будь то личная вкладка или бот, отображайте содержимое, связанное только с действиями пользователя в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="724ff-224">Whether it's a personal tab or bot, display content related to only a user's activity in your app.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-do.png" alt-text="В примере показано, что делать с личным приложением и персонализированным контентом." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-do.png" alt-text="Другой пример показывает, что делать с личным приложением и персонализированным контентом." border="false":::

#### <a name="dont-show-unrelated-or-overly-broad-content"></a><span data-ttu-id="724ff-227">Не: показывать несвязанные или чрезмерно широкий контент</span><span class="sxs-lookup"><span data-stu-id="724ff-227">Don’t: Show unrelated or overly broad content</span></span>

<span data-ttu-id="724ff-228">В личных контекстах не отображайте контент для групп, в которые пользователь не входит.</span><span class="sxs-lookup"><span data-stu-id="724ff-228">In personal contexts, don’t display content for teams a user isn't part of.</span></span> <span data-ttu-id="724ff-229">Личное содержимое бота должно фокусироваться на личности, а не на группе.</span><span class="sxs-lookup"><span data-stu-id="724ff-229">Personal bot content should focus on the individual—not a group.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-dont.png" alt-text="В примере показано, что не нужно делать с личным приложением и персонализированным контентом." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-dont.png" alt-text="Другой пример показывает, что не нужно делать с личным приложением и персонализированным контентом." border="false":::

### <a name="complex-app-features"></a><span data-ttu-id="724ff-232">Сложные функции приложения</span><span class="sxs-lookup"><span data-stu-id="724ff-232">Complex app features</span></span>

#### <a name="do-allow-users-to-access-complex-features-in-a-browser"></a><span data-ttu-id="724ff-233">Do: Разрешить пользователям доступ к сложным функциям в браузере</span><span class="sxs-lookup"><span data-stu-id="724ff-233">Do: Allow users to access complex features in a browser</span></span>

<span data-ttu-id="724ff-234">Ваше приложение должно сосредоточиться на основных задачах в Teams, но вы все равно можете просматривать полное, автономные приложения в браузере.</span><span class="sxs-lookup"><span data-stu-id="724ff-234">Your app should focus on core tasks in Teams, but you can still view the full, standalone app in a browser.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-do.png" alt-text="В примере показано, как обрабатывать сложные функции приложения с помощью личного приложения." border="false":::

#### <a name="dont-include-your-entire-app"></a><span data-ttu-id="724ff-236">Не: включите все приложение</span><span class="sxs-lookup"><span data-stu-id="724ff-236">Don’t: Include your entire app</span></span>

<span data-ttu-id="724ff-237">Если вы не создали приложение специально для Teams, возможно, у вас есть функции, которые не имеют смысла в средстве совместной работы.</span><span class="sxs-lookup"><span data-stu-id="724ff-237">Unless you created your app specifically for Teams, you probably have features that don’t make sense in a collaboration tool.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-dont.png" alt-text="В примере показано, как не обрабатывать сложные функции приложения с помощью личного приложения." border="false":::

## <a name="see-also"></a><span data-ttu-id="724ff-239">См. также</span><span class="sxs-lookup"><span data-stu-id="724ff-239">See also</span></span>

<span data-ttu-id="724ff-240">Эти другие рекомендации по проектированию могут помочь в зависимости от области вашего личного приложения:</span><span class="sxs-lookup"><span data-stu-id="724ff-240">These other design guidelines may help depending on the scope of your personal app:</span></span>

* [<span data-ttu-id="724ff-241">Проектирование вкладки</span><span class="sxs-lookup"><span data-stu-id="724ff-241">Designing your tab</span></span>](../../tabs/design/tabs.md)
* [<span data-ttu-id="724ff-242">Проектирование бота</span><span class="sxs-lookup"><span data-stu-id="724ff-242">Designing you bot</span></span>](../../bots/design/bots.md)
