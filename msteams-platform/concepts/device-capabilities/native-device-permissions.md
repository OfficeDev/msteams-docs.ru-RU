---
title: Запрос разрешений устройства для вашего Microsoft Teams приложения
keywords: разрешения возможностей командных приложений
description: Как обновить манифест приложения, чтобы запросить доступ к родным функциям, которые обычно требуют согласия пользователя
localization_priority: Normal
ms.topic: how-to
ms.openlocfilehash: 34f84285dc883cc474cf1720c42b1699f76c6653
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566182"
---
# <a name="request-device-permissions-for-your-microsoft-teams-app"></a>Запрос разрешений устройства для вашего Microsoft Teams приложения

Вы можете обогатить Teams с помощью родных возможностей устройства, таких как камера, микрофон и местоположение. Этот документ поможет вам запросить согласие пользователя и получить доступ к разрешениям на родных устройств.

> [!NOTE]
> * Чтобы интегрировать возможности мультимедиа в Microsoft Teams [](mobile-camera-image-permissions.md)приложении, см.
> * Чтобы интегрировать возможности сканера штрих-кодов в Microsoft Teams [Teams](qr-barcode-scanner-capability.md)мобильное приложение, см.
> * Чтобы интегрировать возможности определения местоположения в [](location-capability.md)Microsoft Teams приложении, см.

## <a name="native-device-permissions"></a>Разрешения на родные устройства

Необходимо запросить разрешение устройства на доступ к возможностям родных устройств. Разрешения устройства работают одинаково для всех конструкций приложений, таких как вкладки, модули задач или расширения обмена сообщениями. Пользователь должен перейти на страницу разрешений в Teams для управления разрешениями устройств.
Доступ к возможностям устройства позволяет создавать более богатые возможности на Teams, например:
* Захват и просмотр изображений.
* Сканирование qR или штрих-кода.
* Запись и доля коротких видео.
* Запись аудио-памяток и сохранить их для более длительного использования.
* Используйте информацию о местоположении пользователя для отображения соответствующей информации.

## <a name="access-device-permissions"></a>Разрешения на доступ к устройствам

