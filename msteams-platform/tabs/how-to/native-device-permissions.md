---
title: Запрос разрешений устройства для вкладки Microsoft Teams
description: Обновление манифеста приложения для запроса доступа к встроенным функциям, которые обычно требуют согласия пользователя
keywords: Разработка вкладок Teams
ms.openlocfilehash: e9dc6c6f177e3a87e2846bcb836cc38601c9a50e
ms.sourcegitcommit: b13b38a104946c32cd5245a7af706070e534927d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/28/2020
ms.locfileid: "43034038"
---
# <a name="request-device-permissions-for-your-microsoft-teams-tab"></a><span data-ttu-id="02c5a-104">Запрос разрешений устройства для вкладки Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="02c5a-104">Request device permissions for your Microsoft Teams tab</span></span>

<span data-ttu-id="02c5a-105">Вам может потребоваться расширить вкладки с помощью функций, требующих встроенных функций для доступа к устройствам, таких как:</span><span class="sxs-lookup"><span data-stu-id="02c5a-105">You might want to enrich your tab with features that require access native device functionality like:</span></span>

* <span data-ttu-id="02c5a-106">Видеокамер</span><span class="sxs-lookup"><span data-stu-id="02c5a-106">Camera</span></span>
* <span data-ttu-id="02c5a-107">Специальный</span><span class="sxs-lookup"><span data-stu-id="02c5a-107">Microphone</span></span>
* <span data-ttu-id="02c5a-108">Расположение</span><span class="sxs-lookup"><span data-stu-id="02c5a-108">Location</span></span>
* <span data-ttu-id="02c5a-109">Уведомления</span><span class="sxs-lookup"><span data-stu-id="02c5a-109">Notifications</span></span>

![Экран параметров разрешений для устройств](~/assets/images/tabs/device-permissions.png)

> [!IMPORTANT]
>
> <span data-ttu-id="02c5a-111">Встроенные функции устройств в настоящее время не поддерживаются для вкладок мобильных клиентов.</span><span class="sxs-lookup"><span data-stu-id="02c5a-111">Native device functionality is currently not supported for tabs on mobile clients.</span></span>
>
> <span data-ttu-id="02c5a-112">В настоящее время API географического расположения не полностью поддерживается для всех настольных клиентов.</span><span class="sxs-lookup"><span data-stu-id="02c5a-112">The geolocation API is currently not fully supported on all desktop clients.</span></span>

## <a name="device-permissions"></a><span data-ttu-id="02c5a-113">Разрешения для устройств</span><span class="sxs-lookup"><span data-stu-id="02c5a-113">Device permissions</span></span>

<span data-ttu-id="02c5a-114">Доступ к разрешениям для устройств пользователя позволяет создавать более широкие возможности, например:</span><span class="sxs-lookup"><span data-stu-id="02c5a-114">Accessing a user’s device permissions allows you to build much richer experiences, for example:</span></span>

* <span data-ttu-id="02c5a-115">Запись и совместное использование коротких видеороликов</span><span class="sxs-lookup"><span data-stu-id="02c5a-115">Record and share short videos</span></span>
* <span data-ttu-id="02c5a-116">Запись коротких звуковых заметок и их сохранение для последующего использования</span><span class="sxs-lookup"><span data-stu-id="02c5a-116">Record short audio memos and save them for later</span></span>
* <span data-ttu-id="02c5a-117">Использование сведений о местонахождении пользователя для отображения релевантных сведений</span><span class="sxs-lookup"><span data-stu-id="02c5a-117">Use user location information to display relevant information</span></span>

