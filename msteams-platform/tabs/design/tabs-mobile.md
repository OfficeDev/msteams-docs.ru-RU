---
title: Вкладки на мобильных устройствах
description: Описывает рекомендации по проектированию вкладок, работающих на мобильных устройствах.
keywords: рекомендации по проектированию Teams — вкладки личных приложений для мобильных устройств
ms.openlocfilehash: d47039c245b8e262af6e1f60bc0c644dc7e65bd6
ms.sourcegitcommit: e8dfcb167274e996395b77d65999991a18f2051a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/15/2020
ms.locfileid: "47819048"
---
# <a name="tabs-on-mobile"></a><span data-ttu-id="8e036-104">Вкладки на мобильных устройствах</span><span class="sxs-lookup"><span data-stu-id="8e036-104">Tabs on mobile</span></span>

> [!NOTE]
> <span data-ttu-id="8e036-105">Если вкладка канал и группа отображается в клиентах Teams для мобильных устройств, то `setSettings()` конфигурация должна иметь значение для `websiteUrl` Свойства (см. ниже).</span><span class="sxs-lookup"><span data-stu-id="8e036-105">If you choose to have your channel/group tab appear on Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property (see below).</span></span>

<span data-ttu-id="8e036-106">Настраиваемые вкладки могут быть частью канала, группового чата или личного приложения (приложения, содержащие статические вкладки и/или односторонняя робот).</span><span class="sxs-lookup"><span data-stu-id="8e036-106">Custom tabs can be part of a channel, group chat, or personal app (apps that contain static tabs and/or a one-to-one bot).</span></span>

<span data-ttu-id="8e036-107">Персональные приложения доступны на мобильных клиентах в почтовом ящике приложения.</span><span class="sxs-lookup"><span data-stu-id="8e036-107">Personal apps are available on mobile clients in the App Drawer.</span></span> <span data-ttu-id="8e036-108">Приложение можно установить только с настольного компьютера или из веб-клиента и может занимать до 24 часов на мобильных клиентах.</span><span class="sxs-lookup"><span data-stu-id="8e036-108">The app can only be installed from a desktop or web client, and can take up to 24 hours to appear on mobile clients.</span></span>

<span data-ttu-id="8e036-109">На мобильных клиентах доступны также вкладки групп и каналов.</span><span class="sxs-lookup"><span data-stu-id="8e036-109">Group and channel tabs are available on mobile clients as well.</span></span> <span data-ttu-id="8e036-110">Поведение по умолчанию в настоящее время используется `websiteUrl` для запуска вкладки в окне браузера.</span><span class="sxs-lookup"><span data-stu-id="8e036-110">The default behavior is currently to use your `websiteUrl` to launch your tab in a browser window.</span></span> <span data-ttu-id="8e036-111">Тем не менее, они могут загружаться на мобильном клиенте, если щелкнуть `...` меню переполнения рядом с вкладкой и выбрать команду **Открыть**, которая будет использовать `contentUrl` для загрузки вкладки в клиенте Teams Mobile.</span><span class="sxs-lookup"><span data-stu-id="8e036-111">However, they can be loaded on a mobile client by clicking the `...` overflow menu next to the tab and choosing **Open**, which will use your `contentUrl` to load the tab inside the Teams mobile client.</span></span>

![Мобильный ящик приложений](../../assets/images/personal-app-mobile.png)

## <a name="developer-considerations-for-mobile-support"></a><span data-ttu-id="8e036-113">Рекомендации для разработчиков для поддержки мобильных устройств</span><span class="sxs-lookup"><span data-stu-id="8e036-113">Developer considerations for mobile support</span></span>

<span data-ttu-id="8e036-114">При создании приложения, включающего вкладку, необходимо учесть (и протестировать), как эта вкладка будет работать как в клиентах Android, так и в Microsoft Teams для iOS.</span><span class="sxs-lookup"><span data-stu-id="8e036-114">When you're building an app that includes a tab, you need to consider (and test) how your tab will function on both the Android and iOS Microsoft Teams clients.</span></span> <span data-ttu-id="8e036-115">В разделах ниже представлены некоторые ключевые сценарии, которые необходимо учитывать.</span><span class="sxs-lookup"><span data-stu-id="8e036-115">The sections below outline some of the key scenarios you need to consider.</span></span>

### <a name="testing-on-mobile-clients"></a><span data-ttu-id="8e036-116">Тестирование мобильных клиентов</span><span class="sxs-lookup"><span data-stu-id="8e036-116">Testing on mobile clients</span></span>

