---
title: Проектирование расширения собрания
author: heath-hamilton
description: Узнайте, как проектировать приложения на собраниях Teams и получать пакет пользовательского интерфейса Microsoft Teams.
ms.author: lajanuar
ms.topic: conceptual
ms.openlocfilehash: c6e76356b698da4e32e279b0842ab2cc35254e99
ms.sourcegitcommit: 84f408aa2854aa7a5cefaa66ce9a373b19e0864a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/18/2021
ms.locfileid: "49886760"
---
# <a name="designing-your-microsoft-teams-meeting-extension"></a><span data-ttu-id="442f5-103">Разработка расширения собрания Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="442f5-103">Designing your Microsoft Teams meeting extension</span></span>

<span data-ttu-id="442f5-104">Вы можете создавать приложения, чтобы сделать собрания более эффективными.</span><span class="sxs-lookup"><span data-stu-id="442f5-104">You can create apps to make meetings more productive.</span></span> <span data-ttu-id="442f5-105">Например, попросите людей выполнить опрос во время вызова или отправить краткое напоминание, которое не прерывает поток собрания.</span><span class="sxs-lookup"><span data-stu-id="442f5-105">For example, ask people to complete a survey during a call or send a quick reminder that doesn’t interrupt the flow of the meeting.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="442f5-106">Пакет пользовательского интерфейса Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="442f5-106">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="442f5-107">В пакете пользовательского интерфейса Microsoft Teams можно найти более комплексные рекомендации по проектированию, включая элементы, которые можно захватить и изменить при необходимости.</span><span class="sxs-lookup"><span data-stu-id="442f5-107">You can find more comprehensive design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="442f5-108">Get the Microsoft Teams UI Kit (Figma)</span><span class="sxs-lookup"><span data-stu-id="442f5-108">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-meeting-extension"></a><span data-ttu-id="442f5-109">Добавление расширения собрания</span><span class="sxs-lookup"><span data-stu-id="442f5-109">Add a meeting extension</span></span>

<span data-ttu-id="442f5-110">Вы можете добавить расширение собрания до и во время собраний.</span><span class="sxs-lookup"><span data-stu-id="442f5-110">You can add a meeting extension before and during meetings.</span></span> <span data-ttu-id="442f5-111">Вы также можете добавить приложение для определенного собрания непосредственно из Магазина Teams (AppSource).</span><span class="sxs-lookup"><span data-stu-id="442f5-111">You also can add an app for a specific meeting directly from the Teams store (AppSource).</span></span>

### <a name="add-before-a-meeting"></a><span data-ttu-id="442f5-112">Добавить перед собранием</span><span class="sxs-lookup"><span data-stu-id="442f5-112">Add before a meeting</span></span>

<span data-ttu-id="442f5-113">В сведениях о собрании выберите **"Добавить вкладку" +,** чтобы открыть войдите в приложение, и найдите приложения, оптимизированные для собраний.</span><span class="sxs-lookup"><span data-stu-id="442f5-113">In the meeting details, select **Add a tab +** to open the app flyout and find apps optimized for meetings.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/add-before-meeting.png" alt-text="В примере показано, как добавить расширение собрания перед собранием." border="false":::

### <a name="add-during-a-meeting"></a><span data-ttu-id="442f5-115">Добавление во время собрания</span><span class="sxs-lookup"><span data-stu-id="442f5-115">Add during a meeting</span></span>

На собрании выберите **"Добавить** :::image type="icon" source="../../assets/icons/teams-client-more.png":::  >  **приложение" и** выберите нужное приложение.

:::image type="content" source="../../assets/images/apps-in-meetings/add-during-meeting.png" alt-text="В примере показано, как добавить расширение собрания во время собрания." border="false":::

## <a name="before-a-meeting"></a><span data-ttu-id="442f5-118">Перед собранием</span><span class="sxs-lookup"><span data-stu-id="442f5-118">Before a meeting</span></span>

<span data-ttu-id="442f5-119">Перед собранием можно добавить содержимое на вкладку. В следующем примере показан черновик вопроса опроса, на который люди ответят во время вызова.</span><span class="sxs-lookup"><span data-stu-id="442f5-119">Prior to your meeting, you can add content in the tab. The following example shows a draft survey question that people will answer during the call.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/before-meeting-tab.png" alt-text="В примере показано, как приложение в сведениях о собрании перед вызовом." border="false":::

### <a name="anatomy-meeting-tab-before-and-after-meetings"></a><span data-ttu-id="442f5-121">Структура: вкладка "Собрание" (до и после собрания)</span><span class="sxs-lookup"><span data-stu-id="442f5-121">Anatomy: Meeting tab (before and after meetings)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/meeting-details-tab-anatomy.png" alt-text="В примере показана структурная структура вкладки собрания до и после собрания." border="false":::

