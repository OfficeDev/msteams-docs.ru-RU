---
title: Рекомендации по проектированию вкладок
description: Описывает рекомендации по созданию вкладок для контента и совместной работы
keywords: рекомендации по проектированию Teams Справочник по настройке вкладки канала конфигурации статическая вкладка простая вкладка проектирование групп
ms.openlocfilehash: 2d4e809e3ac11a5742113bf65125848a922c0207
ms.sourcegitcommit: 50571f5c6afc86177c4fe1032fe13366a7b706dd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/04/2020
ms.locfileid: "49576864"
---
# <a name="content-and-conversations-all-at-once-using-tabs"></a><span data-ttu-id="9480d-104">Контент и беседы, все сразу с помощью вкладок</span><span class="sxs-lookup"><span data-stu-id="9480d-104">Content and conversations, all at once using tabs</span></span>

> [!Important]
> <span data-ttu-id="9480d-105">**Вкладки на мобильных клиентах**</span><span class="sxs-lookup"><span data-stu-id="9480d-105">**Tabs on Mobile Clients**</span></span>
>
> <span data-ttu-id="9480d-106">Следуйте [указаниям для вкладок на странице Mobile](./tabs-mobile.md) при создании вкладок.</span><span class="sxs-lookup"><span data-stu-id="9480d-106">Follow the [guidance for tabs on mobile](./tabs-mobile.md) when creating your tabs.</span></span> <span data-ttu-id="9480d-107">Если вкладка использует проверку подлинности, необходимо обновить пакет SDK для Teams для Teams до версии 1.4.1 или более поздней, иначе проверка подлинности завершится неуспешно.</span><span class="sxs-lookup"><span data-stu-id="9480d-107">If your tab uses authentication, you must upgrade your Teams JavaScript SDK to version 1.4.1 or later, or authentication will fail.</span></span>
>
> <span data-ttu-id="9480d-108">**Вкладки каналов и групп (настраиваемых) на мобильных устройствах:**</span><span class="sxs-lookup"><span data-stu-id="9480d-108">**Channel/group (configurable) tabs on mobile:**</span></span>
>
> * <span data-ttu-id="9480d-109">Мобильные клиенты показывают только настраиваемые вкладки со значением `websiteUrl` .</span><span class="sxs-lookup"><span data-stu-id="9480d-109">Mobile clients only show configurable tabs that have a value for `websiteUrl`.</span></span> <span data-ttu-id="9480d-110">Если вы хотите, чтобы вкладка отображалась в клиентах Teams для мобильных устройств, необходимо задать значение `websiteUrl` .</span><span class="sxs-lookup"><span data-stu-id="9480d-110">If you want your tab to appear on the Teams mobile clients, you must set the value of `websiteUrl`.</span></span>
> * <span data-ttu-id="9480d-111">Поведение по умолчанию при открытии на мобильном устройстве можно открыть снаружи в браузере с помощью `websiteUrl` .</span><span class="sxs-lookup"><span data-stu-id="9480d-111">Default open behavior on mobile is to open outside in browser using the `websiteUrl`.</span></span> <span data-ttu-id="9480d-112">Для приложений, опубликованных в магазине общедоступных приложений, если вы хотите, чтобы вкладка каналы открывалась внутри Teams по умолчанию, следуйте [указаниям по использованию вкладок на мобильном устройстве](~/tabs/design/tabs-mobile.md), чтобы получить доступ к внесены.</span><span class="sxs-lookup"><span data-stu-id="9480d-112">For apps published to the public App Store, if you want your channel tab to open inside teams by default, follow the [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md), and reach out to your support rep to request to be whitelisted.</span></span>

<span data-ttu-id="9480d-113">Вкладки — это холсты, которые можно использовать для обмена контентом, удержания бесед и размещения сторонних служб в рабочем процессе.</span><span class="sxs-lookup"><span data-stu-id="9480d-113">Tabs are canvases that you can use to share content, hold conversations, and host third-party services, all within a team’s organic workflow.</span></span> <span data-ttu-id="9480d-114">Когда вы создаете вкладку в Microsoft Teams, он помещает веб-приложение спереди и в центре, где оно легко доступно из ключевых бесед.</span><span class="sxs-lookup"><span data-stu-id="9480d-114">When you build a tab in Microsoft Teams, it puts your web app front and center where it’s easily accessible from key conversations.</span></span>

## <a name="guidelines"></a><span data-ttu-id="9480d-115">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="9480d-115">Guidelines</span></span>

