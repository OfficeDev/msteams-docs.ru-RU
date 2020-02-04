---
title: Использование модулей задач в Microsoft Teams Боты
description: Использование модулей задач с Microsoft Teams Боты, в том числе карточек, карты, адаптивные карты и ссылки на Bot Framework.
keywords: модули задач Teams Боты
ms.openlocfilehash: 3a0e4591dbb26ff4afa8cc06edc0a03365da0eca
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675368"
---
# <a name="using-task-modules-from-microsoft-teams-bots"></a><span data-ttu-id="baee3-104">Использование модулей задач из Microsoft Teams Боты</span><span class="sxs-lookup"><span data-stu-id="baee3-104">Using task modules from Microsoft Teams bots</span></span>

<span data-ttu-id="baee3-105">Модули задач можно вызывать из Microsoft Teams боты с помощью кнопок на адаптивных карточках и карточек Bot-инфраструктуры (главный Имиджевый баннер, эскиз и Office 365 Connector).</span><span class="sxs-lookup"><span data-stu-id="baee3-105">Task modules can be invoked from Microsoft Teams bots using buttons on Adaptive cards and Bot Framework cards (Hero, Thumbnail, and Office 365 Connector).</span></span> <span data-ttu-id="baee3-106">Модули задач часто работают быстрее, чем несколько действий, которые разработчик должен отслеживать состояние Bot и позволять пользователю прерывать или отменять последовательность.</span><span class="sxs-lookup"><span data-stu-id="baee3-106">Task modules are often a better user experience than multiple conversation steps where you as a developer have to keep track of bot state and allow the user to interrupt/cancel the sequence.</span></span>

<span data-ttu-id="baee3-107">Существует два способа вызова модулей задач:</span><span class="sxs-lookup"><span data-stu-id="baee3-107">There are two ways of invoking task modules:</span></span>