|<span data-ttu-id="442f5-123">Счетчик</span><span class="sxs-lookup"><span data-stu-id="442f5-123">Counter</span></span>|<span data-ttu-id="442f5-124">Описание</span><span class="sxs-lookup"><span data-stu-id="442f5-124">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="442f5-125">1</span><span class="sxs-lookup"><span data-stu-id="442f5-125">1</span></span>|<span data-ttu-id="442f5-126">**Имя вкладки:** метка навигации для вкладки.</span><span class="sxs-lookup"><span data-stu-id="442f5-126">**Tab name**: Navigation label for your tab.</span></span>|
|<span data-ttu-id="442f5-127">2 </span><span class="sxs-lookup"><span data-stu-id="442f5-127">2</span></span>|<span data-ttu-id="442f5-128">**Переполнение вкладки:** открывает действия с вкладками, например переименовывать и удалять.</span><span class="sxs-lookup"><span data-stu-id="442f5-128">**Tab overflow**: Opens tab actions, such as rename and remove.</span></span>|
|<span data-ttu-id="442f5-129">3</span><span class="sxs-lookup"><span data-stu-id="442f5-129">3</span></span>|<span data-ttu-id="442f5-130">**iframe**: отображает содержимое приложения.</span><span class="sxs-lookup"><span data-stu-id="442f5-130">**iframe**: Displays your app content.</span></span>|

### <a name="designing-with-ui-templates"></a><span data-ttu-id="442f5-131">Проектирование с помощью шаблонов пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="442f5-131">Designing with UI templates</span></span>

<span data-ttu-id="442f5-132">Используйте один из следующих шаблонов пользовательского интерфейса Teams для разработки вкладки для собраний:</span><span class="sxs-lookup"><span data-stu-id="442f5-132">Use one of the following Teams UI templates to help design your meeting tab:</span></span>

