---
title: Запрос разрешений устройства для приложения Microsoft Teams
keywords: возможности приложений Teams разрешения устройства встроенный сканер QR-кодов штрихкод изображение аудио видео
description: Обновление манифеста приложения для запроса доступа к функциям, которые обычно требуют согласия пользователя, таким как сканирование QR-кода, штрихкода, а также возможности работы с изображениями, звуком и видео
ms.localizationpriority: high
ms.topic: how-to
ms.openlocfilehash: cccf527c3abf3a1674b2d1350dd15633ba35c7a8
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111964"
---
# <a name="request-device-permissions-for-your-microsoft-teams-app"></a>Запрос разрешений устройства для приложения Microsoft Teams

Вы можете сделать приложение Teams более функциональным с помощью встроенных возможностей устройства, таких как камера, микрофон и расположение. В этом документе представлена инструкция о том, как запросить согласие пользователя и получить доступ к встроенным разрешениям устройства.

> [!NOTE]
>
> * Чтобы интегрировать возможности мультимедиа в мобильном приложении Microsoft Teams, см. статью [Интеграция возможностей мультимедиа](mobile-camera-image-permissions.md).
> * Чтобы интегрировать сканер QR-кода или штрихкодов в мобильном приложении Microsoft Teams, см. статью [Интеграция функции сканирования QR- или штрихкода](qr-barcode-scanner-capability.md).
> * Чтобы интегрировать возможности определения местоположения в мобильном приложении Microsoft Teams, см. статью [Интеграция возможностей расположения](location-capability.md).

## <a name="native-device-permissions"></a>Встроенные разрешения устройств

Для доступа к возможностям устройств необходимо запросить разрешения устройства. Разрешения устройства работают аналогично для всех конструкций приложений, таких как вкладки, модули задач или расширения для сообщений. Чтобы управлять разрешениями устройств, пользователь должен перейти на страницу разрешений в параметрах Teams.
Доступ к возможностям устройства позволяет создавать более эффективные возможности на платформе Teams, например следующие.

* Захват и просмотр изображений.
* Сканирование QR-кодов или штрихкодов.
* Запись и отправление коротких видео.
* Запись звуковых заметок и сохранение их для дальнейшего использования.
* Использование сведений о расположении пользователя для отображения соответствующей информации.

> [!NOTE]
> * Сейчас Teams не поддерживает разрешения устройств для многооконных приложений, вкладок и боковой панели собрания.
> * Разрешения устройства отличаются в браузере. Подробнее см. в разделе [Разрешения устройств в браузере](browser-device-permissions.md).

## <a name="access-device-permissions"></a>Доступ к разрешениям для устройств

