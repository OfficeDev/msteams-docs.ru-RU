---
title: Возможности работы с камерами и изображениями в Teams
description: Как использовать пакет SDK для Teams JavaScript для включения возможностей встроенной камеры и изображений
keywords: характеристики изображения камеры. собственные разрешения для устройства
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: d0ca4dc9c289ec525aa99ea0e156a9f91f5b5d4a
ms.sourcegitcommit: 50571f5c6afc86177c4fe1032fe13366a7b706dd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/04/2020
ms.locfileid: "49576883"
---
# <a name="camera-and-image-capabilities-in-teams"></a><span data-ttu-id="fe6bc-104">Возможности работы с камерами и изображениями в Teams</span><span class="sxs-lookup"><span data-stu-id="fe6bc-104">Camera and image capabilities in Teams</span></span>

>[!IMPORTANT]
>
> * <span data-ttu-id="fe6bc-105">В настоящее время поддержка возможностей камеры и изображений в Teams доступна только для мобильных клиентов.</span><span class="sxs-lookup"><span data-stu-id="fe6bc-105">At present, Teams support for camera and image capabilities is only available for mobile clients.</span></span>
>* <span data-ttu-id="fe6bc-106">`selectMedia`API, `getMedia` и `viewImages` API можно вызывать из нескольких поверхностей Teams, таких как модули задач, вкладки и персональные приложения.</span><span class="sxs-lookup"><span data-stu-id="fe6bc-106">The `selectMedia`, `getMedia`, and `viewImages` APIs can be invoked from multiple Teams surfaces such as task modules, tabs, and personal apps.</span></span> <span data-ttu-id="fe6bc-107">Более подробную информацию можно _узнать_ в статье [точки входа для приложений Teams](../extensibility-points.md)</span><span class="sxs-lookup"><span data-stu-id="fe6bc-107">For more details, _see_ [Entry points for Teams apps](../extensibility-points.md)</span></span>

