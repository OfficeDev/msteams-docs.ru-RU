---
title: Создание вкладки Microsoft Teams на собрании
author: heath-hamilton
description: Рекомендации и рекомендации по разработке вкладки "в собрании" для Microsoft Teams.
ms.author: lajanuar
ms.topic: conceptual
ms.openlocfilehash: 4f75591468de41b5d4d3ac62a25b93412b3fccaa
ms.sourcegitcommit: f9a2f5cedc9d30ef7a9cf78a47d01cfd277e150d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/23/2020
ms.locfileid: "48243341"
---
# <a name="design-an-in-meeting-tab"></a><span data-ttu-id="808e9-103">Создание вкладки собрания</span><span class="sxs-lookup"><span data-stu-id="808e9-103">Design an in-meeting tab</span></span>

<span data-ttu-id="808e9-104">Вкладка "в собрании" это холст для расширения совместной работы во время собраний.</span><span class="sxs-lookup"><span data-stu-id="808e9-104">The in-meeting tab is a canvas for augmenting collaboration during meetings.</span></span> <span data-ttu-id="808e9-105">В зависимости от возможности вкладки Teams участники могут просматривать содержимое приложения и взаимодействовать с ним в выделенном пространстве за пределами этапа собрания с помощью общих представлений или представлений на основе ролей.</span><span class="sxs-lookup"><span data-stu-id="808e9-105">Based on the Teams tab capability, attendees can see and interact with app content in a dedicated space outside the meeting stage through shared or role-based views.</span></span>

## <a name="use-cases"></a><span data-ttu-id="808e9-106">Варианты использования</span><span class="sxs-lookup"><span data-stu-id="808e9-106">Use cases</span></span>

<span data-ttu-id="808e9-107">С помощью вкладки в собрании пользователи могут выполнять следующие действия:</span><span class="sxs-lookup"><span data-stu-id="808e9-107">People might use the in-meeting tab to:</span></span>

* <span data-ttu-id="808e9-108">Предоставление подробной обратной связи (например, Оценка кандидата на задание)</span><span class="sxs-lookup"><span data-stu-id="808e9-108">Provide detailed feedback (for example, evaluate a job candidate)</span></span>
* <span data-ttu-id="808e9-109">Быстрое создание опроса, опроса или элемента задачи для участников собрания</span><span class="sxs-lookup"><span data-stu-id="808e9-109">Quickly create a poll, survey, or task item for the meeting participants</span></span>
* <span data-ttu-id="808e9-110">Отображение заметок, относящихся к собранию (например, сведений о менеджере по продажам)</span><span class="sxs-lookup"><span data-stu-id="808e9-110">Display notes relevant to the meeting (for example, information about a sales lead)</span></span>

## <a name="example"></a><span data-ttu-id="808e9-111">Пример</span><span class="sxs-lookup"><span data-stu-id="808e9-111">Example</span></span>

<span data-ttu-id="808e9-112">В следующем примере показана вкладка на собрании, в которой отображается контент приложения опроса.</span><span class="sxs-lookup"><span data-stu-id="808e9-112">The following example shows the in-meeting tab displaying survey app content.</span></span>

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-organizer-view.png" alt-text="Пример: вкладка Собрание в собрании может выглядеть с точки зрения организатора собрания.":::

<span data-ttu-id="808e9-114"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Просмотр полного сценария (фигма)</a></span><span class="sxs-lookup"><span data-stu-id="808e9-114"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">See the full scenario (Figma)</a></span></span>

<span data-ttu-id="808e9-115"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Другие примеры вариантов использования (фигма)</a></span><span class="sxs-lookup"><span data-stu-id="808e9-115"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">See other example use cases (Figma)</a></span></span>

## <a name="anatomy"></a><span data-ttu-id="808e9-116">Составляющие</span><span class="sxs-lookup"><span data-stu-id="808e9-116">Anatomy</span></span>

<span data-ttu-id="808e9-117">На вкладке в собрании отображается контент приложения с использованием следующих измерений:</span><span class="sxs-lookup"><span data-stu-id="808e9-117">The in-meeting tab displays your app content using the following dimensions:</span></span>

