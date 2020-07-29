---
title: Запрос разрешений устройства для вкладки Microsoft Teams
description: Обновление манифеста приложения для запроса доступа к встроенным функциям, которые обычно требуют согласия пользователя
keywords: Разработка вкладок Teams
ms.openlocfilehash: e69c7540730307e62035c48ac64cd977419ea5f2
ms.sourcegitcommit: 1b909fb9ccf6cdd84ed0d8f9ea0463243a802a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/28/2020
ms.locfileid: "45434558"
---
# <a name="request-device-permissions-for-your-microsoft-teams-tab"></a><span data-ttu-id="9237d-104">Запрос разрешений устройства для вкладки Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="9237d-104">Request device permissions for your Microsoft Teams tab</span></span>

<span data-ttu-id="9237d-105">Вам может потребоваться расширить вкладки с помощью функций, требующих встроенных функций для доступа к устройствам, таких как:</span><span class="sxs-lookup"><span data-stu-id="9237d-105">You might want to enrich your tab with features that require access native device functionality like:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="9237d-106">Видеокамер</span><span class="sxs-lookup"><span data-stu-id="9237d-106">Camera</span></span>
> * <span data-ttu-id="9237d-107">Специальный</span><span class="sxs-lookup"><span data-stu-id="9237d-107">Microphone</span></span>
> * <span data-ttu-id="9237d-108">Расположение</span><span class="sxs-lookup"><span data-stu-id="9237d-108">Location</span></span>
> * <span data-ttu-id="9237d-109">Уведомления</span><span class="sxs-lookup"><span data-stu-id="9237d-109">Notifications</span></span>

