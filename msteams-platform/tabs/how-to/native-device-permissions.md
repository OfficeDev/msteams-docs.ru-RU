---
title: Запрос разрешений устройства для вкладки Microsoft Teams
description: Обновление манифеста приложения для запроса доступа к встроенным функциям, которые обычно требуют согласия пользователя
keywords: Разработка вкладок Teams
ms.openlocfilehash: 454466ff17ecf275f6ae6c7413df8e117335f3c8
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675169"
---
# <a name="request-device-permissions-for-your-microsoft-teams-tab"></a><span data-ttu-id="5095c-104">Запрос разрешений устройства для вкладки Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="5095c-104">Request device permissions for your Microsoft Teams tab</span></span>

<span data-ttu-id="5095c-105">Вам может потребоваться расширить вкладки с помощью функций, требующих встроенных функций для доступа к устройствам, таких как:</span><span class="sxs-lookup"><span data-stu-id="5095c-105">You might want to enrich your tab with features that require access native device functionality like:</span></span>

* <span data-ttu-id="5095c-106">Видеокамер</span><span class="sxs-lookup"><span data-stu-id="5095c-106">Camera</span></span>
* <span data-ttu-id="5095c-107">Специальный</span><span class="sxs-lookup"><span data-stu-id="5095c-107">Microphone</span></span>
* <span data-ttu-id="5095c-108">Расположение</span><span class="sxs-lookup"><span data-stu-id="5095c-108">Location</span></span>
* <span data-ttu-id="5095c-109">Уведомления</span><span class="sxs-lookup"><span data-stu-id="5095c-109">Notifications</span></span>

![Экран параметров разрешений для устройств](~/assets/images/tabs/device-permissions.png)