<span data-ttu-id="02c5a-118">Несмотря на то, что доступ к этим функциям имеют стандартные в большинстве современных веб-браузеров, необходимо разрешить командам знать, какие функции вы хотите использовать, обновив манифест приложения.</span><span class="sxs-lookup"><span data-stu-id="02c5a-118">While access to these features are standard in most modern web browsers, you need to let Teams know which features you’d like to use by updating your app manifest.</span></span> <span data-ttu-id="02c5a-119">Это позволит вам запросить разрешения так же, как и в браузере, а ваше приложение запущено на настольном клиенте Teams.</span><span class="sxs-lookup"><span data-stu-id="02c5a-119">This will allow you to ask for permissions, the same way you would in a browser, while your app is running on the Teams desktop client.</span></span>

## <a name="properties"></a><span data-ttu-id="02c5a-120">Свойства</span><span class="sxs-lookup"><span data-stu-id="02c5a-120">Properties</span></span>

<span data-ttu-id="02c5a-121">Обновите свое приложение `manifest.json` , добавив `devicePermissions` и указав, какие из пяти свойств вы хотите использовать в вашем приложении:</span><span class="sxs-lookup"><span data-stu-id="02c5a-121">Update your app's `manifest.json` by adding `devicePermissions` and specifying which of the five properties you’d like to use in your application:</span></span>

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```

<span data-ttu-id="02c5a-122">Каждое свойство позволит пользователю запросить согласие пользователя.</span><span class="sxs-lookup"><span data-stu-id="02c5a-122">Each property will allow you to prompt the user to ask for their consent</span></span>

| <span data-ttu-id="02c5a-123">Свойство</span><span class="sxs-lookup"><span data-stu-id="02c5a-123">Property</span></span>      | <span data-ttu-id="02c5a-124">Описание</span><span class="sxs-lookup"><span data-stu-id="02c5a-124">Description</span></span>   |
| --- | --- |
| <span data-ttu-id="02c5a-125">media</span><span class="sxs-lookup"><span data-stu-id="02c5a-125">media</span></span>         | <span data-ttu-id="02c5a-126">разрешение на использование камеры, микрофона и динамиков</span><span class="sxs-lookup"><span data-stu-id="02c5a-126">permission to use the camera, microphone and speakers</span></span> |
| <span data-ttu-id="02c5a-127">географическое положение</span><span class="sxs-lookup"><span data-stu-id="02c5a-127">geolocation</span></span>   | <span data-ttu-id="02c5a-128">разрешение на возврат расположения пользователя</span><span class="sxs-lookup"><span data-stu-id="02c5a-128">permission to return the user's location</span></span>      |
| <span data-ttu-id="02c5a-129">уведомления</span><span class="sxs-lookup"><span data-stu-id="02c5a-129">notifications</span></span> | <span data-ttu-id="02c5a-130">разрешение на отправку уведомлений пользователей</span><span class="sxs-lookup"><span data-stu-id="02c5a-130">permission to send the user notifications</span></span>      |
| <span data-ttu-id="02c5a-131">MIDI</span><span class="sxs-lookup"><span data-stu-id="02c5a-131">midi</span></span>          | <span data-ttu-id="02c5a-132">разрешение на отправку и получение информации MIDI из цифрового музыкального инструмента</span><span class="sxs-lookup"><span data-stu-id="02c5a-132">permission to send and receive midi information from a digital musical instrument</span></span>   |
| <span data-ttu-id="02c5a-133">опенекстернал</span><span class="sxs-lookup"><span data-stu-id="02c5a-133">openExternal</span></span>  | <span data-ttu-id="02c5a-134">разрешение на открытие ссылок во внешних приложениях</span><span class="sxs-lookup"><span data-stu-id="02c5a-134">permission to open links in external applications</span></span>  |

## <a name="checking-permissions-from-your-tab"></a><span data-ttu-id="02c5a-135">Проверка разрешений на вкладке</span><span class="sxs-lookup"><span data-stu-id="02c5a-135">Checking permissions from your tab</span></span>

<span data-ttu-id="02c5a-136">После добавления `devicePermissions` в манифест приложения вы можете проверить разрешения с помощью API-интерфейса HTML5, не вызывая запрос.</span><span class="sxs-lookup"><span data-stu-id="02c5a-136">Once you’ve added `devicePermissions` to your app manifest, you can check permissions using the HTML5 “permissions” API without causing a prompt.</span></span>

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

## <a name="prompting-the-user"></a><span data-ttu-id="02c5a-137">Запрос пользователя</span><span class="sxs-lookup"><span data-stu-id="02c5a-137">Prompting the user</span></span>

<span data-ttu-id="02c5a-138">Чтобы показать запрос на получение согласия на доступ к разрешениям для устройств, необходимо использовать соответствующий API HTML5.</span><span class="sxs-lookup"><span data-stu-id="02c5a-138">In order to show a prompt to get consent to access device permissions you need to leverage the appropriate HTML5 API.</span></span> <span data-ttu-id="02c5a-139">Например, чтобы запросить у пользователя доступ к камере, которую нужно позвонить`getUserMedia`</span><span class="sxs-lookup"><span data-stu-id="02c5a-139">For example, in order to prompt the user to access their camera you need to call `getUserMedia`</span></span>

```Javascript
navigator.mediaDevices.getUserMedia({ audio: true, video: true });
```

<span data-ttu-id="02c5a-140">При вызове по географическому положению отображается запрос на разрешение`getCurrentPosition`</span><span class="sxs-lookup"><span data-stu-id="02c5a-140">Geolocation will  show a permission prompt when you call `getCurrentPosition`</span></span>

```Javascript
navigator.geolocation.getCurrentPosition(function (position) { /*... */ });
```

<span data-ttu-id="02c5a-141">Уведомления будут запрашивать пользователя при вызове`requestPermission`</span><span class="sxs-lookup"><span data-stu-id="02c5a-141">Notifications will prompt the user when you call `requestPermission`</span></span>

```Javascript
Notification.requestPermission(function(result) { /* ... */ });
```

![Запрос на доступ к устройствам с вкладками](~/assets/images/tabs/device-permissions-prompt.png)

## <a name="permission-behavior-across-login-sessions"></a><span data-ttu-id="02c5a-143">Поведение разрешений в сеансах входа</span><span class="sxs-lookup"><span data-stu-id="02c5a-143">Permission behavior across login sessions</span></span>

<span data-ttu-id="02c5a-144">Встроенные разрешения устройств хранятся на каждом сеансе входа.</span><span class="sxs-lookup"><span data-stu-id="02c5a-144">Native device permissions are stored per login session.</span></span> <span data-ttu-id="02c5a-145">Это означает, что если вы входите в другой экземпляр Teams (например, на другом компьютере), ваши разрешения на доступ к устройствам из предыдущих сеансов станут недоступными.</span><span class="sxs-lookup"><span data-stu-id="02c5a-145">This means that if you log into another instance of Teams (ex: on another computer), your device permissions from your previous sessions will not be available.</span></span> <span data-ttu-id="02c5a-146">Вместо этого вам потребуется повторное согласие с разрешениями на устройство для нового сеанса входа.</span><span class="sxs-lookup"><span data-stu-id="02c5a-146">Instead, you will need to re-consent to device permissions for the new login session.</span></span> <span data-ttu-id="02c5a-147">Это также означает, что при выходе из Teams (или переключении клиентов в Teams) разрешения для этого устройства будут удалены для этого предыдущего сеанса.</span><span class="sxs-lookup"><span data-stu-id="02c5a-147">This also means, if you log out of Teams (or switch tenants inside of Teams), your device permissions will be deleted for that previous login session.</span></span> <span data-ttu-id="02c5a-148">Помните об этом при разработке собственных разрешений на устройства: встроенные возможности, на которые вы согласны, относятся только к _текущему_ сеансу входа в систему.</span><span class="sxs-lookup"><span data-stu-id="02c5a-148">Please keep this in mind when developing native device permissions: the native capabilities you consent to are only for your _current_ login session.</span></span>
