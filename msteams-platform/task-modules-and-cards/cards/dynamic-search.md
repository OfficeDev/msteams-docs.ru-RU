---
title: Поиск с автозавершением в адаптивных карточках
author: Rajeshwari-v
description: Описывает упреждающий поиск с помощью элемента управления Input.ChoiceSet в адаптивных карточках
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: surbhigupta
ms.openlocfilehash: 1e302a74ceffb88989989b42aa8a202d1e79fb36
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/27/2022
ms.locfileid: "65103441"
---
# <a name="typeahead-search-in-adaptive-cards"></a>Поиск с автозавершением в адаптивных карточках

Функция упреждающего поиска в адаптивных карточках обеспечивает расширенный интерфейс поиска в компоненте `input.choiceset` . Он предоставляет список вариантов ввода текста в поле поиска. Для поиска и выбора данных можно включить поиск по типу вперед с помощью адаптивных карточек.

Вы можете использовать поиск по типу вперед для следующих поисковых запросов:

* [Статический поиск](#static-typeahead-search)
* [Динамический поиск](#dynamic-typeahead-search)

## <a name="static-typeahead-search"></a>Статический поиск с упреждающей типией

Статический упреждающий поиск позволяет пользователям выполнять поиск по значениям, указанным в `input.choiceset` полезных данных адаптивной карточки. Статический поиск упреждающего ввода можно использовать для отображения пользователю нескольких вариантов. Размер полезных данных в статическом поиске увеличивается с количеством вариантов, указанных в полезных данных.
Когда пользователь начинает вводить текст, варианты фильтруются, что частично соответствует входным данным. В раскрывающемся списке выделены входные символы, соответствующие поиску.

На следующем рисунке показан статический тип упреждающего поиска:

![Статический поиск с упреждающей типией](~/assets/images/Cards/static-typeahead-search.gif)

## <a name="dynamic-typeahead-search"></a>Динамический поиск вперед

Динамический поиск упреждающего ввода полезен для поиска и выбора данных из больших наборов данных. Наборы данных загружаются динамически из набора данных, указанного в полезных данных карточки. Функция упреждающего ввода позволяет отфильтровать варианты по мере типов пользователей.

# <a name="desktop"></a>[Компьютер](#tab/desktop)

:::image type="content" source="../../assets/images/Cards/dynamic-typeahead-search-desktop.png" alt-text="Динамический поиск вперед":::

:::image type="content" source="../../assets/images/Cards/dynamic-typeahead-search-desktop-2.png" alt-text="Динамический упреждающей поиск 2":::

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

Мобильные клиенты Android и iOS поддерживают поиск по типу в адаптивных карточках.

**Сценарий**

Джон — сотрудник магазина, который работает в розничном магазине Xbox. Магазин использует бот для получения новых запросов на покупку от клиентов. Клиент может выполнять поиск из тысяч доступных игр. Для поиска и выбора вариантов клиентов используется поиск с помощью упреждающего поиска в адаптивных карточках.

**Использование упреждающего поиска в адаптивных карточках**

1. Пользователь А открывает бот магазина.
1. Пользователь А отправляет боту команду для нового **запроса клиента**. Бот отвечает адаптивной карточкой с компонентом `Input.ChoiceSet` .
1. Пользователь А использует упреждающее поиск для поиска и выбора информации в зависимости от выбора клиента.

На следующем рисунке показано мобильное взаимодействие с упреждающей функцией поиска:

![Статический поиск с упреждающей типией](~/assets/images/Cards/static-typeahead-search.gif)

---

> [!NOTE]
> С помощью динамического поиска, например расширений сообщений на основе запросов, нельзя получить расширенные возможности карточек.

## <a name="implement-typeahead-search"></a>Реализация упреждающего поиска

`Input.ChoiceSet` — один из важных входных компонентов адаптивных карточек. Вы можете добавить элемент управления "Упреждающий поиск" в `Input.ChoiceSet` компонент для реализации упреждающего поиска. Вы можете выполнить поиск и выбрать необходимые сведения, выбрав следующие параметры:

* Раскрывающийся список, например расширенный выбор.
* Переключатель, например один выбор.
* Флажки, например несколько выбранных элементов.

> [!NOTE]
> Элемент `Input.ChoiceSet` управления основан на стиле и `isMultiSelect` свойствах.

### <a name="schema-properties"></a>Свойства схемы

Следующие свойства являются новыми дополнениями [`Input.ChoiceSet`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) к схеме для включения упреждающего поиска:

| Свойство| Тип | Обязательный | Описание |
|-----------|------|----------|-------------|
| style | Compact <br/> Развернуто <br/> Фильтруется | Нет | Добавляет отфильтрованный стиль в список поддерживаемых проверк для статического упреждающего типа.|
| choices.data | Data.Query | Нет | Включает динамический упреждающей тип в качестве типов пользователей, извлекая удаленный набор вариантов из серверной части. |

### <a name="dataquery-definition"></a>Определение Data.Query

| Свойство| Тип | Обязательный | Описание |
|-----------|------|----------|-------------|
| type | Data.Query | Да | Указывает, что это объект Data.Query.|
| Набора данных | String | Да | Указывает тип данных, извлекаемых динамически. |
| value | String | Нет | Заполняет запрос на вызов бота входными данными, предоставленными пользователем `ChoiceSet`. |
| count | Номер | Нет | Заполняет запрос на вызов бота, чтобы указать количество элементов, которые должны быть возвращены. Бот игнорирует его, если пользователи хотят отправить другую сумму. |
| skip | Номер | Нет | Заполняет запрос на вызов бота, чтобы указать, что пользователи хотят разбиения на страницы и двигаться вперед в списке. |

### <a name="example"></a>Пример

Пример полезных данных, который содержит статический и динамический поиск упреждающего ввода с одним & с несколькими вариантами выбора, как показано ниже.

```json
{
  "type": "AdaptiveCard",
  "body": [
    {
      "columns": [
        {
          "width": "1",
          "items": [
            {
              "size": null,
              "url": "https://urlp.asm.skype.com/v1/url/content?url=https%3a%2f%2fi.imgur.com%2fhdOYxT8.png",
              "height": "auto",
              "type": "Image"
            }
          ],
          "type": "Column"
        },
        {
          "width": "2",
          "items": [
            {
              "size": "extraLarge",
              "text": "Game Purchase",
              "weight": "bolder",
              "wrap": true,
              "type": "TextBlock"
            }
          ],
          "type": "Column"
        }
      ],
      "type": "ColumnSet"
    },
    {
      "text": "Please fill out the below form to send a game purchase request.",
      "wrap": true,
      "type": "TextBlock"
    },
    {
      "columns": [
        {
          "width": "auto",
          "items": [
            {
              "text": "Game: ",
              "wrap": true,
              "height": "stretch",
              "type": "TextBlock"
            }
          ],
          "type": "Column"
        }
      ],
      "type": "ColumnSet"
    },
    {
      "columns": [
        {
          "width": "stretch",
          "items": [
            {
              "choices": [
                {
                  "title": "Call of Duty",
                  "value": "call_of_duty"
                },
                {
                  "title": "Death's Door",
                  "value": "deaths_door"
                },
                {
                  "title": "Grand Theft Auto V",
                  "value": "grand_theft"
                },
                {
                  "title": "Minecraft",
                  "value": "minecraft"
                }
              ],
              "style": "filtered",
              "placeholder": "Search for a game",
              "id": "choiceGameSingle",
              "type": "Input.ChoiceSet"
            }
          ],
          "type": "Column"
        }
      ],
      "type": "ColumnSet"
    },
    {
      "columns": [
        {
          "width": "auto",
          "items": [
            {
              "text": "Multi-Game: ",
              "wrap": true,
              "height": "stretch",
              "type": "TextBlock"
            }
          ],
          "type": "Column"
        }
      ],
      "type": "ColumnSet"
    },
    {
      "columns": [
        {
          "width": "stretch",
          "items": [
            {
              "choices": [
                {
                  "title": "Static Option 1",
                  "value": "static_option_1"
                },
                {
                  "title": "Static Option 2",
                  "value": "static_option_2"
                },
                {
                  "title": "Static Option 3",
                  "value": "static_option_3"
                }
              ],
              "isMultiSelect": true,
              "style": "filtered",
              "choices.data": {
                "type": "Data.Query",
                "dataset": "xbox"
              },
              "id": "choiceGameMulti",
              "type": "Input.ChoiceSet"
            }
          ],
          "type": "Column"
        }
      ],
      "type": "ColumnSet"
    },
    {
      "columns": [
        {
          "width": "auto",
          "items": [
            {
              "text": "Needed by: ",
              "wrap": true,
              "height": "stretch",
              "type": "TextBlock"
            }
          ],
          "type": "Column"
        },
        {
          "width": "stretch",
          "items": [
            {
              "id": "choiceDate",
              "type": "Input.Date"
            }
          ],
          "type": "Column"
        }
      ],
      "type": "ColumnSet"
    },
    {
      "text": "Buy and download digital games and content directly from your Xbox console, Windows 10 PC, or at Xbox.com.",
      "wrap": true,
      "type": "TextBlock"
    },
    {
      "text": "Earn points for what you already do on Xbox, then redeem your points on real rewards. Play more, get rewarded. Start earning today.",
      "wrap": true,
      "type": "TextBlock"
    }
  ],
  "actions": [
    {
      "data": {
        "msteams": {
          "type": "invoke",
          "value": {
            "type": "task/submit"
          }
        }
      },
      "title": "Request Purchase",
      "type": "Action.Submit"
    }
  ],
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "version": "1.2"
}
```

## <a name="code-snippets-for-invoke-request-and-response"></a>Фрагменты кода для запроса и ответа на вызов

### <a name="invoke-request"></a>Вызов запроса

```json
{
    "name": "application/search",
    "type": "invoke",
    "value": {
        "queryText": "fluentui",
        "queryOptions": {
            "skip": 0,
            "top": 15
        },
        "dataset": "npm"
    },
    "locale": "en-US",
    "localTimezone": "America/Los_Angeles",
    // …. other fields
}
```

### <a name="response"></a>Отклик

#### <a name="c"></a>[C#](#tab/csharp)

```csharp
protected override async Task<InvokeResponse> OnInvokeActivityAsync(ITurnContext<IInvokeActivity> turnContext, CancellationToken cancellationToken)
{
    if (turnContext.Activity.Name == "application/search")
    {
 var packages = new[] {
   new { title = "A very extensive set of extension methods", value = "FluentAssertions" },
   new { title = "Fluent UI Library", value = "FluentUI" }};

 var searchResponseData = new
 {
     type = "application/vnd.microsoft.search.searchResponse",
     value = new
     {
  results = packages
     }
 };
 var jsonString = JsonConvert.SerializeObject(searchResponseData);
 JObject jsonData = JObject.Parse(jsonString);
 return new InvokeResponse()
 {
     Status = 200,
     Body = jsonData
 };
    }

    return null;
}
```

#### <a name="nodejs"></a>[Node.js](#tab/nodejs)

```nodejs
  async onInvokeActivity(context) {
    if (context._activity.name == 'application/search') {
      // let searchQuery = context._activity.value.queryText;  // This can be used to filter the results
      var successResult = {
        status: 200,
        body: {
          "type": "application/vnd.microsoft.search.searchResponse",
          "value": {
            "results": [
              {
                "value": "FluentAssertions",
                "title": "A very extensive set of extension methods"
              },
              {
                "value": "FluentUI",
                "title": "Fluent UI Library"
              }
            ]
          }
        }
      }

      return successResult;

    }
  }
```

#### <a name="json"></a>[JSON](#tab/json)

```json
{
    "status": 200,
    "body" : {
        "type": "application/vnd.microsoft.search.searchResponse",
        "value": {
           "results": [
                {
                    "value": "FluentAssertions",
                    "title": "A very extensive set of extension methods."
                },
                {
                    "value": "FluentUI",
                    "title": "Fluent UI Library"
                }
            ]
        }
    }
}
```

---

## <a name="code-sample"></a>Пример кода

|**Название примера** | **Описание** | **C#** | **Node.js** |
|----------------|-----------------|--------------|----------------|
| Управление упреждающего поиска на адаптивных карточках | В примере показаны функции статического и динамического управления упреждающего поиска в адаптивных карточках. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-type-ahead-search-adaptive-cards/csharp) | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-type-ahead-search-adaptive-cards/nodejs) |

## <a name="see-also"></a>Дополнительные ресурсы

* [Универсальные действия для адаптивных карточек](Universal-actions-for-adaptive-cards/Overview.md)
* [Модули задач](../what-are-task-modules.md)
