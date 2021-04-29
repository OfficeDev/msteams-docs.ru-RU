---
title: Вкладки на мобильных устройствах
description: Описывает рекомендации по разработке вкладок, которые работают на мобильных устройствах.
ms.topic: conceptual
localization_priority: Normal
keywords: группы разработки рекомендаций по справочной платформе персональных вкладок мобильных приложений
ms.openlocfilehash: cdcaddf5ba0fb18537e87daa4b459c7377225f76
ms.sourcegitcommit: d90c5dafea09e2893dea8da46ee49516bbaa04b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2021
ms.locfileid: "52075698"
---
# <a name="tabs-on-mobile"></a><span data-ttu-id="fabe7-104">Вкладки на мобильных устройствах</span><span class="sxs-lookup"><span data-stu-id="fabe7-104">Tabs on mobile</span></span>

<span data-ttu-id="fabe7-105">Вы можете включить вкладки в мобильных каналах Teams, чатах и личных приложениях.</span><span class="sxs-lookup"><span data-stu-id="fabe7-105">You can include tabs in Teams mobile channels, chats, and personal apps.</span></span>

## <a name="accessing-personal-tabs"></a><span data-ttu-id="fabe7-106">Доступ к личным вкладкам</span><span class="sxs-lookup"><span data-stu-id="fabe7-106">Accessing personal tabs</span></span>

<span data-ttu-id="fabe7-107">Вы можете получить доступ к личным вкладкам в ящике приложения.</span><span class="sxs-lookup"><span data-stu-id="fabe7-107">You can access personal tabs in the app drawer.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-app-drawer.png" alt-text="Иллюстрация, показывающая ящик мобильного приложения Teams." border="false":::

## <a name="accessing-channel-tabs"></a><span data-ttu-id="fabe7-109">Доступ к вкладке канала</span><span class="sxs-lookup"><span data-stu-id="fabe7-109">Accessing channel tabs</span></span>

<span data-ttu-id="fabe7-110">Вы можете получить доступ к вкладке канала и группы, выбрав кнопку **More** в канале или в чате, в котором они были добавлены.</span><span class="sxs-lookup"><span data-stu-id="fabe7-110">You can access channel and group tabs by selecting the **More** button in the channel or chat in which they've been added.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab.png" alt-text="Иллюстрация, показывающая вкладку Teams для мобильных устройств." border="false":::

## <a name="design-considerations"></a><span data-ttu-id="fabe7-112">Особенности дизайна</span><span class="sxs-lookup"><span data-stu-id="fabe7-112">Design considerations</span></span>

<span data-ttu-id="fabe7-113">Наша мобильная платформа позволяет приложениям быть иммерсивным опытом с контентом приложения, за исключением основной навигации Teams.</span><span class="sxs-lookup"><span data-stu-id="fabe7-113">Our mobile platform allows apps to be an immersive experience with the app content taking up all of the screen apart from main Teams navigation.</span></span> <span data-ttu-id="fabe7-114">Чтобы создать иммерсивный опыт, который подходит для Teams, следуйте этим рекомендациям.</span><span class="sxs-lookup"><span data-stu-id="fabe7-114">To create an immersive experience that fits with Teams, follow these guidelines.</span></span>

### <a name="responsive-design"></a><span data-ttu-id="fabe7-115">Адаптивный дизайн</span><span class="sxs-lookup"><span data-stu-id="fabe7-115">Responsive design</span></span>

