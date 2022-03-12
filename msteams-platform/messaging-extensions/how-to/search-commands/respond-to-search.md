---
title: Ответ на команду поиска
author: surbhigupta
description: Узнайте, как реагировать на команду поиска из расширения обмена сообщениями в приложении Microsoft Teams с помощью примеров и примеров кода
ms.topic: conceptual
ms.author: anclear
ms.localizationpriority: none
ms.openlocfilehash: 42b36e5d7056368463797d1297c0674b33b6b5a0
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453826"
---
# <a name="respond-to-search-command"></a>Ответ на команду поиска

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

После отправки команды поиска `composeExtension/query` `value` веб-служба получает сообщение об вызове, содержащем объект с параметрами поиска. Этот вызов запускается при следующих условиях:

* Как символы вписались в поле поиска.
* `initialRun` установлено, что в манифесте приложения вы получите сообщение вызова, как только будет вызвана команда поиска. Дополнительные сведения см. в [запросе по умолчанию](#default-query).

В этом документе вы можете узнать, как реагировать на запросы пользователей в виде карт и предварительных просмотров, а также условия, при которых Microsoft Teams выдает запрос по умолчанию.

Параметры запроса находятся в объекте `value` в запросе, который включает следующие свойства:

| Имя свойства | Назначение |
|---|---|
| `commandId` | Имя команды, вызываемой пользователем, совпадает с одной из команд, объявленных в манифесте приложения. |
| `parameters` | Массив параметров. Каждый объект параметра содержит имя параметра, а также значение параметра, предоставленное пользователем. |
| `queryOptions` | Параметры pagination: <br>`skip`: Пропустить количество для этого запроса <br>`count`: Количество возвращаемого элемента. |

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionResponse> OnTeamsMessagingExtensionQueryAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionQuery query, CancellationToken cancellationToken)
{
  //code to handle the query
}
```

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

```typescript
class TeamsMessagingExtensionsSearch extends TeamsActivityHandler {
    async handleTeamsMessagingExtensionQuery(context, query) {
  //code to handle the query
    }
}
```

# <a name="json"></a>[JSON](#tab/json)

Ниже JSON сокращается, чтобы выделить наиболее релевантные разделы.

```json
{
  "type": "invoke",
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
...
}
```

* * *

## <a name="respond-to-user-requests"></a>Ответы на запросы пользователей

Когда пользователь выполняет запрос, Microsoft Teams выполняет синхронный http-запрос в службу. В этот момент у кода есть секунды `5` , чтобы предоставить http-ответ на запрос. За это время служба может выполнять дополнительный просмотр или любую другую бизнес-логику, необходимую для обслуживания запроса.

Служба должна отвечать результатами, совпадающие с запросом пользователя. Ответ должен указывать код состояния HTTP `200 OK` и допустимый объект приложения или JSON со следующими свойствами:

|Имя свойства|Назначение|
|---|---|
|`composeExtension`|Конверт ответа верхнего уровня.|
|`composeExtension.type`|Тип ответа. Поддерживаются следующие типы: <br>`result`: Отображает список результатов поиска <br>`auth`: Просит пользователя проверить подлинность <br>`config`: Просит пользователя настроить расширение обмена сообщениями <br>`message`: Отображает простое текстовое сообщение |
|`composeExtension.attachmentLayout`|Указывает макет вложений. Используется для ответов типа `result`. <br>В настоящее время поддерживаются следующие типы: <br>`list`: Список объектов карт, содержащих эскизы, заголовки и текстовые поля <br>`grid`: Сетка изображений эскизов |
|`composeExtension.attachments`|Массив допустимых объектов вложений. Используется для ответов типа `result`. <br>В настоящее время поддерживаются следующие типы: <br>`application/vnd.microsoft.card.thumbnail` <br>`application/vnd.microsoft.card.hero` <br>`application/vnd.microsoft.teams.card.o365connector` <br>`application/vnd.microsoft.card.adaptive`|
|`composeExtension.suggestedActions`|Предлагаемые действия. Используется для ответов типа или `auth` `config`. |
|`composeExtension.text`|Отображение сообщения. Используется для ответов типа `message`. |

### <a name="response-card-types-and-previews"></a>Типы и предварительные просмотры карт отклика

Teams поддерживает следующие типы карт:

* [Карточка эскиза](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [Карточка главного имиджевого баннера](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Карточка соединителя Office 365](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [Адаптивная карточка](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

Чтобы лучше понимать карты и их обзор, см. в этом [обзоре](~/task-modules-and-cards/what-are-cards.md).

Чтобы узнать, как использовать эскизы и типы карт героев, см. в статью [Добавление карт и действий карт](~/task-modules-and-cards/cards/cards-actions.md).

Дополнительные сведения о карточке Office 365 соединители см. в Office 365 [connector.](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)

Список результатов отображается в пользовательском Microsoft Teams с предварительным просмотром каждого элемента. Предварительный просмотр создается одним из двух способов:

* Использование свойства `preview` в объекте `attachment` . Вложение `preview` может быть только карточкой Hero или Thumbnail.
* Извлечение из основных `title`и `text``image` свойств `attachment` объекта. Основные свойства используются только в том случае, `preview` если свойство не указано.

Для карты Hero или Thumbnail, за исключением действия вызова, другие действия, такие как кнопка и касание, не поддерживаются в карточке предварительного просмотра.

Чтобы отправить адаптивную карту или Office 365 соединителю, необходимо включить предварительный просмотр. Свойство `preview` должно быть карточкой Hero или Thumbnail. Если не указать свойство предварительного `attachment` просмотра в объекте, предварительный просмотр не создается.

Для карт Hero и Thumbnail не требуется указывать свойство предварительного просмотра, предварительный просмотр создается по умолчанию.

### <a name="response-example"></a>Пример ответа

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionResponse> OnTeamsMessagingExtensionQueryAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionQuery query, CancellationToken cancellationToken) 
{
  var text = query?.Parameters?[0]?.Value as string ?? string.Empty;

  //searches NuGet for a package
  var obj = JObject.Parse(await (new HttpClient()).GetStringAsync($"https://azuresearch-usnc.nuget.org/query?q=id:{text}&prerelease=true"));
  var packages = obj["data"].Select(item => (item["id"].ToString(), item["version"].ToString(), item["description"].ToString()));

  // We take every row of the results and wrap them in cards wrapped in in MessagingExtensionAttachment objects.
  // The Preview is optional, if it includes a Tap, that will trigger the OnTeamsMessagingExtensionSelectItemAsync event back on this bot.
  var attachments = packages.Select(package => new MessagingExtensionAttachment
      {
          ContentType = HeroCard.ContentType,
          Content = new HeroCard { Title = package.Item1 },
          Preview = new HeroCard { Title = package.Item1, Tap = new CardAction { Type = "invoke", Value = package } }.ToAttachment()
      })
      .ToList();

  // The list of MessagingExtensionAttachments must we wrapped in a MessagingExtensionResult wrapped in a MessagingExtensionResponse.
  return new MessagingExtensionResponse
  {
      ComposeExtension = new MessagingExtensionResult
      {
          Type = "result",
          AttachmentLayout = "list",
          Attachments = attachments
      }
  };
}
```

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

