---
title: Использование пользовательской службы Azure Fluid Relay
author: surbhigupta
description: В этом модуле вы узнаете, как использовать пользовательскую службу Azure Fluid Relay с Live Share.
ms.topic: overview
ms.localizationpriority: high
ms.author: v-ypalikila
ms.date: 07/21/2022
ms.openlocfilehash: b8bec005450515fbef7dfb60e58fac1325235b62
ms.sourcegitcommit: 0fa0bc081da05b2a241fd8054488d9fd0104e17b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/12/2022
ms.locfileid: "68552520"
---
---

# <a name="custom-azure-fluid-relay-service"></a>Пользовательская служба Гибкого ретранслятора Azure

Хотя вы, скорее всего, предпочитаете использовать бесплатную размещенную службу, в некоторых ситуациях полезно использовать собственную службу Azure Fluid Relay для приложения Live Share.

## <a name="pre-requisites"></a>Предварительные требования

1. Создайте панель на стороне собрания и расширение собрания приложения этапа, как показано в руководстве [по валикам для игр](../teams-live-share-tutorial.md).
2. Обновите манифест приложения, чтобы включить все [необходимые разрешения](../teams-live-share-capabilities.md#register-rsc-permissions).
3. Подготовьйте службу Azure Fluid Relay, как описано в этом [руководстве](/azure/azure-fluid-relay/how-tos/provision-fluid-azure-portal).

## <a name="connect-to-azure-fluid-relay-service"></a>Подключение к службе Azure Fluid Relay

При вызове инициализации `LiveShareClient`можно определить собственный `AzureConnectionConfig`. Live Share связывает контейнеры, которые вы создаете, с собраниями, `ITokenProvider` но вам потребуется реализовать интерфейс для подписи маркеров для контейнеров. В этом примере объясняется azure `AzureFunctionTokenProvider`, которая использует облачную функцию Azure для запроса маркера доступа с сервера.

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import { LiveShareClient, LivePresence } from "@microsoft/live-share";
import { SharedMap } from "fluid-framework";
import { AzureFunctionTokenProvider } from "@fluidframework/azure-client";

// Define a custom connection for your app
const options = {
  connection: {
    tenantId: "MY_TENANT_ID",
    tokenProvider: new AzureFunctionTokenProvider(
      "MY_SERVICE_ENDPOINT_URL" + "/api/GetAzureToken",
      { userId: "userId", userName: "Test User" }
    ),
    endpoint: "MY_SERVICE_ENDPOINT_URL",
    type: "remote",
  },
};
// Join the Fluid container
const liveShare = new LiveShareClient(options);
const schema = {
  initialObjects: {
    presence: LivePresence,
    ticTacToePositions: SharedMap,
  },
};
const { container } = await liveShare.joinContainer(schema);

// ... ready to start app sync logic
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import {
  LiveShareClient,
  ILiveShareClientOptions,
  LivePresence,
} from "@microsoft/live-share";
import { SharedMap } from "fluid-framework";
import { AzureFunctionTokenProvider } from "@fluidframework/azure-client";

// Define a custom connection for your app
const options: ILiveShareClientOptions = {
  connection: {
    tenantId: "MY_TENANT_ID",
    tokenProvider: new AzureFunctionTokenProvider(
      "MY_FUNCTION_ENDPOINT_URL" + "/api/GetAzureToken",
      { userId: "userId", userName: "Test User" }
    ),
    endpoint: "MY_SERVICE_ENDPOINT_URL",
    type: "remote",
  },
};
// Join the Fluid container
const liveShare = new LiveShareClient(options);
const schema = {
  initialObjects: {
    presence: LivePresence,
    ticTacToePositions: SharedMap,
  },
};
const { container } = await liveShare.joinContainer(schema);

// ... ready to start app sync logic
```

---

## <a name="why-use-a-custom-azure-fluid-relay-service"></a>Зачем использовать пользовательскую службу Azure Fluid Relay?

Рассмотрите возможность использования пользовательского подключения службы AFR, если:

* Требовать хранение данных в контейнерах с плавными данными за пределами времени существования собрания.
* Передайте конфиденциальные данные через службу, которая требует настраиваемой политики безопасности.
* Разработка функций с помощью Fluid Framework для приложения за пределами Teams.

## <a name="why-use-live-share-with-your-custom-service"></a>Зачем использовать Live Share с пользовательской службой?

Azure Fluid Relay предназначен для работы с любым веб-приложением, то есть работает с Microsoft Teams или без него. Это вызывает важный вопрос: если я создаю собственную службу Azure Fluid Relay, нужно ли мне по-прежнему использовать Live Share?

Live Share имеет функции, которые полезны для распространенных сценариев собраний, которые дополняют другие функции вашего приложения, в том числе:

* [Сопоставление контейнеров](#container-mapping)
* [Динамические объекты и проверка роли](#live-objects-and-role-verification)
* [Синхронизация мультимедиа](#media-synchronization)

### <a name="container-mapping"></a>Сопоставление контейнеров

Вход `LiveShareClient` отвечает `@microsoft/live-share` за сопоставление уникального идентификатора собрания с контейнерами Fluid, что гарантирует, что все участники собрания присоединятся к одному контейнеру. В рамках этого процесса клиент `containerId` пытается подключиться к собранию, которое уже существует. Если контейнер не существует, `AzureClient` `AzureConnectionConfig` `containerId` он используется для создания контейнера с помощью вашего контейнера, а затем передает его другим участникам собрания.

Если ваше приложение уже имеет механизм создания контейнеров Fluid и предоставления к ним общего доступа другим участникам, `containerId` например путем вставки URL-адреса, предоставленного на этапе собрания, это может не потребоваться для вашего приложения.

### <a name="live-objects-and-role-verification"></a>Динамические объекты и проверка роли

Динамические `LivePresence`структуры данных Live Share, `LiveState``LiveEvent` такие как , и предназначены для совместной работы на собраниях и, следовательно, не поддерживаются в гибких контейнерах, используемых за пределами Microsoft Teams. Такие функции, как проверка роли, помогают приложению соответствовать ожиданиям наших пользователей.

> [!NOTE]
> В качестве дополнительных преимуществ динамические объекты также ускоряют задержки сообщений по сравнению с традиционными гибкими структурами данных.

Дополнительные сведения см [. на странице основных возможностей](../teams-live-share-capabilities.md) .

### <a name="media-synchronization"></a>Синхронизация мультимедиа

Пакеты из `@microsoft/live-share-media` не поддерживаются в контейнерах fluid, используемых за пределами Microsoft Teams.

Дополнительные сведения см. [на странице возможностей мультимедиа](../teams-live-share-media-capabilities.md) .

## <a name="see-also"></a>См. также

* [Репозиторий GitHub](https://github.com/microsoft/live-share-sdk)
* [Справочные документы по пакету SDK Live Share](/javascript/api/@microsoft/live-share/)
* [Справочная документация по пакету SDK мультимедиа Live Share](/javascript/api/@microsoft/live-share-media/)
* [Возможности Live Share](../teams-live-share-capabilities.md)
* [Возможности мультимедиа Live Share](../teams-live-share-media-capabilities.md)
* [Вопросы и ответы о Live Share](../teams-live-share-faq.md)
* [Приложения Teams на собраниях](../teams-apps-in-meetings.md)
