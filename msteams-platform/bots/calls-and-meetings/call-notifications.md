---
title: Уведомления о входящих звонках
description: Сведения о протоколе входящих уведомлений для преобразования вызова из устаревшего формата в формат Graph, перенаправления для сопоставления регионов и проверки подлинности обратного вызова.
ms.topic: conceptual
ms.localizationpriority: medium
ms.date: 04/02/2019
ms.openlocfilehash: d5bdd20cb9cb7deef7419acb1da4ac96da2d89a4
ms.sourcegitcommit: 75d0072c021609af33ce584d671f610d78b3aaef
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/28/2022
ms.locfileid: "68100660"
---
# <a name="incoming-call-notifications"></a>Уведомления о входящих звонках

При [регистрации бота](./registering-calling-bot.md#create-new-bot-or-add-calling-capabilities) для звонков и собраний Microsoft Teams указывается URL-адрес веб-перехватчика для звонков. Этот URL-адрес является конечной точкой веб-перехватчика для всех входящих вызовов бота.

## <a name="protocol-determination"></a>Определение протокола

Входящее уведомление предоставляется в устаревшем формате для совместимости с предыдущим [протоколом Skype](/azure/bot-service/dotnet/bot-builder-dotnet-real-time-media-concepts?view=azure-bot-service-3.0&preserve-view=true). Чтобы преобразовать вызов в протокол Microsoft Graph, бот должен определить, имеет ли уведомление устаревший формат, и предоставляет следующий ответ:

```http
HTTP/1.1 204 No Content
```

Бот снова получит уведомление, но на этот раз по протоколу Microsoft Graph.

В будущем выпуске платформы мультимедиа в режиме реального времени можно будет настроить протокол, поддерживаемый приложением, чтобы избежать получения первоначального обратного вызова в устаревшем формате.

В следующем разделе приводятся сведения о входящих уведомлениях звонков, перенаправленных для сопоставления регионов с вашей системой.

## <a name="redirects-for-region-affinity"></a>Перенаправление для сопоставления регионов

Вы вызываете веб-перехватчик из центра обработки данных, в котором проводится вызов. Вызов начинается в любом центре обработки данных и не принимает во значение сходство между регионами. Уведомление отправляется в ваше развертывание в зависимости от разрешения GeoDNS. Если приложение определяет (посредством проверки исходных полезных данных уведомления или иным способом), что должно выполняться в другом развертывании, то предоставляет следующий ответ:

```http
HTTP/1.1 302 Found
Location: your-new-location
```

Включите бот для ответа на входящий вызов с помощью API [ответов](/graph/api/call-answer?view=graph-rest-1.0&tabs=http&preserve-view=true). Можно указать, как адресу обратного вызова `callbackUri` следует обрабатывать этот конкретный вызов. Это полезно для экземпляров с отслеживанием состояния, где вызов обрабатывается определенным разделом и вы хотите внедрить эти сведения в `callbackUri` для маршрутизации в нужный экземпляр.

В следующем разделе приводятся сведения о проверке подлинности обратного вызова путем проверки маркера, опубликованного в веб-перехватчике.

## <a name="authenticate-the-callback"></a>Проверка подлинности обратного вызова

Бот должен исследовать маркер, опубликованный в веб-перехватчике, для проверки запроса. Каждый раз, когда API публикует что-нибудь в веб-перехватчике, сообщение HTTP POST содержит маркер OAuth в заголовке авторизации в качестве маркера носителя, а в качестве аудитории указан идентификатор вашего приложения.

Приложение должно проверить этот маркер перед принятием запроса обратного вызова.

В данном примере программного кода демонстрируется проверка подлинности обратного вызова.

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

Маркер OAuth имеет следующие значения и подписан Skype:

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

Конфигурацию OpenID, опубликованную на <https://api.aps.skype.com/v1/.well-known/OpenIdConfiguration>, можно использовать для проверки маркера. Каждое значение токена OAuth используется следующим образом:

* `aud`, где аудиторией является URI идентификатора приложения, указанный для приложения.
* `tid` — идентификатор клиента для Contoso.com.
* `iss`— издатель маркера, `https://api.botframework.com`

Для обработки кода веб-перехватчик должен проверить маркер, убедиться, что срок его действия не истек, и проверить, подписан ли он опубликованной конфигурацией OpenID. До принятия запроса обратного вызова необходимо также проверить, совпадает ли aud с идентификатором вашего приложения.

Дополнительные сведения см. в статье [Проверка входящих запросов](https://github.com/microsoftgraph/microsoft-graph-comms-samples/blob/master/Samples/Common/Sample.Common/Authentication/AuthenticationProvider.cs).

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Требования и рекомендации для ботов мультимедиа, размещаемых в приложениях](~/bots/calls-and-meetings/requirements-considerations-application-hosted-media-bots.md)

## <a name="see-also"></a>Дополнительные ресурсы

* [Настройка автосекретаря](/microsoftteams/create-a-phone-system-auto-attendant)
* [Настройка автоматического ответа Комнаты Microsoft Teams на видеотелефонных устройствах Teams](/microsoftteams/set-up-auto-answer-on-teams-android)
