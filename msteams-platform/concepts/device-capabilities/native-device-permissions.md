---
title: Запрос разрешений устройства для вкладки
description: Обновление манифеста приложения для запроса доступа к функциям, которые обычно требуют согласия пользователя
ms.topic: how-to
keywords: Разработка вкладок teams
ms.openlocfilehash: a2893fb2905584eac4b398287d431f406c23b12b
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014532"
---
# <a name="request-device-permissions-for-your-microsoft-teams-tab"></a><span data-ttu-id="1cdde-104">Запрос разрешений устройства для вкладки Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="1cdde-104">Request device permissions for your Microsoft Teams tab</span></span>

<span data-ttu-id="1cdde-105">Возможно, вы захотите расширить вкладку с помощью функций, которые требуют доступа к функциям нативных устройств, например:</span><span class="sxs-lookup"><span data-stu-id="1cdde-105">You might want to enrich your tab with features that require access to native device functionality like:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="1cdde-106">Камера</span><span class="sxs-lookup"><span data-stu-id="1cdde-106">Camera</span></span>
> * <span data-ttu-id="1cdde-107">Микрофон</span><span class="sxs-lookup"><span data-stu-id="1cdde-107">Microphone</span></span>
> * <span data-ttu-id="1cdde-108">Расположение</span><span class="sxs-lookup"><span data-stu-id="1cdde-108">Location</span></span>
> * <span data-ttu-id="1cdde-109">Уведомления</span><span class="sxs-lookup"><span data-stu-id="1cdde-109">Notifications</span></span>

