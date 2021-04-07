---
title: Проектирование расширения собрания
author: heath-hamilton
description: Узнайте, как создать приложения на собраниях Teams и получить набор пользовательского интерфейса Microsoft Teams.
ms.author: lajanuar
ms.topic: conceptual
ms.openlocfilehash: e4e7bb05fbc9717a4eb8323302d1a10eac4c77dd
ms.sourcegitcommit: f5ee3fa5ef6126d9bf845948d27d9067b3bbb994
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2021
ms.locfileid: "51596254"
---
# <a name="designing-your-microsoft-teams-meeting-extension"></a><span data-ttu-id="3cbbe-103">Разработка расширения собраний Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="3cbbe-103">Designing your Microsoft Teams meeting extension</span></span>

<span data-ttu-id="3cbbe-104">Вы можете создавать приложения, чтобы сделать собрания более продуктивными.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-104">You can create apps to make meetings more productive.</span></span> <span data-ttu-id="3cbbe-105">Например, попросите людей выполнить опрос во время вызова или отправить быстрое напоминание, которое не прерывает поток собрания.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-105">For example, ask people to complete a survey during a call or send a quick reminder that doesn’t interrupt the flow of the meeting.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="3cbbe-106">Набор пользовательского интерфейса Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="3cbbe-106">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="3cbbe-107">В наборе пользовательского интерфейса Microsoft Teams можно найти более исчерпывающие рекомендации по проектированию, в том числе элементы, которые можно захватить и изменить по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-107">You can find more comprehensive design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3cbbe-108">Получите набор пользовательского интерфейса Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="3cbbe-108">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-meeting-extension"></a><span data-ttu-id="3cbbe-109">Добавление расширения собрания</span><span class="sxs-lookup"><span data-stu-id="3cbbe-109">Add a meeting extension</span></span>

<span data-ttu-id="3cbbe-110">Вы можете добавить расширение собрания до и во время собраний.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-110">You can add a meeting extension before and during meetings.</span></span> <span data-ttu-id="3cbbe-111">Вы также можете добавить приложение для определенного собрания непосредственно из магазина Teams (AppSource).</span><span class="sxs-lookup"><span data-stu-id="3cbbe-111">You also can add an app for a specific meeting directly from the Teams store (AppSource).</span></span>

### <a name="add-before-a-meeting"></a><span data-ttu-id="3cbbe-112">Добавление перед собранием</span><span class="sxs-lookup"><span data-stu-id="3cbbe-112">Add before a meeting</span></span>

<span data-ttu-id="3cbbe-113">В сведениях о собрании выберите Добавить вкладку **+,** чтобы открыть вылет приложения и найти приложения, оптимизированные для собраний.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-113">In the meeting details, select **Add a tab +** to open the app flyout and find apps optimized for meetings.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/add-before-meeting.png" alt-text="В примере показано, как добавить расширение собрания перед собранием." border="false":::

### <a name="add-during-a-meeting"></a><span data-ttu-id="3cbbe-115">Добавление во время собрания</span><span class="sxs-lookup"><span data-stu-id="3cbbe-115">Add during a meeting</span></span>

На собрании выберите **дополнительные** :::image type="icon" source="../../assets/icons/teams-client-more.png":::  >  **добавления приложения** и выберите нужное приложение.

:::image type="content" source="../../assets/images/apps-in-meetings/add-during-meeting.png" alt-text="В примере показано, как добавить расширение собрания во время собрания." border="false":::

## <a name="before-a-meeting"></a><span data-ttu-id="3cbbe-118">Перед собранием</span><span class="sxs-lookup"><span data-stu-id="3cbbe-118">Before a meeting</span></span>

<span data-ttu-id="3cbbe-119">Перед собранием можно добавить содержимое на вкладке. В следующем примере показан проект опроса, на который люди ответят во время вызова.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-119">Prior to your meeting, you can add content in the tab. The following example shows a draft survey question that people will answer during the call.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/before-meeting-tab.png" alt-text="В примере показано, как приложение содержимым в сведениях о собрании перед вызовом." border="false":::

### <a name="anatomy-meeting-tab-before-and-after-meetings"></a><span data-ttu-id="3cbbe-121">Анатомия: вкладка "Собрание" (до и после собраний)</span><span class="sxs-lookup"><span data-stu-id="3cbbe-121">Anatomy: Meeting tab (before and after meetings)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/meeting-details-tab-anatomy.png" alt-text="В примере показана структурная анатомия вкладки собрания до и после собрания." border="false":::

