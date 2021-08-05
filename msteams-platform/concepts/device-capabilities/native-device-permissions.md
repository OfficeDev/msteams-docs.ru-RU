---
title: Запрос разрешений на устройство для Microsoft Teams приложения
keywords: разрешения командных приложений
description: Обновление манифеста приложения для запроса доступа к родным функциям, которые обычно требуют согласия пользователя
localization_priority: Normal
ms.topic: how-to
ms.openlocfilehash: 420b874770a4ad506dbedd575600f333a51ad5c0
ms.sourcegitcommit: ec79bbbc3a8daa1ad96de809fc6d17367e8f0c6b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/04/2021
ms.locfileid: "53726952"
---
# <a name="request-device-permissions-for-your-microsoft-teams-app"></a>Запрос разрешений на устройство для Microsoft Teams приложения

Вы можете обогатить Teams с помощью родных возможностей устройства, таких как камера, микрофон и расположение. В этом документе вы можете узнать, как запрашивать согласие пользователя и получать доступ к разрешениям на родных устройствах.

> [!NOTE]
> * Чтобы интегрировать возможности мультимедиа в Microsoft Teams мобильном приложении, см. в приложении [Integrate media capabilities.](mobile-camera-image-permissions.md)
> * Чтобы интегрировать функцию сканера [QR](qr-barcode-scanner-capability.md)или штрихкода в мобильном приложении Microsoft Teams см. в Teams.
> * Чтобы интегрировать возможности расположения в Microsoft Teams мобильном приложении, см. в [приложении Integrate location capabilities.](location-capability.md)
> * Чтобы интегрировать возможности выборщика людей в Microsoft Teams мобильном приложении, см. в [Teams.](people-picker-capability.md)

## <a name="native-device-permissions"></a>Разрешения на использование родных устройств

Необходимо запросить разрешения устройства для доступа к возможностям родного устройства. Разрешения устройства работают аналогично для всех конструкций приложений, таких как вкладки, модули задач или расширения обмена сообщениями. Пользователь должен перейти на страницу разрешений в Teams параметров для управления разрешениями устройств.
Доступ к возможностям устройства позволяет создавать более богатые возможности на платформе Teams, например:
* Захват и просмотр изображений.
* Сканирование QR или штрихкода.
* Запись и доля коротких видео.
* Запись аудиозаписей и сохранение их для более позднего использования.
* Используйте сведения о расположении пользователя для отображения соответствующих сведений.

> [!NOTE]
> В настоящее время Teams не поддерживает разрешения устройств для нескольких оконных приложений, вкладок и sidepanel собраний. 

## <a name="access-device-permissions"></a>Разрешения на доступ к устройствам