* <span data-ttu-id="808e9-118">**Ширина**: 280 пикселей для области вебвиев.</span><span class="sxs-lookup"><span data-stu-id="808e9-118">**Width**: 280 pixels for the webview area.</span></span> <span data-ttu-id="808e9-119">В левой и правой сторонах вебвиев есть 20 точек заполнения.</span><span class="sxs-lookup"><span data-stu-id="808e9-119">There are 20 pixels of padding on the left and right sides of the webview.</span></span>
* <span data-ttu-id="808e9-120">**Высота**: полный выпуск в нижней части вкладки. Существует 20 точек заполнения между областью вебвиев и заголовком табуляции.</span><span class="sxs-lookup"><span data-stu-id="808e9-120">**Height**: Full bleed to the bottom of the tab. There are 20 pixels of padding between the webview area and tab header.</span></span>

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-anatomy.png" alt-text="Иллюстрация, демонстрирующая пользовательский интерфейс Анатомия расширения собрания на вкладке "собрание"." border="false":::

1. <span data-ttu-id="808e9-122">**Значок приложения**: точка входа на вкладку "в собрании".</span><span class="sxs-lookup"><span data-stu-id="808e9-122">**App icon**: The entry point to the in-meeting tab.</span></span>
1. <span data-ttu-id="808e9-123">**Верхний колонтитул**: включает имя вкладки.</span><span class="sxs-lookup"><span data-stu-id="808e9-123">**Header**: Includes the tab name.</span></span>
1. <span data-ttu-id="808e9-124">**Name**: имя экземпляра вкладки.</span><span class="sxs-lookup"><span data-stu-id="808e9-124">**Name**: The name of the tab instance.</span></span>
1. <span data-ttu-id="808e9-125">**Закрыть**: закрывает вкладку. Всегда используйте значок закрытия сверху справа, а не действие в нижнем колонтитуле.</span><span class="sxs-lookup"><span data-stu-id="808e9-125">**Dismiss**: Dismisses the tab. Always use the upper-right close icon instead of an action in the footer.</span></span>
1. <span data-ttu-id="808e9-126">**Вебвиев**: отображает весь контент стороннего приложения.</span><span class="sxs-lookup"><span data-stu-id="808e9-126">**Webview**: Displays all third-party app content.</span></span>

## <a name="behavior"></a><span data-ttu-id="808e9-127">Поведение</span><span class="sxs-lookup"><span data-stu-id="808e9-127">Behavior</span></span>

### <a name="scale"></a><span data-ttu-id="808e9-128">Масштаб</span><span class="sxs-lookup"><span data-stu-id="808e9-128">Scale</span></span>

<span data-ttu-id="808e9-129">В настоящее время ширина вкладки "в собрании" исправлена.</span><span class="sxs-lookup"><span data-stu-id="808e9-129">Currently, the width of the in-meeting tab is fixed.</span></span>

### <a name="scrolling"></a><span data-ttu-id="808e9-130">Прокрутки</span><span class="sxs-lookup"><span data-stu-id="808e9-130">Scrolling</span></span>

<span data-ttu-id="808e9-131">Вот что нужно знать о прокрутке на вкладке на собрании:</span><span class="sxs-lookup"><span data-stu-id="808e9-131">Here's what to know about scrolling in the in-meeting tab:</span></span>

* <span data-ttu-id="808e9-132">Эту возможность можно прокручивать только по вертикали.</span><span class="sxs-lookup"><span data-stu-id="808e9-132">You should only be able to scroll vertically.</span></span>
* <span data-ttu-id="808e9-133">Отображается только содержимое, к которому вы выполнили прокрутку (ничего или не ниже).</span><span class="sxs-lookup"><span data-stu-id="808e9-133">You can only see the content you've scrolled to (nothing above or below).</span></span>
* <span data-ttu-id="808e9-134">Полоса прокрутки является частью содержимого вебвиев.</span><span class="sxs-lookup"><span data-stu-id="808e9-134">The scrollbar is part of the webview content.</span></span>

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-scroll.png" alt-text="Иллюстрация, на которой показано, как работает прокрутка содержимого вебвиев на вкладке "в собрании"." border="false":::

### <a name="navigation"></a><span data-ttu-id="808e9-136">Навигация</span><span class="sxs-lookup"><span data-stu-id="808e9-136">Navigation</span></span>

<span data-ttu-id="808e9-137">Для сценариев с слоями навигации или большим содержимым рекомендуется разрешить пользователям переходить на дополнительный слой.</span><span class="sxs-lookup"><span data-stu-id="808e9-137">For scenarios with navigation layers or heavy content, we recommend allowing users to navigate to a secondary layer.</span></span> <span data-ttu-id="808e9-138">Пользователи должны иметь возможность вернуться к предыдущему слою.</span><span class="sxs-lookup"><span data-stu-id="808e9-138">Users must be able to go back to the previous layer.</span></span>

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-nav.png" alt-text="Иллюстрация, на которой показано, как работает переход на дополнительный слой на вкладке "в собрании"." border="false":::