|<span data-ttu-id="3cbbe-123">Счетчик</span><span class="sxs-lookup"><span data-stu-id="3cbbe-123">Counter</span></span>|<span data-ttu-id="3cbbe-124">Описание</span><span class="sxs-lookup"><span data-stu-id="3cbbe-124">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="3cbbe-125">1</span><span class="sxs-lookup"><span data-stu-id="3cbbe-125">1</span></span>|<span data-ttu-id="3cbbe-126">**Имя вкладки.** Метка навигации для вкладки.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-126">**Tab name**: Navigation label for your tab.</span></span>|
|<span data-ttu-id="3cbbe-127">2</span><span class="sxs-lookup"><span data-stu-id="3cbbe-127">2</span></span>|<span data-ttu-id="3cbbe-128">**Переполнение вкладки:** открывает действия вкладки, такие как переименование и удаление.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-128">**Tab overflow**: Opens tab actions, such as rename and remove.</span></span>|
|<span data-ttu-id="3cbbe-129">3</span><span class="sxs-lookup"><span data-stu-id="3cbbe-129">3</span></span>|<span data-ttu-id="3cbbe-130">**iframe:** отображает содержимое приложения.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-130">**iframe**: Displays your app content.</span></span>|

### <a name="designing-with-ui-templates"></a><span data-ttu-id="3cbbe-131">Проектирование с помощью шаблонов пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="3cbbe-131">Designing with UI templates</span></span>

<span data-ttu-id="3cbbe-132">Используйте один из следующих шаблонов пользовательского интерфейса Teams, чтобы помочь спроектировать вкладку собраний:</span><span class="sxs-lookup"><span data-stu-id="3cbbe-132">Use one of the following Teams UI templates to help design your meeting tab:</span></span>

