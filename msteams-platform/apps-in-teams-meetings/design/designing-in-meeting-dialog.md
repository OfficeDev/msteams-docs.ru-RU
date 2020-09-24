---
title: Создание диалогового окна собраний Microsoft Teams
author: heath-hamilton
description: Рекомендации и рекомендации по разработке диалогового окна для собраний в Microsoft Teams.
ms.author: lajanuar
ms.topic: conceptual
ms.openlocfilehash: 89e532e6dbd83e54269606f6e051fa377de68f62
ms.sourcegitcommit: f9a2f5cedc9d30ef7a9cf78a47d01cfd277e150d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/23/2020
ms.locfileid: "48243335"
---
# <a name="design-an-in-meeting-dialog"></a><span data-ttu-id="b5b1e-103">Создание диалогового окна собрания</span><span class="sxs-lookup"><span data-stu-id="b5b1e-103">Design an in-meeting dialog</span></span>

<span data-ttu-id="b5b1e-104">Диалоговые окна для собраний отображаются на этапе собрания Teams.</span><span class="sxs-lookup"><span data-stu-id="b5b1e-104">In-meeting dialogs display on the Teams meeting stage.</span></span> <span data-ttu-id="b5b1e-105">Для них требуется вмешательство пользователя, подтверждение или участие, но они не прерывают собрание.</span><span class="sxs-lookup"><span data-stu-id="b5b1e-105">They require a user's attention, confirmation, or interaction but are subtle and don't interrupt the meeting.</span></span>

## <a name="use-cases"></a><span data-ttu-id="b5b1e-106">Варианты использования</span><span class="sxs-lookup"><span data-stu-id="b5b1e-106">Use cases</span></span>

<span data-ttu-id="b5b1e-107">Диалоговые окна для собраний запускаются пользователем (например организатором собрания), которые могут заинтересовать следующих участников:</span><span class="sxs-lookup"><span data-stu-id="b5b1e-107">In-meeting dialogs are triggered by a user (such as the meeting organizer) who might want participants to:</span></span>

* <span data-ttu-id="b5b1e-108">Предоставление кратких отзывов</span><span class="sxs-lookup"><span data-stu-id="b5b1e-108">Provide brief feedback</span></span>
* <span data-ttu-id="b5b1e-109">Получение короткого опроса или опроса</span><span class="sxs-lookup"><span data-stu-id="b5b1e-109">Take a short survey or poll</span></span>
* <span data-ttu-id="b5b1e-110">Предоставление утверждений</span><span class="sxs-lookup"><span data-stu-id="b5b1e-110">Submit approvals</span></span>
* <span data-ttu-id="b5b1e-111">Получение напоминаний</span><span class="sxs-lookup"><span data-stu-id="b5b1e-111">Get reminders</span></span>

## <a name="example"></a><span data-ttu-id="b5b1e-112">Пример</span><span class="sxs-lookup"><span data-stu-id="b5b1e-112">Example</span></span>

<span data-ttu-id="b5b1e-113">В приведенном ниже примере показано, как может выглядеть диалоговое окно для собраний с точки зрения участника собрания.</span><span class="sxs-lookup"><span data-stu-id="b5b1e-113">The following example shows what the in-meeting dialog might look like from a meeting participant's perspective.</span></span> <span data-ttu-id="b5b1e-114">Как видите, контент и задача являются облегченными.</span><span class="sxs-lookup"><span data-stu-id="b5b1e-114">As you can see, the content and task are lightweight.</span></span>

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-participant-view.png" alt-text="Пример, в котором показано, как может выглядеть диалоговое окно для собраний с точки зрения участника собрания.":::

<span data-ttu-id="b5b1e-116"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Просмотр полного сценария (фигма)</a></span><span class="sxs-lookup"><span data-stu-id="b5b1e-116"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">See the full scenario (Figma)</a></span></span>

<span data-ttu-id="b5b1e-117"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Другие примеры вариантов использования (фигма)</a></span><span class="sxs-lookup"><span data-stu-id="b5b1e-117"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">See other example use cases (Figma)</a></span></span>

