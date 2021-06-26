---
title: Использование модулей задач в Microsoft Teams ботах
description: Использование модулей задач с Microsoft Teams ботами, включая карты Bot Framework, адаптивные карты и глубокие ссылки.
localization_priority: Normal
ms.topic: how-to
keywords: модули задач групп ботов
ms.openlocfilehash: 5d9aa2b651a4c99cee75aada62a4d1176a589d79
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140312"
---
# <a name="use-task-modules-from-bots"></a><span data-ttu-id="8bc22-104">Использование модулей задач от ботов</span><span class="sxs-lookup"><span data-stu-id="8bc22-104">Use task modules from bots</span></span>

<span data-ttu-id="8bc22-105">Модули задач могут вызываться из Microsoft Teams с помощью кнопок на картах Adaptive Cards и Bot Framework, которые является героем, эскизом и Office 365 соединителю.</span><span class="sxs-lookup"><span data-stu-id="8bc22-105">Task modules can be invoked from Microsoft Teams bots using buttons on Adaptive Cards and Bot Framework cards that is hero, thumbnail, and Office 365 Connector.</span></span> <span data-ttu-id="8bc22-106">Модули задач часто являются более удобными для пользователей, чем несколько этапов беседы.</span><span class="sxs-lookup"><span data-stu-id="8bc22-106">Task modules are often a better user experience than multiple conversation steps.</span></span> <span data-ttu-id="8bc22-107">Отслеживайте состояние бота и разрешите пользователю прерывать или отменять последовательность.</span><span class="sxs-lookup"><span data-stu-id="8bc22-107">Keep track of bot state and allow the user to interrupt or cancel the sequence.</span></span>

<span data-ttu-id="8bc22-108">Существует два способа ссылки на модули задач:</span><span class="sxs-lookup"><span data-stu-id="8bc22-108">There are two ways of invoking task modules:</span></span>

