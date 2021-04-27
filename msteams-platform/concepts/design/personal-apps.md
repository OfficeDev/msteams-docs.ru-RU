---
title: Проектирование личного приложения
description: Узнайте, как создать личное приложение Teams и получить набор пользовательского интерфейса Microsoft Teams.
author: heath-hamilton
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 8302f3768034014ef5a446effeee0603afe4a5f4
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020760"
---
# <a name="designing-your-personal-app-for-microsoft-teams"></a><span data-ttu-id="c3bd2-103">Разработка личного приложения для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="c3bd2-103">Designing your personal app for Microsoft Teams</span></span>

<span data-ttu-id="c3bd2-104">Персональным приложением может быть бот, частное рабочее пространство или и то, и другое.</span><span class="sxs-lookup"><span data-stu-id="c3bd2-104">A personal app can be a bot, private workspace, or both.</span></span> <span data-ttu-id="c3bd2-105">Иногда он функционирует как место для создания или просмотра контента, в других случаях он предлагает пользователю вид с высоты птичьего полета на все, что у них, когда приложение было настроено как вкладка в нескольких каналах.</span><span class="sxs-lookup"><span data-stu-id="c3bd2-105">Sometimes it functions like a place to create or view content, other times it offers the user a bird’s eye view of everything that's theirs when the app has been configured as a tab in multiple channels.</span></span>

<span data-ttu-id="c3bd2-106">Чтобы направлять разработку приложения, в следующих сведениях описывается и иллюстрируется, как люди могут добавлять, использовать и управлять личными приложениями в Teams.</span><span class="sxs-lookup"><span data-stu-id="c3bd2-106">To guide your app design, the following information describes and illustrates how people can add, use, and manage personal apps in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="c3bd2-107">Комплект разработчика для пользовательского интерфейса Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="c3bd2-107">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="c3bd2-108">В наборе пользовательского интерфейса Microsoft Teams можно найти исчерпывающие рекомендации по разработке персональных приложений, в том числе элементы, которые можно захватить и изменить по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="c3bd2-108">You can find comprehensive personal app design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="c3bd2-109">Набор пользовательского интерфейса также имеет важные темы, такие как доступность и размер отзывчивый, которые здесь не охватываются.</span><span class="sxs-lookup"><span data-stu-id="c3bd2-109">The UI kit also has essential topics such as accessibility and responsive sizing that aren't covered here.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c3bd2-110">Получить комплект разработчика для пользовательского интерфейса Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="c3bd2-110">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-personal-app"></a><span data-ttu-id="c3bd2-111">Добавление личного приложения</span><span class="sxs-lookup"><span data-stu-id="c3bd2-111">Add a personal app</span></span>

<span data-ttu-id="c3bd2-112">Вы можете добавить личное приложение из магазина Teams (AppSource) или вылет приложения, выбрав значок **More** на левой стороне Teams (показано в следующем примере).</span><span class="sxs-lookup"><span data-stu-id="c3bd2-112">You can add a personal app from the Teams store (AppSource) or the app flyout by selecting the **More** icon on the left side of Teams (shown in the following example).</span></span>

:::image type="content" source="../../assets/images/personal-apps/add-from-app-flyout.png" alt-text="В примере показано, как добавить личное приложение из вылета приложения." border="false":::

## <a name="use-a-personal-app-private-workspace"></a><span data-ttu-id="c3bd2-114">Использование личного приложения (личное рабочее пространство)</span><span class="sxs-lookup"><span data-stu-id="c3bd2-114">Use a personal app (private workspace)</span></span>

<span data-ttu-id="c3bd2-115">С помощью частного рабочего пространства можно просматривать содержимое приложения, которое имеет значение для вас в центре расположения, не покидая Teams.</span><span class="sxs-lookup"><span data-stu-id="c3bd2-115">With a private workspace, you can view app content that's meaningful to you in a central location without leaving Teams.</span></span>

<span data-ttu-id="c3bd2-116">(Примечание реализации. Личное рабочее пространство основано на возможностях [*личной*](../../build-your-first-app/build-personal-tab.md) вкладки.)</span><span class="sxs-lookup"><span data-stu-id="c3bd2-116">(Implementation note: The private workspace is based on the [*personal tab*](../../build-your-first-app/build-personal-tab.md) capability.)</span></span>

