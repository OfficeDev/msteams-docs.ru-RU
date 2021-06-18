---
title: Ссылки на карточки
description: Описывает все действия карт и карт, доступные ботам в Teams
localization_priority: Normal
keywords: ссылка на карточки ботов
ms.topic: reference
ms.openlocfilehash: 741980ea79dd23659dd2b8a240d767b8292ca251
ms.sourcegitcommit: 14409950307b135265c8582408be5277b35131dd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/17/2021
ms.locfileid: "52994387"
---
# <a name="cards-reference"></a>Ссылки на карточки

Карты, перечисленные в этом документе, поддерживаются в ботах для Microsoft Teams. Они основаны на картах, определенных bot Framework (BF), но Teams не поддерживает все карты Bot Framework и вместо этого были добавлены некоторые Teams карты. Различия называются в ссылках в этом документе.

## <a name="card-examples"></a>Примеры карт

Дополнительные сведения об использовании карт можно найти в документации для bot Builder SDK v3. Примеры кода также доступны в репозитории Microsoft/BotBuilder-Samples на GitHub.

* .NET
  * [Добавление карт в виде вложений в сообщения.](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)
  * [Карты пример кода Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards).

* Node.js
  * [Добавление карт в виде вложений в сообщения.](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)
  * [Карты пример кода Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards).

## <a name="types-of-cards"></a>Типы карт

В этой таблице показаны типы доступных вам карт:

