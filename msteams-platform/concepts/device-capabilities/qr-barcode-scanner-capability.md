---
title: Интеграция функции сканирования QR- или штрихкода
author: Rajeshwari-v
description: Использование SDK клиента Teams JavaScript для использования возможностей сканера QR или штрихкодов
keywords: QR-код qr code qrcode barcode сканера штрихкода камеры позволяет родных разрешений устройства
localization_priority: Normal
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: 579137f31dd929a6105dd7bcc2d46d84c145ef50
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020739"
---
# <a name="integrate-qr-or-barcode-scanner-capability"></a><span data-ttu-id="78eda-104">Интеграция функции сканирования QR- или штрихкода</span><span class="sxs-lookup"><span data-stu-id="78eda-104">Integrate QR or barcode scanner capability</span></span> 

<span data-ttu-id="78eda-105">В этом документе содержится руководство по интеграции возможностей сканера QR или штрихкодов.</span><span class="sxs-lookup"><span data-stu-id="78eda-105">This document guides you on how to integrate the QR or barcode scanner capability.</span></span> 

<span data-ttu-id="78eda-106">Штрихкод — это метод представления данных в визуальной и машинной форме.</span><span class="sxs-lookup"><span data-stu-id="78eda-106">Barcode is a method of representing data in a visual and machine-readable form.</span></span> <span data-ttu-id="78eda-107">Штрихкод содержит сведения о продукте, например типе, размере, изготовителе и стране происхождения в виде баров и пробелов.</span><span class="sxs-lookup"><span data-stu-id="78eda-107">The barcode contains information about a product, such as a type, size, manufacturer, and Country of origin in the form of bars and spaces.</span></span> <span data-ttu-id="78eda-108">Код читается с помощью оптического сканера на вашей родной камере устройства.</span><span class="sxs-lookup"><span data-stu-id="78eda-108">The code is read using the optical scanner on your native device camera.</span></span> <span data-ttu-id="78eda-109">Для более насыщенной совместной работы можно интегрировать функцию сканера QR или штрихкода, предоставляемую на платформе Teams, с приложением Teams.</span><span class="sxs-lookup"><span data-stu-id="78eda-109">For a richer collaborative experience, you can integrate the QR or barcode scanner capability provided in the Teams platform with your Teams app.</span></span>   

