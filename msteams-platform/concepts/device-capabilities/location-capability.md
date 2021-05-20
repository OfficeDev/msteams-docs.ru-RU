---
title: Интеграция функций местонахождения
author: Rajeshwari-v
description: Как использовать Teams JavaScript SDK для использования возможностей определения местоположения
keywords: возможности карты местоположения родных разрешений устройства
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: b85f19e74d0a8121dd290fc395c1018178437b3a
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566189"
---
# <a name="integrate-location-capabilities"></a><span data-ttu-id="048dd-104">Интеграция функций местонахождения</span><span class="sxs-lookup"><span data-stu-id="048dd-104">Integrate location capabilities</span></span> 

<span data-ttu-id="048dd-105">Этот документ поможет вам интегрировать возможности определения местоположения родного устройства с вашим приложением Teams устройства.</span><span class="sxs-lookup"><span data-stu-id="048dd-105">This document guides you on how to integrate the location capabilities of native device with your Teams app.</span></span>  

<span data-ttu-id="048dd-106">Вы можете [Microsoft Teams JavaScript клиента SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), который предоставляет инструменты, необходимые для вашего приложения для доступа к родным [возможностям устройства пользователя.](native-device-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="048dd-106">You can use [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), which provides the tools necessary for your app to access the user’s [native device capabilities](native-device-permissions.md).</span></span> <span data-ttu-id="048dd-107">Используйте API-файлы местоположения, такие [как getLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) [и showLocation,](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#showLocation_Location___error__SdkError__status__boolean_____void_&preserve-view=true) чтобы интегрировать возможности в приложении.</span><span class="sxs-lookup"><span data-stu-id="048dd-107">Use the location APIs, such as [getLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) and [showLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#showLocation_Location___error__SdkError__status__boolean_____void_&preserve-view=true) to integrate the capabilities within your app.</span></span> 

## <a name="advantages-of-integrating-location-capabilities"></a><span data-ttu-id="048dd-108">Преимущества интеграции возможностей определения местоположения</span><span class="sxs-lookup"><span data-stu-id="048dd-108">Advantages of integrating location capabilities</span></span>

<span data-ttu-id="048dd-109">Основным преимуществом интеграции возможностей определения местоположения в приложениях Teams является то, что он позволяет разработчикам веб-приложений на Teams платформе использовать функциональность местоположения с Microsoft Teams JavaScript SDK.</span><span class="sxs-lookup"><span data-stu-id="048dd-109">The main advantage of integrating location capabilities in your Teams apps is that it allows web app developers on Teams platform to leverage location functionality with Microsoft Teams JavaScript client SDK.</span></span> 

<span data-ttu-id="048dd-110">Следующие примеры показывают, как интеграция возможностей местоположения используется в различных сценариях:</span><span class="sxs-lookup"><span data-stu-id="048dd-110">Following examples show how the integration of location capabilities is used in different scenarios:</span></span>
* <span data-ttu-id="048dd-111">На фабрике руководитель может отслеживать посещаемость рабочих, попросив их сделать селфи в непосредственной близости от фабрики и поделиться им через указанное приложение.</span><span class="sxs-lookup"><span data-stu-id="048dd-111">In a factory, the supervisor can track the attendance of workers by asking them to take a selfie in the vicinity of the factory and share it through the specified app.</span></span> <span data-ttu-id="048dd-112">Данные о местоположении также захватовается и отправляются вместе с изображением.</span><span class="sxs-lookup"><span data-stu-id="048dd-112">The location data also gets captured and sent along with the image.</span></span>
* <span data-ttu-id="048dd-113">Возможности определения местоположения позволяют обслуживающему персоналу поставщика услуг обмениваться с руководством подлинными данными о состоянии здоровья сотовых вышек.</span><span class="sxs-lookup"><span data-stu-id="048dd-113">The location capabilities enables the maintenance staff of a service provider to share authentic health data of cellular towers with the management.</span></span> <span data-ttu-id="048dd-114">Руководство может сравнить любое несоответствие между захваченной информацией о местоположении и данными, представленными обслуживающим персоналом.</span><span class="sxs-lookup"><span data-stu-id="048dd-114">The management can compare any mismatch between captured location information and the data submitted by maintenance staff.</span></span>

<span data-ttu-id="048dd-115">Чтобы интегрировать возможности определения местоположения, необходимо обновить файл манифеста приложения и вызвать API.</span><span class="sxs-lookup"><span data-stu-id="048dd-115">To integrate location capabilities, you must update the app manifest file and call the APIs.</span></span> <span data-ttu-id="048dd-116">Для эффективной интеграции необходимо иметь хорошее понимание [фрагментов кода для](#code-snippets) вызова API-кодов местоположения.</span><span class="sxs-lookup"><span data-stu-id="048dd-116">For effective integration, you must have a good understanding of [code snippets](#code-snippets) for calling the location APIs.</span></span> <span data-ttu-id="048dd-117">Важно ознакомиться с ошибками ответа [API для обработки](#error-handling) ошибок в вашем приложении Teams api.</span><span class="sxs-lookup"><span data-stu-id="048dd-117">It is important to familiarize yourself with the [API response errors](#error-handling) to handle the errors in your Teams app.</span></span>

> [!NOTE] 
> <span data-ttu-id="048dd-118">В настоящее Microsoft Teams поддержка возможностей определения местоположения доступна только для мобильных клиентов.</span><span class="sxs-lookup"><span data-stu-id="048dd-118">Currently, Microsoft Teams support for location capabilities is only available for mobile clients.</span></span>

## <a name="update-manifest"></a><span data-ttu-id="048dd-119">Манифест обновления</span><span class="sxs-lookup"><span data-stu-id="048dd-119">Update manifest</span></span>

<span data-ttu-id="048dd-120">Обновите Teams приложение [manifest.jsфайле,](../../resources/schema/manifest-schema.md#devicepermissions) добавив `devicePermissions` свойство и указав `geolocation` .</span><span class="sxs-lookup"><span data-stu-id="048dd-120">Update your Teams app [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) file by adding the `devicePermissions` property and specifying `geolocation`.</span></span> <span data-ttu-id="048dd-121">Это позволяет вашему приложению запрашивать необходимые разрешения у пользователей, прежде чем они начнут использовать возможности определения местоположения.</span><span class="sxs-lookup"><span data-stu-id="048dd-121">It allows your app to ask for requisite permissions from users before they start using the location capabilities.</span></span>

``` json
"devicePermissions": [
    "geolocation",
],
```

> [!NOTE]
> <span data-ttu-id="048dd-122">Запрос **разрешений автоматически** отображается при инициировании Teams API.</span><span class="sxs-lookup"><span data-stu-id="048dd-122">The **Request Permissions** prompt is automatically displayed when a relevant Teams API is initiated.</span></span> <span data-ttu-id="048dd-123">Для получения дополнительной информации [см.](native-device-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="048dd-123">For more information, see [request device permissions](native-device-permissions.md).</span></span>

## <a name="location-apis"></a><span data-ttu-id="048dd-124">Api-файлы местоположения</span><span class="sxs-lookup"><span data-stu-id="048dd-124">Location APIs</span></span>

<span data-ttu-id="048dd-125">Для определения возможностей определения местоположения устройства необходимо использовать следующий набор API:</span><span class="sxs-lookup"><span data-stu-id="048dd-125">You must use the following set of APIs to enable your device's location capabilities:</span></span>

| <span data-ttu-id="048dd-126">API</span><span class="sxs-lookup"><span data-stu-id="048dd-126">API</span></span>      | <span data-ttu-id="048dd-127">Описание</span><span class="sxs-lookup"><span data-stu-id="048dd-127">Description</span></span>   |
| --- | --- |
|[<span data-ttu-id="048dd-128">getLocation</span><span class="sxs-lookup"><span data-stu-id="048dd-128">getLocation</span></span>](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) | <span data-ttu-id="048dd-129">Предоставляет текущее местоположение устройства пользователя или открывает родной сборщик местоположения и возвращает выбранное пользователем местоположение.</span><span class="sxs-lookup"><span data-stu-id="048dd-129">Gives user’s current device location or opens native location picker and returns the location chosen by the user.</span></span> |
|[<span data-ttu-id="048dd-130">showLocation</span><span class="sxs-lookup"><span data-stu-id="048dd-130">showLocation</span></span>](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#showLocation&preserve-view=true) | <span data-ttu-id="048dd-131">Показывает местоположение на карте.</span><span class="sxs-lookup"><span data-stu-id="048dd-131">Shows location on map.</span></span> |

> [!NOTE]

> <span data-ttu-id="048dd-132">`getLocation()`API поставляется вместе со следующими [конфигурациями ввода,](/javascript/api/@microsoft/teams-js/locationprops?view=msteams-client-js-latest&preserve-view=true) `allowChooseLocation` и `showMap` .</span><span class="sxs-lookup"><span data-stu-id="048dd-132">The `getLocation()` API comes along with following [input configurations](/javascript/api/@microsoft/teams-js/locationprops?view=msteams-client-js-latest&preserve-view=true), `allowChooseLocation` and `showMap`.</span></span> <br/> <span data-ttu-id="048dd-133">Если ценность `allowChooseLocation` *верна, то* пользователи могут выбрать любое место по своему выбору.</span><span class="sxs-lookup"><span data-stu-id="048dd-133">If the value of `allowChooseLocation` is *true*, then the users can choose any location of their choice.</span></span><br/>  <span data-ttu-id="048dd-134">Если значение является *ложным,* то пользователи не могут изменить свое текущее местоположение.</span><span class="sxs-lookup"><span data-stu-id="048dd-134">If the value is *false*, then the users cannot change their current location.</span></span><br/> <span data-ttu-id="048dd-135">Если значение `showMap` является *ложным,* текущее местоположение получается без отображения карты.</span><span class="sxs-lookup"><span data-stu-id="048dd-135">If the value of `showMap` is *false*, the current location is fetched without displaying the map.</span></span> <span data-ttu-id="048dd-136">`showMap` игнорируется, `allowChooseLocation` если установлен на *истинное*.</span><span class="sxs-lookup"><span data-stu-id="048dd-136">`showMap` is ignored if `allowChooseLocation` is set to *true*.</span></span>

<span data-ttu-id="048dd-137">**Веб-приложение для возможностей определения местоположения** 
 ![ веб-приложение опыт для возможностей определения местоположения](../../assets/images/tabs/location-capability.png)</span><span class="sxs-lookup"><span data-stu-id="048dd-137">**Web app experience for location capabilities**
![web app experience for location capabilities](../../assets/images/tabs/location-capability.png)</span></span>

## <a name="error-handling"></a><span data-ttu-id="048dd-138">Обработка ошибок</span><span class="sxs-lookup"><span data-stu-id="048dd-138">Error handling</span></span>

<span data-ttu-id="048dd-139">Вы должны убедиться, что обрабатывать эти ошибки надлежащим образом в Teams приложении.</span><span class="sxs-lookup"><span data-stu-id="048dd-139">You must ensure to handle these errors appropriately in your Teams app.</span></span> <span data-ttu-id="048dd-140">В следующей таблице перечислены коды ошибок и условия, при которых генерируются ошибки:</span><span class="sxs-lookup"><span data-stu-id="048dd-140">The following table lists the error codes and the conditions under which the errors are generated:</span></span> 

|<span data-ttu-id="048dd-141">Код ошибки</span><span class="sxs-lookup"><span data-stu-id="048dd-141">Error code</span></span> |  <span data-ttu-id="048dd-142">Имя ошибки</span><span class="sxs-lookup"><span data-stu-id="048dd-142">Error name</span></span>     | <span data-ttu-id="048dd-143">Condition</span><span class="sxs-lookup"><span data-stu-id="048dd-143">Condition</span></span>|
| --------- | --------------- | -------- |
| <span data-ttu-id="048dd-144">**100**</span><span class="sxs-lookup"><span data-stu-id="048dd-144">**100**</span></span> | <span data-ttu-id="048dd-145">NOT_SUPPORTED_ON_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="048dd-145">NOT_SUPPORTED_ON_PLATFORM</span></span> | <span data-ttu-id="048dd-146">API не поддерживается на текущей платформе.</span><span class="sxs-lookup"><span data-stu-id="048dd-146">API is not supported on the current platform.</span></span>|
| <span data-ttu-id="048dd-147">**500**</span><span class="sxs-lookup"><span data-stu-id="048dd-147">**500**</span></span> | <span data-ttu-id="048dd-148">INTERNAL_ERROR</span><span class="sxs-lookup"><span data-stu-id="048dd-148">INTERNAL_ERROR</span></span> | <span data-ttu-id="048dd-149">Внутренняя ошибка встречается при выполнении требуемой операции.</span><span class="sxs-lookup"><span data-stu-id="048dd-149">Internal error is encountered while performing the required operation.</span></span>|
| <span data-ttu-id="048dd-150">**1000**</span><span class="sxs-lookup"><span data-stu-id="048dd-150">**1000**</span></span> | <span data-ttu-id="048dd-151">PERMISSION_DENIED</span><span class="sxs-lookup"><span data-stu-id="048dd-151">PERMISSION_DENIED</span></span> |<span data-ttu-id="048dd-152">Пользователю было отказано в разрешении на Teams приложение или веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="048dd-152">User denied location permissions to the Teams App or the web-app .</span></span>|
| <span data-ttu-id="048dd-153">**4000**</span><span class="sxs-lookup"><span data-stu-id="048dd-153">**4000**</span></span> | <span data-ttu-id="048dd-154">INVALID_ARGUMENTS</span><span class="sxs-lookup"><span data-stu-id="048dd-154">INVALID_ARGUMENTS</span></span> | <span data-ttu-id="048dd-155">API вызывается с неправильными или недостаточными обязательными аргументами.</span><span class="sxs-lookup"><span data-stu-id="048dd-155">API is invoked with wrong or insufficient mandatory arguments.</span></span>|
| <span data-ttu-id="048dd-156">**8000**</span><span class="sxs-lookup"><span data-stu-id="048dd-156">**8000**</span></span> | <span data-ttu-id="048dd-157">USER_ABORT</span><span class="sxs-lookup"><span data-stu-id="048dd-157">USER_ABORT</span></span> |<span data-ttu-id="048dd-158">Пользователь отменил операцию.</span><span class="sxs-lookup"><span data-stu-id="048dd-158">User cancelled the operation.</span></span>|
| <span data-ttu-id="048dd-159">**9000**</span><span class="sxs-lookup"><span data-stu-id="048dd-159">**9000**</span></span> | <span data-ttu-id="048dd-160">OLD_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="048dd-160">OLD_PLATFORM</span></span> | <span data-ttu-id="048dd-161">Пользователь находится на старой сборке платформы, где реализации API нет.</span><span class="sxs-lookup"><span data-stu-id="048dd-161">User is on old platform build where implementation of the API is not present.</span></span> <span data-ttu-id="048dd-162">Обновление сборки должно решить проблему.</span><span class="sxs-lookup"><span data-stu-id="048dd-162">Upgrading the build should resolve the issue.</span></span>|

## <a name="code-snippets"></a><span data-ttu-id="048dd-163">Фрагменты кода</span><span class="sxs-lookup"><span data-stu-id="048dd-163">Code snippets</span></span>

<span data-ttu-id="048dd-164">**Вызов `getLocation` API для получения местоположения:**</span><span class="sxs-lookup"><span data-stu-id="048dd-164">**Calling `getLocation` API to retrieve the location:**</span></span>

```javascript
let locationProps = {"allowChooseLocation":true,"showMap":true};
microsoftTeams.location.getLocation(locationProps, (err: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
          if (err) {
            output(err);
            return;
          }
          output(JSON.stringify(location));
});
```

<span data-ttu-id="048dd-165">**Вызов `showLocation` API для отображения местоположения:**</span><span class="sxs-lookup"><span data-stu-id="048dd-165">**Calling `showLocation` API to display the location:**</span></span>

```javascript
let location = {"latitude":17,"longitude":17};
microsoftTeams.location.showLocation(location, (err: microsoftTeams.SdkError, result: boolean) => {
          if (err) {
            output(err);
            return;
          }
     output(result);
});
```

## <a name="see-also"></a><span data-ttu-id="048dd-166">См. также</span><span class="sxs-lookup"><span data-stu-id="048dd-166">See also</span></span>

* [<span data-ttu-id="048dd-167">Интеграция медиа-возможностей в Teams</span><span class="sxs-lookup"><span data-stu-id="048dd-167">Integrate media capabilities in Teams</span></span>](mobile-camera-image-permissions.md)
* [<span data-ttu-id="048dd-168">Интеграция возможностей сканирования кода или штрих-кода в Teams</span><span class="sxs-lookup"><span data-stu-id="048dd-168">Integrate QR code or barcode scanner capability in Teams</span></span>](qr-barcode-scanner-capability.md)
