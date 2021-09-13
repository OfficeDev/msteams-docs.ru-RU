---
title: Использование модулей задач в Microsoft Teams ботах
description: Использование модулей задач с Microsoft Teams ботами, включая карты Bot Framework, адаптивные карты и глубокие ссылки.
ms.localizationpriority: medium
ms.topic: how-to
keywords: модули задач групп ботов
ms.openlocfilehash: a548f0d0ae3853f447ba55409bf9edbecced4e60
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/12/2021
ms.locfileid: "59157580"
---
# <a name="use-task-modules-from-bots"></a>Использование модулей задач из ботов

Модули задач могут вызываться из Microsoft Teams с помощью кнопок на картах Adaptive Cards и Bot Framework, которые является героем, эскизом и Office 365 соединителю. Модули задач часто являются более удобными для пользователей, чем несколько этапов беседы. Отслеживайте состояние бота и разрешите пользователю прерывать или отменять последовательность.

Существует два способа ссылки на модули задач:

* Новый вид сообщения вызова: динамически извлекается из бота действие карты для карт Bot Framework или действие карты для адаптивных карт с url-адресом или адаптивной `task/fetch` `invoke` [](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke) `Action.Submit` [](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) `task/fetch` картой.
* URL-адреса глубоких ссылок. Используя синтаксис глубокой ссылки для модулей [задач,](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-deep-link-syntax)вы можете использовать действие карты для карт Bot Framework или действие карты для адаптивных карт `openUrl` [](~/task-modules-and-cards/cards/cards-actions.md#action-type-openurl) `Action.OpenUrl` [](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) соответственно. С url-адресами глубоких ссылок URL-адрес модуля задач или корпус адаптивной карты уже известен, чтобы избежать обратного пути сервера по отношению к `task/fetch` .

> [!IMPORTANT]
> Каждый `url` из них должен реализовать протокол `fallbackUrl` шифрования HTTPS.

В следующем разделе приводится подробная информация об отзове модуля задач с помощью `task/fetch` .

## <a name="invoke-a-task-module-using-taskfetch"></a>Вызов модуля задач с помощью задачи/извлечение

Когда объект действия карты или инициализирован и когда пользователь выбирает кнопку, сообщение `value` `invoke` `Action.Submit` `invoke` отправляется боту. В ответе HTTP на сообщение в объекте оболочки встроен объект `invoke` [TaskInfo,](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) который Teams для отображения модуля задач.

![запрос или ответ на задачу/извлечение](~/assets/images/task-module/task-module-invoke-request-response.png)

Следующие действия предоставляют модуль задач вызова с помощью задачи/извлечение:

1. На этом изображении показана карта героя Bot Framework с действием **Buy** `invoke` [card.](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke) Значение свойства `type` и `task/fetch` остальной объект `value` может быть по вашему выбору.
1. Бот получает сообщение `invoke` HTTP POST.
1. Бот создает объект отклика и возвращает его в тело ответа POST с кодом ответа HTTP 200. Дополнительные сведения о схеме ответов см. в обсуждении [задачи/отправки.](#the-flexibility-of-tasksubmit) В следующем коде приводится пример корпуса ответа HTTP, содержашего объект [TaskInfo,](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) встроенный в объект оболочки:

    ```json
    {
      "task": {
        "type": "continue",
        "value": {
          "title": "Task module title",
          "height": 500,
          "width": "medium",
          "url": "https://contoso.com/msteams/taskmodules/newcustomer",
          "fallbackUrl": "https://contoso.com/msteams/taskmodules/newcustomer"
        }
      }
    }
    ```

    Событие и его ответ для ботов аналогичны функции `task/fetch` `microsoftTeams.tasks.startTask()` в клиентской SDK.

1. Microsoft Teams отображает модуль задач.

В следующем разделе представлены сведения о отправке результатов модуля задач.

## <a name="submit-the-result-of-a-task-module"></a>Отправка результатов модуля задач

Когда пользователь завершает работу с модулем задач, отправка результата обратно боту аналогична тому, как он работает со вкладками. Дополнительные сведения [см. в примере отправки результатов модуля задач.](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-of-submitting-the-result-of-a-task-module) Существует несколько различий:

* HTML или JavaScript. После проверки того, что ввел пользователь, вы вызываем функцию SDK, названную далее как для целей `TaskInfo.url` `microsoftTeams.tasks.submitTask()` `submitTask()` читаемости. Вы можете позвонить без параметров, если Teams закрыть модуль задач, но необходимо передать объект или строку `submitTask()` в `submitHandler` ваш . Передай его в качестве первого `result` параметра. Teams вызывает , является и является объектом или строкой, которую `submitHandler` `err` вы `null` `result` передали `submitTask()` . Если вы `submitTask()` звоните с `result` параметром, необходимо передать или массив `appId` `appId` строк. Это позволяет Teams, что приложение, отправляя результат, является тем же, что вызывалось в модуль задач. Ваш бот получает `task/submit` сообщение, в том числе `result` . Дополнительные сведения см. [в тексте полезной нагрузки `task/fetch` и `task/submit` сообщений.](#payload-of-taskfetch-and-tasksubmit-messages)
* Адаптивная карточка, которая является . Тело адаптивной карты, заполненное пользователем, отправляется боту через сообщение, когда пользователь выбирает `TaskInfo.card` `task/submit` любую `Action.Submit` кнопку.

В следующем разделе приводится подробная информация о гибкости `task/submit` .

## <a name="the-flexibility-of-tasksubmit"></a>Гибкость задачи/отправки

Когда пользователь завершает работу с модулем задач, вызываемой с бота, бот всегда получает `task/submit invoke` сообщение. При ответе на сообщение у вас есть несколько `task/submit` вариантов:

| Http body response                      | Сценарий                                |
| --------------------------------------- | --------------------------------------- |
| Никто не игнорирует `task/submit` сообщение | Самый простой ответ — это отсутствие ответа. Ваш бот не обязан отвечать, когда пользователь завершает работу с модулем задач. |
| <pre>{<br/>  "task": {<br/>    "type": "message",<br/>    "value": "Message text"<br/>  }<br/>}</pre> | Teams отображает значение в `value` всплывающее окно сообщений. |
| <pre>{<br/>  "task": {<br/>    "type": "continue",<br/>    "value": &lt;TaskInfo object&gt;<br/>  }<br/>}</pre> | Позволяет сцеплять последовательности адаптивных карт в мастере или многошаговом опытом. |

> [!NOTE]
> Цепочка адаптивных карт в последовательность — это расширенный сценарий. Пример Node.js поддерживает его. Дополнительные сведения см. [в Microsoft Teams модуля задач Node.js. ](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)

В следующем разделе приводится подробная информация о полезной нагрузке `task/fetch` `task/submit` и сообщениях.

## <a name="payload-of-taskfetch-and-tasksubmit-messages"></a>Полезное количество задач/извлечений и задач/отправки сообщений

В этом разделе определяется схема получения ботом объекта `task/fetch` `task/submit` или объекта Bot `Activity` Framework. Следующая таблица содержит свойства полезной нагрузки `task/fetch` и `task/submit` сообщений:

| Свойство | Описание                          |
| -------- | ------------------------------------ |
| `type`   | Всегда `invoke` .           |
| `name`   | Является либо `task/fetch` `task/submit` или . |
| `value`  | Является ли полезной нагрузка, определяемая разработчиком. Структура объекта такая же, как и то, что отправляется из `value` Teams. Однако в этом случае все по-другому. Она требует поддержки динамических извлечений, как из Bot Framework, то есть, так и из действий `task/fetch` `value` адаптивной `Action.Submit` карты, то есть `data` . Кроме того, что включено или включено в Teams, требуется способ связи Teams с `context` `value` `data` ботом.<br/><br/>Объединяйте значение и "данные" в родительский объект:<br/><br/><pre>{<br/>  "context": {<br/>    "theme": "default" &vert; "dark" &vert; "contrast",<br/>  },<br/>  "data": [value field from Bot Framework card] &vert; [data field from Adaptive Card] <br/>}</pre>  |

В следующем разделе приводится пример получения и ответа на сообщения в `task/fetch` `task/submit` Node.js.

## <a name="example-of-taskfetch-and-tasksubmit-invoke-messages-in-nodejs-and-c"></a>Пример задач/извлечений и задач/отправки ссылок на сообщения в Node.js и C #

# <a name="nodejs"></a>[Node.js](#tab/nodejs)

```typescript
handleTeamsTaskModuleFetch(context, taskModuleRequest) {
    // Called when the user selects an options from the displayed HeroCard or
    // AdaptiveCard.  The result is the action to perform.

    const cardTaskFetchValue = taskModuleRequest.data.data;
    var taskInfo = {}; // TaskModuleTaskInfo

    if (cardTaskFetchValue === TaskModuleIds.YouTube) {
        // Display the YouTube.html page
        taskInfo.url = taskInfo.fallbackUrl = this.baseUrl + '/' + TaskModuleIds.YouTube + '.html';
        this.setTaskInfo(taskInfo, TaskModuleUIConstants.YouTube);
    } else if (cardTaskFetchValue === TaskModuleIds.CustomForm) {
        // Display the CustomForm.html page, and post the form data back via
        // handleTeamsTaskModuleSubmit.
        taskInfo.url = taskInfo.fallbackUrl = this.baseUrl + '/' + TaskModuleIds.CustomForm + '.html';
        this.setTaskInfo(taskInfo, TaskModuleUIConstants.CustomForm);
    } else if (cardTaskFetchValue === TaskModuleIds.AdaptiveCard) {
        // Display an AdaptiveCard to prompt user for text, and post it back via
        // handleTeamsTaskModuleSubmit.
        taskInfo.card = this.createAdaptiveCardAttachment();
        this.setTaskInfo(taskInfo, TaskModuleUIConstants.AdaptiveCard);
    }

    return TaskModuleResponseFactory.toTaskModuleResponse(taskInfo);
}

async handleTeamsTaskModuleSubmit(context, taskModuleRequest) {
    // Called when data is being returned from the selected option (see `handleTeamsTaskModuleFetch').

    // Echo the users input back.  In a production bot, this is where you'd add behavior in
    // response to the input.
    await context.sendActivity(MessageFactory.text('handleTeamsTaskModuleSubmit: ' + JSON.stringify(taskModuleRequest.data)));

    // Return TaskModuleResponse
    return {
        // TaskModuleMessageResponse
        task: {
            type: 'message',
            value: 'Thanks!'
        }
    };
}

setTaskInfo(taskInfo, uiSettings) {
    taskInfo.height = uiSettings.height;
    taskInfo.width = uiSettings.width;
    taskInfo.title = uiSettings.title;
}
```

# <a name="c"></a>[C#](#tab/csharp)

```csharp
protected override Task<TaskModuleResponse> OnTeamsTaskModuleFetchAsync(ITurnContext<IInvokeActivity> turnContext, TaskModuleRequest taskModuleRequest, CancellationToken cancellationToken)
{
    var asJobject = JObject.FromObject(taskModuleRequest.Data);
    var value = asJobject.ToObject<CardTaskFetchValue<string>>()?.Data;

    var taskInfo = new TaskModuleTaskInfo();
    switch (value)
    {
        case TaskModuleIds.YouTube:
            taskInfo.Url = taskInfo.FallbackUrl = _baseUrl + "/" + TaskModuleIds.YouTube;
            SetTaskInfo(taskInfo, TaskModuleUIConstants.YouTube);
            break;
        case TaskModuleIds.CustomForm:
            taskInfo.Url = taskInfo.FallbackUrl = _baseUrl + "/" + TaskModuleIds.CustomForm;
            SetTaskInfo(taskInfo, TaskModuleUIConstants.CustomForm);
            break;
        case TaskModuleIds.AdaptiveCard:
            taskInfo.Card = CreateAdaptiveCardAttachment();
            SetTaskInfo(taskInfo, TaskModuleUIConstants.AdaptiveCard);
            break;
        default:
            break;
    }

    return Task.FromResult(taskInfo.ToTaskModuleResponse());
}

protected override async Task<TaskModuleResponse> OnTeamsTaskModuleSubmitAsync(ITurnContext<IInvokeActivity> turnContext, TaskModuleRequest taskModuleRequest, CancellationToken cancellationToken)
{
    var reply = MessageFactory.Text("OnTeamsTaskModuleSubmitAsync Value: " + JsonConvert.SerializeObject(taskModuleRequest));
    await turnContext.SendActivityAsync(reply, cancellationToken);

    return TaskModuleResponseFactory.CreateResponse("Thanks!");
}

private static void SetTaskInfo(TaskModuleTaskInfo taskInfo, UISettings uIConstants)
{
    taskInfo.Height = uIConstants.Height;
    taskInfo.Width = uIConstants.Width;
    taskInfo.Title = uIConstants.Title.ToString();
}
```

---

### <a name="bot-framework-card-actions-vs-adaptive-card-actionsubmit-actions"></a>Действия карты Bot Framework против действий адаптивной карты.Отправка действий

Схема действий карты Bot Framework отличается от действий адаптивной карты, а способ вызова модулей задач также `Action.Submit` отличается. Объект содержит объект, чтобы он не мешал другим `data` `Action.Submit` `msteams` свойствам карты. В следующей таблице показан пример каждого действия карты:

| Действие карты Bot Framework                              | Действие адаптивной карты.Отправка действия                     |
| ------------------------------------------------------ | ------------------------------------------------------ |
| <pre>{<br/>  "type": "invoke",<br/>  "title": "Buy",<br/>  "value": {<br/>    "type": "task/fetch",<br/>    &lt;...&gt;<br/>  }<br/>}</pre> | <pre>{<br/>  "type": "Action.Submit",<br/>  "id": "btnBuy",<br/>  "title": "Buy",<br/>  "data": {<br/>    &lt;...&gt;,<br/>    "msteams": {<br/>      "type": "task/fetch"<br/>    }<br/>  }<br/>}</pre>  |

## <a name="code-sample"></a>Пример кода

|Название примера | Описание | .NET | Node.js|
|----------------|-----------------|--------------|----------------|
|Пример модуля задач bots-V4 | Примеры для создания модулей задач. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/54.teams-task-module)|[Просмотр](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/54.teams-task-module)|

## <a name="see-also"></a>Дополнительные ресурсы

* [Microsoft Teams пример кода модуля задач в Node.js](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs/blob/master/src/TeamsBot.ts)
* [Примеры Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)
