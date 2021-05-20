---
title: Вкладки на мобильных устройствах
description: Описывает руководящие принципы проектирования вкладок, которые работают на мобильных устройствах.
ms.topic: conceptual
localization_priority: Normal
keywords: команды проектируют руководящие принципы справочной платформы персональных приложений мобильных вкладок
ms.openlocfilehash: 853ab2c52edd1f4faedcc92e6f0e8d0821b580c7
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566700"
---
# <a name="tabs-on-mobile"></a><span data-ttu-id="68d29-104">Вкладки на мобильных устройствах</span><span class="sxs-lookup"><span data-stu-id="68d29-104">Tabs on mobile</span></span>

<span data-ttu-id="68d29-105">Вы можете включить вкладки в Teams мобильных каналов, чатов и личных приложений.</span><span class="sxs-lookup"><span data-stu-id="68d29-105">You can include tabs in Teams mobile channels, chats, and personal apps.</span></span>

## <a name="accessing-personal-tabs"></a><span data-ttu-id="68d29-106">Доступ к личным вкладок</span><span class="sxs-lookup"><span data-stu-id="68d29-106">Accessing personal tabs</span></span>

<span data-ttu-id="68d29-107">Вы можете получить доступ к личным вкладок в ящике приложения.</span><span class="sxs-lookup"><span data-stu-id="68d29-107">You can access personal tabs in the app drawer.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-app-drawer.png" alt-text="Иллюстрация, показывающая Teams ящик мобильного приложения." border="false":::

## <a name="accessing-channel-tabs"></a><span data-ttu-id="68d29-109">Доступ к вкладок канала</span><span class="sxs-lookup"><span data-stu-id="68d29-109">Accessing channel tabs</span></span>

<span data-ttu-id="68d29-110">Вы можете получить доступ к вкладок канала и группы, **выбрав кнопку More** в канале или чате, в котором они были добавлены.</span><span class="sxs-lookup"><span data-stu-id="68d29-110">You can access channel and group tabs by selecting the **More** button in the channel or chat in which they've been added.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab.png" alt-text="Иллюстрация, показывающая Teams мобильную вкладку." border="false":::

## <a name="design-considerations"></a><span data-ttu-id="68d29-112">Особенности дизайна</span><span class="sxs-lookup"><span data-stu-id="68d29-112">Design considerations</span></span>

<span data-ttu-id="68d29-113">Наша мобильная платформа позволяет приложениям быть захватывающим опытом с содержанием приложения, принимая все экраны, кроме основных Teams навигации.</span><span class="sxs-lookup"><span data-stu-id="68d29-113">Our mobile platform allows apps to be an immersive experience with the app content taking up all of the screen apart from main Teams navigation.</span></span> <span data-ttu-id="68d29-114">Чтобы создать захватывающий опыт, который вписывается в Teams, следуйте этим рекомендациям.</span><span class="sxs-lookup"><span data-stu-id="68d29-114">To create an immersive experience that fits with Teams, follow these guidelines.</span></span>

### <a name="responsive-design"></a><span data-ttu-id="68d29-115">Адаптивный дизайн</span><span class="sxs-lookup"><span data-stu-id="68d29-115">Responsive design</span></span>

