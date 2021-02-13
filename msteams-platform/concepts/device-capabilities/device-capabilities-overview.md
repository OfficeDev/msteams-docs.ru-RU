---
title: Обзор возможностей устройств
description: Обзор возможностей нативных устройств.
keywords: Встроенные разрешения устройства для микрофона камеры
ms.topic: overview
ms.openlocfilehash: 8b2f92cb4586d646bde02742883122bb009847ea
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/12/2021
ms.locfileid: "50232851"
---
# <a name="device-capabilities"></a><span data-ttu-id="89e58-104">Возможности устройств</span><span class="sxs-lookup"><span data-stu-id="89e58-104">Device capabilities</span></span> 

<span data-ttu-id="89e58-105">Платформа Microsoft Teams постоянно расширяет возможности разработчика в соответствие со встроенными возможностями от первого разработчика.</span><span class="sxs-lookup"><span data-stu-id="89e58-105">Microsoft Teams platform is continuously enhancing developer capabilities aligning with built-in first-party experiences.</span></span> <span data-ttu-id="89e58-106">Улучшенная платформа Teams позволяет партнерам интегрировать возможности устройств, такие как камера, фотоальбом, микрофон и расположение, с веб-приложениями.</span><span class="sxs-lookup"><span data-stu-id="89e58-106">The enhanced Teams platform allows partners to integrate device capabilities, such as camera, photo gallery, microphone, and location, with their web apps.</span></span> <span data-ttu-id="89e58-107">Такая интеграция снижает барьеры на пути разработки приложений, ускоряет цикл разработки и создает новые сценарии или сценарии использования для сообщества разработчиков.</span><span class="sxs-lookup"><span data-stu-id="89e58-107">This integration reduces the barrier to app development, speeds-up development-cycle, and creates new scenarios or use-cases for the developer community.</span></span>

## <a name="native-device-capabilities"></a><span data-ttu-id="89e58-108">Возможности нативных устройств</span><span class="sxs-lookup"><span data-stu-id="89e58-108">Native device capabilities</span></span>

<span data-ttu-id="89e58-109">На мобильном или настольном устройстве есть встроенные устройства, такие как камера и микрофон, называемые возможностями.</span><span class="sxs-lookup"><span data-stu-id="89e58-109">A mobile or desktop device has built-in devices, such as a camera and microphone, called capabilities.</span></span> <span data-ttu-id="89e58-110">Вы можете получить доступ к следующим возможностям устройств на мобильных или настольных компьютерах с помощью выделенных API, доступных в [клиентском SDK JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)для Microsoft Teams:</span><span class="sxs-lookup"><span data-stu-id="89e58-110">You can access the following device capabilities on mobile or desktop through dedicated APIs available in [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true):</span></span>
* <span data-ttu-id="89e58-111">Возможности мультимедиа, например</span><span class="sxs-lookup"><span data-stu-id="89e58-111">Media capabilities, such as</span></span>
    * <span data-ttu-id="89e58-112">Камера</span><span class="sxs-lookup"><span data-stu-id="89e58-112">Camera</span></span>
    * <span data-ttu-id="89e58-113">Микрофон</span><span class="sxs-lookup"><span data-stu-id="89e58-113">Microphone</span></span>
    * <span data-ttu-id="89e58-114">Галерея</span><span class="sxs-lookup"><span data-stu-id="89e58-114">Gallery</span></span>
* <span data-ttu-id="89e58-115">Расположение</span><span class="sxs-lookup"><span data-stu-id="89e58-115">Location</span></span>

<span data-ttu-id="89e58-116">Получив доступ к возможностям устройств, вы можете интегрировать их с платформой Teams, чтобы улучшить совместную работу.</span><span class="sxs-lookup"><span data-stu-id="89e58-116">After getting access to the device capabilities, you can integrate them with Teams platform to enhance the collaborative experience.</span></span> 

## <a name="request-device-permissions"></a><span data-ttu-id="89e58-117">Запрос разрешений устройства</span><span class="sxs-lookup"><span data-stu-id="89e58-117">Request device permissions</span></span>

<span data-ttu-id="89e58-118">Используйте инструменты, присутствующие в [клиентском SDK JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) для Microsoft Teams, чтобы запросить необходимые разрешения для доступа к возможностям нативных устройств. [](native-device-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="89e58-118">Use the tools present in [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) to  request the required  [permissions](native-device-permissions.md) for  accessing the native device capabilities.</span></span> <span data-ttu-id="89e58-119">Хотя доступ к этим возможностям является стандартным в современных веб-браузерах, необходимо сообщить Teams о возможностях, которые вы используете, обновив манифест приложения.</span><span class="sxs-lookup"><span data-stu-id="89e58-119">While access to these capabilities is standard in modern web browsers, you must inform Teams about the capabilities that you are using by updating your app manifest.</span></span> <span data-ttu-id="89e58-120">Это обновление позволяет запрашивать разрешения, пока приложение работает на мобильных или настольных клиентах Teams.</span><span class="sxs-lookup"><span data-stu-id="89e58-120">This update allows you to request permissions while your app runs on Teams mobile or desktop clients.</span></span>
 
 ## <a name="integrate-device-capabilities"></a><span data-ttu-id="89e58-121">Интеграция возможностей устройств</span><span class="sxs-lookup"><span data-stu-id="89e58-121">Integrate device capabilities</span></span>

<span data-ttu-id="89e58-122">После получения доступа к возможностям устройств используйте **API** возможностей мультимедиа Teams для интеграции этих возможностей с платформой Teams для улучшения пользовательского интерфейса. [](mobile-camera-image-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="89e58-122">After getting access to device capabilities,use **Teams media capability APIs** to [integrate the capabilities](mobile-camera-image-permissions.md) with Teams platform to enhance the user experience.</span></span> <span data-ttu-id="89e58-123">Эти интегрированные возможности позволяют приложению:</span><span class="sxs-lookup"><span data-stu-id="89e58-123">These integrated capabilities allow your app to:</span></span>

* <span data-ttu-id="89e58-124">Захват изображений и совместное их совместное изображение</span><span class="sxs-lookup"><span data-stu-id="89e58-124">Capture and share images</span></span>
* <span data-ttu-id="89e58-125">Запись звука с помощью микрофона</span><span class="sxs-lookup"><span data-stu-id="89e58-125">Record audio through microphone</span></span>
* <span data-ttu-id="89e58-126">Совместное размещение</span><span class="sxs-lookup"><span data-stu-id="89e58-126">Share the location information</span></span>


