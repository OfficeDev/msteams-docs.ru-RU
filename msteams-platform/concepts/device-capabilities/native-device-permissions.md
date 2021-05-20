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
# <a name="request-device-permissions-for-your-microsoft-teams-app"></a><span data-ttu-id="63e94-104">Запрос разрешений устройства для вашего Microsoft Teams приложения</span><span class="sxs-lookup"><span data-stu-id="63e94-104">Request device permissions for your Microsoft Teams app</span></span>

<span data-ttu-id="63e94-105">Вы можете обогатить Teams с помощью родных возможностей устройства, таких как камера, микрофон и местоположение.</span><span class="sxs-lookup"><span data-stu-id="63e94-105">You can enrich your Teams app with native device capabilities, such as camera, microphone, and location.</span></span> <span data-ttu-id="63e94-106">Этот документ поможет вам запросить согласие пользователя и получить доступ к разрешениям на родных устройств.</span><span class="sxs-lookup"><span data-stu-id="63e94-106">This document guides you on how to request user consent and access the native device permissions.</span></span>

> [!NOTE]
> * <span data-ttu-id="63e94-107">Чтобы интегрировать возможности мультимедиа в Microsoft Teams [](mobile-camera-image-permissions.md)приложении, см.</span><span class="sxs-lookup"><span data-stu-id="63e94-107">To integrate media capabilities within your Microsoft Teams mobile app, see [Integrate media capabilities](mobile-camera-image-permissions.md).</span></span>
> * <span data-ttu-id="63e94-108">Чтобы интегрировать возможности сканера штрих-кодов в Microsoft Teams [Teams](qr-barcode-scanner-capability.md)мобильное приложение, см.</span><span class="sxs-lookup"><span data-stu-id="63e94-108">To integrate QR or barcode scanner capability within your Microsoft Teams mobile app, see [Integrate QR or barcode scanner capability in Teams](qr-barcode-scanner-capability.md).</span></span>
> * <span data-ttu-id="63e94-109">Чтобы интегрировать возможности определения местоположения в [](location-capability.md)Microsoft Teams приложении, см.</span><span class="sxs-lookup"><span data-stu-id="63e94-109">To integrate location capabilities within your Microsoft Teams mobile app, see [Integrate location capabilities](location-capability.md).</span></span>

## <a name="native-device-permissions"></a><span data-ttu-id="63e94-110">Разрешения на родные устройства</span><span class="sxs-lookup"><span data-stu-id="63e94-110">Native device permissions</span></span>

<span data-ttu-id="63e94-111">Необходимо запросить разрешение устройства на доступ к возможностям родных устройств.</span><span class="sxs-lookup"><span data-stu-id="63e94-111">You must request the device permissions to access native device capabilities.</span></span> <span data-ttu-id="63e94-112">Разрешения устройства работают одинаково для всех конструкций приложений, таких как вкладки, модули задач или расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="63e94-112">The device permissions work similarly for all app constructs, such as tabs, task modules, or messaging extensions.</span></span> <span data-ttu-id="63e94-113">Пользователь должен перейти на страницу разрешений в Teams для управления разрешениями устройств.</span><span class="sxs-lookup"><span data-stu-id="63e94-113">The user must go to the permissions page in Teams settings to manage device permissions.</span></span>
<span data-ttu-id="63e94-114">Доступ к возможностям устройства позволяет создавать более богатые возможности на Teams, например:</span><span class="sxs-lookup"><span data-stu-id="63e94-114">By accessing the device capabilities, you can build richer experiences on the Teams platform, such as:</span></span>
* <span data-ttu-id="63e94-115">Захват и просмотр изображений.</span><span class="sxs-lookup"><span data-stu-id="63e94-115">Capture and view images.</span></span>
* <span data-ttu-id="63e94-116">Сканирование qR или штрих-кода.</span><span class="sxs-lookup"><span data-stu-id="63e94-116">Scan QR or barcode.</span></span>
* <span data-ttu-id="63e94-117">Запись и доля коротких видео.</span><span class="sxs-lookup"><span data-stu-id="63e94-117">Record and share short videos.</span></span>
* <span data-ttu-id="63e94-118">Запись аудио-памяток и сохранить их для более длительного использования.</span><span class="sxs-lookup"><span data-stu-id="63e94-118">Record audio memos and save them for later use.</span></span>
* <span data-ttu-id="63e94-119">Используйте информацию о местоположении пользователя для отображения соответствующей информации.</span><span class="sxs-lookup"><span data-stu-id="63e94-119">Use the location information of the user to display relevant information.</span></span>

