---
title: Запрос разрешений устройства для Microsoft Teams приложения
keywords: 'Возможности приложений Teams, разрешения устройства для собственной проверки qr barcode: аудио видео'
description: Обновление манифеста приложения для запроса доступа к собственным функциям, которые обычно требуют согласия пользователя, таким как сканирование qr, штрихкод, изображение, аудио, возможности видео
ms.localizationpriority: medium
ms.topic: how-to
ms.openlocfilehash: 5269aed130714bc9afbe97b170d955d79d79abc8
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/27/2022
ms.locfileid: "65103308"
---
# <a name="request-device-permissions-for-your-microsoft-teams-app"></a>Запрос разрешений устройства для Microsoft Teams приложения

Вы можете расширить Teams с помощью собственных возможностей устройства, таких как камера, микрофон и расположение. В этом документе описывается, как запросить согласие пользователя и получить доступ к собственным разрешениям устройства.

> [!NOTE]
>
> * Сведения об интеграции возможностей мультимедиа в мобильном Microsoft Teams см. в статье "Интеграция [возможностей мультимедиа"](mobile-camera-image-permissions.md).
> * Сведения об интеграции функции QR или сканера штрихкодов в мобильном приложении Microsoft Teams см. в статье "Интеграция [QR или сканер штрихкодов" в Teams](qr-barcode-scanner-capability.md).
> * Сведения об интеграции возможностей расположения в мобильном Microsoft Teams см. в статье ["Интеграция возможностей расположения"](location-capability.md).

## <a name="native-device-permissions"></a>Разрешения собственного устройства

Необходимо запросить разрешения устройства для доступа к собственным возможностям устройства. Разрешения устройства работают аналогично для всех конструкций приложения, таких как вкладки, модули задач или расширения сообщений. Пользователь должен перейти на страницу разрешений в Teams параметров для управления разрешениями устройства.
Доступ к возможностям устройства позволяет создавать более широкие возможности на платформе Teams, например:

* Захват и просмотр изображений.
* Сканирование QR или штрихкода.
* Записывайте и делитесь короткими видео.
* Запишите звуковые заметки и сохраните их для последующего использования.
* Используйте сведения о расположении пользователя, чтобы отобразить соответствующую информацию.

> [!NOTE]
> * В настоящее время Teams не поддерживает разрешения устройства для многоокневых приложений, вкладок и панели на стороне собрания.
> * Разрешения устройств в браузере отличаются. Дополнительные сведения см. в [разделе о разрешениях устройства браузера](browser-device-permissions.md).

## <a name="access-device-permissions"></a>Доступ к разрешениям устройства