* <span data-ttu-id="442f5-133">[Список:](../../concepts/design/design-teams-app-ui-templates.md#list)списки могут отображать связанные элементы в сканируемых форматах и позволяют пользователям делать действия со всем списком или отдельными элементами.</span><span class="sxs-lookup"><span data-stu-id="442f5-133">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="442f5-134">[Доска](../../concepts/design/design-teams-app-ui-templates.md#task-board)задач: доска задач, иногда называемая доской канба или плаваемой, — это коллекция карточек, часто используемых для отслеживания состояния элементов или билетов.</span><span class="sxs-lookup"><span data-stu-id="442f5-134">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="442f5-135">[Информационная](../../concepts/design/design-teams-app-ui-templates.md#dashboard)панель : панель мониторинга — это холст, содержащий несколько карточек, которые предоставляют обзор данных или содержимого.</span><span class="sxs-lookup"><span data-stu-id="442f5-135">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="442f5-136">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span><span class="sxs-lookup"><span data-stu-id="442f5-136">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="442f5-137">[Пустое](../../concepts/design/design-teams-app-ui-templates.md#empty-state)состояние: пустой шаблон состояния можно использовать для многих сценариев, включая вход, первый запуск, сообщения об ошибках и многое другое.</span><span class="sxs-lookup"><span data-stu-id="442f5-137">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="442f5-138">[Левый навигационный](../../concepts/design/design-teams-app-ui-templates.md#left-nav)шаблон : левый шаблон навигации может помочь, если вкладка требует определенной навигации.</span><span class="sxs-lookup"><span data-stu-id="442f5-138">[Left nav](../../concepts/design/design-teams-app-ui-templates.md#left-nav): The left nav template can help if your tab requires some navigation.</span></span> <span data-ttu-id="442f5-139">Как правило, навигация по вкладке должна быть минимальной.</span><span class="sxs-lookup"><span data-stu-id="442f5-139">In general, you should keep tab navigation to a minimum.</span></span>

## <a name="use-an-in-meeting-tab"></a><span data-ttu-id="442f5-140">Использование вкладки "Собрание"</span><span class="sxs-lookup"><span data-stu-id="442f5-140">Use an in-meeting tab</span></span>

<span data-ttu-id="442f5-141">Вкладка "Собрание" — это холст для расширения совместной работы во время собраний.</span><span class="sxs-lookup"><span data-stu-id="442f5-141">The in-meeting tab is a canvas for augmenting collaboration during meetings.</span></span> <span data-ttu-id="442f5-142">Участники могут видеть содержимое приложения и взаимодействовать с ним в выделенном пространстве вне стадии собрания с помощью общих представлений или представлений на основе ролей.</span><span class="sxs-lookup"><span data-stu-id="442f5-142">Attendees can see and interact with app content in a dedicated space outside the meeting stage through shared or role-based views.</span></span>

### <a name="use-cases"></a><span data-ttu-id="442f5-143">Варианты использования</span><span class="sxs-lookup"><span data-stu-id="442f5-143">Use cases</span></span>

<span data-ttu-id="442f5-144">На вкладке "Собрание" можно:</span><span class="sxs-lookup"><span data-stu-id="442f5-144">People might use the in-meeting tab to:</span></span>

* <span data-ttu-id="442f5-145">Предоставление подробных отзывов (например, оценка кандидата на должность)</span><span class="sxs-lookup"><span data-stu-id="442f5-145">Provide detailed feedback (for example, evaluate a job candidate)</span></span>
* <span data-ttu-id="442f5-146">Быстрое создание опроса, опроса или элемента задачи для участников собрания</span><span class="sxs-lookup"><span data-stu-id="442f5-146">Quickly create a poll, survey, or task item for the meeting participants</span></span>
* <span data-ttu-id="442f5-147">Отображение заметок, релевантных для собрания (например, сведения о менеджере по продажам)</span><span class="sxs-lookup"><span data-stu-id="442f5-147">Display notes relevant to the meeting (for example, information about a sales lead)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-tab.png" alt-text="В примере показано, как можно представить контент опроса на вкладке &quot;Собрание&quot;." border="false":::

### <a name="anatomy-in-meeting-tab"></a><span data-ttu-id="442f5-149">Структура: вкладка "Собрание"</span><span class="sxs-lookup"><span data-stu-id="442f5-149">Anatomy: In-meeting tab</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-anatomy.png" alt-text="В примере показана структурная структура вкладки на собрании." border="false":::

|<span data-ttu-id="442f5-151">Счетчик</span><span class="sxs-lookup"><span data-stu-id="442f5-151">Counter</span></span>|<span data-ttu-id="442f5-152">Описание</span><span class="sxs-lookup"><span data-stu-id="442f5-152">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="442f5-153">1</span><span class="sxs-lookup"><span data-stu-id="442f5-153">1</span></span>|<span data-ttu-id="442f5-154">**Значок приложения (выбранный)**: прозрачный логотип приложения размером 16 пикселей.</span><span class="sxs-lookup"><span data-stu-id="442f5-154">**App icon (selected)**: 16-pixel transparent app logo.</span></span>|
|<span data-ttu-id="442f5-155">2 </span><span class="sxs-lookup"><span data-stu-id="442f5-155">2</span></span>|<span data-ttu-id="442f5-156">**Имя приложения**</span><span class="sxs-lookup"><span data-stu-id="442f5-156">**App name**</span></span>|
|<span data-ttu-id="442f5-157">3</span><span class="sxs-lookup"><span data-stu-id="442f5-157">3</span></span>|<span data-ttu-id="442f5-158">**Заготовка:** включает имя приложения.</span><span class="sxs-lookup"><span data-stu-id="442f5-158">**Header**: Includes your app name.</span></span>|
|<span data-ttu-id="442f5-159">4 </span><span class="sxs-lookup"><span data-stu-id="442f5-159">4</span></span>|<span data-ttu-id="442f5-160">**Кнопка закрытия:** закрывает вкладку. Всегда используйте верхний правый значок закрытия вместо действия в нижнем.</span><span class="sxs-lookup"><span data-stu-id="442f5-160">**Close button**: Dismisses the tab. Always use the upper-right close icon instead of an action in the footer.</span></span>|
|<span data-ttu-id="442f5-161">5 </span><span class="sxs-lookup"><span data-stu-id="442f5-161">5</span></span>|<span data-ttu-id="442f5-162">**Гистометр** уведомлений: оповещения об ошибках отображаются непосредственно под заголовком и выдвигают содержимое iframe вниз на 20 пикселей.</span><span class="sxs-lookup"><span data-stu-id="442f5-162">**Notification bar**: Error alerts display directly below the header and push the iframe content down by 20 pixels.</span></span>|
|<span data-ttu-id="442f5-163">6 </span><span class="sxs-lookup"><span data-stu-id="442f5-163">6</span></span>|<span data-ttu-id="442f5-164">**iframe**: отображает содержимое приложения.</span><span class="sxs-lookup"><span data-stu-id="442f5-164">**iframe**: Displays your app content.</span></span>|

### <a name="spacing"></a><span data-ttu-id="442f5-165">Интервал</span><span class="sxs-lookup"><span data-stu-id="442f5-165">Spacing</span></span>

<span data-ttu-id="442f5-166">Оптимизируйте вкладку, вместив ее в область iframe размером 280 пикселей.</span><span class="sxs-lookup"><span data-stu-id="442f5-166">Optimize your in-meeting tab to fit edge-to-edge within the 280 pixel-wide iframe area.</span></span> <span data-ttu-id="442f5-167">Слева и справа от iframe и между заголом вкладки имеется 20 пикселей заполнения.</span><span class="sxs-lookup"><span data-stu-id="442f5-167">There are 20 pixels of padding on the left and right sides of the iframe and between the tab header.</span></span> <span data-ttu-id="442f5-168">The iframe is full bleed to the bottom of the tab.</span><span class="sxs-lookup"><span data-stu-id="442f5-168">The iframe is full bleed to the bottom of the tab.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-spacing.png" alt-text="В примере показаны размеры интервала вкладок в собрании." border="false":::

### <a name="scrolling"></a><span data-ttu-id="442f5-170">Прокрутка</span><span class="sxs-lookup"><span data-stu-id="442f5-170">Scrolling</span></span>

<span data-ttu-id="442f5-171">Содержимое Iframe должно прокручиваться вертикально.</span><span class="sxs-lookup"><span data-stu-id="442f5-171">Iframe contents should scroll vertically.</span></span> <span data-ttu-id="442f5-172">Вы можете просмотреть только содержимое, которое вы прокрутите до (ничего выше или ниже).</span><span class="sxs-lookup"><span data-stu-id="442f5-172">You can only see the content you've scrolled to (nothing above or below).</span></span> <span data-ttu-id="442f5-173">Панель прокрутки является частью содержимого iframe.</span><span class="sxs-lookup"><span data-stu-id="442f5-173">The scrollbar is part of the iframe content.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-scrolling.png" alt-text="В примере показано, как прокручивается вкладка &quot;Собрание&quot;." border="false":::

### <a name="navigation"></a><span data-ttu-id="442f5-175">Навигация</span><span class="sxs-lookup"><span data-stu-id="442f5-175">Navigation</span></span>

<span data-ttu-id="442f5-176">В сценариях с уровнями навигации или большим содержимым мы рекомендуем разрешить пользователям переходить на дополнительный уровень.</span><span class="sxs-lookup"><span data-stu-id="442f5-176">For scenarios with navigation layers or heavy content, we recommend allowing users to navigate to a secondary layer.</span></span> <span data-ttu-id="442f5-177">Пользователи должны иметь возможность вернуться на предыдущий уровень.</span><span class="sxs-lookup"><span data-stu-id="442f5-177">Users must be able to go back to the previous layer.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav.png" alt-text="В примере показана навигация в собрании." border="false":::

## <a name="use-an-in-meeting-dialog"></a><span data-ttu-id="442f5-179">Использование диалогового окно собрания</span><span class="sxs-lookup"><span data-stu-id="442f5-179">Use an in-meeting dialog</span></span>

<span data-ttu-id="442f5-180">Диалоги собраний отображаются на стадии собрания Teams.</span><span class="sxs-lookup"><span data-stu-id="442f5-180">In-meeting dialogs display on the Teams meeting stage.</span></span> <span data-ttu-id="442f5-181">Они требуют внимания пользователя, подтверждения или взаимодействия, но являются незначительными и не прерывают собрание.</span><span class="sxs-lookup"><span data-stu-id="442f5-181">They require a user's attention, confirmation, or interaction but are subtle and don't interrupt the meeting.</span></span> <span data-ttu-id="442f5-182">Их следует использовать экономно и для сценариев, ориентированных на светлые и ориентированные на задачи.</span><span class="sxs-lookup"><span data-stu-id="442f5-182">You should use these sparingly and for scenarios that are light and task oriented.</span></span>

### <a name="use-cases"></a><span data-ttu-id="442f5-183">Варианты использования</span><span class="sxs-lookup"><span data-stu-id="442f5-183">Use cases</span></span>

<span data-ttu-id="442f5-184">Диалоговые окно собрания инициирует пользователь (например, организатор собрания), который может потребовать от участников:</span><span class="sxs-lookup"><span data-stu-id="442f5-184">In-meeting dialogs are triggered by a user (such as the meeting organizer) who might want participants to:</span></span>

* <span data-ttu-id="442f5-185">Предоставление краткой обратной связи</span><span class="sxs-lookup"><span data-stu-id="442f5-185">Provide brief feedback</span></span>
* <span data-ttu-id="442f5-186">Краткий опрос</span><span class="sxs-lookup"><span data-stu-id="442f5-186">Take a short survey or poll</span></span>
* <span data-ttu-id="442f5-187">Отправка утверждений</span><span class="sxs-lookup"><span data-stu-id="442f5-187">Submit approvals</span></span>
* <span data-ttu-id="442f5-188">Получать напоминания</span><span class="sxs-lookup"><span data-stu-id="442f5-188">Get reminders</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-dialog.png" alt-text="В примере показано, как можно использовать диалоговое окно собрания." border="false":::

### <a name="anatomy-in-meeting-dialog"></a><span data-ttu-id="442f5-190">Структура: диалоговое окно собрания</span><span class="sxs-lookup"><span data-stu-id="442f5-190">Anatomy: In-meeting dialog</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-anatomy.png" alt-text="В примере показана структурная структура диалогового окно собрания." border="false":::

|<span data-ttu-id="442f5-192">Счетчик</span><span class="sxs-lookup"><span data-stu-id="442f5-192">Counter</span></span>|<span data-ttu-id="442f5-193">Описание</span><span class="sxs-lookup"><span data-stu-id="442f5-193">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="442f5-194">1</span><span class="sxs-lookup"><span data-stu-id="442f5-194">1</span></span>|<span data-ttu-id="442f5-195">**Заглавная** строка: включает значок приложения, имя, строку действия и значок закрытия.</span><span class="sxs-lookup"><span data-stu-id="442f5-195">**Header**: Includes app icon, name, action string, and close icon.</span></span>|
|<span data-ttu-id="442f5-196">2 </span><span class="sxs-lookup"><span data-stu-id="442f5-196">2</span></span>|<span data-ttu-id="442f5-197">**iframe**: отображает содержимое приложения.</span><span class="sxs-lookup"><span data-stu-id="442f5-197">**iframe**: Displays your app content.</span></span>|

### <a name="anatomy-in-meeting-dialog-header"></a><span data-ttu-id="442f5-198">Структура: загор. Диалоговое окно собрания</span><span class="sxs-lookup"><span data-stu-id="442f5-198">Anatomy: In-meeting dialog header</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-header-anatomy.png" alt-text="В примере показана структурная структура загона диалога собрания." border="false":::

<span data-ttu-id="442f5-200">Существует два варианта загона.</span><span class="sxs-lookup"><span data-stu-id="442f5-200">There are two header variants.</span></span> <span data-ttu-id="442f5-201">По возможности используйте вариант с аватаром, чтобы подчеркнуть, что диалоговое окно идет от человека.</span><span class="sxs-lookup"><span data-stu-id="442f5-201">When possible, use the variant with the avatar to reinforce that the dialog is coming from a person.</span></span>

|<span data-ttu-id="442f5-202">Счетчик</span><span class="sxs-lookup"><span data-stu-id="442f5-202">Counter</span></span>|<span data-ttu-id="442f5-203">Описание</span><span class="sxs-lookup"><span data-stu-id="442f5-203">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="442f5-204">1</span><span class="sxs-lookup"><span data-stu-id="442f5-204">1</span></span>|<span data-ttu-id="442f5-205">**Аватар:** человек, который инициирует диалоговое окно собрания.</span><span class="sxs-lookup"><span data-stu-id="442f5-205">**Avatar**: Person who initiates the in-meeting dialog.</span></span>|
|<span data-ttu-id="442f5-206">2 </span><span class="sxs-lookup"><span data-stu-id="442f5-206">2</span></span>|<span data-ttu-id="442f5-207">**Значок приложения**</span><span class="sxs-lookup"><span data-stu-id="442f5-207">**App icon**</span></span>|
|<span data-ttu-id="442f5-208">3</span><span class="sxs-lookup"><span data-stu-id="442f5-208">3</span></span>|<span data-ttu-id="442f5-209">**Имя приложения**</span><span class="sxs-lookup"><span data-stu-id="442f5-209">**App name**</span></span>|
|<span data-ttu-id="442f5-210">4 </span><span class="sxs-lookup"><span data-stu-id="442f5-210">4</span></span>|<span data-ttu-id="442f5-211">**Кнопка закрытия:** закрывает диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="442f5-211">**Close button**: Dismisses the dialog.</span></span>|
|<span data-ttu-id="442f5-212">5 </span><span class="sxs-lookup"><span data-stu-id="442f5-212">5</span></span>|<span data-ttu-id="442f5-213">**Строка** действия: обычно описывает, кто инициировал диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="442f5-213">**Action string**: Typically describes who initiated the dialog.</span></span>|

### <a name="responsive-behavior"></a><span data-ttu-id="442f5-214">Адаптируемое поведение</span><span class="sxs-lookup"><span data-stu-id="442f5-214">Responsive behavior</span></span>

<span data-ttu-id="442f5-215">Диалоги собраний могут различаться по размеру в зависимости от различных сценариев.</span><span class="sxs-lookup"><span data-stu-id="442f5-215">In-meeting dialogs can vary in size to account for different scenarios.</span></span> <span data-ttu-id="442f5-216">Обязательно поддержив заполнение и размеры компонентов.</span><span class="sxs-lookup"><span data-stu-id="442f5-216">Make sure to maintain padding and component sizes.</span></span>

* <span data-ttu-id="442f5-217">**Width**:The iframe width is an absolute value within the range you specify.</span><span class="sxs-lookup"><span data-stu-id="442f5-217">**Width**: The iframe width is an absolute value within the range you specify.</span></span>
* <span data-ttu-id="442f5-218">**Height**: высота диалогового окно определяется содержимым в iframe.</span><span class="sxs-lookup"><span data-stu-id="442f5-218">**Height**: The height of the dialog is determined by the content in the iframe.</span></span> <span data-ttu-id="442f5-219">Вертикальная прокрутка берет на себя содержимое, которое превышает максимальную высоту.</span><span class="sxs-lookup"><span data-stu-id="442f5-219">Vertical scroll takes over for content that exceeds the maximum height.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-responsive.png" alt-text="В примере показано диалоговое окно собрания. Ширина: min--280 пикселей (iframe 248 пикселей). Max --460 пикселей (iframe 428 пикселей). Высота: 300 пикселей (iframe)." border="false":::

## <a name="after-a-meeting"></a><span data-ttu-id="442f5-221">После собрания</span><span class="sxs-lookup"><span data-stu-id="442f5-221">After a meeting</span></span>

<span data-ttu-id="442f5-222">Вы можете вернуться к собранию после его окончания и просмотреть содержимое приложения.</span><span class="sxs-lookup"><span data-stu-id="442f5-222">You can go back to a meeting after it ends and view app content.</span></span> <span data-ttu-id="442f5-223">В этом примере организатор собрания может посмотреть на результаты опроса на вкладке **Contoso.** (Примечание. С точки зрения проектирования нет разницы между вкладками до и после собрания.)</span><span class="sxs-lookup"><span data-stu-id="442f5-223">In this example, the meeting organizer can look at poll results in the **Contoso** tab. (Note: From a design standpoint, there's no difference between a the pre- and post-meeting tab experience.)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/post-meeting-experience.png" alt-text="В примере показана вкладка после собрания." border="false":::

## <a name="best-practices"></a><span data-ttu-id="442f5-225">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="442f5-225">Best practices</span></span>

### <a name="interactions"></a><span data-ttu-id="442f5-226">Взаимодействия</span><span class="sxs-lookup"><span data-stu-id="442f5-226">Interactions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-do.png" alt-text="Пример ограничения числа взаимодействий." border="false":::

#### <a name="do-limit-the-number-of-interactions"></a><span data-ttu-id="442f5-228">Do: ограничение количества взаимодействий</span><span class="sxs-lookup"><span data-stu-id="442f5-228">Do: Limit the number of interactions</span></span>

<span data-ttu-id="442f5-229">В диалоговом окну собрания удалите ненужный контент, который не поможет пользователям быстро выполнить задачи.</span><span class="sxs-lookup"><span data-stu-id="442f5-229">For in-meeting dialogs, remove unnecessary content that doesn't help users accomplish something quickly.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-dont.png" alt-text="Пример, показывающий, как не вводить ненужные элементы." border="false":::

#### <a name="dont-introduce-unnecessary-elements"></a><span data-ttu-id="442f5-231">Не: вводить ненужные элементы</span><span class="sxs-lookup"><span data-stu-id="442f5-231">Don't: Introduce unnecessary elements</span></span>

<span data-ttu-id="442f5-232">Отдельное диалоговое окно собрания с несколькими взаимодействиями может отвлекать от звонка.</span><span class="sxs-lookup"><span data-stu-id="442f5-232">A single in-meeting dialog with multiple interactions can distract from the call.</span></span>

   :::column-end:::
:::row-end:::

### <a name="layout"></a><span data-ttu-id="442f5-233">Макет</span><span class="sxs-lookup"><span data-stu-id="442f5-233">Layout</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-do.png" alt-text="Пример использования макета диалога с одним столбцом." border="false":::

#### <a name="do-use-a-single-column-dialog-layout"></a><span data-ttu-id="442f5-235">Do: Использование макета диалога с одним столбцом</span><span class="sxs-lookup"><span data-stu-id="442f5-235">Do: Use a single-column dialog layout</span></span>

<span data-ttu-id="442f5-236">Так как диалоги находятся в центре стадии собрания, выполнение задачи должно быть быстрым и простым во избежание проблем пользователей.</span><span class="sxs-lookup"><span data-stu-id="442f5-236">Since the dialogs are at the center of the meeting stage, task completion should be fast and simple to avoid user frustration.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-dont.png" alt-text="Пример, показывающий, что не следует засорять пространство расширения собрания." border="false":::

#### <a name="dont-clutter-the-space"></a><span data-ttu-id="442f5-238">Don't: Clutter the space</span><span class="sxs-lookup"><span data-stu-id="442f5-238">Don't: Clutter the space</span></span>

<span data-ttu-id="442f5-239">Сильное или слишком структурированное содержимое может отвлекать и отвлекать, особенно во время собрания.</span><span class="sxs-lookup"><span data-stu-id="442f5-239">Dense or overly structured content can be distracting and overwhelming, especially during a meeting.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-do.png" alt-text="Пример макета вкладки с одним столбцом." border="false":::

#### <a name="do-use-a-single-column-tab-layout"></a><span data-ttu-id="442f5-241">Do: Использование макета вкладки с одним столбцом</span><span class="sxs-lookup"><span data-stu-id="442f5-241">Do: Use a single-column tab layout</span></span>

<span data-ttu-id="442f5-242">С учетом узкой природы вкладки на собрании настоятельно рекомендуется отображать содержимое в одном столбце.</span><span class="sxs-lookup"><span data-stu-id="442f5-242">Given the in-meeting tab's narrow nature, we strongly recommend displaying the contents in a single column.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-dont.png" alt-text="Пример, на котором показана вкладка с несколькими столбцами." border="false":::

#### <a name="dont-use-multiple-columns"></a><span data-ttu-id="442f5-244">Не используйте: используйте несколько столбцов</span><span class="sxs-lookup"><span data-stu-id="442f5-244">Don't: Use multiple columns</span></span>

<span data-ttu-id="442f5-245">Из-за ограниченного пространства на вкладке собрания не рекомендуется использовать макеты с более чем одним столбцом.</span><span class="sxs-lookup"><span data-stu-id="442f5-245">Due to the limited space of the in-meeting tab, layouts with more than one column aren’t recommended.</span></span>

   :::column-end:::
:::row-end:::

### <a name="controls"></a><span data-ttu-id="442f5-246">Элементы управления</span><span class="sxs-lookup"><span data-stu-id="442f5-246">Controls</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-do.png" alt-text="Пример выравнивания основных элементов управления по правому правому направлению." border="false":::

#### <a name="do-right-align-the-primary-action"></a><span data-ttu-id="442f5-248">Do: выравнивание по правому правому направлению основного действия</span><span class="sxs-lookup"><span data-stu-id="442f5-248">Do: Right align the primary action</span></span>

<span data-ttu-id="442f5-249">Мы рекомендуем расположить наиболее сильное визуальное действие в нужное место.</span><span class="sxs-lookup"><span data-stu-id="442f5-249">We recommend positioning the most visually heavy action to the right-most location.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-dont.png" alt-text="Пример, показывающий, как не следует выравнивать основные элементы управления левой стороной." border="false":::

#### <a name="dont-left-or-center-align-actions"></a><span data-ttu-id="442f5-251">Don't: Left or center align actions</span><span class="sxs-lookup"><span data-stu-id="442f5-251">Don't: Left or center align actions</span></span>

<span data-ttu-id="442f5-252">Это отклоняется от стандартного шаблона Teams для размещения управления в диалоговом оке и может конфликтовть с диалогом за верхним.</span><span class="sxs-lookup"><span data-stu-id="442f5-252">This deviates from the standard Teams pattern for control placement in a dialog and may conflict with a dialog behind the top one.</span></span>

   :::column-end:::
:::row-end:::

### <a name="scroll"></a><span data-ttu-id="442f5-253">Прокрутка</span><span class="sxs-lookup"><span data-stu-id="442f5-253">Scroll</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-do.png" alt-text="Пример вертикальной прокрутки на вкладке собрания." border="false":::

#### <a name="do-scroll-vertically"></a><span data-ttu-id="442f5-255">Do: Прокрутка по вертикали</span><span class="sxs-lookup"><span data-stu-id="442f5-255">Do: Scroll vertically</span></span>

<span data-ttu-id="442f5-256">Пользователи ожидают вертикальной прокрутки в Teams (и в другом месте).</span><span class="sxs-lookup"><span data-stu-id="442f5-256">Users expect vertical scrolling in Teams (and elsewhere).</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-dont.png" alt-text="Пример горизонтальной прокрутки на вкладке собрания." border="false":::

#### <a name="dont-scroll-horizontally"></a><span data-ttu-id="442f5-258">Не: прокрутка по горизонтали</span><span class="sxs-lookup"><span data-stu-id="442f5-258">Don't: Scroll horizontally</span></span>

<span data-ttu-id="442f5-259">Горизонтальная прокрутка не является ожидаемым поведением в Teams.</span><span class="sxs-lookup"><span data-stu-id="442f5-259">Horizontal scrolling isn’t an expected behavior in Teams.</span></span> <span data-ttu-id="442f5-260">Другие холсты в среде собраний прокручивается вертикально.</span><span class="sxs-lookup"><span data-stu-id="442f5-260">Other canvases in the meeting environment scroll vertically.</span></span>

   :::column-end:::
:::row-end:::

### <a name="workflows"></a><span data-ttu-id="442f5-261">Рабочие процессы</span><span class="sxs-lookup"><span data-stu-id="442f5-261">Workflows</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-workflow-do.png" alt-text="Пример сложного сценария на вкладке &quot;Собрание&quot;." border="false":::

#### <a name="do-surface-complex-scenarios-in-the-in-meeting-tab"></a><span data-ttu-id="442f5-263">Do: сложные сценарии Surface на вкладке "Собрание"</span><span class="sxs-lookup"><span data-stu-id="442f5-263">Do: Surface complex scenarios in the in-meeting tab</span></span>

<span data-ttu-id="442f5-264">Если ваше приложение включает несколько задач, мы настоятельно рекомендуем использовать вкладку собрания с макетом из одного столбца.</span><span class="sxs-lookup"><span data-stu-id="442f5-264">If your app includes multiple tasks, we strongly recommend using an in-meeting tab with a single-column layout.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-workflow-dont.png" alt-text="Пример, показывающий сложные сценарии в диалоговом оке собрания." border="false":::

#### <a name="dont-make-in-meeting-dialogs-complex"></a><span data-ttu-id="442f5-266">Не: сделать диалоговые окно собрания сложными</span><span class="sxs-lookup"><span data-stu-id="442f5-266">Don't: Make in-meeting dialogs complex</span></span>

<span data-ttu-id="442f5-267">Диалоги на собрании предназначены для краткого взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="442f5-267">In-meeting dialogs are intended for brief interactions.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="442f5-268">Темы</span><span class="sxs-lookup"><span data-stu-id="442f5-268">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-do.png" alt-text="Пример расширения собрания с темной темой." border="false":::

#### <a name="do-use-teams-color-tokens"></a><span data-ttu-id="442f5-270">Do: Use Teams color tokens</span><span class="sxs-lookup"><span data-stu-id="442f5-270">Do: Use Teams color tokens</span></span>

<span data-ttu-id="442f5-271">Собрания Teams оптимизированы для темного режима, чтобы уменьшить визуальный и познавательный шум, чтобы пользователи могли сосредоточиться на обсуждении и общем содержимом.</span><span class="sxs-lookup"><span data-stu-id="442f5-271">Teams meetings are optimized for dark mode to help reduce visual and cognitive noise so users can focus on the discussion and shared content.</span></span> <span data-ttu-id="442f5-272">Узнайте об использовании <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">маркеров цвета (пользовательский интерфейс Fluent).</a></span><span class="sxs-lookup"><span data-stu-id="442f5-272">Learn about using <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a>.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-dont.png" alt-text="Пример расширения собрания с светлой темой по умолчанию." border="false":::

#### <a name="dont-hard-code-hex-values"></a><span data-ttu-id="442f5-274">Don't: Hard code hex values</span><span class="sxs-lookup"><span data-stu-id="442f5-274">Don't: Hard code hex values</span></span>

<span data-ttu-id="442f5-275">Если вы не используете маркеры цвета Teams, ваши макеты будут менее масштабируемыми и займет больше времени на управление.</span><span class="sxs-lookup"><span data-stu-id="442f5-275">If you don’t use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::

### <a name="navigation"></a><span data-ttu-id="442f5-276">Навигация</span><span class="sxs-lookup"><span data-stu-id="442f5-276">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-do.png" alt-text="Пример расширения собрания с кнопкой &quot;Назад&quot;." border="false":::

#### <a name="do-have-a-back-button"></a><span data-ttu-id="442f5-278">Do: Have a Back button</span><span class="sxs-lookup"><span data-stu-id="442f5-278">Do: Have a back button</span></span>

<span data-ttu-id="442f5-279">Если на вкладке собрания имеется несколько уровней навигации, пользователи должны иметь возможность вернуться к своим предыдущим представлениям.</span><span class="sxs-lookup"><span data-stu-id="442f5-279">If you have more than one layer of navigation in an in-meeting tab, users must be able to go back to their previous views.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-dont.png" alt-text="Пример расширения собрания с двумя кнопками с отклоняться." border="false":::

#### <a name="dont-include-another-dismiss-button"></a><span data-ttu-id="442f5-281">Не: включить еще одну кнопку "Отклонять"</span><span class="sxs-lookup"><span data-stu-id="442f5-281">Don't: Include another dismiss button</span></span>

<span data-ttu-id="442f5-282">Предоставление возможности закрыть содержимое вкладки собрания может вызвать проблемы, так как в заголке уже есть кнопка для закрытия самой вкладки собрания.</span><span class="sxs-lookup"><span data-stu-id="442f5-282">Providing an option to close in-meeting tab content may cause issues since there’s already a button in the header to dismiss the in-meeting tab itself.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-caution.png" alt-text="Пример, показывающий модальные модули (или модули задач) на вкладке собрания." border="false":::

#### <a name="caution-avoid-modals-within-the-in-meeting-tab"></a><span data-ttu-id="442f5-284">Внимание! Избегайте модальных модалов на вкладке "Собрание"</span><span class="sxs-lookup"><span data-stu-id="442f5-284">Caution: Avoid modals within the in-meeting tab</span></span>

<span data-ttu-id="442f5-285">Модальные модули (также известные как модули задач) на уже узкой вкладке собрания могут обтекать содержимое и скрывать его.</span><span class="sxs-lookup"><span data-stu-id="442f5-285">Modals (also known as task modules) in the already narrow in-meeting tab might wrap and obscure the content.</span></span>

   :::column-end:::
:::row-end:::

## <a name="validate-your-design"></a><span data-ttu-id="442f5-286">Проверка проекта</span><span class="sxs-lookup"><span data-stu-id="442f5-286">Validate your design</span></span>

<span data-ttu-id="442f5-287">Если вы планируете опубликовать приложение в AppSource, следует понимать проблемы проектирования, которые часто приводят к сбойу приложений во время отправки.</span><span class="sxs-lookup"><span data-stu-id="442f5-287">If you plan to publish your app to AppSource, you should understand the design issues that commonly cause apps to fail during submission.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="442f5-288">Проверка рекомендаций по проверке проекта</span><span class="sxs-lookup"><span data-stu-id="442f5-288">Check design validation guidelines</span></span>](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
