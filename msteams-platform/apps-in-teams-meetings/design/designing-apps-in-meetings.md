---
title: Проектирование расширения собрания
author: heath-hamilton
description: Узнайте, как создать приложения Teams собраниях и получить Microsoft Teams пользовательского интерфейса.
ms.author: lajanuar
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: 0a888c333305e9caafcd0bac0e5549bf08ead424
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566028"
---
# <a name="designing-your-microsoft-teams-meeting-extension"></a><span data-ttu-id="d6bdd-103">Проектирование расширения Microsoft Teams собрания</span><span class="sxs-lookup"><span data-stu-id="d6bdd-103">Designing your Microsoft Teams meeting extension</span></span>

<span data-ttu-id="d6bdd-104">Вы можете создавать приложения, чтобы сделать собрания более продуктивными.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-104">You can create apps to make meetings more productive.</span></span> <span data-ttu-id="d6bdd-105">Например, попросите людей выполнить опрос во время вызова или отправить быстрое напоминание, которое не прерывает поток собрания.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-105">For example, ask people to complete a survey during a call or send a quick reminder that doesn’t interrupt the flow of the meeting.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="d6bdd-106">Комплект разработчика для пользовательского интерфейса Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="d6bdd-106">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="d6bdd-107">В наборе пользовательского интерфейса можно найти более исчерпывающие рекомендации по проектированию Microsoft Teams, в том числе элементы, которые можно захватить и изменить по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-107">You can find more comprehensive design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d6bdd-108">Получить комплект разработчика для пользовательского интерфейса Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="d6bdd-108">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-meeting-extension"></a><span data-ttu-id="d6bdd-109">Добавление расширения собрания</span><span class="sxs-lookup"><span data-stu-id="d6bdd-109">Add a meeting extension</span></span>

<span data-ttu-id="d6bdd-110">Вы можете добавить расширение собрания до и во время собраний.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-110">You can add a meeting extension before and during meetings.</span></span> <span data-ttu-id="d6bdd-111">Вы также можете добавить приложение для определенной встречи непосредственно из Teams магазина (AppSource).</span><span class="sxs-lookup"><span data-stu-id="d6bdd-111">You also can add an app for a specific meeting directly from the Teams store (AppSource).</span></span>

### <a name="add-before-a-meeting"></a><span data-ttu-id="d6bdd-112">Добавление перед собранием</span><span class="sxs-lookup"><span data-stu-id="d6bdd-112">Add before a meeting</span></span>

<span data-ttu-id="d6bdd-113">В сведениях о собрании выберите Добавить вкладку **+,** чтобы открыть вылет приложения и найти приложения, оптимизированные для собраний.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-113">In the meeting details, select **Add a tab +** to open the app flyout and find apps optimized for meetings.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/add-before-meeting.png" alt-text="В примере показано, как добавить расширение собрания перед собранием." border="false":::

### <a name="add-during-a-meeting"></a><span data-ttu-id="d6bdd-115">Добавление во время собрания</span><span class="sxs-lookup"><span data-stu-id="d6bdd-115">Add during a meeting</span></span>

На собрании выберите **дополнительные** :::image type="icon" source="../../assets/icons/teams-client-more.png":::  >  **добавления приложения** и выберите нужное приложение.

:::image type="content" source="../../assets/images/apps-in-meetings/add-during-meeting.png" alt-text="В примере показано, как добавить расширение собрания во время собрания." border="false":::

## <a name="before-a-meeting"></a><span data-ttu-id="d6bdd-118">Перед собранием</span><span class="sxs-lookup"><span data-stu-id="d6bdd-118">Before a meeting</span></span>

<span data-ttu-id="d6bdd-119">Перед собранием можно добавить содержимое на вкладке. В следующем примере показан проект опроса, на который люди ответят во время вызова.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-119">Prior to your meeting, you can add content in the tab. The following example shows a draft survey question that people will answer during the call.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/before-meeting-tab.png" alt-text="В примере показано, как приложение содержимым в сведениях о собрании перед вызовом." border="false":::

### <a name="anatomy-meeting-tab-before-and-after-meetings"></a><span data-ttu-id="d6bdd-121">Анатомия: вкладка "Собрание" (до и после собраний)</span><span class="sxs-lookup"><span data-stu-id="d6bdd-121">Anatomy: Meeting tab (before and after meetings)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/meeting-details-tab-anatomy.png" alt-text="В примере показана структурная анатомия вкладки собрания до и после собрания." border="false":::

