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
# <a name="integrate-media-capabilities"></a>Интеграция возможностей мультимедиа 

В этом документе содержится руководство по интеграции возможностей мультимедиа. Эта интеграция объединяет родной потенциал  устройства, например камеру и **микрофон с** платформой Teams.  

Вы можете использовать [клиент microsoft Teams JavaScript SDK,](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)который предоставляет средства, необходимые вашему приложению для доступа к разрешениям на [устройства пользователя.](native-device-permissions.md) Используйте **подходящие** API средств массовой информации для интеграции  родных возможностей устройства, например камеры и микрофона с платформой Teams в мобильном приложении Microsoft Teams, и создания более богатого опыта.  

## <a name="advantage-of-integrating-media-capabilities"></a>Преимущество интеграции возможностей мультимедиа

Основное преимущество интеграции возможностей устройств в приложениях Teams заключается в том, что он использует элементы управления native Teams, чтобы обеспечить пользователям богатый и захватывающий опыт.
Чтобы интегрировать возможности мультимедиа, необходимо обновить файл манифеста приложения и вызвать API средств массовой информации. 

Для эффективной интеграции необходимо хорошо [](#code-snippets) понимать фрагменты кода для вызова соответствующих API, которые позволяют использовать возможности родного мультимедиа.

Важно ознакомиться с ошибками [ответа API](#error-handling) для обработки ошибок в приложении Teams.

> [!NOTE] 
> В настоящее время поддержка microsoft Teams для средств массовой информации доступна только для мобильных клиентов.

## <a name="update-manifest"></a>Манифест обновления

Обновите приложение Teams [manifest.jsфайле,](../../resources/schema/manifest-schema.md#devicepermissions) добавив `devicePermissions` свойство и указав `media` . Это позволяет приложению запросить необходимые разрешения у пользователей, прежде чем они начнут использовать камеру для захвата изображения, открыть  галерею, чтобы выбрать изображение для отправки в качестве вложения или использовать микрофон для записи беседы. 

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> Запрос **разрешений** автоматически отображается при инициировании соответствующего API Teams. Дополнительные сведения см. в [запросе разрешений устройств.](native-device-permissions.md)

## <a name="media-capability-apis"></a>API возможностей мультимедиа

API [selectMedia,](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true) [getMedia](/javascript/api/@microsoft/teams-js/_media?view=msteams-client-js-latest#getMedia__error__SdkError__blob__Blob_____void_&preserve-view=true)и [viewImages](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#viewImages_ImageUri_____error___SdkError_____void_&preserve-view=true) позволяют использовать возможности родного мультимедиа следующим образом:

* Использование родного **микрофона** позволяет пользователям записывать звук **(запись** 10 минут беседы) с устройства.
* Используйте **родной контроль камеры,** чтобы позволить пользователям **захватывать и прикреплять изображения** в перейти.
* Используйте **поддержку родной галереи,** чтобы позволить пользователям **выбирать изображения устройств в** качестве вложений.
* Используйте управление **для просмотра изображений на** родном уровне, чтобы **просмотреть** несколько изображений одновременно.
* Поддержка **большой передачи изображений** (от 1 МБ до 50 МБ) через мост SDK.
* Поддержка **расширенных возможностей изображения,** позволяющих пользователям просматривать и изменять изображения:
  * Сканирование документов, доски и визитных карт с помощью камеры.
  
> [!IMPORTANT]
>*   API и API можно вызывать с нескольких поверхностей Teams, таких как модули задач, вкладки `selectMedia` `getMedia` и `viewImages` личные приложения. Дополнительные сведения см. в [материале Пункты входа для приложений Teams.](../extensibility-points.md)
>* `selectMedia` API был расширен для поддержки свойств микрофона и звука.

Чтобы включить возможности мультимедиа устройства, необходимо использовать следующий набор API:

| API      | Description   |
| --- | --- |
| [**selectMedia**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true) **(Камера)**| Этот API позволяет  пользователям захватывать или выбирать носители из камеры устройства и возвращать его в веб-приложение. Пользователи могут изменять, обрезать, вращать, аннотировать или рисовать изображения перед отправкой. В ответ **на selectMedia** веб-приложение получает медиа-ИД выбранных изображений и эскиз выбранного мультимедиа. Этот API можно дополнительно настроить с помощью [конфигурации ImageProps.](/javascript/api/@microsoft/teams-js/imageprops?view=msteams-client-js-latest&preserve-view=true) |
| [**selectMedia**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true) **(Микрофон)**| Установите [mediaType](/javascript/api/@microsoft/teams-js/mediatype?view=msteams-client-js-latest&preserve-view=true) в `4` **selectMedia** API для доступа к возможностям микрофона. Этот API также позволяет пользователям записывать звук с микрофона устройства и возвращать записанные клипы в веб-приложение. Перед отправкой пользователи могут приостанавлить, перезаписи и воспроизведения предварительного просмотра записи. В ответ на **selectMedia** веб-приложение получает медиа-ID выбранной аудиозаписи. <br/> Используйте, если требуется настроить продолжительность в `maxDuration` минутах для записи беседы. Текущая продолжительность записи составляет 10 минут, после чего запись прекращается.  |
| [**getMedia**](/javascript/api/@microsoft/teams-js/_media?view=msteams-client-js-latest#getMedia__error__SdkError__blob__Blob_____void_&preserve-view=true)| Этот API извлекает средства массовой информации, захваченные **selectMedia** API в куски, независимо от размера мультимедиа. Эти фрагменты собираются и отправляются обратно в веб-приложение в качестве файла или blob. Размыв мультимедиа на меньшие куски упрощает передачу больших файлов. |
| [**viewImages**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#viewImages_ImageUri_____error___SdkError_____void_&preserve-view=true)| Этот API позволяет пользователю просматривать изображения в полноэкранном режиме в качестве списка прокрутки.|


**Опыт работы с веб-приложением для selectMedia API для возможностей изображения** 
 ![ Камера устройства и опыт работы с изображениями в Teams](../../assets/images/tabs/image-capability.png)

**Опыт работы веб-приложения для selectMedia API для возможностей микрофона** 
 ![ Возможности веб-приложения для микрофона](../../assets/images/tabs/microphone-capability.png)

## <a name="error-handling"></a>Обработка ошибок

Необходимо обеспечить надлежащее обработку этих ошибок в приложении Teams. В следующей таблице перечислены коды ошибок и условия, при которых создаются ошибки: 


|Код ошибки |  Имя ошибки     | Condition|
| --------- | --------------- | -------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | API не поддерживается на текущей платформе.|
| **404** | FILE_NOT_FOUND | Указанный файл не найден в указанном расположении.|
| **500** | INTERNAL_ERROR | При выполнении необходимой операции встречаются внутренние ошибки.|
| **1000** | PERMISSION_DENIED |Пользователю отказано в разрешении.|
| **2000** |NETWORK_ERROR | Проблема сети.|
| **3000** | NO_HW_SUPPORT | Оборудование не поддерживает эту возможность.|
| **4000**| INVALID_ARGUMENTS | Один или несколько аргументов являются недействительными.|
| **5000** | UNAUTHORIZED_USER_OPERATION | Пользователь не уполномочен выполнить эту операцию.|
| **6000** |INSUFFICIENT_RESOURCES | Операция не может быть завершена из-за нехватки ресурсов.|
|**7000** | THROTTLE | Платформа уравняла запрос, так как API часто вызывался.|
|  **8000** | USER_ABORT |Пользователь прерывает операцию.|
| **9000**| OLD_PLATFORM | Код платформы устарел и не реализует этот API.|
| **10000**| SIZE_EXCEEDED |  Значение return слишком большое и превысило границы размера платформы.|

## <a name="code-snippets"></a>Фрагменты кода

**Вызов `selectMedia` API** для захвата изображений с помощью камеры:

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

**Вызов `getMedia` API** для получения больших мультимедиа в кусках:

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

**Вызов `viewImages` API по ID, возвращенный `selectMedia` API:**

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

**Вызов `viewImages` API по URL-адресу:**

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

**Вызовы `selectMedia` и `getMedia` API для записи звука через микрофон:**

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

## <a name="see-also"></a>См. также

> [!div class="nextstepaction"]
> [Интеграция функций сканера QR или штрихкодов в Teams](qr-barcode-scanner-capability.md)