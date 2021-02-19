---
title: Запрос разрешений устройств для приложения Microsoft Teams
keywords: разрешения командных приложений
description: Обновление манифеста приложения для запроса доступа к родным функциям, которые обычно требуют согласия пользователя
ms.topic: how-to
ms.openlocfilehash: 60c28e1170e8bbdf664145bde7f7de585bd55a45
ms.sourcegitcommit: 6ff8d1244ac386641ebf9401804b8df3854b02dc
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/18/2021
ms.locfileid: "50294749"
---
# <a name="request-device-permissions-for-your-microsoft-teams-app"></a>Запрос разрешений устройств для приложения Microsoft Teams

Вы можете обогатить приложение Teams возможностями родного устройства, например камерой, микрофоном и расположением. В этом документе вы можете узнать, как запрашивать согласие пользователя и получать доступ к разрешениям на родном устройстве.

> [!NOTE]
> * Чтобы интегрировать возможности мультимедиа в мобильном приложении Microsoft Teams, см. в приложении [Integrate media capabilities.](mobile-camera-image-permissions.md)
> * Чтобы интегрировать функции сканера QR или штрихкода в мобильном приложении Microsoft Teams, см. в материале [Интеграция функции QR](qr-barcode-scanner-capability.md) или сканера штрихкодов в Teams

## <a name="native-device-permissions"></a>Разрешения на использование родных устройств

Необходимо запросить разрешения устройства для доступа к возможностям родного устройства. Разрешения устройства работают аналогично для всех конструкций приложений, таких как вкладки, модули задач или расширения обмена сообщениями. Чтобы управлять разрешениями устройств, пользователь должен перейти на страницу разрешений в параметрах Teams.
Доступ к возможностям устройства позволяет создавать более богатые возможности на платформе Teams, например:
* Захват и просмотр изображений.
* Сканирование QR или штрихкода.
* Запись и доля коротких видео.
* Запись аудиозаписей и сохранение их для более позднего использования.
* Используйте сведения о расположении пользователя для отображения соответствующих сведений.

## <a name="access-device-permissions"></a>Разрешения на доступ к устройствам