[SDK клиента Microsoft Teams JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) предоставляет средства, необходимые мобильному приложению Teams для доступа к [разрешениям устройства](#manage-permissions) и более эффективного взаимодействия.

Хотя доступ к этим функциям является стандартным в современных веб-браузерах, необходимо сообщить Teams о функциях, которые вы используете, обновив манифест приложения. Это обновление позволяет запрашивать разрешения во время работы приложения в настольных клиентах Teams.

> [!NOTE]
> В настоящее время поддержка Microsoft Teams для возможностей мультимедиа и сканера QR-кодов или штрихкодов доступна только для мобильных клиентов.

## <a name="manage-permissions"></a>Управление разрешениями

Пользователь может управлять разрешениями устройств в параметрах Teams, выбрав параметры разрешений **Разрешить** или **Запретить** для определенных приложений.

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

1. Откройте Teams.
1. Перейдите в **Параметры** > **Разрешения приложений**.
1. Выберите приложение, для которого необходимо выбрать параметры.
1. Выберите нужные параметры.

    ![Экран параметров мобильного устройства с разрешениями устройства](../../assets/images/tabs/MobilePermissions.png)

# <a name="desktop"></a>[Компьютер](#tab/desktop)

1. Откройте приложение Teams
1. Выберите значок профиля в правом верхнем углу окна.
1. Выберите **Параметры** > **Разрешения** в раскрывающемся меню.
1. Выберите нужные параметры.

   ![Экран параметров настольного приложения с разрешениями устройства](~/assets/images/tabs/device-permissions.png)

---

## <a name="specify-permissions"></a>Назначение разрешений

Обновите `manifest.json` приложения, добавив `devicePermissions` и указав, какие из следующих пяти свойств вы используете в приложении.

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```

Каждое свойство позволяет попросить пользователя запросить согласие.

| Свойство      | Описание   |
| --- | --- |
| мультимедиа         | Разрешение на использование камеры, микрофона, динамиков и доступа к коллекции мультимедиа. |
| географическое положение   | Разрешение на получение координат пользователя.      |
| уведомления | Разрешение на отправку уведомлений пользователей.      |
| midi          | Разрешение на отправку и получение данных цифрового интерфейса музыкальных инструментов (MIDI) от цифрового музыкального инструмента   |
| openExternal  | Разрешение на открытие ссылок во внешних приложениях.  |

## <a name="check-permissions-from-your-app"></a>Проверка разрешений из приложения

После добавления `devicePermissions` в манифест приложения проверьте разрешения с помощью **API разрешений HTML5** без запроса:

``` JavaScript
// Different query options:
navigator.permissions.query({ name: 'camera' });
navigator.permissions.query({ name: 'microphone' });
navigator.permissions.query({ name: 'geolocation' });
navigator.permissions.query({ name: 'notifications' });
navigator.permissions.query({ name: 'midi', sysex: true });

// Example:
navigator.permissions.query({name:'geolocation'}).then(function(result) {
  if (result.state == 'granted') {
    // Access granted
  } else if (result.state == 'prompt') {
    // Access has not been granted
  }
});
```

## <a name="use-teams-apis-to-get-device-permissions"></a>Использование API Teams для получения разрешений устройства

Используйте соответствующий API HTML5 или Teams, чтобы отобразить запрос на получение согласия на доступ к разрешениям устройства.

> [!IMPORTANT]
>
> * Поддержка `camera`, `gallery`, и `microphone` включается через [**API selectMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true). Используйте [**API captureImage**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) для одного захвата изображения.
> * Поддержка `location` включается через [**API getLocation**](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true). Этот `getLocation API` следует использовать для определения местоположения, так как API географического расположения HTML5 в настоящее время не полностью поддерживается в настольном клиенте Teams.

Например:

* Чтобы пользователь мог получить доступ к его местоположению, необходимо вызвать `getCurrentPosition()`:

    ```JavaScript
    navigator.geolocation.getCurrentPosition    (function (position) { /*... */ });
    ```

* Чтобы пользователь мог получить доступ к камере на рабочем столе или в Интернете, необходимо вызвать `getUserMedia()`:

    ```JavaScript
    navigator.mediaDevices.getUserMedia({ audio: true, video: true });
    ```

* Чтобы захватить изображение на мобильном устройстве, Teams для мобильных устройств запрашивает разрешение при вызове `captureImage()`:

    ```JavaScript
            function captureImage() {
            microsoftTeams.media.captureImage((error, files) => {
                // If there's any error, an alert shows the error message/code
                if (error) {
                    if (error.message) {
                        alert(" ErrorCode: " + error.errorCode + error.message);
                    } else {
                        alert(" ErrorCode: " + error.errorCode);
                    }
                } else if (files) {
                    image = files[0].content;
                    // Adding this image string in src attr of image tag will display the image on web page.
                    let imageString = "data:" + item.mimeType + ";base64," + image;
                }
            });
        } 
    ```

* При вызове `requestPermission()` пользователю будут отображены уведомления:

    ```JavaScript
    Notification.requestPermission(function(result) { /* ... */ });
    ```

* Чтобы использовать камеру или доступ к фотоальбому, Teams для мобильных устройств запрашивает разрешение при вызове `selectMedia()`:

    ```JavaScript
     function selectMedia() {
     microsoftTeams.media.selectMedia(mediaInput, (error, attachments) => {
         // If there's any error, an alert shows the error message/code
         if (error) {
             if (error.message) {
                 alert(" ErrorCode: " + error.errorCode + error.message);
             } else {
                 alert(" ErrorCode: " + error.errorCode);
             }
         } else if (attachments) {
             // creating image array which contains image string for all attached images. 
             const imageArray = attachments.map((item, index) => {
                 return ("data:" + item.mimeType + ";base64," + item.preview)
             })
         }
     });
    } 
  ```

* Чтобы использовать микрофон, Teams для мобильных устройств запрашивает разрешение при вызове `selectMedia()`:

    ```JavaScript
     function selectMedia() {
     microsoftTeams.media.selectMedia({ maxMediaCount: 1, mediaType: microsoftTeams.media.MediaType.Audio }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
         // If there's any error, an alert shows the error message/code
         if (error) {
             if (error.message) {
                 alert(" ErrorCode: " + error.errorCode + error.message);
             } else {
                 alert(" ErrorCode: " + error.errorCode);
             }
         }

         if (attachments) {
             // taking the first attachment  
             let audioResult = attachments[0];

             // setting audio string which can be used in Video tag
             let audioData = "data:" + audioResult.mimeType + ";base64," + audioResult.preview
         }
     });
     }
    ```

* Чтобы попросить пользователя поделиться местоположением в интерфейсе карты, Teams для мобильных устройств запрашивает разрешение при вызове `getLocation()`:

    ```JavaScript
     function getLocation() {
     microsoftTeams.location.getLocation({ allowChooseLocation: true, showMap: true }, (error: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
         let currentLocation = JSON.stringify(location);
     });
     } 
    ```

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

   ![Запрос разрешений мобильного устройства для вкладок](../../assets/images/tabs/MobileLocationPermission.png)

# <a name="desktop"></a>[Компьютер](#tab/desktop)

   ![Запрос разрешений настольного устройства для вкладок](~/assets/images/tabs/device-permissions-prompt.png)

---

## <a name="permission-behavior-across-login-sessions"></a>Поведение разрешений в сеансах входа

Разрешения устройства сохраняются для каждого сеанса входа. Это означает, что при входе в другой экземпляр Teams, например на другом компьютере, разрешения вашего устройства из предыдущих сеансов будут недоступны. Таким образом, необходимо повторно согласиться на разрешения устройства для нового сеанса. Это также означает, что при выходе из Teams или смене клиента в Teams разрешения устройства удаляются из предыдущего сеанса входа.  

> [!NOTE]
> Если вы даете согласие на разрешения для устройства, оно действует только для _текущего_ сеанса входа.

## <a name="code-sample"></a>Пример кода

| **Название примера** | **Описание** | **Node.js** |
|---------------|--------------|--------|
|Разрешения для устройств | Используйте образец приложения на вкладке Microsoft Teams для демонстрации разрешений устройства |  [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-device-permissions/nodejs) |

## <a name="see-also"></a>Дополнительные ресурсы

* [Разрешения устройства для браузера](browser-device-permissions.md)
* [Интеграция возможностей мультимедиа в Teams](mobile-camera-image-permissions.md)
* [Интеграция функции сканирования QR-кода или штрихкода в Teams](qr-barcode-scanner-capability.md)
* [Интеграция функций местонахождения](location-capability.md)
