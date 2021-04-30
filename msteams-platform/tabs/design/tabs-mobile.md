---
title: Вкладки на мобильных устройствах
description: Описывает рекомендации по разработке вкладок, которые работают на мобильных устройствах.
ms.topic: conceptual
localization_priority: Normal
keywords: группы разработки рекомендаций по справочной платформе персональных вкладок мобильных приложений
ms.openlocfilehash: b9f09ce2603ee2617b8b93ba2132b900c61f2c31
ms.sourcegitcommit: 1256639fa424e3833b44207ce847a245824d48e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/29/2021
ms.locfileid: "52088761"
---
# <a name="tabs-on-mobile"></a><span data-ttu-id="6acd0-104">Вкладки на мобильных устройствах</span><span class="sxs-lookup"><span data-stu-id="6acd0-104">Tabs on mobile</span></span>

<span data-ttu-id="6acd0-105">Вы можете включить вкладки в Teams каналах, чатах и личных приложениях.</span><span class="sxs-lookup"><span data-stu-id="6acd0-105">You can include tabs in Teams mobile channels, chats, and personal apps.</span></span>

## <a name="accessing-personal-tabs"></a><span data-ttu-id="6acd0-106">Доступ к личным вкладкам</span><span class="sxs-lookup"><span data-stu-id="6acd0-106">Accessing personal tabs</span></span>

<span data-ttu-id="6acd0-107">Вы можете получить доступ к личным вкладкам в ящике приложения.</span><span class="sxs-lookup"><span data-stu-id="6acd0-107">You can access personal tabs in the app drawer.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-app-drawer.png" alt-text="Иллюстрация, показывающая Teams мобильного приложения." border="false":::

## <a name="accessing-channel-tabs"></a><span data-ttu-id="6acd0-109">Доступ к вкладке канала</span><span class="sxs-lookup"><span data-stu-id="6acd0-109">Accessing channel tabs</span></span>

<span data-ttu-id="6acd0-110">Вы можете получить доступ к вкладке канала и группы, выбрав кнопку **More** в канале или в чате, в котором они были добавлены.</span><span class="sxs-lookup"><span data-stu-id="6acd0-110">You can access channel and group tabs by selecting the **More** button in the channel or chat in which they've been added.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab.png" alt-text="Иллюстрация, показывающая вкладку Teams мобильной связи." border="false":::

## <a name="design-considerations"></a><span data-ttu-id="6acd0-112">Особенности дизайна</span><span class="sxs-lookup"><span data-stu-id="6acd0-112">Design considerations</span></span>

<span data-ttu-id="6acd0-113">Наша мобильная платформа позволяет приложениям быть иммерсивным опытом с контентом приложения, за исключением основного Teams навигации.</span><span class="sxs-lookup"><span data-stu-id="6acd0-113">Our mobile platform allows apps to be an immersive experience with the app content taking up all of the screen apart from main Teams navigation.</span></span> <span data-ttu-id="6acd0-114">Чтобы создать иммерсивный опыт, который соответствует Teams, следуйте этим рекомендациям.</span><span class="sxs-lookup"><span data-stu-id="6acd0-114">To create an immersive experience that fits with Teams, follow these guidelines.</span></span>

### <a name="responsive-design"></a><span data-ttu-id="6acd0-115">Адаптивный дизайн</span><span class="sxs-lookup"><span data-stu-id="6acd0-115">Responsive design</span></span>

