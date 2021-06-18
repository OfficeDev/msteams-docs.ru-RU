---
title: Интеграция возможностей мультимедиа
author: Rajeshwari-v
description: Использование SDK Teams JavaScript для обеспечения возможностей мультимедиа
keywords: Возможности микрофона изображения камеры для носителей разрешений на устройства
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: e2d3c6e4b9e80d5b09cf597a29e7f3ba67355715
ms.sourcegitcommit: 14409950307b135265c8582408be5277b35131dd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/17/2021
ms.locfileid: "52994380"
---
# <a name="integrate-media-capabilities"></a><span data-ttu-id="768db-104">Интеграция возможностей мультимедиа</span><span class="sxs-lookup"><span data-stu-id="768db-104">Integrate media capabilities</span></span> 

<span data-ttu-id="768db-105">В этом документе содержится руководство по интеграции возможностей мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="768db-105">This document guides you on how to integrate media capabilities.</span></span> <span data-ttu-id="768db-106">Эта интеграция сочетает в себе возможности  родного устройства, такие как камера и микрофон с Teams платформой. </span><span class="sxs-lookup"><span data-stu-id="768db-106">This integration combines the native device capabilities, such as the **camera** and **microphone** with the Teams platform.</span></span>  

<span data-ttu-id="768db-107">Вы можете использовать Microsoft Teams JavaScript клиента [SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), который предоставляет средства, необходимые для вашего приложения для доступа к разрешениям устройства [пользователя](native-device-permissions.md).</span><span class="sxs-lookup"><span data-stu-id="768db-107">You can use [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), that provides the tools necessary for your app to access a user’s [device permissions](native-device-permissions.md).</span></span> <span data-ttu-id="768db-108">Используйте подходящие API средств массовой информации для интеграции  родных возможностей устройства, например камеры и микрофона с платформой Teams в мобильном приложении Microsoft Teams и создания более богатого опыта. </span><span class="sxs-lookup"><span data-stu-id="768db-108">Use suitable  media capability APIs to integrate the native device capabilities, such as the **camera** and **microphone** with the Teams platform within your Microsoft Teams mobile app, and build a richer experience.</span></span> 

## <a name="advantage-of-integrating-media-capabilities"></a><span data-ttu-id="768db-109">Преимущество интеграции возможностей мультимедиа</span><span class="sxs-lookup"><span data-stu-id="768db-109">Advantage of integrating media capabilities</span></span>

<span data-ttu-id="768db-110">Основное преимущество интеграции возможностей устройства в приложениях Teams заключается в том, что он использует элементы управления Teams, чтобы обеспечить пользователям богатый и захватывающий опыт.</span><span class="sxs-lookup"><span data-stu-id="768db-110">The main advantage of integrating device capabilities in your Teams apps is it leverages native Teams controls to provide a rich and immersive experience to your users.</span></span>
<span data-ttu-id="768db-111">Чтобы интегрировать возможности мультимедиа, необходимо обновить файл манифеста приложения и вызвать API средств массовой информации.</span><span class="sxs-lookup"><span data-stu-id="768db-111">To integrate media capabilities you must update the app manifest file and call the media capability APIs.</span></span> 

