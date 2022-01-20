---
title: Типы карточек
description: Описание всех карточек и действий карточек, доступных ботам в Teams
ms.localizationpriority: high
keywords: справочные материалы о карточках для ботов
ms.topic: reference
ms.openlocfilehash: 741bd83b6888527e8e89b5be51dd408bb802fad3
ms.sourcegitcommit: c65a868744e4108b5d786de2350981e3f1f05718
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/19/2022
ms.locfileid: "62081137"
---
# <a name="types-of-cards"></a>Типы карточек

В ботах для Microsoft Teams поддерживаются следующие карточки и коллекции карточек: адаптивные, главный имиджевый баннер, список, соединитель Office 365, квитанция, вход и эскиз. Они основаны на карточках, определенных в Bot Framework, но Teams не поддерживает все карточки из Bot Framework и для него добавлены собственные.

Прежде чем определять различные типы карточек, необходимо понять, как создать карточку главного имиджевого баннера, эскиза или адаптивную карточку.

## <a name="create-a-hero-card-thumbnail-card-or-adaptive-card"></a>Создание карточки главного имиджевого баннера, эскиза или адаптивной карточки

**Создание карточки главного имиджевого баннера, карточки эскиза или адаптивной карточки в App Studio**

1. Перейдите в **App Studio** из Teams.
1. Выберите **Редактор карточек**.
1. Выберите **Создать новую карточку**.
1. Выберите **Создать** для элемента **Карточка главного имиджевого баннера**, **Карточка эскиза** или **Адаптивная карточка**. Для этой карточки показаны сведения о метаданных, кнопках и json, csharp и примеры кода node.

    ![Сведения о карточке главного имиджевого баннера](~/assets/images/Cards/Herocarddetails.png)

1. Выберите **Отправить мне эту карточку**. Карточка отправляется вам в виде сообщения чата.

## <a name="card-examples"></a>Примеры карточек

Дополнительные сведения об использовании карточек можно найти в документации для пакета SDK Bot Builder v3. Примеры кода также доступны в репозитории **Microsoft/BotBuilder-Samples** на GitHub. Ниже приводятся несколько примеров карточек.

* .NET
  * [Добавление карточек в виде вложений в сообщения](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true).
  * [Пример кода карточек в Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards).

* Node.js
  * [Добавление карточек в виде вложений в сообщения](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true).
  * [Пример кода карточек в Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards).

## <a name="card-types"></a>Типы карточек

Вам доступны различные типы карточек в зависимости от требований приложения. В следующей таблице показаны типы доступных карточек:

