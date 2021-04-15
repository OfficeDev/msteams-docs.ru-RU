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
# <a name="using-task-modules-from-microsoft-teams-bots"></a><span data-ttu-id="3892b-104">Использование модулей задач от ботов Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="3892b-104">Using task modules from Microsoft Teams bots</span></span>

<span data-ttu-id="3892b-105">Модули задач можно вызывать из ботов Microsoft Teams с помощью кнопок на адаптивных картах и картах Bot Framework (Hero, Thumbnail и Office 365 Connector).</span><span class="sxs-lookup"><span data-stu-id="3892b-105">Task modules can be invoked from Microsoft Teams bots using buttons on Adaptive cards and Bot Framework cards (Hero, Thumbnail, and Office 365 Connector).</span></span> <span data-ttu-id="3892b-106">Модули задач часто являются более удобными для пользователей, чем несколько этапов беседы, в которых вы как разработчик должны отслеживать состояние бота и позволять пользователю прерывать или отменять последовательность.</span><span class="sxs-lookup"><span data-stu-id="3892b-106">Task modules are often a better user experience than multiple conversation steps where you as a developer have to keep track of bot state and allow the user to interrupt/cancel the sequence.</span></span>

<span data-ttu-id="3892b-107">Существует два способа ссылки на модули задач:</span><span class="sxs-lookup"><span data-stu-id="3892b-107">There are two ways of invoking task modules:</span></span>

