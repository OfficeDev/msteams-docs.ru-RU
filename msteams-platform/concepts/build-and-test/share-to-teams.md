---
title: Общий доступ к кнопке Teams Embedded
description: Добавление на веб-сайт кнопки "общий доступ" для Teams
keywords: Совместное использование Teams в Teams
ms.openlocfilehash: 219724e6ef3448db8a5b1fc70a519803255ffee6
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675515"
---
# <a name="creating-a-share-to-teams-embedded-button"></a><span data-ttu-id="aee22-104">Создание общего доступа к кнопке Teams Embedded</span><span class="sxs-lookup"><span data-stu-id="aee22-104">Creating a Share to Teams embedded button</span></span>

>[!NOTE]
> * <span data-ttu-id="aee22-105">Поддерживаются только настольные версии Edge и Chrome.</span><span class="sxs-lookup"><span data-stu-id="aee22-105">Only the desktop versions of Edge and Chrome are supported.</span></span>
> * <span data-ttu-id="aee22-106">Использование учетных записей Фримиум или Guest не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="aee22-106">Use of Freemium or guest accounts is not supported.</span></span>

<span data-ttu-id="aee22-107">Сторонние веб-сайты могут использовать сценарий запуска для встраивания общего доступа к кнопкам Teams на своих веб-страницах, которые запустят общий доступ к Microsoft Teams во всплывающем окне при нажатии.</span><span class="sxs-lookup"><span data-stu-id="aee22-107">Third-party websites can use the launcher script to embed Share to Teams buttons on their webpages which will launch the Share to Teams experience in a popup window when clicked.</span></span> <span data-ttu-id="aee22-108">Это позволит предоставить ссылку непосредственно любому человеку или каналу Microsoft Teams без переключения контекста.</span><span class="sxs-lookup"><span data-stu-id="aee22-108">This will allow you to share a link directly to any person or Microsoft Teams channel without switching context.</span></span>

![Открыть доступ к всплывающему меню "команды"](~/assets/images/share-to-teams-popup.png)

## <a name="how-to-embed-a-share-to-teams-button"></a><span data-ttu-id="aee22-110">Как внедрить кнопку Share to Teams</span><span class="sxs-lookup"><span data-stu-id="aee22-110">How to embed a Share to Teams button</span></span>

<span data-ttu-id="aee22-111">Сначала необходимо добавить `launcher.js` скрипт на веб-страницу.</span><span class="sxs-lookup"><span data-stu-id="aee22-111">First, you'll need to add the `launcher.js` script on your webpage.</span></span>

```html
<script async defer src="https://teams.microsoft.com/share/launcher.js"></script>
```

<span data-ttu-id="aee22-112">Затем добавьте HTML-элемент на веб-страницу с атрибутом `teams-share-button` Class и ссылка для совместного использования в `data-href` атрибуте.</span><span class="sxs-lookup"><span data-stu-id="aee22-112">Next, add an HTML element on your webpage with the `teams-share-button` class attribute and the link to share in the `data-href` attribute.</span></span>

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>">
</div>
```

<span data-ttu-id="aee22-113">При этом значок Microsoft Teams будет добавлен на веб-сайт.</span><span class="sxs-lookup"><span data-stu-id="aee22-113">This will add the Microsoft Teams icon to your website.</span></span>

![Значок предоставления общего доступа к Teams](~/assets/icons/share-to-teams-icon.png)

<span data-ttu-id="aee22-115">При необходимости используйте `data-icon-px-size` атрибут, если вы хотите изменить размер значков для кнопки Общий доступ для групп.</span><span class="sxs-lookup"><span data-stu-id="aee22-115">Optionally, if you want a different icon size for the Share to Teams button, use the `data-icon-px-size` attribute.</span></span>

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>"
  data-icon-px-size="64">
</div>
```

<span data-ttu-id="aee22-116">Если вы знаете, что предварительный просмотр URL-адреса с вашей ссылки на общий доступ не отображается в Teams (например, для ссылки требуется проверка подлинности пользователя), можно отключить `data-preview` предварительный просмотр `false`URL-адреса, добавив атрибут в значение.</span><span class="sxs-lookup"><span data-stu-id="aee22-116">If you know that the URL preview from your link to be shared won't render well in Teams (for example the link would require user authentication) you can disable the URL preview by adding the `data-preview` attribute set to `false`.</span></span>

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>"
  data-preview="false">