<span data-ttu-id="6acd0-116">Так как вкладка может быть открыта на устройствах с широким диапазоном размеров экрана, она должна следовать принципам [гибкого проектирования.](https://www.w3schools.com/html/html_responsive.asp)</span><span class="sxs-lookup"><span data-stu-id="6acd0-116">Because your tab can be opened on devices with a wide range of screen sizes, it needs to follow [responsive design](https://www.w3schools.com/html/html_responsive.asp) principles.</span></span> <span data-ttu-id="6acd0-117">Все ключевые конструкции должны быть доступны на мобильных устройствах, и представления не должны искажаться.</span><span class="sxs-lookup"><span data-stu-id="6acd0-117">All of the key constructs should be accessible on mobile devices, and the views should not be distorted.</span></span> <span data-ttu-id="6acd0-118">Убедитесь, что при загрузке вкладки на мобильном устройстве все кнопки и ссылки легко доступны с помощью навигации на основе пальцев.</span><span class="sxs-lookup"><span data-stu-id="6acd0-118">Ensure that when your tab is loaded on a mobile device, all buttons and links are easily accessible using finger-based navigation.</span></span>

### <a name="layouts"></a><span data-ttu-id="6acd0-119">макеты;</span><span class="sxs-lookup"><span data-stu-id="6acd0-119">Layouts</span></span>

<span data-ttu-id="6acd0-120">Важно выбрать правильный макет вкладки.</span><span class="sxs-lookup"><span data-stu-id="6acd0-120">Choosing the correct layout for your tab is important.</span></span> <span data-ttu-id="6acd0-121">Необходимо рассмотреть тип представляемой информации и выбрать макет, который организует ее для легкого потребления.</span><span class="sxs-lookup"><span data-stu-id="6acd0-121">You should consider the kind of information you're presenting, and choose a layout that organizes it for easy consumption.</span></span> <span data-ttu-id="6acd0-122">Ниже описаны некоторые возможные варианты.</span><span class="sxs-lookup"><span data-stu-id="6acd0-122">Some potential options are outlined below.</span></span>

#### <a name="single-canvas"></a><span data-ttu-id="6acd0-123">Одно полотно</span><span class="sxs-lookup"><span data-stu-id="6acd0-123">Single canvas</span></span>

<span data-ttu-id="6acd0-124">Это одна большая область, в которой делается работа.</span><span class="sxs-lookup"><span data-stu-id="6acd0-124">This is one large area where work gets done.</span></span> <span data-ttu-id="6acd0-125">Приложение Teams Вики следует этому шаблону.</span><span class="sxs-lookup"><span data-stu-id="6acd0-125">The Teams Wiki app follows this pattern.</span></span> <span data-ttu-id="6acd0-126">Если у вас есть приложение, которое не разделяет контент на более мелкие компоненты, это будет подходящим.</span><span class="sxs-lookup"><span data-stu-id="6acd0-126">If you have an app that doesn’t separate content into smaller components this would be a good fit.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-single-canvas.png" alt-text="Иллюстрация, показывающая Teams одной вкладке холста для мобильных устройств." border="false":::

#### <a name="list"></a><span data-ttu-id="6acd0-128">List</span><span class="sxs-lookup"><span data-stu-id="6acd0-128">List</span></span>

<span data-ttu-id="6acd0-129">Списки отлично подходит для сортировки и фильтрации больших объемов данных и отлично подходит для хранения наиболее важных вещей в верхней части.</span><span class="sxs-lookup"><span data-stu-id="6acd0-129">Lists are great for sorting and filtering large quantities of data and are great at keeping the most important things at the top.</span></span> <span data-ttu-id="6acd0-130">Полезно использовать сортируемые столбцы.</span><span class="sxs-lookup"><span data-stu-id="6acd0-130">It is helpful to use sortable columns.</span></span> <span data-ttu-id="6acd0-131">Действия могут быть добавлены к каждому элементу списка в меню ellipsis.</span><span class="sxs-lookup"><span data-stu-id="6acd0-131">Actions can be added to each list item under the ellipsis menu.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-list.png" alt-text="Иллюстрация, показывающая вкладку Teams списка мобильных устройств." border="false":::

#### <a name="grid"></a><span data-ttu-id="6acd0-133">Grid</span><span class="sxs-lookup"><span data-stu-id="6acd0-133">Grid</span></span>

<span data-ttu-id="6acd0-134">Сетки полезны для демонстрации элементов с высокой наглядности.</span><span class="sxs-lookup"><span data-stu-id="6acd0-134">Grids are useful for showing elements which are highly visual.</span></span> <span data-ttu-id="6acd0-135">Это помогает включить фильтр или управление поиском в верхней части.</span><span class="sxs-lookup"><span data-stu-id="6acd0-135">It helps to include a filter or search control at the top.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-grid.png" alt-text="Иллюстрация, показывающая Teams вкладку с макетом сетки." border="false":::

### <a name="tabs-with-bots-on-mobile"></a><span data-ttu-id="6acd0-137">Вкладки с ботами на мобильных устройствах</span><span class="sxs-lookup"><span data-stu-id="6acd0-137">Tabs with bots on mobile</span></span>

<span data-ttu-id="6acd0-138">Ниже приводится личный пример приложения с вкладками и ботом.</span><span class="sxs-lookup"><span data-stu-id="6acd0-138">The following example is a personal app that has tabs and a bot.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-with-bot.png" alt-text="На рисунке показывая, Teams мобильное приложение с вкладками и ботом." border="false":::

## <a name="ui-components"></a><span data-ttu-id="6acd0-140">Компоненты пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="6acd0-140">UI components</span></span>

### <a name="color-palettes"></a><span data-ttu-id="6acd0-141">Цветовые палитры</span><span class="sxs-lookup"><span data-stu-id="6acd0-141">Color palettes</span></span>

<span data-ttu-id="6acd0-142">Использование нашей утвержденной нейтральной палитры фонов, уведомлений, текста и кнопок поможет приложению чувствовать себя как дома в Teams.</span><span class="sxs-lookup"><span data-stu-id="6acd0-142">Using our approved neutral palette for backgrounds, notifications, text, and buttons will help your app feel more at home in Teams.</span></span> <span data-ttu-id="6acd0-143">Так Teams мобильный имеет две цветовые темы (светлый и темный), это хорошая идея, чтобы убедиться, что ваше приложение выглядит отлично в обоих.</span><span class="sxs-lookup"><span data-stu-id="6acd0-143">Since Teams mobile has two colour themes (light and dark), it’s a good idea to make sure your app looks great in both.</span></span>

#### <a name="light-color"></a><span data-ttu-id="6acd0-144">Светлый цвет</span><span class="sxs-lookup"><span data-stu-id="6acd0-144">Light color</span></span>

![светлая цветовая палитра](../../assets/images/light-color.png)

#### <a name="dark-color"></a><span data-ttu-id="6acd0-146">Темный цвет</span><span class="sxs-lookup"><span data-stu-id="6acd0-146">Dark color</span></span>

![темная цветовая палитра](../../assets/images/dark-color.png)

### <a name="buttons-and-controls"></a><span data-ttu-id="6acd0-148">Кнопки и элементы управления</span><span class="sxs-lookup"><span data-stu-id="6acd0-148">Buttons and controls</span></span>

<span data-ttu-id="6acd0-149">Стиль кнопок позволяет сообщить, какие действия они запускают.</span><span class="sxs-lookup"><span data-stu-id="6acd0-149">The way buttons are styled helps communicate what kind of action they trigger.</span></span> <span data-ttu-id="6acd0-150">Мы поддерживаем широкий диапазон кнопок, которые отформатированы, чтобы показать различные уровни акцента.</span><span class="sxs-lookup"><span data-stu-id="6acd0-150">We maintain a wide range of buttons that are formatted to show different levels of emphasis.</span></span> <span data-ttu-id="6acd0-151">Кнопки могут иметь текст, значок или сочетание текста и значка.</span><span class="sxs-lookup"><span data-stu-id="6acd0-151">Buttons can have text, an icon, or a combination of text and an icon.</span></span> <span data-ttu-id="6acd0-152">Чтобы общаться на разных уровнях в иерархии, мы разработали основные и вторичные кнопки в каждой категории.</span><span class="sxs-lookup"><span data-stu-id="6acd0-152">To communicate different levels in a hierarchy, we designed primary and secondary buttons within each category.</span></span>

#### <a name="buttons"></a><span data-ttu-id="6acd0-153">Кнопки</span><span class="sxs-lookup"><span data-stu-id="6acd0-153">Buttons</span></span>

<span data-ttu-id="6acd0-154">Основные и вторичные кнопки.</span><span class="sxs-lookup"><span data-stu-id="6acd0-154">Primary and secondary buttons.</span></span>

![изображение кнопок](../../assets/images/buttons.png)

#### <a name="selection-controls"></a><span data-ttu-id="6acd0-156">Элементы управления выбором</span><span class="sxs-lookup"><span data-stu-id="6acd0-156">Selection controls</span></span>

<span data-ttu-id="6acd0-157">Кнопки радио, почтовые ящики и очки.</span><span class="sxs-lookup"><span data-stu-id="6acd0-157">Radio buttons, checkboxes, and toggles.</span></span>

![элементы управления выбором](../../assets/images/selection-controls.png)

#### <a name="chiclets-and-pills"></a><span data-ttu-id="6acd0-159">Шиклеты и таблетки</span><span class="sxs-lookup"><span data-stu-id="6acd0-159">Chiclets and pills</span></span>

![шиклеты и таблетки](../../assets/images/chiclets-and-pills.png)

### <a name="typography"></a><span data-ttu-id="6acd0-161">Шрифтовое оформление</span><span class="sxs-lookup"><span data-stu-id="6acd0-161">Typography</span></span>

<span data-ttu-id="6acd0-162">Типография должна быть четкой и целенаправленной.</span><span class="sxs-lookup"><span data-stu-id="6acd0-162">Typography should be clear and purposeful.</span></span> <span data-ttu-id="6acd0-163">Подчеркивать важные сведения и избегать использования нескольких шрифтов и размеров для уменьшения путаницы.</span><span class="sxs-lookup"><span data-stu-id="6acd0-163">Emphasize important information and avoid using multiple fonts and sizes to reduce confusion.</span></span> <span data-ttu-id="6acd0-164">Рекомендуется использовать пример предложения и избегать использования всех колпачок для локализации и разнонабности.</span><span class="sxs-lookup"><span data-stu-id="6acd0-164">We recommend using sentence case and avoiding the usage of all caps for localization and legibility.</span></span>

![мобильный опечаток](../../assets/images/mobile-typography.png)

### <a name="fields-and-flyouts"></a><span data-ttu-id="6acd0-166">Поля и вылеты</span><span class="sxs-lookup"><span data-stu-id="6acd0-166">Fields and flyouts</span></span>

<span data-ttu-id="6acd0-167">Поля — это области, в которых пользователи могут вводить текст.</span><span class="sxs-lookup"><span data-stu-id="6acd0-167">Fields are areas where users can input text.</span></span> <span data-ttu-id="6acd0-168">Вылеты более легкие, чем диалоги, и отображаются на верхней области.</span><span class="sxs-lookup"><span data-stu-id="6acd0-168">Flyouts are more lightweight than dialogs and appear from the top pane.</span></span>

#### <a name="list-controls"></a><span data-ttu-id="6acd0-169">Список элементов управления</span><span class="sxs-lookup"><span data-stu-id="6acd0-169">List controls</span></span>

![элементы управления списками мобильных устройств](../../assets/images/mobile-list-controls.png)

#### <a name="field-controls"></a><span data-ttu-id="6acd0-171">Элементы управления полями</span><span class="sxs-lookup"><span data-stu-id="6acd0-171">Field controls</span></span>

![элементы управления мобильными полями](../../assets/images/mobile-field-controls.png)

## <a name="developer-considerations"></a><span data-ttu-id="6acd0-173">Соображения разработчика</span><span class="sxs-lookup"><span data-stu-id="6acd0-173">Developer considerations</span></span>

<span data-ttu-id="6acd0-174">При создании приложения, включаемого в вкладку, необходимо учитывать (и тестировать) функции вкладки как на Android, так и на Microsoft Teams iOS.</span><span class="sxs-lookup"><span data-stu-id="6acd0-174">When you're building an app that includes a tab, you need to consider (and test) how your tab will function on both the Android and iOS Microsoft Teams clients.</span></span> <span data-ttu-id="6acd0-175">В разделах ниже описаны некоторые ключевые сценарии, которые необходимо рассмотреть.</span><span class="sxs-lookup"><span data-stu-id="6acd0-175">The sections below outline some of the key scenarios you need to consider.</span></span>

### <a name="authentication"></a><span data-ttu-id="6acd0-176">Проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="6acd0-176">Authentication</span></span>

<span data-ttu-id="6acd0-177">Для проверки подлинности для мобильных клиентов необходимо обновить Teams JavaScript SDK по крайней мере до версии 1.4.1.</span><span class="sxs-lookup"><span data-stu-id="6acd0-177">For authentication to work on mobile clients, you must upgrade you Teams JavaScript SDK to at least version 1.4.1.</span></span>

### <a name="low-bandwidth-and-intermittent-connections"></a><span data-ttu-id="6acd0-178">Низкая пропускная способность и периодические подключения</span><span class="sxs-lookup"><span data-stu-id="6acd0-178">Low bandwidth and intermittent connections</span></span>

<span data-ttu-id="6acd0-179">Мобильные клиенты регулярно должны работать с низкой пропускной способностью и периодическими подключениями.</span><span class="sxs-lookup"><span data-stu-id="6acd0-179">Mobile clients regularly need to function with low bandwidth and intermittent connections.</span></span> <span data-ttu-id="6acd0-180">Ваше приложение должно надлежащим образом обрабатывать любые периоды времени, предоставляя пользователю контекстное сообщение.</span><span class="sxs-lookup"><span data-stu-id="6acd0-180">Your app should handle any timeouts appropriately by providing a contextual message to the user.</span></span> <span data-ttu-id="6acd0-181">Кроме того, необходимо использовать индикаторы прогресса пользователей, чтобы предоставить пользователям обратную связь для любых длительных процессов.</span><span class="sxs-lookup"><span data-stu-id="6acd0-181">You should also user progress indicators to provide feedback to your users for any long-running processes.</span></span>

> [!NOTE]
> <span data-ttu-id="6acd0-182">Вкладки включены на мобильных устройствах только после того, как приложение будет добавлено в список разрешений на основе ввода группы утверждения.</span><span class="sxs-lookup"><span data-stu-id="6acd0-182">Tabs are enabled on mobile only after the application is added to an allow list, based on the input of the approval team.</span></span> <span data-ttu-id="6acd0-183">Чтобы проверить отзывчивость мобильных устройств, обратитесь к teamsubm@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="6acd0-183">To check mobile responsiveness, reach out to teamsubm@microsoft.com.</span></span>

### <a name="testing-on-mobile-clients"></a><span data-ttu-id="6acd0-184">Тестирование мобильных клиентов</span><span class="sxs-lookup"><span data-stu-id="6acd0-184">Testing on mobile clients</span></span>

<span data-ttu-id="6acd0-185">Необходимо проверить правильность функции вкладки на мобильных устройствах различных размеров и качеств.</span><span class="sxs-lookup"><span data-stu-id="6acd0-185">You need to validate that your tab functions properly on mobile devices of various sizes and qualities.</span></span> <span data-ttu-id="6acd0-186">Для устройств с Android можно использовать [DevTools](~/tabs/how-to/developer-tools.md) для отладки вкладки во время ее работы.</span><span class="sxs-lookup"><span data-stu-id="6acd0-186">For Android devices, you can use the [DevTools](~/tabs/how-to/developer-tools.md) to debug your tab while it is running.</span></span> <span data-ttu-id="6acd0-187">Рекомендуется протестировать как на высокой, так и на низкой производительности устройств, включая планшет.</span><span class="sxs-lookup"><span data-stu-id="6acd0-187">We recommend that you test on both high- and low-performance devices, including a tablet.</span></span>

### <a name="distribution"></a><span data-ttu-id="6acd0-188">Распределение</span><span class="sxs-lookup"><span data-stu-id="6acd0-188">Distribution</span></span>

<span data-ttu-id="6acd0-189">Приложения, перечисленные в Teams магазине, должны быть утверждены для использования мобильных устройств для правильной работы в Teams клиенте.</span><span class="sxs-lookup"><span data-stu-id="6acd0-189">Apps listed on the Teams store must be approved for mobile use to function properly in the Teams mobile client.</span></span> <span data-ttu-id="6acd0-190">Доступность и поведение вкладок зависят от того, утверждено ли ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="6acd0-190">Tab availability and behavior depends on whether your app is approved.</span></span>

#### <a name="apps-on-teams-store-approved-for-mobile"></a><span data-ttu-id="6acd0-191">Приложения в Teams магазине, утвержденные для мобильных устройств</span><span class="sxs-lookup"><span data-stu-id="6acd0-191">Apps on Teams store approved for mobile</span></span>

<span data-ttu-id="6acd0-192">В следующей таблице описывается доступность вкладок и поведение, когда приложение перечислены в Teams и утверждены для использования в мобильных устройствах.</span><span class="sxs-lookup"><span data-stu-id="6acd0-192">The following table describes tab availability and behavior when the app is listed on the Teams store and approved for mobile use.</span></span>

|<span data-ttu-id="6acd0-193">Возможность</span><span class="sxs-lookup"><span data-stu-id="6acd0-193">Capability</span></span>   |<span data-ttu-id="6acd0-194">Доступность мобильных устройств?</span><span class="sxs-lookup"><span data-stu-id="6acd0-194">Mobile availability?</span></span>   |<span data-ttu-id="6acd0-195">Поведение мобильных устройств</span><span class="sxs-lookup"><span data-stu-id="6acd0-195">Mobile behavior</span></span>|
|----------|-----------|------------|
|<span data-ttu-id="6acd0-196">Канал</span><span class="sxs-lookup"><span data-stu-id="6acd0-196">Channel</span></span> <br /> <span data-ttu-id="6acd0-197">и вкладка группы</span><span class="sxs-lookup"><span data-stu-id="6acd0-197">and group tab</span></span>|<span data-ttu-id="6acd0-198">Да</span><span class="sxs-lookup"><span data-stu-id="6acd0-198">Yes</span></span>|<span data-ttu-id="6acd0-199">Вкладка открывается в Teams клиенте с помощью конфигурации `contentUrl` приложения.</span><span class="sxs-lookup"><span data-stu-id="6acd0-199">Tab opens in the Teams mobile client using your app's `contentUrl` configuration.</span></span>|
|<span data-ttu-id="6acd0-200">Личное приложение</span><span class="sxs-lookup"><span data-stu-id="6acd0-200">Personal app</span></span>|<span data-ttu-id="6acd0-201">Да</span><span class="sxs-lookup"><span data-stu-id="6acd0-201">Yes</span></span>|<span data-ttu-id="6acd0-202">Каждая вкладка в личной вкладке приложения открывается в мобильном клиенте Teams с помощью соответствующей `contentUrl` конфигурации.</span><span class="sxs-lookup"><span data-stu-id="6acd0-202">Each tab in the personal app tab opens in the Teams mobile client using its respective `contentUrl` configuration.</span></span>|

#### <a name="apps-on-teams-store-not-approved-for-mobile"></a><span data-ttu-id="6acd0-203">Приложения в Teams магазине не утверждены для мобильных устройств</span><span class="sxs-lookup"><span data-stu-id="6acd0-203">Apps on Teams store not approved for mobile</span></span>

<span data-ttu-id="6acd0-204">В следующей таблице описывается доступность и поведение вкладок, когда приложение перечислены в Teams, но не утверждено для мобильного использования.</span><span class="sxs-lookup"><span data-stu-id="6acd0-204">The following table describes tab availability and behavior when the app is listed on the Teams store but not approved for mobile use.</span></span>

|<span data-ttu-id="6acd0-205">Возможность</span><span class="sxs-lookup"><span data-stu-id="6acd0-205">Capability</span></span>   |<span data-ttu-id="6acd0-206">Доступность мобильных устройств?</span><span class="sxs-lookup"><span data-stu-id="6acd0-206">Mobile availability?</span></span>|<span data-ttu-id="6acd0-207">Поведение мобильных устройств</span><span class="sxs-lookup"><span data-stu-id="6acd0-207">Mobile behavior</span></span>|
|----------|-----------|------------|
|<span data-ttu-id="6acd0-208">Вкладка каналов и групп</span><span class="sxs-lookup"><span data-stu-id="6acd0-208">Channel and group tab</span></span>|<span data-ttu-id="6acd0-209">Да</span><span class="sxs-lookup"><span data-stu-id="6acd0-209">Yes</span></span>|<span data-ttu-id="6acd0-210">Вкладка открывается в браузере устройства по умолчанию, а не в мобильном клиенте Teams с помощью конфигурации приложения (которая также должна быть включена в функцию источника `websiteUrl` `setSettings()` [кода).](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest#functions)</span><span class="sxs-lookup"><span data-stu-id="6acd0-210">Tab opens in the device's default browser instead of the Teams mobile client using your app's `websiteUrl` configuration (which also must be included in your source code's `setSettings()` [function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest#functions)).</span></span> <span data-ttu-id="6acd0-211">Однако пользователи по-прежнему могут просматривать вкладку в Teams  мобильном клиенте, выбрав Далее рядом с приложением и выбрав **Open,** который запускает конфигурацию `contentUrl` вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="6acd0-211">However, users can still view the tab in the Teams mobile client by selecting **More** next to the app and choosing **Open**, which triggers your app’s `contentUrl` configuration.</span></span>|
|<span data-ttu-id="6acd0-212">Личное приложение</span><span class="sxs-lookup"><span data-stu-id="6acd0-212">Personal app</span></span>|<span data-ttu-id="6acd0-213">НЕТ</span><span class="sxs-lookup"><span data-stu-id="6acd0-213">No</span></span>|<span data-ttu-id="6acd0-214">Неприменимо</span><span class="sxs-lookup"><span data-stu-id="6acd0-214">Not applicable</span></span>|

#### <a name="apps-not-on-teams-store"></a><span data-ttu-id="6acd0-215">Приложения, не Teams магазине</span><span class="sxs-lookup"><span data-stu-id="6acd0-215">Apps not on Teams store</span></span>

<span data-ttu-id="6acd0-216">Если вы перезагружаете приложение или публикацию в каталоге приложений организации, поведение вкладок будет таким же, как и Teams приложений, утвержденных Корпорацией Майкрософт для мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="6acd0-216">If you're sideloading your app or publishing to an org's app catalog, tab behavior will be the same as Teams store apps approved by Microsoft for mobile.</span></span>
