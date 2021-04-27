---
title: Вкладки на мобильных устройствах
description: Описывает рекомендации по разработке вкладок, которые работают на мобильных устройствах.
ms.topic: conceptual
localization_priority: Normal
keywords: группы разработки рекомендаций по справочной платформе персональных вкладок мобильных приложений
ms.openlocfilehash: 6459d6af7899859f25b28587021e26ce6440fbef
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020410"
---
# <a name="tabs-on-mobile"></a><span data-ttu-id="2f69b-104">Вкладки на мобильных устройствах</span><span class="sxs-lookup"><span data-stu-id="2f69b-104">Tabs on mobile</span></span>

> [!NOTE]
> <span data-ttu-id="2f69b-105">Если в мобильных клиентах Teams появится вкладка канал/группа, конфигурация должна иметь значение свойства `setSettings()` `websiteUrl` (см. ниже).</span><span class="sxs-lookup"><span data-stu-id="2f69b-105">If you choose to have your channel/group tab appear on Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property (see below).</span></span>

<span data-ttu-id="2f69b-106">Настраиваемые вкладки могут быть частью канала, группового чата или личного приложения (приложений, содержащих статические вкладки и/или бота один к одному).</span><span class="sxs-lookup"><span data-stu-id="2f69b-106">Custom tabs can be part of a channel, group chat, or personal app (apps that contain static tabs and/or a one-to-one bot).</span></span>

<span data-ttu-id="2f69b-107">Личные приложения доступны для мобильных клиентов в ящике приложения.</span><span class="sxs-lookup"><span data-stu-id="2f69b-107">Personal apps are available on mobile clients in the app drawer.</span></span> <span data-ttu-id="2f69b-108">Приложение может быть установлено только с рабочего стола или веб-клиента и может отображаться на мобильных клиентах до 24 часов.</span><span class="sxs-lookup"><span data-stu-id="2f69b-108">The app can only be installed from a desktop or web client, and can take up to 24 hours to appear on mobile clients.</span></span> <span data-ttu-id="2f69b-109">Кроме того, вы можете обеспечить перезагрузку на мобильном клиенте, выехав и войк.</span><span class="sxs-lookup"><span data-stu-id="2f69b-109">Alternatively, you can enforce a reload on the mobile client by signing out and in.</span></span> <span data-ttu-id="2f69b-110">Это должно сделать мобильное приложение доступным сразу.</span><span class="sxs-lookup"><span data-stu-id="2f69b-110">This should make the mobile app available right away.</span></span>

<span data-ttu-id="2f69b-111">Вкладки канала также доступны на мобильных устройствах.</span><span class="sxs-lookup"><span data-stu-id="2f69b-111">Channel tabs are also available on mobile.</span></span> <span data-ttu-id="2f69b-112">Поведение по умолчанию в настоящее время используется для запуска `websiteUrl` вкладки в окне браузера.</span><span class="sxs-lookup"><span data-stu-id="2f69b-112">The default behavior is currently to use your `websiteUrl` to launch your tab in a browser window.</span></span> <span data-ttu-id="2f69b-113">Однако они могут быть загружены на мобильный клиент, щелкнув меню переполнения рядом со вкладкой и выбрав Open, который будет использовать вашу для загрузки вкладки внутри мобильного клиента `...`  `contentUrl` Teams.</span><span class="sxs-lookup"><span data-stu-id="2f69b-113">However, they can be loaded on a mobile client by clicking the `...` overflow menu next to the tab and choosing **Open**, which will use your `contentUrl` to load the tab inside the Teams mobile client.</span></span>

## <a name="accessing-personal-tabs"></a><span data-ttu-id="2f69b-114">Доступ к личным вкладкам</span><span class="sxs-lookup"><span data-stu-id="2f69b-114">Accessing personal tabs</span></span>

<span data-ttu-id="2f69b-115">На следующем рисунке показано, как получить доступ к личной вкладке на мобильном устройстве.</span><span class="sxs-lookup"><span data-stu-id="2f69b-115">The following illustration shows how you access a personal tab on mobile.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-app-drawer.png" alt-text="Иллюстрация, показывающая ящик мобильного приложения Teams." border="false":::

## <a name="accessing-channel-tabs"></a><span data-ttu-id="2f69b-117">Доступ к вкладке канала</span><span class="sxs-lookup"><span data-stu-id="2f69b-117">Accessing channel tabs</span></span>

