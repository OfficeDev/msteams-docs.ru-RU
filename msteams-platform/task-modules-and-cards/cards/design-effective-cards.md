---
title: Разработка адаптивных карточек для приложения
description: Узнайте, как создать адаптивные карточки для Teams и получить комплект разработчика для пользовательского интерфейса Microsoft Teams.
ms.localizationpriority: high
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 6d908c47585c44718e25ec92dc8e06bff0ef5c9e
ms.sourcegitcommit: 830fdc80556a5fde642850dd6b4d1b7efda3609d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/09/2022
ms.locfileid: "63398626"
---
# <a name="designing-adaptive-cards-for-your-microsoft-teams-app"></a>Разработка адаптивных карточек для приложения Microsoft Teams

Адаптивная карточка содержит произвольный текст элементов карточки и необязательный набор действий. Адаптивные карточки — это фрагменты содержимого с действиями, которые можно добавить в беседу с помощью бота или расширения для сообщений. Эти карточки с помощью текста, графики и кнопок обеспечивают широкие возможности взаимодействия с аудиторией.

Инфраструктура адаптивных карточек используется во многих продуктах Майкрософт, включая Teams. Вы можете отправлять карточки внутри сообщений пользователям с помощью ботов или расширений для сообщений. Кроме того, пользователи могут выполнять действия в карточках при их просмотре.

:::image type="content" source="../../assets/images/adaptive-cards/adaptive-card-overview.png" alt-text="Обзор примера адаптивной карточки." border="false":::

## <a name="microsoft-teams-ui-kit"></a>Комплект разработчика для пользовательского интерфейса Microsoft Teams

В комплекте разработчика для пользовательского интерфейса Microsoft Teams можно найти более полные рекомендации по проектированию адаптивных карточек в Teams, в том числе элементы, которые можно изменять по своему усмотрению. В комплекте разработчика для пользовательского интерфейса также охвачены такие важные области, как тема, специальные возможности и адаптивный размер.

