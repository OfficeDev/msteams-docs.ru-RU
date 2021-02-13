---
title: Запрос разрешений устройства для приложения Microsoft Teams
keywords: Разрешения на доступ к возможностям приложений Teams
description: Обновление манифеста приложения для запроса доступа к функциям, которые обычно требуют согласия пользователя
ms.topic: how-to
ms.openlocfilehash: 0343754eacbb6088a3e44fa5df8ec90e3b10b076
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231612"
---
# <a name="request-device-permissions-for-your-microsoft-teams-app"></a>Запрос разрешений устройства для приложения Microsoft Teams

Вы можете обогатить свое приложение Teams встроенными возможностями устройства, такими как камера, микрофон и расположение. В этом документе содержится руководство по запросу согласия пользователя и доступу к разрешениям на доступ к устройствам.

> [!NOTE]
> Чтобы интегрировать возможности мультимедиа в мобильном приложении Microsoft Teams, см. ["Интеграция возможностей мультимедиа".](mobile-camera-image-permissions.md)

## <a name="native-device-permissions"></a>Разрешения для нативных устройств

Необходимо запросить разрешения устройства для доступа к возможностям нативных устройств. Разрешения устройства работают аналогично для всех конструкций приложения, таких как вкладки, модули задач или расширения обмена сообщениями. Чтобы управлять разрешениями устройств, пользователь должен перейти на страницу разрешений в параметрах Teams.
Доступ к возможностям устройств позволяет создавать на платформе Teams более богатые возможности, например:
* Захват и просмотр изображений.
* Записывать короткие видеоролики и делиться ими.
* Зафиксировать звуковые memos и сохранить их для использования в дальнейшем.
* Используйте сведения о расположении пользователя для отображения соответствующей информации.

## <a name="access-device-permissions"></a>Доступ к разрешениям устройства

