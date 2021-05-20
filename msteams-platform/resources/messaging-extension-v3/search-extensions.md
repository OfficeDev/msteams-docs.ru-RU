---
title: Поиск с расширением обмена сообщениями
description: Описывает, как разрабатывать расширения обмена сообщениями на основе поиска
keywords: команды обмена сообщениями расширения обмена сообщениями поиск
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
# <a name="search-with-messaging-extensions"></a>Поиск с расширением обмена сообщениями

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

Расширение обмена сообщениями на основе поиска позволяет запрашивать вашу службу и размещать эту информацию в виде карты, прямо в ваше сообщение.

![Пример карты расширения обмена сообщениями](~/assets/images/compose-extensions/ceexample.png)

Следующие разделы описывают, как это сделать:

[!include[common content for creating extensions](~/includes/messaging-extensions/messaging-extensions-common.md)]

### <a name="search-type-message-extensions"></a>Расширение сообщений типа поиска

Для расширения обмена сообщениями на основе поиска `type` установите параметр `query` . Ниже приведен пример манифеста с одной командой поиска. Одно расширение обмена сообщениями может иметь до 10 различных команд, связанных с ним. Это может включать в себя как несколько поисковых, так и несколько команд на основе действий.

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

### <a name="test-via-uploading"></a>Тест через загрузку

Вы можете протестировать расширение обмена сообщениями, загрузив приложение.

Чтобы открыть расширение обмена сообщениями, перейдите на любой из ваших чатов или каналов. Выберите **кнопку «Больше** **&#8943;»**(подробнее) в поле для составления и выберите расширение обмена сообщениями.

## <a name="add-event-handlers"></a>Добавление обработчиков событий

Большая часть вашей работы связана `onQuery` с событием, которое обрабатывает все взаимодействия в окне расширения обмена сообщениями.

Если вы `canUpdateConfiguration` `true` устанавливаете в манифесте, вы включаете **элемент Параметры** меню для расширения обмена сообщениями, а также должны обрабатывать `onQuerySettingsUrl` и `onSettingsUpdate` .

### <a name="handle-onquery-events"></a>Ручка на событиях Квери

Расширение обмена сообщениями получает `onQuery` событие, когда что-либо происходит в окне расширения обмена сообщениями или отправляется в окно.

Если расширение обмена сообщениями использует страницу конфигурации, обработчик должен сначала проверить `onQuery` любую сохраненную информацию о конфигурации; если расширение обмена сообщениями не настроено, `config` верните ответ со ссылкой на страницу конфигурации. Имейте в виду, что ответ со страницы конфигурации также обрабатывается `onQuery` . Единственным исключением является, когда страница конфигурации вызывается обработчиком `onQuerySettingsUrl` для; см. следующий раздел:

