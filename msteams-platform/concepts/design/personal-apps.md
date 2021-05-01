---
title: Проектирование личного приложения
description: Узнайте, как создать Teams и получить Microsoft Teams пользовательского интерфейса.
author: heath-hamilton
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: b3f08c39a7900b80fb46d167fae8d9e8bdbcc574
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101557"
---
# <a name="designing-your-personal-app-for-microsoft-teams"></a><span data-ttu-id="a8f71-103">Разработка личного приложения для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="a8f71-103">Designing your personal app for Microsoft Teams</span></span>

<span data-ttu-id="a8f71-104">Персональным приложением может быть бот, частное рабочее пространство или и то, и другое.</span><span class="sxs-lookup"><span data-stu-id="a8f71-104">A personal app can be a bot, private workspace, or both.</span></span> <span data-ttu-id="a8f71-105">Иногда он функционирует как место для создания или просмотра контента, в других случаях он предлагает пользователю вид с высоты птичьего полета на все, что у них, когда приложение было настроено как вкладка в нескольких каналах.</span><span class="sxs-lookup"><span data-stu-id="a8f71-105">Sometimes it functions like a place to create or view content, other times it offers the user a bird’s eye view of everything that's theirs when the app has been configured as a tab in multiple channels.</span></span>

<span data-ttu-id="a8f71-106">Для руководства разработкой приложения в следующих сведениях описывается и иллюстрируется, как люди могут добавлять, использовать и управлять личными приложениями в Teams.</span><span class="sxs-lookup"><span data-stu-id="a8f71-106">To guide your app design, the following information describes and illustrates how people can add, use, and manage personal apps in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="a8f71-107">Комплект разработчика для пользовательского интерфейса Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="a8f71-107">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="a8f71-108">В наборе пользовательского интерфейса можно найти исчерпывающие рекомендации по разработке персональных приложений Microsoft Teams, в том числе элементы, которые можно захватить и изменить по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="a8f71-108">You can find comprehensive personal app design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="a8f71-109">Набор пользовательского интерфейса также имеет важные темы, такие как доступность и размер отзывчивый, которые здесь не охватываются.</span><span class="sxs-lookup"><span data-stu-id="a8f71-109">The UI kit also has essential topics such as accessibility and responsive sizing that aren't covered here.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a8f71-110">Получить комплект разработчика для пользовательского интерфейса Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="a8f71-110">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-personal-app"></a><span data-ttu-id="a8f71-111">Добавление личного приложения</span><span class="sxs-lookup"><span data-stu-id="a8f71-111">Add a personal app</span></span>

<span data-ttu-id="a8f71-112">Вы можете добавить личное приложение из Teams магазина (AppSource) или вылет  приложения, выбрав значок More слева от Teams (показано в следующем примере).</span><span class="sxs-lookup"><span data-stu-id="a8f71-112">You can add a personal app from the Teams store (AppSource) or the app flyout by selecting the **More** icon on the left side of Teams (shown in the following example).</span></span>

:::image type="content" source="../../assets/images/personal-apps/add-from-app-flyout.png" alt-text="В примере показано, как добавить личное приложение из вылета приложения." border="false":::

## <a name="use-a-personal-app-private-workspace"></a><span data-ttu-id="a8f71-114">Использование личного приложения (личное рабочее пространство)</span><span class="sxs-lookup"><span data-stu-id="a8f71-114">Use a personal app (private workspace)</span></span>

<span data-ttu-id="a8f71-115">С помощью частного рабочего пространства вы можете просматривать содержимое приложения, содержательное для вас в центре, не Teams.</span><span class="sxs-lookup"><span data-stu-id="a8f71-115">With a private workspace, you can view app content that's meaningful to you in a central location without leaving Teams.</span></span>

<span data-ttu-id="a8f71-116">(Примечание реализации. Личное рабочее пространство основано на возможностях [*личной*](../../build-your-first-app/build-personal-tab.md) вкладки.)</span><span class="sxs-lookup"><span data-stu-id="a8f71-116">(Implementation note: The private workspace is based on the [*personal tab*](../../build-your-first-app/build-personal-tab.md) capability.)</span></span>