</div>
```

<span data-ttu-id="aee22-117">Если страница динамически отрисовывает содержимое, можно использовать метод, `shareToMicrosoftTeams.renderButtons()` чтобы принудительно отобразить кнопку " **общий доступ** " для соответствующего места в конвейере.</span><span class="sxs-lookup"><span data-stu-id="aee22-117">If your page dynamically renders content, you can use the the `shareToMicrosoftTeams.renderButtons()` method to force the **Share** button to render at the appropriate place in the pipeline.</span></span>

## <a name="crafting-your-website-preview"></a><span data-ttu-id="aee22-118">Создание предварительной версии веб-сайта</span><span class="sxs-lookup"><span data-stu-id="aee22-118">Crafting your website preview</span></span>

<span data-ttu-id="aee22-119">Когда ваш веб-сайт совместно используется в Teams, карточка, вставленная в выбранный канал, будет содержать предварительный просмотр веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="aee22-119">When your website is shared to Teams, the card that is inserted into the selected channel will contain a preview of your website.</span></span> <span data-ttu-id="aee22-120">Вы можете управлять поведением этого предварительного просмотра, убедившись, что соответствующие метаданные добавляются на веб-сайт, к которому предоставлен `data-href` общий доступ (URL-адрес).</span><span class="sxs-lookup"><span data-stu-id="aee22-120">You can control the behavior of this preview by ensuring the appropriate meta-data is added to the website being shared (the `data-href` URL).</span></span> <span data-ttu-id="aee22-121">В таблице ниже представлены необходимые теги.</span><span class="sxs-lookup"><span data-stu-id="aee22-121">The table below outlines the necessary tags.</span></span> <span data-ttu-id="aee22-122">Можно использовать либо версии HTML по умолчанию, либо открытую версию графика.</span><span class="sxs-lookup"><span data-stu-id="aee22-122">You can use either the html default versions, or the Open Graph version.</span></span>

<span data-ttu-id="aee22-123">Для отображения предварительного просмотра необходимо выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="aee22-123">In order for the preview to be displayed you must:</span></span>

* <span data-ttu-id="aee22-124">Включите либо эскиз, либо заголовок и описание (для достижения лучших результатов, включая все три).</span><span class="sxs-lookup"><span data-stu-id="aee22-124">Include either a Thumbnail image, or both a Title and Description (for best results, include all three).</span></span>
* <span data-ttu-id="aee22-125">URL-адрес, к которому предоставлен общий доступ, не может требовать аутентификации.</span><span class="sxs-lookup"><span data-stu-id="aee22-125">The URL being shared cannot require authentication.</span></span> <span data-ttu-id="aee22-126">Если вы по-прежнему можете поделиться им, но Предварительная версия не будет создана.</span><span class="sxs-lookup"><span data-stu-id="aee22-126">If it does you can still share it, but the preview will not be created.</span></span>

|<span data-ttu-id="aee22-127">Значение</span><span class="sxs-lookup"><span data-stu-id="aee22-127">Value</span></span>|<span data-ttu-id="aee22-128">Метатег</span><span class="sxs-lookup"><span data-stu-id="aee22-128">Meta tag</span></span>| <span data-ttu-id="aee22-129">Открытие графика</span><span class="sxs-lookup"><span data-stu-id="aee22-129">Open Graph</span></span>|
|----|----|----|
|<span data-ttu-id="aee22-130">Название</span><span class="sxs-lookup"><span data-stu-id="aee22-130">Title</span></span>|`<meta name="title" content="Example Page Title">`|`<meta property="og:title" content="Example Page Title">`|
|<span data-ttu-id="aee22-131">Описание</span><span class="sxs-lookup"><span data-stu-id="aee22-131">Description</span></span>|`<meta name="description" content="Example Page Description">`|`<meta property="og:description" content="Example Page Description">`|
|<span data-ttu-id="aee22-132">Изображение эскиза</span><span class="sxs-lookup"><span data-stu-id="aee22-132">Thumbnail Image</span></span>| <span data-ttu-id="aee22-133">нет</span><span class="sxs-lookup"><span data-stu-id="aee22-133">none</span></span> |`<meta property="og:image" content="http://example.com/image.jpg">`|

## <a name="share-to-teams-for-education"></a><span data-ttu-id="aee22-134">Совместный доступ к Microsoft Teams для образовательных учреждений</span><span class="sxs-lookup"><span data-stu-id="aee22-134">Share to Teams for Education</span></span>

<span data-ttu-id="aee22-135">Для преподавателей, использующих кнопку Share to Teams, вы получите дополнительные возможности `Create an Assignment`.</span><span class="sxs-lookup"><span data-stu-id="aee22-135">For teachers using the Share to Teams button you'll be given an additional option to `Create an Assignment`.</span></span> <span data-ttu-id="aee22-136">Это позволяет быстро создать назначение в выбранной группе на основе общей ссылки.</span><span class="sxs-lookup"><span data-stu-id="aee22-136">This enables you to quickly create an assignment in the chosen Team based on the shared link.</span></span>

![Открыть доступ к всплывающему меню "команды"](~/assets/images/share-to-teams-popup-edu.png)

## <a name="full-launcherjs-definition"></a><span data-ttu-id="aee22-138">Определение полного загрузчика. js</span><span class="sxs-lookup"><span data-stu-id="aee22-138">Full launcher.js definition</span></span>

| <span data-ttu-id="aee22-139">Свойство</span><span class="sxs-lookup"><span data-stu-id="aee22-139">Property</span></span> | <span data-ttu-id="aee22-140">Атрибут HTML</span><span class="sxs-lookup"><span data-stu-id="aee22-140">HTML attribute</span></span> | <span data-ttu-id="aee22-141">Тип</span><span class="sxs-lookup"><span data-stu-id="aee22-141">Type</span></span> | <span data-ttu-id="aee22-142">По умолчанию</span><span class="sxs-lookup"><span data-stu-id="aee22-142">Default</span></span> | <span data-ttu-id="aee22-143">Описание</span><span class="sxs-lookup"><span data-stu-id="aee22-143">Description</span></span> |
| -------------- | ---------------------- | --------------------- | ------- | ---------------------------------------------------------------------- |
| <span data-ttu-id="aee22-144">href</span><span class="sxs-lookup"><span data-stu-id="aee22-144">href</span></span> | `data-href` | <span data-ttu-id="aee22-145">строка</span><span class="sxs-lookup"><span data-stu-id="aee22-145">string</span></span> | <span data-ttu-id="aee22-146">н/д</span><span class="sxs-lookup"><span data-stu-id="aee22-146">n/a</span></span> | <span data-ttu-id="aee22-147">Значение href для общего доступа к контенту.</span><span class="sxs-lookup"><span data-stu-id="aee22-147">The href of the content to share.</span></span> |
| <span data-ttu-id="aee22-148">preview</span><span class="sxs-lookup"><span data-stu-id="aee22-148">preview</span></span> | `data-preview` | <span data-ttu-id="aee22-149">Логическое значение (в виде строки)</span><span class="sxs-lookup"><span data-stu-id="aee22-149">boolean (as a string)</span></span> | `true` | <span data-ttu-id="aee22-150">Указывает, следует ли отображать содержимое для совместного использования.</span><span class="sxs-lookup"><span data-stu-id="aee22-150">Whether or not to show a preview of the content to share.</span></span> |
| <span data-ttu-id="aee22-151">иконпкссизе</span><span class="sxs-lookup"><span data-stu-id="aee22-151">iconPxSize</span></span> | `data-icon-px-size` | <span data-ttu-id="aee22-152">Number (как строка)</span><span class="sxs-lookup"><span data-stu-id="aee22-152">number (as a string)</span></span> | `32` | <span data-ttu-id="aee22-153">Размер в пикселях кнопки Share to Teams для отображения.</span><span class="sxs-lookup"><span data-stu-id="aee22-153">The size in pixels of the Share-to-Teams button to render.</span></span> |
| <span data-ttu-id="aee22-154">мсгтекст</span><span class="sxs-lookup"><span data-stu-id="aee22-154">msgText</span></span> | `data-msg-text` | <span data-ttu-id="aee22-155">строка</span><span class="sxs-lookup"><span data-stu-id="aee22-155">string</span></span> | <span data-ttu-id="aee22-156">н/д</span><span class="sxs-lookup"><span data-stu-id="aee22-156">n/a</span></span> | <span data-ttu-id="aee22-157">Текст по умолчанию, вставляемый перед ссылкой в поле создания сообщения (предельное число знаков в 200)</span><span class="sxs-lookup"><span data-stu-id="aee22-157">Default Text to be inserted before the link in the message compose box (200 character limit)</span></span> |
| <span data-ttu-id="aee22-158">ассигнинстр</span><span class="sxs-lookup"><span data-stu-id="aee22-158">assignInstr</span></span> | `data-assign-instr` | <span data-ttu-id="aee22-159">строка</span><span class="sxs-lookup"><span data-stu-id="aee22-159">string</span></span> | <span data-ttu-id="aee22-160">н/д</span><span class="sxs-lookup"><span data-stu-id="aee22-160">n/a</span></span> | <span data-ttu-id="aee22-161">Текст по умолчанию, вставляемый в поле "инструкции" для назначений (количество знаков в 200)</span><span class="sxs-lookup"><span data-stu-id="aee22-161">Default Text to be inserted in the assignments "Instructions" field (200 character limit)</span></span> |
| <span data-ttu-id="aee22-162">ассигнтитле</span><span class="sxs-lookup"><span data-stu-id="aee22-162">assignTitle</span></span> | `data-assign-title` | <span data-ttu-id="aee22-163">строка</span><span class="sxs-lookup"><span data-stu-id="aee22-163">string</span></span> | <span data-ttu-id="aee22-164">н/д</span><span class="sxs-lookup"><span data-stu-id="aee22-164">n/a</span></span> | <span data-ttu-id="aee22-165">Текст по умолчанию, вставляемый в поле "название" для назначений (50 знаков)</span><span class="sxs-lookup"><span data-stu-id="aee22-165">Default Text to be inserted in the assignments "Title" field (50 character limit)</span></span> |

### <a name="methods"></a><span data-ttu-id="aee22-166">Методы</span><span class="sxs-lookup"><span data-stu-id="aee22-166">Methods</span></span>

**`shareToMicrosoftTeams.renderButtons(options)`**

<span data-ttu-id="aee22-167">`options`(необязательно):`{ elements?: HTMLElement[] }`</span><span class="sxs-lookup"><span data-stu-id="aee22-167">`options` (optional): `{ elements?: HTMLElement[] }`</span></span>

<span data-ttu-id="aee22-168">Отображает все кнопки общего доступа на странице.</span><span class="sxs-lookup"><span data-stu-id="aee22-168">Renders all share buttons currently on the page.</span></span> <span data-ttu-id="aee22-169">Если необязательный `options` объект предоставляется со списком элементов, эти элементы отображаются на кнопках совместного использования.</span><span class="sxs-lookup"><span data-stu-id="aee22-169">If an optional `options` object is supplied with a list of elements, those elements will be rendered into share buttons.</span></span>

### <a name="setting-default-form-values"></a><span data-ttu-id="aee22-170">Установка значений формы по умолчанию</span><span class="sxs-lookup"><span data-stu-id="aee22-170">Setting default form values</span></span>

<span data-ttu-id="aee22-171">При необходимости можно задать значения по умолчанию для следующих полей в форме Share to teams:</span><span class="sxs-lookup"><span data-stu-id="aee22-171">Optionally, you can choose to set default values for the following fields on the Share to Teams form:</span></span>

* <span data-ttu-id="aee22-172">Произнесите что-то`msgText`вроде this ().</span><span class="sxs-lookup"><span data-stu-id="aee22-172">Say something about this (`msgText`)</span></span>
* <span data-ttu-id="aee22-173">Инструкции по назначению (`assignInstr`)</span><span class="sxs-lookup"><span data-stu-id="aee22-173">Assignment Instructions (`assignInstr`)</span></span>
* <span data-ttu-id="aee22-174">Название назначения (`assignTitle`)</span><span class="sxs-lookup"><span data-stu-id="aee22-174">Assignment Title (`assignTitle`)</span></span>

#### <a name="example-default-form-values"></a><span data-ttu-id="aee22-175">Пример: значения формы по умолчанию</span><span class="sxs-lookup"><span data-stu-id="aee22-175">Example: Default form values</span></span>

```html
<span
    class="teams-share-button"
    data-href="https://www.microsoft.com/education/products/teams"
    data-msg-text="Default Message"
    data-assign-title="Default Assignment Title"
    data-assign-instr="Default Assignment Instructions"
></span>
```