> [!div class="nextstepaction"]
> [Получить комплект разработчика для пользовательского интерфейса Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="adaptive-cards-designer"></a>Конструктор адаптивных карточек

Вы также можете приступить к разработке адаптивных карточек непосредственно в браузере.

> [!div class="nextstepaction"]
> [Попробовать конструктор адаптивных карточек](https://adaptivecards.io/designer/)

## <a name="types-of-adaptive-cards"></a>Типы адаптивных карточек

### <a name="hero"></a>Главный имиджевый баннер

Наша самая большая карточка. Используется для публикации статей или сценариев, в которых изображение играет важнейшую роль.

#### <a name="mobile"></a>Мобильная версия

:::image type="content" source="../../assets/images/adaptive-cards/mobile-hero-card.png" alt-text="Пример адаптивной карточки главного имиджевого баннера на мобильном устройстве." border="false":::

#### <a name="desktop"></a>Версия для настольного компьютера

:::image type="content" source="../../assets/images/adaptive-cards/hero-card.png" alt-text="Пример адаптивной карточки главного имиджевого баннера." border="false":::

### <a name="thumbnail"></a>Эскиз

Используется для отправки простого сообщения с действиями.

#### <a name="mobile"></a>Мобильная версия

:::image type="content" source="../../assets/images/adaptive-cards/mobile-thumbnail-card.png" alt-text="Пример адаптивной карточки эскиза на мобильном устройстве." border="false":::

#### <a name="desktop"></a>Версия для настольного компьютера

:::image type="content" source="../../assets/images/adaptive-cards/thumbnail-card.png" alt-text="Пример адаптивной карточки эскиза." border="false":::

### <a name="list"></a>Список

Используется в сценариях, где пользователь должен выбирать элемент из списка, а элементам не требуется подробное объяснение.

#### <a name="mobile"></a>Мобильная версия

:::image type="content" source="../../assets/images/adaptive-cards/mobile-list-card.png" alt-text="Пример адаптивной карточки списка на мобильном устройстве." border="false":::

#### <a name="desktop"></a>Версия для настольного компьютера

:::image type="content" source="../../assets/images/adaptive-cards/list-card.png" alt-text="Пример адаптивной карточки списка." border="false":::

### <a name="digest"></a>Дайджест

Используется для новостных дайджестов и сводных публикаций. Примечание. Рекомендуем использовать карточку эскиза для одного обновления или новости.

#### <a name="mobile"></a>Мобильная версия

:::image type="content" source="../../assets/images/adaptive-cards/mobile-digest-card.png" alt-text="Пример адаптивной карточки дайджеста на мобильном устройстве." border="false":::

#### <a name="desktop"></a>Версия для настольного компьютера

:::image type="content" source="../../assets/images/adaptive-cards/digest-card.png" alt-text="Пример адаптивной карточки дайджеста." border="false":::

### <a name="media"></a>Мультимедиа

Используется при объединении текста и мультимедиа, например звука или видео.

#### <a name="mobile"></a>Мобильная версия

:::image type="content" source="../../assets/images/adaptive-cards/mobile-media-card.png" alt-text="Пример адаптивной карточки мультимедиа на мобильном устройстве." border="false":::

#### <a name="desktop"></a>Версия для настольного компьютера

:::image type="content" source="../../assets/images/adaptive-cards/media-card.png" alt-text="Пример адаптивной карточки мультимедиа." border="false":::

### <a name="people"></a>Люди

Лучше всего использовать для эффективного уведомления о тех, кто участвует в задаче.

#### <a name="mobile"></a>Мобильная версия

:::image type="content" source="../../assets/images/adaptive-cards/mobile-people-card.png" alt-text="Пример адаптивной карточки людей на мобильном устройстве." border="false":::

#### <a name="desktop"></a>Версия для настольного компьютера

:::image type="content" source="../../assets/images/adaptive-cards/people-card.png" alt-text="Пример адаптивной карточки людей." border="false":::

### <a name="request-ticket"></a>Запрос

Используется для быстрого получения входных данных от пользователя с целью автоматического создания задачи или запроса.

#### <a name="mobile"></a>Мобильная версия

:::image type="content" source="../../assets/images/adaptive-cards/mobile-request-ticket-card.png" alt-text="Пример адаптивной карточки запроса на мобильном устройстве." border="false":::

#### <a name="desktop"></a>Версия для настольного компьютера

:::image type="content" source="../../assets/images/adaptive-cards/request-ticket-card.png" alt-text="Пример адаптивной карточки запроса." border="false":::

### <a name="imageset"></a>ImageSet

Используется для отправки нескольких эскизов изображений.

#### <a name="mobile"></a>Мобильная версия

:::image type="content" source="../../assets/images/adaptive-cards/mobile-image-set-card.png" alt-text="Пример адаптивной карточки набора изображений на мобильном устройстве." border="false":::

#### <a name="desktop"></a>Версия для настольного компьютера

:::image type="content" source="../../assets/images/adaptive-cards/image-set-card.png" alt-text="Пример адаптивной карточки набора изображений." border="false":::

### <a name="actionset"></a>ActionSet

Используется, когда пользователю нужно нажимать кнопку с последующим сбором дополнительных входных данных пользователя с той же карточки.

#### <a name="mobile"></a>Мобильная версия

:::image type="content" source="../../assets/images/adaptive-cards/mobile-action-set-card.png" alt-text="Пример адаптивной карточки набора действий на мобильном устройстве." border="false":::

#### <a name="desktop"></a>Версия для настольного компьютера

:::image type="content" source="../../assets/images/adaptive-cards/action-set-card.png" alt-text="Пример адаптивной карточки набора действий." border="false":::

### <a name="choiceset"></a>ChoiceSet

Используется для сбора нескольких входных данных от пользователя.

#### <a name="mobile"></a>Мобильная версия

:::image type="content" source="../../assets/images/adaptive-cards/mobile-choice-set-card.png" alt-text="Пример адаптивной карточки набора вариантов на мобильном устройстве." border="false":::

#### <a name="desktop"></a>Версия для настольного компьютера

:::image type="content" source="../../assets/images/adaptive-cards/choice-set-card.png" alt-text="Пример адаптивной карточки набора вариантов." border="false":::

## <a name="anatomy"></a>Структура

Адаптивные карточки обладают большой гибкостью. Но как минимум мы настоятельно рекомендуем включать следующие компоненты в каждую карточку.

#### <a name="mobile"></a>Мобильная версия

:::image type="content" source="../../assets/images/adaptive-cards/mobile-anatomy.png" alt-text="Пример адаптивной карточки структуры на мобильном устройстве." border="false":::

|Счетчик|Описание|
|----------|-----------|
|A|**Заголовок**. Создавайте ясные и четкие заголовки.|
|Б|**Копия основного текста**. Сообщайте сведения, слишком длинные или недостаточно важные для включения в заголовок.|
|В|**Основные действия**. Рекомендуется включить от 1 до 3 основных действий. Вы можете выбрать до шести действий.|

#### <a name="desktop"></a>Версия для настольного компьютера

:::image type="content" source="../../assets/images/adaptive-cards/anatomy.png" alt-text="Пример адаптивной карточки структуры." border="false":::

|Счетчик|Описание|
|----------|-----------|
|A|**Заголовок**. Создавайте ясные и четкие заголовки.|
|Б|**Копия основного текста**. Сообщайте сведения, слишком длинные или недостаточно важные для включения в заголовок.|
|В|**Основные действия**. Рекомендуется включить от 1 до 3 основных действий. Вы можете выбрать до шести действий.|

## <a name="best-practices"></a>Рекомендации

Карточки, предназначенные для узкого экрана, хорошо масштабируются на более широких экранах (но не наоборот). Также следует предполагать, что пользователи будут просматривать ваши карточки не только на настольном компьютере.

### <a name="column-layouts"></a>Макеты столбцов

Используйте [`ColumnSet`](https://adaptivecards.io/explorer/ColumnSet.html) для форматирования содержимого карточки в таблицу или сетку. Существует несколько вариантов форматирования ширины столбца. Эти рекомендации помогут вам понять, когда использовать каждый из них.

* `"width": "auto"`: определяет размер каждого столбца в `ColumnSet` согласно контенту приложения, который вы включаете в этот столбец.
  * **Рекомендуется** использовать, если у вас есть контент различной ширины и не нужно указывать приоритет определенного столбца.
  * **Рекомендуется** каждому `TextBlock` присвоить значение `"wrap": true`, так как текст не переносится по умолчанию.
  * **Не рекомендуется** присваивать значение `"width": "auto"` для каждого контейнера столбца. Например, если рядом расположен элемент ввода и кнопка, кнопка может усекаться на некоторых экранах. Вместо этого присвойте значение `auto` для столбца с кнопками и другим контентом, который всегда должен быть полностью виден.
* `"width": "stretch"`: определяет размеры столбцов в зависимости от доступной ширины `ColumnSet`. Когда несколько столбцов используют значение `"stretch"`, они делят доступную ширину на равные части.
  * **Рекомендуется** использовать с одним столбцом, если все остальные столбцы имеют статическую ширину. Например, если в одном столбце содержатся эскизные изображения шириной 50 пикселей каждое.
* `"width": "<number>"`: определяет размеры столбцов пропорционально доступной ширине `ColumnSet`. Например, если вы присвоите трем столбцам значения `"width": "1"`, `"width": "4"` и `"width": "5"`, столбцы используют 10, 40 и 50 процентов от доступной ширины.
* `"width": "<number>px"`: определяет размер столбцов по указанной ширине в пикселях. Этот подход удобен при создании таблиц.
  * **Рекомендуется** использовать, когда не нужно изменять ширину отображаемого контента (например, числа и проценты).
  * **Не рекомендуется** случайно превышать ширину возможностей отображения карточки. Помните, что доступная ширина экрана зависит от устройства. Кроме того, мобильная версия Teams не поддерживает горизонтальную прокрутку, как в классической версии Teams.

#### <a name="example-knowing-when-to-stretch-columns"></a>Пример: понимание того, когда нужно растягивать столбцы

# <a name="design"></a>[Design](#tab/design)

**Рекомендуется:** на этом экране в нижней части карточки находятся два столбца. Ширине компонента ввода присвоено значение `stretch`, а ширине кнопки **Выбрать** — значение `auto`. Это гарантирует, что кнопка полностью остается в представлении.

:::image type="content" source="~/assets/images/adaptive-cards/width-auto-do.png" alt-text="Изображение способа настройки ширины столбца в адаптивных карточках.":::

**Не рекомендуется:** на этом экране параметру `width` обоих столбцов присвоено значение `auto`. В результате кнопка **Выбрать**, расположенная справа, немного усекается по сравнению с элементом ввода.

:::image type="content" source="~/assets/images/adaptive-cards/width-auto-dont.png" alt-text="Изображение того, как не нужно настраивать ширину столбца в адаптивных карточках.":::

# <a name="code"></a>[Code](#tab/code)

Ниже представлен код для реализации примера дизайна, который следует использовать.

```json
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.2",
  "body": [
    {
      "type": "TextBlock",
      "text": "I wasn't able to identify the type of expense. Select from the list:",
      "wrap": true,
      "id": "typePrompt",
      "spacing": "Medium",
      "size": "Medium"
    },
    {
      "type": "ActionSet",
      "actions": [
        {
          "type": "Action.Submit",
          "title": "Phone Bill",
          "data": {
            "msteams": {
              "type": "messageBack",
              "displayText": "Phone Bill",
              "action": "Phone Bill"
            },
            "action": "Phone Bill"
          }
        },
        {
          "type": "Action.Submit",
          "title": "Taxi and Other Transportation",
          "data": {
            "msteams": {
              "type": "messageBack",
              "displayText": "Taxi and Other Transportation",
              "action": "Taxi and Other Transportation"
            },
            "action": "Taxi and Other Transportation"
          }
        },
        {
          "type": "Action.Submit",
          "title": "Entertainment_misc",
          "data": {
            "msteams": {
              "type": "messageBack",
              "displayText": "Entertainment_misc",
              "action": "Entertainment_misc"
            },
            "action": "Entertainment_misc"
          }
        },
        {
          "type": "Action.Submit",
          "title": "Car Rental",
          "data": {
            "msteams": {
              "type": "messageBack",
              "displayText": "Car Rental",
              "action": "Car Rental"
            },
            "action": "Car Rental"
          }
        },
        {
          "type": "Action.Submit",
          "title": "Airfare",
          "data": {
            "msteams": {
              "type": "messageBack",
              "displayText": "Airfare",
              "action": "Airfare"
            },
            "action": "Airfare"
          }
        }
      ],
      "spacing": "Medium"
    },
    {
      "type": "TextBlock",
      "text": "     ",
      "wrap": true
    },
    {
      "type": "ColumnSet",
      "columns": [
        {
          "type": "Column",
          "width": "stretch",
          "items": [
            {
              "type": "Input.ChoiceSet",
              "choices": [
                {
                  "title": "Meals",
                  "value": "Meals"
                },
                {
                  "title": "Parking/Tolls",
                  "value": "Parking/Tolls"
                },
                {
                  "title": "Accomodation",
                  "value": "Accomodation"
                },
                {
                  "title": "Fuel-Gas/Petrol/Diesel",
                  "value": "Fuel-Gas/Petrol/Diesel"
                },
                {
                  "title": "Hotel",
                  "value": "Hotel"
                },
                {
                  "title": "Meals - Employees Only",
                  "value": "Meals - Employees Only"
                },
                {
                  "title": "Accomodations",
                  "value": "Accomodations"
                },
                {
                  "title": "Misc.Expenses",
                  "value": "Misc.Expenses"
                },
                {
                  "title": "Please Categorize",
                  "value": "Please Categorize"
                }
              ],
              "placeholder": "All",
              "id": "expenseTypes",
              "value": "Meals - Employees Only"
            }
          ]
        },
        {
          "type": "Column",
          "width": "auto",
          "items": [
            {
              "type": "ActionSet",
              "actions": [
                {
                  "type": "Action.Submit",
                  "title": "Select",
                  "data": {
                    "msteams": {
                      "type": "messageBack",
                      "displayText": "Select",
                      "action": "applyType"
                    },
                    "action": "applyType"
                  }
                }
              ]
            }
          ]
        }
      ],
      "spacing": "ExtraLarge"
    }
  ]
}
```

---

#### <a name="example-using-fewer-columns"></a>Пример: использование меньшего количества столбцов

**Рекомендуется:** на мобильных устройствах, как правило, лучше отображаются макеты с небольшим количеством столбцов.

:::image type="content" source="~/assets/images/adaptive-cards/column-amount-do.png" alt-text="Изображение правильного количества столбцов в адаптивных карточках.":::

**Не рекомендуется**: использование слишком большого количества столбцов может перегружать содержимое карточки на мобильных устройствах.

:::image type="content" source="~/assets/images/adaptive-cards/column-amount-dont.png" alt-text="Изображение того, как слишком большое количество столбцов может отрицательно влиять на макет адаптивной карточки.":::

#### <a name="example-fixed-width-has-its-place"></a>Пример: применение фиксированной ширины

# <a name="design"></a>[Design](#tab/design)

Если размер отображаемого контента не требуется изменять, настройте для столбцов определенную ширину в пикселях. В этом примере показан левый столбец размером 50 пикселей, а описания рядом с эскизами растягивают длину карточки.

:::image type="content" source="~/assets/images/adaptive-cards/width-auto-do.png" alt-text="Изображение способа настройки ширины столбца в адаптивных карточках.":::

# <a name="code"></a>[Code](#tab/code)

Ниже представлен код для реализации примера дизайна.

```json
{
  "type": "AdaptiveCard",
  "version": "1.0",
  "body": [
    {
      "type": "TextBlock",
      "text": "Pick up where you left off?",
      "weight": "bolder"
    },
    {
      "type": "ColumnSet",
      "spacing": "medium",
      "columns": [
        {
          "type": "Column",
          "width": "50px",
          "items": [
            {
              "type": "Image",
              "url": "https://unsplash.it/80?image=1083",
              "size": "medium"
            }
          ]
        },
        {
          "type": "Column",
          "width": "stretch",
          "items": [
            {
              "type": "TextBlock",
              "text": "Silver Star Mountain Range"
            },
            {
              "type": "TextBlock",
              "text": "Maps",
              "isSubtle": true,
              "spacing": "none"
            }
          ]
        }
      ],
      "selectAction": {
        "type": "Action.OpenUrl",
        "url": "https://www.msn.com"
      }
    },
    {
      "type": "ColumnSet",
      "columns": [
        {
          "type": "Column",
          "width": "50px",
          "items": [
            {
              "type": "Image",
              "url": "https://unsplash.it/80?image=1082",
              "size": "medium"
            }
          ]
        },
        {
          "type": "Column",
          "width": "stretch",
          "style": "emphasis",
          "items": [
            {
              "type": "TextBlock",
              "text": "Kitchen Remodel for Homes"
            },
            {
              "type": "TextBlock",
              "text": "With EMPHASIS",
              "isSubtle": true,
              "spacing": "none"
            }
          ]
        }
      ],
      "selectAction": {
        "type": "Action.OpenUrl",
        "url": "https://www.AdaptiveCards.io"
      }
    },
    {
      "type": "ColumnSet",
      "columns": [
        {
          "type": "Column",
          "width": "50px",
          "items": [
            {
              "type": "Image",
              "url": "https://unsplash.it/80?image=1080",
              "size": "medium"
            }
          ]
        },
        {
          "type": "Column",
          "width": "stretch",
          "items": [
            {
              "type": "TextBlock",
              "text": "The Witcher: A Series"
            },
            {
              "type": "TextBlock",
              "text": "Netflix",
              "isSubtle": true,
              "spacing": "none"
            }
          ]
        }
      ],
      "selectAction": {
        "type": "Action.OpenUrl",
        "url": "https://www.outlook.com"
      }
    }
  ],
  "actions": [
    {
      "type": "Action.OpenUrl",
      "title": "Resume all",
      "url": "ms-cortana:resume-all"
    },
    {
      "type": "Action.OpenUrl",
      "title": "More activities",
      "url": "ms-cortana:more-activities"
    }
  ]
}
```

---

### <a name="text"></a>Текст

Если вы используете [`TextBlock`](https://adaptivecards.io/explorer/TextBlock.html), [`ColumnSet`](https://adaptivecards.io/explorer/ColumnSet.html) или [`Input.ChoiceSet`](https://adaptivecards.io/explorer/Input.ChoiceSet.html), присвойте свойству `wrap` значение `true`, чтобы ваша карточка не усекалась на мобильных устройствах.

#### <a name="example-making-sure-text-doesnt-truncate"></a>Пример: как избежать усечения текста

# <a name="design"></a>[Design](#tab/design)

**Рекомендуется:** на этом экране свойству `wrap` карточки присвоено значение `true`. Это позволяет тексту соответствовать любому размеру экрана.

:::image type="content" source="~/assets/images/adaptive-cards/text-wrap-true.png" alt-text="Изображение способа переноса текста в адаптивных карточках.":::

**Не рекомендуется**: на этом экране карточка не использует свойство `wrap`, поэтому текст усекается на мобильном экране.

:::image type="content" source="~/assets/images/adaptive-cards/text-wrap-false.png" alt-text="Изображение того, что может произойти, если не использовать перенос текста в адаптивных карточках.":::

# <a name="code"></a>[Code](#tab/code)

Ниже представлен код для реализации примера дизайна, который следует использовать.

```json
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.0",
  "body": [
    {
      "type": "TextBlock",
      "text": "What cuisine do you want?"
    },
    {
      "type": "Input.ChoiceSet",
      "id": "myColor",
      "style": "compact",
      "isMultiSelect": false,
      "value": "1",
      "choices": [
        {
          "title": "Chineese",
          "value": "1"
        },
        {
          "title": "Indian",
          "value": "2"
        },
        {
          "title": "Italian",
          "value": "3"
        }
      ]
    },
    {
      "type": "TextBlock",
      "text": "Select the dishes that you like?"
    },
    {
      "type": "Input.ChoiceSet",
      "id": "myColor2",
      "style": "expanded",
      "wrap" : true,
      "isMultiSelect": false,
      "value": "1",
      "choices": [
        {
          "title": "Cauliflower with potatoes sautéed with garam masala",
          "wrap" : true,
          "value": "1"
        },
        {
          "title": "Patties of potato mixed with some vegetables fried",
          "wrap" : true,
          "value": "2"
        },
        {
          "title": "Green capsicum with potatoes sautéed with cumin seeds",
          "wrap" : true,
          "value": "3"
        }
      ]
    }
  ]
}
```

---

### <a name="containers"></a>Контейнеры

`Container` позволяет сгруппировать набор связанных элементов.

* **Рекомендуется** использовать свойство `style`, чтобы выделить контейнер.
* **Рекомендуется** использовать свойство `selectAction`, чтобы связать действие с другими элементами в контейнере.
* **Рекомендуется** использовать свойство `Action.ToggleVisibility`, чтобы сделать группу элементов сворачиваемой.
* **Не рекомендуется** использовать контейнеры для целей, отличных от упомянутых ранее.

### <a name="images"></a>изображения;

Следуйте этим рекомендациям при добавлении изображений на карточки.

* **Рекомендуется** разрабатывать изображения для экранов с высоким значением DPI, чтобы избежать пикселизации. Лучше отобразить изображение 100x100 пикселей в области 50x50 пикселей, чем наоборот.
* **Рекомендуется**: если необходимо управлять точным размером изображений, используйте свойства `width` и `height`.
* **Не рекомендуется** добавлять отступ к изображениям. Это обычно добавляет нежелательные проблемы с интервалами и макетом.
* Что касается цвета фона:
  * **Рекомендуется** использовать прозрачный фон, чтобы ваши изображения адаптировались к любой теме Teams.
  * **Не рекомендуется** включать фиксированный цвет фона, если не требуется демонстрировать пользователям определенный цвет.
  * **Не рекомендуется** добавлять в `TextBlock` цвет фона, приводящий к снижению удобства чтения. Например, если у вас темный фон, используйте более светлый цвет текста и наоборот.

### <a name="actions"></a>Действия

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-do.png" alt-text="Рекомендация о включении в адаптивную карточку только небольшого набора действий." border="false":::

#### <a name="do-use-up-to-six-primary-actions"></a>Рекомендуется: используйте до шести основных действий

Адаптивные карточки могут поддерживать шесть основных действий, но большинству карточек это не требуется. Действия должны быть четкими, краткими и простыми. Чем меньше, тем лучше.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-dont.png" alt-text="Рекомендация о том, как не перегружать пользователей слишком большим количеством действий на адаптивной карточке." border="false":::

#### <a name="dont-use-more-than-six-primary-actions"></a>Не рекомендуется: используйте более шести основных действий

Адаптивные карточки должны представлять быстрое интерактивное содержимое. Слишком много действий могут перегружать пользователя.

   :::column-end:::
:::row-end:::

### <a name="frequency"></a>Частота

:::image type="content" source="../../assets/images/adaptive-cards/frequency-do.png" alt-text="Рекомендация по частоте использования адаптивной карточки." border="false":::

#### <a name="do-be-concise"></a>Рекомендуется: будьте краткими

В беседу можно легко отправить несколько карточек, но после прокрутки и исчезновения карточек с экрана они становятся менее полезными. Попробуйте ограничиться основными моментами. Это особенно актуально в каналах, где пользователи более склонны воспринимать элементы как ненужный "шум".

## <a name="see-also"></a>См. также

* [Карточки и модули задач](~/task-modules-and-cards/cards-and-task-modules.md)
* [Карточки и модули задач, поддерживаемые в боте Teams](~/task-modules-and-cards/what-are-task-modules.md)
* [Работа с универсальными действиями для адаптивных карточек](~/task-modules-and-cards/cards/universal-actions-for-adaptive-cards/work-with-universal-actions-for-adaptive-cards.md)
* [Ответ на действие отправки модуля задач](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)
* [Пользовательские просмотры](~/task-modules-and-cards/cards/universal-actions-for-adaptive-cards/user-specific-views.md)
