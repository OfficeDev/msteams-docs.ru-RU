---
title: Возможности устройства — Обзор
author: Rajeshwari-v
description: Обзор возможностей родного устройства.
ms.author: surbhigupta
keywords: Микрофон микрофона микрофона микрофона qr qr code qrcode штрихкода штрихкода сканера сканера расположения карты изображений камеры возможности родных разрешений устройства
localization_priority: Normal
ms.topic: overview
ms.openlocfilehash: 7d214e5011abdc83d2f6b5b49c2261359259035e
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020753"
---
# <a name="device-capabilities---overview"></a><span data-ttu-id="8ad15-104">Возможности устройства — Обзор</span><span class="sxs-lookup"><span data-stu-id="8ad15-104">Device capabilities - Overview</span></span>

<span data-ttu-id="8ad15-105">Платформа Microsoft Teams непрерывно расширяет возможности разработчиков, выровняясь со встроенными возможностями для первой стороны.</span><span class="sxs-lookup"><span data-stu-id="8ad15-105">Microsoft Teams platform is continuously enhancing developer capabilities aligning with built-in first-party experiences.</span></span> <span data-ttu-id="8ad15-106">Расширенная платформа Teams позволяет партнерам интегрировать возможности устройств, такие как сканер камеры, QR или штрих-кода, фотогалерею, микрофон и расположение с их веб-приложениями.</span><span class="sxs-lookup"><span data-stu-id="8ad15-106">The enhanced Teams platform allows partners to integrate device capabilities, such as camera, QR or barcode scanner, photo gallery, microphone, and location with their web apps.</span></span> <span data-ttu-id="8ad15-107">Эта интеграция снижает барьер для разработки приложений, ускоряет цикл разработки и создает новые сценарии или случаи использования для сообщества разработчиков.</span><span class="sxs-lookup"><span data-stu-id="8ad15-107">This integration reduces the barrier to app development, speeds-up development-cycle, and creates new scenarios or use-cases for the developer community.</span></span>

## <a name="native-device-capabilities"></a><span data-ttu-id="8ad15-108">Возможности родного устройства</span><span class="sxs-lookup"><span data-stu-id="8ad15-108">Native device capabilities</span></span>

<span data-ttu-id="8ad15-109">Мобильное или настольное устройство имеет встроенные устройства, такие как камера и микрофон, называемые возможностями.</span><span class="sxs-lookup"><span data-stu-id="8ad15-109">A mobile or desktop device has built-in devices, such as a camera and microphone, called capabilities.</span></span> <span data-ttu-id="8ad15-110">Вы можете получить доступ к следующим возможностям устройства на мобильных или настольных компьютерах с помощью выделенных API, доступных в [клиентской SDK Microsoft Teams JavaScript:](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="8ad15-110">You can access the following device capabilities on mobile or desktop through dedicated APIs available in [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true):</span></span>
* <span data-ttu-id="8ad15-111">Возможности мультимедиа, такие как</span><span class="sxs-lookup"><span data-stu-id="8ad15-111">Media capabilities, such as</span></span>
    * <span data-ttu-id="8ad15-112">Камера</span><span class="sxs-lookup"><span data-stu-id="8ad15-112">Camera</span></span>
    * <span data-ttu-id="8ad15-113">Микрофон</span><span class="sxs-lookup"><span data-stu-id="8ad15-113">Microphone</span></span>
    * <span data-ttu-id="8ad15-114">Галерея</span><span class="sxs-lookup"><span data-stu-id="8ad15-114">Gallery</span></span>
    * <span data-ttu-id="8ad15-115">Сканер QR или штрихкода</span><span class="sxs-lookup"><span data-stu-id="8ad15-115">QR or barcode scanner</span></span>
* <span data-ttu-id="8ad15-116">Расположение</span><span class="sxs-lookup"><span data-stu-id="8ad15-116">Location</span></span>

<span data-ttu-id="8ad15-117">Получив доступ к возможностям устройства, вы можете интегрировать их с платформой Teams для повышения эффективности совместной работы.</span><span class="sxs-lookup"><span data-stu-id="8ad15-117">After getting access to the device capabilities, you can integrate them with Teams platform to enhance the collaborative experience.</span></span> 

## <a name="request-device-permissions"></a><span data-ttu-id="8ad15-118">Запрос разрешений устройства</span><span class="sxs-lookup"><span data-stu-id="8ad15-118">Request device permissions</span></span>

<span data-ttu-id="8ad15-119">Используйте средства, присутствующие в [клиентской SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) Microsoft [](native-device-permissions.md) Teams JavaScript, чтобы запрашивать необходимые разрешения для доступа к возможностям родного устройства.</span><span class="sxs-lookup"><span data-stu-id="8ad15-119">Use the tools present in [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) to request the required  [permissions](native-device-permissions.md) for accessing the native device capabilities.</span></span> <span data-ttu-id="8ad15-120">Хотя доступ к этим возможностям является стандартным в современных веб-браузерах, необходимо информировать Teams о возможностях, которые вы используете, обновив манифест приложения.</span><span class="sxs-lookup"><span data-stu-id="8ad15-120">While access to these capabilities is standard in modern web browsers, you must inform Teams about the capabilities that you are using by updating your app manifest.</span></span> <span data-ttu-id="8ad15-121">Это обновление позволяет запрашивать разрешения, пока приложение работает на мобильных или настольных клиентах Teams.</span><span class="sxs-lookup"><span data-stu-id="8ad15-121">This update allows you to request permissions while your app runs on Teams mobile or desktop clients.</span></span>
 
 ## <a name="integrate-device-capabilities"></a><span data-ttu-id="8ad15-122">Интеграция возможностей устройства</span><span class="sxs-lookup"><span data-stu-id="8ad15-122">Integrate device capabilities</span></span>

<span data-ttu-id="8ad15-123">После получения доступа к возможностям устройств используйте API [](mobile-camera-image-permissions.md) средств массовой информации Teams для интеграции возможностей мультимедиа с платформой Teams для улучшения пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="8ad15-123">After getting access to device capabilities, use Teams media capability APIs to [integrate media capabilities](mobile-camera-image-permissions.md) with Teams platform to enhance the user experience.</span></span> <span data-ttu-id="8ad15-124">Эти интегрированные возможности позволяют приложению:</span><span class="sxs-lookup"><span data-stu-id="8ad15-124">These integrated capabilities allow your app to:</span></span>

* <span data-ttu-id="8ad15-125">Захват и совместное изображение</span><span class="sxs-lookup"><span data-stu-id="8ad15-125">Capture and share images</span></span>
* <span data-ttu-id="8ad15-126">Сканирование QR или штрих-кода с помощью [управления сканером](qr-barcode-scanner-capability.md)</span><span class="sxs-lookup"><span data-stu-id="8ad15-126">Scan QR or barcode using [scanner control](qr-barcode-scanner-capability.md)</span></span>
* <span data-ttu-id="8ad15-127">Запись звука через микрофон</span><span class="sxs-lookup"><span data-stu-id="8ad15-127">Record audio through microphone</span></span>
* <span data-ttu-id="8ad15-128">Share location using [location picker](location-capability.md).</span><span class="sxs-lookup"><span data-stu-id="8ad15-128">Share location using [location picker](location-capability.md).</span></span>