<span data-ttu-id="8e036-117">Необходимо убедиться, что вкладка правильно функционирует на мобильных устройствах различных размеров и качеств.</span><span class="sxs-lookup"><span data-stu-id="8e036-117">You need to validate that your tab functions properly on mobile devices of various sizes and qualities.</span></span> <span data-ttu-id="8e036-118">Для устройств с Android можно использовать [девтулс](~/tabs/how-to/developer-tools.md) для отладки вкладки во время ее выполнения.</span><span class="sxs-lookup"><span data-stu-id="8e036-118">For Android devices you can use the [DevTools](~/tabs/how-to/developer-tools.md) to debug your tab while it is running.</span></span> <span data-ttu-id="8e036-119">Рекомендуется протестировать как высококачественные, так и низкие устройства, а также на планшете.</span><span class="sxs-lookup"><span data-stu-id="8e036-119">We recommend that you test on both high and low performing devices, as well as on a tablet.</span></span>

### <a name="responsive-design"></a><span data-ttu-id="8e036-120">Адаптивный дизайн</span><span class="sxs-lookup"><span data-stu-id="8e036-120">Responsive design</span></span>

<span data-ttu-id="8e036-121">Так как вкладка может быть открыта на устройствах с широким размером экрана, она должна соответствовать принципам [создания отклика](https://www.w3schools.com/html/html_responsive.asp) .</span><span class="sxs-lookup"><span data-stu-id="8e036-121">Because your tab can be opened on devices with a wide range of screen sizes, it needs to follow [responsive design](https://www.w3schools.com/html/html_responsive.asp) principles.</span></span> <span data-ttu-id="8e036-122">Все основные конструкции должны быть доступны на мобильных устройствах, и представления не должны искажаться.</span><span class="sxs-lookup"><span data-stu-id="8e036-122">All of the key constructs should be accessible on mobile devices, and the views should not be distorted.</span></span> <span data-ttu-id="8e036-123">Убедитесь, что когда вкладка загружена на мобильном устройстве, все кнопки и ссылки легко доступны с помощью навигации на основе пальца.</span><span class="sxs-lookup"><span data-stu-id="8e036-123">Ensure that when your tab is loaded on a mobile device, all buttons and links are easily accessible using finger-based navigation.</span></span>

### <a name="authentication"></a><span data-ttu-id="8e036-124">Проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="8e036-124">Authentication</span></span>

<span data-ttu-id="8e036-125">Для проверки подлинности на мобильных клиентах необходимо обновить пакет SDK Teams JS по крайней мере до версии 1.4.1.</span><span class="sxs-lookup"><span data-stu-id="8e036-125">For authentication to work on mobile clients, you must upgrade you Teams JS SDK to at least version 1.4.1.</span></span>

### <a name="low-bandwidth--intermittent-connections"></a><span data-ttu-id="8e036-126">Низкая пропускная способность & периодические подключения</span><span class="sxs-lookup"><span data-stu-id="8e036-126">Low bandwidth & intermittent connections</span></span>

<span data-ttu-id="8e036-127">Мобильным клиентам часто приходится работать с низкой пропускной способностью и периодическими подключениями.</span><span class="sxs-lookup"><span data-stu-id="8e036-127">Mobile clients regularly need to function with low bandwidth and intermittent connections.</span></span> <span data-ttu-id="8e036-128">Ваше приложение должно соответствующим образом обрабатывать все времена ожидания, предоставляя пользователю контекстное сообщение.</span><span class="sxs-lookup"><span data-stu-id="8e036-128">Your app should handle any timeouts appropriately by providing a contextual message to the user.</span></span> <span data-ttu-id="8e036-129">Кроме того, вы можете сообщить пользователям о длительных процессах.</span><span class="sxs-lookup"><span data-stu-id="8e036-129">You should also user progress indicators to provide feedback to your users for any long-running processes.</span></span>

## <a name="design-considerations-for-mobile"></a><span data-ttu-id="8e036-130">Рекомендации по проектированию для мобильных устройств</span><span class="sxs-lookup"><span data-stu-id="8e036-130">Design considerations for mobile</span></span>

<span data-ttu-id="8e036-131">Наша мобильная платформа позволяет приложениям работать с содержимым приложения, разнимая все экраны, разнимая основные возможности навигации в Teams.</span><span class="sxs-lookup"><span data-stu-id="8e036-131">Our mobile platform allows apps to be an immersive experience with the app content taking up all of the screen apart from main Teams navigation.</span></span> <span data-ttu-id="8e036-132">Чтобы создать иммерсивное приложение, которое тесно работает в клиенте Microsoft Teams, следуйте указаниям ниже.</span><span class="sxs-lookup"><span data-stu-id="8e036-132">To create an immersive experience that fits seamlessly within the Microsoft Teams client, follow the guidelines below.</span></span>

### <a name="layouts"></a><span data-ttu-id="8e036-133">макеты;</span><span class="sxs-lookup"><span data-stu-id="8e036-133">Layouts</span></span>

<span data-ttu-id="8e036-134">Важно выбрать правильный макет для вкладки.</span><span class="sxs-lookup"><span data-stu-id="8e036-134">Choosing the correct layout for your tab is important.</span></span> <span data-ttu-id="8e036-135">Следует учитывать тип данных, которые вы предоставляете, и выбирать макет, который организует его для простоты использования.</span><span class="sxs-lookup"><span data-stu-id="8e036-135">You should consider the kind of information you're presenting, and choose a layout that organizes it for easy consumption.</span></span> <span data-ttu-id="8e036-136">Ниже приведены некоторые возможные параметры.</span><span class="sxs-lookup"><span data-stu-id="8e036-136">Some potential options are outlined below.</span></span>

#### <a name="single-canvas"></a><span data-ttu-id="8e036-137">Один холст</span><span class="sxs-lookup"><span data-stu-id="8e036-137">Single canvas</span></span>

<span data-ttu-id="8e036-138">Это одна большая область, в которой выполняется работу.</span><span class="sxs-lookup"><span data-stu-id="8e036-138">This is one large area where work gets done.</span></span> <span data-ttu-id="8e036-139">Приложение Wiki соответствует этому шаблону.</span><span class="sxs-lookup"><span data-stu-id="8e036-139">The Wiki app follows this pattern.</span></span> <span data-ttu-id="8e036-140">Если у вас есть приложение, не разделяее контент на небольшие компоненты, это будет очень полезно.</span><span class="sxs-lookup"><span data-stu-id="8e036-140">If you have an app that doesn’t separate content into smaller components this would be a good fit.</span></span>

![Макет "один холст"](~/assets/images/mobile-single-canvas.png)

#### <a name="list"></a><span data-ttu-id="8e036-142">Список</span><span class="sxs-lookup"><span data-stu-id="8e036-142">List</span></span>

<span data-ttu-id="8e036-143">Списки отлично подходят для сортировки и фильтрации больших объемов данных и прекрасно подходят для наиболее важных вещей в верхней части.</span><span class="sxs-lookup"><span data-stu-id="8e036-143">Lists are great for sorting and filtering large quantities of data and are great at keeping the most important things at the top.</span></span> <span data-ttu-id="8e036-144">Рекомендуется использовать сортируемый столбцы.</span><span class="sxs-lookup"><span data-stu-id="8e036-144">It is helpful to use sortable columns.</span></span> <span data-ttu-id="8e036-145">Действия можно добавлять к каждому элементу списка в меню с многоточием.</span><span class="sxs-lookup"><span data-stu-id="8e036-145">Actions can be added to each list item under the ellipsis menu.</span></span>

![макет списка](~/assets/images/mobile-list.png)

#### <a name="grid"></a><span data-ttu-id="8e036-147">Таблице</span><span class="sxs-lookup"><span data-stu-id="8e036-147">Grid</span></span>

<span data-ttu-id="8e036-148">Сетки удобно использовать для отображения элементов, которые являются очень визуальными.</span><span class="sxs-lookup"><span data-stu-id="8e036-148">Grids are useful for showing elements which are highly visual.</span></span> <span data-ttu-id="8e036-149">В верхней части можно включить фильтр или элемент управления поиском.</span><span class="sxs-lookup"><span data-stu-id="8e036-149">It helps to include a filter or search control at the top.</span></span>

![макет сетки](~/assets/images/mobile-grid.png)

### <a name="tabs-with-bots-on-mobile"></a><span data-ttu-id="8e036-151">Вкладки с боты на мобильных устройствах</span><span class="sxs-lookup"><span data-stu-id="8e036-151">Tabs with bots on mobile</span></span>

<span data-ttu-id="8e036-152">Ниже приведен пример личного приложения, которое содержит две статические вкладки и элемент Bot.</span><span class="sxs-lookup"><span data-stu-id="8e036-152">The below is an example personal app that contains two static tabs and a bot.</span></span>

![вкладки и боты на мобильных устройствах](~/assets/images/mobile-tab-with-bot.png)

### <a name="ui-components"></a><span data-ttu-id="8e036-154">Компоненты пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="8e036-154">UI Components</span></span>

#### <a name="color-palettes"></a><span data-ttu-id="8e036-155">Цветовые палитры</span><span class="sxs-lookup"><span data-stu-id="8e036-155">Color palettes</span></span>

<span data-ttu-id="8e036-156">Использование нашей утвержденной нейтральной палитры для фоновых рисунков, уведомлений, текста и кнопок поможет вам в работе над приложением в Teams.</span><span class="sxs-lookup"><span data-stu-id="8e036-156">Using our approved neutral palette for backgrounds, notifications, text, and buttons will help your app feel more at home in Teams.</span></span> <span data-ttu-id="8e036-157">Так как в Teams есть две цветные темы (светло-и темная), рекомендуется убедиться в том, что ваше приложение отлично выглядит как.</span><span class="sxs-lookup"><span data-stu-id="8e036-157">Since Teams mobile has two colour themes (light and dark), it’s a good idea to make sure your app looks great in both.</span></span>

##### <a name="light-color"></a><span data-ttu-id="8e036-158">Светлый цвет</span><span class="sxs-lookup"><span data-stu-id="8e036-158">Light color</span></span>

![Палитра "светлый цвет"](~/assets/images/light-color.png)

##### <a name="dark-color"></a><span data-ttu-id="8e036-160">Темный цвет</span><span class="sxs-lookup"><span data-stu-id="8e036-160">Dark color</span></span>

![Темная цветовая палитра](~/assets/images/dark-color.png)

#### <a name="buttons-and-controls"></a><span data-ttu-id="8e036-162">Кнопки и элементы управления</span><span class="sxs-lookup"><span data-stu-id="8e036-162">Buttons and controls</span></span>

<span data-ttu-id="8e036-163">Способ оформления кнопок позволяет сообщить, какие действия они вызывают.</span><span class="sxs-lookup"><span data-stu-id="8e036-163">The way buttons are styled helps communicate what kind of action they trigger.</span></span> <span data-ttu-id="8e036-164">Мы поддерживаем широкий спектр кнопок, отформатированных для отображения различных уровней выделения.</span><span class="sxs-lookup"><span data-stu-id="8e036-164">We maintain a wide range of buttons that are formatted to show different levels of emphasis.</span></span> <span data-ttu-id="8e036-165">У кнопок может быть текст, значок или комбинация текста и значок.</span><span class="sxs-lookup"><span data-stu-id="8e036-165">Buttons can have text, an icon, or a combination of text and an icon.</span></span> <span data-ttu-id="8e036-166">Для связи разных уровней в иерархии мы разработали основные и дополнительные кнопки в каждой категории.</span><span class="sxs-lookup"><span data-stu-id="8e036-166">To communicate different levels in a hierarchy, we designed primary and secondary buttons within each category.</span></span>

![изображение кнопок](~/assets/images/buttons.png)

![элементы управления выбором](~/assets/images/selection-controls.png)

![чиклетс и пиллс](~/assets/images/chiclets-and-pills.png)

#### <a name="typography"></a><span data-ttu-id="8e036-170">Шрифтовое оформление</span><span class="sxs-lookup"><span data-stu-id="8e036-170">Typography</span></span>

<span data-ttu-id="8e036-171">Оформление должно быть ясным и пурпосефулм.</span><span class="sxs-lookup"><span data-stu-id="8e036-171">Typography should be clear and purposeful.</span></span> <span data-ttu-id="8e036-172">Обратите внимание на важную информацию и Избегайте использования нескольких шрифтов и размеров для сокращения путаницы.</span><span class="sxs-lookup"><span data-stu-id="8e036-172">Emphasize important information and avoid using multiple fonts and sizes to reduce confusion.</span></span> <span data-ttu-id="8e036-173">Рекомендуется использовать регистр предложений и избегать использования всех политик для локализации и разборчивости.</span><span class="sxs-lookup"><span data-stu-id="8e036-173">We recommend using sentence case and avoiding the usage of all caps for localization and legibility.</span></span>

![Мобильные типограф](~/assets/images/mobile-typography.png)

#### <a name="fields-and-flyouts"></a><span data-ttu-id="8e036-175">Поля и всплывающие окна</span><span class="sxs-lookup"><span data-stu-id="8e036-175">Fields and Flyouts</span></span>

<span data-ttu-id="8e036-176">Поля — это области, в которых пользователи могут вводить текст.</span><span class="sxs-lookup"><span data-stu-id="8e036-176">Fields are areas where users can input text.</span></span> <span data-ttu-id="8e036-177">Всплывающие окна являются более легковесными, чем диалоговые окна, и отображаются в верхней области.</span><span class="sxs-lookup"><span data-stu-id="8e036-177">Flyouts are more lightweight than dialogs, and appear from the top pane.</span></span>

##### <a name="list-controls"></a><span data-ttu-id="8e036-178">Список элементов управления</span><span class="sxs-lookup"><span data-stu-id="8e036-178">List controls</span></span>

![элементы управления списком для мобильных устройств](~/assets/images/mobile-list-controls.png)

##### <a name="field-controls"></a><span data-ttu-id="8e036-180">Элементы управления полями</span><span class="sxs-lookup"><span data-stu-id="8e036-180">Field controls</span></span>

![Мобильные элементы управления поля](~/assets/images/mobile-field-controls.png)