> [!IMPORTANT]
>
> * <span data-ttu-id="9237d-110">В настоящее время клиент Teams для мобильных устройств поддерживает только `camera` `location` встроенные возможности устройств и доступен во всех конструкциях приложений, в том числе на вкладках.</span><span class="sxs-lookup"><span data-stu-id="9237d-110">Currently, Teams mobile client only supports `camera` and `location`  through native device capabilities and is available on all app constructs including tabs.</span></span> </br>
> * <span data-ttu-id="9237d-111">Поддержка `camera` захвата образов включена с помощью [**API каптуреимаже**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-).</span><span class="sxs-lookup"><span data-stu-id="9237d-111">Support for `camera` image capture is enabled by the [**captureImage API**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-).</span></span>
> * <span data-ttu-id="9237d-112">В настоящее время [**API географического расположения**](../../resources/schema/manifest-schema.md#devicepermissions) не полностью поддерживается для всех настольных клиентов.</span><span class="sxs-lookup"><span data-stu-id="9237d-112">The [**geolocation API**](../../resources/schema/manifest-schema.md#devicepermissions) is currently not fully supported on all desktop clients.</span></span>

## <a name="device-permissions"></a><span data-ttu-id="9237d-113">Разрешения для устройств</span><span class="sxs-lookup"><span data-stu-id="9237d-113">Device permissions</span></span>

<span data-ttu-id="9237d-114">Доступ к разрешениям для устройств пользователя позволяет создавать более широкие возможности, например:</span><span class="sxs-lookup"><span data-stu-id="9237d-114">Accessing a user’s device permissions allows you to build much richer experiences, for example:</span></span>

* <span data-ttu-id="9237d-115">Запись и совместное использование коротких видеороликов</span><span class="sxs-lookup"><span data-stu-id="9237d-115">Record and share short videos</span></span>
* <span data-ttu-id="9237d-116">Запись коротких звуковых заметок и их сохранение для последующего использования</span><span class="sxs-lookup"><span data-stu-id="9237d-116">Record short audio memos and save them for later</span></span>
* <span data-ttu-id="9237d-117">Использование сведений о местонахождении пользователя для отображения релевантных сведений</span><span class="sxs-lookup"><span data-stu-id="9237d-117">Use user location information to display relevant information</span></span>

<span data-ttu-id="9237d-118">Несмотря на то, что доступ к этим функциям имеют стандартные в большинстве современных веб-браузеров, необходимо разрешить командам знать, какие функции вы хотите использовать, обновив манифест приложения.</span><span class="sxs-lookup"><span data-stu-id="9237d-118">While access to these features are standard in most modern web browsers, you need to let Teams know which features you’d like to use by updating your app manifest.</span></span> <span data-ttu-id="9237d-119">Это позволит вам запросить разрешения так же, как и в браузере, а ваше приложение запущено на настольном клиенте Teams.</span><span class="sxs-lookup"><span data-stu-id="9237d-119">This will allow you to ask for permissions, the same way you would in a browser, while your app is running on the Teams desktop client.</span></span>

## <a name="manage-permissions"></a><span data-ttu-id="9237d-120">Управление разрешениями</span><span class="sxs-lookup"><span data-stu-id="9237d-120">Manage permissions</span></span>

# <a name="desktop"></a>[<span data-ttu-id="9237d-121">Desktop</span><span class="sxs-lookup"><span data-stu-id="9237d-121">Desktop</span></span>](#tab/desktop)

1. <span data-ttu-id="9237d-122">Откройте Teams.</span><span class="sxs-lookup"><span data-stu-id="9237d-122">Open Teams.</span></span>
1. <span data-ttu-id="9237d-123">В правом верхнем углу окна выберите свой значок профиля.</span><span class="sxs-lookup"><span data-stu-id="9237d-123">In the upper right corner of the window, select your profile icon.</span></span>
1. <span data-ttu-id="9237d-124">В раскрывающемся меню выберите пункт **Параметры**  ->  **разрешений** .</span><span class="sxs-lookup"><span data-stu-id="9237d-124">Select **Settings** -> **Permissions** from the drop-down menu.</span></span>
1. <span data-ttu-id="9237d-125">Выберите нужные параметры.</span><span class="sxs-lookup"><span data-stu-id="9237d-125">Choose your desired settings.</span></span>

![Экран параметров рабочего стола для разрешений устройства](../../assets/images/tabs/device-permissions.png)

# <a name="mobile"></a>[<span data-ttu-id="9237d-127">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="9237d-127">Mobile</span></span>](#tab/mobile)

1. <span data-ttu-id="9237d-128">Откройте Teams.</span><span class="sxs-lookup"><span data-stu-id="9237d-128">Open Teams.</span></span>
1. <span data-ttu-id="9237d-129">В левом верхнем углу экрана выберите значок меню &#9776;.</span><span class="sxs-lookup"><span data-stu-id="9237d-129">In the upper left corner of the screen, select the &#9776; menu icon.</span></span>
1. <span data-ttu-id="9237d-130">Выберите **Параметры**  ->  **устройства**.</span><span class="sxs-lookup"><span data-stu-id="9237d-130">Select **Settings** -> **Devices**.</span></span>
1. <span data-ttu-id="9237d-131">Выберите нужные параметры.</span><span class="sxs-lookup"><span data-stu-id="9237d-131">Choose your desired settings.</span></span>

![Экран параметров разрешений на доступ к мобильным устройствам](../../assets/images/tabs/mobile-device-permissions-screen.png)

---

## <a name="properties"></a><span data-ttu-id="9237d-133">Свойства</span><span class="sxs-lookup"><span data-stu-id="9237d-133">Properties</span></span>

<span data-ttu-id="9237d-134">Обновите свое приложение `manifest.json` , добавив `devicePermissions` и указав, какие из пяти свойств вы хотите использовать в вашем приложении:</span><span class="sxs-lookup"><span data-stu-id="9237d-134">Update your app's `manifest.json` by adding `devicePermissions` and specifying which of the five properties you’d like to use in your application:</span></span>

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
> <span data-ttu-id="9237d-135">Мультимедиа также используется для разрешений камеры на мобильных устройствах.</span><span class="sxs-lookup"><span data-stu-id="9237d-135">Media is also used for camera permissions in mobile.</span></span>

<span data-ttu-id="9237d-136">Каждое свойство позволит пользователю запросить согласие пользователя.</span><span class="sxs-lookup"><span data-stu-id="9237d-136">Each property will allow you to prompt the user to ask for their consent</span></span>

| <span data-ttu-id="9237d-137">Свойство</span><span class="sxs-lookup"><span data-stu-id="9237d-137">Property</span></span>      | <span data-ttu-id="9237d-138">Описание</span><span class="sxs-lookup"><span data-stu-id="9237d-138">Description</span></span>   |
| --- | --- |
| <span data-ttu-id="9237d-139">СМИ</span><span class="sxs-lookup"><span data-stu-id="9237d-139">media</span></span>         | <span data-ttu-id="9237d-140">разрешение на использование камеры, микрофона и динамиков</span><span class="sxs-lookup"><span data-stu-id="9237d-140">permission to use the camera, microphone and speakers</span></span> |
| <span data-ttu-id="9237d-141">географическое положение</span><span class="sxs-lookup"><span data-stu-id="9237d-141">geolocation</span></span>   | <span data-ttu-id="9237d-142">разрешение на возврат расположения пользователя</span><span class="sxs-lookup"><span data-stu-id="9237d-142">permission to return the user's location</span></span>      |
| <span data-ttu-id="9237d-143">уведомления</span><span class="sxs-lookup"><span data-stu-id="9237d-143">notifications</span></span> | <span data-ttu-id="9237d-144">разрешение на отправку уведомлений пользователей</span><span class="sxs-lookup"><span data-stu-id="9237d-144">permission to send the user notifications</span></span>      |
| <span data-ttu-id="9237d-145">MIDI</span><span class="sxs-lookup"><span data-stu-id="9237d-145">midi</span></span>          | <span data-ttu-id="9237d-146">разрешение на отправку и получение информации MIDI из цифрового музыкального инструмента</span><span class="sxs-lookup"><span data-stu-id="9237d-146">permission to send and receive midi information from a digital musical instrument</span></span>   |
| <span data-ttu-id="9237d-147">опенекстернал</span><span class="sxs-lookup"><span data-stu-id="9237d-147">openExternal</span></span>  | <span data-ttu-id="9237d-148">разрешение на открытие ссылок во внешних приложениях</span><span class="sxs-lookup"><span data-stu-id="9237d-148">permission to open links in external applications</span></span>  |

## <a name="checking-permissions-from-your-tab"></a><span data-ttu-id="9237d-149">Проверка разрешений на вкладке</span><span class="sxs-lookup"><span data-stu-id="9237d-149">Checking permissions from your tab</span></span>

<span data-ttu-id="9237d-150">После добавления `devicePermissions` в манифест приложения вы можете проверить разрешения с помощью API-интерфейса HTML5, не вызывая запрос.</span><span class="sxs-lookup"><span data-stu-id="9237d-150">Once you’ve added `devicePermissions` to your app manifest, you can check permissions using the HTML5 “permissions” API without causing a prompt.</span></span>

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

## <a name="prompting-the-user"></a><span data-ttu-id="9237d-151">Запрос пользователя</span><span class="sxs-lookup"><span data-stu-id="9237d-151">Prompting the user</span></span>

<span data-ttu-id="9237d-152">Чтобы показать запрос на получение согласия на доступ к разрешениям для устройств, необходимо использовать соответствующий HTML5 или API Teams.</span><span class="sxs-lookup"><span data-stu-id="9237d-152">In order to show a prompt to get consent to access device permissions you need to leverage the appropriate HTML5 or Teams API.</span></span> <span data-ttu-id="9237d-153">Например, чтобы запросить у пользователя доступ к камере, которую нужно позвонить`getCurrentPosition`</span><span class="sxs-lookup"><span data-stu-id="9237d-153">For example, in order to prompt the user to access their camera you need to call `getCurrentPosition`</span></span>

```Javascript
navigator.geolocation.getCurrentPosition(function (position) { /*... */ });
```

<span data-ttu-id="9237d-154">Чтобы использовать камеру на настольном компьютере или в Интернете, при вызове Жетусермедиа Teams будет показывать запрос о разрешении.</span><span class="sxs-lookup"><span data-stu-id="9237d-154">To use camera on desktop or web, Teams will show a permission prompt when you call getUserMedia</span></span>

```Javascript
navigator.mediaDevices.getUserMedia({ audio: true, video: true });
```

<span data-ttu-id="9237d-155">Чтобы записать изображение на мобильном устройстве, Teams будет запрашивать разрешение при вызове Каптуреимаже ().</span><span class="sxs-lookup"><span data-stu-id="9237d-155">To capture image on mobile, Teams mobile will ask for permission when called captureImage()</span></span>

```Typescript
function captureImage(callback: (error: SdkError, files: File[]) => void)
```

<span data-ttu-id="9237d-156">Уведомления будут запрашивать пользователя при вызове`requestPermission`</span><span class="sxs-lookup"><span data-stu-id="9237d-156">Notifications will prompt the user when you call `requestPermission`</span></span>

```Javascript
Notification.requestPermission(function(result) { /* ... */ });
```

![Запрос на доступ к устройствам с вкладками](~/assets/images/tabs/device-permissions-prompt.png)

## <a name="permission-behavior-across-login-sessions"></a><span data-ttu-id="9237d-158">Поведение разрешений в сеансах входа</span><span class="sxs-lookup"><span data-stu-id="9237d-158">Permission behavior across login sessions</span></span>

<span data-ttu-id="9237d-159">Встроенные разрешения устройств хранятся на каждом сеансе входа.</span><span class="sxs-lookup"><span data-stu-id="9237d-159">Native device permissions are stored per login session.</span></span> <span data-ttu-id="9237d-160">Это означает, что если вы входите в другой экземпляр Teams (например, на другом компьютере), ваши разрешения на доступ к устройствам из предыдущих сеансов станут недоступными.</span><span class="sxs-lookup"><span data-stu-id="9237d-160">This means that if you log into another instance of Teams (ex: on another computer), your device permissions from your previous sessions will not be available.</span></span> <span data-ttu-id="9237d-161">Вместо этого вам потребуется повторное согласие с разрешениями на устройство для нового сеанса входа.</span><span class="sxs-lookup"><span data-stu-id="9237d-161">Instead, you will need to re-consent to device permissions for the new login session.</span></span> <span data-ttu-id="9237d-162">Это также означает, что при выходе из Teams (или переключении клиентов в Teams) разрешения для этого устройства будут удалены для этого предыдущего сеанса.</span><span class="sxs-lookup"><span data-stu-id="9237d-162">This also means, if you log out of Teams (or switch tenants inside of Teams), your device permissions will be deleted for that previous login session.</span></span> <span data-ttu-id="9237d-163">Помните об этом при разработке собственных разрешений на устройства: встроенные возможности, на которые вы согласны, относятся только к _текущему_ сеансу входа в систему.</span><span class="sxs-lookup"><span data-stu-id="9237d-163">Please keep this in mind when developing native device permissions: the native capabilities you consent to are only for your _current_ login session.</span></span>
