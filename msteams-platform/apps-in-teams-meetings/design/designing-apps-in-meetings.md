---
title: Разработка расширения собрания
author: heath-hamilton
description: Сведения о проектировании приложений в собраниях Teams и получении набора UI Microsoft Teams.
ms.author: lajanuar
ms.topic: conceptual
ms.openlocfilehash: 3d18895626d5f2846d10e7145a622834d82b2e98
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/09/2020
ms.locfileid: "49606366"
---
# <a name="designing-your-microsoft-teams-meeting-extension"></a><span data-ttu-id="fd724-103">Разработка расширения для собраний Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="fd724-103">Designing your Microsoft Teams meeting extension</span></span>

<span data-ttu-id="fd724-104">Вы можете создавать приложения, повышающие продуктивность собраний.</span><span class="sxs-lookup"><span data-stu-id="fd724-104">You can create apps to make meetings more productive.</span></span> <span data-ttu-id="fd724-105">Например, попросите пользователей выполнить опрос во время звонка или отправить быстрое напоминание, не прерывая процесс собрания.</span><span class="sxs-lookup"><span data-stu-id="fd724-105">For example, ask people to complete a survey during a call or send a quick reminder that doesn’t interrupt the flow of the meeting.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="fd724-106">Набор элементов пользовательского интерфейса Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="fd724-106">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="fd724-107">Вы можете найти более подробные рекомендации по проектированию, включая элементы, которые можно прихватить и изменить при необходимости, в наборе UI Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="fd724-107">You can find more comprehensive design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fd724-108">Получение набора элементов пользовательского интерфейса Microsoft Teams (фигма)</span><span class="sxs-lookup"><span data-stu-id="fd724-108">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-meeting-extension"></a><span data-ttu-id="fd724-109">Добавление расширения собрания</span><span class="sxs-lookup"><span data-stu-id="fd724-109">Add a meeting extension</span></span>

<span data-ttu-id="fd724-110">Вы можете добавить добавочный номер собрания до и во время собраний.</span><span class="sxs-lookup"><span data-stu-id="fd724-110">You can add a meeting extension before and during meetings.</span></span> <span data-ttu-id="fd724-111">Кроме того, вы можете получить приложение для определенного собрания непосредственно из хранилища Teams (AppSource).</span><span class="sxs-lookup"><span data-stu-id="fd724-111">You also can an app for a specific meeting directly from the Teams store (AppSource).</span></span>

### <a name="add-before-a-meeting"></a><span data-ttu-id="fd724-112">Добавить перед собранием</span><span class="sxs-lookup"><span data-stu-id="fd724-112">Add before a meeting</span></span>

<span data-ttu-id="fd724-113">Перед собранием в разделе сведения о собрании выберите **Добавить вкладку +** , чтобы открыть всплывающее окно приложения и найти приложения, оптимизированные для собраний.</span><span class="sxs-lookup"><span data-stu-id="fd724-113">Before a meeting, the meeting details select **Add a tab +** to open the app flyout and find apps optimized for meetings.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/add-before-meeting.png" alt-text="В примере показано, как добавить добавочный номер собрания перед собранием." border="false":::

### <a name="add-during-a-meeting"></a><span data-ttu-id="fd724-115">Добавить во время собрания</span><span class="sxs-lookup"><span data-stu-id="fd724-115">Add during a meeting</span></span>

На собрании **выберите пункт** :::image type="icon" source="../../assets/icons/teams-client-more.png":::  >  **Добавить приложение** и выберите нужное приложение.

:::image type="content" source="../../assets/images/apps-in-meetings/add-during-meeting.png" alt-text="Пример показывает, как добавить добавочный номер собрания во время собрания." border="false":::

## <a name="before-a-meeting"></a><span data-ttu-id="fd724-118">Подготовка к собранию</span><span class="sxs-lookup"><span data-stu-id="fd724-118">Before a meeting</span></span>

<span data-ttu-id="fd724-119">Прежде чем приступать к собранию, вы можете добавить контент на вкладке. В следующем примере показан проектный вопрос для опроса, который пользователи будут отвечать во время звонка.</span><span class="sxs-lookup"><span data-stu-id="fd724-119">Prior to your meeting, you can add content in the tab. The following example shows a draft survey question that people will answer during the call.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/before-meeting-tab.png" alt-text="Пример показывает, как получить содержимое приложения в сведениях о собрании перед вызовом." border="false":::

### <a name="anatomy-meeting-tab-before-and-after-meetings"></a><span data-ttu-id="fd724-121">Структура: вкладка "собрание" (до и после собраний)</span><span class="sxs-lookup"><span data-stu-id="fd724-121">Anatomy: Meeting tab (before and after meetings)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/meeting-details-tab-anatomy.png" alt-text="В примере показана структура структуры вкладки собрание до и после собрания." border="false":::