## <a name="access-device-permissions"></a><span data-ttu-id="63e94-120">Разрешения на доступ к устройствам</span><span class="sxs-lookup"><span data-stu-id="63e94-120">Access device permissions</span></span>

<span data-ttu-id="63e94-121">Клиент [Microsoft Teams JavaScript SDK предоставляет](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) инструменты, необходимые для вашего Teams мобильного приложения для доступа к [разрешениям устройства пользователя](#manage-permissions) и создания более богатого опыта.</span><span class="sxs-lookup"><span data-stu-id="63e94-121">The [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) provides the tools necessary for your Teams mobile app to access the user’s [device permissions](#manage-permissions) and build a richer experience.</span></span>

<span data-ttu-id="63e94-122">Хотя доступ к этим функциям является стандартным в современных веб-браузерах, вы должны сообщить Teams об особенностях, которые вы используете, обновляя манифест приложения.</span><span class="sxs-lookup"><span data-stu-id="63e94-122">While access to these features is standard in modern web browsers, you must inform Teams about the features you use by updating your app manifest.</span></span> <span data-ttu-id="63e94-123">Это обновление позволяет запрашивать разрешения, пока приложение работает на Teams столе.</span><span class="sxs-lookup"><span data-stu-id="63e94-123">This update allows you to ask for permissions while your app runs on the Teams desktop client.</span></span>

> [!NOTE] 
> <span data-ttu-id="63e94-124">В настоящее Microsoft Teams поддержка возможностей мультимедиа и возможности сканирования штрих-кодов доступны только для мобильных клиентов.</span><span class="sxs-lookup"><span data-stu-id="63e94-124">Currently, Microsoft Teams support for media capabilities and QR barcode scanner capability is only available for mobile clients.</span></span>

## <a name="manage-permissions"></a><span data-ttu-id="63e94-125">Управление разрешениями</span><span class="sxs-lookup"><span data-stu-id="63e94-125">Manage permissions</span></span>

<span data-ttu-id="63e94-126">Пользователь может управлять разрешениями устройств в Teams настройками, выбирая **разрешения Allow** **или Deny** для определенных приложений.</span><span class="sxs-lookup"><span data-stu-id="63e94-126">A user can manage device permissions in Teams settings by selecting **Allow** or **Deny** permissions to specific apps.</span></span>
 
# <a name="desktop"></a>[<span data-ttu-id="63e94-127">Desktop</span><span class="sxs-lookup"><span data-stu-id="63e94-127">Desktop</span></span>](#tab/desktop)

1. <span data-ttu-id="63e94-128">Откройте приложение Teams для детей.</span><span class="sxs-lookup"><span data-stu-id="63e94-128">Open your Teams app.</span></span>
1. <span data-ttu-id="63e94-129">Выберите значок профиля в правом верхнем углу окна.</span><span class="sxs-lookup"><span data-stu-id="63e94-129">Select your profile icon in the upper right corner of the window.</span></span>
1. <span data-ttu-id="63e94-130">Выберите **Параметры**  >  **разрешения** из выпадают из меню.</span><span class="sxs-lookup"><span data-stu-id="63e94-130">Select **Settings** > **Permissions** from the drop-down menu.</span></span>
1. <span data-ttu-id="63e94-131">Выберите нужные настройки.</span><span class="sxs-lookup"><span data-stu-id="63e94-131">Select your desired settings.</span></span>

   ![Экран настроек настольных настроек устройств](../../assets/images/tabs/device-permissions.png)

# <a name="mobile"></a>[<span data-ttu-id="63e94-133">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="63e94-133">Mobile</span></span>](#tab/mobile)

1. <span data-ttu-id="63e94-134">Открытый Teams.</span><span class="sxs-lookup"><span data-stu-id="63e94-134">Open Teams.</span></span>
1. <span data-ttu-id="63e94-135">Перейти **к Параметры** App  >  **Разрешения**.</span><span class="sxs-lookup"><span data-stu-id="63e94-135">Go to **Settings** > **App Permissions**.</span></span>
1. <span data-ttu-id="63e94-136">Выберите приложение, для которого необходимо выбрать настройки.</span><span class="sxs-lookup"><span data-stu-id="63e94-136">Select the app for which you need to choose the settings.</span></span>
1. <span data-ttu-id="63e94-137">Выберите нужные настройки.</span><span class="sxs-lookup"><span data-stu-id="63e94-137">Select your desired settings.</span></span>

    ![Экран разрешений устройства на мобильные настройки](../../assets/images/tabs/MobilePermissions.png)

---

## <a name="specify-permissions"></a><span data-ttu-id="63e94-139">Указать разрешения</span><span class="sxs-lookup"><span data-stu-id="63e94-139">Specify permissions</span></span>

<span data-ttu-id="63e94-140">Обновите приложение, `manifest.json` добавив и `devicePermissions` указав, какие из пяти свойств, которые вы используете в приложении:</span><span class="sxs-lookup"><span data-stu-id="63e94-140">Update your app's `manifest.json` by adding `devicePermissions` and specifying which of the five properties that you use in your application:</span></span>

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```

<span data-ttu-id="63e94-141">Каждое свойство позволяет побудить пользователя запросить их согласие:</span><span class="sxs-lookup"><span data-stu-id="63e94-141">Each property allows you to prompt the user to ask for their consent:</span></span>

| <span data-ttu-id="63e94-142">Свойство</span><span class="sxs-lookup"><span data-stu-id="63e94-142">Property</span></span>      | <span data-ttu-id="63e94-143">Описание</span><span class="sxs-lookup"><span data-stu-id="63e94-143">Description</span></span>   |
| --- | --- |
| <span data-ttu-id="63e94-144">media</span><span class="sxs-lookup"><span data-stu-id="63e94-144">media</span></span>         | <span data-ttu-id="63e94-145">Разрешение на использование камеры, микрофона, динамиков и медиагалереи доступа.</span><span class="sxs-lookup"><span data-stu-id="63e94-145">Permission to use the camera, microphone, speakers, and access media gallery.</span></span> |
| <span data-ttu-id="63e94-146">геолокация</span><span class="sxs-lookup"><span data-stu-id="63e94-146">geolocation</span></span>   | <span data-ttu-id="63e94-147">Разрешение на возврат местоположения пользователя.</span><span class="sxs-lookup"><span data-stu-id="63e94-147">Permission to return the user's location.</span></span>      |
| <span data-ttu-id="63e94-148">Уведомления</span><span class="sxs-lookup"><span data-stu-id="63e94-148">notifications</span></span> | <span data-ttu-id="63e94-149">Разрешение на отправку уведомлений пользователя.</span><span class="sxs-lookup"><span data-stu-id="63e94-149">Permission to send the user notifications.</span></span>      |
| <span data-ttu-id="63e94-150">миди</span><span class="sxs-lookup"><span data-stu-id="63e94-150">midi</span></span>          | <span data-ttu-id="63e94-151">Разрешение на отправку и получение информации о музыкальном инструменте Digital Interface (MIDI) с цифрового музыкального инструмента.</span><span class="sxs-lookup"><span data-stu-id="63e94-151">Permission to send and receive  Musical Instrument Digital Interface (MIDI) information from a digital musical instrument.</span></span>   |
| <span data-ttu-id="63e94-152">openExternal</span><span class="sxs-lookup"><span data-stu-id="63e94-152">openExternal</span></span>  | <span data-ttu-id="63e94-153">Разрешение на открытие ссылок во внешних приложениях.</span><span class="sxs-lookup"><span data-stu-id="63e94-153">Permission to open links in external applications.</span></span>  |

## <a name="check-permissions-from-your-app"></a><span data-ttu-id="63e94-154">Проверка разрешений из приложения</span><span class="sxs-lookup"><span data-stu-id="63e94-154">Check permissions from your app</span></span>

<span data-ttu-id="63e94-155">После добавления `devicePermissions` в манифест приложения проверьте разрешения с помощью **API разрешений HTML5,** не вызывая подсказки:</span><span class="sxs-lookup"><span data-stu-id="63e94-155">After adding `devicePermissions` to your app manifest, check permissions using the **HTML5 permissions API** without causing a prompt:</span></span>

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

## <a name="use-teams-apis-to-get-device-permissions"></a><span data-ttu-id="63e94-156">Используйте Teams API для получения разрешений на устройства</span><span class="sxs-lookup"><span data-stu-id="63e94-156">Use Teams APIs to get device permissions</span></span>

<span data-ttu-id="63e94-157">Используйте соответствующие HTML5 Teams API для отображения подсказки для получения согласия на доступ к разрешениям устройства.</span><span class="sxs-lookup"><span data-stu-id="63e94-157">Leverage appropriate HTML5 or Teams API, to display a prompt for getting consent to access device permissions.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="63e94-158">Поддержка `camera` , и включен через `gallery` `microphone` [**selectMedia API**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="63e94-158">Support for `camera`, `gallery`, and `microphone` is enabled through [**selectMedia API**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true).</span></span> <span data-ttu-id="63e94-159">Используйте [**API captureImage**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) для одного захвата изображения.</span><span class="sxs-lookup"><span data-stu-id="63e94-159">Use [**captureImage API**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) for a single image capture.</span></span>
> * <span data-ttu-id="63e94-160">Поддержка `location` включена через [**GETLocation API**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="63e94-160">Support for `location` is enabled through [**getLocation API**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true).</span></span> <span data-ttu-id="63e94-161">Вы должны использовать это для `getLocation API` определения местоположения, так как HTML5 геолокационный API в настоящее время не полностью поддерживается Teams настольного клиента.</span><span class="sxs-lookup"><span data-stu-id="63e94-161">You must use this `getLocation API` for location, as HTML5 geolocation API is currently not fully supported on Teams desktop client.</span></span>

<span data-ttu-id="63e94-162">Пример:</span><span class="sxs-lookup"><span data-stu-id="63e94-162">For example:</span></span>
 * <span data-ttu-id="63e94-163">Чтобы побудить пользователя получить доступ к своему местоположению, необходимо `getCurrentPosition()` позвонить:</span><span class="sxs-lookup"><span data-stu-id="63e94-163">To prompt the user to access their location you must call `getCurrentPosition()`:</span></span>

    ```Javascript
    navigator.geolocation.getCurrentPosition    (function (position) { /*... */ });
    ```

 * <span data-ttu-id="63e94-164">Чтобы побудить пользователя получить доступ к камере на рабочем столе или в Интернете, вы должны `getUserMedia()` позвонить:</span><span class="sxs-lookup"><span data-stu-id="63e94-164">To prompt the user to access their camera on desktop or web you must call `getUserMedia()`:</span></span>

    ```Javascript
    navigator.mediaDevices.getUserMedia({ audio: true, video: true });
    ```

 * <span data-ttu-id="63e94-165">Чтобы запечатлеть изображение на мобильном телефоне, Teams мобильный телефон запрашивает разрешение при `captureImage()` вызове:</span><span class="sxs-lookup"><span data-stu-id="63e94-165">To capture the image on mobile, Teams mobile asks for permission when you call `captureImage()`:</span></span>

    ```Javascript
    microsoftTeams.media.captureImage((error: microsoftTeams.SdkError, files: microsoftTeams.media.File[]) => {
      /* ... */
    });
    ```

 * <span data-ttu-id="63e94-166">Уведомления подскажут пользователю при `requestPermission()` вызове:</span><span class="sxs-lookup"><span data-stu-id="63e94-166">Notifications will prompt the user when you call `requestPermission()`:</span></span>

    ```Javascript
    Notification.requestPermission(function(result) { /* ... */ });
    ```




* <span data-ttu-id="63e94-167">Чтобы использовать камеру или доступ к фотогалерее, Teams мобильный запрашивает разрешение при `selectMedia()` вызове:</span><span class="sxs-lookup"><span data-stu-id="63e94-167">To use the camera or access photo gallery, Teams mobile asks permission when you call `selectMedia()`:</span></span>

    ```JavaScript
    microsoftTeams.media.selectMedia({ maxMediaCount: 10, mediaType: microsoftTeams.media.MediaType.Image }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    );
    ```

* <span data-ttu-id="63e94-168">Чтобы использовать микрофон, Teams запрашивает разрешение при `selectMedia()` вызове:</span><span class="sxs-lookup"><span data-stu-id="63e94-168">To use the microphone, Teams mobile asks permission when you call `selectMedia()`:</span></span>

    ```JavaScript 
    microsoftTeams.media.selectMedia({ maxMediaCount: 1, mediaType: microsoftTeams.media.MediaType.Audio }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    });
    ```

* <span data-ttu-id="63e94-169">Чтобы побудить пользователя поделиться местоположением на интерфейсе карты, Teams запрашивает разрешение при `getLocation()` вызове:</span><span class="sxs-lookup"><span data-stu-id="63e94-169">To prompt the user to share location on the map interface, Teams mobile asks permission when you call `getLocation()`:</span></span>

    ```JavaScript 
    microsoftTeams.location.getLocation({ allowChooseLocation: true, showMap: true }, (error: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
      /* ... *
    /});
    ```
# <a name="desktop"></a>[<span data-ttu-id="63e94-170">Desktop</span><span class="sxs-lookup"><span data-stu-id="63e94-170">Desktop</span></span>](#tab/desktop)

   ![Tabs разрешения настольных устройств подсказка](~/assets/images/tabs/device-permissions-prompt.png)

# <a name="mobile"></a>[<span data-ttu-id="63e94-172">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="63e94-172">Mobile</span></span>](#tab/mobile)

   ![Tabs разрешения мобильных устройств подсказка](../../assets/images/tabs/MobileLocationPermission.png)

* * * 

## <a name="permission-behavior-across-login-sessions"></a><span data-ttu-id="63e94-174">Поведение разрешения во всех сеансах входа</span><span class="sxs-lookup"><span data-stu-id="63e94-174">Permission behavior across login sessions</span></span>

<span data-ttu-id="63e94-175">Разрешения устройств хранятся для каждого сеанса входа.</span><span class="sxs-lookup"><span data-stu-id="63e94-175">Device permissions are stored for every login session.</span></span> <span data-ttu-id="63e94-176">Это означает, что если вы войдюете в другой экземпляр Teams, например, на другом компьютере, разрешения на устройство с предыдущих сеансов недоступны.</span><span class="sxs-lookup"><span data-stu-id="63e94-176">It means that if you sign in to another instance of Teams, for example, on another computer, your device permissions from your previous sessions are not available.</span></span> <span data-ttu-id="63e94-177">Поэтому необходимо повторно дать согласие на разрешение устройства на новую сессию.</span><span class="sxs-lookup"><span data-stu-id="63e94-177">Therefore, you must re-consent to device permissions for the new session.</span></span> <span data-ttu-id="63e94-178">Это также означает, что, если вы Teams или переключиться на Teams, разрешения на устройство удаляются из предыдущей сессии входа.</span><span class="sxs-lookup"><span data-stu-id="63e94-178">It also means, if you sign out of Teams or switch tenants in Teams, your device permissions are deleted from the previous login session.</span></span>  

> [!NOTE]
> <span data-ttu-id="63e94-179">При согласии на разрешение на использование родных устройств оно действует только для текущей _сессии_ входа.</span><span class="sxs-lookup"><span data-stu-id="63e94-179">When you consent to the native device permissions, it is valid only for your _current_ login session.</span></span>

## <a name="next-steps"></a><span data-ttu-id="63e94-180">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="63e94-180">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="63e94-181">Интеграция медиа-возможностей в Teams</span><span class="sxs-lookup"><span data-stu-id="63e94-181">Integrate media capabilities in Teams</span></span>](mobile-camera-image-permissions.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="63e94-182">Интеграция возможностей сканера qR или штрих-кодов в Teams</span><span class="sxs-lookup"><span data-stu-id="63e94-182">Integrate QR or barcode scanner capability in Teams</span></span>](qr-barcode-scanner-capability.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="63e94-183">Интеграция возможностей определения местоположения в Teams</span><span class="sxs-lookup"><span data-stu-id="63e94-183">Integrate location capabilities in Teams</span></span>](location-capability.md)
