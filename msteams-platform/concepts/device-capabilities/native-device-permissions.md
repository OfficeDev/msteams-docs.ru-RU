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
# <a name="request-device-permissions-for-your-microsoft-teams-app"></a><span data-ttu-id="34dff-104">Запрос разрешений устройства для приложения Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="34dff-104">Request device permissions for your Microsoft Teams app</span></span>

<span data-ttu-id="34dff-105">Вы можете обогатить свое приложение Teams встроенными возможностями устройства, такими как камера, микрофон и расположение.</span><span class="sxs-lookup"><span data-stu-id="34dff-105">You can enrich your Teams app with native device capabilities, such as camera, microphone, and location.</span></span> <span data-ttu-id="34dff-106">В этом документе содержится руководство по запросу согласия пользователя и доступу к разрешениям на доступ к устройствам.</span><span class="sxs-lookup"><span data-stu-id="34dff-106">This document guides you on how to request user consent and access the native device permissions.</span></span>

> [!NOTE]
> <span data-ttu-id="34dff-107">Чтобы интегрировать возможности мультимедиа в мобильном приложении Microsoft Teams, см. ["Интеграция возможностей мультимедиа".](mobile-camera-image-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="34dff-107">To integrate media capabilities within your Microsoft Teams mobile app, see [Integrate media capabilities](mobile-camera-image-permissions.md).</span></span>

## <a name="native-device-permissions"></a><span data-ttu-id="34dff-108">Разрешения для нативных устройств</span><span class="sxs-lookup"><span data-stu-id="34dff-108">Native device permissions</span></span>

<span data-ttu-id="34dff-109">Необходимо запросить разрешения устройства для доступа к возможностям нативных устройств.</span><span class="sxs-lookup"><span data-stu-id="34dff-109">You must request the device permissions to access native device capabilities.</span></span> <span data-ttu-id="34dff-110">Разрешения устройства работают аналогично для всех конструкций приложения, таких как вкладки, модули задач или расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="34dff-110">The device permissions work similarly for all app constructs, such as tabs, task modules, or messaging extensions.</span></span> <span data-ttu-id="34dff-111">Чтобы управлять разрешениями устройств, пользователь должен перейти на страницу разрешений в параметрах Teams.</span><span class="sxs-lookup"><span data-stu-id="34dff-111">The user must go to the permissions page in Teams settings to manage device permissions.</span></span>
<span data-ttu-id="34dff-112">Доступ к возможностям устройств позволяет создавать на платформе Teams более богатые возможности, например:</span><span class="sxs-lookup"><span data-stu-id="34dff-112">By accessing the device capabilities, you can build richer experiences on the Teams platform, such as:</span></span>
* <span data-ttu-id="34dff-113">Захват и просмотр изображений.</span><span class="sxs-lookup"><span data-stu-id="34dff-113">Capture and view images.</span></span>
* <span data-ttu-id="34dff-114">Записывать короткие видеоролики и делиться ими.</span><span class="sxs-lookup"><span data-stu-id="34dff-114">Record and share short videos.</span></span>
* <span data-ttu-id="34dff-115">Зафиксировать звуковые memos и сохранить их для использования в дальнейшем.</span><span class="sxs-lookup"><span data-stu-id="34dff-115">Record audio memos and save them for later use.</span></span>
* <span data-ttu-id="34dff-116">Используйте сведения о расположении пользователя для отображения соответствующей информации.</span><span class="sxs-lookup"><span data-stu-id="34dff-116">Use the location information of the user to display relevant information.</span></span>

## <a name="access-device-permissions"></a><span data-ttu-id="34dff-117">Доступ к разрешениям устройства</span><span class="sxs-lookup"><span data-stu-id="34dff-117">Access device permissions</span></span>

<span data-ttu-id="34dff-118">Клиентский [SDK JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) для Microsoft Teams предоставляет средства, необходимые [](#manage-permissions) мобильному приложению Teams для доступа к разрешениям устройства пользователя и создания более удобного интерфейса.</span><span class="sxs-lookup"><span data-stu-id="34dff-118">The [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) provides the tools necessary for your Teams mobile app to access the user’s [device permissions](#manage-permissions) and build a richer experience.</span></span>

<span data-ttu-id="34dff-119">Хотя доступ к этим функциям является стандартным в современных веб-браузерах, необходимо сообщить Teams о функции, которые вы используете, обновив манифест приложения.</span><span class="sxs-lookup"><span data-stu-id="34dff-119">While access to these features is standard in modern web browsers, you must inform Teams about the features you use by updating your app manifest.</span></span> <span data-ttu-id="34dff-120">Это обновление позволяет запросить разрешения, пока приложение работает в настольном клиенте Teams.</span><span class="sxs-lookup"><span data-stu-id="34dff-120">This update allows you to ask for permissions while your app runs on the Teams desktop client.</span></span>

> [!NOTE] 
> <span data-ttu-id="34dff-121">В настоящее время поддержка возможностей мультимедиа в Microsoft Teams доступна только для мобильных клиентов.</span><span class="sxs-lookup"><span data-stu-id="34dff-121">Currently, Microsoft Teams support for media capabilities is only available for mobile clients.</span></span>

## <a name="manage-permissions"></a><span data-ttu-id="34dff-122">Управление разрешениями</span><span class="sxs-lookup"><span data-stu-id="34dff-122">Manage permissions</span></span>

<span data-ttu-id="34dff-123">Пользователь может управлять разрешениями устройств в параметрах  Teams, выбирая разрешения "Разрешить" или "Запретить" для определенных приложений. </span><span class="sxs-lookup"><span data-stu-id="34dff-123">A user can manage device permissions in Teams settings by selecting **Allow** or **Deny** permissions to specific apps.</span></span>
 
# <a name="desktop"></a>[<span data-ttu-id="34dff-124">Desktop</span><span class="sxs-lookup"><span data-stu-id="34dff-124">Desktop</span></span>](#tab/desktop)

1. <span data-ttu-id="34dff-125">Откройте приложение Teams.</span><span class="sxs-lookup"><span data-stu-id="34dff-125">Open your Teams app.</span></span>
1. <span data-ttu-id="34dff-126">Выберите значок профиля в правом верхнем углу окна.</span><span class="sxs-lookup"><span data-stu-id="34dff-126">Select your profile icon in the upper right corner of the window.</span></span>
1. <span data-ttu-id="34dff-127">Выберите **"Разрешения**  >  **параметров"** в выпадаемом меню.</span><span class="sxs-lookup"><span data-stu-id="34dff-127">Select **Settings** > **Permissions** from the drop-down menu.</span></span>
1. <span data-ttu-id="34dff-128">Выберите нужные параметры.</span><span class="sxs-lookup"><span data-stu-id="34dff-128">Select your desired settings.</span></span>

   ![Экран параметров рабочего стола для разрешений устройства](../../assets/images/tabs/device-permissions.png)

# <a name="mobile"></a>[<span data-ttu-id="34dff-130">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="34dff-130">Mobile</span></span>](#tab/mobile)

1. <span data-ttu-id="34dff-131">Откройте Teams.</span><span class="sxs-lookup"><span data-stu-id="34dff-131">Open Teams.</span></span>
1. <span data-ttu-id="34dff-132">Go to **Settings**  >  **App Permissions**.</span><span class="sxs-lookup"><span data-stu-id="34dff-132">Go to **Settings** > **App Permissions**.</span></span>
1. <span data-ttu-id="34dff-133">Выберите приложение, для которого необходимо выбрать параметры.</span><span class="sxs-lookup"><span data-stu-id="34dff-133">Select the app for which you need to choose the settings.</span></span>
1. <span data-ttu-id="34dff-134">Выберите нужные параметры.</span><span class="sxs-lookup"><span data-stu-id="34dff-134">Select your desired settings.</span></span>

    ![Экран разрешений устройства для мобильных устройств](../../assets/images/tabs/MobilePermissions.png)

---

## <a name="specify-permissions"></a><span data-ttu-id="34dff-136">Указание разрешений</span><span class="sxs-lookup"><span data-stu-id="34dff-136">Specify permissions</span></span>

<span data-ttu-id="34dff-137">Обновите приложение, добавив и указав, какие из пяти свойств `manifest.json` `devicePermissions` вы используете в приложении:</span><span class="sxs-lookup"><span data-stu-id="34dff-137">Update your app's `manifest.json` by adding `devicePermissions` and specifying which of the five properties that you use in your application:</span></span>

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```

<span data-ttu-id="34dff-138">Каждое свойство позволяет попросить пользователя запросить свое согласие:</span><span class="sxs-lookup"><span data-stu-id="34dff-138">Each property allows you to prompt the user to ask for their consent:</span></span>

| <span data-ttu-id="34dff-139">Свойство</span><span class="sxs-lookup"><span data-stu-id="34dff-139">Property</span></span>      | <span data-ttu-id="34dff-140">Описание</span><span class="sxs-lookup"><span data-stu-id="34dff-140">Description</span></span>   |
| --- | --- |
| <span data-ttu-id="34dff-141">media</span><span class="sxs-lookup"><span data-stu-id="34dff-141">media</span></span>         | <span data-ttu-id="34dff-142">Разрешение на использование камеры, микрофона, динамиков и доступа к коллекции мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="34dff-142">Permission to use the camera, microphone, speakers, and access media gallery.</span></span> |
| <span data-ttu-id="34dff-143">geolocation</span><span class="sxs-lookup"><span data-stu-id="34dff-143">geolocation</span></span>   | <span data-ttu-id="34dff-144">Разрешение на возврат расположения пользователя.</span><span class="sxs-lookup"><span data-stu-id="34dff-144">Permission to return the user's location.</span></span>      |
| <span data-ttu-id="34dff-145">notifications</span><span class="sxs-lookup"><span data-stu-id="34dff-145">notifications</span></span> | <span data-ttu-id="34dff-146">Разрешение на отправку уведомлений пользователя.</span><span class="sxs-lookup"><span data-stu-id="34dff-146">Permission to send the user notifications.</span></span>      |
| <span data-ttu-id="34dff-147">midi</span><span class="sxs-lookup"><span data-stu-id="34dff-147">midi</span></span>          | <span data-ttu-id="34dff-148">Разрешение на отправку и получение сведений о цифровом интерфейсе музыкального инструмента (MIDI) от цифрового музыкального инструмента.</span><span class="sxs-lookup"><span data-stu-id="34dff-148">Permission to send and receive  Musical Instrument Digital Interface (MIDI) information from a digital musical instrument.</span></span>   |
| <span data-ttu-id="34dff-149">openExternal</span><span class="sxs-lookup"><span data-stu-id="34dff-149">openExternal</span></span>  | <span data-ttu-id="34dff-150">Разрешение на открытие ссылок во внешних приложениях.</span><span class="sxs-lookup"><span data-stu-id="34dff-150">Permission to open links in external applications.</span></span>  |

## <a name="check-permissions-from-your-app"></a><span data-ttu-id="34dff-151">Проверка разрешений из приложения</span><span class="sxs-lookup"><span data-stu-id="34dff-151">Check permissions from your app</span></span>

<span data-ttu-id="34dff-152">После добавления в манифест приложения проверьте разрешения с помощью API разрешений `devicePermissions` **HTML5** без запроса:</span><span class="sxs-lookup"><span data-stu-id="34dff-152">After adding `devicePermissions` to your app manifest, check permissions using the **HTML5 permissions API** without causing a prompt:</span></span>

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

## <a name="use-teams-apis-to-get-device-permissions"></a><span data-ttu-id="34dff-153">Использование API Teams для получения разрешений устройства</span><span class="sxs-lookup"><span data-stu-id="34dff-153">Use Teams APIs to get device permissions</span></span>

<span data-ttu-id="34dff-154">Используйте соответствующий API HTML5 или Teams, чтобы отобразить запрос на получение согласия на доступ к разрешениям устройства.</span><span class="sxs-lookup"><span data-stu-id="34dff-154">Leverage appropriate HTML5 or Teams API, to display a prompt for getting consent to access device permissions.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="34dff-155">Поддержка `camera` , `gallery` и `microphone` включена через [**selectMedia API**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="34dff-155">Support for `camera`, `gallery`, and `microphone` is enabled through [**selectMedia API**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true).</span></span> <span data-ttu-id="34dff-156">Используйте [**API captureImage**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) для одного захвата изображения.</span><span class="sxs-lookup"><span data-stu-id="34dff-156">Use [**captureImage API**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) for a single image capture.</span></span>
> * <span data-ttu-id="34dff-157">Поддержка `location` включена через [**API getLocation.**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="34dff-157">Support for `location` is enabled through [**getLocation API**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true).</span></span> <span data-ttu-id="34dff-158">Его необходимо использовать для определения местоположения, так как API географического расположения HTML5 в настоящее время не полностью поддерживается в настольном клиенте `getLocation API` Teams.</span><span class="sxs-lookup"><span data-stu-id="34dff-158">You must use this `getLocation API` for location, as HTML5 geolocation API is currently not fully supported on Teams desktop client.</span></span>

<span data-ttu-id="34dff-159">Например,</span><span class="sxs-lookup"><span data-stu-id="34dff-159">For example:</span></span>
 * <span data-ttu-id="34dff-160">Чтобы у пользователя был доступ к его расположению, необходимо `getCurrentPosition()` вызвать:</span><span class="sxs-lookup"><span data-stu-id="34dff-160">To prompt the user to access their location you must call `getCurrentPosition()`:</span></span>

    ```Javascript
    navigator.geolocation.getCurrentPosition    (function (position) { /*... */ });
    ```

 * <span data-ttu-id="34dff-161">Чтобы у пользователя был доступ к камере на рабочем столе или в Интернете, необходимо `getUserMedia()` вызвать:</span><span class="sxs-lookup"><span data-stu-id="34dff-161">To prompt the user to access their camera on desktop or web you must call `getUserMedia()`:</span></span>

    ```Javascript
    navigator.mediaDevices.getUserMedia({ audio: true, video: true });
    ```

 * <span data-ttu-id="34dff-162">Чтобы захватить изображение на мобильном устройстве, teams mobile запросит разрешение при `captureImage()` вызове:</span><span class="sxs-lookup"><span data-stu-id="34dff-162">To capture the image on mobile, Teams mobile asks for permission when you call `captureImage()`:</span></span>

    ```Javascript
    microsoftTeams.media.captureImage((error: microsoftTeams.SdkError, files: microsoftTeams.media.File[]) => {
      /* ... */
    });
    ```

 * <span data-ttu-id="34dff-163">При вызове уведомлений пользователю будет `requestPermission()` предложено:</span><span class="sxs-lookup"><span data-stu-id="34dff-163">Notifications will prompt the user when you call `requestPermission()`:</span></span>

    ```Javascript
    Notification.requestPermission(function(result) { /* ... */ });
    ```




* <span data-ttu-id="34dff-164">Чтобы использовать камеру или доступ к фотоальбому, Приложение Teams mobile запросит разрешение при `selectMedia()` вызове:</span><span class="sxs-lookup"><span data-stu-id="34dff-164">To use the camera or access photo gallery, Teams mobile asks permission when you call `selectMedia()`:</span></span>

    ```JavaScript
    microsoftTeams.media.selectMedia({ maxMediaCount: 10, mediaType: microsoftTeams.media.MediaType.Image }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    );
    ```

* <span data-ttu-id="34dff-165">Чтобы использовать микрофон, Мобильный телефон Teams запросит разрешение при `selectMedia()` вызове:</span><span class="sxs-lookup"><span data-stu-id="34dff-165">To use the microphone, Teams mobile asks permission when you call `selectMedia()`:</span></span>

    ```JavaScript 
    microsoftTeams.media.selectMedia({ maxMediaCount: 1, mediaType: microsoftTeams.media.MediaType.Audio }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    });
    ```

* <span data-ttu-id="34dff-166">Чтобы попросить пользователя поделиться данными о расположении в интерфейсе карты, Приложение Teams Mobile запросит разрешение при `getLocation()` вызове:</span><span class="sxs-lookup"><span data-stu-id="34dff-166">To prompt the user to share location on the map interface, Teams mobile asks permission when you call `getLocation()`:</span></span>

    ```JavaScript 
    microsoftTeams.location.getLocation({ allowChooseLocation: true, showMap: true }, (error: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
      /* ... *
    /});
    ```
# <a name="desktop"></a>[<span data-ttu-id="34dff-167">Desktop</span><span class="sxs-lookup"><span data-stu-id="34dff-167">Desktop</span></span>](#tab/desktop)

   ![Запрос разрешений для настольных устройств на вкладке](~/assets/images/tabs/device-permissions-prompt.png)

# <a name="mobile"></a>[<span data-ttu-id="34dff-169">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="34dff-169">Mobile</span></span>](#tab/mobile)

   ![Запрос разрешений мобильного устройства "Вкладки"](../../assets/images/tabs/MobileLocationPermission.png)

* * * 

## <a name="permission-behavior-across-login-sessions"></a><span data-ttu-id="34dff-171">Поведение разрешений в сеансах входа</span><span class="sxs-lookup"><span data-stu-id="34dff-171">Permission behavior across login sessions</span></span>

<span data-ttu-id="34dff-172">Разрешения устройства сохраняются для каждого сеанса входа.</span><span class="sxs-lookup"><span data-stu-id="34dff-172">Device permissions are stored for every login session.</span></span> <span data-ttu-id="34dff-173">Это означает, что при входе в другой экземпляр Teams, например, на другом компьютере, разрешения устройства из предыдущих сеансов будут недоступны.</span><span class="sxs-lookup"><span data-stu-id="34dff-173">It means that if you sign in to another instance of Teams, for example, on another computer, your device permissions from your previous sessions are not available.</span></span> <span data-ttu-id="34dff-174">Поэтому необходимо повторно согласиться на использование разрешений устройства для нового сеанса.</span><span class="sxs-lookup"><span data-stu-id="34dff-174">Therefore, you must re-consent to device permissions for the new session.</span></span> <span data-ttu-id="34dff-175">Это также означает, что при выходе из Teams или переключении клиентов в Teams разрешения устройств удаляются из предыдущего сеанса входа.</span><span class="sxs-lookup"><span data-stu-id="34dff-175">It also means, if you sign out of Teams or switch tenants in Teams, your device permissions are deleted from the previous login session.</span></span>  

> [!NOTE]
> <span data-ttu-id="34dff-176">Если вы даете согласие на доступ к нативным разрешениям устройства, это допустимо только для _текущего сеанса_ входа.</span><span class="sxs-lookup"><span data-stu-id="34dff-176">When you consent to the native device permissions, it is valid only for your _current_ login session.</span></span>

## <a name="next-step"></a><span data-ttu-id="34dff-177">Следующий этап</span><span class="sxs-lookup"><span data-stu-id="34dff-177">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="34dff-178">Интеграция возможностей мультимедиа в Teams</span><span class="sxs-lookup"><span data-stu-id="34dff-178">Integrate media capabilities in Teams</span></span>](mobile-camera-image-permissions.md)
