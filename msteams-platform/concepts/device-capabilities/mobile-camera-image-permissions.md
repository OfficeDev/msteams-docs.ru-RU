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
# <a name="camera-and-image-capabilities-in-teams"></a>Возможности работы с камерами и изображениями в Teams

>[!IMPORTANT]
>
> * В настоящее время поддержка возможностей камеры и изображений в Teams доступна только для мобильных клиентов.
>* `selectMedia`API, `getMedia` и `viewImages` API можно вызывать из нескольких поверхностей Teams, таких как модули задач, вкладки и персональные приложения. Более подробную информацию можно _узнать_ в статье [точки входа для приложений Teams](../extensibility-points.md)

Вы можете использовать  [клиентский пакет SDK для Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), чтобы легко интегрировать возможности камеры и изображения в мобильное приложение Microsoft Teams. Пакет SDK предоставляет средства, необходимые для приложения, чтобы получить доступ к [разрешениям устройства](native-device-permissions.md?tabs=desktop#device-permissions) пользователя и создать более насыщенный интерфейс.

Интерфейсы API [селектмедиа](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true), [Media](/javascript/api/@microsoft/teams-js/_media?view=msteams-client-js-latest#getMedia__error__SdkError__blob__Blob_____void_&preserve-view=true)и [виевимажес](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#viewImages_ImageUri_____error___SdkError_____void_&preserve-view=true) позволяют использовать встроенные возможности камеры и изображения следующим образом:

* Используйте встроенный **элемент управления камерой** , чтобы позволить пользователям **записывать и прикреплять изображения** в дороге.
* Используйте встроенную **поддержку коллекций** , чтобы позволить пользователям **выбирать изображения устройств** в качестве вложений.
* Использование встроенного **элемента управления для просмотра изображений** для **предварительного просмотра нескольких изображений** за один раз.
* Поддержка **передачи больших изображений** (до 50 МБ) с помощью моста SDK
* Поддерживает **Расширенные возможности работы с изображениями** , позволяющие пользователям просматривать и редактировать изображения:
  * Сканировать документы, доску, визитные карточки и т. д. через камеру.
  * Обрежьте и поверните изображения.
  * Добавление текста, рукописного фрагмента или заметки FreeHand к изображению.

## <a name="get-started"></a>Начало работы

Обновите приложение Teams [manifest.jsв](../../resources/schema/manifest-schema.md#devicepermissions) файле, добавив `devicePermissions`  свойство и указав `media` . Это позволяет приложению запрашивать у конечных пользователей разрешения, прежде чем использовать камеру для записи изображения или открытия коллекции для выбора изображения, которое будет отправлено в виде вложения.

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> Запрос на получение _разрешений_ автоматически отображается при инициации соответствующего API Teams. Дополнительные сведения см. в *разделе* [request Permissions Devices](native-device-permissions.md).

## <a name="using-camera-and-image-capability-apis"></a>Использование интерфейсов API возможностей камеры и изображений

Можно использовать следующий набор API для включения возможностей камеры и устройств с изображениями:

| API      | Description   |
| --- | --- |
| [**селектмедиа**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest&branch=master#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true)| Этот API позволяет пользователям **записывать или выбирать мультимедиа на исходном устройстве** и возвращать в веб-приложение. Пользователи могут изменять, обрезать, поворачивать, закомментировать и рисовать изображения перед отправкой. В ответ на **селектмедиа** веб-приложение получит идентификаторы носителей выбранных изображений и получит эскиз выбранного носителя. |
| [**Мультимедиа**](/javascript/api/@microsoft/teams-js/_media?view=msteams-client-js-latest&branch=master#getMedia__error__SdkError__blob__Blob_____void_&preserve-view=true)| Этот API получает носители в блоках независимо от размера. Эти блоки собраны и отправляются обратно в веб-приложение в виде файла или большого двоичного объекта. С помощью этого API изображение разбивается на небольшие блоки для упрощения передачи изображений. |
| [**виевимажес**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#viewImages_ImageUri_____error___SdkError_____void_&preserve-view=true)| Этот API позволяет пользователю просматривать изображения в полноэкранном режиме в виде прокручиваемого списка.|

**Взаимодействие с веб-приложениями для API селектмедиа** 
 ![ Камера устройств и взаимодействие с изображениями в Teams](../../assets/images/tabs/image-capability-screenshot.jpg)

## <a name="error-handling"></a>Обработка ошибок

Необходимо изучить коды ошибок ответа API и соответствующим образом обработать их. Ниже приведен список кодов ошибок, которые могут быть возвращены платформой:

|Код ошибки |  Имя ошибки     | Condition|
| --- | --- | --- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | API не поддерживается в текущей платформе.|
| **404** | FILE_NOT_FOUND | Указанный файл не найден в указанном расположении.|
| **500** | INTERNAL_ERROR | При выполнении необходимой операции возникла внутренняя ошибка.|
| **1000** | PERMISSION_DENIED |Разрешения, запрещенные пользователем.|
| **2000** |NETWORK_ERROR | Сетевая ошибка.|
| **3000** | NO_HW_SUPPORT | Базовое оборудование не поддерживает эту возможность.|
| **4000**| INVALID_ARGUMENTS | Один или несколько аргументов являются недопустимыми.|
| **5000** | UNAUTHORIZED_USER_OPERATION | У пользователя нет прав на выполнение этой операции.|
| **6000** |INSUFFICIENT_RESOURCES | Не удалось выполнить операцию из-за недостатка ресурсов.|
|**7000** | THROTTLE | Платформа регулирует запрос, так как API вызывался слишком часто.|
|  **8000** | USER_ABORT |Пользователь прервал операцию.|
| **9000**| OLD_PLATFORM | Код платформы устарел и не реализует этот API.|
| **10000**| SIZE_EXCEEDED |  Возвращаемое значение слишком велико и превысило границы размера платформы.|

## <a name="sample-code-snippets"></a>Примеры фрагментов кода

**Вызов `selectMedia` API**

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

**Вызов `getMedia` API**

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

**Вызов `viewImages`  API по идентификатору**

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

**Вызов API Виевимажес по URL-адресу**

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
