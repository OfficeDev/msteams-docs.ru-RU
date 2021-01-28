---
title: Создание кнопки «Поделиться в Teams»
description: Добавление встроенной кнопки "Поделиться в Teams" на веб-сайте
ms.topic: reference
keywords: Совместное share-to-Teams Teams
ms.openlocfilehash: 46091c957137cc871095ca6a57c0d61fa79d9458
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014336"
---
# <a name="create-a-share-to-teams-button-for-your-website"></a><span data-ttu-id="25442-104">Создайте кнопку «Поделиться в Teams» для своего сайта</span><span class="sxs-lookup"><span data-stu-id="25442-104">Create a Share-to-Teams button for your website</span></span>

>[!NOTE]
> * <span data-ttu-id="25442-105">Поддерживаются только классические версии Edge и Chrome.</span><span class="sxs-lookup"><span data-stu-id="25442-105">Only the desktop versions of Edge and Chrome are supported.</span></span>
> * <span data-ttu-id="25442-106">Использование учетных записей Freemium или гостевых учетных записей не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="25442-106">Use of Freemium or guest accounts is not supported.</span></span>

<span data-ttu-id="25442-107">Сторонние веб-сайты могут использовать сценарий запуска, чтобы встраить кнопки "Поделиться" в teams на своих веб-странице, что позволит при нажатии на них запускать окне "Поделиться в Teams" во всплывающее окно.</span><span class="sxs-lookup"><span data-stu-id="25442-107">Third-party websites can use the launcher script to embed Share to Teams buttons on their webpages which will launch the Share to Teams experience in a popup window when clicked.</span></span> <span data-ttu-id="25442-108">Это позволит вам делиться ссылкой непосредственно с любым человеком или каналом Microsoft Teams без переключения контекста.</span><span class="sxs-lookup"><span data-stu-id="25442-108">This will allow you to share a link directly to any person or Microsoft Teams channel without switching context.</span></span>

![Всплывающее всплывающее окна "Поделиться в Teams"](~/assets/images/share-to-teams-popup.png)

## <a name="how-to-embed-a-share-to-teams-button"></a><span data-ttu-id="25442-110">Как встраить кнопку "Поделиться" в Teams</span><span class="sxs-lookup"><span data-stu-id="25442-110">How to embed a Share to Teams button</span></span>

<span data-ttu-id="25442-111">Сначала необходимо добавить сценарий `launcher.js` на веб-страницу.</span><span class="sxs-lookup"><span data-stu-id="25442-111">First, you'll need to add the `launcher.js` script on your webpage.</span></span>

```html
<script async defer src="https://teams.microsoft.com/share/launcher.js"></script>
```

<span data-ttu-id="25442-112">Затем добавьте htmL-элемент на веб-страницу с атрибутом класса и ссылкой для совместной использования `teams-share-button` в `data-href` атрибуте.</span><span class="sxs-lookup"><span data-stu-id="25442-112">Next, add an HTML element on your webpage with the `teams-share-button` class attribute and the link to share in the `data-href` attribute.</span></span>

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>">
</div>
```

<span data-ttu-id="25442-113">Это добавит значок Microsoft Teams на ваш веб-сайт.</span><span class="sxs-lookup"><span data-stu-id="25442-113">This will add the Microsoft Teams icon to your website.</span></span>

![Значок "Поделиться в Teams"](~/assets/icons/share-to-teams-icon.png)

<span data-ttu-id="25442-115">При желании, если вы хотите использовать другой размер значка для кнопки "Поделиться в Teams", используйте `data-icon-px-size` атрибут.</span><span class="sxs-lookup"><span data-stu-id="25442-115">Optionally, if you want a different icon size for the Share to Teams button, use the `data-icon-px-size` attribute.</span></span>

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>"
  data-icon-px-size="64">
</div>
```

<span data-ttu-id="25442-116">Если вы знаете, что предварительный просмотр URL-адреса из ссылки для совместного просмотра не будет хорошо отрисовки в Teams (например, ссылка требует проверки подлинности пользователя), вы можете отключить предварительный просмотр URL-адресов, добавив атрибут, установленный в `data-preview` `false` .</span><span class="sxs-lookup"><span data-stu-id="25442-116">If you know that the URL preview from your link to be shared won't render well in Teams (for example the link would require user authentication) you can disable the URL preview by adding the `data-preview` attribute set to `false`.</span></span>

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>"
  data-preview="false">