<span data-ttu-id="2f69b-118">На следующем рисунке показано, как получить доступ к вкладке канала на мобильном телефоне.</span><span class="sxs-lookup"><span data-stu-id="2f69b-118">The following illustration shows how you access a channel tab on mobile.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab.png" alt-text="Иллюстрация, показывающая вкладку Teams для мобильных устройств." border="false":::

## <a name="design-considerations"></a><span data-ttu-id="2f69b-120">Особенности дизайна</span><span class="sxs-lookup"><span data-stu-id="2f69b-120">Design considerations</span></span>

<span data-ttu-id="2f69b-121">Наша мобильная платформа позволяет приложениям быть иммерсивным опытом с контентом приложения, за исключением основной навигации Teams.</span><span class="sxs-lookup"><span data-stu-id="2f69b-121">Our mobile platform allows apps to be an immersive experience with the app content taking up all of the screen apart from main Teams navigation.</span></span> <span data-ttu-id="2f69b-122">Чтобы создать иммерсивный опыт, который подходит для Teams, следуйте этим рекомендациям.</span><span class="sxs-lookup"><span data-stu-id="2f69b-122">To create an immersive experience that fits with Teams, follow these guidelines.</span></span>

### <a name="responsive-design"></a><span data-ttu-id="2f69b-123">Адаптивный дизайн</span><span class="sxs-lookup"><span data-stu-id="2f69b-123">Responsive design</span></span>

