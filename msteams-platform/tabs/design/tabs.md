---
title: Рекомендации по проектированию вкладок
description: Описывает рекомендации по созданию вкладок для контента и совместной работы
keywords: рекомендации по разработке Teams Справочник по настройке вкладок платформы
ms.openlocfilehash: adf86678a42e2267af00734e1ef85efced882488
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675146"
---
# <a name="content-and-conversations-all-at-once-using-tabs"></a><span data-ttu-id="5bafb-104">Контент и беседы, все сразу с помощью вкладок</span><span class="sxs-lookup"><span data-stu-id="5bafb-104">Content and conversations, all at once using tabs</span></span>

> [!Important]
> <span data-ttu-id="5bafb-105">**Вкладки на мобильных клиентах**</span><span class="sxs-lookup"><span data-stu-id="5bafb-105">**Tabs on Mobile Clients**</span></span>
>
> <span data-ttu-id="5bafb-106">Следуйте [указаниям для вкладок на странице Mobile](~/tabs/design/tabs-mobile.md) при создании вкладок.</span><span class="sxs-lookup"><span data-stu-id="5bafb-106">Follow the [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md) when creating your tabs.</span></span> <span data-ttu-id="5bafb-107">Если вкладка использует проверку подлинности, необходимо обновить пакет SDK для Teams для Teams до версии 1.4.1 или более поздней, иначе проверка подлинности завершится неуспешно.</span><span class="sxs-lookup"><span data-stu-id="5bafb-107">If your tab uses authentication, you must upgrade your Teams JavaScript SDK to version 1.4.1 or later, or authentication will fail.</span></span>
>
> <span data-ttu-id="5bafb-108">**Личные (статические) вкладки на мобильных устройствах:**</span><span class="sxs-lookup"><span data-stu-id="5bafb-108">**Personal (static) tabs on mobile:**</span></span>
>
> * <span data-ttu-id="5bafb-109">Статические вкладки (личное приложение) доступны в [предварительной версии для разработчиков](~/resources/dev-preview/developer-preview-intro.md).</span><span class="sxs-lookup"><span data-stu-id="5bafb-109">Static tabs (personal app) are available in [developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
> * <span data-ttu-id="5bafb-110">При создании статических вкладок обязательно следуйте [указаниям для вкладок на мобильных устройствах](~/tabs/design/tabs-mobile.md) .</span><span class="sxs-lookup"><span data-stu-id="5bafb-110">While building your static tabs, ensure to follow the [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md)</span></span>
>
> <span data-ttu-id="5bafb-111">**Вкладки каналов и групп (настраиваемых) на мобильных устройствах:**</span><span class="sxs-lookup"><span data-stu-id="5bafb-111">**Channel/group (configurable) tabs on mobile:**</span></span>
>
> * <span data-ttu-id="5bafb-112">Для `websiteUrl`мобильных клиентов отображаются только вкладки со значением.</span><span class="sxs-lookup"><span data-stu-id="5bafb-112">Mobile clients only show tabs that have a value for `websiteUrl`.</span></span> <span data-ttu-id="5bafb-113">Если вы хотите, чтобы вкладка отображалась в клиентах Teams для мобильных устройств, необходимо задать `websiteUrl`значение.</span><span class="sxs-lookup"><span data-stu-id="5bafb-113">If you want your tab to appear on the Teams mobile clients, you must set the value of `websiteUrl`.</span></span>
> * <span data-ttu-id="5bafb-114">Поведение по умолчанию при открытии на мобильном устройстве можно открыть снаружи `websiteUrl`в браузере с помощью.</span><span class="sxs-lookup"><span data-stu-id="5bafb-114">Default open behavior on mobile is to open outside in browser using the `websiteUrl`.</span></span> <span data-ttu-id="5bafb-115">Для приложений, опубликованных в магазине общедоступных приложений, если вы хотите, чтобы вкладка каналы открывалась внутри Teams по умолчанию, следуйте [указаниям по использованию вкладок на мобильном устройстве](~/tabs/design/tabs-mobile.md), чтобы получить доступ к внесены.</span><span class="sxs-lookup"><span data-stu-id="5bafb-115">For apps published to the public App Store, if you want your channel tab to open inside teams by default, follow the [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md), and reach out to your support rep to request to be whitelisted.</span></span>

<span data-ttu-id="5bafb-116">Вкладки — это холсты, которые можно использовать для обмена контентом, удержания бесед и размещения сторонних служб в рабочем процессе.</span><span class="sxs-lookup"><span data-stu-id="5bafb-116">Tabs are canvases that you can use to share content, hold conversations, and host third-party services, all within a team’s organic workflow.</span></span> <span data-ttu-id="5bafb-117">Когда вы создаете вкладку в Microsoft Teams, он помещает веб-приложение спереди и в центре, где оно легко доступно из ключевых бесед.</span><span class="sxs-lookup"><span data-stu-id="5bafb-117">When you build a tab in Microsoft Teams, it puts your web app front and center where it’s easily accessible from key conversations.</span></span>

## <a name="guidelines"></a><span data-ttu-id="5bafb-118">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="5bafb-118">Guidelines</span></span>

<span data-ttu-id="5bafb-119">На хорошей вкладке должны отображаться следующие характеристики:</span><span class="sxs-lookup"><span data-stu-id="5bafb-119">A good tab should display the following characteristics:</span></span>

### <a name="focused-functionality"></a><span data-ttu-id="5bafb-120">Ориентированные функциональные возможности</span><span class="sxs-lookup"><span data-stu-id="5bafb-120">Focused functionality</span></span>

<span data-ttu-id="5bafb-121">Вкладки лучше подходят для конкретных нужд.</span><span class="sxs-lookup"><span data-stu-id="5bafb-121">Tabs work best when they’re built to address a specific need.</span></span> <span data-ttu-id="5bafb-122">Сосредоточьтесь на небольшом наборе задач или подмножестве данных, относящихся к каналу, в котором находится вкладка.</span><span class="sxs-lookup"><span data-stu-id="5bafb-122">Focus on a small set of tasks or a subset of data that’s relevant to the channel the tab is in.</span></span>

### <a name="reduced-chrome"></a><span data-ttu-id="5bafb-123">Сокращенный хром</span><span class="sxs-lookup"><span data-stu-id="5bafb-123">Reduced chrome</span></span>

<span data-ttu-id="5bafb-124">Избегайте создания нескольких панелей на вкладке, добавления слоев навигации или необходимости прокручивать их по вертикали и горизонтали на одной вкладке. Другими словами, старайтесь не использовать вкладки на вкладке.</span><span class="sxs-lookup"><span data-stu-id="5bafb-124">Avoid creating multiple panels in a tab, adding layers of navigation, or requiring users to scroll both vertically and horizontally in one tab. In other words, try not to have tabs in your tab.</span></span>

> [!TIP]
> <span data-ttu-id="5bafb-125">Избегайте создания нескольких панелей на вкладке, добавления слоев навигации или необходимости прокручивать их по вертикали и горизонтали на одной вкладке.</span><span class="sxs-lookup"><span data-stu-id="5bafb-125">Avoid creating multiple panels in a tab, adding layers of navigation, or requiring users to scroll both vertically and horizontally in one tab.</span></span>

### <a name="integration"></a><span data-ttu-id="5bafb-126">Интеграция</span><span class="sxs-lookup"><span data-stu-id="5bafb-126">Integration</span></span>

<span data-ttu-id="5bafb-127">Узнайте о том, как уведомлять пользователей об активности вкладок путем разноски карточек в беседу, например.</span><span class="sxs-lookup"><span data-stu-id="5bafb-127">Find ways to notify users about tab activity by posting cards to a conversation, for example.</span></span>

### <a name="conversational"></a><span data-ttu-id="5bafb-128">Разговорному</span><span class="sxs-lookup"><span data-stu-id="5bafb-128">Conversational</span></span>

<span data-ttu-id="5bafb-129">Найдите способ для упрощения общения вокруг вкладки. Это гарантирует, что центр бесед на содержании, данные или процесс в любой момент.</span><span class="sxs-lookup"><span data-stu-id="5bafb-129">Find a way to facilitate conversation around a tab. This ensures that conversations center on the content, data, or process at hand.</span></span>

### <a name="streamlined-access"></a><span data-ttu-id="5bafb-130">Упрощенный доступ</span><span class="sxs-lookup"><span data-stu-id="5bafb-130">Streamlined access</span></span>

<span data-ttu-id="5bafb-131">Убедитесь, что вы предоставляете доступ к нужным людям в нужное время.</span><span class="sxs-lookup"><span data-stu-id="5bafb-131">Make sure you’re granting access to the right people at the right time.</span></span> <span data-ttu-id="5bafb-132">Сохранение процесса входа в систему не позволит создавать барьеры для участия и совместной работы.</span><span class="sxs-lookup"><span data-stu-id="5bafb-132">Keeping your sign-in process simple will avoid creating barriers to contribution and collaboration.</span></span>

### <a name="personality"></a><span data-ttu-id="5bafb-133">Индивидуальные</span><span class="sxs-lookup"><span data-stu-id="5bafb-133">Personality</span></span>

<span data-ttu-id="5bafb-134">На холсте вкладок удобно иметь возможность фирменного стиля.</span><span class="sxs-lookup"><span data-stu-id="5bafb-134">Your tab canvas presents a good opportunity to brand your experience.</span></span> <span data-ttu-id="5bafb-135">Внедрять собственные логотипы, цвета и макеты для общения.</span><span class="sxs-lookup"><span data-stu-id="5bafb-135">Incorporate your own logos, colors, and layouts to communicate personality.</span></span>

<span data-ttu-id="5bafb-136">Ваш логотип является важной частью вашего удостоверения и подключения к вашим пользователям.</span><span class="sxs-lookup"><span data-stu-id="5bafb-136">Your logo is an important part of your identity and a connection with your users.</span></span> <span data-ttu-id="5bafb-137">Поэтому обязательно включите его.</span><span class="sxs-lookup"><span data-stu-id="5bafb-137">So be sure to include it.</span></span>

* <span data-ttu-id="5bafb-138">Размещение логотипа в левом или правом углу или вдоль нижнего края</span><span class="sxs-lookup"><span data-stu-id="5bafb-138">Place your logo in the left or right corner or along the bottom edge</span></span>
* <span data-ttu-id="5bafb-139">Хранение и ненавязчивая эмблема</span><span class="sxs-lookup"><span data-stu-id="5bafb-139">Keep your logo small and unobtrusive</span></span>

> [!TIP]
> <span data-ttu-id="5bafb-140">Используйте наш стиль оформления, чтобы ваша служба работала как часть Teams.</span><span class="sxs-lookup"><span data-stu-id="5bafb-140">Please work with our visual style so your service feels like a part of Teams.</span></span>

---

## <a name="tab-layouts"></a><span data-ttu-id="5bafb-141">Макеты вкладок</span><span class="sxs-lookup"><span data-stu-id="5bafb-141">Tab layouts</span></span>

[!include[Tab layouts](~/includes/design/tab-layouts.html)]

---

## <a name="types-of-tabs"></a><span data-ttu-id="5bafb-142">Типы вкладок</span><span class="sxs-lookup"><span data-stu-id="5bafb-142">Types of tabs</span></span>

[!include[Tab types](~/includes/design/tab-types.html)]

---

## <a name="configuration-page-height"></a><span data-ttu-id="5bafb-143">Высота страницы конфигурации</span><span class="sxs-lookup"><span data-stu-id="5bafb-143">Configuration page height</span></span>

>[!NOTE]
><span data-ttu-id="5bafb-144">В сентябре 2018 высота [страницы настройки](~/tabs/how-to/create-tab-pages/configuration-page.md) вкладки была увеличена, а ширина осталась неизменной.</span><span class="sxs-lookup"><span data-stu-id="5bafb-144">In September 2018, the height for the tab [configuration page](~/tabs/how-to/create-tab-pages/configuration-page.md) was increased while the width remained unchanged.</span></span> <span data-ttu-id="5bafb-145">Если ваше приложение предназначено для устаревшего размера вкладки, на странице Конфигурация вкладки будет много вертикальных пробелов.</span><span class="sxs-lookup"><span data-stu-id="5bafb-145">If your app is designed for the older size your tab configuration page will have a great deal of vertical whitespace.</span></span> <span data-ttu-id="5bafb-146">Устаревшие приложения хранилища, исключенные из этого изменения, должны обратиться в корпорацию Майкрософт после обновления, чтобы вместить новые измерения.</span><span class="sxs-lookup"><span data-stu-id="5bafb-146">Legacy store apps exempted from this change will need to contact Microsoft after updating to accommodate the new dimensions.</span></span>

<span data-ttu-id="5bafb-147">Размеры страницы настройки вкладки:</span><span class="sxs-lookup"><span data-stu-id="5bafb-147">The dimensions of the tab configuration page:</span></span>

<img width="450px" title="Размеры для вкладок конфигурации" src="~/assets/images/tabs/config-dialog-Contoso2.png" />

### <a name="guidelines-for-tab-configuration-page-format"></a><span data-ttu-id="5bafb-149">Рекомендации по формату страницы настройки вкладки</span><span class="sxs-lookup"><span data-stu-id="5bafb-149">Guidelines for tab configuration page format</span></span>

* <span data-ttu-id="5bafb-150">Основа минимальной высоты области контента на странице настройки вкладки для графических элементов с фиксированной высотой.</span><span class="sxs-lookup"><span data-stu-id="5bafb-150">Base the minimum height of your content area of your tab configuration page on fixed-height graphic elements.</span></span>
* <span data-ttu-id="5bafb-151">Рассчитайте доступное вертикальное пространство (высоту области контента на странице Конфигурация) с помощью `window.innerHeight`.</span><span class="sxs-lookup"><span data-stu-id="5bafb-151">Calculate available vertical space (the height of the content area in the configuration page) using `window.innerHeight`.</span></span> <span data-ttu-id="5bafb-152">При этом возвращается размер страницы конфигурации `<iframe>` , в которой размещается страница конфигурации, которая может измениться в будущих выпусках.</span><span class="sxs-lookup"><span data-stu-id="5bafb-152">This returns the size of the `<iframe>` in which your configuration page resides, which may change in future releases.</span></span> <span data-ttu-id="5bafb-153">При использовании этого значения контент будет автоматически скорректирован до будущих изменений.</span><span class="sxs-lookup"><span data-stu-id="5bafb-153">By using this value your content will adjust automatically to future changes.</span></span>
* <span data-ttu-id="5bafb-154">Выделение вертикального пространства для элементов переменной высоты за вычетом того, что требуется для элементов фиксированной высоты.</span><span class="sxs-lookup"><span data-stu-id="5bafb-154">Allocate vertical space to the variable-height elements minus what's needed for the fixed-height elements.</span></span>
* <span data-ttu-id="5bafb-155">Для состояния *входа* по вертикали и горизонтали по центру содержимого.</span><span class="sxs-lookup"><span data-stu-id="5bafb-155">For the *login* state, vertically and horizontally center the content.</span></span>
* <span data-ttu-id="5bafb-156">Если вы хотите использовать фоновое изображение, вам потребуется новое изображение, в соответствии с областью (предпочтительный), или можно оставить одно и то же изображение и выбрать один из следующих вариантов:</span><span class="sxs-lookup"><span data-stu-id="5bafb-156">If you want a background image, you need either a new image, sized to fit the area (preferred), or you can keep the same image and choose between:</span></span>
  * <span data-ttu-id="5bafb-157">Выравнивание по верхнему левому углу.</span><span class="sxs-lookup"><span data-stu-id="5bafb-157">aligning to the upper left hand corner.</span></span>
  * <span data-ttu-id="5bafb-158">масштабирование изображения по размеру.</span><span class="sxs-lookup"><span data-stu-id="5bafb-158">scaling the image to fit.</span></span>

<span data-ttu-id="5bafb-159">При правильном изменении размера страница настройки вкладки должна выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="5bafb-159">When properly sized, your tab configuration page should look similar to this:</span></span>

<img width="450px" title="Вкладка "Новая конфигурация"" src="~/assets/images/tabs/config-dialog-Contoso.png" />

## <a name="best-practices"></a><span data-ttu-id="5bafb-161">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="5bafb-161">Best practices</span></span>

### <a name="always-include-a-default-state"></a><span data-ttu-id="5bafb-162">Всегда включать состояние по умолчанию</span><span class="sxs-lookup"><span data-stu-id="5bafb-162">Always include a default state</span></span>

<span data-ttu-id="5bafb-163">Включите состояние по умолчанию, чтобы упростить настройку вкладок, даже если вкладка настраиваемая.</span><span class="sxs-lookup"><span data-stu-id="5bafb-163">Include a default state to make tabs easy to set up even if your tab is configurable.</span></span>

### <a name="deep-linking"></a><span data-ttu-id="5bafb-164">Глубокая компоновка</span><span class="sxs-lookup"><span data-stu-id="5bafb-164">Deep linking</span></span>

<span data-ttu-id="5bafb-165">По мере возможности карточки и боты должны иметь глубокую ссылку на Расширенные данные на вкладке размещения. Например, карточка может показывать сводную информацию об ошибках, но при щелчке она может отобразить всю ошибку на вкладке.</span><span class="sxs-lookup"><span data-stu-id="5bafb-165">Whenever possible, cards and bots should deep link to richer data in a hosted tab. For example, a card may show a summary of bug data, but clicking it can shows the entire bug in a tab.</span></span>

### <a name="naming"></a><span data-ttu-id="5bafb-166">Переименовывает</span><span class="sxs-lookup"><span data-stu-id="5bafb-166">Naming</span></span>

<span data-ttu-id="5bafb-167">Во многих случаях имя приложения может делать имя вкладки.</span><span class="sxs-lookup"><span data-stu-id="5bafb-167">In many cases, the name of your app may make a great tab name.</span></span> <span data-ttu-id="5bafb-168">Но рассмотрите возможность именования вкладок в соответствии с функциями, которые они предоставляют.</span><span class="sxs-lookup"><span data-stu-id="5bafb-168">But consider naming your tabs according to the functionality they provide.</span></span>
