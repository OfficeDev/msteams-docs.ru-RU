---
title: Поиск с расширениями обмена сообщениями
description: Описание разработки расширений обмена сообщениями на основе поиска
keywords: команды расширения обмена сообщениями расширениями обмена сообщениями поиска
ms.topic: how-to
localization_priority: Normal
ms.date: 07/20/2019
ms.openlocfilehash: 515472838ff2ad35ef5dd295043ec27c53edb4f1
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566734"
---
# <a name="search-with-messaging-extensions"></a>Поиск с расширениями обмена сообщениями

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

Расширения обмена сообщениями на основе поиска позволяют запрашивать службу и отправлять эти сведения в виде карточки прямо в ваше сообщение.

![Пример карточки расширения обмена сообщениями](~/assets/images/compose-extensions/ceexample.png)

В следующих разделах описано, как это сделать:

[!include[common content for creating extensions](~/includes/messaging-extensions/messaging-extensions-common.md)]

### <a name="search-type-message-extensions"></a>Расширения сообщений типа поиска

Для расширения обмена сообщениями на основе поиска задан `type` параметр `query` . Ниже приведен пример манифеста с одной командой поиска. Одно расширение обмена сообщениями может иметь до 10 различных команд, связанных с ним. Это может включать как несколько команд поиска, так и несколько команд на основе действий.

#### <a name="complete-app-manifest-example"></a>Полный пример манифеста приложения

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

### <a name="test-via-uploading"></a>Тестирование с помощью загрузки

Вы можете протестировать расширение обмена сообщениями, загрузив приложение.