|<span data-ttu-id="fd724-123">Счетчик</span><span class="sxs-lookup"><span data-stu-id="fd724-123">Counter</span></span>|<span data-ttu-id="fd724-124">Описание</span><span class="sxs-lookup"><span data-stu-id="fd724-124">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="fd724-125">1</span><span class="sxs-lookup"><span data-stu-id="fd724-125">1</span></span>|<span data-ttu-id="fd724-126">**Имя вкладки**: "Метка навигации" для вкладки.</span><span class="sxs-lookup"><span data-stu-id="fd724-126">**Tab name**: Navigation label for your tab.</span></span>|
|<span data-ttu-id="fd724-127">2 </span><span class="sxs-lookup"><span data-stu-id="fd724-127">2</span></span>|<span data-ttu-id="fd724-128">**Переполнение табуляции**: открывает действия вкладки, такие как переименование и удаление.</span><span class="sxs-lookup"><span data-stu-id="fd724-128">**Tab overflow**: Opens tab actions, such as rename and remove.</span></span>|
|<span data-ttu-id="fd724-129">3 </span><span class="sxs-lookup"><span data-stu-id="fd724-129">3</span></span>|<span data-ttu-id="fd724-130">**IFRAME**: отображение контента приложения.</span><span class="sxs-lookup"><span data-stu-id="fd724-130">**iframe**: Displays your app content.</span></span>|

### <a name="designing-with-ui-templates"></a><span data-ttu-id="fd724-131">Разработка с помощью шаблонов пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="fd724-131">Designing with UI templates</span></span>

<span data-ttu-id="fd724-132">Используйте один из следующих шаблонов пользовательского интерфейса Teams, чтобы упростить разработку вкладки собрания:</span><span class="sxs-lookup"><span data-stu-id="fd724-132">Use one of the following Teams UI templates to help design your meeting tab:</span></span>