<span data-ttu-id="fabe7-116">Так как вкладка может быть открыта на устройствах с широким диапазоном размеров экрана, она должна следовать принципам [гибкого проектирования.](https://www.w3schools.com/html/html_responsive.asp)</span><span class="sxs-lookup"><span data-stu-id="fabe7-116">Because your tab can be opened on devices with a wide range of screen sizes, it needs to follow [responsive design](https://www.w3schools.com/html/html_responsive.asp) principles.</span></span> <span data-ttu-id="fabe7-117">Все ключевые конструкции должны быть доступны на мобильных устройствах, и представления не должны искажаться.</span><span class="sxs-lookup"><span data-stu-id="fabe7-117">All of the key constructs should be accessible on mobile devices, and the views should not be distorted.</span></span> <span data-ttu-id="fabe7-118">Убедитесь, что при загрузке вкладки на мобильном устройстве все кнопки и ссылки легко доступны с помощью навигации на основе пальцев.</span><span class="sxs-lookup"><span data-stu-id="fabe7-118">Ensure that when your tab is loaded on a mobile device, all buttons and links are easily accessible using finger-based navigation.</span></span>

### <a name="layouts"></a><span data-ttu-id="fabe7-119">макеты;</span><span class="sxs-lookup"><span data-stu-id="fabe7-119">Layouts</span></span>

<span data-ttu-id="fabe7-120">Важно выбрать правильный макет вкладки.</span><span class="sxs-lookup"><span data-stu-id="fabe7-120">Choosing the correct layout for your tab is important.</span></span> <span data-ttu-id="fabe7-121">Необходимо рассмотреть тип представляемой информации и выбрать макет, который организует ее для легкого потребления.</span><span class="sxs-lookup"><span data-stu-id="fabe7-121">You should consider the kind of information you're presenting, and choose a layout that organizes it for easy consumption.</span></span> <span data-ttu-id="fabe7-122">Ниже описаны некоторые возможные варианты.</span><span class="sxs-lookup"><span data-stu-id="fabe7-122">Some potential options are outlined below.</span></span>

#### <a name="single-canvas"></a><span data-ttu-id="fabe7-123">Одно полотно</span><span class="sxs-lookup"><span data-stu-id="fabe7-123">Single canvas</span></span>

<span data-ttu-id="fabe7-124">Это одна большая область, в которой делается работа.</span><span class="sxs-lookup"><span data-stu-id="fabe7-124">This is one large area where work gets done.</span></span> <span data-ttu-id="fabe7-125">Приложение Teams Wiki следует этому шаблону.</span><span class="sxs-lookup"><span data-stu-id="fabe7-125">The Teams Wiki app follows this pattern.</span></span> <span data-ttu-id="fabe7-126">Если у вас есть приложение, которое не разделяет контент на более мелкие компоненты, это будет подходящим.</span><span class="sxs-lookup"><span data-stu-id="fabe7-126">If you have an app that doesn’t separate content into smaller components this would be a good fit.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-single-canvas.png" alt-text="Иллюстрация, на которой показана вкладка &quot;Одно полотно Для мобильных групп&quot;." border="false":::

#### <a name="list"></a><span data-ttu-id="fabe7-128">List</span><span class="sxs-lookup"><span data-stu-id="fabe7-128">List</span></span>

<span data-ttu-id="fabe7-129">Списки отлично подходит для сортировки и фильтрации больших объемов данных и отлично подходит для хранения наиболее важных вещей в верхней части.</span><span class="sxs-lookup"><span data-stu-id="fabe7-129">Lists are great for sorting and filtering large quantities of data and are great at keeping the most important things at the top.</span></span> <span data-ttu-id="fabe7-130">Полезно использовать сортируемые столбцы.</span><span class="sxs-lookup"><span data-stu-id="fabe7-130">It is helpful to use sortable columns.</span></span> <span data-ttu-id="fabe7-131">Действия могут быть добавлены к каждому элементу списка в меню ellipsis.</span><span class="sxs-lookup"><span data-stu-id="fabe7-131">Actions can be added to each list item under the ellipsis menu.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-list.png" alt-text="Иллюстрация, показывающая вкладку список мобильных групп." border="false":::

#### <a name="grid"></a><span data-ttu-id="fabe7-133">Grid</span><span class="sxs-lookup"><span data-stu-id="fabe7-133">Grid</span></span>

<span data-ttu-id="fabe7-134">Сетки полезны для демонстрации элементов с высокой наглядности.</span><span class="sxs-lookup"><span data-stu-id="fabe7-134">Grids are useful for showing elements which are highly visual.</span></span> <span data-ttu-id="fabe7-135">Это помогает включить фильтр или управление поиском в верхней части.</span><span class="sxs-lookup"><span data-stu-id="fabe7-135">It helps to include a filter or search control at the top.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-grid.png" alt-text="На рисунке показана вкладка для мобильных устройств Teams с макетом сетки." border="false":::

### <a name="tabs-with-bots-on-mobile"></a><span data-ttu-id="fabe7-137">Вкладки с ботами на мобильных устройствах</span><span class="sxs-lookup"><span data-stu-id="fabe7-137">Tabs with bots on mobile</span></span>

<span data-ttu-id="fabe7-138">Ниже приводится личный пример приложения с вкладками и ботом.</span><span class="sxs-lookup"><span data-stu-id="fabe7-138">The following example is a personal app that has tabs and a bot.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-with-bot.png" alt-text="На рисунке показывая, как мобильное приложение Teams с вкладками и ботом." border="false":::

## <a name="ui-components"></a><span data-ttu-id="fabe7-140">Компоненты пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="fabe7-140">UI components</span></span>

### <a name="color-palettes"></a><span data-ttu-id="fabe7-141">Цветовые палитры</span><span class="sxs-lookup"><span data-stu-id="fabe7-141">Color palettes</span></span>

<span data-ttu-id="fabe7-142">Использование нашей утвержденной нейтральной палитры фонов, уведомлений, текста и кнопок поможет приложению чувствовать себя как дома в Teams.</span><span class="sxs-lookup"><span data-stu-id="fabe7-142">Using our approved neutral palette for backgrounds, notifications, text, and buttons will help your app feel more at home in Teams.</span></span> <span data-ttu-id="fabe7-143">Так как мобильный телефон Teams имеет две цветовые темы (светлый и темный), лучше убедиться, что ваше приложение отлично выглядит в обоих.</span><span class="sxs-lookup"><span data-stu-id="fabe7-143">Since Teams mobile has two colour themes (light and dark), it’s a good idea to make sure your app looks great in both.</span></span>

#### <a name="light-color"></a><span data-ttu-id="fabe7-144">Светлый цвет</span><span class="sxs-lookup"><span data-stu-id="fabe7-144">Light color</span></span>

![светлая цветовая палитра](../../assets/images/light-color.png)

#### <a name="dark-color"></a><span data-ttu-id="fabe7-146">Темный цвет</span><span class="sxs-lookup"><span data-stu-id="fabe7-146">Dark color</span></span>

![темная цветовая палитра](../../assets/images/dark-color.png)

### <a name="buttons-and-controls"></a><span data-ttu-id="fabe7-148">Кнопки и элементы управления</span><span class="sxs-lookup"><span data-stu-id="fabe7-148">Buttons and controls</span></span>

<span data-ttu-id="fabe7-149">Стиль кнопок позволяет сообщить, какие действия они запускают.</span><span class="sxs-lookup"><span data-stu-id="fabe7-149">The way buttons are styled helps communicate what kind of action they trigger.</span></span> <span data-ttu-id="fabe7-150">Мы поддерживаем широкий диапазон кнопок, которые отформатированы, чтобы показать различные уровни акцента.</span><span class="sxs-lookup"><span data-stu-id="fabe7-150">We maintain a wide range of buttons that are formatted to show different levels of emphasis.</span></span> <span data-ttu-id="fabe7-151">Кнопки могут иметь текст, значок или сочетание текста и значка.</span><span class="sxs-lookup"><span data-stu-id="fabe7-151">Buttons can have text, an icon, or a combination of text and an icon.</span></span> <span data-ttu-id="fabe7-152">Чтобы общаться на разных уровнях в иерархии, мы разработали основные и вторичные кнопки в каждой категории.</span><span class="sxs-lookup"><span data-stu-id="fabe7-152">To communicate different levels in a hierarchy, we designed primary and secondary buttons within each category.</span></span>

#### <a name="buttons"></a><span data-ttu-id="fabe7-153">Кнопки</span><span class="sxs-lookup"><span data-stu-id="fabe7-153">Buttons</span></span>

<span data-ttu-id="fabe7-154">Основные и вторичные кнопки.</span><span class="sxs-lookup"><span data-stu-id="fabe7-154">Primary and secondary buttons.</span></span>

![изображение кнопок](../../assets/images/buttons.png)

#### <a name="selection-controls"></a><span data-ttu-id="fabe7-156">Элементы управления выбором</span><span class="sxs-lookup"><span data-stu-id="fabe7-156">Selection controls</span></span>

<span data-ttu-id="fabe7-157">Кнопки радио, почтовые ящики и очки.</span><span class="sxs-lookup"><span data-stu-id="fabe7-157">Radio buttons, checkboxes, and toggles.</span></span>

![элементы управления выбором](../../assets/images/selection-controls.png)

#### <a name="chiclets-and-pills"></a><span data-ttu-id="fabe7-159">Шиклеты и таблетки</span><span class="sxs-lookup"><span data-stu-id="fabe7-159">Chiclets and pills</span></span>

![шиклеты и таблетки](../../assets/images/chiclets-and-pills.png)

### <a name="typography"></a><span data-ttu-id="fabe7-161">Шрифтовое оформление</span><span class="sxs-lookup"><span data-stu-id="fabe7-161">Typography</span></span>

<span data-ttu-id="fabe7-162">Типография должна быть четкой и целенаправленной.</span><span class="sxs-lookup"><span data-stu-id="fabe7-162">Typography should be clear and purposeful.</span></span> <span data-ttu-id="fabe7-163">Подчеркивать важные сведения и избегать использования нескольких шрифтов и размеров для уменьшения путаницы.</span><span class="sxs-lookup"><span data-stu-id="fabe7-163">Emphasize important information and avoid using multiple fonts and sizes to reduce confusion.</span></span> <span data-ttu-id="fabe7-164">Рекомендуется использовать пример предложения и избегать использования всех колпачок для локализации и разнонабности.</span><span class="sxs-lookup"><span data-stu-id="fabe7-164">We recommend using sentence case and avoiding the usage of all caps for localization and legibility.</span></span>

![мобильный опечаток](../../assets/images/mobile-typography.png)

### <a name="fields-and-flyouts"></a><span data-ttu-id="fabe7-166">Поля и вылеты</span><span class="sxs-lookup"><span data-stu-id="fabe7-166">Fields and flyouts</span></span>

<span data-ttu-id="fabe7-167">Поля — это области, в которых пользователи могут вводить текст.</span><span class="sxs-lookup"><span data-stu-id="fabe7-167">Fields are areas where users can input text.</span></span> <span data-ttu-id="fabe7-168">Вылеты более легкие, чем диалоги, и отображаются на верхней области.</span><span class="sxs-lookup"><span data-stu-id="fabe7-168">Flyouts are more lightweight than dialogs and appear from the top pane.</span></span>

#### <a name="list-controls"></a><span data-ttu-id="fabe7-169">Список элементов управления</span><span class="sxs-lookup"><span data-stu-id="fabe7-169">List controls</span></span>

![элементы управления списками мобильных устройств](../../assets/images/mobile-list-controls.png)

#### <a name="field-controls"></a><span data-ttu-id="fabe7-171">Элементы управления полями</span><span class="sxs-lookup"><span data-stu-id="fabe7-171">Field controls</span></span>

![элементы управления мобильными полями](../../assets/images/mobile-field-controls.png)

## <a name="developer-considerations"></a><span data-ttu-id="fabe7-173">Соображения разработчика</span><span class="sxs-lookup"><span data-stu-id="fabe7-173">Developer considerations</span></span>

<span data-ttu-id="fabe7-174">При создании приложения, включаемого в вкладку, необходимо учитывать (и тестировать) функции вкладки на клиентах Android и iOS Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="fabe7-174">When you're building an app that includes a tab, you need to consider (and test) how your tab will function on both the Android and iOS Microsoft Teams clients.</span></span> <span data-ttu-id="fabe7-175">В разделах ниже описаны некоторые ключевые сценарии, которые необходимо рассмотреть.</span><span class="sxs-lookup"><span data-stu-id="fabe7-175">The sections below outline some of the key scenarios you need to consider.</span></span>

### <a name="authentication"></a><span data-ttu-id="fabe7-176">Проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="fabe7-176">Authentication</span></span>

<span data-ttu-id="fabe7-177">Для проверки подлинности для мобильных клиентов необходимо обновить команду JavaScript SDK по крайней мере до версии 1.4.1.</span><span class="sxs-lookup"><span data-stu-id="fabe7-177">For authentication to work on mobile clients, you must upgrade you Teams JavaScript SDK to at least version 1.4.1.</span></span>

### <a name="low-bandwidth-and-intermittent-connections"></a><span data-ttu-id="fabe7-178">Низкая пропускная способность и периодические подключения</span><span class="sxs-lookup"><span data-stu-id="fabe7-178">Low bandwidth and intermittent connections</span></span>

<span data-ttu-id="fabe7-179">Мобильные клиенты регулярно должны работать с низкой пропускной способностью и периодическими подключениями.</span><span class="sxs-lookup"><span data-stu-id="fabe7-179">Mobile clients regularly need to function with low bandwidth and intermittent connections.</span></span> <span data-ttu-id="fabe7-180">Ваше приложение должно надлежащим образом обрабатывать любые периоды времени, предоставляя пользователю контекстное сообщение.</span><span class="sxs-lookup"><span data-stu-id="fabe7-180">Your app should handle any timeouts appropriately by providing a contextual message to the user.</span></span> <span data-ttu-id="fabe7-181">Кроме того, необходимо использовать индикаторы прогресса пользователей, чтобы предоставить пользователям обратную связь для любых длительных процессов.</span><span class="sxs-lookup"><span data-stu-id="fabe7-181">You should also user progress indicators to provide feedback to your users for any long-running processes.</span></span>

> [!NOTE]
> <span data-ttu-id="fabe7-182">Вкладки включены на мобильных устройствах только после того, как приложение будет добавлено в список разрешений на основе ввода группы утверждения.</span><span class="sxs-lookup"><span data-stu-id="fabe7-182">Tabs are enabled on mobile only after the application is added to an allow list, based on the input of the approval team.</span></span> <span data-ttu-id="fabe7-183">Чтобы проверить отзывчивость мобильных устройств, обратитесь к teamsubm@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="fabe7-183">To check mobile responsiveness, reach out to teamsubm@microsoft.com.</span></span>

### <a name="testing-on-mobile-clients"></a><span data-ttu-id="fabe7-184">Тестирование мобильных клиентов</span><span class="sxs-lookup"><span data-stu-id="fabe7-184">Testing on mobile clients</span></span>

<span data-ttu-id="fabe7-185">Необходимо проверить правильность функции вкладки на мобильных устройствах различных размеров и качеств.</span><span class="sxs-lookup"><span data-stu-id="fabe7-185">You need to validate that your tab functions properly on mobile devices of various sizes and qualities.</span></span> <span data-ttu-id="fabe7-186">Для устройств с Android можно использовать [DevTools](~/tabs/how-to/developer-tools.md) для отладки вкладки во время ее работы.</span><span class="sxs-lookup"><span data-stu-id="fabe7-186">For Android devices, you can use the [DevTools](~/tabs/how-to/developer-tools.md) to debug your tab while it is running.</span></span> <span data-ttu-id="fabe7-187">Рекомендуется протестировать как на высокой, так и на низкой скорости, а также на планшете.</span><span class="sxs-lookup"><span data-stu-id="fabe7-187">We recommend that you test on both high and low performing devices, as well as on a tablet.</span></span>

### <a name="distribution"></a><span data-ttu-id="fabe7-188">Распределение</span><span class="sxs-lookup"><span data-stu-id="fabe7-188">Distribution</span></span>

<span data-ttu-id="fabe7-189">Приложения, перечисленные в магазине Teams, должны быть утверждены для использования на мобильных устройствах для правильного функционирования в мобильном клиенте Teams.</span><span class="sxs-lookup"><span data-stu-id="fabe7-189">Apps listed on the Teams store must be approved for mobile use to function properly in the Teams mobile client.</span></span> <span data-ttu-id="fabe7-190">Поведение вкладок зависит от того, утверждено ли ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="fabe7-190">How tabs behave depends on whether your app is approved.</span></span>

#### <a name="channel-and-group-tab-behavior"></a><span data-ttu-id="fabe7-191">Поведение вкладки канала и группы</span><span class="sxs-lookup"><span data-stu-id="fabe7-191">Channel and group tab behavior</span></span>

* <span data-ttu-id="fabe7-192">**Поведение при одобрении:** открывается в мобильном клиенте Teams с помощью конфигурации `contentUrl` приложения.</span><span class="sxs-lookup"><span data-stu-id="fabe7-192">**Behavior when approved**: Opens in the Teams mobile client using your app's `contentUrl` configuration.</span></span>
* <span data-ttu-id="fabe7-193">**Поведение, если** не утверждено. Откроется в браузере по умолчанию устройства с помощью конфигурации приложения (которая также должна быть включена в функцию `websiteUrl` исходный `setSettings()` код).</span><span class="sxs-lookup"><span data-stu-id="fabe7-193">**Behavior when not approved**: Opens in the device’s default browser using your app's `websiteUrl` configuration (which also must be included in your source code's `setSettings()` function).</span></span> <span data-ttu-id="fabe7-194">Тем не менее, пользователи по-прежнему могут загружать  вкладку в мобильном клиенте Teams, выбрав Дополнительные рядом с приложением и выбрав **Open,** что вызывает конфигурацию `contentUrl` приложения.</span><span class="sxs-lookup"><span data-stu-id="fabe7-194">However, users can still load the tab in the Teams mobile client by selecting **More** next to the app and choosing **Open**, which triggers your app’s `contentUrl` configuration.</span></span>