Чтобы открыть расширение обмена сообщениями, перейдите к любому из ваших чатов или каналов. Выберите **кнопку Дополнительные** параметры **(&#8943;)** в поле составить и выберите расширение обмена сообщениями.

## <a name="add-event-handlers"></a>Добавление обработчиков событий

Большая часть вашей работы включает событие, которое обрабатывает все взаимодействия в окне расширения `onQuery` обмена сообщениями.

Если вы установите `canUpdateConfiguration` в `true` манифесте,  вы включаете элемент Параметры меню для расширения обмена сообщениями и также должны обрабатывать `onQuerySettingsUrl` и `onSettingsUpdate` .

### <a name="handle-onquery-events"></a>Обработка событий OnQuery

Расширение обмена сообщениями получает событие, когда что-либо происходит в окне расширения обмена сообщениями или `onQuery` отправляется в окно.

Если в расширении обмена сообщениями используется страница конфигурации, обработник должен сначала проверить все сохраненные сведения о конфигурации; если расширение обмена сообщениями не настроено, верни ответ со ссылкой на страницу `onQuery` `config` конфигурации. Следует помнить, что ответ со страницы конфигурации также обрабатывается `onQuery` . Единственным исключением является то, когда страница конфигурации вызвана обработит для; см. `onQuerySettingsUrl` следующий раздел:

Если расширение обмена сообщениями требует проверки подлинности, проверьте сведения о состоянии пользователя; Если пользователь не подписан, следуйте инструкциям в разделе [Проверка](#authentication) подлинности в этом разделе.

Далее проверьте, установлен ли набор; если это так, примите соответствующие меры, такие как предоставление инструкций или `initialRun` список ответов.

Остальная часть обработительного средства подсказыет пользователю информацию, отображает список карт предварительного просмотра и возвращает выбранную `onQuery` пользователем карту.

### <a name="handle-onquerysettingsurl-and-onsettingsupdate-events"></a>Обработка событийQuerySettingsUrl и onSettingsUpdate

События и события работают вместе, чтобы включить `onQuerySettingsUrl` элемент `onSettingsUpdate` **Параметры** меню.

![Скриншоты расположения элемента Параметры меню](~/assets/images/compose-extensions/compose-extension-settings-menu-item.png)

Обработник возвращает URL-адрес страницы конфигурации; после закрытия страницы конфигурации обработник принимает и сохраняет `onQuerySettingsUrl` `onSettingsUpdate` возвращенный состояние. Это тот случай, когда не получает ответа `onQuery`  со страницы конфигурации.

## <a name="receive-and-respond-to-queries"></a>Получение и реагирование на запросы

Каждый запрос на расширение обмена сообщениями осуществляется с помощью объекта, `Activity` который будет размещен на URL-адресе вызова. Запрос содержит сведения о командной записи пользователя, таких как ID и значения параметров. В запросе также приводятся метаданные о контексте, в котором вызывалось расширение, включая пользовательский и клиентский ID, а также ID чата или канала и командных ИД.

### <a name="receive-user-requests"></a>Получение запросов пользователей

Когда пользователь выполняет запрос, Microsoft Teams отправляет службе стандартный объект Bot `Activity` Framework. Ваша служба должна выполнять свою логику для набора и набора поддерживаемого типа, как показано `Activity` `type` в `invoke` `name` `composeExtension` следующей таблице.

Помимо стандартных свойств активности бота, полезные данные содержат следующие метаданные запроса:

|Имя свойства|Назначение|
|---|---|
|`type`| Тип запроса; должно быть `invoke` . |
|`name`| Тип команды, выданной службе. В настоящее время поддерживаются следующие типы: <br>`composeExtension/query` <br>`composeExtension/querySettingUrl` <br>`composeExtension/setting` <br>`composeExtension/selectItem` <br>`composeExtension/queryLink` |
|`from.id`| ID пользователя, отправив запрос. |
|`from.name`| Имя пользователя, отправив запрос. |
|`from.aadObjectId`| Azure Active Directory объекта пользователя, отправив запрос. |
|`channelData.tenant.id`| Идентификатор клиента Azure Active Directory. |
|`channelData.channel.id`| ID канала (если запрос был сделан в канале). |
|`channelData.team.id`| Team ID (если запрос был сделан в канале). |
|`clientInfo`|Необязательные метаданные о клиентской программе, используемой для отправки сообщения пользователя. Объект может содержать два свойства:<br>Поле `country` содержит обнаруженное местоположение пользователя.<br>В `platform` поле описывается клиентская платформа обмена сообщениями. <br>Дополнительные сведения см. *в дополнительных* сведениях о типах сущности [non-IRI — clientInfo.](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo)|

Сами параметры запроса находятся в объекте значения, который включает следующие свойства:

| Имя свойства | Назначение |
|---|---|
| `commandId` | Имя команды, вызываемой пользователем, совпадает с одной из команд, объявленных в манифесте приложения. |
| `parameters` | Массив параметров. Каждый объект параметра содержит имя параметра, а также значение параметра, предоставляемого пользователем. |
| `queryOptions` | Параметры pagination: <br>`skip`: пропустить количество для этого запроса <br>`count`: количество элементов, которые необходимо вернуть |

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

### <a name="receive-requests-from-links-inserted-into-the-compose-message-box"></a>Получение запросов из ссылок, вставленных в поле составить сообщение

В качестве альтернативы (или в дополнение) для поиска внешней службы можно использовать URL-адрес, вставленный в поле составить сообщение для запроса службы и возврата карты. На скриншоте ниже пользователь вклеил URL-адрес для элемента работы в Azure DevOps, который расширение обмена сообщениями решило в карточку.

![Пример разгрузки ссылок](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

Чтобы расширение обмена сообщениями взаимодействовало со ссылками таким образом, сначала необходимо добавить массив в манифест приложения, как в `messageHandlers` примере ниже:

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

После того как вы добавите домен для прослушивания манифеста приложения, вам [](#respond-to-user-requests) потребуется изменить код бота, чтобы ответить на приведенную ниже заявку на вызов.

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

### <a name="respond-to-user-requests"></a>Ответы на запросы пользователей

Когда пользователь выполняет запрос, Microsoft Teams выдает синхронный http-запрос в службу. На этот момент у кода есть 5 секунд, чтобы предоставить http-ответ на запрос. За это время служба может выполнять дополнительный просмотр или любую другую бизнес-логику, необходимую для обслуживания запроса.

Служба должна отвечать результатами, совпадающие с запросом пользователя. Ответ должен указывать код состояния HTTP и `200 OK` допустимый объект приложения/json со следующим телом:

|Имя свойства|Назначение|
|---|---|
|`composeExtension`|Конверт ответа верхнего уровня.|
|`composeExtension.type`|Тип ответа. Поддерживаются следующие типы: <br>`result`: отображает список результатов поиска <br>`auth`: просит пользователя проверить подлинность <br>`config`: просит пользователя настроить расширение обмена сообщениями <br>`message`: показывает обычное текстовое сообщение |
|`composeExtension.attachmentLayout`|Указывает макет вложений. Используется для ответов типа `result` . <br>В настоящее время поддерживаются следующие типы: <br>`list`: список объектов карт, содержащих эскизы, заголовки и текстовые поля <br>`grid`: сетка изображений эскизов |
|`composeExtension.attachments`|Массив допустимых объектов вложений. Используется для ответов типа `result` . <br>В настоящее время поддерживаются следующие типы: <br>`application/vnd.microsoft.card.thumbnail` <br>`application/vnd.microsoft.card.hero` <br>`application/vnd.microsoft.teams.card.o365connector` <br>`application/vnd.microsoft.card.adaptive`|
|`composeExtension.suggestedActions`|Предлагаемые действия. Используется для ответов типа `auth` или `config` . |
|`composeExtension.text`|Отображение сообщения. Используется для ответов типа `message` . |

#### <a name="response-card-types-and-previews"></a>Типы и предварительные просмотры карт отклика

Мы поддерживаем следующие типы вложений:

* [Карта эскиза](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [Карта hero](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Office 365 Карта Connector](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [Адаптивная карта](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

Дополнительные сведения см. [в обзоре Карты.](~/task-modules-and-cards/what-are-cards.md)

Чтобы узнать, как использовать эскизы и типы карт героев, см. в статью [Добавление карт и действий карт.](~/task-modules-and-cards/cards/cards-actions.md)

Дополнительные документы, касающиеся Office 365 соединители, см. в Office 365 [карт соединители.](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)

Список результатов отображается в пользовательском Microsoft Teams с предварительным просмотром каждого элемента. Предварительный просмотр создается одним из двух способов:

* Использование `preview` свойства в `attachment` объекте. Вложение `preview` может быть только карточкой Hero или Thumbnail.
* Извлечено из основных свойств и `title` `text` свойств `image` вложения. Они используются только в том случае, если свойство не установлено и `preview` эти свойства доступны.

Вы можете отобразить предварительный просмотр адаптивной или Office 365 соединителя в списке результатов, просто задав его свойство предварительного просмотра; это необязательно, если результаты уже являются картами героя или эскиза. Если вы используете вложение предварительного просмотра, оно должно быть либо карточкой Hero, либо Thumbnail. Если не указано свойство предварительного просмотра, предварительная версия карты не будет отображаться.

#### <a name="response-example"></a>Пример ответа

В этом примере показан ответ с двумя результатами, смешивающие различные форматы карт: Office 365 Connector и Adaptive. Хотя в ответе, скорее всего, необходимо придерживаться формата одной карты, в нем показано, как свойство каждого элемента в коллекции должно явно определять предварительный просмотр в формате hero или `preview` thumbnail, как описано `attachments` выше.

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

Если вы заданы в манифесте, Microsoft Teams запрос "по умолчанию" при первом открываемом пользователем `initialRun` `true` расширении обмена сообщениями. Служба может отвечать на этот запрос набором предпопулярных результатов. Это может быть полезно для отображения, например, недавно просмотримых элементов, избранного или любой другой информации, не зависящих от ввода пользователя.

Запрос по умолчанию имеет ту же структуру, что и любой обычный запрос пользователя, за исключением `initialRun` параметра, значение строки которого `true` .

#### <a name="request-example-for-a-default-query"></a>Запрос примера запроса по умолчанию

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

## <a name="identify-the-user"></a>Определение пользователя

Каждый запрос в службы включает запутываный ID пользователя, который выполнил запрос, а также имя отображения и Azure Active Directory объекта.

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

Значения и значения гарантируются для пользователя, `id` `aadObjectId` Teams проверки подлинности. Они могут использоваться в качестве ключей для иска учетных данных или любого кэшного состояния в службе. Кроме того, каждый запрос содержит Azure Active Directory клиента пользователя, который можно использовать для идентификации организации пользователя. Если это применимо, запрос также содержит командные и канальные ИД, из которых был зародился запрос.

## <a name="authentication"></a>Проверка подлинности

Если ваша служба требует проверки подлинности пользователя, необходимо войти в пользователя, прежде чем он сможет использовать расширение обмена сообщениями. Если вы написали бот или вкладку, которая подписывает пользователя, этот раздел должен быть знаком.

Последовательность будет следующим образом:

1. Пользователь выдает запрос, или запрос по умолчанию автоматически отправляется в службу.
2. Служба проверяет, был ли пользователь впервые проверен, проверяя Teams пользователя.
3. Если пользователь не сдал проверку подлинности, отправьте ответ с предложенным действием, включая `auth` `openUrl` URL-адрес проверки подлинности.
4. Клиент Microsoft Teams запускает всплывающее окно с размещением веб-страницы с помощью данного URL-адреса проверки подлинности.
5. После того как пользователь войдет, необходимо закрыть окно и отправить "код проверки подлинности" Teams клиенту.
6. Затем Teams переиздает запрос в службу, которая включает код проверки подлинности, переданный в шаге 5.

Служба должна убедиться, что код проверки подлинности, полученный на шаге 6, соответствует коду из шага 5. Это гарантирует, что вредоносный пользователь не пытается подменить или скомпрометировать поток входных данных. Это эффективно "закрывает цикл", чтобы завершить безопасную последовательность проверки подлинности.

### <a name="respond-with-a-sign-in-action"></a>Ответ с помощью действия для регистрации

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
> Чтобы возможность регистрации была организована в всплывающее Teams, доменная часть URL-адреса должна быть в списке допустимого домена вашего приложения. Дополнительные сведения см. [в схеме манифеста validDomains.](~/resources/schema/manifest-schema.md#validdomains)

### <a name="start-the-sign-in-flow"></a>Запуск потока входов

Ваш опыт регистрации должен быть отзывчивым и соответствовать в окне всплывающее окно. Он должен интегрироваться с [клиентом Microsoft Teams JavaScript SDK,](/javascript/api/overview/msteams-client)который использует передачу сообщений.

Как и в других встроенных Microsoft Teams, коду в окне необходимо сначала `microsoftTeams.initialize()` позвонить. Если код выполняет поток OAuth, вы можете передать Teams пользователя в окно, которое затем может передать его URL-адресу для регистрации OAuth.

### <a name="complete-the-sign-in-flow"></a>Завершение потока входов

Когда запрос на вход завершается и перенаправляется обратно на страницу, он должен выполнить следующие действия:

1. Создание кода безопасности. (Это может быть случайное число.) Этот код необходимо кэшировать в службе вместе с учетными данными, полученными в потоке входа, например маркерами OAuth 2.0.
2. Вызов `microsoftTeams.authentication.notifySuccess` и пропуск кода безопасности.

На этом этапе окно закрывается и управление передается Teams клиенту. Теперь клиент может переопросить исходный запрос пользователя вместе с кодом безопасности в `state` свойстве. Код безопасности может использовать код безопасности для проверки учетных данных, хранимых ранее, для завершения последовательности проверки подлинности и выполнения запроса пользователя.

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

## <a name="sdk-support"></a>Поддержка SDK

### <a name="net"></a>.NET

Чтобы получать и обрабатывать запросы с помощью SDK bot Builder для .NET, можно проверить тип действия для входящих действий, а затем использовать метод помощника в пакете `invoke` [NuGet Microsoft.Bot.Connector.Teams,](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) чтобы определить, является ли это расширением обмена сообщениями.

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

## <a name="see-also"></a>См. также

[Примеры Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).