Клиент [Microsoft Teams JavaScript предоставляет](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) средства, необходимые мобильному приложению Teams [](#manage-permissions) для доступа к разрешениям на устройства пользователя и создания более насыщенного интерфейса.

Хотя доступ к этим функциям является стандартным в современных веб-браузерах, необходимо информировать Teams о свойствах, которые вы используете, обновив манифест приложения. Это обновление позволяет спрашивать разрешения, пока приложение работает на настольном клиенте Teams.

> [!NOTE] 
> В настоящее время поддержка Microsoft Teams возможностей мультимедиа и сканера штрихкодов QR доступна только для мобильных клиентов.

## <a name="manage-permissions"></a>Управление разрешениями

Пользователь может управлять разрешениями устройств в параметрах  Teams, выбрав **разрешить** или запретить разрешения для определенных приложений.
 
# <a name="desktop"></a>[Desktop](#tab/desktop)

1. Откройте приложение Teams.
1. Выберите значок профиля в правом верхнем углу окна.
1. Выберите **Параметры**  >  **Разрешений** из выпадаемого меню.
1. Выберите нужные параметры.

   ![Экран параметров настольных компьютеров разрешений устройств](../../assets/images/tabs/device-permissions.png)

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

1. Open Teams.
1. Перейдите **к настройкам**  >  **разрешений приложения**.
1. Выберите приложение, для которого необходимо выбрать параметры.
1. Выберите нужные параметры.

    ![Экран разрешений мобильных параметров устройства](../../assets/images/tabs/MobilePermissions.png)

---

## <a name="specify-permissions"></a>Указание разрешений

Обновите приложение, добавив и укажите, какие из пяти свойств вы `manifest.json` `devicePermissions` используете в приложении:

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
| media         | Разрешение на использование камеры, микрофона, динамиков и доступа к медиа-галерее. |
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

## <a name="use-teams-apis-to-get-device-permissions"></a>Использование API Teams для получения разрешений на устройства

Используйте соответствующий API HTML5 или Teams, чтобы отобразить подсказку для получения согласия на доступ к разрешениям устройств.

> [!IMPORTANT]
> * Поддержка `camera` , `gallery` и включен через `microphone` [**selectMedia API**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true). Используйте [**API captureImage**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) для одного захвата изображения.
> * Поддержка `location` включена через [**API getLocation.**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) Это необходимо использовать для расположения, так как API геолокации HTML5 в настоящее время не полностью поддерживается `getLocation API` на настольном клиенте Teams.

Например:
 * Чтобы подсказыть пользователю доступ к их расположению, необходимо `getCurrentPosition()` вызвать:

    ```Javascript
    navigator.geolocation.getCurrentPosition    (function (position) { /*... */ });
    ```

 * Чтобы подсказыть пользователю доступ к камере на рабочем столе или в Интернете, необходимо `getUserMedia()` вызвать:

    ```Javascript
    navigator.mediaDevices.getUserMedia({ audio: true, video: true });
    ```

 * Чтобы запечатлеть изображение на мобильных устройствах, мобильный телефон Teams просит разрешения при `captureImage()` вызове:

    ```Javascript
    microsoftTeams.media.captureImage((error: microsoftTeams.SdkError, files: microsoftTeams.media.File[]) => {
      /* ... */
    });
    ```

 * Уведомления подскажут пользователю при `requestPermission()` вызове:

    ```Javascript
    Notification.requestPermission(function(result) { /* ... */ });
    ```




* Чтобы использовать камеру или доступ к фотогалерее, teams mobile просит разрешения при `selectMedia()` вызове:

    ```JavaScript
    microsoftTeams.media.selectMedia({ maxMediaCount: 10, mediaType: microsoftTeams.media.MediaType.Image }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    );
    ```

* Чтобы использовать микрофон, teams mobile запросит разрешение при `selectMedia()` вызове:

    ```JavaScript 
    microsoftTeams.media.selectMedia({ maxMediaCount: 1, mediaType: microsoftTeams.media.MediaType.Audio }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    });
    ```

* Чтобы побудить пользователя к совместному расположению в интерфейсе карты, teams mobile запросит разрешение при `getLocation()` вызове:

    ```JavaScript 
    microsoftTeams.location.getLocation({ allowChooseLocation: true, showMap: true }, (error: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
      /* ... *
    /});
    ```
# <a name="desktop"></a>[Desktop](#tab/desktop)

   ![Запрос разрешений на настольные устройства tabs](~/assets/images/tabs/device-permissions-prompt.png)

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

   ![Запрос разрешений мобильных устройств Tabs](../../assets/images/tabs/MobileLocationPermission.png)

* * * 

## <a name="permission-behavior-across-login-sessions"></a>Поведение разрешений в сеансах входа

Разрешения устройства хранятся для каждого сеанса входа. Это означает, что при входе в другой экземпляр Teams, например, на другом компьютере, разрешения на устройство с предыдущих сеансов недоступны. Поэтому необходимо повторно согласиться на разрешения устройств для нового сеанса. Это также означает, что если вы выходите из Teams или переключате клиентов в Teams, разрешения устройства удаляются из предыдущего сеанса входа.  

> [!NOTE]
> Если вы даете согласие на разрешения на родном устройстве, оно допустимо только для _текущего_ сеанса входа.

## <a name="next-steps"></a>Дальнейшие действия

> [!div class="nextstepaction"]
> [Интеграция возможностей мультимедиа в Teams](mobile-camera-image-permissions.md)

> [!div class="nextstepaction"]
> [Интеграция функций сканера QR или штрихкодов в Teams](qr-barcode-scanner-capability.md)