<span data-ttu-id="9480d-116">На хорошей вкладке должны отображаться следующие характеристики:</span><span class="sxs-lookup"><span data-stu-id="9480d-116">A good tab should display the following characteristics:</span></span>

### <a name="focused-functionality"></a><span data-ttu-id="9480d-117">Ориентированные функциональные возможности</span><span class="sxs-lookup"><span data-stu-id="9480d-117">Focused functionality</span></span>

<span data-ttu-id="9480d-118">Вкладки лучше подходят для конкретных нужд.</span><span class="sxs-lookup"><span data-stu-id="9480d-118">Tabs work best when they’re built to address a specific need.</span></span> <span data-ttu-id="9480d-119">Сосредоточьтесь на небольшом наборе задач или подмножестве данных, относящихся к каналу, в котором находится вкладка.</span><span class="sxs-lookup"><span data-stu-id="9480d-119">Focus on a small set of tasks or a subset of data that’s relevant to the channel the tab is in.</span></span>

### <a name="reduced-chrome"></a><span data-ttu-id="9480d-120">Сокращенный хром</span><span class="sxs-lookup"><span data-stu-id="9480d-120">Reduced chrome</span></span>

<span data-ttu-id="9480d-121">Избегайте создания нескольких панелей на вкладке, добавления слоев навигации или необходимости прокручивать их по вертикали и горизонтали на одной вкладке. Другими словами, старайтесь не использовать вкладки на вкладке.</span><span class="sxs-lookup"><span data-stu-id="9480d-121">Avoid creating multiple panels in a tab, adding layers of navigation, or requiring users to scroll both vertically and horizontally in one tab. In other words, try not to have tabs in your tab.</span></span>

### <a name="integration"></a><span data-ttu-id="9480d-122">Интеграция</span><span class="sxs-lookup"><span data-stu-id="9480d-122">Integration</span></span>

