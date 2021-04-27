---
title: Запрос разрешений устройств для приложения Microsoft Teams
keywords: разрешения командных приложений
description: Обновление манифеста приложения для запроса доступа к родным функциям, которые обычно требуют согласия пользователя
localization_priority: Normal
ms.topic: how-to
ms.openlocfilehash: 452840c5809da32a79c231f85cd1de9f8746367a
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019855"
---
# <a name="request-device-permissions-for-your-microsoft-teams-app"></a><span data-ttu-id="55a59-104">Запрос разрешений устройств для приложения Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="55a59-104">Request device permissions for your Microsoft Teams app</span></span>

<span data-ttu-id="55a59-105">Вы можете обогатить приложение Teams возможностями родного устройства, например камерой, микрофоном и расположением.</span><span class="sxs-lookup"><span data-stu-id="55a59-105">You can enrich your Teams app with native device capabilities, such as camera, microphone, and location.</span></span> <span data-ttu-id="55a59-106">В этом документе вы можете узнать, как запрашивать согласие пользователя и получать доступ к разрешениям на родных устройствах.</span><span class="sxs-lookup"><span data-stu-id="55a59-106">This document guides you on how to request user consent and access the native device permissions.</span></span>

> [!NOTE]
> * <span data-ttu-id="55a59-107">Чтобы интегрировать возможности мультимедиа в мобильном приложении Microsoft Teams, см. в приложении [Integrate media capabilities.](mobile-camera-image-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="55a59-107">To integrate media capabilities within your Microsoft Teams mobile app, see [Integrate media capabilities](mobile-camera-image-permissions.md).</span></span>
> * <span data-ttu-id="55a59-108">Чтобы интегрировать функции сканера QR или штрихкода в мобильном приложении Microsoft Teams, см. в материале [Интеграция функции QR](qr-barcode-scanner-capability.md) или сканера штрихкодов в Teams</span><span class="sxs-lookup"><span data-stu-id="55a59-108">To integrate QR or barcode scanner capability within your Microsoft Teams mobile app, see [Integrate QR or barcode scanner capability in Teams](qr-barcode-scanner-capability.md)</span></span>
> * <span data-ttu-id="55a59-109">Чтобы интегрировать возможности расположения в мобильном приложении Microsoft Teams, см. в приложении [Integrate location capabilities.](location-capability.md)</span><span class="sxs-lookup"><span data-stu-id="55a59-109">To integrate location capabilities within your Microsoft Teams mobile app, see [Integrate location capabilities](location-capability.md).</span></span>

## <a name="native-device-permissions"></a><span data-ttu-id="55a59-110">Разрешения на использование родных устройств</span><span class="sxs-lookup"><span data-stu-id="55a59-110">Native device permissions</span></span>

<span data-ttu-id="55a59-111">Необходимо запросить разрешения устройства для доступа к возможностям родного устройства.</span><span class="sxs-lookup"><span data-stu-id="55a59-111">You must request the device permissions to access native device capabilities.</span></span> <span data-ttu-id="55a59-112">Разрешения устройства работают аналогично для всех конструкций приложений, таких как вкладки, модули задач или расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="55a59-112">The device permissions work similarly for all app constructs, such as tabs, task modules, or messaging extensions.</span></span> <span data-ttu-id="55a59-113">Чтобы управлять разрешениями устройств, пользователь должен перейти на страницу разрешений в параметрах Teams.</span><span class="sxs-lookup"><span data-stu-id="55a59-113">The user must go to the permissions page in Teams settings to manage device permissions.</span></span>
<span data-ttu-id="55a59-114">Доступ к возможностям устройства позволяет создавать более богатые возможности на платформе Teams, например:</span><span class="sxs-lookup"><span data-stu-id="55a59-114">By accessing the device capabilities, you can build richer experiences on the Teams platform, such as:</span></span>
* <span data-ttu-id="55a59-115">Захват и просмотр изображений.</span><span class="sxs-lookup"><span data-stu-id="55a59-115">Capture and view images.</span></span>
* <span data-ttu-id="55a59-116">Сканирование QR или штрихкода.</span><span class="sxs-lookup"><span data-stu-id="55a59-116">Scan QR or barcode.</span></span>
* <span data-ttu-id="55a59-117">Запись и доля коротких видео.</span><span class="sxs-lookup"><span data-stu-id="55a59-117">Record and share short videos.</span></span>
* <span data-ttu-id="55a59-118">Запись аудиозаписей и сохранение их для более позднего использования.</span><span class="sxs-lookup"><span data-stu-id="55a59-118">Record audio memos and save them for later use.</span></span>
* <span data-ttu-id="55a59-119">Используйте сведения о расположении пользователя для отображения соответствующих сведений.</span><span class="sxs-lookup"><span data-stu-id="55a59-119">Use the location information of the user to display relevant information.</span></span>

## <a name="access-device-permissions"></a><span data-ttu-id="55a59-120">Разрешения на доступ к устройствам</span><span class="sxs-lookup"><span data-stu-id="55a59-120">Access device permissions</span></span>

<span data-ttu-id="55a59-121">Клиент [Microsoft Teams JavaScript предоставляет](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) средства, необходимые мобильному приложению Teams [](#manage-permissions) для доступа к разрешениям на устройства пользователя и создания более насыщенного интерфейса.</span><span class="sxs-lookup"><span data-stu-id="55a59-121">The [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) provides the tools necessary for your Teams mobile app to access the user’s [device permissions](#manage-permissions) and build a richer experience.</span></span>

<span data-ttu-id="55a59-122">Хотя доступ к этим функциям является стандартным в современных веб-браузерах, необходимо информировать Teams о свойствах, которые вы используете, обновив манифест приложения.</span><span class="sxs-lookup"><span data-stu-id="55a59-122">While access to these features is standard in modern web browsers, you must inform Teams about the features you use by updating your app manifest.</span></span> <span data-ttu-id="55a59-123">Это обновление позволяет спрашивать разрешения, пока приложение работает на настольном клиенте Teams.</span><span class="sxs-lookup"><span data-stu-id="55a59-123">This update allows you to ask for permissions while your app runs on the Teams desktop client.</span></span>

> [!NOTE] 
> <span data-ttu-id="55a59-124">В настоящее время поддержка Microsoft Teams возможностей мультимедиа и сканера штрихкодов QR доступна только для мобильных клиентов.</span><span class="sxs-lookup"><span data-stu-id="55a59-124">Currently, Microsoft Teams support for media capabilities and QR barcode scanner capability is only available for mobile clients.</span></span>

## <a name="manage-permissions"></a><span data-ttu-id="55a59-125">Управление разрешениями</span><span class="sxs-lookup"><span data-stu-id="55a59-125">Manage permissions</span></span>

<span data-ttu-id="55a59-126">Пользователь может управлять разрешениями устройств в параметрах  Teams, выбрав **разрешить** или запретить разрешения для определенных приложений.</span><span class="sxs-lookup"><span data-stu-id="55a59-126">A user can manage device permissions in Teams settings by selecting **Allow** or **Deny** permissions to specific apps.</span></span>
 
# <a name="desktop"></a>[<span data-ttu-id="55a59-127">Desktop</span><span class="sxs-lookup"><span data-stu-id="55a59-127">Desktop</span></span>](#tab/desktop)

1. <span data-ttu-id="55a59-128">Откройте приложение Teams.</span><span class="sxs-lookup"><span data-stu-id="55a59-128">Open your Teams app.</span></span>
1. <span data-ttu-id="55a59-129">Выберите значок профиля в правом верхнем углу окна.</span><span class="sxs-lookup"><span data-stu-id="55a59-129">Select your profile icon in the upper right corner of the window.</span></span>
1. <span data-ttu-id="55a59-130">Выберите **Параметры**  >  **Разрешений** из выпадаемого меню.</span><span class="sxs-lookup"><span data-stu-id="55a59-130">Select **Settings** > **Permissions** from the drop-down menu.</span></span>
1. <span data-ttu-id="55a59-131">Выберите нужные параметры.</span><span class="sxs-lookup"><span data-stu-id="55a59-131">Select your desired settings.</span></span>

   ![Экран параметров настольных компьютеров разрешений устройств](../../assets/images/tabs/device-permissions.png)

# <a name="mobile"></a>[<span data-ttu-id="55a59-133">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="55a59-133">Mobile</span></span>](#tab/mobile)

1. <span data-ttu-id="55a59-134">Open Teams.</span><span class="sxs-lookup"><span data-stu-id="55a59-134">Open Teams.</span></span>
1. <span data-ttu-id="55a59-135">Перейдите **к настройкам**  >  **разрешений приложения**.</span><span class="sxs-lookup"><span data-stu-id="55a59-135">Go to **Settings** > **App Permissions**.</span></span>
1. <span data-ttu-id="55a59-136">Выберите приложение, для которого необходимо выбрать параметры.</span><span class="sxs-lookup"><span data-stu-id="55a59-136">Select the app for which you need to choose the settings.</span></span>
1. <span data-ttu-id="55a59-137">Выберите нужные параметры.</span><span class="sxs-lookup"><span data-stu-id="55a59-137">Select your desired settings.</span></span>

    ![Экран разрешений мобильных параметров устройства](../../assets/images/tabs/MobilePermissions.png)

---

## <a name="specify-permissions"></a><span data-ttu-id="55a59-139">Указание разрешений</span><span class="sxs-lookup"><span data-stu-id="55a59-139">Specify permissions</span></span>

<span data-ttu-id="55a59-140">Обновите приложение, добавив и укажите, какие из пяти свойств вы `manifest.json` `devicePermissions` используете в приложении:</span><span class="sxs-lookup"><span data-stu-id="55a59-140">Update your app's `manifest.json` by adding `devicePermissions` and specifying which of the five properties that you use in your application:</span></span>

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```

<span data-ttu-id="55a59-141">Каждое свойство позволяет задать пользователю запрос на его согласие:</span><span class="sxs-lookup"><span data-stu-id="55a59-141">Each property allows you to prompt the user to ask for their consent:</span></span>

| <span data-ttu-id="55a59-142">Свойство</span><span class="sxs-lookup"><span data-stu-id="55a59-142">Property</span></span>      | <span data-ttu-id="55a59-143">Описание</span><span class="sxs-lookup"><span data-stu-id="55a59-143">Description</span></span>   |
| --- | --- |
| <span data-ttu-id="55a59-144">мультимедиа</span><span class="sxs-lookup"><span data-stu-id="55a59-144">media</span></span>         | <span data-ttu-id="55a59-145">Разрешение на использование камеры, микрофона, динамиков и доступа к медиа-галерее.</span><span class="sxs-lookup"><span data-stu-id="55a59-145">Permission to use the camera, microphone, speakers, and access media gallery.</span></span> |
| <span data-ttu-id="55a59-146">геолокация</span><span class="sxs-lookup"><span data-stu-id="55a59-146">geolocation</span></span>   | <span data-ttu-id="55a59-147">Разрешение на возвращение расположения пользователя.</span><span class="sxs-lookup"><span data-stu-id="55a59-147">Permission to return the user's location.</span></span>      |
| <span data-ttu-id="55a59-148">уведомления</span><span class="sxs-lookup"><span data-stu-id="55a59-148">notifications</span></span> | <span data-ttu-id="55a59-149">Разрешение на отправку уведомлений пользователя.</span><span class="sxs-lookup"><span data-stu-id="55a59-149">Permission to send the user notifications.</span></span>      |
| <span data-ttu-id="55a59-150">midi</span><span class="sxs-lookup"><span data-stu-id="55a59-150">midi</span></span>          | <span data-ttu-id="55a59-151">Разрешение на отправку и получение сведений о цифровом интерфейсе музыкальных инструментов (MIDI) с цифрового музыкального инструмента.</span><span class="sxs-lookup"><span data-stu-id="55a59-151">Permission to send and receive  Musical Instrument Digital Interface (MIDI) information from a digital musical instrument.</span></span>   |
| <span data-ttu-id="55a59-152">openExternal</span><span class="sxs-lookup"><span data-stu-id="55a59-152">openExternal</span></span>  | <span data-ttu-id="55a59-153">Разрешение на открытие ссылок во внешних приложениях.</span><span class="sxs-lookup"><span data-stu-id="55a59-153">Permission to open links in external applications.</span></span>  |

## <a name="check-permissions-from-your-app"></a><span data-ttu-id="55a59-154">Проверка разрешений из приложения</span><span class="sxs-lookup"><span data-stu-id="55a59-154">Check permissions from your app</span></span>

<span data-ttu-id="55a59-155">После добавления в манифест приложения проверьте разрешения с помощью `devicePermissions` **API разрешений HTML5** без запроса:</span><span class="sxs-lookup"><span data-stu-id="55a59-155">After adding `devicePermissions` to your app manifest, check permissions using the **HTML5 permissions API** without causing a prompt:</span></span>

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

## <a name="use-teams-apis-to-get-device-permissions"></a><span data-ttu-id="55a59-156">Использование API Teams для получения разрешений на устройства</span><span class="sxs-lookup"><span data-stu-id="55a59-156">Use Teams APIs to get device permissions</span></span>

<span data-ttu-id="55a59-157">Используйте соответствующий API HTML5 или Teams, чтобы отобразить подсказку для получения согласия на доступ к разрешениям устройств.</span><span class="sxs-lookup"><span data-stu-id="55a59-157">Leverage appropriate HTML5 or Teams API, to display a prompt for getting consent to access device permissions.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="55a59-158">Поддержка `camera` , `gallery` и включен через `microphone` [**selectMedia API**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="55a59-158">Support for `camera`, `gallery`, and `microphone` is enabled through [**selectMedia API**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true).</span></span> <span data-ttu-id="55a59-159">Используйте [**API captureImage**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) для одного захвата изображения.</span><span class="sxs-lookup"><span data-stu-id="55a59-159">Use [**captureImage API**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) for a single image capture.</span></span>
> * <span data-ttu-id="55a59-160">Поддержка `location` включена через [**API getLocation.**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="55a59-160">Support for `location` is enabled through [**getLocation API**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true).</span></span> <span data-ttu-id="55a59-161">Это необходимо использовать для расположения, так как API геолокации HTML5 в настоящее время не полностью поддерживается `getLocation API` на настольном клиенте Teams.</span><span class="sxs-lookup"><span data-stu-id="55a59-161">You must use this `getLocation API` for location, as HTML5 geolocation API is currently not fully supported on Teams desktop client.</span></span>

<span data-ttu-id="55a59-162">Например:</span><span class="sxs-lookup"><span data-stu-id="55a59-162">For example:</span></span>
 * <span data-ttu-id="55a59-163">Чтобы подсказыть пользователю доступ к их расположению, необходимо `getCurrentPosition()` вызвать:</span><span class="sxs-lookup"><span data-stu-id="55a59-163">To prompt the user to access their location you must call `getCurrentPosition()`:</span></span>

    ```Javascript
    navigator.geolocation.getCurrentPosition    (function (position) { /*... */ });
    ```

 * <span data-ttu-id="55a59-164">Чтобы подсказыть пользователю доступ к камере на рабочем столе или в Интернете, необходимо `getUserMedia()` вызвать:</span><span class="sxs-lookup"><span data-stu-id="55a59-164">To prompt the user to access their camera on desktop or web you must call `getUserMedia()`:</span></span>

    ```Javascript
    navigator.mediaDevices.getUserMedia({ audio: true, video: true });
    ```

 * <span data-ttu-id="55a59-165">Чтобы захватить изображение на мобильном телефоне, teams mobile просит разрешения при `captureImage()` вызове:</span><span class="sxs-lookup"><span data-stu-id="55a59-165">To capture the image on mobile, Teams mobile asks for permission when you call `captureImage()`:</span></span>

    ```Javascript
    microsoftTeams.media.captureImage((error: microsoftTeams.SdkError, files: microsoftTeams.media.File[]) => {
      /* ... */
    });
    ```

 * <span data-ttu-id="55a59-166">Уведомления подскажут пользователю при `requestPermission()` вызове:</span><span class="sxs-lookup"><span data-stu-id="55a59-166">Notifications will prompt the user when you call `requestPermission()`:</span></span>

    ```Javascript
    Notification.requestPermission(function(result) { /* ... */ });
    ```




* <span data-ttu-id="55a59-167">Чтобы использовать камеру или доступ к фотогалерее, teams mobile просит разрешения при `selectMedia()` вызове:</span><span class="sxs-lookup"><span data-stu-id="55a59-167">To use the camera or access photo gallery, Teams mobile asks permission when you call `selectMedia()`:</span></span>

    ```JavaScript
    microsoftTeams.media.selectMedia({ maxMediaCount: 10, mediaType: microsoftTeams.media.MediaType.Image }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    );
    ```

* <span data-ttu-id="55a59-168">Чтобы использовать микрофон, teams mobile запросит разрешение при `selectMedia()` вызове:</span><span class="sxs-lookup"><span data-stu-id="55a59-168">To use the microphone, Teams mobile asks permission when you call `selectMedia()`:</span></span>

    ```JavaScript 
    microsoftTeams.media.selectMedia({ maxMediaCount: 1, mediaType: microsoftTeams.media.MediaType.Audio }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    });
    ```

* <span data-ttu-id="55a59-169">Чтобы побудить пользователя к совместному расположению в интерфейсе карты, teams mobile запросит разрешение при `getLocation()` вызове:</span><span class="sxs-lookup"><span data-stu-id="55a59-169">To prompt the user to share location on the map interface, Teams mobile asks permission when you call `getLocation()`:</span></span>

    ```JavaScript 
    microsoftTeams.location.getLocation({ allowChooseLocation: true, showMap: true }, (error: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
      /* ... *
    /});
    ```
# <a name="desktop"></a>[<span data-ttu-id="55a59-170">Desktop</span><span class="sxs-lookup"><span data-stu-id="55a59-170">Desktop</span></span>](#tab/desktop)

   ![Запрос разрешений на настольные устройства tabs](~/assets/images/tabs/device-permissions-prompt.png)

# <a name="mobile"></a>[<span data-ttu-id="55a59-172">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="55a59-172">Mobile</span></span>](#tab/mobile)

   ![Запрос разрешений мобильных устройств Tabs](../../assets/images/tabs/MobileLocationPermission.png)

* * * 

## <a name="permission-behavior-across-login-sessions"></a><span data-ttu-id="55a59-174">Поведение разрешений в сеансах входа</span><span class="sxs-lookup"><span data-stu-id="55a59-174">Permission behavior across login sessions</span></span>

<span data-ttu-id="55a59-175">Разрешения устройства хранятся для каждого сеанса входа.</span><span class="sxs-lookup"><span data-stu-id="55a59-175">Device permissions are stored for every login session.</span></span> <span data-ttu-id="55a59-176">Это означает, что при входе в другой экземпляр Teams, например, на другом компьютере, разрешения на устройство с предыдущих сеансов недоступны.</span><span class="sxs-lookup"><span data-stu-id="55a59-176">It means that if you sign in to another instance of Teams, for example, on another computer, your device permissions from your previous sessions are not available.</span></span> <span data-ttu-id="55a59-177">Поэтому необходимо повторно согласиться на разрешения устройств для нового сеанса.</span><span class="sxs-lookup"><span data-stu-id="55a59-177">Therefore, you must re-consent to device permissions for the new session.</span></span> <span data-ttu-id="55a59-178">Это также означает, что если вы выходите из Teams или переключате клиентов в Teams, разрешения устройства удаляются из предыдущего сеанса входа.</span><span class="sxs-lookup"><span data-stu-id="55a59-178">It also means, if you sign out of Teams or switch tenants in Teams, your device permissions are deleted from the previous login session.</span></span>  

> [!NOTE]
> <span data-ttu-id="55a59-179">Если вы даете согласие на разрешения на родном устройстве, оно допустимо только для _текущего_ сеанса входа.</span><span class="sxs-lookup"><span data-stu-id="55a59-179">When you consent to the native device permissions, it is valid only for your _current_ login session.</span></span>

## <a name="next-steps"></a><span data-ttu-id="55a59-180">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="55a59-180">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="55a59-181">Интеграция возможностей мультимедиа в Teams</span><span class="sxs-lookup"><span data-stu-id="55a59-181">Integrate media capabilities in Teams</span></span>](mobile-camera-image-permissions.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="55a59-182">Интеграция функций сканера QR или штрихкодов в Teams</span><span class="sxs-lookup"><span data-stu-id="55a59-182">Integrate QR or barcode scanner capability in Teams</span></span>](qr-barcode-scanner-capability.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="55a59-183">Интеграция возможностей расположения в Teams</span><span class="sxs-lookup"><span data-stu-id="55a59-183">Integrate location capabilities in Teams</span></span>](location-capability.md)