|<span data-ttu-id="d6bdd-123">Счетчик</span><span class="sxs-lookup"><span data-stu-id="d6bdd-123">Counter</span></span>|<span data-ttu-id="d6bdd-124">Описание</span><span class="sxs-lookup"><span data-stu-id="d6bdd-124">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="d6bdd-125">1</span><span class="sxs-lookup"><span data-stu-id="d6bdd-125">1</span></span>|<span data-ttu-id="d6bdd-126">**Имя вкладки.** Метка навигации для вкладки.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-126">**Tab name**: Navigation label for your tab.</span></span>|
|<span data-ttu-id="d6bdd-127">2</span><span class="sxs-lookup"><span data-stu-id="d6bdd-127">2</span></span>|<span data-ttu-id="d6bdd-128">**Переполнение вкладки:** открывает действия вкладки, такие как переименование и удаление.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-128">**Tab overflow**: Opens tab actions, such as rename and remove.</span></span>|
|<span data-ttu-id="d6bdd-129">3</span><span class="sxs-lookup"><span data-stu-id="d6bdd-129">3</span></span>|<span data-ttu-id="d6bdd-130">**iframe:** отображает содержимое приложения.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-130">**iframe**: Displays your app content.</span></span>|

### <a name="designing-with-ui-templates"></a><span data-ttu-id="d6bdd-131">Проектирование с помощью шаблонов пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="d6bdd-131">Designing with UI templates</span></span>

<span data-ttu-id="d6bdd-132">Используйте один из следующих Teams пользовательского интерфейса для разработки вкладки собраний:</span><span class="sxs-lookup"><span data-stu-id="d6bdd-132">Use one of the following Teams UI templates to help design your meeting tab:</span></span>