```typescript
class TeamsMessagingExtensionsSearchBot extends TeamsActivityHandler {
    async handleTeamsMessagingExtensionQuery(context, query) {
        const searchQuery = query.parameters[0].value;
        const response = await axios.get(`http://registry.npmjs.com/-/v1/search?${ querystring.stringify({ text: searchQuery, size: 8 }) }`);

        const attachments = [];
        response.data.objects.forEach(obj => {
            const heroCard = CardFactory.heroCard(obj.package.name);
            const preview = CardFactory.heroCard(obj.package.name);
            const attachment = { ...heroCard, preview };
            attachments.push(attachment);
        });

        return {
            composeExtension: {
                type: 'result',
                attachmentLayout: 'list',
                attachments: attachments
            }
        };
    }
}
```

# <a name="json"></a>[JSON](#tab/json)

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

* * *

### <a name="enable-and-handle-tap-actions"></a>Включить и обрабатывать действия касания

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override Task<MessagingExtensionResponse> OnTeamsMessagingExtensionSelectItemAsync(ITurnContext<IInvokeActivity> turnContext, JObject query, CancellationToken cancellationToken)
{
    // The Preview card's Tap should have a Value property assigned, this will be returned to the bot in this event. 
    var (packageId, version, description, projectUrl, iconUrl) = query.ToObject<(string, string, string, string, string)>();

    var card = new ThumbnailCard
    {
        Title = "Card Select Item",
        Subtitle = description
    };

    var attachment = new MessagingExtensionAttachment
    {
        ContentType = ThumbnailCard.ContentType,
        Content = card,
    };

    return Task.FromResult(new MessagingExtensionResponse
    {
        ComposeExtension = new MessagingExtensionResult
        {
            Type = "result",
            AttachmentLayout = "list",
            Attachments = new List<MessagingExtensionAttachment> { attachment }
        }
    });
}
```

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

```typescript
async handleTeamsMessagingExtensionSelectItem(context, obj) {
        return {
            composeExtension: {
                  type: 'result',
                  attachmentLayout: 'list',
                  attachments: [CardFactory.thumbnailCard(obj.Item3)]
            }
        };
    } 
```

# <a name="json"></a>[JSON](#tab/json)

```json
{
    "name": "composeExtension/selectItem",
    "type": "invoke",
    "value": {
        "Item1": "Package_Name",
        "Item2": "Version",
        "Item3": "Package Description"
    },
    .
    .
    .
}
```

* * *

> [!NOTE]
> `OnTeamsMessagingExtensionSelectItemAsync` не запускается в приложении мобильных групп.

## <a name="default-query"></a>Запрос по умолчанию

Если вы заданы `initialRun` `true` в манифесте, Microsoft Teams запрос по умолчанию,  когда пользователь впервые откроет расширение обмена сообщениями. Служба может отвечать на этот запрос набором предварительно заполненных результатов. Это полезно, когда команда поиска требует проверки подлинности или конфигурации, отображая недавно просмотримые элементы, избранное или любую другую информацию, которая не зависит от ввода пользователя.

Запрос по умолчанию имеет ту же структуру, что и любой обычный запрос пользователя, `name` `initialRun` `value` `true` при этом поле заказано и заказано, как показано в следующем объекте:

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

## <a name="code-sample"></a>Пример кода

| Имя образца           | Описание | .NET    | Node.js   |
|:---------------------|:--------------|:---------|:--------|
|Teams расширения обмена сообщениями| Описывает, как определить команды действий, создать модуль задач и реагировать на отправку действия модуля задач. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[Просмотр](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) |
|Teams расширения обмена сообщениями   |  Описывает, как определить команды поиска и реагировать на поиски.        |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Добавление проверки подлинности в расширение обмена сообщениями](~/messaging-extensions/how-to/add-authentication.md)

## <a name="see-also"></a>См. также

[Добавление конфигурации в расширение обмена сообщениями](~/get-started/first-message-extension.md)
