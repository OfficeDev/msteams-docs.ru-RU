---
title: Использование модулей задач в Microsoft Teams ботов
description: Использование модулей задач с Microsoft Teams ботами, включая карточки Bot Framework, адаптивные карточки и прямые ссылки.
ms.localizationpriority: medium
ms.topic: how-to
keywords: адаптивная карточка с подробными ссылками в модулях задач teams
ms.openlocfilehash: 7391f7e0d9da444831b98b4b6b69a97b35298800
ms.sourcegitcommit: 3bfd0d2c4d83f306023adb45c8a3f829f7150b1d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/27/2022
ms.locfileid: "65073775"
---
# <a name="use-task-modules-from-bots"></a>Использование модулей задач из ботов

Модули задач можно вызывать из ботов Microsoft Teams с помощью кнопок на адаптивных карточках и карточках Bot Framework, которые — главный имиджевый баннер, эскиз и Office 365 Connector. Модули задач часто являются более эффективной процедурой взаимодействия с пользователем, чем несколько шагов беседы. Отслеживайте состояние бота и разрешите пользователю прерывать или отменять последовательность.

Существует два способа вызова модулей задач:

* Новый тип сообщения [](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) вызова: [](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke) `invoke` использование действия карточки для карт Bot Framework `task/fetch``Action.Submit` или действия карточки для адаптивных карточек с URL-адресом или адаптивной карточкой модуля задач извлекается динамически из бота.`task/fetch`
* URL-адреса прямых ссылок. Используя синтаксис глубокой ссылки для модулей [](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) [задач,](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-deep-link-syntax)`openUrl` можно использовать действие карточки для картОчек Bot Framework [](~/task-modules-and-cards/cards/cards-actions.md#action-type-openurl) `Action.OpenUrl` или действие карточки для адаптивных карточек соответственно. При использовании URL-адресов глубоких ссылок URL-адрес `task/fetch`модуля задачи или текст адаптивной карточки уже известен, чтобы избежать кругового пути сервера относительно .

> [!IMPORTANT]
> Каждый `url` из них `fallbackUrl` должен реализовывать протокол шифрования HTTPS.

В следующем разделе приводятся сведения о вызове модуля задачи с помощью `task/fetch`.

## <a name="invoke-a-task-module-using-taskfetch"></a>Вызов модуля задачи с помощью задачи или выборки

Когда объект `value` действия карточки `invoke` `Action.Submit` или инициализирован и когда пользователь нажмет кнопку, `invoke` боту отправляется сообщение. В HTTP-ответе `invoke` на сообщение есть объект [TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object), внедренный в объект-оболочку, который Teams для отображения модуля задачи.

:::image type="content" source="../../assets/images/task-module/task-module-invoke-request-response.png" alt-text="запрос или ответ задачи или выборки":::

Следующие шаги предоставляют модуль задачи вызова с помощью задачи или выборки:

1. На этом изображении показана карточка главного имиджевого баннера Bot Framework с действием **"Купить** `invoke` [карточку"](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke). Значение свойства равно `type` , `task/fetch` а остальная часть `value` объекта может быть по вашему выбору.
1. Бот получает сообщение `invoke` HTTP POST.
1. Бот создает объект ответа и возвращает его в тексте ответа POST с кодом ответа HTTP 200. Дополнительные сведения о схеме ответов см. [в обсуждении задачи или отправки](#the-flexibility-of-tasksubmit). В следующем коде приведен пример текста HTTP-ответа, содержащего объект [TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) , внедренный в объект-оболочку:

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

    Событие `task/fetch` и его ответ для ботов похожи на `microsoftTeams.tasks.startTask()` функцию в клиентском пакете SDK.

1. Microsoft Teams отображает модуль задачи.

В следующем разделе приводятся сведения об отправке результата модуля задачи.

## <a name="submit-the-result-of-a-task-module"></a>Отправка результата модуля задачи

Когда пользователь завершает работу с модулем задач, отправка результата обратно боту аналогична работе с вкладками. Дополнительные сведения см [. в примере отправки результата модуля задачи](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-of-submitting-the-result-of-a-task-module). Существует несколько различий, описанных ниже.

* HTML или JavaScript`TaskInfo.url`, то есть: после проверки введенных пользователем данных вы вызываете функцию пакета SDK`submitTask()`, `microsoftTeams.tasks.submitTask()` которую далее называют функцией для удобочитаемости. Вы можете вызвать его `submitTask()` без параметров, если Teams закрыть модуль задачи, `submitHandler`но необходимо передать объект или строку. Передайте его в качестве первого параметра. `result` Teams вызывает`submitHandler`, `err` является `null`и является `result` объектом или строкой, которые вы передали`submitTask()`. При вызове `submitTask()` с параметром `result` необходимо передать массив `appId` строк `appId` или массив. Это позволяет Teams убедиться, что приложение, отправляющее результат, совпадает с тем, которое вызывает модуль задачи. Бот получает сообщение, `task/submit` в том числе `result`. Дополнительные сведения см [. в полезных данных `task/fetch` и `task/submit` сообщениях](#payload-of-taskfetch-and-tasksubmit-messages).
* Адаптивная карточка`TaskInfo.card``task/submit`: текст адаптивной карточки, заполненный пользователем, отправляется боту через сообщение, когда пользователь нажмет любую кнопку`Action.Submit`.

В следующем разделе приводятся сведения о гибкости `task/submit`.

## <a name="the-flexibility-of-tasksubmit"></a>Гибкость задач и отправки

Когда пользователь завершает работу с модулем задачи, вызываемого ботом, бот всегда `task/submit invoke` получает сообщение. У вас есть несколько вариантов ответа на `task/submit` сообщение следующим образом:

| Ответ текста HTTP                      | Сценарий                                |
| --------------------------------------- | --------------------------------------- |
| Сообщение не игнорируется `task/submit` | Самый простой ответ — это отсутствие ответа. Бот не должен отвечать, когда пользователь завершает работу с модулем задачи. |
| <pre>{<br/>  "task": {<br/>    "type": "message",<br/>    "value": "Message text"<br/>  }<br/>}</pre> | Teams отображает значение во `value` всплывающем окне сообщения. |
| <pre>{<br/>  "task": {<br/>    "type": "continue",<br/>    "value": &lt;TaskInfo object&gt;<br/>  }<br/>}</pre> | Позволяет связывать последовательности адаптивных карточек в мастере или многошаговом интерфейсе. |

> [!NOTE]
> Связывание адаптивных карточек в последовательность — это расширенный сценарий. Пример Node.js поддерживает его. Дополнительные сведения см[. в Microsoft Teams модуля Node.js](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes).

В следующем разделе приводятся сведения о полезных данных и `task/fetch` `task/submit` сообщениях.

## <a name="payload-of-taskfetch-and-tasksubmit-messages"></a>Полезные данные сообщений задачи, получения и отправки

В этом разделе определяется схема того, что получает бот при приеме объекта `task/fetch` или объекта `task/submit` Bot Framework `Activity` . В следующей таблице приведены свойства полезных данных `task/fetch` и `task/submit` сообщений.

| Свойство | Описание                          |
| -------- | ------------------------------------ |
| `type`   | Всегда.`invoke`           |
| `name`   | Имеет значение `task/fetch``task/submit`. |
| `value`  | Определяемые разработчиком полезные данные. Структура объекта совпадает `value` с структурой, отправляемой из Teams. Однако в этом случае он отличается. Для этого требуется поддержка динамической `task/fetch` выборки из Bot Framework, `value` `Action.Submit` то есть действия адаптивной карточки, то есть `data`. В дополнение к включенной или включенной `context` `value` функции Teams боту необходим способ взаимодействия с ботом`data`.<br/><br/>Объедините "value" и "data" в родительский объект:<br/><br/><pre>{<br/>  "context": {<br/>    "theme": "default" &vert; "dark" &vert; "contrast",<br/>  },<br/>  "data": [value field from Bot Framework card] &vert; [data field from Adaptive Card] <br/>}</pre>  |

В следующем разделе приведен пример получения и ответа `task/fetch` `task/submit` на сообщения в Node.js.

## <a name="example-of-taskfetch-and-tasksubmit-invoke-messages-in-nodejs-and-c"></a>Пример сообщений вызова задачи, получения и отправки в Node.js и C #

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

### <a name="bot-framework-card-actions-vs-adaptive-card-actionsubmit-actions"></a>Действия с карточками Bot Framework и действия адаптивной карточки. Отправка действий

Схема действий с карточками Bot Framework `Action.Submit` отличается от действий адаптивной карточки, а способ вызова модулей задач также отличается. В `data` объекте `Action.Submit` содержится объект `msteams` , поэтому он не мешает другим свойствам в карточке. В следующей таблице показан пример каждого действия карточки:

| Действие карточки Bot Framework                              | Действие Adaptive Card Action.Submit                     |
| ------------------------------------------------------ | ------------------------------------------------------ |
| <pre>{<br/>  "type": "invoke",<br/>  "title": "Buy",<br/>  "value": {<br/>    "type": "task/fetch",<br/>    &lt;...&gt;<br/>  }<br/>}</pre> | <pre>{<br/>  "type": "Action.Submit",<br/>  "id": "btnBuy",<br/>  "title": "Buy",<br/>  "data": {<br/>    &lt;...&gt;,<br/>    "msteams": {<br/>      "type": "task/fetch"<br/>    }<br/>  }<br/>}</pre>  |

## <a name="code-sample"></a>Пример кода

|Название примера | Описание | .NET | Node.js|
|----------------|-----------------|--------------|----------------|
|Пример bots-V4 для модуля задач | Примеры для создания модулей задач. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/54.teams-task-module)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/54.teams-task-module)|

## <a name="step-by-step-guide"></a>Пошаговые инструкции

Следуйте [пошаговое руководство по](../../sbs-botbuilder-taskmodule.yml) созданию и выборке бота модуля задач в Teams.

## <a name="see-also"></a>См. также

* [Microsoft Teams пример кода модуля задач в Node.js](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs/blob/master/src/TeamsBot.ts)
* [Примеры Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)