## <a name="components"></a><span data-ttu-id="808e9-140">Компоненты</span><span class="sxs-lookup"><span data-stu-id="808e9-140">Components</span></span>

<span data-ttu-id="808e9-141">Вкладки на собрании в первую очередь строятся с помощью следующих <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">компонентов пользовательского интерфейса (фигма)</a>, основанных на <a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">системе дизайна Fluent</a>.</span><span class="sxs-lookup"><span data-stu-id="808e9-141">In-meeting tabs are built primarily with the following <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">UI components (Figma)</a>, which are based on the <a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">Fluent Design System</a>.</span></span>

<span data-ttu-id="808e9-142">Компонент</span><span class="sxs-lookup"><span data-stu-id="808e9-142">Component</span></span> | <span data-ttu-id="808e9-143">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="808e9-143">Guidelines</span></span> | <span data-ttu-id="808e9-144">Пример</span><span class="sxs-lookup"><span data-stu-id="808e9-144">Example</span></span>
 - | - | -
<span data-ttu-id="808e9-145">Кнопка</span><span class="sxs-lookup"><span data-stu-id="808e9-145">Button</span></span> | <span data-ttu-id="808e9-146">Основные и дополнительные кнопки могут быть средними или малыми</span><span class="sxs-lookup"><span data-stu-id="808e9-146">Primary and secondary buttons can be medium or small</span></span> | <span data-ttu-id="808e9-147">Отправка ответа</span><span class="sxs-lookup"><span data-stu-id="808e9-147">Send a response</span></span>
<span data-ttu-id="808e9-148">Input</span><span class="sxs-lookup"><span data-stu-id="808e9-148">Input</span></span> | <span data-ttu-id="808e9-149">Поле для краткого ввода данных пользователем.</span><span class="sxs-lookup"><span data-stu-id="808e9-149">Field for brief user input.</span></span> <span data-ttu-id="808e9-150">Текст метки может включать значок</span><span class="sxs-lookup"><span data-stu-id="808e9-150">Label text can include an icon</span></span>  | <span data-ttu-id="808e9-151">Введите отзыв</span><span class="sxs-lookup"><span data-stu-id="808e9-151">Enter feedback</span></span>
<span data-ttu-id="808e9-152">Раскрывающийся список</span><span class="sxs-lookup"><span data-stu-id="808e9-152">Dropdown</span></span> | <span data-ttu-id="808e9-153">Выберите один или несколько параметров из списка.</span><span class="sxs-lookup"><span data-stu-id="808e9-153">Select one or more options from a list.</span></span> <span data-ttu-id="808e9-154">Может включать функции поиска и выбора нескольких элементов</span><span class="sxs-lookup"><span data-stu-id="808e9-154">Can include search and multi-selection features</span></span> | <span data-ttu-id="808e9-155">Выбор языка</span><span class="sxs-lookup"><span data-stu-id="808e9-155">Choose a language</span></span>
<span data-ttu-id="808e9-156">Элементы управления выбором</span><span class="sxs-lookup"><span data-stu-id="808e9-156">Selection controls</span></span> | <span data-ttu-id="808e9-157">Используйте флажки для нескольких вариантов или переключателей и переключитесь на один вариант.</span><span class="sxs-lookup"><span data-stu-id="808e9-157">Use checkboxes for multiple choices or radio buttons and toggles for single choices.</span></span> <span data-ttu-id="808e9-158">Для более подробного выбора используйте ползунок</span><span class="sxs-lookup"><span data-stu-id="808e9-158">For more detailed selections, use a slider</span></span> | <span data-ttu-id="808e9-159">Голосование за опрос</span><span class="sxs-lookup"><span data-stu-id="808e9-159">Vote in a poll</span></span>
<span data-ttu-id="808e9-160">Оповещения</span><span class="sxs-lookup"><span data-stu-id="808e9-160">Alerts</span></span> | <span data-ttu-id="808e9-161">При отображении срочных сообщений, состояния ошибок или предупреждений сообщение должно быть кратким и не прерывать текущую задачу пользователя</span><span class="sxs-lookup"><span data-stu-id="808e9-161">Whether displaying an urgent message, error state, or warning, the message should be short and won't interrupt the user's current task</span></span> | <span data-ttu-id="808e9-162">Ошибка отображения при отправке ответа</span><span class="sxs-lookup"><span data-stu-id="808e9-162">Display issue when submitting a response</span></span>

