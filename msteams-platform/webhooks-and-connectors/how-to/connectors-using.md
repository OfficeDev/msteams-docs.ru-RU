---
title: Создание и отправка сообщений
author: laujan
description: В этом модуле вы узнаете, как использовать соединители Office 365, а также создавать и отправлять сообщения с действиями в Microsoft Teams
ms.topic: how-to
ms.localizationpriority: high
ms.openlocfilehash: 5014c23d13dd8f0b1c694c144e936c624c602d40
ms.sourcegitcommit: dccb48902e08484692ab927415bcd3d61dc50db2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/19/2022
ms.locfileid: "67806782"
---
# <a name="create-and-send-messages"></a>Создание и отправка сообщений

Вы можете создавать и отправлять сообщения с действиями с помощью входящих веб-перехватчиков или соединителя Office 365.

## <a name="create-actionable-messages"></a>Создание сообщений с действиями

Сообщения с действиями включают шесть видимых кнопок на карточке. Каждая кнопка определена в свойстве `potentialAction` сообщения с помощью действий `ActionCard`, каждое из которых содержит тип элемента ввода: текстовое поле, элемент управления "Выбор даты" или список с возможностью выбора нескольких вариантов. С каждым `ActionCard` связано действие, например `HttpPOST`.

Карточки соединителя поддерживают следующие действия.

* `ActionCard`: представляет один или несколько типов входных данных и соответствующие действия.
* `HttpPOST`: отправляет запрос POST на URL-адрес.
* `OpenUri`: открывает URI в отдельном браузере или приложении; при необходимости ссылается на разные URI в зависимости от операционной системы.

Действие `ActionCard` поддерживает три типа входных данных:

* `TextInput`: однострочное или многострочное текстовое поле с необязательным ограничением длины.
* `DateInput`: средство выбора даты с необязательным выбором времени.
* `MultichoiceInput`: нумерованный список вариантов с возможностью выбора одного или нескольких пунктов.

`MultichoiceInput` поддерживает свойство `style`, указывающее, отображается ли список изначально полностью развернутым. Значение `style` по умолчанию зависит от значения `isMultiSelect`.

| `isMultiSelect` | Значение `style` по умолчанию |
| --- | --- |
| `false` или не задано | `compact` |
| `true` | `expanded` |

Чтобы отобразить список с несколькими вариантами выбора в компактном стиле, укажите `"isMultiSelect": true` и `"style": true`.

