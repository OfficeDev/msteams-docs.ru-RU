---
title: Запрос разрешений на устройство для Microsoft Teams приложения
keywords: разрешения командных приложений
description: Обновление манифеста приложения для запроса доступа к родным функциям, которые обычно требуют согласия пользователя
localization_priority: Normal
ms.topic: how-to
ms.openlocfilehash: 37312912b4901cd31feeb9b0ee9bc76a3e03826a
ms.sourcegitcommit: 059d22c436ee9b07a61561ff71e03e1c23ff40b8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/30/2021
ms.locfileid: "53211620"
---
# <a name="request-device-permissions-for-your-microsoft-teams-app"></a><span data-ttu-id="3ec89-104">Запрос разрешений на устройство для Microsoft Teams приложения</span><span class="sxs-lookup"><span data-stu-id="3ec89-104">Request device permissions for your Microsoft Teams app</span></span>

<span data-ttu-id="3ec89-105">Вы можете обогатить Teams с помощью родных возможностей устройства, таких как камера, микрофон и расположение.</span><span class="sxs-lookup"><span data-stu-id="3ec89-105">You can enrich your Teams app with native device capabilities, such as camera, microphone, and location.</span></span> <span data-ttu-id="3ec89-106">В этом документе вы можете узнать, как запрашивать согласие пользователя и получать доступ к разрешениям на родных устройствах.</span><span class="sxs-lookup"><span data-stu-id="3ec89-106">This document guides you on how to request user consent and access the native device permissions.</span></span>