[Клиентский пакет SDK Microsoft Teams JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) предоставляет средства, необходимые Teams мобильному приложению для доступа к разрешениям устройства пользователя и создания [](#manage-permissions) более расширенного интерфейса.

Хотя доступ к этим функциям является стандартным в современных веб-браузерах, необходимо сообщить Teams о функциях, которые вы используете, обновив манифест приложения. Это обновление позволяет запрашивать разрешения во время работы приложения на Teams настольном клиенте.

> [!NOTE]
> Сейчас поддержка Microsoft Teams мультимедиа и сканера штрихкодов QR доступна только для мобильных клиентов.

## <a name="manage-permissions"></a>Управление разрешениями

Пользователь может управлять разрешениями устройства в Teams, выбрав "Разрешить" или "Запретить  разрешения для  определенных приложений".

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

1. Откройте Teams.
1. Перейдите **Параметры** >  **App Permissions**.
1. Выберите приложение, для которого необходимо выбрать параметры.
1. Выберите нужные параметры.

    ![Экран параметров мобильных параметров разрешений устройства](../../assets/images/tabs/MobilePermissions.png)

# <a name="desktop"></a>[Компьютер](#tab/desktop)

1. Откройте Teams приложения.
1. Щелкните значок профиля в правом верхнем углу окна.
1. Выберите **Параметры** >  **Permissions** в раскрывающемся меню.
1. Выберите нужные параметры.

   ![Экран параметров рабочего стола разрешений устройства](~/assets/images/tabs/device-permissions.png)

---

## <a name="specify-permissions"></a>Указание разрешений

Обновите приложение, `manifest.json` добавив `devicePermissions` и указав, какие из следующих пяти свойств вы используете в приложении:

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```

Каждое свойство позволяет запрашивать у пользователя согласие:

| Свойство      | Описание   |
| --- | --- |
| Носителя         | Разрешение на использование камеры, микрофона, динамиков и доступа к коллекции носителей. |
| Географического расположения   | Разрешение на возврат расположения пользователя.      |
| Уведомления | Разрешение на отправку уведомлений пользователя.      |
| Midi          | Разрешение на отправку и получение сведений о цифровом инструменте (MIDI) от цифрового инструмента.   |
| openExternal  | Разрешение на открытие ссылок во внешних приложениях.  |

## <a name="check-permissions-from-your-app"></a>Проверка разрешений из приложения

После добавления `devicePermissions` в манифест приложения проверьте разрешения с помощью **API разрешений HTML5** , не вызывая запрос:

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

## <a name="use-teams-apis-to-get-device-permissions"></a>Использование Teams API для получения разрешений устройства

Используйте соответствующий HTML5 или Teams API, чтобы отобразить запрос на получение согласия на доступ к разрешениям устройства.

> [!IMPORTANT]
>
> * Поддержка и `camera``gallery`включена `microphone` с помощью [**API selectMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true). Используйте [**API captureImage**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) для одной записи изображений.
> * Поддержка включена `location` через [**API getLocation**](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true). Его необходимо использовать для `getLocation API` расположения, так как API геолокации HTML5 в настоящее время не полностью поддерживается Teams настольном клиенте.

Например:

* Чтобы предложить пользователю получить доступ к его расположению, необходимо вызвать:`getCurrentPosition()`

    ```JavaScript
    navigator.geolocation.getCurrentPosition    (function (position) { /*... */ });
    ```

* Чтобы предложить пользователю получить доступ к камере на рабочем столе или в Интернете, необходимо вызвать:`getUserMedia()`

    ```JavaScript
    navigator.mediaDevices.getUserMedia({ audio: true, video: true });
    ```

* Чтобы записать изображение на мобильном устройстве, Teams запрашивает разрешение при вызове`captureImage()`:

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

* При вызове уведомления пользователю будет предложено:`requestPermission()`

    ```JavaScript
    Notification.requestPermission(function(result) { /* ... */ });
    ```

* Чтобы использовать камеру или фотоальбом, Teams мобильный телефон запрашивает разрешение при вызове`selectMedia()`:

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

* Чтобы использовать микрофон, Teams запрашивает разрешение при вызове`selectMedia()`:

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

* Чтобы предложить пользователю предоставить общий доступ к расположению в интерфейсе карты, Teams мобильный телефон запрашивает разрешение при вызове`getLocation()`:

    ```JavaScript
     function getLocation() {
     microsoftTeams.location.getLocation({ allowChooseLocation: true, showMap: true }, (error: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
         let currentLocation = JSON.stringify(location);
     });
     } 
    ```

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

   ![Запрос разрешений для мобильных устройств tabs](../../assets/images/tabs/MobileLocationPermission.png)

# <a name="desktop"></a>[Компьютер](#tab/desktop)

   ![Запрос разрешений для настольных устройств табуляции](~/assets/images/tabs/device-permissions-prompt.png)

---

## <a name="permission-behavior-across-login-sessions"></a>Поведение разрешений в сеансах входа

Разрешения устройства сохраняются для каждого сеанса входа. Это означает, что при входе в другой экземпляр Teams, например на другом компьютере, разрешения устройства из предыдущих сеансов будут недоступны. Поэтому необходимо повторно дать согласие на разрешения устройства для нового сеанса. Это также означает, что при выходе Teams или переключении клиентов в Teams разрешения устройства удаляются из предыдущего сеанса входа.  

> [!NOTE]
> Если вы даете согласие на разрешения собственного устройства, оно допустимо только для _текущего сеанса_ входа.

## <a name="code-sample"></a>Пример кода

| **Название примера** | **Описание** | **Node.js** |
|---------------|--------------|--------|
|Разрешения для устройств | Демонстрация разрешений устройств с помощью примера Microsoft Teams табуляции |  [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-device-permissions/nodejs) |

## <a name="see-also"></a>Дополнительные ресурсы

* [Разрешения устройства для браузера](browser-device-permissions.md)
* [Интеграция возможностей мультимедиа в Teams](mobile-camera-image-permissions.md)
* [Интеграция функции QR или сканера штрихкодов в Teams](qr-barcode-scanner-capability.md)
* [Интеграция функций местонахождения](location-capability.md)