Клиентский [SDK JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) для Microsoft Teams предоставляет средства, необходимые [](#manage-permissions) мобильному приложению Teams для доступа к разрешениям устройства пользователя и создания более удобного интерфейса.

Хотя доступ к этим функциям является стандартным в современных веб-браузерах, необходимо сообщить Teams о функции, которые вы используете, обновив манифест приложения. Это обновление позволяет запросить разрешения, пока приложение работает в настольном клиенте Teams.

> [!NOTE] 
> В настоящее время поддержка возможностей мультимедиа в Microsoft Teams доступна только для мобильных клиентов.

## <a name="manage-permissions"></a>Управление разрешениями

Пользователь может управлять разрешениями устройств в параметрах  Teams, выбирая разрешения "Разрешить" или "Запретить" для определенных приложений. 
 
# <a name="desktop"></a>[Desktop](#tab/desktop)

1. Откройте приложение Teams.
1. Выберите значок профиля в правом верхнем углу окна.
1. Выберите **"Разрешения**  >  **параметров"** в выпадаемом меню.
1. Выберите нужные параметры.

   ![Экран параметров рабочего стола для разрешений устройства](../../assets/images/tabs/device-permissions.png)

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

1. Откройте Teams.
1. Go to **Settings**  >  **App Permissions**.
1. Выберите приложение, для которого необходимо выбрать параметры.
1. Выберите нужные параметры.

    ![Экран разрешений устройства для мобильных устройств](../../assets/images/tabs/MobilePermissions.png)

---

## <a name="specify-permissions"></a>Указание разрешений

Обновите приложение, добавив и указав, какие из пяти свойств `manifest.json` `devicePermissions` вы используете в приложении:

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```

Каждое свойство позволяет попросить пользователя запросить свое согласие:

| Свойство      | Описание   |
| --- | --- |
| media         | Разрешение на использование камеры, микрофона, динамиков и доступа к коллекции мультимедиа. |
| geolocation   | Разрешение на возврат расположения пользователя.      |
| notifications | Разрешение на отправку уведомлений пользователя.      |
| midi          | Разрешение на отправку и получение сведений о цифровом интерфейсе музыкального инструмента (MIDI) от цифрового музыкального инструмента.   |
| openExternal  | Разрешение на открытие ссылок во внешних приложениях.  |

## <a name="check-permissions-from-your-app"></a>Проверка разрешений из приложения

После добавления в манифест приложения проверьте разрешения с помощью API разрешений `devicePermissions` **HTML5** без запроса:

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

## <a name="use-teams-apis-to-get-device-permissions"></a>Использование API Teams для получения разрешений устройства

Используйте соответствующий API HTML5 или Teams, чтобы отобразить запрос на получение согласия на доступ к разрешениям устройства.

> [!IMPORTANT]
> * Поддержка `camera` , `gallery` и `microphone` включена через [**selectMedia API**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true). Используйте [**API captureImage**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) для одного захвата изображения.
> * Поддержка `location` включена через [**API getLocation.**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) Его необходимо использовать для определения местоположения, так как API географического расположения HTML5 в настоящее время не полностью поддерживается в настольном клиенте `getLocation API` Teams.

Например,
 * Чтобы у пользователя был доступ к его расположению, необходимо `getCurrentPosition()` вызвать:

    ```Javascript
    navigator.geolocation.getCurrentPosition    (function (position) { /*... */ });
    ```

 * Чтобы у пользователя был доступ к камере на рабочем столе или в Интернете, необходимо `getUserMedia()` вызвать:

    ```Javascript
    navigator.mediaDevices.getUserMedia({ audio: true, video: true });
    ```

 * Чтобы захватить изображение на мобильном устройстве, teams mobile запросит разрешение при `captureImage()` вызове:

    ```Javascript
    microsoftTeams.media.captureImage((error: microsoftTeams.SdkError, files: microsoftTeams.media.File[]) => {
      /* ... */
    });
    ```

 * При вызове уведомлений пользователю будет `requestPermission()` предложено:

    ```Javascript
    Notification.requestPermission(function(result) { /* ... */ });
    ```




* Чтобы использовать камеру или доступ к фотоальбому, Приложение Teams mobile запросит разрешение при `selectMedia()` вызове:

    ```JavaScript
    microsoftTeams.media.selectMedia({ maxMediaCount: 10, mediaType: microsoftTeams.media.MediaType.Image }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    );
    ```

* Чтобы использовать микрофон, Мобильный телефон Teams запросит разрешение при `selectMedia()` вызове:

    ```JavaScript 
    microsoftTeams.media.selectMedia({ maxMediaCount: 1, mediaType: microsoftTeams.media.MediaType.Audio }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    });
    ```

* Чтобы попросить пользователя поделиться данными о расположении в интерфейсе карты, Приложение Teams Mobile запросит разрешение при `getLocation()` вызове:

    ```JavaScript 
    microsoftTeams.location.getLocation({ allowChooseLocation: true, showMap: true }, (error: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
      /* ... *
    /});
    ```
# <a name="desktop"></a>[Desktop](#tab/desktop)

   ![Запрос разрешений для настольных устройств на вкладке](~/assets/images/tabs/device-permissions-prompt.png)

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

   ![Запрос разрешений мобильного устройства "Вкладки"](../../assets/images/tabs/MobileLocationPermission.png)

* * * 

## <a name="permission-behavior-across-login-sessions"></a>Поведение разрешений в сеансах входа

Разрешения устройства сохраняются для каждого сеанса входа. Это означает, что при входе в другой экземпляр Teams, например, на другом компьютере, разрешения устройства из предыдущих сеансов будут недоступны. Поэтому необходимо повторно согласиться на использование разрешений устройства для нового сеанса. Это также означает, что при выходе из Teams или переключении клиентов в Teams разрешения устройств удаляются из предыдущего сеанса входа.  

> [!NOTE]
> Если вы даете согласие на доступ к нативным разрешениям устройства, это допустимо только для _текущего сеанса_ входа.

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Интеграция возможностей мультимедиа в Teams](mobile-camera-image-permissions.md)