Дополнительные сведения о действиях с карточками соединителя см. в разделе [Действия](/outlook/actionable-messages/card-reference#actions).

> [!NOTE]
>
> * Значение `compact` для свойства `style` в Microsoft Teams равноценно значению `normal` для свойства `style` в Microsoft Outlook.
> * Для действия HttpPOST маркер носителя включается в запросы. Этот маркер содержит удостоверение пользователя Microsoft Azure Active Directory (Azure AD) Office 365, выполнившего действие.

## <a name="send-a-message-through-incoming-webhook-or-office-365-connector"></a>Отправка сообщения через входящий веб-перехватчик или соединитель Office 365

Чтобы отправить сообщение через входящий веб-перехватчик или соединитель Office 365, необходимо отправить полезные данные JSON на URL-адрес веб-перехватчика. Эти полезные данные будут отображаться в [форме карточки соединителя Office 365](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).

С помощью этого кода JSON также можно создавать карточки с различными элементами для ввода данных, например текстовыми полями, переключателями множественного выбора или средствами выбора даты и времени. Код, генерирующий карточку и отправляющий ее на URL-адрес веб-перехватчика, может выполняться в любой размещенной службе. Эти карточки определяются как часть сообщений с действиями, а также поддерживаются в [карточках](~/task-modules-and-cards/what-are-cards.md), используемых ботами Teams и расширениями сообщений.

### <a name="example-of-connector-message"></a>Пример сообщения соединителя

Пример сообщения соединителя выглядит следующим образом.

```json
{
    "@type": "MessageCard",
    "@context": "http://schema.org/extensions",
    "themeColor": "0076D7",
    "summary": "Larry Bryant created a new task",
    "sections": [{
        "activityTitle": "Larry Bryant created a new task",
        "activitySubtitle": "On Project Tango",
        "activityImage": "https://teamsnodesample.azurewebsites.net/static/img/image5.png",
        "facts": [{
            "name": "Assigned to",
            "value": "Unassigned"
        }, {
            "name": "Due date",
            "value": "Mon May 01 2017 17:07:18 GMT-0700 (Pacific Daylight Time)"
        }, {
            "name": "Status",
            "value": "Not started"
        }],
        "markdown": true
    }],
    "potentialAction": [{
        "@type": "ActionCard",
        "name": "Add a comment",
        "inputs": [{
            "@type": "TextInput",
            "id": "comment",
            "isMultiline": false,
            "title": "Add a comment here for this task"
        }],
        "actions": [{
            "@type": "HttpPOST",
            "name": "Add comment",
            "target": "https://learn.microsoft.com/outlook/actionable-messages"
        }]
    }, {
        "@type": "ActionCard",
        "name": "Set due date",
        "inputs": [{
            "@type": "DateInput",
            "id": "dueDate",
            "title": "Enter a due date for this task"
        }],
        "actions": [{
            "@type": "HttpPOST",
            "name": "Save",
            "target": "https://learn.microsoft.com/outlook/actionable-messages"
        }]
    }, {
        "@type": "OpenUri",
        "name": "Learn More",
        "targets": [{
            "os": "default",
            "uri": "https://learn.microsoft.com/outlook/actionable-messages"
        }]
    }, {
        "@type": "ActionCard",
        "name": "Change status",
        "inputs": [{
            "@type": "MultichoiceInput",
            "id": "list",
            "title": "Select a status",
            "isMultiSelect": "false",
            "choices": [{
                "display": "In Progress",
                "value": "1"
            }, {
                "display": "Active",
                "value": "2"
            }, {
                "display": "Closed",
                "value": "3"
            }]
        }],
        "actions": [{
            "@type": "HttpPOST",
            "name": "Save",
            "target": "https://learn.microsoft.com/outlook/actionable-messages"
        }]
    }]
}
```

Это сообщение предоставляет на канале представленную ниже карточку.

![Снимок экрана с карточкой соединителя](~/assets/images/connectorcard.png)

## <a name="send-messages-using-curl-and-powershell"></a>Отправка сообщений с помощью cURL и PowerShell

# <a name="curl"></a>[cURL](#tab/cURL)

Чтобы опубликовать сообщение в веб-перехватчике с помощью cURL. выполните следующие действия.

1. Установите cURL с [сайта cURL](https://curl.haxx.se/).

1. Введите в командной строке следующую команду cURL:

   ```bash
   // on macOS or Linux
   curl -H 'Content-Type: application/json' -d '{"text": "Hello World"}' <YOUR WEBHOOK URL>
   ```

   ```bash
   // on Windows
   curl.exe -H "Content-Type:application/json" -d "{'text':'Hello World'}" <YOUR WEBHOOK URL>
   ```

    > [!NOTE]
    > В случае успешного выполнения запроса POST команда `curl` должна возвращать простой отклик **1**.

1. Проверьте наличие новой опубликованной карты в клиенте Teams.

# <a name="powershell"></a>[PowerShell](#tab/PowerShell)

 Необходимое условие: установка PowerShell и знакомство с основами его использования.

Чтобы отправить сообщения веб-перехватчику с помощью PowerShell, выполните следующие действия.

1. В командной строке PowerShell введите следующую команду:

   ```powershell
   Invoke-RestMethod -Method post -ContentType 'Application/Json' -Body '{"text":"Hello World!"}' -Uri <YOUR WEBHOOK URL>
   ```

    > [!NOTE]
    > В случае успешного выполнения запроса POST команда `Invoke-RestMethod` должна возвращать простой отклик **1**.

1. Проверьте канал Teams, связанный с URL-адресом веб-перехватчика. На канале появится новая карточка. Перед использованием соединителя для тестирования или публикации приложения необходимо сделать следующее.

    * [Включение двух значков](../../concepts/build-and-test/apps-package.md#app-icons).
    * Измените раздел `icons` манифеста на имена файлов значков, а не на их URL-адреса.

---

## <a name="send-adaptive-cards-using-an-incoming-webhook"></a>Отправка адаптивных карточек с помощью входящего веб-перехватчика

> [!NOTE]
>
> * Все собственные элементы схемы адаптивных карточек, кроме `Action.Submit`, полностью поддерживаются.
> * Поддерживаемые действия: [**Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html), [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html) и [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html).

Чтобы отправить адаптивные карточки через входящий веб-перехватчик, выполните следующие действия.

1. [Настройте пользовательский веб-перехватчик в Teams.](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
1. Создайте JSON-файл адаптивной карточки, используя следующий код:

    ```json
    {
       "type":"message",
       "attachments":[
          {
             "contentType":"application/vnd.microsoft.card.adaptive",
             "contentUrl":null,
             "content":{
                "$schema":"http://adaptivecards.io/schemas/adaptive-card.json",
                "type":"AdaptiveCard",
                "version":"1.2",
                "body":[
                    {
                    "type": "TextBlock",
                    "text": "For Samples and Templates, see [https://adaptivecards.io/samples](https://adaptivecards.io/samples)"
                    }
                ]
             }
          }
       ]
    }
    ```

    Имеются следующие свойства JSON-файла адаптивной карточки.

    * Поле `"type"` должно иметь значение `"message"`.
    * Массив `"attachments"` содержит набор объектов card.
    * В поле `"contentType"` следует задать тип "Адаптивная карточка".
    * Объект `"content"` — это карточка, отформатированная в JSON.

1. Проверьте адаптивную карточку с помощью Postman.

    * Протестируйте адаптивную карточку с помощью [Postman](https://www.postman.com) для отправки запроса POST на URL-адрес, созданный для настройки входящих веб-перехватчиков.
    * Вставьте файл JSON в текст запроса и просмотрите сообщение адаптивной карточки в Teams.

> [!TIP]
> Используйте [примеры кода и шаблоны](https://adaptivecards.io/samples) адаптивной карточки для проверки основной части запроса POST.

## <a name="rate-limiting-for-connectors"></a>Ограничение скорости для соединителей

Ограничения скорости приложений управляют трафиком, который разрешено создавать в канале соединителю или входящему веб-перехватчику. В Teams запросы отслеживаются с помощью окна фиксированной скорости и инкрементного счетчика с измерением в секундах. Если за секунду было выполнено более четырех запросов, клиентское подключение будут ограничено до тех пор, пока окно не обновится в течение длительности окна фиксированной скорости.

### <a name="transactions-per-second-thresholds"></a>Пороговые значения количества транзакций в секунду

В следующей таблице представлены сведения о транзакциях с учетом времени.

| Время в секундах  | Максимальное разрешенное количество запросов  |
|---|---|
| 1   | 4  |  
| 30   | 60  |  
| 3600   | 100  |
| 7200 | 150  |
| 86400  | 1800  |

[Логика повторных попыток с экспоненциальной задержкой](/azure/architecture/patterns/retry) поможет избежать ограничения скорости в тех случаях, когда число запросов за секунду превышает пределы. Следуйте [рекомендациям](../../bots/how-to/rate-limit.md), чтобы не достичь ограничений скорости.

> [!NOTE]
> [Логика повторных попыток с экспоненциальной задержкой](/azure/architecture/patterns/retry) может смягчить ограничение скорости в случаях, когда запросы превышают ограничения в течение одной секунды. Обратитесь к [ответам HTTP 429](../../bots/how-to/rate-limit.md#handle-http-429-responses), чтобы избежать ограничения пропускной способности.

```csharp
// Please note that response body needs to be extracted and read 
// as Connectors do not throw 429s
try
{
    // Perform Connector POST operation     
    var httpResponseMessage = await _client.PostAsync(IncomingWebhookUrl, new StringContent(content));
    // Read response content
    var responseContent = await httpResponseMessage.Content.ReadAsStringAsync();
    if (responseContent.Contains("Microsoft Teams endpoint returned HTTP error 429")) 
    {
        // initiate retry logic
    }
}
```

Эти ограничения установлены с целью предотвратить перегрузку канала запросами от соединителя и обеспечивают удобство работы пользователей.

## <a name="see-also"></a>См. также

* [Соединители Office 365 для Microsoft Teams](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [Создание входящего веб-перехватчика](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [Создание исходящего веб-перехватчика](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)
* [Ограничение скорости трафика для сообщений ботов Teams](~/bots/how-to/rate-limit.md)
* [Создание вкладок с использованием адаптивных карточек](~/tabs/how-to/build-adaptive-card-tabs.md)
* [Форматирование карточек в Microsoft Teams](~/task-modules-and-cards/cards/cards-format.md)
* [Создание бота уведомлений с помощью JavaScript](../../sbs-gs-notificationbot.yml)
* [Создание первого приложения бота с помощью JavaScript](../../sbs-gs-bot.yml)