* <span data-ttu-id="3cbbe-133">[Список.](../../concepts/design/design-teams-app-ui-templates.md#list)Списки могут отображать связанные элементы в сканируемых форматах и позволяют пользователям принимать меры по всему списку или отдельным пунктам.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-133">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="3cbbe-134">[Доска](../../concepts/design/design-teams-app-ui-templates.md#task-board)задач. Доска задач, иногда называемая канбанской или плавательные дорожки, — это коллекция карт, часто используемых для отслеживания состояния элементов или билетов.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-134">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="3cbbe-135">[Панель](../../concepts/design/design-teams-app-ui-templates.md#dashboard)мониторинга: панель мониторинга — это холст, содержащий несколько карт, которые предоставляют обзор данных или контента.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-135">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="3cbbe-136">[Form:](../../concepts/design/design-teams-app-ui-templates.md#form)Forms are for collecting, validating and submitting user input in a structured way.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-136">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="3cbbe-137">[Пустое](../../concepts/design/design-teams-app-ui-templates.md#empty-state)состояние. Пустой шаблон состояния можно использовать для многих сценариев, включая вход, первый запуск, сообщения об ошибках и многое другое.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-137">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="3cbbe-138">[Левый nav](../../concepts/design/design-teams-app-ui-templates.md#left-nav). Шаблон левого nav может помочь если ваша вкладка требует некоторой навигации.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-138">[Left nav](../../concepts/design/design-teams-app-ui-templates.md#left-nav): The left nav template can help if your tab requires some navigation.</span></span> <span data-ttu-id="3cbbe-139">В общем, вы должны сохранить навигацию вкладок до минимума.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-139">In general, you should keep tab navigation to a minimum.</span></span>

## <a name="use-an-in-meeting-tab"></a><span data-ttu-id="3cbbe-140">Использование вкладки в собрании</span><span class="sxs-lookup"><span data-stu-id="3cbbe-140">Use an in-meeting tab</span></span>

<span data-ttu-id="3cbbe-141">Вкладка на собрании — это холст для расширения совместной работы во время собраний.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-141">The in-meeting tab is a canvas for augmenting collaboration during meetings.</span></span> <span data-ttu-id="3cbbe-142">Участники могут видеть и взаимодействовать с контентом приложения в выделенном пространстве за пределами стадии собраний с помощью общих представлений или представлений на основе ролей.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-142">Attendees can see and interact with app content in a dedicated space outside the meeting stage through shared or role-based views.</span></span>

### <a name="use-cases"></a><span data-ttu-id="3cbbe-143">Варианты использования</span><span class="sxs-lookup"><span data-stu-id="3cbbe-143">Use cases</span></span>

<span data-ttu-id="3cbbe-144">Люди могут использовать вкладку на собрании, чтобы:</span><span class="sxs-lookup"><span data-stu-id="3cbbe-144">People might use the in-meeting tab to:</span></span>

* <span data-ttu-id="3cbbe-145">Предоставление подробных отзывов (например, оценка кандидата на работу)</span><span class="sxs-lookup"><span data-stu-id="3cbbe-145">Provide detailed feedback (for example, evaluate a job candidate)</span></span>
* <span data-ttu-id="3cbbe-146">Быстро создайте элемент опроса, опроса или задачи для участников собрания.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-146">Quickly create a poll, survey, or task item for the meeting participants</span></span>
* <span data-ttu-id="3cbbe-147">Отображение заметок, соответствующих собранию (например, сведения о лидере продаж)</span><span class="sxs-lookup"><span data-stu-id="3cbbe-147">Display notes relevant to the meeting (for example, information about a sales lead)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-tab.png" alt-text="В примере показано, как можно представить содержимое опроса на вкладке на собрании." border="false":::

### <a name="anatomy-in-meeting-tab"></a><span data-ttu-id="3cbbe-149">Anatomy: In-meeting tab</span><span class="sxs-lookup"><span data-stu-id="3cbbe-149">Anatomy: In-meeting tab</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-anatomy.png" alt-text="В примере показана структурная анатомия вкладки на собрании." border="false":::

|<span data-ttu-id="3cbbe-151">Счетчик</span><span class="sxs-lookup"><span data-stu-id="3cbbe-151">Counter</span></span>|<span data-ttu-id="3cbbe-152">Описание</span><span class="sxs-lookup"><span data-stu-id="3cbbe-152">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="3cbbe-153">1</span><span class="sxs-lookup"><span data-stu-id="3cbbe-153">1</span></span>|<span data-ttu-id="3cbbe-154">**Значок приложения (выбранный)**: 16-пиксельный прозрачный логотип приложения.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-154">**App icon (selected)**: 16-pixel transparent app logo.</span></span>|
|<span data-ttu-id="3cbbe-155">2</span><span class="sxs-lookup"><span data-stu-id="3cbbe-155">2</span></span>|<span data-ttu-id="3cbbe-156">**Имя приложения**</span><span class="sxs-lookup"><span data-stu-id="3cbbe-156">**App name**</span></span>|
|<span data-ttu-id="3cbbe-157">3</span><span class="sxs-lookup"><span data-stu-id="3cbbe-157">3</span></span>|<span data-ttu-id="3cbbe-158">**Заглавное** имя. Включает имя приложения.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-158">**Header**: Includes your app name.</span></span>|
|<span data-ttu-id="3cbbe-159">4 </span><span class="sxs-lookup"><span data-stu-id="3cbbe-159">4</span></span>|<span data-ttu-id="3cbbe-160">**Кнопка закрыть:** отклонять вкладку. Всегда используйте значок верхнего правого закрытия вместо действия в подножке.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-160">**Close button**: Dismisses the tab. Always use the upper-right close icon instead of an action in the footer.</span></span>|
|<span data-ttu-id="3cbbe-161">5 </span><span class="sxs-lookup"><span data-stu-id="3cbbe-161">5</span></span>|<span data-ttu-id="3cbbe-162">**Панели** уведомлений. Оповещения об ошибках отображаются непосредственно под заголовком и толкают содержимое iframe вниз на 20 пикселей.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-162">**Notification bar**: Error alerts display directly below the header and push the iframe content down by 20 pixels.</span></span>|
|<span data-ttu-id="3cbbe-163">6 </span><span class="sxs-lookup"><span data-stu-id="3cbbe-163">6</span></span>|<span data-ttu-id="3cbbe-164">**iframe:** отображает содержимое приложения.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-164">**iframe**: Displays your app content.</span></span>|

### <a name="spacing"></a><span data-ttu-id="3cbbe-165">Интервал</span><span class="sxs-lookup"><span data-stu-id="3cbbe-165">Spacing</span></span>

<span data-ttu-id="3cbbe-166">Оптимизируйте вкладку в собрании, чтобы поместиться по краям в области iframe шириной 280 пикселей.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-166">Optimize your in-meeting tab to fit edge-to-edge within the 280 pixel-wide iframe area.</span></span> <span data-ttu-id="3cbbe-167">На левой и правой сторонах iframe и между загонами вкладок имеется 20 пикселей.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-167">There are 20 pixels of padding on the left and right sides of the iframe and between the tab header.</span></span> <span data-ttu-id="3cbbe-168">Iframe полностью кровотока в нижней части вкладки.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-168">The iframe is full bleed to the bottom of the tab.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-spacing.png" alt-text="В примере показаны размеры интервала между вкладками в собрании." border="false":::

### <a name="scrolling"></a><span data-ttu-id="3cbbe-170">Прокрутка</span><span class="sxs-lookup"><span data-stu-id="3cbbe-170">Scrolling</span></span>

<span data-ttu-id="3cbbe-171">Содержимое Iframe должно прокручиваться вертикально.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-171">Iframe contents should scroll vertically.</span></span> <span data-ttu-id="3cbbe-172">Вы можете видеть только содержимое, которое вы прокрутите (ничего выше или ниже).</span><span class="sxs-lookup"><span data-stu-id="3cbbe-172">You can only see the content you've scrolled to (nothing above or below).</span></span> <span data-ttu-id="3cbbe-173">Панель прокрутки является частью контента iframe.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-173">The scrollbar is part of the iframe content.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-scrolling.png" alt-text="В примере показано, как прокручивается вкладка на собрании." border="false":::

### <a name="navigation"></a><span data-ttu-id="3cbbe-175">Навигация</span><span class="sxs-lookup"><span data-stu-id="3cbbe-175">Navigation</span></span>

<span data-ttu-id="3cbbe-176">Для сценариев со слоями навигации или тяжелым контентом рекомендуется разрешить пользователям переходить на вторичный уровень.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-176">For scenarios with navigation layers or heavy content, we recommend allowing users to navigate to a secondary layer.</span></span> <span data-ttu-id="3cbbe-177">Пользователи должны иметь возможность вернуться к предыдущему слою.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-177">Users must be able to go back to the previous layer.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav.png" alt-text="В примере показана навигация в собрании." border="false":::

## <a name="use-an-in-meeting-dialog"></a><span data-ttu-id="3cbbe-179">Использование диалогового номера на собрании</span><span class="sxs-lookup"><span data-stu-id="3cbbe-179">Use an in-meeting dialog</span></span>

<span data-ttu-id="3cbbe-180">Диалоги на собрании отображаются на этапе собрания Teams.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-180">In-meeting dialogs display on the Teams meeting stage.</span></span> <span data-ttu-id="3cbbe-181">Они требуют внимания пользователя, подтверждения или взаимодействия, но являются тонкими и не прерывают собрание.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-181">They require a user's attention, confirmation, or interaction but are subtle and don't interrupt the meeting.</span></span> <span data-ttu-id="3cbbe-182">Эти сценарии следует использовать экономно и для сценариев, ориентированных на легкие и задачи.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-182">You should use these sparingly and for scenarios that are light and task oriented.</span></span>

### <a name="use-cases"></a><span data-ttu-id="3cbbe-183">Варианты использования</span><span class="sxs-lookup"><span data-stu-id="3cbbe-183">Use cases</span></span>

<span data-ttu-id="3cbbe-184">Диалоговые точки на собрании запускаются пользователем (например, организатором собрания), который может потребовать от участников:</span><span class="sxs-lookup"><span data-stu-id="3cbbe-184">In-meeting dialogs are triggered by a user (such as the meeting organizer) who might want participants to:</span></span>

* <span data-ttu-id="3cbbe-185">Предоставление кратких отзывов</span><span class="sxs-lookup"><span data-stu-id="3cbbe-185">Provide brief feedback</span></span>
* <span data-ttu-id="3cbbe-186">Краткий опрос или опрос</span><span class="sxs-lookup"><span data-stu-id="3cbbe-186">Take a short survey or poll</span></span>
* <span data-ttu-id="3cbbe-187">Отправка утверждений</span><span class="sxs-lookup"><span data-stu-id="3cbbe-187">Submit approvals</span></span>
* <span data-ttu-id="3cbbe-188">Получать напоминания</span><span class="sxs-lookup"><span data-stu-id="3cbbe-188">Get reminders</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-dialog.png" alt-text="В примере показано, как можно использовать диалоговое окно на собрании." border="false":::

### <a name="anatomy-in-meeting-dialog"></a><span data-ttu-id="3cbbe-190">Анатомия: диалоговое окно на собрании</span><span class="sxs-lookup"><span data-stu-id="3cbbe-190">Anatomy: In-meeting dialog</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-anatomy.png" alt-text="В примере показана структурная анатомия диалогов на собрании." border="false":::

|<span data-ttu-id="3cbbe-192">Счетчик</span><span class="sxs-lookup"><span data-stu-id="3cbbe-192">Counter</span></span>|<span data-ttu-id="3cbbe-193">Описание</span><span class="sxs-lookup"><span data-stu-id="3cbbe-193">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="3cbbe-194">1</span><span class="sxs-lookup"><span data-stu-id="3cbbe-194">1</span></span>|<span data-ttu-id="3cbbe-195">**Заглавная** строка: включает значок приложения, имя, строку действия и значок закрытия.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-195">**Header**: Includes app icon, name, action string, and close icon.</span></span>|
|<span data-ttu-id="3cbbe-196">2</span><span class="sxs-lookup"><span data-stu-id="3cbbe-196">2</span></span>|<span data-ttu-id="3cbbe-197">**iframe:** отображает содержимое приложения.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-197">**iframe**: Displays your app content.</span></span>|

### <a name="anatomy-in-meeting-dialog-header"></a><span data-ttu-id="3cbbe-198">Анатомия: диалоговое заглавное окно в собрании</span><span class="sxs-lookup"><span data-stu-id="3cbbe-198">Anatomy: In-meeting dialog header</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-header-anatomy.png" alt-text="В примере показана структурная анатомия диалогового загона на собрании." border="false":::

<span data-ttu-id="3cbbe-200">Существует два варианта загона.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-200">There are two header variants.</span></span> <span data-ttu-id="3cbbe-201">По возможности используйте вариант с аватаром, чтобы подчеркнуть, что диалоговое окно идет от человека.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-201">When possible, use the variant with the avatar to reinforce that the dialog is coming from a person.</span></span>

|<span data-ttu-id="3cbbe-202">Счетчик</span><span class="sxs-lookup"><span data-stu-id="3cbbe-202">Counter</span></span>|<span data-ttu-id="3cbbe-203">Описание</span><span class="sxs-lookup"><span data-stu-id="3cbbe-203">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="3cbbe-204">1</span><span class="sxs-lookup"><span data-stu-id="3cbbe-204">1</span></span>|<span data-ttu-id="3cbbe-205">**Аватар:** человек, который инициирует диалоговое окно на собрании.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-205">**Avatar**: Person who initiates the in-meeting dialog.</span></span>|
|<span data-ttu-id="3cbbe-206">2</span><span class="sxs-lookup"><span data-stu-id="3cbbe-206">2</span></span>|<span data-ttu-id="3cbbe-207">**Значок приложения**</span><span class="sxs-lookup"><span data-stu-id="3cbbe-207">**App icon**</span></span>|
|<span data-ttu-id="3cbbe-208">3</span><span class="sxs-lookup"><span data-stu-id="3cbbe-208">3</span></span>|<span data-ttu-id="3cbbe-209">**Имя приложения**</span><span class="sxs-lookup"><span data-stu-id="3cbbe-209">**App name**</span></span>|
|<span data-ttu-id="3cbbe-210">4 </span><span class="sxs-lookup"><span data-stu-id="3cbbe-210">4</span></span>|<span data-ttu-id="3cbbe-211">**Кнопка Закрыть:** отклонять диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-211">**Close button**: Dismisses the dialog.</span></span>|
|<span data-ttu-id="3cbbe-212">5 </span><span class="sxs-lookup"><span data-stu-id="3cbbe-212">5</span></span>|<span data-ttu-id="3cbbe-213">**Строка** действия. Обычно описывается, кто инициировал диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-213">**Action string**: Typically describes who initiated the dialog.</span></span>|

### <a name="responsive-behavior"></a><span data-ttu-id="3cbbe-214">Адаптируемое поведение</span><span class="sxs-lookup"><span data-stu-id="3cbbe-214">Responsive behavior</span></span>

<span data-ttu-id="3cbbe-215">Диалоги на собрании могут отличаться по размеру для учета различных сценариев.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-215">In-meeting dialogs can vary in size to account for different scenarios.</span></span> <span data-ttu-id="3cbbe-216">Убедитесь, что поддерживается обивка и размеры компонентов.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-216">Make sure to maintain padding and component sizes.</span></span>

* <span data-ttu-id="3cbbe-217">**Ширина.** Можно указать ширину iframe диалогов в любом месте в поддерживаемом диапазоне размеров.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-217">**Width**: You can specify the width of the dialog's iframe anywhere within the supported size range.</span></span>
* <span data-ttu-id="3cbbe-218">**Высота.** Вы можете указать высоту iframe диалогов в любом месте в поддерживаемом диапазоне размеров.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-218">**Height**: You can specify the height of the dialog's iframe anywhere within the supported size range.</span></span> <span data-ttu-id="3cbbe-219">Вы также можете разрешить пользователям прокрутку по вертикали, если содержимое приложения превышает максимальную высоту.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-219">You also can allow users to scroll vertically if your app content exceeds the maximum height.</span></span>

<span data-ttu-id="3cbbe-220">Чтобы реализовать, укажите ширину и высоту с помощью [`externalResourceUrl`](~/apps-in-teams-meetings/create-apps-for-teams-meetings.md#notificationsignal-api) ключа.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-220">To implement, specify the width and height using the [`externalResourceUrl`](~/apps-in-teams-meetings/create-apps-for-teams-meetings.md#notificationsignal-api) key.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-responsive.png" alt-text="В примере показан диалоговое окно на собрании. Ширина: min--280 пикселей (248 пикселей iframe). Max--460 пикселей (428 пикселей iframe). Высота: 300 пикселей (iframe)." border="false":::

## <a name="after-a-meeting"></a><span data-ttu-id="3cbbe-222">После собрания</span><span class="sxs-lookup"><span data-stu-id="3cbbe-222">After a meeting</span></span>

<span data-ttu-id="3cbbe-223">Вы можете вернуться к собранию после его окончания и просмотреть содержимое приложения.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-223">You can go back to a meeting after it ends and view app content.</span></span> <span data-ttu-id="3cbbe-224">В этом примере организатор собрания может посмотреть результаты опроса на вкладке **Contoso.** (Примечание. С точки зрения дизайна нет разницы между опытом вкладки до и после собрания.)</span><span class="sxs-lookup"><span data-stu-id="3cbbe-224">In this example, the meeting organizer can look at poll results in the **Contoso** tab. (Note: From a design standpoint, there's no difference between a the pre- and post-meeting tab experience.)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/post-meeting-experience.png" alt-text="В примере показана вкладка после собрания." border="false":::

## <a name="best-practices"></a><span data-ttu-id="3cbbe-226">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="3cbbe-226">Best practices</span></span>

### <a name="interactions"></a><span data-ttu-id="3cbbe-227">Взаимодействие</span><span class="sxs-lookup"><span data-stu-id="3cbbe-227">Interactions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-do.png" alt-text="Пример, показывающий, как ограничить количество взаимодействий." border="false":::

#### <a name="do-limit-the-number-of-interactions"></a><span data-ttu-id="3cbbe-229">Do: Ограничение количества взаимодействий</span><span class="sxs-lookup"><span data-stu-id="3cbbe-229">Do: Limit the number of interactions</span></span>

<span data-ttu-id="3cbbe-230">Для диалогов на собраниях удалите ненужный контент, который не поможет пользователям быстро выполнить свою задачу.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-230">For in-meeting dialogs, remove unnecessary content that doesn't help users accomplish something quickly.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-dont.png" alt-text="Пример, показывающий, как не вводить ненужные элементы." border="false":::

#### <a name="dont-introduce-unnecessary-elements"></a><span data-ttu-id="3cbbe-232">Не: вводить ненужные элементы</span><span class="sxs-lookup"><span data-stu-id="3cbbe-232">Don't: Introduce unnecessary elements</span></span>

<span data-ttu-id="3cbbe-233">Один диалоговое окно с несколькими взаимодействиями может отвлечь от вызова.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-233">A single in-meeting dialog with multiple interactions can distract from the call.</span></span>

   :::column-end:::
:::row-end:::

### <a name="layout"></a><span data-ttu-id="3cbbe-234">Макет</span><span class="sxs-lookup"><span data-stu-id="3cbbe-234">Layout</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-do.png" alt-text="Пример, показывающий использование макета диалогов с одним столбцом." border="false":::

#### <a name="do-use-a-single-column-dialog-layout"></a><span data-ttu-id="3cbbe-236">Do: Использование макета диалогов с одним столбцом</span><span class="sxs-lookup"><span data-stu-id="3cbbe-236">Do: Use a single-column dialog layout</span></span>

<span data-ttu-id="3cbbe-237">Так как диалоги находятся в центре стадии собрания, завершение задачи должно быть быстрым и простым, чтобы избежать разочарования пользователей.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-237">Since the dialogs are at the center of the meeting stage, task completion should be fast and simple to avoid user frustration.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-dont.png" alt-text="Пример, показывающий, что не следует загромождать пространство расширения собрания." border="false":::

#### <a name="dont-clutter-the-space"></a><span data-ttu-id="3cbbe-239">Не: загромождать пространство</span><span class="sxs-lookup"><span data-stu-id="3cbbe-239">Don't: Clutter the space</span></span>

<span data-ttu-id="3cbbe-240">Плотный или чрезмерно структурированный контент может отвлекать и ошеломить, особенно во время собрания.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-240">Dense or overly structured content can be distracting and overwhelming, especially during a meeting.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-do.png" alt-text="Пример макета вкладки с одним столбцом." border="false":::

#### <a name="do-use-a-single-column-tab-layout"></a><span data-ttu-id="3cbbe-242">Do: Использование макета вкладок с одним столбцом</span><span class="sxs-lookup"><span data-stu-id="3cbbe-242">Do: Use a single-column tab layout</span></span>

<span data-ttu-id="3cbbe-243">Учитывая узкий характер вкладки на собрании, настоятельно рекомендуется отображать содержимое в одном столбце.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-243">Given the in-meeting tab's narrow nature, we strongly recommend displaying the contents in a single column.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-dont.png" alt-text="Пример, показывающий вкладку с несколькими столбцами." border="false":::

#### <a name="dont-use-multiple-columns"></a><span data-ttu-id="3cbbe-245">Не используйте несколько столбцов</span><span class="sxs-lookup"><span data-stu-id="3cbbe-245">Don't: Use multiple columns</span></span>

<span data-ttu-id="3cbbe-246">Из-за ограниченного пространства вкладки в собрании макеты с более чем одним столбцом не рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-246">Due to the limited space of the in-meeting tab, layouts with more than one column aren’t recommended.</span></span>

   :::column-end:::
:::row-end:::

### <a name="controls"></a><span data-ttu-id="3cbbe-247">Элементы управления</span><span class="sxs-lookup"><span data-stu-id="3cbbe-247">Controls</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-do.png" alt-text="Пример, показывающий, как правильно выравнивать основные элементы управления." border="false":::

#### <a name="do-right-align-the-primary-action"></a><span data-ttu-id="3cbbe-249">Do: правильно выравнивание основного действия</span><span class="sxs-lookup"><span data-stu-id="3cbbe-249">Do: Right align the primary action</span></span>

<span data-ttu-id="3cbbe-250">Рекомендуется расположить наиболее визуально тяжелое действие в нужном месте.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-250">We recommend positioning the most visually heavy action to the right-most location.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-dont.png" alt-text="Пример, показывающий, как не следует выровнять основные элементы управления." border="false":::

#### <a name="dont-left-or-center-align-actions"></a><span data-ttu-id="3cbbe-252">Не: действия левого или центрального выравнивания</span><span class="sxs-lookup"><span data-stu-id="3cbbe-252">Don't: Left or center align actions</span></span>

<span data-ttu-id="3cbbe-253">Это отклоняется от стандартного шаблона Teams для размещения управления в диалоговом окте и может противоречить диалоговику за верхней.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-253">This deviates from the standard Teams pattern for control placement in a dialog and may conflict with a dialog behind the top one.</span></span>

   :::column-end:::
:::row-end:::

### <a name="scroll"></a><span data-ttu-id="3cbbe-254">Прокрутка</span><span class="sxs-lookup"><span data-stu-id="3cbbe-254">Scroll</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-do.png" alt-text="Пример, показывающий вертикальную прокрутку на вкладке в собрании." border="false":::

#### <a name="do-scroll-vertically"></a><span data-ttu-id="3cbbe-256">Do: Прокрутите по вертикали</span><span class="sxs-lookup"><span data-stu-id="3cbbe-256">Do: Scroll vertically</span></span>

<span data-ttu-id="3cbbe-257">Пользователи ожидают вертикального прокрутки в Teams (и в других местах).</span><span class="sxs-lookup"><span data-stu-id="3cbbe-257">Users expect vertical scrolling in Teams (and elsewhere).</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-dont.png" alt-text="Пример, показывающий горизонтальную прокрутку на вкладке на собрании." border="false":::

#### <a name="dont-scroll-horizontally"></a><span data-ttu-id="3cbbe-259">Не: прокрутите по горизонтали</span><span class="sxs-lookup"><span data-stu-id="3cbbe-259">Don't: Scroll horizontally</span></span>

<span data-ttu-id="3cbbe-260">Горизонтальная прокрутка не является ожидаемым поведением в Teams.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-260">Horizontal scrolling isn’t an expected behavior in Teams.</span></span> <span data-ttu-id="3cbbe-261">Другие холсты в среде собраний прокрутки вертикально.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-261">Other canvases in the meeting environment scroll vertically.</span></span>

   :::column-end:::
:::row-end:::

### <a name="workflows"></a><span data-ttu-id="3cbbe-262">Рабочие процессы</span><span class="sxs-lookup"><span data-stu-id="3cbbe-262">Workflows</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-workflow-do.png" alt-text="Пример, показывающий сложный сценарий на вкладке на собрании." border="false":::

#### <a name="do-surface-complex-scenarios-in-the-in-meeting-tab"></a><span data-ttu-id="3cbbe-264">Do: Surface complex scenarios in the in-meeting tab</span><span class="sxs-lookup"><span data-stu-id="3cbbe-264">Do: Surface complex scenarios in the in-meeting tab</span></span>

<span data-ttu-id="3cbbe-265">Если ваше приложение включает несколько задач, настоятельно рекомендуется использовать вкладку на собрании с макетом с одним столбцом.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-265">If your app includes multiple tasks, we strongly recommend using an in-meeting tab with a single-column layout.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-workflow-dont.png" alt-text="Пример, показывающий сложные сценарии в диалоговом окантове встречи." border="false":::

#### <a name="dont-make-in-meeting-dialogs-complex"></a><span data-ttu-id="3cbbe-267">Don't: Make in-meeting dialogs complex</span><span class="sxs-lookup"><span data-stu-id="3cbbe-267">Don't: Make in-meeting dialogs complex</span></span>

<span data-ttu-id="3cbbe-268">Диалоги на собраниях предназначены для кратких взаимодействий.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-268">In-meeting dialogs are intended for brief interactions.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="3cbbe-269">Темы</span><span class="sxs-lookup"><span data-stu-id="3cbbe-269">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-do.png" alt-text="Пример, показывающий расширение собрания с темной темой." border="false":::

#### <a name="do-use-teams-color-tokens"></a><span data-ttu-id="3cbbe-271">Do: Использование маркеров цвета Teams</span><span class="sxs-lookup"><span data-stu-id="3cbbe-271">Do: Use Teams color tokens</span></span>

<span data-ttu-id="3cbbe-272">Собрания команд оптимизированы для темного режима, чтобы уменьшить визуальный и когнитивный шум, чтобы пользователи могли сосредоточиться на обсуждении и совместном контенте.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-272">Teams meetings are optimized for dark mode to help reduce visual and cognitive noise so users can focus on the discussion and shared content.</span></span> <span data-ttu-id="3cbbe-273">Узнайте об использовании <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">маркеров цвета (fluent UI).</a></span><span class="sxs-lookup"><span data-stu-id="3cbbe-273">Learn about using <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a>.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-dont.png" alt-text="Пример, показывающий расширение собрания с темой по умолчанию (светлая)." border="false":::

#### <a name="dont-hard-code-hex-values"></a><span data-ttu-id="3cbbe-275">Don't: Hard code hex values</span><span class="sxs-lookup"><span data-stu-id="3cbbe-275">Don't: Hard code hex values</span></span>

<span data-ttu-id="3cbbe-276">Если вы не используете цветные маркеры Teams, ваши проекты будут менее масштабируемыми и на управление ими будет уйма времени.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-276">If you don’t use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::

### <a name="navigation"></a><span data-ttu-id="3cbbe-277">Навигация</span><span class="sxs-lookup"><span data-stu-id="3cbbe-277">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-do.png" alt-text="Пример, показывающий расширение собрания с кнопкой &quot;Назад&quot;." border="false":::

#### <a name="do-have-a-back-button"></a><span data-ttu-id="3cbbe-279">Do: Есть кнопка "Назад"</span><span class="sxs-lookup"><span data-stu-id="3cbbe-279">Do: Have a back button</span></span>

<span data-ttu-id="3cbbe-280">Если на вкладке на собрании имеется несколько уровней навигации, пользователи должны иметь возможность вернуться к своим предыдущим представлениям.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-280">If you have more than one layer of navigation in an in-meeting tab, users must be able to go back to their previous views.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-dont.png" alt-text="Пример, показывающий расширение собрания с двумя кнопками увольнения." border="false":::

#### <a name="dont-include-another-dismiss-button"></a><span data-ttu-id="3cbbe-282">Не: включи еще одну кнопку увольнения</span><span class="sxs-lookup"><span data-stu-id="3cbbe-282">Don't: Include another dismiss button</span></span>

<span data-ttu-id="3cbbe-283">Предоставление возможности закрыть содержимое вкладки в собрании может вызвать проблемы, так как в загонах уже есть кнопка, чтобы отклонять сам вкладку в собрании.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-283">Providing an option to close in-meeting tab content may cause issues since there’s already a button in the header to dismiss the in-meeting tab itself.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-caution.png" alt-text="Пример, показывающий модули (или модули задач) в вкладке на собрании." border="false":::

#### <a name="caution-avoid-modals-within-the-in-meeting-tab"></a><span data-ttu-id="3cbbe-285">Внимание. Избегайте модалов в вкладке в собрании</span><span class="sxs-lookup"><span data-stu-id="3cbbe-285">Caution: Avoid modals within the in-meeting tab</span></span>

<span data-ttu-id="3cbbe-286">Модули (также известные как модули задач) на уже узкой вкладке в собрании могут обернуть содержимое и скрыть его.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-286">Modals (also known as task modules) in the already narrow in-meeting tab might wrap and obscure the content.</span></span>

   :::column-end:::
:::row-end:::

## <a name="validate-your-design"></a><span data-ttu-id="3cbbe-287">Проверка дизайна</span><span class="sxs-lookup"><span data-stu-id="3cbbe-287">Validate your design</span></span>

<span data-ttu-id="3cbbe-288">Если вы планируете опубликовать приложение в AppSource, необходимо понять проблемы проектирования, которые обычно приводят к сбойу приложений во время отправки.</span><span class="sxs-lookup"><span data-stu-id="3cbbe-288">If you plan to publish your app to AppSource, you should understand the design issues that commonly cause apps to fail during submission.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3cbbe-289">Проверка рекомендаций по проверке конструкции</span><span class="sxs-lookup"><span data-stu-id="3cbbe-289">Check design validation guidelines</span></span>](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
