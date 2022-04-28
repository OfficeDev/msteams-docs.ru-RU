---
title: Добавление проверки подлинности в расширение сообщения
author: surbhigupta
description: Узнайте, как добавить проверку подлинности в расширение сообщения с помощью примеров кода и примеров
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: e3f799214a5007f90c03b2a7f9ac280c8e8760e1
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104415"
---
# <a name="add-authentication-to-your-message-extension"></a>Добавление проверки подлинности в расширение сообщения

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

## <a name="identify-the-user"></a>Идентификация пользователя

Каждый запрос к службам включает идентификатор пользователя, отображаемое имя пользователя и Azure Active Directory объекта.

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

Для `id` пользователя`aadObjectId`, прошедшего проверку подлинности, Teams гарантируется Teams. Они используются в качестве ключей для поиска учетных данных или любого кэшированного состояния в службе. Кроме того, каждый запрос содержит Azure Active Directory клиента, который используется для идентификации организации пользователя. Если применимо, запрос также содержит идентификатор команды и идентификатор канала, из которого был создан запрос.

## <a name="authentication"></a>Проверка подлинности

Если служба требует проверки подлинности пользователя, пользователи должны войти в систему, прежде чем использовать расширение сообщения. Шаги проверки подлинности аналогичны шагам бота или вкладки. Последовательность выглядит следующим образом:

1. Пользователь отправляет запрос или запрос по умолчанию автоматически отправляется в службу.
1. Ваша служба проверяет, является ли пользователь прошедшим проверку подлинности, проверяя идентификатор Teams пользователя.
1. Если пользователь не прошедший проверку подлинности, `auth` `openUrl` отправьте ответ с предлагаемым действием, включая URL-адрес проверки подлинности.
1. Клиент Microsoft Teams запускает диалоговое окно, в котором размещается ваша веб-страница, используя заданный URL-адрес проверки подлинности.
1. После входа пользователя следует закрыть окно и отправить код проверки подлинности Teams  клиенту.
1. Затем Teams повторно передает запрос в службу, в том числе код проверки подлинности, переданный на шаге 5.

Служба должна убедиться, что код проверки подлинности, полученный на шаге 6, соответствует коду из шага 5. Это гарантирует, что злоумышленник не будет пытаться подделывать или скомпрометировать поток входа. Это фактически "закрывает цикл" для завершения последовательности безопасной проверки подлинности.

### <a name="respond-with-a-sign-in-action"></a>Ответ с помощью действия входа

Чтобы предложить пользователю, не прошедшему проверку подлинности, выполнить вход, `openUrl` ответите предлагаемым действием типа, которое включает URL-адрес проверки подлинности.

#### <a name="response-example-for-a-sign-in-action"></a>Пример ответа для действия входа

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
>
> * Чтобы интерфейс входа размещался во всплывающем Teams, часть URL-адреса домена должна быть в списке допустимых доменов приложения. Дополнительные сведения см [. в разделе validDomains](~/resources/schema/manifest-schema.md#validdomains) в схеме манифеста.
> * Размер всплывающего окна проверки подлинности можно определить, включив параметры строки запроса ширины и высоты `Value = $"{_siteUrl}/searchSettings.html?settings={escapedSettings}",`.

### <a name="start-the-sign-in-flow"></a>Запуск потока входа

Процесс входа должен быть гибким и умещаться во всплывающем окне. Он должен интегрироваться с [клиентским пакетом SDK Microsoft Teams JavaScript](/javascript/api/overview/msteams-client), который использует передачу сообщений.

Как и в случае с другими встроенными Microsoft Teams, код в окне должен сначала вызываться`microsoftTeams.initialize()`. Если код выполняет поток OAuth, вы можете передать Teams пользователя в окно, которое затем передает его по URL-адресу для входа в OAuth.

### <a name="complete-the-sign-in-flow"></a>Завершение потока входа

После завершения запроса на вход и перенаправления обратно на страницу он должен выполнить следующие действия:

1. Создайте код безопасности, случайное число. Этот код необходимо кэшировать в службе вместе с учетными данными, полученными в потоке входа, например маркерами OAuth 2.0.
1. Вызовите `microsoftTeams.authentication.notifySuccess` и передайте код безопасности.

На этом этапе окно закрывается, и элемент управления передается Teams клиента. Теперь клиент повторно выполняет исходный пользовательский запрос вместе с кодом безопасности в свойстве `state` . Код безопасности может использовать код безопасности для поиска учетных данных, сохраненных ранее, для завершения последовательности проверки подлинности, а затем выполнения запроса пользователя.

#### <a name="reissued-request-example"></a>Пример повторно выданного запроса

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
|Расширения сообщений — аутентификация и конфигурация | Расширение сообщения со страницей конфигурации принимает поисковые запросы и возвращает результаты после входа пользователя. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config)|[Просмотр](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/javascript_nodejs/52.teams-messaging-extensions-search-auth-config)|

## <a name="see-also"></a>Дополнительные ресурсы

[Поддержка единого входа для расширений сообщений](~/messaging-extensions/how-to/enable-sso-auth-me.md)
