---
title: Создание кнопки Share-to-Teams
description: Добавление встроенной кнопки Share to Teams на веб-сайте
ms.topic: reference
localization_priority: Normal
keywords: Share Teams Share-to-Teams
ms.openlocfilehash: c77c4149c95685e17e8f789a9536b4d81e05d13f
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020825"
---
# <a name="create-share-to-teams-button"></a><span data-ttu-id="ee482-104">Создание кнопки Share-to-Teams</span><span class="sxs-lookup"><span data-stu-id="ee482-104">Create Share-to-Teams button</span></span>

<span data-ttu-id="ee482-105">Сторонние веб-сайты могут использовать сценарий запуска для встраив кнопки Share-to-Teams на своих веб-сайтах.</span><span class="sxs-lookup"><span data-stu-id="ee482-105">Third-party websites can use the launcher script to embed Share-to-Teams buttons on their webpages.</span></span> <span data-ttu-id="ee482-106">При выборе запускается опыт share-to-Teams в всплывающее окно.</span><span class="sxs-lookup"><span data-stu-id="ee482-106">When you select, it launches the Share-to-Teams experience in a pop-up window.</span></span> <span data-ttu-id="ee482-107">Это позволяет обмениваться ссылками напрямую с любым человеком или каналом Microsoft Teams без переключения контекста.</span><span class="sxs-lookup"><span data-stu-id="ee482-107">This allows you to share a link directly to any person or Microsoft Teams channel without switching the context.</span></span> <span data-ttu-id="ee482-108">В этом документе вы можете узнать, как создать и встраить кнопку Share-to-Teams для веб-сайта, создать предварительный просмотр веб-сайта и расширить возможности share-to-Teams для образования.</span><span class="sxs-lookup"><span data-stu-id="ee482-108">This document guides you on how to create, and embed a Share-to-Teams button for your website, craft your website preview, and extend Share-to-Teams for Education.</span></span>

> [!NOTE]
> * <span data-ttu-id="ee482-109">Поддерживаются только настольные версии Edge и Chrome.</span><span class="sxs-lookup"><span data-stu-id="ee482-109">Only the desktop versions of Edge and Chrome are supported.</span></span>
> * <span data-ttu-id="ee482-110">Использование учетных записей Freemium или гостевой не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="ee482-110">Use of Freemium or guest accounts is not supported.</span></span>  

<span data-ttu-id="ee482-111">На следующем изображении отображается всплывающее представление share-to-Teams:</span><span class="sxs-lookup"><span data-stu-id="ee482-111">The following image displays the Share-to-Teams pop-up experience:</span></span>

![Всплывающее всплыв](~/assets/images/share-to-teams-popup.png)

## <a name="embed-a-share-to-teams-button"></a><span data-ttu-id="ee482-113">Встраить кнопку Share to Teams</span><span class="sxs-lookup"><span data-stu-id="ee482-113">Embed a Share to Teams button</span></span>

1. <span data-ttu-id="ee482-114">Добавьте `launcher.js` скрипт на веб-страницу.</span><span class="sxs-lookup"><span data-stu-id="ee482-114">Add the `launcher.js` script on your webpage.</span></span>

    ```html
    <script async defer src="https://teams.microsoft.com/share/launcher.js"></script>
    ```

1. <span data-ttu-id="ee482-115">Добавьте элемент HTML на веб-страницу с атрибутом класса и ссылкой, `teams-share-button` которая будет делиться в `data-href` атрибуте.</span><span class="sxs-lookup"><span data-stu-id="ee482-115">Add a HTML element on your webpage with the `teams-share-button` class attribute and the link to share in the `data-href` attribute.</span></span>

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>">
    </div>
    ```

    <span data-ttu-id="ee482-116">После завершения этого значка Microsoft Teams добавляется на ваш веб-сайт.</span><span class="sxs-lookup"><span data-stu-id="ee482-116">After completing this, the Microsoft Teams icon gets added to your website.</span></span> <span data-ttu-id="ee482-117">На следующем изображении показан значок Share-to-Teams:</span><span class="sxs-lookup"><span data-stu-id="ee482-117">The following image shows Share-to-Teams icon:</span></span>

    ![Share to Teams icon](~/assets/icons/share-to-teams-icon.png)

1. <span data-ttu-id="ee482-119">Кроме того, если для кнопки Share-to Teams нужен другой размер значка, используйте `data-icon-px-size` атрибут.</span><span class="sxs-lookup"><span data-stu-id="ee482-119">Alternatively, if you want a different icon size for the Share-to Teams button, use the `data-icon-px-size` attribute.</span></span>

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>"
      data-icon-px-size="64">
    </div>
    ```
