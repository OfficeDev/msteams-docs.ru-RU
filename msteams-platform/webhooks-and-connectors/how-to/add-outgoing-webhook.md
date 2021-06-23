---
title: Добавление пользовательских ботов в Microsoft Teams с исходяшими веб-оками
description: описывает, как добавить исходяющий веб-сайт
ms.topic: conceptual
ms.author: lajanuar
localization_priority: Normal
keywords: teams tabs outgoing webhook actionable message verify webhook
ms.openlocfilehash: 2fac6f42e27a4c8cb3d079ea281d458a4dfe41ed
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069178"
---
# <a name="add-custom-bots-to-teams-with-outgoing-webhooks"></a>Добавление пользовательских ботов в Teams с исходяшими веб-оками

## <a name="outgoing-webhooks-in-teams"></a>Исходяние веб-сайтов в Teams

Webhooks — это выдающийся способ интеграции Teams с внешними приложениями. Веб-ок — это, по сути, запрос POST, отправленный на URL-адрес вызова. Исходяющие веб-оки позволяют пользователям отправлять сообщения на веб-службу без полного процесса создания ботов с [помощью Microsoft Bot Framework](https://dev.botframework.com/).

Исходяющий веб-сайт отправляет данные Teams любой выбранной службе, способной принимать полезной нагрузки JSON. После добавления исходяющих веб-ок в команду он выступает в качестве бота и ищет сообщения в каналах с помощью **\@ упоминания**. Он отправляет уведомления внешним веб-службам и отвечает богатыми сообщениями, в том числе карточками и изображениями.

## <a name="outgoing-webhook-key-features"></a>Исходяние ключевых функций веб-сайта

| Возможность | Описание |
| ------- | ----------- |
| Конфигурация scoped| Webhooks имеют область действия на уровне группы. Необходимо пройти процесс настройки для каждой команды, в которой необходимо добавить исходяющий веб-сайт. |
| Реактивное сообщение| Пользователи должны использовать @mention для получения сообщений для веб-пользователя. В настоящее время пользователи могут отправлять сообщения об исходяшем веб-сайте только в общедоступных каналах, а не в личной или частной области. |
|Стандартный обмен сообщениями HTTP|Ответы отображаются в той же цепочке, что и исходное сообщение запроса, и могут включать любое содержимое сообщений в рамках бота, например богатый текст, изображения, карты и эмодзи. Несмотря на то, что исходяющие веб-пользователи могут использовать карты, они не могут использовать любые действия карт, за исключением `openURL` .|
| Teams Поддержка метода API|Исходяющий веб-сайт отправляет HTTP POST веб-службе и обрабатывает ответ обратно. Они не могут получить доступ к другим API, таким как извлечение списка или списка каналов в команде.|

## <a name="creating-actionable-messages"></a>Создание сообщений с действиями

Карты соединители включают три видимые кнопки на карте. Каждая кнопка определяется в `potentialAction` свойстве сообщения с помощью `ActionCard` действий. Каждый из них содержит тип ввода, текстовое поле, выбор даты `ActionCard` или список с несколькими вариантами выбора. Каждое `ActionCard` действие имеет связанное действие, `HttpPOST` например.

Карточки соединителей поддерживают действия трех типов:

| Действие | Описание |
| ------- | ----------- |
| `ActionCard` |Представляет один или несколько типов ввода и связанные действия.|
| `HttpPOST` | Отправляет запрос POST на URL-адрес. |
| `OpenUri` |  Открывает URI в отдельном браузере или приложении, необязательно нацелив различные URL-адреса на основе операционных систем.|

Действие `ActionCard` поддерживает три типа входных данных:

| Тип ввода | Описание |
| ------- | ----------- |
| `TextInput` | Однострочная или многострочная текстовая область с необязательным ограничением длины. |
| `DateInput` | Селектор даты с необязательным селектором времени. |
| `MultichoiceInput` | Указанный список вариантов, предлагающий один выбор или несколько вариантов.|

`MultichoiceInput` поддерживает `style` свойство, которое управляет отображением полного расширенного списка. Значение по умолчанию `style` зависит от `isMultiSelect` значения.

| `isMultiSelect` значение  | `style` Значение по умолчанию  |
| --- | --- |
| `false` или не задано | Стиль по умолчанию `compact`|
| `true` | Стиль по умолчанию `expanded` |

> [!NOTE]
> * Введите как и , если вы хотите, чтобы список с несколькими `"isMultiSelect": true` `"style": true` выборами отображался в компактном стиле.
> * Выбор свойства в Teams то же самое, что и выбор свойства в `compact` `style` Microsoft `normal` `style` Outlook.
> * Веб-сайты поддерживают только Office 365 и адаптивные карточки.

Другие сведения о действиях карт соединители см. в справке **[Действия](/outlook/actionable-messages/card-reference#actions)** в справочной карточке сообщения.

## <a name="adding-outgoing-webhooks-to-your-app"></a>Добавление исходяющих веб-ок в приложение

**Сценарий.** Нажмите уведомления об изменении состояния на сервере Teams канала в приложение.  
**Пример.** У вас есть бизнес-приложение, которое отслеживает все операции CRUD, сделанные для записей сотрудников Teams пользователей отдела кадров канала через Office 365 аренды.

### <a name="1-create-a-url-on-your-apps-server-to-accept-and-process-a-post-request-with-a-json-payload"></a>1. Создайте URL-адрес на сервере приложения, чтобы принять и обработать запрос POST с полезной нагрузкой JSON

Ваша служба получает сообщения в стандартной схеме обмена сообщениями службы ботов Azure. Соединитель платформы ботов — это служба RESTful, которая позволяет вашей службе обрабатывать обмен отформатированными сообщениями JSON с помощью протоколов HTTPS, как описано в [API службы Azure Bot.](/bot-framework/rest-api/bot-framework-rest-connector-api-reference) Кроме того, вы можете следовать [Microsoft Bot Framework SDK] для обработки и размыва сообщений. См. также [о службе ботов Azure.](/azure/bot-service/bot-service-overview-introduction)


Исходяющие веб-окки имеют область действия до уровня и видны `team` всем участникам группы. Так же, как и **\@** бот, пользователям необходимо упомянуть имя исходятого веб-пользователя, чтобы вызвать его в канале.

### <a name="2-create-a-method-to-verify-the-outgoing-webhook-hmac-token"></a>2. Создайте метод проверки исходятого маркера HMAC веб-ок

#### <a name="hmac-signature-for-testing-with-code-example"></a>Подпись HMAC для тестирования с помощью примера кода

Использование примера входящие сообщения и id: "contoso" signingKeyDictionary {"contoso", "vqF0En+Z0ucuRTM/01o2GuhHH3hKKk/N2bOmlM31zaA=" }.

Используйте значение "HMAC 03TCao0i55H1eVKUusZOTZRjtvYTs+mO41mPL+R1e1U=" в авторизации загона запроса.

Чтобы убедиться, что служба получает вызовы только от Teams клиентов, Teams код HMAC в заговорке `hmac` HTTP. Всегда включал код в протокол проверки подлинности.

Код всегда должен проверять подпись HMAC, включенную в запрос:

* Создание маркера HMAC из тела запроса сообщения. Для этого на большинстве платформ существуют стандартные библиотеки (см. в Node.js [Crypto](https://nodejs.org/api/crypto.html#crypto_crypto) или [Teams Webhook Sample](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs) for \# C). Microsoft Teams использует стандартную криптографию HMAC SHA256. Необходимо преобразовать тело в массив byte в UTF8.
* Вычисляйте хаш из массива byte  маркера безопасности, предоставляемого Teams при регистрации исходяшего веб-окка в Teams клиенте]. См. [статью Создать исходяющий веб-сайт](#create-an-outgoing-webhook).
* Преобразование hash в строку с помощью кодификации UTF-8.
* Сравните строковую величину сгенерированного hash со значением, заданным в запросе HTTP.

### <a name="3-create-a-method-to-send-a-success-or-failure-response"></a>3. Создайте метод для отправки ответа на ошибку или успешность

Ответы из исходяющих веб-сайтов отображаются в той же цепочке ответов, что и исходное сообщение. Когда пользователь выполняет запрос, Microsoft Teams выполняет синхронный http-запрос в службу, и код получает пять секунд для ответа на сообщение до времени и прекращения подключения.

### <a name="example-response"></a>Пример отклика

```json
{
    "type": "message",
    "text": "This is a reply!"
}
```

> [!NOTE]
> * Вы можете отправлять адаптивную карту, карточку героя и текстовые сообщения в виде вложений с исходяшим веб-сайтом.
> * Форматирование поддержки карт. Дополнительные сведения см. в [виде карт формата с разметками.](~/task-modules-and-cards/cards/cards-format.md?tabs=adaptive-md%2Cconnector-html#formatting-cards-with-markdown)

Ниже приводится пример ответа адаптивной карты:

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
string content = await this.Request.Content.ReadAsStringAsync();
Activity incomingActivity = JsonConvert.DeserializeObject<Activity>(content);

var Card = new AdaptiveCard(new AdaptiveSchemaVersion("1.4"))
{
    Body = new List<AdaptiveElement>()
    {
        new AdaptiveTextBlock(){Text= $"Request sent by: {incomingActivity.From.Name}"},
        new AdaptiveImage(){Url=new Uri("https://c.s-microsoft.com/en-us/CMSImages/DesktopContent-04_UPDATED.png?version=43c80870-99dd-7fb1-48c0-59aced085ab6")},
        new AdaptiveTextBlock(){Text="Sample image for Adaptive Card.."}
    }
};

var attachment = new Attachment()
{
    ContentType = AdaptiveCard.ContentType,
    Content = Card
};

var sampleResponseActivity = new Activity
{
    Attachments = new [] { attachment }
};

return sampleResponseActivity;
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
var receivedMsg = JSON.parse(payload);
var responseMsg = JSON.stringify({
    "type": "message",
    "attachments": [
        {
            "contentType": "application/vnd.microsoft.card.adaptive",
            "contentUrl": null,
            "content": {
                "type": "AdaptiveCard",
                "version": "1.4",
                "body": [
                    {
                        "type": "TextBlock",
                        "text": "Request sent by: " + receivedMsg.from.name
                    },
                    {
                        "type": "Image",
                        "url": "https://c.s-microsoft.com/en-us/CMSImages/DesktopContent-04_UPDATED.png?version=43c80870-99dd-7fb1-48c0-59aced085ab6"
                    },
                    {
                        "type": "TextBlock",
                        "text": "Sample image for Adaptive Card."
                    }
                ]
            },
            "name": null,
            "thumbnailUrl": null
        }
    ]
});
```

# <a name="json"></a>[JSON](#tab/json)

```json
{
    "type": "message",
    "attachments": [
        {
            "contentType": "application/vnd.microsoft.card.adaptive",
            "content": {
                "type": "AdaptiveCard",
                "version": "1.4",
                "body": [
                    {
                        "type": "TextBlock",
                        "text": "Request sent by: Megan"
                    },
                    {
                        "type": "Image",
                        "url": "https://c.s-microsoft.com/en-us/CMSImages/DesktopContent-04_UPDATED.png?version=43c80870-99dd-7fb1-48c0-59aced085ab6"
                    },
                    {
                        "type": "TextBlock",
                        "text": "Sample image for Adaptive Card.."
                    }
                ]
            }
        }
    ]
}
```

* * *

## <a name="create-an-outgoing-webhook"></a>Создание исходящего веб-перехватчика

1. Выберите соответствующую команду и выберите **команду Manage** из (&#8226;&#8226;&#8226;) выпадаемого меню.
1. Выберите **вкладку Apps** из панели навигации.
1. Из нижнего правого угла окна выберите **Создать исходяющий веб-сайт**.
1. В результате всплывающее окно выполните необходимые поля:

>* **Имя.** Название веб-страницы и @mention нажмите
>* **URL-адрес** вызова: конечная точка HTTPS, которая принимает полезной нагрузки JSON и получает запросы POST из Teams
>* **Описание.** Подробные строки, которые отображаются в карточке профиля и панели мониторинга приложений на уровне команды.
>* **Изображение профиля:** необязательный значок приложения для вашего веб-пользователя
>* Выберите **кнопку Создать** из нижнего правого угла всплывающее окно, а исходяющий веб-сайт добавляется в каналы текущей группы.
>* В следующем диалоговом окне отображается маркер безопасности кода проверки подлинности сообщений на основе хэширования [(HMAC),](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301) который используется для проверки подлинности вызовов между Teams и назначенной внешней службой.
>* Исходяющий веб-сайт доступен пользователям группы, только если URL-адрес действителен, а маркеры проверки подлинности сервера и клиента равны, например, рукопожатие HMAC.

## <a name="code-sample"></a>Пример кода
|**Пример имени** | **Описание** | **.NET** | **Node.js** |
|----------------|------------------|--------|----------------|
| Исходящие веб-перехватчики | Примеры создания **пользовательских ботов,** которые будут использоваться в Microsoft Teams.| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/nodejs)|

