---
title: Использование модулей задач в ботах Microsoft Teams
description: Как использовать модули задач с ботами Microsoft Teams, включая карточки Bot Framework, адаптивные карточки и ссылки на контент.
ms.localizationpriority: high
ms.topic: how-to
keywords: задачи модули команды боты глубинные ссылки адаптивная карточка
ms.openlocfilehash: 1074eee616ca7a5d78a071fb42c23d0010a8300d
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111334"
---
# <a name="use-task-modules-from-bots"></a>Использование модулей задач из ботов

Модули задач можно вызывать из ботов Microsoft Teams с помощью кнопок на адаптивных карточках и карточках Bot Framework, таких как главный имиджевый баннер, эскиз и соединитель Office 365. Модули задач часто обеспечивают лучший пользовательский интерфейс, чем несколько шагов диалога. Отслеживайте состояние бота и разрешайте пользователю прерывать или отменять последовательность.

Существует два способа вызова модулей задач:

* Новый тип сообщения о вызове`task/fetch`: использование `invoke` [действия карточки](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke) для карточек Bot Framework или `Action.Submit` [действие карточки](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) для адаптивных карточек с `task/fetch`, модулем задачи, либо URL-адресом, либо адаптивной карточкой, динамически извлекается из вашего бота.
* URL-адреса глубинных ссылок: используя [синтаксис глубоких ссылок для модулей задач](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-deep-link-syntax), вы можете использовать `openUrl` [действие карточки](~/task-modules-and-cards/cards/cards-actions.md#action-type-openurl)для карточек Bot Framework или`Action.OpenUrl` [действие карточки](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) для адаптивных карточек соответственно. При использовании URL-адресов глубинных ссылок URL-адрес модуля задачи или текст адаптивной карточки уже известны, чтобы избежать кругового пути сервера относительно `task/fetch`.

> [!IMPORTANT]
> Каждый `url` и `fallbackUrl` должен реализовать протокол шифрования HTTPS.

В следующем разделе приведены сведения о вызове модуля задач с помощью `task/fetch`.

## <a name="invoke-a-task-module-using-taskfetch"></a>Вызвать модуль задач с помощью task/fetch

Когда `value` объект действия карточки `invoke` или `Action.Submit` инициализируется и когда пользователь выбирает кнопку, боту отправляется сообщение `invoke`. В ответе HTTP на сообщение `invoke` есть [объект TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object), встроенный в объект-оболочку, который Teams использует для отображения модуля задачи.

:::image type="content" source="../../assets/images/task-module/task-module-invoke-request-response.png" alt-text="запрос или ответ task/fetch":::

Следующие шаги предоставляют модуль задачи вызова с помощью task/fetch:

1. На этом изображении показана карточка главного имиджевого баннера Bot Framework с действием **Купить** `invoke` [карточку](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke). Значение свойства `type` является `task/fetch` и остальная часть объекта `value` может быть на ваш выбор.
1. Бот получает сообщение `invoke` HTTP POST.
1. Бот создает объект отклика и возвращает его в тексте отклика POST с кодом отклика HTTP 200. Подробнее о схеме для откликов в [Обсуждении task/submit](#the-flexibility-of-tasksubmit). Следующий код представляет собой пример текста отклика HTTP, который содержит [объект TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object), встроенный в объект-оболочку:

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

    `task/fetch`Событие и его ответ для ботов аналогичны функции `microsoftTeams.tasks.startTask()` в клиентском SDK.

1. Microsoft Teams отображает модуль задач.

В следующем разделе приведены сведения об отправке результатов модуля задачи.

## <a name="submit-the-result-of-a-task-module"></a>Отправить результат модуля задачи

Когда пользователь завершает работу с модулем задачи, отправка результата обратно боту аналогична отправке с вкладками. Подробнее в [примере отправки результата модуля задачи](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-of-submitting-the-result-of-a-task-module). Есть несколько отличий:

* HTML или JavaScript, `TaskInfo.url`: после проверки того, что ввел пользователь, вы вызываете функцию `microsoftTeams.tasks.submitTask()` SDK, называемую далее `submitTask()`для простоты чтения. Вы можете вызвать `submitTask()` без параметров, если хотите, чтобы Teams закрыла модуль задачи, но вы должны передать объект или строку в ваш `submitHandler`. Передайте его как первый параметр, `result`. Teams вызывает `submitHandler`, `err` является `null`, и `result` — это объект или строка, переданные в `submitTask()`. Если вызвать `submitTask()` с параметром `result`, необходимо передать `appId` или массив строк `appId`. Это позволяет Teams убедиться, что приложение, отправляющее результат, является тем же, что вызвало модуль задачи. Бот получает сообщение `task/submit`, включая `result`. Подробнее см. [полезные данные `task/fetch` и `task/submit` сообщения](#payload-of-taskfetch-and-tasksubmit-messages).
* Адаптивная карточка `TaskInfo.card`: текст адаптивной карточки, заполненный пользователем, отправляется боту через `task/submit` сообщение при нажатии пользователем любой кнопки `Action.Submit`.

Следующий раздел содержит подробные сведения о гибкости `task/submit`.

## <a name="the-flexibility-of-tasksubmit"></a>Гибкость task/submit

Когда пользователь завершает работу с модулем задачи, вызванным из бота, бот всегда получает сообщение `task/submit invoke`. У вас есть следующие варианты ответа на `task/submit`:

| Ответ в тексте HTTP                      | Сценарий                                |
| --------------------------------------- | --------------------------------------- |
| Нет игнорирует сообщение `task/submit` | Самый простой отклик — это отсутствие отклика. От вашего бота не требуется ответа, когда пользователь закончит работу с модулем задачи. |
| <pre>{<br/>  "task": {<br/>    "type": "message",<br/>    "value": "Message text"<br/>  }<br/>}</pre> | Teams отображает значение `value` во всплывающем окне сообщения. |
| <pre>{<br/>  "task": {<br/>    "type": "continue",<br/>    "value": &lt;TaskInfo object&gt;<br/>  }<br/>}</pre> | Позволяет соединять последовательности адаптивных карточек в мастере или в многоэтапном действии. |

> [!NOTE]
> Объединение адаптивных карточек в последовательность — это расширенный сценарий. Образец приложения Node.js поддерживает его. Подробнее в разделе [Модуль задач Microsoft Teams Node.js](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes).

Следующий раздел содержит подробные сведения о полезных данных сообщений `task/fetch` и `task/submit`.

## <a name="payload-of-taskfetch-and-tasksubmit-messages"></a>Полезные данные task/fetch и сообщения task/fetch

В этом разделе определяется схема того, что ваш бот получает при получении объекта `task/fetch` или `task/submit` Bot Framework `Activity`. В следующей таблице представлены свойства полезных данных `task/fetch` и сообщений `task/submit`:

| Свойство | Описание                          |
| -------- | ------------------------------------ |
| `type`   | Всегда `invoke`.           |
| `name`   | Возможные значения: `task/fetch` или `task/submit`. |
| `value`  | Являются полезными данными определяемыми разработчиком. Структура объекта `value` такая же, как и отправляемая из Teams.. Однако в данном случае все иначе. Для этого требуется поддержка динамической выборки, которая исходит как `task/fetch` от bot Framework, то есть`value`, так и от действий Adaptive Card`Action.Submit`, то есть `data`. Требуется способ связи Teams `context` с ботом в дополнение к тому, что включен в `value` или `data`.<br/><br/>Объединение ''значений'' и ''данных'' в родительский объект:<br/><br/><pre>{<br/>  "context": {<br/>    "theme": "default" &vert; "dark" &vert; "contrast",<br/>  },<br/>  "data": [value field from Bot Framework card] &vert; [data field from Adaptive Card] <br/>}</pre>  |

В следующем разделе приведен пример получения и ответа на сообщения вызова `task/fetch` и `task/submit` в Node.js.

## <a name="example-of-taskfetch-and-tasksubmit-invoke-messages-in-nodejs-and-c"></a>Пример сообщений вызова task/fetch и task/submit в Node.js и C#

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

### <a name="bot-framework-card-actions-vs-adaptive-card-actionsubmit-actions"></a>Действия карточки Bot Framework и действие адаптивной карточки Action.Submit

Схема действий карточки Bot Framework отличается от действий адаптивной карточки `Action.Submit` и способ вызова модулей задач также отличается. Объект `data` в `Action.Submit` содержит объект `msteams`, поэтому он не мешает другим свойствам карточки. В следующей таблице показан пример каждого действия карточки:

| Действие карточки Bot Framework                              | Действие адаптивной карточки Submit action                     |
| ------------------------------------------------------ | ------------------------------------------------------ |
| <pre>{<br/>  "type": "invoke",<br/>  "title": "Buy",<br/>  "value": {<br/>    "type": "task/fetch",<br/>    &lt;...&gt;<br/>  }<br/>}</pre> | <pre>{<br/>  "type": "Action.Submit",<br/>  "id": "btnBuy",<br/>  "title": "Buy",<br/>  "data": {<br/>    &lt;...&gt;,<br/>    "msteams": {<br/>      "type": "task/fetch"<br/>    }<br/>  }<br/>}</pre>  |

## <a name="code-sample"></a>Пример кода

|Название примера | Описание | .NET | Node.js|
|----------------|-----------------|--------------|----------------|
|Примеры ботов модуля задач-V4 | Образцы для создания модулей задач. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/54.teams-task-module)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/54.teams-task-module)|

## <a name="step-by-step-guide"></a>Пошаговые инструкции

Следуйте [пошаговым инструкциям](../../sbs-botbuilder-taskmodule.yml), чтобы создать и получить бот модуля задач в Teams

## <a name="see-also"></a>Дополнительные ресурсы

* [Пример кода модуля задач Microsoft Teams в Node.js](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs/blob/master/src/TeamsBot.ts)
* [Образцы Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)
