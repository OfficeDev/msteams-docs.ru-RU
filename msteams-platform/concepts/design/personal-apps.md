---
title: Разработка личного приложения
description: Узнайте, как разработать личное приложение Teams и получить набор пользовательских интерфейсов Microsoft Teams.
author: heath-hamilton
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 971071be9f345815f5461646d7970efdf05fd5c4
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/09/2020
ms.locfileid: "49605022"
---
# <a name="designing-your-personal-app-for-microsoft-teams"></a><span data-ttu-id="972fe-103">Разработка личного приложения для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="972fe-103">Designing your personal app for Microsoft Teams</span></span>

<span data-ttu-id="972fe-104">Личное приложение может представлять собой Bot, частные рабочие области или и то, и другое.</span><span class="sxs-lookup"><span data-stu-id="972fe-104">A personal app can be a bot, private workspace, or both.</span></span> <span data-ttu-id="972fe-105">Иногда она работает так же, как место для создания или просмотра контента, а также в других случаях, когда приложение настроено как вкладка в нескольких каналах.</span><span class="sxs-lookup"><span data-stu-id="972fe-105">Sometimes it functions like a place to create or view content, other times it offers the user a bird’s eye view of everything that’s theirs when the app has been configured as a tab in multiple channels.</span></span>

<span data-ttu-id="972fe-106">В следующей статье описываются и демонстрируются способы добавления и использования персональных приложений в Teams, а также управления ими.</span><span class="sxs-lookup"><span data-stu-id="972fe-106">To guide your app design, the following information describes and illustrates how people can add, use, and manage personal apps in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="972fe-107">Набор элементов пользовательского интерфейса Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="972fe-107">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="972fe-108">Вы можете найти подробные рекомендации по проектированию личных приложений, в том числе элементы, которые можно изменять и изменять при необходимости, в наборе UI Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="972fe-108">You can find comprehensive personal app design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="972fe-109">Кроме того, в наборе элементов пользовательского интерфейса есть важные темы, такие как специальные возможности и размеры отклика, которые не рассматриваются здесь.</span><span class="sxs-lookup"><span data-stu-id="972fe-109">The UI kit also has essential topics such as accessibility and responsive sizing that aren't covered here.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="972fe-110">Получение набора элементов пользовательского интерфейса Microsoft Teams (фигма)</span><span class="sxs-lookup"><span data-stu-id="972fe-110">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-personal-app"></a><span data-ttu-id="972fe-111">Добавление личного приложения</span><span class="sxs-lookup"><span data-stu-id="972fe-111">Add a personal app</span></span>

<span data-ttu-id="972fe-112">Вы можете добавить личное приложение из приложения Store (AppSource) или из всплывающего меню приложения, щелкнув значок **More (дополнительно** ) в левой части Teams (показано в следующем примере).</span><span class="sxs-lookup"><span data-stu-id="972fe-112">You can add a personal app from the Teams store (AppSource) or the app flyout by selecting the **More** icon on the left side of Teams (shown in the following example).</span></span>

:::image type="content" source="../../assets/images/personal-apps/add-from-app-flyout.png" alt-text="Пример показывает, как добавить личное приложение из всплывающего меню приложения." border="false":::

## <a name="use-a-personal-app-private-workspace"></a><span data-ttu-id="972fe-114">Использование личного приложения (личная рабочая область)</span><span class="sxs-lookup"><span data-stu-id="972fe-114">Use a personal app (private workspace)</span></span>

<span data-ttu-id="972fe-115">С помощью частной рабочей области вы можете просматривать контент приложений, который имеет смысл в централизованном расположении, не выходя из Teams.</span><span class="sxs-lookup"><span data-stu-id="972fe-115">With a private workspace, you can view app content that's meaningful to you in a central location without leaving Teams.</span></span>

<span data-ttu-id="972fe-116">(Примечание о реализации. Частная Рабочая область основана на возможности [*вкладки "личные"*](../../build-your-first-app/build-personal-tab.md) .)</span><span class="sxs-lookup"><span data-stu-id="972fe-116">(Implementation note: The private workspace is based on the [*personal tab*](../../build-your-first-app/build-personal-tab.md) capability.)</span></span>

