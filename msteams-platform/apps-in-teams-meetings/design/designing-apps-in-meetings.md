---
title: Проектирование расширения собрания
author: heath-hamilton
description: Узнайте, как создать приложения Teams собраниях и получить Microsoft Teams пользовательского интерфейса.
ms.author: lajanuar
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: a08e5a850a62b0cf73661d00e07e55e46abce32f
ms.sourcegitcommit: 3560ee1619e3ab6483a250f1d7f2ceb69353b2dc
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/08/2021
ms.locfileid: "53335412"
---
# <a name="designing-your-microsoft-teams-meeting-extension"></a><span data-ttu-id="502ce-103">Проектирование расширения Microsoft Teams собрания</span><span class="sxs-lookup"><span data-stu-id="502ce-103">Designing your Microsoft Teams meeting extension</span></span>

<span data-ttu-id="502ce-104">Вы можете создавать приложения, чтобы сделать собрания более продуктивными.</span><span class="sxs-lookup"><span data-stu-id="502ce-104">You can create apps to make meetings more productive.</span></span> <span data-ttu-id="502ce-105">Например, попросите людей выполнить опрос во время вызова или отправить быстрое напоминание, которое не прерывает поток собрания.</span><span class="sxs-lookup"><span data-stu-id="502ce-105">For example, ask people to complete a survey during a call or send a quick reminder that doesn’t interrupt the flow of the meeting.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="502ce-106">Комплект разработчика для пользовательского интерфейса Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="502ce-106">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="502ce-107">В наборе пользовательского интерфейса можно найти более исчерпывающие рекомендации по проектированию Microsoft Teams, в том числе элементы, которые можно захватить и изменить по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="502ce-107">You can find more comprehensive design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="502ce-108">Получить комплект разработчика для пользовательского интерфейса Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="502ce-108">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-meeting-extension"></a><span data-ttu-id="502ce-109">Добавление расширения собрания</span><span class="sxs-lookup"><span data-stu-id="502ce-109">Add a meeting extension</span></span>

<span data-ttu-id="502ce-110">Пользователи могут добавлять расширение собрания до и во время собраний.</span><span class="sxs-lookup"><span data-stu-id="502ce-110">Users can add a meeting extension before and during meetings.</span></span> <span data-ttu-id="502ce-111">Они также могут добавлять приложение для определенной встречи непосредственно из Teams магазина.</span><span class="sxs-lookup"><span data-stu-id="502ce-111">They also can add an app for a specific meeting directly from the Teams store.</span></span>

### <a name="add-before-a-meeting"></a><span data-ttu-id="502ce-112">Добавление перед собранием</span><span class="sxs-lookup"><span data-stu-id="502ce-112">Add before a meeting</span></span>

<span data-ttu-id="502ce-113">В сведениях о собрании пользователи могут выбрать Добавить вкладку **+,** чтобы открыть вылет приложения и найти приложения, оптимизированные для собраний.</span><span class="sxs-lookup"><span data-stu-id="502ce-113">In the meeting details, users can select **Add a tab +** to open the app flyout and find apps optimized for meetings.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/add-before-meeting.png" alt-text="В примере показано, как добавить расширение собрания перед собранием." border="false":::

### <a name="add-during-a-meeting"></a><span data-ttu-id="502ce-115">Добавление во время собрания</span><span class="sxs-lookup"><span data-stu-id="502ce-115">Add during a meeting</span></span>

# <a name="desktop"></a>[<span data-ttu-id="502ce-116">Классическая версия</span><span class="sxs-lookup"><span data-stu-id="502ce-116">Desktop</span></span>](#tab/desktop)

На собрании пользователи могут выбрать **дополнительные** добавления :::image type="icon" source="../../assets/icons/teams-client-more.png":::  >  **приложения** и выбрать нужное приложение.