> [!NOTE]
> <span data-ttu-id="1cdde-110">Чтобы интегрировать возможности камеры и изображений в мобильном приложении Microsoft Teams, см. функции камеры и [изображений в Teams.](../../concepts/device-capabilities/mobile-camera-image-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="1cdde-110">To integrate camera and image capabilities within your Microsoft Teams mobile app, see [Camera and image capabilities in Teams.](../../concepts/device-capabilities/mobile-camera-image-permissions.md)</span></span>

> [!IMPORTANT]
>
> * <span data-ttu-id="1cdde-111">В настоящее время мобильный клиент Teams поддерживает только доступ к возможностям , и через возможности нативных устройств и доступен во всех конструкциях приложения, включая `camera` `gallery` `mic` `location` вкладки.</span><span class="sxs-lookup"><span data-stu-id="1cdde-111">At present, Teams mobile client only supports access to `camera`, `gallery`, `mic`, and `location` through native device capabilities and is available on all app constructs including tabs.</span></span> </br>
> * <span data-ttu-id="1cdde-112">Поддержка , `camera` `gallery` и `mic` включена через [**selectMedia API**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="1cdde-112">Support for `camera`, `gallery`, and `mic` is enabled through [**selectMedia API**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true).</span></span> <span data-ttu-id="1cdde-113">Для одного захвата изображения можно использовать [**API captureImage.**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="1cdde-113">For single image capture you may use [**captureImage API**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true).</span></span>
> * <span data-ttu-id="1cdde-114">Поддержка `location` включена через [**API getLocation.**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="1cdde-114">Support for `location` is enabled through [**getLocation API**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true).</span></span> <span data-ttu-id="1cdde-115">Рекомендуется использовать этот API, так как В настоящее время [**API**](../../resources/schema/manifest-schema.md#devicepermissions) географического местонахождения не полностью поддерживается на всех классических клиентах.</span><span class="sxs-lookup"><span data-stu-id="1cdde-115">It's recommended you use this API as [**geolocation API**](../../resources/schema/manifest-schema.md#devicepermissions) is currently not fully supported on all desktop clients.</span></span>

## <a name="device-permissions"></a><span data-ttu-id="1cdde-116">Разрешения для устройств</span><span class="sxs-lookup"><span data-stu-id="1cdde-116">Device permissions</span></span>

<span data-ttu-id="1cdde-117">Доступ к разрешениям устройства пользователя позволяет создавать гораздо более богатые возможности, например:</span><span class="sxs-lookup"><span data-stu-id="1cdde-117">Accessing a user’s device permissions allows you to build much richer experiences, for example:</span></span>

* <span data-ttu-id="1cdde-118">Запись и совместное видео</span><span class="sxs-lookup"><span data-stu-id="1cdde-118">Record and share short videos</span></span>
* <span data-ttu-id="1cdde-119">Запись коротких звуковых memos и их сохранение для более поздней 2016 г.</span><span class="sxs-lookup"><span data-stu-id="1cdde-119">Record short audio memos and save them for later</span></span>
* <span data-ttu-id="1cdde-120">Использование сведений о расположении пользователей для отображения соответствующей информации</span><span class="sxs-lookup"><span data-stu-id="1cdde-120">Use user location information to display relevant information</span></span>

<span data-ttu-id="1cdde-121">Хотя доступ к этим функциям является стандартным в большинстве современных веб-браузеров, необходимо дать Teams знать, какие функции вы хотите использовать, обновив манифест приложения.</span><span class="sxs-lookup"><span data-stu-id="1cdde-121">While access to these features is standard in most modern web browsers, you need to let Teams know which features you’d like to use by updating your app manifest.</span></span> <span data-ttu-id="1cdde-122">Это позволит вам запросить разрешения так же, как в браузере, когда ваше приложение работает в настольном клиенте Teams.</span><span class="sxs-lookup"><span data-stu-id="1cdde-122">This will allow you to ask for permissions, the same way you would in a browser, while your app is running on the Teams desktop client.</span></span>

## <a name="manage-permissions"></a><span data-ttu-id="1cdde-123">Управление разрешениями</span><span class="sxs-lookup"><span data-stu-id="1cdde-123">Manage permissions</span></span>

# <a name="desktop"></a>[<span data-ttu-id="1cdde-124">Desktop</span><span class="sxs-lookup"><span data-stu-id="1cdde-124">Desktop</span></span>](#tab/desktop)

1. <span data-ttu-id="1cdde-125">Откройте Teams.</span><span class="sxs-lookup"><span data-stu-id="1cdde-125">Open Teams.</span></span>
1. <span data-ttu-id="1cdde-126">В правом верхнем углу окна выберите значок профиля.</span><span class="sxs-lookup"><span data-stu-id="1cdde-126">In the upper right corner of the window, select your profile icon.</span></span>
1. <span data-ttu-id="1cdde-127">Выберите **"Разрешения**  ->  **параметров"** в выпадаемом меню.</span><span class="sxs-lookup"><span data-stu-id="1cdde-127">Select **Settings** -> **Permissions** from the drop-down menu.</span></span>
1. <span data-ttu-id="1cdde-128">Выберите нужные параметры.</span><span class="sxs-lookup"><span data-stu-id="1cdde-128">Choose your desired settings.</span></span>

![Экран параметров рабочего стола для разрешений устройства](../../assets/images/tabs/device-permissions.png)

# <a name="mobile"></a>[<span data-ttu-id="1cdde-130">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="1cdde-130">Mobile</span></span>](#tab/mobile)

1. <span data-ttu-id="1cdde-131">Откройте Teams.</span><span class="sxs-lookup"><span data-stu-id="1cdde-131">Open Teams.</span></span>
1. <span data-ttu-id="1cdde-132">Go to **Settings**  ->  **App Permissions**.</span><span class="sxs-lookup"><span data-stu-id="1cdde-132">Go to **Settings** -> **App Permissions**.</span></span>
1. <span data-ttu-id="1cdde-133">Выберите приложение, для которое нужно выбрать параметры.</span><span class="sxs-lookup"><span data-stu-id="1cdde-133">Select the app you need to choose settings for.</span></span>
1. <span data-ttu-id="1cdde-134">Выберите нужные параметры.</span><span class="sxs-lookup"><span data-stu-id="1cdde-134">Choose your desired settings.</span></span>

![Экран разрешений устройства для мобильных устройств](../../assets/images/tabs/MobilePermissions.png)

---

## <a name="properties"></a><span data-ttu-id="1cdde-136">Свойства</span><span class="sxs-lookup"><span data-stu-id="1cdde-136">Properties</span></span>

<span data-ttu-id="1cdde-137">Обновите приложение, добавив и указав, какое из пяти свойств вы хотите `manifest.json` `devicePermissions` использовать в приложении:</span><span class="sxs-lookup"><span data-stu-id="1cdde-137">Update your app's `manifest.json` by adding `devicePermissions` and specifying which of the five properties you’d like to use in your application:</span></span>

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
> <span data-ttu-id="1cdde-138">Мультимедиа также используется для разрешений камеры на мобильных устройствах.</span><span class="sxs-lookup"><span data-stu-id="1cdde-138">Media is also used for camera permissions on mobile.</span></span>

<span data-ttu-id="1cdde-139">Каждое свойство позволит вам попросить пользователя запросить свое согласие:</span><span class="sxs-lookup"><span data-stu-id="1cdde-139">Each property will allow you to prompt the user to ask for their consent:</span></span>

| <span data-ttu-id="1cdde-140">Свойство</span><span class="sxs-lookup"><span data-stu-id="1cdde-140">Property</span></span>      | <span data-ttu-id="1cdde-141">Описание</span><span class="sxs-lookup"><span data-stu-id="1cdde-141">Description</span></span>   |
| --- | --- |
| <span data-ttu-id="1cdde-142">media</span><span class="sxs-lookup"><span data-stu-id="1cdde-142">media</span></span>         | <span data-ttu-id="1cdde-143">разрешение на использование камеры, микрофона, динамиков и галереи мультимедиа</span><span class="sxs-lookup"><span data-stu-id="1cdde-143">permission to use the camera, microphone, speakers, and access media gallery</span></span> |
| <span data-ttu-id="1cdde-144">geolocation</span><span class="sxs-lookup"><span data-stu-id="1cdde-144">geolocation</span></span>   | <span data-ttu-id="1cdde-145">разрешение на возврат расположения пользователя</span><span class="sxs-lookup"><span data-stu-id="1cdde-145">permission to return the user's location</span></span>      |
| <span data-ttu-id="1cdde-146">notifications</span><span class="sxs-lookup"><span data-stu-id="1cdde-146">notifications</span></span> | <span data-ttu-id="1cdde-147">разрешение на отправку уведомлений пользователя</span><span class="sxs-lookup"><span data-stu-id="1cdde-147">permission to send the user notifications</span></span>      |
| <span data-ttu-id="1cdde-148">midi</span><span class="sxs-lookup"><span data-stu-id="1cdde-148">midi</span></span>          | <span data-ttu-id="1cdde-149">разрешение на отправку и получение сведений midi от цифрового музыкального инструмента</span><span class="sxs-lookup"><span data-stu-id="1cdde-149">permission to send and receive midi information from a digital musical instrument</span></span>   |
| <span data-ttu-id="1cdde-150">openExternal</span><span class="sxs-lookup"><span data-stu-id="1cdde-150">openExternal</span></span>  | <span data-ttu-id="1cdde-151">разрешение на открытие ссылок во внешних приложениях</span><span class="sxs-lookup"><span data-stu-id="1cdde-151">permission to open links in external applications</span></span>  |

## <a name="checking-permissions-from-your-tab"></a><span data-ttu-id="1cdde-152">Проверка разрешений на вкладке</span><span class="sxs-lookup"><span data-stu-id="1cdde-152">Checking permissions from your tab</span></span>

<span data-ttu-id="1cdde-153">После того как вы добавите в манифест приложения, вы можете проверить разрешения с помощью `devicePermissions` API "разрешений" HTML5 без запроса.</span><span class="sxs-lookup"><span data-stu-id="1cdde-153">Once you’ve added `devicePermissions` to your app manifest, you can check permissions using the HTML5 “permissions” API without causing a prompt.</span></span>

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

## <a name="prompting-the-user"></a><span data-ttu-id="1cdde-154">Запрос пользователя</span><span class="sxs-lookup"><span data-stu-id="1cdde-154">Prompting the user</span></span>

<span data-ttu-id="1cdde-155">Чтобы показать запрос на согласие на доступ к разрешениям устройства, необходимо использовать соответствующий API HTML5 или Teams.</span><span class="sxs-lookup"><span data-stu-id="1cdde-155">To show a prompt to get consent to access device permissions you need to leverage the appropriate HTML5 or Teams API.</span></span> 

<span data-ttu-id="1cdde-156">Например, чтобы у пользователя получить доступ к его расположению, необходимо `getCurrentPosition` вызвать:</span><span class="sxs-lookup"><span data-stu-id="1cdde-156">For example, to prompt the user to access their location you need to call `getCurrentPosition`:</span></span>

```Javascript
navigator.geolocation.getCurrentPosition(function (position) { /*... */ });
```

<span data-ttu-id="1cdde-157">Чтобы использовать камеру на рабочем столе или в Интернете, Teams будет показывать запрос на разрешение при `getUserMedia` вызове:</span><span class="sxs-lookup"><span data-stu-id="1cdde-157">To use the camera on desktop or web, Teams will show a permission prompt when you call `getUserMedia`:</span></span>

```Javascript
navigator.mediaDevices.getUserMedia({ audio: true, video: true });
```

<span data-ttu-id="1cdde-158">Чтобы захватить изображение на мобильных устройствах, Teams Mobile запросит разрешение при `captureImage()` вызове:</span><span class="sxs-lookup"><span data-stu-id="1cdde-158">To capture the image on mobile, Teams mobile will ask for permission when you call `captureImage()`:</span></span>

```Javascript
microsoftTeams.media.captureImage((error: microsoftTeams.SdkError, files: microsoftTeams.media.File[]) => {
  /* ... */
});
```

<span data-ttu-id="1cdde-159">При вызове уведомлений пользователю будет `requestPermission` предложено:</span><span class="sxs-lookup"><span data-stu-id="1cdde-159">Notifications will prompt the user when you call `requestPermission`:</span></span>

```Javascript
Notification.requestPermission(function(result) { /* ... */ });
```

<span data-ttu-id="1cdde-160">Чтобы использовать камеру или доступ к фотоальбому, Teams Mobile запросит разрешение при `selectMedia()` вызове:</span><span class="sxs-lookup"><span data-stu-id="1cdde-160">To use camera or access photo gallery, Teams mobile will ask permission when you call `selectMedia()`:</span></span>

```JavaScript
microsoftTeams.media.selectMedia({ maxMediaCount: 10, mediaType: microsoftTeams.media.MediaType.Image }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
  /* ... */
});
```

<span data-ttu-id="1cdde-161">Чтобы использовать микрофон, Teams Mobile запросит разрешение при `selectMedia()` вызове:</span><span class="sxs-lookup"><span data-stu-id="1cdde-161">To use mic, Teams mobile will ask permission when you call `selectMedia()`:</span></span>

```JavaScript 
microsoftTeams.media.selectMedia({ maxMediaCount: 1, mediaType: microsoftTeams.media.MediaType.Audio }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
  /* ... */
});
```

<span data-ttu-id="1cdde-162">Чтобы попросить пользователя поделиться расположением в интерфейсе карты, Приложение Teams Mobile запросит разрешение при `getLocation()` вызове:</span><span class="sxs-lookup"><span data-stu-id="1cdde-162">To prompt user to share location on map interface, Teams mobile will ask permission when you call `getLocation()`:</span></span>

```JavaScript 
microsoftTeams.location.getLocation({ allowChooseLocation: true, showMap: true }, (error: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
  /* ... *
/});
```

# <a name="desktop"></a>[<span data-ttu-id="1cdde-163">Desktop</span><span class="sxs-lookup"><span data-stu-id="1cdde-163">Desktop</span></span>](#tab/desktop)

![Запрос разрешений для настольных устройств на вкладке](~/assets/images/tabs/device-permissions-prompt.png)

# <a name="mobile"></a>[<span data-ttu-id="1cdde-165">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="1cdde-165">Mobile</span></span>](#tab/mobile)

![Запрос разрешений мобильного устройства "Вкладки"](../../assets/images/tabs/MobileLocationPermission.png)


## <a name="permission-behavior-across-login-sessions"></a><span data-ttu-id="1cdde-167">Поведение разрешений в сеансах входа</span><span class="sxs-lookup"><span data-stu-id="1cdde-167">Permission behavior across login sessions</span></span>

<span data-ttu-id="1cdde-168">Разрешения для устройств сохраняются для каждого сеанса входа.</span><span class="sxs-lookup"><span data-stu-id="1cdde-168">Native device permissions are stored for every login session.</span></span> <span data-ttu-id="1cdde-169">Это означает, что при входе в другой экземпляр Teams (например, на другом компьютере) разрешения устройства из предыдущих сеансов будут недоступны.</span><span class="sxs-lookup"><span data-stu-id="1cdde-169">It means that if you log into another instance of Teams (ex: on another computer), your device permissions from your previous sessions will not be available.</span></span> <span data-ttu-id="1cdde-170">Вместо этого вам потребуется повторно согласиться на использование разрешений устройства для нового сеанса входа.</span><span class="sxs-lookup"><span data-stu-id="1cdde-170">Instead, you will need to re-consent to device permissions for the new login session.</span></span> <span data-ttu-id="1cdde-171">Это также означает, что при выходе из Teams (или переключении клиентов в Teams) разрешения устройства будут удалены для предыдущего сеанса входа.</span><span class="sxs-lookup"><span data-stu-id="1cdde-171">It also means, if you log out of Teams (or switch tenants inside of Teams), your device permissions will be deleted for that previous login session.</span></span> <span data-ttu-id="1cdde-172">Помните об этом при разработке нативных разрешений устройства: те же возможности, которые вы даете согласие, будут только для _текущего_ сеанса входа в систему.</span><span class="sxs-lookup"><span data-stu-id="1cdde-172">Please keep this in mind when developing native device permissions: the native capabilities you consent to are only for your _current_ login session.</span></span>
