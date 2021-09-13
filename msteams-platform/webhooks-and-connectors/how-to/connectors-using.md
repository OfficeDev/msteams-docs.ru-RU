---
title: Создание и отправка сообщений
author: laujan
description: Сведения о том, как использовать Соединители Office 365 в Microsoft Teams.
ms.topic: how-to
ms.localizationpriority: medium
keywords: соединитель teams o365
ms.openlocfilehash: 6d10a173079fb31db303e98bfaf0800ff048a187
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/12/2021
ms.locfileid: "59157656"
---
# <a name="create-and-send-messages"></a>Создание и отправка сообщений

Вы можете создавать действия сообщения и отправлять их через входящие веб-ок или Office 365 соединителю.

## <a name="create-actionable-messages"></a>Создание actionable messages

Действия сообщений включают три видимые кнопки на карте. Каждая кнопка определяется в свойстве сообщения с помощью действий, каждая из которых имеет тип ввода, текстовое поле, выбор даты или список нескольких `potentialAction` `ActionCard` вариантов. Каждое `ActionCard` из них имеет связанное действие, например `HttpPOST` .

Карты соединители поддерживают следующие действия:

- `ActionCard`: Представляет один или несколько типов ввода и связанных действий.
- `HttpPOST`: Отправляет запрос POST на URL-адрес.
- `OpenUri`: Открывает URI в отдельном браузере или приложении, необязательно нацелены различные URL-адреса на основе операционных систем.

Действие `ActionCard` поддерживает три типа входных данных:

- `TextInput`: Одно строковое или многолинейное текстовое поле с необязательным ограничением длины.
- `DateInput`: Селектор даты с необязательным селектором времени.
- `MultichoiceInput`: Перечисляется список вариантов, предлагающих один выбор или несколько вариантов.

`MultichoiceInput` поддерживает свойство `style`, указывающее, отображается ли список изначально полностью развернутым. Значение по умолчанию `style` зависит от `isMultiSelect` значения:

| `isMultiSelect` | Значение `style` по умолчанию |
| --- | --- |
| `false` или не задано | `compact` |
| `true` | `expanded` |

Чтобы отобразить список multiselect в компактном стиле, необходимо указать оба `"isMultiSelect": true` и `"style": true` .