1. <span data-ttu-id="ee482-120">Если общая ссылка требует проверки подлинности пользователя, а предварительный просмотр URL-адреса из общей ссылки не будет хорошо отрисовки в Teams, можно отключить предварительный просмотр URL-адреса, добавив набор `data-preview` `false` атрибутов.</span><span class="sxs-lookup"><span data-stu-id="ee482-120">If the shared link requires user authentication, and the URL preview from your link to be shared does not render well in Teams then, you can disable the URL preview by adding the `data-preview` attribute set to `false`.</span></span>

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>"
      data-preview="false">
    </div>
    ```

1. <span data-ttu-id="ee482-121">Если на странице динамически отрисовка контента, можно использовать метод, чтобы заставить кнопку Share отрисовки в нужном месте `shareToMicrosoftTeams.renderButtons()` в конвейере. </span><span class="sxs-lookup"><span data-stu-id="ee482-121">If your page dynamically renders content, you can use the the `shareToMicrosoftTeams.renderButtons()` method to force the **Share** button to render at the appropriate place in the pipeline.</span></span>

## <a name="craft-your-website-preview"></a><span data-ttu-id="ee482-122">Создайте предварительный просмотр веб-сайта</span><span class="sxs-lookup"><span data-stu-id="ee482-122">Craft your website preview</span></span>

<span data-ttu-id="ee482-123">Когда веб-сайт является общим для Teams, карта, вставленная в выбранный канал, содержит предварительный просмотр веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="ee482-123">When your website is shared to Teams, the card that is inserted into the selected channel contains a preview of your website.</span></span> <span data-ttu-id="ee482-124">Вы можете управлять поведением этого предварительного просмотра, обеспечивая добавление соответствующих метаданных на общий веб-сайт, например `data-href` URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="ee482-124">You can control the behavior of this preview by ensuring the appropriate meta-data is added to the website being shared, such as the `data-href` URL.</span></span>  

<span data-ttu-id="ee482-125">**Отображение предварительного просмотра**</span><span class="sxs-lookup"><span data-stu-id="ee482-125">**To display the preview**</span></span>

* <span data-ttu-id="ee482-126">Вы должны включить либо **изображение эскиза**, или как **название и** **описание**.</span><span class="sxs-lookup"><span data-stu-id="ee482-126">You must include either a **Thumbnail image**, or both a **Title** and **Description**.</span></span> <span data-ttu-id="ee482-127">Для наилучших результатов включаем все три.</span><span class="sxs-lookup"><span data-stu-id="ee482-127">For best results, include all three.</span></span>
* <span data-ttu-id="ee482-128">Общий URL-адрес не требует проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="ee482-128">The shared URL does not require authentication.</span></span> <span data-ttu-id="ee482-129">Если для этого требуется проверка подлинности, вы можете поделиться им, но предварительный просмотр не создан.</span><span class="sxs-lookup"><span data-stu-id="ee482-129">If it requires authentication, you can share it, but the preview is not created.</span></span>

<span data-ttu-id="ee482-130">В следующей таблице описаны необходимые теги:</span><span class="sxs-lookup"><span data-stu-id="ee482-130">The following table outlines the necessary tags:</span></span>

|<span data-ttu-id="ee482-131">Значение</span><span class="sxs-lookup"><span data-stu-id="ee482-131">Value</span></span>|<span data-ttu-id="ee482-132">Метатег</span><span class="sxs-lookup"><span data-stu-id="ee482-132">Meta tag</span></span>| <span data-ttu-id="ee482-133">Open Graph</span><span class="sxs-lookup"><span data-stu-id="ee482-133">Open Graph</span></span>|
|----|----|----|
|<span data-ttu-id="ee482-134">Название</span><span class="sxs-lookup"><span data-stu-id="ee482-134">Title</span></span>|`<meta name="title" content="Example Page Title">`|`<meta property="og:title" content="Example Page Title">`|
|<span data-ttu-id="ee482-135">Описание</span><span class="sxs-lookup"><span data-stu-id="ee482-135">Description</span></span>|`<meta name="description" content="Example Page Description">`|`<meta property="og:description" content="Example Page Description">`|
|<span data-ttu-id="ee482-136">Эскиз изображения</span><span class="sxs-lookup"><span data-stu-id="ee482-136">Thumbnail Image</span></span>| <span data-ttu-id="ee482-137">нет.</span><span class="sxs-lookup"><span data-stu-id="ee482-137">none.</span></span> |`<meta property="og:image" content="http://example.com/image.jpg">`|

<span data-ttu-id="ee482-138">Можно использовать либо html-версии по умолчанию, либо версию Open Graph.</span><span class="sxs-lookup"><span data-stu-id="ee482-138">You can use either the html default versions, or the Open Graph version.</span></span>

## <a name="share-to-teams-for-education"></a><span data-ttu-id="ee482-139">Share to Teams for Education</span><span class="sxs-lookup"><span data-stu-id="ee482-139">Share to Teams for Education</span></span>

<span data-ttu-id="ee482-140">Для преподавателей, использующих кнопку Share to Teams, существует дополнительный параметр `Create an Assignment` .</span><span class="sxs-lookup"><span data-stu-id="ee482-140">For teachers using the Share to Teams button, there is an additional option to `Create an Assignment`.</span></span> <span data-ttu-id="ee482-141">Это позволяет быстро создавать назначение в выбранной команде на основе общей ссылки.</span><span class="sxs-lookup"><span data-stu-id="ee482-141">This enables you to quickly create an assignment in the chosen Team, based on the shared link.</span></span> <span data-ttu-id="ee482-142">На следующем изображении отображается share-to-Teams для образования:</span><span class="sxs-lookup"><span data-stu-id="ee482-142">The following image displays Share-to-Teams for education:</span></span> 

![Share to Teams popup education](~/assets/images/share-to-teams-popup-edu.png)

## <a name="full-launcherjs-definition"></a><span data-ttu-id="ee482-144">Полное launcher.js определение</span><span class="sxs-lookup"><span data-stu-id="ee482-144">Full launcher.js definition</span></span>

| <span data-ttu-id="ee482-145">Свойство</span><span class="sxs-lookup"><span data-stu-id="ee482-145">Property</span></span> | <span data-ttu-id="ee482-146">Атрибут HTML</span><span class="sxs-lookup"><span data-stu-id="ee482-146">HTML attribute</span></span> | <span data-ttu-id="ee482-147">Type</span><span class="sxs-lookup"><span data-stu-id="ee482-147">Type</span></span> | <span data-ttu-id="ee482-148">По умолчанию</span><span class="sxs-lookup"><span data-stu-id="ee482-148">Default</span></span> | <span data-ttu-id="ee482-149">Описание</span><span class="sxs-lookup"><span data-stu-id="ee482-149">Description</span></span> |
| -------------- | ---------------------- | --------------------- | ------- | ---------------------------------------------------------------------- |
| <span data-ttu-id="ee482-150">href</span><span class="sxs-lookup"><span data-stu-id="ee482-150">href</span></span> | `data-href` | <span data-ttu-id="ee482-151">String</span><span class="sxs-lookup"><span data-stu-id="ee482-151">string</span></span> | <span data-ttu-id="ee482-152">н/д</span><span class="sxs-lookup"><span data-stu-id="ee482-152">n/a</span></span> | <span data-ttu-id="ee482-153">Href контента для обмена.</span><span class="sxs-lookup"><span data-stu-id="ee482-153">The href of the content to share.</span></span> |
| <span data-ttu-id="ee482-154">preview</span><span class="sxs-lookup"><span data-stu-id="ee482-154">preview</span></span> | `data-preview` | <span data-ttu-id="ee482-155">boolean (как строка)</span><span class="sxs-lookup"><span data-stu-id="ee482-155">boolean (as a string)</span></span> | `true` | <span data-ttu-id="ee482-156">Следует ли показывать предварительный просмотр контента для обмена.</span><span class="sxs-lookup"><span data-stu-id="ee482-156">Whether or not to show a preview of the content to share.</span></span> |
| <span data-ttu-id="ee482-157">iconPxSize</span><span class="sxs-lookup"><span data-stu-id="ee482-157">iconPxSize</span></span> | `data-icon-px-size` | <span data-ttu-id="ee482-158">номер (в качестве строки)</span><span class="sxs-lookup"><span data-stu-id="ee482-158">number (as a string)</span></span> | `32` | <span data-ttu-id="ee482-159">Размер пикселей кнопки Share-to-Teams для отрисовки.</span><span class="sxs-lookup"><span data-stu-id="ee482-159">The size in pixels of the Share-to-Teams button to render.</span></span> |
| <span data-ttu-id="ee482-160">msgText</span><span class="sxs-lookup"><span data-stu-id="ee482-160">msgText</span></span> | `data-msg-text` | <span data-ttu-id="ee482-161">String</span><span class="sxs-lookup"><span data-stu-id="ee482-161">string</span></span> | <span data-ttu-id="ee482-162">н/д</span><span class="sxs-lookup"><span data-stu-id="ee482-162">n/a</span></span> | <span data-ttu-id="ee482-163">Текст по умолчанию должен быть вставлен перед ссылкой в поле для составить сообщение.</span><span class="sxs-lookup"><span data-stu-id="ee482-163">Default Text to be inserted before the link in the message compose box.</span></span> <span data-ttu-id="ee482-164">Максимальное число символов — 200.</span><span class="sxs-lookup"><span data-stu-id="ee482-164">Maximum number of characters is 200.</span></span> |
| <span data-ttu-id="ee482-165">assignInstr</span><span class="sxs-lookup"><span data-stu-id="ee482-165">assignInstr</span></span> | `data-assign-instr` | <span data-ttu-id="ee482-166">String</span><span class="sxs-lookup"><span data-stu-id="ee482-166">string</span></span> | <span data-ttu-id="ee482-167">н/д</span><span class="sxs-lookup"><span data-stu-id="ee482-167">n/a</span></span> | <span data-ttu-id="ee482-168">Текст по умолчанию, который будет вставлен в поле "Инструкции".</span><span class="sxs-lookup"><span data-stu-id="ee482-168">Default Text to be inserted in the assignments "Instructions" field.</span></span> <span data-ttu-id="ee482-169">Максимальное число символов — 200.</span><span class="sxs-lookup"><span data-stu-id="ee482-169">Maximum number of characters is 200.</span></span> |
| <span data-ttu-id="ee482-170">assignTitle</span><span class="sxs-lookup"><span data-stu-id="ee482-170">assignTitle</span></span> | `data-assign-title` | <span data-ttu-id="ee482-171">String</span><span class="sxs-lookup"><span data-stu-id="ee482-171">string</span></span> | <span data-ttu-id="ee482-172">н/д</span><span class="sxs-lookup"><span data-stu-id="ee482-172">n/a</span></span> | <span data-ttu-id="ee482-173">Текст по умолчанию, который будет вставлен в поле "Title".</span><span class="sxs-lookup"><span data-stu-id="ee482-173">Default Text to be inserted in the assignments "Title" field.</span></span> <span data-ttu-id="ee482-174">Максимальное число символов — 50.</span><span class="sxs-lookup"><span data-stu-id="ee482-174">Maximum number of characters is 50.</span></span> |

### <a name="methods"></a><span data-ttu-id="ee482-175">Methods</span><span class="sxs-lookup"><span data-stu-id="ee482-175">Methods</span></span>

**`shareToMicrosoftTeams.renderButtons(options)`**

<span data-ttu-id="ee482-176">`options` (необязательный): `{ elements?: HTMLElement[] }`</span><span class="sxs-lookup"><span data-stu-id="ee482-176">`options` (optional): `{ elements?: HTMLElement[] }`</span></span>

<span data-ttu-id="ee482-177">В настоящее время все кнопки обмена отрисовка на странице.</span><span class="sxs-lookup"><span data-stu-id="ee482-177">Currently, all share buttons are rendered on the page.</span></span> <span data-ttu-id="ee482-178">Если необязательный объект снабжен списком элементов, эти элементы `options` отрисовыются в кнопки share.</span><span class="sxs-lookup"><span data-stu-id="ee482-178">If an optional `options` object is supplied with a list of elements, those elements are rendered into share buttons.</span></span>

### <a name="set-default-form-values"></a><span data-ttu-id="ee482-179">Настройка значений форм по умолчанию</span><span class="sxs-lookup"><span data-stu-id="ee482-179">Set default form values</span></span>

<span data-ttu-id="ee482-180">Можно выбрать для набора значений по умолчанию для следующих полей в форме Share to Teams:</span><span class="sxs-lookup"><span data-stu-id="ee482-180">You can select to set default values for the following fields on the Share to Teams form:</span></span>

* <span data-ttu-id="ee482-181">Скажите что-нибудь об этом: `msgText`</span><span class="sxs-lookup"><span data-stu-id="ee482-181">Say something about this: `msgText`</span></span>
* <span data-ttu-id="ee482-182">Инструкции по назначению: `assignInstr`</span><span class="sxs-lookup"><span data-stu-id="ee482-182">Assignment Instructions: `assignInstr`</span></span>
* <span data-ttu-id="ee482-183">Название назначения: `assignTitle`</span><span class="sxs-lookup"><span data-stu-id="ee482-183">Assignment Title: `assignTitle`</span></span>

#### <a name="example"></a><span data-ttu-id="ee482-184">Пример</span><span class="sxs-lookup"><span data-stu-id="ee482-184">Example</span></span>

 <span data-ttu-id="ee482-185">Значения форм по умолчанию даются в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="ee482-185">Default form values are given in the following example:</span></span>

```html
<span
    class="teams-share-button"
    data-href="https://www.microsoft.com/education/products/teams"
    data-msg-text="Default Message"
    data-assign-title="Default Assignment Title"
    data-assign-instr="Default Assignment Instructions"
></span>
```

## <a name="see-also"></a><span data-ttu-id="ee482-186">См. также</span><span class="sxs-lookup"><span data-stu-id="ee482-186">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ee482-187">Интеграция веб-приложений</span><span class="sxs-lookup"><span data-stu-id="ee482-187">Integrate web apps</span></span>](~/samples/integrate-web-apps-overview.md)