## <a name="theming"></a><span data-ttu-id="808e9-163">Темы</span><span class="sxs-lookup"><span data-stu-id="808e9-163">Theming</span></span>

### <a name="colors"></a><span data-ttu-id="808e9-164">Цвета</span><span class="sxs-lookup"><span data-stu-id="808e9-164">Colors</span></span>

<span data-ttu-id="808e9-165">Используйте <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">рекомендуемую цветовую схему (фигма)</a> для фоновых изображений, переднего плана и состояний.</span><span class="sxs-lookup"><span data-stu-id="808e9-165">Use the <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">recommended color scheme (Figma)</a> for backgrounds, foregrounds, and conveying states.</span></span>

### <a name="typography"></a><span data-ttu-id="808e9-166">Шрифтовое оформление</span><span class="sxs-lookup"><span data-stu-id="808e9-166">Typography</span></span>

<span data-ttu-id="808e9-167">Используйте <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Рекомендуемые размеры и веса шрифтов (фигма)</a> для заголовков, основного текста и текста метаданных.</span><span class="sxs-lookup"><span data-stu-id="808e9-167">Use the <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">recommended font sizes and weights (Figma)</a> for titles, body text, and metadata text.</span></span>

## <a name="best-practices"></a><span data-ttu-id="808e9-168">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="808e9-168">Best practices</span></span>

### <a name="responsiveness"></a><span data-ttu-id="808e9-169">Отклика</span><span class="sxs-lookup"><span data-stu-id="808e9-169">Responsiveness</span></span>

<span data-ttu-id="808e9-170">Макеты вкладок на собрании должны иметь возможность масштабироваться до различных размеров.</span><span class="sxs-lookup"><span data-stu-id="808e9-170">In-meeting tab layouts should be able to scale to various sizes.</span></span> <span data-ttu-id="808e9-171">Рассмотрите способ масштабирования вкладки и получения фигуры до, во время и после собрания.</span><span class="sxs-lookup"><span data-stu-id="808e9-171">Consider how the tab will scale and take shape before, during, and after the meeting.</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-before-meeting.png" alt-text="Иллюстрация, на которой показано, что содержимое вкладки "в собрании" выглядит как вкладка полноэкранного экрана перед собранием и после него." border="false":::

#### <a name="before-the-meeting"></a><span data-ttu-id="808e9-173">Перед собранием</span><span class="sxs-lookup"><span data-stu-id="808e9-173">Before the meeting</span></span>

<span data-ttu-id="808e9-174">Убедитесь, что макет вкладок можно адаптировать к разметке справа или слева для разных языков, а элементы управления перемещаются в правильное расположение.</span><span class="sxs-lookup"><span data-stu-id="808e9-174">Make sure your tab layout can adapt to a right or left layout for different languages and that controls move to the correct locations.</span></span> <span data-ttu-id="808e9-175">(Макеты перед собраниями также могут применяться к макетам после собраний.)</span><span class="sxs-lookup"><span data-stu-id="808e9-175">(Pre-meeting layouts can also apply to post-meeting layouts.)</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-during-meeting.png" alt-text="Иллюстрация, на которой показано, как содержимое вкладки перед собранием сжимается на вкладке "на собрание" во время собрания." border="false":::

#### <a name="during-the-meeting"></a><span data-ttu-id="808e9-177">Во время собрания</span><span class="sxs-lookup"><span data-stu-id="808e9-177">During the meeting</span></span>

<span data-ttu-id="808e9-178">Содержимое вкладки регулируется макетом и расположением вкладок на собрании.</span><span class="sxs-lookup"><span data-stu-id="808e9-178">Tab content adjusts to the in-meeting tab layout and location.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="808e9-179">Темы</span><span class="sxs-lookup"><span data-stu-id="808e9-179">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-theming-do.png" alt-text="Иллюстрация, на которой показано, как создать вкладку в собрании для темной темы, используемой в собраниях Teams." border="false":::

#### <a name="do-design-for-a-dark-theme"></a><span data-ttu-id="808e9-181">Do: дизайн для темной темы</span><span class="sxs-lookup"><span data-stu-id="808e9-181">Do: Design for a dark theme</span></span>

