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
# <a name="integrate-location-capabilities"></a>Интеграция функций местонахождения 

Этот документ поможет вам интегрировать возможности определения местоположения родного устройства с вашим приложением Teams устройства.  

Вы можете [Microsoft Teams JavaScript клиента SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), который предоставляет инструменты, необходимые для вашего приложения для доступа к родным [возможностям устройства пользователя.](native-device-permissions.md) Используйте API-файлы местоположения, такие [как getLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) [и showLocation,](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#showLocation_Location___error__SdkError__status__boolean_____void_&preserve-view=true) чтобы интегрировать возможности в приложении. 

## <a name="advantages-of-integrating-location-capabilities"></a>Преимущества интеграции возможностей определения местоположения

Основным преимуществом интеграции возможностей определения местоположения в приложениях Teams является то, что он позволяет разработчикам веб-приложений на Teams платформе использовать функциональность местоположения с Microsoft Teams JavaScript SDK. 

Следующие примеры показывают, как интеграция возможностей местоположения используется в различных сценариях:
* На фабрике руководитель может отслеживать посещаемость рабочих, попросив их сделать селфи в непосредственной близости от фабрики и поделиться им через указанное приложение. Данные о местоположении также захватовается и отправляются вместе с изображением.
* Возможности определения местоположения позволяют обслуживающему персоналу поставщика услуг обмениваться с руководством подлинными данными о состоянии здоровья сотовых вышек. Руководство может сравнить любое несоответствие между захваченной информацией о местоположении и данными, представленными обслуживающим персоналом.

Чтобы интегрировать возможности определения местоположения, необходимо обновить файл манифеста приложения и вызвать API. Для эффективной интеграции необходимо иметь хорошее понимание [фрагментов кода для](#code-snippets) вызова API-кодов местоположения. Важно ознакомиться с ошибками ответа [API для обработки](#error-handling) ошибок в вашем приложении Teams api.

> [!NOTE] 
> В настоящее Microsoft Teams поддержка возможностей определения местоположения доступна только для мобильных клиентов.

## <a name="update-manifest"></a>Манифест обновления

Обновите Teams приложение [manifest.jsфайле,](../../resources/schema/manifest-schema.md#devicepermissions) добавив `devicePermissions` свойство и указав `geolocation` . Это позволяет вашему приложению запрашивать необходимые разрешения у пользователей, прежде чем они начнут использовать возможности определения местоположения.

``` json
"devicePermissions": [
    "geolocation",
],
```

> [!NOTE]
> Запрос **разрешений автоматически** отображается при инициировании Teams API. Для получения дополнительной информации [см.](native-device-permissions.md)

## <a name="location-apis"></a>Api-файлы местоположения

Для определения возможностей определения местоположения устройства необходимо использовать следующий набор API:

| API      | Описание   |
| --- | --- |
|[getLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) | Предоставляет текущее местоположение устройства пользователя или открывает родной сборщик местоположения и возвращает выбранное пользователем местоположение. |
|[showLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#showLocation&preserve-view=true) | Показывает местоположение на карте. |

> [!NOTE]

> `getLocation()`API поставляется вместе со следующими [конфигурациями ввода,](/javascript/api/@microsoft/teams-js/locationprops?view=msteams-client-js-latest&preserve-view=true) `allowChooseLocation` и `showMap` . <br/> Если ценность `allowChooseLocation` *верна, то* пользователи могут выбрать любое место по своему выбору.<br/>  Если значение является *ложным,* то пользователи не могут изменить свое текущее местоположение.<br/> Если значение `showMap` является *ложным,* текущее местоположение получается без отображения карты. `showMap` игнорируется, `allowChooseLocation` если установлен на *истинное*.

**Веб-приложение для возможностей определения местоположения** 
 ![ веб-приложение опыт для возможностей определения местоположения](../../assets/images/tabs/location-capability.png)

## <a name="error-handling"></a>Обработка ошибок

Вы должны убедиться, что обрабатывать эти ошибки надлежащим образом в Teams приложении. В следующей таблице перечислены коды ошибок и условия, при которых генерируются ошибки: 

|Код ошибки |  Имя ошибки     | Condition|
| --------- | --------------- | -------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | API не поддерживается на текущей платформе.|
| **500** | INTERNAL_ERROR | Внутренняя ошибка встречается при выполнении требуемой операции.|
| **1000** | PERMISSION_DENIED |Пользователю было отказано в разрешении на Teams приложение или веб-приложение.|
| **4000** | INVALID_ARGUMENTS | API вызывается с неправильными или недостаточными обязательными аргументами.|
| **8000** | USER_ABORT |Пользователь отменил операцию.|
| **9000** | OLD_PLATFORM | Пользователь находится на старой сборке платформы, где реализации API нет. Обновление сборки должно решить проблему.|

## <a name="code-snippets"></a>Фрагменты кода

**Вызов `getLocation` API для получения местоположения:**

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

**Вызов `showLocation` API для отображения местоположения:**

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

* [Интеграция медиа-возможностей в Teams](mobile-camera-image-permissions.md)
* [Интеграция возможностей сканирования кода или штрих-кода в Teams](qr-barcode-scanner-capability.md)
