---
title: Справочник по карточкам
description: Описывает все карточки и действия карточки, доступные боты в Teams.
keywords: Справочник по карточкам Боты
ms.openlocfilehash: 9cd868e504e426cbe56ed1c5d05c8e6adc1e1ddf
ms.sourcegitcommit: 61edf47c9dd1dbc1df03d0d9fb83bfedca4c423b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2020
ms.locfileid: "44801489"
---
# <a name="cards-reference"></a>Справочник по карточкам

Карточки, перечисленные в этом разделе, поддерживаются в боты для Teams. Они основаны на карточках, определенных с помощью Bot Framework, но в Teams не поддерживаются все карточки с интерфейсом Bot и добавлены некоторые из них. Различия вызываемы в приведенных ниже ссылках.

## <a name="card-examples"></a>Примеры карточек

Дополнительные сведения об использовании карточек можно найти в документации по пакету SDK для Bot Builder (v3). Кроме того, вы можете найти примеры кода в репозитории Microsoft/Ботбуилдер-Samples на сайте GitHub.

* .NET
  * [Добавление карточек в качестве вложений в сообщения](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments)
  * [Пример кода карточек (построитель построителя)](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/CSharp/cards-RichCards)
* Node.js
  * [Добавление карточек в качестве вложений в сообщения](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)
  * [Пример кода карточек (построитель построителя)](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/Node/cards-RichCards)

## <a name="types-of-cards"></a>Типы карточек

В этой таблице перечислены доступные типы карт.