* <span data-ttu-id="3892b-108">**Новый вид сообщения вызова `task/fetch` .**</span><span class="sxs-lookup"><span data-stu-id="3892b-108">**A new kind of invoke message `task/fetch`.**</span></span> <span data-ttu-id="3892b-109">Использование действия карты для карт Bot Framework или действия карт для адаптивных карт с модулем задач (URL-адрес или адаптивная карта) извлекается динамически из `invoke` [](~/task-modules-and-cards/cards/cards-actions.md#invoke) `Action.Submit` [](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) `task/fetch` вашего бота.</span><span class="sxs-lookup"><span data-stu-id="3892b-109">Using the `invoke` [card action](~/task-modules-and-cards/cards/cards-actions.md#invoke) for Bot Framework cards, or the `Action.Submit` [card action](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) for Adaptive cards, with `task/fetch`, the task module (either a URL or an Adaptive card) is fetched dynamically from your bot.</span></span>
* <span data-ttu-id="3892b-110">**URL-адреса глубоких ссылок.**</span><span class="sxs-lookup"><span data-stu-id="3892b-110">**Deep link URLs.**</span></span> <span data-ttu-id="3892b-111">Используя [синтаксис](~/task-modules-and-cards/what-are-task-modules.md#task-module-deep-link-syntax)глубокой ссылки для модулей задач, вы можете использовать действие карты для карт Bot Framework или действие карты для адаптивных карт `openUrl` [](~/task-modules-and-cards/cards/cards-actions.md#openurl) `Action.OpenUrl` [](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) соответственно.</span><span class="sxs-lookup"><span data-stu-id="3892b-111">Using the [deep link syntax for task modules](~/task-modules-and-cards/what-are-task-modules.md#task-module-deep-link-syntax), you can use the `openUrl` [card action](~/task-modules-and-cards/cards/cards-actions.md#openurl) for Bot Framework cards or the `Action.OpenUrl` [card action](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) for Adaptive cards, respectively.</span></span> <span data-ttu-id="3892b-112">С URL-адресами глубоких ссылок URL-адрес модуля задач или корпус адаптивной карты, очевидно, известен заранее, избегая обратного пути сервера по отношению к `task/fetch` .</span><span class="sxs-lookup"><span data-stu-id="3892b-112">With deep link URLs, the task module URL or Adaptive card body is obviously known in advance, avoiding a server round-trip relative to `task/fetch`.</span></span>

>[!IMPORTANT]
><span data-ttu-id="3892b-113">Чтобы обеспечить безопасность сообщений, каждый из них должен реализовать `url` `fallbackUrl` протокол шифрования HTTPS.</span><span class="sxs-lookup"><span data-stu-id="3892b-113">To ensure secure communications, each `url` and `fallbackUrl` must implement the HTTPS encryption protocol.</span></span>

## <a name="invoking-a-task-module-via-taskfetch"></a><span data-ttu-id="3892b-114">Ссылки на модуль задач через задачу/извлечение</span><span class="sxs-lookup"><span data-stu-id="3892b-114">Invoking a task module via task/fetch</span></span>

<span data-ttu-id="3892b-115">Когда объект действия карточки или инициализирован надлежащим образом (подробнее см. ниже), когда пользователь нажимает кнопку, сообщение отправляется `value` `invoke` `Action.Submit` `invoke` боту.</span><span class="sxs-lookup"><span data-stu-id="3892b-115">When the `value` object of the `invoke` card action or `Action.Submit` is initialized in the proper way (explained in more detail below), when a user presses the button an `invoke` message is sent to the bot.</span></span> <span data-ttu-id="3892b-116">В ответе HTTP на сообщение есть объект `invoke` [TaskInfo,](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) встроенный в объект оболочки, который Teams использует для отображения модуля задач.</span><span class="sxs-lookup"><span data-stu-id="3892b-116">In the HTTP response to the `invoke` message, there's a [TaskInfo object](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) embedded in a wrapper object, which Teams uses to display the task module.</span></span>

![задача/извлечение запроса/ответа](~/assets/images/task-module/task-module-invoke-request-response.png)

<span data-ttu-id="3892b-118">Рассмотрим каждый шаг более подробно:</span><span class="sxs-lookup"><span data-stu-id="3892b-118">Let's look at each step in a bit more detail:</span></span>

1. <span data-ttu-id="3892b-119">В этом примере показана карта Bot Framework Hero с действием карточки `invoke` ["Купить".](~/task-modules-and-cards/cards/cards-actions.md#invoke)</span><span class="sxs-lookup"><span data-stu-id="3892b-119">This example shows a Bot Framework Hero card with a "Buy" `invoke` [card action](~/task-modules-and-cards/cards/cards-actions.md#invoke).</span></span> <span data-ttu-id="3892b-120">Значение свойства — остальная часть объекта может быть `type` `task/fetch` `value` любой, что вам нравится.</span><span class="sxs-lookup"><span data-stu-id="3892b-120">The value of the `type` property is `task/fetch` - the rest of the `value` object can be whatever you like.</span></span>
2. <span data-ttu-id="3892b-121">Бот получает сообщение `invoke` HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="3892b-121">The bot receives the `invoke` HTTP POST message.</span></span>
3. <span data-ttu-id="3892b-122">Бот создает объект отклика и возвращает его в тело ответа POST с кодом ответа HTTP 200.</span><span class="sxs-lookup"><span data-stu-id="3892b-122">The bot creates a response object and returns it in the body of the POST response with an HTTP 200 response code.</span></span> <span data-ttu-id="3892b-123">Схема ответов описана ниже в обсуждении [задачи/отправки,](#the-flexibility-of-tasksubmit)но теперь важно помнить, что тело ответа HTTP содержит объект [TaskInfo,](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) встроенный в объект оболочки, например:</span><span class="sxs-lookup"><span data-stu-id="3892b-123">The schema for responses is described [below in the discussion on task/submit](#the-flexibility-of-tasksubmit), but the important thing to remember now is that the body of the HTTP response contains a [TaskInfo object](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) embedded in a wrapper object, e.g.:</span></span>

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

    <span data-ttu-id="3892b-124">Событие и его ответ для ботов похожи концептуально на функцию клиента `task/fetch` `microsoftTeams.tasks.startTask()` SDK.</span><span class="sxs-lookup"><span data-stu-id="3892b-124">The `task/fetch` event and its response for bots is similar, conceptually, to the `microsoftTeams.tasks.startTask()` function in the client SDK.</span></span>
4. <span data-ttu-id="3892b-125">Microsoft Teams отображает модуль задач.</span><span class="sxs-lookup"><span data-stu-id="3892b-125">Microsoft Teams displays the task module.</span></span>

## <a name="submitting-the-result-of-a-task-module"></a><span data-ttu-id="3892b-126">Отправка результатов модуля задач</span><span class="sxs-lookup"><span data-stu-id="3892b-126">Submitting the result of a task module</span></span>

<span data-ttu-id="3892b-127">Когда пользователь завершает работу с модулем задач, отправка результата [](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module)обратно боту похожа на то, как он работает со вкладками, но есть несколько различий, поэтому он также описан здесь.</span><span class="sxs-lookup"><span data-stu-id="3892b-127">When the user is finished with the task module, submitting the result back to the bot is similar [to the way it works with tabs](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module), but there are a few differences, so it's described here too.</span></span>

* <span data-ttu-id="3892b-128">**HTML/JavaScript ( `TaskInfo.url` )**.</span><span class="sxs-lookup"><span data-stu-id="3892b-128">**HTML/JavaScript (`TaskInfo.url`)**.</span></span> <span data-ttu-id="3892b-129">После проверки того, что вошел пользователь, вы вызываете функцию SDK (далее она называется для целей `microsoftTeams.tasks.submitTask()` `submitTask()` читаемости).</span><span class="sxs-lookup"><span data-stu-id="3892b-129">Once you've validated what the user has entered, you call the `microsoftTeams.tasks.submitTask()` SDK function (referred to hereafter as `submitTask()` for readability purposes).</span></span> <span data-ttu-id="3892b-130">Вы можете звонить без параметров, если вы просто хотите, чтобы Teams закрыли модуль задач, но большую часть времени вы хотите передать объект или строку `submitTask()` в `submitHandler` ваш .</span><span class="sxs-lookup"><span data-stu-id="3892b-130">You can call `submitTask()` without any parameters if you just want Teams to close the task module, but most of the time you'll want to pass an object or a string to your `submitHandler`.</span></span> <span data-ttu-id="3892b-131">Просто передай его в качестве первого `result` параметра.</span><span class="sxs-lookup"><span data-stu-id="3892b-131">Simply pass it as the first parameter, `result`.</span></span> <span data-ttu-id="3892b-132">Команды `submitHandler` вызовят: будет и будет `err` `null` `result` объектом или строкой, которую вы передали `submitTask()` .</span><span class="sxs-lookup"><span data-stu-id="3892b-132">Teams will invoke `submitHandler`: `err` will be `null` and `result` will be the object/string you passed to `submitTask()`.</span></span> <span data-ttu-id="3892b-133">Если вы вызываете с параметром, необходимо передать или массив строк: это позволяет Teams проверить, что приложение, отправляя результат, является тем же, что вызывалось в модуль `submitTask()` `result`  `appId` `appId` задач.</span><span class="sxs-lookup"><span data-stu-id="3892b-133">If you do call `submitTask()` with a `result` parameter, you **must** pass an `appId` or an array of `appId` strings: this allows Teams to validate that the app sending the result is the same one which invoked the task module.</span></span> <span data-ttu-id="3892b-134">Ваш бот получит `task/submit` сообщение, в том `result` числе, как описано [ниже](#payload-of-taskfetch-and-tasksubmit-messages).</span><span class="sxs-lookup"><span data-stu-id="3892b-134">Your bot will receive a `task/submit` message including `result` as described [below](#payload-of-taskfetch-and-tasksubmit-messages).</span></span>
* <span data-ttu-id="3892b-135">**Адаптивная карта ( `TaskInfo.card` )**.</span><span class="sxs-lookup"><span data-stu-id="3892b-135">**Adaptive card (`TaskInfo.card`)**.</span></span> <span data-ttu-id="3892b-136">Тело адаптивной карты (как заполнено пользователем) будет отправлено боту через сообщение, когда пользователь `task/submit` нажимает любую `Action.Submit` кнопку.</span><span class="sxs-lookup"><span data-stu-id="3892b-136">The Adaptive card body (as filled in by the user) will be sent to the bot via a `task/submit` message when the user presses any `Action.Submit` button.</span></span>

## <a name="the-flexibility-of-tasksubmit"></a><span data-ttu-id="3892b-137">Гибкость задачи/отправки</span><span class="sxs-lookup"><span data-stu-id="3892b-137">The flexibility of task/submit</span></span>

<span data-ttu-id="3892b-138">В предыдущем разделе вы узнали, что после завершения работы с модулем задач, вызываемом ботом, бот всегда получает `task/submit invoke` сообщение.</span><span class="sxs-lookup"><span data-stu-id="3892b-138">In the previous section, you learned that when the user finishes with a task module invoked from a bot, the bot always receives a `task/submit invoke` message.</span></span> <span data-ttu-id="3892b-139">В качестве разработчика у вас есть несколько *вариантов* ответа на `task/submit` сообщение:</span><span class="sxs-lookup"><span data-stu-id="3892b-139">As a developer, you have several options when *responding* to the `task/submit` message:</span></span>

| <span data-ttu-id="3892b-140">HTTP Body Response</span><span class="sxs-lookup"><span data-stu-id="3892b-140">HTTP Body Response</span></span>                      | <span data-ttu-id="3892b-141">Сценарий</span><span class="sxs-lookup"><span data-stu-id="3892b-141">Scenario</span></span>                                |
| --------------------------------------- | --------------------------------------- |
| <span data-ttu-id="3892b-142">Нет (игнорировать `task/submit` сообщение)</span><span class="sxs-lookup"><span data-stu-id="3892b-142">None (ignore the `task/submit` message)</span></span> | <span data-ttu-id="3892b-143">Самый простой ответ — это отсутствие ответа.</span><span class="sxs-lookup"><span data-stu-id="3892b-143">The simplest response is no response at all.</span></span> <span data-ttu-id="3892b-144">Ваш бот не обязан отвечать, когда пользователь завершает работу с модулем задач.</span><span class="sxs-lookup"><span data-stu-id="3892b-144">Your bot is not required to respond when the user is finished with the task module.</span></span> |
| <pre>{<br/>  "task": {<br/>    "type": "message",<br/>    "value": "Message text"<br/>  }<br/>}</pre> | <span data-ttu-id="3892b-145">Teams будет отображать значение в `value` всплывающее окно сообщения.</span><span class="sxs-lookup"><span data-stu-id="3892b-145">Teams will display the value of `value` in a popup message box.</span></span> |
| <pre>{<br/>  "task": {<br/>    "type": "continue",<br/>    "value": &lt;TaskInfo object&gt;<br/>  }<br/>}</pre> | <span data-ttu-id="3892b-146">Позволяет "цепить" последовательности адаптивных карт вместе в мастере и многошаговом опытом.</span><span class="sxs-lookup"><span data-stu-id="3892b-146">Allows you to "chain" sequences of Adaptive cards together in a wizard/multi-step experience.</span></span> <span data-ttu-id="3892b-147">_Обратите внимание, что цепочка адаптивных карт в последовательность является расширенным сценарием и не задокументирована здесь. Однако Node.js пример приложения поддерживает его, и его работа задокументирована в [README.md файле.](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)_</span><span class="sxs-lookup"><span data-stu-id="3892b-147">_Note that chaining Adaptive cards into a sequence is an advanced scenario and not documented here. The Node.js sample app supports it, however, and how it works is documented in [its README.md file](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)._</span></span> |

## <a name="payload-of-taskfetch-and-tasksubmit-messages"></a><span data-ttu-id="3892b-148">Полезное количество задач/извлечений и задач/отправки сообщений</span><span class="sxs-lookup"><span data-stu-id="3892b-148">Payload of task/fetch and task/submit messages</span></span>

<span data-ttu-id="3892b-149">В этом разделе определяется схема получения ботом объекта `task/fetch` `task/submit` или объекта Bot `Activity` Framework.</span><span class="sxs-lookup"><span data-stu-id="3892b-149">This section defines the schema of what your bot receives when it receives a `task/fetch` or `task/submit` Bot Framework `Activity` object.</span></span> <span data-ttu-id="3892b-150">Ниже отображаются важные верхнего уровня:</span><span class="sxs-lookup"><span data-stu-id="3892b-150">The important top-level appear below:</span></span>

| <span data-ttu-id="3892b-151">Свойство</span><span class="sxs-lookup"><span data-stu-id="3892b-151">Property</span></span> | <span data-ttu-id="3892b-152">Описание</span><span class="sxs-lookup"><span data-stu-id="3892b-152">Description</span></span>                          |
| -------- | ------------------------------------ |
| `type`   | <span data-ttu-id="3892b-153">Всегда будет `invoke`</span><span class="sxs-lookup"><span data-stu-id="3892b-153">Will always be `invoke`</span></span>              |
| `name`   | <span data-ttu-id="3892b-154">Либо, `task/fetch` либо `task/submit`</span><span class="sxs-lookup"><span data-stu-id="3892b-154">Either `task/fetch` or `task/submit`</span></span> |
| `value`  | <span data-ttu-id="3892b-155">Полезной нагрузки, определенной разработчиком.</span><span class="sxs-lookup"><span data-stu-id="3892b-155">The developer-defined payload.</span></span> <span data-ttu-id="3892b-156">Обычно структура объекта отражает то, что `value` было отправлено из Teams.</span><span class="sxs-lookup"><span data-stu-id="3892b-156">Normally the structure of the `value` object mirrors what was sent from Teams.</span></span> <span data-ttu-id="3892b-157">В этом случае, однако, это другое, потому что мы хотим поддерживать динамические извлечение () как из Bot Framework ( ) и адаптивные действия карты ( ), и нам нужен способ связи Teams с ботом в дополнение к тому, что было включено `task/fetch` `value` в `Action.Submit` `data` `context` `value` / `data` .</span><span class="sxs-lookup"><span data-stu-id="3892b-157">In this case, however, it's different because we want to support dynamic fetch (`task/fetch`) from both Bot Framework (`value`) and Adaptive card `Action.Submit` actions (`data`), and we need a way to communicate Teams `context` to the bot in addition to what was included in `value`/`data`.</span></span><br/><br/><span data-ttu-id="3892b-158">Мы объединяя эти два объекта в родительский объект:</span><span class="sxs-lookup"><span data-stu-id="3892b-158">We do this by combining the two into a parent object:</span></span><br/><br/><pre>{<br/>  "context": {<br/>    "theme": "default" &vert; "dark" &vert; "contrast",<br/>  },<br/>  "data": [value field from Bot Framework card] &vert; [data field from Adaptive Card] <br/>}</pre>  |

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---nodejs"></a><span data-ttu-id="3892b-159">Пример: получение и реагирование на задачу/получение и отправку сообщений вызовов — Node.js</span><span class="sxs-lookup"><span data-stu-id="3892b-159">Example: Receiving and responding to task/fetch and task/submit invoke messages - Node.js</span></span>

> [!NOTE]
> <span data-ttu-id="3892b-160">Пример кода, приведенного ниже, был изменен между техническим предварительным просмотром и окончательным выпуском этой функции: схема запроса изменена, чтобы следовать за тем, что было задокументировано `task/fetch` [в предыдущем разделе](#payload-of-taskfetch-and-tasksubmit-messages).</span><span class="sxs-lookup"><span data-stu-id="3892b-160">The sample code below was modified between Technical Preview and final release of this feature: the schema of the `task/fetch` request changed to follow what was [documented in the previous section](#payload-of-taskfetch-and-tasksubmit-messages).</span></span> <span data-ttu-id="3892b-161">То есть документация была правильной, но реализация не была.</span><span class="sxs-lookup"><span data-stu-id="3892b-161">That is, the documentation was correct but the implementation was not.</span></span> <span data-ttu-id="3892b-162">Ниже приведены `// for Technical Preview [...]` комментарии к измененным комментариям.</span><span class="sxs-lookup"><span data-stu-id="3892b-162">See the `// for Technical Preview [...]` comments below for what changed.</span></span>

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

<span data-ttu-id="3892b-163">*См. также* пример примера модуля задач [Microsoft Teams — примеры nodejs](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs/blob/master/src/TeamsBot.ts) и [Bot Framework.](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)</span><span class="sxs-lookup"><span data-stu-id="3892b-163">*See also*, [Microsoft Teams task module sample code — nodejs](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs/blob/master/src/TeamsBot.ts) and  [Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---c"></a><span data-ttu-id="3892b-164">Пример: получение и реагирование на задачу/получение и отправку сообщений вызовов - C #</span><span class="sxs-lookup"><span data-stu-id="3892b-164">Example: Receiving and responding to task/fetch and task/submit invoke messages - C#</span></span>

<span data-ttu-id="3892b-165">В C# ботах сообщения обрабатываются контроллером, `invoke` `HttpResponseMessage()` обрабатывая `Activity` сообщение.</span><span class="sxs-lookup"><span data-stu-id="3892b-165">In C# bots, `invoke` messages are processed by an `HttpResponseMessage()` controller processing an `Activity` message.</span></span> <span data-ttu-id="3892b-166">Запросы `task/fetch` и ответы — это `task/submit` JSON.</span><span class="sxs-lookup"><span data-stu-id="3892b-166">The `task/fetch` and `task/submit` requests and responses are JSON.</span></span> <span data-ttu-id="3892b-167">В C# не так удобно иметь дело с необработанных JSON, как в Node.js, поэтому для обработки сериализации в JSON и из JSON необходимы классы обертки.</span><span class="sxs-lookup"><span data-stu-id="3892b-167">In C#, it's not as convenient to deal with raw JSON as it is in Node.js, so you need wrapper classes to handle the serialization to and from JSON.</span></span> <span data-ttu-id="3892b-168">Прямой поддержки этого в microsoft Teams [C# SDK](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) пока нет, но вы можете увидеть пример того, как будут выглядеть эти простые классы оболочки в C# примере приложения [.](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Models/TaskModel.cs)</span><span class="sxs-lookup"><span data-stu-id="3892b-168">There's no direct support for this in the Microsoft Teams [C# SDK](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) yet, but you can see an example of what these simple wrapper classes would look like in the [C# sample app](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Models/TaskModel.cs).</span></span>

<span data-ttu-id="3892b-169">Ниже приведен пример кода в C# для обработки и сообщений с помощью этих классов оболочки ( , ), выдержки `task/fetch` `task/submit` из `TaskInfo` `TaskEnvelope` [примера](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs):</span><span class="sxs-lookup"><span data-stu-id="3892b-169">Below is example code in C# for handling `task/fetch` and `task/submit` messages using these wrapper classes (`TaskInfo`, `TaskEnvelope`), excerpted from the [sample](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs):</span></span>

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

<span data-ttu-id="3892b-170">Не показана в вышеуказанной примере функция, которая задает , и свойства `SetTaskInfo()` `height` объекта для каждого `width` `title` `TaskInfo` случая.</span><span class="sxs-lookup"><span data-stu-id="3892b-170">Not shown in the above example is the `SetTaskInfo()` function, which sets the `height`, `width`, and `title` properties of the `TaskInfo` object for each case.</span></span> <span data-ttu-id="3892b-171">Вот исходный [код setTaskInfo()](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs).</span><span class="sxs-lookup"><span data-stu-id="3892b-171">Here's the [source code for SetTaskInfo()](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs).</span></span>

### <a name="bot-framework-card-actions-vs-adaptive-card-actionsubmit-actions"></a><span data-ttu-id="3892b-172">Действия карты Bot Framework против действий адаптивной карты Action.Submit</span><span class="sxs-lookup"><span data-stu-id="3892b-172">Bot Framework card actions vs. Adaptive card Action.Submit actions</span></span>

<span data-ttu-id="3892b-173">Схема действий карт Bot Framework немного отличается от действий адаптивной `Action.Submit` карты.</span><span class="sxs-lookup"><span data-stu-id="3892b-173">The schema for Bot Framework card actions is slightly different from Adaptive card `Action.Submit` actions.</span></span> <span data-ttu-id="3892b-174">В результате способ вызова модулей задач также немного отличается: объект содержит объект, чтобы он не мешал другим свойствам `data` `Action.Submit` `msteams` карты.</span><span class="sxs-lookup"><span data-stu-id="3892b-174">As a result, the way to invoke task modules is slightly different too: the `data` object in `Action.Submit` contains an `msteams` object so it won't interfere with other properties in the card.</span></span> <span data-ttu-id="3892b-175">В следующей таблице показан пример каждого из них:</span><span class="sxs-lookup"><span data-stu-id="3892b-175">The following table shows an example of each:</span></span>

| <span data-ttu-id="3892b-176">Действие карты Bot Framework</span><span class="sxs-lookup"><span data-stu-id="3892b-176">Bot Framework card action</span></span>                              | <span data-ttu-id="3892b-177">Действие адаптивной карты Action.Submit</span><span class="sxs-lookup"><span data-stu-id="3892b-177">Adaptive card Action.Submit action</span></span>                     |
| ------------------------------------------------------ | ------------------------------------------------------ |
| <pre>{<br/>  "type": "invoke",<br/>  "title": "Buy",<br/>  "value": {<br/>    "type": "task/fetch",<br/>    &lt;...&gt;<br/>  }<br/>}</pre> | <pre>{<br/>  "type": "Action.Submit",<br/>  "id": "btnBuy",<br/>  "title": "Buy",<br/>  "data": {<br/>    &lt;...&gt;,<br/>    "msteams": {<br/>      "type": "task/fetch"<br/>    }<br/>  }<br/>}</pre>  |
