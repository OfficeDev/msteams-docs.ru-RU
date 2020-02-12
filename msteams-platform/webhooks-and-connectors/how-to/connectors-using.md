---
title: Отправка сообщений соединителям и веб-перехватчикам
description: Сведения о том, как использовать Соединители Office 365 в Microsoft Teams.
localization_priority: Priority
keywords: соединитель teams o365
ms.openlocfilehash: 56ef6adc7731eadc0a799f489867d8e056248e03
ms.sourcegitcommit: 060b486c38b72a3e6b63b4d617b759174082a508
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/12/2020
ms.locfileid: "41953469"
---
# <a name="sending-messages-to-connectors-and-webhooks"></a>Отправка сообщений соединителям и веб-перехватчикам

Чтобы отправить сообщение через соединитель Office 365 или входящий веб-перехватчик, необходимо отправить полезные данные JSON на URL-адрес веб-перехватчика. Как правило, эти полезные данные будут отображаться в [форме карточки соединителя Office 365](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).

С помощью этого кода JSON также можно создавать карточки с различными элементами для ввода данных, например текстовыми полями, переключателями множественного выбора или средствами выбора даты и времени. Код, генерирующий карточку и отправляющий ее на URL-адрес веб-перехватчика, может выполняться в любой размещенной службе. Эти карточки определяются в составе сообщений с действиями, а также поддерживаются в [карточках](~/task-modules-and-cards/what-are-cards.md), используемых ботами Teams и расширениями для обмена сообщениями.

### <a name="example-connector-message"></a>Пример сообщения соединителя

```json
{
    "@type": "MessageCard",
    "@context": "http://schema.org/extensions",
    "themeColor": "0076D7",
    "summary": "Larry Bryant created a new task",
    "sections": [{
        "activityTitle": "![TestImage](https://47a92947.ngrok.io/Content/Images/default.png)Larry Bryant created a new task",
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
            "target": "http://..."
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
            "target": "http://..."
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
            "target": "http://..."
        }]
    }]
}
```

Это сообщение создает на канале представленную ниже карточку.

![Снимок экрана с карточкой соединителя](~/assets/images/connectors/connector_message.png)

## <a name="creating-actionable-messages"></a>Создание сообщений с действиями

В примере карточки из предыдущего раздела отображаются три кнопки. Каждая кнопка определена в свойстве `potentialAction` сообщения с помощью действий `ActionCard`, каждое из которых содержит тип элемента ввода: текстовое поле, элемент управления "Выбор даты" или список с возможностью выбора нескольких вариантов. С каждым действием `ActionCard` связано другое действие, например `HttpPOST`.

Карточки соединителей поддерживают действия трех типов:

- `ActionCard`: представляет один или несколько типов входных данных и соответствующие действия;
- `HttpPOST`: отправляет запрос POST на URL-адрес;
- `OpenUri`: открывает URI в отдельном браузере или приложении; при необходимости ссылается на разные URI в зависимости от операционной системы.

(Четвертое действие, `ViewAction`, также поддерживается, но больше не требуется. Используйте вместо него действие `OpenUri`.)

Действие `ActionCard` поддерживает три типа входных данных:

- `TextInput`: однострочное или многострочное текстовое поле с необязательным ограничением длины;
- `DateInput`: средство выбора даты с необязательным выбором времени;
- `MultichoiceInput`: нумерованный список вариантов с возможностью выбора одного или нескольких пунктов;

`MultichoiceInput` поддерживает свойство `style`, указывающее, отображается ли список изначально полностью развернутым. Значение `style` по умолчанию зависит от значения `isMultiSelect`.

| `isMultiSelect` | Значение `style` по умолчанию |
| --- | --- |
| `false` или не задано | `compact` |
| `true` | `expanded` |

Если вам нужно, чтобы список со множественным выбором изначально отображался в компактном стиле, необходимо задать значения `"isMultiSelect": true` и `"style": true`.

> [!NOTE]
> Значение `compact` для свойства `style` в Microsoft Teams равноценно значению `normal` для свойства `style` в Microsoft Outlook.