Дополнительные сведения о действиях карт соединители см. в см. в ["Действиях".](/outlook/actionable-messages/card-reference#actions)

> [!NOTE]
> * Значение `compact` для свойства `style` в Microsoft Teams равноценно значению `normal` для свойства `style` в Microsoft Outlook.
> * Для действия HttpPOST маркер носителя включается в запросы. Маркер содержит удостоверение Azure AD пользователя Office 365, выполнившего действие.

## <a name="send-a-message-through-incoming-webhook-or-office-365-connector"></a>Отправка сообщения через входящий веб-ок или Office 365 соединителю

Чтобы отправить сообщение через входящий веб-Office 365 соединитель, отправьте полезное сообщение JSON в URL-адрес веб-страницы. Эта нагрузка должна быть в виде Office 365 [соединители.](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)

Вы также можете использовать этот JSON для создания карт, содержащих богатые входные данные, такие как запись текста, многоцелевая или выбор даты и времени. Код, который создает карточку и публикует ее на URL-адрес веб-страницы, может работать на любой хост-службе. Эти карточки определяются как часть действий, а [](~/task-modules-and-cards/what-are-cards.md)также поддерживаются в картах, используемых в Teams ботах и расширениях обмена сообщениями.

### <a name="example-of-connector-message"></a>Пример сообщения соединитетеля

Пример сообщения соединители следующим образом:

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
            "target": "https://docs.microsoft.com/outlook/actionable-messages"
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
            "target": "https://docs.microsoft.com/outlook/actionable-messages"
        }]
    }, {
        "@type": "OpenUri",
        "name": "Learn More",
        "targets": [{
            "os": "default",
            "uri": "https://docs.microsoft.com/outlook/actionable-messages"
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
            "target": "https://docs.microsoft.com/outlook/actionable-messages"
        }]
    }]
}
```

Это сообщение содержит следующую карточку в канале:

![Снимок экрана карты соединители](~/assets/images/connectorcard.png)

## <a name="send-messages-using-curl-and-powershell"></a>Отправка сообщений с помощью cURL и PowerShell

# <a name="curl"></a>[cURL](#tab/cURL)

**Публикация сообщения в веб-сайте cURL**

1. Установка cURL с помощью: https://curl.haxx.se/ .

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
    > Если post успешно, вы должны увидеть простой **выход 1** `curl` по .

1. Проверьте Microsoft Teams клиента для новой карты.

# <a name="powershell"></a>[PowerShell](#tab/PowerShell)

 Обязательное условие: установка PowerShell и ознакомление с его базовым использованием.

**Публикация сообщения на веб-сайте с помощью PowerShell**

1. В командной строке PowerShell введите следующую команду:

   ```powershell
   Invoke-RestMethod -Method post -ContentType 'Application/Json' -Body '{"text":"Hello World!"}' -Uri <YOUR WEBHOOK URL>
   ```

    > [!NOTE]
    > Если post успешно, вы должны увидеть простой **выход 1** `Invoke-RestMethod` по .

1. Проверьте канал Microsoft Teams, связанный с URL-адресом веб-перехватчика. Вы можете увидеть новую карту, размещенную на канале. Прежде чем использовать соединители для тестирования или публикации приложения, необходимо сделать следующее:

    - [Включение двух значков](../../concepts/build-and-test/apps-package.md#app-icons).
    - Измените `icons` часть манифеста на имена файлов значков вместо URL-адресов.

---

## <a name="send-adaptive-cards-using-an-incoming-webhook"></a>Отправка адаптивных карт с помощью входящих веб-ок

> [!NOTE]
> * Все элементы схемы адаптивной карты, за `Action.Submit` исключением, полностью поддерживаются.
> * Поддерживаемые [**действия: Action.OpenURL,**](https://adaptivecards.io/explorer/Action.OpenUrl.html) [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html)и [**Action.ToggleVisibility.**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html)

**Отправка адаптивных карт через входящий веб-сайт**

1. [Настройка настраиваемой веб-страницы](~/webhooks-and-connectors/how-to/add-incoming-webhook.md) в Teams.
1. Создание файла JSON адаптивной карты с помощью следующего кода:

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

    Свойства файла Adaptive Card JSON:

    * Поле `"type"` должно иметь значение `"message"`.
    * Массив `"attachments"` содержит набор объектов card.
    * Поле `"contentType"` должно быть настроено на тип адаптивной карты.
    * Объект `"content"` — это карточка, отформатированная в JSON.

1. Проверьте адаптивную карту с помощью почтальонов:

    * Проверьте адаптивную карту с помощью [postman](https://www.postman.com) для отправки запроса POST на URL-адрес, созданный для создания входящих веб-ок.
    * Вклеить файл JSON в тело запроса и просмотреть сообщение адаптивной карты в Teams.

> [!TIP]
> Используйте образцы и [шаблоны](https://adaptivecards.io/samples) кода адаптивной карты для проверки тела запроса POST.

## <a name="rate-limiting-for-connectors"></a>Ограничение скорости для соединителей

Ограничения скорости приложений контролируют трафик, который может создавать соединителя или входящий веб-ок на канале. Teams отслеживать запросы с помощью окна фиксированной скорости и инкрементного счетчика, измеряемой в секундах. Если за секунду будет выполнено более четырех запросов, подключение клиента будет отлажено до тех пор, пока окно не обновит срок действия фиксированной скорости.

### <a name="transactions-per-second-thresholds"></a>Пороговые значения количества транзакций в секунду

В следующей таблице данная статья содержит сведения о транзакциях, основанных на времени:

| Время в секундах  | Максимальное разрешенное количество запросов  |
|---|---|
| 1   | 4   |  
| 30   | 60  |  
| 3600   | 100  |
| 7200 | 150  |
| 86400  | 1800  |

Логика повторной работы с [экспоненциальным](/azure/architecture/patterns/retry) отсевом может уменьшить ограничение скорости для случаев, когда запросы превышают ограничения в течение секунды. Следуйте [лучшим практикам,](../../bots/how-to/rate-limit.md) чтобы не ударить по ограничениям скорости.

> [!NOTE]
> Логика повторной работы с [экспоненциальным](/azure/architecture/patterns/retry) отсевом может уменьшить ограничение скорости для случаев, когда запросы превышают ограничения в течение секунды. См. за [откликами HTTP 429](../../bots/how-to/rate-limit.md#handle-http-429-responses), чтобы не достигать ограничений по скорости.

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

Эти ограничения имеются для уменьшения нежелательной почты канала соединитетелем и обеспечения оптимального опытом для пользователей.

## <a name="see-also"></a>См. также

* [Office 365 Соединители для Microsoft Teams](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [Создание входящих веб-ок](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [Создание исходятого веб-окка](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)
