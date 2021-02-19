---
title: Интеграция функции сканера QR или штрихкода
description: Использование SDK клиента Teams JavaScript для использования возможностей сканера QR или штрихкодов
keywords: QR-код qr code qrcode barcode сканера штрихкода камеры позволяет родных разрешений устройства
ms.author: lajanuar
ms.openlocfilehash: 048c6b58fc126d1dd08867605784b6a150737195
ms.sourcegitcommit: 0bb6efb3003a1949288e4601e3301b69e67d4c26
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/18/2021
ms.locfileid: "50295091"
---
# <a name="integrate-qr-or-barcode-scanner-capability"></a><span data-ttu-id="f937c-104">Интеграция функции сканера QR или штрихкода</span><span class="sxs-lookup"><span data-stu-id="f937c-104">Integrate QR or barcode scanner capability</span></span> 

<span data-ttu-id="f937c-105">Штрихкод — это метод представления данных в визуальной и машинной форме.</span><span class="sxs-lookup"><span data-stu-id="f937c-105">Barcode is a method of representing data in a visual and machine-readable form.</span></span> <span data-ttu-id="f937c-106">Штрих-код содержит сведения о продукте, например типе, размере, изготовителе и стране происхождения в виде баров и пробелов.</span><span class="sxs-lookup"><span data-stu-id="f937c-106">The barcode contains information about a product, such as a type, size, manufacturer, and Country of origin in the form of bars and spaces.</span></span> <span data-ttu-id="f937c-107">Код читается с помощью оптического сканера на вашей родной камере устройства.</span><span class="sxs-lookup"><span data-stu-id="f937c-107">The code is read using the optical scanner on your native device camera.</span></span> <span data-ttu-id="f937c-108">Для более насыщенной совместной работы можно интегрировать функцию сканера QR или штрихкода, предоставляемую на платформе Teams, с приложением Teams.</span><span class="sxs-lookup"><span data-stu-id="f937c-108">For a richer collaborative experience, you can integrate the QR or barcode scanner capability provided in the Teams platform with your Teams app.</span></span> <span data-ttu-id="f937c-109">В этом документе содержится руководство по интеграции возможностей.</span><span class="sxs-lookup"><span data-stu-id="f937c-109">This document guides you on how to integrate the capability.</span></span>  

