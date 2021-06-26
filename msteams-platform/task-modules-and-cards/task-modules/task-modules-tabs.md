---
title: Использование модулей задач в Microsoft Teams вкладками
description: Объясняет, как вызывать модули задач из Teams вкладок с помощью Microsoft Teams SDK клиента.
localization_priority: Normal
ms.topic: how-to
keywords: модули задач группы вкладок sdk клиента
ms.openlocfilehash: 8afd2c93261f28aa7ced4c98d29be27dca35f8b1
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140557"
---
# <a name="use-task-modules-in-tabs"></a><span data-ttu-id="42df9-104">Использование модулей задач на вкладке</span><span class="sxs-lookup"><span data-stu-id="42df9-104">Use task modules in tabs</span></span>

<span data-ttu-id="42df9-105">Добавьте модуль задач на вкладку, чтобы упростить работу пользователя для любых процессов, которые требуют ввода данных.</span><span class="sxs-lookup"><span data-stu-id="42df9-105">Add a task module to your tab to simplify your user's experience for any workflows that require data input.</span></span> <span data-ttu-id="42df9-106">Модули задач позволяют собирать входные данные в всплывающее Teams-Aware Microsoft.</span><span class="sxs-lookup"><span data-stu-id="42df9-106">Task modules allow you to gather their input in a Microsoft Teams-Aware pop-up.</span></span> <span data-ttu-id="42df9-107">Хорошим примером этого является редактирование карт Планировщика.</span><span class="sxs-lookup"><span data-stu-id="42df9-107">A good example of this is editing Planner cards.</span></span> <span data-ttu-id="42df9-108">Для создания аналогичного опыта можно использовать модули задач.</span><span class="sxs-lookup"><span data-stu-id="42df9-108">You can use task modules to create a similar experience.</span></span>

<span data-ttu-id="42df9-109">Чтобы поддерживать функцию модуля задач, в клиентскую [SDK Teams две новые функции.](/javascript/api/overview/msteams-client)</span><span class="sxs-lookup"><span data-stu-id="42df9-109">To support the task module feature, two new functions are added to the [Teams client SDK](/javascript/api/overview/msteams-client).</span></span> <span data-ttu-id="42df9-110">В следующем коде показан пример этих двух функций:</span><span class="sxs-lookup"><span data-stu-id="42df9-110">The following code shows an example of these two functions:</span></span>

```typescript
microsoftTeams.tasks.startTask(
    taskInfo: TaskInfo,
    submitHandler?: (err: string, result: string | any) => void
): void;

microsoftTeams.tasks.submitTask(
    result?: string | any,
    appIds?: string | string[]
): void;
```

<span data-ttu-id="42df9-111">Вы можете увидеть, как работает отправка модуля задач со вкладки и отправка результатов работы модуля задач.</span><span class="sxs-lookup"><span data-stu-id="42df9-111">You can see how invoking a task module from a tab and submitting the result of a task module works.</span></span>

## <a name="invoke-a-task-module-from-a-tab"></a><span data-ttu-id="42df9-112">Вызов модуля задач со вкладки</span><span class="sxs-lookup"><span data-stu-id="42df9-112">Invoke a task module from a tab</span></span>

<span data-ttu-id="42df9-113">Чтобы вызвать модуль задач со вкладки, используйте передачу объекта `microsoftTeams.tasks.startTask()` [TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) и необязательный вызов `submitHandler` функции.</span><span class="sxs-lookup"><span data-stu-id="42df9-113">To invoke a task module from a tab use `microsoftTeams.tasks.startTask()` passing a [TaskInfo object](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) and an optional `submitHandler` callback function.</span></span> <span data-ttu-id="42df9-114">Необходимо рассмотреть два случая:</span><span class="sxs-lookup"><span data-stu-id="42df9-114">There are two cases to consider:</span></span>

