---
title: Добавление проверки подлинности в расширение для сообщений
author: surbhigupta
description: Добавление проверки подлинности в расширение обмена сообщениями
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 85353608e062d30529d67184716f65c3e2de1863
ms.sourcegitcommit: 22c9e44437720d30c992a4a3626a2a9f745983c1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/03/2021
ms.locfileid: "60719863"
---
# <a name="add-authentication-to-your-messaging-extension"></a>Добавление проверки подлинности в расширение для сообщений

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

## <a name="identify-the-user"></a>Определение пользователя

Каждый запрос в службы включает пользовательский ИД, имя отображения пользователя и Azure Active Directory объекта.

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

Данные и значения гарантируются для пользователя, `id` `aadObjectId` Teams проверки подлинности. Они используются в качестве ключей для слежки за учетными данными или любым кэшным состоянием в службе. Кроме того, каждый запрос содержит Azure Active Directory клиента, который используется для идентификации организации пользователя. Если это применимо, запрос также содержит командный ИД и ИД канала, из которого был зародился запрос.

## <a name="authentication"></a>Аутентификация

Если ваша служба требует проверки подлинности пользователей, пользователи должны войти, прежде чем использовать расширение обмена сообщениями. Этапы проверки подлинности аналогичны шагам бота или вкладки. Последовательность будет следующим образом:

1. Пользователь выдает запрос или запрос по умолчанию автоматически отправляется в службу.
1. Служба проверяет, проверяется ли проверка подлинности пользователя, проверяя Teams пользователя.
1. Если у пользователя нет проверки подлинности, отправьте ответ с предложенным действием, включая `auth` `openUrl` URL-адрес проверки подлинности.
1. Клиент Microsoft Teams запускает диалоговое окно с размещением веб-страницы с помощью данного URL-адреса проверки подлинности.
1. После того как пользователь войдет,  необходимо закрыть окно и отправить код проверки подлинности Teams клиенту.
1. Затем Teams переиздает запрос в службу, которая включает код проверки подлинности, переданный в шаге 5.

Служба должна убедиться, что код проверки подлинности, полученный на шаге 6, соответствует коду из шага 5. Это гарантирует, что вредоносный пользователь не пытается подменить или скомпрометировать вход в потоке. Это эффективно "закрывает цикл", чтобы завершить безопасную последовательность проверки подлинности.

### <a name="respond-with-a-sign-in-action"></a>Ответ с помощью знака в действии

Чтобы подсказывать неавентированному пользователю войти, ответьте предложенным действием типа, которое включает URL-адрес проверки `openUrl` подлинности.

#### <a name="response-example-for-a-sign-in-action"></a>Пример ответа для действия входного знака

```json
{
  "composeExtension":{
    "type":"auth",
    "suggestedActions":{
      "actions":[
        {
          "type": "openUrl",
          "value": "https://example.com/auth",
          "title": "Sign in to this app"
        }
      ]
    }
  }
}
```

> [!NOTE]
> Чтобы вход в окне Teams, доменная часть URL-адреса должна быть в списке допустимого домена вашего приложения. Дополнительные сведения см. [в схеме манифеста validDomains.](~/resources/schema/manifest-schema.md#validdomains)

### <a name="start-the-sign-in-flow"></a>Запуск знака в потоке

Ваш вход должен быть отзывчивым и соответствовать всплывающее окно. Он должен интегрироваться с [клиентом Microsoft Teams JavaScript SDK,](/javascript/api/overview/msteams-client)который использует передачу сообщений.

Как и в других встроенных Microsoft Teams, коду в окне необходимо сначала `microsoftTeams.initialize()` позвонить. Если код выполняет поток OAuth, вы можете передать Teams пользователя в окно, которое затем передает его в URL-адрес для регистрации OAuth.

### <a name="complete-the-sign-in-flow"></a>Завершить вход в поток

Когда вход в запросе завершается и перенаправляется обратно на страницу, он должен выполнить следующие действия:

1. Создание кода безопасности, случайное число. Необходимо кэшировать этот код в службе вместе с учетными данными, полученными через вход в поток, например маркерами OAuth 2.0.
1. Вызов `microsoftTeams.authentication.notifySuccess` и пропуск кода безопасности.

На этом этапе окно закрывается и управление передается Teams клиенту. Теперь клиент переизбирает исходный запрос пользователя вместе с кодом безопасности в `state` свойстве. Код безопасности может использовать код безопасности для проверки учетных данных, хранимых ранее, для завершения последовательности проверки подлинности и выполнения запроса пользователя.

#### <a name="reissued-request-example"></a>Пример повторного запроса

```json
{
    "name": "composeExtension/query",
    "value": {
        "commandId": "insertWiki",
        "parameters": [{
            "name": "searchKeyword",
            "value": "lakers"
        }],
        "state": "12345",
        "queryOptions": {
            "skip": 0,
            "count": 25
        }
    },
    "type": "invoke",
    "timestamp": "2017-04-26T05:18:25.629Z",
    "localTimestamp": "2017-04-25T22:18:25.629-07:00",
    "entities": [{
        "locale": "en-US",
        "country": "US",
        "platform": "Web",
        "type": "clientInfo"
    }],
    "text": "",
    "attachments": [],
    "address": {
        "id": "f:7638210432489287768",
        "channelId": "msteams",
        "user": {
            "id": "29:1A5TJWHkbOwSyu_L9Ktk9QFI1d_kBOEPeNEeO1INscpKHzHTvWfiau5AX_6y3SuiOby-r73dzHJ17HipUWqGPgw",
            "aadObjectId": "fc8ca1c0-d043-4af6-b09f-141536207403"
        },
        "conversation": {
            "id": "19:7705841b240044b297123ad7f9c99217@thread.skype"
        },
        "bot": {
            "id": "28:c073afa8-7e77-4f92-b3e7-aa589e952a3e",
            "name": "maotestbot2"
        },
        "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
        "useAuth": true
    },
    "source": "msteams"
}
```

## <a name="code-sample"></a>Пример кода
|**Название примера** | **Описание** |**.NET** | **Node.js**|
|----------------|-----------------|--------------|----------------|
|Расширения обмена сообщениями — auth и config | Расширение обмена сообщениями, которое имеет страницу конфигурации, принимает запросы на поиск и возвращает результаты после того, как пользователь войт. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config)|[View](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/javascript_nodejs/52.teams-messaging-extensions-search-auth-config)| 

 
