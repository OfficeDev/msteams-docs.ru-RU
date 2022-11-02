---
title: Ответ на команду поиска
author: surbhigupta
description: Узнайте, как реагировать на команду поиска из расширения сообщений в приложении Microsoft Teams. Узнайте, как реагировать на запрос пользователя.
ms.topic: conceptual
ms.author: anclear
ms.localizationpriority: medium
ms.openlocfilehash: 97fe20097e98a015759ba030004fb8c0b3b5e3f9
ms.sourcegitcommit: 9ea9a70d2591bce6b8c980d22014e160f7b45f91
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/02/2022
ms.locfileid: "68819949"
---
# <a name="respond-to-search-command"></a>Ответ на команду поиска

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

После отправки пользователем команды поиска веб-служба получает `composeExtension/query` сообщение вызова, содержащее `value` объект с параметрами поиска. Этот вызов активируется со следующими условиями:

* Как символы вводятся в поле поиска.
* `initialRun` в манифесте приложения задано значение true. Вы получите сообщение о вызове сразу после вызова команды поиска. Дополнительные сведения см. в статье [Запрос по умолчанию](#default-query).

В этом документе описано, как реагировать на запросы пользователей в виде карточек и предварительных просмотров, а также об условиях, при которых Microsoft Teams выдает запрос по умолчанию.

Параметры запроса находятся в объекте `value` запроса, который включает следующие свойства:

| Имя свойства | Назначение |
|---|---|
| `commandId` | Имя команды, вызываемой пользователем, соответствующее одной из команд, объявленных в манифесте приложения. |
| `parameters` | Массив параметров. Каждый объект параметра содержит имя параметра, а также значение параметра, предоставленное пользователем. |
| `queryOptions` | Параметры разбиения на страницы: <br>`skip`: количество пропусков для этого запроса <br>`count`: количество возвращаемых элементов. |

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

Приведенный ниже код JSON сокращен, чтобы выделить наиболее важные разделы.

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

Когда пользователь выполняет запрос, Microsoft Teams отправляет синхронный HTTP-запрос к вашей службе. На этом этапе у кода есть `5` секунды для предоставления HTTP-ответа на запрос. В течение этого времени служба может выполнить дополнительный поиск или любую другую бизнес-логику, необходимую для обслуживания запроса.

Служба должна ответить результатами, соответствующими запросу пользователя. В ответе должен быть указан код `200 OK` состояния HTTP и допустимый объект приложения или JSON со следующими свойствами:

|Имя свойства|Назначение|
|---|---|
|`composeExtension`|Конверт ответа верхнего уровня.|
|`composeExtension.type`|Тип ответа. Поддерживаются следующие типы: <br>`result`: отображает список результатов поиска. <br>`auth`: запрашивает проверку подлинности пользователя. <br>`config`: предлагает пользователю настроить расширение сообщений. <br>`message`: отображает текстовое сообщение. |
|`composeExtension.attachmentLayout`|Задает макет вложений. Используется для ответов типа `result`. <br>В настоящее время поддерживаются следующие типы: <br>`list`: список объектов карточек, содержащих поля эскизов, заголовка и текста. <br>`grid`: сетка эскизов изображений |
|`composeExtension.attachments`|Массив допустимых объектов вложений. Используется для ответов типа `result`. <br>В настоящее время поддерживаются следующие типы: <br>`application/vnd.microsoft.card.thumbnail` <br>`application/vnd.microsoft.card.hero` <br>`application/vnd.microsoft.teams.card.o365connector` <br>`application/vnd.microsoft.card.adaptive`|
|`composeExtension.suggestedActions`|Предлагаемые действия. Используется для ответов типа `auth` или `config`. |
|`composeExtension.text`|Отображаемое сообщение. Используется для ответов типа `message`. |

### <a name="response-card-types-and-previews"></a>Типы и предварительные версии карточек ответа

Teams поддерживает следующие типы карточек:

* [Карточка эскиза](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [Карточка главного имиджевого баннера](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Карточка соединителя Office 365](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [Адаптивная карточка](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

Чтобы лучше понять карточки и ознакомиться с ними, ознакомьтесь со сведениями [о карточках](~/task-modules-and-cards/what-are-cards.md).

Сведения об использовании типов эскизов и карточек-героев см. в статье [Добавление карточек и действий с карточками](~/task-modules-and-cards/cards/cards-actions.md).

Дополнительные сведения о карточке соединителя Office 365 см. в разделе [Использование карточек соединителя Office 365](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).

Список результатов отображается в пользовательском интерфейсе Microsoft Teams с предварительным просмотром каждого элемента. Предварительная версия создается одним из двух способов:

* `preview` Использование свойства в объекте `attachment` . Вложение `preview` может быть только героем или карточкой эскиза.
* Извлечение из основных `title`свойств `attachment` , `text`и `image` объекта . Основные свойства используются только в том случае, `preview` если свойство не указано.

Для карточки "Герой" или "Эскиз", за исключением действия вызова, другие действия, такие как кнопка и касание, не поддерживаются в карточке предварительного просмотра.

Чтобы отправить адаптивную карточку или карточку соединителя Office 365, необходимо включить предварительную версию. Свойство `preview` должно быть карточкой "Герой" или "Эскиз". Если не указать свойство предварительного просмотра в объекте `attachment` , предварительный просмотр не создается.

Для карточек главного элемента и эскизов не требуется указывать свойство предварительного просмотра. Предварительный просмотр создается по умолчанию.

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
> `OnTeamsMessagingExtensionSelectItemAsync` не активируется в приложении mobile Teams.

## <a name="default-query"></a>Запрос по умолчанию

Если в манифесте задано значение `initialRun` , `true` Microsoft Teams выдает запрос **по умолчанию** , когда пользователь впервые открывает расширение сообщения. Ваша служба может ответить на этот запрос набором предварительно заполненных результатов. Это полезно, если команда поиска требует проверки подлинности или настройки, отображая недавно просмотрированные элементы, избранное или любую другую информацию, которая не зависит от введенных пользователем данных.

Запрос по умолчанию имеет ту же структуру, что и любой обычный запрос пользователя, при этом `name` для поля задано значение `initialRun` и `value` задано значение , `true` как показано в следующем объекте:

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
|Поиск в расширении для сообщений Teams   |  Описывает, как определить команды поиска и отвечать на поисковые запросы.        |[Просмотр](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[Просмотр](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Добавление проверки подлинности в расширение сообщений](~/messaging-extensions/how-to/add-authentication.md)

## <a name="see-also"></a>См. также

* [Расширения для сообщений](../../what-are-messaging-extensions.md)
* [Создание первого приложения вкладки с помощью JavaScript](../../../sbs-gs-javascript.yml)
* [composeExtensions](../../../resources/schema/manifest-schema.md#composeextensions)