| Тип карты | Описание |
| --- | --- |
| [Адаптивная карта](#adaptive-card) | Эта карта является высоко настраиваемой картой, которая может содержать любое сочетание текстов, речи, изображений, кнопок и полей ввода. |
| [Карта hero](#hero-card) | Эта карта обычно содержит одно большое изображение, одну или несколько кнопок и небольшое количество текста. |
| [Карта списка](#list-card) | Эта карта — это список элементов прокрутки. |
| [Office 365 соединители](#office-365-connector-card) | Эта карта имеет гибкий макет с несколькими разделами, полями, изображениями и действиями. |
| [Карта получения](#receipt-card) | Эта карта предоставляет квитанцию пользователю. |
| [Карточка Signin](#signin-card) | Эта карта позволяет боту запрашивать, чтобы пользователь войди. |
| [Карта эскиза](#thumbnail-card) | Эта карта обычно содержит одно изображение эскиза, короткий текст и одну или несколько кнопок. |
| [Коллекции карт](#card-collections) | Эти карты используются для возврата нескольких элементов в одном ответе. |

## <a name="common-properties-for-all-cards"></a>Общие свойства для всех карт

### <a name="inline-card-images"></a>Inline card images

Карта может содержать рядное изображение, включив ссылку на общедоступный образ. В целях производительности рекомендуется использовать изображение в общедоступных сетях доставки контента (CDN).

Изображения масштабироваться или по размеру при сохранении соотношения аспектов для покрытия области изображения. Затем изображения обрезаются из центра, чтобы достичь соответствующего соотношения аспектов для карты.

Изображения должны быть не более 1024×1024 в формате PNG, JPEG или GIF и не поддерживают анимированный GIF.

| Свойство | Тип  | Описание |
| --- | --- | --- |
| url | URL-адрес | URL-адрес HTTPS к изображению. |
| alt | String | Доступное описание изображения. |

> [!NOTE]
> Если карта содержит URL-адрес изображения, который проходит перенаправление перед окончательным изображением, перенаправление в URL-адрес изображения не поддерживается. Это происходит для изображений, общих в общедоступных облаках.

### <a name="buttons"></a>Кнопки

Кнопки показаны в нижней части карты. Текст кнопки всегда находится в одной строке и усечен, если текст превышает ширину кнопки. Никаких дополнительных кнопок, помимо максимального числа, поддерживаемого картой, не отображается.

Дополнительные сведения см. в [карточных действиях.](~/task-modules-and-cards/cards/cards-actions.md)

### <a name="card-formatting"></a>Форматирование карт

Дополнительные сведения о форматирования текста в картах см. [в документе форматирование карт.](~/task-modules-and-cards/cards/cards-format.md)

## <a name="adaptive-card"></a>Адаптивная карта

Адаптивная карта — это настраиваемая карта, которая может содержать любое сочетание текстовых, речевого, изображений, кнопок и полей ввода. Дополнительные сведения см. в [рублях адаптивных карт v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).

### <a name="support-for-adaptive-cards"></a>Поддержка адаптивных карт

| Боты в Teams | Расширения для система обмена сообщениями  | Соединители | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |

> [!NOTE]
> * Teams поддерживает v1.2 или более ранние функции адаптивной карты.
> * Положительный или разрушительный стиль действий не поддерживается в адаптивных картах на Teams платформе.
> * Элементы мультимедиа в настоящее время не поддерживаются в адаптивных картах на Teams платформе.

### <a name="example-of-an-adaptive-card"></a>Пример адаптивной карты

![Пример адаптивной карты](~/assets/images/cards/adaptivecard.png)

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

#### <a name="additional-information-on-adaptive-cards"></a>Дополнительные сведения о адаптивных картах

Ссылка на Bot Framework:

* [Адаптивные Node.js](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)
* [Адаптивная карта C #](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)

## <a name="hero-card"></a>Карта hero

Карта, которая обычно содержит одно большое изображение, одну или несколько кнопок и текст.

### <a name="support-for-hero-cards"></a>Поддержка карт-героев

| Боты в Teams | Расширения для система обмена сообщениями  | Соединители | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |

### <a name="properties-of-a-hero-card"></a>Свойства карты-героя

| Свойство | Тип  | Описание |
| --- | --- | --- |
| title | Форматированный текст  | Название карты. Максимум 2 строки. |
| субтитры | Форматированный текст  | Субтитр карты. Максимум 2 строки.|
| текст | Форматированный текст  | Текст отображается под субтитром. Параметры форматирования см. [в виде форматирования карт.](~/task-modules-and-cards/cards/cards-format.md) |
| изображения | Массив изображений | Изображение, отображаемого в верхней части карты. Соотношение аспектов 16:9. |
| кнопки | Массив объектов действий | Набор действий, применимых к текущей карте. Максимум 6. |
| нажмите кнопку | Объект Action | Активируется при нажатии на карточку самого пользователя. |

### <a name="example-of-a-hero-card"></a>Пример карточки героя

![Пример карточки героя](~/assets/images/cards/hero.png)

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

### <a name="additional-information-on-hero-cards"></a>Дополнительные сведения о картах-героях

Ссылка на Bot Framework:

* [Карточка героя Node.js](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-a-hero-card&preserve-view=true)
* [Карта героя C #](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-hero-card&preserve-view=true)

## <a name="list-card"></a>Карта списка

Карта списка была добавлена Teams для предоставления функций, которые не могут предоставляться в коллекции списков. Карта списка содержит список элементов для прокрутки.

### <a name="support-for-list-cards"></a>Поддержка карт списка

| Боты в Teams | Расширения для система обмена сообщениями  | Соединители | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ |✔ |

### <a name="properties-of-a-list-card"></a>Свойства карты списка

| Свойство | Тип  | Описание |
| --- | --- | --- |
| title | Форматированный текст  | Название карты. Максимум 2 строки.|
| элементы | Массив элементов списка ||
| кнопки | Массив объектов действий | Набор действий, применимых к текущей карте. Максимум 6. |

### <a name="example-of-a-list-card"></a>Пример карты списка

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

## <a name="office-365-connector-card"></a>Office 365 соединители

Соедините Office 365 поддерживается в Teams, а не в Bot Framework. Эта карта обеспечивает гибкую схему с несколькими разделами, полями, изображениями и действиями. Эта карта инкапсулирует соединителем карту, чтобы она была использована ботами. О различиях между соединитеными картами и картой O365 см. в заметках на [Office 365 соединители.](#notes-on-the-office-365-connector-card)

### <a name="support-for-office-365-connector-cards"></a>Поддержка Office 365 соединители

| Боты в Teams | Расширения для система обмена сообщениями  | Соединители | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✔ | ✖ |

### <a name="properties-of-the-office-365-connector-card"></a>Свойства карты Office 365 соединители

| Свойство | Тип  | Описание |
| --- | --- | --- |
| title | Форматированный текст  | Название карты. Максимум 2 строки. |
| summary | Форматированный текст  | Сводка карты. Максимум 2 строки. |
| текст | Форматированный текст  | Текст отображается под субтитром. Параметры форматирования см. [в виде форматирования карт.](~/task-modules-and-cards/cards/cards-format.md) |
| themeColor | Строка HEX | Цвет, который переопределяет accentColor, предоставленный из манифеста приложения. |

### <a name="notes-on-the-office-365-connector-card"></a>Заметки на Office 365 соединители

Office 365 соединители карточки работают правильно в Microsoft Teams, включая [действия ActionCard](/outlook/actionable-messages/card-reference#actioncard-action).

Одним из важных отличий между использованием соединитеных карт из соединитетеля и использованием соединитеных карт в боте является обработка действий карт.

* Для соединитетеля конечная точка получает полезное сообщение карточки через HTTP POST.
* Для бота действие запускает действие, которое отправляет боту только ID действия и `HttpPOST` `invoke` тело.

Каждая соединитечная карта может отображать не более десяти разделов, а каждый раздел может содержать не более пяти изображений и пять действий.

> [!NOTE]
> Дополнительные разделы, изображения или действия в сообщении не отображаются.

Все текстовые поля поддерживают разметку и HTML. Вы можете контролировать, в каких разделах используется разметка или HTML, установив `markdown` свойство в сообщении. По умолчанию `markdown` установлено `true` значение . Если вы хотите использовать HTML вместо этого, установите `markdown` `false` .

Если указать `themeColor` свойство, оно переопределит `accentColor` свойство в манифесте приложения.

Чтобы указать стиль `activityImage` визуализации, можно задать `activityImageType` следующим образом:

| Значение | Описание |
| --- | --- |
| `avatar` | По умолчанию; `activityImage` обрезается как круг. |
| `article` | `activityImage` отображается в качестве прямоугольника и сохраняет отношение аспектов. |

Другие сведения о свойствах карт соединители см. в справке к карточкам [сообщений.](/outlook/actionable-messages/card-reference) Единственными свойствами карт соединители, Microsoft Teams которые в настоящее время не поддерживаются, являются следующими:

* `heroImage`
* `hideOriginalBody`
* `startGroup`всегда рассматривается как `true` в Teams
* `originator`
* `correlationId`

### <a name="example-of-an-office-365-connector-card"></a>Пример карты Office 365 соединители

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

## <a name="receipt-card"></a>Карта получения

Teams поддерживает карточку получения. Это карточка, которая позволяет боту предоставлять пользователю квитанцию. Обычно он содержит список элементов, которые необходимо включить в квитанцию, например налоговые и общие сведения.

### <a name="support-for-receipt-cards"></a>Поддержка карт получения

| Боты в Teams | Расширения для система обмена сообщениями  | Соединители | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |

### <a name="example-of-a-receipt-card"></a>Пример карты получения

![Пример карты получения](~/assets/images/cards/receipt.png)

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

### <a name="additional-information-on-receipt-cards"></a>Дополнительные сведения о карточках получения

Ссылка на Bot Framework:

* [Карточка получения Node.js](/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [Карта получения C #](/dotnet/api/microsoft.bot.schema.receiptcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="signin-card"></a>Карточка Signin

Карта Signin позволяет боту запрашивать вход пользователя. Поддерживается в Teams в несколько иной форме, чем в bot Framework. Карта signin в Teams похожа на карточку signin в bot Framework, за исключением того, что карточка signin в Teams поддерживает только два действия: `signin` и `openUrl` .

Действие signin можно использовать с любой карты в Teams, а не только с карты signin. Дополнительные сведения о проверке подлинности см. в Microsoft Teams поток проверки [подлинности для ботов.](~/bots/how-to/authentication/auth-flow-bot.md)

### <a name="support-for-signin-cards"></a>Поддержка подписных карт

| Боты в Teams | Расширения для система обмена сообщениями  | Соединители | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ | ✔ |

### <a name="additional-information-on-signin-cards"></a>Дополнительные сведения о подписных карточках

Ссылка на Bot Framework:

* [Карточка signin Node.js](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [Signin card C #](/dotnet/api/microsoft.bot.schema.signincard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="thumbnail-card"></a>Карта эскиза

Карточка, которая обычно содержит одно изображение эскиза, одну или несколько кнопок и текст.

### <a name="support-for-thumbnail-cards"></a>Поддержка карт эскизов

| Боты в Teams | Расширения для система обмена сообщениями  | Соединители | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |

![Пример карты эскиза](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a>Свойства карты эскиза

| Свойство | Тип  | Описание |
| --- | --- | --- |
| title | Форматированный текст  | Название карты. Максимум 2 строки.|
| субтитры | Форматированный текст  | Субтитр карты. Максимум 2 строки.|
| текст | Форматированный текст  | Текст отображается под субтитром. Параметры форматирования см. [в виде форматирования карт.](~/task-modules-and-cards/cards/cards-format.md) |
| изображения | Массив изображений | Изображение, отображаемого в верхней части карты. Отношение аспектов 1:1 к квадрату. |
| кнопки | Массив объектов действий | Набор действий, применимых к текущей карте. Максимум 6. |
| нажмите кнопку | Объект Action | Активируется при нажатии на карточку самого пользователя. |

### <a name="example-of-a-thumbnail-card"></a>Пример карты эскиза

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

Ссылка на Bot Framework:

* [Эскиз карты Node.js](/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [Эскиз карты C #](/dotnet/api/microsoft.bot.schema.thumbnailcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="card-collections"></a>Коллекции карт

Teams поддерживает коллекции карт.

Коллекции карт включают `builder.AttachmentLayout.carousel` и `builder.AttachmentLayout.list` . Эти коллекции содержат адаптивные, герой или эскизные карточки.

## <a name="carousel-collection"></a>Коллекция Карусель

Макет [карусель показывает](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) карусель карт, необязательно с связанными кнопками действия.

### <a name="support-for-carousel-collections"></a>Поддержка коллекций карусель

| Боты в Teams | Расширения для система обмена сообщениями  | Соединители | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ | ✔ |

> [!NOTE]
> Карусель может отображать не более десяти карт на сообщение.

### <a name="properties-of-a-carousel-card"></a>Свойства карусели

Свойства карусельной карты такие же, как и у карт героя и эскизов.

### <a name="example-of-a-carousel-collection"></a>Пример коллекции карусель

![Пример карусели карт](~/assets/images/cards/carousel.png)

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

`builder.AttachmentLayoutTypes.Carousel` синтаксис для коллекций карусели.

## <a name="list-collection"></a>Коллекция списков

### <a name="support-for-list-collections"></a>Поддержка коллекций списков

В макете списка показан вертикально сложенный список карт, необязательно связанный с кнопками действия.

| Боты в Teams | Расширения для система обмена сообщениями  | Соединители | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |

### <a name="example-of-a-list-collection"></a>Пример коллекции списков

![Пример списка карт](~/assets/images/cards/list.png)

Свойства такие же, как для карты героя или эскиза.

В списке может отображаться не более десяти карт на сообщение.

> [!NOTE]
> Некоторые сочетания карт списка еще не поддерживаются на iOS и Android.

### <a name="syntax-for-list-collections"></a>Синтаксис для коллекций списков

`builder.AttachmentLayout.list` синтаксис для коллекций списков.

## <a name="cards-not-supported-in-teams"></a>Карты, не поддерживаемые в Teams

Следующие карты реализуются в рамках Bot Framework, но не поддерживаются Teams:

* Карты анимации
* Аудиокарты
* Видеокарты