* <span data-ttu-id="baee3-108">**Новый тип сообщения `task/fetch`вызова.**</span><span class="sxs-lookup"><span data-stu-id="baee3-108">**A new kind of invoke message `task/fetch`.**</span></span> <span data-ttu-id="baee3-109">`invoke` С помощью [действия карточки](~/task-modules-and-cards/cards/cards-actions.md#invoke) для карточек ленты (Bot) или `Action.Submit` [действия карты](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) для адаптивных карт с `task/fetch`помощью модуля задач (URL-адрес или Адаптивная карта) выполняется динамическое извлечение из ленты.</span><span class="sxs-lookup"><span data-stu-id="baee3-109">Using the `invoke` [card action](~/task-modules-and-cards/cards/cards-actions.md#invoke) for Bot Framework cards, or the `Action.Submit` [card action](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) for Adaptive cards, with `task/fetch`, the task module (either a URL or an Adaptive card) is fetched dynamically from your bot.</span></span>
* <span data-ttu-id="baee3-110">**URL-адреса глубокой ссылки.**</span><span class="sxs-lookup"><span data-stu-id="baee3-110">**Deep link URLs.**</span></span> <span data-ttu-id="baee3-111">С помощью [синтаксиса глубокой ссылки для модулей задач](~/task-modules-and-cards/what-are-task-modules.md#task-module-deep-link-syntax)можно использовать `openUrl` [действия с картой](~/task-modules-and-cards/cards/cards-actions.md#openurl) для карточек ленты или `Action.OpenUrl` [действия карты](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) для адаптивных карт соответственно.</span><span class="sxs-lookup"><span data-stu-id="baee3-111">Using the [deep link syntax for task modules](~/task-modules-and-cards/what-are-task-modules.md#task-module-deep-link-syntax), you can use the `openUrl` [card action](~/task-modules-and-cards/cards/cards-actions.md#openurl) for Bot Framework cards or the `Action.OpenUrl` [card action](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) for Adaptive cards, respectively.</span></span> <span data-ttu-id="baee3-112">При использовании URL-адресов с глубокими ссылками URL-адрес модуля задачи или адаптивный текст карточки очевидно известен заранее, что позволяет избежать `task/fetch`кругового пути к серверу.</span><span class="sxs-lookup"><span data-stu-id="baee3-112">With deep link URLs, the task module URL or Adaptive card body is obviously known in advance, avoiding a server round-trip relative to `task/fetch`.</span></span>

## <a name="invoking-a-task-module-via-taskfetch"></a><span data-ttu-id="baee3-113">Вызов модуля задачи с помощью задачи/извлечения</span><span class="sxs-lookup"><span data-stu-id="baee3-113">Invoking a task module via task/fetch</span></span>

<span data-ttu-id="baee3-114">Когда `value` объект действия `invoke` карточки или `Action.Submit` инициализирован правильно (подробно описывается ниже), когда пользователь нажимает кнопку, `invoke` сообщение отправляется в Bot.</span><span class="sxs-lookup"><span data-stu-id="baee3-114">When the `value` object of the `invoke` card action or `Action.Submit` is initialized in the proper way (explained in more detail below), when a user presses the button an `invoke` message is sent to the bot.</span></span> <span data-ttu-id="baee3-115">В HTTP-ответе на `invoke` сообщение существует [объект таскинфо](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) , внедренный в объект-оболочку, который Teams использует для отображения модуля задачи.</span><span class="sxs-lookup"><span data-stu-id="baee3-115">In the HTTP response to the `invoke` message, there's a [TaskInfo object](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) embedded in a wrapper object, which Teams uses to display the task module.</span></span>

![запрос/ответ на задачу/получение](~/assets/images/task-module/task-module-invoke-request-response.png)

<span data-ttu-id="baee3-117">Рассмотрим каждый шаг чуть подробнее:</span><span class="sxs-lookup"><span data-stu-id="baee3-117">Let's look at each step in a bit more detail:</span></span>

1. <span data-ttu-id="baee3-118">В этом примере показана карточка главный Имиджевый баннер Framework с `invoke` [действием](~/task-modules-and-cards/cards/cards-actions.md#invoke)"Купить" карточки.</span><span class="sxs-lookup"><span data-stu-id="baee3-118">This example shows a Bot Framework Hero card with a "Buy" `invoke` [card action](~/task-modules-and-cards/cards/cards-actions.md#invoke).</span></span> <span data-ttu-id="baee3-119">Значение `type` свойства — `task/fetch` остальная часть `value` объекта может быть любым.</span><span class="sxs-lookup"><span data-stu-id="baee3-119">The value of the `type` property is `task/fetch` - the rest of the `value` object can be whatever you like.</span></span>
2. <span data-ttu-id="baee3-120">Bot получает сообщение `invoke` HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="baee3-120">The bot receives the `invoke` HTTP POST message.</span></span>
3. <span data-ttu-id="baee3-121">Bot создает объект Response и возвращает его в тексте ответа POST с кодом отклика HTTP 200.</span><span class="sxs-lookup"><span data-stu-id="baee3-121">The bot creates a response object and returns it in the body of the POST response with an HTTP 200 response code.</span></span> <span data-ttu-id="baee3-122">Схема для ответов описана [ниже в разделе "задача/Передача](#the-flexibility-of-tasksubmit)", но важная вещь состоит в том, что текст HTTP-ответа содержит [объект таскинфо](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) , внедренный в объект-оболочку, например:</span><span class="sxs-lookup"><span data-stu-id="baee3-122">The schema for responses is described [below in the discussion on task/submit](#the-flexibility-of-tasksubmit), but the important thing to remember now is that the body of the HTTP response contains a [TaskInfo object](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) embedded in a wrapper object, e.g.:</span></span>

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
    
    <span data-ttu-id="baee3-123">`task/fetch` Событие и его ответ для Боты похожи, концептуально, в `microsoftTeams.tasks.startTask()` функцию в клиентской SDK.</span><span class="sxs-lookup"><span data-stu-id="baee3-123">The `task/fetch` event and its response for bots is similar, conceptually, to the `microsoftTeams.tasks.startTask()` function in the client SDK.</span></span>
4. <span data-ttu-id="baee3-124">В Microsoft Teams отображается модуль задач.</span><span class="sxs-lookup"><span data-stu-id="baee3-124">Microsoft Teams displays the task module.</span></span>

## <a name="submitting-the-result-of-a-task-module"></a><span data-ttu-id="baee3-125">Отправка результата модуля задачи</span><span class="sxs-lookup"><span data-stu-id="baee3-125">Submitting the result of a task module</span></span>

<span data-ttu-id="baee3-126">Когда пользователь завершает работу с модулем задач, отправка результата обратно на сервер-Bot похожа на то, [как он работает с вкладками](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module), но существует несколько различий, поэтому он также описан здесь.</span><span class="sxs-lookup"><span data-stu-id="baee3-126">When the user is finished with the task module, submitting the result back to the bot is similar [to the way it works with tabs](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module), but there are a few differences, so it's described here too.</span></span>

* <span data-ttu-id="baee3-127">**HTML/JavaScript (`TaskInfo.url`)**.</span><span class="sxs-lookup"><span data-stu-id="baee3-127">**HTML/JavaScript (`TaskInfo.url`)**.</span></span> <span data-ttu-id="baee3-128">Когда вы проверили введенные пользователем сведения, вы вызываете `microsoftTeams.tasks.submitTask()` функцию SDK (которая упоминается в `submitTask()` дальнейшем для удобства чтения).</span><span class="sxs-lookup"><span data-stu-id="baee3-128">Once you've validated what the user has entered, you call the `microsoftTeams.tasks.submitTask()` SDK function (referred to hereafter as `submitTask()` for readability purposes).</span></span> <span data-ttu-id="baee3-129">Вы можете вызвать `submitTask()` без параметров, если вы хотите, чтобы команда закрывала модуль задач, но в большинстве случаев требуется передать объект или строку в `submitHandler`.</span><span class="sxs-lookup"><span data-stu-id="baee3-129">You can call `submitTask()` without any parameters if you just want Teams to close the task module, but most of the time you'll want to pass an object or a string to your `submitHandler`.</span></span> <span data-ttu-id="baee3-130">Просто передавайте его в качестве первого параметра `result`,.</span><span class="sxs-lookup"><span data-stu-id="baee3-130">Simply pass it as the first parameter, `result`.</span></span> <span data-ttu-id="baee3-131">Teams `submitHandler`вызовет `err` : будет `null` и `result` будет объект или строка, которые вы передали `submitTask()`.</span><span class="sxs-lookup"><span data-stu-id="baee3-131">Teams will invoke `submitHandler`: `err` will be `null` and `result` will be the object/string you passed to `submitTask()`.</span></span> <span data-ttu-id="baee3-132">При вызове `submitTask()` с `result` параметром **необходимо** передать объект `appId` или массив `appId` строк: Это позволяет Teams проверить, что приложение отправляет результат, то же, что вызвало модуль задачи.</span><span class="sxs-lookup"><span data-stu-id="baee3-132">If you do call `submitTask()` with a `result` parameter, you **must** pass an `appId` or an array of `appId` strings: this allows Teams to validate that the app sending the result is the same one which invoked the task module.</span></span> <span data-ttu-id="baee3-133">Ваш робот получит `task/submit` сообщение, в `result` том числе, как описано [ниже](#payload-of-taskfetch-and-tasksubmit-messages).</span><span class="sxs-lookup"><span data-stu-id="baee3-133">Your bot will receive a `task/submit` message including `result` as described [below](#payload-of-taskfetch-and-tasksubmit-messages).</span></span>
* <span data-ttu-id="baee3-134">**Адаптивная Карта`TaskInfo.card`()**.</span><span class="sxs-lookup"><span data-stu-id="baee3-134">**Adaptive card (`TaskInfo.card`)**.</span></span> <span data-ttu-id="baee3-135">Текст адаптивной карточки (заполняемой пользователем) будет отправляться в Bot через `task/submit` сообщение, когда пользователь нажимает любую `Action.Submit` кнопку.</span><span class="sxs-lookup"><span data-stu-id="baee3-135">The Adaptive card body (as filled in by the user) will be sent to the bot via a `task/submit` message when the user presses any `Action.Submit` button.</span></span>

## <a name="the-flexibility-of-tasksubmit"></a><span data-ttu-id="baee3-136">Гибкость задачи и отсылки</span><span class="sxs-lookup"><span data-stu-id="baee3-136">The flexibility of task/submit</span></span>

<span data-ttu-id="baee3-137">В предыдущем разделе вы узнали, что когда пользователь завершается с помощью модуля задачи, вызванного из Bot, Bot всегда получает `task/submit invoke` сообщение.</span><span class="sxs-lookup"><span data-stu-id="baee3-137">In the previous section, you learned that when the user finishes with a task module invoked from a bot, the bot always receives a `task/submit invoke` message.</span></span> <span data-ttu-id="baee3-138">Как разработчик, у вас есть несколько вариантов *ответа* на `task/submit` сообщение:</span><span class="sxs-lookup"><span data-stu-id="baee3-138">As a developer, you have several options when *responding* to the `task/submit` message:</span></span>

| <span data-ttu-id="baee3-139">Ответ основного текста HTTP</span><span class="sxs-lookup"><span data-stu-id="baee3-139">HTTP Body Response</span></span>                      | <span data-ttu-id="baee3-140">Сценарий</span><span class="sxs-lookup"><span data-stu-id="baee3-140">Scenario</span></span>                                |
| --------------------------------------- | --------------------------------------- |
| <span data-ttu-id="baee3-141">Нет (пропускать `task/submit` сообщение)</span><span class="sxs-lookup"><span data-stu-id="baee3-141">None (ignore the `task/submit` message)</span></span> | <span data-ttu-id="baee3-142">Самый простой ответ вообще не отвечает.</span><span class="sxs-lookup"><span data-stu-id="baee3-142">The simplest response is no response at all.</span></span> <span data-ttu-id="baee3-143">Ваш робот не должен отвечать, когда пользователь завершает работу с модулем задач.</span><span class="sxs-lookup"><span data-stu-id="baee3-143">Your bot is not required to respond when the user is finished with the task module.</span></span> |
| <pre>{<br/>  "task": {<br/>    "type": "message",<br/>    "value": "Message text"<br/>  }<br/>}</pre> | <span data-ttu-id="baee3-144">Teams отобразит значение `value` всплывающего окна сообщения.</span><span class="sxs-lookup"><span data-stu-id="baee3-144">Teams will display the value of `value` in a popup message box.</span></span> |
| <pre>{<br/>  "task": {<br/>    "type": "continue",<br/>    "value": &lt;TaskInfo object&gt;<br/>  }<br/>}</pre> | <span data-ttu-id="baee3-145">Позволяет "цепочку" цепочек адаптивных карточек в мастере и многоэтапной работе.</span><span class="sxs-lookup"><span data-stu-id="baee3-145">Allows you to "chain" sequences of Adaptive cards together in a wizard/multi-step experience.</span></span> <span data-ttu-id="baee3-146">_Обратите внимание, что сцепление адаптивных карт в последовательность является расширенным сценарием и не задокументировано здесь. Однако пример приложения Node. js поддерживает его, и как это работает в [файле readme.md](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)._</span><span class="sxs-lookup"><span data-stu-id="baee3-146">_Note that chaining Adaptive cards into a sequence is an advanced scenario and not documented here. The Node.js sample app supports it, however, and how it works is documented in [its README.md file](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)._</span></span> |

## <a name="payload-of-taskfetch-and-tasksubmit-messages"></a><span data-ttu-id="baee3-147">Полезные данные о задачах, получении и задачах и отправляя сообщения</span><span class="sxs-lookup"><span data-stu-id="baee3-147">Payload of task/fetch and task/submit messages</span></span>

<span data-ttu-id="baee3-148">В этом разделе определяется схема того, что Bot получает, `task/fetch` когда он получает объект `task/submit` или объект `Activity` Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="baee3-148">This section defines the schema of what your bot receives when it receives a `task/fetch` or `task/submit` Bot Framework `Activity` object.</span></span> <span data-ttu-id="baee3-149">Ниже приведен самый важный уровень верхнего уровня:</span><span class="sxs-lookup"><span data-stu-id="baee3-149">The important top-level appear below:</span></span>

| <span data-ttu-id="baee3-150">Свойство</span><span class="sxs-lookup"><span data-stu-id="baee3-150">Property</span></span> | <span data-ttu-id="baee3-151">Описание</span><span class="sxs-lookup"><span data-stu-id="baee3-151">Description</span></span>                          |
| -------- | ------------------------------------ |
| `type`   | <span data-ttu-id="baee3-152">Всегда будет`invoke`</span><span class="sxs-lookup"><span data-stu-id="baee3-152">Will always be `invoke`</span></span>              |
| `name`   | <span data-ttu-id="baee3-153">Один `task/fetch` или`task/submit`</span><span class="sxs-lookup"><span data-stu-id="baee3-153">Either `task/fetch` or `task/submit`</span></span> |
| `value`  | <span data-ttu-id="baee3-154">Полезные данные, определенные разработчиком.</span><span class="sxs-lookup"><span data-stu-id="baee3-154">The developer-defined payload.</span></span> <span data-ttu-id="baee3-155">Как правило, структура `value` объекта отражается на том, что было отправлено из Teams.</span><span class="sxs-lookup"><span data-stu-id="baee3-155">Normally the structure of the `value` object mirrors what was sent from Teams.</span></span> <span data-ttu-id="baee3-156">В этом случае, однако, это отличается, так как мы хотим`task/fetch`поддерживать динамическую выборку () из обеих действий`value`: Bot Framework ( `Action.Submit` ) и`data`адаптивных карт (), и нам нужен способ `context` для обмена командами с Bot в дополнение к тому `value` / `data`, что было включено в.</span><span class="sxs-lookup"><span data-stu-id="baee3-156">In this case, however, it's different because we want to support dynamic fetch (`task/fetch`) from both Bot Framework (`value`) and Adaptive card `Action.Submit` actions (`data`), and we need a way to communicate Teams `context` to the bot in addition to what was included in `value`/`data`.</span></span><br/><br/><span data-ttu-id="baee3-157">Для этого необходимо объединить два объекта в родительский.</span><span class="sxs-lookup"><span data-stu-id="baee3-157">We do this by combining the two into a parent object:</span></span><br/><br/><pre>{<br/>  "context": {<br/>    "theme": "default" &vert; "dark" &vert; "contrast",<br/>  },<br/>  "data": [value field from Bot Framework card] &vert; [data field from Adaptive Card] <br/>}</pre>  |

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---nodejs"></a><span data-ttu-id="baee3-158">Пример: получение и ответ на сообщения о задачах, получении и задачах и вызываемых запросах — Node. js</span><span class="sxs-lookup"><span data-stu-id="baee3-158">Example: Receiving and responding to task/fetch and task/submit invoke messages - Node.js</span></span>

<span data-ttu-id="baee3-159">Работа с `invoke` сообщениями в среде Bot может быть немного сложнее, так как в пакет SDK для ленты нет формальной поддержки.</span><span class="sxs-lookup"><span data-stu-id="baee3-159">Dealing with `invoke` messages in Bot Framework can be a little tricky because there's no formal support for them in the Bot Framework SDK.</span></span> <span data-ttu-id="baee3-160">Для простоты в Teams были созданы `onInvoke()` вспомогательные функции в [пакете ботбуилдер-Teams NPM (для Node. js)](https://www.npmjs.com/package/botbuilder-teams).</span><span class="sxs-lookup"><span data-stu-id="baee3-160">To make it easier, Teams has created `onInvoke()` helper functions in the [botbuilder-teams npm package (for Node.js)](https://www.npmjs.com/package/botbuilder-teams).</span></span> <span data-ttu-id="baee3-161">В этом примере ниже показано, как это сделать:</span><span class="sxs-lookup"><span data-stu-id="baee3-161">This example below shows how to do it:</span></span>

> [!NOTE]
> <span data-ttu-id="baee3-162">Приведенный ниже пример кода был изменен между техническим и окончательным выпуском этой функции: схема `task/fetch` запроса изменилась [на следующий пример.](#payload-of-taskfetch-and-tasksubmit-messages)</span><span class="sxs-lookup"><span data-stu-id="baee3-162">The sample code below was modified between Technical Preview and final release of this feature: the schema of the `task/fetch` request changed to follow what was [documented in the previous section](#payload-of-taskfetch-and-tasksubmit-messages).</span></span> <span data-ttu-id="baee3-163">Это значит, что документация была правильной, но не была реализована.</span><span class="sxs-lookup"><span data-stu-id="baee3-163">That is, the documentation was correct but the implementation was not.</span></span> <span data-ttu-id="baee3-164">Ознакомьтесь с `// for Technical Preview [...]` комментариями, которые вы изменили.</span><span class="sxs-lookup"><span data-stu-id="baee3-164">See the `// for Technical Preview [...]` comments below for what changed.</span></span>

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

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---c"></a><span data-ttu-id="baee3-165">Пример: получение и ответ на сообщения о задачах, выдачах и задачах и запросах Invoke-C #</span><span class="sxs-lookup"><span data-stu-id="baee3-165">Example: Receiving and responding to task/fetch and task/submit invoke messages - C#</span></span>

<span data-ttu-id="baee3-166">В C# Боты `invoke` сообщения обрабатываются с помощью `HttpResponseMessage()` обработки `Activity` сообщения контроллера.</span><span class="sxs-lookup"><span data-stu-id="baee3-166">In C# bots, `invoke` messages are processed by an `HttpResponseMessage()` controller processing an `Activity` message.</span></span> <span data-ttu-id="baee3-167">`task/fetch` Запросы и ответы — `task/submit` JSON.</span><span class="sxs-lookup"><span data-stu-id="baee3-167">The `task/fetch` and `task/submit` requests and responses are JSON.</span></span> <span data-ttu-id="baee3-168">В C# неудобно работать с RAW JSON, так как он находится в файле Node. js, поэтому для обработки сериализации и последующего использования JSON необходимы классы оберток.</span><span class="sxs-lookup"><span data-stu-id="baee3-168">In C#, it's not as convenient to deal with raw JSON as it is in Node.js, so you need wrapper classes to handle the serialization to and from JSON.</span></span> <span data-ttu-id="baee3-169">В Microsoft Teams [SDK](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) нет прямой поддержки, но вы можете увидеть пример того, как будут выглядеть эти простые классы оберток в [образце приложения на языке C#](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Models/TaskModel.cs).</span><span class="sxs-lookup"><span data-stu-id="baee3-169">There's no direct support for this in the Microsoft Teams [C# SDK](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) yet, but you can see an example of what these simple wrapper classes would look like in the [C# sample app](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Models/TaskModel.cs).</span></span>

<span data-ttu-id="baee3-170">Ниже приведен пример кода на языке C# для `task/fetch` обработки `task/submit` и сообщений, использующих`TaskInfo`эти `TaskEnvelope`классы оболочки (,), взятые из [примера](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs):</span><span class="sxs-lookup"><span data-stu-id="baee3-170">Below is example code in C# for handling `task/fetch` and `task/submit` messages using these wrapper classes (`TaskInfo`, `TaskEnvelope`), excerpted from the [sample](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs):</span></span>

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

<span data-ttu-id="baee3-171">В приведенном выше примере не показана `SetTaskInfo()` функция, которая задает свойства `height`, `width`и `title` свойства `TaskInfo` объекта для каждого случая.</span><span class="sxs-lookup"><span data-stu-id="baee3-171">Not shown in the above example is the `SetTaskInfo()` function, which sets the `height`, `width`, and `title` properties of the `TaskInfo` object for each case.</span></span> <span data-ttu-id="baee3-172">Ниже приведен [Исходный код для сеттаскинфо ()](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs).</span><span class="sxs-lookup"><span data-stu-id="baee3-172">Here's the [source code for SetTaskInfo()](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs).</span></span>

### <a name="bot-framework-card-actions-vs-adaptive-card-actionsubmit-actions"></a><span data-ttu-id="baee3-173">Действия с карточками Bot и адаптивной карты. действия по отсылке</span><span class="sxs-lookup"><span data-stu-id="baee3-173">Bot Framework card actions vs. Adaptive card Action.Submit actions</span></span>

<span data-ttu-id="baee3-174">Схема действий для действий с карточной картой несколько отличается от действий адаптивной карточки `Action.Submit` .</span><span class="sxs-lookup"><span data-stu-id="baee3-174">The schema for Bot Framework card actions is slightly different from Adaptive card `Action.Submit` actions.</span></span> <span data-ttu-id="baee3-175">В результате, способ вызова модулей задач немного отличается: `data` объект `Action.Submit` содержит `msteams` объект, поэтому он не будет влиять на другие свойства карточки.</span><span class="sxs-lookup"><span data-stu-id="baee3-175">As a result, the way to invoke task modules is slightly different too: the `data` object in `Action.Submit` contains an `msteams` object so it won't interfere with other properties in the card.</span></span> <span data-ttu-id="baee3-176">В следующей таблице приведен пример каждого из них:</span><span class="sxs-lookup"><span data-stu-id="baee3-176">The following table shows an example of each:</span></span>

| <span data-ttu-id="baee3-177">Действие с картой инфраструктуры Bot</span><span class="sxs-lookup"><span data-stu-id="baee3-177">Bot Framework card action</span></span>                              | <span data-ttu-id="baee3-178">Действие адаптивной карточки. действие отсылки</span><span class="sxs-lookup"><span data-stu-id="baee3-178">Adaptive card Action.Submit action</span></span>                     |
| ------------------------------------------------------ | ------------------------------------------------------ |
| <pre>{<br/>  "type": "invoke",<br/>  "title": "Buy",<br/>  "value": {<br/>    "type": "task/fetch",<br/>    &lt;...&gt;<br/>  }<br/>}</pre> | <pre>{<br/>  "type": "Action.Submit",<br/>  "id": "btnBuy",<br/>  "title": "Buy",<br/>  "data": {<br/>    &lt;...&gt;,<br/>    "msteams": {<br/>      "type": "task/fetch"<br/>    }<br/>  }<br/>}</pre>  |
