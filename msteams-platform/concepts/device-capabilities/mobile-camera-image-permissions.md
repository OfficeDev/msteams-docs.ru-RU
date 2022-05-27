---
title: Интеграция возможностей мультимедиа
author: Rajeshwari-v
description: Узнайте, как использовать клиентский пакет SDK Teams JavaScript для включения мультимедийных возможностей с помощью примеров кода.
keywords: API мультимедиа разрешений для встроенного устройства с изображением камеры
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: lajanuar
ms.openlocfilehash: a65f39d3796bc0dacaa80f6badba7a011716edbf
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/27/2022
ms.locfileid: "65756760"
---
# <a name="integrate-media-capabilities"></a>Интеграция возможностей мультимедиа

Вы можете интегрировать собственные возможности устройства, такие как **камера** и **микрофон**, с вашим приложением Teams. Для интеграции вы можете использовать [SDK клиента Microsoft Teams JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), который предоставляет инструменты, необходимые вашему приложению для доступа к [разрешениям устройства](native-device-permissions.md) пользователя. Используйте подходящие API-интерфейсы мультимедийных возможностей, чтобы интегрировать возможности устройства, такие как **камера** и **микрофон**, с платформой Teams в вашем мобильном приложении Microsoft Teams и создать более богатые возможности.

## <a name="advantage-of-integrating-media-capabilities"></a>Преимущество интеграции медиа-возможностей

Основное преимущество интеграции возможностей устройств в ваши приложения Teams заключается в том, что они используют собственные элементы управления Teams, чтобы предоставить вашим пользователям богатый и захватывающий опыт.
Чтобы интегрировать возможности мультимедиа, необходимо обновить файл манифеста приложения и вызвать API возможностей мультимедиа.