<span data-ttu-id="fe6bc-108">Вы можете использовать  [клиентский пакет SDK для Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), чтобы легко интегрировать возможности камеры и изображения в мобильное приложение Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="fe6bc-108">You can use the  [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), to easily integrate camera and image capabilities within your Microsoft Teams mobile app.</span></span> <span data-ttu-id="fe6bc-109">Пакет SDK предоставляет средства, необходимые для приложения, чтобы получить доступ к [разрешениям устройства](native-device-permissions.md?tabs=desktop#device-permissions) пользователя и создать более насыщенный интерфейс.</span><span class="sxs-lookup"><span data-stu-id="fe6bc-109">The SDK provides the tools necessary for your app to access a user’s [device permissions](native-device-permissions.md?tabs=desktop#device-permissions) and build a richer experience.</span></span>

<span data-ttu-id="fe6bc-110">Интерфейсы API [селектмедиа](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true), [Media](/javascript/api/@microsoft/teams-js/_media?view=msteams-client-js-latest#getMedia__error__SdkError__blob__Blob_____void_&preserve-view=true)и [виевимажес](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#viewImages_ImageUri_____error___SdkError_____void_&preserve-view=true) позволяют использовать встроенные возможности камеры и изображения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="fe6bc-110">The [selectMedia](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true), [getMedia](/javascript/api/@microsoft/teams-js/_media?view=msteams-client-js-latest#getMedia__error__SdkError__blob__Blob_____void_&preserve-view=true), and [viewImages](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#viewImages_ImageUri_____error___SdkError_____void_&preserve-view=true) APIs enable you to use native camera/image capabilities as follows:</span></span>

* <span data-ttu-id="fe6bc-111">Используйте встроенный **элемент управления камерой** , чтобы позволить пользователям **записывать и прикреплять изображения** в дороге.</span><span class="sxs-lookup"><span data-stu-id="fe6bc-111">Use native **camera control** to allow users to **capture and attach images** on the go.</span></span>
* <span data-ttu-id="fe6bc-112">Используйте встроенную **поддержку коллекций** , чтобы позволить пользователям **выбирать изображения устройств** в качестве вложений.</span><span class="sxs-lookup"><span data-stu-id="fe6bc-112">Use native **gallery support** to allow users to **select device images** as attachments.</span></span>
* <span data-ttu-id="fe6bc-113">Использование встроенного **элемента управления для просмотра изображений** для **предварительного просмотра нескольких изображений** за один раз.</span><span class="sxs-lookup"><span data-stu-id="fe6bc-113">Use native **image viewer control** to **preview multiple images** at one time.</span></span>
* <span data-ttu-id="fe6bc-114">Поддержка **передачи больших изображений** (до 50 МБ) с помощью моста SDK</span><span class="sxs-lookup"><span data-stu-id="fe6bc-114">Support **large image transfer** (up to 50 MB) via the SDK bridge</span></span>
* <span data-ttu-id="fe6bc-115">Поддерживает **Расширенные возможности работы с изображениями** , позволяющие пользователям просматривать и редактировать изображения:</span><span class="sxs-lookup"><span data-stu-id="fe6bc-115">Support **advanced image capabilities** allowing users to preview and edit images:</span></span>
  * <span data-ttu-id="fe6bc-116">Сканировать документы, доску, визитные карточки и т. д. через камеру.</span><span class="sxs-lookup"><span data-stu-id="fe6bc-116">Scan document, whiteboard, business cards, etc., through the camera.</span></span>
  * <span data-ttu-id="fe6bc-117">Обрежьте и поверните изображения.</span><span class="sxs-lookup"><span data-stu-id="fe6bc-117">Crop and rotate the images.</span></span>
  * <span data-ttu-id="fe6bc-118">Добавление текста, рукописного фрагмента или заметки FreeHand к изображению.</span><span class="sxs-lookup"><span data-stu-id="fe6bc-118">Add text, ink, or freehand annotation to the image.</span></span>

## <a name="get-started"></a><span data-ttu-id="fe6bc-119">Начало работы</span><span class="sxs-lookup"><span data-stu-id="fe6bc-119">Get started</span></span>

<span data-ttu-id="fe6bc-120">Обновите приложение Teams [manifest.jsв](../../resources/schema/manifest-schema.md#devicepermissions) файле, добавив `devicePermissions`  свойство и указав `media` .</span><span class="sxs-lookup"><span data-stu-id="fe6bc-120">Update your Teams app [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) file by adding the `devicePermissions`  property and specifying `media`.</span></span> <span data-ttu-id="fe6bc-121">Это позволяет приложению запрашивать у конечных пользователей разрешения, прежде чем использовать камеру для записи изображения или открытия коллекции для выбора изображения, которое будет отправлено в виде вложения.</span><span class="sxs-lookup"><span data-stu-id="fe6bc-121">This allows your app to ask for requisite permissions from end-users before they use the camera to capture the image or open the gallery to select an image to submit as an attachment.</span></span>

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> <span data-ttu-id="fe6bc-122">Запрос на получение _разрешений_ автоматически отображается при инициации соответствующего API Teams.</span><span class="sxs-lookup"><span data-stu-id="fe6bc-122">The _Request Permissions_ prompt is automatically displayed when a relevant Teams API is initiated.</span></span> <span data-ttu-id="fe6bc-123">Дополнительные сведения см. в *разделе* [request Permissions Devices](native-device-permissions.md).</span><span class="sxs-lookup"><span data-stu-id="fe6bc-123">For more details, *see* [Request device permissions](native-device-permissions.md).</span></span>

## <a name="using-camera-and-image-capability-apis"></a><span data-ttu-id="fe6bc-124">Использование интерфейсов API возможностей камеры и изображений</span><span class="sxs-lookup"><span data-stu-id="fe6bc-124">Using camera and image capability APIs</span></span>

<span data-ttu-id="fe6bc-125">Можно использовать следующий набор API для включения возможностей камеры и устройств с изображениями:</span><span class="sxs-lookup"><span data-stu-id="fe6bc-125">You can use the following set of APIs to enable camera and image device capabilities:</span></span>

| <span data-ttu-id="fe6bc-126">API</span><span class="sxs-lookup"><span data-stu-id="fe6bc-126">API</span></span>      | <span data-ttu-id="fe6bc-127">Description</span><span class="sxs-lookup"><span data-stu-id="fe6bc-127">Description</span></span>   |
| --- | --- |
| [<span data-ttu-id="fe6bc-128">**селектмедиа**</span><span class="sxs-lookup"><span data-stu-id="fe6bc-128">**selectMedia**</span></span>](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest&branch=master#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true)| <span data-ttu-id="fe6bc-129">Этот API позволяет пользователям **записывать или выбирать мультимедиа на исходном устройстве** и возвращать в веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="fe6bc-129">This API allows users to **capture or select media from a native device** and return to the web-app.</span></span> <span data-ttu-id="fe6bc-130">Пользователи могут изменять, обрезать, поворачивать, закомментировать и рисовать изображения перед отправкой.</span><span class="sxs-lookup"><span data-stu-id="fe6bc-130">Users may choose to edit, crop, rotate, annotate, or draw over images before submission.</span></span> <span data-ttu-id="fe6bc-131">В ответ на **селектмедиа** веб-приложение получит идентификаторы носителей выбранных изображений и получит эскиз выбранного носителя.</span><span class="sxs-lookup"><span data-stu-id="fe6bc-131">In response to **selectMedia**, the web-app will receive media ids of selected images and may receive a thumbnail of the selected media.</span></span> |
| [<span data-ttu-id="fe6bc-132">**Мультимедиа**</span><span class="sxs-lookup"><span data-stu-id="fe6bc-132">**getMedia**</span></span>](/javascript/api/@microsoft/teams-js/_media?view=msteams-client-js-latest&branch=master#getMedia__error__SdkError__blob__Blob_____void_&preserve-view=true)| <span data-ttu-id="fe6bc-133">Этот API получает носители в блоках независимо от размера.</span><span class="sxs-lookup"><span data-stu-id="fe6bc-133">This API retrieves the media in chunks irrespective of size.</span></span> <span data-ttu-id="fe6bc-134">Эти блоки собраны и отправляются обратно в веб-приложение в виде файла или большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="fe6bc-134">These chunks are assembled and sent back to the web app as a file/blob.</span></span> <span data-ttu-id="fe6bc-135">С помощью этого API изображение разбивается на небольшие блоки для упрощения передачи изображений.</span><span class="sxs-lookup"><span data-stu-id="fe6bc-135">With this API an image is broken into smaller chunks to facilitate large image transfer.</span></span> |
| [<span data-ttu-id="fe6bc-136">**виевимажес**</span><span class="sxs-lookup"><span data-stu-id="fe6bc-136">**viewImages**</span></span>](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#viewImages_ImageUri_____error___SdkError_____void_&preserve-view=true)| <span data-ttu-id="fe6bc-137">Этот API позволяет пользователю просматривать изображения в полноэкранном режиме в виде прокручиваемого списка.</span><span class="sxs-lookup"><span data-stu-id="fe6bc-137">This API enables the user to view images full-screen mode as a scrollable list.</span></span>|

<span data-ttu-id="fe6bc-138">**Взаимодействие с веб-приложениями для API селектмедиа** 
 ![ Камера устройств и взаимодействие с изображениями в Teams](../../assets/images/tabs/image-capability-screenshot.jpg)</span><span class="sxs-lookup"><span data-stu-id="fe6bc-138">**Web app experience for selectMedia API**
![device camera and image experience in Teams](../../assets/images/tabs/image-capability-screenshot.jpg)</span></span>

## <a name="error-handling"></a><span data-ttu-id="fe6bc-139">Обработка ошибок</span><span class="sxs-lookup"><span data-stu-id="fe6bc-139">Error handling</span></span>

<span data-ttu-id="fe6bc-140">Необходимо изучить коды ошибок ответа API и соответствующим образом обработать их.</span><span class="sxs-lookup"><span data-stu-id="fe6bc-140">You should understand the API response error codes and handle them appropriately.</span></span> <span data-ttu-id="fe6bc-141">Ниже приведен список кодов ошибок, которые могут быть возвращены платформой:</span><span class="sxs-lookup"><span data-stu-id="fe6bc-141">Below is a list of error codes that may be returned by the platform:</span></span>

|<span data-ttu-id="fe6bc-142">Код ошибки</span><span class="sxs-lookup"><span data-stu-id="fe6bc-142">Error code</span></span> |  <span data-ttu-id="fe6bc-143">Имя ошибки</span><span class="sxs-lookup"><span data-stu-id="fe6bc-143">Error Name</span></span>     | <span data-ttu-id="fe6bc-144">Condition</span><span class="sxs-lookup"><span data-stu-id="fe6bc-144">Condition</span></span>|
| --- | --- | --- |
| <span data-ttu-id="fe6bc-145">**100**</span><span class="sxs-lookup"><span data-stu-id="fe6bc-145">**100**</span></span> | <span data-ttu-id="fe6bc-146">NOT_SUPPORTED_ON_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="fe6bc-146">NOT_SUPPORTED_ON_PLATFORM</span></span> | <span data-ttu-id="fe6bc-147">API не поддерживается в текущей платформе.</span><span class="sxs-lookup"><span data-stu-id="fe6bc-147">API not supported in the current platform.</span></span>|
| <span data-ttu-id="fe6bc-148">**404**</span><span class="sxs-lookup"><span data-stu-id="fe6bc-148">**404**</span></span> | <span data-ttu-id="fe6bc-149">FILE_NOT_FOUND</span><span class="sxs-lookup"><span data-stu-id="fe6bc-149">FILE_NOT_FOUND</span></span> | <span data-ttu-id="fe6bc-150">Указанный файл не найден в указанном расположении.</span><span class="sxs-lookup"><span data-stu-id="fe6bc-150">The file specified was not found on the given location.</span></span>|
| <span data-ttu-id="fe6bc-151">**500**</span><span class="sxs-lookup"><span data-stu-id="fe6bc-151">**500**</span></span> | <span data-ttu-id="fe6bc-152">INTERNAL_ERROR</span><span class="sxs-lookup"><span data-stu-id="fe6bc-152">INTERNAL_ERROR</span></span> | <span data-ttu-id="fe6bc-153">При выполнении необходимой операции возникла внутренняя ошибка.</span><span class="sxs-lookup"><span data-stu-id="fe6bc-153">Internal error encountered while performing the required operation.</span></span>|
| <span data-ttu-id="fe6bc-154">**1000**</span><span class="sxs-lookup"><span data-stu-id="fe6bc-154">**1000**</span></span> | <span data-ttu-id="fe6bc-155">PERMISSION_DENIED</span><span class="sxs-lookup"><span data-stu-id="fe6bc-155">PERMISSION_DENIED</span></span> |<span data-ttu-id="fe6bc-156">Разрешения, запрещенные пользователем.</span><span class="sxs-lookup"><span data-stu-id="fe6bc-156">Permissions denied by the user.</span></span>|
| <span data-ttu-id="fe6bc-157">**2000**</span><span class="sxs-lookup"><span data-stu-id="fe6bc-157">**2000**</span></span> |<span data-ttu-id="fe6bc-158">NETWORK_ERROR</span><span class="sxs-lookup"><span data-stu-id="fe6bc-158">NETWORK_ERROR</span></span> | <span data-ttu-id="fe6bc-159">Сетевая ошибка.</span><span class="sxs-lookup"><span data-stu-id="fe6bc-159">Network issue.</span></span>|
| <span data-ttu-id="fe6bc-160">**3000**</span><span class="sxs-lookup"><span data-stu-id="fe6bc-160">**3000**</span></span> | <span data-ttu-id="fe6bc-161">NO_HW_SUPPORT</span><span class="sxs-lookup"><span data-stu-id="fe6bc-161">NO_HW_SUPPORT</span></span> | <span data-ttu-id="fe6bc-162">Базовое оборудование не поддерживает эту возможность.</span><span class="sxs-lookup"><span data-stu-id="fe6bc-162">Underlying hardware doesn't support the capability.</span></span>|
| <span data-ttu-id="fe6bc-163">**4000**</span><span class="sxs-lookup"><span data-stu-id="fe6bc-163">**4000**</span></span>| <span data-ttu-id="fe6bc-164">INVALID_ARGUMENTS</span><span class="sxs-lookup"><span data-stu-id="fe6bc-164">INVALID_ARGUMENTS</span></span> | <span data-ttu-id="fe6bc-165">Один или несколько аргументов являются недопустимыми.</span><span class="sxs-lookup"><span data-stu-id="fe6bc-165">One or more arguments is invalid.</span></span>|
| <span data-ttu-id="fe6bc-166">**5000**</span><span class="sxs-lookup"><span data-stu-id="fe6bc-166">**5000**</span></span> | <span data-ttu-id="fe6bc-167">UNAUTHORIZED_USER_OPERATION</span><span class="sxs-lookup"><span data-stu-id="fe6bc-167">UNAUTHORIZED_USER_OPERATION</span></span> | <span data-ttu-id="fe6bc-168">У пользователя нет прав на выполнение этой операции.</span><span class="sxs-lookup"><span data-stu-id="fe6bc-168">User is not authorized to complete this operation.</span></span>|
| <span data-ttu-id="fe6bc-169">**6000**</span><span class="sxs-lookup"><span data-stu-id="fe6bc-169">**6000**</span></span> |<span data-ttu-id="fe6bc-170">INSUFFICIENT_RESOURCES</span><span class="sxs-lookup"><span data-stu-id="fe6bc-170">INSUFFICIENT_RESOURCES</span></span> | <span data-ttu-id="fe6bc-171">Не удалось выполнить операцию из-за недостатка ресурсов.</span><span class="sxs-lookup"><span data-stu-id="fe6bc-171">The operation couldn't be completed due to insufficient resources.</span></span>|
|<span data-ttu-id="fe6bc-172">**7000**</span><span class="sxs-lookup"><span data-stu-id="fe6bc-172">**7000**</span></span> | <span data-ttu-id="fe6bc-173">THROTTLE</span><span class="sxs-lookup"><span data-stu-id="fe6bc-173">THROTTLE</span></span> | <span data-ttu-id="fe6bc-174">Платформа регулирует запрос, так как API вызывался слишком часто.</span><span class="sxs-lookup"><span data-stu-id="fe6bc-174">The platform throttled the request because the API was invoked too frequently.</span></span>|
|  <span data-ttu-id="fe6bc-175">**8000**</span><span class="sxs-lookup"><span data-stu-id="fe6bc-175">**8000**</span></span> | <span data-ttu-id="fe6bc-176">USER_ABORT</span><span class="sxs-lookup"><span data-stu-id="fe6bc-176">USER_ABORT</span></span> |<span data-ttu-id="fe6bc-177">Пользователь прервал операцию.</span><span class="sxs-lookup"><span data-stu-id="fe6bc-177">User aborted the operation.</span></span>|
| <span data-ttu-id="fe6bc-178">**9000**</span><span class="sxs-lookup"><span data-stu-id="fe6bc-178">**9000**</span></span>| <span data-ttu-id="fe6bc-179">OLD_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="fe6bc-179">OLD_PLATFORM</span></span> | <span data-ttu-id="fe6bc-180">Код платформы устарел и не реализует этот API.</span><span class="sxs-lookup"><span data-stu-id="fe6bc-180">The platform code is outdated and doesn't implement this API.</span></span>|
| <span data-ttu-id="fe6bc-181">**10000**</span><span class="sxs-lookup"><span data-stu-id="fe6bc-181">**10000**</span></span>| <span data-ttu-id="fe6bc-182">SIZE_EXCEEDED</span><span class="sxs-lookup"><span data-stu-id="fe6bc-182">SIZE_EXCEEDED</span></span> |  <span data-ttu-id="fe6bc-183">Возвращаемое значение слишком велико и превысило границы размера платформы.</span><span class="sxs-lookup"><span data-stu-id="fe6bc-183">The return value is too big and has exceeded the platform size boundaries.</span></span>|

## <a name="sample-code-snippets"></a><span data-ttu-id="fe6bc-184">Примеры фрагментов кода</span><span class="sxs-lookup"><span data-stu-id="fe6bc-184">Sample code snippets</span></span>

<span data-ttu-id="fe6bc-185">**Вызов `selectMedia` API**</span><span class="sxs-lookup"><span data-stu-id="fe6bc-185">**Calling `selectMedia` API**</span></span>

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

<span data-ttu-id="fe6bc-186">**Вызов `getMedia` API**</span><span class="sxs-lookup"><span data-stu-id="fe6bc-186">**Calling `getMedia` API**</span></span>

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

<span data-ttu-id="fe6bc-187">**Вызов `viewImages`  API по идентификатору**</span><span class="sxs-lookup"><span data-stu-id="fe6bc-187">**Calling `viewImages`  API by ID**</span></span>

```javascript
view images by id:
    assumption: attachmentArray = select Media API Outputlet uriList = [];
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

<span data-ttu-id="fe6bc-188">**Вызов API Виевимажес по URL-адресу**</span><span class="sxs-lookup"><span data-stu-id="fe6bc-188">**Calling viewImages API by URL**</span></span>

```javascript
View Images by URL:
    // Assumption 2 urls, url1 and url2let uriList = [];
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
}
```
