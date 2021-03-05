---
title: Интеграция возможностей расположения
description: Использование SDK клиента Teams JavaScript для использования возможностей расположения
keywords: Возможности карты расположения для родных разрешений устройств
ms.author: lajanuar
ms.openlocfilehash: fccf39c37c785be716bfff26907f9184c0d9beec
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449641"
---
# <a name="integrate-location-capabilities"></a>Интеграция возможностей расположения 

В этом документе вы можете узнать, как интегрировать возможности расположения родного устройства с приложением Teams.  

Вы можете использовать [клиентскую SDK Microsoft Teams JavaScript,](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)которая предоставляет средства, необходимые вашему приложению для доступа к возможностям родного [устройства пользователя.](native-device-permissions.md) Используйте API расположения, такие как [getLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_) и [showLocation,](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#showLocation_Location___error__SdkError__status__boolean_____void_) чтобы интегрировать возможности в приложении. 

## <a name="advantages-of-integrating-location-capabilities"></a>Преимущества интеграции возможностей расположения

Основное преимущество интеграции возможностей расположения в приложениях Teams заключается в том, что он позволяет разработчикам веб-приложений на платформе Teams использовать функции расположения с клиентом Microsoft Teams JavaScript SDK. 

В следующих примерах покажите, как интеграция возможностей расположения используется в различных сценариях:
* На фабрике руководитель может отслеживать посещаемость рабочих, попросив их сделать селфи в непосредственной близости от фабрики и поделиться им через указанное приложение. Данные о расположении также захватываются и отправляются вместе с изображением.
* Возможности расположения позволяют обслуживаемом персоналу поставщика услуг обмениваться с руководством подлинными данными о состоянии здоровья вышек сотовой связи. Руководство может сравнить любое несоответствие между захваченными сведениями о расположении и данными, представленными сотрудниками службы технического обслуживания.

Чтобы интегрировать возможности расположения, необходимо обновить файл манифеста приложения и вызвать API. Для эффективной интеграции необходимо хорошо [](#code-snippets) понимать фрагменты кода для вызова API расположения. Важно ознакомиться с ошибками [ответа API](#error-handling) для обработки ошибок в приложении Teams.

> [!NOTE] 
> В настоящее время поддержка microsoft Teams возможностей расположения доступна только для мобильных клиентов.

## <a name="update-manifest"></a>Манифест обновления

Обновите приложение Teams [manifest.jsфайле,](../../resources/schema/manifest-schema.md#devicepermissions) добавив `devicePermissions` свойство и указав `geolocation` . Это позволяет приложению запросить необходимые разрешения у пользователей, прежде чем они начнут использовать возможности расположения.

``` json
"devicePermissions": [
    "geolocation",
],
```

> [!NOTE]
> Запрос **разрешений** автоматически отображается при инициировании соответствующего API Teams. Дополнительные сведения см. в [запросе разрешений устройств.](native-device-permissions.md)

## <a name="location-apis"></a>API расположения

Чтобы включить возможности расположения устройства, необходимо использовать следующий набор API:

| API      | Описание   |
| --- | --- |
|[getLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_) | Предоставляет текущее расположение устройства или открывает выбор родного расположения и возвращает выбранное пользователем расположение. |
|[showLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#showLocation) | Отображает расположение на карте |

> [!NOTE]

> API `getLocation()` поставляется вместе со [следующими конфигурациями ввода](https://docs.microsoft.com/en-us/javascript/api/@microsoft/teams-js/locationprops?view=msteams-client-js-latest)и `allowChooseLocation` `showMap` . <br/> Если значение верно, пользователи могут выбрать `allowChooseLocation` любое расположение по своему выбору. <br/>  Если значение *ложное,* пользователи не могут изменить текущее расположение.<br/> Если значение `showMap` false, текущее расположение извлекается без отображения карты. `showMap`игнорируется, `allowChooseLocation` если установлено, что это *верно.* 

**Опыт работы с веб-приложениями для возможностей расположения** 
 ![ Опыт работы веб-приложения для возможностей расположения](../../assets/images/tabs/location-capability.png)

## <a name="error-handling"></a>Обработка ошибок

Необходимо обеспечить надлежащее обработку этих ошибок в приложении Teams. В следующей таблице перечислены коды ошибок и условия, при которых создаются ошибки: 

|Код ошибки |  Имя ошибки     | Condition|
| --------- | --------------- | -------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | API не поддерживается на текущей платформе.|
| **500** | INTERNAL_ERROR | При выполнении необходимой операции встречаются внутренние ошибки.|
| **1000** | PERMISSION_DENIED |Пользователю отказано в разрешении на расположение в Командное приложение или веб-приложение.|
| **4000** | INVALID_ARGUMENTS | API вызывается с неправильными или недостаточными обязательными аргументами.|
| **8000** | USER_ABORT |Пользователь отменил операцию.|
| **9000** | OLD_PLATFORM | Пользователь находится на старой сборке платформы, где нет реализации API. Обновление сборки должно решить проблему.|

## <a name="code-snippets"></a>Фрагменты кода

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

## <a name="see-also"></a>См. также

> [!div class="nextstepaction"]
> [Интеграция возможностей мультимедиа в Teams](mobile-camera-image-permissions.md)

> [!div class="nextstepaction"]
> [Интеграция функций сканера QR или штрихкодов в Teams](qr-barcode-scanner-capability.md)