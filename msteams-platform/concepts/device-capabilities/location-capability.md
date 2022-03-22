---
title: Интеграция функций местонахождения
author: Rajeshwari-v
description: Узнайте, как использовать SDK Teams JavaScript для использования возможностей расположения с помощью фрагментов кода и примеров
keywords: Возможности карты расположения для родных разрешений устройств
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: surbhigupta
ms.openlocfilehash: a375d8f7c2692c9da8e220474c2c0ece97b623c2
ms.sourcegitcommit: a36760750ff4f510c374a4c956be57f7c1b4a0db
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/20/2022
ms.locfileid: "63675015"
---
# <a name="integrate-location-capabilities"></a>Интеграция функций местонахождения

Вы можете интегрировать возможности расположения родного устройства с вашим Teams приложением.  

Вы можете [Microsoft Teams клиентской SDK JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), которая предоставляет средства, необходимые вашему приложению для доступа к возможностям родного [устройства пользователя](native-device-permissions.md). Используйте API расположения, такие как [getLocation](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) и [showLocation](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#showLocation_Location___error__SdkError__status__boolean_____void_&preserve-view=true) , чтобы интегрировать возможности в приложении.

## <a name="advantages-of-integrating-location-capabilities"></a>Преимущества интеграции возможностей расположения

Основное преимущество интеграции возможностей расположения в Teams приложениях заключается в том, что она позволяет разработчикам веб-приложений на Teams платформе использовать функции расположения с помощью Microsoft Teams клиента JavaScript SDK.

В следующих примерах покажите, как интеграция возможностей расположения используется в различных сценариях:

* На фабрике руководитель может отслеживать посещаемость рабочих, попросив их сделать селфи в непосредственной близости от фабрики и поделиться им через указанное приложение. Данные о расположении также захватываются и отправляются вместе с изображением.
* Возможности расположения позволяют обслуживаемом персоналу поставщика услуг обмениваться с руководством подлинными данными о состоянии здоровья вышек сотовой связи. Руководство может сравнить любое несоответствие между захваченными сведениями о расположении и данными, представленными сотрудниками службы технического обслуживания.

Чтобы интегрировать возможности расположения, необходимо обновить файл манифеста приложения и вызвать API. Для эффективной интеграции необходимо хорошо понимать фрагменты кода для [](#code-snippets) вызова API расположения.
Важно ознакомиться с ошибками [ответа API](#error-handling) для обработки ошибок в Teams приложении.

> [!NOTE]
> В настоящее Microsoft Teams поддержка возможностей расположения доступна только для мобильных клиентов.

## <a name="update-manifest"></a>Изменение манифеста

Обновите [Teams-файл приложения manifest.json](../../resources/schema/manifest-schema.md#devicepermissions), `devicePermissions` добавив свойство и указав `geolocation`. Это позволяет приложению запросить необходимые разрешения у пользователей, прежде чем они начнут использовать возможности расположения. Измените манифест приложения, выполнив следующие шаги.

``` json
"devicePermissions": [
    "geolocation",
],
```

> [!NOTE]
> * Запрос **разрешений** автоматически отображается при Teams API. Дополнительные сведения см. в [запросе разрешений устройств](native-device-permissions.md).
> * Разрешения устройств отличаются в браузере. Дополнительные сведения см. в [разрешении на устройство браузера](browser-device-permissions.md).

## <a name="location-apis"></a>API расположения

Чтобы включить возможности расположения устройства, необходимо использовать следующий набор API:

| API      | Описание   |
| --- | --- |
|[getLocation](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) | Предоставляет текущее расположение устройства или открывает выбор родного расположения и возвращает выбранное пользователем расположение. |
|[showLocation](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#showLocation_Location___error__SdkError__status__boolean_____void_&preserve-view=true) | Отображает расположение на карте. |

> [!NOTE]
> API `getLocation()` поставляется вместе со следующими [конфигурациями](/javascript/api/@microsoft/teams-js/locationprops?view=msteams-client-js-latest&preserve-view=true) ввода и `allowChooseLocation` `showMap`. <br/> Если значение верно `allowChooseLocation` *, пользователи* могут выбрать любое расположение по своему выбору.<br/>  Если *значение ложное*, пользователи не могут изменить текущее расположение.<br/> Если значение false `showMap` *,* текущее расположение извлекается без отображения карты. `showMap` игнорируется, если `allowChooseLocation` установлено, что это *верно*.

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

|Код ошибки |  Имя ошибки     | Условие|
| --------- | --------------- | -------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | API не поддерживается на текущей платформе.|
| **500** | INTERNAL_ERROR | При выполнении необходимой операции встречаются внутренние ошибки.|
| **1000** | PERMISSION_DENIED |Пользователю отказано в разрешении на Teams или веб-приложении.|
| **4000** | INVALID_ARGUMENTS | API вызывается с неправильными или недостаточными обязательными аргументами.|
| **8000** | USER_ABORT |Пользователь отменил операцию.|
| **9000** | OLD_PLATFORM | Пользователь находится на старой сборке платформы, где нет реализации API. Обновление сборки должно решить проблему.|

### <a name="code-sample"></a>Пример кода

|Название примера | Описание | C# | Node.js |
|----------------|-----------------|--------------|--------------|
| Текущее расположение регистрации приложения | Пользователи могут проверить текущее расположение и просмотреть все предыдущие проверки расположения.| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-checkin-location/csharp) | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-checkin-location/nodejs) |

## <a name="see-also"></a>Дополнительные ресурсы

* [Интеграция возможностей мультимедиа в Teams](mobile-camera-image-permissions.md)
* [Интеграция QR-кода или возможности сканера штрихкодов в Teams](qr-barcode-scanner-capability.md)
* [Интеграция выборщика людей в Teams](people-picker-capability.md)
