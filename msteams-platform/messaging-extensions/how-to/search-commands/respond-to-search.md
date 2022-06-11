---
title: Ответ на команду поиска
author: surbhigupta
description: Узнайте, как реагировать на команду поиска из расширения сообщения в приложении Microsoft Teams с помощью примеров кода и примеров
ms.topic: conceptual
ms.author: anclear
ms.localizationpriority: medium
ms.openlocfilehash: 9e7dbfb6eed724fb56e7ae1e03a2132d7450947a
ms.sourcegitcommit: 12510f34b00bfdd0b0e92d35c8dbe6ea1f6f0be2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/11/2022
ms.locfileid: "66032804"
---
# <a name="respond-to-search-command"></a>Ответ на команду поиска

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

После того как пользователь отправит команду поиска, веб-служба `composeExtension/query` `value` получит сообщение об вызове, содержащее объект с параметрами поиска. Этот вызов запускается со следующими условиями:

* По мере ввода символов в поле поиска.
* `initialRun` В манифесте приложения задано значение true. Вы получаете сообщение об вызове сразу после вызова команды поиска. Дополнительные сведения см. в [описании запроса по умолчанию](#default-query).

В этом документе описывается, как реагировать на запросы пользователей в виде карточек и предварительных версий, а также условия, при которых Microsoft Teams выполняет запрос по умолчанию.

Параметры запроса находятся в объекте `value` в запросе, который включает следующие свойства:

| Имя свойства | Назначение |
|---|---|
| `commandId` | Имя команды, вызываемой пользователем, совпадает с одной из команд, объявленных в манифесте приложения. |
| `parameters` | Массив параметров. Каждый объект параметра содержит имя параметра, а также значение параметра, предоставленное пользователем. |
| `queryOptions` | Параметры разбиения на страницы: <br>`skip`: пропуск счетчика для этого запроса <br>`count`: количество возвращаемых элементов. |

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

Приведенный ниже код JSON сокращен для выделения наиболее релевантных разделов.

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

## <a name="respond-to-user-requests"></a>Реагирование на запросы пользователей

Когда пользователь выполняет запрос, Microsoft Teams выполняет синхронный HTTP-запрос к службе. На этом этапе у кода есть секунды `5` для предоставления HTTP-ответа на запрос. В течение этого времени служба может выполнить дополнительный поиск или любую другую бизнес-логику, необходимую для обслуживания запроса.

Служба должна отвечать на запросы, соответствующие запросу пользователя. Ответ должен указывать код состояния HTTP `200 OK` и допустимое приложение или объект JSON со следующими свойствами:

|Имя свойства|Назначение|
|---|---|
|`composeExtension`|Конверт ответа верхнего уровня.|
|`composeExtension.type`|Тип ответа. Поддерживаются следующие типы: <br>`result`: отображает список результатов поиска. <br>`auth`: предлагает пользователю выполнить проверку подлинности. <br>`config`: предлагает пользователю настроить расширение сообщения. <br>`message`: отображает простое текстовое сообщение. |
|`composeExtension.attachmentLayout`|Задает макет вложений. Используется для ответов типа `result`. <br>В настоящее время поддерживаются следующие типы: <br>`list`: список объектов карточек, содержащих эскизы, заголовки и текстовые поля. <br>`grid`: сетка эскизов изображений |
|`composeExtension.attachments`|Массив допустимых объектов вложений. Используется для ответов типа `result`. <br>В настоящее время поддерживаются следующие типы: <br>`application/vnd.microsoft.card.thumbnail` <br>`application/vnd.microsoft.card.hero` <br>`application/vnd.microsoft.teams.card.o365connector` <br>`application/vnd.microsoft.card.adaptive`|
|`composeExtension.suggestedActions`|Предлагаемые действия. Используется для ответов типа или `auth` `config`. |
|`composeExtension.text`|Отображаемое сообщение. Используется для ответов типа `message`. |

### <a name="response-card-types-and-previews"></a>Типы и предварительные версии карточки ответа

Teams поддерживает следующие типы карточек:

* [Карточка эскиза](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [Карточка главного имиджевого баннера](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Карточка соединителя Office 365](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [Адаптивная карточка](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

Чтобы лучше понять и просмотреть карточки, ознакомьтесь [со сведениями о карточках](~/task-modules-and-cards/what-are-cards.md).

Сведения о том, как использовать эскизы и типы карточек имиджевого баннера, см. в статье ["Добавление карточек и действий с карточками"](~/task-modules-and-cards/cards/cards-actions.md).

Дополнительные сведения о карточке Office 365 соединителя см. в разделе ["Использование Office 365 соединителей"](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).

Список результатов отображается в пользовательском Microsoft Teams с предварительным просмотром каждого элемента. Предварительный просмотр создается одним из двух способов:

* Использование свойства `preview` в объекте `attachment` . Вложение `preview` может быть только имиджевой или эскизной карточкой.
* Извлечение из основных `title`свойств `text``image` и свойств `attachment` объекта. Базовые свойства используются только в том случае, `preview` если свойство не указано.

Для карточки hero или thumbnail, за исключением действия вызова, другие действия, такие как кнопка и касание, не поддерживаются в карточке предварительного просмотра.

Чтобы отправить адаптивную карточку или Office 365 соединителя, необходимо включить предварительную версию. Свойство `preview` должно быть карточкой hero или thumbnail. Если не указать свойство предварительного просмотра в `attachment` объекте, предварительный просмотр не создается.

Для карточек "Главный имиджевый баннер" и "Эскизы" не нужно указывать свойство предварительного просмотра. Предварительный просмотр создается по умолчанию.

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

### <a name="enable-and-handle-tap-actions"></a>Включение и обработка действий касания

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
> `OnTeamsMessagingExtensionSelectItemAsync` не активируется в приложении мобильных команд.

## <a name="default-query"></a>Запрос по умолчанию

Если вы заданы `initialRun` `true` в манифесте, Microsoft Teams запрос по умолчанию, когда  пользователь впервые открывает расширение сообщения. Служба может ответить на этот запрос с помощью набора предварительно заполненных результатов. Это полезно, если для команды поиска требуется проверка подлинности или настройка, отображение недавно просматриваемых элементов, избранного или любой другой информации, которая не зависит от введенных пользователем данных.

Запрос по умолчанию имеет ту же структуру, что и любой обычный пользовательский запрос. `name` `initialRun` `value` `true` Для поля задано значение и значение, как показано в следующем объекте:

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

| Название примера           | Описание | .NET    | Node.js   |
|:---------------------|:--------------|:---------|:--------|
|Действие расширения для сообщений Teams| Описывает, как определить команды действий, создать модуль задач и ответить на действие отправки модуля задач. |[Просмотр](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[Просмотр](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) |
|Поиск в расширении для сообщений Teams   |  Описывает, как определить команды поиска и отвечать на поисковые запросы.        |[Просмотр](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Добавление проверки подлинности в расширение сообщения](~/messaging-extensions/how-to/add-authentication.md)

## <a name="see-also"></a>См. также

[Добавление конфигурации в расширение сообщения](~/get-started/first-message-extension.md)