<span data-ttu-id="808e9-182">Собрания Teams оптимизированы для темного режима, что позволяет снизить визуальное и пользовательское шум, чтобы пользователи могли сосредоточиться на обсуждении и общем содержимом.</span><span class="sxs-lookup"><span data-stu-id="808e9-182">Teams meetings are optimized for dark mode to help reduce visual and cognitive noise so users can focus on the discussion and shared content.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-theming-dont.png" alt-text="Иллюстрация, на которой показано, что не следует использовать цвета, не кондуЦиве в темную тему Teams." border="false":::

#### <a name="dont-use-unfamiliar-colors"></a><span data-ttu-id="808e9-184">Не используйте незнакомые цвета.</span><span class="sxs-lookup"><span data-stu-id="808e9-184">Don't: Use unfamiliar colors</span></span>

<span data-ttu-id="808e9-185">Цвета, которые могут пересекаться со средой для собраний, могут отвлекаться от несущего объема в Teams.</span><span class="sxs-lookup"><span data-stu-id="808e9-185">Colors that clash with the meeting environment may be distracting and appear less native to Teams.</span></span>

   :::column-end:::
:::row-end:::

### <a name="scrolling"></a><span data-ttu-id="808e9-186">Прокрутки</span><span class="sxs-lookup"><span data-stu-id="808e9-186">Scrolling</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-scroll-do.png" alt-text="Иллюстрация, на которой показано, следует использовать только вертикальные полосы прокрутки на вкладке на собрании." border="false":::

#### <a name="do-scroll-vertically"></a><span data-ttu-id="808e9-188">Do: вертикальная прокрутка</span><span class="sxs-lookup"><span data-stu-id="808e9-188">Do: Scroll vertically</span></span>

<span data-ttu-id="808e9-189">Пользователи предполагают вертикальную прокрутку в Teams (и в других местах).</span><span class="sxs-lookup"><span data-stu-id="808e9-189">Users anticipate vertical scrolling in Teams (and elsewhere).</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-scroll-dont.png" alt-text="Иллюстрация, на которой показано, не следует разрешать горизонтальную прокрутку на вкладке на собрании." border="false":::

#### <a name="dont-scroll-horizontally"></a><span data-ttu-id="808e9-191">Не: прокручивать по горизонтали</span><span class="sxs-lookup"><span data-stu-id="808e9-191">Don't: Scroll horizontally</span></span>

<span data-ttu-id="808e9-192">Горизонтальная полоса прокрутки не является ожидаемым поведением в Teams.</span><span class="sxs-lookup"><span data-stu-id="808e9-192">Horizontal scrolling isn’t an expected behavior in Teams.</span></span> <span data-ttu-id="808e9-193">Другие холсты в среде проведения собраний прокручиваются вертикально.</span><span class="sxs-lookup"><span data-stu-id="808e9-193">Other canvases in the meeting environment scroll vertically.</span></span>

   :::column-end:::
:::row-end:::

### <a name="layout"></a><span data-ttu-id="808e9-194">Макет</span><span class="sxs-lookup"><span data-stu-id="808e9-194">Layout</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-layout-do.png" alt-text="Иллюстрация, на которой показан рекомендуемый макет с одним столбцом на вкладке "в собрании"." border="false":::

#### <a name="do-single-columns"></a><span data-ttu-id="808e9-196">Do: Single Columns</span><span class="sxs-lookup"><span data-stu-id="808e9-196">Do: Single columns</span></span>

<span data-ttu-id="808e9-197">При наличии узкой природы вкладки в собрании настоятельно рекомендуется отобразить содержимое в отдельном столбце.</span><span class="sxs-lookup"><span data-stu-id="808e9-197">Given the in-meeting tab’s narrow nature, we strongly recommend displaying the contents in a single column.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-layout-dont.png" alt-text="Иллюстрация, на которой показано, что макет с двумя столбцами на вкладке на собрании не подходит." border="false":::

#### <a name="dont-multiple-columns"></a><span data-ttu-id="808e9-199">Не: несколько столбцов</span><span class="sxs-lookup"><span data-stu-id="808e9-199">Don't: Multiple columns</span></span>

<span data-ttu-id="808e9-200">Из-за ограниченного пространства вкладки в собрании не рекомендуется использовать макеты с несколькими столбцами.</span><span class="sxs-lookup"><span data-stu-id="808e9-200">Due to the limited space of the in-meeting tab, layouts with more than one column aren’t recommended.</span></span>

   :::column-end:::
:::row-end:::

