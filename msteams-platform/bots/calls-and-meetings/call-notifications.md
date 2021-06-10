---
title: Уведомления о входящих звонках
description: Подробные технические сведения об обработке уведомлений от входящих вызовов
ms.topic: conceptual
localization_priority: Normal
keywords: близость области вызовов вызовов уведомлений о вызове
ms.date: 04/02/2019
ms.openlocfilehash: 06068c13d27598b9a7b5e70181c69f9efb2c0afb
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020178"
---
# <a name="incoming-call-notifications"></a>Уведомления о входящих звонках

При [регистрации бота](./registering-calling-bot.md#create-new-bot-or-add-calling-capabilities)вызовов и собраний для Microsoft Teams указан веб-сайт для вызова URL-адреса. Этот URL-адрес является конечной точкой веб-адреса для всех входящих звонков в бот.

## <a name="protocol-determination"></a>Определение протокола

Входящие уведомления предоставляются в устаревшем формате для совместимости с предыдущим протоколом [Skype.](/azure/bot-service/dotnet/bot-builder-dotnet-real-time-media-concepts?view=azure-bot-service-3.0&preserve-view=true) Чтобы преобразовать вызов в протокол Microsoft Graph, бот должен определить, находится ли уведомление в устаревшем формате, и предоставить следующий ответ:

```http
HTTP/1.1 204 No Content
```

Бот получает уведомление снова, но на этот раз в протоколе Microsoft Graph.

В будущем выпуске медиаплатформы в режиме реального времени можно настроить протокол, поддерживаемый вашим приложением, чтобы избежать первоначального вызова в устаревшем формате.

В следующем разделе приводится подробная информация о входящих уведомлениях о вызове, перенаправленных для сродства региона к развертыванию.

## <a name="redirects-for-region-affinity"></a>Перенаправления для сродства регионов

Вы звоните на веб-сайт из центра обработки данных, где размещен вызов. Вызов запускается в любом центре обработки данных и не учитывает особенности региона. Уведомление отправляется в развертывание в зависимости от разрешения GeoDNS. Если ваше приложение определяет, проверяя начальную нагрузку уведомления или иным образом, что оно должно выполнить в другом развертывании, приложение предоставляет следующий ответ:

```http
HTTP/1.1 302 Found
Location: your-new-location
```

Уделите боту ответ на входящий вызов с [помощью](https://developer.microsoft.com/graph/docs/api-reference/beta/api/call_answer) API ответа. Вы можете указать `callbackUri` для обработки этого конкретного вызова. Это полезно для тех случаев, когда вызов обрабатывается определенным разделом, и эту информацию необходимо встраить в маршрутную маршрутику в `callbackUri` нужный экземпляр.

В следующем разделе приводится подробная информация о проверке подлинности вызова путем проверки маркера, размещенного на веб-сайте.

## <a name="authenticate-the-callback"></a>Проверка подлинности вызова

Для проверки запроса бот должен проверить маркер, который был размещен на веб-сайте. Каждый раз, когда API публикуется на веб-сайте, сообщение HTTP POST содержит маркер OAuth в заголовке авторизации в качестве маркера носители, а аудитория — в качестве ID приложения.

Ваше приложение должно проверить этот маркер, прежде чем принимать запрос на вызов.

Для проверки подлинности вызова используется следующий пример кода:

```http
POST https://bot.contoso.com/api/calls
Content-Type: application/json
Authentication: Bearer <TOKEN>

"value": [
    "subscriptionId": "2887CEE8344B47C291F1AF628599A93C",
    "subscriptionExpirationDateTime": "2016-11-20T18:23:45.9356913Z",
    "changeType": "updated",
    "resource": "/app/calls/8A934F51F25B4EE19613D4049491857B",
    "resourceData": {
        "@odata.type": "#microsoft.graph.call",
        "state": "Established"
    }
]
```

Маркер OAuth имеет следующие значения и подписывается Skype:

```json
{
    "aud": "0efc74f7-41c3-47a4-8775-7259bfef4241",
    "iss": "https://api.botframework.com",
    "iat": 1466741440,
    "nbf": 1466741440,
    "exp": 1466745340,
    "tid": "1fdd12d0-4620-44ed-baec-459b611f84b2"
}
```

Конфигурация OpenID, опубликованная на сайте, <https://api.aps.skype.com/v1/.well-known/OpenIdConfiguration> может использоваться для проверки маркера. Каждое значение маркера OAuth используется следующим образом:

* `aud` где аудитория — это URI ID приложения, заданный для приложения.
* `tid` является id клиента для Contoso.com.
* `iss` является эмитентом `https://api.botframework.com` маркеров.

Для обработки кода веб-сайт должен проверить маркер, убедиться, что он не истек, и проверить, был ли он подписан опубликованной конфигурацией OpenID. Кроме того, перед принятием запроса на вызов необходимо проверить, соответствует ли aud вашему ID приложения.

Дополнительные сведения см. в [ссылке проверка входящие запросы.](https://github.com/microsoftgraph/microsoft-graph-comms-samples/blob/master/Samples/Common/Sample.Common/Authentication/AuthenticationProvider.cs)

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Требования и соображения к медийным ботам с хостингом приложений](~/bots/calls-and-meetings/requirements-considerations-application-hosted-media-bots.md)