> [!NOTE]
> * <span data-ttu-id="3ec89-107">Чтобы интегрировать возможности мультимедиа в Microsoft Teams мобильном приложении, см. в приложении [Integrate media capabilities.](mobile-camera-image-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="3ec89-107">To integrate media capabilities within your Microsoft Teams mobile app, see [Integrate media capabilities](mobile-camera-image-permissions.md).</span></span>
> * <span data-ttu-id="3ec89-108">Чтобы интегрировать функцию сканера [QR](qr-barcode-scanner-capability.md)или штрихкода в мобильном приложении Microsoft Teams см. в Teams.</span><span class="sxs-lookup"><span data-stu-id="3ec89-108">To integrate QR or barcode scanner capability within your Microsoft Teams mobile app, see [Integrate QR or barcode scanner capability in Teams](qr-barcode-scanner-capability.md).</span></span>
> * <span data-ttu-id="3ec89-109">Чтобы интегрировать возможности расположения в Microsoft Teams мобильном приложении, см. в [приложении Integrate location capabilities.](location-capability.md)</span><span class="sxs-lookup"><span data-stu-id="3ec89-109">To integrate location capabilities within your Microsoft Teams mobile app, see [Integrate location capabilities](location-capability.md).</span></span>
> * <span data-ttu-id="3ec89-110">Чтобы интегрировать возможности выборщика людей в Microsoft Teams мобильном приложении, см. в [Teams.](people-picker-capability.md)</span><span class="sxs-lookup"><span data-stu-id="3ec89-110">To integrate People Picker capability within your Microsoft Teams mobile app, see [Integrate People Picker capability in Teams](people-picker-capability.md).</span></span>

## <a name="native-device-permissions"></a><span data-ttu-id="3ec89-111">Разрешения на использование родных устройств</span><span class="sxs-lookup"><span data-stu-id="3ec89-111">Native device permissions</span></span>

<span data-ttu-id="3ec89-112">Необходимо запросить разрешения устройства для доступа к возможностям родного устройства.</span><span class="sxs-lookup"><span data-stu-id="3ec89-112">You must request the device permissions to access native device capabilities.</span></span> <span data-ttu-id="3ec89-113">Разрешения устройства работают аналогично для всех конструкций приложений, таких как вкладки, модули задач или расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="3ec89-113">The device permissions work similarly for all app constructs, such as tabs, task modules, or messaging extensions.</span></span> <span data-ttu-id="3ec89-114">Пользователь должен перейти на страницу разрешений в Teams параметров для управления разрешениями устройств.</span><span class="sxs-lookup"><span data-stu-id="3ec89-114">The user must go to the permissions page in Teams settings to manage device permissions.</span></span>
<span data-ttu-id="3ec89-115">Доступ к возможностям устройства позволяет создавать более богатые возможности на платформе Teams, например:</span><span class="sxs-lookup"><span data-stu-id="3ec89-115">By accessing the device capabilities, you can build richer experiences on the Teams platform, such as:</span></span>
* <span data-ttu-id="3ec89-116">Захват и просмотр изображений.</span><span class="sxs-lookup"><span data-stu-id="3ec89-116">Capture and view images.</span></span>
* <span data-ttu-id="3ec89-117">Сканирование QR или штрихкода.</span><span class="sxs-lookup"><span data-stu-id="3ec89-117">Scan QR or barcode.</span></span>
* <span data-ttu-id="3ec89-118">Запись и доля коротких видео.</span><span class="sxs-lookup"><span data-stu-id="3ec89-118">Record and share short videos.</span></span>
* <span data-ttu-id="3ec89-119">Запись аудиозаписей и сохранение их для более позднего использования.</span><span class="sxs-lookup"><span data-stu-id="3ec89-119">Record audio memos and save them for later use.</span></span>
* <span data-ttu-id="3ec89-120">Используйте сведения о расположении пользователя для отображения соответствующих сведений.</span><span class="sxs-lookup"><span data-stu-id="3ec89-120">Use the location information of the user to display relevant information.</span></span>

> [!NOTE]
> <span data-ttu-id="3ec89-121">В настоящее время Teams не поддерживает разрешения устройств для нескольких оконных приложений, вкладок и sidepanel собраний.</span><span class="sxs-lookup"><span data-stu-id="3ec89-121">Currently, Teams does not support device permissions for multi window apps, tabs, and the meeting sidepanel.</span></span> 

## <a name="access-device-permissions"></a><span data-ttu-id="3ec89-122">Разрешения на доступ к устройствам</span><span class="sxs-lookup"><span data-stu-id="3ec89-122">Access device permissions</span></span>

<span data-ttu-id="3ec89-123">Клиент [Microsoft Teams JavaScript SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) предоставляет средства, необходимые Teams мобильному приложению для [](#manage-permissions) доступа к разрешениям устройств пользователя и создания более насыщенного интерфейса.</span><span class="sxs-lookup"><span data-stu-id="3ec89-123">The [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) provides the tools necessary for your Teams mobile app to access the user’s [device permissions](#manage-permissions) and build a richer experience.</span></span>

<span data-ttu-id="3ec89-124">Хотя доступ к этим функциям является стандартным в современных веб-браузерах, необходимо информировать Teams о свойствах, которые вы используете, обновив манифест приложения.</span><span class="sxs-lookup"><span data-stu-id="3ec89-124">While access to these features is standard in modern web browsers, you must inform Teams about the features you use by updating your app manifest.</span></span> <span data-ttu-id="3ec89-125">Это обновление позволяет спрашивать разрешения, пока приложение работает на Teams настольном клиенте.</span><span class="sxs-lookup"><span data-stu-id="3ec89-125">This update allows you to ask for permissions while your app runs on the Teams desktop client.</span></span>

> [!NOTE] 
> <span data-ttu-id="3ec89-126">В настоящее время Microsoft Teams средства массовой информации и возможности сканера штрихкодов QR доступны только для мобильных клиентов.</span><span class="sxs-lookup"><span data-stu-id="3ec89-126">Currently, Microsoft Teams support for media capabilities and QR barcode scanner capability is only available for mobile clients.</span></span>

## <a name="manage-permissions"></a><span data-ttu-id="3ec89-127">Управление разрешениями</span><span class="sxs-lookup"><span data-stu-id="3ec89-127">Manage permissions</span></span>

<span data-ttu-id="3ec89-128">Пользователь может управлять разрешениями устройств в Teams параметров,  выбрав **разрешить** или запретить разрешения для определенных приложений.</span><span class="sxs-lookup"><span data-stu-id="3ec89-128">A user can manage device permissions in Teams settings by selecting **Allow** or **Deny** permissions to specific apps.</span></span>
 
# <a name="desktop"></a>[<span data-ttu-id="3ec89-129">Классическая версия</span><span class="sxs-lookup"><span data-stu-id="3ec89-129">Desktop</span></span>](#tab/desktop)

1. <span data-ttu-id="3ec89-130">Откройте приложение Teams.</span><span class="sxs-lookup"><span data-stu-id="3ec89-130">Open your Teams app.</span></span>
1. <span data-ttu-id="3ec89-131">Выберите значок профиля в правом верхнем углу окна.</span><span class="sxs-lookup"><span data-stu-id="3ec89-131">Select your profile icon in the upper right corner of the window.</span></span>
1. <span data-ttu-id="3ec89-132">Выберите **Параметры**  >  **разрешений** из выпадаемого меню.</span><span class="sxs-lookup"><span data-stu-id="3ec89-132">Select **Settings** > **Permissions** from the drop-down menu.</span></span>
1. <span data-ttu-id="3ec89-133">Выберите нужные параметры.</span><span class="sxs-lookup"><span data-stu-id="3ec89-133">Select your desired settings.</span></span>

   ![Экран параметров настольных компьютеров разрешений устройств](../../assets/images/tabs/device-permissions.png)

# <a name="mobile"></a>[<span data-ttu-id="3ec89-135">Мобильная версия</span><span class="sxs-lookup"><span data-stu-id="3ec89-135">Mobile</span></span>](#tab/mobile)

1. <span data-ttu-id="3ec89-136">Откройте Teams.</span><span class="sxs-lookup"><span data-stu-id="3ec89-136">Open Teams.</span></span>
1. <span data-ttu-id="3ec89-137">Перейдите **Параметры**  >  **разрешения на приложения.**</span><span class="sxs-lookup"><span data-stu-id="3ec89-137">Go to **Settings** > **App Permissions**.</span></span>
1. <span data-ttu-id="3ec89-138">Выберите приложение, для которого необходимо выбрать параметры.</span><span class="sxs-lookup"><span data-stu-id="3ec89-138">Select the app for which you need to choose the settings.</span></span>
1. <span data-ttu-id="3ec89-139">Выберите нужные параметры.</span><span class="sxs-lookup"><span data-stu-id="3ec89-139">Select your desired settings.</span></span>

    ![Экран разрешений мобильных параметров устройства](../../assets/images/tabs/MobilePermissions.png)

---

## <a name="specify-permissions"></a><span data-ttu-id="3ec89-141">Указание разрешений</span><span class="sxs-lookup"><span data-stu-id="3ec89-141">Specify permissions</span></span>

<span data-ttu-id="3ec89-142">Обновите приложение, добавив и укажите, какие из следующих пяти свойств вы `manifest.json` `devicePermissions` используете в приложении:</span><span class="sxs-lookup"><span data-stu-id="3ec89-142">Update your app's `manifest.json` by adding `devicePermissions` and specifying which of the following five properties that you use in your application:</span></span>

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```

<span data-ttu-id="3ec89-143">Каждое свойство позволяет задать пользователю запрос на его согласие:</span><span class="sxs-lookup"><span data-stu-id="3ec89-143">Each property allows you to prompt the user to ask for their consent:</span></span>

| <span data-ttu-id="3ec89-144">Свойство</span><span class="sxs-lookup"><span data-stu-id="3ec89-144">Property</span></span>      | <span data-ttu-id="3ec89-145">Описание</span><span class="sxs-lookup"><span data-stu-id="3ec89-145">Description</span></span>   |
| --- | --- |
| <span data-ttu-id="3ec89-146">мультимедиа</span><span class="sxs-lookup"><span data-stu-id="3ec89-146">media</span></span>         | <span data-ttu-id="3ec89-147">Разрешение на использование камеры, микрофона, динамиков и доступа к медиа-галерее.</span><span class="sxs-lookup"><span data-stu-id="3ec89-147">Permission to use the camera, microphone, speakers, and access media gallery.</span></span> |
| <span data-ttu-id="3ec89-148">геолокация</span><span class="sxs-lookup"><span data-stu-id="3ec89-148">geolocation</span></span>   | <span data-ttu-id="3ec89-149">Разрешение на возвращение расположения пользователя.</span><span class="sxs-lookup"><span data-stu-id="3ec89-149">Permission to return the user's location.</span></span>      |
| <span data-ttu-id="3ec89-150">уведомления</span><span class="sxs-lookup"><span data-stu-id="3ec89-150">notifications</span></span> | <span data-ttu-id="3ec89-151">Разрешение на отправку уведомлений пользователя.</span><span class="sxs-lookup"><span data-stu-id="3ec89-151">Permission to send the user notifications.</span></span>      |
| <span data-ttu-id="3ec89-152">midi</span><span class="sxs-lookup"><span data-stu-id="3ec89-152">midi</span></span>          | <span data-ttu-id="3ec89-153">Разрешение на отправку и получение сведений о цифровом интерфейсе музыкальных инструментов (MIDI) с цифрового музыкального инструмента.</span><span class="sxs-lookup"><span data-stu-id="3ec89-153">Permission to send and receive  Musical Instrument Digital Interface (MIDI) information from a digital musical instrument.</span></span>   |
| <span data-ttu-id="3ec89-154">openExternal</span><span class="sxs-lookup"><span data-stu-id="3ec89-154">openExternal</span></span>  | <span data-ttu-id="3ec89-155">Разрешение на открытие ссылок во внешних приложениях.</span><span class="sxs-lookup"><span data-stu-id="3ec89-155">Permission to open links in external applications.</span></span>  |

## <a name="check-permissions-from-your-app"></a><span data-ttu-id="3ec89-156">Проверка разрешений из приложения</span><span class="sxs-lookup"><span data-stu-id="3ec89-156">Check permissions from your app</span></span>

<span data-ttu-id="3ec89-157">После добавления в манифест приложения проверьте разрешения с помощью `devicePermissions` **API разрешений HTML5** без запроса:</span><span class="sxs-lookup"><span data-stu-id="3ec89-157">After adding `devicePermissions` to your app manifest, check permissions using the **HTML5 permissions API** without causing a prompt:</span></span>

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

## <a name="use-teams-apis-to-get-device-permissions"></a><span data-ttu-id="3ec89-158">Используйте Teams API для получения разрешений на устройства</span><span class="sxs-lookup"><span data-stu-id="3ec89-158">Use Teams APIs to get device permissions</span></span>

<span data-ttu-id="3ec89-159">Используйте соответствующие HTML5 или Teams API, чтобы отобразить подсказку для получения согласия на доступ к разрешениям устройств.</span><span class="sxs-lookup"><span data-stu-id="3ec89-159">Leverage appropriate HTML5 or Teams API, to display a prompt for getting consent to access device permissions.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="3ec89-160">Поддержка `camera` , `gallery` и включен через `microphone` [**selectMedia API**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="3ec89-160">Support for `camera`, `gallery`, and `microphone` is enabled through [**selectMedia API**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true).</span></span> <span data-ttu-id="3ec89-161">Используйте [**API captureImage**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) для одного захвата изображения.</span><span class="sxs-lookup"><span data-stu-id="3ec89-161">Use [**captureImage API**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) for a single image capture.</span></span>
> * <span data-ttu-id="3ec89-162">Поддержка `location` включена через [**API getLocation.**](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="3ec89-162">Support for `location` is enabled through [**getLocation API**](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true).</span></span> <span data-ttu-id="3ec89-163">Это необходимо использовать для расположения, так как API геолокации HTML5 в настоящее время не полностью поддерживается на `getLocation API` Teams настольном клиенте.</span><span class="sxs-lookup"><span data-stu-id="3ec89-163">You must use this `getLocation API` for location, as HTML5 geolocation API is currently not fully supported on Teams desktop client.</span></span>

<span data-ttu-id="3ec89-164">Например:</span><span class="sxs-lookup"><span data-stu-id="3ec89-164">For example:</span></span>
 * <span data-ttu-id="3ec89-165">Чтобы подсказыть пользователю доступ к их расположению, необходимо `getCurrentPosition()` вызвать:</span><span class="sxs-lookup"><span data-stu-id="3ec89-165">To prompt the user to access their location you must call `getCurrentPosition()`:</span></span>

    ```Javascript
    navigator.geolocation.getCurrentPosition    (function (position) { /*... */ });
    ```

 * <span data-ttu-id="3ec89-166">Чтобы подсказыть пользователю доступ к камере на рабочем столе или в Интернете, необходимо `getUserMedia()` вызвать:</span><span class="sxs-lookup"><span data-stu-id="3ec89-166">To prompt the user to access their camera on desktop or web you must call `getUserMedia()`:</span></span>

    ```Javascript
    navigator.mediaDevices.getUserMedia({ audio: true, video: true });
    ```

 * <span data-ttu-id="3ec89-167">Чтобы захватить изображение на мобильном телефоне, Teams мобильный просит разрешения при `captureImage()` вызове:</span><span class="sxs-lookup"><span data-stu-id="3ec89-167">To capture the image on mobile, Teams mobile asks for permission when you call `captureImage()`:</span></span>

    ```Javascript
    microsoftTeams.media.captureImage((error: microsoftTeams.SdkError, files: microsoftTeams.media.File[]) => {
      /* ... */
    });
    ```

 * <span data-ttu-id="3ec89-168">Уведомления подскажут пользователю при `requestPermission()` вызове:</span><span class="sxs-lookup"><span data-stu-id="3ec89-168">Notifications will prompt the user when you call `requestPermission()`:</span></span>

    ```Javascript
    Notification.requestPermission(function(result) { /* ... */ });
    ```




* <span data-ttu-id="3ec89-169">Чтобы использовать камеру или доступ к фотогалерее, Teams мобильный просит разрешения при `selectMedia()` вызове:</span><span class="sxs-lookup"><span data-stu-id="3ec89-169">To use the camera or access photo gallery, Teams mobile asks permission when you call `selectMedia()`:</span></span>

    ```JavaScript
    microsoftTeams.media.selectMedia({ maxMediaCount: 10, mediaType: microsoftTeams.media.MediaType.Image }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    );
    ```

* <span data-ttu-id="3ec89-170">Чтобы использовать микрофон, Teams мобильный спрашивает разрешения при `selectMedia()` вызове:</span><span class="sxs-lookup"><span data-stu-id="3ec89-170">To use the microphone, Teams mobile asks permission when you call `selectMedia()`:</span></span>

    ```JavaScript 
    microsoftTeams.media.selectMedia({ maxMediaCount: 1, mediaType: microsoftTeams.media.MediaType.Audio }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    });
    ```

* <span data-ttu-id="3ec89-171">Чтобы побудить пользователя к совместному расположению в интерфейсе карты, Teams мобильный просит разрешения при `getLocation()` вызове:</span><span class="sxs-lookup"><span data-stu-id="3ec89-171">To prompt the user to share location on the map interface, Teams mobile asks permission when you call `getLocation()`:</span></span>

    ```JavaScript 
    microsoftTeams.location.getLocation({ allowChooseLocation: true, showMap: true }, (error: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
      /* ... *
    /});
    ```
# <a name="desktop"></a>[<span data-ttu-id="3ec89-172">Классическая версия</span><span class="sxs-lookup"><span data-stu-id="3ec89-172">Desktop</span></span>](#tab/desktop)

   ![Запрос разрешений на настольные устройства tabs](~/assets/images/tabs/device-permissions-prompt.png)

# <a name="mobile"></a>[<span data-ttu-id="3ec89-174">Мобильная версия</span><span class="sxs-lookup"><span data-stu-id="3ec89-174">Mobile</span></span>](#tab/mobile)

   ![Запрос разрешений мобильных устройств Tabs](../../assets/images/tabs/MobileLocationPermission.png)

* * * 

## <a name="permission-behavior-across-login-sessions"></a><span data-ttu-id="3ec89-176">Поведение разрешений в сеансах входа</span><span class="sxs-lookup"><span data-stu-id="3ec89-176">Permission behavior across login sessions</span></span>

<span data-ttu-id="3ec89-177">Разрешения устройства хранятся для каждого сеанса входа.</span><span class="sxs-lookup"><span data-stu-id="3ec89-177">Device permissions are stored for every login session.</span></span> <span data-ttu-id="3ec89-178">Это означает, что при входе в другой экземпляр Teams, например, на другом компьютере, разрешения на устройство с предыдущих сеансов недоступны.</span><span class="sxs-lookup"><span data-stu-id="3ec89-178">It means that if you sign in to another instance of Teams, for example, on another computer, your device permissions from your previous sessions are not available.</span></span> <span data-ttu-id="3ec89-179">Поэтому необходимо повторно согласиться на разрешения устройств для нового сеанса.</span><span class="sxs-lookup"><span data-stu-id="3ec89-179">Therefore, you must re-consent to device permissions for the new session.</span></span> <span data-ttu-id="3ec89-180">Это также означает, что если вы Teams или переключите клиентов в Teams, разрешения устройства удаляются из предыдущего сеанса входа.</span><span class="sxs-lookup"><span data-stu-id="3ec89-180">It also means, if you sign out of Teams or switch tenants in Teams, your device permissions are deleted from the previous login session.</span></span>  

> [!NOTE]
> <span data-ttu-id="3ec89-181">Если вы даете согласие на разрешения на родном устройстве, оно допустимо только для _текущего_ сеанса входа.</span><span class="sxs-lookup"><span data-stu-id="3ec89-181">When you consent to the native device permissions, it is valid only for your _current_ login session.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3ec89-182">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3ec89-182">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3ec89-183">Интеграция возможностей мультимедиа в Teams</span><span class="sxs-lookup"><span data-stu-id="3ec89-183">Integrate media capabilities in Teams</span></span>](mobile-camera-image-permissions.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="3ec89-184">Интеграция возможностей сканера QR или штрихкодов в Teams</span><span class="sxs-lookup"><span data-stu-id="3ec89-184">Integrate QR or barcode scanner capability in Teams</span></span>](qr-barcode-scanner-capability.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="3ec89-185">Интеграция возможностей расположения в Teams</span><span class="sxs-lookup"><span data-stu-id="3ec89-185">Integrate location capabilities in Teams</span></span>](location-capability.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="3ec89-186">Интеграция возможностей выборщика людей в Teams</span><span class="sxs-lookup"><span data-stu-id="3ec89-186">Integrate People Picker capability in Teams</span></span>](people-picker-capability.md)
