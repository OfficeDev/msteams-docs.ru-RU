---
title: Проектирование расширения собрания
author: heath-hamilton
description: Узнайте, как разрабатывать приложения на Teams собраниях и получить Microsoft Teams пользовательского интерфейса.
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
# <a name="designing-your-microsoft-teams-meeting-extension"></a><span data-ttu-id="d16b9-103">Проектирование Microsoft Teams собрания</span><span class="sxs-lookup"><span data-stu-id="d16b9-103">Designing your Microsoft Teams meeting extension</span></span>

<span data-ttu-id="d16b9-104">Вы можете создавать приложения, чтобы сделать собрания более продуктивными.</span><span class="sxs-lookup"><span data-stu-id="d16b9-104">You can create apps to make meetings more productive.</span></span> <span data-ttu-id="d16b9-105">Например, попросите людей заполнить опрос во время звонка или отправить быстрое напоминание, которое не прерывает поток собрания.</span><span class="sxs-lookup"><span data-stu-id="d16b9-105">For example, ask people to complete a survey during a call or send a quick reminder that doesn’t interrupt the flow of the meeting.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="d16b9-106">Комплект разработчика для пользовательского интерфейса Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="d16b9-106">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="d16b9-107">Более полные рекомендации по проектированию, включая элементы, которые можно захватить и изменить по мере необходимости, можно найти в Microsoft Teams пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="d16b9-107">You can find more comprehensive design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d16b9-108">Получить комплект разработчика для пользовательского интерфейса Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="d16b9-108">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-meeting-extension"></a><span data-ttu-id="d16b9-109">Добавление расширения собрания</span><span class="sxs-lookup"><span data-stu-id="d16b9-109">Add a meeting extension</span></span>

<span data-ttu-id="d16b9-110">Можно добавить продление собрания до и во время собраний.</span><span class="sxs-lookup"><span data-stu-id="d16b9-110">You can add a meeting extension before and during meetings.</span></span> <span data-ttu-id="d16b9-111">Вы также можете добавить приложение для конкретной встречи непосредственно из Teams (AppSource).</span><span class="sxs-lookup"><span data-stu-id="d16b9-111">You also can add an app for a specific meeting directly from the Teams store (AppSource).</span></span>

### <a name="add-before-a-meeting"></a><span data-ttu-id="d16b9-112">Добавить перед собранием</span><span class="sxs-lookup"><span data-stu-id="d16b9-112">Add before a meeting</span></span>

<span data-ttu-id="d16b9-113">В деталях собрания выберите **Добавить вкладку, чтобы** открыть вылет приложения и найти приложения, оптимизированные для собраний.</span><span class="sxs-lookup"><span data-stu-id="d16b9-113">In the meeting details, select **Add a tab +** to open the app flyout and find apps optimized for meetings.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/add-before-meeting.png" alt-text="Пример показывает, как добавить продление собрания перед собранием." border="false":::

### <a name="add-during-a-meeting"></a><span data-ttu-id="d16b9-115">Добавить во время собрания</span><span class="sxs-lookup"><span data-stu-id="d16b9-115">Add during a meeting</span></span>

На собрании выберите **больше добавить** приложение :::image type="icon" source="../../assets/icons/teams-client-more.png":::  >  **и выбрать** нужное приложение.

:::image type="content" source="../../assets/images/apps-in-meetings/add-during-meeting.png" alt-text="Пример показывает, как добавить расширение собрания во время собрания." border="false":::

## <a name="before-a-meeting"></a><span data-ttu-id="d16b9-118">Перед собранием</span><span class="sxs-lookup"><span data-stu-id="d16b9-118">Before a meeting</span></span>

<span data-ttu-id="d16b9-119">Перед собранием можно добавить содержимое во вкладку. В следующем примере показан проект опроса, на который люди ответят во время звонка.</span><span class="sxs-lookup"><span data-stu-id="d16b9-119">Prior to your meeting, you can add content in the tab. The following example shows a draft survey question that people will answer during the call.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/before-meeting-tab.png" alt-text="Пример показывает, как использовать содержимое в деталях собрания перед вызовом." border="false":::

### <a name="anatomy-meeting-tab-before-and-after-meetings"></a><span data-ttu-id="d16b9-121">Анатомия: Вкладка собрания (до и после встреч)</span><span class="sxs-lookup"><span data-stu-id="d16b9-121">Anatomy: Meeting tab (before and after meetings)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/meeting-details-tab-anatomy.png" alt-text="Пример показывает структурную анатомию вкладки собрания до и после собрания." border="false":::

