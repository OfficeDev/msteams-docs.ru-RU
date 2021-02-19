---
title: Интеграция возможностей мультимедиа
description: Использование SDK клиента Teams JavaScript для обеспечения возможностей мультимедиа
keywords: Возможности микрофона изображения камеры для носителей разрешений на устройства
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 4876b4de9340cc2bd27a14e363954573ea42f05d
ms.sourcegitcommit: 6ff8d1244ac386641ebf9401804b8df3854b02dc
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/18/2021
ms.locfileid: "50294742"
---
# <a name="integrate-media-capabilities"></a><span data-ttu-id="b18e7-104">Интеграция возможностей мультимедиа</span><span class="sxs-lookup"><span data-stu-id="b18e7-104">Integrate media capabilities</span></span> 

<span data-ttu-id="b18e7-105">В этом документе содержится руководство по интеграции возможностей мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="b18e7-105">This document guides you on how to integrate media capabilities.</span></span> <span data-ttu-id="b18e7-106">Эта интеграция объединяет родной потенциал  устройства, например камеру и **микрофон с** платформой Teams.</span><span class="sxs-lookup"><span data-stu-id="b18e7-106">This integration combines the native device capabilities, such as the **camera** and **microphone** with the Teams platform.</span></span>  

<span data-ttu-id="b18e7-107">Вы можете использовать [клиент microsoft Teams JavaScript SDK,](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)который предоставляет средства, необходимые вашему приложению для доступа к разрешениям на [устройства пользователя.](native-device-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="b18e7-107">You can use [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), that provides the tools necessary for your app to access a user’s [device permissions](native-device-permissions.md).</span></span> <span data-ttu-id="b18e7-108">Используйте **подходящие** API средств массовой информации для интеграции  родных возможностей устройства, например камеры и микрофона с платформой Teams в мобильном приложении Microsoft Teams, и создания более богатого опыта. </span><span class="sxs-lookup"><span data-stu-id="b18e7-108">Use suitable  **media capability APIs** to integrate the native device capabilities, such as the **camera** and **microphone** with the Teams platform within your Microsoft Teams mobile app, and build a richer experience.</span></span> 

## <a name="advantage-of-integrating-media-capabilities"></a><span data-ttu-id="b18e7-109">Преимущество интеграции возможностей мультимедиа</span><span class="sxs-lookup"><span data-stu-id="b18e7-109">Advantage of integrating media capabilities</span></span>

<span data-ttu-id="b18e7-110">Основное преимущество интеграции возможностей устройств в приложениях Teams заключается в том, что он использует элементы управления native Teams, чтобы обеспечить пользователям богатый и захватывающий опыт.</span><span class="sxs-lookup"><span data-stu-id="b18e7-110">The main advantage of integrating device capabilities in your Teams apps is it leverages native Teams controls to provide a rich and immersive experience to your users.</span></span>
<span data-ttu-id="b18e7-111">Чтобы интегрировать возможности мультимедиа, необходимо обновить файл манифеста приложения и вызвать API средств массовой информации.</span><span class="sxs-lookup"><span data-stu-id="b18e7-111">To integrate media capabilities you must update the app manifest file and call the media capability APIs.</span></span> 

<span data-ttu-id="b18e7-112">Для эффективной интеграции необходимо хорошо [](#code-snippets) понимать фрагменты кода для вызова соответствующих API, которые позволяют использовать возможности родного мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="b18e7-112">For effective integration, you must have a good understanding of [code snippets](#code-snippets) for calling the respective APIs, which allow you to use native media capabilities.</span></span>

<span data-ttu-id="b18e7-113">Важно ознакомиться с ошибками [ответа API](#error-handling) для обработки ошибок в приложении Teams.</span><span class="sxs-lookup"><span data-stu-id="b18e7-113">It is important to familiarize yourself with the [API response errors](#error-handling) to handle the errors in your Teams app.</span></span>

> [!NOTE] 
> <span data-ttu-id="b18e7-114">В настоящее время поддержка microsoft Teams для средств массовой информации доступна только для мобильных клиентов.</span><span class="sxs-lookup"><span data-stu-id="b18e7-114">Currently, Microsoft Teams support for media capabilities is only available for mobile clients.</span></span>

## <a name="update-manifest"></a><span data-ttu-id="b18e7-115">Манифест обновления</span><span class="sxs-lookup"><span data-stu-id="b18e7-115">Update manifest</span></span>

<span data-ttu-id="b18e7-116">Обновите приложение Teams [manifest.jsфайле,](../../resources/schema/manifest-schema.md#devicepermissions) добавив `devicePermissions` свойство и указав `media` .</span><span class="sxs-lookup"><span data-stu-id="b18e7-116">Update your Teams app [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) file by adding the `devicePermissions` property and specifying `media`.</span></span> <span data-ttu-id="b18e7-117">Это позволяет приложению запросить необходимые разрешения у пользователей, прежде чем они начнут использовать камеру для захвата изображения, открыть  галерею, чтобы выбрать изображение для отправки в качестве вложения или использовать микрофон для записи беседы. </span><span class="sxs-lookup"><span data-stu-id="b18e7-117">It allows your app to ask for requisite permissions from users before they start using  the **camera** to capture the image, open the gallery to select an image to submit as an attachment, or use the **microphone** to record the conversation.</span></span>

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> <span data-ttu-id="b18e7-118">Запрос **разрешений** автоматически отображается при инициировании соответствующего API Teams.</span><span class="sxs-lookup"><span data-stu-id="b18e7-118">The **Request Permissions** prompt is automatically displayed when a relevant Teams API is initiated.</span></span> <span data-ttu-id="b18e7-119">Дополнительные сведения см. в [запросе разрешений устройств.](native-device-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="b18e7-119">For more information, see [Request device permissions](native-device-permissions.md).</span></span>

## <a name="media-capability-apis"></a><span data-ttu-id="b18e7-120">API возможностей мультимедиа</span><span class="sxs-lookup"><span data-stu-id="b18e7-120">Media capability APIs</span></span>

<span data-ttu-id="b18e7-121">API [selectMedia,](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true) [getMedia](/javascript/api/@microsoft/teams-js/_media?view=msteams-client-js-latest#getMedia__error__SdkError__blob__Blob_____void_&preserve-view=true)и [viewImages](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#viewImages_ImageUri_____error___SdkError_____void_&preserve-view=true) позволяют использовать возможности родного мультимедиа следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b18e7-121">The [selectMedia](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true), [getMedia](/javascript/api/@microsoft/teams-js/_media?view=msteams-client-js-latest#getMedia__error__SdkError__blob__Blob_____void_&preserve-view=true), and [viewImages](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#viewImages_ImageUri_____error___SdkError_____void_&preserve-view=true) APIs enable you to use native media capabilities as follows:</span></span>

* <span data-ttu-id="b18e7-122">Использование родного **микрофона** позволяет пользователям записывать звук **(запись** 10 минут беседы) с устройства.</span><span class="sxs-lookup"><span data-stu-id="b18e7-122">Use the native **microphone** to allow users to **record audio** (record 10 minutes of conversation) from the device.</span></span>
* <span data-ttu-id="b18e7-123">Используйте **родной контроль камеры,** чтобы позволить пользователям **захватывать и прикреплять изображения** в перейти.</span><span class="sxs-lookup"><span data-stu-id="b18e7-123">Use native **camera control** to allow users to **capture and attach images** on the go.</span></span>
* <span data-ttu-id="b18e7-124">Используйте **поддержку родной галереи,** чтобы позволить пользователям **выбирать изображения устройств в** качестве вложений.</span><span class="sxs-lookup"><span data-stu-id="b18e7-124">Use native **gallery support** to allow users to **select device images** as attachments.</span></span>
* <span data-ttu-id="b18e7-125">Используйте управление **для просмотра изображений на** родном уровне, чтобы **просмотреть** несколько изображений одновременно.</span><span class="sxs-lookup"><span data-stu-id="b18e7-125">Use native **image viewer control** to **preview multiple images** at one time.</span></span>
* <span data-ttu-id="b18e7-126">Поддержка **большой передачи изображений** (от 1 МБ до 50 МБ) через мост SDK.</span><span class="sxs-lookup"><span data-stu-id="b18e7-126">Support **large image transfer** (from 1 MB to 50 MB) through the SDK bridge.</span></span>
* <span data-ttu-id="b18e7-127">Поддержка **расширенных возможностей изображения,** позволяющих пользователям просматривать и изменять изображения:</span><span class="sxs-lookup"><span data-stu-id="b18e7-127">Support **advanced image capabilities** allowing users to preview and edit images:</span></span>
  * <span data-ttu-id="b18e7-128">Сканирование документов, доски и визитных карт с помощью камеры.</span><span class="sxs-lookup"><span data-stu-id="b18e7-128">Scan document, whiteboard, and business cards  through the camera.</span></span>
  
> [!IMPORTANT]
>*   <span data-ttu-id="b18e7-129">API и API можно вызывать с нескольких поверхностей Teams, таких как модули задач, вкладки `selectMedia` `getMedia` и `viewImages` личные приложения.</span><span class="sxs-lookup"><span data-stu-id="b18e7-129">The `selectMedia`, `getMedia`, and `viewImages` APIs can be invoked from multiple Teams surfaces such as task modules, tabs, and personal apps.</span></span> <span data-ttu-id="b18e7-130">Дополнительные сведения см. в [материале Пункты входа для приложений Teams.](../extensibility-points.md)</span><span class="sxs-lookup"><span data-stu-id="b18e7-130">For more details, see [Entry points for Teams apps](../extensibility-points.md).</span></span>
>* <span data-ttu-id="b18e7-131">`selectMedia` API был расширен для поддержки свойств микрофона и звука.</span><span class="sxs-lookup"><span data-stu-id="b18e7-131">`selectMedia` API has been extended to support mic and audio properties.</span></span>

<span data-ttu-id="b18e7-132">Чтобы включить возможности мультимедиа устройства, необходимо использовать следующий набор API:</span><span class="sxs-lookup"><span data-stu-id="b18e7-132">You must use the following set of APIs to enable your device's media capabilities:</span></span>

| <span data-ttu-id="b18e7-133">API</span><span class="sxs-lookup"><span data-stu-id="b18e7-133">API</span></span>      | <span data-ttu-id="b18e7-134">Description</span><span class="sxs-lookup"><span data-stu-id="b18e7-134">Description</span></span>   |
| --- | --- |
| <span data-ttu-id="b18e7-135">[**selectMedia**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true) **(Камера)**</span><span class="sxs-lookup"><span data-stu-id="b18e7-135">[**selectMedia**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true) (**Camera)**</span></span>| <span data-ttu-id="b18e7-136">Этот API позволяет  пользователям захватывать или выбирать носители из камеры устройства и возвращать его в веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="b18e7-136">This API allows users to **capture or select media from the device camera** and return it to the web-app.</span></span> <span data-ttu-id="b18e7-137">Пользователи могут изменять, обрезать, вращать, аннотировать или рисовать изображения перед отправкой.</span><span class="sxs-lookup"><span data-stu-id="b18e7-137">The users can edit, crop, rotate, annotate, or draw over images before submission.</span></span> <span data-ttu-id="b18e7-138">В ответ **на selectMedia** веб-приложение получает медиа-ИД выбранных изображений и эскиз выбранного мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="b18e7-138">In response to **selectMedia**, the web-app receives the media IDs of selected images and a thumbnail of the selected media.</span></span> <span data-ttu-id="b18e7-139">Этот API можно дополнительно настроить с помощью [конфигурации ImageProps.](/javascript/api/@microsoft/teams-js/imageprops?view=msteams-client-js-latest&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="b18e7-139">This API can be further configured through the [ImageProps](/javascript/api/@microsoft/teams-js/imageprops?view=msteams-client-js-latest&preserve-view=true) configuration.</span></span> |
| <span data-ttu-id="b18e7-140">[**selectMedia**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true) **(Микрофон)**</span><span class="sxs-lookup"><span data-stu-id="b18e7-140">[**selectMedia**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true) (**Microphone**)</span></span>| <span data-ttu-id="b18e7-141">Установите [mediaType](/javascript/api/@microsoft/teams-js/mediatype?view=msteams-client-js-latest&preserve-view=true) в `4` **selectMedia** API для доступа к возможностям микрофона.</span><span class="sxs-lookup"><span data-stu-id="b18e7-141">Set the [mediaType](/javascript/api/@microsoft/teams-js/mediatype?view=msteams-client-js-latest&preserve-view=true) to `4` in **selectMedia** API for accessing microphone  capability.</span></span> <span data-ttu-id="b18e7-142">Этот API также позволяет пользователям записывать звук с микрофона устройства и возвращать записанные клипы в веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="b18e7-142">This API also allows users to record audio from the device microphone and return recorded clips to the web-app.</span></span> <span data-ttu-id="b18e7-143">Перед отправкой пользователи могут приостанавлить, перезаписи и воспроизведения предварительного просмотра записи.</span><span class="sxs-lookup"><span data-stu-id="b18e7-143">The users can pause, re-record, and play recording preview before submission.</span></span> <span data-ttu-id="b18e7-144">В ответ на **selectMedia** веб-приложение получает медиа-ID выбранной аудиозаписи.</span><span class="sxs-lookup"><span data-stu-id="b18e7-144">In response to **selectMedia**, the web-app receives media IDs of the selected audio recording.</span></span> <br/> <span data-ttu-id="b18e7-145">Используйте, если требуется настроить продолжительность в `maxDuration` минутах для записи беседы.</span><span class="sxs-lookup"><span data-stu-id="b18e7-145">Use `maxDuration`, if you require to configure a duration in minutes for recording the conversation.</span></span> <span data-ttu-id="b18e7-146">Текущая продолжительность записи составляет 10 минут, после чего запись прекращается.</span><span class="sxs-lookup"><span data-stu-id="b18e7-146">The current duration for recording is 10 minutes, after which the recording terminates.</span></span>  |
| [<span data-ttu-id="b18e7-147">**getMedia**</span><span class="sxs-lookup"><span data-stu-id="b18e7-147">**getMedia**</span></span>](/javascript/api/@microsoft/teams-js/_media?view=msteams-client-js-latest#getMedia__error__SdkError__blob__Blob_____void_&preserve-view=true)| <span data-ttu-id="b18e7-148">Этот API извлекает средства массовой информации, захваченные **selectMedia** API в куски, независимо от размера мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="b18e7-148">This API retrieves the media captured by **selectMedia** API in chunks, irrespective of the media size.</span></span> <span data-ttu-id="b18e7-149">Эти фрагменты собираются и отправляются обратно в веб-приложение в качестве файла или blob.</span><span class="sxs-lookup"><span data-stu-id="b18e7-149">These chunks are assembled and sent back to the web app as a file or blob.</span></span> <span data-ttu-id="b18e7-150">Размыв мультимедиа на меньшие куски упрощает передачу больших файлов.</span><span class="sxs-lookup"><span data-stu-id="b18e7-150">Breaking of media into smaller chunks facilitates large file transfer.</span></span> |
| [<span data-ttu-id="b18e7-151">**viewImages**</span><span class="sxs-lookup"><span data-stu-id="b18e7-151">**viewImages**</span></span>](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#viewImages_ImageUri_____error___SdkError_____void_&preserve-view=true)| <span data-ttu-id="b18e7-152">Этот API позволяет пользователю просматривать изображения в полноэкранном режиме в качестве списка прокрутки.</span><span class="sxs-lookup"><span data-stu-id="b18e7-152">This API enables the user to view images in  full-screen mode as a scrollable list.</span></span>|


<span data-ttu-id="b18e7-153">**Опыт работы с веб-приложением для selectMedia API для возможностей изображения** 
 ![ Камера устройства и опыт работы с изображениями в Teams](../../assets/images/tabs/image-capability.png)</span><span class="sxs-lookup"><span data-stu-id="b18e7-153">**Web app experience for selectMedia API for image capability**
![device camera and image experience in Teams](../../assets/images/tabs/image-capability.png)</span></span>

<span data-ttu-id="b18e7-154">**Опыт работы веб-приложения для selectMedia API для возможностей микрофона** 
 ![ Возможности веб-приложения для микрофона](../../assets/images/tabs/microphone-capability.png)</span><span class="sxs-lookup"><span data-stu-id="b18e7-154">**Web app experience for selectMedia API for microphone capability**
![web app experience for microphone capability](../../assets/images/tabs/microphone-capability.png)</span></span>

## <a name="error-handling"></a><span data-ttu-id="b18e7-155">Обработка ошибок</span><span class="sxs-lookup"><span data-stu-id="b18e7-155">Error handling</span></span>

<span data-ttu-id="b18e7-156">Необходимо обеспечить надлежащее обработку этих ошибок в приложении Teams.</span><span class="sxs-lookup"><span data-stu-id="b18e7-156">You must ensure to handle these errors appropriately in your Teams app.</span></span> <span data-ttu-id="b18e7-157">В следующей таблице перечислены коды ошибок и условия, при которых создаются ошибки:</span><span class="sxs-lookup"><span data-stu-id="b18e7-157">The following table lists the error codes and the conditions under which the errors are generated:</span></span> 


|<span data-ttu-id="b18e7-158">Код ошибки</span><span class="sxs-lookup"><span data-stu-id="b18e7-158">Error code</span></span> |  <span data-ttu-id="b18e7-159">Имя ошибки</span><span class="sxs-lookup"><span data-stu-id="b18e7-159">Error name</span></span>     | <span data-ttu-id="b18e7-160">Condition</span><span class="sxs-lookup"><span data-stu-id="b18e7-160">Condition</span></span>|
| --------- | --------------- | -------- |
| <span data-ttu-id="b18e7-161">**100**</span><span class="sxs-lookup"><span data-stu-id="b18e7-161">**100**</span></span> | <span data-ttu-id="b18e7-162">NOT_SUPPORTED_ON_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="b18e7-162">NOT_SUPPORTED_ON_PLATFORM</span></span> | <span data-ttu-id="b18e7-163">API не поддерживается на текущей платформе.</span><span class="sxs-lookup"><span data-stu-id="b18e7-163">API is not supported on the current platform.</span></span>|
| <span data-ttu-id="b18e7-164">**404**</span><span class="sxs-lookup"><span data-stu-id="b18e7-164">**404**</span></span> | <span data-ttu-id="b18e7-165">FILE_NOT_FOUND</span><span class="sxs-lookup"><span data-stu-id="b18e7-165">FILE_NOT_FOUND</span></span> | <span data-ttu-id="b18e7-166">Указанный файл не найден в указанном расположении.</span><span class="sxs-lookup"><span data-stu-id="b18e7-166">File specified is not found in the given location.</span></span>|
| <span data-ttu-id="b18e7-167">**500**</span><span class="sxs-lookup"><span data-stu-id="b18e7-167">**500**</span></span> | <span data-ttu-id="b18e7-168">INTERNAL_ERROR</span><span class="sxs-lookup"><span data-stu-id="b18e7-168">INTERNAL_ERROR</span></span> | <span data-ttu-id="b18e7-169">При выполнении необходимой операции встречаются внутренние ошибки.</span><span class="sxs-lookup"><span data-stu-id="b18e7-169">Internal error is encountered while performing the required operation.</span></span>|
| <span data-ttu-id="b18e7-170">**1000**</span><span class="sxs-lookup"><span data-stu-id="b18e7-170">**1000**</span></span> | <span data-ttu-id="b18e7-171">PERMISSION_DENIED</span><span class="sxs-lookup"><span data-stu-id="b18e7-171">PERMISSION_DENIED</span></span> |<span data-ttu-id="b18e7-172">Пользователю отказано в разрешении.</span><span class="sxs-lookup"><span data-stu-id="b18e7-172">Permission is denied by the user.</span></span>|
| <span data-ttu-id="b18e7-173">**2000**</span><span class="sxs-lookup"><span data-stu-id="b18e7-173">**2000**</span></span> |<span data-ttu-id="b18e7-174">NETWORK_ERROR</span><span class="sxs-lookup"><span data-stu-id="b18e7-174">NETWORK_ERROR</span></span> | <span data-ttu-id="b18e7-175">Проблема сети.</span><span class="sxs-lookup"><span data-stu-id="b18e7-175">Network issue.</span></span>|
| <span data-ttu-id="b18e7-176">**3000**</span><span class="sxs-lookup"><span data-stu-id="b18e7-176">**3000**</span></span> | <span data-ttu-id="b18e7-177">NO_HW_SUPPORT</span><span class="sxs-lookup"><span data-stu-id="b18e7-177">NO_HW_SUPPORT</span></span> | <span data-ttu-id="b18e7-178">Оборудование не поддерживает эту возможность.</span><span class="sxs-lookup"><span data-stu-id="b18e7-178">Underlying hardware does not support the capability.</span></span>|
| <span data-ttu-id="b18e7-179">**4000**</span><span class="sxs-lookup"><span data-stu-id="b18e7-179">**4000**</span></span>| <span data-ttu-id="b18e7-180">INVALID_ARGUMENTS</span><span class="sxs-lookup"><span data-stu-id="b18e7-180">INVALID_ARGUMENTS</span></span> | <span data-ttu-id="b18e7-181">Один или несколько аргументов являются недействительными.</span><span class="sxs-lookup"><span data-stu-id="b18e7-181">One or more arguments are invalid.</span></span>|
| <span data-ttu-id="b18e7-182">**5000**</span><span class="sxs-lookup"><span data-stu-id="b18e7-182">**5000**</span></span> | <span data-ttu-id="b18e7-183">UNAUTHORIZED_USER_OPERATION</span><span class="sxs-lookup"><span data-stu-id="b18e7-183">UNAUTHORIZED_USER_OPERATION</span></span> | <span data-ttu-id="b18e7-184">Пользователь не уполномочен выполнить эту операцию.</span><span class="sxs-lookup"><span data-stu-id="b18e7-184">User is not authorized to complete this operation.</span></span>|
| <span data-ttu-id="b18e7-185">**6000**</span><span class="sxs-lookup"><span data-stu-id="b18e7-185">**6000**</span></span> |<span data-ttu-id="b18e7-186">INSUFFICIENT_RESOURCES</span><span class="sxs-lookup"><span data-stu-id="b18e7-186">INSUFFICIENT_RESOURCES</span></span> | <span data-ttu-id="b18e7-187">Операция не может быть завершена из-за нехватки ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b18e7-187">Operation could not be completed due to insufficient resources.</span></span>|
|<span data-ttu-id="b18e7-188">**7000**</span><span class="sxs-lookup"><span data-stu-id="b18e7-188">**7000**</span></span> | <span data-ttu-id="b18e7-189">THROTTLE</span><span class="sxs-lookup"><span data-stu-id="b18e7-189">THROTTLE</span></span> | <span data-ttu-id="b18e7-190">Платформа уравняла запрос, так как API часто вызывался.</span><span class="sxs-lookup"><span data-stu-id="b18e7-190">Platform throttled the request as the API was invoked frequently.</span></span>|
|  <span data-ttu-id="b18e7-191">**8000**</span><span class="sxs-lookup"><span data-stu-id="b18e7-191">**8000**</span></span> | <span data-ttu-id="b18e7-192">USER_ABORT</span><span class="sxs-lookup"><span data-stu-id="b18e7-192">USER_ABORT</span></span> |<span data-ttu-id="b18e7-193">Пользователь прерывает операцию.</span><span class="sxs-lookup"><span data-stu-id="b18e7-193">User aborts the operation.</span></span>|
| <span data-ttu-id="b18e7-194">**9000**</span><span class="sxs-lookup"><span data-stu-id="b18e7-194">**9000**</span></span>| <span data-ttu-id="b18e7-195">OLD_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="b18e7-195">OLD_PLATFORM</span></span> | <span data-ttu-id="b18e7-196">Код платформы устарел и не реализует этот API.</span><span class="sxs-lookup"><span data-stu-id="b18e7-196">Platform code is outdated and does not implement this API.</span></span>|
| <span data-ttu-id="b18e7-197">**10000**</span><span class="sxs-lookup"><span data-stu-id="b18e7-197">**10000**</span></span>| <span data-ttu-id="b18e7-198">SIZE_EXCEEDED</span><span class="sxs-lookup"><span data-stu-id="b18e7-198">SIZE_EXCEEDED</span></span> |  <span data-ttu-id="b18e7-199">Значение return слишком большое и превысило границы размера платформы.</span><span class="sxs-lookup"><span data-stu-id="b18e7-199">Return value is too big and has exceeded the platform size boundaries.</span></span>|

## <a name="code-snippets"></a><span data-ttu-id="b18e7-200">Фрагменты кода</span><span class="sxs-lookup"><span data-stu-id="b18e7-200">Code snippets</span></span>

<span data-ttu-id="b18e7-201">**Вызов `selectMedia` API** для захвата изображений с помощью камеры:</span><span class="sxs-lookup"><span data-stu-id="b18e7-201">**Calling `selectMedia` API** for capturing images using camera:</span></span>

```javascript
let imageProp: microsoftTeams.media.ImageProps = {
    sources: [microsoftTeams.media.Source.Camera, microsoftTeams.media.Source.Gallery],
    startMode: microsoftTeams.media.CameraStartMode.Photo,
    ink: false,
    cameraSwitcher: false,
    textSticker: false,
    enableFilter: true,
};
let mediaInput: microsoftTeams.media.MediaInputs = {
    mediaType: microsoftTeams.media.MediaType.Image,
    maxMediaCount: 10,
    imageProps: imageProp
};
microsoftTeams.media.selectMedia(mediaInput, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
    if (error) {
        if (error.message) {
            alert(" ErrorCode: " + error.errorCode + error.message);
        } else {
            alert(" ErrorCode: " + error.errorCode);
        }
    }
    if (attachments) {
        let y = attachments[0];
        img.src = ("data:" + y.mimeType + ";base64," + y.preview);
    }
});
```

<span data-ttu-id="b18e7-202">**Вызов `getMedia` API** для получения больших мультимедиа в кусках:</span><span class="sxs-lookup"><span data-stu-id="b18e7-202">**Calling `getMedia` API** to retrieve large media in chunks:</span></span>

```javascript
let media: microsoftTeams.media.Media = attachments[0]
media.getMedia((error: microsoftTeams.SdkError, blob: Blob) => {
    if (blob) {
        if (blob.type.includes("image")) {
            img.src = (URL.createObjectURL(blob));
        }
    }
    if (error) {
        if (error.message) {
            alert(" ErrorCode: " + error.errorCode + error.message);
        } else {
            alert(" ErrorCode: " + error.errorCode);
        }
    }
});
```

<span data-ttu-id="b18e7-203">**Вызов `viewImages` API по ID, возвращенный `selectMedia` API:**</span><span class="sxs-lookup"><span data-stu-id="b18e7-203">**Calling `viewImages` API by ID returned by `selectMedia` API**:</span></span>

```javascript
// View images by id:
// Assumption: attachmentArray = select Media API Output
let uriList = [];
if (attachmentArray && attachmentArray.length > 0) {
    for (let i = 0; i < attachmentArray.length; i++) {
        let file = attachmentArray[i];
        if (file.mimeType.includes("image")) {
            let imageUri = {
                value: file.content,
                type: 1,
            }
            uriList.push(imageUri);
        } else {
            alert("File type is not image");
        }
    }
}
if (uriList.length > 0) {
    microsoftTeams.media.viewImages(uriList, (error: microsoftTeams.SdkError) => {
        if (error) {
            if (error.message) {
                output(" ErrorCode: " + error.errorCode + error.message);
            } else {
                output(" ErrorCode: " + error.errorCode);
            }
        }
    });
} else {
    output("Url list is empty");
}
```

<span data-ttu-id="b18e7-204">**Вызов `viewImages` API по URL-адресу:**</span><span class="sxs-lookup"><span data-stu-id="b18e7-204">**Calling `viewImages` API by URL**:</span></span>

```javascript
// View Images by URL:
// Assumption 2 urls, url1 and url2
let uriList = [];
if (URL1 != null && URL1.length > 0) {
    let imageUri = {
        value: URL1,
        type: 2,
    }
    uriList.push(imageUri);
}
if (URL2 != null && URL2.length > 0) {
    let imageUri = {
        value: URL2,
        type: 2,
    }
    uriList.push(imageUri);
}
if (uriList.length > 0) {
    microsoftTeams.media.viewImages(uriList, (error: microsoftTeams.SdkError) => {
        if (error) {
            if (error.message) {
                output(" ErrorCode: " + error.errorCode + error.message);
            } else {
                output(" ErrorCode: " + error.errorCode);
            }
        }
    });
} else {
    output("Url list is empty");
}
```

<span data-ttu-id="b18e7-205">**Вызовы `selectMedia` и `getMedia` API для записи звука через микрофон:**</span><span class="sxs-lookup"><span data-stu-id="b18e7-205">**Calling `selectMedia` and `getMedia` APIs for recording audio through microphone**:</span></span>

```javascript
let mediaInput: microsoftTeams.media.MediaInputs = {
    mediaType: microsoftTeams.media.MediaType.Audio,
    maxMediaCount: 1,
};
microsoftTeams.media.selectMedia(mediaInput, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
    if (error) {
        if (error.message) {
            alert(" ErrorCode: " + error.errorCode + error.message);
        } else {
            alert(" ErrorCode: " + error.errorCode);
        }
    }
    // If you want to directly use the audio file (for smaller file sizes (~4MB))    if (attachments) {
    let audioResult = attachments[0];
    var videoElement = document.createElement("video");
    videoElement.setAttribute("src", ("data:" + y.mimeType + ";base64," + y.preview));
    //To use the audio file via get Media API for bigger audio file sizes greater than 4MB        audioResult.getMedia((error: microsoftTeams.SdkError, blob: Blob) => {
    if (blob) {
        if (blob.type.includes("video")) {
            videoElement.setAttribute("src", URL.createObjectURL(blob));
        }
    }
    if (error) {
        if (error.message) {
            alert(" ErrorCode: " + error.errorCode + error.message);
        } else {
            alert(" ErrorCode: " + error.errorCode);
        }
    }
});
```

## <a name="see-also"></a><span data-ttu-id="b18e7-206">См. также</span><span class="sxs-lookup"><span data-stu-id="b18e7-206">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b18e7-207">Интеграция функций сканера QR или штрихкодов в Teams</span><span class="sxs-lookup"><span data-stu-id="b18e7-207">Integrate QR or barcode scanner capability in Teams</span></span>](qr-barcode-scanner-capability.md)