* <span data-ttu-id="42df9-115">Значение `TaskInfo.url` установлено для URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="42df9-115">The value of `TaskInfo.url` is set to a URL.</span></span> <span data-ttu-id="42df9-116">Окно модуля задач отображается и `TaskModule.url` загружается как `<iframe>` внутреннее.</span><span class="sxs-lookup"><span data-stu-id="42df9-116">The task module window appears and `TaskModule.url` is loaded as an `<iframe>` inside it.</span></span> <span data-ttu-id="42df9-117">JavaScript на этой странице вызывает `microsoftTeams.initialize()` .</span><span class="sxs-lookup"><span data-stu-id="42df9-117">JavaScript on that page calls `microsoftTeams.initialize()`.</span></span> <span data-ttu-id="42df9-118">Если на странице есть функция и ошибка при вызове, то вызывается с задаваемой строкой ошибки, `submitHandler` `microsoftTeams.tasks.startTask()` `submitHandler` `err` указывающей то же самое.</span><span class="sxs-lookup"><span data-stu-id="42df9-118">If there is a `submitHandler` function on the page and there is an error when invoking `microsoftTeams.tasks.startTask()`, then `submitHandler` is invoked with `err` set to the error string indicating the same.</span></span> <span data-ttu-id="42df9-119">Дополнительные сведения см. в ссылке на ошибки [вызовов модулей задач.](#task-module-invocation-errors)</span><span class="sxs-lookup"><span data-stu-id="42df9-119">For more information, see [task module invocation errors](#task-module-invocation-errors).</span></span>
* <span data-ttu-id="42df9-120">Значение JSON для адаптивной `taskInfo.card` [карты](~/task-modules-and-cards/task-modules/invoking-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment).</span><span class="sxs-lookup"><span data-stu-id="42df9-120">The value of `taskInfo.card` is the [JSON for an Adaptive Card](~/task-modules-and-cards/task-modules/invoking-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment).</span></span> <span data-ttu-id="42df9-121">Функция JavaScript не может вызываться при закрытии или нажатии кнопки `submitHandler` на адаптивной карте.</span><span class="sxs-lookup"><span data-stu-id="42df9-121">There is no JavaScript `submitHandler` function to call when the user closes or presses a button on the Adaptive Card.</span></span> <span data-ttu-id="42df9-122">Единственный способ получить то, что вошел пользователь, — это передача результата боту.</span><span class="sxs-lookup"><span data-stu-id="42df9-122">The only way to receive what the user entered is by passing the result to a bot.</span></span> <span data-ttu-id="42df9-123">Чтобы использовать модуль задач адаптивной карты со вкладки, приложение должно включить бот, чтобы получить любой ответ от пользователя.</span><span class="sxs-lookup"><span data-stu-id="42df9-123">To use an Adaptive Card task module from a tab, your app must include a bot to get any response from the user.</span></span>

<span data-ttu-id="42df9-124">В следующем разделе приводится пример ссылки на модуль задач.</span><span class="sxs-lookup"><span data-stu-id="42df9-124">The next section gives an example of invoking a task module.</span></span>

## <a name="example-of-invoking-a-task-module"></a><span data-ttu-id="42df9-125">Пример ссылки на модуль задач</span><span class="sxs-lookup"><span data-stu-id="42df9-125">Example of invoking a task module</span></span>

<span data-ttu-id="42df9-126">На следующем изображении отображается модуль задач:</span><span class="sxs-lookup"><span data-stu-id="42df9-126">The following image displays the task module:</span></span>

![Модуль задач — настраиваемая форма](~/assets/images/task-module/task-module-custom-form.png)

<span data-ttu-id="42df9-128">Следующий код адаптируется из [примера модуля задач:](~/task-modules-and-cards/task-modules/invoking-task-modules.md#code-sample)</span><span class="sxs-lookup"><span data-stu-id="42df9-128">The following code is adapted from [the task module sample](~/task-modules-and-cards/task-modules/invoking-task-modules.md#code-sample):</span></span>

```javascript
let taskInfo = {
    title: null,
    height: null,
    width: null,
    url: null,
    card: null,
    fallbackUrl: null,
    completionBotId: null,
};

taskInfo.url = "https://contoso.com/teamsapp/customform";
taskInfo.title = "Custom Form";
taskInfo.height = 510;
taskInfo.width = 430;
submitHandler = (err, result) => {
    console.log(`Submit handler - err: ${err}`);
    console.log(`Submit handler - result\rName: ${result.name}\rEmail: ${result.email}\rFavorite book: ${result.favoriteBook}`);
};
microsoftTeams.tasks.startTask(taskInfo, submitHandler);
```

<span data-ttu-id="42df9-129">Это `submitHandler` очень просто, и оно повторяет значение `err` консоли или `result` консоли.</span><span class="sxs-lookup"><span data-stu-id="42df9-129">The `submitHandler` is very simple and it echoes the value of `err` or `result` to the console.</span></span>

## <a name="submit-the-result-of-a-task-module"></a><span data-ttu-id="42df9-130">Отправка результатов модуля задач</span><span class="sxs-lookup"><span data-stu-id="42df9-130">Submit the result of a task module</span></span>

<span data-ttu-id="42df9-131">Функция `submitHandler` находится на `TaskInfo.url` веб-странице и используется с `TaskInfo.url` .</span><span class="sxs-lookup"><span data-stu-id="42df9-131">The `submitHandler` function resides in the `TaskInfo.url` web page and is used with `TaskInfo.url`.</span></span> <span data-ttu-id="42df9-132">Если при вызове модуля задач возникла ошибка, функция немедленно вызывается строкой, указывающей, какая `submitHandler` `err` ошибка [произошла.](#task-module-invocation-errors)</span><span class="sxs-lookup"><span data-stu-id="42df9-132">If there is an error when invoking the task module, your `submitHandler` function is immediately invoked with an `err` string indicating what [error occurred](#task-module-invocation-errors).</span></span> <span data-ttu-id="42df9-133">Функция также называется строкой, когда пользователь выбирает X в правом верхнем справа от модуля задач, чтобы `submitHandler` `err` закрыть ее.</span><span class="sxs-lookup"><span data-stu-id="42df9-133">The `submitHandler` function is also called with an `err` string when the user selects X at the upper right of the task module to close it.</span></span>

<span data-ttu-id="42df9-134">Если ошибки вызова нет и пользователь не выбирает X, чтобы отклонять ее, пользователь выбирает кнопку по завершению.</span><span class="sxs-lookup"><span data-stu-id="42df9-134">If there is no invocation error and the user does not select X to dismiss it, the user chooses a button when finished.</span></span> <span data-ttu-id="42df9-135">В зависимости от url-адреса или адаптивной карты в модуле задач в следующих разделах указаны сведения о том, что происходит.</span><span class="sxs-lookup"><span data-stu-id="42df9-135">Depending on whether it is a URL or an Adaptive Card in the task module, the next sections provide details on what occurs.</span></span>

### <a name="html-or-javascript-taskinfourl"></a><span data-ttu-id="42df9-136">HTML или JavaScript `TaskInfo.url`</span><span class="sxs-lookup"><span data-stu-id="42df9-136">HTML or JavaScript `TaskInfo.url`</span></span>

<span data-ttu-id="42df9-137">После проверки входных данных пользователя вызываем функцию `microsoftTeams.tasks.submitTask()` SDK, которая называется `submitTask()` .</span><span class="sxs-lookup"><span data-stu-id="42df9-137">After validating the user's inputs, call the `microsoftTeams.tasks.submitTask()` SDK function referred to as `submitTask()`.</span></span> <span data-ttu-id="42df9-138">Вызов `submitTask()` без параметров, если Teams закрыть модуль задач.</span><span class="sxs-lookup"><span data-stu-id="42df9-138">Call `submitTask()` without any parameters if you just want Teams to close the task module.</span></span> <span data-ttu-id="42df9-139">Вы можете передать объект или строку в `submitHandler` ваш .</span><span class="sxs-lookup"><span data-stu-id="42df9-139">You can pass an object or a string to your `submitHandler`.</span></span>

<span data-ttu-id="42df9-140">Передай результат в качестве первого параметра.</span><span class="sxs-lookup"><span data-stu-id="42df9-140">Pass your result as the first parameter.</span></span> <span data-ttu-id="42df9-141">Teams вызывает, где находится и является объект или `submitHandler` `err` `null` строка, которую вы `result` передали `submitTask()` .</span><span class="sxs-lookup"><span data-stu-id="42df9-141">Teams invokes `submitHandler` where `err` is `null` and `result` is the object or string you passed to `submitTask()`.</span></span> <span data-ttu-id="42df9-142">Если вы `submitTask()` звоните с `result` параметром, необходимо передать или массив `appId` `appId` строк.</span><span class="sxs-lookup"><span data-stu-id="42df9-142">If you call `submitTask()` with a `result` parameter, you must pass an `appId` or an array of `appId` strings.</span></span> <span data-ttu-id="42df9-143">Это позволяет Teams, что приложение, отправляя результат, является таким же, как и вызываемого модуля задач.</span><span class="sxs-lookup"><span data-stu-id="42df9-143">This permits Teams to validate that the app sending the result is same as the invoked task module.</span></span>

### <a name="adaptive-card-taskinfocard"></a><span data-ttu-id="42df9-144">Адаптивная карта `TaskInfo.card`</span><span class="sxs-lookup"><span data-stu-id="42df9-144">Adaptive Card `TaskInfo.card`</span></span>

<span data-ttu-id="42df9-145">Когда вы вызываете модуль задач с помощью кнопки, а пользователь выбирает кнопку, значения в карточке возвращаются в качестве `submitHandler` `Action.Submit` значения `result` .</span><span class="sxs-lookup"><span data-stu-id="42df9-145">When you invoke the task module with a `submitHandler` and the user selects an `Action.Submit` button, the values in the card are returned as the value of `result`.</span></span> <span data-ttu-id="42df9-146">Если пользователь выбирает ключ Esc или X в правом верхнем справа, `err` возвращается вместо него.</span><span class="sxs-lookup"><span data-stu-id="42df9-146">If the user selects the Esc key or X at the top right, `err` is returned instead.</span></span> <span data-ttu-id="42df9-147">Если приложение содержит бот в дополнение к вкладке, вы можете просто включить бот в качестве значения `appId` `completionBotId` в `TaskInfo` объекте.</span><span class="sxs-lookup"><span data-stu-id="42df9-147">If your app contains a bot in addition to a tab, you can simply include the `appId` of the bot as the value of `completionBotId` in the `TaskInfo` object.</span></span> <span data-ttu-id="42df9-148">Тело адаптивной карты, заполненное пользователем, отправляется боту с помощью сообщения, когда пользователь `task/submit invoke` выбирает `Action.Submit` кнопку.</span><span class="sxs-lookup"><span data-stu-id="42df9-148">The Adaptive Card body as filled in by the user is sent to the bot using a `task/submit invoke` message when the user selects an `Action.Submit` button.</span></span> <span data-ttu-id="42df9-149">Схема объекта, который вы получаете, очень похожа на схему, которую вы получаете для задач/извлечений и [задач/отправки сообщений.](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages)</span><span class="sxs-lookup"><span data-stu-id="42df9-149">The schema for the object you receive is very similar to [the schema you receive for task/fetch and task/submit messages](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages).</span></span> <span data-ttu-id="42df9-150">Единственное отличие состоит в том, что схема объекта JSON является объектом Адаптивной карты, а не объектом, содержащим объект Adaptive Card, как при использования адаптивных карт с [ботами.](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages)</span><span class="sxs-lookup"><span data-stu-id="42df9-150">The only difference is that the schema of the JSON object is an Adaptive Card object as opposed to an object containing an Adaptive Card object as [when Adaptive cards are used with bots](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages).</span></span>

<span data-ttu-id="42df9-151">В следующем разделе приводится пример отправки результатов модуля задач.</span><span class="sxs-lookup"><span data-stu-id="42df9-151">The next section gives an example of submitting the result of a task module.</span></span>

## <a name="example-of-submitting-the-result-of-a-task-module"></a><span data-ttu-id="42df9-152">Пример отправки результата модуля задач</span><span class="sxs-lookup"><span data-stu-id="42df9-152">Example of submitting the result of a task module</span></span>

<span data-ttu-id="42df9-153">Дополнительные сведения см. в [htmL-форме в модуле задач.](#example-of-invoking-a-task-module)</span><span class="sxs-lookup"><span data-stu-id="42df9-153">For more information, see the [HTML form in the task module](#example-of-invoking-a-task-module).</span></span> <span data-ttu-id="42df9-154">В следующем коде приводится пример определения формы:</span><span class="sxs-lookup"><span data-stu-id="42df9-154">The following code gives an example of where the form is defined:</span></span>

```html
<form method="POST" id="customerForm" action="/register" onSubmit="return validateForm()">
```

<span data-ttu-id="42df9-155">Существует пять полей в этой форме, но для этого примера требуется только три значения, `name` `email` и `favoriteBook` .</span><span class="sxs-lookup"><span data-stu-id="42df9-155">There are five fields on this form but for this example only three values are required, `name`, `email`, and `favoriteBook`.</span></span>

<span data-ttu-id="42df9-156">В следующем коде приводится пример `validateForm()` функции, которая `submitTask()` вызывает:</span><span class="sxs-lookup"><span data-stu-id="42df9-156">The following code gives an example of the `validateForm()` function that calls `submitTask()`:</span></span>

```javascript
function validateForm() {
    var customerInfo = {
        name: document.forms["customerForm"]["name"].value,
        email: document.forms["customerForm"]["email"].value,
        favoriteBook: document.forms["customerForm"]["favoriteBook"].value
    }
    microsoftTeams.tasks.submitTask(customerInfo, "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx");
    return true;
}
```

<span data-ttu-id="42df9-157">В следующем разделе печатались проблемы с вызовом модулей задач и сообщения об ошибках.</span><span class="sxs-lookup"><span data-stu-id="42df9-157">The next section provides task module invocation problems and their error messages.</span></span>

## <a name="task-module-invocation-errors"></a><span data-ttu-id="42df9-158">Ошибки при вызове модуля задач</span><span class="sxs-lookup"><span data-stu-id="42df9-158">Task module invocation errors</span></span>

<span data-ttu-id="42df9-159">В следующей таблице возможен доступ к следующим значениям: `err` `submitHandler`</span><span class="sxs-lookup"><span data-stu-id="42df9-159">The following table provides the possible values of `err` that can be received by your `submitHandler`:</span></span>

| <span data-ttu-id="42df9-160">Проблема</span><span class="sxs-lookup"><span data-stu-id="42df9-160">Problem</span></span> | <span data-ttu-id="42df9-161">Сообщение об ошибке, значение `err`</span><span class="sxs-lookup"><span data-stu-id="42df9-161">Error message that is value of `err`</span></span> |
| ------- | ------------------------------ |
| <span data-ttu-id="42df9-162">Значения для обоих `TaskInfo.url` и `TaskInfo.card` были указаны.</span><span class="sxs-lookup"><span data-stu-id="42df9-162">Values for both `TaskInfo.url` and `TaskInfo.card` were specified.</span></span> | <span data-ttu-id="42df9-163">Значения для карты и URL-адреса были указаны.</span><span class="sxs-lookup"><span data-stu-id="42df9-163">Values for both card and URL were specified.</span></span> <span data-ttu-id="42df9-164">Разрешено одно или другое, но не то и другое.</span><span class="sxs-lookup"><span data-stu-id="42df9-164">One or the other, but not both, are allowed.</span></span> |
| <span data-ttu-id="42df9-165">Ни `TaskInfo.url` `TaskInfo.card` указанных, ни указанных.</span><span class="sxs-lookup"><span data-stu-id="42df9-165">Neither `TaskInfo.url` nor `TaskInfo.card` specified.</span></span> | <span data-ttu-id="42df9-166">Необходимо указать значение для карты или URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="42df9-166">You must specify a value for either card or URL.</span></span> |
| <span data-ttu-id="42df9-167">Недействительный `appId` .</span><span class="sxs-lookup"><span data-stu-id="42df9-167">Invalid `appId`.</span></span> | <span data-ttu-id="42df9-168">Недействительный ID приложения.</span><span class="sxs-lookup"><span data-stu-id="42df9-168">Invalid app ID.</span></span> |
| <span data-ttu-id="42df9-169">Пользователь выбрал кнопку X, закрыв ее.</span><span class="sxs-lookup"><span data-stu-id="42df9-169">User selected X button, closing it.</span></span> | <span data-ttu-id="42df9-170">Пользователь отменил или закрыл модуль задач.</span><span class="sxs-lookup"><span data-stu-id="42df9-170">User cancelled or closed the task module.</span></span> |

## <a name="code-sample"></a><span data-ttu-id="42df9-171">Пример кода</span><span class="sxs-lookup"><span data-stu-id="42df9-171">Code sample</span></span>

|<span data-ttu-id="42df9-172">Пример имени</span><span class="sxs-lookup"><span data-stu-id="42df9-172">Sample name</span></span> | <span data-ttu-id="42df9-173">Description</span><span class="sxs-lookup"><span data-stu-id="42df9-173">Description</span></span> | <span data-ttu-id="42df9-174">.NET</span><span class="sxs-lookup"><span data-stu-id="42df9-174">.NET</span></span> | <span data-ttu-id="42df9-175">Node.js</span><span class="sxs-lookup"><span data-stu-id="42df9-175">Node.js</span></span>|
|----------------|-----------------|--------------|----------------|
|<span data-ttu-id="42df9-176">Пример вкладок модуля задач и ботов-V3</span><span class="sxs-lookup"><span data-stu-id="42df9-176">Task module sample tabs and bots-V3</span></span> | <span data-ttu-id="42df9-177">Примеры для создания модулей задач.</span><span class="sxs-lookup"><span data-stu-id="42df9-177">Samples for creating task modules.</span></span> |[<span data-ttu-id="42df9-178">View</span><span class="sxs-lookup"><span data-stu-id="42df9-178">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/csharp)|[<span data-ttu-id="42df9-179">View</span><span class="sxs-lookup"><span data-stu-id="42df9-179">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/nodejs)| 

## <a name="see-also"></a><span data-ttu-id="42df9-180">См. также</span><span class="sxs-lookup"><span data-stu-id="42df9-180">See also</span></span>

[<span data-ttu-id="42df9-181">Вызов и увольнение модулей задач</span><span class="sxs-lookup"><span data-stu-id="42df9-181">Invoke and dismiss task modules</span></span>](~/task-modules-and-cards/task-modules/invoking-task-modules.md)

## <a name="next-step"></a><span data-ttu-id="42df9-182">Следующий этап</span><span class="sxs-lookup"><span data-stu-id="42df9-182">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="42df9-183">Использование модулей задач от ботов</span><span class="sxs-lookup"><span data-stu-id="42df9-183">Using task modules from bots</span></span>](~/task-modules-and-cards/task-modules/task-modules-bots.md)
