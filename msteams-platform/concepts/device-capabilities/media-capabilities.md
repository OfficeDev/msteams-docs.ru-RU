---
title: Интеграция возможностей мультимедиа
author: Rajeshwari-v
description: Узнайте, как использовать клиентский пакет SDK JavaScript для Teams для включения возможностей мультимедиа с помощью примеров кода, а также преимущества интеграции возможностей мультимедиа.
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: lajanuar
ms.openlocfilehash: b4e552f77b181d005f4a2f3da7967a0fdb1f3ac5
ms.sourcegitcommit: 79d525c0be309200e930cdd942bc2c753d0b718c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/19/2022
ms.locfileid: "66841780"
---
# <a name="integrate-media-capabilities"></a>Интеграция возможностей мультимедиа

Вы можете интегрировать собственные возможности устройства, такие как камера и микрофон, с приложением Teams. Для интеграции можно использовать клиентский [пакет SDK JavaScript для Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) , который предоставляет необходимые инструменты для доступа к разрешениям устройства [пользователя](native-device-permissions.md). Используйте подходящие API возможностей мультимедиа для интеграции возможностей устройства, таких как камера и микрофон, с платформой Teams в приложении Microsoft Teams и создания более удобного интерфейса. Возможность мультимедиа доступна для веб-клиента Teams, настольных компьютеров и мобильных устройств. Чтобы интегрировать возможности мультимедиа, необходимо обновить файл манифеста приложения и вызвать API возможностей мультимедиа.