### <a name="navigation"></a><span data-ttu-id="808e9-201">Навигация</span><span class="sxs-lookup"><span data-stu-id="808e9-201">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-nav-do.png" alt-text="Иллюстрация, на которой показано, следует всегда предоставлять кнопку "назад", если в приложении вкладки на собрании есть несколько уровней навигации." border="false":::

#### <a name="do-have-a-back-button"></a><span data-ttu-id="808e9-203">Do: кнопка "назад"</span><span class="sxs-lookup"><span data-stu-id="808e9-203">Do: Have a back button</span></span>

<span data-ttu-id="808e9-204">Если имеется несколько уровней навигации, пользователи должны иметь возможность вернуться к предыдущему представлению.</span><span class="sxs-lookup"><span data-stu-id="808e9-204">If you have more than one layer of navigation, users must be able to go back to their previous view.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-nav-dont.png" alt-text="Иллюстрация, на которой показано, как добавление новой кнопки "Закрыть" на вкладке "на собрание" для навигации является избыточной и может привести к возникновению проблем." border="false":::

#### <a name="dont-include-another-close-button"></a><span data-ttu-id="808e9-206">Не: включить еще одну кнопку "Закрыть"</span><span class="sxs-lookup"><span data-stu-id="808e9-206">Don't: Include another close button</span></span>

<span data-ttu-id="808e9-207">Предоставление возможности закрыть содержимое вкладки собраний может привести к проблемам, так как в заголовке уже есть кнопка Закрыть для закрытия вкладки в собрании.</span><span class="sxs-lookup"><span data-stu-id="808e9-207">Providing an option to close in-meeting tab content may cause issues since there’s already a close button in the header to dismiss the in-meeting tab itself.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-nav-caution.png" alt-text="Иллюстрация, на которой показано, что при использовании модальных модальек (например, модулей задач) на вкладке на собрании задано ограниченное пространство." border="false":::

#### <a name="caution-using-dialogs-in-a-narrow-space"></a><span data-ttu-id="808e9-209">Внимание! использование диалоговых окон в узком пространстве</span><span class="sxs-lookup"><span data-stu-id="808e9-209">Caution: Using dialogs in a narrow space</span></span>

<span data-ttu-id="808e9-210">Диалоговые окна, такие как модули задач, на вкладке уже более узкое собрание могут переносить и скрывать содержимое.</span><span class="sxs-lookup"><span data-stu-id="808e9-210">Dialogs, such as task modules, in the already narrow in-meeting tab might wrap and obscure the content.</span></span>

   :::column-end:::
:::row-end:::

## <a name="accessibility"></a><span data-ttu-id="808e9-211">Специальные возможности</span><span class="sxs-lookup"><span data-stu-id="808e9-211">Accessibility</span></span>

<span data-ttu-id="808e9-212">Сведения о специальных возможностях содержатся в разделе <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">фигма</a>.</span><span class="sxs-lookup"><span data-stu-id="808e9-212">For information on accessibility, see <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Figma</a>.</span></span>

## <a name="resources"></a><span data-ttu-id="808e9-213">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="808e9-213">Resources</span></span>

* <span data-ttu-id="808e9-214"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Файл фигма для расширений собраний Microsoft Teams</a></span><span class="sxs-lookup"><span data-stu-id="808e9-214"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Microsoft Teams meeting extensions Figma file</a></span></span>
* [<span data-ttu-id="808e9-215">Рекомендации по проектированию вкладок</span><span class="sxs-lookup"><span data-stu-id="808e9-215">Tabs design guidelines</span></span>](../../tabs/design/tabs.md)
* [<span data-ttu-id="808e9-216">Рекомендации по проектированию вкладок для мобильных устройств</span><span class="sxs-lookup"><span data-stu-id="808e9-216">Tabs design guidelines for mobile</span></span>](../../tabs/design/tabs-mobile.md)

## <a name="validate-your-design"></a><span data-ttu-id="808e9-217">Проверка проекта</span><span class="sxs-lookup"><span data-stu-id="808e9-217">Validate your design</span></span>

<span data-ttu-id="808e9-218">Если вы планируете опубликовать свое приложение в AppSource, следует изучить проблемы, которые обычно приводят к сбою приложений во время отправки.</span><span class="sxs-lookup"><span data-stu-id="808e9-218">If you plan to publish your app to AppSource, you should understand the design issues that commonly cause apps to fail during submission.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="808e9-219">Проверка рекомендаций по проверке макета</span><span class="sxs-lookup"><span data-stu-id="808e9-219">Check design validation guidelines</span></span>](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines)
