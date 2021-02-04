---
title: Вкладки на мобильных устройствах
description: Описание рекомендаций по разработке вкладок, которые работают на мобильных устройствах.
ms.topic: conceptual
keywords: 'руководство по проектированию teams: справочные руководства по платформе личных приложений для мобильных вкладок'
ms.openlocfilehash: 70ff46e446b146b134f34830e8867133cbeeca14
ms.sourcegitcommit: f74b74d5bed1df193e59f46121ada443fb57277b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/03/2021
ms.locfileid: "50093290"
---
# <a name="tabs-on-mobile"></a><span data-ttu-id="a0362-104">Вкладки на мобильных устройствах</span><span class="sxs-lookup"><span data-stu-id="a0362-104">Tabs on mobile</span></span>

> [!NOTE]
> <span data-ttu-id="a0362-105">Если вкладка "Канал/группа" будет отображаться на мобильных клиентах Teams, конфигурация должна иметь значение свойства `setSettings()` `websiteUrl` (см. ниже).</span><span class="sxs-lookup"><span data-stu-id="a0362-105">If you choose to have your channel/group tab appear on Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property (see below).</span></span>

<span data-ttu-id="a0362-106">Настраиваемые вкладки могут быть частью канала, группового чата или личного приложения (приложений, содержащих статические вкладки и/или бота "один к одному").</span><span class="sxs-lookup"><span data-stu-id="a0362-106">Custom tabs can be part of a channel, group chat, or personal app (apps that contain static tabs and/or a one-to-one bot).</span></span>

<span data-ttu-id="a0362-107">Личные приложения доступны на мобильных клиентах в средстве "Ящик приложения".</span><span class="sxs-lookup"><span data-stu-id="a0362-107">Personal apps are available on mobile clients in the app drawer.</span></span> <span data-ttu-id="a0362-108">Приложение может быть установлено только с настольного компьютера или веб-клиента и может отображаться на мобильных клиентах в течение 24 часов.</span><span class="sxs-lookup"><span data-stu-id="a0362-108">The app can only be installed from a desktop or web client, and can take up to 24 hours to appear on mobile clients.</span></span>

<span data-ttu-id="a0362-109">Вкладки канала также доступны на мобильных устройствах.</span><span class="sxs-lookup"><span data-stu-id="a0362-109">Channel tabs are also available on mobile.</span></span> <span data-ttu-id="a0362-110">Поведение по умолчанию в настоящее время используется для запуска вкладки `websiteUrl` в окне браузера.</span><span class="sxs-lookup"><span data-stu-id="a0362-110">The default behavior is currently to use your `websiteUrl` to launch your tab in a browser window.</span></span> <span data-ttu-id="a0362-111">Однако их можно загрузить на мобильный клиент, щелкнув меню переполнения рядом с вкладкой и выбрав команду `...` **"Открыть",** которая будет использовать вашу вкладку для загрузки в мобильном клиенте `contentUrl` Teams.</span><span class="sxs-lookup"><span data-stu-id="a0362-111">However, they can be loaded on a mobile client by clicking the `...` overflow menu next to the tab and choosing **Open**, which will use your `contentUrl` to load the tab inside the Teams mobile client.</span></span>

## <a name="accessing-personal-tabs"></a><span data-ttu-id="a0362-112">Доступ к личным вкладкам</span><span class="sxs-lookup"><span data-stu-id="a0362-112">Accessing personal tabs</span></span>

<span data-ttu-id="a0362-113">На следующем рисунке показано, как получить доступ к личной вкладке на мобильном устройстве.</span><span class="sxs-lookup"><span data-stu-id="a0362-113">The following illustration shows how you access a personal tab on mobile.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-app-drawer.png" alt-text="Иллюстрация, показывающая ящик мобильного приложения Teams." border="false":::

## <a name="accessing-channel-tabs"></a><span data-ttu-id="a0362-115">Доступ к вкладке канала</span><span class="sxs-lookup"><span data-stu-id="a0362-115">Accessing channel tabs</span></span>

<span data-ttu-id="a0362-116">На следующем рисунке показано, как получить доступ к вкладке канала на мобильном устройстве.</span><span class="sxs-lookup"><span data-stu-id="a0362-116">The following illustration shows how you access a channel tab on mobile.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab.png" alt-text="Иллюстрация, на которой показана вкладка &quot;Teams для мобильных устройств&quot;." border="false":::

