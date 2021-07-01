---
title: Интеграция функций местонахождения
author: Rajeshwari-v
description: Использование SDK Teams JavaScript для использования возможностей расположения
keywords: Возможности карты расположения для родных разрешений устройств
ms.topic: conceptual
localization_priority: Normal
ms.author: surbhigupta
ms.openlocfilehash: 3e6c4bda9a1a0024380cb295cd280db1d630f019
ms.sourcegitcommit: 059d22c436ee9b07a61561ff71e03e1c23ff40b8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/30/2021
ms.locfileid: "53211613"
---
# <a name="integrate-location-capabilities"></a><span data-ttu-id="b07d7-104">Интеграция функций местонахождения</span><span class="sxs-lookup"><span data-stu-id="b07d7-104">Integrate location capabilities</span></span> 

<span data-ttu-id="b07d7-105">Вы можете интегрировать возможности расположения родного устройства с Teams приложением.</span><span class="sxs-lookup"><span data-stu-id="b07d7-105">You can integrate the location capabilities of native device with your Teams app.</span></span>  

<span data-ttu-id="b07d7-106">Вы можете [использовать Microsoft Teams JavaScript клиента SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), который предоставляет средства, необходимые для вашего приложения, чтобы получить доступ к возможностям родного [устройства пользователя](native-device-permissions.md).</span><span class="sxs-lookup"><span data-stu-id="b07d7-106">You can use [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), which provides the tools necessary for your app to access the user’s [native device capabilities](native-device-permissions.md).</span></span> <span data-ttu-id="b07d7-107">Используйте API расположения, такие как [getLocation](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) и [showLocation,](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#showLocation_Location___error__SdkError__status__boolean_____void_&preserve-view=true) чтобы интегрировать возможности в приложении.</span><span class="sxs-lookup"><span data-stu-id="b07d7-107">Use the location APIs, such as [getLocation](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) and [showLocation](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#showLocation_Location___error__SdkError__status__boolean_____void_&preserve-view=true) to integrate the capabilities within your app.</span></span> 

## <a name="advantages-of-integrating-location-capabilities"></a><span data-ttu-id="b07d7-108">Преимущества интеграции возможностей расположения</span><span class="sxs-lookup"><span data-stu-id="b07d7-108">Advantages of integrating location capabilities</span></span>

<span data-ttu-id="b07d7-109">Основное преимущество интеграции возможностей расположения в Teams приложений заключается в том, что он позволяет разработчикам веб-приложений на Teams платформе использовать функции расположения с помощью SDK Microsoft Teams JavaScript.</span><span class="sxs-lookup"><span data-stu-id="b07d7-109">The main advantage of integrating location capabilities in your Teams apps is that it allows web app developers on Teams platform to leverage location functionality with Microsoft Teams JavaScript client SDK.</span></span> 

<span data-ttu-id="b07d7-110">В следующих примерах покажите, как интеграция возможностей расположения используется в различных сценариях:</span><span class="sxs-lookup"><span data-stu-id="b07d7-110">Following examples show how the integration of location capabilities is used in different scenarios:</span></span>
* <span data-ttu-id="b07d7-111">На фабрике руководитель может отслеживать посещаемость рабочих, попросив их сделать селфи в непосредственной близости от фабрики и поделиться им через указанное приложение.</span><span class="sxs-lookup"><span data-stu-id="b07d7-111">In a factory, the supervisor can track the attendance of workers by asking them to take a selfie in the vicinity of the factory and share it through the specified app.</span></span> <span data-ttu-id="b07d7-112">Данные о расположении также захватываются и отправляются вместе с изображением.</span><span class="sxs-lookup"><span data-stu-id="b07d7-112">The location data also gets captured and sent along with the image.</span></span>
* <span data-ttu-id="b07d7-113">Возможности расположения позволяют обслуживаемом персоналу поставщика услуг обмениваться с руководством подлинными данными о состоянии здоровья вышек сотовой связи.</span><span class="sxs-lookup"><span data-stu-id="b07d7-113">The location capabilities enables the maintenance staff of a service provider to share authentic health data of cellular towers with the management.</span></span> <span data-ttu-id="b07d7-114">Руководство может сравнить любое несоответствие между захваченными сведениями о расположении и данными, представленными сотрудниками службы технического обслуживания.</span><span class="sxs-lookup"><span data-stu-id="b07d7-114">The management can compare any mismatch between captured location information and the data submitted by maintenance staff.</span></span>

<span data-ttu-id="b07d7-115">Чтобы интегрировать возможности расположения, необходимо обновить файл манифеста приложения и вызвать API.</span><span class="sxs-lookup"><span data-stu-id="b07d7-115">To integrate location capabilities, you must update the app manifest file and call the APIs.</span></span> <span data-ttu-id="b07d7-116">Для эффективной интеграции необходимо хорошо [](#code-snippets) понимать фрагменты кода для вызова API расположения.</span><span class="sxs-lookup"><span data-stu-id="b07d7-116">For effective integration, you must have a good understanding of [code snippets](#code-snippets) for calling the location APIs.</span></span> <span data-ttu-id="b07d7-117">Важно ознакомиться с ошибками [ответа API](#error-handling) для обработки ошибок в Teams приложении.</span><span class="sxs-lookup"><span data-stu-id="b07d7-117">It is important to familiarize yourself with the [API response errors](#error-handling) to handle the errors in your Teams app.</span></span>

> [!NOTE] 
> <span data-ttu-id="b07d7-118">В настоящее Microsoft Teams поддержка возможностей расположения доступна только для мобильных клиентов.</span><span class="sxs-lookup"><span data-stu-id="b07d7-118">Currently, Microsoft Teams support for location capabilities is available for mobile clients only.</span></span>

## <a name="update-manifest"></a><span data-ttu-id="b07d7-119">Манифест обновления</span><span class="sxs-lookup"><span data-stu-id="b07d7-119">Update manifest</span></span>

<span data-ttu-id="b07d7-120">Обновите Teams приложение [manifest.jsфайле,](../../resources/schema/manifest-schema.md#devicepermissions) добавив `devicePermissions` свойство и указав `geolocation` .</span><span class="sxs-lookup"><span data-stu-id="b07d7-120">Update your Teams app [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) file by adding the `devicePermissions` property and specifying `geolocation`.</span></span> <span data-ttu-id="b07d7-121">Это позволяет приложению запросить необходимые разрешения у пользователей, прежде чем они начнут использовать возможности расположения.</span><span class="sxs-lookup"><span data-stu-id="b07d7-121">It allows your app to ask for requisite permissions from users before they start using the location capabilities.</span></span> <span data-ttu-id="b07d7-122">Обновление манифеста приложения:</span><span class="sxs-lookup"><span data-stu-id="b07d7-122">The update for app manifest is as follows:</span></span>

``` json
"devicePermissions": [
    "geolocation",
],
```

> [!NOTE]
> <span data-ttu-id="b07d7-123">Запрос **разрешения запроса** автоматически отображается при Teams API.</span><span class="sxs-lookup"><span data-stu-id="b07d7-123">The **Request Permissions** prompt is automatically displayed when a relevant Teams API is initiated.</span></span> <span data-ttu-id="b07d7-124">Дополнительные сведения см. в [запросе разрешений устройств.](native-device-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="b07d7-124">For more information, see [request device permissions](native-device-permissions.md).</span></span>

## <a name="location-apis"></a><span data-ttu-id="b07d7-125">API расположения</span><span class="sxs-lookup"><span data-stu-id="b07d7-125">Location APIs</span></span>

<span data-ttu-id="b07d7-126">Чтобы включить возможности расположения устройства, необходимо использовать следующий набор API:</span><span class="sxs-lookup"><span data-stu-id="b07d7-126">You must use the following set of APIs to enable your device's location capabilities:</span></span>

| <span data-ttu-id="b07d7-127">API</span><span class="sxs-lookup"><span data-stu-id="b07d7-127">API</span></span>      | <span data-ttu-id="b07d7-128">Описание</span><span class="sxs-lookup"><span data-stu-id="b07d7-128">Description</span></span>   |
| --- | --- |
|[<span data-ttu-id="b07d7-129">getLocation</span><span class="sxs-lookup"><span data-stu-id="b07d7-129">getLocation</span></span>](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) | <span data-ttu-id="b07d7-130">Предоставляет текущее расположение устройства или открывает выбор родного расположения и возвращает выбранное пользователем расположение.</span><span class="sxs-lookup"><span data-stu-id="b07d7-130">Gives user’s current device location or opens native location picker and returns the location chosen by the user.</span></span> |
|[<span data-ttu-id="b07d7-131">showLocation</span><span class="sxs-lookup"><span data-stu-id="b07d7-131">showLocation</span></span>](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#showLocation_Location___error__SdkError__status__boolean_____void_&preserve-view=true) | <span data-ttu-id="b07d7-132">Отображает расположение на карте.</span><span class="sxs-lookup"><span data-stu-id="b07d7-132">Shows location on map.</span></span> |

> [!NOTE]
> <span data-ttu-id="b07d7-133">API `getLocation()` поставляется вместе со [следующими конфигурациями ввода](/javascript/api/@microsoft/teams-js/locationprops?view=msteams-client-js-latest&preserve-view=true)и `allowChooseLocation` `showMap` .</span><span class="sxs-lookup"><span data-stu-id="b07d7-133">The `getLocation()` API comes along with following [input configurations](/javascript/api/@microsoft/teams-js/locationprops?view=msteams-client-js-latest&preserve-view=true), `allowChooseLocation` and `showMap`.</span></span> <br/> <span data-ttu-id="b07d7-134">Если значение верно, пользователи могут выбрать `allowChooseLocation` любое расположение по своему выбору. </span><span class="sxs-lookup"><span data-stu-id="b07d7-134">If the value of `allowChooseLocation` is *true*, then the users can choose any location of their choice.</span></span><br/>  <span data-ttu-id="b07d7-135">Если значение *ложное,* пользователи не могут изменить текущее расположение.</span><span class="sxs-lookup"><span data-stu-id="b07d7-135">If the value is *false*, then the users cannot change their current location.</span></span><br/> <span data-ttu-id="b07d7-136">Если значение `showMap` false, текущее расположение извлекается без отображения карты.</span><span class="sxs-lookup"><span data-stu-id="b07d7-136">If the value of `showMap` is *false*, the current location is fetched without displaying the map.</span></span> <span data-ttu-id="b07d7-137">`showMap`игнорируется, `allowChooseLocation` если установлено, что это *верно.*</span><span class="sxs-lookup"><span data-stu-id="b07d7-137">`showMap` is ignored if `allowChooseLocation` is set to *true*.</span></span>

<span data-ttu-id="b07d7-138">На следующем изображении повеяна возможность расположения веб-приложения:</span><span class="sxs-lookup"><span data-stu-id="b07d7-138">The following image depicts web app experience of location capabilities:</span></span>

![Опыт работы веб-приложения для возможностей расположения](../../assets/images/tabs/location-capability.png)

### <a name="code-snippets"></a><span data-ttu-id="b07d7-140">Фрагменты кода</span><span class="sxs-lookup"><span data-stu-id="b07d7-140">Code snippets</span></span>

<span data-ttu-id="b07d7-141">**Вызов `getLocation` API для получения расположения:**</span><span class="sxs-lookup"><span data-stu-id="b07d7-141">**Calling `getLocation` API to retrieve the location:**</span></span>

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

<span data-ttu-id="b07d7-142">**Вызов `showLocation` API для отображения расположения:**</span><span class="sxs-lookup"><span data-stu-id="b07d7-142">**Calling `showLocation` API to display the location:**</span></span>

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

## <a name="error-handling"></a><span data-ttu-id="b07d7-143">Обработка ошибок</span><span class="sxs-lookup"><span data-stu-id="b07d7-143">Error handling</span></span>

<span data-ttu-id="b07d7-144">Необходимо обеспечить надлежащее обработку этих ошибок в Teams приложении.</span><span class="sxs-lookup"><span data-stu-id="b07d7-144">You must ensure to handle these errors appropriately in your Teams app.</span></span> <span data-ttu-id="b07d7-145">В следующей таблице перечислены коды ошибок и условия, при которых создаются ошибки:</span><span class="sxs-lookup"><span data-stu-id="b07d7-145">The following table lists the error codes and the conditions under which the errors are generated:</span></span> 

|<span data-ttu-id="b07d7-146">Код ошибки</span><span class="sxs-lookup"><span data-stu-id="b07d7-146">Error code</span></span> |  <span data-ttu-id="b07d7-147">Имя ошибки</span><span class="sxs-lookup"><span data-stu-id="b07d7-147">Error name</span></span>     | <span data-ttu-id="b07d7-148">Condition</span><span class="sxs-lookup"><span data-stu-id="b07d7-148">Condition</span></span>|
| --------- | --------------- | -------- |
| <span data-ttu-id="b07d7-149">**100**</span><span class="sxs-lookup"><span data-stu-id="b07d7-149">**100**</span></span> | <span data-ttu-id="b07d7-150">NOT_SUPPORTED_ON_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="b07d7-150">NOT_SUPPORTED_ON_PLATFORM</span></span> | <span data-ttu-id="b07d7-151">API не поддерживается на текущей платформе.</span><span class="sxs-lookup"><span data-stu-id="b07d7-151">API is not supported on the current platform.</span></span>|
| <span data-ttu-id="b07d7-152">**500**</span><span class="sxs-lookup"><span data-stu-id="b07d7-152">**500**</span></span> | <span data-ttu-id="b07d7-153">INTERNAL_ERROR</span><span class="sxs-lookup"><span data-stu-id="b07d7-153">INTERNAL_ERROR</span></span> | <span data-ttu-id="b07d7-154">При выполнении необходимой операции встречаются внутренние ошибки.</span><span class="sxs-lookup"><span data-stu-id="b07d7-154">Internal error is encountered while performing the required operation.</span></span>|
| <span data-ttu-id="b07d7-155">**1000**</span><span class="sxs-lookup"><span data-stu-id="b07d7-155">**1000**</span></span> | <span data-ttu-id="b07d7-156">PERMISSION_DENIED</span><span class="sxs-lookup"><span data-stu-id="b07d7-156">PERMISSION_DENIED</span></span> |<span data-ttu-id="b07d7-157">Пользователю отказано в разрешении на Teams или веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="b07d7-157">User denied location permissions to the Teams App or the web-app .</span></span>|
| <span data-ttu-id="b07d7-158">**4000**</span><span class="sxs-lookup"><span data-stu-id="b07d7-158">**4000**</span></span> | <span data-ttu-id="b07d7-159">INVALID_ARGUMENTS</span><span class="sxs-lookup"><span data-stu-id="b07d7-159">INVALID_ARGUMENTS</span></span> | <span data-ttu-id="b07d7-160">API вызывается с неправильными или недостаточными обязательными аргументами.</span><span class="sxs-lookup"><span data-stu-id="b07d7-160">API is invoked with wrong or insufficient mandatory arguments.</span></span>|
| <span data-ttu-id="b07d7-161">**8000**</span><span class="sxs-lookup"><span data-stu-id="b07d7-161">**8000**</span></span> | <span data-ttu-id="b07d7-162">USER_ABORT</span><span class="sxs-lookup"><span data-stu-id="b07d7-162">USER_ABORT</span></span> |<span data-ttu-id="b07d7-163">Пользователь отменил операцию.</span><span class="sxs-lookup"><span data-stu-id="b07d7-163">User cancelled the operation.</span></span>|
| <span data-ttu-id="b07d7-164">**9000**</span><span class="sxs-lookup"><span data-stu-id="b07d7-164">**9000**</span></span> | <span data-ttu-id="b07d7-165">OLD_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="b07d7-165">OLD_PLATFORM</span></span> | <span data-ttu-id="b07d7-166">Пользователь находится на старой сборке платформы, где нет реализации API.</span><span class="sxs-lookup"><span data-stu-id="b07d7-166">User is on old platform build where implementation of the API is not present.</span></span> <span data-ttu-id="b07d7-167">Обновление сборки должно решить проблему.</span><span class="sxs-lookup"><span data-stu-id="b07d7-167">Upgrading the build should resolve the issue.</span></span>|

## <a name="see-also"></a><span data-ttu-id="b07d7-168">См. также</span><span class="sxs-lookup"><span data-stu-id="b07d7-168">See also</span></span>

* [<span data-ttu-id="b07d7-169">Интеграция возможностей мультимедиа в Teams</span><span class="sxs-lookup"><span data-stu-id="b07d7-169">Integrate media capabilities in Teams</span></span>](mobile-camera-image-permissions.md)
* [<span data-ttu-id="b07d7-170">Интеграция QR-кода или возможности сканера штрихкодов в Teams</span><span class="sxs-lookup"><span data-stu-id="b07d7-170">Integrate QR code or barcode scanner capability in Teams</span></span>](qr-barcode-scanner-capability.md)
* [<span data-ttu-id="b07d7-171">Интеграция возможностей выборщика людей в Teams</span><span class="sxs-lookup"><span data-stu-id="b07d7-171">Integrate People Picker capability in Teams</span></span>](people-picker-capability.md)