* <span data-ttu-id="fd724-133">[Список](../../concepts/design/design-teams-app-ui-templates.md#list): списки могут отображать связанные элементы в формате с возможностью записи, а пользователи выполнять действия для всего списка или отдельных элементов.</span><span class="sxs-lookup"><span data-stu-id="fd724-133">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="fd724-134">[Доска задач](../../concepts/design/design-teams-app-ui-templates.md#task-board): доска задач, иногда называемая доской Канбан или свим желобами, — это коллекция карточек, часто используемых для отслеживания состояния рабочих элементов или билетов.</span><span class="sxs-lookup"><span data-stu-id="fd724-134">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="fd724-135">[Панель мониторинга](../../concepts/design/design-teams-app-ui-templates.md#dashboard): панель мониторинга — это холст, содержащий несколько карточек, которые предоставляют обзор данных или контента.</span><span class="sxs-lookup"><span data-stu-id="fd724-135">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="fd724-136">[Форма](../../concepts/design/design-teams-app-ui-templates.md#form): формы предназначены для сбора, проверки и отправки пользовательских данных структурированным способом.</span><span class="sxs-lookup"><span data-stu-id="fd724-136">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="fd724-137">[Пустое состояние](../../concepts/design/design-teams-app-ui-templates.md#empty-state): шаблон пустое состояние можно использовать для многих сценариев, в том числе входа в систему, первого запуска, сообщений об ошибках и многого другого.</span><span class="sxs-lookup"><span data-stu-id="fd724-137">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="fd724-138">[Левая панель навигации](../../concepts/design/design-teams-app-ui-templates.md#left-nav): левая панель навигации может помочь вам, если на вкладке требуется выполнить некоторую навигацию.</span><span class="sxs-lookup"><span data-stu-id="fd724-138">[Left nav](../../concepts/design/design-teams-app-ui-templates.md#left-nav): The left nav template can help if your tab requires some navigation.</span></span> <span data-ttu-id="fd724-139">Как правило, переход по клавише Tab должен быть минимальным.</span><span class="sxs-lookup"><span data-stu-id="fd724-139">In general, you should keep tab navigation to a minimum.</span></span>

## <a name="use-an-in-meeting-tab"></a><span data-ttu-id="fd724-140">Использование вкладки собрания</span><span class="sxs-lookup"><span data-stu-id="fd724-140">Use an in-meeting tab</span></span>

<span data-ttu-id="fd724-141">Вкладка "в собрании" это холст для расширения совместной работы во время собраний.</span><span class="sxs-lookup"><span data-stu-id="fd724-141">The in-meeting tab is a canvas for augmenting collaboration during meetings.</span></span> <span data-ttu-id="fd724-142">Участники могут видеть содержимое приложения и взаимодействовать с ним в выделенном пространстве за престановкой с помощью общих представлений или представлений на основе ролей.</span><span class="sxs-lookup"><span data-stu-id="fd724-142">Attendees can see and interact with app content in a dedicated space outside the meeting stage through shared or role-based views.</span></span>

### <a name="use-cases"></a><span data-ttu-id="fd724-143">Варианты использования</span><span class="sxs-lookup"><span data-stu-id="fd724-143">Use cases</span></span>

<span data-ttu-id="fd724-144">С помощью вкладки в собрании пользователи могут выполнять следующие действия:</span><span class="sxs-lookup"><span data-stu-id="fd724-144">People might use the in-meeting tab to:</span></span>

* <span data-ttu-id="fd724-145">Предоставление подробной обратной связи (например, Оценка кандидата на задание)</span><span class="sxs-lookup"><span data-stu-id="fd724-145">Provide detailed feedback (for example, evaluate a job candidate)</span></span>
* <span data-ttu-id="fd724-146">Быстрое создание опроса, опроса или элемента задачи для участников собрания</span><span class="sxs-lookup"><span data-stu-id="fd724-146">Quickly create a poll, survey, or task item for the meeting participants</span></span>
* <span data-ttu-id="fd724-147">Отображение заметок, относящихся к собранию (например, сведений о менеджере по продажам)</span><span class="sxs-lookup"><span data-stu-id="fd724-147">Display notes relevant to the meeting (for example, information about a sales lead)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-tab.png" alt-text="Пример показывает, как можно представить содержимое опроса на вкладке на собрании." border="false":::

### <a name="anatomy-in-meeting-tab"></a><span data-ttu-id="fd724-149">Структура: вкладка "на собрание"</span><span class="sxs-lookup"><span data-stu-id="fd724-149">Anatomy: In-meeting tab</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-anatomy.png" alt-text="В примере показана структурная структура вкладки на собрании." border="false":::

|<span data-ttu-id="fd724-151">Счетчик</span><span class="sxs-lookup"><span data-stu-id="fd724-151">Counter</span></span>|<span data-ttu-id="fd724-152">Описание</span><span class="sxs-lookup"><span data-stu-id="fd724-152">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="fd724-153">1</span><span class="sxs-lookup"><span data-stu-id="fd724-153">1</span></span>|<span data-ttu-id="fd724-154">**Значок приложения (выбран)**: логотип 16-пиксельного прозрачного приложения.</span><span class="sxs-lookup"><span data-stu-id="fd724-154">**App icon (selected)**: 16-pixel transparent app logo.</span></span>|
|<span data-ttu-id="fd724-155">2 </span><span class="sxs-lookup"><span data-stu-id="fd724-155">2</span></span>|<span data-ttu-id="fd724-156">**Имя приложения**</span><span class="sxs-lookup"><span data-stu-id="fd724-156">**App name**</span></span>|
|<span data-ttu-id="fd724-157">3 </span><span class="sxs-lookup"><span data-stu-id="fd724-157">3</span></span>|<span data-ttu-id="fd724-158">**Верхний колонтитул**: включает имя приложения.</span><span class="sxs-lookup"><span data-stu-id="fd724-158">**Header**: Includes your app name.</span></span>|
|<span data-ttu-id="fd724-159">4 </span><span class="sxs-lookup"><span data-stu-id="fd724-159">4</span></span>|<span data-ttu-id="fd724-160">**Кнопка закрытия**: закрывает вкладку. Всегда используйте значок закрытия сверху справа, а не действие в нижнем колонтитуле.</span><span class="sxs-lookup"><span data-stu-id="fd724-160">**Close button**: Dismisses the tab. Always use the upper-right close icon instead of an action in the footer.</span></span>|
|<span data-ttu-id="fd724-161">5 </span><span class="sxs-lookup"><span data-stu-id="fd724-161">5</span></span>|<span data-ttu-id="fd724-162">**Панель уведомлений**: оповещения об ошибках отображаются непосредственно под заголовком и помещают содержимое IFRAME вниз на 20 пикселей.</span><span class="sxs-lookup"><span data-stu-id="fd724-162">**Notification bar**: Error alerts display directly below the header and push the iframe content down by 20 pixels.</span></span>|
|<span data-ttu-id="fd724-163">6 </span><span class="sxs-lookup"><span data-stu-id="fd724-163">6</span></span>|<span data-ttu-id="fd724-164">**IFRAME**: отображение контента приложения.</span><span class="sxs-lookup"><span data-stu-id="fd724-164">**iframe**: Displays your app content.</span></span>|

### <a name="spacing"></a><span data-ttu-id="fd724-165">Интервал</span><span class="sxs-lookup"><span data-stu-id="fd724-165">Spacing</span></span>

<span data-ttu-id="fd724-166">Оптимизация вкладки в собрании для размещения пограничных пограничных точек в области IFRAME на уровне 280.</span><span class="sxs-lookup"><span data-stu-id="fd724-166">Optimize your in-meeting tab to fit edge-to-edge within the 280 pixel-wide iframe area.</span></span> <span data-ttu-id="fd724-167">На левой и правой сторонах окна iframe и между заголовком вкладки имеется 20 точек заполнения.</span><span class="sxs-lookup"><span data-stu-id="fd724-167">There are 20 pixels of padding on the left and right sides of the iframe and between the tab header.</span></span> <span data-ttu-id="fd724-168">В нижней части вкладки IFRAME находится полный выход из системы.</span><span class="sxs-lookup"><span data-stu-id="fd724-168">The iframe is full bleed to the bottom of the tab.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-spacing.png" alt-text="Пример: отображение измерений расстояний для вкладок собраний." border="false":::

### <a name="scrolling"></a><span data-ttu-id="fd724-170">Прокрутки</span><span class="sxs-lookup"><span data-stu-id="fd724-170">Scrolling</span></span>

<span data-ttu-id="fd724-171">Содержимое IFRAME должно прокручиваться по вертикали.</span><span class="sxs-lookup"><span data-stu-id="fd724-171">Iframe contents should scroll vertically.</span></span> <span data-ttu-id="fd724-172">Отображается только содержимое, к которому вы выполнили прокрутку (ничего или не ниже).</span><span class="sxs-lookup"><span data-stu-id="fd724-172">You can only see the content you've scrolled to (nothing above or below).</span></span> <span data-ttu-id="fd724-173">Полоса прокрутки является частью содержимого IFRAME.</span><span class="sxs-lookup"><span data-stu-id="fd724-173">The scrollbar is part of the iframe content.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-scrolling.png" alt-text="Пример, демонстрирующий прокрутку вкладки в собрании." border="false":::

### <a name="navigation"></a><span data-ttu-id="fd724-175">Навигация</span><span class="sxs-lookup"><span data-stu-id="fd724-175">Navigation</span></span>

<span data-ttu-id="fd724-176">Для сценариев с слоями навигации или большим содержимым рекомендуется разрешить пользователям переходить на дополнительный слой.</span><span class="sxs-lookup"><span data-stu-id="fd724-176">For scenarios with navigation layers or heavy content, we recommend allowing users to navigate to a secondary layer.</span></span> <span data-ttu-id="fd724-177">Пользователи должны иметь возможность вернуться к предыдущему слою.</span><span class="sxs-lookup"><span data-stu-id="fd724-177">Users must be able to go back to the previous layer.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav.png" alt-text="Пример: Навигация по собранию." border="false":::

## <a name="use-an-in-meeting-dialog"></a><span data-ttu-id="fd724-179">Использование диалогового окна для собраний</span><span class="sxs-lookup"><span data-stu-id="fd724-179">Use an in-meeting dialog</span></span>

<span data-ttu-id="fd724-180">Диалоговые окна для собраний отображаются на этапе собрания Teams.</span><span class="sxs-lookup"><span data-stu-id="fd724-180">In-meeting dialogs display on the Teams meeting stage.</span></span> <span data-ttu-id="fd724-181">Для них требуется вмешательство пользователя, подтверждение или участие, но они не прерывают собрание.</span><span class="sxs-lookup"><span data-stu-id="fd724-181">They require a user's attention, confirmation, or interaction but are subtle and don't interrupt the meeting.</span></span> <span data-ttu-id="fd724-182">Их следует использовать с осторожностью, а для непростых и ориентированных на задачи сценариев.</span><span class="sxs-lookup"><span data-stu-id="fd724-182">You should use these sparingly and for scenarios that are light and task oriented.</span></span>

### <a name="use-cases"></a><span data-ttu-id="fd724-183">Варианты использования</span><span class="sxs-lookup"><span data-stu-id="fd724-183">Use cases</span></span>

<span data-ttu-id="fd724-184">Диалоговые окна для собраний запускаются пользователем (например организатором собрания), которые могут заинтересовать следующих участников:</span><span class="sxs-lookup"><span data-stu-id="fd724-184">In-meeting dialogs are triggered by a user (such as the meeting organizer) who might want participants to:</span></span>

* <span data-ttu-id="fd724-185">Предоставление кратких отзывов</span><span class="sxs-lookup"><span data-stu-id="fd724-185">Provide brief feedback</span></span>
* <span data-ttu-id="fd724-186">Получение короткого опроса или опроса</span><span class="sxs-lookup"><span data-stu-id="fd724-186">Take a short survey or poll</span></span>
* <span data-ttu-id="fd724-187">Предоставление утверждений</span><span class="sxs-lookup"><span data-stu-id="fd724-187">Submit approvals</span></span>
* <span data-ttu-id="fd724-188">Получение напоминаний</span><span class="sxs-lookup"><span data-stu-id="fd724-188">Get reminders</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-dialog.png" alt-text="В примере показано, как использовать диалоговое окно для собраний." border="false":::

### <a name="anatomy-in-meeting-dialog"></a><span data-ttu-id="fd724-190">Структура: диалоговое окно для собраний</span><span class="sxs-lookup"><span data-stu-id="fd724-190">Anatomy: In-meeting dialog</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-anatomy.png" alt-text="В примере показана структура структуры диалогового окна для собраний." border="false":::

|<span data-ttu-id="fd724-192">Счетчик</span><span class="sxs-lookup"><span data-stu-id="fd724-192">Counter</span></span>|<span data-ttu-id="fd724-193">Описание</span><span class="sxs-lookup"><span data-stu-id="fd724-193">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="fd724-194">1</span><span class="sxs-lookup"><span data-stu-id="fd724-194">1</span></span>|<span data-ttu-id="fd724-195">**Верхний колонтитул**: включает значок приложения, имя, строку действия и значок закрытия.</span><span class="sxs-lookup"><span data-stu-id="fd724-195">**Header**: Includes app icon, name, action string, and close icon.</span></span>|
|<span data-ttu-id="fd724-196">2 </span><span class="sxs-lookup"><span data-stu-id="fd724-196">2</span></span>|<span data-ttu-id="fd724-197">**IFRAME**: отображение контента приложения.</span><span class="sxs-lookup"><span data-stu-id="fd724-197">**iframe**: Displays your app content.</span></span>|

### <a name="anatomy-in-meeting-dialog-header"></a><span data-ttu-id="fd724-198">Структура: заголовок диалогового окна собрания</span><span class="sxs-lookup"><span data-stu-id="fd724-198">Anatomy: In-meeting dialog header</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-header-anatomy.png" alt-text="В примере показана структура структуры заголовка диалогового окна для собраний." border="false":::

<span data-ttu-id="fd724-200">Существует два варианта заголовков.</span><span class="sxs-lookup"><span data-stu-id="fd724-200">There are two header variants.</span></span> <span data-ttu-id="fd724-201">По возможности используйте вариант с Аватаром, чтобы подкрепить диалоговое окно от человека.</span><span class="sxs-lookup"><span data-stu-id="fd724-201">When possible, use the variant with the avatar to reinforce that the dialog is coming from a person.</span></span>

|<span data-ttu-id="fd724-202">Счетчик</span><span class="sxs-lookup"><span data-stu-id="fd724-202">Counter</span></span>|<span data-ttu-id="fd724-203">Описание</span><span class="sxs-lookup"><span data-stu-id="fd724-203">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="fd724-204">1</span><span class="sxs-lookup"><span data-stu-id="fd724-204">1</span></span>|<span data-ttu-id="fd724-205">**Аватар**: пользователь, инициирующий диалоговое окно в собрании.</span><span class="sxs-lookup"><span data-stu-id="fd724-205">**Avatar**: Person who initiates the in-meeting dialog.</span></span>|
|<span data-ttu-id="fd724-206">2 </span><span class="sxs-lookup"><span data-stu-id="fd724-206">2</span></span>|<span data-ttu-id="fd724-207">**Значок приложения**</span><span class="sxs-lookup"><span data-stu-id="fd724-207">**App icon**</span></span>|
|<span data-ttu-id="fd724-208">3 </span><span class="sxs-lookup"><span data-stu-id="fd724-208">3</span></span>|<span data-ttu-id="fd724-209">**Имя приложения**</span><span class="sxs-lookup"><span data-stu-id="fd724-209">**App name**</span></span>|
|<span data-ttu-id="fd724-210">4 </span><span class="sxs-lookup"><span data-stu-id="fd724-210">4</span></span>|<span data-ttu-id="fd724-211">**Кнопка "Закрыть"**: диалоговое окно закрывается.</span><span class="sxs-lookup"><span data-stu-id="fd724-211">**Close button**: Dismisses the dialog.</span></span>|
|<span data-ttu-id="fd724-212">5 </span><span class="sxs-lookup"><span data-stu-id="fd724-212">5</span></span>|<span data-ttu-id="fd724-213">**Строка действия**: обычно описывает, кто инициировал диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="fd724-213">**Action string**: Typically describes who initiated the dialog.</span></span>|

### <a name="responsive-behavior"></a><span data-ttu-id="fd724-214">Адаптируемое поведение</span><span class="sxs-lookup"><span data-stu-id="fd724-214">Responsive behavior</span></span>

<span data-ttu-id="fd724-215">Размер диалоговых окон для собраний может различаться в зависимости от различных сценариев.</span><span class="sxs-lookup"><span data-stu-id="fd724-215">In-meeting dialogs can vary in size to account for different scenarios.</span></span> <span data-ttu-id="fd724-216">Обязательно сохраните размеры полей и компонентов.</span><span class="sxs-lookup"><span data-stu-id="fd724-216">Make sure to maintain padding and component sizes.</span></span>

* <span data-ttu-id="fd724-217">**Ширина**: ширина интернет-кадра является абсолютным значением в указанном диапазоне.</span><span class="sxs-lookup"><span data-stu-id="fd724-217">**Width**: The iframe width is an absolute value within the range you specify.</span></span>
* <span data-ttu-id="fd724-218">**Height**: высота диалогового окна определяется содержимым в IFRAME.</span><span class="sxs-lookup"><span data-stu-id="fd724-218">**Height**: The height of the dialog is determined by the content in the iframe.</span></span> <span data-ttu-id="fd724-219">Вертикальная прокрутка занимает больше места для контента, который превышает максимальную высоту.</span><span class="sxs-lookup"><span data-stu-id="fd724-219">Vertical scroll takes over for content that exceeds the maximum height.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-responsive.png" alt-text="В примере показано диалоговое окно для собраний. Ширина: min--280 пикселей (248 пикселей IFRAME). Max--460 пикселей (в кадре IFRAME в 428 пикселей). Высота: 300 пикселей (IFRAME)." border="false":::

## <a name="after-a-meeting"></a><span data-ttu-id="fd724-221">После собрания</span><span class="sxs-lookup"><span data-stu-id="fd724-221">After a meeting</span></span>

<span data-ttu-id="fd724-222">Вы можете вернуться к собранию после его завершения и просмотреть контент приложения.</span><span class="sxs-lookup"><span data-stu-id="fd724-222">You can go back to a meeting after it ends and view app content.</span></span> <span data-ttu-id="fd724-223">В этом примере организатор собрания может просматривать результаты опроса на вкладке **contoso** . (Примечание: с точки зрения проекта различия между вкладками, выполняемыми до и после собрания, не различаются.)</span><span class="sxs-lookup"><span data-stu-id="fd724-223">In this example, the meeting organizer can look at poll results in the **Contoso** tab. (Note: From a design standpoint, there's no difference between a the pre- and post-meeting tab experience.)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/post-meeting-experience.png" alt-text="В примере показана вкладка после собрания." border="false":::

## <a name="best-practices"></a><span data-ttu-id="fd724-225">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="fd724-225">Best practices</span></span>

### <a name="interactions"></a><span data-ttu-id="fd724-226">Диалог</span><span class="sxs-lookup"><span data-stu-id="fd724-226">Interactions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-do.png" alt-text="Пример, иллюстрирующий рекомендации по добавочному номеру собрания." border="false":::

#### <a name="do-limit-the-number-of-interactions"></a><span data-ttu-id="fd724-228">Do: Ограничьте число взаимодействий</span><span class="sxs-lookup"><span data-stu-id="fd724-228">Do: Limit the number of interactions</span></span>

<span data-ttu-id="fd724-229">В диалоговых окнах для собраний удалите ненужные материалы, не позволяющие пользователям быстро выполнить какие-либо действия.</span><span class="sxs-lookup"><span data-stu-id="fd724-229">For in-meeting dialogs, remove unnecessary content that doesn't help users accomplish something quickly.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-dont.png" alt-text="Пример, иллюстрирующий рекомендации по добавочному номеру собрания." border="false":::

#### <a name="dont-introduce-unnecessary-elements"></a><span data-ttu-id="fd724-231">Не следует добавлять ненужные элементы.</span><span class="sxs-lookup"><span data-stu-id="fd724-231">Don't: Introduce unnecessary elements</span></span>

<span data-ttu-id="fd724-232">Отдельное диалоговое окно для собраний с несколькими взаимодействиями может отвлечь от вызова.</span><span class="sxs-lookup"><span data-stu-id="fd724-232">A single in-meeting dialog with multiple interactions can distract from the call.</span></span>

   :::column-end:::
:::row-end:::

### <a name="layout"></a><span data-ttu-id="fd724-233">Макет</span><span class="sxs-lookup"><span data-stu-id="fd724-233">Layout</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-do.png" alt-text="Пример, иллюстрирующий рекомендации по добавочному номеру собрания." border="false":::

#### <a name="do-use-single-column-layouts"></a><span data-ttu-id="fd724-235">Do: использование макетов с одним столбцом</span><span class="sxs-lookup"><span data-stu-id="fd724-235">Do: Use single-column layouts</span></span>

<span data-ttu-id="fd724-236">Так как диалоги находятся в центре этапа собрания, выполнение задачи должно быть быстрым и простым, чтобы избежать недовольство пользователей.</span><span class="sxs-lookup"><span data-stu-id="fd724-236">Since the dialogs are at the center of the meeting stage, task completion should be fast and simple to avoid user frustration.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-dont.png" alt-text="Пример, иллюстрирующий рекомендации по добавочному номеру собрания." border="false":::

#### <a name="dont-clutter-the-space"></a><span data-ttu-id="fd724-238">Не совсем: незагромождения места</span><span class="sxs-lookup"><span data-stu-id="fd724-238">Don't: Clutter the space</span></span>

<span data-ttu-id="fd724-239">Сжатые и более структурированные контент могут отвлекаться и передаваться, особенно во время собрания.</span><span class="sxs-lookup"><span data-stu-id="fd724-239">Dense or overly structured content can be distracting and overwhelming, especially during a meeting.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-do.png" alt-text="Пример, иллюстрирующий рекомендации по добавочному номеру собрания." border="false":::

#### <a name="do-use-single-columns"></a><span data-ttu-id="fd724-241">Do: использование одиночных столбцов</span><span class="sxs-lookup"><span data-stu-id="fd724-241">Do: Use single columns</span></span>

<span data-ttu-id="fd724-242">При наличии узкой природы вкладки в собрании настоятельно рекомендуется отобразить содержимое в отдельном столбце.</span><span class="sxs-lookup"><span data-stu-id="fd724-242">Given the in-meeting tab's narrow nature, we strongly recommend displaying the contents in a single column.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-dont.png" alt-text="Пример, иллюстрирующий рекомендации по добавочному номеру собрания." border="false":::

#### <a name="dont-use-multiple-columns"></a><span data-ttu-id="fd724-244">Не: использовать несколько столбцов</span><span class="sxs-lookup"><span data-stu-id="fd724-244">Don't: Use multiple columns</span></span>

<span data-ttu-id="fd724-245">Из-за ограниченного пространства вкладки в собрании не рекомендуется использовать макеты с несколькими столбцами.</span><span class="sxs-lookup"><span data-stu-id="fd724-245">Due to the limited space of the in-meeting tab, layouts with more than one column aren’t recommended.</span></span>

   :::column-end:::
:::row-end:::

### <a name="controls"></a><span data-ttu-id="fd724-246">Элементы управления</span><span class="sxs-lookup"><span data-stu-id="fd724-246">Controls</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-do.png" alt-text="Пример, иллюстрирующий рекомендации по добавочному номеру собрания." border="false":::

#### <a name="do-right-align-the-primary-action"></a><span data-ttu-id="fd724-248">Do: выравнивание по правому краю основного действия</span><span class="sxs-lookup"><span data-stu-id="fd724-248">Do: Right align the primary action</span></span>

<span data-ttu-id="fd724-249">Мы рекомендуем поситиоининг наиболее визуально активное действие в крайнем правом расположении.</span><span class="sxs-lookup"><span data-stu-id="fd724-249">We recommend positioining the most visually heavy action to the right-most location.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-dont.png" alt-text="Пример, иллюстрирующий рекомендации по добавочному номеру собрания." border="false":::

#### <a name="dont-left-or-center-align-actions"></a><span data-ttu-id="fd724-251">Не: действия слева или Выровнять по центру</span><span class="sxs-lookup"><span data-stu-id="fd724-251">Don't: Left or center align actions</span></span>

<span data-ttu-id="fd724-252">Это отличается от стандартного шаблона команд для управления размещением в диалоговом окне и может конфликтовать с диалоговым окном, расположенным в верхней части.</span><span class="sxs-lookup"><span data-stu-id="fd724-252">This deviates from the standard Teams pattern for control placement in a dialog and may conflict with a dialog behind the top one.</span></span>

   :::column-end:::
:::row-end:::

### <a name="scroll"></a><span data-ttu-id="fd724-253">Прокрутка</span><span class="sxs-lookup"><span data-stu-id="fd724-253">Scroll</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-do.png" alt-text="Пример, иллюстрирующий рекомендации по добавочному номеру собрания." border="false":::

#### <a name="do-scroll-vertically"></a><span data-ttu-id="fd724-255">Do: вертикальная прокрутка</span><span class="sxs-lookup"><span data-stu-id="fd724-255">Do: Scroll vertically</span></span>

<span data-ttu-id="fd724-256">Мы рекомендуем расместить наиболее визуально активное действие в крайнем крайнем месте.</span><span class="sxs-lookup"><span data-stu-id="fd724-256">We recommend positioning the most visually heavy action to the right-most location.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-dont.png" alt-text="Пример, иллюстрирующий рекомендации по добавочному номеру собрания." border="false":::

#### <a name="dont-scroll-horizontally"></a><span data-ttu-id="fd724-258">Не: прокручивать по горизонтали</span><span class="sxs-lookup"><span data-stu-id="fd724-258">Don't: Scroll horizontally</span></span>

<span data-ttu-id="fd724-259">Горизонтальная полоса прокрутки не является ожидаемым поведением в Teams.</span><span class="sxs-lookup"><span data-stu-id="fd724-259">Horizontal scrolling isn’t an expected behavior in Teams.</span></span> <span data-ttu-id="fd724-260">Другие холсты в среде проведения собраний прокручиваются вертикально.</span><span class="sxs-lookup"><span data-stu-id="fd724-260">Other canvases in the meeting environment scroll vertically.</span></span>

   :::column-end:::
:::row-end:::

### <a name="workflows"></a><span data-ttu-id="fd724-261">Рабочие процессы</span><span class="sxs-lookup"><span data-stu-id="fd724-261">Workflows</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-workflow-do.png" alt-text="Пример, иллюстрирующий рекомендации по добавочному номеру собрания." border="false":::

#### <a name="do-surface-complex-scenarios-in-the-in-meeting-tab"></a><span data-ttu-id="fd724-263">Do: сложные сценарии на вкладке "на собрании"</span><span class="sxs-lookup"><span data-stu-id="fd724-263">Do: Surface complex scenarios in the in-meeting tab</span></span>

<span data-ttu-id="fd724-264">Если ваше приложение содержит несколько задач, настоятельно рекомендуется использовать макет с одним столбцом на вкладке на собрании.</span><span class="sxs-lookup"><span data-stu-id="fd724-264">If your app includes multiple tasks, we strongly recommend a single-column layout in an in-meeting tab.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-workflow-dont.png" alt-text="Пример, иллюстрирующий рекомендации по добавочному номеру собрания." border="false":::

#### <a name="dont-package-complex-scenarios-in-the-in-meeting-dialog"></a><span data-ttu-id="fd724-266">Не: сложные сценарии в диалоговом окне "в собрании"</span><span class="sxs-lookup"><span data-stu-id="fd724-266">Don't: Package complex scenarios in the in-meeting dialog</span></span>

<span data-ttu-id="fd724-267">Диалоги в собрании предназначены для кратких интерактивных действий.</span><span class="sxs-lookup"><span data-stu-id="fd724-267">In-meeting dialogs are intended for brief interactions.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="fd724-268">Темы</span><span class="sxs-lookup"><span data-stu-id="fd724-268">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-do.png" alt-text="Пример, иллюстрирующий рекомендации по добавочному номеру собрания." border="false":::

#### <a name="do-use-teams-color-tokens"></a><span data-ttu-id="fd724-270">Do: использование цветовых маркеров Team</span><span class="sxs-lookup"><span data-stu-id="fd724-270">Do: Use Teams color tokens</span></span>

<span data-ttu-id="fd724-271">Собрания Teams оптимизированы для темного режима, что позволяет снизить визуальное и пользовательское шум, чтобы пользователи могли сосредоточиться на обсуждении и общем содержимом.</span><span class="sxs-lookup"><span data-stu-id="fd724-271">Teams meetings are optimized for dark mode to help reduce visual and cognitive noise so users can focus on the discussion and shared content.</span></span> <span data-ttu-id="fd724-272">Сведения об использовании <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">цветовых маркеров (пользовательский интерфейс Fluent)</a>.</span><span class="sxs-lookup"><span data-stu-id="fd724-272">Learn about using <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a>.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-dont.png" alt-text="Пример, иллюстрирующий рекомендации по добавочному номеру собрания." border="false":::

#### <a name="dont-include-another-dismiss-button"></a><span data-ttu-id="fd724-274">Не: включить еще одну кнопку закрытия</span><span class="sxs-lookup"><span data-stu-id="fd724-274">Don't: Include another dismiss button</span></span>

<span data-ttu-id="fd724-275">Предоставление возможности закрыть содержимое вкладки собраний может привести к проблемам, так как в заголовке уже есть кнопка для закрытия вкладки в собрании.</span><span class="sxs-lookup"><span data-stu-id="fd724-275">Providing an option to close in-meeting tab content may cause issues since there’s already a button in the header to dismiss the in-meeting tab itself.</span></span>

   :::column-end:::
:::row-end:::

### <a name="navigation"></a><span data-ttu-id="fd724-276">Навигация</span><span class="sxs-lookup"><span data-stu-id="fd724-276">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-do.png" alt-text="Пример, иллюстрирующий рекомендации по добавочному номеру собрания." border="false":::

#### <a name="do-have-a-back-button"></a><span data-ttu-id="fd724-278">Do: кнопка "назад"</span><span class="sxs-lookup"><span data-stu-id="fd724-278">Do: Have a back button</span></span>

<span data-ttu-id="fd724-279">Если на вкладке на собрании имеется несколько слоев навигации, пользователи должны иметь возможность вернуться к предыдущим представлениям.</span><span class="sxs-lookup"><span data-stu-id="fd724-279">If you have more than one layer of navigation in an in-meeting tab, users must be able to go back to their previous views.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-dont.png" alt-text="Пример, иллюстрирующий рекомендации по добавочному номеру собрания." border="false":::

#### <a name="dont-include-another-dismiss-button"></a><span data-ttu-id="fd724-281">Не: включить еще одну кнопку закрытия</span><span class="sxs-lookup"><span data-stu-id="fd724-281">Don't: Include another dismiss button</span></span>

<span data-ttu-id="fd724-282">Предоставление возможности закрыть содержимое вкладки собраний может привести к проблемам, так как в заголовке уже есть кнопка для закрытия вкладки в собрании.</span><span class="sxs-lookup"><span data-stu-id="fd724-282">Providing an option to close in-meeting tab content may cause issues since there’s already a button in the header to dismiss the in-meeting tab itself.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-caution.png" alt-text="Пример, иллюстрирующий рекомендации по добавочному номеру собрания." border="false":::

#### <a name="caution-avoid-modals-within-the-in-meeting-tab"></a><span data-ttu-id="fd724-284">Внимание! не используйте модальные окна на вкладке "собрание".</span><span class="sxs-lookup"><span data-stu-id="fd724-284">Caution: Avoid modals within the in-meeting tab</span></span>

<span data-ttu-id="fd724-285">Модальные (также называемые модулями задач) в уже узкой вкладке "собрание" могут переносить и скрывать содержимое.</span><span class="sxs-lookup"><span data-stu-id="fd724-285">Modals (also known as task modules) in the already narrow in-meeting tab might wrap and obscure the content.</span></span>

   :::column-end:::
:::row-end:::

## <a name="validate-your-design"></a><span data-ttu-id="fd724-286">Проверка проекта</span><span class="sxs-lookup"><span data-stu-id="fd724-286">Validate your design</span></span>

<span data-ttu-id="fd724-287">Если вы планируете опубликовать свое приложение в AppSource, следует изучить проблемы, которые обычно приводят к сбою приложений во время отправки.</span><span class="sxs-lookup"><span data-stu-id="fd724-287">If you plan to publish your app to AppSource, you should understand the design issues that commonly cause apps to fail during submission.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fd724-288">Проверка рекомендаций по проверке макета</span><span class="sxs-lookup"><span data-stu-id="fd724-288">Check design validation guidelines</span></span>](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