<span data-ttu-id="9480d-123">Узнайте, как уведомлять пользователей об активности вкладок путем отправки [адаптивных карточек](../../task-modules-and-cards/what-are-cards.md#adaptive-cards) в беседу.</span><span class="sxs-lookup"><span data-stu-id="9480d-123">Find ways to notify users about tab activity by posting [adaptive cards](../../task-modules-and-cards/what-are-cards.md#adaptive-cards) to a conversation.</span></span>

### <a name="conversational"></a><span data-ttu-id="9480d-124">Разговорному</span><span class="sxs-lookup"><span data-stu-id="9480d-124">Conversational</span></span>

<span data-ttu-id="9480d-125">Найдите способ для упрощения общения вокруг вкладки. Это гарантирует, что центр бесед на содержании, данные или процесс в любой момент.</span><span class="sxs-lookup"><span data-stu-id="9480d-125">Find a way to facilitate conversation around a tab. This ensures that conversations center on the content, data, or process at hand.</span></span>

### <a name="streamlined-access"></a><span data-ttu-id="9480d-126">Упрощенный доступ</span><span class="sxs-lookup"><span data-stu-id="9480d-126">Streamlined access</span></span>

<span data-ttu-id="9480d-127">Убедитесь, что вы предоставляете доступ к нужным людям в нужное время.</span><span class="sxs-lookup"><span data-stu-id="9480d-127">Make sure you’re granting access to the right people at the right time.</span></span> <span data-ttu-id="9480d-128">Сохранение процесса входа в систему не позволит создавать барьеры для участия и совместной работы.</span><span class="sxs-lookup"><span data-stu-id="9480d-128">Keeping your sign-in process simple will avoid creating barriers to contribution and collaboration.</span></span>

### <a name="responsiveness-to-window-sizing"></a><span data-ttu-id="9480d-129">Скорость отклика при изменении размера окна</span><span class="sxs-lookup"><span data-stu-id="9480d-129">Responsiveness to window sizing</span></span>

<span data-ttu-id="9480d-130">Teams можно использовать в размерах окон как небольшие 720px, поэтому убедитесь, что вкладка используется в небольшом окне так же, как и удобство при высоком разрешении.</span><span class="sxs-lookup"><span data-stu-id="9480d-130">Teams can be used in window sizes as small as 720px, so making sure that a tab is usable in a small window is just as important as usability at very high resolutions.</span></span>

### <a name="flat-navigation"></a><span data-ttu-id="9480d-131">Плоская Навигация</span><span class="sxs-lookup"><span data-stu-id="9480d-131">Flat navigation</span></span>

<span data-ttu-id="9480d-132">Мы просим разработчиков не добавлять на вкладки весь портал. Хранение сравнительно плоской структуры помогает поддерживать более простую модель беседы.</span><span class="sxs-lookup"><span data-stu-id="9480d-132">We ask developers not to add their entire portal to a tab. Keeping the navigation relatively flat helps maintain a simpler conversational model.</span></span> <span data-ttu-id="9480d-133">Другими словами, беседа представляет собой список вещей, таких как рассмотренные рабочие элементы, или одна вещь, например Spec.</span><span class="sxs-lookup"><span data-stu-id="9480d-133">In other words, the conversation is about a list of things, such as triaged work items, or a single thing, like a spec.</span></span>

<span data-ttu-id="9480d-134">В цепочке обсуждений есть проблемы, связанные с навигацией с углубленной иерархией навигации.</span><span class="sxs-lookup"><span data-stu-id="9480d-134">There are inherent navigational challenges with deep navigation hierarchy, within threaded conversations.</span></span> <span data-ttu-id="9480d-135">Для оптимального взаимодействия с пользователем вы можете сохранить навигацию на вкладке по меньшей мере и иметь следующий вид:</span><span class="sxs-lookup"><span data-stu-id="9480d-135">For the best user experience, your tab navigation should be kept to a minimum and be designed as follows:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="9480d-136">**Открывает модуль задачи, такой как отдельный рабочий элемент или сущность**.</span><span class="sxs-lookup"><span data-stu-id="9480d-136">**Opens a task module such as an individual work item or entity**.</span></span> <span data-ttu-id="9480d-137">Это исключает возможность полностью отменять чат и является лучшим вариантом, чтобы отследить обсуждение вкладки, а не вложенных сущностей или возможностей редактирования.</span><span class="sxs-lookup"><span data-stu-id="9480d-137">This precludes chat entirely and is the best option to keep chat specifically about the tab and not the sub-entities or editing experiences.</span></span>
>* <span data-ttu-id="9480d-138">**Открывает псевдо диалоговое окно в IFRAME**.</span><span class="sxs-lookup"><span data-stu-id="9480d-138">**Opens a pseudo dialog in an iframe**.</span></span> <span data-ttu-id="9480d-139">При использовании с экранным фоном рекомендуется использовать более светлый цвет, а не темный.</span><span class="sxs-lookup"><span data-stu-id="9480d-139">If used with a screened background we recommend using the lighter color rather than the dark.</span></span> <span data-ttu-id="9480d-140">`app-gray-10 at 30%`Прозрачность работает хорошо.</span><span class="sxs-lookup"><span data-stu-id="9480d-140">The `app-gray-10 at 30%` transparency works well.</span></span>
>* <span data-ttu-id="9480d-141">**Открывает страницу браузера**.</span><span class="sxs-lookup"><span data-stu-id="9480d-141">**Opens a browser page**.</span></span>

### <a name="personality"></a><span data-ttu-id="9480d-142">Индивидуальные</span><span class="sxs-lookup"><span data-stu-id="9480d-142">Personality</span></span>

<span data-ttu-id="9480d-143">На холсте вкладок можно получить прекрасную возможность для фирменного стиля работы.</span><span class="sxs-lookup"><span data-stu-id="9480d-143">Your tab canvas presents a great opportunity to brand your experience.</span></span> <span data-ttu-id="9480d-144">Ваш логотип является важной частью вашего удостоверения и подключения к вашим пользователям. Убедитесь, что он должен быть включен:</span><span class="sxs-lookup"><span data-stu-id="9480d-144">Your logo is an important part of your identity and connection with your users., so be sure to include it:</span></span>

> [!div class="checklist"]
>
>* <span data-ttu-id="9480d-145">Размещение логотипа в левом или правом углу или вдоль нижнего края</span><span class="sxs-lookup"><span data-stu-id="9480d-145">Place your logo in the left or right corner or along the bottom edge</span></span>
> * <span data-ttu-id="9480d-146">Хранение и ненавязчивая эмблема</span><span class="sxs-lookup"><span data-stu-id="9480d-146">Keep your logo small and unobtrusive</span></span>

<span data-ttu-id="9480d-147">Включение собственных цветов и макетов твилл также помогает в общении.</span><span class="sxs-lookup"><span data-stu-id="9480d-147">Incorporating your own colors and layouts twill also aid in communicating personality.</span></span>

> [!TIP]
> <span data-ttu-id="9480d-148">Используйте наш стиль оформления, чтобы ваша служба работала как часть Teams.</span><span class="sxs-lookup"><span data-stu-id="9480d-148">Please work with our visual style so your service feels like a part of Teams.</span></span> <span data-ttu-id="9480d-149">*Просмотреть*, например, [цвета Teams](../../concepts/design/components/color.md)</span><span class="sxs-lookup"><span data-stu-id="9480d-149">*See*, for example [Teams Colors](../../concepts/design/components/color.md)</span></span>

---

## <a name="tab-layouts"></a><span data-ttu-id="9480d-150">Макеты вкладок</span><span class="sxs-lookup"><span data-stu-id="9480d-150">Tab layouts</span></span>

[!INCLUDE [Tab layouts](../../includes/design/tab-layouts.html)]

---

## <a name="types-of-tabs"></a><span data-ttu-id="9480d-151">Типы вкладок</span><span class="sxs-lookup"><span data-stu-id="9480d-151">Types of tabs</span></span>

[!INCLUDE [Tab types](../../includes/design/tab-types.html)]

---

## <a name="configuration-page-height"></a><span data-ttu-id="9480d-152">Высота страницы конфигурации</span><span class="sxs-lookup"><span data-stu-id="9480d-152">Configuration page height</span></span>

>[!IMPORTANT]
><span data-ttu-id="9480d-153">В сентябре 2018 высота [страницы настройки](~/tabs/how-to/create-tab-pages/configuration-page.md) вкладки была увеличена, а ширина осталась неизменной.</span><span class="sxs-lookup"><span data-stu-id="9480d-153">In September 2018, the height for the tab [configuration page](~/tabs/how-to/create-tab-pages/configuration-page.md) was increased while the width remained unchanged.</span></span> <span data-ttu-id="9480d-154">Если ваше приложение предназначено для устаревшего размера вкладки, на странице Конфигурация вкладки будет много вертикальных пробелов.</span><span class="sxs-lookup"><span data-stu-id="9480d-154">If your app is designed for the older size your tab configuration page will have a great deal of vertical whitespace.</span></span> <span data-ttu-id="9480d-155">Устаревшие приложения хранилища, исключенные из этого изменения, должны обратиться в корпорацию Майкрософт после обновления, чтобы вместить новые измерения.</span><span class="sxs-lookup"><span data-stu-id="9480d-155">Legacy store apps exempted from this change will need to contact Microsoft after updating to accommodate the new dimensions.</span></span>

<span data-ttu-id="9480d-156">Размеры страницы настройки вкладки:</span><span class="sxs-lookup"><span data-stu-id="9480d-156">The dimensions of the tab configuration page:</span></span>


<img width="450px" title="Размеры для вкладок конфигурации" src="~/assets/images/tabs/config-dialog-Contoso2.png" alt="sizes for config tabs" />


### <a name="guidelines-for-tab-configuration-page-format"></a><span data-ttu-id="9480d-158">Рекомендации по формату страницы настройки вкладки</span><span class="sxs-lookup"><span data-stu-id="9480d-158">Guidelines for tab configuration page format</span></span>

* <span data-ttu-id="9480d-159">Основа минимальной высоты области контента на странице настройки вкладки для графических элементов с фиксированной высотой.</span><span class="sxs-lookup"><span data-stu-id="9480d-159">Base the minimum height of your content area of your tab configuration page on fixed-height graphic elements.</span></span>
* <span data-ttu-id="9480d-160">Рассчитайте доступное вертикальное пространство (высоту области контента на странице Конфигурация) с помощью `window.innerHeight` .</span><span class="sxs-lookup"><span data-stu-id="9480d-160">Calculate available vertical space (the height of the content area in the configuration page) using `window.innerHeight`.</span></span> <span data-ttu-id="9480d-161">При этом возвращается размер `<iframe>` страницы конфигурации, в которой размещается страница конфигурации, которая может измениться в будущих выпусках.</span><span class="sxs-lookup"><span data-stu-id="9480d-161">This returns the size of the `<iframe>` in which your configuration page resides, which may change in future releases.</span></span> <span data-ttu-id="9480d-162">При использовании этого значения контент будет автоматически скорректирован до будущих изменений.</span><span class="sxs-lookup"><span data-stu-id="9480d-162">By using this value your content will adjust automatically to future changes.</span></span>
* <span data-ttu-id="9480d-163">Выделение вертикального пространства для элементов переменной высоты за вычетом того, что требуется для элементов фиксированной высоты.</span><span class="sxs-lookup"><span data-stu-id="9480d-163">Allocate vertical space to the variable-height elements minus what's needed for the fixed-height elements.</span></span>
* <span data-ttu-id="9480d-164">Для состояния *входа* по вертикали и горизонтали по центру содержимого.</span><span class="sxs-lookup"><span data-stu-id="9480d-164">For the *login* state, vertically and horizontally center the content.</span></span>
* <span data-ttu-id="9480d-165">Если вы хотите использовать фоновое изображение, вам потребуется новое изображение, в соответствии с областью (предпочтительный), или можно оставить одно и то же изображение и выбрать один из следующих вариантов:</span><span class="sxs-lookup"><span data-stu-id="9480d-165">If you want a background image, you need either a new image, sized to fit the area (preferred), or you can keep the same image and choose between:</span></span>
  * <span data-ttu-id="9480d-166">Выравнивание по верхнему левому углу.</span><span class="sxs-lookup"><span data-stu-id="9480d-166">aligning to the upper left hand corner.</span></span>
  * <span data-ttu-id="9480d-167">масштабирование изображения по размеру.</span><span class="sxs-lookup"><span data-stu-id="9480d-167">scaling the image to fit.</span></span>

<span data-ttu-id="9480d-168">При правильном изменении размера страница настройки вкладки должна выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9480d-168">When properly sized, your tab configuration page should look similar to this:</span></span>

<img width="450px" title="Вкладка "Новая конфигурация"" src="~/assets/images/tabs/config-dialog-Contoso.png" alt="new config tab"/>

## <a name="best-practices"></a><span data-ttu-id="9480d-170">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="9480d-170">Best practices</span></span>

### <a name="always-include-a-default-state"></a><span data-ttu-id="9480d-171">Всегда включать состояние по умолчанию</span><span class="sxs-lookup"><span data-stu-id="9480d-171">Always include a default state</span></span>

<span data-ttu-id="9480d-172">Включите состояние по умолчанию, чтобы упростить настройку вкладок, даже если вкладка настраиваемая.</span><span class="sxs-lookup"><span data-stu-id="9480d-172">Include a default state to make tabs easy to set up even if your tab is configurable.</span></span>

### <a name="deep-linking"></a><span data-ttu-id="9480d-173">Глубокая компоновка</span><span class="sxs-lookup"><span data-stu-id="9480d-173">Deep linking</span></span>

<span data-ttu-id="9480d-174">По мере возможности карточки и боты должны иметь глубокую ссылку на Расширенные данные на вкладке размещения. Например, карточка может показывать сводную информацию об ошибках, но при щелчке она может отобразить всю ошибку на вкладке.</span><span class="sxs-lookup"><span data-stu-id="9480d-174">Whenever possible, cards and bots should deep link to richer data in a hosted tab. For example, a card may show a summary of bug data, but clicking it can shows the entire bug in a tab.</span></span>

### <a name="naming"></a><span data-ttu-id="9480d-175">Переименовывает</span><span class="sxs-lookup"><span data-stu-id="9480d-175">Naming</span></span>

<span data-ttu-id="9480d-176">Во многих случаях имя приложения будет иметь отличное название вкладки.</span><span class="sxs-lookup"><span data-stu-id="9480d-176">In many cases, the name of your app will make a great tab name.</span></span> <span data-ttu-id="9480d-177">Кроме того, рекомендуется называть вкладки в соответствии с функциями, которые они предоставляют.</span><span class="sxs-lookup"><span data-stu-id="9480d-177">But, also consider naming your tabs according to the functionality they provide.</span></span>

### <a name="multi-window"></a><span data-ttu-id="9480d-178">Несколько окон</span><span class="sxs-lookup"><span data-stu-id="9480d-178">Multi-window</span></span>

<span data-ttu-id="9480d-179">Вкладки каналов с сложными возможностями редактирования должны открыть представление редактора в нескольких окнах, а не на вкладке.</span><span class="sxs-lookup"><span data-stu-id="9480d-179">Channel tabs that have complex editing capabilities must open the editor view in multi-window rather than a tab.</span></span>

### <a name="no-horizontal-scrolling"></a><span data-ttu-id="9480d-180">Без горизонтальной прокрутки</span><span class="sxs-lookup"><span data-stu-id="9480d-180">No horizontal scrolling</span></span>

<span data-ttu-id="9480d-181">На вкладке не должно быть горизонтальной прокрутки.</span><span class="sxs-lookup"><span data-stu-id="9480d-181">Tab should not have horizontal scrolling.</span></span>

### <a name="easy-navigation"></a><span data-ttu-id="9480d-182">Простая навигация</span><span class="sxs-lookup"><span data-stu-id="9480d-182">Easy navigation</span></span>

<span data-ttu-id="9480d-183">Переход внутри приложения-вкладки должен быть легко выполняться, например, при необходимости или в следующих страницах:</span><span class="sxs-lookup"><span data-stu-id="9480d-183">Navigation inside a tab app must be easy to follow i.e. pages have the following where necessary/applicable:</span></span>
* <span data-ttu-id="9480d-184">Кнопки "назад"</span><span class="sxs-lookup"><span data-stu-id="9480d-184">Back buttons</span></span>
* <span data-ttu-id="9480d-185">Заголовки страниц</span><span class="sxs-lookup"><span data-stu-id="9480d-185">Page headers</span></span>
* <span data-ttu-id="9480d-186">Иерархическая навигация</span><span class="sxs-lookup"><span data-stu-id="9480d-186">Breadcrumbs</span></span>
* <span data-ttu-id="9480d-187">Меню "гамбургер"</span><span class="sxs-lookup"><span data-stu-id="9480d-187">Hamburger menus</span></span>

### <a name="undo-last-action"></a><span data-ttu-id="9480d-188">Отмена последнего действия</span><span class="sxs-lookup"><span data-stu-id="9480d-188">Undo last action</span></span>

<span data-ttu-id="9480d-189">Пользователь должен иметь возможность отменить последнее действие в приложении.</span><span class="sxs-lookup"><span data-stu-id="9480d-189">User must be able to undo their last action in the app.</span></span>

### <a name="share-content"></a><span data-ttu-id="9480d-190">Общий доступ к контенту</span><span class="sxs-lookup"><span data-stu-id="9480d-190">Share content</span></span>

<span data-ttu-id="9480d-191">Персональные приложения должны позволять пользователям обмениваться контентом из личного приложения с другими участниками группы.</span><span class="sxs-lookup"><span data-stu-id="9480d-191">Personal apps should enable users to share content from a personal app experience with other team members.</span></span> <span data-ttu-id="9480d-192">Вкладка канал должна обеспечивать навигацию, дополняющую главную навигацию по командам, а не конфликтующую с ней (например, направляющие левой панели навигации).</span><span class="sxs-lookup"><span data-stu-id="9480d-192">Channel tab must provide navigation that complements the main Teams navigation, rather than conflicting with it (such as left rail nav-bars).</span></span>

### <a name="single-view"></a><span data-ttu-id="9480d-193">Одно представление</span><span class="sxs-lookup"><span data-stu-id="9480d-193">Single view</span></span>

<span data-ttu-id="9480d-194">Персональные приложения должны представлять контент из экземпляров этого приложения группы или группового чата в отдельном представлении, например, пользователь Trello должен иметь возможность просматривать все экземпляры системных плат Trello, которые они участвуют на уровне команды в личном приложении.</span><span class="sxs-lookup"><span data-stu-id="9480d-194">Personal apps should present content from team or group chat scoped instances of that app in a single view, e.g., a Trello user should be able to see all instances of Trello boards they participate in at a team level in their personal app.</span></span>

### <a name="no-app-bar"></a><span data-ttu-id="9480d-195">Нет панели приложений</span><span class="sxs-lookup"><span data-stu-id="9480d-195">No app bar</span></span>

<span data-ttu-id="9480d-196">Вкладки не должны предоставлять панель приложения со значками в левой границе, которые конфликтуют с навигацией по основным командам Teams.</span><span class="sxs-lookup"><span data-stu-id="9480d-196">Tabs should not provide an app bar with icons in the left rail that conflicts with the main Teams navigation.</span></span>

### <a name="navigation"></a><span data-ttu-id="9480d-197">Навигация</span><span class="sxs-lookup"><span data-stu-id="9480d-197">Navigation</span></span>

<span data-ttu-id="9480d-198">На вкладках не должно быть более 3 уровней навигации в приложении.</span><span class="sxs-lookup"><span data-stu-id="9480d-198">Tabs should not have more than 3 levels of navigation within the app.</span></span>

### <a name="l2l3-view"></a><span data-ttu-id="9480d-199">Представление L2/L3</span><span class="sxs-lookup"><span data-stu-id="9480d-199">L2/L3 view</span></span>

<span data-ttu-id="9480d-200">Вторичные и третичные страницы на вкладке должны быть открыты в представлении L2/L3 в основной области вкладок, которая переходит по адресной строке.</span><span class="sxs-lookup"><span data-stu-id="9480d-200">Secondary and tertiary pages in a tab should be opened in an L2/L3 view in the main tab area that is navigated via the breadcrumb.</span></span>

### <a name="no-link-to-external-browser"></a><span data-ttu-id="9480d-201">Нет ссылки на внешний браузер</span><span class="sxs-lookup"><span data-stu-id="9480d-201">No link to external browser</span></span>

<span data-ttu-id="9480d-202">Конечные объекты ссылок на вкладках не должны ссылаться на внешний браузер, но должны ссылаться на элементы div, содержащиеся в Teams.</span><span class="sxs-lookup"><span data-stu-id="9480d-202">Link targets in tabs should not link to an external browser but should link to div elements contained within Teams.</span></span> <span data-ttu-id="9480d-203">Например, внутри модулей задач, вкладок и т. д.</span><span class="sxs-lookup"><span data-stu-id="9480d-203">For example, inside task Modules, tabs, etc.</span></span>

## <a name="notifications-for-tabs"></a><span data-ttu-id="9480d-204">Уведомления для вкладок</span><span class="sxs-lookup"><span data-stu-id="9480d-204">Notifications for tabs</span></span>

<span data-ttu-id="9480d-205">Существует два режима уведомления об изменениях содержимого на вкладке:</span><span class="sxs-lookup"><span data-stu-id="9480d-205">There are two modes of notification for tab content changes:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="9480d-206">**Использование API приложений для уведомления пользователей об изменениях**.</span><span class="sxs-lookup"><span data-stu-id="9480d-206">**Use the app API to notify users of changes**.</span></span> <span data-ttu-id="9480d-207">Это сообщение будет отображаться в веб-канале активности пользователя и имеет глубокую ссылку на вкладку. *Дополнительные*  [ссылки на материалы и функции в Microsoft Teams](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true )</span><span class="sxs-lookup"><span data-stu-id="9480d-207">This message will show up in the user’s activity feed and deep link to the tab. *See*  [Create deep links to content and features in Microsoft Teams](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true )</span></span>

> * <span data-ttu-id="9480d-208">**Использование ленты**.</span><span class="sxs-lookup"><span data-stu-id="9480d-208">**Use a bot**.</span></span> <span data-ttu-id="9480d-209">Этот метод является предпочтительным, особенно если выбран целевой поток вкладок.</span><span class="sxs-lookup"><span data-stu-id="9480d-209">This method is preferred especially if the Tab thread is targeted.</span></span> <span data-ttu-id="9480d-210">В результате цепочка вкладок будет перемещена в представление "недавно активные".</span><span class="sxs-lookup"><span data-stu-id="9480d-210">The result will be that the tab’s threaded conversation will be moved into view as recently active.</span></span> <span data-ttu-id="9480d-211">Этот метод также позволяет использовать некоторые сложности при отправке уведомления.</span><span class="sxs-lookup"><span data-stu-id="9480d-211">This method also allows for some sophistication in how the notification is sent.</span></span>

<span data-ttu-id="9480d-212">При отправке сообщения в поток вкладок увеличивается осведомленность о действиях для всех пользователей без явного уведомления всех.</span><span class="sxs-lookup"><span data-stu-id="9480d-212">Sending a message to a tab thread increases the awareness of activity to all users without explicitly notifying everyone.</span></span> <span data-ttu-id="9480d-213">Это относится без шума.</span><span class="sxs-lookup"><span data-stu-id="9480d-213">This is awareness without noise.</span></span> <span data-ttu-id="9480d-214">Кроме того, если `@mention`  для определенных пользователей одно и то же уведомление будет размещаться в своем канале, то детально привязать их к потоку вкладок напрямую.</span><span class="sxs-lookup"><span data-stu-id="9480d-214">In addition, when you `@mention`  specific users the same notification will be placed in their feed, deep linking them to the tab thread directly.</span></span>

### <a name="tab-design-best-practices"></a><span data-ttu-id="9480d-215">Рекомендации по проектированию вкладок</span><span class="sxs-lookup"><span data-stu-id="9480d-215">Tab design best practices</span></span>

* <span data-ttu-id="9480d-216">Вкладки личных и статических элементов должны позволять пользователям предоставлять общий доступ к содержимому личных приложений с другими участниками группы.</span><span class="sxs-lookup"><span data-stu-id="9480d-216">Personal/Static tabs should enable users to share content from a personal app experience with another team members.</span></span>
* <span data-ttu-id="9480d-217">На вкладках "личные/статические" могут отображаться данные из экземпляров этого приложения группы или группового чата в едином представлении.</span><span class="sxs-lookup"><span data-stu-id="9480d-217">Personal/Static tabs may present content from team or group chat scoped instances of that app in a single view.</span></span>
* <span data-ttu-id="9480d-218">Конечные объекты ссылок на вкладках не должны ссылаться на внешний браузер, но должны ссылаться на элементы div, содержащиеся в командах (например, внутри, модулей задач, вкладках и т. д.).</span><span class="sxs-lookup"><span data-stu-id="9480d-218">Link targets in tabs should not link to an external browser but should link to div elements contained within Teams (example-inside, task modules, tabs, etc).</span></span>
* <span data-ttu-id="9480d-219">Вкладки должны отвечать на темы команды.</span><span class="sxs-lookup"><span data-stu-id="9480d-219">Tabs should be responsive to Team’s themes.</span></span> <span data-ttu-id="9480d-220">Когда тема Teams изменяется, тема в приложении также должна измениться в соответствии с темой.</span><span class="sxs-lookup"><span data-stu-id="9480d-220">When the Teams theme is changed, the theme within the app should also change to reflect that theme.</span></span>
* <span data-ttu-id="9480d-221">На вкладках должны использоваться компоненты с стилем Teams, где это возможно.</span><span class="sxs-lookup"><span data-stu-id="9480d-221">Tabs should use Teams-styled components where possible.</span></span> <span data-ttu-id="9480d-222">Это означает внедрение шрифтов в Teams, ввод пандусов, цветовых палитр, системы сетки, движения, тона голоса и т. д.</span><span class="sxs-lookup"><span data-stu-id="9480d-222">It means adopting Teams fonts, type ramps, color palettes, grid system, motion, tone of voice, etc.</span></span>
* <span data-ttu-id="9480d-223">Вкладки должны использовать поведение взаимодействия в Teams для навигации на странице, положения и использования диалоговых окон, информационных иерархий и т. д.</span><span class="sxs-lookup"><span data-stu-id="9480d-223">Tabs should use Teams interaction behaviors for in-page navigation, position, and use of dialogs, information hierarchies, etc.</span></span>
* <span data-ttu-id="9480d-224">На вкладках должно использоваться стандартное меню гамбургера Teams и/или строка навигации для навигации в приложении.</span><span class="sxs-lookup"><span data-stu-id="9480d-224">Tabs should use the standard Teams hamburger menu and/or breadcrumb for in-app navigation.</span></span> <span data-ttu-id="9480d-225">Вкладки не должны предоставлять панель приложения со значками в левой границе, которые конфликтуют с навигацией по основным командам Teams.</span><span class="sxs-lookup"><span data-stu-id="9480d-225">Tabs should not provide an app bar with icons in the left rail that conflicts with the main Teams navigation.</span></span>
* <span data-ttu-id="9480d-226">На вкладках не должно быть более трех уровней навигации в приложении.</span><span class="sxs-lookup"><span data-stu-id="9480d-226">Tabs should not have more than three levels of navigation within the app.</span></span>
* <span data-ttu-id="9480d-227">Вторичные и третичные страницы на вкладке должны быть открыты в представлении L2/L3 в основной области вкладок, которая переходит по адресной строке.</span><span class="sxs-lookup"><span data-stu-id="9480d-227">Secondary and tertiary pages in a tab should be opened in an L2/L3 view in the main tab area that is navigated via the breadcrumb.</span></span>
* <span data-ttu-id="9480d-228">Вкладки с сложными возможностями редактирования в приложении должны открыть представление редактора в нескольких окнах, а не вкладках (для настольных компьютеров и веб-сайта).</span><span class="sxs-lookup"><span data-stu-id="9480d-228">Tabs that have complex editing capabilities within the app should open the editor view in multi-window rather than a tab (for desktop and web).</span></span>
* <span data-ttu-id="9480d-229">Для улучшения качества взаимодействия с пользователем можно добавить персональный робот, который отправляет пользователю приветственное сообщение при первом запуске и реагирует на команды **Hi**, **Help** и **Hello** .</span><span class="sxs-lookup"><span data-stu-id="9480d-229">For improved user experience include a personal bot that sends a welcome message to the user on the first run and responds to the **hi**, **help**, and **hello** commands.</span></span> <span data-ttu-id="9480d-230">Вы можете обратиться к документации по [Боты](../../bots/what-are-bots.md#in-a-one-to-one-chat) для получения дополнительной помощи.</span><span class="sxs-lookup"><span data-stu-id="9480d-230">You can refer to the documentation on [conversational bots](../../bots/what-are-bots.md#in-a-one-to-one-chat) for further assistance.</span></span>
