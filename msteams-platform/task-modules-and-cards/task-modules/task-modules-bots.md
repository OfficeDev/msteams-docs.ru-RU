---
title: Использование модулей задач в Microsoft Teams ботов
description: Как использовать модули задач с роботами Microsoft Teams ботов, включая карты Bot Framework, адаптивные карты и глубокие ссылки
localization_priority: Normal
ms.topic: how-to
keywords: задачи модули команды ботов
ms.openlocfilehash: bfaf3dfe791c1736aeb418e2689e513908f04534
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566572"
---
# <a name="using-task-modules-from-microsoft-teams-bots"></a>Использование модулей задач от Microsoft Teams ботов

Модули задач могут вызываться из Microsoft Teams с помощью кнопок на адаптивных картах и карт Bot Framework (Hero, Thumbnail и Office 365 Connector). Модули задач часто являются лучшим пользовательским интерфейсом, чем несколько шагов разговора, где вы, как разработчик, должны отслеживать состояние бота и позволять пользователю прерывать/отменять последовательность.

Существует два способа вызова модулей задач:

* **Новый вид вызова сообщения `task/fetch` .** Использование действия `invoke` [карты для](~/task-modules-and-cards/cards/cards-actions.md#invoke) карт Bot Framework, или `Action.Submit` [действия карты для](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) адаптивных `task/fetch` карт, с , модуль задачи (либо URL или адаптивной карты) получает динамически от вашего бота.
* **Глубокая ссылка URL-адреса.** Используя [синтаксис глубоких ссылок для модулей](~/task-modules-and-cards/what-are-task-modules.md#task-module-deep-link-syntax)задач, вы можете использовать действие `openUrl` [](~/task-modules-and-cards/cards/cards-actions.md#openurl) карты для карт Bot Framework `Action.OpenUrl` [или действия](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) карты для адаптивных карт, соответственно. С глубокой ссылкой URL-адреса, URL-адрес модуля задачи или адаптивной карты тела, очевидно, известно заранее, избегая сервера туда и обратно по отношению к `task/fetch` .

>[!IMPORTANT]
>Для обеспечения безопасной связи, `url` каждый `fallbackUrl` и должен реализовать протокол шифрования HTTPS.

## <a name="invoking-a-task-module-through-taskfetch"></a>Вызов модуля задач через задачу/получение

Когда `value` объект действия карты или инициализирован надлежащим `invoke` образом (объясняется более подробно `Action.Submit` ниже), когда пользователь нажимает кнопку `invoke` сообщение отправляется боту. В ответе HTTP на `invoke` сообщение есть объект [TaskInfo,](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) встроенный в объект обертки, который Teams используется для отображения модуля задач.

![задача/запрос/ответ](~/assets/images/task-module/task-module-invoke-request-response.png)

Давайте рассмотрим каждый шаг более подробно:

1. В этом примере показана карта Bot Framework Hero с действием карты `invoke` ["Купить".](~/task-modules-and-cards/cards/cards-actions.md#invoke) Значение свойства `type` - `task/fetch` остальная часть объекта может быть `value` все, что вам нравится.
1. Бот получает сообщение `invoke` HTTP POST.
1. Бот создает объект ответа и возвращает его в тело ответа POST с кодом ответа HTTP 200. Схема ответов описана ниже в обсуждении задачи [/отправки,](#the-flexibility-of-tasksubmit)но сейчас важно помнить, что тело ответа HTTP содержит объект [TaskInfo,](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) встроенный в объект обертки. Пример:

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

    Событие `task/fetch` и его реакция на ботов похожи, концептуально, на `microsoftTeams.tasks.startTask()` функцию клиента SDK.
1. Microsoft Teams отображает модуль задачи.

## <a name="submitting-the-result-of-a-task-module"></a>Отправка результата модуля задач

Когда пользователь закончил с модулем задачи, отправка результата обратно в бот похож на [то, как он работает с вкладками,](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module)но Есть несколько различий, так что описано здесь тоже.

* **HTML/JavaScript ( `TaskInfo.url` .** После проверки того, что пользователь ввел, вы называете `microsoftTeams.tasks.submitTask()` функцию SDK (в дальнейшем она `submitTask()` называется для целей читаемости). Вы можете `submitTask()` позвонить без каких-либо параметров, если вы Teams просто хотите, чтобы закрыть модуль задачи, но большую часть времени вы хотите передать объект или строку к вашему `submitHandler` . Просто переветь его в качестве первого параметра, `result` . Teams будет вызывать `submitHandler` : будет и будет объект / строка вы `err` `null` `result` перешли к `submitTask()` . Если вы `submitTask()` звоните с `result` параметром, **вы** должны пройти `appId` или массив `appId` строк: это позволяет Teams проверить, что приложение отправки результат тот же, который вызвал модуль задачи. Ваш бот получит сообщение, в `task/submit` том числе, `result` как описано [ниже](#payload-of-taskfetch-and-tasksubmit-messages).
* **Адаптивная карта `TaskInfo.card` ()**. Тело адаптивной карты (заполненное пользователем) будет отправлено боту через `task/submit` сообщение, когда пользователь нажимает любую `Action.Submit` кнопку.

## <a name="the-flexibility-of-tasksubmit"></a>Гибкость задачи/отправки

В предыдущем разделе вы узнали, что когда пользователь заканчивает с модулем задач, вызванным от бота, бот всегда получает `task/submit invoke` сообщение. Как разработчик, у вас есть несколько вариантов *при ответе* на `task/submit` сообщение:

| ОТВЕТ тела HTTP                      | Сценарий                                |
| --------------------------------------- | --------------------------------------- |
| Нет (игнорировать `task/submit` сообщение) | Самый простой ответ - это вообще никакой ответ. Ваш бот не обязан отвечать, когда пользователь закончил с модулем задачи. |
| <pre>{<br/>  "task": {<br/>    "type": "message",<br/>    "value": "Message text"<br/>  }<br/>}</pre> | Teams будет отображать значение в `value` всплывающем ящике сообщения. |
| <pre>{<br/>  "task": {<br/>    "type": "continue",<br/>    "value": &lt;TaskInfo object&gt;<br/>  }<br/>}</pre> | Позволяет "цепочка" последовательности адаптивных карт вместе в мастер / многоступенчатый опыт. _Обратите внимание, что цепочка адаптивных карт в последовательность является продвинутым сценарием и не документирована здесь. Однако Node.js приложение поддерживает его и то, как оно работает, задокументировано [в его README.md файле.](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)_ |

## <a name="payload-of-taskfetch-and-tasksubmit-messages"></a>Полезная нагрузка задач/извлечения и задачи/отправки сообщений

В этом разделе определяется схема того, что получает ваш бот, когда получает `task/fetch` объект `task/submit` Bot `Activity` Framework. Важные верхние уровни появляются ниже:

| Свойство | Описание                          |
| -------- | ------------------------------------ |
| `type`   | Всегда будет `invoke`              |
| `name`   | Либо `task/fetch` или `task/submit` |
| `value`  | Определяемая разработчиком полезная нагрузка. Обычно структура объекта отражает `value` то, что было отправлено из Teams. В этом случае, однако, это другое, потому что мы хотим поддержать динамический `task/fetch` извлечение ( ) от обоих Bot Framework ( `value` ) и адаптивной карты действия (), и нам `Action.Submit` `data` нужен способ общаться Teams `context` с ботом в дополнение к тому, что было включено `value` / `data` в .<br/><br/>Мы делаем это, объединяя два в родительский объект:<br/><br/><pre>{<br/>  "context": {<br/>    "theme": "default" &vert; "dark" &vert; "contrast",<br/>  },<br/>  "data": [value field from Bot Framework card] &vert; [data field from Adaptive Card] <br/>}</pre>  |

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---nodejs"></a>Пример: Прием и реагирование на сообщения вызова задачи/извлечения и задачи/отправки - Node.js

> [!NOTE]
> Пример кода ниже был изменен между техническим предварительным просмотром и окончательным выпуском этой функции: схема запроса `task/fetch` изменена, чтобы следовать тому, что [было задокументировано в предыдущем разделе.](#payload-of-taskfetch-and-tasksubmit-messages) То есть документация была правильной, но реализация не была. Смотрите комментарии `// for Technical Preview [...]` ниже за то, что изменилось.

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

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---c"></a>Пример: Получение и реагирование на сообщения вызова задачи/извлечения и задачи/отправки - C #

В ботах СЗ `invoke` сообщения обрабатываются контроллером, `HttpResponseMessage()` обрабатываемым `Activity` сообщением. Запросы `task/fetch` `task/submit` и ответы JSON. В C-классах не так удобно иметь дело с необработанным JSON, как в Node.js, поэтому вам нужны классы оберток для обработки сериализации в и из JSON. Прямой поддержки этому в Microsoft Teams [C'SDK](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) пока нет, но вы можете увидеть пример того, как будут выглядеть эти простые [классы обертки в примере приложения C](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Models/TaskModel.cs).

Ниже приведен пример кода в C- для обработки `task/fetch` и `task/submit` сообщений с использованием этих классов `TaskInfo` обертки (, `TaskEnvelope` ), выдержки из [образца:](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs)

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

Не показано в приведеном выше `SetTaskInfo()` примере `height` функция, `width` которая устанавливает , и свойства объекта для каждого `title` `TaskInfo` случая. Вот исходный [код для SetTaskInfo ()](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs).

### <a name="bot-framework-card-actions-vs-adaptive-card-actionsubmit-actions"></a>Действия Бот Фреймвейт карты против Адаптивная карта Action.Submit действия

Схема действий карты Bot Framework немного отличается от действий адаптивной `Action.Submit` карты. В результате способ вызова модулей задач также несколько отличается: `data` объект `Action.Submit` содержит `msteams` объект, поэтому он не будет вмешиваться в другие свойства карты. В следующей таблице приведен пример каждого из них:

| Действие карт Bot Framework                              | Адаптивная карта Action.Submit действий                     |
| ------------------------------------------------------ | ------------------------------------------------------ |
| <pre>{<br/>  "type": "invoke",<br/>  "title": "Buy",<br/>  "value": {<br/>    "type": "task/fetch",<br/>    &lt;...&gt;<br/>  }<br/>}</pre> | <pre>{<br/>  "type": "Action.Submit",<br/>  "id": "btnBuy",<br/>  "title": "Buy",<br/>  "data": {<br/>    &lt;...&gt;,<br/>    "msteams": {<br/>      "type": "task/fetch"<br/>    }<br/>  }<br/>}</pre>  |

## <a name="see-also"></a>См. также

* [Microsoft Teams модуль задачи - nodejs](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs/blob/master/src/TeamsBot.ts)
* [Образцы Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).