<span data-ttu-id="768db-112">Для эффективной интеграции необходимо хорошо [](#code-snippets) понимать фрагменты кода для вызова соответствующих API, которые позволяют использовать возможности родного мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="768db-112">For effective integration, you must have a good understanding of [code snippets](#code-snippets) for calling the respective APIs, which allow you to use native media capabilities.</span></span>

<span data-ttu-id="768db-113">Важно ознакомиться с ошибками [ответа API](#error-handling) для обработки ошибок в Teams приложении.</span><span class="sxs-lookup"><span data-stu-id="768db-113">It is important to familiarize yourself with the [API response errors](#error-handling) to handle the errors in your Teams app.</span></span>

> [!NOTE] 
> * <span data-ttu-id="768db-114">В настоящее Microsoft Teams поддержка возможностей мультимедиа доступна только для мобильных клиентов.</span><span class="sxs-lookup"><span data-stu-id="768db-114">Currently, Microsoft Teams support for media capabilities is only available for mobile clients.</span></span>    
> * <span data-ttu-id="768db-115">В настоящее время Teams не поддерживает разрешения устройств для нескольких оконных приложений, вкладок и sidepanel собраний.</span><span class="sxs-lookup"><span data-stu-id="768db-115">Currently, Teams does not support device permissions for multi window apps, tabs, and the meeting sidepanel.</span></span> 

## <a name="update-manifest"></a><span data-ttu-id="768db-116">Манифест обновления</span><span class="sxs-lookup"><span data-stu-id="768db-116">Update manifest</span></span>

<span data-ttu-id="768db-117">Обновите Teams приложение [manifest.jsфайле,](../../resources/schema/manifest-schema.md#devicepermissions) добавив `devicePermissions` свойство и указав `media` .</span><span class="sxs-lookup"><span data-stu-id="768db-117">Update your Teams app [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) file by adding the `devicePermissions` property and specifying `media`.</span></span> <span data-ttu-id="768db-118">Это позволяет приложению запросить необходимые разрешения у пользователей, прежде чем они начнут использовать камеру для захвата изображения, открыть  галерею, чтобы выбрать изображение для отправки в качестве вложения или использовать микрофон для записи беседы. </span><span class="sxs-lookup"><span data-stu-id="768db-118">It allows your app to ask for requisite permissions from users before they start using  the **camera** to capture the image, open the gallery to select an image to submit as an attachment, or use the **microphone** to record the conversation.</span></span>

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> <span data-ttu-id="768db-119">Запрос **разрешения запроса** автоматически отображается при Teams API.</span><span class="sxs-lookup"><span data-stu-id="768db-119">The **Request Permissions** prompt is automatically displayed when a relevant Teams API is initiated.</span></span> <span data-ttu-id="768db-120">Дополнительные сведения см. в [запросе разрешений устройств.](native-device-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="768db-120">For more information, see [Request device permissions](native-device-permissions.md).</span></span>

## <a name="media-capability-apis"></a><span data-ttu-id="768db-121">API возможностей мультимедиа</span><span class="sxs-lookup"><span data-stu-id="768db-121">Media capability APIs</span></span>

<span data-ttu-id="768db-122">API [selectMedia,](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true) [getMedia](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediachunk?view=msteams-client-js-latest&preserve-view=true)и [viewImages](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageuri?view=msteams-client-js-latest&preserve-view=true) позволяют использовать возможности родного мультимедиа следующим образом:</span><span class="sxs-lookup"><span data-stu-id="768db-122">The [selectMedia](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true), [getMedia](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediachunk?view=msteams-client-js-latest&preserve-view=true), and [viewImages](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageuri?view=msteams-client-js-latest&preserve-view=true) APIs enable you to use native media capabilities as follows:</span></span>

* <span data-ttu-id="768db-123">Использование родного **микрофона** позволяет пользователям записывать звук **(запись** 10 минут беседы) с устройства.</span><span class="sxs-lookup"><span data-stu-id="768db-123">Use the native **microphone** to allow users to **record audio** (record 10 minutes of conversation) from the device.</span></span>
* <span data-ttu-id="768db-124">Используйте **родной контроль камеры,** чтобы позволить пользователям **захватывать и прикреплять изображения** в перейти.</span><span class="sxs-lookup"><span data-stu-id="768db-124">Use native **camera control** to allow users to **capture and attach images** on the go.</span></span>
* <span data-ttu-id="768db-125">Используйте **поддержку родной галереи,** чтобы позволить пользователям **выбирать изображения устройств в** качестве вложений.</span><span class="sxs-lookup"><span data-stu-id="768db-125">Use native **gallery support** to allow users to **select device images** as attachments.</span></span>
* <span data-ttu-id="768db-126">Используйте управление **для просмотра изображений на** родном уровне, чтобы **просмотреть** несколько изображений одновременно.</span><span class="sxs-lookup"><span data-stu-id="768db-126">Use native **image viewer control** to **preview multiple images** at one time.</span></span>
* <span data-ttu-id="768db-127">Поддержка **большой передачи изображений** (от 1 МБ до 50 МБ) через мост SDK.</span><span class="sxs-lookup"><span data-stu-id="768db-127">Support **large image transfer** (from 1 MB to 50 MB) through the SDK bridge.</span></span>
* <span data-ttu-id="768db-128">Поддержка **расширенных возможностей изображения,** позволяющих пользователям просматривать и изменять изображения:</span><span class="sxs-lookup"><span data-stu-id="768db-128">Support **advanced image capabilities** allowing users to preview and edit images:</span></span>
  * <span data-ttu-id="768db-129">Сканирование документов, доски и визитных карт с помощью камеры.</span><span class="sxs-lookup"><span data-stu-id="768db-129">Scan document, whiteboard, and business cards  through the camera.</span></span>
  
> [!IMPORTANT]
> * <span data-ttu-id="768db-130">API и API можно вызывать с нескольких поверхностей Teams, таких как модули задач, вкладки `selectMedia` `getMedia` и `viewImages` личные приложения.</span><span class="sxs-lookup"><span data-stu-id="768db-130">The `selectMedia`, `getMedia`, and `viewImages` APIs can be invoked from multiple Teams surfaces, such as task modules, tabs, and personal apps.</span></span> <span data-ttu-id="768db-131">Дополнительные сведения см. в [материале Пункты входа для Teams приложений.](../extensibility-points.md)</span><span class="sxs-lookup"><span data-stu-id="768db-131">For more details, see [Entry points for Teams apps](../extensibility-points.md).</span></span>
> * <span data-ttu-id="768db-132">`selectMedia` API расширен для поддержки свойств микрофона и звука.</span><span class="sxs-lookup"><span data-stu-id="768db-132">`selectMedia` API has been extended to support microphone and audio properties.</span></span>

<span data-ttu-id="768db-133">Чтобы включить возможности мультимедиа устройства, необходимо использовать следующий набор API:</span><span class="sxs-lookup"><span data-stu-id="768db-133">You must use the following set of APIs to enable your device's media capabilities:</span></span>

| <span data-ttu-id="768db-134">API</span><span class="sxs-lookup"><span data-stu-id="768db-134">API</span></span>      | <span data-ttu-id="768db-135">Описание</span><span class="sxs-lookup"><span data-stu-id="768db-135">Description</span></span>   |
| --- | --- |
| <span data-ttu-id="768db-136">[**selectMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true) **(Камера)**</span><span class="sxs-lookup"><span data-stu-id="768db-136">[**selectMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true) (**Camera)**</span></span>| <span data-ttu-id="768db-137">Этот API позволяет  пользователям захватывать или выбирать носители из камеры устройства и возвращать его в веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="768db-137">This API allows users to **capture or select media from the device camera** and return it to the web-app.</span></span> <span data-ttu-id="768db-138">Пользователи могут изменять, обрезать, вращать, аннотировать или рисовать изображения перед отправкой.</span><span class="sxs-lookup"><span data-stu-id="768db-138">The users can edit, crop, rotate, annotate, or draw over images before submission.</span></span> <span data-ttu-id="768db-139">В ответ веб-приложение получает медиа-ID выбранных изображений и эскиз `selectMedia` выбранного носитля.</span><span class="sxs-lookup"><span data-stu-id="768db-139">In response to `selectMedia`, the web-app receives the media IDs of selected images and a thumbnail of the selected media.</span></span> <span data-ttu-id="768db-140">Этот API можно дополнительно настроить с помощью [конфигурации ImageProps.](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageprops?view=msteams-client-js-latest&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="768db-140">This API can be further configured through the [ImageProps](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageprops?view=msteams-client-js-latest&preserve-view=true) configuration.</span></span> |
| <span data-ttu-id="768db-141">[**selectMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true) **(Микрофон)**</span><span class="sxs-lookup"><span data-stu-id="768db-141">[**selectMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true) (**Microphone**)</span></span>| <span data-ttu-id="768db-142">Установите [mediaType](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediatype?view=msteams-client-js-latest&preserve-view=true) в `4` `selectMedia` API для доступа к возможностям микрофона.</span><span class="sxs-lookup"><span data-stu-id="768db-142">Set the [mediaType](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediatype?view=msteams-client-js-latest&preserve-view=true) to `4` in `selectMedia` API for accessing microphone  capability.</span></span> <span data-ttu-id="768db-143">Этот API также позволяет пользователям записывать звук с микрофона устройства и возвращать записанные клипы в веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="768db-143">This API also allows users to record audio from the device microphone and return recorded clips to the web-app.</span></span> <span data-ttu-id="768db-144">Перед отправкой пользователи могут приостанавлить, перезаписи и воспроизведения предварительного просмотра записи.</span><span class="sxs-lookup"><span data-stu-id="768db-144">The users can pause, re-record, and play recording preview before submission.</span></span> <span data-ttu-id="768db-145">В ответ на **selectMedia** веб-приложение получает медиа-ID выбранной аудиозаписи.</span><span class="sxs-lookup"><span data-stu-id="768db-145">In response to **selectMedia**, the web-app receives media IDs of the selected audio recording.</span></span> <br/> <span data-ttu-id="768db-146">Используйте, если требуется настроить продолжительность в минутах `maxDuration` для записи беседы.</span><span class="sxs-lookup"><span data-stu-id="768db-146">Use `maxDuration`, if you require to configure a duration in minutes for recording the conversation.</span></span> <span data-ttu-id="768db-147">Текущая продолжительность записи составляет 10 минут, после чего запись прекращается.</span><span class="sxs-lookup"><span data-stu-id="768db-147">The current duration for recording is 10 minutes, after which the recording terminates.</span></span>  |
| [<span data-ttu-id="768db-148">**getMedia**</span><span class="sxs-lookup"><span data-stu-id="768db-148">**getMedia**</span></span>](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediachunk?view=msteams-client-js-latest&preserve-view=true)| <span data-ttu-id="768db-149">Этот API извлекает средства массовой информации, захваченные API в `selectMedia` куски, независимо от размера мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="768db-149">This API retrieves the media captured by `selectMedia` API in chunks, irrespective of the media size.</span></span> <span data-ttu-id="768db-150">Эти фрагменты собираются и отправляются обратно в веб-приложение в качестве файла или blob.</span><span class="sxs-lookup"><span data-stu-id="768db-150">These chunks are assembled and sent back to the web app as a file or blob.</span></span> <span data-ttu-id="768db-151">Размыв мультимедиа на меньшие куски упрощает передачу больших файлов.</span><span class="sxs-lookup"><span data-stu-id="768db-151">Breaking of media into smaller chunks facilitates large file transfer.</span></span> |
| [<span data-ttu-id="768db-152">**viewImages**</span><span class="sxs-lookup"><span data-stu-id="768db-152">**viewImages**</span></span>](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageuri?view=msteams-client-js-latest&preserve-view=true)| <span data-ttu-id="768db-153">Этот API позволяет пользователю просматривать изображения в полноэкранном режиме в качестве списка прокрутки.</span><span class="sxs-lookup"><span data-stu-id="768db-153">This API enables the user to view images in  full-screen mode as a scrollable list.</span></span>|


<span data-ttu-id="768db-154">**Опыт работы с веб-приложением для selectMedia API для возможностей изображения** 
 ![ устройство камеры и изображения в Teams](../../assets/images/tabs/image-capability.png)</span><span class="sxs-lookup"><span data-stu-id="768db-154">**Web app experience for selectMedia API for image capability**
![device camera and image experience in Teams](../../assets/images/tabs/image-capability.png)</span></span>

<span data-ttu-id="768db-155">**Опыт работы веб-приложения для selectMedia API для возможностей микрофона** 
 ![ Возможности веб-приложения для микрофона](../../assets/images/tabs/microphone-capability.png)</span><span class="sxs-lookup"><span data-stu-id="768db-155">**Web app experience for selectMedia API for microphone capability**
![web app experience for microphone capability](../../assets/images/tabs/microphone-capability.png)</span></span>

## <a name="error-handling"></a><span data-ttu-id="768db-156">Обработка ошибок</span><span class="sxs-lookup"><span data-stu-id="768db-156">Error handling</span></span>

<span data-ttu-id="768db-157">Необходимо обеспечить надлежащее обработку этих ошибок в Teams приложении.</span><span class="sxs-lookup"><span data-stu-id="768db-157">You must ensure to handle these errors appropriately in your Teams app.</span></span> <span data-ttu-id="768db-158">В следующей таблице перечислены коды ошибок и условия, при которых создаются ошибки:</span><span class="sxs-lookup"><span data-stu-id="768db-158">The following table lists the error codes and the conditions under which the errors are generated:</span></span> 


|<span data-ttu-id="768db-159">Код ошибки</span><span class="sxs-lookup"><span data-stu-id="768db-159">Error code</span></span> |  <span data-ttu-id="768db-160">Имя ошибки</span><span class="sxs-lookup"><span data-stu-id="768db-160">Error name</span></span>     | <span data-ttu-id="768db-161">Условие</span><span class="sxs-lookup"><span data-stu-id="768db-161">Condition</span></span>|
| --------- | --------------- | -------- |
| <span data-ttu-id="768db-162">**100**</span><span class="sxs-lookup"><span data-stu-id="768db-162">**100**</span></span> | <span data-ttu-id="768db-163">NOT_SUPPORTED_ON_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="768db-163">NOT_SUPPORTED_ON_PLATFORM</span></span> | <span data-ttu-id="768db-164">API не поддерживается на текущей платформе.</span><span class="sxs-lookup"><span data-stu-id="768db-164">API is not supported on the current platform.</span></span>|
| <span data-ttu-id="768db-165">**404**</span><span class="sxs-lookup"><span data-stu-id="768db-165">**404**</span></span> | <span data-ttu-id="768db-166">FILE_NOT_FOUND</span><span class="sxs-lookup"><span data-stu-id="768db-166">FILE_NOT_FOUND</span></span> | <span data-ttu-id="768db-167">Указанный файл не найден в указанном расположении.</span><span class="sxs-lookup"><span data-stu-id="768db-167">File specified is not found in the given location.</span></span>|
| <span data-ttu-id="768db-168">**500**</span><span class="sxs-lookup"><span data-stu-id="768db-168">**500**</span></span> | <span data-ttu-id="768db-169">INTERNAL_ERROR</span><span class="sxs-lookup"><span data-stu-id="768db-169">INTERNAL_ERROR</span></span> | <span data-ttu-id="768db-170">При выполнении необходимой операции встречаются внутренние ошибки.</span><span class="sxs-lookup"><span data-stu-id="768db-170">Internal error is encountered while performing the required operation.</span></span>|
| <span data-ttu-id="768db-171">**1000**</span><span class="sxs-lookup"><span data-stu-id="768db-171">**1000**</span></span> | <span data-ttu-id="768db-172">PERMISSION_DENIED</span><span class="sxs-lookup"><span data-stu-id="768db-172">PERMISSION_DENIED</span></span> |<span data-ttu-id="768db-173">Пользователю отказано в разрешении.</span><span class="sxs-lookup"><span data-stu-id="768db-173">Permission is denied by the user.</span></span>|
| <span data-ttu-id="768db-174">**2000**</span><span class="sxs-lookup"><span data-stu-id="768db-174">**2000**</span></span> |<span data-ttu-id="768db-175">NETWORK_ERROR</span><span class="sxs-lookup"><span data-stu-id="768db-175">NETWORK_ERROR</span></span> | <span data-ttu-id="768db-176">Проблема сети.</span><span class="sxs-lookup"><span data-stu-id="768db-176">Network issue.</span></span>|
| <span data-ttu-id="768db-177">**3000**</span><span class="sxs-lookup"><span data-stu-id="768db-177">**3000**</span></span> | <span data-ttu-id="768db-178">NO_HW_SUPPORT</span><span class="sxs-lookup"><span data-stu-id="768db-178">NO_HW_SUPPORT</span></span> | <span data-ttu-id="768db-179">Оборудование не поддерживает эту возможность.</span><span class="sxs-lookup"><span data-stu-id="768db-179">Underlying hardware does not support the capability.</span></span>|
| <span data-ttu-id="768db-180">**4000**</span><span class="sxs-lookup"><span data-stu-id="768db-180">**4000**</span></span>| <span data-ttu-id="768db-181">INVALID_ARGUMENTS</span><span class="sxs-lookup"><span data-stu-id="768db-181">INVALID_ARGUMENTS</span></span> | <span data-ttu-id="768db-182">Один или несколько аргументов являются недействительными.</span><span class="sxs-lookup"><span data-stu-id="768db-182">One or more arguments are invalid.</span></span>|
| <span data-ttu-id="768db-183">**5000**</span><span class="sxs-lookup"><span data-stu-id="768db-183">**5000**</span></span> | <span data-ttu-id="768db-184">UNAUTHORIZED_USER_OPERATION</span><span class="sxs-lookup"><span data-stu-id="768db-184">UNAUTHORIZED_USER_OPERATION</span></span> | <span data-ttu-id="768db-185">Пользователь не уполномочен выполнить эту операцию.</span><span class="sxs-lookup"><span data-stu-id="768db-185">User is not authorized to complete this operation.</span></span>|
| <span data-ttu-id="768db-186">**6000**</span><span class="sxs-lookup"><span data-stu-id="768db-186">**6000**</span></span> |<span data-ttu-id="768db-187">INSUFFICIENT_RESOURCES</span><span class="sxs-lookup"><span data-stu-id="768db-187">INSUFFICIENT_RESOURCES</span></span> | <span data-ttu-id="768db-188">Операция не может быть завершена из-за нехватки ресурсов.</span><span class="sxs-lookup"><span data-stu-id="768db-188">Operation could not be completed due to insufficient resources.</span></span>|
|<span data-ttu-id="768db-189">**7000**</span><span class="sxs-lookup"><span data-stu-id="768db-189">**7000**</span></span> | <span data-ttu-id="768db-190">THROTTLE</span><span class="sxs-lookup"><span data-stu-id="768db-190">THROTTLE</span></span> | <span data-ttu-id="768db-191">Платформа уравняла запрос, так как API часто вызывался.</span><span class="sxs-lookup"><span data-stu-id="768db-191">Platform throttled the request as the API was invoked frequently.</span></span>|
|  <span data-ttu-id="768db-192">**8000**</span><span class="sxs-lookup"><span data-stu-id="768db-192">**8000**</span></span> | <span data-ttu-id="768db-193">USER_ABORT</span><span class="sxs-lookup"><span data-stu-id="768db-193">USER_ABORT</span></span> |<span data-ttu-id="768db-194">Пользователь прерывает операцию.</span><span class="sxs-lookup"><span data-stu-id="768db-194">User aborts the operation.</span></span>|
| <span data-ttu-id="768db-195">**9000**</span><span class="sxs-lookup"><span data-stu-id="768db-195">**9000**</span></span>| <span data-ttu-id="768db-196">OLD_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="768db-196">OLD_PLATFORM</span></span> | <span data-ttu-id="768db-197">Код платформы устарел и не реализует этот API.</span><span class="sxs-lookup"><span data-stu-id="768db-197">Platform code is outdated and does not implement this API.</span></span>|
| <span data-ttu-id="768db-198">**10000**</span><span class="sxs-lookup"><span data-stu-id="768db-198">**10000**</span></span>| <span data-ttu-id="768db-199">SIZE_EXCEEDED</span><span class="sxs-lookup"><span data-stu-id="768db-199">SIZE_EXCEEDED</span></span> |  <span data-ttu-id="768db-200">Значение return слишком большое и превысило границы размера платформы.</span><span class="sxs-lookup"><span data-stu-id="768db-200">Return value is too big and has exceeded the platform size boundaries.</span></span>|

## <a name="code-snippets"></a><span data-ttu-id="768db-201">Фрагменты кода</span><span class="sxs-lookup"><span data-stu-id="768db-201">Code snippets</span></span>

<span data-ttu-id="768db-202">**Вызов `selectMedia` API** для захвата изображений с помощью камеры:</span><span class="sxs-lookup"><span data-stu-id="768db-202">**Calling `selectMedia` API** for capturing images using camera:</span></span>

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

<span data-ttu-id="768db-203">**Вызов `getMedia` API** для получения больших мультимедиа в кусках:</span><span class="sxs-lookup"><span data-stu-id="768db-203">**Calling `getMedia` API** to retrieve large media in chunks:</span></span>

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

<span data-ttu-id="768db-204">**Вызов `viewImages` API по ID, возвращенный `selectMedia` API:**</span><span class="sxs-lookup"><span data-stu-id="768db-204">**Calling `viewImages` API by ID returned by `selectMedia` API**:</span></span>

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

<span data-ttu-id="768db-205">**Вызов `viewImages` API по URL-адресу:**</span><span class="sxs-lookup"><span data-stu-id="768db-205">**Calling `viewImages` API by URL**:</span></span>

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

<span data-ttu-id="768db-206">**Вызовы `selectMedia` и `getMedia` API для записи звука через микрофон:**</span><span class="sxs-lookup"><span data-stu-id="768db-206">**Calling `selectMedia` and `getMedia` APIs for recording audio through microphone**:</span></span>

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

## <a name="see-also"></a><span data-ttu-id="768db-207">См. также</span><span class="sxs-lookup"><span data-stu-id="768db-207">See also</span></span>

* [<span data-ttu-id="768db-208">Интеграция возможностей сканера QR или штрихкодов в Teams</span><span class="sxs-lookup"><span data-stu-id="768db-208">Integrate QR or barcode scanner capability in Teams</span></span>](qr-barcode-scanner-capability.md)
* [<span data-ttu-id="768db-209">Интеграция возможностей расположения в Teams</span><span class="sxs-lookup"><span data-stu-id="768db-209">Integrate location capabilities in Teams</span></span>](location-capability.md)
