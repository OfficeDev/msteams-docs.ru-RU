---
title: Вкладки на мобильных устройствах
description: Описывает рекомендации по проектированию вкладок, работающих на мобильных устройствах.
keywords: рекомендации по проектированию Teams — вкладки личных приложений для мобильных устройств
ms.openlocfilehash: a1939465b04a1fe4b803efaf83402852ca536059
ms.sourcegitcommit: b51a4982842948336cfabedb63bdf8f72703585e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/25/2020
ms.locfileid: "48279767"
---
# <a name="tabs-on-mobile"></a><span data-ttu-id="ba2c3-104">Вкладки на мобильных устройствах</span><span class="sxs-lookup"><span data-stu-id="ba2c3-104">Tabs on mobile</span></span>

> [!NOTE]
> <span data-ttu-id="ba2c3-105">Если вкладка канал и группа отображается в клиентах Teams для мобильных устройств, то `setSettings()` конфигурация должна иметь значение для `websiteUrl` Свойства (см. ниже).</span><span class="sxs-lookup"><span data-stu-id="ba2c3-105">If you choose to have your channel/group tab appear on Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property (see below).</span></span>

<span data-ttu-id="ba2c3-106">Настраиваемые вкладки могут быть частью канала, группового чата или личного приложения (приложения, содержащие статические вкладки и/или односторонняя робот).</span><span class="sxs-lookup"><span data-stu-id="ba2c3-106">Custom tabs can be part of a channel, group chat, or personal app (apps that contain static tabs and/or a one-to-one bot).</span></span>

<span data-ttu-id="ba2c3-107">Персональные приложения доступны на мобильных клиентах в почтовом ящике приложения.</span><span class="sxs-lookup"><span data-stu-id="ba2c3-107">Personal apps are available on mobile clients in the app drawer.</span></span> <span data-ttu-id="ba2c3-108">Приложение можно установить только с настольного компьютера или из веб-клиента и может занимать до 24 часов на мобильных клиентах.</span><span class="sxs-lookup"><span data-stu-id="ba2c3-108">The app can only be installed from a desktop or web client, and can take up to 24 hours to appear on mobile clients.</span></span>

<span data-ttu-id="ba2c3-109">Вкладки каналов также доступны на мобильных устройствах.</span><span class="sxs-lookup"><span data-stu-id="ba2c3-109">Channel tabs are also available on mobile.</span></span> <span data-ttu-id="ba2c3-110">Поведение по умолчанию в настоящее время используется `websiteUrl` для запуска вкладки в окне браузера.</span><span class="sxs-lookup"><span data-stu-id="ba2c3-110">The default behavior is currently to use your `websiteUrl` to launch your tab in a browser window.</span></span> <span data-ttu-id="ba2c3-111">Тем не менее, они могут загружаться на мобильном клиенте, если щелкнуть `...` меню переполнения рядом с вкладкой и выбрать команду **Открыть**, которая будет использовать `contentUrl` для загрузки вкладки в клиенте Teams Mobile.</span><span class="sxs-lookup"><span data-stu-id="ba2c3-111">However, they can be loaded on a mobile client by clicking the `...` overflow menu next to the tab and choosing **Open**, which will use your `contentUrl` to load the tab inside the Teams mobile client.</span></span>

## <a name="accessing-personal-tabs"></a><span data-ttu-id="ba2c3-112">Доступ к личным вкладкам</span><span class="sxs-lookup"><span data-stu-id="ba2c3-112">Accessing personal tabs</span></span>

<span data-ttu-id="ba2c3-113">На следующем рисунке показано, как получить доступ к вкладке личные сведения на мобильном устройстве.</span><span class="sxs-lookup"><span data-stu-id="ba2c3-113">The following illustration shows how you access a personal tab on mobile.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-app-drawer.png" alt-text="Иллюстрация, на которой показан входной ящик приложений Teams." border="false":::

## <a name="accessing-channel-tabs"></a><span data-ttu-id="ba2c3-115">Доступ к вкладкам каналов</span><span class="sxs-lookup"><span data-stu-id="ba2c3-115">Accessing channel tabs</span></span>

<span data-ttu-id="ba2c3-116">На следующем рисунке показано, как получить доступ к вкладке канала на мобильном устройстве.</span><span class="sxs-lookup"><span data-stu-id="ba2c3-116">The following illustration shows how you access a channel tab on mobile.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab.png" alt-text="Иллюстрация, на которой показана вкладка Teams Mobile." border="false":::