Все остальные сведения о действиях карточек соединителей представлены в разделе **[Действия](/outlook/actionable-messages/card-reference#actions)** справки по карточкам сообщений с действиями.

## <a name="setting-up-a-custom-incoming-webhook"></a>Настройка пользовательского входящего веб-перехватчика

Выполните указанные ниже действия, чтобы отправить простую карточку в соединитель.

1. В Microsoft Teams нажмите **Дополнительные параметры** (**&#8943;**) рядом с названием канала и выберите **Соединители**.
2. Прокрутите список соединителей до пункта **Входящий веб-перехватчик** и нажмите кнопку **Добавить**.
3. Введите имя веб-перехватчика, отправьте изображение, которое следует связать с данными от веб-перехватчика, и нажмите кнопку **Создать**.
4. Скопируйте веб-перехватчик в буфер обмена и сохраните его. Для отправки информации в Microsoft Teams вам потребуется URL-адрес веб-перехватчика.
5. Нажмите кнопку **Готово**.

### <a name="post-a-message-to-the-webhook-using-curl"></a>Отправка сообщения веб-перехватчику с помощью cURL

Для выполнения описанных ниже действий используется [cURL](https://curl.haxx.se/). Предполагается, что у вас уже установлена эта программа, а вы знакомы с основами ее использования.

1. Введите в командной строке следующую команду cURL:

   ```bash
   curl -H "Content-Type: application/json" -d "{\"text\": \"Hello World\"}" <YOUR WEBHOOK URL>
   ```

2. В случае успешного выполнения запроса POST команда `curl` должна возвращать простой отклик **1**.
3. Проверьте клиент Microsoft Teams. Вы увидите новую карточку, опубликованную в группе.

### <a name="post-a-message-to-the-webhook-using-powershell"></a>Отправка сообщения веб-перехватчику с помощью PowerShell

Для выполнения описанных ниже действий используется PowerShell. Предполагается, что у вас уже установлена эта программа, а вы знакомы с основами ее использования.

1. В командной строке PowerShell введите следующую команду:

   ```powershell
   Invoke-RestMethod -Method post -ContentType 'Application/Json' -Body '{"text":"Hello World!"}' -Uri <YOUR WEBHOOK URL>
   ```

2. В случае успешного выполнения запроса POST команда `Invoke-RestMethod` должна возвращать простой отклик **1**.
3. Проверьте канал Microsoft Teams, связанный с URL-адресом веб-перехватчика. На канале должна появиться новая карточка.

- Включите два значка, следуя инструкциям из раздела [Значки](~/concepts/build-and-test/apps-package.md#icons).
- Измените раздел `icons` манифеста, чтобы он ссылался на имена файлов значков, а не на их URL-адреса.

Приведенный ниже файл manifest.json содержит основные элементы, необходимые для тестирования и отправки приложения.

> [!NOTE]
> Замените `id` и `connectorId` в приведенном ниже примере на GUID соединителя.

#### <a name="example-manifestjson-with-connector"></a>Пример manifest.json с соединителем

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "id": "e9343a03-0a5e-4c1f-95a8-263a565505a5",
  "version": "1.0",
  "packageName": "com.sampleapp",
  "developer": {
    "name": "Publisher",
    "websiteUrl": "https://www.microsoft.com",
    "privacyUrl": "https://www.microsoft.com",
    "termsOfUseUrl": "https://www.microsoft.com"
  },
  "description": {
    "full": "This is a small sample app we made for you! This app has samples of all capabilities Microsoft Teams supports.",
    "short": "This is a small sample app we made for you!"
  },
  "icons": {
    "outline": "sampleapp-outline.png",
    "color": "sampleapp-color.png"
  },
  "connectors": [
    {
      "connectorId": "e9343a03-0a5e-4c1f-95a8-263a565505a5",
      "scopes": [
        "team"
      ]
    }
  ],
  "name": {
    "short": "Sample App",
    "full": "Sample App"
  },
  "accentColor": "#FFFFFF",
  "needsIdentity": "true"
}
```

## <a name="testing-your-connector"></a>Тестирование соединителя

Чтобы тестировать соединитель, отправьте его команде, как в любом другом приложении. Вы можете создать ZIP-пакет, используя файл манифеста с панели администрирования для разработчиков соединителей (измененный согласно инструкциям из предыдущего раздела) и два файла значков.

После отправки приложения откройте список соединителей с любого канала. Прокрутите вниз, чтобы найти свое приложение в разделе **Отправленные**.

![Снимок экрана раздела отправленных приложений в диалоговом окне соединителя](~/assets/images/connectors/connector_dialog_uploaded.png)

Теперь можно запустить среду настройки. Обратите внимание, что этот процесс полностью выполняется в Microsoft Teams во всплывающем окне. В настоящее время он отличается от процесса настройки в созданных нами соединителях. Мы работаем над согласованием этих процессов.

Чтобы убедиться в правильной работе действия `HttpPOST`, используйте [пользовательский входящий веб-перехватчик](#setting-up-a-custom-incoming-webhook).

## <a name="rate-limiting-for-connectors"></a>Ограничение скорости для соединителей

Ограничения скорости приложений управляют трафиком, который разрешено создавать в канале соединителю или входящему веб-перехватчику. В Teams запросы отслеживаются с помощью окна фиксированной скорости и инкрементного счетчика с измерением в секундах.  При наличии слишком большого количества запросов скорость подключения клиента будет ограничена до обновления окна, т. е. в течение длительности окна фиксированной скорости.

### <a name="transactions-per-second-thresholds"></a>**Пороговые значения количества транзакций в секунду**

| Время (секунды)  | Максимальное разрешенное количество запросов  |
|---|---|
| 1   | 4  |  
| 30   | 60  |  
| 3600   | 100  |
| 7200 | 150  |
| 86 400  | 1800  |

*Также см. * [Соединители Office 365 — Microsoft Teams](https://docs.microsoft.com/connectors/teams/)

[Логика повторных попыток с экспоненциальной задержкой](/azure/architecture/patterns/retry), подобная приведенной ниже, поможет избежать ограничения скорости в тех случаях, когда число запросов за секунду превышает пределы. Следуйте [рекомендациям](../../bots/how-to/rate-limit.md#best-practices), чтобы предотвратить достижение пределов скорости.

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