* <span data-ttu-id="8bc22-109">Новый вид сообщения вызова: динамически извлекается из бота действие карты для карт Bot Framework или действие карты для адаптивных карт с url-адресом или адаптивной `task/fetch` `invoke` [](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke) `Action.Submit` [](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) `task/fetch` картой.</span><span class="sxs-lookup"><span data-stu-id="8bc22-109">A new kind of invoke message `task/fetch`: Using the `invoke` [card action](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke) for Bot Framework cards, or the `Action.Submit` [card action](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) for Adaptive cards, with `task/fetch`, task module either a URL or an Adaptive Card, is fetched dynamically from your bot.</span></span>
* <span data-ttu-id="8bc22-110">URL-адреса глубоких ссылок. Используя синтаксис глубокой ссылки для модулей [задач,](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-deep-link-syntax)вы можете использовать действие карты для карт Bot Framework или действие карты для адаптивных карт `openUrl` [](~/task-modules-and-cards/cards/cards-actions.md#action-type-openurl) `Action.OpenUrl` [](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) соответственно.</span><span class="sxs-lookup"><span data-stu-id="8bc22-110">Deep link URLs: Using the [deep link syntax for task modules](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-deep-link-syntax), you can use the `openUrl` [card action](~/task-modules-and-cards/cards/cards-actions.md#action-type-openurl) for Bot Framework cards or the `Action.OpenUrl` [card action](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) for Adaptive Cards, respectively.</span></span> <span data-ttu-id="8bc22-111">С url-адресами глубоких ссылок URL-адрес модуля задач или корпус адаптивной карты уже известен, чтобы избежать обратного пути сервера по отношению к `task/fetch` .</span><span class="sxs-lookup"><span data-stu-id="8bc22-111">With deep link URLs, the task module URL or Adaptive Card body is already known to avoid a server round-trip relative to `task/fetch`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8bc22-112">Каждый `url` из них должен реализовать протокол `fallbackUrl` шифрования HTTPS.</span><span class="sxs-lookup"><span data-stu-id="8bc22-112">Each `url` and `fallbackUrl` must implement the HTTPS encryption protocol.</span></span>

<span data-ttu-id="8bc22-113">В следующем разделе приводится подробная информация об отзове модуля задач с помощью `task/fetch` .</span><span class="sxs-lookup"><span data-stu-id="8bc22-113">The next section provides details on invoking a task module using `task/fetch`.</span></span>

## <a name="invoke-a-task-module-using-taskfetch"></a><span data-ttu-id="8bc22-114">Вызов модуля задач с помощью задачи/извлечение</span><span class="sxs-lookup"><span data-stu-id="8bc22-114">Invoke a task module using task/fetch</span></span>

<span data-ttu-id="8bc22-115">Когда объект действия карты или инициализирован и когда пользователь выбирает кнопку, сообщение `value` `invoke` `Action.Submit` `invoke` отправляется боту.</span><span class="sxs-lookup"><span data-stu-id="8bc22-115">When the `value` object of the `invoke` card action or `Action.Submit` is initialized and when a user selects the button, an `invoke` message is sent to the bot.</span></span> <span data-ttu-id="8bc22-116">В ответе HTTP на сообщение в объекте оболочки встроен объект `invoke` [TaskInfo,](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) который Teams для отображения модуля задач.</span><span class="sxs-lookup"><span data-stu-id="8bc22-116">In the HTTP response to the `invoke` message, there is a [TaskInfo object](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) embedded in a wrapper object, which Teams uses to display the task module.</span></span>

![запрос или ответ на задачу/извлечение](~/assets/images/task-module/task-module-invoke-request-response.png)

<span data-ttu-id="8bc22-118">Следующие действия предоставляют модуль задач вызова с помощью задачи/извлечение:</span><span class="sxs-lookup"><span data-stu-id="8bc22-118">The following steps provides the invoke task module using task/fetch:</span></span>

1. <span data-ttu-id="8bc22-119">На этом изображении показана карта героя Bot Framework с действием **Buy** `invoke` [card.](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke)</span><span class="sxs-lookup"><span data-stu-id="8bc22-119">This image shows a Bot Framework hero card with a **Buy** `invoke` [card action](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke).</span></span> <span data-ttu-id="8bc22-120">Значение свойства `type` и `task/fetch` остальной объект `value` может быть по вашему выбору.</span><span class="sxs-lookup"><span data-stu-id="8bc22-120">The value of the `type` property is `task/fetch` and the rest of the `value` object can be of your choice.</span></span>
1. <span data-ttu-id="8bc22-121">Бот получает сообщение `invoke` HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="8bc22-121">The bot receives the `invoke` HTTP POST message.</span></span>
1. <span data-ttu-id="8bc22-122">Бот создает объект отклика и возвращает его в тело ответа POST с кодом ответа HTTP 200.</span><span class="sxs-lookup"><span data-stu-id="8bc22-122">The bot creates a response object and returns it in the body of the POST response with an HTTP 200 response code.</span></span> <span data-ttu-id="8bc22-123">Дополнительные сведения о схеме ответов см. в обсуждении [задачи/отправки.](#the-flexibility-of-tasksubmit)</span><span class="sxs-lookup"><span data-stu-id="8bc22-123">For more information on schema for responses, see [the discussion on task/submit](#the-flexibility-of-tasksubmit).</span></span> <span data-ttu-id="8bc22-124">В следующем коде приводится пример корпуса ответа HTTP, содержашего объект [TaskInfo,](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) встроенный в объект оболочки:</span><span class="sxs-lookup"><span data-stu-id="8bc22-124">The following code provides an example of body of the HTTP response that contains a [TaskInfo object](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) embedded in a wrapper object:</span></span>

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

    <span data-ttu-id="8bc22-125">Событие и его ответ для ботов аналогичны функции `task/fetch` `microsoftTeams.tasks.startTask()` в клиентской SDK.</span><span class="sxs-lookup"><span data-stu-id="8bc22-125">The `task/fetch` event and its response for bots is similar to the `microsoftTeams.tasks.startTask()` function in the client SDK.</span></span>

1. <span data-ttu-id="8bc22-126">Microsoft Teams отображает модуль задач.</span><span class="sxs-lookup"><span data-stu-id="8bc22-126">Microsoft Teams displays the task module.</span></span>

<span data-ttu-id="8bc22-127">В следующем разделе представлены сведения о отправке результатов модуля задач.</span><span class="sxs-lookup"><span data-stu-id="8bc22-127">The next section provides details on submitting the result of a task module.</span></span>

## <a name="submit-the-result-of-a-task-module"></a><span data-ttu-id="8bc22-128">Отправка результатов модуля задач</span><span class="sxs-lookup"><span data-stu-id="8bc22-128">Submit the result of a task module</span></span>

<span data-ttu-id="8bc22-129">Когда пользователь завершает работу с модулем задач, отправка результата обратно боту аналогична тому, как он работает со вкладками.</span><span class="sxs-lookup"><span data-stu-id="8bc22-129">When the user is finished with the task module, submitting the result back to the bot is similar to the way it works with tabs.</span></span> <span data-ttu-id="8bc22-130">Дополнительные сведения [см. в примере отправки результатов модуля задач.](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-of-submitting-the-result-of-a-task-module)</span><span class="sxs-lookup"><span data-stu-id="8bc22-130">For more information, see [example of submitting the result of a task module](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-of-submitting-the-result-of-a-task-module).</span></span> <span data-ttu-id="8bc22-131">Существует несколько различий:</span><span class="sxs-lookup"><span data-stu-id="8bc22-131">There are a few differences as follows:</span></span>

* <span data-ttu-id="8bc22-132">HTML или JavaScript. После проверки того, что ввел пользователь, вы вызываем функцию SDK, названную далее как для целей `TaskInfo.url` `microsoftTeams.tasks.submitTask()` `submitTask()` читаемости.</span><span class="sxs-lookup"><span data-stu-id="8bc22-132">HTML or JavaScript that is `TaskInfo.url`: Once you have validated what the user has entered, you call the `microsoftTeams.tasks.submitTask()` SDK function referred to hereafter as `submitTask()` for readability purposes.</span></span> <span data-ttu-id="8bc22-133">Вы можете позвонить без параметров, если Teams закрыть модуль задач, но необходимо передать объект или строку `submitTask()` в `submitHandler` ваш .</span><span class="sxs-lookup"><span data-stu-id="8bc22-133">You can call `submitTask()` without any parameters if you want Teams to close the task module, but you must pass an object or a string to your `submitHandler`.</span></span> <span data-ttu-id="8bc22-134">Передай его в качестве первого `result` параметра.</span><span class="sxs-lookup"><span data-stu-id="8bc22-134">Pass it as the first parameter, `result`.</span></span> <span data-ttu-id="8bc22-135">Teams вызывает , является и является объектом или строкой, которую `submitHandler` `err` вы `null` `result` передали `submitTask()` .</span><span class="sxs-lookup"><span data-stu-id="8bc22-135">Teams invokes `submitHandler`, `err` is `null`, and `result` is the object or string you passed to `submitTask()`.</span></span> <span data-ttu-id="8bc22-136">Если вы `submitTask()` звоните с `result` параметром, необходимо передать или массив `appId` `appId` строк.</span><span class="sxs-lookup"><span data-stu-id="8bc22-136">If you call `submitTask()` with a `result` parameter, you must pass an `appId` or an array of `appId` strings.</span></span> <span data-ttu-id="8bc22-137">Это позволяет Teams, что приложение, отправляя результат, является тем же, что вызывалось в модуль задач.</span><span class="sxs-lookup"><span data-stu-id="8bc22-137">This allows Teams to validate that the app sending the result is the same one which invoked the task module.</span></span> <span data-ttu-id="8bc22-138">Ваш бот получает `task/submit` сообщение, в том числе `result` .</span><span class="sxs-lookup"><span data-stu-id="8bc22-138">Your bot receives a `task/submit` message including `result`.</span></span> <span data-ttu-id="8bc22-139">Дополнительные сведения см. [в тексте полезной нагрузки `task/fetch` и `task/submit` сообщений.](#payload-of-taskfetch-and-tasksubmit-messages)</span><span class="sxs-lookup"><span data-stu-id="8bc22-139">For more information, see [payload of `task/fetch` and `task/submit` messages](#payload-of-taskfetch-and-tasksubmit-messages).</span></span>
* <span data-ttu-id="8bc22-140">Адаптивная карточка, которая является . Тело адаптивной карты, заполненное пользователем, отправляется боту через сообщение, когда пользователь выбирает `TaskInfo.card` `task/submit` любую `Action.Submit` кнопку.</span><span class="sxs-lookup"><span data-stu-id="8bc22-140">Adaptive Card that is `TaskInfo.card`: The Adaptive Card body as filled in by the user is sent to the bot through a `task/submit` message when the user selects any `Action.Submit` button.</span></span>

<span data-ttu-id="8bc22-141">В следующем разделе приводится подробная информация о гибкости `task/submit` .</span><span class="sxs-lookup"><span data-stu-id="8bc22-141">The next section provides details on the flexibility of `task/submit`.</span></span>

## <a name="the-flexibility-of-tasksubmit"></a><span data-ttu-id="8bc22-142">Гибкость задачи/отправки</span><span class="sxs-lookup"><span data-stu-id="8bc22-142">The flexibility of task/submit</span></span>

<span data-ttu-id="8bc22-143">Когда пользователь завершает работу с модулем задач, вызываемой с бота, бот всегда получает `task/submit invoke` сообщение.</span><span class="sxs-lookup"><span data-stu-id="8bc22-143">When the user finishes with a task module invoked from a bot, the bot always receives a `task/submit invoke` message.</span></span> <span data-ttu-id="8bc22-144">При ответе на сообщение у вас есть несколько `task/submit` вариантов:</span><span class="sxs-lookup"><span data-stu-id="8bc22-144">You have several options when responding to the `task/submit` message as follows:</span></span>

| <span data-ttu-id="8bc22-145">Http body response</span><span class="sxs-lookup"><span data-stu-id="8bc22-145">HTTP body response</span></span>                      | <span data-ttu-id="8bc22-146">Сценарий</span><span class="sxs-lookup"><span data-stu-id="8bc22-146">Scenario</span></span>                                |
| --------------------------------------- | --------------------------------------- |
| <span data-ttu-id="8bc22-147">Никто не игнорирует `task/submit` сообщение</span><span class="sxs-lookup"><span data-stu-id="8bc22-147">None ignore the `task/submit` message</span></span> | <span data-ttu-id="8bc22-148">Самый простой ответ — это отсутствие ответа.</span><span class="sxs-lookup"><span data-stu-id="8bc22-148">The simplest response is no response at all.</span></span> <span data-ttu-id="8bc22-149">Ваш бот не обязан отвечать, когда пользователь завершает работу с модулем задач.</span><span class="sxs-lookup"><span data-stu-id="8bc22-149">Your bot is not required to respond when the user is finished with the task module.</span></span> |
| <pre>{<br/>  "task": {<br/>    "type": "message",<br/>    "value": "Message text"<br/>  }<br/>}</pre> | <span data-ttu-id="8bc22-150">Teams отображает значение в `value` всплывающее окно сообщений.</span><span class="sxs-lookup"><span data-stu-id="8bc22-150">Teams displays the value of `value` in a pop-up message box.</span></span> |
| <pre>{<br/>  "task": {<br/>    "type": "continue",<br/>    "value": &lt;TaskInfo object&gt;<br/>  }<br/>}</pre> | <span data-ttu-id="8bc22-151">Позволяет сцеплять последовательности адаптивных карт в мастере или многошаговом опытом.</span><span class="sxs-lookup"><span data-stu-id="8bc22-151">Allows you to chain sequences of Adaptive Cards together in a wizard or multi-step experience.</span></span> |

> [!NOTE]
> <span data-ttu-id="8bc22-152">Цепочка адаптивных карт в последовательность — это расширенный сценарий.</span><span class="sxs-lookup"><span data-stu-id="8bc22-152">Chaining Adaptive Cards into a sequence is an advanced scenario.</span></span> <span data-ttu-id="8bc22-153">Пример Node.js поддерживает его.</span><span class="sxs-lookup"><span data-stu-id="8bc22-153">The Node.js sample app supports it.</span></span> <span data-ttu-id="8bc22-154">Дополнительные сведения см. [в Microsoft Teams модуля задач Node.js. ](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)</span><span class="sxs-lookup"><span data-stu-id="8bc22-154">For more information, see [Microsoft Teams task module Node.js](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes).</span></span>

<span data-ttu-id="8bc22-155">В следующем разделе приводится подробная информация о полезной нагрузке `task/fetch` `task/submit` и сообщениях.</span><span class="sxs-lookup"><span data-stu-id="8bc22-155">The next section provides details on payload of `task/fetch` and `task/submit` messages.</span></span>

## <a name="payload-of-taskfetch-and-tasksubmit-messages"></a><span data-ttu-id="8bc22-156">Полезное количество задач/извлечений и задач/отправки сообщений</span><span class="sxs-lookup"><span data-stu-id="8bc22-156">Payload of task/fetch and task/submit messages</span></span>

<span data-ttu-id="8bc22-157">В этом разделе определяется схема получения ботом объекта `task/fetch` `task/submit` или объекта Bot `Activity` Framework.</span><span class="sxs-lookup"><span data-stu-id="8bc22-157">This section defines the schema of what your bot receives when it receives a `task/fetch` or `task/submit` Bot Framework `Activity` object.</span></span> <span data-ttu-id="8bc22-158">Следующая таблица содержит свойства полезной нагрузки `task/fetch` и `task/submit` сообщений:</span><span class="sxs-lookup"><span data-stu-id="8bc22-158">The following table provides the properties of payload of `task/fetch` and `task/submit` messages:</span></span>

| <span data-ttu-id="8bc22-159">Свойство</span><span class="sxs-lookup"><span data-stu-id="8bc22-159">Property</span></span> | <span data-ttu-id="8bc22-160">Описание</span><span class="sxs-lookup"><span data-stu-id="8bc22-160">Description</span></span>                          |
| -------- | ------------------------------------ |
| `type`   | <span data-ttu-id="8bc22-161">Всегда `invoke` .</span><span class="sxs-lookup"><span data-stu-id="8bc22-161">Is always `invoke`.</span></span>           |
| `name`   | <span data-ttu-id="8bc22-162">Является либо `task/fetch` `task/submit` или .</span><span class="sxs-lookup"><span data-stu-id="8bc22-162">Is either `task/fetch` or `task/submit`.</span></span> |
| `value`  | <span data-ttu-id="8bc22-163">Является ли полезной нагрузка, определяемая разработчиком.</span><span class="sxs-lookup"><span data-stu-id="8bc22-163">Is the developer-defined payload.</span></span> <span data-ttu-id="8bc22-164">Структура объекта такая же, как и то, что отправляется из `value` Teams.</span><span class="sxs-lookup"><span data-stu-id="8bc22-164">The structure of the `value` object is the same as what is sent from Teams.</span></span> <span data-ttu-id="8bc22-165">Однако в этом случае все по-другому.</span><span class="sxs-lookup"><span data-stu-id="8bc22-165">In this case, however, it is different.</span></span> <span data-ttu-id="8bc22-166">Она требует поддержки динамических извлечений, как из Bot Framework, то есть, так и из действий `task/fetch` `value` адаптивной `Action.Submit` карты, то есть `data` .</span><span class="sxs-lookup"><span data-stu-id="8bc22-166">It requires support for dynamic fetch that is `task/fetch` from both Bot Framework, which is `value` and Adaptive Card `Action.Submit` actions, which is `data`.</span></span> <span data-ttu-id="8bc22-167">Кроме того, что включено или включено в Teams, требуется способ связи Teams с `context` `value` `data` ботом.</span><span class="sxs-lookup"><span data-stu-id="8bc22-167">A way to communicate Teams `context` to the bot is required in addition to what is included in `value` or `data`.</span></span><br/><br/><span data-ttu-id="8bc22-168">Объединяйте значение и "данные" в родительский объект:</span><span class="sxs-lookup"><span data-stu-id="8bc22-168">Combine 'value' and 'data' into a parent object:</span></span><br/><br/><pre>{<br/>  "context": {<br/>    "theme": "default" &vert; "dark" &vert; "contrast",<br/>  },<br/>  "data": [value field from Bot Framework card] &vert; [data field from Adaptive Card] <br/>}</pre>  |

<span data-ttu-id="8bc22-169">В следующем разделе приводится пример получения и ответа на сообщения в `task/fetch` `task/submit` Node.js.</span><span class="sxs-lookup"><span data-stu-id="8bc22-169">The next section provides an example of receiving and responding to `task/fetch` and `task/submit` invoke messages in Node.js.</span></span>

## <a name="example-of-taskfetch-and-tasksubmit-invoke-messages-in-nodejs-and-c"></a><span data-ttu-id="8bc22-170">Пример задач/извлечений и задач/отправки ссылок на сообщения в Node.js и C #</span><span class="sxs-lookup"><span data-stu-id="8bc22-170">Example of task/fetch and task/submit invoke messages in Node.js and C#</span></span>

# <a name="nodejs"></a>[<span data-ttu-id="8bc22-171">Node.js</span><span class="sxs-lookup"><span data-stu-id="8bc22-171">Node.js</span></span>](#tab/nodejs)

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

# <a name="c"></a>[<span data-ttu-id="8bc22-172">C#</span><span class="sxs-lookup"><span data-stu-id="8bc22-172">C#</span></span>](#tab/csharp)

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

### <a name="bot-framework-card-actions-vs-adaptive-card-actionsubmit-actions"></a><span data-ttu-id="8bc22-173">Действия карты Bot Framework против действий адаптивной карты.Отправка действий</span><span class="sxs-lookup"><span data-stu-id="8bc22-173">Bot Framework card actions vs. Adaptive Card Action.Submit actions</span></span>

<span data-ttu-id="8bc22-174">Схема действий карты Bot Framework отличается от действий адаптивной карты, а способ вызова модулей задач также `Action.Submit` отличается.</span><span class="sxs-lookup"><span data-stu-id="8bc22-174">The schema for Bot Framework card actions is different from Adaptive Card `Action.Submit` actions and the way to invoke task modules is also different.</span></span> <span data-ttu-id="8bc22-175">Объект содержит объект, чтобы он не мешал другим `data` `Action.Submit` `msteams` свойствам карты.</span><span class="sxs-lookup"><span data-stu-id="8bc22-175">The `data` object in `Action.Submit` contains an `msteams` object so it does not interfere with other properties in the card.</span></span> <span data-ttu-id="8bc22-176">В следующей таблице показан пример каждого действия карты:</span><span class="sxs-lookup"><span data-stu-id="8bc22-176">The following table shows an example of each card action:</span></span>

| <span data-ttu-id="8bc22-177">Действие карты Bot Framework</span><span class="sxs-lookup"><span data-stu-id="8bc22-177">Bot Framework card action</span></span>                              | <span data-ttu-id="8bc22-178">Действие адаптивной карты.Отправка действия</span><span class="sxs-lookup"><span data-stu-id="8bc22-178">Adaptive Card Action.Submit action</span></span>                     |
| ------------------------------------------------------ | ------------------------------------------------------ |
| <pre>{<br/>  "type": "invoke",<br/>  "title": "Buy",<br/>  "value": {<br/>    "type": "task/fetch",<br/>    &lt;...&gt;<br/>  }<br/>}</pre> | <pre>{<br/>  "type": "Action.Submit",<br/>  "id": "btnBuy",<br/>  "title": "Buy",<br/>  "data": {<br/>    &lt;...&gt;,<br/>    "msteams": {<br/>      "type": "task/fetch"<br/>    }<br/>  }<br/>}</pre>  |

## <a name="code-sample"></a><span data-ttu-id="8bc22-179">Пример кода</span><span class="sxs-lookup"><span data-stu-id="8bc22-179">Code sample</span></span>

|<span data-ttu-id="8bc22-180">Пример имени</span><span class="sxs-lookup"><span data-stu-id="8bc22-180">Sample name</span></span> | <span data-ttu-id="8bc22-181">Description</span><span class="sxs-lookup"><span data-stu-id="8bc22-181">Description</span></span> | <span data-ttu-id="8bc22-182">.NET</span><span class="sxs-lookup"><span data-stu-id="8bc22-182">.NET</span></span> | <span data-ttu-id="8bc22-183">Node.js</span><span class="sxs-lookup"><span data-stu-id="8bc22-183">Node.js</span></span>|
|----------------|-----------------|--------------|----------------|
|<span data-ttu-id="8bc22-184">Пример модуля задач bots-V4</span><span class="sxs-lookup"><span data-stu-id="8bc22-184">Task module sample bots-V4</span></span> | <span data-ttu-id="8bc22-185">Примеры для создания модулей задач.</span><span class="sxs-lookup"><span data-stu-id="8bc22-185">Samples for creating task modules.</span></span> |[<span data-ttu-id="8bc22-186">View</span><span class="sxs-lookup"><span data-stu-id="8bc22-186">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/54.teams-task-module)|[<span data-ttu-id="8bc22-187">View</span><span class="sxs-lookup"><span data-stu-id="8bc22-187">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/54.teams-task-module)|

## <a name="see-also"></a><span data-ttu-id="8bc22-188">См. также</span><span class="sxs-lookup"><span data-stu-id="8bc22-188">See also</span></span>

* [<span data-ttu-id="8bc22-189">Microsoft Teams пример кода модуля задач в Node.js</span><span class="sxs-lookup"><span data-stu-id="8bc22-189">Microsoft Teams task module sample code in Node.js</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs/blob/master/src/TeamsBot.ts)
* [<span data-ttu-id="8bc22-190">Примеры Bot Framework</span><span class="sxs-lookup"><span data-stu-id="8bc22-190">Bot Framework samples</span></span>](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)