#### <a name="personal-app-behavior"></a><span data-ttu-id="fabe7-195">Поведение личного приложения</span><span class="sxs-lookup"><span data-stu-id="fabe7-195">Personal app behavior</span></span>

* <span data-ttu-id="fabe7-196">**Поведение при одобрении:** Каждая вкладка в личном приложении отображает в мобильном клиенте Teams с помощью соответствующей `contentUrl` конфигурации.</span><span class="sxs-lookup"><span data-stu-id="fabe7-196">**Behavior when approved**: Each tab in the personal app displays in the Teams mobile client using their respective `contentUrl` configuration.</span></span>
* <span data-ttu-id="fabe7-197">**Поведение, если не утверждено.** Личное приложение недоступно в мобильном клиенте Teams.</span><span class="sxs-lookup"><span data-stu-id="fabe7-197">**Behavior when not approved**: The personal app is unavailable in the Teams mobile client.</span></span>

#### <a name="non-teams-store-app-behavior"></a><span data-ttu-id="fabe7-198">Поведение приложений, не в командных магазинах</span><span class="sxs-lookup"><span data-stu-id="fabe7-198">Non-Teams store app behavior</span></span>

<span data-ttu-id="fabe7-199">Если вы перезагружаете приложение или публикацию в каталоге приложений организации, поведение вкладок будет таким же, как и приложения магазина Teams, утвержденные Корпорацией Майкрософт для мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="fabe7-199">If you're sideloading your app or publishing to an org's app catalog, tab behavior will be the same as Teams store apps approved by Microsoft for mobile.</span></span>
