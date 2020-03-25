---
title: Запрос разрешений устройства для вкладки Microsoft Teams
description: Обновление манифеста приложения для запроса доступа к встроенным функциям, которые обычно требуют согласия пользователя
keywords: Разработка вкладок Teams
ms.openlocfilehash: f0e19c0ed716147c097137c4ef0bf3454783b2eb
ms.sourcegitcommit: c4a7bc638e848a702cce92798cba84917fcecc35
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/24/2020
ms.locfileid: "42928519"
---
# <a name="request-device-permissions-for-your-microsoft-teams-tab"></a><span data-ttu-id="3ea36-104">Запрос разрешений устройства для вкладки Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="3ea36-104">Request device permissions for your Microsoft Teams tab</span></span>

<span data-ttu-id="3ea36-105">Вам может потребоваться расширить вкладки с помощью функций, требующих встроенных функций для доступа к устройствам, таких как:</span><span class="sxs-lookup"><span data-stu-id="3ea36-105">You might want to enrich your tab with features that require access native device functionality like:</span></span>

* <span data-ttu-id="3ea36-106">Видеокамер</span><span class="sxs-lookup"><span data-stu-id="3ea36-106">Camera</span></span>
* <span data-ttu-id="3ea36-107">Специальный</span><span class="sxs-lookup"><span data-stu-id="3ea36-107">Microphone</span></span>
* <span data-ttu-id="3ea36-108">Расположение</span><span class="sxs-lookup"><span data-stu-id="3ea36-108">Location</span></span>
* <span data-ttu-id="3ea36-109">Уведомления</span><span class="sxs-lookup"><span data-stu-id="3ea36-109">Notifications</span></span>

![Экран параметров разрешений для устройств](~/assets/images/tabs/device-permissions.png)

