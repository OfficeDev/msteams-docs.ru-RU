---
title: Введите поиск вперед в адаптивных картах
author: Rajeshwari-v
description: Описывает поиск в начале ввода с помощью управления Input.ChoiceSet в адаптивных картах
ms.topic: conceptual
localization_priority: Normal
ms.author: surbhigupta
ms.openlocfilehash: 95041b1a24ac083329a809b8a5989d77e2430e26
ms.sourcegitcommit: e45742fd2aa2ff5e5c15e8f7c20cc14fbef6d441
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/18/2021
ms.locfileid: "61075585"
---
# <a name="typeahead-search-in-adaptive-cards"></a>Введите поиск вперед в адаптивных картах

Функция поиска в адаптивных картах позволяет повысить возможности поиска в `input.choiceset` компоненте. В нем содержится список вариантов ввода текста в поле поиска. Для поиска и выбора данных можно включить предварительный поиск в типе с помощью адаптивных карт.

Для следующих поисков можно использовать поиск в печатных видах:

* [Статичный поиск](#static-typeahead-search)
* [Динамический поиск](#dynamic-typeahead-search)

## <a name="static-typeahead-search"></a>Статичный поиск впереди типа

Статичный поиск в виде впереди позволяет пользователям искать значения, указанные в полезной нагрузке `input.choiceset` адаптивной карты. Для демонстрации пользователю нескольких вариантов можно использовать статичный поиск. Размер полезной нагрузки в статическом поиске увеличивается с количеством вариантов, указанных в полезной нагрузке.
Когда пользователь начинает вводить тексты, выбор фильтруется, что частично совпадает с входными данными. В списке выпаданий выделены символы ввода, которые соответствуют поиску.

На следующем изображении демонстрируется статичный тип поиска:

![Статичный поиск впереди типа](~/assets/images/Cards/static-typeahead-search.gif)

## <a name="dynamic-typeahead-search"></a>Динамический поиск по типу вперед

Динамический поиск впереди типов полезен для поиска и выбора данных из больших наборов данных. Наборы данных загружаются динамически из набора данных, указанного в полезной нагрузке карты. Функция впереди типа помогает отфильтровать выбор в виде типов пользователей.

# <a name="desktop"></a>[Компьютер](#tab/desktop)

![Динамический поиск по типу вперед](~/assets/images/Cards/dynamic-typeahead-search-desktop.png)

![Динамическое изображение поиска на опередил типе 2](~/assets/images/Cards/dynamic-typeahead-search-desktop-2.png)

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

Мобильные клиенты Android и iOS поддерживают поиск в адаптивных картах.

**Сценарий**

Джон — сотрудник магазина, который работает в розничном магазине Xbox. Магазин использует бот для того, чтобы принимать новые запросы на покупку от клиентов. Клиент может искать из тысяч доступных игр. Поиск в адаптивных картах используется для поиска и выбора выбора клиентов.

**Использование поиска в адаптивных картах**

1. Пользователь A открывает бот магазина.
1. Пользователь A отправляет команду боту для нового **запроса клиента.** Бот отвечает адаптивной картой, которая имеет `Input.ChoiceSet` компонент.
1. Пользователь A использует поиск в печатных целях для поиска и выбора сведений, основанных на выборе клиента.

Следующее изображение иллюстрирует мобильный опыт поиска в печатных устройствах:

![Статичный поиск впереди типа](~/assets/images/Cards/static-typeahead-search.gif)

---

> [!NOTE]
> С динамическим поиском нельзя получить богатые впечатления от карт, например расширения обмена сообщениями на основе запросов.

## <a name="implement-typeahead-search"></a>Реализация поиска на опережных типах

`Input.ChoiceSet` является одним из важных компонентов ввода в адаптивных картах. Вы можете добавить элемент управления поиском впереди в `Input.ChoiceSet` компонент для реализации поиска на опередиле. Вы можете искать и выбирать требуемую информацию с помощью следующих выборок:

* Dropdown, например расширенный выбор.
* Кнопка "Радио", например один выбор.
* Флажки, например несколько выборов.

> [!NOTE]
> Управление `Input.ChoiceSet` основано на стиле и `isMultiSelect` свойствах.

### <a name="schema-properties"></a>Свойства схемы

Следующими свойствами являются новые дополнения к [`Input.ChoiceSet`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) схеме, позволяющие ввести поиск заранее:

| Свойство| Тип | Обязательный | Описание |
|-----------|------|----------|-------------|
| style | Compact <br/> Развернуто <br/> Отфильтрованный | Нет | Добавляет фильтрованный стиль в список поддерживаемых проверки для статического типа.|
| choices.data | Data.Query | Нет | Включает динамический тип вперед в качестве типов пользователей, извлекая удаленный набор вариантов из backend. |

### <a name="dataquery-definition"></a>Определение Data.Query

| Свойство| Тип | Обязательный | Описание |
|-----------|------|----------|-------------|
| type | Data.Query | Да | Указывает, что это объект Data.Query.|
| набор данных | Строка | Да | Указывает тип данных, которые извлекаются динамически. |
| value | Строка | Нет | Заполняет запрос на вызов бота с помощью ввода, предоставленного `ChoiceSet` пользователем. |
| count | Номер | Нет | Заполняет запрос на вызов бота, чтобы указать количество элементов, которые должны быть возвращены. Бот игнорирует его, если пользователи хотят отправить другую сумму. | 
| skip | Номер | Нет | Заполняет запрос на вызов бота, чтобы указать, что пользователи хотят входить в список и продвигаться вперед. |

### <a name="example"></a>Пример

Пример полезной нагрузки, содержащем статичный и динамический поиск с & нескольких вариантов выбора следующим образом:

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

## <a name="see-also"></a>См. также

* [Универсальные действия для адаптивных карточек](Universal-actions-for-adaptive-cards/Overview.md)
* [Модули задач](../what-are-task-modules.md)