<span data-ttu-id="2f69b-124">Так как вкладка может быть открыта на устройствах с широким диапазоном размеров экрана, она должна следовать принципам [гибкого проектирования.](https://www.w3schools.com/html/html_responsive.asp)</span><span class="sxs-lookup"><span data-stu-id="2f69b-124">Because your tab can be opened on devices with a wide range of screen sizes, it needs to follow [responsive design](https://www.w3schools.com/html/html_responsive.asp) principles.</span></span> <span data-ttu-id="2f69b-125">Все ключевые конструкции должны быть доступны на мобильных устройствах, и представления не должны искажаться.</span><span class="sxs-lookup"><span data-stu-id="2f69b-125">All of the key constructs should be accessible on mobile devices, and the views should not be distorted.</span></span> <span data-ttu-id="2f69b-126">Убедитесь, что при загрузке вкладки на мобильном устройстве все кнопки и ссылки легко доступны с помощью навигации на основе пальцев.</span><span class="sxs-lookup"><span data-stu-id="2f69b-126">Ensure that when your tab is loaded on a mobile device, all buttons and links are easily accessible using finger-based navigation.</span></span>

### <a name="layouts"></a><span data-ttu-id="2f69b-127">макеты;</span><span class="sxs-lookup"><span data-stu-id="2f69b-127">Layouts</span></span>

<span data-ttu-id="2f69b-128">Важно выбрать правильный макет вкладки.</span><span class="sxs-lookup"><span data-stu-id="2f69b-128">Choosing the correct layout for your tab is important.</span></span> <span data-ttu-id="2f69b-129">Необходимо рассмотреть тип представляемой информации и выбрать макет, который организует ее для легкого потребления.</span><span class="sxs-lookup"><span data-stu-id="2f69b-129">You should consider the kind of information you're presenting, and choose a layout that organizes it for easy consumption.</span></span> <span data-ttu-id="2f69b-130">Ниже описаны некоторые возможные варианты.</span><span class="sxs-lookup"><span data-stu-id="2f69b-130">Some potential options are outlined below.</span></span>

#### <a name="single-canvas"></a><span data-ttu-id="2f69b-131">Одно полотно</span><span class="sxs-lookup"><span data-stu-id="2f69b-131">Single canvas</span></span>

<span data-ttu-id="2f69b-132">Это одна большая область, в которой делается работа.</span><span class="sxs-lookup"><span data-stu-id="2f69b-132">This is one large area where work gets done.</span></span> <span data-ttu-id="2f69b-133">Приложение Teams Wiki следует этому шаблону.</span><span class="sxs-lookup"><span data-stu-id="2f69b-133">The Teams Wiki app follows this pattern.</span></span> <span data-ttu-id="2f69b-134">Если у вас есть приложение, которое не разделяет контент на более мелкие компоненты, это будет подходящим.</span><span class="sxs-lookup"><span data-stu-id="2f69b-134">If you have an app that doesn’t separate content into smaller components this would be a good fit.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-single-canvas.png" alt-text="Иллюстрация, на которой показана вкладка &quot;Одно полотно Для мобильных групп&quot;." border="false":::

#### <a name="list"></a><span data-ttu-id="2f69b-136">List</span><span class="sxs-lookup"><span data-stu-id="2f69b-136">List</span></span>

<span data-ttu-id="2f69b-137">Списки отлично подходит для сортировки и фильтрации больших объемов данных и отлично подходит для хранения наиболее важных вещей в верхней части.</span><span class="sxs-lookup"><span data-stu-id="2f69b-137">Lists are great for sorting and filtering large quantities of data and are great at keeping the most important things at the top.</span></span> <span data-ttu-id="2f69b-138">Полезно использовать сортируемые столбцы.</span><span class="sxs-lookup"><span data-stu-id="2f69b-138">It is helpful to use sortable columns.</span></span> <span data-ttu-id="2f69b-139">Действия могут быть добавлены к каждому элементу списка в меню ellipsis.</span><span class="sxs-lookup"><span data-stu-id="2f69b-139">Actions can be added to each list item under the ellipsis menu.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-list.png" alt-text="Иллюстрация, показывающая вкладку список мобильных групп." border="false":::

#### <a name="grid"></a><span data-ttu-id="2f69b-141">Grid</span><span class="sxs-lookup"><span data-stu-id="2f69b-141">Grid</span></span>

<span data-ttu-id="2f69b-142">Сетки полезны для демонстрации элементов с высокой наглядности.</span><span class="sxs-lookup"><span data-stu-id="2f69b-142">Grids are useful for showing elements which are highly visual.</span></span> <span data-ttu-id="2f69b-143">Это помогает включить фильтр или управление поиском в верхней части.</span><span class="sxs-lookup"><span data-stu-id="2f69b-143">It helps to include a filter or search control at the top.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-grid.png" alt-text="На рисунке показана вкладка для мобильных устройств Teams с макетом сетки." border="false":::

### <a name="tabs-with-bots-on-mobile"></a><span data-ttu-id="2f69b-145">Вкладки с ботами на мобильных устройствах</span><span class="sxs-lookup"><span data-stu-id="2f69b-145">Tabs with bots on mobile</span></span>

<span data-ttu-id="2f69b-146">Ниже приводится личный пример приложения с вкладками и ботом.</span><span class="sxs-lookup"><span data-stu-id="2f69b-146">The following example is a personal app that has tabs and a bot.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-with-bot.png" alt-text="На рисунке показывая, как мобильное приложение Teams с вкладками и ботом." border="false":::

## <a name="ui-components"></a><span data-ttu-id="2f69b-148">Компоненты пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="2f69b-148">UI components</span></span>

### <a name="color-palettes"></a><span data-ttu-id="2f69b-149">Цветовые палитры</span><span class="sxs-lookup"><span data-stu-id="2f69b-149">Color palettes</span></span>

<span data-ttu-id="2f69b-150">Использование нашей утвержденной нейтральной палитры фонов, уведомлений, текста и кнопок поможет приложению чувствовать себя как дома в Teams.</span><span class="sxs-lookup"><span data-stu-id="2f69b-150">Using our approved neutral palette for backgrounds, notifications, text, and buttons will help your app feel more at home in Teams.</span></span> <span data-ttu-id="2f69b-151">Так как мобильный телефон Teams имеет две цветовые темы (светлый и темный), лучше убедиться, что ваше приложение отлично выглядит в обоих.</span><span class="sxs-lookup"><span data-stu-id="2f69b-151">Since Teams mobile has two colour themes (light and dark), it’s a good idea to make sure your app looks great in both.</span></span>

#### <a name="light-color"></a><span data-ttu-id="2f69b-152">Светлый цвет</span><span class="sxs-lookup"><span data-stu-id="2f69b-152">Light color</span></span>

![светлая цветовая палитра](../../assets/images/light-color.png)

#### <a name="dark-color"></a><span data-ttu-id="2f69b-154">Темный цвет</span><span class="sxs-lookup"><span data-stu-id="2f69b-154">Dark color</span></span>

![темная цветовая палитра](../../assets/images/dark-color.png)

### <a name="buttons-and-controls"></a><span data-ttu-id="2f69b-156">Кнопки и элементы управления</span><span class="sxs-lookup"><span data-stu-id="2f69b-156">Buttons and controls</span></span>

<span data-ttu-id="2f69b-157">Стиль кнопок позволяет сообщить, какие действия они запускают.</span><span class="sxs-lookup"><span data-stu-id="2f69b-157">The way buttons are styled helps communicate what kind of action they trigger.</span></span> <span data-ttu-id="2f69b-158">Мы поддерживаем широкий диапазон кнопок, которые отформатированы, чтобы показать различные уровни акцента.</span><span class="sxs-lookup"><span data-stu-id="2f69b-158">We maintain a wide range of buttons that are formatted to show different levels of emphasis.</span></span> <span data-ttu-id="2f69b-159">Кнопки могут иметь текст, значок или сочетание текста и значка.</span><span class="sxs-lookup"><span data-stu-id="2f69b-159">Buttons can have text, an icon, or a combination of text and an icon.</span></span> <span data-ttu-id="2f69b-160">Чтобы общаться на разных уровнях в иерархии, мы разработали основные и вторичные кнопки в каждой категории.</span><span class="sxs-lookup"><span data-stu-id="2f69b-160">To communicate different levels in a hierarchy, we designed primary and secondary buttons within each category.</span></span>

#### <a name="buttons"></a><span data-ttu-id="2f69b-161">Кнопки</span><span class="sxs-lookup"><span data-stu-id="2f69b-161">Buttons</span></span>

<span data-ttu-id="2f69b-162">Основные и вторичные кнопки.</span><span class="sxs-lookup"><span data-stu-id="2f69b-162">Primary and secondary buttons.</span></span>

![изображение кнопок](../../assets/images/buttons.png)

#### <a name="selection-controls"></a><span data-ttu-id="2f69b-164">Элементы управления выбором</span><span class="sxs-lookup"><span data-stu-id="2f69b-164">Selection controls</span></span>

<span data-ttu-id="2f69b-165">Кнопки радио, почтовые ящики и очки.</span><span class="sxs-lookup"><span data-stu-id="2f69b-165">Radio buttons, checkboxes, and toggles.</span></span>

![элементы управления выбором](../../assets/images/selection-controls.png)

#### <a name="chiclets-and-pills"></a><span data-ttu-id="2f69b-167">Шиклеты и таблетки</span><span class="sxs-lookup"><span data-stu-id="2f69b-167">Chiclets and pills</span></span>

![шиклеты и таблетки](../../assets/images/chiclets-and-pills.png)

### <a name="typography"></a><span data-ttu-id="2f69b-169">Шрифтовое оформление</span><span class="sxs-lookup"><span data-stu-id="2f69b-169">Typography</span></span>

<span data-ttu-id="2f69b-170">Типография должна быть четкой и целенаправленной.</span><span class="sxs-lookup"><span data-stu-id="2f69b-170">Typography should be clear and purposeful.</span></span> <span data-ttu-id="2f69b-171">Подчеркивать важные сведения и избегать использования нескольких шрифтов и размеров для уменьшения путаницы.</span><span class="sxs-lookup"><span data-stu-id="2f69b-171">Emphasize important information and avoid using multiple fonts and sizes to reduce confusion.</span></span> <span data-ttu-id="2f69b-172">Рекомендуется использовать пример предложения и избегать использования всех колпачок для локализации и разнонабности.</span><span class="sxs-lookup"><span data-stu-id="2f69b-172">We recommend using sentence case and avoiding the usage of all caps for localization and legibility.</span></span>

![мобильный опечаток](../../assets/images/mobile-typography.png)

### <a name="fields-and-flyouts"></a><span data-ttu-id="2f69b-174">Поля и вылеты</span><span class="sxs-lookup"><span data-stu-id="2f69b-174">Fields and flyouts</span></span>

<span data-ttu-id="2f69b-175">Поля — это области, в которых пользователи могут вводить текст.</span><span class="sxs-lookup"><span data-stu-id="2f69b-175">Fields are areas where users can input text.</span></span> <span data-ttu-id="2f69b-176">Вылеты более легкие, чем диалоги, и отображаются на верхней области.</span><span class="sxs-lookup"><span data-stu-id="2f69b-176">Flyouts are more lightweight than dialogs and appear from the top pane.</span></span>

#### <a name="list-controls"></a><span data-ttu-id="2f69b-177">Список элементов управления</span><span class="sxs-lookup"><span data-stu-id="2f69b-177">List controls</span></span>

![элементы управления списками мобильных устройств](../../assets/images/mobile-list-controls.png)

#### <a name="field-controls"></a><span data-ttu-id="2f69b-179">Элементы управления полями</span><span class="sxs-lookup"><span data-stu-id="2f69b-179">Field controls</span></span>

![элементы управления мобильными полями](../../assets/images/mobile-field-controls.png)

## <a name="developer-considerations"></a><span data-ttu-id="2f69b-181">Соображения разработчика</span><span class="sxs-lookup"><span data-stu-id="2f69b-181">Developer considerations</span></span>

<span data-ttu-id="2f69b-182">При создании приложения, включаемого в вкладку, необходимо учитывать (и тестировать) функции вкладки на клиентах Android и iOS Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="2f69b-182">When you're building an app that includes a tab, you need to consider (and test) how your tab will function on both the Android and iOS Microsoft Teams clients.</span></span> <span data-ttu-id="2f69b-183">В разделах ниже описаны некоторые ключевые сценарии, которые необходимо рассмотреть.</span><span class="sxs-lookup"><span data-stu-id="2f69b-183">The sections below outline some of the key scenarios you need to consider.</span></span>

### <a name="testing-on-mobile-clients"></a><span data-ttu-id="2f69b-184">Тестирование мобильных клиентов</span><span class="sxs-lookup"><span data-stu-id="2f69b-184">Testing on mobile clients</span></span>

<span data-ttu-id="2f69b-185">Необходимо проверить правильность функции вкладки на мобильных устройствах различных размеров и качеств.</span><span class="sxs-lookup"><span data-stu-id="2f69b-185">You need to validate that your tab functions properly on mobile devices of various sizes and qualities.</span></span> <span data-ttu-id="2f69b-186">Для устройств с Android можно использовать [DevTools](~/tabs/how-to/developer-tools.md) для отладки вкладки во время ее работы.</span><span class="sxs-lookup"><span data-stu-id="2f69b-186">For Android devices, you can use the [DevTools](~/tabs/how-to/developer-tools.md) to debug your tab while it is running.</span></span> <span data-ttu-id="2f69b-187">Рекомендуется протестировать как на высокой, так и на низкой скорости, а также на планшете.</span><span class="sxs-lookup"><span data-stu-id="2f69b-187">We recommend that you test on both high and low performing devices, as well as on a tablet.</span></span>

### <a name="authentication"></a><span data-ttu-id="2f69b-188">Проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="2f69b-188">Authentication</span></span>

<span data-ttu-id="2f69b-189">Для проверки подлинности для мобильных клиентов необходимо обновить команду JavaScript SDK по крайней мере до версии 1.4.1.</span><span class="sxs-lookup"><span data-stu-id="2f69b-189">For authentication to work on mobile clients, you must upgrade you Teams JavaScript SDK to at least version 1.4.1.</span></span>

### <a name="low-bandwidth-and-intermittent-connections"></a><span data-ttu-id="2f69b-190">Низкая пропускная способность и периодические подключения</span><span class="sxs-lookup"><span data-stu-id="2f69b-190">Low bandwidth and intermittent connections</span></span>

<span data-ttu-id="2f69b-191">Мобильные клиенты регулярно должны работать с низкой пропускной способностью и периодическими подключениями.</span><span class="sxs-lookup"><span data-stu-id="2f69b-191">Mobile clients regularly need to function with low bandwidth and intermittent connections.</span></span> <span data-ttu-id="2f69b-192">Ваше приложение должно надлежащим образом обрабатывать любые периоды времени, предоставляя пользователю контекстное сообщение.</span><span class="sxs-lookup"><span data-stu-id="2f69b-192">Your app should handle any timeouts appropriately by providing a contextual message to the user.</span></span> <span data-ttu-id="2f69b-193">Кроме того, необходимо использовать индикаторы прогресса пользователей, чтобы предоставить пользователям обратную связь для любых длительных процессов.</span><span class="sxs-lookup"><span data-stu-id="2f69b-193">You should also user progress indicators to provide feedback to your users for any long-running processes.</span></span>

> [!NOTE]
> <span data-ttu-id="2f69b-194">Вкладки включены на мобильных устройствах только после того, как приложение будет добавлено в список разрешений на основе ввода группы утверждения.</span><span class="sxs-lookup"><span data-stu-id="2f69b-194">Tabs are enabled on mobile only after the application is added to an allow list, based on the input of the approval team.</span></span> <span data-ttu-id="2f69b-195">Чтобы проверить отзывчивость мобильных устройств, обратитесь к teamsubm@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="2f69b-195">To check mobile responsiveness, reach out to teamsubm@microsoft.com.</span></span> 