<span data-ttu-id="78eda-110">Вы можете использовать [клиентскую SDK Microsoft Teams JavaScript,](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)которая предоставляет средства, необходимые вашему приложению для доступа к возможностям родного [устройства пользователя.](native-device-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="78eda-110">You can use [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), which provides the tools necessary for your app to access the user’s [native device capabilities](native-device-permissions.md).</span></span> <span data-ttu-id="78eda-111">Используйте `scanBarCode` API для интеграции возможностей сканера в приложении.</span><span class="sxs-lookup"><span data-stu-id="78eda-111">Use the `scanBarCode` API to integrate the scanner capability within your app.</span></span> 

## <a name="advantage-of-integrating-qr-or-barcode-scanner-capability"></a><span data-ttu-id="78eda-112">Преимущество интеграции функции сканера QR или штрихкода</span><span class="sxs-lookup"><span data-stu-id="78eda-112">Advantage of integrating QR or barcode scanner capability</span></span>

<span data-ttu-id="78eda-113">Ниже следующую возможность интеграции возможностей сканера QR или штрихкодов:</span><span class="sxs-lookup"><span data-stu-id="78eda-113">Following are the advantages of integration of QR or barcode scanner capabilities:</span></span> 

* <span data-ttu-id="78eda-114">Интеграция позволяет разработчикам веб-приложений на платформе Teams использовать функции сканирования QR или штрихкодов с помощью SDK клиента Teams JavaScript.</span><span class="sxs-lookup"><span data-stu-id="78eda-114">The integration allows web app developers on Teams platform to leverage QR or barcode scanning functionality with Teams JavaScript client SDK.</span></span>
* <span data-ttu-id="78eda-115">С помощью этой функции пользователю необходимо выровнять QR или штрих-код в кадре в центре пользовательского интерфейса сканера, и код автоматически сканируется.</span><span class="sxs-lookup"><span data-stu-id="78eda-115">With this feature, the user only needs to align a QR or barcode within a frame at the center of the scanner UI and the code gets scanned automatically.</span></span> <span data-ttu-id="78eda-116">Хранимые данные делятся с веб-приложением вызова.</span><span class="sxs-lookup"><span data-stu-id="78eda-116">The stored data is shared back with the calling web app.</span></span> <span data-ttu-id="78eda-117">Это позволяет избежать неудобств и человеческих ошибок при вводе длинных кодов продуктов или других соответствующих сведений вручную.</span><span class="sxs-lookup"><span data-stu-id="78eda-117">This avoids the inconvenience and human-errors of entering lengthy product codes or other relevant information manually.</span></span>

<span data-ttu-id="78eda-118">Чтобы интегрировать возможности сканера QR или штрихкода, необходимо обновить файл манифеста приложения и вызвать `scanBarCode` API.</span><span class="sxs-lookup"><span data-stu-id="78eda-118">To integrate QR or barcode scanner capability, you must update the app manifest file and call the `scanBarCode` API.</span></span> <span data-ttu-id="78eda-119">Для эффективной интеграции необходимо хорошо [](#code-snippet) понимать фрагмент кода для вызова API, который позволяет использовать родной QR или `scanBarCode` сканер штрихкодов.</span><span class="sxs-lookup"><span data-stu-id="78eda-119">For effective integration, you must have a good understanding of [code snippet](#code-snippet) for calling the `scanBarCode` API, which allows you to use native QR or barcode scanner capability.</span></span> <span data-ttu-id="78eda-120">API предоставляет ошибку для неподдержаемой стандарта штрихкода.</span><span class="sxs-lookup"><span data-stu-id="78eda-120">The API gives an error for an unsupported barcode standard.</span></span>
<span data-ttu-id="78eda-121">Важно ознакомиться с ошибками [ответа API](#error-handling) для обработки ошибок в приложении Teams.</span><span class="sxs-lookup"><span data-stu-id="78eda-121">It is important to familiarize yourself with the [API response errors](#error-handling) to handle the errors in your Teams app.</span></span>

> [!NOTE] 
> <span data-ttu-id="78eda-122">В настоящее время поддержка Microsoft Teams для функции сканера QR или штрихкода доступна только для мобильных клиентов.</span><span class="sxs-lookup"><span data-stu-id="78eda-122">Currently, Microsoft Teams support for QR or barcode scanner capability is only available for mobile clients.</span></span>

## <a name="update-manifest"></a><span data-ttu-id="78eda-123">Манифест обновления</span><span class="sxs-lookup"><span data-stu-id="78eda-123">Update manifest</span></span>

<span data-ttu-id="78eda-124">Обновите приложение Teams [manifest.jsфайле,](../../resources/schema/manifest-schema.md#devicepermissions) добавив `devicePermissions` свойство и указав `media` .</span><span class="sxs-lookup"><span data-stu-id="78eda-124">Update your Teams app [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) file by adding the `devicePermissions` property and specifying `media`.</span></span> <span data-ttu-id="78eda-125">Это позволяет приложению запросить необходимые разрешения у пользователей, прежде чем они начнут использовать функцию сканера QR или штрихкода.</span><span class="sxs-lookup"><span data-stu-id="78eda-125">It allows your app to ask for requisite permissions from users before they start using  the QR or barcode scanner capability.</span></span>

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> <span data-ttu-id="78eda-126">Запрос **разрешений** автоматически отображается при инициировании соответствующего API Teams.</span><span class="sxs-lookup"><span data-stu-id="78eda-126">The **Request Permissions** prompt is automatically displayed when a relevant Teams API is initiated.</span></span> <span data-ttu-id="78eda-127">Дополнительные сведения см. в [запросе разрешений устройств.](native-device-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="78eda-127">For more information, see [Request device permissions](native-device-permissions.md).</span></span>

## <a name="scanbarcode-api"></a><span data-ttu-id="78eda-128">ScanBarCode API</span><span class="sxs-lookup"><span data-stu-id="78eda-128">ScanBarCode API</span></span>

<span data-ttu-id="78eda-129">API вызывает управление сканером, которое позволяет пользователю сканировать различные типы штрихкода и возвращает результат `ScanBarCode` в качестве строки.</span><span class="sxs-lookup"><span data-stu-id="78eda-129">The `ScanBarCode` API invokes scanner control that enables the user to scan different types of barcode, and returns the result as a string.</span></span>

<span data-ttu-id="78eda-130">Чтобы настроить функцию сканирования штрихкодов, необязательная конфигурация штрихкода передается в качестве ввода `ScanBarCode` в API.</span><span class="sxs-lookup"><span data-stu-id="78eda-130">To customize the barcode scanning experience, optional barcode configuration is passed as input to `ScanBarCode` API.</span></span> <span data-ttu-id="78eda-131">Вы можете указать интервал времени сканирования в секундах с помощью `timeOutIntervalInSec` .</span><span class="sxs-lookup"><span data-stu-id="78eda-131">You can specify the scan time-out interval in seconds using `timeOutIntervalInSec`.</span></span> <span data-ttu-id="78eda-132">Его значение по умолчанию — 30 секунд, а максимальное — 60 секунд.</span><span class="sxs-lookup"><span data-stu-id="78eda-132">Its default value is 30 seconds and the maximum value is 60 seconds.</span></span>

<span data-ttu-id="78eda-133">API **scanBarCode()** поддерживает следующие типы штрихкодов:</span><span class="sxs-lookup"><span data-stu-id="78eda-133">The **scanBarCode()** API supports the following barcode types:</span></span>

| <span data-ttu-id="78eda-134">Тип штрихкода</span><span class="sxs-lookup"><span data-stu-id="78eda-134">Barcode Type</span></span> | <span data-ttu-id="78eda-135">Поддерживается на Android</span><span class="sxs-lookup"><span data-stu-id="78eda-135">Supported on Android</span></span> | <span data-ttu-id="78eda-136">Поддерживается на iOS</span><span class="sxs-lookup"><span data-stu-id="78eda-136">Supported on iOS</span></span> |
| ---------- | ---------- | ------------ |
| <span data-ttu-id="78eda-137">Codebar</span><span class="sxs-lookup"><span data-stu-id="78eda-137">Codebar</span></span> | <span data-ttu-id="78eda-138">Да</span><span class="sxs-lookup"><span data-stu-id="78eda-138">Yes</span></span> | <span data-ttu-id="78eda-139">Нет</span><span class="sxs-lookup"><span data-stu-id="78eda-139">No</span></span> |
| <span data-ttu-id="78eda-140">Код 39</span><span class="sxs-lookup"><span data-stu-id="78eda-140">Code 39</span></span> | <span data-ttu-id="78eda-141">Да</span><span class="sxs-lookup"><span data-stu-id="78eda-141">Yes</span></span> | <span data-ttu-id="78eda-142">Да</span><span class="sxs-lookup"><span data-stu-id="78eda-142">Yes</span></span> | 
| <span data-ttu-id="78eda-143">Код 93</span><span class="sxs-lookup"><span data-stu-id="78eda-143">Code 93</span></span> | <span data-ttu-id="78eda-144">Да</span><span class="sxs-lookup"><span data-stu-id="78eda-144">Yes</span></span> | <span data-ttu-id="78eda-145">Да</span><span class="sxs-lookup"><span data-stu-id="78eda-145">Yes</span></span> |
| <span data-ttu-id="78eda-146">Код 128</span><span class="sxs-lookup"><span data-stu-id="78eda-146">Code 128</span></span> | <span data-ttu-id="78eda-147">Да</span><span class="sxs-lookup"><span data-stu-id="78eda-147">Yes</span></span> | <span data-ttu-id="78eda-148">Да</span><span class="sxs-lookup"><span data-stu-id="78eda-148">Yes</span></span> |
| <span data-ttu-id="78eda-149">EAN-13</span><span class="sxs-lookup"><span data-stu-id="78eda-149">EAN-13</span></span> | <span data-ttu-id="78eda-150">Да</span><span class="sxs-lookup"><span data-stu-id="78eda-150">Yes</span></span> | <span data-ttu-id="78eda-151">Да</span><span class="sxs-lookup"><span data-stu-id="78eda-151">Yes</span></span> |
| <span data-ttu-id="78eda-152">EAN-8</span><span class="sxs-lookup"><span data-stu-id="78eda-152">EAN-8</span></span> | <span data-ttu-id="78eda-153">Да</span><span class="sxs-lookup"><span data-stu-id="78eda-153">Yes</span></span> | <span data-ttu-id="78eda-154">Да</span><span class="sxs-lookup"><span data-stu-id="78eda-154">Yes</span></span> |
| <span data-ttu-id="78eda-155">ITF</span><span class="sxs-lookup"><span data-stu-id="78eda-155">ITF</span></span> | <span data-ttu-id="78eda-156">Нет</span><span class="sxs-lookup"><span data-stu-id="78eda-156">No</span></span> | <span data-ttu-id="78eda-157">Да</span><span class="sxs-lookup"><span data-stu-id="78eda-157">Yes</span></span> |
| <span data-ttu-id="78eda-158">Код QR</span><span class="sxs-lookup"><span data-stu-id="78eda-158">QR Code</span></span> | <span data-ttu-id="78eda-159">Да</span><span class="sxs-lookup"><span data-stu-id="78eda-159">Yes</span></span> | <span data-ttu-id="78eda-160">Да</span><span class="sxs-lookup"><span data-stu-id="78eda-160">Yes</span></span> |
| <span data-ttu-id="78eda-161">Расширение RSS</span><span class="sxs-lookup"><span data-stu-id="78eda-161">RSS Expanded</span></span> | <span data-ttu-id="78eda-162">Да</span><span class="sxs-lookup"><span data-stu-id="78eda-162">Yes</span></span> | <span data-ttu-id="78eda-163">Нет</span><span class="sxs-lookup"><span data-stu-id="78eda-163">No</span></span> |
| <span data-ttu-id="78eda-164">RSS-14</span><span class="sxs-lookup"><span data-stu-id="78eda-164">RSS-14</span></span> | <span data-ttu-id="78eda-165">Да</span><span class="sxs-lookup"><span data-stu-id="78eda-165">Yes</span></span> | <span data-ttu-id="78eda-166">Нет</span><span class="sxs-lookup"><span data-stu-id="78eda-166">No</span></span> |
| <span data-ttu-id="78eda-167">UPC-A</span><span class="sxs-lookup"><span data-stu-id="78eda-167">UPC-A</span></span> | <span data-ttu-id="78eda-168">Да</span><span class="sxs-lookup"><span data-stu-id="78eda-168">Yes</span></span> | <span data-ttu-id="78eda-169">Да</span><span class="sxs-lookup"><span data-stu-id="78eda-169">Yes</span></span> |
| <span data-ttu-id="78eda-170">UPC-E</span><span class="sxs-lookup"><span data-stu-id="78eda-170">UPC-E</span></span> | <span data-ttu-id="78eda-171">Да</span><span class="sxs-lookup"><span data-stu-id="78eda-171">Yes</span></span> | <span data-ttu-id="78eda-172">Да</span><span class="sxs-lookup"><span data-stu-id="78eda-172">Yes</span></span> |

<span data-ttu-id="78eda-173">**Опыт работы с веб-приложением для `ScanBarCode` API для возможностей веб-приложения** для QR или сканера штрихкодов для 
 ![ функции сканера qr или штрихкодов](../../assets/images/tabs/qr-barcode-scanner-capability.png)</span><span class="sxs-lookup"><span data-stu-id="78eda-173">**Web app experience for `ScanBarCode` API for QR or barcode scanner capability**
![web app experience for qr or barcode scanner capability](../../assets/images/tabs/qr-barcode-scanner-capability.png)</span></span>

## <a name="error-handling"></a><span data-ttu-id="78eda-174">Обработка ошибок</span><span class="sxs-lookup"><span data-stu-id="78eda-174">Error handling</span></span>

<span data-ttu-id="78eda-175">Необходимо обеспечить надлежащее обработку этих ошибок в приложении Teams.</span><span class="sxs-lookup"><span data-stu-id="78eda-175">You must ensure to handle these errors appropriately in your Teams app.</span></span> <span data-ttu-id="78eda-176">В следующей таблице перечислены коды ошибок и условия, при которых создаются ошибки:</span><span class="sxs-lookup"><span data-stu-id="78eda-176">The following table lists the error codes and the conditions under which the errors are generated:</span></span> 

|<span data-ttu-id="78eda-177">Код ошибки</span><span class="sxs-lookup"><span data-stu-id="78eda-177">Error code</span></span> |  <span data-ttu-id="78eda-178">Имя ошибки</span><span class="sxs-lookup"><span data-stu-id="78eda-178">Error name</span></span>     | <span data-ttu-id="78eda-179">Условие</span><span class="sxs-lookup"><span data-stu-id="78eda-179">Condition</span></span>|
| --------- | --------------- | -------- |
| <span data-ttu-id="78eda-180">**100**</span><span class="sxs-lookup"><span data-stu-id="78eda-180">**100**</span></span> | <span data-ttu-id="78eda-181">NOT_SUPPORTED_ON_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="78eda-181">NOT_SUPPORTED_ON_PLATFORM</span></span> | <span data-ttu-id="78eda-182">API не поддерживается на текущей платформе.</span><span class="sxs-lookup"><span data-stu-id="78eda-182">API is not supported on the current platform.</span></span>|
| <span data-ttu-id="78eda-183">**500**</span><span class="sxs-lookup"><span data-stu-id="78eda-183">**500**</span></span> | <span data-ttu-id="78eda-184">INTERNAL_ERROR</span><span class="sxs-lookup"><span data-stu-id="78eda-184">INTERNAL_ERROR</span></span> | <span data-ttu-id="78eda-185">При выполнении необходимой операции встречаются внутренние ошибки.</span><span class="sxs-lookup"><span data-stu-id="78eda-185">Internal error is encountered while performing the required operation.</span></span>|
| <span data-ttu-id="78eda-186">**1000**</span><span class="sxs-lookup"><span data-stu-id="78eda-186">**1000**</span></span> | <span data-ttu-id="78eda-187">PERMISSION_DENIED</span><span class="sxs-lookup"><span data-stu-id="78eda-187">PERMISSION_DENIED</span></span> |<span data-ttu-id="78eda-188">Пользователю отказано в разрешении.</span><span class="sxs-lookup"><span data-stu-id="78eda-188">Permission is denied by the user.</span></span>|
| <span data-ttu-id="78eda-189">**3000**</span><span class="sxs-lookup"><span data-stu-id="78eda-189">**3000**</span></span> | <span data-ttu-id="78eda-190">NO_HW_SUPPORT</span><span class="sxs-lookup"><span data-stu-id="78eda-190">NO_HW_SUPPORT</span></span> | <span data-ttu-id="78eda-191">Оборудование не поддерживает эту возможность.</span><span class="sxs-lookup"><span data-stu-id="78eda-191">Underlying hardware does not support the capability.</span></span>|
| <span data-ttu-id="78eda-192">**4000**</span><span class="sxs-lookup"><span data-stu-id="78eda-192">**4000**</span></span> | <span data-ttu-id="78eda-193">INVALID_ARGUMENTS</span><span class="sxs-lookup"><span data-stu-id="78eda-193">INVALID_ARGUMENTS</span></span> | <span data-ttu-id="78eda-194">Один или несколько аргументов являются недействительными.</span><span class="sxs-lookup"><span data-stu-id="78eda-194">One or more arguments are invalid.</span></span>|
| <span data-ttu-id="78eda-195">**8000**</span><span class="sxs-lookup"><span data-stu-id="78eda-195">**8000**</span></span> | <span data-ttu-id="78eda-196">USER_ABORT</span><span class="sxs-lookup"><span data-stu-id="78eda-196">USER_ABORT</span></span> |<span data-ttu-id="78eda-197">Пользователь прерывает операцию.</span><span class="sxs-lookup"><span data-stu-id="78eda-197">User aborts the operation.</span></span>|
| <span data-ttu-id="78eda-198">**8001**</span><span class="sxs-lookup"><span data-stu-id="78eda-198">**8001**</span></span> | <span data-ttu-id="78eda-199">OPERATION_TIMED_OUT</span><span class="sxs-lookup"><span data-stu-id="78eda-199">OPERATION_TIMED_OUT</span></span> | <span data-ttu-id="78eda-200">Не удалось обнаружить штрих-код в заданный интервал времени.</span><span class="sxs-lookup"><span data-stu-id="78eda-200">Could not detect the barcode in the given time interval.</span></span>|
| <span data-ttu-id="78eda-201">**9000**</span><span class="sxs-lookup"><span data-stu-id="78eda-201">**9000**</span></span> | <span data-ttu-id="78eda-202">OLD_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="78eda-202">OLD_PLATFORM</span></span> | <span data-ttu-id="78eda-203">Код платформы устарел и не реализует этот API.</span><span class="sxs-lookup"><span data-stu-id="78eda-203">Platform code is outdated and does not implement this API.</span></span>|

## <a name="code-snippet"></a><span data-ttu-id="78eda-204">Фрагмент кода</span><span class="sxs-lookup"><span data-stu-id="78eda-204">Code snippet</span></span>

<span data-ttu-id="78eda-205">**Вызов `ScanBarCode()` API** для сканирования QR или штрихкода с помощью камеры:</span><span class="sxs-lookup"><span data-stu-id="78eda-205">**Calling `ScanBarCode()` API** for scanning QR or barcode using camera:</span></span>

```javascript
const config: microsoftTeams.media.BarCodeConfig = {
  timeOutIntervalInSec: 30};
microsoftTeams.media.scanBarCode((error: microsoftTeams.SdkError, decodedText: string) => {
  if (error) {
    if (error.message) {
      output(" ErrorCode: " + error.errorCode + error.message);
    } else {
      output(" ErrorCode: " + error.errorCode);
    }
  } else if (decodedText) {
    output(decodedText);
  }
}, config);
```

## <a name="see-also"></a><span data-ttu-id="78eda-206">См. также</span><span class="sxs-lookup"><span data-stu-id="78eda-206">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="78eda-207">Интеграция возможностей мультимедиа в Teams</span><span class="sxs-lookup"><span data-stu-id="78eda-207">Integrate media capabilities in Teams</span></span>](mobile-camera-image-permissions.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="78eda-208">Интеграция возможностей расположения в Teams</span><span class="sxs-lookup"><span data-stu-id="78eda-208">Integrate location capabilities in Teams</span></span>](location-capability.md)