> [!IMPORTANT]
> <span data-ttu-id="3ea36-111">Встроенные функции устройств в настоящее время не поддерживаются для вкладок на мобильных клиентах, однако скоро будет доступна полная поддержка.</span><span class="sxs-lookup"><span data-stu-id="3ea36-111">Native device functionality is currently not supported for tabs on mobile clients but full support is coming soon.</span></span> <span data-ttu-id="3ea36-112">Чтобы подготовиться к этому изменению, следуйте [указаниям для вкладок на странице Mobile](~/tabs/design/tabs-mobile.md) при создании вкладок.</span><span class="sxs-lookup"><span data-stu-id="3ea36-112">To prepare for this change you should follow the [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md) when creating your tabs.</span></span> <span data-ttu-id="3ea36-113">В настоящее время персональные приложения (статические вкладки) доступны в [предварительной версии для разработчиков](~/resources/dev-preview/developer-preview-intro.md).</span><span class="sxs-lookup"><span data-stu-id="3ea36-113">Personal apps (static tabs) are currently available in [developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
>
> <span data-ttu-id="3ea36-114">Когда будет выпущена полная поддержка вкладок:</span><span class="sxs-lookup"><span data-stu-id="3ea36-114">When full support for tabs is released:</span></span>
>
> * <span data-ttu-id="3ea36-115">Все вкладки всегда будут доступны на мобильных устройствах</span><span class="sxs-lookup"><span data-stu-id="3ea36-115">All tabs will always be available on mobile</span></span>
> * <span data-ttu-id="3ea36-116">Вы `contentUrl` **будете загружены в клиенте Mobile Teams**.</span><span class="sxs-lookup"><span data-stu-id="3ea36-116">Your `contentUrl` **will be loaded in the mobile Teams client**.</span></span>
> * <span data-ttu-id="3ea36-117">Для вкладок каналов и групп пользователи по-прежнему могут открывать вкладку в отдельном браузере `websiteUrl`, но при этом `contentUrl` будут загружаться первыми.</span><span class="sxs-lookup"><span data-stu-id="3ea36-117">For channel/group tabs, users can still open your tab in a separate browser via your `websiteUrl`, however your `contentUrl` will be loaded first.</span></span>  

## <a name="device-permissions"></a><span data-ttu-id="3ea36-118">Разрешения для устройств</span><span class="sxs-lookup"><span data-stu-id="3ea36-118">Device permissions</span></span>

<span data-ttu-id="3ea36-119">Доступ к разрешениям для устройств пользователя позволяет создавать более широкие возможности, например:</span><span class="sxs-lookup"><span data-stu-id="3ea36-119">Accessing a user’s device permissions allows you to build much richer experiences, for example:</span></span>

* <span data-ttu-id="3ea36-120">Запись и совместное использование коротких видеороликов</span><span class="sxs-lookup"><span data-stu-id="3ea36-120">Record and share short videos</span></span>
* <span data-ttu-id="3ea36-121">Запись коротких звуковых заметок и их сохранение для последующего использования</span><span class="sxs-lookup"><span data-stu-id="3ea36-121">Record short audio memos and save them for later</span></span>
* <span data-ttu-id="3ea36-122">Использование сведений о местонахождении пользователя для отображения релевантных сведений</span><span class="sxs-lookup"><span data-stu-id="3ea36-122">Use user location information to display relevant information</span></span>

<span data-ttu-id="3ea36-123">Несмотря на то, что доступ к этим функциям имеют стандартные в большинстве современных веб-браузеров, необходимо разрешить командам знать, какие функции вы хотите использовать, обновив манифест приложения.</span><span class="sxs-lookup"><span data-stu-id="3ea36-123">While access to these features are standard in most modern web browsers, you need to let Teams know which features you’d like to use by updating your app manifest.</span></span> <span data-ttu-id="3ea36-124">Это позволит вам запросить разрешения так же, как и в браузере, а ваше приложение запущено на настольном клиенте Teams.</span><span class="sxs-lookup"><span data-stu-id="3ea36-124">This will allow you to ask for permissions, the same way you would in a browser, while your app is running on the Teams desktop client.</span></span>

## <a name="properties"></a><span data-ttu-id="3ea36-125">Свойства</span><span class="sxs-lookup"><span data-stu-id="3ea36-125">Properties</span></span>

<span data-ttu-id="3ea36-126">Обновите свое приложение `manifest.json` , добавив `devicePermissions` и указав, какие из пяти свойств вы хотите использовать в вашем приложении:</span><span class="sxs-lookup"><span data-stu-id="3ea36-126">Update your app's `manifest.json` by adding `devicePermissions` and specifying which of the five properties you’d like to use in your application:</span></span>

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```

<span data-ttu-id="3ea36-127">Каждое свойство позволит пользователю запросить согласие пользователя.</span><span class="sxs-lookup"><span data-stu-id="3ea36-127">Each property will allow you to prompt the user to ask for their consent</span></span>

| <span data-ttu-id="3ea36-128">Свойство</span><span class="sxs-lookup"><span data-stu-id="3ea36-128">Property</span></span>      | <span data-ttu-id="3ea36-129">Описание</span><span class="sxs-lookup"><span data-stu-id="3ea36-129">Description</span></span>   |
| --- | --- |
| <span data-ttu-id="3ea36-130">СМИ</span><span class="sxs-lookup"><span data-stu-id="3ea36-130">media</span></span>         | <span data-ttu-id="3ea36-131">разрешение на использование камеры, микрофона и динамиков</span><span class="sxs-lookup"><span data-stu-id="3ea36-131">permission to use the camera, microphone and speakers</span></span> |
| <span data-ttu-id="3ea36-132">географическое положение</span><span class="sxs-lookup"><span data-stu-id="3ea36-132">geolocation</span></span>   | <span data-ttu-id="3ea36-133">разрешение на возврат расположения пользователя</span><span class="sxs-lookup"><span data-stu-id="3ea36-133">permission to return the user's location</span></span>      |
| <span data-ttu-id="3ea36-134">уведомления</span><span class="sxs-lookup"><span data-stu-id="3ea36-134">notifications</span></span> | <span data-ttu-id="3ea36-135">разрешение на отправку уведомлений пользователей</span><span class="sxs-lookup"><span data-stu-id="3ea36-135">permission to send the user notifications</span></span>      |
| <span data-ttu-id="3ea36-136">MIDI</span><span class="sxs-lookup"><span data-stu-id="3ea36-136">midi</span></span>          | <span data-ttu-id="3ea36-137">разрешение на отправку и получение информации MIDI из цифрового музыкального инструмента</span><span class="sxs-lookup"><span data-stu-id="3ea36-137">permission to send and receive midi information from a digital musical instrument</span></span>   |
| <span data-ttu-id="3ea36-138">опенекстернал</span><span class="sxs-lookup"><span data-stu-id="3ea36-138">openExternal</span></span>  | <span data-ttu-id="3ea36-139">разрешение на открытие ссылок во внешних приложениях</span><span class="sxs-lookup"><span data-stu-id="3ea36-139">permission to open links in external applications</span></span>  |

## <a name="checking-permissions-from-your-tab"></a><span data-ttu-id="3ea36-140">Проверка разрешений на вкладке</span><span class="sxs-lookup"><span data-stu-id="3ea36-140">Checking permissions from your tab</span></span>

<span data-ttu-id="3ea36-141">После добавления `devicePermissions` в манифест приложения вы можете проверить разрешения с помощью API-интерфейса HTML5, не вызывая запрос.</span><span class="sxs-lookup"><span data-stu-id="3ea36-141">Once you’ve added `devicePermissions` to your app manifest, you can check permissions using the HTML5 “permissions” API without causing a prompt.</span></span>

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

## <a name="prompting-the-user"></a><span data-ttu-id="3ea36-142">Запрос пользователя</span><span class="sxs-lookup"><span data-stu-id="3ea36-142">Prompting the user</span></span>

<span data-ttu-id="3ea36-143">Чтобы показать запрос на получение согласия на доступ к разрешениям для устройств, необходимо использовать соответствующий API HTML5.</span><span class="sxs-lookup"><span data-stu-id="3ea36-143">In order to show a prompt to get consent to access device permissions you need to leverage the appropriate HTML5 API.</span></span> <span data-ttu-id="3ea36-144">Например, чтобы запросить у пользователя доступ к камере, которую нужно позвонить`getUserMedia`</span><span class="sxs-lookup"><span data-stu-id="3ea36-144">For example, in order to prompt the user to access their camera you need to call `getUserMedia`</span></span>

```Javascript
navigator.mediaDevices.getUserMedia({ audio: true, video: true });
```

<span data-ttu-id="3ea36-145">При вызове по географическому положению отображается запрос на разрешение`getCurrentPosition`</span><span class="sxs-lookup"><span data-stu-id="3ea36-145">Geolocation will  show a permission prompt when you call `getCurrentPosition`</span></span>

```Javascript
navigator.geolocation.getCurrentPosition(function (position) { /*... */ });
```

<span data-ttu-id="3ea36-146">Уведомления будут запрашивать пользователя при вызове`requestPermission`</span><span class="sxs-lookup"><span data-stu-id="3ea36-146">Notifications will prompt the user when you call `requestPermission`</span></span>

```Javascript
Notification.requestPermission(function(result) { /* ... */ });
```

![Запрос на доступ к устройствам с вкладками](~/assets/images/tabs/device-permissions-prompt.png)

## <a name="permission-behavior-across-login-sessions"></a><span data-ttu-id="3ea36-148">Поведение разрешений в сеансах входа</span><span class="sxs-lookup"><span data-stu-id="3ea36-148">Permission behavior across login sessions</span></span>

<span data-ttu-id="3ea36-149">Встроенные разрешения устройств хранятся на каждом сеансе входа.</span><span class="sxs-lookup"><span data-stu-id="3ea36-149">Native device permissions are stored per login session.</span></span> <span data-ttu-id="3ea36-150">Это означает, что если вы входите в другой экземпляр Teams (например, на другом компьютере), ваши разрешения на доступ к устройствам из предыдущих сеансов станут недоступными.</span><span class="sxs-lookup"><span data-stu-id="3ea36-150">This means that if you log into another instance of Teams (ex: on another computer), your device permissions from your previous sessions will not be available.</span></span> <span data-ttu-id="3ea36-151">Вместо этого вам потребуется повторное согласие с разрешениями на доступ к устройствам для новой учетной записи сессоин.</span><span class="sxs-lookup"><span data-stu-id="3ea36-151">Instead, you will need to re-consent to device permissions for the new login sessoin.</span></span> <span data-ttu-id="3ea36-152">Это также означает, что при выходе из Teams (или переключении клиентов в Teams) разрешения для этого устройства будут удалены для этого предыдущего сеанса.</span><span class="sxs-lookup"><span data-stu-id="3ea36-152">This also means, if you log out of Teams (or switch tenants inside of Teams), your device permissions will be deleted for that previous login session.</span></span> <span data-ttu-id="3ea36-153">Помните об этом при разработке собственных разрешений на устройства: встроенные возможности, которые вы согласные, относятся только к _текущей_ учетной записи сессоин.</span><span class="sxs-lookup"><span data-stu-id="3ea36-153">Please keep this in mind when developing native device permissions: the native capabilities you consent to are only for your _current_ login sessoin.</span></span>