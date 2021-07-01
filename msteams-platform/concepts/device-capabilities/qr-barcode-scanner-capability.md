---
title: Интеграция функции сканирования QR- или штрихкода
author: Rajeshwari-v
description: Использование SDK Teams JavaScript для использования возможностей сканера QR или штрихкодов
keywords: QR-код qr code qrcode barcode сканера штрихкода камеры позволяет родных разрешений устройства
localization_priority: Normal
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: 4e34e75a6b439c67c831352e07344fd2cf011543
ms.sourcegitcommit: 059d22c436ee9b07a61561ff71e03e1c23ff40b8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/30/2021
ms.locfileid: "53211578"
---
# <a name="integrate-qr-or-barcode-scanner-capability"></a>Интеграция функции сканирования QR- или штрихкода 

Штрихкод — это метод представления данных в визуальной и машинной форме. Штрихкод содержит сведения о продукте, например типе, размере, изготовителе и стране происхождения в виде баров и пробелов. Код читается с помощью оптического сканера на вашей родной камере устройства. Для более насыщенного взаимодействия можно интегрировать функцию сканера QR или штрих-кода, предоставляемую на платформе Teams с Teams приложением.   

Вы можете [использовать Microsoft Teams JavaScript клиента SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), который предоставляет средства, необходимые для вашего приложения, чтобы получить доступ к возможностям родного [устройства пользователя](native-device-permissions.md). Используйте [API scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) для интеграции возможностей сканера в приложении. 

## <a name="advantage-of-integrating-qr-or-barcode-scanner-capability"></a>Преимущество интеграции функции сканера QR или штрихкода

Ниже следующую возможность интеграции возможностей сканера QR или штрихкодов: 

* Интеграция позволяет разработчикам веб-приложений на Teams использовать функции сканирования QR или штрихкодов Teams клиентской SDK JavaScript.
* С помощью этой функции пользователю необходимо выровнять QR или штрих-код в кадре в центре пользовательского интерфейса сканера, и код автоматически сканируется. Хранимые данные делятся с веб-приложением вызова. Это позволяет избежать неудобств и человеческих ошибок при вводе длинных кодов продуктов или других соответствующих сведений вручную.

Чтобы интегрировать возможности сканера QR или штрихкода, необходимо обновить файл манифеста приложения и вызвать [API scanBarCode.](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) Для эффективной интеграции необходимо хорошо [](#code-snippet) понимать фрагмент кода для вызова API [scanBarCode,](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) который позволяет использовать родной QR или сканер штрихкодов. API предоставляет ошибку для неподдержаемой стандарта штрихкода.
Важно ознакомиться с ошибками [ответа API](#error-handling) для обработки ошибок в Teams приложении.

> [!NOTE] 
> В настоящее Microsoft Teams поддержка возможностей сканера QR или штрихкодов доступна только для мобильных клиентов.

## <a name="update-manifest"></a>Манифест обновления

Обновите Teams приложение [manifest.jsфайле,](../../resources/schema/manifest-schema.md#devicepermissions) добавив `devicePermissions` свойство и указав `media` . Это позволяет приложению запросить необходимые разрешения у пользователей, прежде чем они начнут использовать функцию сканера QR или штрихкода. Обновление манифеста приложения:

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> Запрос **разрешения запроса** автоматически отображается при Teams API. Дополнительные сведения см. в [запросе разрешений устройств.](native-device-permissions.md)

## <a name="scanbarcode-api"></a>ScanBarCode API

API [scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) вызывает управление сканером, которое позволяет пользователю сканировать различные типы штрихкода и возвращает результат в качестве строки.

Чтобы настроить функцию сканирования штрихкодов, необязательная конфигурация штрихкода передается в качестве ввода в [API scanBarCode.](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) [](/javascript/api/@microsoft/teams-js/microsoftteams.media.barcodeconfig?view=msteams-client-js-latest&preserve-view=true) Вы можете указать интервал времени сканирования в секундах с помощью `timeOutIntervalInSec` . Его значение по умолчанию — 30 секунд, а максимальное — 60 секунд.

API **scanBarCode()** поддерживает следующие типы штрихкодов:

| Тип штрихкода | Поддерживается на Android | Поддерживается на iOS |
| ---------- | ---------- | ------------ |
| Codebar | Да | Нет |
| Код 39 | Да | Да | 
| Код 93 | Да | Да |
| Код 128 | Да | Да |
| EAN-13 | Да | Да |
| EAN-8 | Да | Да |
| ITF | Нет | Да |
| Код QR | Да | Да |
| Расширение RSS | Да | Нет |
| RSS-14 | Да | Нет |
| UPC-A | Да | Да |
| UPC-E | Да | Да |

На следующем изображении показана возможность веб-приложения для QR или сканера штрихкодов:

![возможности сканера qr или штрихкодов для веб-приложений](../../assets/images/tabs/qr-barcode-scanner-capability.png)

## <a name="error-handling"></a>Обработка ошибок

Необходимо обеспечить надлежащее обработку этих ошибок в Teams приложении. В следующей таблице перечислены коды ошибок и условия, при которых создаются ошибки: 

|Код ошибки |  Имя ошибки     | Condition|
| --------- | --------------- | -------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | API не поддерживается на текущей платформе.|
| **500** | INTERNAL_ERROR | При выполнении необходимой операции встречаются внутренние ошибки.|
| **1000** | PERMISSION_DENIED |Пользователю отказано в разрешении.|
| **3000** | NO_HW_SUPPORT | Оборудование не поддерживает эту возможность.|
| **4000** | INVALID_ARGUMENTS | Один или несколько аргументов являются недействительными.|
| **8000** | USER_ABORT |Пользователь прерывает операцию.|
| **8001** | OPERATION_TIMED_OUT | Не удалось обнаружить штрих-код в заданный интервал времени.|
| **9000** | OLD_PLATFORM | Код платформы устарел и не реализует этот API.|

## <a name="code-snippet"></a>Фрагмент кода

**Вызов `ScanBarCode()` API** для сканирования QR или штрихкода с помощью камеры:

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

## <a name="see-also"></a>См. также

* [Интеграция возможностей мультимедиа в Teams](mobile-camera-image-permissions.md)
* [Интеграция возможностей расположения в Teams](location-capability.md)
* [Интеграция возможностей выборщика людей в Teams](people-picker-capability.md)