<span data-ttu-id="68d29-116">Поскольку вкладка может быть открыта на устройствах с широким диапазоном размеров экрана, она должна следовать [принципам адаптивного](https://www.w3schools.com/html/html_responsive.asp) дизайна.</span><span class="sxs-lookup"><span data-stu-id="68d29-116">Because your tab can be opened on devices with a wide range of screen sizes, it needs to follow [responsive design](https://www.w3schools.com/html/html_responsive.asp) principles.</span></span> <span data-ttu-id="68d29-117">Все ключевые конструкции должны быть доступны на мобильных устройствах, и представления не должны быть искажены.</span><span class="sxs-lookup"><span data-stu-id="68d29-117">All of the key constructs should be accessible on mobile devices, and the views should not be distorted.</span></span> <span data-ttu-id="68d29-118">Убедитесь, что при загрузке вкладки на мобильное устройство все кнопки и ссылки легко доступны с помощью навигации на основе пальцев.</span><span class="sxs-lookup"><span data-stu-id="68d29-118">Ensure that when your tab is loaded on a mobile device, all buttons and links are easily accessible using finger-based navigation.</span></span>

### <a name="layouts"></a><span data-ttu-id="68d29-119">макеты;</span><span class="sxs-lookup"><span data-stu-id="68d29-119">Layouts</span></span>

<span data-ttu-id="68d29-120">Выбор правильного макета для вкладки имеет важное значение.</span><span class="sxs-lookup"><span data-stu-id="68d29-120">Choosing the correct layout for your tab is important.</span></span> <span data-ttu-id="68d29-121">Вы должны рассмотреть вид информации, которую вы представляете, и выбрать макет, который организует его для легкого потребления.</span><span class="sxs-lookup"><span data-stu-id="68d29-121">You should consider the kind of information you're presenting, and choose a layout that organizes it for easy consumption.</span></span> <span data-ttu-id="68d29-122">Ниже изложены некоторые потенциальные варианты.</span><span class="sxs-lookup"><span data-stu-id="68d29-122">Some potential options are outlined below.</span></span>

#### <a name="single-canvas"></a><span data-ttu-id="68d29-123">Одно холст</span><span class="sxs-lookup"><span data-stu-id="68d29-123">Single canvas</span></span>

<span data-ttu-id="68d29-124">Это одна большая область, где работа делается.</span><span class="sxs-lookup"><span data-stu-id="68d29-124">This is one large area where work gets done.</span></span> <span data-ttu-id="68d29-125">Приложение Teams Вики следует этой схеме.</span><span class="sxs-lookup"><span data-stu-id="68d29-125">The Teams Wiki app follows this pattern.</span></span> <span data-ttu-id="68d29-126">Если у вас есть приложение, которое не разделяет содержимое на более мелкие компоненты, это было бы хорошо подходит.</span><span class="sxs-lookup"><span data-stu-id="68d29-126">If you have an app that doesn’t separate content into smaller components this would be a good fit.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-single-canvas.png" alt-text="Иллюстрация, показывающая Teams мобильную вкладку с одним холстом." border="false":::

#### <a name="list"></a><span data-ttu-id="68d29-128">List</span><span class="sxs-lookup"><span data-stu-id="68d29-128">List</span></span>

<span data-ttu-id="68d29-129">Списки отлично подованы для сортировки и фильтрации больших объемов данных и отлично подхвеки находятся на самом верху.</span><span class="sxs-lookup"><span data-stu-id="68d29-129">Lists are great for sorting and filtering large quantities of data and are great at keeping the most important things at the top.</span></span> <span data-ttu-id="68d29-130">Полезно использовать сортируемые столбцы.</span><span class="sxs-lookup"><span data-stu-id="68d29-130">It is helpful to use sortable columns.</span></span> <span data-ttu-id="68d29-131">Действия могут быть добавлены к каждому пункту списка в меню ellipsis.</span><span class="sxs-lookup"><span data-stu-id="68d29-131">Actions can be added to each list item under the ellipsis menu.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-list.png" alt-text="Иллюстрация, показывающая Teams мобильный список вкладок." border="false":::

#### <a name="grid"></a><span data-ttu-id="68d29-133">сетка</span><span class="sxs-lookup"><span data-stu-id="68d29-133">Grid</span></span>

<span data-ttu-id="68d29-134">Сетки полезны для отображения элементов, которые являются весьма визуальными.</span><span class="sxs-lookup"><span data-stu-id="68d29-134">Grids are useful for showing elements which are highly visual.</span></span> <span data-ttu-id="68d29-135">Это помогает включить фильтр или контроль поиска в верхней части.</span><span class="sxs-lookup"><span data-stu-id="68d29-135">It helps to include a filter or search control at the top.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-grid.png" alt-text="Иллюстрация, показывающая Teams мобильную вкладку с макетом сетки." border="false":::

### <a name="tabs-with-bots-on-mobile"></a><span data-ttu-id="68d29-137">Вкладки с ботами на мобильном телефоне</span><span class="sxs-lookup"><span data-stu-id="68d29-137">Tabs with bots on mobile</span></span>

<span data-ttu-id="68d29-138">Следующим примером является личное приложение, которое имеет вкладки и бот:</span><span class="sxs-lookup"><span data-stu-id="68d29-138">The following example is a personal app that has tabs and a bot:</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-with-bot.png" alt-text="Иллюстрация, показывающая, Teams приложение, которое имеет вкладки и бота." border="false":::

## <a name="ui-components"></a><span data-ttu-id="68d29-140">Компоненты пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="68d29-140">UI components</span></span>

### <a name="color-palettes"></a><span data-ttu-id="68d29-141">Цветовые палитры</span><span class="sxs-lookup"><span data-stu-id="68d29-141">Color palettes</span></span>

<span data-ttu-id="68d29-142">Использование утвержденной нейтральной палитры для фонов, уведомлений, текста и кнопок поможет вашему приложению чувствовать себя как дома в Teams.</span><span class="sxs-lookup"><span data-stu-id="68d29-142">Using our approved neutral palette for backgrounds, notifications, text, and buttons will help your app feel more at home in Teams.</span></span> <span data-ttu-id="68d29-143">Так Teams мобильный имеет две цветные темы (светлые и темные), это хорошая идея, чтобы убедиться, что ваше приложение выглядит великолепно в обоих.</span><span class="sxs-lookup"><span data-stu-id="68d29-143">Since Teams mobile has two colour themes (light and dark), it’s a good idea to make sure your app looks great in both.</span></span>

#### <a name="light-color"></a><span data-ttu-id="68d29-144">Светлый цвет</span><span class="sxs-lookup"><span data-stu-id="68d29-144">Light color</span></span>

![светлая цветовая палитра](../../assets/images/light-color.png)

#### <a name="dark-color"></a><span data-ttu-id="68d29-146">Темный цвет</span><span class="sxs-lookup"><span data-stu-id="68d29-146">Dark color</span></span>

![темная цветовая палитра](../../assets/images/dark-color.png)

### <a name="buttons-and-controls"></a><span data-ttu-id="68d29-148">Кнопки и элементы управления</span><span class="sxs-lookup"><span data-stu-id="68d29-148">Buttons and controls</span></span>

<span data-ttu-id="68d29-149">Способ стиль кнопок помогает сообщить, какие действия они вызывают.</span><span class="sxs-lookup"><span data-stu-id="68d29-149">The way buttons are styled helps communicate what kind of action they trigger.</span></span> <span data-ttu-id="68d29-150">Мы поддерживаем широкий спектр кнопок, которые отформатированы, чтобы показать различные уровни внимания.</span><span class="sxs-lookup"><span data-stu-id="68d29-150">We maintain a wide range of buttons that are formatted to show different levels of emphasis.</span></span> <span data-ttu-id="68d29-151">Кнопки могут иметь текст, значок или комбинацию текста и значка.</span><span class="sxs-lookup"><span data-stu-id="68d29-151">Buttons can have text, an icon, or a combination of text and an icon.</span></span> <span data-ttu-id="68d29-152">Для передачи различных уровней в иерархии мы разработали основные и вторичные кнопки в каждой категории.</span><span class="sxs-lookup"><span data-stu-id="68d29-152">To communicate different levels in a hierarchy, we designed primary and secondary buttons within each category.</span></span>

#### <a name="buttons"></a><span data-ttu-id="68d29-153">Кнопки</span><span class="sxs-lookup"><span data-stu-id="68d29-153">Buttons</span></span>

<span data-ttu-id="68d29-154">Первичные и вторичные кнопки.</span><span class="sxs-lookup"><span data-stu-id="68d29-154">Primary and secondary buttons.</span></span>

![кнопки изображения](../../assets/images/buttons.png)

#### <a name="selection-controls"></a><span data-ttu-id="68d29-156">Элементы управления выбором</span><span class="sxs-lookup"><span data-stu-id="68d29-156">Selection controls</span></span>

<span data-ttu-id="68d29-157">Кнопки радио, флажки и переключатели.</span><span class="sxs-lookup"><span data-stu-id="68d29-157">Radio buttons, checkboxes, and toggles.</span></span>

![контроль отбора](../../assets/images/selection-controls.png)

#### <a name="chiclets-and-pills"></a><span data-ttu-id="68d29-159">Чиклеты и таблетки</span><span class="sxs-lookup"><span data-stu-id="68d29-159">Chiclets and pills</span></span>

![шиклеты и таблетки](../../assets/images/chiclets-and-pills.png)

### <a name="typography"></a><span data-ttu-id="68d29-161">Шрифтовое оформление</span><span class="sxs-lookup"><span data-stu-id="68d29-161">Typography</span></span>

<span data-ttu-id="68d29-162">Типография должна быть четкой и целенаправленной.</span><span class="sxs-lookup"><span data-stu-id="68d29-162">Typography should be clear and purposeful.</span></span> <span data-ttu-id="68d29-163">Подчеркните важную информацию и избегайте использования нескольких шрифтов и размеров для уменьшения путаницы.</span><span class="sxs-lookup"><span data-stu-id="68d29-163">Emphasize important information and avoid using multiple fonts and sizes to reduce confusion.</span></span> <span data-ttu-id="68d29-164">Мы рекомендуем использовать предложение случае и избежать использования всех шапки для локализации и разборчивости.</span><span class="sxs-lookup"><span data-stu-id="68d29-164">We recommend using sentence case and avoiding the usage of all caps for localization and legibility.</span></span>

![мобильный типограф](../../assets/images/mobile-typography.png)

### <a name="fields-and-flyouts"></a><span data-ttu-id="68d29-166">Поля и вылеты</span><span class="sxs-lookup"><span data-stu-id="68d29-166">Fields and flyouts</span></span>

<span data-ttu-id="68d29-167">Поля – это области, где пользователи могут вводить текст.</span><span class="sxs-lookup"><span data-stu-id="68d29-167">Fields are areas where users can input text.</span></span> <span data-ttu-id="68d29-168">Flyouts являются более легкими, чем диалоги и появляются с верхнего стекла.</span><span class="sxs-lookup"><span data-stu-id="68d29-168">Flyouts are more lightweight than dialogs and appear from the top pane.</span></span>

#### <a name="list-controls"></a><span data-ttu-id="68d29-169">Список элементов управления</span><span class="sxs-lookup"><span data-stu-id="68d29-169">List controls</span></span>

![мобильный список элементов управления](../../assets/images/mobile-list-controls.png)

#### <a name="field-controls"></a><span data-ttu-id="68d29-171">Элементы управления полями</span><span class="sxs-lookup"><span data-stu-id="68d29-171">Field controls</span></span>

![мобильные полевые элементы управления](../../assets/images/mobile-field-controls.png)

## <a name="developer-considerations"></a><span data-ttu-id="68d29-173">Соображения разработчика</span><span class="sxs-lookup"><span data-stu-id="68d29-173">Developer considerations</span></span>

<span data-ttu-id="68d29-174">Когда вы строите приложение, которое включает в себя вкладку, вам нужно рассмотреть (и проверить), как ваша вкладка будет функционировать как на Android и iOS Microsoft Teams клиентов.</span><span class="sxs-lookup"><span data-stu-id="68d29-174">When you're building an app that includes a tab, you need to consider (and test) how your tab will function on both the Android and iOS Microsoft Teams clients.</span></span> <span data-ttu-id="68d29-175">В нижесюмях ниже излагаются некоторые из ключевых сценариев, которые необходимо рассмотреть.</span><span class="sxs-lookup"><span data-stu-id="68d29-175">The sections below outline some of the key scenarios you need to consider.</span></span>

### <a name="authentication"></a><span data-ttu-id="68d29-176">Проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="68d29-176">Authentication</span></span>

<span data-ttu-id="68d29-177">Для того чтобы аутентификация работала на мобильных клиентах, необходимо обновить Teams JavaScript SDK по крайней мере до версии 1.4.1.</span><span class="sxs-lookup"><span data-stu-id="68d29-177">For authentication to work on mobile clients, you must upgrade you Teams JavaScript SDK to at least version 1.4.1.</span></span>

### <a name="low-bandwidth-and-intermittent-connections"></a><span data-ttu-id="68d29-178">Низкая пропускная способность и прерывистые соединения</span><span class="sxs-lookup"><span data-stu-id="68d29-178">Low bandwidth and intermittent connections</span></span>

<span data-ttu-id="68d29-179">Мобильные клиенты регулярно должны функционировать с низкой пропускной способностью и прерывистыми соединениями.</span><span class="sxs-lookup"><span data-stu-id="68d29-179">Mobile clients regularly need to function with low bandwidth and intermittent connections.</span></span> <span data-ttu-id="68d29-180">Ваше приложение должно обрабатывать любые тайм-ауты надлежащим образом, предоставляя контекстное сообщение пользователю.</span><span class="sxs-lookup"><span data-stu-id="68d29-180">Your app should handle any timeouts appropriately by providing a contextual message to the user.</span></span> <span data-ttu-id="68d29-181">Вы также должны индикаторы прогресса пользователя, чтобы обеспечить обратную связь с пользователями для любых длительных процессов.</span><span class="sxs-lookup"><span data-stu-id="68d29-181">You should also user progress indicators to provide feedback to your users for any long-running processes.</span></span>

> [!NOTE]
> <span data-ttu-id="68d29-182">Вкладки включены на мобильный телефон только после того, как приложение будет добавлено в список разрешений, на основе ввода группы утверждения.</span><span class="sxs-lookup"><span data-stu-id="68d29-182">Tabs are enabled on mobile only after the application is added to an allow list, based on the input of the approval team.</span></span> <span data-ttu-id="68d29-183">Чтобы проверить мобильную отзывчивость, обратитесь к teamsubm@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="68d29-183">To check mobile responsiveness, reach out to teamsubm@microsoft.com.</span></span>

### <a name="testing-on-mobile-clients"></a><span data-ttu-id="68d29-184">Тестирование мобильных клиентов</span><span class="sxs-lookup"><span data-stu-id="68d29-184">Testing on mobile clients</span></span>

<span data-ttu-id="68d29-185">Необходимо проверить, правильно ли работает вкладка на мобильных устройствах различных размеров и качеств.</span><span class="sxs-lookup"><span data-stu-id="68d29-185">You need to validate that your tab functions properly on mobile devices of various sizes and qualities.</span></span> <span data-ttu-id="68d29-186">Для android устройств, вы можете использовать [DevTools для отладки](~/tabs/how-to/developer-tools.md) вкладке во время его работы.</span><span class="sxs-lookup"><span data-stu-id="68d29-186">For Android devices, you can use the [DevTools](~/tabs/how-to/developer-tools.md) to debug your tab while it is running.</span></span> <span data-ttu-id="68d29-187">Мы рекомендуем тестировать как на высок-, так и на низкую производительность устройств, включая планшет.</span><span class="sxs-lookup"><span data-stu-id="68d29-187">We recommend that you test on both high- and low-performance devices, including a tablet.</span></span>

### <a name="distribution"></a><span data-ttu-id="68d29-188">распределение</span><span class="sxs-lookup"><span data-stu-id="68d29-188">Distribution</span></span>

<span data-ttu-id="68d29-189">Приложения, перечисленные в Teams магазине, должны быть одобрены для мобильного использования, чтобы функционировать должным образом Teams мобильного клиента.</span><span class="sxs-lookup"><span data-stu-id="68d29-189">Apps listed on the Teams store must be approved for mobile use to function properly in the Teams mobile client.</span></span> <span data-ttu-id="68d29-190">Доступность и поведение вкладок зависят от того, одобрено ли ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="68d29-190">Tab availability and behavior depends on whether your app is approved.</span></span>

#### <a name="apps-on-teams-store-approved-for-mobile"></a><span data-ttu-id="68d29-191">Приложения в Teams магазине одобрены для мобильных устройств</span><span class="sxs-lookup"><span data-stu-id="68d29-191">Apps on Teams store approved for mobile</span></span>

<span data-ttu-id="68d29-192">В следующей таблице описывается доступность и поведение вкладок, когда приложение перечислено в Teams и одобрено для мобильного использования:</span><span class="sxs-lookup"><span data-stu-id="68d29-192">The following table describes tab availability and behavior when the app is listed on the Teams store and approved for mobile use:</span></span>

|<span data-ttu-id="68d29-193">Возможность</span><span class="sxs-lookup"><span data-stu-id="68d29-193">Capability</span></span>   |<span data-ttu-id="68d29-194">Доступность мобильных устройств?</span><span class="sxs-lookup"><span data-stu-id="68d29-194">Mobile availability?</span></span>   |<span data-ttu-id="68d29-195">Мобильное поведение</span><span class="sxs-lookup"><span data-stu-id="68d29-195">Mobile behavior</span></span>|
|----------|-----------|------------|
|<span data-ttu-id="68d29-196">Канал</span><span class="sxs-lookup"><span data-stu-id="68d29-196">Channel</span></span> <br /> <span data-ttu-id="68d29-197">и вкладка группы</span><span class="sxs-lookup"><span data-stu-id="68d29-197">and group tab</span></span>|<span data-ttu-id="68d29-198">Да</span><span class="sxs-lookup"><span data-stu-id="68d29-198">Yes</span></span>|<span data-ttu-id="68d29-199">Вкладка открывается в Teams мобильного клиента с помощью конфигурации `contentUrl` приложения.</span><span class="sxs-lookup"><span data-stu-id="68d29-199">Tab opens in the Teams mobile client using your app's `contentUrl` configuration.</span></span>|
|<span data-ttu-id="68d29-200">Личное приложение</span><span class="sxs-lookup"><span data-stu-id="68d29-200">Personal app</span></span>|<span data-ttu-id="68d29-201">Да</span><span class="sxs-lookup"><span data-stu-id="68d29-201">Yes</span></span>|<span data-ttu-id="68d29-202">Каждая вкладка в вкладке личного приложения открывается в Teams клиента, используя его `contentUrl` конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="68d29-202">Each tab in the personal app tab opens in the Teams mobile client using its respective `contentUrl` configuration.</span></span>|

#### <a name="apps-on-teams-store-not-approved-for-mobile"></a><span data-ttu-id="68d29-203">Приложения в Teams не одобрены для мобильных устройств</span><span class="sxs-lookup"><span data-stu-id="68d29-203">Apps on Teams store not approved for mobile</span></span>

<span data-ttu-id="68d29-204">В следующей таблице описывается доступность и поведение вкладок, когда приложение перечислено в магазине Teams, но не одобрено для мобильного использования:</span><span class="sxs-lookup"><span data-stu-id="68d29-204">The following table describes tab availability and behavior when the app is listed on the Teams store but not approved for mobile use:</span></span>

| <span data-ttu-id="68d29-205">Возможность</span><span class="sxs-lookup"><span data-stu-id="68d29-205">Capability</span></span> | <span data-ttu-id="68d29-206">Доступность мобильных устройств?</span><span class="sxs-lookup"><span data-stu-id="68d29-206">Mobile availability?</span></span> | <span data-ttu-id="68d29-207">Мобильное поведение</span><span class="sxs-lookup"><span data-stu-id="68d29-207">Mobile behavior</span></span> |
|----------|-----------|------------|
|<span data-ttu-id="68d29-208">Вкладка канала и группы</span><span class="sxs-lookup"><span data-stu-id="68d29-208">Channel and group tab</span></span>|<span data-ttu-id="68d29-209">Да</span><span class="sxs-lookup"><span data-stu-id="68d29-209">Yes</span></span>|<span data-ttu-id="68d29-210">Вкладка открывается в браузере устройства по умолчанию вместо мобильного клиента Teams с помощью `websiteUrl` конфигурации приложения, которая также должна быть включена в функцию вашего исходных `setSettings()` [кодов.](/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest#functions&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="68d29-210">Tab opens in the device's default browser instead of the Teams mobile client using your app's `websiteUrl` configuration, which also must be included in your source code's `setSettings()` [function](/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest#functions&preserve-view=true).</span></span> <span data-ttu-id="68d29-211">Тем не менее, пользователи по-прежнему могут просматривать вкладку в мобильном Teams, выбрав **больше** рядом с **приложением и выбрав Open**, который запускает конфигурацию вашего `contentUrl` приложения.</span><span class="sxs-lookup"><span data-stu-id="68d29-211">However, users can still view the tab in the Teams mobile client by selecting **More** next to the app and choosing **Open**, which triggers your app’s `contentUrl` configuration.</span></span>|
|<span data-ttu-id="68d29-212">Личное приложение</span><span class="sxs-lookup"><span data-stu-id="68d29-212">Personal app</span></span>|<span data-ttu-id="68d29-213">НЕТ</span><span class="sxs-lookup"><span data-stu-id="68d29-213">No</span></span>|<span data-ttu-id="68d29-214">Неприменимо</span><span class="sxs-lookup"><span data-stu-id="68d29-214">Not applicable</span></span>|

#### <a name="apps-not-on-teams-store"></a><span data-ttu-id="68d29-215">Приложения, не Teams магазине</span><span class="sxs-lookup"><span data-stu-id="68d29-215">Apps not on Teams store</span></span>

<span data-ttu-id="68d29-216">Если вы поддерживаете загрузку приложения или публикуете его в каталоге приложений организации, поведение вкладок будет таким же, как Teams приложений, одобренных корпорацией Майкрософт для мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="68d29-216">If you're sideloading your app or publishing to an org's app catalog, tab behavior will be the same as Teams store apps approved by Microsoft for mobile.</span></span>