## <a name="design-considerations"></a><span data-ttu-id="ba2c3-118">Особенности дизайна</span><span class="sxs-lookup"><span data-stu-id="ba2c3-118">Design considerations</span></span>

<span data-ttu-id="ba2c3-119">Наша мобильная платформа позволяет приложениям работать с содержимым приложения, разнимая все экраны, разнимая основные возможности навигации в Teams.</span><span class="sxs-lookup"><span data-stu-id="ba2c3-119">Our mobile platform allows apps to be an immersive experience with the app content taking up all of the screen apart from main Teams navigation.</span></span> <span data-ttu-id="ba2c3-120">Чтобы создать иммерсивное взаимодействие с Teams, следуйте этим рекомендациям.</span><span class="sxs-lookup"><span data-stu-id="ba2c3-120">To create an immersive experience that fits with Teams, follow these guidelines.</span></span>

### <a name="responsive-design"></a><span data-ttu-id="ba2c3-121">Адаптивный дизайн</span><span class="sxs-lookup"><span data-stu-id="ba2c3-121">Responsive design</span></span>

<span data-ttu-id="ba2c3-122">Так как вкладка может быть открыта на устройствах с широким размером экрана, она должна соответствовать принципам [создания отклика](https://www.w3schools.com/html/html_responsive.asp) .</span><span class="sxs-lookup"><span data-stu-id="ba2c3-122">Because your tab can be opened on devices with a wide range of screen sizes, it needs to follow [responsive design](https://www.w3schools.com/html/html_responsive.asp) principles.</span></span> <span data-ttu-id="ba2c3-123">Все основные конструкции должны быть доступны на мобильных устройствах, и представления не должны искажаться.</span><span class="sxs-lookup"><span data-stu-id="ba2c3-123">All of the key constructs should be accessible on mobile devices, and the views should not be distorted.</span></span> <span data-ttu-id="ba2c3-124">Убедитесь, что когда вкладка загружена на мобильном устройстве, все кнопки и ссылки легко доступны с помощью навигации на основе пальца.</span><span class="sxs-lookup"><span data-stu-id="ba2c3-124">Ensure that when your tab is loaded on a mobile device, all buttons and links are easily accessible using finger-based navigation.</span></span>

### <a name="layouts"></a><span data-ttu-id="ba2c3-125">макеты;</span><span class="sxs-lookup"><span data-stu-id="ba2c3-125">Layouts</span></span>

<span data-ttu-id="ba2c3-126">Важно выбрать правильный макет для вкладки.</span><span class="sxs-lookup"><span data-stu-id="ba2c3-126">Choosing the correct layout for your tab is important.</span></span> <span data-ttu-id="ba2c3-127">Следует учитывать тип данных, которые вы предоставляете, и выбирать макет, который организует его для простоты использования.</span><span class="sxs-lookup"><span data-stu-id="ba2c3-127">You should consider the kind of information you're presenting, and choose a layout that organizes it for easy consumption.</span></span> <span data-ttu-id="ba2c3-128">Ниже приведены некоторые возможные параметры.</span><span class="sxs-lookup"><span data-stu-id="ba2c3-128">Some potential options are outlined below.</span></span>

#### <a name="single-canvas"></a><span data-ttu-id="ba2c3-129">Один холст</span><span class="sxs-lookup"><span data-stu-id="ba2c3-129">Single canvas</span></span>

<span data-ttu-id="ba2c3-130">Это одна большая область, в которой выполняется работу.</span><span class="sxs-lookup"><span data-stu-id="ba2c3-130">This is one large area where work gets done.</span></span> <span data-ttu-id="ba2c3-131">Приложение Teams соответствует этому шаблону.</span><span class="sxs-lookup"><span data-stu-id="ba2c3-131">The Teams Wiki app follows this pattern.</span></span> <span data-ttu-id="ba2c3-132">Если у вас есть приложение, не разделяее контент на небольшие компоненты, это будет очень полезно.</span><span class="sxs-lookup"><span data-stu-id="ba2c3-132">If you have an app that doesn’t separate content into smaller components this would be a good fit.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-single-canvas.png" alt-text="Иллюстрация, на которой показана вкладка "один холст для мобильных устройств"." border="false":::

#### <a name="list"></a><span data-ttu-id="ba2c3-134">Список</span><span class="sxs-lookup"><span data-stu-id="ba2c3-134">List</span></span>

<span data-ttu-id="ba2c3-135">Списки отлично подходят для сортировки и фильтрации больших объемов данных и прекрасно подходят для наиболее важных вещей в верхней части.</span><span class="sxs-lookup"><span data-stu-id="ba2c3-135">Lists are great for sorting and filtering large quantities of data and are great at keeping the most important things at the top.</span></span> <span data-ttu-id="ba2c3-136">Рекомендуется использовать сортируемый столбцы.</span><span class="sxs-lookup"><span data-stu-id="ba2c3-136">It is helpful to use sortable columns.</span></span> <span data-ttu-id="ba2c3-137">Действия можно добавлять к каждому элементу списка в меню с многоточием.</span><span class="sxs-lookup"><span data-stu-id="ba2c3-137">Actions can be added to each list item under the ellipsis menu.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-list.png" alt-text="Иллюстрация, на которой показана вкладка списка для мобильных устройств Teams." border="false":::

#### <a name="grid"></a><span data-ttu-id="ba2c3-139">Таблице</span><span class="sxs-lookup"><span data-stu-id="ba2c3-139">Grid</span></span>

<span data-ttu-id="ba2c3-140">Сетки удобно использовать для отображения элементов, которые являются очень визуальными.</span><span class="sxs-lookup"><span data-stu-id="ba2c3-140">Grids are useful for showing elements which are highly visual.</span></span> <span data-ttu-id="ba2c3-141">В верхней части можно включить фильтр или элемент управления поиском.</span><span class="sxs-lookup"><span data-stu-id="ba2c3-141">It helps to include a filter or search control at the top.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-grid.png" alt-text="Иллюстрация вкладки Teams Mobile с макетом сетки." border="false":::

### <a name="tabs-with-bots-on-mobile"></a><span data-ttu-id="ba2c3-143">Вкладки с боты на мобильных устройствах</span><span class="sxs-lookup"><span data-stu-id="ba2c3-143">Tabs with bots on mobile</span></span>

<span data-ttu-id="ba2c3-144">Ниже приведен пример личного приложения с вкладками и Bot.</span><span class="sxs-lookup"><span data-stu-id="ba2c3-144">The following example is a personal app that has tabs and a bot.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-with-bot.png" alt-text="Иллюстрация, на которой показано, как приложение для мобильных устройств имеет вкладки и Bot." border="false":::

## <a name="ui-components"></a><span data-ttu-id="ba2c3-146">Компоненты пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="ba2c3-146">UI components</span></span>

### <a name="color-palettes"></a><span data-ttu-id="ba2c3-147">Цветовые палитры</span><span class="sxs-lookup"><span data-stu-id="ba2c3-147">Color palettes</span></span>

<span data-ttu-id="ba2c3-148">Использование нашей утвержденной нейтральной палитры для фоновых рисунков, уведомлений, текста и кнопок поможет вам в работе над приложением в Teams.</span><span class="sxs-lookup"><span data-stu-id="ba2c3-148">Using our approved neutral palette for backgrounds, notifications, text, and buttons will help your app feel more at home in Teams.</span></span> <span data-ttu-id="ba2c3-149">Так как в Teams есть две цветные темы (светло-и темная), рекомендуется убедиться в том, что ваше приложение отлично выглядит как.</span><span class="sxs-lookup"><span data-stu-id="ba2c3-149">Since Teams mobile has two colour themes (light and dark), it’s a good idea to make sure your app looks great in both.</span></span>

#### <a name="light-color"></a><span data-ttu-id="ba2c3-150">Светлый цвет</span><span class="sxs-lookup"><span data-stu-id="ba2c3-150">Light color</span></span>

![Палитра "светлый цвет"](../../assets/images/light-color.png)

#### <a name="dark-color"></a><span data-ttu-id="ba2c3-152">Темный цвет</span><span class="sxs-lookup"><span data-stu-id="ba2c3-152">Dark color</span></span>

![Темная цветовая палитра](../../assets/images/dark-color.png)

### <a name="buttons-and-controls"></a><span data-ttu-id="ba2c3-154">Кнопки и элементы управления</span><span class="sxs-lookup"><span data-stu-id="ba2c3-154">Buttons and controls</span></span>

<span data-ttu-id="ba2c3-155">Способ оформления кнопок позволяет сообщить, какие действия они вызывают.</span><span class="sxs-lookup"><span data-stu-id="ba2c3-155">The way buttons are styled helps communicate what kind of action they trigger.</span></span> <span data-ttu-id="ba2c3-156">Мы поддерживаем широкий спектр кнопок, отформатированных для отображения различных уровней выделения.</span><span class="sxs-lookup"><span data-stu-id="ba2c3-156">We maintain a wide range of buttons that are formatted to show different levels of emphasis.</span></span> <span data-ttu-id="ba2c3-157">У кнопок может быть текст, значок или комбинация текста и значок.</span><span class="sxs-lookup"><span data-stu-id="ba2c3-157">Buttons can have text, an icon, or a combination of text and an icon.</span></span> <span data-ttu-id="ba2c3-158">Для связи разных уровней в иерархии мы разработали основные и дополнительные кнопки в каждой категории.</span><span class="sxs-lookup"><span data-stu-id="ba2c3-158">To communicate different levels in a hierarchy, we designed primary and secondary buttons within each category.</span></span>

#### <a name="buttons"></a><span data-ttu-id="ba2c3-159">Кнопки</span><span class="sxs-lookup"><span data-stu-id="ba2c3-159">Buttons</span></span>

<span data-ttu-id="ba2c3-160">Основные и дополнительные кнопки.</span><span class="sxs-lookup"><span data-stu-id="ba2c3-160">Primary and secondary buttons.</span></span>

![изображение кнопок](../../assets/images/buttons.png)

#### <a name="selection-controls"></a><span data-ttu-id="ba2c3-162">Элементы управления выбором</span><span class="sxs-lookup"><span data-stu-id="ba2c3-162">Selection controls</span></span>

<span data-ttu-id="ba2c3-163">Переключатели, флажки и переключатели.</span><span class="sxs-lookup"><span data-stu-id="ba2c3-163">Radio buttons, checkboxes, and toggles.</span></span>

![элементы управления выбором](../../assets/images/selection-controls.png)

#### <a name="chiclets-and-pills"></a><span data-ttu-id="ba2c3-165">Чиклетс и пиллс</span><span class="sxs-lookup"><span data-stu-id="ba2c3-165">Chiclets and pills</span></span>

![чиклетс и пиллс](../../assets/images/chiclets-and-pills.png)

### <a name="typography"></a><span data-ttu-id="ba2c3-167">Шрифтовое оформление</span><span class="sxs-lookup"><span data-stu-id="ba2c3-167">Typography</span></span>

<span data-ttu-id="ba2c3-168">Оформление должно быть ясным и пурпосефулм.</span><span class="sxs-lookup"><span data-stu-id="ba2c3-168">Typography should be clear and purposeful.</span></span> <span data-ttu-id="ba2c3-169">Обратите внимание на важную информацию и Избегайте использования нескольких шрифтов и размеров для сокращения путаницы.</span><span class="sxs-lookup"><span data-stu-id="ba2c3-169">Emphasize important information and avoid using multiple fonts and sizes to reduce confusion.</span></span> <span data-ttu-id="ba2c3-170">Рекомендуется использовать регистр предложений и избегать использования всех политик для локализации и разборчивости.</span><span class="sxs-lookup"><span data-stu-id="ba2c3-170">We recommend using sentence case and avoiding the usage of all caps for localization and legibility.</span></span>

![Мобильные типограф](../../assets/images/mobile-typography.png)

### <a name="fields-and-flyouts"></a><span data-ttu-id="ba2c3-172">Поля и всплывающие окна</span><span class="sxs-lookup"><span data-stu-id="ba2c3-172">Fields and flyouts</span></span>

<span data-ttu-id="ba2c3-173">Поля — это области, в которых пользователи могут вводить текст.</span><span class="sxs-lookup"><span data-stu-id="ba2c3-173">Fields are areas where users can input text.</span></span> <span data-ttu-id="ba2c3-174">Всплывающие окна являются более легковесными, чем диалоговые окна, и отображаются в верхней области.</span><span class="sxs-lookup"><span data-stu-id="ba2c3-174">Flyouts are more lightweight than dialogs and appear from the top pane.</span></span>

#### <a name="list-controls"></a><span data-ttu-id="ba2c3-175">Список элементов управления</span><span class="sxs-lookup"><span data-stu-id="ba2c3-175">List controls</span></span>

![элементы управления списком для мобильных устройств](../../assets/images/mobile-list-controls.png)

#### <a name="field-controls"></a><span data-ttu-id="ba2c3-177">Элементы управления полями</span><span class="sxs-lookup"><span data-stu-id="ba2c3-177">Field controls</span></span>

![Мобильные элементы управления поля](../../assets/images/mobile-field-controls.png)

## <a name="developer-considerations"></a><span data-ttu-id="ba2c3-179">Рекомендации для разработчиков</span><span class="sxs-lookup"><span data-stu-id="ba2c3-179">Developer considerations</span></span>

<span data-ttu-id="ba2c3-180">При создании приложения, включающего вкладку, необходимо учесть (и протестировать), как эта вкладка будет работать как в клиентах Android, так и в Microsoft Teams для iOS.</span><span class="sxs-lookup"><span data-stu-id="ba2c3-180">When you're building an app that includes a tab, you need to consider (and test) how your tab will function on both the Android and iOS Microsoft Teams clients.</span></span> <span data-ttu-id="ba2c3-181">В разделах ниже представлены некоторые ключевые сценарии, которые необходимо учитывать.</span><span class="sxs-lookup"><span data-stu-id="ba2c3-181">The sections below outline some of the key scenarios you need to consider.</span></span>

### <a name="testing-on-mobile-clients"></a><span data-ttu-id="ba2c3-182">Тестирование мобильных клиентов</span><span class="sxs-lookup"><span data-stu-id="ba2c3-182">Testing on mobile clients</span></span>

<span data-ttu-id="ba2c3-183">Необходимо убедиться, что вкладка правильно функционирует на мобильных устройствах различных размеров и качеств.</span><span class="sxs-lookup"><span data-stu-id="ba2c3-183">You need to validate that your tab functions properly on mobile devices of various sizes and qualities.</span></span> <span data-ttu-id="ba2c3-184">Для устройств с Android можно использовать [девтулс](~/tabs/how-to/developer-tools.md) для отладки вкладки во время ее выполнения.</span><span class="sxs-lookup"><span data-stu-id="ba2c3-184">For Android devices, you can use the [DevTools](~/tabs/how-to/developer-tools.md) to debug your tab while it is running.</span></span> <span data-ttu-id="ba2c3-185">Рекомендуется протестировать как высококачественные, так и низкие устройства, а также на планшете.</span><span class="sxs-lookup"><span data-stu-id="ba2c3-185">We recommend that you test on both high and low performing devices, as well as on a tablet.</span></span>

### <a name="authentication"></a><span data-ttu-id="ba2c3-186">Проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="ba2c3-186">Authentication</span></span>

<span data-ttu-id="ba2c3-187">Для проверки подлинности на мобильных клиентах необходимо обновить пакет SDK для Teams JavaScript по крайней мере до версии 1.4.1.</span><span class="sxs-lookup"><span data-stu-id="ba2c3-187">For authentication to work on mobile clients, you must upgrade you Teams JavaScript SDK to at least version 1.4.1.</span></span>

### <a name="low-bandwidth-and-intermittent-connections"></a><span data-ttu-id="ba2c3-188">Низкой пропускной способности и периодических подключений</span><span class="sxs-lookup"><span data-stu-id="ba2c3-188">Low bandwidth and intermittent connections</span></span>

<span data-ttu-id="ba2c3-189">Мобильным клиентам часто приходится работать с низкой пропускной способностью и периодическими подключениями.</span><span class="sxs-lookup"><span data-stu-id="ba2c3-189">Mobile clients regularly need to function with low bandwidth and intermittent connections.</span></span> <span data-ttu-id="ba2c3-190">Ваше приложение должно соответствующим образом обрабатывать все времена ожидания, предоставляя пользователю контекстное сообщение.</span><span class="sxs-lookup"><span data-stu-id="ba2c3-190">Your app should handle any timeouts appropriately by providing a contextual message to the user.</span></span> <span data-ttu-id="ba2c3-191">Кроме того, вы можете сообщить пользователям о длительных процессах.</span><span class="sxs-lookup"><span data-stu-id="ba2c3-191">You should also user progress indicators to provide feedback to your users for any long-running processes.</span></span>
