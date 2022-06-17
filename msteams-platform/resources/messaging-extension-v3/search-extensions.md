---
title: Поиск с помощью расширений сообщений
description: В этом модуле вы узнаете, как разрабатывать расширения сообщений на основе поиска.
ms.topic: how-to
ms.localizationpriority: medium
ms.date: 07/20/2019
ms.openlocfilehash: a555091558d66e070f09ec6df8338ac686657019
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/17/2022
ms.locfileid: "66142754"
---
# <a name="search-with-message-extensions"></a>Поиск с помощью расширений сообщений

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

Расширения сообщений на основе поиска позволяют запрашивать службу и публиковать эти сведения в виде карточки прямо в сообщении.

![Пример карточки расширения сообщения](~/assets/images/compose-extensions/ceexample.png)

В следующих разделах описано, как это сделать.

[!include[common content for creating extensions](~/includes/messaging-extensions/messaging-extensions-common.md)]

## <a name="search-type-message-extensions"></a>Расширения сообщений типа поиска

Для расширения сообщений на основе поиска задайте для параметра `type` значение .`query` Ниже приведен пример манифеста с одной командой поиска. С одним расширением сообщения может быть связано до 10 различных команд. Это может включать как несколько команд поиска, так и несколько команд на основе действий.

### <a name="complete-app-manifest-example"></a>Полный пример манифеста приложения

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "version": "1.0",
  "id": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
  "packageName": "com.microsoft.teams.samples.bing",
  "developer": {
    "name": "John Developer",
    "websiteUrl": "http://bingbotservice.azurewebsites.net/",
    "privacyUrl": "http://bingbotservice.azurewebsites.net/privacy",
    "termsOfUseUrl": "http://bingbotservice.azurewebsites.net/termsofuse"
  },
  "name": {
    "short": "Bing",
    "full": "Bing"
  },
  "description": {
    "short": "Find Bing search results",
    "full": "Find Bing search results and share them with your team members."
  },
  "icons": {
    "outline": "bing-outline.jpg",
    "color": "bing-color.jpg"
  },
  "accentColor": "#ff6a00",
  "composeExtensions": [
    {
      "botId": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
      "canUpdateConfiguration": true,
      "commands": [{
          "id": "searchCmd",
          "description": "Search Bing for information on the web",
          "title": "Search",
          "initialRun": true,
          "parameters": [{
            "name": "searchKeyword",
            "description": "Enter your search keywords",
            "title": "Keywords"
          }]
        }
      ]
    }
  ],
  "permissions": [
    "identity",
    "messageTeamMembers"
  ],
  "validDomains": [
    "bingbotservice.azurewebsites.net",
    "*.bingbotservice.azurewebsites.net"
  ]
}
```

## <a name="test-via-uploading"></a>Тестирование с помощью отправки

Расширение сообщения можно протестировать, передав приложение.

Чтобы открыть расширение сообщения, перейдите к любому из чатов или каналов. Нажмите **кнопку "Дополнительные** параметры **" (&#8943;**) в поле создания сообщения и выберите расширение сообщения.

## <a name="add-event-handlers"></a>Добавление обработчиков событий

Большая часть работы связана с событием `onQuery` , которое обрабатывает все взаимодействия в окне расширения сообщения.

Если вы задано `canUpdateConfiguration` в `true` манифесте, вы включаете  Параметры меню для расширения сообщения, а также должны обрабатывать `onQuerySettingsUrl` и .`onSettingsUpdate`

## <a name="handle-onquery-events"></a>Обработка событий onQuery

Расширение сообщения получает событие, `onQuery` когда что-либо происходит в окне расширения сообщения или отправляется в окно.

Если расширение сообщения использует страницу конфигурации, `onQuery` обработчик должен сначала проверить наличие сохраненных сведений о конфигурации. Если расширение сообщения не настроено, `config` возвращается ответ со ссылкой на страницу конфигурации. Имейте в виду, что ответ со страницы конфигурации также обрабатывается `onQuery`. Единственным исключением является вызов страницы конфигурации `onQuerySettingsUrl`обработчиком. См. следующий раздел:

Если расширение сообщения требует проверки подлинности, проверьте сведения о состоянии пользователя. Если пользователь не выполнил вход, следуйте инструкциям в разделе " [Проверка](#authentication) подлинности" далее в этом разделе.

Затем проверьте, задано `initialRun` ли значение. Если это так, выполните соответствующие действия, такие как предоставление инструкций или список ответов.

Остальная часть обработчика `onQuery` запрашивает у пользователя сведения, отображает список карт предварительного просмотра и возвращает карточку, выбранную пользователем.

## <a name="handle-onquerysettingsurl-and-onsettingsupdate-events"></a>Обработка событий onQuerySettingsUrl и onSettingsUpdate

События `onQuerySettingsUrl` и `onSettingsUpdate` события работают вместе, **чтобы включить Параметры** меню.

![Снимки экрана расположений Параметры меню](~/assets/images/compose-extensions/compose-extension-settings-menu-item.png)

Обработчик `onQuerySettingsUrl` возвращает URL-адрес страницы конфигурации. `onSettingsUpdate` После закрытия страницы конфигурации обработчик принимает и сохраняет возвращенное состояние. Это один из вариантов, в `onQuery` *котором не* получается ответ со страницы конфигурации.

## <a name="receive-and-respond-to-queries"></a>Получение запросов и реагирование на них

Каждый запрос к расширению сообщения выполняется с помощью объекта `Activity` , который отправляется в URL-адрес обратного вызова. Запрос содержит сведения о пользовательской команде, такие как идентификатор и значения параметров. Запрос также предоставляет метаданные о контексте, в котором было вызвано расширение, включая идентификатор пользователя и клиента, а также идентификатор чата, канал и идентификаторы команды.

### <a name="receive-user-requests"></a>Получение запросов пользователей

Когда пользователь выполняет запрос, Microsoft Teams службе стандартный объект Bot Framework`Activity`. Служба должна выполнять логику для `Activity` `name` `type` `invoke` `composeExtension` поддерживаемого типа, как показано в следующей таблице.

Помимо стандартных свойств действий бота, полезные данные содержат следующие метаданные запроса:

|Имя свойства|Назначение|
|---|---|
|`type`| Тип запроса; должен иметь значение `invoke`. |
|`name`| Тип команды, выпущенной для вашей службы. В настоящее время поддерживаются следующие типы: <br>`composeExtension/query` <br>`composeExtension/querySettingUrl` <br>`composeExtension/setting` <br>`composeExtension/selectItem` <br>`composeExtension/queryLink` |
|`from.id`| Идентификатор пользователя, отправившего запрос. |
|`from.name`| Имя пользователя, отправившего запрос. |
|`from.aadObjectId`| Microsoft Azure Active Directory (Azure AD) объекта пользователя, отправив запрос. |
|`channelData.tenant.id`| Microsoft Azure Active Directory (Azure AD) клиента. |
|`channelData.channel.id`| Идентификатор канала (если запрос был выполнен в канале). |
|`channelData.team.id`| Идентификатор команды (если запрос был выполнен в канале). |
|`clientInfo`|Необязательные метаданные о клиентском программном обеспечении, используемом для отправки сообщения пользователя. Сущность может содержать два свойства:<br>Поле `country` содержит обнаруженное расположение пользователя.<br>В `platform` этом поле описывается клиентская платформа обмена сообщениями. <br>Дополнительные сведения см. *в статье о* типах сущностей, отличных от [IRI, — clientInfo](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo).|

Параметры запроса находятся в объекте значения, который включает следующие свойства:

| Имя свойства | Назначение |
|---|---|
| `commandId` | Имя команды, вызываемой пользователем, совпадает с одной из команд, объявленных в манифесте приложения. |
| `parameters` | Массив параметров: каждый объект параметра содержит имя параметра, а также значение параметра, предоставленное пользователем. |
| `queryOptions` | Параметры разбиения на страницы: <br>`skip`: пропуск счетчика для этого запроса <br>`count`: количество возвращаемых элементов |

#### <a name="request-example"></a>Пример запроса

```json
{
  "name": "composeExtension/query",
  "value": {
    "commandId": "searchCmd",
    "parameters": [
      {
        "name": "searchKeywords",
        "value": "Toronto"
      }
    ],
    "queryOptions": {
      "skip": 0,
      "count": 25
    }
  },
  "type": "invoke",
  "timestamp": "2017-05-01T15:45:51.876Z",
  "localTimestamp": "2017-05-01T08:45:51.876-07:00",
  "id": "f:622749630322482883",
  "channelId": "msteams",
  "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
  "from": {
    "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
    "name": "Larry Jin",
    "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
  },
  "conversation": {
    "id": "19:skypespaces_8198cfe0dd2647ae91930f0974768a40@thread.skype"
  },
  "recipient": {
    "id": "28:b4922ea1-5315-4fd0-9b21-d941ab06e39f",
    "name": "TheComposeExtensionDev"
  },
  "entities": [
    {
    "type": "clientInfo",
      "country": "US",
      "platform": "Windows"
    }
  ]
}
```

### <a name="receive-requests-from-links-inserted-into-the-compose-message-box"></a>Получение запросов по ссылкам, вставленным в окно создания сообщения

В качестве альтернативы (или в дополнение) к поиску во внешней службе можно использовать URL-адрес, вставленный в поле сообщения создания, для запроса службы и возврата карточки. На снимке экрана ниже пользователь вставлен в URL-адрес рабочего элемента в Azure DevOps который расширение сообщения разрешило в карточку.

![Пример развертывания ссылки](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

Чтобы расширение сообщения `messageHandlers` взаимодействовать со ссылками таким образом, сначала необходимо добавить массив в манифест приложения, как показано в примере ниже:

```json
"composeExtensions": [
  {
    "botId": "abc123456-ab12-ab12-ab12-abcdef123456",
    "messageHandlers": [
      {
        "type": "link",
        "value": {
          "domains": [
            "*.trackeddomain.com"
          ]
        }
      }
    ]
  }
]
```

После добавления домена для прослушивания манифеста приложения необходимо изменить код бота, чтобы он ответил на приведенный ниже запрос на вызов[](#respond-to-user-requests).

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

Если приложение возвращает несколько элементов, будет использоваться только первый.

### <a name="respond-to-user-requests"></a>Реагирование на запросы пользователей

Когда пользователь выполняет запрос, Microsoft Teams выполняет синхронный HTTP-запрос к службе. На этом этапе код имеет 5 секунд для предоставления HTTP-ответа на запрос. В течение этого времени служба может выполнить дополнительный поиск или любую другую бизнес-логику, необходимую для обслуживания запроса.

Ваша служба должна отвечать на запросы, соответствующие запросу пользователя. Ответ должен указывать код состояния HTTP и `200 OK` допустимый объект приложения или json со следующим текстом:

|Имя свойства|Назначение|
|---|---|
|`composeExtension`|Конверт ответа верхнего уровня.|
|`composeExtension.type`|Тип ответа. Поддерживаются следующие типы: <br>`result`: отображает список результатов поиска. <br>`auth`: предлагает пользователю выполнить проверку подлинности. <br>`config`: предлагает пользователю настроить расширение сообщения. <br>`message`: показывает обычное текстовое сообщение |
|`composeExtension.attachmentLayout`|Задает макет вложений. Используется для ответов типа `result`. <br>В настоящее время поддерживаются следующие типы: <br>`list`: список объектов карточек, содержащих эскизы, заголовки и текстовые поля. <br>`grid`: сетка эскизов изображений |
|`composeExtension.attachments`|Массив допустимых объектов вложений. Используется для ответов типа `result`. <br>В настоящее время поддерживаются следующие типы: <br>`application/vnd.microsoft.card.thumbnail` <br>`application/vnd.microsoft.card.hero` <br>`application/vnd.microsoft.teams.card.o365connector` <br>`application/vnd.microsoft.card.adaptive`|
|`composeExtension.suggestedActions`|Предлагаемые действия. Используется для ответов типа или `auth` `config`. |
|`composeExtension.text`|Отображаемое сообщение. Используется для ответов типа `message`. |

#### <a name="response-card-types-and-previews"></a>Типы и предварительные версии карточки ответа

Поддерживаются следующие типы вложений:

* [Карточка эскиза](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [Карточка главного имиджевого баннера](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Карточка соединителя Office 365](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [Адаптивная карточка](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

Дополнительные сведения см. в [разделе "Карточки](~/task-modules-and-cards/what-are-cards.md) ".

Сведения о том, как использовать эскизы и типы карточек имиджевого баннера, см. в статье ["Добавление карточек и действий с карточками"](~/task-modules-and-cards/cards/cards-actions.md).

Дополнительные сведения о карточке соединителя Office 365 см. в статье ["Использование Office 365 соединителей"](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).

Список результатов отображается в пользовательском Microsoft Teams с предварительным просмотром каждого элемента. Предварительный просмотр создается одним из двух способов:

* Использование свойства `preview` в объекте `attachment` . Вложение `preview` может быть только карточкой имиджевого баннера или эскиза.
* Извлекается из основных свойств `title``text``image` и свойств вложения. Они используются, только если `preview` свойство не задано и эти свойства доступны.

Вы можете отобразить предварительную версию адаптивной или Office 365 карточки соединителя в списке результатов, просто настроив ее свойство предварительного просмотра. Это необязательно, если результаты уже являются имиджевыми или эскизными карточками. Если вы используете вложение предварительного просмотра, оно должно быть карточкой hero или Thumbnail. Если свойство предварительного просмотра не указано, предварительный просмотр карточки завершится ошибкой и ничего не будет отображаться.

#### <a name="response-example"></a>Пример ответа

В этом примере показан ответ с двумя результатами, смешивая различные форматы карточек: Office 365 Connector и Adaptive. Хотя вы, скорее всего, захотите использовать один формат карточки в ответе, в нем показано, как свойство каждого элемента в коллекции должно явно определять предварительный просмотр в формате главного имиджевого баннера или эскиза, `preview` `attachments` как описано выше.

```json
{
  "composeExtension": {
    "type": "result",
    "attachmentLayout": "list",
    "attachments": [
      {
        "contentType": "application/vnd.microsoft.teams.card.o365connector",
        "content": {
          "sections": [
            {
              "activityTitle": "[85069]: Create a cool app",
              "activityImage&quot;: &quot;https://placekitten.com/200/200"
            },
            {
              "title": "Details",
              "facts": [
                {
                  "name": "Assigned to:",
                  "value&quot;: &quot;[Larry Brown](mailto:larryb@example.com)"
                },
                {
                  "name": "State:",
                  "value": "Active"
                }
              ]
            }
          ]
        },
        "preview": {
          "contentType": "application/vnd.microsoft.card.thumbnail",
          "content": {
            "title": "85069: Create a cool app",
            "images": [
              {
                "url": "https://placekitten.com/200/200"
              }
            ]
          }
        }
      },
      {
        "contentType": "application/vnd.microsoft.card.adaptive",
        "content": {
          "type": "AdaptiveCard",
          "body": [
            {
              "type": "Container",
              "items": [
                {
                  "type": "TextBlock",
                  "text": "Microsoft Corp (NASDAQ: MSFT)",
                  "size": "medium",
                  "isSubtle": true
                },
                {
                  "type": "TextBlock",
                  "text": "September 19, 4:00 PM EST",
                  "isSubtle": true
                }
              ]
            },
            {
              "type": "Container",
              "spacing": "none",
              "items": [
                {
                  "type": "ColumnSet",
                  "columns": [
                    {
                      "type": "Column",
                      "width": "stretch",
                      "items": [
                        {
                          "type": "TextBlock",
                          "text": "75.30",
                          "size": "extraLarge"
                        },
                        {
                          "type": "TextBlock",
                          "text": "▼ 0.20 (0.32%)",
                          "size": "small",
                          "color": "attention",
                          "spacing": "none"
                        }
                      ]
                    },
                    {
                      "type": "Column",
                      "width": "auto",
                      "items": [
                        {
                          "type": "FactSet",
                          "facts": [
                            {
                              "title": "Open",
                              "value": "62.24"
                            },
                            {
                              "title": "High",
                              "value": "62.98"
                            },
                            {
                              "title": "Low",
                              "value": "62.20"
                            }
                          ]
                        }
                      ]
                    }
                  ]
                }
              ]
            }
          ],
          "version": "1.0"
        },
        "preview": {
          "contentType": "application/vnd.microsoft.card.thumbnail",
          "content": {
            "title": "Microsoft Corp (NASDAQ: MSFT)",
            "text": "75.30 ▼ 0.20 (0.32%)"
          }
        }
      }
    ]
  }
}
```

### <a name="default-query"></a>Запрос по умолчанию

Если задано `initialRun` значение `true` в манифесте, Microsoft Teams запрос по умолчанию, когда пользователь впервые открывает расширение сообщения. Ваша служба может отвечать на этот запрос с помощью набора предварительно заполненных результатов. Это может быть полезно для отображения, например, недавно просматриваемых элементов, избранного или любой другой информации, которая не зависит от введенных пользователем данных.

Запрос по умолчанию имеет ту же структуру, что и любой обычный пользовательский запрос, `initialRun` за исключением параметра, строковое значение которого равно `true`.

#### <a name="request-example-for-a-default-query"></a>Пример запроса для запроса по умолчанию

```json
{
  "type": "invoke",
  "name": "composeExtension/query",
  "value": {
    "commandId": "searchCmd",
    "parameters": [
      {
        "name": "initialRun",
        "value": "true"
      }
    ],
    "queryOptions": {
      "skip": 0,
      "count": 25
    }
  },
  ⋮
}
```

## <a name="identify-the-user"></a>Идентификация пользователя

Каждый запрос к службам включает в себя скрытый идентификатор пользователя, выполнив запрос, а также отображаемое имя пользователя и Microsoft Azure Active Directory (Azure AD) объекта.

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

Гарантируется `id` `aadObjectId`, что значения будут у пользователя, прошедшего проверку подлинности, Teams пользователя. Их можно использовать в качестве ключей для поиска учетных данных или любого кэшированного состояния в службе. Кроме того, каждый запрос содержит Microsoft Azure Active Directory (Azure AD) клиента пользователя, который можно использовать для идентификации организации пользователя. Если применимо, запрос также содержит идентификаторы команды и канала, из которых был создан запрос.

## <a name="authentication"></a>Проверка подлинности

Если вашей службе требуется проверка подлинности пользователя, необходимо войти в систему, прежде чем он сможет использовать расширение сообщения. Если вы написали бот или вкладку, которая входит в пользователя, этот раздел должен быть знаком.

Последовательность выглядит следующим образом:

1. Пользователь отправляет запрос или запрос по умолчанию автоматически отправляется в службу.
2. Ваша служба проверяет, был ли пользователь впервые прошедший проверку подлинности, проверяя идентификатор Teams пользователя.
3. Если пользователь не прошедший проверку подлинности, `auth` `openUrl` отправьте ответ с предлагаемым действием, включая URL-адрес проверки подлинности.
4. Клиент Microsoft Teams запускает всплывающее окно, в котором размещается ваша веб-страница, используя заданный URL-адрес проверки подлинности.
5. После входа пользователя следует закрыть окно и отправить "код проверки подлинности" Teams клиенту.
6. Затем Teams повторно передает запрос в службу, в том числе код проверки подлинности, переданный на шаге 5.

Служба должна убедиться, что код проверки подлинности, полученный на шаге 6, соответствует коду из шага 5. Это гарантирует, что злоумышленник не будет пытаться подделывать или скомпрометировать поток входа. Это фактически "закрывает цикл" для завершения последовательности надежной проверки подлинности.

### <a name="respond-with-a-sign-in-action"></a>Ответ с помощью действия входа

Чтобы предложить пользователю, не прошедшему проверку подлинности, выполнить вход, в ответном сообщении предложите ему выполнить действие типа `openUrl` и укажите URL-адрес проверки подлинности.

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
> Чтобы интерфейс входа размещался во всплывающем Teams, часть URL-адреса домена должна находиться в списке допустимых доменов приложения. Дополнительные сведения см. в разделе [validDomains](~/resources/schema/manifest-schema.md#validdomains) в схеме манифеста.

### <a name="start-the-sign-in-flow"></a>Запуск потока входа

Процесс входа должен быть гибким и умещаться во всплывающем окне. Он должен интегрироваться с [клиентским пакетом SDK Microsoft Teams JavaScript](/javascript/api/overview/msteams-client), который использует передачу сообщений.

Как и в случае с другими встроенными пользовательскими интерфейсами Microsoft Teams, код в окне должен сначала вызвать `microsoftTeams.initialize()`. Если код выполняет поток OAuth, вы можете передать идентификатор пользователя Teams в окно, который затем можно передать по URL-адресу для входа в OAuth.

### <a name="complete-the-sign-in-flow"></a>Завершение потока входа

После завершения запроса на вход и перенаправления на страницу он должен выполнить следующие действия:

1. Создайте код безопасности. (Это может быть случайное число.) Необходимо кэшировать этот код в службе вместе с учетными данными, полученными с помощью потока входа, например маркеров OAuth 2.0.
2. Вызовите `microsoftTeams.authentication.notifySuccess` и передайте код безопасности.

На этом этапе окно закрывается, и управление передается Teams клиенту. Теперь клиент может повторно выполнить исходный пользовательский запрос вместе с кодом безопасности в свойстве `state` . Ваша программа может использовать код безопасности для поиска учетных данных, сохраненных ранее, для завершения последовательности проверки подлинности, а затем для выполнения запроса пользователя.

#### <a name="reissued-request-example"></a>Пример повторно отправленного запроса

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
        "type": "clientInfo",
        "country": "US",
        "platform": "Web",
        
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

## <a name="sdk-support"></a>Поддержка пакета SDK

### <a name="net"></a>.NET

Чтобы получать и обрабатывать запросы с помощью пакета SDK Bot Builder для .NET, `invoke` можно проверить тип действия для входящего действия, а затем использовать вспомогательный метод в пакете [NuGet Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams), чтобы определить, является ли это действием расширения сообщения.

#### <a name="example-code-in-net"></a>Пример кода в .NET

```csharp
public async Task<HttpResponseMessage> Post([FromBody]Activity activity)
{
    if (activity.Type == ActivityTypes.Invoke) // Received an invoke
    {
        if (activity.IsComposeExtensionQuery())
        {
            // This is the response object that will get sent back to the messaging extension request.
            ComposeExtensionResponse invokeResponse = null;

            // This helper method gets the query as an object.
            var query = activity.GetComposeExtensionQueryData();

            if (query.CommandId != null && query.Parameters != null && query.Parameters.Count > 0)
            {
                // query.Parameters has the parameters sent by client
                var results = new ComposeExtensionResult()
                {
                    AttachmentLayout = "list",
                    Type = "result",
                    Attachments = new List<ComposeExtensionAttachment>(),
                };
                invokeResponse.ComposeExtension = results;
            }

            // Return the response
            return Request.CreateResponse<ComposeExtensionResponse>(HttpStatusCode.OK, invokeResponse);
        } else
        {
            // Handle other types of Invoke activities here.
        }
    } else {
      // Failure case catch-all.
      var response = Request.CreateResponse(HttpStatusCode.BadRequest);
      response.Content = new StringContent("Invalid request! This API supports only messaging extension requests. Check your query and try again");
      return response;
    }
}
```

### <a name="nodejs"></a>Node.js

#### <a name="example-code-in-nodejs"></a>Пример кода в Node.js

```javascript
require('dotenv').config();