## <a name="design-considerations"></a><span data-ttu-id="a0362-118">Особенности дизайна</span><span class="sxs-lookup"><span data-stu-id="a0362-118">Design considerations</span></span>

<span data-ttu-id="a0362-119">Наша мобильная платформа позволяет приложениям иммерсивно работать с содержимым приложения, отбирая весь экран отдельно от основной навигации Teams.</span><span class="sxs-lookup"><span data-stu-id="a0362-119">Our mobile platform allows apps to be an immersive experience with the app content taking up all of the screen apart from main Teams navigation.</span></span> <span data-ttu-id="a0362-120">Чтобы создать иммерсивное впечатление, отличное от Teams, следуйте этим рекомендациям.</span><span class="sxs-lookup"><span data-stu-id="a0362-120">To create an immersive experience that fits with Teams, follow these guidelines.</span></span>

### <a name="responsive-design"></a><span data-ttu-id="a0362-121">Адаптивный дизайн</span><span class="sxs-lookup"><span data-stu-id="a0362-121">Responsive design</span></span>

<span data-ttu-id="a0362-122">Так как вкладку можно открыть на устройствах с широким диапазоном размеров экрана, она должна следовать принципам [адаптивного дизайна.](https://www.w3schools.com/html/html_responsive.asp)</span><span class="sxs-lookup"><span data-stu-id="a0362-122">Because your tab can be opened on devices with a wide range of screen sizes, it needs to follow [responsive design](https://www.w3schools.com/html/html_responsive.asp) principles.</span></span> <span data-ttu-id="a0362-123">Все ключевые конструкции должны быть доступны на мобильных устройствах, и представления не должны быть искажены.</span><span class="sxs-lookup"><span data-stu-id="a0362-123">All of the key constructs should be accessible on mobile devices, and the views should not be distorted.</span></span> <span data-ttu-id="a0362-124">Убедитесь, что при загрузке вкладки на мобильном устройстве все кнопки и ссылки легко доступны с помощью навигации с помощью пальцев.</span><span class="sxs-lookup"><span data-stu-id="a0362-124">Ensure that when your tab is loaded on a mobile device, all buttons and links are easily accessible using finger-based navigation.</span></span>

### <a name="layouts"></a><span data-ttu-id="a0362-125">макеты;</span><span class="sxs-lookup"><span data-stu-id="a0362-125">Layouts</span></span>

<span data-ttu-id="a0362-126">Важно выбрать правильный макет для вкладки.</span><span class="sxs-lookup"><span data-stu-id="a0362-126">Choosing the correct layout for your tab is important.</span></span> <span data-ttu-id="a0362-127">Следует рассмотреть тип представляемой информации и выбрать макет, который упорядочитает ее для простого использования.</span><span class="sxs-lookup"><span data-stu-id="a0362-127">You should consider the kind of information you're presenting, and choose a layout that organizes it for easy consumption.</span></span> <span data-ttu-id="a0362-128">Некоторые возможные варианты описаны ниже.</span><span class="sxs-lookup"><span data-stu-id="a0362-128">Some potential options are outlined below.</span></span>

#### <a name="single-canvas"></a><span data-ttu-id="a0362-129">Один холст</span><span class="sxs-lookup"><span data-stu-id="a0362-129">Single canvas</span></span>

<span data-ttu-id="a0362-130">Это одна большая область, в которой нужно сделать работу.</span><span class="sxs-lookup"><span data-stu-id="a0362-130">This is one large area where work gets done.</span></span> <span data-ttu-id="a0362-131">Приложение вики-сайта Teams следует этому шаблону.</span><span class="sxs-lookup"><span data-stu-id="a0362-131">The Teams Wiki app follows this pattern.</span></span> <span data-ttu-id="a0362-132">Если у вас есть приложение, которое не разделяет содержимое на более мелкие компоненты, это будет хорошим местом.</span><span class="sxs-lookup"><span data-stu-id="a0362-132">If you have an app that doesn’t separate content into smaller components this would be a good fit.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-single-canvas.png" alt-text="Иллюстрация, на которой показана вкладка &quot;Один холст&quot; для мобильных устройств Teams." border="false":::

#### <a name="list"></a><span data-ttu-id="a0362-134">Перечисление</span><span class="sxs-lookup"><span data-stu-id="a0362-134">List</span></span>

<span data-ttu-id="a0362-135">Списки отлично подходит для сортировки и фильтрации больших объемов данных и отлично по-настоящему важны.</span><span class="sxs-lookup"><span data-stu-id="a0362-135">Lists are great for sorting and filtering large quantities of data and are great at keeping the most important things at the top.</span></span> <span data-ttu-id="a0362-136">Полезно использовать столбцы с возможностью сортировки.</span><span class="sxs-lookup"><span data-stu-id="a0362-136">It is helpful to use sortable columns.</span></span> <span data-ttu-id="a0362-137">Действия можно добавить к каждому элементу списка в меню с многолипсом.</span><span class="sxs-lookup"><span data-stu-id="a0362-137">Actions can be added to each list item under the ellipsis menu.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-list.png" alt-text="Иллюстрация, на которой показана вкладка списка для мобильных устройств Teams." border="false":::

#### <a name="grid"></a><span data-ttu-id="a0362-139">Grid</span><span class="sxs-lookup"><span data-stu-id="a0362-139">Grid</span></span>

<span data-ttu-id="a0362-140">Сетки полезны для показа элементов с высокой наглядности.</span><span class="sxs-lookup"><span data-stu-id="a0362-140">Grids are useful for showing elements which are highly visual.</span></span> <span data-ttu-id="a0362-141">Он помогает включить фильтр или управление поиском в верхней части.</span><span class="sxs-lookup"><span data-stu-id="a0362-141">It helps to include a filter or search control at the top.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-grid.png" alt-text="Иллюстрация с мобильной вкладкой Teams с макетом сетки." border="false":::

### <a name="tabs-with-bots-on-mobile"></a><span data-ttu-id="a0362-143">Вкладки с ботами на мобильных устройствах</span><span class="sxs-lookup"><span data-stu-id="a0362-143">Tabs with bots on mobile</span></span>

<span data-ttu-id="a0362-144">В следующем примере это личное приложение с вкладками и ботом.</span><span class="sxs-lookup"><span data-stu-id="a0362-144">The following example is a personal app that has tabs and a bot.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-with-bot.png" alt-text="Иллюстрация, показывающая, как мобильное приложение Teams с вкладками и ботом." border="false":::

## <a name="ui-components"></a><span data-ttu-id="a0362-146">Компоненты пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="a0362-146">UI components</span></span>

### <a name="color-palettes"></a><span data-ttu-id="a0362-147">Цветовые палитры</span><span class="sxs-lookup"><span data-stu-id="a0362-147">Color palettes</span></span>

<span data-ttu-id="a0362-148">Использование нашей утвержденной нейтральной палитры для фонов, уведомлений, текста и кнопок поможет вашему приложению лучше работать дома в Teams.</span><span class="sxs-lookup"><span data-stu-id="a0362-148">Using our approved neutral palette for backgrounds, notifications, text, and buttons will help your app feel more at home in Teams.</span></span> <span data-ttu-id="a0362-149">Так как на мобильных устройствах Teams есть две темы (светлая и темная), лучше убедиться, что ваше приложение хорошо выглядит в обоих этих приложениях.</span><span class="sxs-lookup"><span data-stu-id="a0362-149">Since Teams mobile has two colour themes (light and dark), it’s a good idea to make sure your app looks great in both.</span></span>

#### <a name="light-color"></a><span data-ttu-id="a0362-150">Цвет света</span><span class="sxs-lookup"><span data-stu-id="a0362-150">Light color</span></span>

![светлая цветовая палитра](../../assets/images/light-color.png)

#### <a name="dark-color"></a><span data-ttu-id="a0362-152">Темный цвет</span><span class="sxs-lookup"><span data-stu-id="a0362-152">Dark color</span></span>

![темная цветовая палитра](../../assets/images/dark-color.png)

### <a name="buttons-and-controls"></a><span data-ttu-id="a0362-154">Кнопки и элементы управления</span><span class="sxs-lookup"><span data-stu-id="a0362-154">Buttons and controls</span></span>

<span data-ttu-id="a0362-155">Стиль кнопок помогает сообщить, какие действия они запускают.</span><span class="sxs-lookup"><span data-stu-id="a0362-155">The way buttons are styled helps communicate what kind of action they trigger.</span></span> <span data-ttu-id="a0362-156">Мы поддерживаем широкий спектр кнопок, отформатированные для показа различных уровней акцента.</span><span class="sxs-lookup"><span data-stu-id="a0362-156">We maintain a wide range of buttons that are formatted to show different levels of emphasis.</span></span> <span data-ttu-id="a0362-157">Кнопки могут иметь текст, значок или сочетание текста и значка.</span><span class="sxs-lookup"><span data-stu-id="a0362-157">Buttons can have text, an icon, or a combination of text and an icon.</span></span> <span data-ttu-id="a0362-158">Для связи разных уровней в иерархии мы разработали основные и дополнительные кнопки в каждой категории.</span><span class="sxs-lookup"><span data-stu-id="a0362-158">To communicate different levels in a hierarchy, we designed primary and secondary buttons within each category.</span></span>

#### <a name="buttons"></a><span data-ttu-id="a0362-159">Кнопки</span><span class="sxs-lookup"><span data-stu-id="a0362-159">Buttons</span></span>

<span data-ttu-id="a0362-160">Основные и дополнительные кнопки.</span><span class="sxs-lookup"><span data-stu-id="a0362-160">Primary and secondary buttons.</span></span>

![изображение кнопок](../../assets/images/buttons.png)

#### <a name="selection-controls"></a><span data-ttu-id="a0362-162">Элементы управления выбором</span><span class="sxs-lookup"><span data-stu-id="a0362-162">Selection controls</span></span>

<span data-ttu-id="a0362-163">Radio buttons, checkboxes, and toggles.</span><span class="sxs-lookup"><span data-stu-id="a0362-163">Radio buttons, checkboxes, and toggles.</span></span>

![элементы управления выбором](../../assets/images/selection-controls.png)

#### <a name="chiclets-and-pills"></a><span data-ttu-id="a0362-165">Податки и ветви</span><span class="sxs-lookup"><span data-stu-id="a0362-165">Chiclets and pills</span></span>

![2016](../../assets/images/chiclets-and-pills.png)

### <a name="typography"></a><span data-ttu-id="a0362-167">Шрифтовое оформление</span><span class="sxs-lookup"><span data-stu-id="a0362-167">Typography</span></span>

<span data-ttu-id="a0362-168">Оформление должно быть понятным и целеустремленным.</span><span class="sxs-lookup"><span data-stu-id="a0362-168">Typography should be clear and purposeful.</span></span> <span data-ttu-id="a0362-169">Подчеркивать важную информацию и избегать использования нескольких шрифтов и размеров, чтобы уменьшить путаницу.</span><span class="sxs-lookup"><span data-stu-id="a0362-169">Emphasize important information and avoid using multiple fonts and sizes to reduce confusion.</span></span> <span data-ttu-id="a0362-170">Мы рекомендуем использовать случай предложения и избегать использования всех caps для локализации и различивости.</span><span class="sxs-lookup"><span data-stu-id="a0362-170">We recommend using sentence case and avoiding the usage of all caps for localization and legibility.</span></span>

![опечатка для мобильных устройств](../../assets/images/mobile-typography.png)

### <a name="fields-and-flyouts"></a><span data-ttu-id="a0362-172">Поля и flyouts</span><span class="sxs-lookup"><span data-stu-id="a0362-172">Fields and flyouts</span></span>

<span data-ttu-id="a0362-173">Поля — это области, в которых пользователи могут вводить текст.</span><span class="sxs-lookup"><span data-stu-id="a0362-173">Fields are areas where users can input text.</span></span> <span data-ttu-id="a0362-174">Flyouts are more lightweight than dialogs and appear from the top pane.</span><span class="sxs-lookup"><span data-stu-id="a0362-174">Flyouts are more lightweight than dialogs and appear from the top pane.</span></span>

#### <a name="list-controls"></a><span data-ttu-id="a0362-175">Список элементов управления</span><span class="sxs-lookup"><span data-stu-id="a0362-175">List controls</span></span>

![элементы управления списками для мобильных устройств](../../assets/images/mobile-list-controls.png)

#### <a name="field-controls"></a><span data-ttu-id="a0362-177">Элементы управления полями</span><span class="sxs-lookup"><span data-stu-id="a0362-177">Field controls</span></span>

![элементы управления полями для мобильных устройств](../../assets/images/mobile-field-controls.png)

## <a name="developer-considerations"></a><span data-ttu-id="a0362-179">Вопросы для разработчиков</span><span class="sxs-lookup"><span data-stu-id="a0362-179">Developer considerations</span></span>

<span data-ttu-id="a0362-180">При создании приложения, которое включает вкладку, необходимо учесть (и протестировать) работу вкладки на клиентах Microsoft Teams для Android и iOS.</span><span class="sxs-lookup"><span data-stu-id="a0362-180">When you're building an app that includes a tab, you need to consider (and test) how your tab will function on both the Android and iOS Microsoft Teams clients.</span></span> <span data-ttu-id="a0362-181">В разделах ниже описаны некоторые ключевые сценарии, которые необходимо учесть.</span><span class="sxs-lookup"><span data-stu-id="a0362-181">The sections below outline some of the key scenarios you need to consider.</span></span>

### <a name="testing-on-mobile-clients"></a><span data-ttu-id="a0362-182">Тестирование на мобильных клиентах</span><span class="sxs-lookup"><span data-stu-id="a0362-182">Testing on mobile clients</span></span>

<span data-ttu-id="a0362-183">Необходимо проверить, правильно ли работает вкладка на мобильных устройствах различных размеров и качества.</span><span class="sxs-lookup"><span data-stu-id="a0362-183">You need to validate that your tab functions properly on mobile devices of various sizes and qualities.</span></span> <span data-ttu-id="a0362-184">Для устройств с Android можно использовать [DevTools](~/tabs/how-to/developer-tools.md) для отладки вкладки во время ее работы.</span><span class="sxs-lookup"><span data-stu-id="a0362-184">For Android devices, you can use the [DevTools](~/tabs/how-to/developer-tools.md) to debug your tab while it is running.</span></span> <span data-ttu-id="a0362-185">Рекомендуется тестировать как на высокой, так и на малой скорости, а также на планшете.</span><span class="sxs-lookup"><span data-stu-id="a0362-185">We recommend that you test on both high and low performing devices, as well as on a tablet.</span></span>

### <a name="authentication"></a><span data-ttu-id="a0362-186">Проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="a0362-186">Authentication</span></span>

<span data-ttu-id="a0362-187">Чтобы проверка подлинности работала на мобильных клиентах, необходимо обновить SDK JavaScript для Teams по крайней мере до версии 1.4.1.</span><span class="sxs-lookup"><span data-stu-id="a0362-187">For authentication to work on mobile clients, you must upgrade you Teams JavaScript SDK to at least version 1.4.1.</span></span>

### <a name="low-bandwidth-and-intermittent-connections"></a><span data-ttu-id="a0362-188">Низкая пропускная способность и периодические подключения</span><span class="sxs-lookup"><span data-stu-id="a0362-188">Low bandwidth and intermittent connections</span></span>

<span data-ttu-id="a0362-189">Мобильные клиенты регулярно должны работать с низкой пропускной способностью и периодическими подключениями.</span><span class="sxs-lookup"><span data-stu-id="a0362-189">Mobile clients regularly need to function with low bandwidth and intermittent connections.</span></span> <span data-ttu-id="a0362-190">Ваше приложение должно правильно обрабатывать времявыдающие действия, предоставляя пользователю контекстное сообщение.</span><span class="sxs-lookup"><span data-stu-id="a0362-190">Your app should handle any timeouts appropriately by providing a contextual message to the user.</span></span> <span data-ttu-id="a0362-191">Кроме того, индикаторы хода выполнения следует использовать для предоставления пользователям отзывов о любых длительных процессах.</span><span class="sxs-lookup"><span data-stu-id="a0362-191">You should also user progress indicators to provide feedback to your users for any long-running processes.</span></span>

> [!NOTE]
> <span data-ttu-id="a0362-192">Вкладки включены на мобильных устройствах только после того, как приложение будет добавлено в список разрешений на основе входных данных группы утверждения.</span><span class="sxs-lookup"><span data-stu-id="a0362-192">Tabs are enabled on mobile only after the application is added to an allow list, based on the input of the approval team.</span></span> <span data-ttu-id="a0362-193">Чтобы проверить отклик мобильных устройств, обратитесь к teamsubm@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="a0362-193">To check mobile responsiveness, reach out to teamsubm@microsoft.com.</span></span> 