<span data-ttu-id="f937c-110">Вы можете использовать [клиентскую SDK Microsoft Teams JavaScript,](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)которая предоставляет средства, необходимые вашему приложению для доступа к возможностям родного [устройства пользователя.](native-device-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="f937c-110">You can use [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), which provides the tools necessary for your app to access the user’s [native device capabilities](native-device-permissions.md).</span></span> <span data-ttu-id="f937c-111">Используйте `scanBarCode` API для интеграции возможностей сканера в приложении.</span><span class="sxs-lookup"><span data-stu-id="f937c-111">Use the `scanBarCode` API to integrate the scanner capability within your app.</span></span> 

## <a name="advantage-of-integrating-qr-or-barcode-scanner-capability"></a><span data-ttu-id="f937c-112">Преимущество интеграции функции сканера QR или штрихкода</span><span class="sxs-lookup"><span data-stu-id="f937c-112">Advantage of integrating QR or barcode scanner capability</span></span>

* <span data-ttu-id="f937c-113">Интеграция позволяет разработчикам веб-приложений на платформе Teams использовать функции сканирования QR или штрихкодов с помощью SDK клиента Teams JavaScript.</span><span class="sxs-lookup"><span data-stu-id="f937c-113">The integration allows web app developers on Teams platform to leverage QR or barcode scanning functionality with Teams JavaScript client SDK.</span></span>
* <span data-ttu-id="f937c-114">С помощью этой функции пользователю необходимо выровнять QR или штрих-код в кадре в центре пользовательского интерфейса сканера, и код автоматически сканируется.</span><span class="sxs-lookup"><span data-stu-id="f937c-114">With this feature, the user only needs to align a QR or barcode within a frame at the center of the scanner UI and the code gets scanned automatically.</span></span> <span data-ttu-id="f937c-115">Хранимые данные делятся с веб-приложением вызова.</span><span class="sxs-lookup"><span data-stu-id="f937c-115">The stored data is shared back with the calling web app.</span></span> <span data-ttu-id="f937c-116">Это позволяет избежать неудобств и человеческих ошибок при вводе длинных кодов продуктов или других соответствующих сведений вручную.</span><span class="sxs-lookup"><span data-stu-id="f937c-116">This avoids the inconvenience and human-errors of entering lengthy product codes or other relevant information manually.</span></span>

<span data-ttu-id="f937c-117">Чтобы интегрировать возможности сканера QR или штрихкода, необходимо обновить файл манифеста приложения и вызвать `scanBarCode` API.</span><span class="sxs-lookup"><span data-stu-id="f937c-117">To integrate QR or barcode scanner capability, you must update the app manifest file and call the `scanBarCode` API.</span></span> <span data-ttu-id="f937c-118">Для эффективной интеграции необходимо хорошо [](#code-snippet) понимать фрагмент кода для вызова API, который позволяет использовать родной QR или `scanBarCode` сканер штрихкодов.</span><span class="sxs-lookup"><span data-stu-id="f937c-118">For effective integration, you must have a good understanding of [code snippet](#code-snippet) for calling the `scanBarCode` API, which allows you to use native QR or barcode scanner capability.</span></span> <span data-ttu-id="f937c-119">API предоставляет ошибку для неподдержаемой стандарта штрихкода.</span><span class="sxs-lookup"><span data-stu-id="f937c-119">The API gives an error for an unsupported barcode standard.</span></span>
<span data-ttu-id="f937c-120">Важно ознакомиться с ошибками [ответа API](#error-handling) для обработки ошибок в приложении Teams.</span><span class="sxs-lookup"><span data-stu-id="f937c-120">It is important to familiarize yourself with the [API response errors](#error-handling) to handle the errors in your Teams app.</span></span>

> [!NOTE] 
> <span data-ttu-id="f937c-121">В настоящее время поддержка Microsoft Teams для функции сканера QR или штрихкода доступна только для мобильных клиентов.</span><span class="sxs-lookup"><span data-stu-id="f937c-121">Currently, Microsoft Teams support for QR or barcode scanner capability is only available for mobile clients.</span></span>

## <a name="update-manifest"></a><span data-ttu-id="f937c-122">Манифест обновления</span><span class="sxs-lookup"><span data-stu-id="f937c-122">Update manifest</span></span>

<span data-ttu-id="f937c-123">Обновите приложение Teams [manifest.jsфайле,](../../resources/schema/manifest-schema.md#devicepermissions) добавив `devicePermissions` свойство и указав `media` .</span><span class="sxs-lookup"><span data-stu-id="f937c-123">Update your Teams app [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) file by adding the `devicePermissions` property and specifying `media`.</span></span> <span data-ttu-id="f937c-124">Это позволяет приложению запросить необходимые разрешения у пользователей, прежде чем они начнут использовать функцию сканера QR или штрихкода.</span><span class="sxs-lookup"><span data-stu-id="f937c-124">It allows your app to ask for requisite permissions from users before they start using  the QR or barcode scanner capability.</span></span>

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> <span data-ttu-id="f937c-125">Запрос **разрешений** автоматически отображается при инициировании соответствующего API Teams.</span><span class="sxs-lookup"><span data-stu-id="f937c-125">The **Request Permissions** prompt is automatically displayed when a relevant Teams API is initiated.</span></span> <span data-ttu-id="f937c-126">Дополнительные сведения см. в [запросе разрешений устройств.](native-device-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="f937c-126">For more information, see [Request device permissions](native-device-permissions.md).</span></span>

## <a name="scanbarcode-api"></a><span data-ttu-id="f937c-127">ScanBarCode API</span><span class="sxs-lookup"><span data-stu-id="f937c-127">ScanBarCode API</span></span>

<span data-ttu-id="f937c-128">API вызывает управление сканером, которое позволяет пользователю сканировать различные типы штрихкода и возвращает результат `ScanBarCode` в качестве строки.</span><span class="sxs-lookup"><span data-stu-id="f937c-128">The `ScanBarCode` API invokes scanner control that enables the user to scan different types of barcode, and returns the result as a string.</span></span>

<span data-ttu-id="f937c-129">Чтобы настроить функцию сканирования штрихкодов, необязательная конфигурация штрихкода передается в качестве ввода `ScanBarCode` в API.</span><span class="sxs-lookup"><span data-stu-id="f937c-129">To customize the barcode scanning experience, optional barcode configuration is passed as input to `ScanBarCode` API.</span></span> <span data-ttu-id="f937c-130">Вы можете указать интервал времени сканирования в секундах с помощью `timeOutIntervalInSec` .</span><span class="sxs-lookup"><span data-stu-id="f937c-130">You can specify the scan time-out interval in seconds using `timeOutIntervalInSec`.</span></span> <span data-ttu-id="f937c-131">Его значение по умолчанию — 30 секунд, а максимальное — 60 секунд.</span><span class="sxs-lookup"><span data-stu-id="f937c-131">Its default value is 30 seconds and the maximum value is 60 seconds.</span></span>

<span data-ttu-id="f937c-132">API **scanBarCode()** поддерживает следующие типы штрихкодов:</span><span class="sxs-lookup"><span data-stu-id="f937c-132">The **scanBarCode()** API supports the following barcode types:</span></span>

| <span data-ttu-id="f937c-133">Тип штрихкода</span><span class="sxs-lookup"><span data-stu-id="f937c-133">Barcode Type</span></span> | <span data-ttu-id="f937c-134">Поддерживается на Android</span><span class="sxs-lookup"><span data-stu-id="f937c-134">Supported on Android</span></span> | <span data-ttu-id="f937c-135">Поддерживается на iOS</span><span class="sxs-lookup"><span data-stu-id="f937c-135">Supported on iOS</span></span> |
| ---------- | ---------- | ------------ |
| <span data-ttu-id="f937c-136">Codebar</span><span class="sxs-lookup"><span data-stu-id="f937c-136">Codebar</span></span> | <span data-ttu-id="f937c-137">Да</span><span class="sxs-lookup"><span data-stu-id="f937c-137">Yes</span></span> | <span data-ttu-id="f937c-138">Нет</span><span class="sxs-lookup"><span data-stu-id="f937c-138">No</span></span> |
| <span data-ttu-id="f937c-139">Код 39</span><span class="sxs-lookup"><span data-stu-id="f937c-139">Code 39</span></span> | <span data-ttu-id="f937c-140">Да</span><span class="sxs-lookup"><span data-stu-id="f937c-140">Yes</span></span> | <span data-ttu-id="f937c-141">Да</span><span class="sxs-lookup"><span data-stu-id="f937c-141">Yes</span></span> | 
| <span data-ttu-id="f937c-142">Код 93</span><span class="sxs-lookup"><span data-stu-id="f937c-142">Code 93</span></span> | <span data-ttu-id="f937c-143">Да</span><span class="sxs-lookup"><span data-stu-id="f937c-143">Yes</span></span> | <span data-ttu-id="f937c-144">Да</span><span class="sxs-lookup"><span data-stu-id="f937c-144">Yes</span></span> |
| <span data-ttu-id="f937c-145">Код 128</span><span class="sxs-lookup"><span data-stu-id="f937c-145">Code 128</span></span> | <span data-ttu-id="f937c-146">Да</span><span class="sxs-lookup"><span data-stu-id="f937c-146">Yes</span></span> | <span data-ttu-id="f937c-147">Да</span><span class="sxs-lookup"><span data-stu-id="f937c-147">Yes</span></span> |
| <span data-ttu-id="f937c-148">EAN-13</span><span class="sxs-lookup"><span data-stu-id="f937c-148">EAN-13</span></span> | <span data-ttu-id="f937c-149">Да</span><span class="sxs-lookup"><span data-stu-id="f937c-149">Yes</span></span> | <span data-ttu-id="f937c-150">Да</span><span class="sxs-lookup"><span data-stu-id="f937c-150">Yes</span></span> |
| <span data-ttu-id="f937c-151">EAN-8</span><span class="sxs-lookup"><span data-stu-id="f937c-151">EAN-8</span></span> | <span data-ttu-id="f937c-152">Да</span><span class="sxs-lookup"><span data-stu-id="f937c-152">Yes</span></span> | <span data-ttu-id="f937c-153">Да</span><span class="sxs-lookup"><span data-stu-id="f937c-153">Yes</span></span> |
| <span data-ttu-id="f937c-154">ITF</span><span class="sxs-lookup"><span data-stu-id="f937c-154">ITF</span></span> | <span data-ttu-id="f937c-155">Нет</span><span class="sxs-lookup"><span data-stu-id="f937c-155">No</span></span> | <span data-ttu-id="f937c-156">Да</span><span class="sxs-lookup"><span data-stu-id="f937c-156">Yes</span></span> |
| <span data-ttu-id="f937c-157">Код QR</span><span class="sxs-lookup"><span data-stu-id="f937c-157">QR Code</span></span> | <span data-ttu-id="f937c-158">Да</span><span class="sxs-lookup"><span data-stu-id="f937c-158">Yes</span></span> | <span data-ttu-id="f937c-159">Да</span><span class="sxs-lookup"><span data-stu-id="f937c-159">Yes</span></span> |
| <span data-ttu-id="f937c-160">Расширение RSS</span><span class="sxs-lookup"><span data-stu-id="f937c-160">RSS Expanded</span></span> | <span data-ttu-id="f937c-161">Да</span><span class="sxs-lookup"><span data-stu-id="f937c-161">Yes</span></span> | <span data-ttu-id="f937c-162">Нет</span><span class="sxs-lookup"><span data-stu-id="f937c-162">No</span></span> |
| <span data-ttu-id="f937c-163">RSS-14</span><span class="sxs-lookup"><span data-stu-id="f937c-163">RSS-14</span></span> | <span data-ttu-id="f937c-164">Да</span><span class="sxs-lookup"><span data-stu-id="f937c-164">Yes</span></span> | <span data-ttu-id="f937c-165">Нет</span><span class="sxs-lookup"><span data-stu-id="f937c-165">No</span></span> |
| <span data-ttu-id="f937c-166">UPC-A</span><span class="sxs-lookup"><span data-stu-id="f937c-166">UPC-A</span></span> | <span data-ttu-id="f937c-167">Да</span><span class="sxs-lookup"><span data-stu-id="f937c-167">Yes</span></span> | <span data-ttu-id="f937c-168">Да</span><span class="sxs-lookup"><span data-stu-id="f937c-168">Yes</span></span> |
| <span data-ttu-id="f937c-169">UPC-E</span><span class="sxs-lookup"><span data-stu-id="f937c-169">UPC-E</span></span> | <span data-ttu-id="f937c-170">Да</span><span class="sxs-lookup"><span data-stu-id="f937c-170">Yes</span></span> | <span data-ttu-id="f937c-171">Да</span><span class="sxs-lookup"><span data-stu-id="f937c-171">Yes</span></span> |

<span data-ttu-id="f937c-172">**Опыт работы с веб-приложением для `ScanBarCode` API для возможностей веб-приложения** для QR или сканера штрихкодов для 
 ![ функции сканера qr или штрихкодов](../../assets/images/tabs/qr-barcode-scanner-capability.png)</span><span class="sxs-lookup"><span data-stu-id="f937c-172">**Web app experience for `ScanBarCode` API for QR or barcode scanner capability**
![web app experience for qr or barcode scanner capability](../../assets/images/tabs/qr-barcode-scanner-capability.png)</span></span>

## <a name="error-handling"></a><span data-ttu-id="f937c-173">Обработка ошибок</span><span class="sxs-lookup"><span data-stu-id="f937c-173">Error handling</span></span>

<span data-ttu-id="f937c-174">Необходимо обеспечить надлежащее обработку этих ошибок в приложении Teams.</span><span class="sxs-lookup"><span data-stu-id="f937c-174">You must ensure to handle these errors appropriately in your Teams app.</span></span> <span data-ttu-id="f937c-175">В следующей таблице перечислены коды ошибок и условия, при которых создаются ошибки:</span><span class="sxs-lookup"><span data-stu-id="f937c-175">The following table lists the error codes and the conditions under which the errors are generated:</span></span> 

|<span data-ttu-id="f937c-176">Код ошибки</span><span class="sxs-lookup"><span data-stu-id="f937c-176">Error code</span></span> |  <span data-ttu-id="f937c-177">Имя ошибки</span><span class="sxs-lookup"><span data-stu-id="f937c-177">Error name</span></span>     | <span data-ttu-id="f937c-178">Condition</span><span class="sxs-lookup"><span data-stu-id="f937c-178">Condition</span></span>|
| --------- | --------------- | -------- |
| <span data-ttu-id="f937c-179">**100**</span><span class="sxs-lookup"><span data-stu-id="f937c-179">**100**</span></span> | <span data-ttu-id="f937c-180">NOT_SUPPORTED_ON_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="f937c-180">NOT_SUPPORTED_ON_PLATFORM</span></span> | <span data-ttu-id="f937c-181">API не поддерживается на текущей платформе.</span><span class="sxs-lookup"><span data-stu-id="f937c-181">API is not supported on the current platform.</span></span>|
| <span data-ttu-id="f937c-182">**500**</span><span class="sxs-lookup"><span data-stu-id="f937c-182">**500**</span></span> | <span data-ttu-id="f937c-183">INTERNAL_ERROR</span><span class="sxs-lookup"><span data-stu-id="f937c-183">INTERNAL_ERROR</span></span> | <span data-ttu-id="f937c-184">При выполнении необходимой операции встречаются внутренние ошибки.</span><span class="sxs-lookup"><span data-stu-id="f937c-184">Internal error is encountered while performing the required operation.</span></span>|
| <span data-ttu-id="f937c-185">**1000**</span><span class="sxs-lookup"><span data-stu-id="f937c-185">**1000**</span></span> | <span data-ttu-id="f937c-186">PERMISSION_DENIED</span><span class="sxs-lookup"><span data-stu-id="f937c-186">PERMISSION_DENIED</span></span> |<span data-ttu-id="f937c-187">Пользователю отказано в разрешении.</span><span class="sxs-lookup"><span data-stu-id="f937c-187">Permission is denied by the user.</span></span>|
| <span data-ttu-id="f937c-188">**3000**</span><span class="sxs-lookup"><span data-stu-id="f937c-188">**3000**</span></span> | <span data-ttu-id="f937c-189">NO_HW_SUPPORT</span><span class="sxs-lookup"><span data-stu-id="f937c-189">NO_HW_SUPPORT</span></span> | <span data-ttu-id="f937c-190">Оборудование не поддерживает эту возможность.</span><span class="sxs-lookup"><span data-stu-id="f937c-190">Underlying hardware does not support the capability.</span></span>|
| <span data-ttu-id="f937c-191">**4000**</span><span class="sxs-lookup"><span data-stu-id="f937c-191">**4000**</span></span> | <span data-ttu-id="f937c-192">INVALID_ARGUMENTS</span><span class="sxs-lookup"><span data-stu-id="f937c-192">INVALID_ARGUMENTS</span></span> | <span data-ttu-id="f937c-193">Один или несколько аргументов являются недействительными.</span><span class="sxs-lookup"><span data-stu-id="f937c-193">One or more arguments are invalid.</span></span>|
| <span data-ttu-id="f937c-194">**8000**</span><span class="sxs-lookup"><span data-stu-id="f937c-194">**8000**</span></span> | <span data-ttu-id="f937c-195">USER_ABORT</span><span class="sxs-lookup"><span data-stu-id="f937c-195">USER_ABORT</span></span> |<span data-ttu-id="f937c-196">Пользователь прерывает операцию.</span><span class="sxs-lookup"><span data-stu-id="f937c-196">User aborts the operation.</span></span>|
| <span data-ttu-id="f937c-197">**8001**</span><span class="sxs-lookup"><span data-stu-id="f937c-197">**8001**</span></span> | <span data-ttu-id="f937c-198">OPERATION_TIMED_OUT</span><span class="sxs-lookup"><span data-stu-id="f937c-198">OPERATION_TIMED_OUT</span></span> | <span data-ttu-id="f937c-199">Не удалось обнаружить штрих-код в заданный интервал времени.</span><span class="sxs-lookup"><span data-stu-id="f937c-199">Could not detect the barcode in the given time interval.</span></span>|
| <span data-ttu-id="f937c-200">**9000**</span><span class="sxs-lookup"><span data-stu-id="f937c-200">**9000**</span></span> | <span data-ttu-id="f937c-201">OLD_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="f937c-201">OLD_PLATFORM</span></span> | <span data-ttu-id="f937c-202">Код платформы устарел и не реализует этот API.</span><span class="sxs-lookup"><span data-stu-id="f937c-202">Platform code is outdated and does not implement this API.</span></span>|

## <a name="code-snippet"></a><span data-ttu-id="f937c-203">Фрагмент кода</span><span class="sxs-lookup"><span data-stu-id="f937c-203">Code snippet</span></span>

<span data-ttu-id="f937c-204">**Вызов `ScanBarCode()` API** для сканирования QR или штрихкода с помощью камеры:</span><span class="sxs-lookup"><span data-stu-id="f937c-204">**Calling `ScanBarCode()` API** for scanning QR or barcode using camera:</span></span>

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

## <a name="see-also"></a><span data-ttu-id="f937c-205">См. также</span><span class="sxs-lookup"><span data-stu-id="f937c-205">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f937c-206">Интеграция возможностей мультимедиа в Teams</span><span class="sxs-lookup"><span data-stu-id="f937c-206">Integrate media capabilities in Teams</span></span>](mobile-camera-image-permissions.md)