* <span data-ttu-id="d6bdd-133">[Список.](../../concepts/design/design-teams-app-ui-templates.md#list)Списки могут отображать связанные элементы в сканируемых форматах и позволяют пользователям принимать меры по всему списку или отдельным пунктам.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-133">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="d6bdd-134">[Доска](../../concepts/design/design-teams-app-ui-templates.md#task-board)задач. Доска задач, иногда называемая канбанской или плавательные дорожки, — это коллекция карт, часто используемых для отслеживания состояния элементов или билетов.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-134">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="d6bdd-135">[Панель](../../concepts/design/design-teams-app-ui-templates.md#dashboard)мониторинга: панель мониторинга — это холст, содержащий несколько карт, которые предоставляют обзор данных или контента.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-135">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="d6bdd-136">[Form:](../../concepts/design/design-teams-app-ui-templates.md#form)Forms are for collecting, validating and submitting user input in a structured way.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-136">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="d6bdd-137">[Пустое](../../concepts/design/design-teams-app-ui-templates.md#empty-state)состояние. Пустой шаблон состояния можно использовать для многих сценариев, включая вход, первый запуск, сообщения об ошибках и многое другое.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-137">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="d6bdd-138">[Левый nav](../../concepts/design/design-teams-app-ui-templates.md#left-nav). Шаблон левого nav может помочь если ваша вкладка требует некоторой навигации.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-138">[Left nav](../../concepts/design/design-teams-app-ui-templates.md#left-nav): The left nav template can help if your tab requires some navigation.</span></span> <span data-ttu-id="d6bdd-139">В общем, вы должны сохранить навигацию вкладок до минимума.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-139">In general, you should keep tab navigation to a minimum.</span></span>

## <a name="use-an-in-meeting-tab"></a><span data-ttu-id="d6bdd-140">Использование вкладки в собрании</span><span class="sxs-lookup"><span data-stu-id="d6bdd-140">Use an in-meeting tab</span></span>

<span data-ttu-id="d6bdd-141">Вкладка на собрании — это холст для расширения совместной работы во время собраний.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-141">The in-meeting tab is a canvas for augmenting collaboration during meetings.</span></span> <span data-ttu-id="d6bdd-142">Участники могут видеть и взаимодействовать с контентом приложения в выделенном пространстве за пределами стадии собраний с помощью общих представлений или представлений на основе ролей.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-142">Attendees can see and interact with app content in a dedicated space outside the meeting stage through shared or role-based views.</span></span>

### <a name="use-cases"></a><span data-ttu-id="d6bdd-143">Варианты использования</span><span class="sxs-lookup"><span data-stu-id="d6bdd-143">Use cases</span></span>

<span data-ttu-id="d6bdd-144">Люди могут использовать вкладку на собрании, чтобы:</span><span class="sxs-lookup"><span data-stu-id="d6bdd-144">People might use the in-meeting tab to:</span></span>

* <span data-ttu-id="d6bdd-145">Предоставление подробных отзывов.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-145">Provide detailed feedback.</span></span> <span data-ttu-id="d6bdd-146">Например, оцените кандидата на работу.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-146">For example, evaluate a job candidate.</span></span>
* <span data-ttu-id="d6bdd-147">Создайте элемент опроса, опроса или задачи для участников собрания.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-147">Create a poll, survey, or task item for the meeting participants.</span></span>
* <span data-ttu-id="d6bdd-148">Отображение заметок, соответствующих собранию.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-148">Display notes relevant to the meeting.</span></span> <span data-ttu-id="d6bdd-149">Например, сведения о лидере продаж.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-149">For example, information about a sales lead.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-tab.png" alt-text="В примере показано, как можно представить содержимое опроса на вкладке на собрании." border="false":::

### <a name="anatomy-in-meeting-tab"></a><span data-ttu-id="d6bdd-151">Anatomy: In-meeting tab</span><span class="sxs-lookup"><span data-stu-id="d6bdd-151">Anatomy: In-meeting tab</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-anatomy.png" alt-text="В примере показана структурная анатомия вкладки на собрании." border="false":::

|<span data-ttu-id="d6bdd-153">Счетчик</span><span class="sxs-lookup"><span data-stu-id="d6bdd-153">Counter</span></span>|<span data-ttu-id="d6bdd-154">Описание</span><span class="sxs-lookup"><span data-stu-id="d6bdd-154">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="d6bdd-155">1</span><span class="sxs-lookup"><span data-stu-id="d6bdd-155">1</span></span>|<span data-ttu-id="d6bdd-156">**Значок приложения (выбранный)**: 16-пиксельный прозрачный логотип приложения.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-156">**App icon (selected)**: 16-pixel transparent app logo.</span></span>|
|<span data-ttu-id="d6bdd-157">2</span><span class="sxs-lookup"><span data-stu-id="d6bdd-157">2</span></span>|<span data-ttu-id="d6bdd-158">**Имя приложения**</span><span class="sxs-lookup"><span data-stu-id="d6bdd-158">**App name**</span></span>|
|<span data-ttu-id="d6bdd-159">3</span><span class="sxs-lookup"><span data-stu-id="d6bdd-159">3</span></span>|<span data-ttu-id="d6bdd-160">**Заглавное** имя. Включает имя приложения.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-160">**Header**: Includes your app name.</span></span>|
|<span data-ttu-id="d6bdd-161">4 </span><span class="sxs-lookup"><span data-stu-id="d6bdd-161">4</span></span>|<span data-ttu-id="d6bdd-162">**Кнопка закрыть:** отклонять вкладку. Всегда используйте значок верхнего правого закрытия вместо действия в подножке.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-162">**Close button**: Dismisses the tab. Always use the upper-right close icon instead of an action in the footer.</span></span>|
|<span data-ttu-id="d6bdd-163">5 </span><span class="sxs-lookup"><span data-stu-id="d6bdd-163">5</span></span>|<span data-ttu-id="d6bdd-164">**Панели** уведомлений. Оповещения об ошибках отображаются непосредственно под заголовком и толкают содержимое iframe вниз на 20 пикселей.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-164">**Notification bar**: Error alerts display directly below the header and push the iframe content down by 20 pixels.</span></span>|
|<span data-ttu-id="d6bdd-165">6 </span><span class="sxs-lookup"><span data-stu-id="d6bdd-165">6</span></span>|<span data-ttu-id="d6bdd-166">**iframe:** отображает содержимое приложения.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-166">**iframe**: Displays your app content.</span></span>|

### <a name="spacing"></a><span data-ttu-id="d6bdd-167">Интервал</span><span class="sxs-lookup"><span data-stu-id="d6bdd-167">Spacing</span></span>

<span data-ttu-id="d6bdd-168">Оптимизируйте вкладку в собрании, чтобы поместиться по краям в области iframe шириной 280 пикселей.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-168">Optimize your in-meeting tab to fit edge-to-edge within the 280 pixel-wide iframe area.</span></span> <span data-ttu-id="d6bdd-169">На левой и правой сторонах iframe и между загонами вкладок имеется 20 пикселей.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-169">There are 20 pixels of padding on the left and right sides of the iframe and between the tab header.</span></span> <span data-ttu-id="d6bdd-170">Iframe полностью кровотока в нижней части вкладки.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-170">The iframe is full bleed to the bottom of the tab.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-spacing.png" alt-text="В примере показаны размеры интервала между вкладками в собрании." border="false":::

### <a name="scrolling"></a><span data-ttu-id="d6bdd-172">Прокрутка</span><span class="sxs-lookup"><span data-stu-id="d6bdd-172">Scrolling</span></span>

<span data-ttu-id="d6bdd-173">Содержимое Iframe должно прокручиваться вертикально.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-173">Iframe contents should scroll vertically.</span></span> <span data-ttu-id="d6bdd-174">Вы можете видеть только содержимое, которое вы прокрутите (ничего выше или ниже).</span><span class="sxs-lookup"><span data-stu-id="d6bdd-174">You can only see the content you've scrolled to (nothing above or below).</span></span> <span data-ttu-id="d6bdd-175">Панель прокрутки является частью контента iframe.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-175">The scrollbar is part of the iframe content.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-scrolling.png" alt-text="В примере показано, как прокручивается вкладка на собрании." border="false":::

### <a name="navigation"></a><span data-ttu-id="d6bdd-177">Навигация</span><span class="sxs-lookup"><span data-stu-id="d6bdd-177">Navigation</span></span>

<span data-ttu-id="d6bdd-178">Для сценариев со слоями навигации или тяжелым контентом рекомендуется разрешить пользователям переходить на вторичный уровень.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-178">For scenarios with navigation layers or heavy content, we recommend allowing users to navigate to a secondary layer.</span></span> <span data-ttu-id="d6bdd-179">Пользователи должны иметь возможность вернуться к предыдущему слою.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-179">Users must be able to go back to the previous layer.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav.png" alt-text="В примере показана навигация в собрании." border="false":::

## <a name="use-an-in-meeting-dialog"></a><span data-ttu-id="d6bdd-181">Использование диалогового номера на собрании</span><span class="sxs-lookup"><span data-stu-id="d6bdd-181">Use an in-meeting dialog</span></span>

<span data-ttu-id="d6bdd-182">Диалоги на собрании отображаются на Teams собрания.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-182">In-meeting dialogs display on the Teams meeting stage.</span></span> <span data-ttu-id="d6bdd-183">Они требуют внимания пользователя, подтверждения или взаимодействия, но являются тонкими и не прерывают собрание.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-183">They require a user's attention, confirmation, or interaction but are subtle and don't interrupt the meeting.</span></span> <span data-ttu-id="d6bdd-184">Эти сценарии следует использовать экономно и для сценариев, ориентированных на легкие и задачи.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-184">You should use these sparingly and for scenarios that are light and task oriented.</span></span>

### <a name="use-cases"></a><span data-ttu-id="d6bdd-185">Варианты использования</span><span class="sxs-lookup"><span data-stu-id="d6bdd-185">Use cases</span></span>

<span data-ttu-id="d6bdd-186">Диалоговые точки на собрании запускаются пользователем (например, организатором собрания), который может потребовать от участников:</span><span class="sxs-lookup"><span data-stu-id="d6bdd-186">In-meeting dialogs are triggered by a user (such as the meeting organizer) who might want participants to:</span></span>

* <span data-ttu-id="d6bdd-187">Предоставление кратких отзывов</span><span class="sxs-lookup"><span data-stu-id="d6bdd-187">Provide brief feedback</span></span>
* <span data-ttu-id="d6bdd-188">Краткий опрос или опрос</span><span class="sxs-lookup"><span data-stu-id="d6bdd-188">Take a short survey or poll</span></span>
* <span data-ttu-id="d6bdd-189">Отправка утверждений</span><span class="sxs-lookup"><span data-stu-id="d6bdd-189">Submit approvals</span></span>
* <span data-ttu-id="d6bdd-190">Получать напоминания</span><span class="sxs-lookup"><span data-stu-id="d6bdd-190">Get reminders</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-dialog.png" alt-text="В примере показано, как можно использовать диалоговое окно на собрании." border="false":::

### <a name="anatomy-in-meeting-dialog"></a><span data-ttu-id="d6bdd-192">Анатомия: диалоговое окно на собрании</span><span class="sxs-lookup"><span data-stu-id="d6bdd-192">Anatomy: In-meeting dialog</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-anatomy.png" alt-text="В примере показана структурная анатомия диалогов на собрании." border="false":::

|<span data-ttu-id="d6bdd-194">Счетчик</span><span class="sxs-lookup"><span data-stu-id="d6bdd-194">Counter</span></span>|<span data-ttu-id="d6bdd-195">Описание</span><span class="sxs-lookup"><span data-stu-id="d6bdd-195">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="d6bdd-196">1</span><span class="sxs-lookup"><span data-stu-id="d6bdd-196">1</span></span>|<span data-ttu-id="d6bdd-197">**Заглавная** строка: включает значок приложения, имя, строку действия и значок закрытия.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-197">**Header**: Includes app icon, name, action string, and close icon.</span></span>|
|<span data-ttu-id="d6bdd-198">2</span><span class="sxs-lookup"><span data-stu-id="d6bdd-198">2</span></span>|<span data-ttu-id="d6bdd-199">**iframe:** отображает содержимое приложения.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-199">**iframe**: Displays your app content.</span></span>|

### <a name="anatomy-in-meeting-dialog-header"></a><span data-ttu-id="d6bdd-200">Анатомия: диалоговое заглавное окно в собрании</span><span class="sxs-lookup"><span data-stu-id="d6bdd-200">Anatomy: In-meeting dialog header</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-header-anatomy.png" alt-text="В примере показана структурная анатомия диалогового загона на собрании." border="false":::

<span data-ttu-id="d6bdd-202">Существует два варианта загона.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-202">There are two header variants.</span></span> <span data-ttu-id="d6bdd-203">По возможности используйте вариант с аватаром, чтобы подчеркнуть, что диалоговое окно идет от человека.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-203">When possible, use the variant with the avatar to reinforce that the dialog is coming from a person.</span></span>

|<span data-ttu-id="d6bdd-204">Счетчик</span><span class="sxs-lookup"><span data-stu-id="d6bdd-204">Counter</span></span>|<span data-ttu-id="d6bdd-205">Описание</span><span class="sxs-lookup"><span data-stu-id="d6bdd-205">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="d6bdd-206">1</span><span class="sxs-lookup"><span data-stu-id="d6bdd-206">1</span></span>|<span data-ttu-id="d6bdd-207">**Аватар:** человек, который инициирует диалоговое окно на собрании.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-207">**Avatar**: Person who initiates the in-meeting dialog.</span></span>|
|<span data-ttu-id="d6bdd-208">2</span><span class="sxs-lookup"><span data-stu-id="d6bdd-208">2</span></span>|<span data-ttu-id="d6bdd-209">**Значок приложения**</span><span class="sxs-lookup"><span data-stu-id="d6bdd-209">**App icon**</span></span>|
|<span data-ttu-id="d6bdd-210">3</span><span class="sxs-lookup"><span data-stu-id="d6bdd-210">3</span></span>|<span data-ttu-id="d6bdd-211">**Имя приложения**</span><span class="sxs-lookup"><span data-stu-id="d6bdd-211">**App name**</span></span>|
|<span data-ttu-id="d6bdd-212">4 </span><span class="sxs-lookup"><span data-stu-id="d6bdd-212">4</span></span>|<span data-ttu-id="d6bdd-213">**Кнопка Закрыть:** отклонять диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-213">**Close button**: Dismisses the dialog.</span></span>|
|<span data-ttu-id="d6bdd-214">5 </span><span class="sxs-lookup"><span data-stu-id="d6bdd-214">5</span></span>|<span data-ttu-id="d6bdd-215">**Строка** действия. Обычно описывается, кто инициировал диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-215">**Action string**: Typically describes who initiated the dialog.</span></span>|

### <a name="responsive-behavior"></a><span data-ttu-id="d6bdd-216">Адаптируемое поведение</span><span class="sxs-lookup"><span data-stu-id="d6bdd-216">Responsive behavior</span></span>

<span data-ttu-id="d6bdd-217">Диалоги на собрании могут отличаться по размеру для учета различных сценариев.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-217">In-meeting dialogs can vary in size to account for different scenarios.</span></span> <span data-ttu-id="d6bdd-218">Убедитесь, что поддерживается обивка и размеры компонентов.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-218">Make sure to maintain padding and component sizes.</span></span>

* <span data-ttu-id="d6bdd-219">**Ширина.** Можно указать ширину iframe диалогов в любом месте в поддерживаемом диапазоне размеров.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-219">**Width**: You can specify the width of the dialog's iframe anywhere within the supported size range.</span></span>
* <span data-ttu-id="d6bdd-220">**Высота.** Вы можете указать высоту iframe диалогов в любом месте в поддерживаемом диапазоне размеров.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-220">**Height**: You can specify the height of the dialog's iframe anywhere within the supported size range.</span></span> <span data-ttu-id="d6bdd-221">Вы также можете разрешить пользователям прокрутку по вертикали, если содержимое приложения превышает максимальную высоту.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-221">You also can allow users to scroll vertically if your app content exceeds the maximum height.</span></span>

<span data-ttu-id="d6bdd-222">Чтобы реализовать, укажите ширину и высоту с помощью [`externalResourceUrl`](~/apps-in-teams-meetings/create-apps-for-teams-meetings.md#notificationsignal-api) ключа.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-222">To implement, specify the width and height using the [`externalResourceUrl`](~/apps-in-teams-meetings/create-apps-for-teams-meetings.md#notificationsignal-api) key.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-responsive.png" alt-text="В примере показан диалоговое окно на собрании. Ширина: min--280 пикселей (248 пикселей iframe). Max--460 пикселей (428 пикселей iframe). Высота: 300 пикселей (iframe)." border="false":::

## <a name="after-a-meeting"></a><span data-ttu-id="d6bdd-224">После собрания</span><span class="sxs-lookup"><span data-stu-id="d6bdd-224">After a meeting</span></span>

<span data-ttu-id="d6bdd-225">Вы можете вернуться к собранию после его окончания и просмотреть содержимое приложения.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-225">You can go back to a meeting after it ends and view app content.</span></span> <span data-ttu-id="d6bdd-226">В этом примере организатор собрания может посмотреть результаты опроса на вкладке **Contoso.** (Примечание. С точки зрения дизайна нет разницы между опытом вкладки до и после собрания.)</span><span class="sxs-lookup"><span data-stu-id="d6bdd-226">In this example, the meeting organizer can look at poll results in the **Contoso** tab. (Note: From a design standpoint, there's no difference between a the pre- and post-meeting tab experience.)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/post-meeting-experience.png" alt-text="В примере показана вкладка после собрания." border="false":::

## <a name="best-practices"></a><span data-ttu-id="d6bdd-228">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="d6bdd-228">Best practices</span></span>

<span data-ttu-id="d6bdd-229">Используйте эти рекомендации для создания качественного приложения.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-229">Use these recommendations to create a quality app experience.</span></span>

### <a name="interactions"></a><span data-ttu-id="d6bdd-230">Взаимодействие</span><span class="sxs-lookup"><span data-stu-id="d6bdd-230">Interactions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-do.png" alt-text="Пример, показывающий, как ограничить количество взаимодействий." border="false":::

#### <a name="do-limit-the-number-of-interactions"></a><span data-ttu-id="d6bdd-232">Do: Ограничение количества взаимодействий</span><span class="sxs-lookup"><span data-stu-id="d6bdd-232">Do: Limit the number of interactions</span></span>

<span data-ttu-id="d6bdd-233">Для диалогов на собраниях удалите ненужный контент, который не поможет пользователям быстро выполнить свою задачу.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-233">For in-meeting dialogs, remove unnecessary content that doesn't help users accomplish something quickly.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-dont.png" alt-text="Пример, показывающий, как не вводить ненужные элементы." border="false":::

#### <a name="dont-introduce-unnecessary-elements"></a><span data-ttu-id="d6bdd-235">Не: вводить ненужные элементы</span><span class="sxs-lookup"><span data-stu-id="d6bdd-235">Don't: Introduce unnecessary elements</span></span>

<span data-ttu-id="d6bdd-236">Один диалоговое окно с несколькими взаимодействиями может отвлечь от вызова.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-236">A single in-meeting dialog with multiple interactions can distract from the call.</span></span>

   :::column-end:::
:::row-end:::

### <a name="layout"></a><span data-ttu-id="d6bdd-237">Макет</span><span class="sxs-lookup"><span data-stu-id="d6bdd-237">Layout</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-do.png" alt-text="Пример, показывающий использование макета диалогов с одним столбцом." border="false":::

#### <a name="do-use-a-single-column-dialog-layout"></a><span data-ttu-id="d6bdd-239">Do: Использование макета диалогов с одним столбцом</span><span class="sxs-lookup"><span data-stu-id="d6bdd-239">Do: Use a single-column dialog layout</span></span>

<span data-ttu-id="d6bdd-240">Так как диалоги находятся в центре стадии собрания, завершение задачи должно быть быстрым и простым, чтобы избежать разочарования пользователей.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-240">Since the dialogs are at the center of the meeting stage, task completion should be fast and simple to avoid user frustration.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-dont.png" alt-text="Пример, показывающий, что не следует загромождать пространство расширения собрания." border="false":::

#### <a name="dont-clutter-the-space"></a><span data-ttu-id="d6bdd-242">Не: загромождать пространство</span><span class="sxs-lookup"><span data-stu-id="d6bdd-242">Don't: Clutter the space</span></span>

<span data-ttu-id="d6bdd-243">Плотный или чрезмерно структурированный контент может отвлекать и ошеломить, особенно во время собрания.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-243">Dense or overly structured content can be distracting and overwhelming, especially during a meeting.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-do.png" alt-text="Пример макета вкладки с одним столбцом." border="false":::

#### <a name="do-use-a-single-column-tab-layout"></a><span data-ttu-id="d6bdd-245">Do: Использование макета вкладок с одним столбцом</span><span class="sxs-lookup"><span data-stu-id="d6bdd-245">Do: Use a single-column tab layout</span></span>

<span data-ttu-id="d6bdd-246">Учитывая узкий характер вкладки на собрании, настоятельно рекомендуется отображать содержимое в одном столбце.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-246">Given the in-meeting tab's narrow nature, we strongly recommend displaying the contents in a single column.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-dont.png" alt-text="Пример, показывающий вкладку с несколькими столбцами." border="false":::

#### <a name="dont-use-multiple-columns"></a><span data-ttu-id="d6bdd-248">Не используйте несколько столбцов</span><span class="sxs-lookup"><span data-stu-id="d6bdd-248">Don't: Use multiple columns</span></span>

<span data-ttu-id="d6bdd-249">Из-за ограниченного пространства вкладки в собрании макеты с более чем одним столбцом не рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-249">Due to the limited space of the in-meeting tab, layouts with more than one column aren’t recommended.</span></span>

   :::column-end:::
:::row-end:::

### <a name="controls"></a><span data-ttu-id="d6bdd-250">Элементы управления</span><span class="sxs-lookup"><span data-stu-id="d6bdd-250">Controls</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-do.png" alt-text="Пример, показывающий, как правильно выравнивать основные элементы управления." border="false":::

#### <a name="do-right-align-the-primary-action"></a><span data-ttu-id="d6bdd-252">Do: правильно выравнивание основного действия</span><span class="sxs-lookup"><span data-stu-id="d6bdd-252">Do: Right align the primary action</span></span>

<span data-ttu-id="d6bdd-253">Рекомендуется расположить наиболее визуально тяжелое действие в нужном месте.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-253">We recommend positioning the most visually heavy action to the right-most location.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-dont.png" alt-text="Пример, показывающий, как не следует выровнять основные элементы управления." border="false":::

#### <a name="dont-left-or-center-align-actions"></a><span data-ttu-id="d6bdd-255">Не: действия левого или центрального выравнивания</span><span class="sxs-lookup"><span data-stu-id="d6bdd-255">Don't: Left or center align actions</span></span>

<span data-ttu-id="d6bdd-256">Это отклоняется от стандартного шаблона Teams для размещения управления в диалоговом окте и может противоречить диалоговику за верхней.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-256">This deviates from the standard Teams pattern for control placement in a dialog and may conflict with a dialog behind the top one.</span></span>

   :::column-end:::
:::row-end:::

### <a name="scroll"></a><span data-ttu-id="d6bdd-257">Прокрутка</span><span class="sxs-lookup"><span data-stu-id="d6bdd-257">Scroll</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-do.png" alt-text="Пример, показывающий вертикальную прокрутку на вкладке в собрании." border="false":::

#### <a name="do-scroll-vertically"></a><span data-ttu-id="d6bdd-259">Do: Прокрутите по вертикали</span><span class="sxs-lookup"><span data-stu-id="d6bdd-259">Do: Scroll vertically</span></span>

<span data-ttu-id="d6bdd-260">Пользователи ожидают вертикального прокрутки Teams (и в других местах).</span><span class="sxs-lookup"><span data-stu-id="d6bdd-260">Users expect vertical scrolling in Teams (and elsewhere).</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-dont.png" alt-text="Пример, показывающий горизонтальную прокрутку на вкладке на собрании." border="false":::

#### <a name="dont-scroll-horizontally"></a><span data-ttu-id="d6bdd-262">Не: прокрутите по горизонтали</span><span class="sxs-lookup"><span data-stu-id="d6bdd-262">Don't: Scroll horizontally</span></span>

<span data-ttu-id="d6bdd-263">Горизонтальная прокрутка не является ожидаемым поведением в Teams.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-263">Horizontal scrolling isn’t an expected behavior in Teams.</span></span> <span data-ttu-id="d6bdd-264">Другие холсты в среде собраний прокрутки вертикально.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-264">Other canvases in the meeting environment scroll vertically.</span></span>

   :::column-end:::
:::row-end:::

### <a name="workflows"></a><span data-ttu-id="d6bdd-265">Рабочие процессы</span><span class="sxs-lookup"><span data-stu-id="d6bdd-265">Workflows</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-workflow-do.png" alt-text="Пример, показывающий сложный сценарий на вкладке на собрании." border="false":::

#### <a name="do-surface-complex-scenarios-in-the-in-meeting-tab"></a><span data-ttu-id="d6bdd-267">Do: Surface complex scenarios in the in-meeting tab</span><span class="sxs-lookup"><span data-stu-id="d6bdd-267">Do: Surface complex scenarios in the in-meeting tab</span></span>

<span data-ttu-id="d6bdd-268">Если ваше приложение включает несколько задач, настоятельно рекомендуется использовать вкладку на собрании с макетом с одним столбцом.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-268">If your app includes multiple tasks, we strongly recommend using an in-meeting tab with a single-column layout.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-workflow-dont.png" alt-text="Пример, показывающий сложные сценарии в диалоговом окантове встречи." border="false":::

#### <a name="dont-make-in-meeting-dialogs-complex"></a><span data-ttu-id="d6bdd-270">Don't: Make in-meeting dialogs complex</span><span class="sxs-lookup"><span data-stu-id="d6bdd-270">Don't: Make in-meeting dialogs complex</span></span>

<span data-ttu-id="d6bdd-271">Диалоги на собраниях предназначены для кратких взаимодействий.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-271">In-meeting dialogs are intended for brief interactions.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="d6bdd-272">Темы</span><span class="sxs-lookup"><span data-stu-id="d6bdd-272">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-do.png" alt-text="Пример, показывающий расширение собрания с темной темой." border="false":::

#### <a name="do-use-teams-color-tokens"></a><span data-ttu-id="d6bdd-274">Do: использование Teams маркеров цвета</span><span class="sxs-lookup"><span data-stu-id="d6bdd-274">Do: Use Teams color tokens</span></span>

<span data-ttu-id="d6bdd-275">Teams для темного режима оптимизированы, чтобы уменьшить визуальный и когнитивный шум, чтобы пользователи могли сосредоточиться на обсуждении и совместном контенте.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-275">Teams meetings are optimized for dark mode to help reduce visual and cognitive noise so users can focus on the discussion and shared content.</span></span> <span data-ttu-id="d6bdd-276">Узнайте об использовании <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">маркеров цвета (fluent UI).</a></span><span class="sxs-lookup"><span data-stu-id="d6bdd-276">Learn about using <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a>.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-dont.png" alt-text="Пример, показывающий расширение собрания с темой по умолчанию (светлая)." border="false":::

#### <a name="dont-hard-code-hex-values"></a><span data-ttu-id="d6bdd-278">Don't: Hard code hex values</span><span class="sxs-lookup"><span data-stu-id="d6bdd-278">Don't: Hard code hex values</span></span>

<span data-ttu-id="d6bdd-279">Если вы не используете маркеры Teams цвета, ваши проекты будут менее масштабируемыми и у вас будет больше времени для управления.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-279">If you don’t use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::

### <a name="navigation"></a><span data-ttu-id="d6bdd-280">Навигация</span><span class="sxs-lookup"><span data-stu-id="d6bdd-280">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-do.png" alt-text="Пример, показывающий расширение собрания с кнопкой &quot;Назад&quot;." border="false":::

#### <a name="do-have-a-back-button"></a><span data-ttu-id="d6bdd-282">Do: Есть кнопка "Назад"</span><span class="sxs-lookup"><span data-stu-id="d6bdd-282">Do: Have a back button</span></span>

<span data-ttu-id="d6bdd-283">Если на вкладке на собрании имеется несколько уровней навигации, пользователи должны иметь возможность вернуться к своим предыдущим представлениям.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-283">If you have more than one layer of navigation in an in-meeting tab, users must be able to go back to their previous views.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-dont.png" alt-text="Пример, показывающий расширение собрания с двумя кнопками увольнения." border="false":::

#### <a name="dont-include-another-dismiss-button"></a><span data-ttu-id="d6bdd-285">Не: включи еще одну кнопку увольнения</span><span class="sxs-lookup"><span data-stu-id="d6bdd-285">Don't: Include another dismiss button</span></span>

<span data-ttu-id="d6bdd-286">Предоставление возможности закрыть содержимое вкладки в собрании может вызвать проблемы, так как в загонах уже есть кнопка, чтобы отклонять сам вкладку в собрании.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-286">Providing an option to close in-meeting tab content may cause issues since there’s already a button in the header to dismiss the in-meeting tab itself.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-caution.png" alt-text="Пример, показывающий модули (или модули задач) в вкладке на собрании." border="false":::

#### <a name="caution-avoid-modals-within-the-in-meeting-tab"></a><span data-ttu-id="d6bdd-288">Внимание. Избегайте модалов в вкладке в собрании</span><span class="sxs-lookup"><span data-stu-id="d6bdd-288">Caution: Avoid modals within the in-meeting tab</span></span>

<span data-ttu-id="d6bdd-289">Модули (также известные как модули задач) на уже узкой вкладке в собрании могут обернуть содержимое и скрыть его.</span><span class="sxs-lookup"><span data-stu-id="d6bdd-289">Modals (also known as task modules) in the already narrow in-meeting tab might wrap and obscure the content.</span></span>

   :::column-end:::
:::row-end:::