### <a name="anatomy-personal-app-private-workspace"></a><span data-ttu-id="c3bd2-117">Анатомия: Личное приложение (личное рабочее пространство)</span><span class="sxs-lookup"><span data-stu-id="c3bd2-117">Anatomy: Personal app (private workspace)</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-component-anatomy.png" alt-text="В примере показана анатомия компонентов личной вкладки." border="false":::

|<span data-ttu-id="c3bd2-119">Счетчик</span><span class="sxs-lookup"><span data-stu-id="c3bd2-119">Counter</span></span>|<span data-ttu-id="c3bd2-120">Описание</span><span class="sxs-lookup"><span data-stu-id="c3bd2-120">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="c3bd2-121">A</span><span class="sxs-lookup"><span data-stu-id="c3bd2-121">A</span></span>|<span data-ttu-id="c3bd2-122">**Присвоение приложения:** логотип и имя приложения.</span><span class="sxs-lookup"><span data-stu-id="c3bd2-122">**App attribution**: Your app logo and name.</span></span>|
|<span data-ttu-id="c3bd2-123">B</span><span class="sxs-lookup"><span data-stu-id="c3bd2-123">B</span></span>|<span data-ttu-id="c3bd2-124">**Вкладки.** Обеспечивает навигацию для личного приложения.</span><span class="sxs-lookup"><span data-stu-id="c3bd2-124">**Tabs**: Provides navigation for your personal app.</span></span> <span data-ttu-id="c3bd2-125">Например, включаем **вкладку "О"** или **"Справка".**</span><span class="sxs-lookup"><span data-stu-id="c3bd2-125">For example, include an **About** or **Help** tab.</span></span>|
|<span data-ttu-id="c3bd2-126">C</span><span class="sxs-lookup"><span data-stu-id="c3bd2-126">C</span></span>|<span data-ttu-id="c3bd2-127">**Представление всплывающих** окон: отодвигает содержимое приложения из родительского окна в автономный детский окне.</span><span class="sxs-lookup"><span data-stu-id="c3bd2-127">**Popout view**: Pushes your app content from a parent window to a standalone child window.</span></span>|
|<span data-ttu-id="c3bd2-128">D</span><span class="sxs-lookup"><span data-stu-id="c3bd2-128">D</span></span>|<span data-ttu-id="c3bd2-129">**Дополнительные меню:** включает дополнительные сведения о приложении и параметры.</span><span class="sxs-lookup"><span data-stu-id="c3bd2-129">**More menu**: Includes additional app information and options.</span></span> <span data-ttu-id="c3bd2-130">(Можно также сделать **параметры** вкладками.)</span><span class="sxs-lookup"><span data-stu-id="c3bd2-130">(You could alternatively make **Settings** a tab.)</span></span>|

:::image type="content" source="../../assets/images/personal-apps/personal-tab-structural-anatomy.png" alt-text="В примере показана структурная анатомия личной вкладки." border="false":::

|<span data-ttu-id="c3bd2-132">Счетчик</span><span class="sxs-lookup"><span data-stu-id="c3bd2-132">Counter</span></span>|<span data-ttu-id="c3bd2-133">Описание</span><span class="sxs-lookup"><span data-stu-id="c3bd2-133">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="c3bd2-134">A</span><span class="sxs-lookup"><span data-stu-id="c3bd2-134">A</span></span>|<span data-ttu-id="c3bd2-135">**Вкладки.** Обеспечивает навигацию для личного приложения.</span><span class="sxs-lookup"><span data-stu-id="c3bd2-135">**Tabs**: Provides navigation for your personal app.</span></span>|
|<span data-ttu-id="c3bd2-136">1</span><span class="sxs-lookup"><span data-stu-id="c3bd2-136">1</span></span>|<span data-ttu-id="c3bd2-137">**iframe:** отображает содержимое приложения.</span><span class="sxs-lookup"><span data-stu-id="c3bd2-137">**iframe**: Displays your app content.</span></span>|

### <a name="designing-with-ui-templates"></a><span data-ttu-id="c3bd2-138">Проектирование с помощью шаблонов пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="c3bd2-138">Designing with UI templates</span></span>