Клиент [Microsoft Teams JavaScript SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) предоставляет средства, необходимые Teams мобильному приложению для [](#manage-permissions) доступа к разрешениям устройств пользователя и создания более насыщенного интерфейса.

Хотя доступ к этим функциям является стандартным в современных веб-браузерах, необходимо информировать Teams о свойствах, которые вы используете, обновив манифест приложения. Это обновление позволяет спрашивать разрешения, пока приложение работает на Teams настольном клиенте.

> [!NOTE] 
> В настоящее время Microsoft Teams средства массовой информации и возможности сканера штрихкодов QR доступны только для мобильных клиентов.

## <a name="manage-permissions"></a>Управление разрешениями

Пользователь может управлять разрешениями устройств в Teams параметров,  выбрав **разрешить** или запретить разрешения для определенных приложений.
 
# <a name="desktop"></a>[Классическая версия](#tab/desktop)

1. Откройте приложение Teams.
1. Выберите значок профиля в правом верхнем углу окна.
1. Выберите **Параметры**  >  **разрешений** из выпадаемого меню.
1. Выберите нужные параметры.

   ![Экран параметров настольных компьютеров разрешений устройств](../../assets/images/tabs/device-permissions.png)

# <a name="mobile"></a>[Мобильная версия](#tab/mobile)

1. Откройте Teams.
1. Перейдите **Параметры**  >  **разрешения на приложения.**
1. Выберите приложение, для которого необходимо выбрать параметры.
1. Выберите нужные параметры.

    ![Экран разрешений мобильных параметров устройства](../../assets/images/tabs/MobilePermissions.png)

---

## <a name="specify-permissions"></a>Указание разрешений

Обновите приложение, добавив и укажите, какие из следующих пяти свойств вы `manifest.json` `devicePermissions` используете в приложении:

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```

Каждое свойство позволяет задать пользователю запрос на его согласие:

| Свойство      | Описание   |
| --- | --- |
| мультимедиа         | Разрешение на использование камеры, микрофона, динамиков и доступа к медиа-галерее. |
| геолокация   | Разрешение на возвращение расположения пользователя.      |
| уведомления | Разрешение на отправку уведомлений пользователя.      |
| midi          | Разрешение на отправку и получение сведений о цифровом интерфейсе музыкальных инструментов (MIDI) с цифрового музыкального инструмента.   |
| openExternal  | Разрешение на открытие ссылок во внешних приложениях.  |

## <a name="check-permissions-from-your-app"></a>Проверка разрешений из приложения

После добавления в манифест приложения проверьте разрешения с помощью `devicePermissions` **API разрешений HTML5** без запроса:

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

Используйте соответствующие HTML5 или Teams API, чтобы отобразить подсказку для получения согласия на доступ к разрешениям устройств.

> [!IMPORTANT]
> * Поддержка `camera` , `gallery` и включен через `microphone` [**selectMedia API**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true). Используйте [**API captureImage**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) для одного захвата изображения.
> * Поддержка `location` включена через [**API getLocation.**](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) Это необходимо использовать для расположения, так как API геолокации HTML5 в настоящее время не полностью поддерживается на `getLocation API` Teams настольном клиенте.

Примеры:
 * Чтобы подсказыть пользователю доступ к их расположению, необходимо `getCurrentPosition()` вызвать:

    ```Javascript
    navigator.geolocation.getCurrentPosition    (function (position) { /*... */ });
    ```

 * Чтобы подсказыть пользователю доступ к камере на рабочем столе или в Интернете, необходимо `getUserMedia()` вызвать:

    ```Javascript
    navigator.mediaDevices.getUserMedia({ audio: true, video: true });
    ```

 * Чтобы захватить изображение на мобильном телефоне, Teams мобильный просит разрешения при `captureImage()` вызове:

    ```Javascript
    microsoftTeams.media.captureImage((error: microsoftTeams.SdkError, files: microsoftTeams.media.File[]) => {
      /* ... */
    });
    ```

 * Уведомления подскажут пользователю при `requestPermission()` вызове:

    ```Javascript
    Notification.requestPermission(function(result) { /* ... */ });
    ```




* Чтобы использовать камеру или доступ к фотогалерее, Teams мобильный просит разрешения при `selectMedia()` вызове:

    ```JavaScript
    microsoftTeams.media.selectMedia({ maxMediaCount: 10, mediaType: microsoftTeams.media.MediaType.Image }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    );
    ```

* Чтобы использовать микрофон, Teams мобильный спрашивает разрешения при `selectMedia()` вызове:

    ```JavaScript 
    microsoftTeams.media.selectMedia({ maxMediaCount: 1, mediaType: microsoftTeams.media.MediaType.Audio }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    });
    ```

* Чтобы побудить пользователя к совместному расположению в интерфейсе карты, Teams мобильный просит разрешения при `getLocation()` вызове:

    ```JavaScript 
    microsoftTeams.location.getLocation({ allowChooseLocation: true, showMap: true }, (error: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
      /* ... *
    /});
    ```
# <a name="desktop"></a>[Классическая версия](#tab/desktop)

   ![Запрос разрешений на настольные устройства tabs](~/assets/images/tabs/device-permissions-prompt.png)

# <a name="mobile"></a>[Мобильная версия](#tab/mobile)

   ![Запрос разрешений мобильных устройств Tabs](../../assets/images/tabs/MobileLocationPermission.png)

* * * 

## <a name="permission-behavior-across-login-sessions"></a>Поведение разрешений в сеансах входа

Разрешения устройства хранятся для каждого сеанса входа. Это означает, что при входе в другой экземпляр Teams, например, на другом компьютере, разрешения на устройство с предыдущих сеансов недоступны. Поэтому необходимо повторно согласиться на разрешения устройств для нового сеанса. Это также означает, что если вы Teams или переключите клиентов в Teams, разрешения устройства удаляются из предыдущего сеанса входа.  

> [!NOTE]
> Если вы даете согласие на разрешения на родном устройстве, оно допустимо только для _текущего_ сеанса входа.

## <a name="code-sample"></a>Пример кода

| **Имя образца** | **Описание** | **Node.js** |
|---------------|--------------|--------|
|Разрешения для устройств | Используйте Microsoft Teams пример вкладки для демонстрации разрешений устройств |  [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-device-permissions/nodejs) |

## <a name="next-steps"></a>Дальнейшие действия

> [!div class="nextstepaction"]
> [Интеграция возможностей мультимедиа в Teams](mobile-camera-image-permissions.md)

> [!div class="nextstepaction"]
> [Интеграция возможностей сканера QR или штрихкодов в Teams](qr-barcode-scanner-capability.md)

> [!div class="nextstepaction"]
> [Интеграция возможностей расположения в Teams](location-capability.md)

> [!div class="nextstepaction"]
> [Интеграция возможностей выборщика людей в Teams](people-picker-capability.md)