</div>
```

<span data-ttu-id="25442-117">Если страница динамически отрисовки содержимого, можно использовать метод для принудительного отображения кнопки "Поделиться" в соответствующем `shareToMicrosoftTeams.renderButtons()` месте конвейера. </span><span class="sxs-lookup"><span data-stu-id="25442-117">If your page dynamically renders content, you can use the the `shareToMicrosoftTeams.renderButtons()` method to force the **Share** button to render at the appropriate place in the pipeline.</span></span>

## <a name="crafting-your-website-preview"></a><span data-ttu-id="25442-118">Создайте предварительную версию веб-сайта</span><span class="sxs-lookup"><span data-stu-id="25442-118">Crafting your website preview</span></span>

<span data-ttu-id="25442-119">Когда ваш веб-сайт будет общим для Teams, карточка, вставленная в выбранный канал, будет содержать предварительный просмотр вашего веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="25442-119">When your website is shared to Teams, the card that is inserted into the selected channel will contain a preview of your website.</span></span> <span data-ttu-id="25442-120">Вы можете управлять поведением этой предварительной версии, убедившись, что соответствующие метаданные добавлены на веб-сайт для общего просмотра `data-href` (URL-адрес).</span><span class="sxs-lookup"><span data-stu-id="25442-120">You can control the behavior of this preview by ensuring the appropriate meta-data is added to the website being shared (the `data-href` URL).</span></span> <span data-ttu-id="25442-121">В таблице ниже описаны необходимые теги.</span><span class="sxs-lookup"><span data-stu-id="25442-121">The table below outlines the necessary tags.</span></span> <span data-ttu-id="25442-122">Вы можете использовать либо версии html по умолчанию, либо версию Open Graph.</span><span class="sxs-lookup"><span data-stu-id="25442-122">You can use either the html default versions, or the Open Graph version.</span></span>

<span data-ttu-id="25442-123">Чтобы предварительный просмотр отображался, необходимо:</span><span class="sxs-lookup"><span data-stu-id="25442-123">In order for the preview to be displayed you must:</span></span>

* <span data-ttu-id="25442-124">Включаем изображение эскиза или заголовок и описание (для наилучших результатов включаем все три).</span><span class="sxs-lookup"><span data-stu-id="25442-124">Include either a Thumbnail image, or both a Title and Description (for best results, include all three).</span></span>
* <span data-ttu-id="25442-125">URL-адрес, к который требуется общий доступ, не может требовать проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="25442-125">The URL being shared cannot require authentication.</span></span> <span data-ttu-id="25442-126">Если вы по-прежнему можете поделиться им, но предварительный просмотр не будет создан.</span><span class="sxs-lookup"><span data-stu-id="25442-126">If it does you can still share it, but the preview will not be created.</span></span>

|<span data-ttu-id="25442-127">Значение</span><span class="sxs-lookup"><span data-stu-id="25442-127">Value</span></span>|<span data-ttu-id="25442-128">Метатег</span><span class="sxs-lookup"><span data-stu-id="25442-128">Meta tag</span></span>| <span data-ttu-id="25442-129">Open Graph</span><span class="sxs-lookup"><span data-stu-id="25442-129">Open Graph</span></span>|
|----|----|----|
|<span data-ttu-id="25442-130">Название</span><span class="sxs-lookup"><span data-stu-id="25442-130">Title</span></span>|`<meta name="title" content="Example Page Title">`|`<meta property="og:title" content="Example Page Title">`|
|<span data-ttu-id="25442-131">Описание</span><span class="sxs-lookup"><span data-stu-id="25442-131">Description</span></span>|`<meta name="description" content="Example Page Description">`|`<meta property="og:description" content="Example Page Description">`|
|<span data-ttu-id="25442-132">Эскиз</span><span class="sxs-lookup"><span data-stu-id="25442-132">Thumbnail Image</span></span>| <span data-ttu-id="25442-133">Нет</span><span class="sxs-lookup"><span data-stu-id="25442-133">none</span></span> |`<meta property="og:image" content="http://example.com/image.jpg">`|

## <a name="share-to-teams-for-education"></a><span data-ttu-id="25442-134">Совместное участие в Teams для образования</span><span class="sxs-lookup"><span data-stu-id="25442-134">Share to Teams for Education</span></span>

<span data-ttu-id="25442-135">Преподавателям, использующим кнопку "Поделиться в Teams", будет предоставлен дополнительный параметр `Create an Assignment` .</span><span class="sxs-lookup"><span data-stu-id="25442-135">For teachers using the Share to Teams button you'll be given an additional option to `Create an Assignment`.</span></span> <span data-ttu-id="25442-136">Это позволяет быстро создать назначение в выбранной команде на основе общей ссылки.</span><span class="sxs-lookup"><span data-stu-id="25442-136">This enables you to quickly create an assignment in the chosen Team based on the shared link.</span></span>

![Всплывающее всплывающее окна "Поделиться в Teams"](~/assets/images/share-to-teams-popup-edu.png)

## <a name="full-launcherjs-definition"></a><span data-ttu-id="25442-138">Полное launcher.js определения</span><span class="sxs-lookup"><span data-stu-id="25442-138">Full launcher.js definition</span></span>

| <span data-ttu-id="25442-139">Свойство</span><span class="sxs-lookup"><span data-stu-id="25442-139">Property</span></span> | <span data-ttu-id="25442-140">Атрибут HTML</span><span class="sxs-lookup"><span data-stu-id="25442-140">HTML attribute</span></span> | <span data-ttu-id="25442-141">Тип</span><span class="sxs-lookup"><span data-stu-id="25442-141">Type</span></span> | <span data-ttu-id="25442-142">По умолчанию</span><span class="sxs-lookup"><span data-stu-id="25442-142">Default</span></span> | <span data-ttu-id="25442-143">Описание</span><span class="sxs-lookup"><span data-stu-id="25442-143">Description</span></span> |
| -------------- | ---------------------- | --------------------- | ------- | ---------------------------------------------------------------------- |
| <span data-ttu-id="25442-144">href</span><span class="sxs-lookup"><span data-stu-id="25442-144">href</span></span> | `data-href` | <span data-ttu-id="25442-145">string</span><span class="sxs-lookup"><span data-stu-id="25442-145">string</span></span> | <span data-ttu-id="25442-146">н/д</span><span class="sxs-lookup"><span data-stu-id="25442-146">n/a</span></span> | <span data-ttu-id="25442-147">Href содержимого для совместной работы.</span><span class="sxs-lookup"><span data-stu-id="25442-147">The href of the content to share.</span></span> |
| <span data-ttu-id="25442-148">preview</span><span class="sxs-lookup"><span data-stu-id="25442-148">preview</span></span> | `data-preview` | <span data-ttu-id="25442-149">boolean (в качестве строки)</span><span class="sxs-lookup"><span data-stu-id="25442-149">boolean (as a string)</span></span> | `true` | <span data-ttu-id="25442-150">Следует ли показывать предварительный просмотр содержимого для демонстрации.</span><span class="sxs-lookup"><span data-stu-id="25442-150">Whether or not to show a preview of the content to share.</span></span> |
| <span data-ttu-id="25442-151">iconPxSize</span><span class="sxs-lookup"><span data-stu-id="25442-151">iconPxSize</span></span> | `data-icon-px-size` | <span data-ttu-id="25442-152">number (в строке)</span><span class="sxs-lookup"><span data-stu-id="25442-152">number (as a string)</span></span> | `32` | <span data-ttu-id="25442-153">Размер в пикселях кнопки share-to-Teams для отрисовки.</span><span class="sxs-lookup"><span data-stu-id="25442-153">The size in pixels of the Share-to-Teams button to render.</span></span> |
| <span data-ttu-id="25442-154">msgText</span><span class="sxs-lookup"><span data-stu-id="25442-154">msgText</span></span> | `data-msg-text` | <span data-ttu-id="25442-155">string</span><span class="sxs-lookup"><span data-stu-id="25442-155">string</span></span> | <span data-ttu-id="25442-156">н/д</span><span class="sxs-lookup"><span data-stu-id="25442-156">n/a</span></span> | <span data-ttu-id="25442-157">Текст по умолчанию, вставляемый перед ссылкой в поле составить сообщение (ограничение в 200 символов)</span><span class="sxs-lookup"><span data-stu-id="25442-157">Default Text to be inserted before the link in the message compose box (200 character limit)</span></span> |
| <span data-ttu-id="25442-158">assignInstr</span><span class="sxs-lookup"><span data-stu-id="25442-158">assignInstr</span></span> | `data-assign-instr` | <span data-ttu-id="25442-159">string</span><span class="sxs-lookup"><span data-stu-id="25442-159">string</span></span> | <span data-ttu-id="25442-160">н/д</span><span class="sxs-lookup"><span data-stu-id="25442-160">n/a</span></span> | <span data-ttu-id="25442-161">Текст по умолчанию, вставляемый в поле "Инструкции" (ограничение в 200 символов)</span><span class="sxs-lookup"><span data-stu-id="25442-161">Default Text to be inserted in the assignments "Instructions" field (200 character limit)</span></span> |
| <span data-ttu-id="25442-162">assignTitle</span><span class="sxs-lookup"><span data-stu-id="25442-162">assignTitle</span></span> | `data-assign-title` | <span data-ttu-id="25442-163">string</span><span class="sxs-lookup"><span data-stu-id="25442-163">string</span></span> | <span data-ttu-id="25442-164">н/д</span><span class="sxs-lookup"><span data-stu-id="25442-164">n/a</span></span> | <span data-ttu-id="25442-165">Текст по умолчанию, вставляемый в поле "Название" (ограничение в 50 символов)</span><span class="sxs-lookup"><span data-stu-id="25442-165">Default Text to be inserted in the assignments "Title" field (50 character limit)</span></span> |

### <a name="methods"></a><span data-ttu-id="25442-166">Методы</span><span class="sxs-lookup"><span data-stu-id="25442-166">Methods</span></span>

**`shareToMicrosoftTeams.renderButtons(options)`**

<span data-ttu-id="25442-167">`options` (необязательно): `{ elements?: HTMLElement[] }`</span><span class="sxs-lookup"><span data-stu-id="25442-167">`options` (optional): `{ elements?: HTMLElement[] }`</span></span>

<span data-ttu-id="25442-168">Отрисовка всех кнопок для совместной оказания услуг, которые в настоящее время находятся на странице.</span><span class="sxs-lookup"><span data-stu-id="25442-168">Renders all share buttons currently on the page.</span></span> <span data-ttu-id="25442-169">Если необязательный объект предоставляется со списком элементов, эти элементы будут отрисовыны в кнопки `options` для совместной работы.</span><span class="sxs-lookup"><span data-stu-id="25442-169">If an optional `options` object is supplied with a list of elements, those elements will be rendered into share buttons.</span></span>

### <a name="setting-default-form-values"></a><span data-ttu-id="25442-170">Установка значений формы по умолчанию</span><span class="sxs-lookup"><span data-stu-id="25442-170">Setting default form values</span></span>

<span data-ttu-id="25442-171">При желании вы можете установить значения по умолчанию для следующих полей в форме "Поделиться в Teams":</span><span class="sxs-lookup"><span data-stu-id="25442-171">Optionally, you can choose to set default values for the following fields on the Share to Teams form:</span></span>

* <span data-ttu-id="25442-172">Скажите что-нибудь об этом ( `msgText` )</span><span class="sxs-lookup"><span data-stu-id="25442-172">Say something about this (`msgText`)</span></span>
* <span data-ttu-id="25442-173">Инструкции по назначению ( `assignInstr` )</span><span class="sxs-lookup"><span data-stu-id="25442-173">Assignment Instructions (`assignInstr`)</span></span>
* <span data-ttu-id="25442-174">Заголовок назначения ( `assignTitle` )</span><span class="sxs-lookup"><span data-stu-id="25442-174">Assignment Title (`assignTitle`)</span></span>

#### <a name="example-default-form-values"></a><span data-ttu-id="25442-175">Пример: значения форм по умолчанию</span><span class="sxs-lookup"><span data-stu-id="25442-175">Example: Default form values</span></span>

```html
<span
    class="teams-share-button"
    data-href="https://www.microsoft.com/education/products/teams"
    data-msg-text="Default Message"
    data-assign-title="Default Assignment Title"
    data-assign-instr="Default Assignment Instructions"
></span>
```