| Тип карточки | Описание |
| --- | --- |
| [Адаптивная карточка](#adaptive-card) | Эту карточку можно настроить и в нее можно добавить любую комбинацию текста, речи, изображений, кнопок и полей ввода. |
| [Карточка главного имиджевого баннера](#hero-card) | Эта карточка обычно содержит одно крупное изображение, одну или несколько кнопок и небольшой объем текста. |
| [Карточка списка](#list-card) | Эта карточка содержит прокручивающийся список элементов. |
| [Карточка соединителя Office 365](#office-365-connector-card) | Эта карточка имеет гибкий макет с несколькими разделами, полями, изображениями и действиями. |
| [Карточка квитанции](#receipt-card) | Эта карточка предоставляет пользователю квитанцию. |
| [Карточка входа](#signin-card) | Эта карточка позволяет боту запрашивать у пользователя вход в систему. |
| [Карточка эскиза](#thumbnail-card) | Эта карточка обычно содержит один эскиз, короткий текст и одну или несколько кнопок. |
| [Коллекции карточек](#card-collections) | Эта коллекция карточек используется для возврата нескольких элементов в одном ответе. |

## <a name="features-that-support-different-card-types"></a>Функции, которые поддерживают разные типы карточек

| Тип карточки | Боты | Предварительные просмотры расширений сообщений | Результаты расширения сообщения | Модули задач | Исходящие веб-перехватчики | Входящие веб-перехватчики | Соединители Office 365 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Адаптивная карточка | ✔ | ✖ | ✔ | ✔ | ✔ | ✔ | ✖ |
| Карточка соединителя Office 365 | ✔ | ✖ | ✔ | ✖ | ✔ | ✔ | ✔ |
| Карточка главного имиджевого баннера | ✔ | ✔ | ✔ | ✖ | ✔ | ✔ | ✖ |
| Карточка эскиза | ✔ | ✔ | ✔ | ✖ | ✔ | ✔ | ✖ |
| Карточка списка | ✔ | ✖ | ✖ | ✖ | ✔ | ✔ | ✖ |
| Карточка квитанции | ✔ | ✖ | ✖ | ✖ | ✖ | ✔ | ✖ |
| Карточка входа | ✔ | ✖ | ✖ | ✖ | ✖ | ✖ | ✖ |

> [!NOTE]
> Для адаптивных карточек во входящих веб-перехватчиках полностью поддерживаются все встроенные элементы схемы адаптивных карточек, кроме `Action.Submit`. Поддерживаемые действия: [**Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html), [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html), [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html) и [**Action.Execute**](/adaptive-cards/authoring-cards/universal-action-model#actionexecute).

## <a name="common-properties-for-all-cards"></a>Общие свойства для всех карточек

Просмотрите общие свойства, применимые для всех карточек.

> [!NOTE]
> Карточки главного имиджевого баннера и эскиза с несколькими действиями автоматически разбиваются на несколько карточек в макете с каруселью.

### <a name="inline-card-images"></a>Встроенные изображения в карточках

Карточка может содержать в себе изображение за счет добавления ссылки на общедоступное изображение. В целях повышения производительности, настоятельно рекомендуется размещать изображение в общедоступных сетях доставки содержимого (CDN).

Изображения масштабируются по размеру, чтобы сохранить пропорции для покрытия области изображения. Затем изображения вырезаются из центра, чтобы получить подходящие пропорции для карточки.

Изображения должны иметь разрешение не более 1024x1024 и иметь формат PNG, JPEG или GIF. GIF с анимацией не поддерживаются.

Следующая таблица содержит свойства встроенных изображений в карточках:

| Свойство | Тип  | Описание |
| --- | --- | --- |
| url | URL-адрес | URL-адрес изображения с HTTPS. |
| alt | Строка | Понятное описание изображения. |

> [!NOTE]
> Если карточка содержит URL-адрес изображения, который перенаправляет перед окончательным изображением, перенаправление в URL-адресе изображения не поддерживается. Это правдиво для изображений, размещенных для общего доступа в публичном облаке.

### <a name="buttons"></a>Кнопки

Кнопки показаны в столбик в нижней части карточки. Текст кнопок всегда находится в одной строке и усекается, если длина текста превышает ширину кнопки. Дополнительные кнопки, кроме максимального числа, поддерживаемого картой, не отображаются.

Дополнительные сведения см. в разделе о [действиях с карточками](~/task-modules-and-cards/cards/cards-actions.md).

### <a name="card-formatting"></a>Форматирование карточек

Дополнительные сведения о формате текста в карточках см. в разделе о [форматировании карточек](~/task-modules-and-cards/cards/cards-format.md).

После рассмотрения общих свойств всех карточек вы можете начать работать с адаптивными карточками, которые помогают повысить вовлеченность и эффективность, добавляя содержимое с действиями непосредственно в приложения, которые вы используете.

## <a name="adaptive-card"></a>Адаптивная карточка

Адаптивная карточка — это настраиваемая карточка, которая может содержать любое сочетание текста, речи, изображений, кнопок и полей ввода. Дополнительные сведения см. в разделе [Адаптивные карточки](https://github.com/microsoft/AdaptiveCards/releases/tag/2020.07).

### <a name="support-for-adaptive-cards"></a>Поддержка адаптивных карточек

В следующей таблице представлены функции, поддерживающие адаптивные карточки.

| Боты в Teams | Расширения для система обмена сообщениями  | Connectors | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |

> [!NOTE]
> * Платформа Teams поддерживает функции адаптивных карточек версии 1.4 или более ранних версий, если они отправляются ботами или используются в расширениях для сообщений с действиями.
> * Платформа Teams поддерживает возможности адаптивных карточек версии 1.3 или более ранних версий для остальных возможностей, таких как карточки, отправленные пользователем (расширения для обмена сообщениями на основе поиска и развертывание ссылок), вкладки и модули задач.
> * Стиль положительных или деструктивных действий в адаптивных карточках на платформе Teams не поддерживается.
> * Элементы мультимедиа в настоящее время не поддерживаются в адаптивных карточках на платформе Teams.

### <a name="example-of-adaptive-card"></a>Пример адаптивной карточки

![Пример адаптивной карточки](~/assets/images/cards/adaptivecard.png)

Ниже представлен пример кода адаптивной карточки.

```json
{
  "contentType": "application/vnd.microsoft.card.adaptive",
  "content": {
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "type": "AdaptiveCard",
    "version": "1.0",
    "body": [
      {
        "type": "Container",
        "items": [
          {
            "type": "TextBlock",
            "text": "Publish Adaptive Card schema",
            "weight": "bolder",
            "size": "medium"
          },
          {
            "type": "ColumnSet",
            "columns": [
              {
                "type": "Column",
                "width": "auto",
                "items": [
                  {
                    "type": "Image",
                    "url": "https://pbs.twimg.com/profile_images/3647943215/d7f12830b3c17a5a9e4afcc370e3a37e_400x400.jpeg",
                    "size": "small",
                    "style": "person"
                  }
                ]
              },
              {
                "type": "Column",
                "width": "stretch",
                "items": [
                  {
                    "type": "TextBlock",
                    "text": "Matt Hidinger",
                    "weight": "bolder",
                    "wrap": true
                  },
                  {
                    "type": "TextBlock",
                    "spacing": "none",
                    "text": "Created {{DATE(2017-02-14T06:08:39Z, SHORT)}}",
                    "isSubtle": true,
                    "wrap": true
                  }
                ]
              }
            ]
          }
        ]
      },
      {
        "type": "Container",
        "items": [
          {
            "type": "TextBlock",
            "text": "Now that we have defined the main rules and features of the format, we need to produce a schema and publish it to GitHub. The schema will be the starting point of our reference documentation.",
            "wrap": true
          },
          {
            "type": "FactSet",
            "facts": [
              {
                "title": "Board:",
                "value": "Adaptive Card"
              },
              {
                "title": "List:",
                "value": "Backlog"
              },
              {
                "title": "Assigned to:",
                "value": "Matt Hidinger"
              },
              {
                "title": "Due date:",
                "value": "Not set"
              }
            ]
          }
        ]
      }
    ],
    "actions": [
      {
        "type": "Action.ShowCard",
        "title": "Set due date",
        "card": {
          "type": "AdaptiveCard",
          "body": [
            {
              "type": "Input.Date",
              "id": "dueDate"
            }
          ],
          "actions": [
            {
              "type": "Action.Submit",
              "title": "OK"
            }
          ]
        }
      },
      {
        "type": "Action.ShowCard",
        "title": "Comment",
        "card": {
          "type": "AdaptiveCard",
          "body": [
            {
              "type": "Input.Text",
              "id": "comment",
              "isMultiline": true,
              "placeholder": "Enter your comment"
            }
          ],
          "actions": [
            {
              "type": "Action.Submit",
              "title": "OK"
            }
          ]
        }
      }
    ]
  }  
}
```

#### <a name="additional-information-on-adaptive-cards"></a>Дополнительные сведения об адаптивных карточках

Справочник по Bot Framework:

* [Узел адаптивных карточек](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)
* [Адаптивная карточка C#](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)

Теперь вы можете работать с карточкой главного имиджевого баннера, многоцелевой карточкой для визуального выделения возможного выбора пользователя.

## <a name="hero-card"></a>Карточка главного имиджевого баннера

Эта карточка обычно содержит одно крупное изображение, одну или несколько кнопок и текст.

### <a name="support-for-hero-cards"></a>Поддержка карточек главного имиджевого баннера

В следующей таблице представлены функции, поддерживающие карточки главного имиджевого баннера.

| Боты в Teams | Расширения для система обмена сообщениями  | Connectors | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |

### <a name="properties-of-a-hero-card"></a>Свойства карточки главного имиджевого баннера

Следующая таблица содержит свойства карточки главного имиджевого баннера.

| Свойство | Тип  | Описание |
| --- | --- | --- |
| title | Форматированный текст  | Заголовок карточки. Не более двух строк. |
| подзаголовок | Форматированный текст  | Подзаголовок карточки. Не более двух строк.|
| текст | Форматированный текст  | Текст отображается под подзаголовком. Параметры форматирования см. в разделе о [форматировании карточек](~/task-modules-and-cards/cards/cards-format.md). |
| изображения | Массив изображений | Изображение, отображаемое в верхней части карточки. Пропорции: 16:9. |
| кнопки | Массив объектов действий | Набор действий, применимых к текущей карточке. Не более шести. |
| прикосновение | Объект Action | Активируется, когда пользователь нажимает на карточку. |

### <a name="example-of-a-hero-card"></a>Пример карточки главного имиджевого баннера

![Пример карточки главного имиджевого баннера](~/assets/images/cards/hero.png)

Ниже представлен пример кода карточки главного имиджевого баннера.

```json
{
   "contentType": "application/vnd.microsoft.card.hero",
   "content": {
     "title": "Seattle Center Monorail",
     "subtitle": "Seattle Center Monorail",
     "text": "The Seattle Center Monorail is an elevated train line between Seattle Center (near the Space Needle) and downtown Seattle. It was built for the 1962 World's Fair. Its original two trains, completed in 1961, are still in service.",
     "images": [
       {
         "url":"https://upload.wikimedia.org/wikipedia/commons/thumb/4/49/Seattle_monorail01_2008-02-25.jpg/1024px-Seattle_monorail01_2008-02-25.jpg"
       }
     ],
    "buttons": [
      {
         "type": "openUrl",
         "title": "Official website",
         "value": "https://www.seattlemonorail.com"
       },
      {
        "type": "openUrl",
        "title": "Wikipeda page",
        "value": "https://en.wikipedia.org/wiki/Seattle_Center_Monorail"
       }
     ]
   }
}

```

### <a name="additional-information-on-hero-cards"></a>Дополнительные сведения о карточках главного имиджевого баннера

Справочник по Bot Framework:

* [Node.js карточки главного имиджевого баннера](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-a-hero-card&preserve-view=true)
* [C# карточки главного имиджевого баннера](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-hero-card&preserve-view=true)

## <a name="list-card"></a>Карточка списка

Карточка списка была добавлена в Teams для предоставления функций, которых нет в коллекции списков. Карточка списка содержит прокручивающийся список элементов.

### <a name="support-for-list-cards"></a>Поддержка карточек списков

В следующей таблице представлены функции, поддерживающие карточки списков.

| Боты в Teams | Расширения для система обмена сообщениями  | Connectors | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ |✔ |

### <a name="properties-of-a-list-card"></a>Свойства карточки списка

Следующая таблица содержит свойства карточки списка.

| Свойство | Тип  | Описание |
| --- | --- | --- |
| title | Форматированный текст  | Заголовок карточки. Не более 2 строк.|
| items | Массив элементов списка | Набор элементов, применимых к карточке.|
| кнопки | Массив объектов действий | Набор действий, применимых к текущей карточке. Не более 6. |

### <a name="example-of-a-list-card"></a>Пример карточки списка

Ниже представлен пример кода карточки списка.

```json
{
  "contentType": "application/vnd.microsoft.teams.card.list",
  "content": {
    "title": "Card title",
    "items": [
      {
        "type": "file",
        "id": "https://contoso.sharepoint.com/teams/new/Shared%20Documents/Report.xlsx",
        "title": "Report",
        "subtitle": "teams > new > design",
        "tap": {
          "type": "imBack",
          "value": "editOnline https://contoso.sharepoint.com/teams/new/Shared%20Documents/Report.xlsx"
        }
      },
      {
        "type": "resultItem",
        "icon": "https://cdn2.iconfinder.com/data/icons/social-icons-33/128/Trello-128.png",
        "title": "Trello title",
        "subtitle": "A Trello subtitle",
        "tap": {
          "type": "openUrl",
          "value": "http://trello.com"
        }
      },
      {
        "type": "section",
        "title": "Manager"
      },
      {
        "type": "person",
        "id": "JohnDoe@contoso.com",
        "title": "John Doe",
        "subtitle": "Manager",
        "tap": {
          "type": "imBack",
          "value": "whois JohnDoe@contoso.com"
        }
      }
    ],
    "buttons": [
      {
        "type": "imBack",
        "title": "Select",
        "value": "whois"
      }
    ]
  }
}
```

## <a name="office-365-connector-card"></a>Карточка соединителя Office 365

Вы можете работать с карточкой соединителя Office 365, которая предоставляет гибкий макет и отличный способ получения полезной информации. Карточка соединителя Office 365 поддерживается в Teams, но не в Bot Framework. Эта карточка предоставляет гибкий макет с несколькими разделами, полями, изображениями и действиями. Эта карточка содержит карточку соединителя, чтобы ее могли использовать боты. Различия между карточками соединителя и карточкой соединителя Office 365 см. в разделе [Дополнительные сведения о карточке соединителя Office 365](#additional-information-on-the-office-365-connector-card).

### <a name="support-for-office-365-connector-cards"></a>Поддержка карточек соединителя Office 365

В следующей таблице представлены функции, поддерживающие карточки соединители Office 365.

| Боты в Teams | Расширения для система обмена сообщениями  | Connectors | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✔ | ✖ |

### <a name="properties-of-the-office-365-connector-card"></a>Свойства карточки соединителя Office 365

В следующей таблице представлены свойства карточки соединители Office 365.

| Свойство | Тип  | Описание |
| --- | --- | --- |
| title | Форматированный текст  | Заголовок карточки. Не более двух строк. |
| summary | Форматированный текст  | Сводка карточки. Не более двух строк. |
| текст | Форматированный текст  | Текст отображается под подзаголовком. Параметры форматирования см. в разделе о [форматировании карточек](~/task-modules-and-cards/cards/cards-format.md). |
| themeColor | Строка шестнадцатиричных значений | Цвет, который переопределяет `accentColor` из манифеста приложения. |

### <a name="additional-information-on-the-office-365-connector-card"></a>Дополнительные сведения о карточке соединителя Office 365

Карточки соединителей Office 365 правильно работают в Microsoft Teams, включая [`ActionCard` действия](/outlook/actionable-messages/card-reference#actioncard-action).

Важное различие между использованием карточек соединителя из соединителя и использованием карточек соединителей в боте — обработка действий карточек. В следующей таблице перечислены эти различия.

| Connector | Bot |
| --- | --- |
| Конечная точка получает полезные данные карточки через HTTP POST. | Действие `HttpPOST` активирует действие `invoke`, которое отправляет боту только идентификатор и основную часть действия.|

Каждая карточка соединителя может отображать не более десяти разделов, а каждый раздел может содержать не больше пяти изображений и пяти действий.

> [!NOTE]
> Дополнительные разделы, изображения или действия в сообщении не отображаются.

Все текстовые поля поддерживают Markdown и HTML. Вы можете управлять тем, в каких разделах используется Markdown или HTML, задав свойство `markdown` в сообщении. По умолчанию `markdown` имеет значение `true`. Если вы хотите вместо этого использовать HTML, установите для `markdown` значение `false`.

Если указать свойство `themeColor`, это переопределит свойство `accentColor` в манифесте приложения.

Чтобы задать стиль отрисовки для `activityImage`, можно задать `activityImageType` как показано в следующей таблице.

| Значение | Описание |
| --- | --- |
| `avatar` | По умолчанию `activityImage` обрезается как круг. |
| `article` | `activityImage` отображается как прямоугольник и сохраняет пропорции. |

Все остальные сведения о действиях карточек соединителей представлены в разделе о [карточках сообщений с действиями](/outlook/actionable-messages/card-reference). В настоящее время Teams не поддерживает только следующие свойства карточки соединителя.

* `heroImage`
* `hideOriginalBody`
* В Teams `startGroup` всегда рассматриваются как `true`
* `originator`
* `correlationId`

### <a name="example-of-an-office-365-connector-card"></a>Пример карточки соединителя Office 365

Ниже представлен пример кода карточки соединителя Office 365.

```json
{
  "contentType": "application/vnd.microsoft.teams.card.o365connector",
  "content": {
    "@type": "MessageCard",
    "@context": "http://schema.org/extensions",
    "summary": "John Doe commented on Trello",
    "title": "Project Tango",
    "sections": [
        {
            "activityTitle": "John Doe commented",
            "activitySubtitle": "On Project Tango",
            "activityText": "\"Here are the designs\"",
            "activityImage": "http://connectorsdemo.azurewebsites.net/images/MSC12_Oscar_002.jpg"
        },
        {
            "title": "Details",
            "facts": [
                {
                    "name": "Labels",
                    "value": "Designs, redlines"
                },
                {
                    "name": "Due date",
                    "value": "Dec 7, 2016"
                },
                {
                    "name": "Attachments",
                    "value": "[final.jpg](http://connectorsdemo.azurewebsites.net/images/WIN14_Jan_04.jpg)"
                }
            ]
        },
        {
            "title": "Images",
            "images": [
                {
                    "image":"http://connectorsdemo.azurewebsites.net/images/MicrosoftSurface_024_Cafe_OH-06315_VS_R1c.jpg"
                },
                {
                    "image":"http://connectorsdemo.azurewebsites.net/images/WIN12_Scene_01.jpg"
                },
                {
                    "image":"http://connectorsdemo.azurewebsites.net/images/WIN12_Anthony_02.jpg"
                }
            ]
        }
    ],
    "potentialAction": [
        {
            "@context": "http://schema.org",
            "@type": "ViewAction",
            "name": "View in Trello",
            "target": [
                "https://trello.com/c/1101/"
            ]
        }
    ]
  }
}
```

## <a name="receipt-card"></a>Карточка квитанции

Teams поддерживает карточки квитанции. Это карточка, которая позволяет боту предоставлять пользователю квитанцию. Как правило, он содержит список элементов, которые необходимо включить в квитанцию, например налог и общую информацию.

### <a name="support-for-receipt-cards"></a>Поддержка карточек квитанций

В следующей таблице представлены функции, поддерживающие карточки квитанций.

| Боты в Teams | Расширения для система обмена сообщениями  | Connectors | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |

### <a name="example-of-a-receipt-card"></a>Пример карточки квитанции

![Пример карточки квитанции](~/assets/images/cards/receipt.png)

Ниже представлен пример кода карточки квитанции.

```json
{
  "contentType": "application/vnd.microsoft.card.receipt",
  "content": {
    "title": "John Doe",
    "facts": [
      {
        "key": "Order Number",
        "value": "1234"
      },
      {
        "key": "Payment Method",
        "value": "VISA 5555-****"
      }
    ],
    "items": [
      {
        "title": "Data Transfer",
        "image": {
          "url": "https://github.com/amido/azure-vector-icons/raw/master/renders/traffic-manager.png"
        },
        "price": "$ 38.45",
        "quantity": "368"
      },
      {
        "title": "App Service",
        "image": {
          "url": "https://github.com/amido/azure-vector-icons/raw/master/renders/cloud-service.png"
        },
        "price": "$ 45.00",
        "quantity": "720"
      }
    ],
    "total": "$ 90.95",
    "tax": "$ 7.50",
    "buttons": [
      {
        "type": "openUrl",
        "title": "More information",
        "image": "https://account.windowsazure.com/content/6.10.1.38-.8225.160809-1618/aux-pre/images/offer-icon-freetrial.png",
        "value": "https://azure.microsoft.com/en-us/pricing/"
      }
    ]
  }
}
```

### <a name="additional-information-on-receipt-cards"></a>Дополнительные сведения о карточках квитанций

Справочник по Bot Framework:

* [Node.js карточки квитанций](/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [C# карточки квитанций](/dotnet/api/microsoft.bot.schema.receiptcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="signin-card"></a>Карточка входа

Карточка входа в Teams похожа на карточку входа в Bot Framework, за исключением того, что карточка входа в Teams поддерживает только два действия `signin` и `openUrl`.

Действие входа можно использовать с помощью любой карточки в Teams, а не только карточки входа. Дополнительные сведения см. в статье [Поток проверки подлинности для ботов в Teams](~/bots/how-to/authentication/auth-flow-bot.md).

### <a name="support-for-signin-cards"></a>Поддержка карточек входа

В следующей таблице представлены функции, поддерживающие карточки входа.

| Боты в Teams | Расширения для система обмена сообщениями  | Connectors | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ | ✔ |

### <a name="additional-information-on-signin-cards"></a>Дополнительные сведения о карточках входа

Справочник по Bot Framework:

* [Node.js карточки входа](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [C# карточки входа](/dotnet/api/microsoft.bot.schema.signincard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="thumbnail-card"></a>Карточка эскиза

Вы можете работать с карточкой эскиза, которая используется для отправки простого сообщения с действиями. Такая карточка обычно содержит один эскиз, одну или несколько кнопок и текст.

### <a name="support-for-thumbnail-cards"></a>Поддержка карточек эскиза

В следующей таблице представлены функции, поддерживающие карточки эскиза.

| Боты в Teams | Расширения для система обмена сообщениями  | Connectors | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |

![Пример карточки эскиза](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a>Свойства карточки эскиза

Следующая таблица содержит свойства карточки эскиза.

| Свойство | Тип  | Описание |
| --- | --- | --- |
| title | Форматированный текст  | Заголовок карточки. Не более 2 строк.|
| подзаголовок | Форматированный текст  | Подзаголовок карточки. Не более 2 строк.|
| текст | Форматированный текст  | Текст отображается под подзаголовком. Параметры форматирования см. в разделе о [форматировании карточек](~/task-modules-and-cards/cards/cards-format.md). |
| изображения | Массив изображений | Изображение, отображаемое в верхней части карточки. Пропорции 1:1, квадрат. |
| кнопки | Массив объектов действий | Набор действий, применимых к текущей карточке. Не более 6. |
| прикосновение | Объект Action | Активируется, когда пользователь нажимает на карточку. |

### <a name="example-of-a-thumbnail-card"></a>Пример карточки эскиза

Ниже представлен пример кода карточки эскиза.

```json
{
  "contentType": "application/vnd.microsoft.card.thumbnail",
  "content": {
    "title": "Bender",
    "subtitle": "tale of a robot who dared to love",
    "text": "Bender Bending Rodríguez is a main character in the animated television series Futurama. He was created by series creators Matt Groening and David X. Cohen, and is voiced by John DiMaggio",
    "images": [
      {
        "url": "https://upload.wikimedia.org/wikipedia/en/a/a6/Bender_Rodriguez.png",
        "alt": "Bender Rodríguez"
      }
    ],
    "buttons": [
      {
        "type": "imBack",
        "title": "Thumbs Up",
        "image": "http://moopz.com/assets_c/2012/06/emoji-thumbs-up-150-thumb-autox125-140616.jpg",
        "value": "I like it"
      },
      {
        "type": "imBack",
        "title": "Thumbs Down",
        "image": "http://yourfaceisstupid.com/wp-content/uploads/2014/08/thumbs-down.png",
        "value": "I don't like it"
      },
      {
        "type": "openUrl",
        "title": "I feel lucky",
        "image": "http://thumb9.shutterstock.com/photos/thumb_large/683806/148441982.jpg",
        "value": "https://www.bing.com/images/search?q=bender&qpvt=bender&qpvt=bender&qpvt=bender&FORM=IGRE"
      }
    ],
    "tap": {
      "type": "imBack",
      "value": "Tapped it!"
    }
  }
}
```

### <a name="additional-information"></a>Дополнительные сведения

Справочник по Bot Framework:

* [Node.js карточки эскиза](/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [C# карточки эскиза](/dotnet/api/microsoft.bot.schema.thumbnailcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="card-collections"></a>Коллекции карточек

Вы можете работать с коллекциями карточек, которые включают карусели и коллекции списков. Teams поддерживает коллекции карточек. Коллекции карточек включают `builder.AttachmentLayout.carousel` и `builder.AttachmentLayout.list`. Эти коллекции содержат адаптивные карточки, карточки главного имиджевого баннера и карточки эскиза.

### <a name="carousel-collection"></a>Коллекция с каруселью

В [макете с каруселью](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) отображается карусель карточек с возможностью привязать кнопки действий.

#### <a name="support-for-carousel-collections"></a>Поддержка коллекций с каруселью

В следующей таблице представлены функции, поддерживающие коллекции с каруселью.

| Боты в Teams | Расширения для система обмена сообщениями  | Connectors | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ | ✔ |

> [!NOTE]
> Карусель может отображать не более десяти карточек на сообщение.

#### <a name="properties-of-a-carousel-card"></a>Свойства карточки с каруселью

Свойства карточки с каруселью такие же, как и у карточки главного имиджевого баннера и карточки эскиза.

#### <a name="example-of-a-carousel-collection"></a>Пример коллекции с каруселью

![Пример карусели карточек](~/assets/images/cards/carousel.png)

Ниже представлен пример кода коллекции с каруселью.

```json
{
 "attachmentLayout": "carousel",
 "attachments":[
    {
      "contentType": "application/vnd.microsoft.card.adaptive",
      "content": {
        "type": "AdaptiveCard",
        "version": "1.0",
        "body": [
          {
            "type": "Container",
            "items": [
              {
                "type": "TextBlock",
                "size": "extraLarge",
                "weight": "bolder",
                "text": "Welcome to Employee Connect",
                "height": "stretch"
              },
              {
                "type": "TextBlock",
                "size": "medium",
                "weight": "bolder",
                "text": "Add events to your calendar",
                "height": "stretch"
              },
              {
                "type": "TextBlock",
                "weight": "bolder",
                "text": "The bot can send \r\rnotification to remind \r\ryou about the latest \r\revents and trainings.",
                "wrap": true,
                "height": "stretch"
              },
              {
                "type": "ColumnSet",
                "columns": [
                  {
                    "type": "Column",
                    "items": [],
                    "height": "stretch"
                  }
                ]
              },
              {
                "type": "ColumnSet",
                "columns": [
                  {
                    "type": "Column",
                    "items": [],
                    "height": "stretch"
                  }
                ]
              }
            ]
          }
        ],
        "actions": [
          {
            "type": "Action.Submit",
            "title": "Let's get started"
          }
        ]
      }
    },
    {
      "contentType": "application/vnd.microsoft.card.adaptive",
      "content": {
        "type": "AdaptiveCard",
        "version": "1.2",
        "body": [
          {
            "type": "Container",
            "items": [
              {
                "type": "TextBlock",
                "size": "large",
                "weight": "bolder",
                "text": "Employee connect"
              },
              {
                "type": "TextBlock",
                "text": "The bot can send notifications \r\rto remind you about the latest \r\r events and trainings",
                "wrap": true,
                "maxWidth": 2
              },
              {
                "type": "ColumnSet",
                "columns": [
                  {
                    "type": "Column",
                    "items": [],
                    "height": "stretch"
                  }
                ]
              },
              {
                "type": "ColumnSet",
                "columns": [
                  {
                    "type": "Column",
                    "items": [],
                    "height": "stretch"
                  }
                ]
              }
            ]
          }
        ],
        "actions": [
          {
            "type": "Action.Submit",
            "title": "Let's get started"
          }
        ]
      }
    },
    {
      "contentType": "application/vnd.microsoft.card.adaptive",
      "content": {
        "type": "AdaptiveCard",
        "version": "1.0",
        "body": [
          {
            "type": "Container",
            "items": [
              {
                "type": "TextBlock",
                "size": "large",
                "weight": "bolder",
                "text": "Employee Connect final"
              },
              {
                "type": "TextBlock",
                "weight": "bolder",
                "text": "Create and manage your tasks",
                "wrap": true
              },
              {
                "type": "TextBlock",
                "text": "The app identifies all your pending tasks \r\r and helps you manage everything at \r\r one place.",
                "wrap": true
              },
              {
                "type": "TextBlock",
                "weight": "bolder",
                "text": "Try these commands \r\r- Pending Submissions \r\r- Pending Approvals- My Tools",
                "wrap": true,
                "height": "stretch"
              }
            ]
          }
        ],
        "actions": [
          {
            "type": "Action.Submit",
            "title": "Let's get started"
          }
        ]
      }
    }
  ]
}
```

#### <a name="syntax-for-carousel-collections"></a>Синтаксис коллекций с каруселью

`builder.AttachmentLayoutTypes.Carousel` — это синтаксис для коллекций с каруселью.

### <a name="list-collection"></a>Коллекция списков

В макете списка отображается вертикальный столбец со списком карточек с возможностью привязать кнопки действий.

#### <a name="support-for-list-collections"></a>Поддержка коллекций списков

В следующей таблице представлены функции, поддерживающие коллекции списков.

| Боты в Teams | Расширения для система обмена сообщениями  | Connectors | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |

#### <a name="example-of-a-list-collection"></a>Пример коллекции списков

![Пример списка карточек](~/assets/images/cards/list.png)

Свойства коллекций списков такие же, как и у карточек главного имиджевого баннера или карточек эскиза.

Список может отображать не более десяти карточек на сообщение.

> [!NOTE]
> Некоторые сочетания карточек списков пока не поддерживаются в iOS и Android.

#### <a name="syntax-for-list-collections"></a>Синтаксис для коллекций списков

`builder.AttachmentLayout.list` — это синтаксис для коллекций списков.

## <a name="cards-not-supported-in-teams"></a>Карточки, которые не поддерживаются в Teams

Следующие карточки реализованы в Bot Framework, но не поддерживаются в Teams.

* Карточки анимации
* Карточки с аудио
* Карточки с видео

## <a name="see-also"></a>См. также

* [Модули задач](~/task-modules-and-cards/what-are-task-modules.md)
* [Карточки формата](~/task-modules-and-cards/cards/cards-format.md)
* [Актуальные карточки](~/task-modules-and-cards/cards/universal-actions-for-adaptive-cards/up-to-date-views.md)
* [Работа с универсальными действиями для адаптивных карточек](~/task-modules-and-cards/cards/universal-actions-for-adaptive-cards/work-with-universal-actions-for-adaptive-cards.md)
* [Отзывы о завершении формы](~/bots/how-to/conversations/conversation-messages.md#form-completion-feedback)