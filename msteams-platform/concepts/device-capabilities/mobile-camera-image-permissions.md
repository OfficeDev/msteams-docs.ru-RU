---
title: Интеграция возможностей мультимедиа
author: Rajeshwari-v
description: Использование SDK Teams JavaScript для обеспечения возможностей мультимедиа
keywords: Возможности микрофона изображения камеры для носителей разрешений на устройства
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 22d4a791e83cf36f18b75a3846865835b0ee024f
ms.sourcegitcommit: 059d22c436ee9b07a61561ff71e03e1c23ff40b8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/30/2021
ms.locfileid: "53211627"
---
# <a name="integrate-media-capabilities"></a>Интеграция возможностей мультимедиа 

Вы можете интегрировать возможности родного  устройства,  такие как камера и микрофон с Teams приложением. Для интеграции можно использовать Microsoft Teams [Клиента JavaScript SDK,](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)который предоставляет средства, необходимые вашему приложению для доступа к разрешениям устройства [пользователя.](native-device-permissions.md) Используйте подходящие API средств массовой информации для  интеграции  возможностей устройства, например камеры и микрофона с платформой Teams в мобильном приложении Microsoft Teams и создания более богатого опыта. 

## <a name="advantage-of-integrating-media-capabilities"></a>Преимущество интеграции возможностей мультимедиа

Основное преимущество интеграции возможностей устройства в приложениях Teams заключается в том, что он использует элементы управления Teams, чтобы обеспечить пользователям богатый и захватывающий опыт.
Чтобы интегрировать возможности мультимедиа, необходимо обновить файл манифеста приложения и вызвать API средств массовой информации. 

Для эффективной интеграции необходимо хорошо [](#code-snippets) понимать фрагменты кода для вызова соответствующих API, которые позволяют использовать возможности родного мультимедиа.

Важно ознакомиться с ошибками [ответа API](#error-handling) для обработки ошибок в Teams приложении.

> [!NOTE] 
> * В настоящее время Microsoft Teams средства массовой информации доступны только для мобильных клиентов.   
> * В настоящее время Teams не поддерживает разрешения устройств для нескольких оконных приложений, вкладок и sidepanel собраний.    

## <a name="update-manifest"></a>Манифест обновления

Обновите Teams приложение [manifest.jsфайле,](../../resources/schema/manifest-schema.md#devicepermissions) добавив `devicePermissions` свойство и указав `media` . Это позволяет приложению запросить необходимые разрешения у пользователей, прежде чем они начнут использовать камеру для захвата изображения, открыть  галерею, чтобы выбрать изображение для отправки в качестве вложения или использовать микрофон для записи беседы.  Обновление манифеста приложения:

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> Запрос **разрешения запроса** автоматически отображается при Teams API. Дополнительные сведения см. в [запросе разрешений устройств.](native-device-permissions.md)

## <a name="media-capability-apis"></a>API возможностей мультимедиа

API [selectMedia,](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true) [getMedia](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediachunk?view=msteams-client-js-latest&preserve-view=true)и [viewImages](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageuri?view=msteams-client-js-latest&preserve-view=true) позволяют использовать возможности родного мультимедиа следующим образом:

* Использование родного **микрофона** позволяет пользователям записывать звук **(запись** 10 минут беседы) с устройства.
* Используйте **родной контроль камеры,** чтобы позволить пользователям **захватывать и прикреплять изображения** в перейти.
* Используйте **поддержку родной галереи,** чтобы позволить пользователям **выбирать изображения устройств в** качестве вложений.
* Используйте управление **для просмотра изображений на** родном уровне, чтобы **просмотреть** несколько изображений одновременно.
* Поддержка **большой передачи изображений** (от 1 МБ до 50 МБ) через мост SDK.
* Поддержка **расширенных возможностей изображения,** позволяющих пользователям просматривать и изменять изображения:
  * Сканирование документов, доски и визитных карт с помощью камеры.
  
> [!IMPORTANT]
> * API и API можно вызывать с нескольких поверхностей Teams, таких как модули задач, вкладки `selectMedia` `getMedia` и `viewImages` личные приложения. Дополнительные сведения см. в [материале Пункты входа для Teams приложений.](../extensibility-points.md)
> * `selectMedia` API расширен для поддержки свойств микрофона и звука.

Чтобы включить возможности мультимедиа устройства, необходимо использовать следующий набор API:

| API      | Описание   |
| --- | --- |
| [**selectMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true) **(Камера)**| Этот API позволяет  пользователям захватывать или выбирать носители из камеры устройства и возвращать его в веб-приложение. Пользователи могут изменять, обрезать, вращать, аннотировать или рисовать изображения перед отправкой. В ответ веб-приложение получает медиа-ID выбранных изображений и эскиз `selectMedia` выбранного носитля. Этот API можно дополнительно настроить с помощью [конфигурации ImageProps.](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageprops?view=msteams-client-js-latest&preserve-view=true) |
| [**selectMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true) **(Микрофон)**| Установите [mediaType](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediatype?view=msteams-client-js-latest&preserve-view=true) в `4` `selectMedia` API для доступа к возможностям микрофона. Этот API также позволяет пользователям записывать звук с микрофона устройства и возвращать записанные клипы в веб-приложение. Перед отправкой пользователи могут приостанавлить, перезаписи и воспроизведения предварительного просмотра записи. В ответ на **selectMedia** веб-приложение получает медиа-ID выбранной аудиозаписи. <br/> Используйте, если требуется настроить продолжительность в минутах `maxDuration` для записи беседы. Текущая продолжительность записи составляет 10 минут, после чего запись прекращается.  |
| [**getMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediachunk?view=msteams-client-js-latest&preserve-view=true)| Этот API извлекает средства массовой информации, захваченные API в `selectMedia` куски, независимо от размера мультимедиа. Эти фрагменты собираются и отправляются обратно в веб-приложение в качестве файла или blob. Размыв мультимедиа на меньшие куски упрощает передачу больших файлов. |
| [**viewImages**](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageuri?view=msteams-client-js-latest&preserve-view=true)| Этот API позволяет пользователю просматривать изображения в полноэкранном режиме в качестве списка прокрутки.|

На следующем изображении повеяна возможность `selectMedia` API для веб-приложений:

![устройство камеры и изображения в Teams](../../assets/images/tabs/image-capability.png)

На следующем изображении показана возможность API API веб-приложения `selectMedia` для микрофона:

![Возможности веб-приложения для микрофона](../../assets/images/tabs/microphone-capability.png)

## <a name="error-handling"></a>Обработка ошибок

Необходимо обеспечить надлежащее обработку этих ошибок в Teams приложении. В следующей таблице перечислены коды ошибок и условия, при которых создаются ошибки: 

|Код ошибки |  Имя ошибки     | Condition|
| --------- | --------------- | -------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | API не поддерживается на текущей платформе.|
| **404** | FILE_NOT_FOUND | Указанный файл не найден в указанном расположении.|
| **500** | INTERNAL_ERROR | При выполнении необходимой операции встречаются внутренние ошибки.|
| **1000** | PERMISSION_DENIED |Пользователю отказано в разрешении.|
| **3000** | NO_HW_SUPPORT | Оборудование не поддерживает эту возможность.|
| **4000**| INVALID_ARGUMENTS | Один или несколько аргументов являются недействительными.|
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

* [Интеграция возможностей сканера QR или штрихкодов в Teams](qr-barcode-scanner-capability.md)
* [Интеграция возможностей расположения в Teams](location-capability.md)
* [Интеграция возможностей выборщика людей в Teams](people-picker-capability.md)

