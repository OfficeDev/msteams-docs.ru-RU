---
title: Использование модулей задач в ботах Microsoft Teams
description: Использование модулей задач с ботами Microsoft Teams, включая карты Bot Framework, адаптивные карты и глубокие ссылки.
ms.topic: how-to
keywords: модули задач групп ботов
ms.openlocfilehash: d87b55bf202184f315abf69dfc34fc4db9125c4f
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696474"
---
# <a name="using-task-modules-from-microsoft-teams-bots"></a>Использование модулей задач от ботов Microsoft Teams

Модули задач можно вызывать из ботов Microsoft Teams с помощью кнопок на адаптивных картах и картах Bot Framework (Hero, Thumbnail и Office 365 Connector). Модули задач часто являются более удобными для пользователей, чем несколько этапов беседы, в которых вы как разработчик должны отслеживать состояние бота и позволять пользователю прерывать или отменять последовательность.

Существует два способа ссылки на модули задач:

* **Новый вид сообщения вызова `task/fetch` .** Использование действия карты для карт Bot Framework или действия карт для адаптивных карт с модулем задач (URL-адрес или адаптивная карта) извлекается динамически из `invoke` [](~/task-modules-and-cards/cards/cards-actions.md#invoke) `Action.Submit` [](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) `task/fetch` вашего бота.
* **URL-адреса глубоких ссылок.** Используя [синтаксис](~/task-modules-and-cards/what-are-task-modules.md#task-module-deep-link-syntax)глубокой ссылки для модулей задач, вы можете использовать действие карты для карт Bot Framework или действие карты для адаптивных карт `openUrl` [](~/task-modules-and-cards/cards/cards-actions.md#openurl) `Action.OpenUrl` [](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) соответственно. С URL-адресами глубоких ссылок URL-адрес модуля задач или корпус адаптивной карты, очевидно, известен заранее, избегая обратного пути сервера по отношению к `task/fetch` .

>[!IMPORTANT]
>Чтобы обеспечить безопасность сообщений, каждый из них должен реализовать `url` `fallbackUrl` протокол шифрования HTTPS.

## <a name="invoking-a-task-module-via-taskfetch"></a>Ссылки на модуль задач через задачу/извлечение

Когда объект действия карточки или инициализирован надлежащим образом (подробнее см. ниже), когда пользователь нажимает кнопку, сообщение отправляется `value` `invoke` `Action.Submit` `invoke` боту. В ответе HTTP на сообщение есть объект `invoke` [TaskInfo,](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) встроенный в объект оболочки, который Teams использует для отображения модуля задач.

![задача/извлечение запроса/ответа](~/assets/images/task-module/task-module-invoke-request-response.png)

Рассмотрим каждый шаг более подробно:

1. В этом примере показана карта Bot Framework Hero с действием карточки `invoke` ["Купить".](~/task-modules-and-cards/cards/cards-actions.md#invoke) Значение свойства — остальная часть объекта может быть `type` `task/fetch` `value` любой, что вам нравится.
2. Бот получает сообщение `invoke` HTTP POST.
3. Бот создает объект отклика и возвращает его в тело ответа POST с кодом ответа HTTP 200. Схема ответов описана ниже в обсуждении [задачи/отправки,](#the-flexibility-of-tasksubmit)но теперь важно помнить, что тело ответа HTTP содержит объект [TaskInfo,](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) встроенный в объект оболочки, например:

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

    Событие и его ответ для ботов похожи концептуально на функцию клиента `task/fetch` `microsoftTeams.tasks.startTask()` SDK.
4. Microsoft Teams отображает модуль задач.

## <a name="submitting-the-result-of-a-task-module"></a>Отправка результатов модуля задач

Когда пользователь завершает работу с модулем задач, отправка результата [](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module)обратно боту похожа на то, как он работает со вкладками, но есть несколько различий, поэтому он также описан здесь.

* **HTML/JavaScript ( `TaskInfo.url` )**. После проверки того, что вошел пользователь, вы вызываете функцию SDK (далее она называется для целей `microsoftTeams.tasks.submitTask()` `submitTask()` читаемости). Вы можете звонить без параметров, если вы просто хотите, чтобы Teams закрыли модуль задач, но большую часть времени вы хотите передать объект или строку `submitTask()` в `submitHandler` ваш . Просто передай его в качестве первого `result` параметра. Команды `submitHandler` вызовят: будет и будет `err` `null` `result` объектом или строкой, которую вы передали `submitTask()` . Если вы вызываете с параметром, необходимо передать или массив строк: это позволяет Teams проверить, что приложение, отправляя результат, является тем же, что вызывалось в модуль `submitTask()` `result`  `appId` `appId` задач. Ваш бот получит `task/submit` сообщение, в том `result` числе, как описано [ниже](#payload-of-taskfetch-and-tasksubmit-messages).
* **Адаптивная карта ( `TaskInfo.card` )**. Тело адаптивной карты (как заполнено пользователем) будет отправлено боту через сообщение, когда пользователь `task/submit` нажимает любую `Action.Submit` кнопку.

## <a name="the-flexibility-of-tasksubmit"></a>Гибкость задачи/отправки

В предыдущем разделе вы узнали, что после завершения работы с модулем задач, вызываемом ботом, бот всегда получает `task/submit invoke` сообщение. В качестве разработчика у вас есть несколько *вариантов* ответа на `task/submit` сообщение:

| HTTP Body Response                      | Сценарий                                |
| --------------------------------------- | --------------------------------------- |
| Нет (игнорировать `task/submit` сообщение) | Самый простой ответ — это отсутствие ответа. Ваш бот не обязан отвечать, когда пользователь завершает работу с модулем задач. |
| <pre>{<br/>  "task": {<br/>    "type": "message",<br/>    "value": "Message text"<br/>  }<br/>}</pre> | Teams будет отображать значение в `value` всплывающее окно сообщения. |
| <pre>{<br/>  "task": {<br/>    "type": "continue",<br/>    "value": &lt;TaskInfo object&gt;<br/>  }<br/>}</pre> | Позволяет "цепить" последовательности адаптивных карт вместе в мастере и многошаговом опытом. _Обратите внимание, что цепочка адаптивных карт в последовательность является расширенным сценарием и не задокументирована здесь. Однако Node.js пример приложения поддерживает его, и его работа задокументирована в [README.md файле.](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)_ |

## <a name="payload-of-taskfetch-and-tasksubmit-messages"></a>Полезное количество задач/извлечений и задач/отправки сообщений

В этом разделе определяется схема получения ботом объекта `task/fetch` `task/submit` или объекта Bot `Activity` Framework. Ниже отображаются важные верхнего уровня:

| Свойство | Описание                          |
| -------- | ------------------------------------ |
| `type`   | Всегда будет `invoke`              |
| `name`   | Либо, `task/fetch` либо `task/submit` |
| `value`  | Полезной нагрузки, определенной разработчиком. Обычно структура объекта отражает то, что `value` было отправлено из Teams. В этом случае, однако, это другое, потому что мы хотим поддерживать динамические извлечение () как из Bot Framework ( ) и адаптивные действия карты ( ), и нам нужен способ связи Teams с ботом в дополнение к тому, что было включено `task/fetch` `value` в `Action.Submit` `data` `context` `value` / `data` .<br/><br/>Мы объединяя эти два объекта в родительский объект:<br/><br/><pre>{<br/>  "context": {<br/>    "theme": "default" &vert; "dark" &vert; "contrast",<br/>  },<br/>  "data": [value field from Bot Framework card] &vert; [data field from Adaptive Card] <br/>}</pre>  |

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---nodejs"></a>Пример: получение и реагирование на задачу/получение и отправку сообщений вызовов — Node.js

> [!NOTE]
> Пример кода, приведенного ниже, был изменен между техническим предварительным просмотром и окончательным выпуском этой функции: схема запроса изменена, чтобы следовать за тем, что было задокументировано `task/fetch` [в предыдущем разделе](#payload-of-taskfetch-and-tasksubmit-messages). То есть документация была правильной, но реализация не была. Ниже приведены `// for Technical Preview [...]` комментарии к измененным комментариям.

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

*См. также* пример примера модуля задач [Microsoft Teams — примеры nodejs](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs/blob/master/src/TeamsBot.ts) и [Bot Framework.](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---c"></a>Пример: получение и реагирование на задачу/получение и отправку сообщений вызовов - C #

В C# ботах сообщения обрабатываются контроллером, `invoke` `HttpResponseMessage()` обрабатывая `Activity` сообщение. Запросы `task/fetch` и ответы — это `task/submit` JSON. В C# не так удобно иметь дело с необработанных JSON, как в Node.js, поэтому для обработки сериализации в JSON и из JSON необходимы классы обертки. Прямой поддержки этого в microsoft Teams [C# SDK](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) пока нет, но вы можете увидеть пример того, как будут выглядеть эти простые классы оболочки в C# примере приложения [.](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Models/TaskModel.cs)

Ниже приведен пример кода в C# для обработки и сообщений с помощью этих классов оболочки ( , ), выдержки `task/fetch` `task/submit` из `TaskInfo` `TaskEnvelope` [примера](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs):

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

Не показана в вышеуказанной примере функция, которая задает , и свойства `SetTaskInfo()` `height` объекта для каждого `width` `title` `TaskInfo` случая. Вот исходный [код setTaskInfo()](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs).

### <a name="bot-framework-card-actions-vs-adaptive-card-actionsubmit-actions"></a>Действия карты Bot Framework против действий адаптивной карты Action.Submit

Схема действий карт Bot Framework немного отличается от действий адаптивной `Action.Submit` карты. В результате способ вызова модулей задач также немного отличается: объект содержит объект, чтобы он не мешал другим свойствам `data` `Action.Submit` `msteams` карты. В следующей таблице показан пример каждого из них:

| Действие карты Bot Framework                              | Действие адаптивной карты Action.Submit                     |
| ------------------------------------------------------ | ------------------------------------------------------ |
| <pre>{<br/>  "type": "invoke",<br/>  "title": "Buy",<br/>  "value": {<br/>    "type": "task/fetch",<br/>    &lt;...&gt;<br/>  }<br/>}</pre> | <pre>{<br/>  "type": "Action.Submit",<br/>  "id": "btnBuy",<br/>  "title": "Buy",<br/>  "data": {<br/>    &lt;...&gt;,<br/>    "msteams": {<br/>      "type": "task/fetch"<br/>    }<br/>  }<br/>}</pre>  |