> [!IMPORTANT]
> <span data-ttu-id="5095c-111">Встроенные функции устройств в настоящее время не поддерживаются для вкладок на мобильных клиентах, однако скоро будет доступна полная поддержка.</span><span class="sxs-lookup"><span data-stu-id="5095c-111">Native device functionality is currently not supported for tabs on mobile clients but full support is coming soon.</span></span> <span data-ttu-id="5095c-112">Чтобы подготовиться к этому изменению, следуйте [указаниям для вкладок на странице Mobile](~/tabs/design/tabs-mobile.md) при создании вкладок.</span><span class="sxs-lookup"><span data-stu-id="5095c-112">To prepare for this change you should follow the [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md) when creating your tabs.</span></span> <span data-ttu-id="5095c-113">В настоящее время персональные приложения (статические вкладки) доступны в [предварительной версии для разработчиков](~/resources/dev-preview/developer-preview-intro.md).</span><span class="sxs-lookup"><span data-stu-id="5095c-113">Personal apps (static tabs) are currently available in [developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
>
> <span data-ttu-id="5095c-114">Когда будет выпущена полная поддержка вкладок:</span><span class="sxs-lookup"><span data-stu-id="5095c-114">When full support for tabs is released:</span></span>
>
> * <span data-ttu-id="5095c-115">Все вкладки всегда будут доступны на мобильных устройствах</span><span class="sxs-lookup"><span data-stu-id="5095c-115">All tabs will always be available on mobile</span></span>
> * <span data-ttu-id="5095c-116">Вы `contentUrl` **будете загружены в клиенте Mobile Teams**.</span><span class="sxs-lookup"><span data-stu-id="5095c-116">Your `contentUrl` **will be loaded in the mobile Teams client**.</span></span>
> * <span data-ttu-id="5095c-117">Для вкладок каналов и групп пользователи по-прежнему могут открывать вкладку в отдельном браузере `websiteUrl`, но при этом `contentUrl` будут загружаться первыми.</span><span class="sxs-lookup"><span data-stu-id="5095c-117">For channel/group tabs, users can still open your tab in a separate browser via your `websiteUrl`, however your `contentUrl` will be loaded first.</span></span>  

## <a name="device-permissions"></a><span data-ttu-id="5095c-118">Разрешения для устройств</span><span class="sxs-lookup"><span data-stu-id="5095c-118">Device permissions</span></span>

<span data-ttu-id="5095c-119">Доступ к разрешениям для устройств пользователя позволяет создавать более широкие возможности, например:</span><span class="sxs-lookup"><span data-stu-id="5095c-119">Accessing a user’s device permissions allows you to build much richer experiences, for example:</span></span>

* <span data-ttu-id="5095c-120">Запись и совместное использование коротких видеороликов</span><span class="sxs-lookup"><span data-stu-id="5095c-120">Record and share short videos</span></span>
* <span data-ttu-id="5095c-121">Запись коротких звуковых заметок и их сохранение для последующего использования</span><span class="sxs-lookup"><span data-stu-id="5095c-121">Record short audio memos and save them for later</span></span>
* <span data-ttu-id="5095c-122">Использование сведений о местонахождении пользователя для отображения релевантных сведений</span><span class="sxs-lookup"><span data-stu-id="5095c-122">Use user location information to display relevant information</span></span>

<span data-ttu-id="5095c-123">Несмотря на то, что доступ к этим функциям имеют стандартные в большинстве современных веб-браузеров, необходимо разрешить командам знать, какие функции вы хотите использовать, обновив манифест приложения.</span><span class="sxs-lookup"><span data-stu-id="5095c-123">While access to these features are standard in most modern web browsers, you need to let Teams know which features you’d like to use by updating your app manifest.</span></span> <span data-ttu-id="5095c-124">Это позволит вам запросить разрешения так же, как и в браузере, а ваше приложение запущено на настольном клиенте Teams.</span><span class="sxs-lookup"><span data-stu-id="5095c-124">This will allow you to ask for permissions, the same way you would in a browser, while your app is running on the Teams desktop client.</span></span>

## <a name="properties"></a><span data-ttu-id="5095c-125">Свойства</span><span class="sxs-lookup"><span data-stu-id="5095c-125">Properties</span></span>

<span data-ttu-id="5095c-126">Обновите свое приложение `manifest.json` , добавив `devicePermissions` и указав, какие из пяти свойств вы хотите использовать в вашем приложении:</span><span class="sxs-lookup"><span data-stu-id="5095c-126">Update your app's `manifest.json` by adding `devicePermissions` and specifying which of the five properties you’d like to use in your application:</span></span>

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```

<span data-ttu-id="5095c-127">Каждое свойство позволит пользователю запросить согласие пользователя.</span><span class="sxs-lookup"><span data-stu-id="5095c-127">Each property will allow you to prompt the user to ask for their consent</span></span>

| <span data-ttu-id="5095c-128">Свойство</span><span class="sxs-lookup"><span data-stu-id="5095c-128">Property</span></span>      | <span data-ttu-id="5095c-129">Описание</span><span class="sxs-lookup"><span data-stu-id="5095c-129">Description</span></span>   |
| --- | --- |
| <span data-ttu-id="5095c-130">СМИ</span><span class="sxs-lookup"><span data-stu-id="5095c-130">media</span></span>         | <span data-ttu-id="5095c-131">разрешение на использование камеры, микрофона и динамиков</span><span class="sxs-lookup"><span data-stu-id="5095c-131">permission to use the camera, microphone and speakers</span></span> |
| <span data-ttu-id="5095c-132">географическое положение</span><span class="sxs-lookup"><span data-stu-id="5095c-132">geolocation</span></span>   | <span data-ttu-id="5095c-133">разрешение на возврат расположения пользователя</span><span class="sxs-lookup"><span data-stu-id="5095c-133">permission to return the user's location</span></span>      |
| <span data-ttu-id="5095c-134">уведомления</span><span class="sxs-lookup"><span data-stu-id="5095c-134">notifications</span></span> | <span data-ttu-id="5095c-135">разрешение на отправку уведомлений пользователей</span><span class="sxs-lookup"><span data-stu-id="5095c-135">permission to send the user notifications</span></span>      |
| <span data-ttu-id="5095c-136">MIDI</span><span class="sxs-lookup"><span data-stu-id="5095c-136">midi</span></span>          | <span data-ttu-id="5095c-137">разрешение на отправку и получение информации MIDI из цифрового музыкального инструмента</span><span class="sxs-lookup"><span data-stu-id="5095c-137">permission to send and receive midi information from a digital musical instrument</span></span>   |
| <span data-ttu-id="5095c-138">опенекстернал</span><span class="sxs-lookup"><span data-stu-id="5095c-138">openExternal</span></span>  | <span data-ttu-id="5095c-139">разрешение на открытие ссылок во внешних приложениях</span><span class="sxs-lookup"><span data-stu-id="5095c-139">permission to open links in external applications</span></span>  |

## <a name="checking-permissions-from-your-tab"></a><span data-ttu-id="5095c-140">Проверка разрешений на вкладке</span><span class="sxs-lookup"><span data-stu-id="5095c-140">Checking permissions from your tab</span></span>

<span data-ttu-id="5095c-141">После добавления `devicePermissions` в манифест приложения вы можете проверить разрешения с помощью API-интерфейса HTML5, не вызывая запрос.</span><span class="sxs-lookup"><span data-stu-id="5095c-141">Once you’ve added `devicePermissions` to your app manifest, you can check permissions using the HTML5 “permissions” API without causing a prompt.</span></span>

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

## <a name="prompting-the-user"></a><span data-ttu-id="5095c-142">Запрос пользователя</span><span class="sxs-lookup"><span data-stu-id="5095c-142">Prompting the user</span></span>

<span data-ttu-id="5095c-143">Чтобы показать запрос на получение согласия на доступ к разрешениям для устройств, необходимо использовать соответствующий API HTML5.</span><span class="sxs-lookup"><span data-stu-id="5095c-143">In order to show a prompt to get consent to access device permissions you need to leverage the appropriate HTML5 API.</span></span> <span data-ttu-id="5095c-144">Например, чтобы запросить у пользователя доступ к камере, которую нужно позвонить`getUserMedia`</span><span class="sxs-lookup"><span data-stu-id="5095c-144">For example, in order to prompt the user to access their camera you need to call `getUserMedia`</span></span>

```Javascript
navigator.mediaDevices.getUserMedia({ audio: true, video: true });
```

<span data-ttu-id="5095c-145">При вызове по географическому положению отображается запрос на разрешение`getCurrentPosition`</span><span class="sxs-lookup"><span data-stu-id="5095c-145">Geolocation will  show a permission prompt when you call `getCurrentPosition`</span></span>

```Javascript
navigator.geolocation.getCurrentPosition(function (position) { /*... */ });
```

<span data-ttu-id="5095c-146">Уведомления будут запрашивать пользователя при вызове`requestPermission`</span><span class="sxs-lookup"><span data-stu-id="5095c-146">Notifications will prompt the user when you call `requestPermission`</span></span>

```Javascript
Notification.requestPermission(function(result) { /* ... */ });
```

![Запрос на доступ к устройствам с вкладками](~/assets/images/tabs/device-permissions-prompt.png)