### <a name="anatomy-personal-app-private-workspace"></a><span data-ttu-id="a8f71-117">Анатомия: Личное приложение (личное рабочее пространство)</span><span class="sxs-lookup"><span data-stu-id="a8f71-117">Anatomy: Personal app (private workspace)</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-component-anatomy.png" alt-text="В примере показана анатомия компонентов личной вкладки." border="false":::

|<span data-ttu-id="a8f71-119">Счетчик</span><span class="sxs-lookup"><span data-stu-id="a8f71-119">Counter</span></span>|<span data-ttu-id="a8f71-120">Описание</span><span class="sxs-lookup"><span data-stu-id="a8f71-120">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="a8f71-121">A</span><span class="sxs-lookup"><span data-stu-id="a8f71-121">A</span></span>|<span data-ttu-id="a8f71-122">**Присвоение приложения:** логотип и имя приложения.</span><span class="sxs-lookup"><span data-stu-id="a8f71-122">**App attribution**: Your app logo and name.</span></span>|
|<span data-ttu-id="a8f71-123">B</span><span class="sxs-lookup"><span data-stu-id="a8f71-123">B</span></span>|<span data-ttu-id="a8f71-124">**Вкладки.** Обеспечивает навигацию для личного приложения.</span><span class="sxs-lookup"><span data-stu-id="a8f71-124">**Tabs**: Provides navigation for your personal app.</span></span> <span data-ttu-id="a8f71-125">Например, включаем **вкладку "О"** или **"Справка".**</span><span class="sxs-lookup"><span data-stu-id="a8f71-125">For example, include an **About** or **Help** tab.</span></span>|
|<span data-ttu-id="a8f71-126">C</span><span class="sxs-lookup"><span data-stu-id="a8f71-126">C</span></span>|<span data-ttu-id="a8f71-127">**Представление всплывающих** окон: отодвигает содержимое приложения из родительского окна в автономный детский окне.</span><span class="sxs-lookup"><span data-stu-id="a8f71-127">**Popout view**: Pushes your app content from a parent window to a standalone child window.</span></span>|
|<span data-ttu-id="a8f71-128">D</span><span class="sxs-lookup"><span data-stu-id="a8f71-128">D</span></span>|<span data-ttu-id="a8f71-129">**Дополнительные меню:** включает дополнительные сведения о приложении и параметры.</span><span class="sxs-lookup"><span data-stu-id="a8f71-129">**More menu**: Includes additional app information and options.</span></span> <span data-ttu-id="a8f71-130">(Можно также сделать **Параметры** вкладку.)</span><span class="sxs-lookup"><span data-stu-id="a8f71-130">(You could alternatively make **Settings** a tab.)</span></span>|

:::image type="content" source="../../assets/images/personal-apps/personal-tab-structural-anatomy.png" alt-text="В примере показана структурная анатомия личной вкладки." border="false":::

|<span data-ttu-id="a8f71-132">Счетчик</span><span class="sxs-lookup"><span data-stu-id="a8f71-132">Counter</span></span>|<span data-ttu-id="a8f71-133">Описание</span><span class="sxs-lookup"><span data-stu-id="a8f71-133">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="a8f71-134">A</span><span class="sxs-lookup"><span data-stu-id="a8f71-134">A</span></span>|<span data-ttu-id="a8f71-135">**Вкладки.** Обеспечивает навигацию для личного приложения.</span><span class="sxs-lookup"><span data-stu-id="a8f71-135">**Tabs**: Provides navigation for your personal app.</span></span>|
|<span data-ttu-id="a8f71-136">1</span><span class="sxs-lookup"><span data-stu-id="a8f71-136">1</span></span>|<span data-ttu-id="a8f71-137">**iframe:** отображает содержимое приложения.</span><span class="sxs-lookup"><span data-stu-id="a8f71-137">**iframe**: Displays your app content.</span></span>|

### <a name="designing-with-ui-templates"></a><span data-ttu-id="a8f71-138">Проектирование с помощью шаблонов пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="a8f71-138">Designing with UI templates</span></span>

