---
title: Запрос разрешений устройства для вкладки Microsoft Teams
description: Обновление манифеста приложения для запроса доступа к функциям, которые обычно требуют согласия пользователя
keywords: Разработка вкладок teams
ms.openlocfilehash: 6be183d2610616f3bd3bdf32554976322193c132
ms.sourcegitcommit: d0e71ea63af2f67eba75ba283ec46cc7cdf87d75
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/24/2020
ms.locfileid: "49731981"
---
# <a name="request-device-permissions-for-your-microsoft-teams-tab"></a>Запрос разрешений устройства для вкладки Microsoft Teams

Возможно, вы захотите расширить вкладку функциями, которые требуют доступа к функциям нативных устройств, например:

> [!div class="checklist"]
>
> * Камера
> * Микрофон
> * Расположение
> * Уведомления

[!Note] Чтобы интегрировать возможности камеры и изображений в мобильном приложении Microsoft Teams, обратитесь к возможностям камеры и [изображений в Teams.](../../concepts/device-capabilities/mobile-camera-image-permissions.md)

> [!IMPORTANT]
>
> * В настоящее время мобильный клиент Teams поддерживает только доступ к возможностям , и через возможности нативных устройств и доступен во всех конструкциях приложения, включая `camera` `gallery` `mic` `location` вкладки. </br>
> * Поддержка `camera` , `gallery` и `mic` включена через [**selectMedia API**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true). Для одного захвата изображения можно использовать [**API captureImage.**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true)
> * Поддержка `location` включена с помощью [**API getLocation.**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) Рекомендуется использовать этот API, так как [**API**](../../resources/schema/manifest-schema.md#devicepermissions) географического местонахождения в настоящее время не полностью поддерживается на всех классических клиентах.

## <a name="device-permissions"></a>Разрешения для устройств

Доступ к разрешениям устройства пользователя позволяет создавать гораздо более богатые возможности, например:

* Запись и совместное видео
* Зафиксировать короткие звуковые memo и сохранить их для более поздней 2016 г.
* Использование сведений о расположении пользователей для отображения соответствующей информации

Хотя доступ к этим функциям является стандартным в большинстве современных веб-браузеров, необходимо дать Teams знать, какие функции вы хотите использовать, обновив манифест приложения. Это позволит вам запросить разрешения так же, как в браузере, когда ваше приложение работает в настольном клиенте Teams.

## <a name="manage-permissions"></a>Управление разрешениями

# <a name="desktop"></a>[Desktop](#tab/desktop)

1. Откройте Teams.
1. В правом верхнем углу окна выберите значок профиля.
1. Выберите **"Разрешения**  ->  **параметров"** в выпадаемом меню.
1. Выберите нужные параметры.

![Экран параметров рабочего стола для разрешений устройства](../../assets/images/tabs/device-permissions.png)

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

1. Откройте Teams.
1. Go to **Settings**  ->  **App Permissions**.
1. Выберите приложение, для которое нужно выбрать параметры.
1. Выберите нужные параметры.

![Экран разрешений устройства для мобильных устройств](../../assets/images/tabs/MobilePermissions.png)

---

## <a name="properties"></a>Свойства

Обновите приложение, добавив и указав, какое из пяти свойств вы хотите `manifest.json` `devicePermissions` использовать в приложении:

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```
> [!Note]
>
> Мультимедиа также используется для разрешений камеры на мобильных устройствах.

Каждое свойство позволит вам попросить пользователя запросить свое согласие:

| Свойство      | Описание   |
| --- | --- |
| media         | разрешение на использование камеры, микрофона, динамиков и галереи мультимедиа |
| geolocation   | разрешение на возврат расположения пользователя      |
| notifications | разрешение на отправку уведомлений пользователя      |
| midi          | разрешение на отправку и получение сведений midi от цифрового музыкального инструмента   |
| openExternal  | разрешение на открытие ссылок во внешних приложениях  |

## <a name="checking-permissions-from-your-tab"></a>Проверка разрешений на вкладке

После того как вы добавите в манифест приложения, вы можете проверить разрешения с помощью `devicePermissions` API "разрешений" HTML5 без запроса.

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

## <a name="prompting-the-user"></a>Запрос пользователя

Чтобы показать запрос на согласие на доступ к разрешениям устройства, необходимо использовать соответствующий API HTML5 или Teams. 

Например, чтобы у пользователя получить доступ к его расположению, необходимо `getCurrentPosition` вызвать:

```Javascript
navigator.geolocation.getCurrentPosition(function (position) { /*... */ });
```

Чтобы использовать камеру на настольном компьютере или в Интернете, Teams будет показывать запрос на разрешение при `getUserMedia` вызове:

```Javascript
navigator.mediaDevices.getUserMedia({ audio: true, video: true });
```

Чтобы захватить изображение на мобильных устройствах, Teams Mobile запросит разрешение при `captureImage()` вызове:

```Javascript
microsoftTeams.media.captureImage((error: microsoftTeams.SdkError, files: microsoftTeams.media.File[]) => {
  /* ... */
});
```

При вызове уведомлений пользователю будет `requestPermission` предложено:

```Javascript
Notification.requestPermission(function(result) { /* ... */ });
```

Чтобы использовать камеру или доступ к фотоальбому, Teams Mobile запросит разрешение при `selectMedia()` вызове:

```JavaScript
microsoftTeams.media.selectMedia({ maxMediaCount: 10, mediaType: microsoftTeams.media.MediaType.Image }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
  /* ... */
});
```

Чтобы использовать микрофон, Teams Mobile запросит разрешение при `selectMedia()` вызове:

```JavaScript 
microsoftTeams.media.selectMedia({ maxMediaCount: 1, mediaType: microsoftTeams.media.MediaType.Audio }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
  /* ... */
});
```

Чтобы попросить пользователя поделиться расположением в интерфейсе карты, Приложение Teams Mobile запросит разрешение при `getLocation()` вызове:

```JavaScript 
microsoftTeams.location.getLocation({ allowChooseLocation: true, showMap: true }, (error: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
  /* ... *
/});
```

# <a name="desktop"></a>[Desktop](#tab/desktop)

![Запрос разрешений для настольных устройств на вкладке](~/assets/images/tabs/device-permissions-prompt.png)

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

![Запрос разрешений мобильного устройства "Вкладки"](../../assets/images/tabs/MobileLocationPermission.png)


## <a name="permission-behavior-across-login-sessions"></a>Поведение разрешений в сеансах входа

Разрешения для устройств сохраняются для каждого сеанса входа. Это означает, что при входе в другой экземпляр Teams (например, на другом компьютере) разрешения устройства из предыдущих сеансов будут недоступны. Вместо этого вам потребуется повторно согласиться на использование разрешений устройства для нового сеанса входа. Это также означает, что при выходе из Teams (или переключении клиентов в Teams) разрешения устройства будут удалены для предыдущего сеанса входа. Помните об этом при разработке нативных разрешений для устройств: те же возможности, которые вы даете согласие, будут только для _текущего_ сеанса входа в систему.
