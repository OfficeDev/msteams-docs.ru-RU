---
title: Справочник по карточкам
description: Описание всех карточек и действий карточек, доступных ботам в Teams
keywords: bots cards reference
ms.openlocfilehash: 22a4faa932173387cbefe900e30106d063c49e50
ms.sourcegitcommit: 5739245903278d521ec920427248b6b48676e637
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/07/2021
ms.locfileid: "49778396"
---
# <a name="cards-reference"></a>Справочник по карточкам

Карточки, перечисленные в этом разделе, поддерживаются в ботах для Teams. Они основаны на карточках, определенных в Bot Framework, но Teams не поддерживает все карточки Bot Framework и добавил некоторые из них. Различия вызваны в ссылках ниже.

## <a name="card-examples"></a>Примеры карт

Дополнительные сведения об использовании карточек можно найти в документации для SDK построитель ботов (v3). Кроме того, примеры кода доступны в репозитории Microsoft/BotBuilder-Samples на GitHub.

* .NET
  * [Добавление карточек в виде вложений в сообщения](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments)
  * [Пример кода карточек (построитель ботов 3)](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/CSharp/cards-RichCards)
* Node.js
  * [Добавление карточек в виде вложений в сообщения](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)
  * [Пример кода карточек (построитель ботов 3)](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/Node/cards-RichCards)

## <a name="types-of-cards"></a>Типы карточек

В этой таблице показаны типы доступных карточек.