|<span data-ttu-id="d16b9-123">Счетчик</span><span class="sxs-lookup"><span data-stu-id="d16b9-123">Counter</span></span>|<span data-ttu-id="d16b9-124">Описание</span><span class="sxs-lookup"><span data-stu-id="d16b9-124">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="d16b9-125">1</span><span class="sxs-lookup"><span data-stu-id="d16b9-125">1</span></span>|<span data-ttu-id="d16b9-126">**Название вкладки**: Навигационный ярлык для вкладки.</span><span class="sxs-lookup"><span data-stu-id="d16b9-126">**Tab name**: Navigation label for your tab.</span></span>|
|<span data-ttu-id="d16b9-127">2</span><span class="sxs-lookup"><span data-stu-id="d16b9-127">2</span></span>|<span data-ttu-id="d16b9-128">**Переполняем** вкладок: открывается вкладка действий, таких как переименование и удаление.</span><span class="sxs-lookup"><span data-stu-id="d16b9-128">**Tab overflow**: Opens tab actions, such as rename and remove.</span></span>|
|<span data-ttu-id="d16b9-129">3</span><span class="sxs-lookup"><span data-stu-id="d16b9-129">3</span></span>|<span data-ttu-id="d16b9-130">**iframe**: Отображает содержимое приложения.</span><span class="sxs-lookup"><span data-stu-id="d16b9-130">**iframe**: Displays your app content.</span></span>|

### <a name="designing-with-ui-templates"></a><span data-ttu-id="d16b9-131">Проектирование с шаблонами пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="d16b9-131">Designing with UI templates</span></span>

<span data-ttu-id="d16b9-132">Используйте один из следующих шаблонов Teams пользовательского интерфейса, чтобы помочь спроектировать вкладку собрания:</span><span class="sxs-lookup"><span data-stu-id="d16b9-132">Use one of the following Teams UI templates to help design your meeting tab:</span></span>