### <a name="anatomy-personal-app-private-workspace"></a><span data-ttu-id="972fe-117">Структура: личное приложение (личная рабочая область)</span><span class="sxs-lookup"><span data-stu-id="972fe-117">Anatomy: Personal app (private workspace)</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-component-anatomy.png" alt-text="В примере показана структура компонента личной вкладки." border="false":::

|<span data-ttu-id="972fe-119">Счетчик</span><span class="sxs-lookup"><span data-stu-id="972fe-119">Counter</span></span>|<span data-ttu-id="972fe-120">Описание</span><span class="sxs-lookup"><span data-stu-id="972fe-120">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="972fe-121">A</span><span class="sxs-lookup"><span data-stu-id="972fe-121">A</span></span>|<span data-ttu-id="972fe-122">**Атрибуты приложений**: ваш логотип и имя приложения.</span><span class="sxs-lookup"><span data-stu-id="972fe-122">**App attribution**: Your app logo and name.</span></span>|
|<span data-ttu-id="972fe-123">B</span><span class="sxs-lookup"><span data-stu-id="972fe-123">B</span></span>|<span data-ttu-id="972fe-124">**Вкладки**: предоставляет навигацию для личного приложения.</span><span class="sxs-lookup"><span data-stu-id="972fe-124">**Tabs**: Provides navigation for your personal app.</span></span> <span data-ttu-id="972fe-125">Например, включите вкладку " **о программе** " или " **Справка** ".</span><span class="sxs-lookup"><span data-stu-id="972fe-125">For example, include an **About** or **Help** tab.</span></span>|
|<span data-ttu-id="972fe-126">C</span><span class="sxs-lookup"><span data-stu-id="972fe-126">C</span></span>|<span data-ttu-id="972fe-127">**Всплывающем окне View**: помещение контента приложения из родительского окна в автономное дочернее окно.</span><span class="sxs-lookup"><span data-stu-id="972fe-127">**Popout view**: Pushes your app content from a parent window to a standalone child window.</span></span>|
|<span data-ttu-id="972fe-128">D</span><span class="sxs-lookup"><span data-stu-id="972fe-128">D</span></span>|<span data-ttu-id="972fe-129">**Другое меню**: включает дополнительные сведения о приложении и другие параметры.</span><span class="sxs-lookup"><span data-stu-id="972fe-129">**More menu**: Includes additional app information and options.</span></span> <span data-ttu-id="972fe-130">(Можно также сделать **Параметры** вкладкой.)</span><span class="sxs-lookup"><span data-stu-id="972fe-130">(You could alternatively make **Settings** a tab.)</span></span>|

:::image type="content" source="../../assets/images/personal-apps/personal-tab-structural-anatomy.png" alt-text="В примере показана структура структуры личной вкладки." border="false":::

|<span data-ttu-id="972fe-132">Счетчик</span><span class="sxs-lookup"><span data-stu-id="972fe-132">Counter</span></span>|<span data-ttu-id="972fe-133">Описание</span><span class="sxs-lookup"><span data-stu-id="972fe-133">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="972fe-134">A</span><span class="sxs-lookup"><span data-stu-id="972fe-134">A</span></span>|<span data-ttu-id="972fe-135">**Вкладки**: предоставляет навигацию для личного приложения.</span><span class="sxs-lookup"><span data-stu-id="972fe-135">**Tabs**: Provides navigation for your personal app.</span></span>|
|<span data-ttu-id="972fe-136">1 </span><span class="sxs-lookup"><span data-stu-id="972fe-136">1</span></span>|<span data-ttu-id="972fe-137">**IFRAME**: отображение контента приложения.</span><span class="sxs-lookup"><span data-stu-id="972fe-137">**iframe**: Displays your app content.</span></span>|

### <a name="designing-with-ui-templates"></a><span data-ttu-id="972fe-138">Разработка с помощью шаблонов пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="972fe-138">Designing with UI templates</span></span>

