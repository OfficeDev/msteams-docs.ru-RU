---
title: Ссылки на карточки
description: Описывает все карты и действия карты, доступные для ботов в Teams
localization_priority: Normal
keywords: Боты карты ссылки
ms.topic: reference
ms.openlocfilehash: cab7f1659759f40beb1aba59531ee6c1a84662c1
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566861"
---
# <a name="cards-reference"></a>Ссылки на карточки

Карты, перечисленные в этом документе, поддерживаются в ботах в течение Microsoft Teams. Они основаны на картах, определенных Bot Framework, но Teams не поддерживает все карты Bot Framework, и вместо этого Teams карты были добавлены. Различия называются в ссылках в этом документе.

## <a name="card-examples"></a>Примеры карт

Дополнительную информацию о том, как использовать карты, можно найти в документации для Bot Builder SDK v3. Образцы кода также доступны в репозитории Microsoft/BotBuilder-Samples на GitHub.

* .NET
  * [Добавить карты в качестве вложений в сообщения.](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)
  * [Карты образец кода Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards).

* Node.js
  * [Добавить карты в качестве вложений в сообщения.](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)
  * [Карты образец кода Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards).

## <a name="types-of-cards"></a>Типы карт

В этой таблице показаны доступные вам типы карт:

| Тип карты | Описание |
| --- | --- |
| [Адаптивная карта](#adaptive-card) | Эта карта является очень настраиваемой картой, которая может содержать любую комбинацию текстовых, речеспособных, изображений, кнопок и входных полей. |
| [Карта героя](#hero-card) | Эта карта обычно содержит одно большое изображение, одну или несколько кнопок и небольшое количество текста. |
| [Карта списка](#list-card) | Эта карта является прокруткой списка элементов. |
| [Office 365-карта](#office-365-connector-card) | Эта карта имеет гибкую компоновку с несколькими разделами, полями, изображениями и действиями. |
| [Квитанция карты](#receipt-card) | Эта карта предоставляет квитанцию пользователю. |
| [Карта Сигнина](#signin-card) | Эта карта позволяет боту запрашивать, чтобы пользователь влиться. |
| [Thumbnail карты](#thumbnail-card) | Эта карта обычно содержит одно изображение эскиза, короткий текст и одну или несколько кнопок. |
| [Коллекции карт](#card-collections) | Эта карточка используется для возврата нескольких элементов в одном ответе. |

## <a name="common-properties-for-all-cards"></a>Общие свойства для всех карт

### <a name="inline-card-images"></a>Изображения стационарных карт

Карта может содержать рядное изображение, включив ссылку на общедоступное изображение. Для целей производительности настоятельно рекомендуется разместить изображение в общедоступной сети доставки контента (CDN).

Изображения масштабируются или уменьшены в размерах при сохранении соотношения сторон для покрытия области изображения. Изображения затем обрезаются из центра для достижения соответствующего соотношения сторон для карты.

Изображения должны быть не более 1024×1024, в формате PNG, JPEG или GIF, и не поддерживать анимированный GIF.

| Свойство | Тип  | Описание |
| --- | --- | --- |
| url | URL-адрес | URL-адрес HTTPS на изображение. |
| alt | String | Доступное описание изображения. |

> [!NOTE]
> Если карта включает URL-адрес изображения, который проходит через перенаправление перед окончательным изображением, перенаправление URL-адреса изображения не поддерживается. Это происходит для изображений, еханых в общедоступных облаках.

### <a name="buttons"></a>Кнопки

Кнопки отображаются уложенными в нижней части карты. Текст кнопки всегда находится на одной строке и усечен, если текст превышает ширину кнопки. Дополнительные кнопки, выходящие за рамки максимального числа, поддерживаемого картой, не отображаются.

Для получения дополнительной информации, [смотрите действия карты](~/task-modules-and-cards/cards/cards-actions.md).

### <a name="card-formatting"></a>Форматирование карт

Для получения дополнительной информации о форматировании текста в картах, [см.](~/task-modules-and-cards/cards/cards-format.md)

## <a name="adaptive-card"></a>Адаптивная карта

Адаптивная карта представляет собой настраиваемую карту, которая может содержать любую комбинацию текстовых, речеспособных, изображений, кнопок и полей ввода. Для получения дополнительной информации [см.](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0)

### <a name="support-for-adaptive-cards"></a>Поддержка адаптивных карт

| Боты в Teams | Расширения для система обмена сообщениями  | Соединители | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |

> [!NOTE]
> * Teams поддерживает v1.2 или более ранние функции адаптивной карты.
> * Медиа-элементы в настоящее время не поддерживаются в адаптивной карте v1.2 Teams платформы.

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

#### <a name="additional-information-on-adaptive-cards"></a>Дополнительная информация об адаптивных картах

Ссылка на Bot Framework:

* [Адаптивные карты Node.js](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)
* [Адаптивная карта C #](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)

## <a name="hero-card"></a>Карта героя

Карта, которая обычно содержит одно большое изображение, одну или несколько кнопок и текст.

### <a name="support-for-hero-cards"></a>Поддержка карт героев

| Боты в Teams | Расширения для система обмена сообщениями  | Соединители | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |

### <a name="properties-of-a-hero-card"></a>Свойства карты героя

| Свойство | Тип  | Описание |
| --- | --- | --- |
| title | Форматированный текст  | Название карты. Максимум 2 строки. |
| подзаголовок | Форматированный текст  | Подзаголовок карты. Максимум 2 строки.|
| текст | Форматированный текст  | Текст появляется под подзаголовком. Для форматирования опций [см.](~/task-modules-and-cards/cards/cards-format.md) |
| Изображения | Массив изображений | Изображение отображается в верхней части карты. Соотношение сторон 16:9. |
| Кнопки | Массив объектов действия | Набор действий, применимых к текущей карте. Максимум 6. |
| кран | Объект Action | Активируется при нажатии пользователя на сам карту. |

### <a name="example-of-a-hero-card"></a>Пример карты героя

![Пример карты героя](~/assets/images/cards/hero.png)

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

### <a name="additional-information-on-hero-cards"></a>Дополнительная информация о картах героев

Ссылка на Bot Framework:

* [Герой карты Node.js](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-a-hero-card&preserve-view=true)
* [Карта героя C #](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-hero-card&preserve-view=true)

## <a name="list-card"></a>Карта списка

Карта списка была добавлена в систему, Teams функции сверх того, что может предоставить коллекция списков. Карта списка содержит список элементов для прокрутки.

### <a name="support-for-list-cards"></a>Поддержка карт списков

| Боты в Teams | Расширения для система обмена сообщениями  | Соединители | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ |✔ |

### <a name="properties-of-a-list-card"></a>Свойства карты списка

| Свойство | Тип  | Описание |
| --- | --- | --- |
| title | Форматированный текст  | Название карты. Максимум 2 строки.|
| элементы | Массив элементов списка ||
| Кнопки | Массив объектов действия | Набор действий, применимых к текущей карте. Максимум 6. |

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

## <a name="office-365-connector-card"></a>Office 365-карта

Карта Office 365 разъем поддерживается в Teams, а не в Bot Framework. Эта карта обеспечивает гибкую компоновку с несколькими разделами, полями, изображениями и действиями. Эта карта инкапсулирует разъем карты, так что он может быть использован ботов. Различия между разъемами и картой O365 см. [Примечания на Office 365 разъема.](#notes-on-the-office-365-connector-card)

### <a name="support-for-office-365-connector-cards"></a>Поддержка Office 365 разъемов

| Боты в Teams | Расширения для система обмена сообщениями  | Соединители | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✔ | ✖ |

### <a name="properties-of-the-office-365-connector-card"></a>Свойства Office 365 карты

| Свойство | Тип  | Описание |
| --- | --- | --- |
| title | Форматированный текст  | Название карты. Максимум 2 строки. |
| summary | Форматированный текст  | Резюме карты. Максимум 2 строки. |
| текст | Форматированный текст  | Текст появляется под подзаголовком. Для форматирования опций [см.](~/task-modules-and-cards/cards/cards-format.md) |
| themeColor | Строка HEX | Цвет, переопределяет акцентColor, предоставленный из манифеста приложения. |

### <a name="notes-on-the-office-365-connector-card"></a>Заметки на Office 365 разъеме карты

Office 365 разъем карты функционируют должным образом в Microsoft Teams, в том [числе ActionCard действия](/outlook/actionable-messages/card-reference#actioncard-action).

Одним из важных различий между использованием разъемных карт из разъема и использованием разъемных карт в вашем боте является обработка действий карты.

* Для разъема конечная точка получает полезную нагрузку карты через HTTP POST.
* Для бота действие `HttpPOST` запускает действие, `invoke` которое отправляет боту только идентификатор действия и тело.

Каждая карта разъема может отображать не более десяти разделов, и каждый раздел может содержать не более пяти изображений и пять действий.

> [!NOTE]
> Любые дополнительные разделы, изображения или действия в сообщении не отображаются.

Все текстовые поля поддерживают разметку и HTML. Вы можете контролировать, какие разделы используют разметку или HTML, установив `markdown` свойство в сообщении. По `markdown` умолчанию устанавливается `true` . Если вы хотите использовать HTML вместо этого, `markdown` установите на `false` .

Если вы `themeColor` указываете свойство, оно переопределяет `accentColor` свойство в манифесте приложения.

Чтобы указать стиль рендеринга `activityImage` для, вы можете установить `activityImageType` следующим образом:

| Значение | Описание |
| --- | --- |
| `avatar` | По умолчанию; `activityImage` обрезается как круг. |
| `article` | `activityImage` отображается как прямоугольник и сохраняет свое соотношение сторон. |

Для всех других деталей о свойствах разъемной карты, смотрите [действий ссылку карты сообщения.](/outlook/actionable-messages/card-reference) Единственными свойствами разъемной карты, которые Microsoft Teams в настоящее время не поддерживают, являются следующие:

* `heroImage`
* `hideOriginalBody`
* `startGroup`всегда рассматривается `true` как в Teams
* `originator`
* `correlationId`

### <a name="example-of-an-office-365-connector-card"></a>Пример карты Office 365 разъема

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

## <a name="receipt-card"></a>Квитанция карты

Teams поддерживает квитанцию. Это карта, которая позволяет боту предоставить квитанцию пользователю. Как правило, он содержит список товаров, которые можно включить в квитанцию, такие как налог и общая информация.

### <a name="support-for-receipt-cards"></a>Поддержка квитанций

| Боты в Teams | Расширения для система обмена сообщениями  | Соединители | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |

### <a name="example-of-a-receipt-card"></a>Пример квитанции

![Пример квитанции](~/assets/images/cards/receipt.png)

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

### <a name="additional-information-on-receipt-cards"></a>Дополнительная информация о квитанциях

Ссылка на Bot Framework:

* [Квитанция по Node.js](/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [Квитанция карты C #](/dotnet/api/microsoft.bot.schema.receiptcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="signin-card"></a>Карта Сигнина

Карта Signin позволяет боту запросить у пользователя регистрацию. Он поддерживается в Teams в несколько иной форме, чем это имеется в Bot Framework. Карта signin в Teams похожа на карту signin в Bot Framework, за исключением того, что карта signin в Teams поддерживает только два действия: `signin` и `openUrl` .

Действия signin можно использовать с любой карты в Teams, а не только с карты signin. Для получения дополнительной информации об аутентификации [Microsoft Teams потока аутентификации для ботов.](~/bots/how-to/authentication/auth-flow-bot.md)

### <a name="support-for-signin-cards"></a>Поддержка подписных карт

| Боты в Teams | Расширения для система обмена сообщениями  | Соединители | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ | ✔ |

### <a name="additional-information-on-signin-cards"></a>Дополнительная информация о карточках signin

Ссылка на Bot Framework:

* [Сигнин карточный Node.js](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [Сигнин-карта C #](/dotnet/api/microsoft.bot.schema.signincard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="thumbnail-card"></a>Thumbnail карты

Карта, которая обычно содержит одно изображение эскиза, одну или несколько кнопок и текст.

### <a name="support-for-thumbnail-cards"></a>Поддержка эскизных карт

| Боты в Teams | Расширения для система обмена сообщениями  | Соединители | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |

![Пример карты эскиза](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a>Свойства эскизной карты

| Свойство | Тип  | Описание |
| --- | --- | --- |
| title | Форматированный текст  | Название карты. Максимум 2 строки.|
| подзаголовок | Форматированный текст  | Подзаголовок карты. Максимум 2 строки.|
| текст | Форматированный текст  | Текст появляется под подзаголовком. Для форматирования опций [см.](~/task-modules-and-cards/cards/cards-format.md) |
| Изображения | Массив изображений | Изображение отображается в верхней части карты. Соотношение аспектов 1:1 квадрат. |
| Кнопки | Массив объектов действия | Набор действий, применимых к текущей карте. Максимум 6. |
| кран | Объект Action | Активируется при нажатии пользователя на сам карту. |

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

* [Thumbnail карты Node.js](/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [Thumbnail карты C #](/dotnet/api/microsoft.bot.schema.thumbnailcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="card-collections"></a>Коллекции карт

Teams поддерживает коллекции карт.

Коллекции карт включают `builder.AttachmentLayout.carousel` и `builder.AttachmentLayout.list` . Эти коллекции содержат адаптивные, геройские или эскизные карты.

## <a name="carousel-collection"></a>Коллекция каруселей

Макет [карусели показывает](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) карусель карт, дополнительно с связанными кнопками действия.

### <a name="support-for-carousel-collections"></a>Поддержка коллекций каруселей

| Боты в Teams | Расширения для система обмена сообщениями  | Соединители | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ | ✔ |

> [!NOTE]
> Карусель может отображать не более десяти карт на одно сообщение.

### <a name="properties-of-a-carousel-card"></a>Свойства карусели карты

Свойства карты карусели такие же, как у героя и эскизных карт.

### <a name="example-of-a-carousel-collection"></a>Пример коллекции каруселей

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

### <a name="syntax-for-carousel-collections"></a>Синтаксис для коллекций каруселей

`builder.AttachmentLayoutTypes.Carousel` является синтаксисом для коллекций каруселей.

## <a name="list-collection"></a>Коллекция списков

### <a name="support-for-list-collections"></a>Поддержка коллекций списков

Макет списка показывает вертикально сложенный список карт, дополнительно с связанными кнопками действия.

| Боты в Teams | Расширения для система обмена сообщениями  | Соединители | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |

### <a name="example-of-a-list-collection"></a>Пример коллекции списков

![Пример списка карт](~/assets/images/cards/list.png)

Свойства такие же, как для героя или эскиз карты.

Список может отображать не более десяти карт на одно сообщение.

> [!NOTE]
> Некоторые комбинации карт списка пока не поддерживаются на iOS и Android.

### <a name="syntax-for-list-collections"></a>Синтаксис для коллекций списков

`builder.AttachmentLayout.list` является синтаксисом для коллекций списков.

## <a name="cards-not-supported-in-teams"></a>Карты, не поддерживаемые в Teams

Следующие карты реализованы Bot Framework, но не поддерживаются Teams:

* Анимационные карты
* Аудиокарты
* Видеокарты