<span data-ttu-id="a8f71-139">Используйте один из следующих Teams пользовательского интерфейса для разработки личной вкладки:</span><span class="sxs-lookup"><span data-stu-id="a8f71-139">Use one of the following Teams UI templates to help design your personal tab:</span></span>

* <span data-ttu-id="a8f71-140">[Список.](../../concepts/design/design-teams-app-ui-templates.md#list)Списки могут отображать связанные элементы в сканируемых форматах и позволяют пользователям принимать меры по всему списку или отдельным пунктам.</span><span class="sxs-lookup"><span data-stu-id="a8f71-140">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="a8f71-141">[Доска](../../concepts/design/design-teams-app-ui-templates.md#task-board)задач. Доска задач, иногда называемая канбанской или плавательные дорожки, — это коллекция карт, часто используемых для отслеживания состояния элементов или билетов.</span><span class="sxs-lookup"><span data-stu-id="a8f71-141">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="a8f71-142">[Панель](../../concepts/design/design-teams-app-ui-templates.md#dashboard)мониторинга: панель мониторинга — это холст, содержащий несколько карт, которые предоставляют обзор данных или контента.</span><span class="sxs-lookup"><span data-stu-id="a8f71-142">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="a8f71-143">[Form:](../../concepts/design/design-teams-app-ui-templates.md#form)Forms are for collecting, validating and submitting user input in a structured way.</span><span class="sxs-lookup"><span data-stu-id="a8f71-143">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="a8f71-144">[Пустое](../../concepts/design/design-teams-app-ui-templates.md#empty-state)состояние. Пустой шаблон состояния можно использовать для многих сценариев, включая вход, первый запуск, сообщения об ошибках и многое другое.</span><span class="sxs-lookup"><span data-stu-id="a8f71-144">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="a8f71-145">[Левый nav](../../concepts/design/design-teams-app-ui-templates.md#left-nav). Шаблон левого nav может помочь если ваша вкладка требует некоторой навигации.</span><span class="sxs-lookup"><span data-stu-id="a8f71-145">[Left nav](../../concepts/design/design-teams-app-ui-templates.md#left-nav): The left nav template can help if your tab requires some navigation.</span></span> <span data-ttu-id="a8f71-146">В общем, вы должны сохранить навигацию вкладок до минимума.</span><span class="sxs-lookup"><span data-stu-id="a8f71-146">In general, you should keep tab navigation to a minimum.</span></span>

## <a name="use-a-personal-app-bot"></a><span data-ttu-id="a8f71-147">Использование личного приложения (бота)</span><span class="sxs-lookup"><span data-stu-id="a8f71-147">Use a personal app (bot)</span></span>

<span data-ttu-id="a8f71-148">Личные приложения могут включать бот для индивидуальных бесед и частных уведомлений (например, когда коллега публикует комментарий на вашей доске).</span><span class="sxs-lookup"><span data-stu-id="a8f71-148">Personal apps can include a bot for one-on-one conversations and private notifications (for instance, when a colleague posts a comment on your artboard).</span></span> <span data-ttu-id="a8f71-149">Бот доступен на указанной вкладке.</span><span class="sxs-lookup"><span data-stu-id="a8f71-149">The bot is available in a tab you specify.</span></span>

### <a name="anatomy-personal-app-bot"></a><span data-ttu-id="a8f71-150">Анатомия: личное приложение (бот)</span><span class="sxs-lookup"><span data-stu-id="a8f71-150">Anatomy: Personal app (bot)</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-bot-anatomy.png" alt-text="В примере показана анатомия компонентов персональных ботов." border="false":::

|<span data-ttu-id="a8f71-152">Счетчик</span><span class="sxs-lookup"><span data-stu-id="a8f71-152">Counter</span></span>|<span data-ttu-id="a8f71-153">Описание</span><span class="sxs-lookup"><span data-stu-id="a8f71-153">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="a8f71-154">A</span><span class="sxs-lookup"><span data-stu-id="a8f71-154">A</span></span>|<span data-ttu-id="a8f71-155">**Вкладка Бот.** Например, включаем вкладку **Chat** для доступа к беседам и уведомлениям ботов.</span><span class="sxs-lookup"><span data-stu-id="a8f71-155">**Bot tab**: For example, include a **Chat** tab to access bot conversations and notifications.</span></span>|
|<span data-ttu-id="a8f71-156">B</span><span class="sxs-lookup"><span data-stu-id="a8f71-156">B</span></span>|<span data-ttu-id="a8f71-157">**Сообщение бота.** Боты часто отправляют сообщения и уведомления в виде карты (например, адаптивной карты).</span><span class="sxs-lookup"><span data-stu-id="a8f71-157">**Bot message**: Bots often send messages and notifications in the form of a card (such as an Adaptive Card).</span></span>|
|<span data-ttu-id="a8f71-158">C</span><span class="sxs-lookup"><span data-stu-id="a8f71-158">C</span></span>|<span data-ttu-id="a8f71-159">**Compose box**: Вводное поле для отправки сообщений боту.</span><span class="sxs-lookup"><span data-stu-id="a8f71-159">**Compose box**: Input field for sending messages to the bot.</span></span>|

## <a name="manage-a-personal-tab"></a><span data-ttu-id="a8f71-160">Управление личной вкладке</span><span class="sxs-lookup"><span data-stu-id="a8f71-160">Manage a personal tab</span></span>

<span data-ttu-id="a8f71-161">На левой стороне Teams пользователи могут правой кнопкой мыши личного приложения, чтобы закрепить, удалить и настроить другие параметры приложения.</span><span class="sxs-lookup"><span data-stu-id="a8f71-161">On the left side of Teams, users can right click the personal app to pin, remove, and configure other app options.</span></span>

:::image type="content" source="../../assets/images/personal-apps/manage-personal-tab.png" alt-text="В примере показаны параметры управления личным приложением." border="false":::

## <a name="best-practices"></a><span data-ttu-id="a8f71-163">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="a8f71-163">Best practices</span></span>

<span data-ttu-id="a8f71-164">Используйте эти рекомендации для создания качественного приложения.</span><span class="sxs-lookup"><span data-stu-id="a8f71-164">Use these recommendations to create a quality app experience.</span></span>

### <a name="tab-priority"></a><span data-ttu-id="a8f71-165">Приоритет tab</span><span class="sxs-lookup"><span data-stu-id="a8f71-165">Tab priority</span></span>

#### <a name="do-show-the-most-relevant-content-in-the-first-tab"></a><span data-ttu-id="a8f71-166">Do: Показать наиболее релевантный контент на первой вкладке</span><span class="sxs-lookup"><span data-stu-id="a8f71-166">Do: Show the most relevant content in the first tab</span></span>

<span data-ttu-id="a8f71-167">При гибком размере вкладки справа могут быть усечены или невещены.</span><span class="sxs-lookup"><span data-stu-id="a8f71-167">With responsive sizing, tabs on the right may become truncated or out of view.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-do.png" alt-text="В примере показано, как личное приложение отображает наиболее релевантный контент на первой вкладке." border="false":::

#### <a name="dont-lead-with-secondary-content-or-metadata"></a><span data-ttu-id="a8f71-169">Не: руководство со вторичным контентом или метаданными</span><span class="sxs-lookup"><span data-stu-id="a8f71-169">Don’t: Lead with secondary content or metadata</span></span>

<span data-ttu-id="a8f71-170">Как и стандартное веб-приложение, навигация вкладок должна развиваться в порядке, который помогает понять основные функции приложения.</span><span class="sxs-lookup"><span data-stu-id="a8f71-170">Like a standard web app, tab navigation should progress in an order that helps make sense of your app’s primary features.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-dont.png" alt-text="В примере показано личное приложение, ведущее со вторичным контентом или метаданными." border="false":::

### <a name="tab-hierarchy"></a><span data-ttu-id="a8f71-172">Иерархия вкладок</span><span class="sxs-lookup"><span data-stu-id="a8f71-172">Tab hierarchy</span></span>

#### <a name="do-tabs-should-be-of-equal-hierarchy-and-represent-key-app-pages"></a><span data-ttu-id="a8f71-173">Do: Tabs should be of equal hierarchy and represent key app pages</span><span class="sxs-lookup"><span data-stu-id="a8f71-173">Do: Tabs should be of equal hierarchy and represent key app pages</span></span>

<span data-ttu-id="a8f71-174">Ваши вкладки должны классифицировать основные функции и содержимое приложения.</span><span class="sxs-lookup"><span data-stu-id="a8f71-174">Your tabs should categorize your app’s primary features and content.</span></span> <span data-ttu-id="a8f71-175">При гибком размере содержимое справа может стать усеченным или невыясненным.</span><span class="sxs-lookup"><span data-stu-id="a8f71-175">With responsive sizing, content on the right may become truncated or out of view.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-do.png" alt-text="В примере показано личное приложение с вкладками равной иерархии." border="false":::

#### <a name="dont-include-different-levels-of-hierarchy"></a><span data-ttu-id="a8f71-177">Не: включайте различные уровни иерархии</span><span class="sxs-lookup"><span data-stu-id="a8f71-177">Don't: Include different levels of hierarchy</span></span>

<span data-ttu-id="a8f71-178">Ваше содержимое должно развиваться в логическом порядке, что помогает пользователям понять его.</span><span class="sxs-lookup"><span data-stu-id="a8f71-178">Your content should progress in a logical order that helps users make sense of it.</span></span> <span data-ttu-id="a8f71-179">Если у вас есть две вкладки, которые тесно связаны, рассмотрите возможность их объединения в одну вкладку.</span><span class="sxs-lookup"><span data-stu-id="a8f71-179">If you have two tabs that are closely related, consider combining them into one tab.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-dont.png" alt-text="В примере показано личное приложение с различными уровнями иерархии." border="false":::

### <a name="first-run-experience"></a><span data-ttu-id="a8f71-181">Интерфейс при первом запуске</span><span class="sxs-lookup"><span data-stu-id="a8f71-181">First-run experience</span></span>

#### <a name="do-include-a-first-run-experience"></a><span data-ttu-id="a8f71-182">Do: Включите первый запуск</span><span class="sxs-lookup"><span data-stu-id="a8f71-182">Do: Include a first-run experience</span></span>

<span data-ttu-id="a8f71-183">При первом использовании личного приложения должен быть по крайней мере приветственный экран.</span><span class="sxs-lookup"><span data-stu-id="a8f71-183">There should be at least a welcome screen the first time you use a personal app.</span></span> <span data-ttu-id="a8f71-184">Для ботов опишите, что может сделать ваш бот, и предопишите быстрые действия, например кнопку вход.</span><span class="sxs-lookup"><span data-stu-id="a8f71-184">For bots, describe what your bot can do and provide quick actions, such as a sign-in button.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-do.png" alt-text="В примере показано, что нужно делать во время личного опыта запуска приложения." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-fre-do.png" alt-text="В другом примере показано, что нужно делать во время работы с личным приложением в первом запуске." border="false":::

#### <a name="dont-start-with-a-blank-screen"></a><span data-ttu-id="a8f71-187">Не: начните с пустого экрана</span><span class="sxs-lookup"><span data-stu-id="a8f71-187">Don't: Start with a blank screen</span></span>

<span data-ttu-id="a8f71-188">Пользователи могут быть сбиты с толку, если при первом запуске приложения ничего не отображается.</span><span class="sxs-lookup"><span data-stu-id="a8f71-188">Users might be confused if nothing displays the first time they run your app.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-dont.png" alt-text="В примере показано, что не нужно делать во время первого запуска личного приложения." border="false":::

### <a name="personalized-content"></a><span data-ttu-id="a8f71-190">Персонализированный контент</span><span class="sxs-lookup"><span data-stu-id="a8f71-190">Personalized content</span></span>

#### <a name="do-aggregate-app-content-relevant-to-a-user"></a><span data-ttu-id="a8f71-191">Do: Совокупный контент приложения, релевантный пользователю</span><span class="sxs-lookup"><span data-stu-id="a8f71-191">Do: Aggregate app content relevant to a user</span></span>

<span data-ttu-id="a8f71-192">Будь то личная вкладка или бот, отображайте содержимое, связанное только с действиями пользователя в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="a8f71-192">Whether it's a personal tab or bot, display content related to only a user's activity in your app.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-do.png" alt-text="В примере показано, что делать с личным приложением и персонализированным контентом." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-do.png" alt-text="Другой пример показывает, что делать с личным приложением и персонализированным контентом." border="false":::

#### <a name="dont-show-unrelated-or-overly-broad-content"></a><span data-ttu-id="a8f71-195">Не: показывать несвязанные или чрезмерно широкий контент</span><span class="sxs-lookup"><span data-stu-id="a8f71-195">Don’t: Show unrelated or overly broad content</span></span>

<span data-ttu-id="a8f71-196">В личных контекстах не отображайте контент для групп, в которые пользователь не входит.</span><span class="sxs-lookup"><span data-stu-id="a8f71-196">In personal contexts, don’t display content for teams a user isn't part of.</span></span> <span data-ttu-id="a8f71-197">Личное содержимое бота должно фокусироваться на личности, а не на группе.</span><span class="sxs-lookup"><span data-stu-id="a8f71-197">Personal bot content should focus on the individual—not a group.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-dont.png" alt-text="В примере показано, что не нужно делать с личным приложением и персонализированным контентом." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-dont.png" alt-text="Другой пример показывает, что не нужно делать с личным приложением и персонализированным контентом." border="false":::

### <a name="complex-app-features"></a><span data-ttu-id="a8f71-200">Сложные функции приложения</span><span class="sxs-lookup"><span data-stu-id="a8f71-200">Complex app features</span></span>

#### <a name="do-allow-users-to-access-complex-features-in-a-browser"></a><span data-ttu-id="a8f71-201">Do: Разрешить пользователям доступ к сложным функциям в браузере</span><span class="sxs-lookup"><span data-stu-id="a8f71-201">Do: Allow users to access complex features in a browser</span></span>

<span data-ttu-id="a8f71-202">Ваше приложение должно сосредоточиться на основных задачах в Teams, но вы все равно можете просматривать полное, автономные приложения в браузере.</span><span class="sxs-lookup"><span data-stu-id="a8f71-202">Your app should focus on core tasks in Teams, but you can still view the full, standalone app in a browser.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-do.png" alt-text="В примере показано, как обрабатывать сложные функции приложения с помощью личного приложения." border="false":::

#### <a name="dont-include-your-entire-app"></a><span data-ttu-id="a8f71-204">Не: включите все приложение</span><span class="sxs-lookup"><span data-stu-id="a8f71-204">Don’t: Include your entire app</span></span>

<span data-ttu-id="a8f71-205">Если вы не создали приложение специально для Teams, возможно, у вас есть функции, которые не имеют смысла в средстве совместной работы.</span><span class="sxs-lookup"><span data-stu-id="a8f71-205">Unless you created your app specifically for Teams, you probably have features that don’t make sense in a collaboration tool.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-dont.png" alt-text="В примере показано, как не обрабатывать сложные функции приложения с помощью личного приложения." border="false":::

## <a name="see-also"></a><span data-ttu-id="a8f71-207">См. также</span><span class="sxs-lookup"><span data-stu-id="a8f71-207">See also</span></span>

<span data-ttu-id="a8f71-208">Эти другие рекомендации по проектированию могут помочь в зависимости от области вашего личного приложения:</span><span class="sxs-lookup"><span data-stu-id="a8f71-208">These other design guidelines may help depending on the scope of your personal app:</span></span>

* [<span data-ttu-id="a8f71-209">Проектирование вкладки</span><span class="sxs-lookup"><span data-stu-id="a8f71-209">Designing your tab</span></span>](../../tabs/design/tabs.md)
* [<span data-ttu-id="a8f71-210">Проектирование бота</span><span class="sxs-lookup"><span data-stu-id="a8f71-210">Designing you bot</span></span>](../../bots/design/bots.md)