| Тип карточки | Описание |
| --- | --- |
| [Адаптивная карточка](#adaptive-card) | Карточка с высокой настройкой, которая может содержать любое сочетание текста, речи, изображений, кнопок и полей ввода. |
| [Hero Card](#hero-card) | Обычно содержит одно большое изображение, одну или несколько кнопок и небольшой объем текста. |
| [Карточка списка](#list-card) | Список прокрутки элементов. |
| [Карточка соединители Office 365](#office-365-connector-card) | Гибкий макет с несколькими разделами, полями, изображениями и действиями. |
| [Чековая карта](#receipt-card) | Предоставляет пользователю квитанцию. |
| [Карточка для подписи](#signin-card) | Позволяет боту запрашивать вход пользователя. |
| [Thumbnail Card](#thumbnail-card) | Обычно содержит один эскиз, короткий текст и одну или несколько кнопок. |
| [Коллекции карт](#card-collections) | Используется для возврата нескольких элементов в одном ответе |

## <a name="common-properties-for-all-cards"></a>Общие свойства для всех карточек

### <a name="inline-card-images"></a>Inline card images

Карточка может содержать в себе изображение, включив ссылку на общедоступный образ. В целях производительности мы настоятельно рекомендуем вам проводить образ в общедоступных сетях доставки содержимого (CDN).

Изображения масштабются вверх или вниз по размеру, сохраняя пропорции для покрытия области изображения, а затем обрезаются от центра, чтобы добиться соответствующего пропорций карточки.

Изображения должны иметь не более 1024×1024 в формате PNG, JPEG или GIF; анимированное GIF официально не поддерживается.

| Свойство | Тип  | Описание |
| --- | --- | --- |
| url | URL-адрес | URL-адрес ИЗОБРАЖЕНИЯ ПО HTTPS |
| alt | String | Доступное описание изображения |

### <a name="buttons"></a>Кнопки

Кнопки показаны в нижней части карточки. Текст кнопки всегда находится в одной строке и будет усечен, если текст превышает ширину кнопки. Дополнительные кнопки, которые выходят за пределы максимального числа, поддерживаемого картой, не будут показаны.

Дополнительные [сведения см.](~/task-modules-and-cards/cards/cards-actions.md) в действиях карточки.

### <a name="card-formatting"></a>Форматирование карт

Дополнительные [сведения о форматирование](~/task-modules-and-cards/cards/cards-format.md) текста в карточках см. в документе "Форматирование карточек".

## <a name="adaptive-card"></a>Адаптивная карточка

Настраиваемая карточка, которая может содержать любое сочетание текста, речи, изображений, кнопок и полей ввода. *См.* ["Адаптивные карточки" 1.2.0.](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0)

### <a name="support-for-adaptive-cards"></a>Поддержка адаптивных карточек

| Боты в Teams | Расширения для сообщений  | Соединители | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |
|

> [!NOTE]
> * Платформа Teams поддерживает функции адаптивной карточки 1.2 или более ранней.
> * Элементы мультимедиа в настоящее время не поддерживаются в адаптивной карточке 1.2 на платформе Teams.
### <a name="example-adaptive-card"></a>Пример адаптивной карточки

![Пример адаптивной карточки](~/assets/images/cards/adaptivecard.png)

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

#### <a name="for-more-information-on-adaptive-cards"></a>Дополнительные сведения об адаптивных карточках

* [Обзор адаптивных карточек](/adaptive-cards/)
* [Действия адаптивной карточки в Teams](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)

## <a name="hero-card"></a>Карточка "Главного"

Карточка, которая обычно содержит одно большое изображение, одну или несколько кнопок и текста.

### <a name="support-for-hero-cards"></a>Поддержка карточек "Главного"

| Боты в Teams | Расширения для сообщений  | Соединители | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |
|

### <a name="properties-of-a-hero-card"></a>Свойства карточки "Hero"

| Свойство | Тип  | Описание |
| --- | --- | --- |
| title | Форматированный текст  | Название карточки. Не более 2 строк. |
| subtitle | Форматированный текст  | Субтитры на карточке. Не более 2 строк.|
| текст | Форматированный текст  | Текст отображается сразу под субтитром; См. [параметры форматирования](~/task-modules-and-cards/cards/cards-format.md) карточки |
| images | Массив изображений | Изображение, отображаемого в верхней части карточки. Пропорции 16:9 |
| buttons | Массив объектов действий | Набор действий, применимых к текущей карточке. Максимум 6 |
| tap | Объект Action | Это действие будет активировано, когда пользователь коснитесь самой карточки |
|

### <a name="example-hero-card"></a>Пример карточки "Образец"

![Пример главного карточки](~/assets/images/cards/hero.png)

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

### <a name="for-more-information-on-hero-cards"></a>Дополнительные сведения о картах Hero

Справка по Bot Framework:

* [Узел главного карточки](https://docs.microsoft.com/javascript/api/botframework-schema/herocard)
* [Главный карточка C #](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.herocard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="list-card"></a>Карточка списка

Карточка списка была добавлена в Teams для предоставления функций, которые выходят за рамки того, что может предоставить коллекция списков. На карточке списка содержится прокручивающийся список элементов.

### <a name="support-for-list-cards"></a>Поддержка карточек списков

| Боты в Teams | Расширения для сообщений  | Соединители | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ |✔ |
|

### <a name="properties-of-a-list-card"></a>Свойства карточки списка

| Свойство | Тип  | Описание |
| --- | --- | --- |
| title | Форматированный текст  | Название карточки. Не более 2 строк.|
| items | Массив элементов списка  ||
| buttons | Массив объектов действий | Набор действий, применимых к текущей карточке. Максимум 6. |

### <a name="example-list-card"></a>Пример карточки списка

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

## <a name="office-365-connector-card"></a>Карточка соединители Office 365

Поддерживается в Teams, а не в Bot Framework.

Карточка соединители Office 365 предоставляет гибкий макет с несколькими разделами, полями, изображениями и действиями. Эта карточка инкапсулирует карточку соединителя, чтобы ее могли использовать боты. Различия между карточками соединители и картой O365 см. в разделе примечаний.

### <a name="support-for-office-365-connector-cards"></a>Поддержка карточек соединители Office 365

| Боты в Teams | Расширения для сообщений  | Соединители | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✔ | ✖ |
|

### <a name="properties-of-the-office-365-connector-card"></a>Свойства карточки соединители Office 365

| Свойство | Тип  | Описание |
| --- | --- | --- |
| title | Форматированный текст  | Название карточки. Не более 2 строк. |
| summary | Форматированный текст  | Сводка карточки. Не более 2 строк. |
| текст | Форматированный текст  | Текст отображается сразу под субтитром; См. [параметры форматирования](~/task-modules-and-cards/cards/cards-format.md) карточки |
| themeColor | Строка HEX | цвет, который переопределит accentColor, предоставленный из манифеста приложения |

### <a name="notes-on-the-office-365-connector-card"></a>Примечания на карточке соединители Office 365

Карточки соединители Office 365 правильно работают в Microsoft Teams, включая [действия ActionCard.](/outlook/actionable-messages/card-reference#actioncard-action)

Одно из важных отличий между использованием карточек соединители из соединители и карточек соединители в боте обработка действий карт.

* Для соединители конечная точка получает полезной нагрузки карточки через HTTP POST.
* Для бота действие запускает действие, которое отправляет боту только ИД и `HttpPOST` `invoke` тело действия.

Каждая карточка соединители может отображать не более 10 разделов, а каждый раздел может содержать не более 5 изображений и 5 действий.

> [!NOTE]
> Дополнительные разделы, изображения или действия в сообщении не отображаются.

Все текстовые поля поддерживают Markdown и HTML. Вы можете управлять тем, в каких разделах используется Markdown или HTML, установив `markdown` свойство в сообщении. По умолчанию установлено значение ; если вы хотите использовать `markdown` `true` HTML, установите `markdown` значение `false` .

Если указать `themeColor` свойство, оно переопределит `accentColor` свойство в манифесте приложения.

Чтобы указать стиль отрисовки, `activityImage` можно задать его следующим `activityImageType` образом.

| Значение | Описание |
| --- | --- |
| `avatar` | По умолчанию; `activityImage` будет обрезана в круге |
| `article` | `activityImage` будет отображаться как прямоугольник с сохранением пропорций |

Все остальные сведения о свойствах карточки соединители см. в справочнике по карточкам [сообщений с действиями.](/outlook/actionable-messages/card-reference) Единственными свойствами карточки соединитела, которые в настоящее время не поддерживаются Microsoft Teams, являются:

* `heroImage`
* `hideOriginalBody`
* `startGroup` (всегда рассматривается как `true` в Teams)
* `originator`
* `correlationId`

### <a name="example-office-365-connector-card"></a>Пример карточки соединители Office 365

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

## <a name="receipt-card"></a>Чековая карта

Поддерживается в Teams.

Карточка, которая позволяет боту предоставлять пользователю квитанцию. Обычно он содержит список элементов, которые необходимо включить в квитанцию, налог и общую информацию, а также другой текст.

### <a name="support-for-receipts-cards"></a>Поддержка карточек квитанций

| Боты в Teams | Расширения для сообщений  | Соединители | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |
|

### <a name="for-more-information-on-receipt-cards"></a>Дополнительные сведения о карточках квитанций

Справка по Bot Framework:

* [Узел карточки квитанции](https://docs.microsoft.com/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [Чековая карта C #](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.receiptcard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="signin-card"></a>Карточка для подписи

Карточка, которая позволяет боту запрашивать вход пользователя. Поддерживается в Teams в несколько другом формате, чем в Bot Framework. Карточка для регистрации в Teams похожа на карточку для регистрации в структуре бота, за исключением того, что карточка для регистрации в Teams поддерживает только два действия: `signin` и `openUrl` .

Действие *для регистрации можно* использовать с любой карточки в Teams, а не только с карточки для регистрации. Дополнительные сведения о проверке подлинности ботов см. в разделе "Поток проверки подлинности [Microsoft Teams".](~/bots/how-to/authentication/auth-flow-bot.md)

### <a name="support-for-signin-cards"></a>Поддержка карточек для регистрации

| Боты в Teams | Расширения для сообщений  | Соединители | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ | ✔ |
|

### <a name="for-more-information-on-signin-cards"></a>Дополнительные сведения о карточках для подписи

Справка по Bot Framework:

* [Узел карточки для подписи](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [Карточка для подписи C #](/dotnet/api/microsoft.bot.connector.signincard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="thumbnail-card"></a>Эскиз карточки

Карточка, которая обычно содержит один эскиз, одну или несколько кнопок и текст.

### <a name="support-for-thumbnail-cards"></a>Поддержка карточек эскизов

| Боты в Teams | Расширения для сообщений  | Соединители | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |
|

![Пример карточки эскиза](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a>Свойства карточки thumbnail

| Свойство | Тип  | Описание |
| --- | --- | --- |
| title | Форматированный текст  | Название карточки. Не более 2 строк.|
| subtitle | Форматированный текст  | Субтитры на карточке. Не более 2 строк.|
| текст | Форматированный текст  | Текст отображается сразу под субтитром; См. [параметры форматирования](~/task-modules-and-cards/cards/cards-format.md) карточки |
| images | Массив изображений | Изображение, отображаемого в верхней части карточки. Пропорции 1:1 (квадрат) |
| buttons | Массив объектов действий | Набор действий, применимых к текущей карточке. Максимум 6 |
| tap | Объект Action | Это действие будет активировано, когда пользователь коснитесь самой карточки |
|

### <a name="example-thumbnail-card"></a>Пример карточки thumbnail

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

### <a name="for-more-information"></a>Дополнительные сведения

Справка по Bot Framework:

* [Узел карты эскиза](https://docs.microsoft.com/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [Эскиз карточки C #](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.thumbnailcard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="card-collections"></a>Коллекции карт

Коллекции карт поддерживаются в Teams.

Коллекции карт: `builder.AttachmentLayout.carousel` и `builder.AttachmentLayout.list` . Эти коллекции содержат адаптивные карточки, карты hero или thumbnail.

## <a name="carousel-collection"></a>Коллекция карусели

На [макете карусели](/azure/bot-service/dotnet/bot-builder-dotnet-add-rich-card-attachments?view=azure-bot-service-3.0&preserve-view=true) показана карусели карт, при желании с кнопками связанных действий.

### <a name="support-for-carousel-collections"></a>Поддержка коллекций карусели

| Боты в Teams | Расширения для сообщений  | Соединители | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ | ✔ |
|

> [!NOTE]
> Карусель может отображать не более 10 карт на сообщение.

### <a name="properties-of-a-carousel-card"></a>Свойства карточки карусели

Свойства карточки карусели такие же, как и у карт главного и эскиза.

### <a name="example-carousel-collection"></a>Пример коллекции Carousel

![Пример карусели карточек](~/assets/images/cards/carousel.png)

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

### <a name="syntax-for-carousel-collections"></a>Синтаксис для коллекций карусели

`builder.AttachmentLayoutTypes.Carousel`

## <a name="list-collection"></a>Коллекция List

### <a name="support-for-list-collections"></a>Поддержка коллекций списков

Макет списка отображает список карт с вертикальным расположением, при желании с связанными кнопками действий.

| Боты в Teams | Расширения для сообщений  | Соединители | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |
|

### <a name="example-list-collection"></a>Пример коллекции List

![Пример списка карточек](~/assets/images/cards/list.png)

Свойства такие же, как для главного или эскиза карточки.

В списке может отображаться не более 10 карт на сообщение.

> [!NOTE]
> Некоторые сочетания карточек списков пока не поддерживаются в iOS и Android.

### <a name="syntax-for-list-collections"></a>Синтаксис для коллекций списков

`builder.AttachmentLayout.list`

## <a name="cards-not-supported-in-teams"></a>Карточки не поддерживаются в Teams

Следующие карточки реализованы в Bot Framework, но НЕ поддерживаются Teams.

* Карты анимации
* Аудиокарты
* Видеокарты
