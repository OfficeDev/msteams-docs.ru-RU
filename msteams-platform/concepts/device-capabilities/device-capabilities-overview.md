---
title: Возможности устройства - Обзор
author: Rajeshwari-v
description: Обзор возможностей родных устройств.
ms.author: surbhigupta
keywords: камера изображения медиа микрофон микрофон qr код qrcode штрих-код сканера местоположение карты возможности родного устройства разрешений
localization_priority: Normal
ms.topic: overview
ms.openlocfilehash: 8df8341e8996e4bf380575ac59e05325da16bd0d
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566196"
---
# <a name="device-capabilities"></a><span data-ttu-id="212e6-104">Возможности устройств</span><span class="sxs-lookup"><span data-stu-id="212e6-104">Device capabilities</span></span>

<span data-ttu-id="212e6-105">Microsoft Teams платформа постоянно совершенствует возможности разработчиков, согласуясь со встроенным опытом первой стороны.</span><span class="sxs-lookup"><span data-stu-id="212e6-105">Microsoft Teams platform is continuously enhancing developer capabilities aligning with built-in first-party experiences.</span></span> <span data-ttu-id="212e6-106">Улучшенная платформа Teams позволяет партнерам интегрировать возможности устройств, такие как камера, сканер штрих-кодов, фотогалерея, микрофон и местоположение с их веб-приложениями.</span><span class="sxs-lookup"><span data-stu-id="212e6-106">The enhanced Teams platform allows partners to integrate device capabilities, such as camera, QR or barcode scanner, photo gallery, microphone, and location with their web apps.</span></span> <span data-ttu-id="212e6-107">Эта интеграция уменьшает барьер на пути разработки приложений, ускоряет цикл разработки и создает новые сценарии или случаи использования для сообщества разработчиков.</span><span class="sxs-lookup"><span data-stu-id="212e6-107">This integration reduces the barrier to app development, speeds-up development-cycle, and creates new scenarios or use-cases for the developer community.</span></span>

## <a name="native-device-capabilities"></a><span data-ttu-id="212e6-108">Возможности родных устройств</span><span class="sxs-lookup"><span data-stu-id="212e6-108">Native device capabilities</span></span>

<span data-ttu-id="212e6-109">Мобильное или настольное устройство имеет встроенные устройства, такие как камера и микрофон, называемые возможностями.</span><span class="sxs-lookup"><span data-stu-id="212e6-109">A mobile or desktop device has built-in devices, such as a camera and microphone, called capabilities.</span></span> <span data-ttu-id="212e6-110">Вы можете получить доступ к следующим возможностям устройства на мобильном или рабочем столе через специальные API, [доступные в Microsoft Teams JavaScript SDK:](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="212e6-110">You can access the following device capabilities on mobile or desktop through dedicated APIs available in [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true):</span></span>
* <span data-ttu-id="212e6-111">Возможности мультимедиа, такие как</span><span class="sxs-lookup"><span data-stu-id="212e6-111">Media capabilities, such as</span></span>
    * <span data-ttu-id="212e6-112">фотоаппарат</span><span class="sxs-lookup"><span data-stu-id="212e6-112">Camera</span></span>
    * <span data-ttu-id="212e6-113">микрофон</span><span class="sxs-lookup"><span data-stu-id="212e6-113">Microphone</span></span>
    * <span data-ttu-id="212e6-114">Галерея</span><span class="sxs-lookup"><span data-stu-id="212e6-114">Gallery</span></span>
    * <span data-ttu-id="212e6-115">Сканер штрих-кодов или штрих-кодов</span><span class="sxs-lookup"><span data-stu-id="212e6-115">QR or barcode scanner</span></span>
* <span data-ttu-id="212e6-116">Местонахождение</span><span class="sxs-lookup"><span data-stu-id="212e6-116">Location</span></span>

<span data-ttu-id="212e6-117">Получив доступ к возможностям устройства, вы можете интегрировать их с Teams платформой для повышения совместной работы.</span><span class="sxs-lookup"><span data-stu-id="212e6-117">After getting access to the device capabilities, you can integrate them with Teams platform to enhance the collaborative experience.</span></span> 

## <a name="request-device-permissions"></a><span data-ttu-id="212e6-118">Запрос разрешений устройства</span><span class="sxs-lookup"><span data-stu-id="212e6-118">Request device permissions</span></span>

<span data-ttu-id="212e6-119">Используйте инструменты, [присутствующие Microsoft Teams JavaScript клиента SDK,](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) чтобы запросить [необходимые разрешения](native-device-permissions.md) для доступа к родным возможностям устройства.</span><span class="sxs-lookup"><span data-stu-id="212e6-119">Use the tools present in [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) to request the required  [permissions](native-device-permissions.md) for accessing the native device capabilities.</span></span> <span data-ttu-id="212e6-120">Хотя доступ к этим возможностям является стандартным в современных веб-браузерах, вы должны Teams о возможностях, которые вы используете, обновляя манифест приложения.</span><span class="sxs-lookup"><span data-stu-id="212e6-120">While access to these capabilities is standard in modern web browsers, you must inform Teams about the capabilities that you are using by updating your app manifest.</span></span> <span data-ttu-id="212e6-121">Это обновление позволяет запрашивать разрешения, пока приложение работает на Teams или настольных клиентах.</span><span class="sxs-lookup"><span data-stu-id="212e6-121">This update allows you to request permissions while your app runs on Teams mobile or desktop clients.</span></span>
 
 ## <a name="integrate-device-capabilities"></a><span data-ttu-id="212e6-122">Интеграция возможностей устройств</span><span class="sxs-lookup"><span data-stu-id="212e6-122">Integrate device capabilities</span></span>

<span data-ttu-id="212e6-123">После получения доступа к возможностям устройства используйте Teams API для интеграции [медиа-возможностей](mobile-camera-image-permissions.md) с Teams платформой для улучшения пользовательского опыта.</span><span class="sxs-lookup"><span data-stu-id="212e6-123">After getting access to device capabilities, use Teams media capability APIs to [integrate media capabilities](mobile-camera-image-permissions.md) with Teams platform to enhance the user experience.</span></span> <span data-ttu-id="212e6-124">Эти интегрированные возможности позволяют приложению:</span><span class="sxs-lookup"><span data-stu-id="212e6-124">These integrated capabilities allow your app to:</span></span>

* <span data-ttu-id="212e6-125">Захват и общий просмотр изображений.</span><span class="sxs-lookup"><span data-stu-id="212e6-125">Capture and share images.</span></span>
* <span data-ttu-id="212e6-126">Сканирование qR или штрих-кода с помощью [сканера управления.](qr-barcode-scanner-capability.md)</span><span class="sxs-lookup"><span data-stu-id="212e6-126">Scan QR or barcode using [scanner control](qr-barcode-scanner-capability.md).</span></span>
* <span data-ttu-id="212e6-127">Запись звука через микрофон.</span><span class="sxs-lookup"><span data-stu-id="212e6-127">Record audio through microphone.</span></span>
* <span data-ttu-id="212e6-128">Поделитесь местоположением [с помощью сборщика местоположения.](location-capability.md)</span><span class="sxs-lookup"><span data-stu-id="212e6-128">Share location using [location picker](location-capability.md).</span></span>
