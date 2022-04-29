---
title: Интеграция функций местонахождения
author: Rajeshwari-v
description: Узнайте, как применять клиентский пакет SDK JavaScript для Teams, чтобы использовать функции местонахождения с помощью фрагментов кода и примеров
keywords: собственные разрешения устройства для функций местонахождения на карте
ms.topic: conceptual
ms.localizationpriority: high
ms.author: surbhigupta
ms.openlocfilehash: 369e9307a8007d45cc42ae4059b16cdcf9a3cc4c
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111187"
---
# <a name="integrate-location-capabilities"></a>Интеграция функций местонахождения

Вы можете интегрировать функции местонахождения собственного устройства с приложением Teams.  

Вы можете использовать [клиентский пакет SDK JavaScript для Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), который предоставляет средства, необходимые приложению для доступа к [собственным функциям местонахождения устройства](native-device-permissions.md) пользователя. Используйте API-интерфейсы местонахождения, например [getLocation](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) и [showLocation](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#showLocation_Location___error__SdkError__status__boolean_____void_&preserve-view=true), для интеграции функций в ваше приложение.

## <a name="advantages-of-integrating-location-capabilities"></a>Преимущества интеграции функций местонахождения

Основное преимущество интеграции функций местонахождения в приложениях Teams заключается в том, что это позволяет разработчикам веб-приложений на платформе Teams использовать функции местонахождения с клиентским пакетом SDK JavaScript для Microsoft Teams.

В следующих примерах показано, как интеграция функций местонахождения используется в разных сценариях.

* На фабрике руководитель может отслеживать присутствие рабочих, предлагая им сделать селфи вблизи фабрики и поделиться им через указанное приложение. Данные о местонахождении фиксируются и отправляются вместе с изображением.
* Функции местонахождения позволяют обслуживающему персоналу поставщика услуг делиться с руководством данными о состоянии вышек сотовой связи. Руководство может сравнить любые несоответствия между собранными сведениями о местонахождении и данными, отправленными обслуживающим персоналом.

Чтобы интегрировать функции местонахождения, обновите файл манифеста приложения и вызовите API. Для эффективной интеграции вы должны хорошо понимать [фрагменты кода](#code-snippets) для вызова API-интерфейсов местонахождения.
Важно ознакомиться с [ошибками отклика API](#error-handling) для обработки ошибок в вашем приложении Teams.

> [!NOTE]
> В настоящее время Microsoft Teams поддерживает функции местонахождения только для мобильных клиентов.

## <a name="update-manifest"></a>Изменение манифеста

Обновите файл [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) своего приложения Teams, добавив свойство `devicePermissions` и указав `geolocation`. Это позволяет приложению запрашивать необходимые разрешения у пользователей, прежде чем они начнут использовать функции местонахождения. Измените манифест приложения, выполнив следующие шаги.

``` json
"devicePermissions": [
    "geolocation",
],
```

> [!NOTE]
> * Приглашение **Запрос разрешений** автоматически отображается при запуске соответствующего API Teams. Дополнительные сведения см. в статье [Запрос разрешений устройства](native-device-permissions.md).
> * Разрешения устройств в браузере отличаются. Дополнительные сведения см. в статье [Разрешения устройств в браузере](browser-device-permissions.md).

## <a name="location-apis"></a>API-интерфейсы местонахождения

Чтобы включить функции местонахождения, используйте следующий набор API.

| API      | Описание   |
| --- | --- |
|[getLocation](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) | Предоставляет текущее местонахождение устройства пользователя или открывает собственное средство выбора местонахождения и возвращает местонахождение, выбранное пользователем. |
|[showLocation](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#showLocation_Location___error__SdkError__status__boolean_____void_&preserve-view=true) | Отображает местонахождение на карте. |

> [!NOTE]
> API `getLocation()` поставляется со следующими [конфигурациями ввода](/javascript/api/@microsoft/teams-js/locationprops?view=msteams-client-js-latest&preserve-view=true): `allowChooseLocation` и `showMap`. <br/> Если значением `allowChooseLocation` является *true*, пользователи могут выбрать любое местонахождение.<br/>  Если значение равно *false*, пользователи не могут изменить свое текущее местонахождение.<br/> Если значением `showMap` является *false*, текущее местонахождение извлекается без отображения карты. `showMap` игнорируется, если для `allowChooseLocation` установлено значение *true*.

На следующем изображении показан интерфейс веб-приложения с функциями местонахождения.

![интерфейс веб-приложения для функций местонахождения](../../assets/images/tabs/location-capability.png)

### <a name="code-snippets"></a>Фрагменты кода

**Вызов API `getLocation` для получения местонахождения:**

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

**Вызов API `showLocation` для отображения местонахождения:**

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

## <a name="error-handling"></a>Обработка ошибок

Обеспечьте правильную обработку этих ошибок в своем приложении Teams. В следующей таблице перечислены коды ошибок и условия, при которых возникают ошибки.

|Код ошибки |  Название ошибки     | Условие|
| --------- | --------------- | -------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | API не поддерживается на текущей платформе.|
| **500** | INTERNAL_ERROR | При выполнении необходимой операции возникла внутренняя ошибка.|
| **1000** | PERMISSION_DENIED |Пользователь отклонил разрешения на доступ к сведениям о местонахождении для приложения Teams или веб-приложения.|
| **4000** | INVALID_ARGUMENTS | API вызывается с неправильными или недостаточными обязательными аргументами.|
| **8000** | USER_ABORT |Пользователь отменил операцию.|
| **9000** | OLD_PLATFORM | Пользователь использует старую сборку платформы, где отсутствует реализация API. Обновление сборки должно устранить проблему.|

### <a name="code-sample"></a>Пример кода

|Название примера | Описание | C# | Node.js |
|----------------|-----------------|--------------|--------------|
| Проверка текущего местонахождения приложением | Пользователи могут проверить текущее местонахождение и просмотреть все предыдущие проверки местонахождения.| [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-checkin-location/csharp) | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-checkin-location/nodejs) |

## <a name="see-also"></a>Дополнительные ресурсы

* [Интеграция возможностей мультимедиа в Teams](mobile-camera-image-permissions.md)
* [Интеграция функции сканирования QR- или штрихкода в Teams](qr-barcode-scanner-capability.md)
* [Интеграция средства выбора людей в Teams](people-picker-capability.md)
