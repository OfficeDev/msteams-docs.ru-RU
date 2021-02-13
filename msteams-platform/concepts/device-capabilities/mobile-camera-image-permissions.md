---
title: Интеграция возможностей мультимедиа
description: Использование клиентского SDK JavaScript для Teams для обеспечения возможностей мультимедиа
keywords: 'Микрофон изображения камеры: встроенный носитель разрешений устройства'
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 4126551858116343689e08c4b4f385eb0bbc7ed1
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231601"
---
# <a name="integrate-media-capabilities"></a>Интеграция возможностей мультимедиа 

В этом документе вы можете узнать, как интегрировать возможности мультимедиа. Эта интеграция объединяет встроенные возможности  устройства, такие как камера и **микрофон,** с платформой Teams.  

Вы можете использовать [клиентский SDK JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)для Microsoft Teams, который предоставляет средства, необходимые приложению для доступа к разрешениям устройства [пользователя.](native-device-permissions.md) Используйте **подходящие** API возможностей мультимедиа для интеграции встроенных  возможностей  устройств, таких как камера и микрофон, с платформой Teams в мобильном приложении Microsoft Teams, и создайте более богатые возможности. 

## <a name="advantage-of-integrating-media-capabilities"></a>Преимущества интеграции возможностей мультимедиа

Основное преимущество интеграции возможностей устройств в приложения Teams заключается в том, что он использует встроенные элементы управления Teams, чтобы предоставить пользователям богатый и иммерсивный опыт.
Для интеграции возможностей мультимедиа необходимо обновить файл манифеста приложения и вызвать API возможностей мультимедиа. 