:::image type="content" source="../../assets/images/apps-in-meetings/add-during-meeting.png" alt-text="В примере показано, как добавить расширение собрания во время собрания." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="502ce-119">Мобильная версия</span><span class="sxs-lookup"><span data-stu-id="502ce-119">Mobile</span></span>](#tab/mobile)

После добавления приложения на рабочем столе вы можете выбрать приложение и использовать его на собрании, выбрав **Подробнее** :::image type="icon" source="../../assets/icons/teams-client-more.png"::: .

:::image type="content" source="../../assets/images/apps-in-meetings/mobile-add-during-meeting.png" alt-text="В примере показано, как добавить расширение собрания во время собрания на мобильном телефоне." border="false":::

---

## <a name="before-a-meeting"></a><span data-ttu-id="502ce-122">Перед собранием</span><span class="sxs-lookup"><span data-stu-id="502ce-122">Before a meeting</span></span>

<span data-ttu-id="502ce-123">Перед собранием пользователи могут добавлять содержимое на вкладке. В следующем примере показан проект опроса, на который люди ответят во время вызова.</span><span class="sxs-lookup"><span data-stu-id="502ce-123">Prior to a meeting, users can add content in the tab. The following example shows a draft survey question that people will answer during the call.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/before-meeting-tab.png" alt-text="В примере показано, как приложение содержимым в сведениях о собрании перед вызовом." border="false":::

### <a name="anatomy-meeting-tab-before-and-after-meetings"></a><span data-ttu-id="502ce-125">Анатомия: вкладка "Собрание" (до и после собраний)</span><span class="sxs-lookup"><span data-stu-id="502ce-125">Anatomy: Meeting tab (before and after meetings)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/meeting-details-tab-anatomy.png" alt-text="В примере показана структурная анатомия вкладки собрания до и после собрания." border="false":::

|<span data-ttu-id="502ce-127">Счетчик</span><span class="sxs-lookup"><span data-stu-id="502ce-127">Counter</span></span>|<span data-ttu-id="502ce-128">Описание</span><span class="sxs-lookup"><span data-stu-id="502ce-128">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="502ce-129">1</span><span class="sxs-lookup"><span data-stu-id="502ce-129">1</span></span>|<span data-ttu-id="502ce-130">**Имя вкладки.** Метка навигации для вкладки.</span><span class="sxs-lookup"><span data-stu-id="502ce-130">**Tab name**: Navigation label for your tab.</span></span>|
|<span data-ttu-id="502ce-131">2</span><span class="sxs-lookup"><span data-stu-id="502ce-131">2</span></span>|<span data-ttu-id="502ce-132">**Переполнение вкладки:** открывает действия вкладки, такие как переименование и удаление.</span><span class="sxs-lookup"><span data-stu-id="502ce-132">**Tab overflow**: Opens tab actions, such as rename and remove.</span></span>|
|<span data-ttu-id="502ce-133">3</span><span class="sxs-lookup"><span data-stu-id="502ce-133">3</span></span>|<span data-ttu-id="502ce-134">**iframe:** отображает содержимое приложения.</span><span class="sxs-lookup"><span data-stu-id="502ce-134">**iframe**: Displays your app content.</span></span>|

### <a name="designing-with-ui-templates"></a><span data-ttu-id="502ce-135">Проектирование с помощью шаблонов пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="502ce-135">Designing with UI templates</span></span>

<span data-ttu-id="502ce-136">Используйте один из следующих Teams пользовательского интерфейса для разработки вкладки собраний:</span><span class="sxs-lookup"><span data-stu-id="502ce-136">Use one of the following Teams UI templates to help design your meeting tab:</span></span>

* <span data-ttu-id="502ce-137">[Список.](../../concepts/design/design-teams-app-ui-templates.md#list)Списки могут отображать связанные элементы в сканируемых форматах и позволяют пользователям принимать меры по всему списку или отдельным пунктам.</span><span class="sxs-lookup"><span data-stu-id="502ce-137">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="502ce-138">[Доска](../../concepts/design/design-teams-app-ui-templates.md#task-board)задач. Доска задач, иногда называемая канбанской или плавательные дорожки, — это коллекция карт, часто используемых для отслеживания состояния элементов или билетов.</span><span class="sxs-lookup"><span data-stu-id="502ce-138">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="502ce-139">[Панель](../../concepts/design/design-teams-app-ui-templates.md#dashboard)мониторинга: панель мониторинга — это холст, содержащий несколько карт, которые предоставляют обзор данных или контента.</span><span class="sxs-lookup"><span data-stu-id="502ce-139">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="502ce-140">[Form:](../../concepts/design/design-teams-app-ui-templates.md#form)Forms are for collecting, validating and submitting user input in a structured way.</span><span class="sxs-lookup"><span data-stu-id="502ce-140">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="502ce-141">[Пустое](../../concepts/design/design-teams-app-ui-templates.md#empty-state)состояние. Пустой шаблон состояния можно использовать для многих сценариев, включая вход, первый запуск, сообщения об ошибках и многое другое.</span><span class="sxs-lookup"><span data-stu-id="502ce-141">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="502ce-142">[Левый nav](../../concepts/design/design-teams-app-advanced-ui-components.md#left-nav). Компонент левого nav может помочь если ваша вкладка требует некоторой навигации.</span><span class="sxs-lookup"><span data-stu-id="502ce-142">[Left nav](../../concepts/design/design-teams-app-advanced-ui-components.md#left-nav): The left nav component can help if your tab requires some navigation.</span></span> <span data-ttu-id="502ce-143">В общем, необходимо сохранить навигацию до минимума.</span><span class="sxs-lookup"><span data-stu-id="502ce-143">In general, you should keep navigation to a minimum.</span></span>

## <a name="use-an-in-meeting-tab"></a><span data-ttu-id="502ce-144">Использование вкладки в собрании</span><span class="sxs-lookup"><span data-stu-id="502ce-144">Use an in-meeting tab</span></span>

<span data-ttu-id="502ce-145">Вкладка на собрании — это холст для расширения совместной работы во время собраний.</span><span class="sxs-lookup"><span data-stu-id="502ce-145">The in-meeting tab is a canvas for augmenting collaboration during meetings.</span></span> <span data-ttu-id="502ce-146">Участники могут видеть и взаимодействовать с контентом приложения в выделенном пространстве за пределами стадии собраний с помощью общих представлений или представлений на основе ролей.</span><span class="sxs-lookup"><span data-stu-id="502ce-146">Attendees can see and interact with app content in a dedicated space outside the meeting stage through shared or role-based views.</span></span>

### <a name="use-cases"></a><span data-ttu-id="502ce-147">Варианты использования</span><span class="sxs-lookup"><span data-stu-id="502ce-147">Use cases</span></span>

<span data-ttu-id="502ce-148">Люди могут использовать вкладку на собрании, чтобы:</span><span class="sxs-lookup"><span data-stu-id="502ce-148">People might use the in-meeting tab to:</span></span>

* <span data-ttu-id="502ce-149">Предоставление подробных отзывов.</span><span class="sxs-lookup"><span data-stu-id="502ce-149">Provide detailed feedback.</span></span> <span data-ttu-id="502ce-150">Например, оцените кандидата на работу.</span><span class="sxs-lookup"><span data-stu-id="502ce-150">For example, evaluate a job candidate.</span></span>
* <span data-ttu-id="502ce-151">Создайте элемент опроса, опроса или задачи для участников собрания.</span><span class="sxs-lookup"><span data-stu-id="502ce-151">Create a poll, survey, or task item for the meeting participants.</span></span>
* <span data-ttu-id="502ce-152">Отображение заметок, соответствующих собранию.</span><span class="sxs-lookup"><span data-stu-id="502ce-152">Display notes relevant to the meeting.</span></span> <span data-ttu-id="502ce-153">Например, сведения о лидере продаж.</span><span class="sxs-lookup"><span data-stu-id="502ce-153">For example, information about a sales lead.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="502ce-154">Классическая версия</span><span class="sxs-lookup"><span data-stu-id="502ce-154">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-tab.png" alt-text="В примере показано, как можно представить содержимое опроса на вкладке на собрании." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="502ce-156">Мобильная версия</span><span class="sxs-lookup"><span data-stu-id="502ce-156">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/apps-in-meetings/mobile-use-in-meeting-tab.png" alt-text="В примере показано, как можно представить содержимое опроса в вкладке на собрании на мобильном телефоне." border="false":::

---

### <a name="anatomy-in-meeting-tab"></a><span data-ttu-id="502ce-158">Anatomy: In-meeting tab</span><span class="sxs-lookup"><span data-stu-id="502ce-158">Anatomy: In-meeting tab</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-anatomy.png" alt-text="В примере показана структурная анатомия вкладки на собрании." border="false":::

|<span data-ttu-id="502ce-160">Счетчик</span><span class="sxs-lookup"><span data-stu-id="502ce-160">Counter</span></span>|<span data-ttu-id="502ce-161">Описание</span><span class="sxs-lookup"><span data-stu-id="502ce-161">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="502ce-162">1</span><span class="sxs-lookup"><span data-stu-id="502ce-162">1</span></span>|<span data-ttu-id="502ce-163">**Значок приложения (выбранный)**: 16-пиксельный прозрачный логотип приложения.</span><span class="sxs-lookup"><span data-stu-id="502ce-163">**App icon (selected)**: 16-pixel transparent app logo.</span></span>|
|<span data-ttu-id="502ce-164">2</span><span class="sxs-lookup"><span data-stu-id="502ce-164">2</span></span>|<span data-ttu-id="502ce-165">**Имя приложения**</span><span class="sxs-lookup"><span data-stu-id="502ce-165">**App name**</span></span>|
|<span data-ttu-id="502ce-166">3</span><span class="sxs-lookup"><span data-stu-id="502ce-166">3</span></span>|<span data-ttu-id="502ce-167">**Заглавное** имя. Включает имя приложения.</span><span class="sxs-lookup"><span data-stu-id="502ce-167">**Header**: Includes your app name.</span></span>|
|<span data-ttu-id="502ce-168">4 </span><span class="sxs-lookup"><span data-stu-id="502ce-168">4</span></span>|<span data-ttu-id="502ce-169">**Кнопка закрыть:** отклонять вкладку. Всегда используйте значок верхнего правого закрытия вместо действия в подножке.</span><span class="sxs-lookup"><span data-stu-id="502ce-169">**Close button**: Dismisses the tab. Always use the upper-right close icon instead of an action in the footer.</span></span>|
|<span data-ttu-id="502ce-170">5 </span><span class="sxs-lookup"><span data-stu-id="502ce-170">5</span></span>|<span data-ttu-id="502ce-171">**Панели** уведомлений. Оповещения об ошибках отображаются непосредственно под заголовком и толкают содержимое iframe вниз на 20 пикселей.</span><span class="sxs-lookup"><span data-stu-id="502ce-171">**Notification bar**: Error alerts display directly below the header and push the iframe content down by 20 pixels.</span></span>|
|<span data-ttu-id="502ce-172">6 </span><span class="sxs-lookup"><span data-stu-id="502ce-172">6</span></span>|<span data-ttu-id="502ce-173">**iframe:** отображает содержимое приложения.</span><span class="sxs-lookup"><span data-stu-id="502ce-173">**iframe**: Displays your app content.</span></span>|

### <a name="spacing"></a><span data-ttu-id="502ce-174">Интервал</span><span class="sxs-lookup"><span data-stu-id="502ce-174">Spacing</span></span>

<span data-ttu-id="502ce-175">Оптимизируйте вкладку в собрании, чтобы поместиться по краям в области iframe шириной 280 пикселей.</span><span class="sxs-lookup"><span data-stu-id="502ce-175">Optimize your in-meeting tab to fit edge-to-edge within the 280 pixel-wide iframe area.</span></span> <span data-ttu-id="502ce-176">На левой и правой сторонах iframe и между загонами вкладок имеется 20 пикселей.</span><span class="sxs-lookup"><span data-stu-id="502ce-176">There are 20 pixels of padding on the left and right sides of the iframe and between the tab header.</span></span> <span data-ttu-id="502ce-177">Iframe полностью кровотока в нижней части вкладки.</span><span class="sxs-lookup"><span data-stu-id="502ce-177">The iframe is full bleed to the bottom of the tab.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-spacing.png" alt-text="В примере показаны размеры интервала между вкладками в собрании." border="false":::

### <a name="scrolling"></a><span data-ttu-id="502ce-179">Прокрутка</span><span class="sxs-lookup"><span data-stu-id="502ce-179">Scrolling</span></span>

<span data-ttu-id="502ce-180">Помните следующее, если вы разрешаете прокрутку:</span><span class="sxs-lookup"><span data-stu-id="502ce-180">Remember the following if you allow scrolling:</span></span>

* <span data-ttu-id="502ce-181">Содержимое в содержимом iframe должно прокручиваться только по вертикали.</span><span class="sxs-lookup"><span data-stu-id="502ce-181">Content in the iframe contents should only scroll vertically.</span></span>
* <span data-ttu-id="502ce-182">Пользователи должны видеть только прокрутку контента (ничего выше или ниже).</span><span class="sxs-lookup"><span data-stu-id="502ce-182">Users should only see the content they've scrolled to (nothing above or below).</span></span> 
* <span data-ttu-id="502ce-183">Панель прокрутки является частью контента iframe.</span><span class="sxs-lookup"><span data-stu-id="502ce-183">The scrollbar is part of the iframe content.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-scrolling.png" alt-text="В примере показано, как прокручивается вкладка на собрании." border="false":::

### <a name="navigation"></a><span data-ttu-id="502ce-185">Навигация</span><span class="sxs-lookup"><span data-stu-id="502ce-185">Navigation</span></span>

<span data-ttu-id="502ce-186">Для сценариев со слоями навигации или тяжелым контентом рекомендуется разрешить пользователям переходить на вторичный уровень.</span><span class="sxs-lookup"><span data-stu-id="502ce-186">For scenarios with navigation layers or heavy content, we recommend allowing users to navigate to a secondary layer.</span></span> <span data-ttu-id="502ce-187">Пользователи должны иметь возможность вернуться к предыдущему слою.</span><span class="sxs-lookup"><span data-stu-id="502ce-187">Users must be able to go back to the previous layer.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav.png" alt-text="В примере показана навигация в собрании." border="false":::

## <a name="use-an-in-meeting-dialog"></a><span data-ttu-id="502ce-189">Использование диалогового номера на собрании</span><span class="sxs-lookup"><span data-stu-id="502ce-189">Use an in-meeting dialog</span></span>

<span data-ttu-id="502ce-190">Диалоги на собрании отображаются на Teams собрания.</span><span class="sxs-lookup"><span data-stu-id="502ce-190">In-meeting dialogs display on the Teams meeting stage.</span></span> <span data-ttu-id="502ce-191">Они требуют внимания пользователя, подтверждения или взаимодействия, но являются тонкими и не прерывают собрание.</span><span class="sxs-lookup"><span data-stu-id="502ce-191">They require a user's attention, confirmation, or interaction but are subtle and don't interrupt the meeting.</span></span> <span data-ttu-id="502ce-192">Эти сценарии следует использовать экономно и для сценариев, ориентированных на легкие и задачи.</span><span class="sxs-lookup"><span data-stu-id="502ce-192">You should use these sparingly and for scenarios that are light and task oriented.</span></span>

### <a name="use-cases"></a><span data-ttu-id="502ce-193">Варианты использования</span><span class="sxs-lookup"><span data-stu-id="502ce-193">Use cases</span></span>

<span data-ttu-id="502ce-194">Диалоговые точки на собрании запускаются пользователем (например, организатором собрания), который может потребовать от участников:</span><span class="sxs-lookup"><span data-stu-id="502ce-194">In-meeting dialogs are triggered by a user (such as the meeting organizer) who might want participants to:</span></span>

* <span data-ttu-id="502ce-195">Предоставление кратких отзывов</span><span class="sxs-lookup"><span data-stu-id="502ce-195">Provide brief feedback</span></span>
* <span data-ttu-id="502ce-196">Краткий опрос или опрос</span><span class="sxs-lookup"><span data-stu-id="502ce-196">Take a short survey or poll</span></span>
* <span data-ttu-id="502ce-197">Отправка утверждений</span><span class="sxs-lookup"><span data-stu-id="502ce-197">Submit approvals</span></span>
* <span data-ttu-id="502ce-198">Получать напоминания</span><span class="sxs-lookup"><span data-stu-id="502ce-198">Get reminders</span></span>

# <a name="desktop"></a>[<span data-ttu-id="502ce-199">Классическая версия</span><span class="sxs-lookup"><span data-stu-id="502ce-199">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-dialog.png" alt-text="В примере показано, как можно использовать диалоговое окно на собрании." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="502ce-201">Мобильная версия</span><span class="sxs-lookup"><span data-stu-id="502ce-201">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/apps-in-meetings/mobile-use-in-meeting-dialog.png" alt-text="В примере показано, как можно использовать диалоговое окно на собрании на мобильном телефоне." border="false":::

---

### <a name="anatomy-in-meeting-dialog"></a><span data-ttu-id="502ce-203">Анатомия: диалоговое окно на собрании</span><span class="sxs-lookup"><span data-stu-id="502ce-203">Anatomy: In-meeting dialog</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-anatomy.png" alt-text="В примере показана структурная анатомия диалогов на собрании." border="false":::

|<span data-ttu-id="502ce-205">Счетчик</span><span class="sxs-lookup"><span data-stu-id="502ce-205">Counter</span></span>|<span data-ttu-id="502ce-206">Описание</span><span class="sxs-lookup"><span data-stu-id="502ce-206">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="502ce-207">1</span><span class="sxs-lookup"><span data-stu-id="502ce-207">1</span></span>|<span data-ttu-id="502ce-208">**Заглавная** строка: включает значок приложения, имя, строку действия и значок закрытия.</span><span class="sxs-lookup"><span data-stu-id="502ce-208">**Header**: Includes app icon, name, action string, and close icon.</span></span>|
|<span data-ttu-id="502ce-209">2</span><span class="sxs-lookup"><span data-stu-id="502ce-209">2</span></span>|<span data-ttu-id="502ce-210">**iframe:** отображает содержимое приложения.</span><span class="sxs-lookup"><span data-stu-id="502ce-210">**iframe**: Displays your app content.</span></span>|

### <a name="anatomy-in-meeting-dialog-header"></a><span data-ttu-id="502ce-211">Анатомия: диалоговое заглавное окно в собрании</span><span class="sxs-lookup"><span data-stu-id="502ce-211">Anatomy: In-meeting dialog header</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-header-anatomy.png" alt-text="В примере показана структурная анатомия диалогового загона на собрании." border="false":::

<span data-ttu-id="502ce-213">Существует два варианта загона.</span><span class="sxs-lookup"><span data-stu-id="502ce-213">There are two header variants.</span></span> <span data-ttu-id="502ce-214">По возможности используйте вариант с аватаром, чтобы подчеркнуть, что диалоговое окно идет от человека.</span><span class="sxs-lookup"><span data-stu-id="502ce-214">When possible, use the variant with the avatar to reinforce that the dialog is coming from a person.</span></span>

|<span data-ttu-id="502ce-215">Счетчик</span><span class="sxs-lookup"><span data-stu-id="502ce-215">Counter</span></span>|<span data-ttu-id="502ce-216">Описание</span><span class="sxs-lookup"><span data-stu-id="502ce-216">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="502ce-217">1</span><span class="sxs-lookup"><span data-stu-id="502ce-217">1</span></span>|<span data-ttu-id="502ce-218">**Аватар:** человек, который инициирует диалоговое окно на собрании.</span><span class="sxs-lookup"><span data-stu-id="502ce-218">**Avatar**: Person who initiates the in-meeting dialog.</span></span>|
|<span data-ttu-id="502ce-219">2</span><span class="sxs-lookup"><span data-stu-id="502ce-219">2</span></span>|<span data-ttu-id="502ce-220">**Значок приложения**</span><span class="sxs-lookup"><span data-stu-id="502ce-220">**App icon**</span></span>|
|<span data-ttu-id="502ce-221">3</span><span class="sxs-lookup"><span data-stu-id="502ce-221">3</span></span>|<span data-ttu-id="502ce-222">**Имя приложения**</span><span class="sxs-lookup"><span data-stu-id="502ce-222">**App name**</span></span>|
|<span data-ttu-id="502ce-223">4 </span><span class="sxs-lookup"><span data-stu-id="502ce-223">4</span></span>|<span data-ttu-id="502ce-224">**Кнопка Закрыть:** отклонять диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="502ce-224">**Close button**: Dismisses the dialog.</span></span>|
|<span data-ttu-id="502ce-225">5 </span><span class="sxs-lookup"><span data-stu-id="502ce-225">5</span></span>|<span data-ttu-id="502ce-226">**Строка** действия. Обычно описывается, кто инициировал диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="502ce-226">**Action string**: Typically describes who initiated the dialog.</span></span>|

### <a name="responsive-behavior-in-meeting-dialogs"></a><span data-ttu-id="502ce-227">Отзывчивое поведение: диалоговые логи на собрании</span><span class="sxs-lookup"><span data-stu-id="502ce-227">Responsive behavior: In-meeting dialogs</span></span>

<span data-ttu-id="502ce-228">Диалоги на собрании могут отличаться по размеру для учета различных сценариев.</span><span class="sxs-lookup"><span data-stu-id="502ce-228">In-meeting dialogs can vary in size to account for different scenarios.</span></span> <span data-ttu-id="502ce-229">Убедитесь, что поддерживается обивка и размеры компонентов.</span><span class="sxs-lookup"><span data-stu-id="502ce-229">Make sure to maintain padding and component sizes.</span></span>

* <span data-ttu-id="502ce-230">**Ширина.** Можно указать ширину iframe диалогов в любом месте в поддерживаемом диапазоне размеров.</span><span class="sxs-lookup"><span data-stu-id="502ce-230">**Width**: You can specify the width of the dialog's iframe anywhere within the supported size range.</span></span>
* <span data-ttu-id="502ce-231">**Высота.** Вы можете указать высоту iframe диалогов в любом месте в поддерживаемом диапазоне размеров.</span><span class="sxs-lookup"><span data-stu-id="502ce-231">**Height**: You can specify the height of the dialog's iframe anywhere within the supported size range.</span></span> <span data-ttu-id="502ce-232">Вы также можете разрешить пользователям прокрутку по вертикали, если содержимое приложения превышает максимальную высоту.</span><span class="sxs-lookup"><span data-stu-id="502ce-232">You also can allow users to scroll vertically if your app content exceeds the maximum height.</span></span>

<span data-ttu-id="502ce-233">Чтобы реализовать, укажите ширину и высоту с помощью [`externalResourceUrl`](~/apps-in-teams-meetings/create-apps-for-teams-meetings.md#notificationsignal-api) ключа.</span><span class="sxs-lookup"><span data-stu-id="502ce-233">To implement, specify the width and height using the [`externalResourceUrl`](~/apps-in-teams-meetings/create-apps-for-teams-meetings.md#notificationsignal-api) key.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-responsive.png" alt-text="В примере показан диалоговое окно на собрании. Ширина: min--280 пикселей (248 пикселей iframe). Max--460 пикселей (428 пикселей iframe). Высота: 300 пикселей (iframe)." border="false":::

## <a name="use-the-shared-meeting-stage"></a><span data-ttu-id="502ce-235">Использование общего этапа собраний</span><span class="sxs-lookup"><span data-stu-id="502ce-235">Use the shared meeting stage</span></span>

<span data-ttu-id="502ce-236">Общая стадия собраний помогает участникам встречи взаимодействовать с контентом приложения и сотрудничать с ним в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="502ce-236">Shared meeting stage helps meeting participants interact with and collaborate on app content in real-time.</span></span> <span data-ttu-id="502ce-237">Например, пользователи могут сосредоточиться на редактировании документа, мозговом штурме с помощью доски или просмотре панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="502ce-237">For example, users can focus their call on editing a document, brainstorming with a whiteboard, or reviewing a dashboard.</span></span>

<span data-ttu-id="502ce-238">Приложения, общие на этапе собрания, занимают то же место, что и общий экран.</span><span class="sxs-lookup"><span data-stu-id="502ce-238">Apps shared to the meeting stage occupy the same space as a shared screen.</span></span> <span data-ttu-id="502ce-239">Этап переориентирован для всех участников собрания.</span><span class="sxs-lookup"><span data-stu-id="502ce-239">The stage reorients for all meeting participants.</span></span>

### <a name="use-cases"></a><span data-ttu-id="502ce-240">Варианты использования</span><span class="sxs-lookup"><span data-stu-id="502ce-240">Use cases</span></span>

<span data-ttu-id="502ce-241">Общий этап собраний — это совместная работа и участие.</span><span class="sxs-lookup"><span data-stu-id="502ce-241">The shared meeting stage is all about collaboration and participation.</span></span> <span data-ttu-id="502ce-242">Вот несколько примеров сценариев, которые помогут вам начать работу.</span><span class="sxs-lookup"><span data-stu-id="502ce-242">Here are some example scenarios to help you get started.</span></span>

:::row:::
   :::column span="1":::

<span data-ttu-id="502ce-243">**Редактирование и проверка.** Погрузитесь в панели мониторинга и планирование со всеми по вызову.</span><span class="sxs-lookup"><span data-stu-id="502ce-243">**Edit and review**: Dive into dashboards and planning with everyone on the call.</span></span>

   :::column-end:::
   :::column span="3":::

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-edit-review.png" alt-text="В примере показана панель мониторинга, которая просматривается на общей стадии собрания." border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="1":::

<span data-ttu-id="502ce-245">**Доска.** Рисуйте и идеи вместе на общем холсте.</span><span class="sxs-lookup"><span data-stu-id="502ce-245">**Whiteboard**: Draw and ideate together on a shared canvas.</span></span>

   :::column-end:::
   :::column span="3":::

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-whiteboard.png" alt-text="В примере показана доска на общем этапе собрания." border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="1":::

<span data-ttu-id="502ce-247">**Викторина:** Проверка знаний и получение информации с помощью интерактивных материалов.</span><span class="sxs-lookup"><span data-stu-id="502ce-247">**Quiz**: Test knowledge and gain insights with interactive materials.</span></span>

   :::column-end:::
   :::column span="3":::

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-quiz.png" alt-text="В примере показана викторина на общей стадии собрания." border="false":::

   :::column-end:::
:::row-end:::

### <a name="anatomy-shared-meeting-stage"></a><span data-ttu-id="502ce-249">Анатомия: общий этап собраний</span><span class="sxs-lookup"><span data-stu-id="502ce-249">Anatomy: Shared meeting stage</span></span>

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-anatomy.png" alt-text="На изображении показана анатомия дизайна общей стадии собраний." border="false":::

|<span data-ttu-id="502ce-251">Счетчик</span><span class="sxs-lookup"><span data-stu-id="502ce-251">Counter</span></span>|<span data-ttu-id="502ce-252">Описание</span><span class="sxs-lookup"><span data-stu-id="502ce-252">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="502ce-253">1</span><span class="sxs-lookup"><span data-stu-id="502ce-253">1</span></span>|<span data-ttu-id="502ce-254">**Значок** приложения. Выделенная значок указывает, что вкладка приложения на собрании открыта.</span><span class="sxs-lookup"><span data-stu-id="502ce-254">**App icon**: The highlighted icon indicates the app's in-meeting tab is open.</span></span>|
|<span data-ttu-id="502ce-255">2</span><span class="sxs-lookup"><span data-stu-id="502ce-255">2</span></span>|<span data-ttu-id="502ce-256">**Кнопка "Share to meeting stage":** точка входа, чтобы поделиться приложением со стадией собрания.</span><span class="sxs-lookup"><span data-stu-id="502ce-256">**Share to meeting stage button**: The entry point to share the app to the meeting stage.</span></span> <span data-ttu-id="502ce-257">Отображает, если настроить приложение для использования общей стадии собраний.</span><span class="sxs-lookup"><span data-stu-id="502ce-257">Displays if you configure your app to use the shared meeting stage.</span></span>|
|<span data-ttu-id="502ce-258">3</span><span class="sxs-lookup"><span data-stu-id="502ce-258">3</span></span>|<span data-ttu-id="502ce-259">**iframe:** отображает содержимое приложения.</span><span class="sxs-lookup"><span data-stu-id="502ce-259">**iframe**: Displays your app content.</span></span>|
|<span data-ttu-id="502ce-260">4 </span><span class="sxs-lookup"><span data-stu-id="502ce-260">4</span></span>|<span data-ttu-id="502ce-261">Остановка доступа к **кнопке**: Перестает делиться приложением со стадией собрания.</span><span class="sxs-lookup"><span data-stu-id="502ce-261">**Stop sharing button**: Stops sharing the app to the meeting stage.</span></span> <span data-ttu-id="502ce-262">Отображает только участника, который запустил долю.</span><span class="sxs-lookup"><span data-stu-id="502ce-262">Displays only for the participant who started the share.</span></span>|
|<span data-ttu-id="502ce-263">5 </span><span class="sxs-lookup"><span data-stu-id="502ce-263">5</span></span>|<span data-ttu-id="502ce-264">**Атрибуция presenter:** отображает имя участника, который поделился приложением.</span><span class="sxs-lookup"><span data-stu-id="502ce-264">**Presenter attribution**: Displays the name of the participant who shared the app.</span></span>|

### <a name="responsive-behavior-shared-meeting-stage"></a><span data-ttu-id="502ce-265">Отзывчивое поведение: общая стадия собрания</span><span class="sxs-lookup"><span data-stu-id="502ce-265">Responsive behavior: Shared meeting stage</span></span>

<span data-ttu-id="502ce-266">Приложения, общие на этапе собрания, различаются по размеру в зависимости от состояния собрания и размера окна.</span><span class="sxs-lookup"><span data-stu-id="502ce-266">Apps shared to the meeting stage vary in size based on the state of the meeting and how the user resizes the window.</span></span> <span data-ttu-id="502ce-267">Поддерживать обивку и реагировать на навигацию и элементы управления так же, как и в браузере.</span><span class="sxs-lookup"><span data-stu-id="502ce-267">Maintain padding and the responsive layout of navigation and controls just as you would in a browser.</span></span>

* <span data-ttu-id="502ce-268">**Боковая** панель. Пользователь может открыть боковую панель в любое время во время собрания, чтобы пообщаться, просмотреть список или использовать приложение (например, вкладку на собрании).</span><span class="sxs-lookup"><span data-stu-id="502ce-268">**Side panel**: A user can have the side panel open at any time during a meeting to chat, view the roster, or use an app (i.e., in-meeting tab).</span></span> <span data-ttu-id="502ce-269">Этап динамически перестановки, когда панель открыта.</span><span class="sxs-lookup"><span data-stu-id="502ce-269">The stage dynamically rearranges when the panel is open.</span></span>
* <span data-ttu-id="502ce-270">**Сетка видео и аудио:** видео- и аудиосистемы всегда видны для демонстрации участников собрания.</span><span class="sxs-lookup"><span data-stu-id="502ce-270">**Video and audio grid**: The video and audio grid is always visible to show meeting participants.</span></span> <span data-ttu-id="502ce-271">Если пользователь прожекторы или пин-коды кого-то на собрании, это увеличивает высоту или ширину сетки участников в зависимости от ориентации.</span><span class="sxs-lookup"><span data-stu-id="502ce-271">When a user spotlights or pins someone in the meeting, this increases the height or width of the participant grid depending on the orientation.</span></span>

#### <a name="meeting-stage-without-side-panel"></a><span data-ttu-id="502ce-272">Этап собрания (без боковой панели)</span><span class="sxs-lookup"><span data-stu-id="502ce-272">Meeting stage (without side panel)</span></span>

<span data-ttu-id="502ce-273">Если боковая панель не открыта, уровень собрания по умолчанию составляет 994x678 пикселей и может быть не менее 792x382 пикселей.</span><span class="sxs-lookup"><span data-stu-id="502ce-273">When the side panel isn't open, the meeting stage is 994x678 pixels by default and can be a minimum 792x382 pixels.</span></span>

:::image type="content" source="~/assets/images/apps-in-meetings/meeting-stage-no-side-panel.png" alt-text="Изображение, на котором показана отзывчивость общей стадии собрания с закрытой боковой панелью." border="false":::

#### <a name="meeting-stage-with-side-panel"></a><span data-ttu-id="502ce-275">Этап собрания (с боковой панелью)</span><span class="sxs-lookup"><span data-stu-id="502ce-275">Meeting stage (with side panel)</span></span>

<span data-ttu-id="502ce-276">При открытой боковой панели уровень собрания по умолчанию составляет 918x540 пикселей и может быть не менее 472x382 пикселей.</span><span class="sxs-lookup"><span data-stu-id="502ce-276">When the side panel is open, the meeting stage is 918x540 pixels by default and can be a minimum 472x382 pixels.</span></span>

:::image type="content" source="~/assets/images/apps-in-meetings/meeting-stage-with-side-panel.png" alt-text="Изображение, показывающая отзывчивость общей стадии собрания с открытой боковой панелью." border="false":::

## <a name="after-a-meeting"></a><span data-ttu-id="502ce-278">После собрания</span><span class="sxs-lookup"><span data-stu-id="502ce-278">After a meeting</span></span>

<span data-ttu-id="502ce-279">Вы можете вернуться к собранию после его окончания и просмотреть содержимое приложения.</span><span class="sxs-lookup"><span data-stu-id="502ce-279">You can go back to a meeting after it ends and view app content.</span></span> <span data-ttu-id="502ce-280">В этом примере организатор собрания может посмотреть результаты опроса на вкладке **Contoso.** (Примечание. С точки зрения дизайна нет разницы между опытом вкладки до и после собрания.)</span><span class="sxs-lookup"><span data-stu-id="502ce-280">In this example, the meeting organizer can look at poll results in the **Contoso** tab. (Note: From a design standpoint, there's no difference between a the pre- and post-meeting tab experience.)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/post-meeting-experience.png" alt-text="В примере показана вкладка после собрания." border="false":::

## <a name="best-practices"></a><span data-ttu-id="502ce-282">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="502ce-282">Best practices</span></span>

<span data-ttu-id="502ce-283">Используйте эти рекомендации для создания качественных приложений.</span><span class="sxs-lookup"><span data-stu-id="502ce-283">Use these recommendations to create a quality app experience.</span></span>

### <a name="interactions"></a><span data-ttu-id="502ce-284">Взаимодействие</span><span class="sxs-lookup"><span data-stu-id="502ce-284">Interactions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-do.png" alt-text="Пример, показывающий, как ограничить количество взаимодействий." border="false":::

#### <a name="do-limit-the-number-of-interactions"></a><span data-ttu-id="502ce-286">Do: Ограничение количества взаимодействий</span><span class="sxs-lookup"><span data-stu-id="502ce-286">Do: Limit the number of interactions</span></span>

<span data-ttu-id="502ce-287">Для диалогов на собраниях удалите ненужный контент, который не поможет пользователям быстро выполнить свою задачу.</span><span class="sxs-lookup"><span data-stu-id="502ce-287">For in-meeting dialogs, remove unnecessary content that doesn't help users accomplish something quickly.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-dont.png" alt-text="Пример, показывающий, как не вводить ненужные элементы." border="false":::

#### <a name="dont-introduce-unnecessary-elements"></a><span data-ttu-id="502ce-289">Не: вводить ненужные элементы</span><span class="sxs-lookup"><span data-stu-id="502ce-289">Don't: Introduce unnecessary elements</span></span>

<span data-ttu-id="502ce-290">Один диалоговое окно с несколькими взаимодействиями может отвлечь от вызова.</span><span class="sxs-lookup"><span data-stu-id="502ce-290">A single in-meeting dialog with multiple interactions can distract from the call.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-shared-stage-do.png" alt-text="Пример, показывающий, как создать сфокусированную среду." border="false":::

#### <a name="do-create-a-focused-environment"></a><span data-ttu-id="502ce-292">Do: Создание сфокусированной среды</span><span class="sxs-lookup"><span data-stu-id="502ce-292">Do: Create a focused environment</span></span>

<span data-ttu-id="502ce-293">Рекомендуется сохранить область действия приложения только на стадии собрания.</span><span class="sxs-lookup"><span data-stu-id="502ce-293">We recommend keeping your app’s experience scoped to just the meeting stage.</span></span> <span data-ttu-id="502ce-294">Вы можете использовать вкладку на собрании в боковой панели в качестве дополнительного закрытого представления для определенных сценариев.</span><span class="sxs-lookup"><span data-stu-id="502ce-294">You can use an in-meeting tab in the side panel as a secondary, private view for certain scenarios.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-shared-stage-dont.png" alt-text="Пример, показывающий, как не включать конкурирующие поверхности во время собраний." border="false":::

#### <a name="dont-include-competing-surfaces"></a><span data-ttu-id="502ce-296">Не: включайте конкурирующие поверхности</span><span class="sxs-lookup"><span data-stu-id="502ce-296">Don't: Include competing surfaces</span></span>

<span data-ttu-id="502ce-297">Ваше приложение должно задавать пользователям фокусироваться только на одной поверхности, независимо от того, сотрудничает ли оно на сцене или отвечает на диалоговое окно на собрании.</span><span class="sxs-lookup"><span data-stu-id="502ce-297">Your app should only ask users to focus on a single surface a time, whether it's collaborating on the stage or responding to an in-meeting dialog.</span></span> <span data-ttu-id="502ce-298">(Примечание. Нельзя, чтобы диалоговые диалоги запускались другими приложениями, пока ваше приложение находится на стадии.)</span><span class="sxs-lookup"><span data-stu-id="502ce-298">(Note: You can’t keep dialogs being triggered by other apps while your app is on the stage.)</span></span> 

   :::column-end:::
:::row-end:::

### <a name="layout"></a><span data-ttu-id="502ce-299">Макет</span><span class="sxs-lookup"><span data-stu-id="502ce-299">Layout</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-do.png" alt-text="Пример, показывающий использование макета диалогов с одним столбцом." border="false":::

#### <a name="do-use-a-one-column-dialog"></a><span data-ttu-id="502ce-301">Do: Используйте диалоговое окно с одним столбцом</span><span class="sxs-lookup"><span data-stu-id="502ce-301">Do: Use a one-column dialog</span></span>

<span data-ttu-id="502ce-302">Так как диалоги находятся в центре стадии собрания, завершение задачи должно быть быстрым и простым, чтобы избежать разочарования пользователей.</span><span class="sxs-lookup"><span data-stu-id="502ce-302">Since the dialogs are at the center of the meeting stage, task completion should be fast and simple to avoid user frustration.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-dont.png" alt-text="Пример, показывающий, что не следует загромождать пространство расширения собрания." border="false":::

#### <a name="dont-clutter-the-space"></a><span data-ttu-id="502ce-304">Не: загромождать пространство</span><span class="sxs-lookup"><span data-stu-id="502ce-304">Don't: Clutter the space</span></span>

<span data-ttu-id="502ce-305">Плотный или чрезмерно структурированный контент может отвлекать и ошеломить, особенно во время собрания.</span><span class="sxs-lookup"><span data-stu-id="502ce-305">Dense or overly structured content can be distracting and overwhelming, especially during a meeting.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-do.png" alt-text="Пример макета вкладки с одним столбцом." border="false":::

#### <a name="do-use-a-one-column-tab"></a><span data-ttu-id="502ce-307">Do: Используйте вкладку с одним столбцом</span><span class="sxs-lookup"><span data-stu-id="502ce-307">Do: Use a one-column tab</span></span>

<span data-ttu-id="502ce-308">Учитывая узкий характер вкладки на собрании, настоятельно рекомендуется отображать содержимое в одном столбце.</span><span class="sxs-lookup"><span data-stu-id="502ce-308">Given the in-meeting tab's narrow nature, we strongly recommend displaying the contents in a single column.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-dont.png" alt-text="Пример, показывающий вкладку с несколькими столбцами." border="false":::

#### <a name="dont-use-multiple-columns"></a><span data-ttu-id="502ce-310">Не используйте несколько столбцов</span><span class="sxs-lookup"><span data-stu-id="502ce-310">Don't: Use multiple columns</span></span>

<span data-ttu-id="502ce-311">Из-за ограниченного пространства вкладки в собрании макеты с более чем одним столбцом не рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="502ce-311">Due to the limited space of the in-meeting tab, layouts with more than one column aren’t recommended.</span></span>

   :::column-end:::
:::row-end:::

### <a name="controls"></a><span data-ttu-id="502ce-312">Элементы управления</span><span class="sxs-lookup"><span data-stu-id="502ce-312">Controls</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-do.png" alt-text="Пример, показывающий, как правильно выравнивать основные элементы управления." border="false":::

#### <a name="do-right-align-the-primary-action"></a><span data-ttu-id="502ce-314">Do: правильно выравнивание основного действия</span><span class="sxs-lookup"><span data-stu-id="502ce-314">Do: Right align the primary action</span></span>

<span data-ttu-id="502ce-315">Рекомендуется расположить наиболее визуально тяжелое действие в нужном месте.</span><span class="sxs-lookup"><span data-stu-id="502ce-315">We recommend positioning the most visually heavy action to the right-most location.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-dont.png" alt-text="Пример, показывающий, как не следует выровнять основные элементы управления." border="false":::

#### <a name="dont-left-or-center-align-actions"></a><span data-ttu-id="502ce-317">Не: действия левого или центрального выравнивания</span><span class="sxs-lookup"><span data-stu-id="502ce-317">Don't: Left or center align actions</span></span>

<span data-ttu-id="502ce-318">Это отклоняется от стандартного шаблона Teams для размещения управления в диалоговом окте и может противоречить диалоговику за верхней.</span><span class="sxs-lookup"><span data-stu-id="502ce-318">This deviates from the standard Teams pattern for control placement in a dialog and may conflict with a dialog behind the top one.</span></span>

   :::column-end:::
:::row-end:::

### <a name="scrolling"></a><span data-ttu-id="502ce-319">Прокрутка</span><span class="sxs-lookup"><span data-stu-id="502ce-319">Scrolling</span></span>

:::row:::
   :::column span="":::

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-do.png" alt-text="Пример, показывающий вертикальную прокрутку на вкладке в собрании." border="false":::

:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-scroll-do.png" alt-text="Пример, показывающий вертикальную прокрутку на общем этапе собрания." border="false":::

#### <a name="do-scroll-vertically"></a><span data-ttu-id="502ce-322">Do: Прокрутите по вертикали</span><span class="sxs-lookup"><span data-stu-id="502ce-322">Do: Scroll vertically</span></span>

<span data-ttu-id="502ce-323">Пользователи ожидают вертикального прокрутки Teams (и в других местах).</span><span class="sxs-lookup"><span data-stu-id="502ce-323">Users expect vertical scrolling in Teams (and elsewhere).</span></span> <span data-ttu-id="502ce-324">Это может не применяться, если у вас есть творческий холст, например доска, которую пользователи могут панорамирование по оси x и y.</span><span class="sxs-lookup"><span data-stu-id="502ce-324">This may not apply if you have a creative canvas, such as a whiteboard, which users can pan across the x and y axis.</span></span>

   :::column-end:::
   :::column span="":::

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-dont.png" alt-text="Пример, показывающий горизонтальную прокрутку на вкладке на собрании." border="false":::

:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-scroll-dont.png" alt-text="Пример, показывающий горизонтальную прокрутку на общем этапе собрания." border="false":::

#### <a name="dont-scroll-horizontally"></a><span data-ttu-id="502ce-327">Не: прокрутите по горизонтали</span><span class="sxs-lookup"><span data-stu-id="502ce-327">Don't: Scroll horizontally</span></span>

<span data-ttu-id="502ce-328">Горизонтальная прокрутка не является ожидаемым поведением в Teams (включая среду собраний).</span><span class="sxs-lookup"><span data-stu-id="502ce-328">Horizontal scrolling isn’t an expected behavior in Teams (including the meeting environment).</span></span>

   :::column-end:::
:::row-end:::

### <a name="workflows"></a><span data-ttu-id="502ce-329">Рабочие процессы</span><span class="sxs-lookup"><span data-stu-id="502ce-329">Workflows</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-workflow-do.png" alt-text="Пример, показывающий сложный сценарий на вкладке на собрании." border="false":::

#### <a name="do-surface-complex-scenarios-in-the-in-meeting-tab"></a><span data-ttu-id="502ce-331">Do: Surface complex scenarios in the in-meeting tab</span><span class="sxs-lookup"><span data-stu-id="502ce-331">Do: Surface complex scenarios in the in-meeting tab</span></span>

<span data-ttu-id="502ce-332">Если ваше приложение включает несколько задач, настоятельно рекомендуется использовать вкладку на собрании с макетом с одним столбцом.</span><span class="sxs-lookup"><span data-stu-id="502ce-332">If your app includes multiple tasks, we strongly recommend using an in-meeting tab with a single-column layout.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-workflow-dont.png" alt-text="Пример, показывающий сложные сценарии в диалоговом окантове встречи." border="false":::

#### <a name="dont-make-in-meeting-dialogs-complex"></a><span data-ttu-id="502ce-334">Don't: Make in-meeting dialogs complex</span><span class="sxs-lookup"><span data-stu-id="502ce-334">Don't: Make in-meeting dialogs complex</span></span>

<span data-ttu-id="502ce-335">Диалоги на собраниях предназначены для кратких взаимодействий.</span><span class="sxs-lookup"><span data-stu-id="502ce-335">In-meeting dialogs are intended for brief interactions.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="502ce-336">Визуальные темы</span><span class="sxs-lookup"><span data-stu-id="502ce-336">Theming</span></span>

:::row:::
   :::column span="":::

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-do.png" alt-text="Пример, показывающий расширение собрания с темной темой." border="false":::

:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-theming-do.png" alt-text="Другой пример, показывающий расширение собрания с темной темой." border="false":::

#### <a name="do-focus-on-dark-theme"></a><span data-ttu-id="502ce-339">Do: Фокус на темной теме</span><span class="sxs-lookup"><span data-stu-id="502ce-339">Do: Focus on dark theme</span></span>

<span data-ttu-id="502ce-340">Teams для темной темы, чтобы уменьшить визуальный и когнитивный шум, чтобы пользователи могли сосредоточиться на обсуждении и совместном контенте.</span><span class="sxs-lookup"><span data-stu-id="502ce-340">Teams meetings are optimized for dark theme to help reduce visual and cognitive noise so users can focus on the discussion and shared content.</span></span> <span data-ttu-id="502ce-341">Помните, что некоторым типам приложений (например, доска и редактирование документов) не требуется темное полотно.</span><span class="sxs-lookup"><span data-stu-id="502ce-341">Keep in mind certain types of apps (such as whiteboarding and document editing) don't need a dark canvas.</span></span>

   :::column-end:::
   :::column span="":::

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-dont.png" alt-text="Пример, показывающий расширение собрания с цветами, которые не соответствуют теме собрания." border="false":::

:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-theming-dont.png" alt-text="Другой пример, показывающий расширение собрания с цветами, не совпадать с темой собрания." border="false":::

#### <a name="dont-use-unfamiliar-colors"></a><span data-ttu-id="502ce-344">Не используйте незнакомые цвета</span><span class="sxs-lookup"><span data-stu-id="502ce-344">Don't: Use unfamiliar colors</span></span>

<span data-ttu-id="502ce-345">Цвета, конфликтующие с средой собраний, могут отвлекать и казаться менее родными для Teams.</span><span class="sxs-lookup"><span data-stu-id="502ce-345">Colors that clash with the meeting environment may be distracting and appear less native to Teams.</span></span> <span data-ttu-id="502ce-346">Узнайте о рампе [Teams,](https://developer.microsoft.com/fluentui#/styles/web/colors/products)включая нейтральные темы вызовов.</span><span class="sxs-lookup"><span data-stu-id="502ce-346">Learn about the Teams [color ramp](https://developer.microsoft.com/fluentui#/styles/web/colors/products), including call theme neutrals.</span></span>

   :::column-end:::
:::row-end:::

### <a name="navigation"></a><span data-ttu-id="502ce-347">Навигация</span><span class="sxs-lookup"><span data-stu-id="502ce-347">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-do.png" alt-text="Пример, показывающий расширение собрания с кнопкой &quot;Назад&quot;." border="false":::

#### <a name="do-have-a-back-button"></a><span data-ttu-id="502ce-349">Do: Есть кнопка "Назад"</span><span class="sxs-lookup"><span data-stu-id="502ce-349">Do: Have a back button</span></span>

<span data-ttu-id="502ce-350">Если на вкладке на собрании имеется несколько уровней навигации, пользователи должны иметь возможность вернуться к своим предыдущим представлениям.</span><span class="sxs-lookup"><span data-stu-id="502ce-350">If you have more than one layer of navigation in an in-meeting tab, users must be able to go back to their previous views.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-dont.png" alt-text="Пример, показывающий расширение собрания с двумя кнопками увольнения." border="false":::

#### <a name="dont-include-another-dismiss-button"></a><span data-ttu-id="502ce-352">Не: включи еще одну кнопку увольнения</span><span class="sxs-lookup"><span data-stu-id="502ce-352">Don't: Include another dismiss button</span></span>

<span data-ttu-id="502ce-353">Предоставление возможности закрыть содержимое вкладки в собрании может вызвать проблемы, так как в загонах уже есть кнопка, чтобы отклонять сам вкладку в собрании.</span><span class="sxs-lookup"><span data-stu-id="502ce-353">Providing an option to close in-meeting tab content may cause issues since there’s already a button in the header to dismiss the in-meeting tab itself.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-caution.png" alt-text="Пример, показывающий модули (или модули задач) в вкладке на собрании." border="false":::

#### <a name="caution-avoid-modals-within-the-in-meeting-tab"></a><span data-ttu-id="502ce-355">Внимание. Избегайте модалов в вкладке в собрании</span><span class="sxs-lookup"><span data-stu-id="502ce-355">Caution: Avoid modals within the in-meeting tab</span></span>

<span data-ttu-id="502ce-356">Модули (также известные как модули задач) на уже узкой вкладке в собрании могут обернуть содержимое и скрыть его.</span><span class="sxs-lookup"><span data-stu-id="502ce-356">Modals (also known as task modules) in the already narrow in-meeting tab might wrap and obscure the content.</span></span>

   :::column-end:::
:::row-end:::

### <a name="responsive-behavior"></a><span data-ttu-id="502ce-357">Адаптируемое поведение</span><span class="sxs-lookup"><span data-stu-id="502ce-357">Responsive behavior</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-responsiveness-do.png" alt-text="Пример, показывающий, как правильно использовать расширение собрания." border="false":::

#### <a name="do-resize-and-scale-your-app-responsively"></a><span data-ttu-id="502ce-359">Do: Resize and scale your app responsively</span><span class="sxs-lookup"><span data-stu-id="502ce-359">Do: Resize and scale your app responsively</span></span>

<span data-ttu-id="502ce-360">Содержимое приложения должно динамически меняться и конденсироваться в небольших окнах.</span><span class="sxs-lookup"><span data-stu-id="502ce-360">App content should dynamically resize and condense in smaller windows.</span></span> <span data-ttu-id="502ce-361">Сохраняйте основные навигации вашего приложения и все плавающие элементы управления видимыми.</span><span class="sxs-lookup"><span data-stu-id="502ce-361">Keep your app’s main navigation and any floating controls visible.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-responsiveness-dont.png" alt-text="Пример, показывающий, как не правильно использовать расширение собрания." border="false":::

#### <a name="dont-crop-or-clip-primary-ui-components"></a><span data-ttu-id="502ce-363">Не: Обрезать или обрезать основные компоненты пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="502ce-363">Don't: Crop or clip primary UI components</span></span>

<span data-ttu-id="502ce-364">Плавающая навигация и элементы управления с экрана и поиск свитка могут привести к путанице для пользователей.</span><span class="sxs-lookup"><span data-stu-id="502ce-364">Floating navigation and controls off screen and requiring a scroll to find can be confusing for users.</span></span> <span data-ttu-id="502ce-365">Содержимое приложения не должно прокручиваться горизонтально, если оно не может поместиться в iframe.</span><span class="sxs-lookup"><span data-stu-id="502ce-365">Your app content shouldn’t scroll horizontally when it can't fit in the iframe.</span></span>

   :::column-end:::
:::row-end:::

## <a name="next-step"></a><span data-ttu-id="502ce-366">Следующий этап</span><span class="sxs-lookup"><span data-stu-id="502ce-366">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="502ce-367">Настройка приложения для собраний</span><span class="sxs-lookup"><span data-stu-id="502ce-367">Configure your app for meetings</span></span>](~/apps-in-teams-meetings/enable-and-configure-your-app-for-teams-meetings.md)