Если расширение обмена сообщениями требует проверки подлинности, проверьте информацию о состоянии пользователя; если пользователь не ввеся, следуйте инструкциям в разделе [Аутентификация](#authentication) позже в этой теме.

Далее проверьте, `initialRun` установлен ли набор; если да, то принять соответствующие меры, такие как предоставление инструкций или список ответов.

Остальная часть обработчика `onQuery` для запросов пользователя к информации, отображает список карт предварительного просмотра и возвращает карту, выбранную пользователем.

### <a name="handle-onquerysettingsurl-and-onsettingsupdate-events"></a>Ручка на событиях КвериSettingsUrl и onSettingsUpdate

События `onQuerySettingsUrl` и `onSettingsUpdate` события работают вместе, чтобы **Параметры пункт** меню.

![Скриншоты местонахождения Параметры пункта меню](~/assets/images/compose-extensions/compose-extension-settings-menu-item.png)

Обработчик возвращает `onQuerySettingsUrl` URL для страницы конфигурации; после закрытия страницы конфигурации обработчик принимает и сохраняет `onSettingsUpdate` возвращенный состояние. Это тот случай, когда `onQuery` *не получает* ответа со страницы конфигурации.

## <a name="receive-and-respond-to-queries"></a>Получать и отвечать на запросы

Каждый запрос на расширение обмена сообщениями делается через `Activity` объект, который размещен на ваш URL-адрес обратного вызова. Запрос содержит информацию о команде пользователя, такую как значения идентификатора и параметра. Запрос также поставляет метаданные о контексте, в котором было вызвано ваше расширение, включая идентификатор пользователя и арендатора, а также идентификатор чата или идентификаторы чата или канала и команды.

### <a name="receive-user-requests"></a>Получение запросов пользователей

Когда пользователь выполняет запрос, Microsoft Teams отправляет вашу службу стандартному объекту Bot `Activity` Framework. Служба должна выполнять свою логику для набора `Activity` и `type` настройки `invoke` `name` поддерживаемого `composeExtension` типа, как показано в следующей таблице.

В дополнение к стандартным свойствам активности бота, полезная нагрузка содержит следующие метаданные запроса:

|Имя свойства|Назначение|
|---|---|
|`type`| Тип запроса; должно быть `invoke` . |
|`name`| Тип команды, которая выдается службе. В настоящее время поддерживаются следующие типы: <br>`composeExtension/query` <br>`composeExtension/querySettingUrl` <br>`composeExtension/setting` <br>`composeExtension/selectItem` <br>`composeExtension/queryLink` |
|`from.id`| Идентификатор пользователя, который отправил запрос. |
|`from.name`| Имя пользователя, отправленное запросом. |
|`from.aadObjectId`| Azure Active Directory идентификатор пользователя, который отправил запрос. |
|`channelData.tenant.id`| Идентификатор клиента Azure Active Directory. |
|`channelData.channel.id`| Идентификатор канала (если запрос был сделан в канале). |
|`channelData.team.id`| Идентификатор команды (если запрос был сделан в канале). |
|`clientInfo`|Дополнительные метаданные о клиентском программном обеспечении, используемом для отправки сообщения пользователя. Сущность может содержать два свойства:<br>`country`Поле содержит обнаруженное местоположение пользователя.<br>Поле `platform` описывает клиентскую платформу обмена сообщениями. <br>Для получения дополнительной информации, *пожалуйста,* [смотрите типы не-IRI entity - clientInfo](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo).|

Параметры запроса сами по себе находятся в объекте значения, который включает в себя следующие свойства:

| Имя свойства | Назначение |
|---|---|
| `commandId` | Имя команды, вызываемой пользователем, соответствующее одной из команд, заявленных в манифесте приложения. |
| `parameters` | Массив параметров: Каждый объект параметра содержит имя параметра, а также значение параметра, предоставляемое пользователем. |
| `queryOptions` | Параметры пагинации: <br>`skip`: пропустить подсчет для этого запроса <br>`count`: количество элементов для возврата |

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

### <a name="receive-requests-from-links-inserted-into-the-compose-message-box"></a>Получение запросов от ссылок, вставленных в поле сообщений compose

В качестве альтернативы (или в дополнение) к поиску внешнего сервиса, вы можете использовать URL-адрес, вставленный в поле для составления сообщений, чтобы запросить услугу и вернуть карту. На скриншоте ниже пользователь вставить в URL для рабочего элемента в Azure DevOps который расширение обмена сообщениями решил в карту.

![Пример разворачивания ссылки](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

Чтобы расширение обмена сообщениями взаимодействовать со ссылками таким образом, сначала необходимо добавить массив в `messageHandlers` манифест приложения, как в приведенной ниже примере:

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

После того как вы добавили домен для прослушивания манифеста приложения, вам нужно изменить код бота, чтобы [ответить на](#respond-to-user-requests) нижеувленный запрос вызова.

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

Если приложение возвращает несколько элементов, будет использован только первый.

### <a name="respond-to-user-requests"></a>Отвечайте на запросы пользователей

Когда пользователь выполняет запрос, Microsoft Teams выдает синхронный запрос HTTP в службу. На этом этапе у кода есть 5 секунд, чтобы дать ответ на запрос HTTP. За это время служба может выполнить дополнительный осмотр или любую другую бизнес-логику, необходимую для обслуживания запроса.

Служба должна отвечать результатами, соответствующими запросу пользователя. В ответе должен быть указан код статуса HTTP `200 OK` и действительный объект приложения/json со следующим органом:

|Имя свойства|Назначение|
|---|---|
|`composeExtension`|Конверт ответа верхнего уровня.|
|`composeExtension.type`|Тип ответа. Поддерживаются следующие типы: <br>`result`: отображает список результатов поиска <br>`auth`: просит пользователя проверить подлинность <br>`config`: просит пользователя настроить расширение обмена сообщениями <br>`message`: показывает обычное текстовое сообщение |
|`composeExtension.attachmentLayout`|Определяет расположение вложений. Используется для ответов типа `result` . <br>В настоящее время поддерживаются следующие типы: <br>`list`: список карточных объектов, содержащих эскизы, заголовки и текстовые поля <br>`grid`: сетка эскизных изображений |
|`composeExtension.attachments`|Массив действительных объектов вложений. Используется для ответов типа `result` . <br>В настоящее время поддерживаются следующие типы: <br>`application/vnd.microsoft.card.thumbnail` <br>`application/vnd.microsoft.card.hero` <br>`application/vnd.microsoft.teams.card.o365connector` <br>`application/vnd.microsoft.card.adaptive`|
|`composeExtension.suggestedActions`|Предлагаемые действия. Используется для ответов типа `auth` или `config` . |
|`composeExtension.text`|Сообщение для отображения. Используется для ответов типа `message` . |

#### <a name="response-card-types-and-previews"></a>Типы карт реагирования и предварительные просмотры

Мы поддерживаем следующие типы вложений:

* [Thumbnail карты](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [Карта героя](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Office 365 Коннекторная карта](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [Адаптивная карта](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

Для получения дополнительной информации [см.](~/task-modules-and-cards/what-are-cards.md)

Чтобы узнать, как использовать эскизы и типы карт героя, [см.](~/task-modules-and-cards/cards/cards-actions.md)

Дополнительную документацию, касающуюся Office 365 Connector, [можно Office 365 карт Connector.](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)

Список результатов отображается в пользовательском интерфейсе Microsoft Teams с предварительным просмотром каждого элемента. Предварительный просмотр генерируется одним из двух способов:

* Использование `preview` свойства внутри `attachment` объекта. Вложение `preview` может быть только герой или Thumbnail карты.
* Извлечено из `title` `text` основных, `image` и свойства крепления. Они используются только в том `preview` случае, если свойство не установлено и эти свойства доступны.

Вы можете отобразить предварительный просмотр адаптивной или Office 365 Connector в списке результатов, просто установив его свойство предварительного просмотра; это не обязательно, если результаты уже герой или эскиз карты. Если вы используете вложение предварительного просмотра, это должна быть либо карта Героя, либо Thumbnail. Если не указано свойство предварительного просмотра, предварительный просмотр карты потерпит неудачу и ничего не будет отображаться.

#### <a name="response-example"></a>Пример ответа

Этот пример показывает ответ с двумя результатами, смешивая различные форматы карт: Office 365 Connector и Adaptive. Хотя вы, вероятно, захотите придерживаться формата одной карты в своем ответе, он показывает, `preview` как свойство каждого элемента в коллекции должно четко определить `attachments` предварительный просмотр в формате героя или эскиза, как описано выше.

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

Если вы `initialRun` устанавливаете `true` в манифесте, Microsoft Teams выдает "по умолчанию" запрос, когда пользователь впервые открывает расширение обмена сообщениями. Служба может ответить на этот запрос набором заранее заселенных результатов. Это может быть полезно для отображения, например, недавно просмотренных элементов, избранных или любой другой информации, которая не зависит от пользовательского ввода.

Запрос по умолчанию имеет ту же структуру, что и любой обычный запрос пользователя, за исключением `initialRun` параметра, значение строки `true` которого.

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

## <a name="identify-the-user"></a>Идентификация пользователя

Каждый запрос на ваши службы включает в себя запутанное удостоверение пользователя, выдвив которое выполнило запрос, а также имя дисплея пользователя и идентификатор Azure Active Directory объекта.

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

Значения `id` `aadObjectId` и значения гарантированно являются ценностями аутентифицированного Teams пользователя. Они могут быть использованы в качестве ключей для выглядеть учетные данные или любое кэшированные состояния в вашем сервисе. Кроме того, каждый запрос содержит Azure Active Directory идентификатор пользователя, который может быть использован для идентификации организации пользователя. Если это применимо, запрос также содержит ID команды и канала, из которых возник запрос.

## <a name="authentication"></a>Проверка подлинности

Если ваша служба требует проверки подлинности пользователя, необходимо войти в систему пользователя, прежде чем он или она смогла использовать расширение обмена сообщениями. Если вы написали бота или вкладку, которая подписывается на пользователя, этот раздел должен быть знаком.

Последовательность заключается в следующем:

1. Пользователь выдает запрос, или запрос по умолчанию автоматически отправляется в службу.
2. Служба проверяет, проверил ли пользователь сначала подлинность, проверив Teams идентификатор пользователя.
3. Если пользователь не подтвердил подлинность, отправьте ответ с предлагаемым `auth` `openUrl` действием, включая URL-адрес проверки подлинности.
4. Клиент Microsoft Teams всплывающее окно, на хостинге веб-страницы, используя данный URL-адрес аутентификации.
5. После того, как пользователь войтыт, вы должны закрыть окно и отправить "код аутентификации" Teams клиента.
6. Затем Teams переоформляет запрос на ваш сервис, который включает код проверки подлинности, пройденный в шаге 5.

Служба должна убедиться, что код проверки подлинности, полученный в шаге 6, совпадает с кодом шага 5. Это гарантирует, что злоумышленник не пытается подделать или скомпрометировать поток ва-банк. Это фактически "закрывает цикл", чтобы закончить безопасную последовательность проверки подлинности.

### <a name="respond-with-a-sign-in-action"></a>Ответить с ва-воють

Чтобы побудить неодохновленного пользователя войти в систему, ответьте предложенным действием типа, `openUrl` которое включает URL-адрес проверки подлинности.

#### <a name="response-example-for-a-sign-in-action"></a>Пример ответа для действия в действии

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
> Для того, чтобы во всплывающем компьютере Teams, доменная часть URL-адреса должна быть в списке действительных доменов вашего приложения. Для получения дополнительной информации [см.](~/resources/schema/manifest-schema.md#validdomains)

### <a name="start-the-sign-in-flow"></a>Запуск потока ва-в

Ваш опыт регистрации должен быть отзывчивым и вписываться в всплывающее окно. Он должен интегрироваться с [Microsoft Teams JavaScript SDK](/javascript/api/overview/msteams-client), который использует передачу сообщений.

Как и в случае с другими встроенными Microsoft Teams, код внутри окна должен быть первым `microsoftTeams.initialize()` вызовом. Если ваш код выполняет поток OAuth, вы можете передать идентификатор пользователя Teams в окно, который затем может передать его на URL-адрес регистрации OAuth.

### <a name="complete-the-sign-in-flow"></a>Завершите поток ва-вв

Когда запрос на регистрацию завершается и перенаправляется обратно на страницу, он должен выполнить следующие шаги:

1. Создание кода безопасности. (Это может быть случайное число.) Вам необходимо кэшировать этот код на службе, а также учетные данные, полученные через поток входа, такие как токены OAuth 2.0.
2. Звоните `microsoftTeams.authentication.notifySuccess` и перевезье кода безопасности.

В этот момент окно закрывается и управление передается Teams клиента. Клиент теперь может переиздать исходный пользовательский запрос вместе с кодом безопасности в `state` свойстве. Код может использовать код безопасности для проверки учетных данных, хранящихся ранее, для завершения последовательности проверки подлинности, а затем для выполнения запроса пользователя.

#### <a name="reissued-request-example"></a>Пример переизданного запроса

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

Для получения и обработки запросов с Bot Builder SDK для .NET, вы можете проверить тип `invoke` действия на входящий деятельности, а затем использовать метод помощников в пакете NuGet [Microsoft.Bot.Connector.Teams,](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) чтобы определить, является ли это расширение деятельности обмена сообщениями.

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

[Образцы Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).