## <a name="anatomy"></a><span data-ttu-id="b5b1e-118">Составляющие</span><span class="sxs-lookup"><span data-stu-id="b5b1e-118">Anatomy</span></span>

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-anatomy.png" alt-text="Пользовательский интерфейс Анатомия представления диалогового окна для собраний." border="false":::

1. <span data-ttu-id="b5b1e-120">**Значок приложения**</span><span class="sxs-lookup"><span data-stu-id="b5b1e-120">**App icon**</span></span>
1. <span data-ttu-id="b5b1e-121">**Имя приложения**</span><span class="sxs-lookup"><span data-stu-id="b5b1e-121">**App name**</span></span>
1. <span data-ttu-id="b5b1e-122">**Строка действия**</span><span class="sxs-lookup"><span data-stu-id="b5b1e-122">**Action string**</span></span>
1. <span data-ttu-id="b5b1e-123">**Значок закрытия:** Закрывает отдельное диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="b5b1e-123">**Dismiss icon:** Closes a single dialog.</span></span> <span data-ttu-id="b5b1e-124">Всегда используйте значок закрытия сверху справа, а не действие в нижнем колонтитуле.</span><span class="sxs-lookup"><span data-stu-id="b5b1e-124">Always use the upper-right close icon instead of an action in the footer.</span></span>
1. <span data-ttu-id="b5b1e-125">**Вебвиев**: отображает все содержимое и кнопки сторонних приложений (рекомендуется использовать стандартные кнопки групповых команд).</span><span class="sxs-lookup"><span data-stu-id="b5b1e-125">**Webview**: Displays all third-party app content and buttons (standard Teams buttons recommended).</span></span>

### <a name="sizing"></a><span data-ttu-id="b5b1e-126">Способ</span><span class="sxs-lookup"><span data-stu-id="b5b1e-126">Sizing</span></span>

<span data-ttu-id="b5b1e-127">Размеры диалоговых окон собраний могут различаться в зависимости от различных вариантов использования, но всегда необходимо сохранять заполнение и размеры компонентов.</span><span class="sxs-lookup"><span data-stu-id="b5b1e-127">In-meeting dialogs can vary in size to account for different use cases, but you must always maintain padding and component sizes.</span></span>

* <span data-ttu-id="b5b1e-128">**Height**: высота диалогового окна определяется содержимым в вебвиев.</span><span class="sxs-lookup"><span data-stu-id="b5b1e-128">**Height**: The height of the dialog is determined by the content in the webview.</span></span> <span data-ttu-id="b5b1e-129">Вертикальная прокрутка занимает больше места для контента, который превышает максимальную заданную высоту.</span><span class="sxs-lookup"><span data-stu-id="b5b1e-129">Vertical scroll takes over for content that exceeds the maximum height you specify.</span></span>
* <span data-ttu-id="b5b1e-130">**Ширина**: ширина вебвиев — это абсолютное значение в указанном диапазоне.</span><span class="sxs-lookup"><span data-stu-id="b5b1e-130">**Width**: The width of the webview is an absolute value within the range you specify.</span></span>

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-sizing.png" alt-text="Иллюстрация, в которой показаны возможные размеры диалогового окна для собраний. Height: высота диалогового окна определяется содержимым в вебвиев. Вертикальная прокрутка применяется к содержимому, которое превышает максимальную высоту (определено пользователем). Min: None. Максимум: 400 пикселей (320 пикселей вебвиев). Ширина: ширина вебвиев — это абсолютное значение в указанном диапазоне. Min: 288 пикселей (256 пикселей вебвиев). Максимум: 468 пикселей (436 пикселей вебвиев)." border="false":::

## <a name="behavior"></a><span data-ttu-id="b5b1e-132">Поведение</span><span class="sxs-lookup"><span data-stu-id="b5b1e-132">Behavior</span></span>

<span data-ttu-id="b5b1e-133">В <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">фигма</a>можно просмотреть общее поведение диалогового окна для собраний, например REST, Загрузка и многое другое.</span><span class="sxs-lookup"><span data-stu-id="b5b1e-133">See general in-meeting dialog behavior, such as rest, loading, and more, in <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Figma</a>.</span></span>

### <a name="position"></a><span data-ttu-id="b5b1e-134">Position</span><span class="sxs-lookup"><span data-stu-id="b5b1e-134">Position</span></span>

