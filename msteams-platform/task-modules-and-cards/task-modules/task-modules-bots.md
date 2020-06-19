---
title: Использование модулей задач в Microsoft Teams Боты
description: Использование модулей задач с Microsoft Teams Боты, в том числе карточек, карты, адаптивные карты и ссылки на Bot Framework.
keywords: модули задач Teams Боты
ms.openlocfilehash: 32fb6a4aa0a8bf2297a4f60331dc5c6c6aceb4e2
ms.sourcegitcommit: 214eccbadb7f3a67236b79a041ef487b7bf6dfbd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/07/2020
ms.locfileid: "44801513"
---
# <a name="using-task-modules-from-microsoft-teams-bots"></a>Использование модулей задач из Microsoft Teams Боты

Модули задач можно вызывать из Microsoft Teams боты с помощью кнопок на адаптивных карточках и карточек Bot-инфраструктуры (главный Имиджевый баннер, эскиз и Office 365 Connector). Модули задач часто работают быстрее, чем несколько действий, которые разработчик должен отслеживать состояние Bot и позволять пользователю прерывать или отменять последовательность.

Существует два способа вызова модулей задач:

* **Новый тип сообщения вызова `task/fetch` .** С помощью `invoke` [действия карточки](~/task-modules-and-cards/cards/cards-actions.md#invoke) для карточек ленты (Bot) или `Action.Submit` [действия карты](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) для адаптивных карт с помощью `task/fetch` модуля задач (URL-адрес или Адаптивная карта) выполняется динамическое извлечение из ленты.
* **URL-адреса глубокой ссылки.** С помощью [синтаксиса глубокой ссылки для модулей задач](~/task-modules-and-cards/what-are-task-modules.md#task-module-deep-link-syntax)можно использовать `openUrl` [действия с картой](~/task-modules-and-cards/cards/cards-actions.md#openurl) для карточек ленты или `Action.OpenUrl` [действия карты](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) для адаптивных карт соответственно. При использовании URL-адресов с глубокими ссылками URL-адрес модуля задачи или адаптивный текст карточки очевидно известен заранее, что позволяет избежать кругового пути к серверу `task/fetch` .

>[!IMPORTANT]
>Для обеспечения безопасной связи каждый из `url` них `fallbackUrl` должен реализовать протокол шифрования HTTPS.

## <a name="invoking-a-task-module-via-taskfetch"></a>Вызов модуля задачи с помощью задачи/извлечения

Когда `value` объект `invoke` действия карточки или `Action.Submit` инициализирован правильно (подробно описывается ниже), когда пользователь нажимает кнопку, `invoke` сообщение отправляется в Bot. В HTTP-ответе на `invoke` сообщение существует [объект таскинфо](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) , внедренный в объект-оболочку, который Teams использует для отображения модуля задачи.

![запрос/ответ на задачу/получение](~/assets/images/task-module/task-module-invoke-request-response.png)

Рассмотрим каждый шаг чуть подробнее:

1. В этом примере показана карточка главный Имиджевый баннер Framework с `invoke` [действием](~/task-modules-and-cards/cards/cards-actions.md#invoke)"Купить" карточки. Значение `type` свойства — `task/fetch` остальная часть `value` объекта может быть любым.
2. Bot получает `invoke` сообщение HTTP POST.
3. Bot создает объект Response и возвращает его в тексте ответа POST с кодом отклика HTTP 200. Схема для ответов описана [ниже в разделе "задача/Передача](#the-flexibility-of-tasksubmit)", но важная вещь состоит в том, что текст HTTP-ответа содержит [объект таскинфо](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) , внедренный в объект-оболочку, например:

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

    `task/fetch`Событие и его ответ для Боты похожи, концептуально, в `microsoftTeams.tasks.startTask()` функцию в клиентской SDK.
4. В Microsoft Teams отображается модуль задач.

## <a name="submitting-the-result-of-a-task-module"></a>Отправка результата модуля задачи

Когда пользователь завершает работу с модулем задач, отправка результата обратно на сервер-Bot похожа на то, [как он работает с вкладками](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module), но существует несколько различий, поэтому он также описан здесь.

* **HTML/JavaScript ( `TaskInfo.url` )**. Когда вы проверили введенные пользователем сведения, вы вызываете `microsoftTeams.tasks.submitTask()` функцию SDK (которая упоминается в дальнейшем `submitTask()` для удобства чтения). Вы можете вызвать `submitTask()` без параметров, если вы хотите, чтобы команда закрывала модуль задач, но в большинстве случаев требуется передать объект или строку в `submitHandler` . Просто передавайте его в качестве первого параметра, `result` . Teams вызовет `submitHandler` : `err` будет `null` и `result` будет объект или строка, которые вы передали `submitTask()` . При вызове `submitTask()` с `result` параметром **необходимо** передать объект `appId` или массив `appId` строк: Это позволяет Teams проверить, что приложение отправляет результат, то же, что вызвало модуль задачи. Ваш робот получит `task/submit` сообщение `result` , в том числе, как описано [ниже](#payload-of-taskfetch-and-tasksubmit-messages).
* **Адаптивная карта ( `TaskInfo.card` )**. Текст адаптивной карточки (заполняемой пользователем) будет отправляться в Bot через `task/submit` сообщение, когда пользователь нажимает любую `Action.Submit` кнопку.

## <a name="the-flexibility-of-tasksubmit"></a>Гибкость задачи и отсылки

В предыдущем разделе вы узнали, что когда пользователь завершается с помощью модуля задачи, вызванного из Bot, Bot всегда получает `task/submit invoke` сообщение. Как разработчик, у вас есть несколько вариантов *ответа* на `task/submit` сообщение:

| Ответ основного текста HTTP                      | Сценарий                                |
| --------------------------------------- | --------------------------------------- |
| Нет (пропускать `task/submit` сообщение) | Самый простой ответ вообще не отвечает. Ваш робот не должен отвечать, когда пользователь завершает работу с модулем задач. |
| <pre>{<br/>  "task": {<br/>    "type": "message",<br/>    "value": "Message text"<br/>  }<br/>}</pre> | Teams отобразит значение `value` всплывающего окна сообщения. |
| <pre>{<br/>  "task": {<br/>    "type": "continue",<br/>    "value": &lt;TaskInfo object&gt;<br/>  }<br/>}</pre> | Позволяет "цепочку" цепочек адаптивных карточек в мастере и многоэтапной работе. _Обратите внимание, что сцепление адаптивных карт в последовательность является расширенным сценарием и не задокументировано здесь. Однако в этом примере приложение Node.js поддерживает его, и как это работает в [файле readme.md](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)._ |

## <a name="payload-of-taskfetch-and-tasksubmit-messages"></a>Полезные данные о задачах, получении и задачах и отправляя сообщения

В этом разделе определяется схема того, что Bot получает, когда он получает `task/fetch` `task/submit` объект или объект Bot Framework `Activity` . Ниже приведен самый важный уровень верхнего уровня:

| Свойство | Описание                          |
| -------- | ------------------------------------ |
| `type`   | Всегда будет`invoke`              |
| `name`   | Один `task/fetch` или`task/submit` |
| `value`  | Полезные данные, определенные разработчиком. Как правило, структура `value` объекта отражается на том, что было отправлено из Teams. В этом случае, однако, это отличается, так как мы хотим поддерживать динамическую выборку ( `task/fetch` ) из обеих действий: Bot Framework ( `value` ) и адаптивных карт `Action.Submit` ( `data` ), и нам нужен способ для обмена командами `context` с Bot в дополнение к тому, что было включено в `value` / `data` .<br/><br/>Для этого необходимо объединить два объекта в родительский.<br/><br/><pre>{<br/>  "context": {<br/>    "theme": "default" &vert; "dark" &vert; "contrast",<br/>  },<br/>  "data": [value field from Bot Framework card] &vert; [data field from Adaptive Card] <br/>}</pre>  |

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---nodejs"></a>Пример: получение и ответ на сообщения о задачах, выдачах и задачах и вызываемых запросах — Node.js

> [!NOTE]
> Приведенный ниже пример кода был изменен между техническим и окончательным выпуском этой функции: схема `task/fetch` запроса изменилась на следующий пример [documented in the previous section](#payload-of-taskfetch-and-tasksubmit-messages). Это значит, что документация была правильной, но не была реализована. Ознакомьтесь с `// for Technical Preview [...]` комментариями, которые вы изменили.

```typescript
// Handle requests and responses for a "Custom Form" and an "Adaptive card" task module.
// Assumes request is coming from an Adaptive card Action.Submit button that has a "taskModule" property indicating what to invoke
private async onInvoke(event: builder.IEvent, cb: (err: Error, body: any, status?: number) => void): Promise<void> {
    let invokeType = (event as any).name;
    let invokeValue = (event as any).value;
    if (invokeType === undefined) {
        invokeType = null;
    }
    switch (invokeType) {
        case "task/fetch": {
            if (invokeValue !== undefined && invokeValue.data.taskModule === "customform") { // for Technical Preview, was invokeValue.taskModule
                // Return the specified task module response to the bot
                let fetchTemplate: any = {
                    "task": {
                        "type": "continue",
                        "value": {
                            "title": "Custom Form",
                            "height": 510,
                            "width": 430,
                            "fallbackUrl": "https://contoso.com/teamsapp/customform",
                            "url": "https://contoso.com/teamsapp/customform",
                        }
                    }
                };
                cb(null, fetchTemplate, 200);
            };
            if (invokeValue !== undefined && invokeValue.data.taskModule === "adaptivecard") { // for Technical Preview, was invokeValue.taskModule
                let adaptiveCard = {
                    "type": "AdaptiveCard",
                    "body": [
                        {
                            "type": "TextBlock",
                            "text": "Here is a ninja cat:"
                        },
                        {
                            "type": "Image",
                            "url": "http://adaptivecards.io/content/cats/1.png",
                            "size": "Medium"
                        }
                    ],
                    "version": "1.0"
                };
                // Return the specified task module response to the bot
                let fetchTemplate: any = {
                    "task": {
                        "type": "continue",
                        "value": {
                            "title": "Ninja Cat",
                            "height": "small",
                            "width": "small",
                            "card": {
                                contentType: "application/vnd.microsoft.card.adaptive",
                                content: adaptiveCard,
                            }
                        }
                    }
                };
                cb(null, fetchTemplate, 200);
            };
            break;
        }
        case "task/submit": {
            if (invokeValue.data !== undefined) {
                // It's a valid task module response
                let submitResponse: any = {
                    "task": {
                        "type": "message",
                        "value": "Task complete!",
                    }
                };
                cb(null, fetchTemplates.submitMessageResponse, 200)
            }
        }
    }
}
```

*See also* [Пример кода для модуля задач Microsoft Teams — примеры кода NodeJS](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs/blob/master/src/TeamsBot.ts) и [Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---c"></a>Пример: получение и ответ на сообщения о задачах, выдачах и задачах и запросах Invoke-C #

В C# Боты `invoke` сообщения обрабатываются с помощью `HttpResponseMessage()` обработки сообщения контроллера `Activity` . `task/fetch`Запросы и `task/submit` ответы — JSON. В C# неудобно работать с необработанным JSON, так как он находится в Node.js, поэтому для обработки сериализации и последующего использования JSON необходимы классы-оболочки. В Microsoft Teams [SDK](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) нет прямой поддержки, но вы можете увидеть пример того, как будут выглядеть эти простые классы оберток в [образце приложения на языке C#](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Models/TaskModel.cs).

Ниже приведен пример кода на языке C# для обработки `task/fetch` и `task/submit` сообщений, использующих эти классы оболочки ( `TaskInfo` , `TaskEnvelope` ), взятые из [примера](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs):

```csharp
private HttpResponseMessage HandleInvokeMessages(Activity activity)
{
    var activityValue = activity.Value.ToString();
    if (activity.Name == "task/fetch")
    {
        var action = Newtonsoft.Json.JsonConvert.DeserializeObject<Models.BotFrameworkCardValue<string>>(activityValue);

        Models.TaskInfo taskInfo = GetTaskInfo(action.Data);
        Models.TaskEnvelope taskEnvelope = new Models.TaskEnvelope
        {
            Task = new Models.Task()
            {
                Type = Models.TaskType.Continue,
                TaskInfo = taskInfo
            }
        };
        return Request.CreateResponse(HttpStatusCode.OK, taskEnvelope);
    }
    else if (activity.Name == "task/submit")
    {
        ConnectorClient connector = new ConnectorClient(new Uri(activity.ServiceUrl));
        Activity reply = activity.CreateReply("Received = " + activity.Value.ToString());
        connector.Conversations.ReplyToActivity(reply);
    }
    return new HttpResponseMessage(HttpStatusCode.Accepted);
}

// Helper function for building the TaskInfo object based on the incoming request
private static Models.TaskInfo GetTaskInfo(string actionInfo)
{
    Models.TaskInfo taskInfo = new Models.TaskInfo();
    switch (actionInfo)
    {
        case TaskModuleIds.YouTube:
            taskInfo.Url = taskInfo.FallbackUrl = ApplicationSettings.BaseUrl + "/" + TaskModuleIds.YouTube;
            SetTaskInfo(taskInfo, TaskModuleUIConstants.YouTube);
            break;
        case TaskModuleIds.PowerApp:
            taskInfo.Url = taskInfo.FallbackUrl = ApplicationSettings.BaseUrl + "/" + TaskModuleIds.PowerApp;
            SetTaskInfo(taskInfo, TaskModuleUIConstants.PowerApp);
            break;
        case TaskModuleIds.CustomForm:
            taskInfo.Url = taskInfo.FallbackUrl = ApplicationSettings.BaseUrl + "/" + TaskModuleIds.CustomForm;
            SetTaskInfo(taskInfo, TaskModuleUIConstants.CustomForm);
            break;
        case TaskModuleIds.AdaptiveCard:
            taskInfo.Card = AdaptiveCardHelper.GetAdaptiveCard();
            SetTaskInfo(taskInfo, TaskModuleUIConstants.AdaptiveCard);
            break;
        default:
            break;
    }
    return taskInfo;
}
```

В приведенном выше примере не показана `SetTaskInfo()` функция, которая задает `height` свойства, `width` и `title` свойства `TaskInfo` объекта для каждого случая. Ниже приведен [Исходный код для сеттаскинфо ()](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs).

### <a name="bot-framework-card-actions-vs-adaptive-card-actionsubmit-actions"></a>Действия с карточками Bot и адаптивной карты. действия по отсылке

Схема действий для действий с карточной картой несколько отличается от действий адаптивной карточки `Action.Submit` . В результате, способ вызова модулей задач немного отличается: `data` объект `Action.Submit` содержит `msteams` объект, поэтому он не будет влиять на другие свойства карточки. В следующей таблице приведен пример каждого из них:

| Действие с картой инфраструктуры Bot                              | Действие адаптивной карточки. действие отсылки                     |
| ------------------------------------------------------ | ------------------------------------------------------ |
| <pre>{<br/>  "type": "invoke",<br/>  "title": "Buy",<br/>  "value": {<br/>    "type": "task/fetch",<br/>    &lt;...&gt;<br/>  }<br/>}</pre> | <pre>{<br/>  "type": "Action.Submit",<br/>  "id": "btnBuy",<br/>  "title": "Buy",<br/>  "data": {<br/>    &lt;...&gt;,<br/>    "msteams": {<br/>      "type": "task/fetch"<br/>    }<br/>  }<br/>}</pre>  |
