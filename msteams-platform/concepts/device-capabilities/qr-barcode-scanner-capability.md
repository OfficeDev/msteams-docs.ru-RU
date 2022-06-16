---
title: Интеграция функции сканирования QR- или штрихкода
author: Rajeshwari-v
description: Использование клиентского пакета SDK Teams для JavaScript для использования возможностей сканера QR или штрихкода
keywords: камера мультимедиа QR-код qrcode штрих-код штрихкод сканер сканировать возможности встроенные устройство разрешения
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: 2dced2abc29ee21e50a3a37ccfed4811102cc8ce
ms.sourcegitcommit: b4986bf529c74444db67b7ce522b3b0d2c2a8e28
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/16/2022
ms.locfileid: "66130503"
---
# <a name="integrate-qr-or-barcode-scanner-capability"></a>Интеграция функции сканирования QR- или штрихкода

Штрихкод — это метод представления данных в визуальной и машиночитаемой форме. Штрихкод содержит сведения о продукте, такую как тип, размер, производитель и страна происхождения в виде штрихов и пробелов. Код считывается с помощью оптического сканера на встроенной камере устройства. Для расширения возможностей совместной работы можно интегрировать возможности сканера QR или штрихкода, предоставляемые на платформе Teams, с вашим приложением Teams.

Вы можете использовать [клиентский пакет SDK JavaScript для Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), который предоставляет средства, необходимые приложению для доступа к [собственным функциям местонахождения устройства](native-device-permissions.md) пользователя. Используйте API [scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) для интеграции возможностей сканера в приложение.

## <a name="advantage-of-integrating-qr-or-barcode-scanner-capability"></a>Преимущества интеграции сканера QR или штрихкода

Ниже приведены преимущества интеграции возможностей сканера QR или штрихкода:

* Интеграция позволяет разработчикам веб-приложений на платформе Teams использовать функции сканирования QR или штрихкода с помощью пакета SDK клиента Teams для JavaScript.
* С помощью этой функции пользователю нужно только выровнять QR или штрихкод внутри рамки в центре пользовательского интерфейса сканера, и код сканируется автоматически. Сохраненные данные передаются вызывающему веб-приложению. Это позволяет избежать неудобств и человеческих ошибок при вводе длинных кодов продуктов или других важных сведений вручную.

Чтобы интегрировать возможности сканера QR или штрихкода, необходимо обновить файл манифеста приложения и вызвать API-интерфейс [scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_). Для эффективной интеграции необходимо хорошо понимать [фрагмент кода](#code-snippet) для вызова API [scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_), который позволяет вам использовать собственные возможности сканера QR или штрихкода. API выдает ошибку для неподдерживаемого стандарта штрихкода.
Важно ознакомиться с [ошибками ответа API](#error-handling) для управления ошибками в приложении Teams.

> [!NOTE]
> В настоящее время поддержка Microsoft Teams для сканера QR или штрихкода доступна только для мобильных клиентов.

## <a name="update-manifest"></a>Изменение манифеста

Обновите файл [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) своего приложения Teams, добавив свойство `devicePermissions` и указав `media`. Это позволяет приложению запрашивать необходимые разрешения у пользователей, прежде чем они начнут использовать возможности сканера QR или штрихкода. Измените манифест приложения, выполнив следующие шаги.

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> Приглашение **Запрос разрешений** автоматически отображается при запуске соответствующего API Teams. Дополнительные сведения см. в статье [Запрос разрешений устройства](native-device-permissions.md).

## <a name="scanbarcode-api"></a>ScanBarCode API

API [scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) вызывает элемент управления сканером, который позволяет пользователю сканировать различные типы штрихкодов и возвращает результат в виде строки.

Чтобы настроить процесс сканирования штрихкода, необязательная [конфигурация штрихкода](/javascript/api/@microsoft/teams-js/microsoftteams.media.barcodeconfig?view=msteams-client-js-latest&preserve-view=true) передается в качестве входных данных в API-интерфейс [scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_). Вы можете указать интервал времени ожидания сканирования в секундах с помощью `timeOutIntervalInSec`. Его значение по умолчанию — 30 секунд, а максимальное значение — 60 секунд.

API **scanBarCode()** поддерживает следующие типы штрихкодов:

| Тип штрихкода | Поддерживается в Android | Поддерживается в iOS |
| ---------- | ---------- | ------------ |
| Кодовая панель | Да | Нет |
| Код 39 | Да | Да |
| Код 93 | Да | Да |
| Код 128 | Да | Да |
| EAN-13 | Да | Да |
| EAN-8 | Да | Да |
| Комиссия за международную транзакцию | Нет | Да |
| QR-код | Да | Да |
| Развернутый RSS | Да | Нет |
| RSS-14 | Да | Нет |
| UPC-A | Да | Да |
| UPC-E | Да | Да |

На следующем изображении показано взаимодействие веб-приложения со сканером QR или штрихкода:

![взаимодействие веб-приложения со сканером QR или штрих-кода](../../assets/images/tabs/qr-barcode-scanner-capability.png)

## <a name="error-handling"></a>Обработка ошибок

Обеспечьте правильную обработку этих ошибок в приложении Teams. В следующей таблице перечислены коды ошибок и условия, при которых возникают ошибки:

|Код ошибки |  Название ошибки     | Условие|
| --------- | --------------- | -------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | API не поддерживается на текущей платформе.|
| **500** | INTERNAL_ERROR | При выполнении требуемой операции обнаружена внутренняя ошибка.|
| **1000** | PERMISSION_DENIED |Разрешение отклонено пользователем.|
| **3000** | NO_HW_SUPPORT | Базовое оборудование не поддерживает эту возможность.|
| **4000** | INVALID_ARGUMENTS | Один или несколько недопустимых аргументов.|
| **8000** | USER_ABORT |Пользователь прерывает операцию.|
| **8001** | OPERATION_TIMED_OUT | Не удалось обнаружить штрихкод в заданный интервал времени.|
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

* [Интеграция возможностей мультимедиа](media-capabilities.md)
* [Интеграция функций местонахождения](location-capability.md)
* [Интеграция средства выбора людей в Teams](people-picker-capability.md)