<span data-ttu-id="b5b1e-135">Диалоги в собрании выравниваются в центре этапа собрания.</span><span class="sxs-lookup"><span data-stu-id="b5b1e-135">In-meeting dialogs are aligned in the center of the meeting stage.</span></span> <span data-ttu-id="b5b1e-136">Они не могут быть перенесены и работать в рамках платформы Teams на уровне системы.</span><span class="sxs-lookup"><span data-stu-id="b5b1e-136">They can’t be dragged and work within the framework of Teams system-level notifications.</span></span>

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-position.png" alt-text="Иллюстрация отображения пользовательского интерфейса диалогового окна для собраний." border="false":::

### <a name="aggregation"></a><span data-ttu-id="b5b1e-138">Объединен</span><span class="sxs-lookup"><span data-stu-id="b5b1e-138">Aggregation</span></span>

<span data-ttu-id="b5b1e-139">Одновременно отображается только одно диалоговое окно, ранжирование по стеку от последнего к последнему, отправленному внизу.</span><span class="sxs-lookup"><span data-stu-id="b5b1e-139">Only one dialog displays at a time, stack ranking from last to most recent sent to the bottom.</span></span> <span data-ttu-id="b5b1e-140">После того как диалоговое окно будет устранено или закрыто, оно будет следующим.</span><span class="sxs-lookup"><span data-stu-id="b5b1e-140">Once a dialog is resolved or dismissed, the next one take its place.</span></span>

<span data-ttu-id="b5b1e-141"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Пример (фигма)</a></span><span class="sxs-lookup"><span data-stu-id="b5b1e-141"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">See an example (Figma)</a></span></span>

### <a name="scrolling"></a><span data-ttu-id="b5b1e-142">Прокрутки</span><span class="sxs-lookup"><span data-stu-id="b5b1e-142">Scrolling</span></span>

<span data-ttu-id="b5b1e-143">Прокрутка происходит в части вебвиев диалогового окна собрания.</span><span class="sxs-lookup"><span data-stu-id="b5b1e-143">Scrolling occurs in the webview portion of an in-meeting dialog.</span></span> <span data-ttu-id="b5b1e-144">Обратите внимание на следующие особенности прокрутки:</span><span class="sxs-lookup"><span data-stu-id="b5b1e-144">Remember the following about scrolling:</span></span>

* <span data-ttu-id="b5b1e-145">Эту возможность можно прокручивать только по вертикали.</span><span class="sxs-lookup"><span data-stu-id="b5b1e-145">You should only be able to scroll vertically.</span></span>
* <span data-ttu-id="b5b1e-146">Отображается только содержимое, к которому вы выполнили прокрутку (ничего или не ниже).</span><span class="sxs-lookup"><span data-stu-id="b5b1e-146">You can only see the content you've scrolled to (nothing above or below).</span></span>

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-scroll.png" alt-text="Иллюстрация, на которой показано, как работает прокрутка содержимого вебвиев в диалоговом окне собраний." border="false":::

### <a name="buttons"></a><span data-ttu-id="b5b1e-148">Кнопки</span><span class="sxs-lookup"><span data-stu-id="b5b1e-148">Buttons</span></span>