<span data-ttu-id="972fe-139">Используйте один из следующих шаблонов пользовательского интерфейса Teams для создания личной вкладки:</span><span class="sxs-lookup"><span data-stu-id="972fe-139">Use one of the following Teams UI templates to help design your personal tab:</span></span>

* <span data-ttu-id="972fe-140">[Список](../../concepts/design/design-teams-app-ui-templates.md#list): списки могут отображать связанные элементы в формате с возможностью записи, а пользователи выполнять действия для всего списка или отдельных элементов.</span><span class="sxs-lookup"><span data-stu-id="972fe-140">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="972fe-141">[Доска задач](../../concepts/design/design-teams-app-ui-templates.md#task-board): доска задач, иногда называемая доской Канбан или свим желобами, — это коллекция карточек, часто используемых для отслеживания состояния рабочих элементов или билетов.</span><span class="sxs-lookup"><span data-stu-id="972fe-141">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="972fe-142">[Панель мониторинга](../../concepts/design/design-teams-app-ui-templates.md#dashboard): панель мониторинга — это холст, содержащий несколько карточек, которые предоставляют обзор данных или контента.</span><span class="sxs-lookup"><span data-stu-id="972fe-142">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="972fe-143">[Форма](../../concepts/design/design-teams-app-ui-templates.md#form): формы предназначены для сбора, проверки и отправки пользовательских данных структурированным способом.</span><span class="sxs-lookup"><span data-stu-id="972fe-143">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="972fe-144">[Пустое состояние](../../concepts/design/design-teams-app-ui-templates.md#empty-state): шаблон пустое состояние можно использовать для многих сценариев, в том числе входа в систему, первого запуска, сообщений об ошибках и многого другого.</span><span class="sxs-lookup"><span data-stu-id="972fe-144">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="972fe-145">[Левая панель навигации](../../concepts/design/design-teams-app-ui-templates.md#left-nav): левая панель навигации может помочь вам, если на вкладке требуется выполнить некоторую навигацию.</span><span class="sxs-lookup"><span data-stu-id="972fe-145">[Left nav](../../concepts/design/design-teams-app-ui-templates.md#left-nav): The left nav template can help if your tab requires some navigation.</span></span> <span data-ttu-id="972fe-146">Как правило, переход по клавише Tab должен быть минимальным.</span><span class="sxs-lookup"><span data-stu-id="972fe-146">In general, you should keep tab navigation to a minimum.</span></span>

## <a name="use-a-personal-app-bot"></a><span data-ttu-id="972fe-147">Использование личного приложения (Bot)</span><span class="sxs-lookup"><span data-stu-id="972fe-147">Use a personal app (bot)</span></span>

<span data-ttu-id="972fe-148">Персональные приложения могут включать робота для однообъектных бесед и частных уведомлений (например, когда коллега публикует комментарий в монтажной области).</span><span class="sxs-lookup"><span data-stu-id="972fe-148">Personal apps can include a bot for one-on-one conversations and private notifications (for instance, when a colleague posts a comment on your artboard).</span></span> <span data-ttu-id="972fe-149">Элемент Bot доступен на заданной вкладке.</span><span class="sxs-lookup"><span data-stu-id="972fe-149">The bot is available in a tab you specify.</span></span>

### <a name="anatomy-personal-app-bot"></a><span data-ttu-id="972fe-150">Структура: личное приложение (Bot)</span><span class="sxs-lookup"><span data-stu-id="972fe-150">Anatomy: Personal app (bot)</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-bot-anatomy.png" alt-text="В примере показана структура персональных компонентов Bot." border="false":::

|<span data-ttu-id="972fe-152">Счетчик</span><span class="sxs-lookup"><span data-stu-id="972fe-152">Counter</span></span>|<span data-ttu-id="972fe-153">Описание</span><span class="sxs-lookup"><span data-stu-id="972fe-153">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="972fe-154">A</span><span class="sxs-lookup"><span data-stu-id="972fe-154">A</span></span>|<span data-ttu-id="972fe-155">**Вкладка "bot"**: например, включите вкладку **Chat** , чтобы получить доступ к беседам и уведомлениям в Bot.</span><span class="sxs-lookup"><span data-stu-id="972fe-155">**Bot tab**: For example, include a **Chat** tab to access bot conversations and notifications.</span></span>|
|<span data-ttu-id="972fe-156">B</span><span class="sxs-lookup"><span data-stu-id="972fe-156">B</span></span>|<span data-ttu-id="972fe-157">**Сообщение Bot**: Боты часто отправляет сообщения и уведомления в виде карточки (например, адаптивной карты).</span><span class="sxs-lookup"><span data-stu-id="972fe-157">**Bot message**: Bots often send messages and notifications in the form of a card (such as an Adaptive Card).</span></span>|
|<span data-ttu-id="972fe-158">C</span><span class="sxs-lookup"><span data-stu-id="972fe-158">C</span></span>|<span data-ttu-id="972fe-159">**Поле создания**: поле ввода для отправки сообщений в Bot.</span><span class="sxs-lookup"><span data-stu-id="972fe-159">**Compose box**: Input field for sending messages to the bot.</span></span>|

## <a name="best-practices"></a><span data-ttu-id="972fe-160">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="972fe-160">Best practices</span></span>

### <a name="tab-priority"></a><span data-ttu-id="972fe-161">Приоритет вкладки</span><span class="sxs-lookup"><span data-stu-id="972fe-161">Tab priority</span></span>

#### <a name="do-show-the-most-relevant-content-in-the-first-tab"></a><span data-ttu-id="972fe-162">Do: отображение наиболее релевантного содержимого на первой вкладке</span><span class="sxs-lookup"><span data-stu-id="972fe-162">Do: Show the most relevant content in the first tab</span></span>

<span data-ttu-id="972fe-163">При быстром масштабировании вкладки справа могут быть усечены или отображаться.</span><span class="sxs-lookup"><span data-stu-id="972fe-163">With responsive sizing, tabs on the right may become truncated or out of view.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-do.png" alt-text="В примере показана Рекомендуемая Настройка личных приложений." border="false":::

#### <a name="dont-lead-with-secondary-content-or-metadata"></a><span data-ttu-id="972fe-165">Не: интерес с дополнительным содержимым или метаданными</span><span class="sxs-lookup"><span data-stu-id="972fe-165">Don’t: Lead with secondary content or metadata</span></span>

<span data-ttu-id="972fe-166">Как и в случае со стандартным веб-приложением, Навигация по табуляции должна быть продолжена в порядке, позволяющем понять основные функции приложения.</span><span class="sxs-lookup"><span data-stu-id="972fe-166">Like a standard web app, tab navigation should progress in an order that helps make sense of your app’s primary features.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-dont.png" alt-text="В примере показана Рекомендуемая Настройка личных приложений." border="false":::

### <a name="tab-hierarchy"></a><span data-ttu-id="972fe-168">Иерархия вкладок</span><span class="sxs-lookup"><span data-stu-id="972fe-168">Tab hierarchy</span></span>

#### <a name="do-tabs-should-be-of-equal-hierarchy-and-represent-key-app-pages"></a><span data-ttu-id="972fe-169">Do: вкладки должны иметь одинаковую иерархию и представлять ключевые страницы приложений</span><span class="sxs-lookup"><span data-stu-id="972fe-169">Do: Tabs should be of equal hierarchy and represent key app pages</span></span>

<span data-ttu-id="972fe-170">Вкладки должны классифицировать основные компоненты и содержимое приложения.</span><span class="sxs-lookup"><span data-stu-id="972fe-170">Your tabs should categorize your app’s primary features and content.</span></span> <span data-ttu-id="972fe-171">При быстром масштабировании содержимое в правой части может быть усечено или не отображаться.</span><span class="sxs-lookup"><span data-stu-id="972fe-171">With responsive sizing, content on the right may become truncated or out of view.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-do.png" alt-text="В примере показана Рекомендуемая Настройка личных приложений." border="false":::

#### <a name="dont-include-different-levels-of-hierarchy"></a><span data-ttu-id="972fe-173">Не используйте разные уровни иерархии.</span><span class="sxs-lookup"><span data-stu-id="972fe-173">Don't: Include different levels of hierarchy</span></span>

<span data-ttu-id="972fe-174">Контент должен продвигается в логическом порядке, который поможет пользователям понять его.</span><span class="sxs-lookup"><span data-stu-id="972fe-174">Your content should progress in a logical order that helps users make sense of it.</span></span> <span data-ttu-id="972fe-175">Если у вас есть две вкладки, которые тесно связаны друг с другом, рассмотрите их объединение на одной вкладке.</span><span class="sxs-lookup"><span data-stu-id="972fe-175">If you have two tabs that are closely related, consider combining them into one tab.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-dont.png" alt-text="В примере показана Рекомендуемая Настройка личных приложений." border="false":::

### <a name="first-run-experience"></a><span data-ttu-id="972fe-177">Интерфейс при первом запуске</span><span class="sxs-lookup"><span data-stu-id="972fe-177">First-run experience</span></span>

#### <a name="do-include-a-first-run-experience"></a><span data-ttu-id="972fe-178">Do: Включение интерфейса первого запуска</span><span class="sxs-lookup"><span data-stu-id="972fe-178">Do: Include a first-run experience</span></span>

<span data-ttu-id="972fe-179">При первом использовании личного приложения должен отображаться по крайней мере экран приветствия.</span><span class="sxs-lookup"><span data-stu-id="972fe-179">There should be at least a welcome screen the first time you use a personal app.</span></span> <span data-ttu-id="972fe-180">В Боты опишите действия, которые может выполнять Bot, и предоставляя быстрые действия, такие как кнопка входа.</span><span class="sxs-lookup"><span data-stu-id="972fe-180">For bots, describe what your bot can do and provide quick actions, such as a sign-in button.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-do.png" alt-text="В примере показана Рекомендуемая Настройка личных приложений." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-fre-do.png" alt-text="В примере показана Рекомендуемая Настройка личных приложений." border="false":::

#### <a name="dont-start-with-a-blank-screen"></a><span data-ttu-id="972fe-183">Не совсем: начало с пустого экрана</span><span class="sxs-lookup"><span data-stu-id="972fe-183">Don't: Start with a blank screen</span></span>

<span data-ttu-id="972fe-184">Пользователи могут запутаться, если при первом запуске приложения ничего не отображается.</span><span class="sxs-lookup"><span data-stu-id="972fe-184">Users might be confused if nothing displays the first time they run your app.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-dont.png" alt-text="В примере показана Рекомендуемая Настройка личных приложений." border="false":::

### <a name="personalized-content"></a><span data-ttu-id="972fe-186">Персонализированное содержимое</span><span class="sxs-lookup"><span data-stu-id="972fe-186">Personalized content</span></span>

#### <a name="do-aggregate-app-content-relevant-to-a-user"></a><span data-ttu-id="972fe-187">Do: Объединение контента приложения, относящегося к пользователю</span><span class="sxs-lookup"><span data-stu-id="972fe-187">Do: Aggregate app content relevant to a user</span></span>

<span data-ttu-id="972fe-188">Независимо от того, является ли это личная вкладка или Bot, отображается содержимое, связанное только с действиями пользователя в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="972fe-188">Whether it's a personal tab or bot, display content related to only a user's activity in your app.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-do.png" alt-text="В примере показана Рекомендуемая Настройка личных приложений." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-do.png" alt-text="В примере показана Рекомендуемая Настройка личных приложений." border="false":::

#### <a name="dont-show-unrelated-or-overly-broad-content"></a><span data-ttu-id="972fe-191">Не: показывать несвязанный или слишком большой контент</span><span class="sxs-lookup"><span data-stu-id="972fe-191">Don’t: Show unrelated or overly broad content</span></span>

<span data-ttu-id="972fe-192">В личных контекстах не отображать контент для Teams, не входящих в состав.</span><span class="sxs-lookup"><span data-stu-id="972fe-192">In personal contexts, don’t display content for teams a user isn't part of.</span></span> <span data-ttu-id="972fe-193">Личное содержимое Bot должно сосредоточиться на индивидуальной, а не группе.</span><span class="sxs-lookup"><span data-stu-id="972fe-193">Personal bot content should focus on the individual—not a group.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-dont.png" alt-text="В примере показана Рекомендуемая Настройка личных приложений." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-dont.png" alt-text="В примере показана Рекомендуемая Настройка личных приложений." border="false":::

### <a name="complex-app-features"></a><span data-ttu-id="972fe-196">Функции сложных приложений</span><span class="sxs-lookup"><span data-stu-id="972fe-196">Complex app features</span></span>

#### <a name="do-allow-users-to-access-complex-features-in-a-browser"></a><span data-ttu-id="972fe-197">Do: разрешает пользователям получать доступ к сложным функциям в браузере</span><span class="sxs-lookup"><span data-stu-id="972fe-197">Do: Allow users to access complex features in a browser</span></span>

<span data-ttu-id="972fe-198">Ваше приложение должно сосредоточиться на основных задачах в Teams, но вы по-прежнему можете просматривать полное автономное приложение в браузере.</span><span class="sxs-lookup"><span data-stu-id="972fe-198">Your app should focus on core tasks in Teams, but you can still view the full, standalone app in a browser.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-do.png" alt-text="В примере показана Рекомендуемая Настройка личных приложений." border="false":::

#### <a name="dont-include-your-entire-app"></a><span data-ttu-id="972fe-200">Не включайте свое приложение целиком.</span><span class="sxs-lookup"><span data-stu-id="972fe-200">Don’t: Include your entire app</span></span>

<span data-ttu-id="972fe-201">Если вы не создали приложение специально для Teams, вероятно, у вас есть функции, которые не имеют смысла в средстве совместной работы.</span><span class="sxs-lookup"><span data-stu-id="972fe-201">Unless you created your app specifically for Teams, you probably have features that don’t make sense in a collaboration tool.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-dont.png" alt-text="В примере показана Рекомендуемая Настройка личных приложений." border="false":::

## <a name="manage-a-personal-tab"></a><span data-ttu-id="972fe-203">Управление вкладкой "личные"</span><span class="sxs-lookup"><span data-stu-id="972fe-203">Manage a personal tab</span></span>

<span data-ttu-id="972fe-204">В левой части Teams пользователи могут щелкнуть личное приложение, чтобы закрепить, удалить и настроить другие параметры приложения.</span><span class="sxs-lookup"><span data-stu-id="972fe-204">On the left side of Teams, users can right click the personal app to pin, remove, and configure other app options.</span></span>

:::image type="content" source="../../assets/images/personal-apps/manage-personal-tab.png" alt-text="В примере показаны параметры для управления личным приложением." border="false":::

## <a name="learn-more"></a><span data-ttu-id="972fe-206">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="972fe-206">Learn more</span></span>

<span data-ttu-id="972fe-207">Другие рекомендации по проектированию могут пригодиться в зависимости от области личных приложений:</span><span class="sxs-lookup"><span data-stu-id="972fe-207">These other design guidelines may help depending on the scope of your personal app:</span></span>

* [<span data-ttu-id="972fe-208">Разработка вкладки</span><span class="sxs-lookup"><span data-stu-id="972fe-208">Designing your tab</span></span>](../../tabs/design/tabs.md)
* [<span data-ttu-id="972fe-209">Разработка ленты</span><span class="sxs-lookup"><span data-stu-id="972fe-209">Designing you bot</span></span>](../../bots/design/bots.md)

## <a name="validate-your-design"></a><span data-ttu-id="972fe-210">Проверка проекта</span><span class="sxs-lookup"><span data-stu-id="972fe-210">Validate your design</span></span>

<span data-ttu-id="972fe-211">Если вы планируете опубликовать свое приложение в AppSource, следует изучить проблемы, которые обычно приводят к сбою приложений во время отправки.</span><span class="sxs-lookup"><span data-stu-id="972fe-211">If you plan to publish your app to AppSource, you should understand the design issues that commonly cause apps to fail during submission.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="972fe-212">Проверка рекомендаций по проверке макета</span><span class="sxs-lookup"><span data-stu-id="972fe-212">Check design validation guidelines</span></span>](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