Для эффективной интеграции вы должны хорошо понимать [фрагменты кода](#code-snippets) для вызова соответствующих API, которые позволяют использовать собственные возможности мультимедиа. Важно ознакомиться с [ошибками ответа API](#error-handling) для управления ошибками в приложении Teams.

## <a name="advantages"></a>Преимущества

Основное преимущество интеграции возможностей устройств в ваши приложения Teams заключается в том, что они используют собственные элементы управления Teams, чтобы предоставить вашим пользователям богатый и захватывающий опыт. В следующих сценариях демонстрируются преимущества возможностей мультимедиа:

* Разрешите пользователю записывать приблизительный макет, нарисованный на физической доске через мобильный телефон, и использовать полученные изображения в качестве параметров опроса в групповом чате Teams.

* Разрешите пользователю записывать звуковое сообщение и присоединять его к запросу на инцидент.

* Разрешите пользователю сканировать физические документы со смартфона, чтобы создать заявку на автострахование.

> [!NOTE]
>
> * В настоящее время Teams не поддерживает разрешения устройств во всплывающем окне чата, вкладке и панели на стороне собрания.</br>
> * Разрешения устройства в браузере отличаются. Дополнительные сведения см. в статье [Разрешения устройств в браузере](browser-device-permissions.md).
> * Запрос разрешений автоматически отображается на мобильном устройстве при запуске соответствующего API Teams. Дополнительные сведения см. в статье [Запрос разрешений устройства](native-device-permissions.md).

## <a name="update-manifest"></a>Изменение манифеста

Обновите файл [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) своего приложения Teams, добавив свойство `devicePermissions` и указав `media`. Это позволяет вашему приложению запрашивать необходимые разрешения у пользователей, прежде чем они начнут использовать камеру для захвата изображения, открывать галерею, чтобы выбрать изображение для отправки в качестве вложения, или использовать микрофон для записи разговора. Измените манифест приложения, выполнив следующие шаги.

``` json
"devicePermissions": [
    "media",
],
```

## <a name="media-capability-apis"></a>API-интерфейсы мультимедийных возможностей

В [selectMedia](/javascript/api/@microsoft/teams-js/media#@microsoft-teams-js-media-selectmedia), [getMedia](/javascript/api/@microsoft/teams-js/media.media#@microsoft-teams-js-media-media-getmedia) и [viewImages](/javascript/api/@microsoft/teams-js/media#@microsoft-teams-js-media-viewimages) API-интерфейсы позволяют использовать собственные мультимедийные возможности следующим образом:

* Используйте **microphone** чтобы разрешить пользователям **запись звука** (запись 10 минут беседы) с устройства.
* Используйте встроенное **управление камерой**, чтобы пользователи могли **снимать и прикреплять изображения** на ходу.
* Используйте встроенную **поддержку галереи**, чтобы пользователи могли **выбирать изображения устройств** в качестве вложений.
* Используйте встроенное **средство просмотра изображений** для одновременного **предварительного просмотра нескольких изображений**.
* Поддержка **передачи больших изображений** (от 1 МБ до 50 МБ) через мост SDK.
* Поддержка **расширенных возможностей изображений** , позволяя пользователям просматривать и редактировать изображения.
* Сканировать документы, доску и визитные карточки с помощью камеры.
  
> [!IMPORTANT]
>
> * API-интерфейсы `selectMedia`, `getMedia`, и `viewImages` можно вызывать из нескольких поверхностей Teams, таких как модули задач, вкладки и личные приложения. Дополнительные сведения см. в [разделе "Точки входа" для приложений Teams](../extensibility-points.md).</br>
> * `selectMedia` API поддерживает как возможности камеры, так и микрофона с помощью различных конфигураций ввода.
> * API `selectMedia` для доступа к возможностям микрофона поддерживается только для мобильных клиентов.

В следующей таблице перечислены наборы API-интерфейсов для включения возможностей мультимедиа устройства:

| API      | Описание   |
| --- | --- |
| [**selectMedia**](/javascript/api/@microsoft/teams-js/media#@microsoft-teams-js-media-selectmedia) (**Камера)**| Этот API позволяет пользователям **захватывать или выбирать мультимедиа с камеры устройства** и возвращать его в веб-приложение. Пользователи могут редактировать, обрезать, поворачивать, комментировать или рисовать поверх изображений перед отправкой. В ответ `selectMedia` веб-приложение получает идентификаторы мультимедиа выбранных изображений и миниатюру выбранного мультимедиа. Этот API можно дополнительно настроить с помощью конфигурации [ImageProps](/javascript/api/@microsoft/teams-js/media.imageprops). |
| [**selectMedia**](/javascript/api/@microsoft/teams-js/media#@microsoft-teams-js-media-selectmedia) (**Микрофон**)| [Задайте для mediaType](/javascript/api/@microsoft/teams-js/media.mediatype) значение `4` (Audio) в `selectMedia` API для доступа к возможности микрофона. Этот API также позволяет пользователям записывать звук с микрофона устройства и возвращать записанные клипы в веб-приложение. Пользователи могут приостанавливать, перезаписывать и предварительно прослушивать записи перед отправкой. В ответ на  **selectMedia** веб-приложение получает идентификаторы мультимедиа выбранной аудиозаписи. <br/> Используйте `maxDuration`, если вам нужно настроить продолжительность записи разговора в минутах. Текущая продолжительность записи составляет 10 минут, после чего запись прекращается.  |
| [**getMedia**](/javascript/api/@microsoft/teams-js/media.media#@microsoft-teams-js-media-media-getmedia)| Этот API извлекает мультимедиа, захваченные API `selectMedia`, по частям, независимо от размера мультимедиа. Эти фрагменты собираются и отправляются обратно в веб-приложение в виде файла или большого двоичного объекта. Разбивка мультимедиа на более мелкие фрагменты облегчает передачу больших файлов. |
| [**viewImages**](/javascript/api/@microsoft/teams-js/media#@microsoft-teams-js-media-viewimages)| Этот API позволяет пользователю просматривать изображения в полноэкранном режиме в виде прокручиваемого списка.|

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

На следующем рисунке показан интерфейс `selectMedia` API веб-приложения для возможностей образа:

:::image type="content" source="~/assets/images/tabs/media-capability-mobile2.png" alt-text="Иллюстрация, на которой показана возможность использования изображения для мобильных устройств.":::

> [!NOTE]
>
> На устройствах с Android версии до 7 `selectMedia` API запускает собственный интерфейс камеры Android, а не собственный интерфейс камеры Teams.

На следующем рисунке показан интерфейс `selectMedia` API веб-приложения для возможности микрофона:

:::image type="content" source="~/assets/images/tabs/microphone-capability.png" alt-text="На рисунке показана возможность микрофона для мобильных устройств.":::

# <a name="desktop"></a>[Компьютер](#tab/desktop)

На следующем рисунке показан интерфейс `selectMedia` API веб-приложения для возможностей образа:

:::image type="content" source="~/assets/images/tabs/media-capability-desktop1.png" alt-text="Иллюстрация, на которой показана возможность мультимедиа для рабочего стола.":::

---

## <a name="error-handling"></a>Обработка ошибок

Убедитесь, что эти ошибки правильно обрабатываются в приложении Teams. В следующей таблице перечислены коды ошибок и описания, в которых создаются ошибки:

|Код ошибки |  Название ошибки     | Описание|
| --------- | --------------- | -------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | API не поддерживается на текущей платформе.|
| **404** | FILE_NOT_FOUND | Указанный файл не найден в указанном расположении.|
| **500** | INTERNAL_ERROR | При выполнении требуемой операции обнаружена внутренняя ошибка.|
| **1000** | PERMISSION_DENIED |Разрешение отклонено пользователем.|
| **3000** | NO_HW_SUPPORT | Оборудование не поддерживает эту возможность.|
| **4000**| INVALID_ARGUMENTS | Один или несколько недопустимых аргументов.|
|  **8000** | USER_ABORT |Пользователь прерывает операцию.|
| **9000**| OLD_PLATFORM | Код платформы устарел и не реализует этот API.|
| **10000**| SIZE_EXCEEDED |  Возвращаемое значение слишком велико и превышает пределы размера платформы.|

## <a name="code-snippets"></a>Фрагменты кода

* API `selectMedia` вызова для записи изображений с помощью камеры:

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

* Вызовите `getMedia` API для получения больших носителей фрагментами:

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

* Вызовите `viewImages` API по идентификатору, который возвращается `selectMedia` API:

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

* Вызов `viewImages` API по URL-адресу:

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

* Вызов и `selectMedia` `getMedia` API-интерфейсы для записи звука через микрофон:

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
* [Интеграция средства "Выбор людей"](people-picker-capability.md)
* [Требования и рекомендации для медиа-ботов, размещаемых в приложениях](~/bots/calls-and-meetings/requirements-considerations-application-hosted-media-bots.md)