Для эффективной интеграции вы должны хорошо понимать [фрагменты кода](#code-snippets) для вызова соответствующих API, которые позволяют использовать собственные возможности мультимедиа.

Важно ознакомиться с ошибками ответа [API](#error-handling) для обработки ошибок в Teams приложения.

> [!NOTE]
>
> * В настоящее время Microsoft Teams поддерживает возможности мультимедиа только для мобильных клиентов.
> * Сейчас Teams не поддерживает разрешения устройств для многооконных приложений, вкладок и боковой панели собрания.
> * Разрешения устройства отличаются в браузере. Подробнее см. в разделе [Разрешения устройств в браузере](browser-device-permissions.md).

## <a name="update-manifest"></a>Изменение манифеста

Обновите файл [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) приложения Teams, добавив свойство `devicePermissions` и указав `media`. Это позволяет вашему приложению запрашивать необходимые разрешения у пользователей, прежде чем они начнут использовать **камеру** для захвата изображения, открывать галерею, чтобы выбрать изображение для отправки в качестве вложения, или использовать **микрофон** для записи разговора. Измените манифест приложения, выполнив следующие шаги.

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> **Запрос разрешений** автоматически отображается при запуске соответствующего API Teams. Дополнительные сведения см. в статье [Запрос разрешений устройства](native-device-permissions.md).

## <a name="media-capability-apis"></a>API-интерфейсы мультимедийных возможностей

В [selectMedia](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true), [getMedia](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediachunk?view=msteams-client-js-latest&preserve-view=true) и [viewImages](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageuri?view=msteams-client-js-latest&preserve-view=true) API-интерфейсы позволяют использовать собственные мультимедийные возможности следующим образом:

* Используйте **microphone** чтобы разрешить пользователям **запись звука** (запись 10 минут беседы) с устройства.
* Используйте встроенное **управление камерой**, чтобы пользователи могли **снимать и прикреплять изображения** на ходу.
* Используйте встроенную **поддержку галереи**, чтобы пользователи могли **выбирать изображения устройств** в качестве вложений.
* Используйте встроенное **средство просмотра изображений** для одновременного **предварительного просмотра нескольких изображений**.
* Поддержка **передачи больших изображений** (от 1 МБ до 50 МБ) через мост SDK.
* Поддержка **расширенных возможностей** изображения позволяет пользователям просматривать и редактировать изображения:
  * Сканируйте документы, доски и визитные карточки с помощью камеры.
  
> [!IMPORTANT]
>
> * API-интерфейсы `selectMedia`, `getMedia`, и `viewImages` можно вызывать из нескольких поверхностей Teams, таких как модули задач, вкладки и личные приложения. Дополнительные сведения см. в [разделе "Точки входа" Teams приложений](../extensibility-points.md).
> * `selectMedia` API был расширен для поддержки свойств микрофона и звука.

чтобы включить мультимедийные возможности вашего устройства, необходимо использовать следующий набор API:

| API      | Описание   |
| --- | --- |
| [**selectMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true) (**Камера)**| Этот API позволяет пользователям **захватывать или выбирать мультимедиа с камеры устройства** и возвращать его в веб-приложение. Пользователи могут редактировать, обрезать, поворачивать, комментировать или рисовать поверх изображений перед отправкой. В ответ `selectMedia` веб-приложение получает идентификаторы мультимедиа выбранных изображений и миниатюру выбранного мультимедиа. Этот API можно дополнительно настроить с помощью конфигурации [ImageProps](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageprops?view=msteams-client-js-latest&preserve-view=true). |
| [**selectMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true) (**Микрофон**)| Установите [mediaType](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediatype?view=msteams-client-js-latest&preserve-view=true) на `4` в `selectMedia` для доступа к возможностям микрофона. Этот API также позволяет пользователям записывать звук с микрофона устройства и возвращать записанные клипы в веб-приложение. Пользователи могут приостанавливать, перезаписывать и предварительно прослушивать записи перед отправкой. В ответ на  **selectMedia** веб-приложение получает идентификаторы мультимедиа выбранной аудиозаписи. <br/> Используйте `maxDuration`, если вам нужно настроить продолжительность записи разговора в минутах. Текущая продолжительность записи составляет 10 минут, после чего запись прекращается.  |
| [**getMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediachunk?view=msteams-client-js-latest&preserve-view=true)| Этот API извлекает мультимедиа, захваченные API `selectMedia`, по частям, независимо от размера мультимедиа. Эти фрагменты собираются и отправляются обратно в веб-приложение в виде файла или большого двоичного объекта. Разбивка мультимедиа на более мелкие фрагменты облегчает передачу больших файлов. |
| [**viewImages**](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageuri?view=msteams-client-js-latest&preserve-view=true)| Этот API позволяет пользователю просматривать изображения в полноэкранном режиме в виде прокручиваемого списка.|

На следующем изображении показано взаимодействие веб-приложения с API `selectMedia` для возможности изображения:

![камера устройства и изображения в Teams](../../assets/images/tabs/image-capability.png)

На следующем изображении показано взаимодействие веб-приложения с API `selectMedia` для возможности микрофона.

![взаимодействие с веб-приложением для возможности микрофона](../../assets/images/tabs/microphone-capability.png)

## <a name="error-handling"></a>Обработка ошибок

Обеспечьте правильную обработку этих ошибок в приложении Teams. В следующей таблице перечислены коды ошибок и условия, при которых возникают ошибки:

|Код ошибки |  Название ошибки     | Условие|
| --------- | --------------- | -------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | API не поддерживается на текущей платформе.|
| **404** | FILE_NOT_FOUND | Указанный файл не найден в указанном расположении.|
| **500** | INTERNAL_ERROR | При выполнении требуемой операции обнаружена внутренняя ошибка.|
| **1000** | PERMISSION_DENIED |Разрешение отклонено пользователем.|
| **3000** | NO_HW_SUPPORT | Базовое оборудование не поддерживает эту возможность.|
| **4000**| INVALID_ARGUMENTS | Один или несколько недопустимых аргументов.|
|  **8000** | USER_ABORT |Пользователь прерывает операцию.|
| **9000**| OLD_PLATFORM | Код платформы устарел и не реализует этот API.|
| **10000**| SIZE_EXCEEDED |  Возвращаемое значение слишком велико и превышает пределы размера платформы.|

## <a name="code-snippets"></a>Фрагменты кода

**Вызов`selectMedia` API** для захвата изображений с помощью камеры:

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

**Вызов`getMedia` API** для извлечения больших медиа фрагментами:

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

**Вызов`viewImages` по идентификатору, возвращаемому `selectMedia` API**:

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

**Вызов`viewImages` API по URL**:

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

**Вызов`selectMedia` и `getMedia` API для записи звука через микрофон**:

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

## <a name="see-also"></a>Дополнительные ресурсы

* [Интегрируйте возможности сканера QR или штрих-кода в Teams](qr-barcode-scanner-capability.md)
* [Интеграция функций местонахождения](location-capability.md)
* [Интеграция средства выбора людей в Teams](people-picker-capability.md)
* [Требования и рекомендации для медиа-ботов, размещаемых в приложениях](~/bots/calls-and-meetings/requirements-considerations-application-hosted-media-bots.md)