* <span data-ttu-id="d16b9-133">[Список](../../concepts/design/design-teams-app-ui-templates.md#list): Списки могут отображать связанные элементы в сканируемом формате и позволяют пользователям принимать меры по всему списку или отдельным элементам.</span><span class="sxs-lookup"><span data-stu-id="d16b9-133">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="d16b9-134">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): Целевая доска, иногда называемая доска kanban или плавательные дорожки, представляет собой набор карт, часто используемых для отслеживания состояния рабочих предметов или билетов.</span><span class="sxs-lookup"><span data-stu-id="d16b9-134">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="d16b9-135">[Панель мониторинга](../../concepts/design/design-teams-app-ui-templates.md#dashboard): Панель мониторинга — это холст, содержащий несколько карт, которые обеспечивают обзор данных или содержимого.</span><span class="sxs-lookup"><span data-stu-id="d16b9-135">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="d16b9-136">[Форма](../../concepts/design/design-teams-app-ui-templates.md#form): Формы для сбора, проверки и отправки пользовательского ввода структурированным способом.</span><span class="sxs-lookup"><span data-stu-id="d16b9-136">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="d16b9-137">[Пустое состояние](../../concepts/design/design-teams-app-ui-templates.md#empty-state): Пустой шаблон состояния может быть использован для многих сценариев, включая войти в него, первый запуск, сообщения об ошибках и многое другое.</span><span class="sxs-lookup"><span data-stu-id="d16b9-137">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="d16b9-138">[Левый навигатор](../../concepts/design/design-teams-app-ui-templates.md#left-nav): Левый шаблон навигации может помочь, если ваша вкладка требует некоторой навигации.</span><span class="sxs-lookup"><span data-stu-id="d16b9-138">[Left nav](../../concepts/design/design-teams-app-ui-templates.md#left-nav): The left nav template can help if your tab requires some navigation.</span></span> <span data-ttu-id="d16b9-139">Как правило, следует с минимумом следить за навигацией.</span><span class="sxs-lookup"><span data-stu-id="d16b9-139">In general, you should keep tab navigation to a minimum.</span></span>

## <a name="use-an-in-meeting-tab"></a><span data-ttu-id="d16b9-140">Использование вкладки «Встреча»</span><span class="sxs-lookup"><span data-stu-id="d16b9-140">Use an in-meeting tab</span></span>

<span data-ttu-id="d16b9-141">Вкладка встречи — это холст для расширения совместной работы во время собраний.</span><span class="sxs-lookup"><span data-stu-id="d16b9-141">The in-meeting tab is a canvas for augmenting collaboration during meetings.</span></span> <span data-ttu-id="d16b9-142">Участники могут видеть и взаимодействовать с контентом приложения в специальном пространстве за пределами стадии собрания с помощью общих или ролевых представлений.</span><span class="sxs-lookup"><span data-stu-id="d16b9-142">Attendees can see and interact with app content in a dedicated space outside the meeting stage through shared or role-based views.</span></span>

### <a name="use-cases"></a><span data-ttu-id="d16b9-143">Варианты использования</span><span class="sxs-lookup"><span data-stu-id="d16b9-143">Use cases</span></span>

<span data-ttu-id="d16b9-144">Люди могут использовать вкладку на собрании для:</span><span class="sxs-lookup"><span data-stu-id="d16b9-144">People might use the in-meeting tab to:</span></span>

* <span data-ttu-id="d16b9-145">Предоставьте подробную обратную связь.</span><span class="sxs-lookup"><span data-stu-id="d16b9-145">Provide detailed feedback.</span></span> <span data-ttu-id="d16b9-146">Например, оцените кандидата на работу.</span><span class="sxs-lookup"><span data-stu-id="d16b9-146">For example, evaluate a job candidate.</span></span>
* <span data-ttu-id="d16b9-147">Создайте элемент опроса, опроса или задачи для участников собрания.</span><span class="sxs-lookup"><span data-stu-id="d16b9-147">Create a poll, survey, or task item for the meeting participants.</span></span>
* <span data-ttu-id="d16b9-148">Отображение заметок, имеющих отношение к собранию.</span><span class="sxs-lookup"><span data-stu-id="d16b9-148">Display notes relevant to the meeting.</span></span> <span data-ttu-id="d16b9-149">Например, информация о лидере продаж.</span><span class="sxs-lookup"><span data-stu-id="d16b9-149">For example, information about a sales lead.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-tab.png" alt-text="Пример показывает, как можно представить содержимое опроса во вкладке &quot;Встреча&quot;." border="false":::

### <a name="anatomy-in-meeting-tab"></a><span data-ttu-id="d16b9-151">Анатомия: Вкладка встречи</span><span class="sxs-lookup"><span data-stu-id="d16b9-151">Anatomy: In-meeting tab</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-anatomy.png" alt-text="Пример показывает структурную анатомию вкладки в собрании." border="false":::

|<span data-ttu-id="d16b9-153">Счетчик</span><span class="sxs-lookup"><span data-stu-id="d16b9-153">Counter</span></span>|<span data-ttu-id="d16b9-154">Описание</span><span class="sxs-lookup"><span data-stu-id="d16b9-154">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="d16b9-155">1</span><span class="sxs-lookup"><span data-stu-id="d16b9-155">1</span></span>|<span data-ttu-id="d16b9-156">**Значок приложения (выбранный)**: 16-пиксельный прозрачный логотип приложения.</span><span class="sxs-lookup"><span data-stu-id="d16b9-156">**App icon (selected)**: 16-pixel transparent app logo.</span></span>|
|<span data-ttu-id="d16b9-157">2</span><span class="sxs-lookup"><span data-stu-id="d16b9-157">2</span></span>|<span data-ttu-id="d16b9-158">**Имя приложения**</span><span class="sxs-lookup"><span data-stu-id="d16b9-158">**App name**</span></span>|
|<span data-ttu-id="d16b9-159">3</span><span class="sxs-lookup"><span data-stu-id="d16b9-159">3</span></span>|<span data-ttu-id="d16b9-160">**Заголовок**: Включает имя приложения.</span><span class="sxs-lookup"><span data-stu-id="d16b9-160">**Header**: Includes your app name.</span></span>|
|<span data-ttu-id="d16b9-161">4 </span><span class="sxs-lookup"><span data-stu-id="d16b9-161">4</span></span>|<span data-ttu-id="d16b9-162">**Кнопка закрытия**: Отклоняет вкладку. Всегда используйте верхнюю правую близкую иконку вместо действия в подножке.</span><span class="sxs-lookup"><span data-stu-id="d16b9-162">**Close button**: Dismisses the tab. Always use the upper-right close icon instead of an action in the footer.</span></span>|
|<span data-ttu-id="d16b9-163">5 </span><span class="sxs-lookup"><span data-stu-id="d16b9-163">5</span></span>|<span data-ttu-id="d16b9-164">**Бар уведомлений**: Предупреждения об ошибках отображаются прямо под заголовком и нажимают содержимое iframe вниз на 20 пикселей.</span><span class="sxs-lookup"><span data-stu-id="d16b9-164">**Notification bar**: Error alerts display directly below the header and push the iframe content down by 20 pixels.</span></span>|
|<span data-ttu-id="d16b9-165">6 </span><span class="sxs-lookup"><span data-stu-id="d16b9-165">6</span></span>|<span data-ttu-id="d16b9-166">**iframe**: Отображает содержимое приложения.</span><span class="sxs-lookup"><span data-stu-id="d16b9-166">**iframe**: Displays your app content.</span></span>|

### <a name="spacing"></a><span data-ttu-id="d16b9-167">Интервал</span><span class="sxs-lookup"><span data-stu-id="d16b9-167">Spacing</span></span>

<span data-ttu-id="d16b9-168">Оптимизируйте вкладку в собрании, чтобы соответствовать от края до края в области iframe шириной 280 пикселей.</span><span class="sxs-lookup"><span data-stu-id="d16b9-168">Optimize your in-meeting tab to fit edge-to-edge within the 280 pixel-wide iframe area.</span></span> <span data-ttu-id="d16b9-169">Есть 20 пикселей обивка на левой и правой сторонах iframe и между заголовком вкладки.</span><span class="sxs-lookup"><span data-stu-id="d16b9-169">There are 20 pixels of padding on the left and right sides of the iframe and between the tab header.</span></span> <span data-ttu-id="d16b9-170">iframe полна кровотечения в нижней части вкладки.</span><span class="sxs-lookup"><span data-stu-id="d16b9-170">The iframe is full bleed to the bottom of the tab.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-spacing.png" alt-text="Пример показывает размеры интервалов вкладок во встрече." border="false":::

### <a name="scrolling"></a><span data-ttu-id="d16b9-172">прокрутка</span><span class="sxs-lookup"><span data-stu-id="d16b9-172">Scrolling</span></span>

<span data-ttu-id="d16b9-173">Содержимое Iframe должно прокручиваться вертикально.</span><span class="sxs-lookup"><span data-stu-id="d16b9-173">Iframe contents should scroll vertically.</span></span> <span data-ttu-id="d16b9-174">Вы можете видеть только содержимое, в которое вы прокрутили (ничего выше или ниже).</span><span class="sxs-lookup"><span data-stu-id="d16b9-174">You can only see the content you've scrolled to (nothing above or below).</span></span> <span data-ttu-id="d16b9-175">Прокрутка является частью содержимого iframe.</span><span class="sxs-lookup"><span data-stu-id="d16b9-175">The scrollbar is part of the iframe content.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-scrolling.png" alt-text="Пример показывает, как прокручивается вкладка в собрании." border="false":::

### <a name="navigation"></a><span data-ttu-id="d16b9-177">Навигация</span><span class="sxs-lookup"><span data-stu-id="d16b9-177">Navigation</span></span>

<span data-ttu-id="d16b9-178">Для сценариев с навигационными слоями или тяжелым содержанием мы рекомендуем разрешить пользователям переходить на вторичный слой.</span><span class="sxs-lookup"><span data-stu-id="d16b9-178">For scenarios with navigation layers or heavy content, we recommend allowing users to navigate to a secondary layer.</span></span> <span data-ttu-id="d16b9-179">Пользователи должны иметь возможность вернуться к предыдущему уровеньу.</span><span class="sxs-lookup"><span data-stu-id="d16b9-179">Users must be able to go back to the previous layer.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav.png" alt-text="Пример показывает во встрече навигацию." border="false":::

## <a name="use-an-in-meeting-dialog"></a><span data-ttu-id="d16b9-181">Используйте диалог на встрече</span><span class="sxs-lookup"><span data-stu-id="d16b9-181">Use an in-meeting dialog</span></span>

<span data-ttu-id="d16b9-182">Диалоги на встрече отображаются на Teams собрания.</span><span class="sxs-lookup"><span data-stu-id="d16b9-182">In-meeting dialogs display on the Teams meeting stage.</span></span> <span data-ttu-id="d16b9-183">Они требуют внимания, подтверждения или взаимодействия пользователя, но являются тонкими и не прерывают встречу.</span><span class="sxs-lookup"><span data-stu-id="d16b9-183">They require a user's attention, confirmation, or interaction but are subtle and don't interrupt the meeting.</span></span> <span data-ttu-id="d16b9-184">Вы должны использовать их экономно и для сценариев, которые являются легкими и ориентированными на задачи.</span><span class="sxs-lookup"><span data-stu-id="d16b9-184">You should use these sparingly and for scenarios that are light and task oriented.</span></span>

### <a name="use-cases"></a><span data-ttu-id="d16b9-185">Варианты использования</span><span class="sxs-lookup"><span data-stu-id="d16b9-185">Use cases</span></span>

<span data-ttu-id="d16b9-186">Диалоги на собрании запускаются пользователем (например, организатором собрания), который может захотеть, чтобы участники:</span><span class="sxs-lookup"><span data-stu-id="d16b9-186">In-meeting dialogs are triggered by a user (such as the meeting organizer) who might want participants to:</span></span>

* <span data-ttu-id="d16b9-187">Предоставьте краткую обратную связь</span><span class="sxs-lookup"><span data-stu-id="d16b9-187">Provide brief feedback</span></span>
* <span data-ttu-id="d16b9-188">Краткое обследование или опрос</span><span class="sxs-lookup"><span data-stu-id="d16b9-188">Take a short survey or poll</span></span>
* <span data-ttu-id="d16b9-189">Отправить утверждения</span><span class="sxs-lookup"><span data-stu-id="d16b9-189">Submit approvals</span></span>
* <span data-ttu-id="d16b9-190">Получай напоминания</span><span class="sxs-lookup"><span data-stu-id="d16b9-190">Get reminders</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-dialog.png" alt-text="Пример показывает, как можно использовать диалог на собрании." border="false":::

### <a name="anatomy-in-meeting-dialog"></a><span data-ttu-id="d16b9-192">Анатомия: Диалог на встрече</span><span class="sxs-lookup"><span data-stu-id="d16b9-192">Anatomy: In-meeting dialog</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-anatomy.png" alt-text="Пример показывает структурную анатомию диалога на встрече." border="false":::

|<span data-ttu-id="d16b9-194">Счетчик</span><span class="sxs-lookup"><span data-stu-id="d16b9-194">Counter</span></span>|<span data-ttu-id="d16b9-195">Описание</span><span class="sxs-lookup"><span data-stu-id="d16b9-195">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="d16b9-196">1</span><span class="sxs-lookup"><span data-stu-id="d16b9-196">1</span></span>|<span data-ttu-id="d16b9-197">**Заголовок**: Включает значок приложения, имя, строку действия и близкий значок.</span><span class="sxs-lookup"><span data-stu-id="d16b9-197">**Header**: Includes app icon, name, action string, and close icon.</span></span>|
|<span data-ttu-id="d16b9-198">2</span><span class="sxs-lookup"><span data-stu-id="d16b9-198">2</span></span>|<span data-ttu-id="d16b9-199">**iframe**: Отображает содержимое приложения.</span><span class="sxs-lookup"><span data-stu-id="d16b9-199">**iframe**: Displays your app content.</span></span>|

### <a name="anatomy-in-meeting-dialog-header"></a><span data-ttu-id="d16b9-200">Анатомия: Заголовок диалога на встрече</span><span class="sxs-lookup"><span data-stu-id="d16b9-200">Anatomy: In-meeting dialog header</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-header-anatomy.png" alt-text="Пример показывает структурную анатомию заголовка диалога на собрании." border="false":::

<span data-ttu-id="d16b9-202">Существует два варианта заголовка.</span><span class="sxs-lookup"><span data-stu-id="d16b9-202">There are two header variants.</span></span> <span data-ttu-id="d16b9-203">Когда это возможно, используйте вариант с аватаром, чтобы укрепить, что диалог исходит от человека.</span><span class="sxs-lookup"><span data-stu-id="d16b9-203">When possible, use the variant with the avatar to reinforce that the dialog is coming from a person.</span></span>

|<span data-ttu-id="d16b9-204">Счетчик</span><span class="sxs-lookup"><span data-stu-id="d16b9-204">Counter</span></span>|<span data-ttu-id="d16b9-205">Описание</span><span class="sxs-lookup"><span data-stu-id="d16b9-205">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="d16b9-206">1</span><span class="sxs-lookup"><span data-stu-id="d16b9-206">1</span></span>|<span data-ttu-id="d16b9-207">**Аватар**: Человек, который инициирует диалог на встрече.</span><span class="sxs-lookup"><span data-stu-id="d16b9-207">**Avatar**: Person who initiates the in-meeting dialog.</span></span>|
|<span data-ttu-id="d16b9-208">2</span><span class="sxs-lookup"><span data-stu-id="d16b9-208">2</span></span>|<span data-ttu-id="d16b9-209">**Значок приложения**</span><span class="sxs-lookup"><span data-stu-id="d16b9-209">**App icon**</span></span>|
|<span data-ttu-id="d16b9-210">3</span><span class="sxs-lookup"><span data-stu-id="d16b9-210">3</span></span>|<span data-ttu-id="d16b9-211">**Имя приложения**</span><span class="sxs-lookup"><span data-stu-id="d16b9-211">**App name**</span></span>|
|<span data-ttu-id="d16b9-212">4 </span><span class="sxs-lookup"><span data-stu-id="d16b9-212">4</span></span>|<span data-ttu-id="d16b9-213">**Закрыть кнопку**: Увольняет диалог.</span><span class="sxs-lookup"><span data-stu-id="d16b9-213">**Close button**: Dismisses the dialog.</span></span>|
|<span data-ttu-id="d16b9-214">5 </span><span class="sxs-lookup"><span data-stu-id="d16b9-214">5</span></span>|<span data-ttu-id="d16b9-215">**Строка действия**: Обычно описывает, кто инициировал диалог.</span><span class="sxs-lookup"><span data-stu-id="d16b9-215">**Action string**: Typically describes who initiated the dialog.</span></span>|

### <a name="responsive-behavior"></a><span data-ttu-id="d16b9-216">Адаптируемое поведение</span><span class="sxs-lookup"><span data-stu-id="d16b9-216">Responsive behavior</span></span>

<span data-ttu-id="d16b9-217">Диалоги на собраниях могут различаться по размеру для учета различных сценариев.</span><span class="sxs-lookup"><span data-stu-id="d16b9-217">In-meeting dialogs can vary in size to account for different scenarios.</span></span> <span data-ttu-id="d16b9-218">Убедитесь в том, чтобы поддерживать обивку и размеры компонентов.</span><span class="sxs-lookup"><span data-stu-id="d16b9-218">Make sure to maintain padding and component sizes.</span></span>

* <span data-ttu-id="d16b9-219">**Ширина**: Вы можете указать ширину iframe диалога в любом месте в пределах поддерживаемого диапазона размеров.</span><span class="sxs-lookup"><span data-stu-id="d16b9-219">**Width**: You can specify the width of the dialog's iframe anywhere within the supported size range.</span></span>
* <span data-ttu-id="d16b9-220">**Высота**: Вы можете указать высоту iframe диалога в любом месте в пределах поддерживаемого диапазона размеров.</span><span class="sxs-lookup"><span data-stu-id="d16b9-220">**Height**: You can specify the height of the dialog's iframe anywhere within the supported size range.</span></span> <span data-ttu-id="d16b9-221">Вы также можете разрешить пользователям прокрутку вертикально, если содержимое приложения превышает максимальную высоту.</span><span class="sxs-lookup"><span data-stu-id="d16b9-221">You also can allow users to scroll vertically if your app content exceeds the maximum height.</span></span>

<span data-ttu-id="d16b9-222">Для реализации укажите ширину и высоту с помощью [`externalResourceUrl`](~/apps-in-teams-meetings/create-apps-for-teams-meetings.md#notificationsignal-api) ключа.</span><span class="sxs-lookup"><span data-stu-id="d16b9-222">To implement, specify the width and height using the [`externalResourceUrl`](~/apps-in-teams-meetings/create-apps-for-teams-meetings.md#notificationsignal-api) key.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-responsive.png" alt-text="Пример показывает диалог на встрече. Ширина: Мин--280 пикселей (248 пикселей iframe). Макс--460 пикселей (428 пикселей iframe). Высота: 300 пикселей (iframe)." border="false":::

## <a name="after-a-meeting"></a><span data-ttu-id="d16b9-224">После собрания</span><span class="sxs-lookup"><span data-stu-id="d16b9-224">After a meeting</span></span>

<span data-ttu-id="d16b9-225">Вы можете вернуться к собранию после его окончания и просмотреть содержимое приложения.</span><span class="sxs-lookup"><span data-stu-id="d16b9-225">You can go back to a meeting after it ends and view app content.</span></span> <span data-ttu-id="d16b9-226">В этом примере организатор собрания может посмотреть на результаты опроса во **вкладке Contoso.** (Примечание: С точки зрения проектирования нет никакой разницы между вкладкой до и после собрания).)</span><span class="sxs-lookup"><span data-stu-id="d16b9-226">In this example, the meeting organizer can look at poll results in the **Contoso** tab. (Note: From a design standpoint, there's no difference between a the pre- and post-meeting tab experience.)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/post-meeting-experience.png" alt-text="На примере иллюстрации показана вкладка после собрания." border="false":::

## <a name="best-practices"></a><span data-ttu-id="d16b9-228">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="d16b9-228">Best practices</span></span>

<span data-ttu-id="d16b9-229">Используйте эти рекомендации для создания качественного приложения.</span><span class="sxs-lookup"><span data-stu-id="d16b9-229">Use these recommendations to create a quality app experience.</span></span>

### <a name="interactions"></a><span data-ttu-id="d16b9-230">Взаимодействия</span><span class="sxs-lookup"><span data-stu-id="d16b9-230">Interactions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-do.png" alt-text="Пример, показывающий, как ограничить количество взаимодействий." border="false":::

#### <a name="do-limit-the-number-of-interactions"></a><span data-ttu-id="d16b9-232">У: Ограничьте количество взаимодействий</span><span class="sxs-lookup"><span data-stu-id="d16b9-232">Do: Limit the number of interactions</span></span>

<span data-ttu-id="d16b9-233">Для диалогов на собрании удалите ненужный контент, который не поможет пользователям быстро что-то сделать.</span><span class="sxs-lookup"><span data-stu-id="d16b9-233">For in-meeting dialogs, remove unnecessary content that doesn't help users accomplish something quickly.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-dont.png" alt-text="Пример, показывающий, как не вводить ненужные элементы." border="false":::

#### <a name="dont-introduce-unnecessary-elements"></a><span data-ttu-id="d16b9-235">Не: Ввеся ненужные элементы</span><span class="sxs-lookup"><span data-stu-id="d16b9-235">Don't: Introduce unnecessary elements</span></span>

<span data-ttu-id="d16b9-236">Один диалог на встрече с несколькими взаимодействиями может отвлечь от вызова.</span><span class="sxs-lookup"><span data-stu-id="d16b9-236">A single in-meeting dialog with multiple interactions can distract from the call.</span></span>

   :::column-end:::
:::row-end:::

### <a name="layout"></a><span data-ttu-id="d16b9-237">Макет</span><span class="sxs-lookup"><span data-stu-id="d16b9-237">Layout</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-do.png" alt-text="Пример, показывающий, как следует использовать макет диалога с одной колонкой." border="false":::

#### <a name="do-use-a-single-column-dialog-layout"></a><span data-ttu-id="d16b9-239">У: Используйте одноко колготок диалог макет</span><span class="sxs-lookup"><span data-stu-id="d16b9-239">Do: Use a single-column dialog layout</span></span>

<span data-ttu-id="d16b9-240">Поскольку диалоги находятся в центре стадии собрания, завершение задачи должно быть быстрым и простым, чтобы избежать разочарования пользователей.</span><span class="sxs-lookup"><span data-stu-id="d16b9-240">Since the dialogs are at the center of the meeting stage, task completion should be fast and simple to avoid user frustration.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-dont.png" alt-text="Пример, показывающий, что не следует загромождать пространство расширения собрания." border="false":::

#### <a name="dont-clutter-the-space"></a><span data-ttu-id="d16b9-242">Не: Загромождать пространство</span><span class="sxs-lookup"><span data-stu-id="d16b9-242">Don't: Clutter the space</span></span>

<span data-ttu-id="d16b9-243">Плотный или чрезмерно структурированный контент может отвлекать и подавлять, особенно во время собрания.</span><span class="sxs-lookup"><span data-stu-id="d16b9-243">Dense or overly structured content can be distracting and overwhelming, especially during a meeting.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-do.png" alt-text="Пример, показывающий макет вкладки с одной колонкой." border="false":::

#### <a name="do-use-a-single-column-tab-layout"></a><span data-ttu-id="d16b9-245">У: Используйте макет вкладки с одной колонкой</span><span class="sxs-lookup"><span data-stu-id="d16b9-245">Do: Use a single-column tab layout</span></span>

<span data-ttu-id="d16b9-246">Учитывая узкий характер вкладки в заседании, мы настоятельно рекомендуем отображать содержимое в одном столбце.</span><span class="sxs-lookup"><span data-stu-id="d16b9-246">Given the in-meeting tab's narrow nature, we strongly recommend displaying the contents in a single column.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-dont.png" alt-text="Пример отображения вкладки с несколькими столбцами." border="false":::

#### <a name="dont-use-multiple-columns"></a><span data-ttu-id="d16b9-248">Не: Используйте несколько столбцов</span><span class="sxs-lookup"><span data-stu-id="d16b9-248">Don't: Use multiple columns</span></span>

<span data-ttu-id="d16b9-249">Из-за ограниченного пространства вкладки в собрании макеты с более чем одним столбецом не рекомендуются.</span><span class="sxs-lookup"><span data-stu-id="d16b9-249">Due to the limited space of the in-meeting tab, layouts with more than one column aren’t recommended.</span></span>

   :::column-end:::
:::row-end:::

### <a name="controls"></a><span data-ttu-id="d16b9-250">Элементы управления</span><span class="sxs-lookup"><span data-stu-id="d16b9-250">Controls</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-do.png" alt-text="Пример, показывающий, как правильно выровнять основные элементы управления." border="false":::

#### <a name="do-right-align-the-primary-action"></a><span data-ttu-id="d16b9-252">Do: Право выровнять первичное действие</span><span class="sxs-lookup"><span data-stu-id="d16b9-252">Do: Right align the primary action</span></span>

<span data-ttu-id="d16b9-253">Рекомендуем позиционировать наиболее визуально тяжелые действия в нужном месте.</span><span class="sxs-lookup"><span data-stu-id="d16b9-253">We recommend positioning the most visually heavy action to the right-most location.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-dont.png" alt-text="Пример, показывающий, как не следует левая выравнивание основных элементов управления." border="false":::

#### <a name="dont-left-or-center-align-actions"></a><span data-ttu-id="d16b9-255">Не: Левые или центральные действия выравнивания</span><span class="sxs-lookup"><span data-stu-id="d16b9-255">Don't: Left or center align actions</span></span>

<span data-ttu-id="d16b9-256">Это отклоняется от стандартной Teams для размещения элементов управления в диалоге и может в конфликте с диалогом за верхним.</span><span class="sxs-lookup"><span data-stu-id="d16b9-256">This deviates from the standard Teams pattern for control placement in a dialog and may conflict with a dialog behind the top one.</span></span>

   :::column-end:::
:::row-end:::

### <a name="scroll"></a><span data-ttu-id="d16b9-257">Прокрутка</span><span class="sxs-lookup"><span data-stu-id="d16b9-257">Scroll</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-do.png" alt-text="Пример, показывающий вертикальную прокрутку во вкладке &quot;Встреча&quot;." border="false":::

#### <a name="do-scroll-vertically"></a><span data-ttu-id="d16b9-259">У: Прокрутите вертикально</span><span class="sxs-lookup"><span data-stu-id="d16b9-259">Do: Scroll vertically</span></span>

<span data-ttu-id="d16b9-260">Пользователи ожидают вертикальной прокрутки в Teams (и в других местах).</span><span class="sxs-lookup"><span data-stu-id="d16b9-260">Users expect vertical scrolling in Teams (and elsewhere).</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-dont.png" alt-text="Пример, показывающий горизонтальную прокрутку во вкладке &quot;Встреча&quot;." border="false":::

#### <a name="dont-scroll-horizontally"></a><span data-ttu-id="d16b9-262">Не: Прокрутите горизонтально</span><span class="sxs-lookup"><span data-stu-id="d16b9-262">Don't: Scroll horizontally</span></span>

<span data-ttu-id="d16b9-263">Горизонтальная прокрутка не является ожидаемым поведением в Teams.</span><span class="sxs-lookup"><span data-stu-id="d16b9-263">Horizontal scrolling isn’t an expected behavior in Teams.</span></span> <span data-ttu-id="d16b9-264">Другие полотна в среде собрания прокрутки по вертикали.</span><span class="sxs-lookup"><span data-stu-id="d16b9-264">Other canvases in the meeting environment scroll vertically.</span></span>

   :::column-end:::
:::row-end:::

### <a name="workflows"></a><span data-ttu-id="d16b9-265">Рабочие процессы</span><span class="sxs-lookup"><span data-stu-id="d16b9-265">Workflows</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-workflow-do.png" alt-text="Пример, показывающий сложный сценарий во вкладке &quot;Встреча&quot;." border="false":::

#### <a name="do-surface-complex-scenarios-in-the-in-meeting-tab"></a><span data-ttu-id="d16b9-267">У: Сценарии поверхностного комплекса во вкладке "Встреча"</span><span class="sxs-lookup"><span data-stu-id="d16b9-267">Do: Surface complex scenarios in the in-meeting tab</span></span>

<span data-ttu-id="d16b9-268">Если ваше приложение включает в себя несколько задач, мы настоятельно рекомендуем использовать вкладку в собрании с макетом одной колонки.</span><span class="sxs-lookup"><span data-stu-id="d16b9-268">If your app includes multiple tasks, we strongly recommend using an in-meeting tab with a single-column layout.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-workflow-dont.png" alt-text="Пример, показывающий сложные сценарии в диалоге на встрече." border="false":::

#### <a name="dont-make-in-meeting-dialogs-complex"></a><span data-ttu-id="d16b9-270">Не: Сделать на встрече диалоги сложными</span><span class="sxs-lookup"><span data-stu-id="d16b9-270">Don't: Make in-meeting dialogs complex</span></span>

<span data-ttu-id="d16b9-271">Диалоги на встрече предназначены для краткого взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="d16b9-271">In-meeting dialogs are intended for brief interactions.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="d16b9-272">Темы</span><span class="sxs-lookup"><span data-stu-id="d16b9-272">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-do.png" alt-text="Пример, показывающий расширение собрания с темной темой." border="false":::

#### <a name="do-use-teams-color-tokens"></a><span data-ttu-id="d16b9-274">У: Используйте Teams цветные жетоны</span><span class="sxs-lookup"><span data-stu-id="d16b9-274">Do: Use Teams color tokens</span></span>

<span data-ttu-id="d16b9-275">Teams оптимизированы для темного режима, чтобы помочь уменьшить визуальный и когнитивный шум, чтобы пользователи могли сосредоточиться на обсуждении и общем контенте.</span><span class="sxs-lookup"><span data-stu-id="d16b9-275">Teams meetings are optimized for dark mode to help reduce visual and cognitive noise so users can focus on the discussion and shared content.</span></span> <span data-ttu-id="d16b9-276">Узнайте об использовании <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">цветовых жетонов (Fluent UI).</a></span><span class="sxs-lookup"><span data-stu-id="d16b9-276">Learn about using <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a>.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-dont.png" alt-text="Пример, показывающий расширение собрания с темой по умолчанию (свет)." border="false":::

#### <a name="dont-hard-code-hex-values"></a><span data-ttu-id="d16b9-278">Не: Жесткий код hex значения</span><span class="sxs-lookup"><span data-stu-id="d16b9-278">Don't: Hard code hex values</span></span>

<span data-ttu-id="d16b9-279">Если вы не используете Teams, ваши проекты будут менее масштабируемыми и потребуется больше времени для управления.</span><span class="sxs-lookup"><span data-stu-id="d16b9-279">If you don’t use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::

### <a name="navigation"></a><span data-ttu-id="d16b9-280">Навигация</span><span class="sxs-lookup"><span data-stu-id="d16b9-280">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-do.png" alt-text="Пример, показывающий расширение собрания с кнопкой &quot;Назад&quot;." border="false":::

#### <a name="do-have-a-back-button"></a><span data-ttu-id="d16b9-282">У: Иметь кнопку "Назад"</span><span class="sxs-lookup"><span data-stu-id="d16b9-282">Do: Have a back button</span></span>

<span data-ttu-id="d16b9-283">Если во вкладке собрания находится более одного уровня навигации, пользователи должны иметь возможность вернуться к прежним представлениям.</span><span class="sxs-lookup"><span data-stu-id="d16b9-283">If you have more than one layer of navigation in an in-meeting tab, users must be able to go back to their previous views.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-dont.png" alt-text="Пример, показывающий расширение собрания с двумя кнопками увольнения." border="false":::

#### <a name="dont-include-another-dismiss-button"></a><span data-ttu-id="d16b9-285">Не: Включите еще одну кнопку увольнения</span><span class="sxs-lookup"><span data-stu-id="d16b9-285">Don't: Include another dismiss button</span></span>

<span data-ttu-id="d16b9-286">Предоставление опции закрытия содержимого вкладки в заседании может вызвать проблемы, так как в заголовке уже есть кнопка для увольнения самой вкладки в собрании.</span><span class="sxs-lookup"><span data-stu-id="d16b9-286">Providing an option to close in-meeting tab content may cause issues since there’s already a button in the header to dismiss the in-meeting tab itself.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-caution.png" alt-text="Пример отображения модалов (или модулей задач) во вкладке &quot;Встреча&quot;." border="false":::

#### <a name="caution-avoid-modals-within-the-in-meeting-tab"></a><span data-ttu-id="d16b9-288">Внимание: Избегайте модалей в вкладке "Встреча"</span><span class="sxs-lookup"><span data-stu-id="d16b9-288">Caution: Avoid modals within the in-meeting tab</span></span>

<span data-ttu-id="d16b9-289">Модалы (также известные как модули задач) в и без того узкой вкладке в собрании могут обернуть и скрыть содержимое.</span><span class="sxs-lookup"><span data-stu-id="d16b9-289">Modals (also known as task modules) in the already narrow in-meeting tab might wrap and obscure the content.</span></span>

   :::column-end:::
:::row-end:::