<span data-ttu-id="b5b1e-149">Кнопки диалогового окна для собраний входят в состав вебвиев ([см. несколько примеров](#best-practices)).</span><span class="sxs-lookup"><span data-stu-id="b5b1e-149">In-meeting dialog buttons are part of the webview ([see some examples](#best-practices)).</span></span>

<span data-ttu-id="b5b1e-150">В отличие от схожих компонентов, диалоги в диалоговых окнах для собраний удаляются после того, как пользователь нажимает кнопку.</span><span class="sxs-lookup"><span data-stu-id="b5b1e-150">Unlike similar components, in-meeting dialogs are dismissed once a user selects a button.</span></span>

## <a name="components"></a><span data-ttu-id="b5b1e-151">Компоненты</span><span class="sxs-lookup"><span data-stu-id="b5b1e-151">Components</span></span>

<span data-ttu-id="b5b1e-152">Диалоги в собрании в основном создаются с помощью следующих <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">компонентов пользовательского интерфейса (фигма)</a>, основанных на <a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">системе дизайна Fluent</a>.</span><span class="sxs-lookup"><span data-stu-id="b5b1e-152">In-meeting dialogs are built primarily with the following <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">UI components (Figma)</a>, which are based on the <a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">Fluent Design System</a>.</span></span>

<span data-ttu-id="b5b1e-153">Компонент</span><span class="sxs-lookup"><span data-stu-id="b5b1e-153">Component</span></span> | <span data-ttu-id="b5b1e-154">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="b5b1e-154">Guidelines</span></span> | <span data-ttu-id="b5b1e-155">Пример</span><span class="sxs-lookup"><span data-stu-id="b5b1e-155">Example</span></span>
 - | - | -
<span data-ttu-id="b5b1e-156">Кнопка</span><span class="sxs-lookup"><span data-stu-id="b5b1e-156">Button</span></span> | <span data-ttu-id="b5b1e-157">Основные и дополнительные кнопки могут быть средними или малыми</span><span class="sxs-lookup"><span data-stu-id="b5b1e-157">Primary and secondary buttons can be medium or small</span></span> | <span data-ttu-id="b5b1e-158">Отправка ответа</span><span class="sxs-lookup"><span data-stu-id="b5b1e-158">Send a response</span></span>
<span data-ttu-id="b5b1e-159">Input</span><span class="sxs-lookup"><span data-stu-id="b5b1e-159">Input</span></span> | <span data-ttu-id="b5b1e-160">Поле для краткого ввода данных пользователем.</span><span class="sxs-lookup"><span data-stu-id="b5b1e-160">Field for brief user input.</span></span> <span data-ttu-id="b5b1e-161">Текст метки может включать значок</span><span class="sxs-lookup"><span data-stu-id="b5b1e-161">Label text can include an icon</span></span>  | <span data-ttu-id="b5b1e-162">Введите отзыв</span><span class="sxs-lookup"><span data-stu-id="b5b1e-162">Enter feedback</span></span>
<span data-ttu-id="b5b1e-163">Раскрывающийся список</span><span class="sxs-lookup"><span data-stu-id="b5b1e-163">Dropdown</span></span> | <span data-ttu-id="b5b1e-164">Выберите один или несколько параметров из списка.</span><span class="sxs-lookup"><span data-stu-id="b5b1e-164">Select one or more options from a list.</span></span> <span data-ttu-id="b5b1e-165">Может включать функции поиска и выбора нескольких элементов</span><span class="sxs-lookup"><span data-stu-id="b5b1e-165">Can include search and multi-selection features</span></span> | <span data-ttu-id="b5b1e-166">Выбор языка</span><span class="sxs-lookup"><span data-stu-id="b5b1e-166">Choose a language</span></span>
<span data-ttu-id="b5b1e-167">Элементы управления выбором</span><span class="sxs-lookup"><span data-stu-id="b5b1e-167">Selection controls</span></span> | <span data-ttu-id="b5b1e-168">Используйте флажки для нескольких вариантов или переключателей и переключитесь на один вариант.</span><span class="sxs-lookup"><span data-stu-id="b5b1e-168">Use checkboxes for multiple choices or radio buttons and toggles for single choices.</span></span> <span data-ttu-id="b5b1e-169">Для более подробного выбора используйте ползунок</span><span class="sxs-lookup"><span data-stu-id="b5b1e-169">For more detailed selections, use a slider</span></span> | <span data-ttu-id="b5b1e-170">Голосование за опрос</span><span class="sxs-lookup"><span data-stu-id="b5b1e-170">Vote in a poll</span></span>
<span data-ttu-id="b5b1e-171">Оповещения</span><span class="sxs-lookup"><span data-stu-id="b5b1e-171">Alerts</span></span> | <span data-ttu-id="b5b1e-172">При отображении срочных сообщений, состояния ошибок или предупреждений сообщение должно быть кратким и не прерывать текущую задачу пользователя</span><span class="sxs-lookup"><span data-stu-id="b5b1e-172">Whether displaying an urgent message, error state, or warning, the message should be short and won't interrupt the user's current task</span></span> | <span data-ttu-id="b5b1e-173">Ошибка отображения при отправке ответа</span><span class="sxs-lookup"><span data-stu-id="b5b1e-173">Display issue when submitting a response</span></span>

## <a name="theming"></a><span data-ttu-id="b5b1e-174">Темы</span><span class="sxs-lookup"><span data-stu-id="b5b1e-174">Theming</span></span>

### <a name="colors"></a><span data-ttu-id="b5b1e-175">Цвета</span><span class="sxs-lookup"><span data-stu-id="b5b1e-175">Colors</span></span>

<span data-ttu-id="b5b1e-176">Используйте <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">рекомендуемую цветовую схему (фигма)</a> для фоновых изображений, переднего плана и состояний.</span><span class="sxs-lookup"><span data-stu-id="b5b1e-176">Use the <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">recommended color scheme (Figma)</a> for backgrounds, foregrounds, and conveying states.</span></span>

### <a name="typography"></a><span data-ttu-id="b5b1e-177">Шрифтовое оформление</span><span class="sxs-lookup"><span data-stu-id="b5b1e-177">Typography</span></span>

<span data-ttu-id="b5b1e-178">Используйте <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Рекомендуемые размеры и веса шрифтов (фигма)</a> для заголовков, основного текста и текста метаданных.</span><span class="sxs-lookup"><span data-stu-id="b5b1e-178">Use the <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">recommended font sizes and weights (Figma)</a> for titles, body text, and metadata text.</span></span>

## <a name="best-practices"></a><span data-ttu-id="b5b1e-179">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="b5b1e-179">Best practices</span></span>

<span data-ttu-id="b5b1e-180">Несмотря на то, что в диалоговых окнах для собраний вызовы более эффективны, они также могут дераил вызовы, если они слишком перегружены.</span><span class="sxs-lookup"><span data-stu-id="b5b1e-180">While in-meeting dialogs can make calls more effective, they also can derail calls if too obtrusive.</span></span> <span data-ttu-id="b5b1e-181">Как правило, эти диалоговые окна следует использовать экономно и следовать приведенным ниже рекомендациям.</span><span class="sxs-lookup"><span data-stu-id="b5b1e-181">In general, use the dialogs sparingly and follow these best practices.</span></span>

### <a name="navigation"></a><span data-ttu-id="b5b1e-182">Навигация</span><span class="sxs-lookup"><span data-stu-id="b5b1e-182">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-steps-do.png" alt-text="Иллюстрация, демонстрирующая способ ограничения содержимого диалогового окна собрания на один экран, чтобы пользователи могли сосредоточиться на собрании." border="false":::

#### <a name="do-keep-it-contained"></a><span data-ttu-id="b5b1e-184">Do: Храните его</span><span class="sxs-lookup"><span data-stu-id="b5b1e-184">Do: Keep it contained</span></span>

<span data-ttu-id="b5b1e-185">Ограничение содержимого диалогового окна для собраний на один экран, чтобы пользователи могли сосредоточиться на собрании.</span><span class="sxs-lookup"><span data-stu-id="b5b1e-185">Limit in-meeting dialog content to a single screen so users can focus on the meeting.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-steps-dont.png" alt-text="Иллюстрация, в которой показано, как диалоги в диалоговых окнах собраний не требуют от пользователей переходить по содержимому." border="false":::

#### <a name="dont-include-multiple-steps"></a><span data-ttu-id="b5b1e-187">Не: включать несколько шагов</span><span class="sxs-lookup"><span data-stu-id="b5b1e-187">Don't: Include multiple steps</span></span>

<span data-ttu-id="b5b1e-188">В диалоговых окнах для собраний не требуется перемещаться по содержимому.</span><span class="sxs-lookup"><span data-stu-id="b5b1e-188">In-meeting dialogs shouldn't require users to navigate through content.</span></span>

   :::column-end:::
:::row-end:::

### <a name="interactions"></a><span data-ttu-id="b5b1e-189">Диалог</span><span class="sxs-lookup"><span data-stu-id="b5b1e-189">Interactions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-interactions-do.png" alt-text="Иллюстрация, на которой показано, почему необходимо удалить ненужные материалы, не позволяющие пользователям быстро выполнить что-либо." border="false":::

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-interactions-dont.png" alt-text="На другом рисунке показано, почему необходимо удалить ненужные материалы, которые не помогают пользователям быстро выполнить какие-либо действия." border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-tab-do.png" alt-text="Иллюстрация, на которой показано, что при необходимости использовать сложные взаимодействия рекомендуется использовать один столбец в области "права на собрание"." border="false":::

#### <a name="do-limit-number-of-interactions"></a><span data-ttu-id="b5b1e-193">Do: ограничить количество взаимодействий</span><span class="sxs-lookup"><span data-stu-id="b5b1e-193">Do: Limit number of interactions</span></span>

<span data-ttu-id="b5b1e-194">Удалите ненужные материалы, не позволяющие пользователям быстро выполнить что-либо.</span><span class="sxs-lookup"><span data-stu-id="b5b1e-194">Remove unnecessary content that doesn't help users accomplish something quickly.</span></span> <span data-ttu-id="b5b1e-195">Если вам нужны сложные взаимодействия, мы настоятельно рекомендуем отображать контент с помощью одного столбца на вкладке на собрании.</span><span class="sxs-lookup"><span data-stu-id="b5b1e-195">If you need complex interactions, we strongly recommend displaying your content using a single column on the in-meeting tab instead.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-tab-dont.png" alt-text="Иллюстрация, демонстрирующая недостаточное количество взаимодействий в диалоговом окне собраний." border="false":::

#### <a name="dont-introduce-unnecessary-elements"></a><span data-ttu-id="b5b1e-197">Не следует добавлять ненужные элементы.</span><span class="sxs-lookup"><span data-stu-id="b5b1e-197">Don't: Introduce unnecessary elements</span></span>

<span data-ttu-id="b5b1e-198">Вы можете разрабатывать одно диалоговое окно для собраний с несколькими взаимодействиями, но слишком много может отвлекаться от собрания.</span><span class="sxs-lookup"><span data-stu-id="b5b1e-198">You may be able to design a single in-meeting dialog with multiple interactions, but too many can distract from the meeting.</span></span>

   :::column-end:::
:::row-end:::

### <a name="layout"></a><span data-ttu-id="b5b1e-199">Макет</span><span class="sxs-lookup"><span data-stu-id="b5b1e-199">Layout</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-layout-do.png" alt-text="Иллюстрация идеального макета для диалоговых окон для собраний." border="false":::

#### <a name="do-use-single-column-layouts"></a><span data-ttu-id="b5b1e-201">Do: использование макетов с одним столбцом</span><span class="sxs-lookup"><span data-stu-id="b5b1e-201">Do: Use single-column layouts</span></span>

<span data-ttu-id="b5b1e-202">Так как диалоги находятся в центре этапа собрания, выполнение задачи должно быть быстрым и простым, чтобы избежать недовольство пользователей.</span><span class="sxs-lookup"><span data-stu-id="b5b1e-202">Since the dialogs are at the center of the meeting stage, task completion should be fast and simple to avoid user frustration.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-layout-dont.png" alt-text="Иллюстрация, на которой показан макет диалоговых окон для собраний, которые не рекомендуются." border="false":::

#### <a name="dont-clutter-the-space"></a><span data-ttu-id="b5b1e-204">Не совсем: незагромождения места</span><span class="sxs-lookup"><span data-stu-id="b5b1e-204">Don't: Clutter the space</span></span>

<span data-ttu-id="b5b1e-205">Сжатые и более структурированные контент могут отвлекаться и передаваться, особенно во время собрания.</span><span class="sxs-lookup"><span data-stu-id="b5b1e-205">Dense or overly structured content can be distracting and overwhelming, especially during a meeting.</span></span>

   :::column-end:::
:::row-end:::

### <a name="size"></a><span data-ttu-id="b5b1e-206">Size</span><span class="sxs-lookup"><span data-stu-id="b5b1e-206">Size</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-size-do.png" alt-text="Иллюстрация того, как размер диалогового окна для проведения собрания всегда должен быть одинаковым." border="false":::

#### <a name="do-keep-it-consistent"></a><span data-ttu-id="b5b1e-208">Do: обеспечение согласованности</span><span class="sxs-lookup"><span data-stu-id="b5b1e-208">Do: Keep it consistent</span></span>

<span data-ttu-id="b5b1e-209">Это важно, так как диалоги в собрании всегда отображаются в одном и том же расположении.</span><span class="sxs-lookup"><span data-stu-id="b5b1e-209">This is important because in-meeting dialogs always display in the same location.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-size-dont.png" alt-text="Иллюстрация, в которой показано, как не следует использовать разные размеры диалоговых окон." border="false":::

#### <a name="dont-always-fit-to-the-content"></a><span data-ttu-id="b5b1e-211">Не следует всегда помещаться в содержимом.</span><span class="sxs-lookup"><span data-stu-id="b5b1e-211">Don't: Always fit to the content</span></span>

<span data-ttu-id="b5b1e-212">Возможно, вы пытаетесь избежать горизонтальной прокрутки, но в одном приложении несогласованно несколько размеров диалогового окна для собраний.</span><span class="sxs-lookup"><span data-stu-id="b5b1e-212">You may be trying to avoid horizontal scrolling, but multiple in-meeting dialog sizes within the same app is an inconsistent experience.</span></span>

   :::column-end:::
:::row-end:::

### <a name="controls"></a><span data-ttu-id="b5b1e-213">Элементы управления</span><span class="sxs-lookup"><span data-stu-id="b5b1e-213">Controls</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-controls-do.png" alt-text="Иллюстрация, на которой показано место размещения кнопок в диалоговом окне собраний." border="false":::

#### <a name="do-right-align-the-primary-action"></a><span data-ttu-id="b5b1e-215">Do: выравнивание по правому краю основного действия</span><span class="sxs-lookup"><span data-stu-id="b5b1e-215">Do: Right align the primary action</span></span>

<span data-ttu-id="b5b1e-216">Мы рекомендуем расместить наиболее визуально активное действие в крайнем крайнем месте.</span><span class="sxs-lookup"><span data-stu-id="b5b1e-216">We recommend positioning the most visually heavy action to the right-most location.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-controls-dont.png" alt-text="Иллюстрация, на которой показано, как не располагать кнопки в диалоговом окне собрания." border="false":::

#### <a name="dont-left-or-center-align-actions"></a><span data-ttu-id="b5b1e-218">Не: действия слева или Выровнять по центру</span><span class="sxs-lookup"><span data-stu-id="b5b1e-218">Don't: Left or center align actions</span></span>

<span data-ttu-id="b5b1e-219">Это отличается от стандартного шаблона команд для управления размещением в диалоговом окне и может конфликтовать с диалоговым окном, расположенным в верхней части.</span><span class="sxs-lookup"><span data-stu-id="b5b1e-219">This deviates from the standard Teams pattern for control placement in a dialog and may conflict with a dialog behind the top one.</span></span>

   :::column-end:::
:::row-end:::

## <a name="accessibility"></a><span data-ttu-id="b5b1e-220">Специальные возможности</span><span class="sxs-lookup"><span data-stu-id="b5b1e-220">Accessibility</span></span>

<span data-ttu-id="b5b1e-221">Сведения о специальных возможностях содержатся в разделе <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">фигма</a>.</span><span class="sxs-lookup"><span data-stu-id="b5b1e-221">For information on accessibility, see <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Figma</a>.</span></span>

## <a name="resources"></a><span data-ttu-id="b5b1e-222">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="b5b1e-222">Resources</span></span>

* <span data-ttu-id="b5b1e-223"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Файл фигма для расширений собраний Microsoft Teams</a></span><span class="sxs-lookup"><span data-stu-id="b5b1e-223"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Microsoft Teams meeting extensions Figma file</a></span></span>

## <a name="validate-your-design"></a><span data-ttu-id="b5b1e-224">Проверка проекта</span><span class="sxs-lookup"><span data-stu-id="b5b1e-224">Validate your design</span></span>

<span data-ttu-id="b5b1e-225">Если вы планируете опубликовать свое приложение в AppSource, следует изучить проблемы, которые обычно приводят к сбою приложений во время отправки.</span><span class="sxs-lookup"><span data-stu-id="b5b1e-225">If you plan to publish your app to AppSource, you should understand the design issues that commonly cause apps to fail during submission.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b5b1e-226">Проверка рекомендаций по проверке макета</span><span class="sxs-lookup"><span data-stu-id="b5b1e-226">Check design validation guidelines</span></span>](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines)
