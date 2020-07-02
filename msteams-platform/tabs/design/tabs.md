---
title: Рекомендации по проектированию вкладок
description: Описывает рекомендации по созданию вкладок для контента и совместной работы
keywords: рекомендации по разработке Teams Справочник по настройке вкладок платформы
ms.openlocfilehash: 51c2d7ac445d03ed993764d964b7a5d8b69399f5
ms.sourcegitcommit: e355f59d2d21a2d5ae36cc46acad5ed4765b42e0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2020
ms.locfileid: "45021617"
---
# <a name="content-and-conversations-all-at-once-using-tabs"></a><span data-ttu-id="8d463-104">Контент и беседы, все сразу с помощью вкладок</span><span class="sxs-lookup"><span data-stu-id="8d463-104">Content and conversations, all at once using tabs</span></span>

> [!Important]
> <span data-ttu-id="8d463-105">**Вкладки на мобильных клиентах**</span><span class="sxs-lookup"><span data-stu-id="8d463-105">**Tabs on Mobile Clients**</span></span>
>
> <span data-ttu-id="8d463-106">Следуйте [указаниям для вкладок на странице Mobile](./tabs-mobile.md) при создании вкладок.</span><span class="sxs-lookup"><span data-stu-id="8d463-106">Follow the [guidance for tabs on mobile](./tabs-mobile.md) when creating your tabs.</span></span> <span data-ttu-id="8d463-107">Если вкладка использует проверку подлинности, необходимо обновить пакет SDK для Teams для Teams до версии 1.4.1 или более поздней, иначе проверка подлинности завершится неуспешно.</span><span class="sxs-lookup"><span data-stu-id="8d463-107">If your tab uses authentication, you must upgrade your Teams JavaScript SDK to version 1.4.1 or later, or authentication will fail.</span></span>
>
> <span data-ttu-id="8d463-108">**Личные (статические) вкладки на мобильных устройствах:**</span><span class="sxs-lookup"><span data-stu-id="8d463-108">**Personal (static) tabs on mobile:**</span></span>
>
> * <span data-ttu-id="8d463-109">Статические вкладки (личное приложение) доступны в [предварительной версии для разработчиков](~/resources/dev-preview/developer-preview-intro.md).</span><span class="sxs-lookup"><span data-stu-id="8d463-109">Static tabs (personal app) are available in [developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
> * <span data-ttu-id="8d463-110">При создании статических вкладок обязательно следуйте [указаниям для вкладок на мобильных устройствах](~/tabs/design/tabs-mobile.md) .</span><span class="sxs-lookup"><span data-stu-id="8d463-110">While building your static tabs, ensure to follow the [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md)</span></span>
>
> <span data-ttu-id="8d463-111">**Вкладки каналов и групп (настраиваемых) на мобильных устройствах:**</span><span class="sxs-lookup"><span data-stu-id="8d463-111">**Channel/group (configurable) tabs on mobile:**</span></span>
>
> * <span data-ttu-id="8d463-112">Для мобильных клиентов отображаются только вкладки со значением `websiteUrl` .</span><span class="sxs-lookup"><span data-stu-id="8d463-112">Mobile clients only show tabs that have a value for `websiteUrl`.</span></span> <span data-ttu-id="8d463-113">Если вы хотите, чтобы вкладка отображалась в клиентах Teams для мобильных устройств, необходимо задать значение `websiteUrl` .</span><span class="sxs-lookup"><span data-stu-id="8d463-113">If you want your tab to appear on the Teams mobile clients, you must set the value of `websiteUrl`.</span></span>
> * <span data-ttu-id="8d463-114">Поведение по умолчанию при открытии на мобильном устройстве можно открыть снаружи в браузере с помощью `websiteUrl` .</span><span class="sxs-lookup"><span data-stu-id="8d463-114">Default open behavior on mobile is to open outside in browser using the `websiteUrl`.</span></span> <span data-ttu-id="8d463-115">Для приложений, опубликованных в магазине общедоступных приложений, если вы хотите, чтобы вкладка каналы открывалась внутри Teams по умолчанию, следуйте [указаниям по использованию вкладок на мобильном устройстве](~/tabs/design/tabs-mobile.md), чтобы получить доступ к внесены.</span><span class="sxs-lookup"><span data-stu-id="8d463-115">For apps published to the public App Store, if you want your channel tab to open inside teams by default, follow the [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md), and reach out to your support rep to request to be whitelisted.</span></span>

<span data-ttu-id="8d463-116">Вкладки — это холсты, которые можно использовать для обмена контентом, удержания бесед и размещения сторонних служб в рабочем процессе.</span><span class="sxs-lookup"><span data-stu-id="8d463-116">Tabs are canvases that you can use to share content, hold conversations, and host third-party services, all within a team’s organic workflow.</span></span> <span data-ttu-id="8d463-117">Когда вы создаете вкладку в Microsoft Teams, он помещает веб-приложение спереди и в центре, где оно легко доступно из ключевых бесед.</span><span class="sxs-lookup"><span data-stu-id="8d463-117">When you build a tab in Microsoft Teams, it puts your web app front and center where it’s easily accessible from key conversations.</span></span>

## <a name="guidelines"></a><span data-ttu-id="8d463-118">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="8d463-118">Guidelines</span></span>

<span data-ttu-id="8d463-119">На хорошей вкладке должны отображаться следующие характеристики:</span><span class="sxs-lookup"><span data-stu-id="8d463-119">A good tab should display the following characteristics:</span></span>

### <a name="focused-functionality"></a><span data-ttu-id="8d463-120">Ориентированные функциональные возможности</span><span class="sxs-lookup"><span data-stu-id="8d463-120">Focused functionality</span></span>

<span data-ttu-id="8d463-121">Вкладки лучше подходят для конкретных нужд.</span><span class="sxs-lookup"><span data-stu-id="8d463-121">Tabs work best when they’re built to address a specific need.</span></span> <span data-ttu-id="8d463-122">Сосредоточьтесь на небольшом наборе задач или подмножестве данных, относящихся к каналу, в котором находится вкладка.</span><span class="sxs-lookup"><span data-stu-id="8d463-122">Focus on a small set of tasks or a subset of data that’s relevant to the channel the tab is in.</span></span>

### <a name="reduced-chrome"></a><span data-ttu-id="8d463-123">Сокращенный хром</span><span class="sxs-lookup"><span data-stu-id="8d463-123">Reduced chrome</span></span>

<span data-ttu-id="8d463-124">Избегайте создания нескольких панелей на вкладке, добавления слоев навигации или необходимости прокручивать их по вертикали и горизонтали на одной вкладке. Другими словами, старайтесь не использовать вкладки на вкладке.</span><span class="sxs-lookup"><span data-stu-id="8d463-124">Avoid creating multiple panels in a tab, adding layers of navigation, or requiring users to scroll both vertically and horizontally in one tab. In other words, try not to have tabs in your tab.</span></span>

### <a name="integration"></a><span data-ttu-id="8d463-125">Интеграция</span><span class="sxs-lookup"><span data-stu-id="8d463-125">Integration</span></span>

<span data-ttu-id="8d463-126">Узнайте, как уведомлять пользователей об активности вкладок путем отправки [адаптивных карточек](../../task-modules-and-cards/what-are-cards.md#adaptive-cards) в беседу.</span><span class="sxs-lookup"><span data-stu-id="8d463-126">Find ways to notify users about tab activity by posting [adaptive cards](../../task-modules-and-cards/what-are-cards.md#adaptive-cards) to a conversation.</span></span>

### <a name="conversational"></a><span data-ttu-id="8d463-127">Разговорному</span><span class="sxs-lookup"><span data-stu-id="8d463-127">Conversational</span></span>

<span data-ttu-id="8d463-128">Найдите способ для упрощения общения вокруг вкладки. Это гарантирует, что центр бесед на содержании, данные или процесс в любой момент.</span><span class="sxs-lookup"><span data-stu-id="8d463-128">Find a way to facilitate conversation around a tab. This ensures that conversations center on the content, data, or process at hand.</span></span>

### <a name="streamlined-access"></a><span data-ttu-id="8d463-129">Упрощенный доступ</span><span class="sxs-lookup"><span data-stu-id="8d463-129">Streamlined access</span></span>

<span data-ttu-id="8d463-130">Убедитесь, что вы предоставляете доступ к нужным людям в нужное время.</span><span class="sxs-lookup"><span data-stu-id="8d463-130">Make sure you’re granting access to the right people at the right time.</span></span> <span data-ttu-id="8d463-131">Сохранение процесса входа в систему не позволит создавать барьеры для участия и совместной работы.</span><span class="sxs-lookup"><span data-stu-id="8d463-131">Keeping your sign-in process simple will avoid creating barriers to contribution and collaboration.</span></span>

### <a name="responsiveness-to-window-sizing"></a><span data-ttu-id="8d463-132">Скорость отклика при изменении размера окна</span><span class="sxs-lookup"><span data-stu-id="8d463-132">Responsiveness to window sizing</span></span>

<span data-ttu-id="8d463-133">Teams можно использовать в размерах окон как небольшие 720px, поэтому убедитесь, что вкладка используется в небольшом окне так же, как и удобство при высоком разрешении.</span><span class="sxs-lookup"><span data-stu-id="8d463-133">Teams can be used in window sizes as small as 720px, so making sure that a tab is usable in a small window is just as important as usability at very high resolutions.</span></span>

### <a name="flat-navigation"></a><span data-ttu-id="8d463-134">Плоская Навигация</span><span class="sxs-lookup"><span data-stu-id="8d463-134">Flat navigation</span></span>

<span data-ttu-id="8d463-135">Мы просим разработчиков не добавлять весь портал на вкладку. хранение сравнительно плоской структуры помогает поддерживать более простую модель беседы.</span><span class="sxs-lookup"><span data-stu-id="8d463-135">We ask developers not to add their entire portal to a tab. Keeping the navigation relatively flat helps maintain a simpler conversational model.</span></span> <span data-ttu-id="8d463-136">Другими словами, беседа представляет собой список вещей, таких как рассмотренные рабочие элементы, или одна вещь, например Spec.</span><span class="sxs-lookup"><span data-stu-id="8d463-136">In other words, the conversation is about a list of things, such as triaged work items, or a single thing, like a spec.</span></span>

<span data-ttu-id="8d463-137">В цепочке обсуждений есть проблемы, связанные с навигацией с углубленной иерархией навигации.</span><span class="sxs-lookup"><span data-stu-id="8d463-137">There are inherent navigational challenges with deep navigation hierarchy, within threaded conversations.</span></span> <span data-ttu-id="8d463-138">Для оптимального взаимодействия с пользователем вы можете сохранить навигацию на вкладке по меньшей мере и иметь следующий вид:</span><span class="sxs-lookup"><span data-stu-id="8d463-138">For the best user experience, your tab navigation should be kept to a minimum and be designed as follows:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="8d463-139">**Открывает модуль задачи, такой как отдельный рабочий элемент или сущность**.</span><span class="sxs-lookup"><span data-stu-id="8d463-139">**Opens a task module such as an individual work item or entity**.</span></span> <span data-ttu-id="8d463-140">Это исключает возможность полностью отменять чат и является лучшим вариантом, чтобы отследить обсуждение вкладки, а не вложенных сущностей или возможностей редактирования.</span><span class="sxs-lookup"><span data-stu-id="8d463-140">This precludes chat entirely and is the best option to keep chat specifically about the tab and not the sub-entities or editing experiences.</span></span>
>* <span data-ttu-id="8d463-141">**Открывает псевдо диалоговое окно в IFRAME**.</span><span class="sxs-lookup"><span data-stu-id="8d463-141">**Opens a pseudo dialog in an iframe**.</span></span> <span data-ttu-id="8d463-142">При использовании с экранным фоном рекомендуется использовать более светлый цвет, а не темный.</span><span class="sxs-lookup"><span data-stu-id="8d463-142">If used with a screened background we recommend using the lighter color rather than the dark.</span></span> <span data-ttu-id="8d463-143">`app-gray-10 at 30%`Прозрачность работает хорошо.</span><span class="sxs-lookup"><span data-stu-id="8d463-143">The `app-gray-10 at 30%` transparency works well.</span></span>
>* <span data-ttu-id="8d463-144">**Открывает страницу браузера**.</span><span class="sxs-lookup"><span data-stu-id="8d463-144">**Opens a browser page**.</span></span>

### <a name="personality"></a><span data-ttu-id="8d463-145">Индивидуальные</span><span class="sxs-lookup"><span data-stu-id="8d463-145">Personality</span></span>

<span data-ttu-id="8d463-146">На холсте вкладок можно получить прекрасную возможность для фирменного стиля работы.</span><span class="sxs-lookup"><span data-stu-id="8d463-146">Your tab canvas presents a great opportunity to brand your experience.</span></span> <span data-ttu-id="8d463-147">Ваш логотип является важной частью вашего удостоверения и подключения к вашим пользователям. Убедитесь, что он должен быть включен:</span><span class="sxs-lookup"><span data-stu-id="8d463-147">Your logo is an important part of your identity and connection with your users., so be sure to include it:</span></span>

> [!div class="checklist"]
>
>* <span data-ttu-id="8d463-148">Размещение логотипа в левом или правом углу или вдоль нижнего края</span><span class="sxs-lookup"><span data-stu-id="8d463-148">Place your logo in the left or right corner or along the bottom edge</span></span>
> * <span data-ttu-id="8d463-149">Хранение и ненавязчивая эмблема</span><span class="sxs-lookup"><span data-stu-id="8d463-149">Keep your logo small and unobtrusive</span></span>

<span data-ttu-id="8d463-150">Включение собственных цветов и макетов твилл также помогает в общении.</span><span class="sxs-lookup"><span data-stu-id="8d463-150">Incorporating your own colors and layouts twill also aid in communicating personality.</span></span>

> [!TIP]
> <span data-ttu-id="8d463-151">Используйте наш стиль оформления, чтобы ваша служба работала как часть Teams.</span><span class="sxs-lookup"><span data-stu-id="8d463-151">Please work with our visual style so your service feels like a part of Teams.</span></span> <span data-ttu-id="8d463-152">*Просмотреть*, например, [цвета Teams](../../concepts/design/components/color.md)</span><span class="sxs-lookup"><span data-stu-id="8d463-152">*See*, for example [Teams Colors](../../concepts/design/components/color.md)</span></span>

---

## <a name="tab-layouts"></a><span data-ttu-id="8d463-153">Макеты вкладок</span><span class="sxs-lookup"><span data-stu-id="8d463-153">Tab layouts</span></span>

[!INCLUDE [Tab layouts](../../includes/design/tab-layouts.html)]

---

## <a name="types-of-tabs"></a><span data-ttu-id="8d463-154">Типы вкладок</span><span class="sxs-lookup"><span data-stu-id="8d463-154">Types of tabs</span></span>

[!INCLUDE [Tab types](../../includes/design/tab-types.html)]

---

## <a name="configuration-page-height"></a><span data-ttu-id="8d463-155">Высота страницы конфигурации</span><span class="sxs-lookup"><span data-stu-id="8d463-155">Configuration page height</span></span>

>[!IMPORTANT]
><span data-ttu-id="8d463-156">В сентябре 2018 высота [страницы настройки](~/tabs/how-to/create-tab-pages/configuration-page.md) вкладки была увеличена, а ширина осталась неизменной.</span><span class="sxs-lookup"><span data-stu-id="8d463-156">In September 2018, the height for the tab [configuration page](~/tabs/how-to/create-tab-pages/configuration-page.md) was increased while the width remained unchanged.</span></span> <span data-ttu-id="8d463-157">Если ваше приложение предназначено для устаревшего размера вкладки, на странице Конфигурация вкладки будет много вертикальных пробелов.</span><span class="sxs-lookup"><span data-stu-id="8d463-157">If your app is designed for the older size your tab configuration page will have a great deal of vertical whitespace.</span></span> <span data-ttu-id="8d463-158">Устаревшие приложения хранилища, исключенные из этого изменения, должны обратиться в корпорацию Майкрософт после обновления, чтобы вместить новые измерения.</span><span class="sxs-lookup"><span data-stu-id="8d463-158">Legacy store apps exempted from this change will need to contact Microsoft after updating to accommodate the new dimensions.</span></span>

<span data-ttu-id="8d463-159">Размеры страницы настройки вкладки:</span><span class="sxs-lookup"><span data-stu-id="8d463-159">The dimensions of the tab configuration page:</span></span>

<img width="450px" title="Размеры для вкладок конфигурации" src="~/assets/images/tabs/config-dialog-Contoso2.png" />

### <a name="guidelines-for-tab-configuration-page-format"></a><span data-ttu-id="8d463-161">Рекомендации по формату страницы настройки вкладки</span><span class="sxs-lookup"><span data-stu-id="8d463-161">Guidelines for tab configuration page format</span></span>

* <span data-ttu-id="8d463-162">Основа минимальной высоты области контента на странице настройки вкладки для графических элементов с фиксированной высотой.</span><span class="sxs-lookup"><span data-stu-id="8d463-162">Base the minimum height of your content area of your tab configuration page on fixed-height graphic elements.</span></span>
* <span data-ttu-id="8d463-163">Рассчитайте доступное вертикальное пространство (высоту области контента на странице Конфигурация) с помощью `window.innerHeight` .</span><span class="sxs-lookup"><span data-stu-id="8d463-163">Calculate available vertical space (the height of the content area in the configuration page) using `window.innerHeight`.</span></span> <span data-ttu-id="8d463-164">При этом возвращается размер `<iframe>` страницы конфигурации, в которой размещается страница конфигурации, которая может измениться в будущих выпусках.</span><span class="sxs-lookup"><span data-stu-id="8d463-164">This returns the size of the `<iframe>` in which your configuration page resides, which may change in future releases.</span></span> <span data-ttu-id="8d463-165">При использовании этого значения контент будет автоматически скорректирован до будущих изменений.</span><span class="sxs-lookup"><span data-stu-id="8d463-165">By using this value your content will adjust automatically to future changes.</span></span>
* <span data-ttu-id="8d463-166">Выделение вертикального пространства для элементов переменной высоты за вычетом того, что требуется для элементов фиксированной высоты.</span><span class="sxs-lookup"><span data-stu-id="8d463-166">Allocate vertical space to the variable-height elements minus what's needed for the fixed-height elements.</span></span>
* <span data-ttu-id="8d463-167">Для состояния *входа* по вертикали и горизонтали по центру содержимого.</span><span class="sxs-lookup"><span data-stu-id="8d463-167">For the *login* state, vertically and horizontally center the content.</span></span>
* <span data-ttu-id="8d463-168">Если вы хотите использовать фоновое изображение, вам потребуется новое изображение, в соответствии с областью (предпочтительный), или можно оставить одно и то же изображение и выбрать один из следующих вариантов:</span><span class="sxs-lookup"><span data-stu-id="8d463-168">If you want a background image, you need either a new image, sized to fit the area (preferred), or you can keep the same image and choose between:</span></span>
  * <span data-ttu-id="8d463-169">Выравнивание по верхнему левому углу.</span><span class="sxs-lookup"><span data-stu-id="8d463-169">aligning to the upper left hand corner.</span></span>
  * <span data-ttu-id="8d463-170">масштабирование изображения по размеру.</span><span class="sxs-lookup"><span data-stu-id="8d463-170">scaling the image to fit.</span></span>

<span data-ttu-id="8d463-171">При правильном изменении размера страница настройки вкладки должна выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="8d463-171">When properly sized, your tab configuration page should look similar to this:</span></span>

<img width="450px" title="Вкладка "Новая конфигурация"" src="~/assets/images/tabs/config-dialog-Contoso.png" />

## <a name="best-practices"></a><span data-ttu-id="8d463-173">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="8d463-173">Best practices</span></span>

### <a name="always-include-a-default-state"></a><span data-ttu-id="8d463-174">Всегда включать состояние по умолчанию</span><span class="sxs-lookup"><span data-stu-id="8d463-174">Always include a default state</span></span>

<span data-ttu-id="8d463-175">Включите состояние по умолчанию, чтобы упростить настройку вкладок, даже если вкладка настраиваемая.</span><span class="sxs-lookup"><span data-stu-id="8d463-175">Include a default state to make tabs easy to set up even if your tab is configurable.</span></span>

### <a name="deep-linking"></a><span data-ttu-id="8d463-176">Глубокая компоновка</span><span class="sxs-lookup"><span data-stu-id="8d463-176">Deep linking</span></span>

<span data-ttu-id="8d463-177">По мере возможности карточки и боты должны иметь глубокую ссылку на Расширенные данные на вкладке размещения. Например, карточка может показывать сводную информацию об ошибках, но при щелчке она может отобразить всю ошибку на вкладке.</span><span class="sxs-lookup"><span data-stu-id="8d463-177">Whenever possible, cards and bots should deep link to richer data in a hosted tab. For example, a card may show a summary of bug data, but clicking it can shows the entire bug in a tab.</span></span>

### <a name="naming"></a><span data-ttu-id="8d463-178">Переименовывает</span><span class="sxs-lookup"><span data-stu-id="8d463-178">Naming</span></span>

<span data-ttu-id="8d463-179">Во многих случаях имя приложения будет иметь отличное название вкладки.</span><span class="sxs-lookup"><span data-stu-id="8d463-179">In many cases, the name of your app will make a great tab name.</span></span> <span data-ttu-id="8d463-180">Кроме того, рекомендуется называть вкладки в соответствии с функциями, которые они предоставляют.</span><span class="sxs-lookup"><span data-stu-id="8d463-180">But, also consider naming your tabs according to the functionality they provide.</span></span>

## <a name="notifications-for-tabs"></a><span data-ttu-id="8d463-181">Уведомления для вкладок</span><span class="sxs-lookup"><span data-stu-id="8d463-181">Notifications for tabs</span></span>

<span data-ttu-id="8d463-182">Существует два режима уведомления об изменениях содержимого на вкладке:</span><span class="sxs-lookup"><span data-stu-id="8d463-182">There are two modes of notification for tab content changes:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="8d463-183">**Использование API приложений для уведомления пользователей об изменениях**.</span><span class="sxs-lookup"><span data-stu-id="8d463-183">**Use the app api to notify users of changes**.</span></span> <span data-ttu-id="8d463-184">Это сообщение будет отображаться в веб-канале активности пользователя и имеет глубокую ссылку на вкладку. *Дополнительные*  [ссылки на материалы и функции в Microsoft Teams](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest)</span><span class="sxs-lookup"><span data-stu-id="8d463-184">This message will show up in the user’s activity feed and deep link to the tab. *See*  [Create deep links to content and features in Microsoft Teams](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest)</span></span>
> * <span data-ttu-id="8d463-185">**Использование ленты**.</span><span class="sxs-lookup"><span data-stu-id="8d463-185">**Use a bot**.</span></span> <span data-ttu-id="8d463-186">Этот метод является предпочтительным, особенно если выбран целевой поток вкладок.</span><span class="sxs-lookup"><span data-stu-id="8d463-186">This method is preferred especially if the Tab thread is targeted.</span></span> <span data-ttu-id="8d463-187">В результате цепочка вкладок будет перемещена в представление "недавно активные".</span><span class="sxs-lookup"><span data-stu-id="8d463-187">The result will be that the tab’s threaded conversation will be moved into view as recently active.</span></span> <span data-ttu-id="8d463-188">Этот метод также позволяет использовать некоторые сложности при отправке уведомления.</span><span class="sxs-lookup"><span data-stu-id="8d463-188">This method also allows for some sophistication in how the notification is sent.</span></span>

  <span data-ttu-id="8d463-189">При отправке сообщения в поток вкладок увеличивается осведомленность о действиях для всех пользователей без явного уведомления всех.</span><span class="sxs-lookup"><span data-stu-id="8d463-189">Sending a message to a tab thread increases the awareness of activity to all users without explicitly notifying everyone.</span></span> <span data-ttu-id="8d463-190">Это относится без шума.</span><span class="sxs-lookup"><span data-stu-id="8d463-190">This is awareness without noise.</span></span> <span data-ttu-id="8d463-191">Кроме того, если `@mention` для определенных пользователей одно и то же уведомление будет размещаться в своем канале, то детально привязать их к потоку вкладок напрямую.</span><span class="sxs-lookup"><span data-stu-id="8d463-191">In addition, when you `@mention`  specific users the same notification will be placed in their feed, deep linking them to the tab thread directly.</span></span>