<span data-ttu-id="c3bd2-139">Для разработки личной вкладки используйте один из следующих шаблонов пользовательского интерфейса Teams:</span><span class="sxs-lookup"><span data-stu-id="c3bd2-139">Use one of the following Teams UI templates to help design your personal tab:</span></span>

* <span data-ttu-id="c3bd2-140">[Список.](../../concepts/design/design-teams-app-ui-templates.md#list)Списки могут отображать связанные элементы в сканируемых форматах и позволяют пользователям принимать меры по всему списку или отдельным пунктам.</span><span class="sxs-lookup"><span data-stu-id="c3bd2-140">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="c3bd2-141">[Доска](../../concepts/design/design-teams-app-ui-templates.md#task-board)задач. Доска задач, иногда называемая канбанской или плавательные дорожки, — это коллекция карт, часто используемых для отслеживания состояния элементов или билетов.</span><span class="sxs-lookup"><span data-stu-id="c3bd2-141">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="c3bd2-142">[Панель](../../concepts/design/design-teams-app-ui-templates.md#dashboard)мониторинга: панель мониторинга — это холст, содержащий несколько карт, которые предоставляют обзор данных или контента.</span><span class="sxs-lookup"><span data-stu-id="c3bd2-142">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="c3bd2-143">[Form:](../../concepts/design/design-teams-app-ui-templates.md#form)Forms are for collecting, validating and submitting user input in a structured way.</span><span class="sxs-lookup"><span data-stu-id="c3bd2-143">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="c3bd2-144">[Пустое](../../concepts/design/design-teams-app-ui-templates.md#empty-state)состояние. Пустой шаблон состояния можно использовать для многих сценариев, включая вход, первый запуск, сообщения об ошибках и многое другое.</span><span class="sxs-lookup"><span data-stu-id="c3bd2-144">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="c3bd2-145">[Левый nav](../../concepts/design/design-teams-app-ui-templates.md#left-nav). Шаблон левого nav может помочь если ваша вкладка требует некоторой навигации.</span><span class="sxs-lookup"><span data-stu-id="c3bd2-145">[Left nav](../../concepts/design/design-teams-app-ui-templates.md#left-nav): The left nav template can help if your tab requires some navigation.</span></span> <span data-ttu-id="c3bd2-146">В общем, вы должны сохранить навигацию вкладок до минимума.</span><span class="sxs-lookup"><span data-stu-id="c3bd2-146">In general, you should keep tab navigation to a minimum.</span></span>

## <a name="use-a-personal-app-bot"></a><span data-ttu-id="c3bd2-147">Использование личного приложения (бота)</span><span class="sxs-lookup"><span data-stu-id="c3bd2-147">Use a personal app (bot)</span></span>

<span data-ttu-id="c3bd2-148">Личные приложения могут включать бот для индивидуальных бесед и частных уведомлений (например, когда коллега публикует комментарий на вашей доске).</span><span class="sxs-lookup"><span data-stu-id="c3bd2-148">Personal apps can include a bot for one-on-one conversations and private notifications (for instance, when a colleague posts a comment on your artboard).</span></span> <span data-ttu-id="c3bd2-149">Бот доступен на указанной вкладке.</span><span class="sxs-lookup"><span data-stu-id="c3bd2-149">The bot is available in a tab you specify.</span></span>

### <a name="anatomy-personal-app-bot"></a><span data-ttu-id="c3bd2-150">Анатомия: личное приложение (бот)</span><span class="sxs-lookup"><span data-stu-id="c3bd2-150">Anatomy: Personal app (bot)</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-bot-anatomy.png" alt-text="В примере показана анатомия компонентов персональных ботов." border="false":::

|<span data-ttu-id="c3bd2-152">Счетчик</span><span class="sxs-lookup"><span data-stu-id="c3bd2-152">Counter</span></span>|<span data-ttu-id="c3bd2-153">Описание</span><span class="sxs-lookup"><span data-stu-id="c3bd2-153">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="c3bd2-154">A</span><span class="sxs-lookup"><span data-stu-id="c3bd2-154">A</span></span>|<span data-ttu-id="c3bd2-155">**Вкладка Бот.** Например, включаем вкладку **Chat** для доступа к беседам и уведомлениям ботов.</span><span class="sxs-lookup"><span data-stu-id="c3bd2-155">**Bot tab**: For example, include a **Chat** tab to access bot conversations and notifications.</span></span>|
|<span data-ttu-id="c3bd2-156">B</span><span class="sxs-lookup"><span data-stu-id="c3bd2-156">B</span></span>|<span data-ttu-id="c3bd2-157">**Сообщение бота.** Боты часто отправляют сообщения и уведомления в виде карты (например, адаптивной карты).</span><span class="sxs-lookup"><span data-stu-id="c3bd2-157">**Bot message**: Bots often send messages and notifications in the form of a card (such as an Adaptive Card).</span></span>|
|<span data-ttu-id="c3bd2-158">C</span><span class="sxs-lookup"><span data-stu-id="c3bd2-158">C</span></span>|<span data-ttu-id="c3bd2-159">**Compose box**: Вводное поле для отправки сообщений боту.</span><span class="sxs-lookup"><span data-stu-id="c3bd2-159">**Compose box**: Input field for sending messages to the bot.</span></span>|

## <a name="best-practices"></a><span data-ttu-id="c3bd2-160">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="c3bd2-160">Best practices</span></span>

### <a name="tab-priority"></a><span data-ttu-id="c3bd2-161">Приоритет tab</span><span class="sxs-lookup"><span data-stu-id="c3bd2-161">Tab priority</span></span>

#### <a name="do-show-the-most-relevant-content-in-the-first-tab"></a><span data-ttu-id="c3bd2-162">Do: Показать наиболее релевантный контент на первой вкладке</span><span class="sxs-lookup"><span data-stu-id="c3bd2-162">Do: Show the most relevant content in the first tab</span></span>

<span data-ttu-id="c3bd2-163">При гибком размере вкладки справа могут быть усечены или невещены.</span><span class="sxs-lookup"><span data-stu-id="c3bd2-163">With responsive sizing, tabs on the right may become truncated or out of view.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-do.png" alt-text="В примере показана лучшая практика личного приложения." border="false":::

#### <a name="dont-lead-with-secondary-content-or-metadata"></a><span data-ttu-id="c3bd2-165">Не: руководство со вторичным контентом или метаданными</span><span class="sxs-lookup"><span data-stu-id="c3bd2-165">Don’t: Lead with secondary content or metadata</span></span>

<span data-ttu-id="c3bd2-166">Как и стандартное веб-приложение, навигация вкладок должна развиваться в порядке, который помогает понять основные функции приложения.</span><span class="sxs-lookup"><span data-stu-id="c3bd2-166">Like a standard web app, tab navigation should progress in an order that helps make sense of your app’s primary features.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-dont.png" alt-text="Пример наилучшей практики личного приложения." border="false":::

### <a name="tab-hierarchy"></a><span data-ttu-id="c3bd2-168">Иерархия вкладок</span><span class="sxs-lookup"><span data-stu-id="c3bd2-168">Tab hierarchy</span></span>

#### <a name="do-tabs-should-be-of-equal-hierarchy-and-represent-key-app-pages"></a><span data-ttu-id="c3bd2-169">Do: Tabs should be of equal hierarchy and represent key app pages</span><span class="sxs-lookup"><span data-stu-id="c3bd2-169">Do: Tabs should be of equal hierarchy and represent key app pages</span></span>

<span data-ttu-id="c3bd2-170">Ваши вкладки должны классифицировать основные функции и содержимое приложения.</span><span class="sxs-lookup"><span data-stu-id="c3bd2-170">Your tabs should categorize your app’s primary features and content.</span></span> <span data-ttu-id="c3bd2-171">При гибком размере содержимое справа может стать усеченным или невыясненным.</span><span class="sxs-lookup"><span data-stu-id="c3bd2-171">With responsive sizing, content on the right may become truncated or out of view.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-do.png" alt-text="В примере показана лучшая практика личного приложения." border="false":::

#### <a name="dont-include-different-levels-of-hierarchy"></a><span data-ttu-id="c3bd2-173">Не: включайте различные уровни иерархии</span><span class="sxs-lookup"><span data-stu-id="c3bd2-173">Don't: Include different levels of hierarchy</span></span>

<span data-ttu-id="c3bd2-174">Ваше содержимое должно развиваться в логическом порядке, что помогает пользователям понять его.</span><span class="sxs-lookup"><span data-stu-id="c3bd2-174">Your content should progress in a logical order that helps users make sense of it.</span></span> <span data-ttu-id="c3bd2-175">Если у вас есть две вкладки, которые тесно связаны, рассмотрите возможность их объединения в одну вкладку.</span><span class="sxs-lookup"><span data-stu-id="c3bd2-175">If you have two tabs that are closely related, consider combining them into one tab.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-dont.png" alt-text="В примере показана лучшая практика личного приложения." border="false":::

### <a name="first-run-experience"></a><span data-ttu-id="c3bd2-177">Интерфейс при первом запуске</span><span class="sxs-lookup"><span data-stu-id="c3bd2-177">First-run experience</span></span>

#### <a name="do-include-a-first-run-experience"></a><span data-ttu-id="c3bd2-178">Do: Включите первый запуск</span><span class="sxs-lookup"><span data-stu-id="c3bd2-178">Do: Include a first-run experience</span></span>

<span data-ttu-id="c3bd2-179">При первом использовании личного приложения должен быть по крайней мере приветственный экран.</span><span class="sxs-lookup"><span data-stu-id="c3bd2-179">There should be at least a welcome screen the first time you use a personal app.</span></span> <span data-ttu-id="c3bd2-180">Для ботов опишите, что может сделать ваш бот, и предопишите быстрые действия, например кнопку вход.</span><span class="sxs-lookup"><span data-stu-id="c3bd2-180">For bots, describe what your bot can do and provide quick actions, such as a sign-in button.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-do.png" alt-text="На рисунке показана лучшая практика личного приложения." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-fre-do.png" alt-text="Пример наилучшей практики личного приложения." border="false":::

#### <a name="dont-start-with-a-blank-screen"></a><span data-ttu-id="c3bd2-183">Не: начните с пустого экрана</span><span class="sxs-lookup"><span data-stu-id="c3bd2-183">Don't: Start with a blank screen</span></span>

<span data-ttu-id="c3bd2-184">Пользователи могут быть сбиты с толку, если при первом запуске приложения ничего не отображается.</span><span class="sxs-lookup"><span data-stu-id="c3bd2-184">Users might be confused if nothing displays the first time they run your app.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-dont.png" alt-text="На рисунке показана лучшая практика личного приложения." border="false":::

### <a name="personalized-content"></a><span data-ttu-id="c3bd2-186">Персонализированный контент</span><span class="sxs-lookup"><span data-stu-id="c3bd2-186">Personalized content</span></span>

#### <a name="do-aggregate-app-content-relevant-to-a-user"></a><span data-ttu-id="c3bd2-187">Do: Совокупный контент приложения, релевантный пользователю</span><span class="sxs-lookup"><span data-stu-id="c3bd2-187">Do: Aggregate app content relevant to a user</span></span>

<span data-ttu-id="c3bd2-188">Будь то личная вкладка или бот, отображайте содержимое, связанное только с действиями пользователя в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="c3bd2-188">Whether it's a personal tab or bot, display content related to only a user's activity in your app.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-do.png" alt-text="В примере приводится пример наилучшей практики личного приложения." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-do.png" alt-text="В примере показана лучшая практика личного приложения." border="false":::

#### <a name="dont-show-unrelated-or-overly-broad-content"></a><span data-ttu-id="c3bd2-191">Не: показывать несвязанные или чрезмерно широкий контент</span><span class="sxs-lookup"><span data-stu-id="c3bd2-191">Don’t: Show unrelated or overly broad content</span></span>

<span data-ttu-id="c3bd2-192">В личных контекстах не отображайте контент для групп, в которые пользователь не входит.</span><span class="sxs-lookup"><span data-stu-id="c3bd2-192">In personal contexts, don’t display content for teams a user isn't part of.</span></span> <span data-ttu-id="c3bd2-193">Личное содержимое бота должно фокусироваться на личности, а не на группе.</span><span class="sxs-lookup"><span data-stu-id="c3bd2-193">Personal bot content should focus on the individual—not a group.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-dont.png" alt-text="Раскрыт пример наилучшей практики личного приложения." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-dont.png" alt-text="В примере показана лучшая практика личного приложения." border="false":::

### <a name="complex-app-features"></a><span data-ttu-id="c3bd2-196">Сложные функции приложения</span><span class="sxs-lookup"><span data-stu-id="c3bd2-196">Complex app features</span></span>

#### <a name="do-allow-users-to-access-complex-features-in-a-browser"></a><span data-ttu-id="c3bd2-197">Do: Разрешить пользователям доступ к сложным функциям в браузере</span><span class="sxs-lookup"><span data-stu-id="c3bd2-197">Do: Allow users to access complex features in a browser</span></span>

<span data-ttu-id="c3bd2-198">Ваше приложение должно сосредоточиться на основных задачах в Teams, но вы все равно можете просматривать полное, автономные приложения в браузере.</span><span class="sxs-lookup"><span data-stu-id="c3bd2-198">Your app should focus on core tasks in Teams, but you can still view the full, standalone app in a browser.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-do.png" alt-text="В примере показана лучшая практика личного приложения." border="false":::

#### <a name="dont-include-your-entire-app"></a><span data-ttu-id="c3bd2-200">Не: включите все приложение</span><span class="sxs-lookup"><span data-stu-id="c3bd2-200">Don’t: Include your entire app</span></span>

<span data-ttu-id="c3bd2-201">Если вы не создали приложение специально для Teams, возможно, у вас есть функции, которые не имеют смысла в средстве совместной работы.</span><span class="sxs-lookup"><span data-stu-id="c3bd2-201">Unless you created your app specifically for Teams, you probably have features that don’t make sense in a collaboration tool.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-dont.png" alt-text="Иллюстрация предоставляет личные приложения наилучшей практики." border="false":::

## <a name="manage-a-personal-tab"></a><span data-ttu-id="c3bd2-203">Управление личной вкладке</span><span class="sxs-lookup"><span data-stu-id="c3bd2-203">Manage a personal tab</span></span>

<span data-ttu-id="c3bd2-204">В левой части Teams пользователи могут правой кнопкой мыши личные приложения, чтобы закрепить, удалить и настроить другие параметры приложения.</span><span class="sxs-lookup"><span data-stu-id="c3bd2-204">On the left side of Teams, users can right click the personal app to pin, remove, and configure other app options.</span></span>

:::image type="content" source="../../assets/images/personal-apps/manage-personal-tab.png" alt-text="В примере показаны параметры управления личным приложением." border="false":::

## <a name="learn-more"></a><span data-ttu-id="c3bd2-206">Подробнее</span><span class="sxs-lookup"><span data-stu-id="c3bd2-206">Learn more</span></span>

<span data-ttu-id="c3bd2-207">Эти другие рекомендации по проектированию могут помочь в зависимости от области вашего личного приложения:</span><span class="sxs-lookup"><span data-stu-id="c3bd2-207">These other design guidelines may help depending on the scope of your personal app:</span></span>

* [<span data-ttu-id="c3bd2-208">Проектирование вкладки</span><span class="sxs-lookup"><span data-stu-id="c3bd2-208">Designing your tab</span></span>](../../tabs/design/tabs.md)
* [<span data-ttu-id="c3bd2-209">Проектирование бота</span><span class="sxs-lookup"><span data-stu-id="c3bd2-209">Designing you bot</span></span>](../../bots/design/bots.md)

## <a name="validate-your-design"></a><span data-ttu-id="c3bd2-210">Проверка приложения</span><span class="sxs-lookup"><span data-stu-id="c3bd2-210">Validate your design</span></span>

<span data-ttu-id="c3bd2-211">Если вы планируете опубликовать приложение в AppSource, следует понимать проблемы проектирования, из-за которых отправка приложения часто бывает неудачной.</span><span class="sxs-lookup"><span data-stu-id="c3bd2-211">If you plan to publish your app to AppSource, you should understand the design issues that commonly cause apps to fail during submission.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c3bd2-212">Ознакомьтесь с рекомендациями по проверке дизайна</span><span class="sxs-lookup"><span data-stu-id="c3bd2-212">Check design validation guidelines</span></span>](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