Для эффективной интеграции необходимо иметь [](#code-snippets) хорошее представление о фрагментах кода для вызова соответствующих API, которые позволяют использовать возможности нативных носителей.

Важно ознакомиться с ошибками ответа [API](#error-handling) для обработки ошибок в приложении Teams.

> [!NOTE] 
> В настоящее время поддержка возможностей мультимедиа в Microsoft Teams доступна только для мобильных клиентов.

## <a name="update-manifest"></a>Обновление манифеста

Обновите приложение Teams [manifest.jsв файле,](../../resources/schema/manifest-schema.md#devicepermissions) добавив `devicePermissions` свойство и указав `media` . Это позволяет приложению запросить необходимые разрешения у пользователей, прежде чем они начнут использовать камеру для захвата изображения, откройте  галерею, чтобы выбрать изображение для отправки в виде вложения, или используйте микрофон для записи беседы. 

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> Запрос **разрешений автоматически** отображается при инициировании соответствующего API Teams. Дополнительные сведения см. в [запросе разрешений устройства.](native-device-permissions.md)

## <a name="media-capability-apis"></a>API возможностей мультимедиа

API [selectMedia,](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true) [getMedia](/javascript/api/@microsoft/teams-js/_media?view=msteams-client-js-latest#getMedia__error__SdkError__blob__Blob_____void_&preserve-view=true)и [viewImages](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#viewImages_ImageUri_____error___SdkError_____void_&preserve-view=true) позволяют использовать возможности нативных носителей следующим образом:

* Используйте встроенный **микрофон,** чтобы разрешить пользователям записывать звук **(запись** 10 минут беседы) с устройства.
* Используйте **нативный контроль камеры,** чтобы разрешить пользователям **захватывать и присоединять изображения** в путь.
* Используйте **поддержку коллекции,** чтобы разрешить пользователям выбирать изображения **устройств в** качестве вложений.
* Используйте **нативный контроль просмотра изображений** для **предварительного просмотра нескольких изображений** одновременно.
* Поддержка **передачи больших изображений** (от 1 МБ до 50 МБ) через мост SDK.
* Поддержка **расширенных возможностей изображений,** позволяющих пользователям просматривать и редактировать изображения:
  * Сканирование документа, доски и визитных карточек с помощью камеры.
  
> [!IMPORTANT]
>*   API , и могут вызываться из нескольких поверхностей Teams, таких как модули задач, вкладки `selectMedia` `getMedia` и `viewImages` личные приложения. Дополнительные сведения [см. в пунктах входа для приложений Teams.](../extensibility-points.md)
>* `selectMedia` API был расширен для поддержки свойств микрофона и звука.

Чтобы включить возможности мультимедиа на устройстве, необходимо использовать следующий набор API:

| API      | Описание   |
| --- | --- |
| [**selectMedia**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true) (**Camera)**| Этот API позволяет пользователям захватывать или выбирать **мультимедиа** с камеры устройства и возвращать его в веб-приложение. Пользователи могут редактировать, обрезать, вращать, примечать или рисовать изображения перед отправкой. В ответ на **selectMedia** веб-приложение получает ид мультимедиа выбранных изображений и эскиз выбранного мультимедиа. Этот API можно дополнительно настроить с помощью [конфигурации ImageProps.](/javascript/api/@microsoft/teams-js/imageprops?view=msteams-client-js-latest&preserve-view=true) |
| [**selectMedia**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true) **(микрофон)**| Установите [для mediaType](/javascript/api/@microsoft/teams-js/mediatype?view=msteams-client-js-latest&preserve-view=true) в `4` **selectMedia** API для доступа к возможности микрофона. Этот API также позволяет пользователям записывать звук с микрофона устройства и возвращать записанные клипы в веб-приложение. Пользователи могут приостанавлить, повторно записывать и играть предварительный просмотр записи перед отправкой. В ответ на **selectMedia** веб-приложение получает ид мультимедиа выбранной аудиозаписи. <br/> Используйте , если требуется настроить длительность в минутах `maxDuration` для записи беседы. Текущая продолжительность записи составляет 10 минут, после чего запись завершается.  |
| [**getMedia**](/javascript/api/@microsoft/teams-js/_media?view=msteams-client-js-latest#getMedia__error__SdkError__blob__Blob_____void_&preserve-view=true)| Этот API извлекает мультимедиа, захваченные **selectMedia** API, фрагментами, независимо от размера мультимедиа. Эти блоки собираются и отправляются обратно в веб-приложение в качестве файла или BLOB-файла. Размыв мультимедиа на меньшие блоки упрощает передачу больших файлов. |
| [**viewImages**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#viewImages_ImageUri_____error___SdkError_____void_&preserve-view=true)| Этот API позволяет пользователю просматривать изображения в полноэкранном режиме в качестве прокручиваемого списка.|


**Возможности веб-приложения для selectMedia API для функции изображений** 
 ![ Камеры и изображения устройств в Teams](../../assets/images/tabs/image-capability.png)

**Возможности веб-приложения для selectMedia API для возможности микрофона** 
 ![ Возможности веб-приложения для работы с микрофоном](../../assets/images/tabs/microphone-capability.png)

## <a name="error-handling"></a>Обработка ошибок

В приложении Teams необходимо обеспечить соответствующую обработку этих ошибок. В следующей таблице перечислены коды ошибок и условия, при которых создаются ошибки: 


|Код ошибки |  Имя ошибки     | Condition|
| --------- | --------------- | -------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | API не поддерживается на текущей платформе.|
| **404** | FILE_NOT_FOUND | Указанный файл не найден в указанном расположении.|
| **500** | INTERNAL_ERROR | При выполнении необходимой операции произошла внутренняя ошибка.|
| **1000** | PERMISSION_DENIED |Пользователь отказано в разрешении.|
| **2000** |NETWORK_ERROR | Проблема с сетью.|
| **3000** | NO_HW_SUPPORT | Аппаратное обеспечение не поддерживает эту возможность.|
| **4000**| INVALID_ARGUMENTS | Один или несколько аргументов недопустимы.|
| **5000** | UNAUTHORIZED_USER_OPERATION | Пользователь не имеет права на завершение этой операции.|
| **6000** |INSUFFICIENT_RESOURCES | Не удалось завершить операцию из-за недостатка ресурсов.|
|**7000** | THROTTLE | Платформа регулирования запроса, так как API вызывался часто.|
|  **8000** | USER_ABORT |Пользователь прерывает операцию.|
| **9000**| OLD_PLATFORM | Код платформы устарел и не реализует этот API.|
| **10000**| SIZE_EXCEEDED |  Возвращаемая величина слишком велика и превысила границы размера платформы.|

## <a name="code-snippets"></a>Фрагменты кода

**Вызов `selectMedia` API для** захвата изображений с помощью камеры:

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

**Вызов `getMedia` API для** получения больших объемов мультимедиа по частям:

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

**Вызов `viewImages` API по ИД, возвращаемой `selectMedia` API:**

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

**Вызовы `selectMedia` и `getMedia` API для записи звука с помощью микрофона:**

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
