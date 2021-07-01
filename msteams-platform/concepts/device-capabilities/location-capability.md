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
# <a name="integrate-location-capabilities"></a>Интеграция функций местонахождения 

Вы можете интегрировать возможности расположения родного устройства с Teams приложением.  

Вы можете [использовать Microsoft Teams JavaScript клиента SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), который предоставляет средства, необходимые для вашего приложения, чтобы получить доступ к возможностям родного [устройства пользователя](native-device-permissions.md). Используйте API расположения, такие как [getLocation](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) и [showLocation,](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#showLocation_Location___error__SdkError__status__boolean_____void_&preserve-view=true) чтобы интегрировать возможности в приложении. 

## <a name="advantages-of-integrating-location-capabilities"></a>Преимущества интеграции возможностей расположения

Основное преимущество интеграции возможностей расположения в Teams приложений заключается в том, что он позволяет разработчикам веб-приложений на Teams платформе использовать функции расположения с помощью SDK Microsoft Teams JavaScript. 

В следующих примерах покажите, как интеграция возможностей расположения используется в различных сценариях:
* На фабрике руководитель может отслеживать посещаемость рабочих, попросив их сделать селфи в непосредственной близости от фабрики и поделиться им через указанное приложение. Данные о расположении также захватываются и отправляются вместе с изображением.
* Возможности расположения позволяют обслуживаемом персоналу поставщика услуг обмениваться с руководством подлинными данными о состоянии здоровья вышек сотовой связи. Руководство может сравнить любое несоответствие между захваченными сведениями о расположении и данными, представленными сотрудниками службы технического обслуживания.

Чтобы интегрировать возможности расположения, необходимо обновить файл манифеста приложения и вызвать API. Для эффективной интеграции необходимо хорошо [](#code-snippets) понимать фрагменты кода для вызова API расположения. Важно ознакомиться с ошибками [ответа API](#error-handling) для обработки ошибок в Teams приложении.

> [!NOTE] 
> В настоящее Microsoft Teams поддержка возможностей расположения доступна только для мобильных клиентов.

## <a name="update-manifest"></a>Манифест обновления

Обновите Teams приложение [manifest.jsфайле,](../../resources/schema/manifest-schema.md#devicepermissions) добавив `devicePermissions` свойство и указав `geolocation` . Это позволяет приложению запросить необходимые разрешения у пользователей, прежде чем они начнут использовать возможности расположения. Обновление манифеста приложения:

``` json
"devicePermissions": [
    "geolocation",
],
```

> [!NOTE]
> Запрос **разрешения запроса** автоматически отображается при Teams API. Дополнительные сведения см. в [запросе разрешений устройств.](native-device-permissions.md)

## <a name="location-apis"></a>API расположения

Чтобы включить возможности расположения устройства, необходимо использовать следующий набор API:

| API      | Описание   |
| --- | --- |
|[getLocation](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) | Предоставляет текущее расположение устройства или открывает выбор родного расположения и возвращает выбранное пользователем расположение. |
|[showLocation](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#showLocation_Location___error__SdkError__status__boolean_____void_&preserve-view=true) | Отображает расположение на карте. |

> [!NOTE]
> API `getLocation()` поставляется вместе со [следующими конфигурациями ввода](/javascript/api/@microsoft/teams-js/locationprops?view=msteams-client-js-latest&preserve-view=true)и `allowChooseLocation` `showMap` . <br/> Если значение верно, пользователи могут выбрать `allowChooseLocation` любое расположение по своему выбору. <br/>  Если значение *ложное,* пользователи не могут изменить текущее расположение.<br/> Если значение `showMap` false, текущее расположение извлекается без отображения карты. `showMap`игнорируется, `allowChooseLocation` если установлено, что это *верно.*

На следующем изображении повеяна возможность расположения веб-приложения:

![Опыт работы веб-приложения для возможностей расположения](../../assets/images/tabs/location-capability.png)

### <a name="code-snippets"></a>Фрагменты кода

**Вызов `getLocation` API для получения расположения:**

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

**Вызов `showLocation` API для отображения расположения:**

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

Необходимо обеспечить надлежащее обработку этих ошибок в Teams приложении. В следующей таблице перечислены коды ошибок и условия, при которых создаются ошибки: 

|Код ошибки |  Имя ошибки     | Condition|
| --------- | --------------- | -------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | API не поддерживается на текущей платформе.|
| **500** | INTERNAL_ERROR | При выполнении необходимой операции встречаются внутренние ошибки.|
| **1000** | PERMISSION_DENIED |Пользователю отказано в разрешении на Teams или веб-приложение.|
| **4000** | INVALID_ARGUMENTS | API вызывается с неправильными или недостаточными обязательными аргументами.|
| **8000** | USER_ABORT |Пользователь отменил операцию.|
| **9000** | OLD_PLATFORM | Пользователь находится на старой сборке платформы, где нет реализации API. Обновление сборки должно решить проблему.|

## <a name="see-also"></a>См. также

* [Интеграция возможностей мультимедиа в Teams](mobile-camera-image-permissions.md)
* [Интеграция QR-кода или возможности сканера штрихкодов в Teams](qr-barcode-scanner-capability.md)
* [Интеграция возможностей выборщика людей в Teams](people-picker-capability.md)