| Тип карточки | Описание |
| --- | --- |
| [Адаптивная карта](#adaptive-card) | Карточка с широкими возможностями настройки, которая может содержать любую комбинацию текста, речи, изображений, кнопок и полей ввода. |
| [Карточка главный Имиджевый баннер](#hero-card) | Обычно содержит одно крупное изображение, одну или несколько кнопок и небольшое количество текста. |
| [Карточка списка](#list-card) | Прокручиваемый список элементов. |
| [Соединительная карта Office 365](#office-365-connector-card) | Гибкий макет с несколькими разделами, полями, изображениями и действиями. |
| [Карточка приходной накладной](#receipt-card) | Предоставляет пользователю уведомление. |
| [Карточка входа](#signin-card) | Позволяет роботу отправить запрос на вход пользователя. |
| [Карточка эскиза](#thumbnail-card) | Обычно содержит одно эскизное изображение, некоторый короткий текст, а также одну или несколько кнопок. |
| [Коллекции карточек](#card-collections) | Используется для возвращения нескольких элементов в едином ответе |

## <a name="common-properties-for-all-cards"></a>Общие свойства для всех карточек

### <a name="inline-card-images"></a>Изображения в виде встроенных карточек

Ваша карточка может содержать встроенное изображение, включив ссылку на общедоступное изображение. В целях повышения производительности мы настоятельно рекомендуем размещать образ в общедоступной сети обмена контентом (CDN).

Изображения масштабируются вверх или вниз, сохраняя пропорции изображения, а затем обрезаются из центра для достижения соответствующих пропорций карточки.

Изображения должны быть не менее 1024 × 1024 и 1 МБ в формате PNG, JPEG или GIF; анимированный GIF-файл не поддерживается официально.

| Свойство | Тип  | Описание |
| --- | --- | --- |
| url | URL-адрес | URL-адрес HTTPS для изображения |
| alt | String | Доступное описание изображения |

### <a name="buttons"></a>Кнопки

Кнопки отображаются в нижней части карточки. Текст на кнопке всегда находится в одной строке и будет обрезан, если текст превышает ширину кнопки. Все дополнительные кнопки, превышающие максимальное число, поддерживаемое картой, не будут отображаться.

Для получения дополнительных сведений просмотрите [действия с картой](~/task-modules-and-cards/cards/cards-actions.md) .

### <a name="card-formatting"></a>Форматирование карточки

Дополнительные сведения о форматировании текста [в карточках см.](~/task-modules-and-cards/cards/cards-format.md)

## <a name="adaptive-card"></a>Адаптивная карта

Настраиваемая карточка, которая может содержать любую комбинацию текста, речи, изображений, кнопок и полей ввода. *Просмотрите раздел* [адаптивные карточки v 1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).

### <a name="support-for-adaptive-cards"></a>Поддержка адаптивных карт

| Боты в Teams | Расширения для сообщений  | Соединители | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |
|

### <a name="example-adaptive-card"></a>Пример адаптивной карточки

![Пример адаптивной карточки карты](~/assets/images/cards/adaptivecard.png)

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

#### <a name="for-more-information-on-adaptive-cards"></a>Дополнительные сведения о адаптивных картах

* [Обзор адаптивных карточек](/adaptive-cards/)
* [Действия адаптивной карточки в Teams](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)

## <a name="hero-card"></a>Карточка главный Имиджевый баннер

Карточка, которая обычно содержит одно крупное изображение, одну или несколько кнопок и текста.

### <a name="support-for-hero-cards"></a>Поддержка карточек главный Имиджевый баннер

| Боты в Teams | Расширения для сообщений  | Соединители | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |
|

### <a name="properties-of-a-hero-card"></a>Свойства карточки главный Имиджевый баннер

| Свойство | Тип  | Описание |
| --- | --- | --- |
| title | Форматированный текст  | Название карточки. Максимум 2 строки; форматирование в настоящее время не поддерживается |
| Подзаголовок | Форматированный текст  | Подзаголовок карточки. Максимум 2 строки; форматирование в настоящее время не поддерживается |
| текст | Форматированный текст  | Текст отображается сразу под подназванием; сведения о [форматировании карточек](~/task-modules-and-cards/cards/cards-format.md) для параметров форматирования |
| изображения | Массив изображений | Изображение, отображаемое в верхней части карточки. Пропорции 16:9 |
| Button | Массив объектов Action | Набор действий, применяемых к текущей карточке. Максимум 6 |
| тематическ | Объект Action | Это действие активируется, когда пользователь найдет на саму карточку |
|

### <a name="example-hero-card"></a>Пример карточки главный Имиджевый баннер

![Пример карточки главный Имиджевый баннер](~/assets/images/cards/hero.png)

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

### <a name="for-more-information-on-hero-cards"></a>Дополнительные сведения о карточках главный Имиджевый баннер

Справочные материалы по платформе Bot:

* [Узел карточки главный Имиджевый баннер](https://docs.microsoft.com/javascript/api/botframework-schema/herocard)
* [Карточка главный Имиджевый баннер C #](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.herocard?view=botbuilder-dotnet-3.0)

## <a name="list-card"></a>Карточка списка

В Microsoft Teams карточка списка была добавлена для предоставления функций, помимо того, что может предоставить коллекция списков. Карточка List предоставляет прокручиваемый список элементов.

### <a name="support-for-list-cards"></a>Поддержка карточек со списками

| Боты в Teams | Расширения для сообщений  | Соединители | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ |✔ |
|

### <a name="properties-of-a-list-card"></a>Свойства карточки списка

| Свойство | Тип  | Описание |
| --- | --- | --- |
| title | Форматированный текст  | Название карточки. Максимум 2 строки; форматирование в настоящее время не поддерживается |
| items | Массив элементов списка  ||
| Button | Массив объектов Action | Набор действий, применяемых к текущей карточке. Не более 6. Не отображается на мобильном устройстве. |
|

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

## <a name="office-365-connector-card"></a>Соединительная карта Office 365

Поддерживается в Microsoft Teams, а не в среде Bot.

Соединительная карта Office 365 предоставляет гибкий макет с несколькими разделами, полями, изображениями и действиями. Эта карточка содержит карту подключателя, чтобы ее можно было использовать в Боты. В разделе "Примечания" представлены различия между соединителными картами и картой O365.

### <a name="support-for-office-365-connector-cards"></a>Поддержка карт соединителей Office 365

| Боты в Teams | Расширения для сообщений  | Соединители | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✔ | ✖ |
|

### <a name="properties-of-the-office-365-connector-card"></a>Свойства карточки соединителя Office 365

| Свойство | Тип  | Описание |
| --- | --- | --- |
| title | Форматированный текст  | Название карточки. Максимум 2 строки; форматирование в настоящее время не поддерживается |
| summary | Форматированный текст  | Сводка по карточке. Максимум 2 строки; форматирование в настоящее время не поддерживается |
| текст | Форматированный текст  | Текст отображается сразу под подназванием; сведения о [форматировании карточек](~/task-modules-and-cards/cards/cards-format.md) для параметров форматирования |
| themeColor | ШЕСТНАДЦАТЕРИЧная строка | цвет, переопределяющий Акцентколор, предоставленный в манифесте приложения |

### <a name="notes-on-the-office-365-connector-card"></a>Примечания к соединительной карте Office 365

Карты соединителей Office 365 правильно работают в Microsoft Teams, включая [действия ActionCard](/outlook/actionable-messages/card-reference#actioncard-action).

Одним из важных различий между использованием карт соединителей с соединителя и карт подключателя в Bot является обработка действий с картой.

* Для соединителя конечная точка получает полезные данные карточки через HTTP POST.
* Для элемента Bot `HttpPOST` действие запускает `invoke` действие, которое ОТПРАВЛЯЕТ только идентификатор действия и основной текст в Bot.

Каждая соединительная карта может отображать не более 10 разделов, а каждый раздел может содержать не более 5 изображений и 5 действий.

> [!NOTE]
> Дополнительные разделы, изображения или действия в сообщении не будут отображаться.

Все текстовые поля поддерживают Markdown и HTML. Вы можете управлять тем, какие разделы используют Markdown или HTML, задав `markdown` свойство в сообщении. По умолчанию `markdown` имеет значение `true` ;, если вы хотите использовать HTML, задайте значение `markdown` `false` .

Если указать `themeColor` свойство, оно переопределяет `accentColor` свойство в манифесте приложения.

Чтобы указать стиль отображения для `activityImage` , можно задать следующие значения `activityImageType` :

| Значение | Описание |
| --- | --- |
| `avatar` | Умолчани `activityImage`будет обрезан как круг |
| `article` | `activityImage`будет отображаться как прямоугольник и сохранять пропорции |

Дополнительные сведения о свойствах карт соединителей можно узнать в статье [Справочник по карточкам сообщений с действиями](/outlook/actionable-messages/card-reference). В настоящее время в Microsoft Teams в настоящее время не поддерживаются следующие свойства карточки соединителя:

* `heroImage`
* `hideOriginalBody`
* `startGroup`(всегда обрабатываются как `true` в Teams)
* `originator`
* `correlationId`

### <a name="example-office-365-connector-card"></a>Пример карточки соединителя Office 365

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

## <a name="receipt-card"></a>Карточка приходной накладной

Поддерживается в Teams.

Карточка, позволяющая роботу получить уведомление для пользователя. Как правило, он содержит список элементов, которые необходимо включить в сведения о получении, налогах и итогах, а также другие тексты.

### <a name="support-for-receipts-cards"></a>Поддержка карточек чеков

| Боты в Teams | Расширения для сообщений  | Соединители | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |
|

### <a name="for-more-information-on-receipt-cards"></a>Дополнительные сведения о карточках прихода

Справочные материалы по платформе Bot:

* [Узел карточки чеков](https://docs.microsoft.com/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest)
* [Карточка прихода C #](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.receiptcard?view=botbuilder-dotnet-3.0)

## <a name="signin-card"></a>Карточка входа

Карточка, позволяющая роботу отправить запрос на вход пользователя. Поддерживается в Microsoft Teams в несколько разных формах, чем в Bot Framework. Карточка входа в Teams аналогична карте входа в Bot Framework с исключением, что карточка входа в Teams поддерживает только два действия: `signin` и `openUrl` .

*Действие SignIn* можно использовать с любой карточки в Teams, а не только с помощью карточки входа. Для получения дополнительных сведений о проверке подлинности обратитесь к разделу [Проверка подлинности Microsoft Teams для Боты](~/bots/how-to/authentication/auth-flow-bot.md) .

### <a name="support-for-signin-cards"></a>Поддержка карточек входа

| Боты в Teams | Расширения для сообщений  | Соединители | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ | ✔ |
|

### <a name="for-more-information-on-signin-cards"></a>Дополнительные сведения о карточках входа

Справочные материалы по платформе Bot:

* [Узел карточки входа](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest)
* [Карточка входа в систему C #](/dotnet/api/microsoft.bot.connector.signincard?view=botbuilder-dotnet-3.0)

## <a name="thumbnail-card"></a>Карточка эскиза

Карточка, которая обычно содержит одно эскизное изображение, одну или несколько кнопок и текст.

### <a name="support-for-thumbnail-cards"></a>Поддержка карт эскизов

| Боты в Teams | Расширения для сообщений  | Соединители | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |
|

![Пример карточки эскиза](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a>Свойства карточки эскиза

| Свойство | Тип  | Описание |
| --- | --- | --- |
| title | Форматированный текст  | Название карточки. Максимум 2 строки; форматирование в настоящее время не поддерживается |
| Подзаголовок | Форматированный текст  | Подзаголовок карточки. Максимум 2 строки; форматирование в настоящее время не поддерживается |
| текст | Форматированный текст  | Текст отображается сразу под подназванием; сведения о [форматировании карточек](~/task-modules-and-cards/cards/cards-format.md) для параметров форматирования |
| изображения | Массив изображений | Изображение, отображаемое в верхней части карточки. Пропорции 1:1 (квадрат) |
| Button | Массив объектов Action | Набор действий, применяемых к текущей карточке. Максимум 6 |
| тематическ | Объект Action | Это действие активируется, когда пользователь найдет на саму карточку |
|

### <a name="example-thumbnail-card"></a>Пример карточки эскиза

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

Справочные материалы по платформе Bot:

* [Узел карточки эскиза](https://docs.microsoft.com/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest)
* [Карта с эскизом C #](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.thumbnailcard?view=botbuilder-dotnet-3.0)

## <a name="card-collections"></a>Коллекции карточек

Коллекции карточек поддерживаются в Teams.

Коллекции карточек предоставляются с помощью Bot Framework: `builder.AttachmentLayout.carousel` и `builder.AttachmentLayout.list` . Эти коллекции могут содержать адаптивные, главный Имиджевый баннер или карты эскиза.

## <a name="carousel-collection"></a>Коллекция обойм

[Макет обоймы](/azure/bot-service/dotnet/bot-builder-dotnet-add-rich-card-attachments?view=azure-bot-service-3.0) отображает обойму карточек (при необходимости) с соответствующими кнопками действия.

### <a name="support-for-carousel-collections"></a>Поддержка коллекций обойм

| Боты в Teams | Расширения для сообщений  | Соединители | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ | ✔ |
|

> [!NOTE]
> В обойме может отображаться не более 10 карточек для каждого сообщения.

### <a name="example-carousel-collection"></a>Пример коллекции обойм

![Пример обоймы карточек](~/assets/images/cards/carousel.png)

Это те же свойства, что и для карты главный Имиджевый баннер или эскиза.

### <a name="syntax-for-carousel-collections"></a>Синтаксис для коллекций обойм

`builder.AttachmentLayout.carousel`

## <a name="list-collection"></a>Коллекция List

### <a name="support-for-list-collections"></a>Поддержка коллекций списков

В раскладке списка отображается вертикальный список карточек, при необходимости связанные с ними кнопки действий.

| Боты в Teams | Расширения для сообщений  | Соединители | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |
|

### <a name="example-list-collection"></a>Пример коллекции списков

![Пример списка карточек](~/assets/images/cards/list.png)

Это те же свойства, что и для карты главный Имиджевый баннер или эскиза.

В списке может отображаться не более 10 карточек для каждого сообщения.

> [!NOTE]
> Некоторые комбинации карточек со списками пока не поддерживаются в iOS и Android.

### <a name="syntax-for-list-collections"></a>Синтаксис коллекций списков

`builder.AttachmentLayout.list`

## <a name="cards-not-supported-in-teams"></a>Карточки, не поддерживаемые в Teams

Следующие карты реализуются с помощью Bot Framework, но не поддерживаются в Teams.

* Карты анимации
* Звуковые карты
* Видеокарты