Клиент [Microsoft Teams JavaScript SDK предоставляет](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) инструменты, необходимые для вашего Teams мобильного приложения для доступа к [разрешениям устройства пользователя](#manage-permissions) и создания более богатого опыта.

Хотя доступ к этим функциям является стандартным в современных веб-браузерах, вы должны сообщить Teams об особенностях, которые вы используете, обновляя манифест приложения. Это обновление позволяет запрашивать разрешения, пока приложение работает на Teams столе.

> [!NOTE] 
> В настоящее Microsoft Teams поддержка возможностей мультимедиа и возможности сканирования штрих-кодов доступны только для мобильных клиентов.

## <a name="manage-permissions"></a>Управление разрешениями

Пользователь может управлять разрешениями устройств в Teams настройками, выбирая **разрешения Allow** **или Deny** для определенных приложений.
 
# <a name="desktop"></a>[Desktop](#tab/desktop)

1. Откройте приложение Teams для детей.
1. Выберите значок профиля в правом верхнем углу окна.
1. Выберите **Параметры**  >  **разрешения** из выпадают из меню.
1. Выберите нужные настройки.

   ![Экран настроек настольных настроек устройств](../../assets/images/tabs/device-permissions.png)

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

1. Открытый Teams.
1. Перейти **к Параметры** App  >  **Разрешения**.
1. Выберите приложение, для которого необходимо выбрать настройки.
1. Выберите нужные настройки.

    ![Экран разрешений устройства на мобильные настройки](../../assets/images/tabs/MobilePermissions.png)

---

## <a name="specify-permissions"></a>Указать разрешения

Обновите приложение, `manifest.json` добавив и `devicePermissions` указав, какие из пяти свойств, которые вы используете в приложении:

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```

Каждое свойство позволяет побудить пользователя запросить их согласие:

| Свойство      | Описание   |
| --- | --- |
| media         | Разрешение на использование камеры, микрофона, динамиков и медиагалереи доступа. |
| геолокация   | Разрешение на возврат местоположения пользователя.      |
| Уведомления | Разрешение на отправку уведомлений пользователя.      |
| миди          | Разрешение на отправку и получение информации о музыкальном инструменте Digital Interface (MIDI) с цифрового музыкального инструмента.   |
| openExternal  | Разрешение на открытие ссылок во внешних приложениях.  |

## <a name="check-permissions-from-your-app"></a>Проверка разрешений из приложения

После добавления `devicePermissions` в манифест приложения проверьте разрешения с помощью **API разрешений HTML5,** не вызывая подсказки:

``` Javascript
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

## <a name="use-teams-apis-to-get-device-permissions"></a>Используйте Teams API для получения разрешений на устройства

Используйте соответствующие HTML5 Teams API для отображения подсказки для получения согласия на доступ к разрешениям устройства.

> [!IMPORTANT]
> * Поддержка `camera` , и включен через `gallery` `microphone` [**selectMedia API**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true). Используйте [**API captureImage**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) для одного захвата изображения.
> * Поддержка `location` включена через [**GETLocation API**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true). Вы должны использовать это для `getLocation API` определения местоположения, так как HTML5 геолокационный API в настоящее время не полностью поддерживается Teams настольного клиента.

Пример:
 * Чтобы побудить пользователя получить доступ к своему местоположению, необходимо `getCurrentPosition()` позвонить:

    ```Javascript
    navigator.geolocation.getCurrentPosition    (function (position) { /*... */ });
    ```

 * Чтобы побудить пользователя получить доступ к камере на рабочем столе или в Интернете, вы должны `getUserMedia()` позвонить:

    ```Javascript
    navigator.mediaDevices.getUserMedia({ audio: true, video: true });
    ```

 * Чтобы запечатлеть изображение на мобильном телефоне, Teams мобильный телефон запрашивает разрешение при `captureImage()` вызове:

    ```Javascript
    microsoftTeams.media.captureImage((error: microsoftTeams.SdkError, files: microsoftTeams.media.File[]) => {
      /* ... */
    });
    ```

 * Уведомления подскажут пользователю при `requestPermission()` вызове:

    ```Javascript
    Notification.requestPermission(function(result) { /* ... */ });
    ```




* Чтобы использовать камеру или доступ к фотогалерее, Teams мобильный запрашивает разрешение при `selectMedia()` вызове:

    ```JavaScript
    microsoftTeams.media.selectMedia({ maxMediaCount: 10, mediaType: microsoftTeams.media.MediaType.Image }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    );
    ```

* Чтобы использовать микрофон, Teams запрашивает разрешение при `selectMedia()` вызове:

    ```JavaScript 
    microsoftTeams.media.selectMedia({ maxMediaCount: 1, mediaType: microsoftTeams.media.MediaType.Audio }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    });
    ```

* Чтобы побудить пользователя поделиться местоположением на интерфейсе карты, Teams запрашивает разрешение при `getLocation()` вызове:

    ```JavaScript 
    microsoftTeams.location.getLocation({ allowChooseLocation: true, showMap: true }, (error: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
      /* ... *
    /});
    ```
# <a name="desktop"></a>[Desktop](#tab/desktop)

   ![Tabs разрешения настольных устройств подсказка](~/assets/images/tabs/device-permissions-prompt.png)

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

   ![Tabs разрешения мобильных устройств подсказка](../../assets/images/tabs/MobileLocationPermission.png)

* * * 

## <a name="permission-behavior-across-login-sessions"></a>Поведение разрешения во всех сеансах входа

Разрешения устройств хранятся для каждого сеанса входа. Это означает, что если вы войдюете в другой экземпляр Teams, например, на другом компьютере, разрешения на устройство с предыдущих сеансов недоступны. Поэтому необходимо повторно дать согласие на разрешение устройства на новую сессию. Это также означает, что, если вы Teams или переключиться на Teams, разрешения на устройство удаляются из предыдущей сессии входа.  

> [!NOTE]
> При согласии на разрешение на использование родных устройств оно действует только для текущей _сессии_ входа.

## <a name="next-steps"></a>Дальнейшие действия

> [!div class="nextstepaction"]
> [Интеграция медиа-возможностей в Teams](mobile-camera-image-permissions.md)

> [!div class="nextstepaction"]
> [Интеграция возможностей сканера qR или штрих-кодов в Teams](qr-barcode-scanner-capability.md)

> [!div class="nextstepaction"]
> [Интеграция возможностей определения местоположения в Teams](location-capability.md)