import * as restify from 'restify';
import * as builder from 'botbuilder';
import * as teamBuilder from 'botbuilder-teams';

class App {
    run() {
        const server = restify.createServer();
        let teamChatConnector = new teamBuilder.TeamsChatConnector({
            appId: process.env.MICROSOFT_APP_ID,
            appPassword: process.env.MICROSOFT_APP_PASSWORD
        });

        // Command ID must match what's defined in manifest
        teamChatConnector.onQuery('<%= commandId %>',
            (event: builder.IEvent,
            query: teamBuilder.ComposeExtensionQuery,
            callback: (err: Error, result: teamBuilder.IComposeExtensionResponse, statusCode: number) => void) => {
                // Check for initialRun; i.e., when you should return default results
                // if (query.parameters[0].name === 'initialRun') {}

                // Check query.queryOptions.count and query.queryOptions.skip for paging

                // Return auth response
                // let response = teamBuilder.ComposeExtensionResponse.auth().actions([
                //     builder.CardAction.openUrl(null, 'https://authUrl', 'Please sign in')
                // ]).toResponse();

                // Return config response
                // let response = teamBuilder.ComposeExtensionResponse.config().actions([
                //     builder.CardAction.openUrl(null, 'https://configUrl', 'Please sign in')
                // ]).toResponse();

                // Return result response
                let response = teamBuilder.ComposeExtensionResponse.result('list').attachments([
                    new builder.ThumbnailCard()
                        .title('Test thumbnail card')
                        .text('This is a test thumbnail card')
                        .images([new builder.CardImage().url('https://bot-framework.azureedge.net/bot-icons-v1/bot-framework-default-9.png')])
                        .toAttachment()
                ]).toResponse();
                callback(null, response, 200);
            });
        server.post('/api/composeExtension', teamChatConnector.listen());
        server.listen(process.env.PORT, () => console.log(`listening to port:` + process.env.PORT));
    }
}

const app = new App();
app.run();
```

## <a name="see-also"></a>Дополнительные ресурсы

[Примеры Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).
