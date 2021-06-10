---
title: Использование модулей задач в Microsoft Teams вкладками
description: Объясняет, как вызывать модули задач с Teams вкладок с помощью Microsoft Teams SDK клиента
localization_priority: Normal
ms.topic: how-to
keywords: модули задач группы вкладок sdk клиента
ms.openlocfilehash: 5e85fd0662b8a15d6b98d9c2d2dfa5137b05fa39
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019526"
---
# <a name="using-task-modules-in-tabs"></a><span data-ttu-id="881be-104">Использование модулей задач во вкладках</span><span class="sxs-lookup"><span data-stu-id="881be-104">Using task modules in tabs</span></span>

<span data-ttu-id="881be-105">Добавление модуля задач на вкладку может значительно упростить работу пользователя для любых процессов, которые требуют ввода данных.</span><span class="sxs-lookup"><span data-stu-id="881be-105">Adding a task module to your tab can greatly simplify your user's experience for any workflows that require data input.</span></span> <span data-ttu-id="881be-106">Модули задач позволяют собирать свои входные данные в всплывающее Teams,хорошо известное.</span><span class="sxs-lookup"><span data-stu-id="881be-106">Task modules allow you to gather their input in a Teams-aware popup.</span></span> <span data-ttu-id="881be-107">Хорошим примером этого является редактирование карт Планировщика; вы можете использовать модули задач для создания аналогичного опыта.</span><span class="sxs-lookup"><span data-stu-id="881be-107">A good example of this is editing Planner cards; you can use task modules to create a similar experience.</span></span>

<span data-ttu-id="881be-108">Для поддержки функции модуля задач в клиентскую [SDK Microsoft Teams две новые функции:](/javascript/api/overview/msteams-client)</span><span class="sxs-lookup"><span data-stu-id="881be-108">To support the task module feature, two new functions were added to the [Microsoft Teams client SDK](/javascript/api/overview/msteams-client):</span></span>

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

<span data-ttu-id="881be-109">Давайте посмотрим, как каждый из них работает.</span><span class="sxs-lookup"><span data-stu-id="881be-109">Let's see how each of them work.</span></span>

## <a name="invoking-a-task-module-from-a-tab"></a><span data-ttu-id="881be-110">Ссылки на модуль задач со вкладки</span><span class="sxs-lookup"><span data-stu-id="881be-110">Invoking a task module from a tab</span></span>

<span data-ttu-id="881be-111">Чтобы вызвать модуль задач со вкладки, используйте передачу объекта `microsoftTeams.tasks.startTask()` [TaskInfo](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) и необязательный вызов `submitHandler` функции.</span><span class="sxs-lookup"><span data-stu-id="881be-111">To invoke a task module from a tab use `microsoftTeams.tasks.startTask()` passing a [TaskInfo object](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) and an optional `submitHandler` callback function.</span></span> <span data-ttu-id="881be-112">Как было описано выше, необходимо рассмотреть два случая:</span><span class="sxs-lookup"><span data-stu-id="881be-112">As described earlier, there are two cases to consider:</span></span>

1. <span data-ttu-id="881be-113">Значение `TaskInfo.url` установлено для URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="881be-113">The value of `TaskInfo.url` is set to a URL.</span></span> <span data-ttu-id="881be-114">Окно модуля задач отображается и `TaskModule.url` загружается как `<iframe>` внутреннее.</span><span class="sxs-lookup"><span data-stu-id="881be-114">The task module window appears and `TaskModule.url` is loaded as an `<iframe>` inside it.</span></span> <span data-ttu-id="881be-115">JavaScript на этой странице должен вызвать `microsoftTeams.initialize()` .</span><span class="sxs-lookup"><span data-stu-id="881be-115">JavaScript on that page should call `microsoftTeams.initialize()`.</span></span> <span data-ttu-id="881be-116">Если на странице есть функция и при вызове есть ошибка, то вызывается с набором к строке ошибки, указывающей ошибку, как описано `submitHandler` `microsoftTeams.tasks.startTask()` `submitHandler` `err` [ниже.](#task-module-invocation-errors)</span><span class="sxs-lookup"><span data-stu-id="881be-116">If there is a `submitHandler` function on the page and there is an error when invoking `microsoftTeams.tasks.startTask()`, then `submitHandler` is invoked with `err` set to the error string indicating the error as described [below](#task-module-invocation-errors).</span></span>
1. <span data-ttu-id="881be-117">Значение `taskInfo.card` JSON для [адаптивной карты](~/task-modules-and-cards/what-are-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment).</span><span class="sxs-lookup"><span data-stu-id="881be-117">The value of `taskInfo.card` is the [JSON for an Adaptive card](~/task-modules-and-cards/what-are-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment).</span></span> <span data-ttu-id="881be-118">В этом случае не нужно вызывать функцию JavaScript, когда пользователь закрывает или нажимает кнопку на адаптивной карте; единственный способ получить то, что вошел пользователь, это передача результата `submitHandler` боту.</span><span class="sxs-lookup"><span data-stu-id="881be-118">In this case there's obviously not any JavaScript `submitHandler` function to call when the user closes or presses a button on the Adaptive card; the only way to receive what the user entered is by passing the result to a bot.</span></span> <span data-ttu-id="881be-119">Чтобы использовать модуль задач адаптивной карты со вкладки, приложение должно включить бот, чтобы получить любую информацию от пользователя.</span><span class="sxs-lookup"><span data-stu-id="881be-119">To use an Adaptive card task module from a tab your app must include a bot to get any information back from the user.</span></span> <span data-ttu-id="881be-120">Это объясняется ниже.</span><span class="sxs-lookup"><span data-stu-id="881be-120">This is explained below.</span></span>

## <a name="example-invoking-a-task-module"></a><span data-ttu-id="881be-121">Пример: наводка модуля задач</span><span class="sxs-lookup"><span data-stu-id="881be-121">Example: Invoking a task module</span></span>

<span data-ttu-id="881be-122">Ниже приведен код, адаптированный из [примера модуля задач.](~/task-modules-and-cards/what-are-task-modules.md#code-sample)</span><span class="sxs-lookup"><span data-stu-id="881be-122">The code below is adapted from [the task module sample](~/task-modules-and-cards/what-are-task-modules.md#code-sample).</span></span> <span data-ttu-id="881be-123">Вот как выглядит модуль задач:</span><span class="sxs-lookup"><span data-stu-id="881be-123">Here's what the task module looks like:</span></span>

![Модуль задач — настраиваемая форма](~/assets/images/task-module/task-module-custom-form.png)

<span data-ttu-id="881be-125">Это `submitHandler` очень просто; оно просто перекликается со значением консоли или `err` `result` консоли:</span><span class="sxs-lookup"><span data-stu-id="881be-125">The `submitHandler` is very simple; it just echoes the value of `err` or `result` to the console:</span></span>

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

## <a name="submitting-the-result-of-a-task-module"></a><span data-ttu-id="881be-126">Отправка результатов модуля задач</span><span class="sxs-lookup"><span data-stu-id="881be-126">Submitting the result of a task module</span></span>

<span data-ttu-id="881be-127">Функция `submitHandler` используется с `TaskInfo.url` .</span><span class="sxs-lookup"><span data-stu-id="881be-127">The `submitHandler` function is used with `TaskInfo.url`.</span></span> <span data-ttu-id="881be-128">Функция `submitHandler` находится на `TaskInfo.url` веб-странице.</span><span class="sxs-lookup"><span data-stu-id="881be-128">The `submitHandler` function resides in the `TaskInfo.url` web page.</span></span> <span data-ttu-id="881be-129">Если при вызове модуля задачи возникла ошибка, функция будет немедленно вызвана строкой, указывающей, какая `submitHandler` `err` ошибка [произошла.](#task-module-invocation-errors)</span><span class="sxs-lookup"><span data-stu-id="881be-129">If there's an error when invoking the task module your `submitHandler` function will be immediately invoked with an `err` string indicating which [error occurred](#task-module-invocation-errors).</span></span> <span data-ttu-id="881be-130">Функция также называется строкой, когда пользователь нажимает X в правом верхнем `submitHandler` `err` справа от модуля задач.</span><span class="sxs-lookup"><span data-stu-id="881be-130">The `submitHandler` function is also called with an `err` string when the user presses the X at the upper right of task module.</span></span>

<span data-ttu-id="881be-131">Если нет ошибки вызова и пользователь не нажимает X, чтобы отклонять ее, пользователь нажимает кнопку по завершению.</span><span class="sxs-lookup"><span data-stu-id="881be-131">If there's no invocation error and the user doesn't press X to dismiss it, the user presses a button when finished.</span></span> <span data-ttu-id="881be-132">В зависимости от того, url-адрес или адаптивная карта в модуле задач, вот что происходит:</span><span class="sxs-lookup"><span data-stu-id="881be-132">Depending on whether it's a URL or an Adaptive card in the task module, here's what happens:</span></span>

### <a name="htmljavascript-taskinfourl"></a><span data-ttu-id="881be-133">HTML/JavaScript ( `TaskInfo.url` )</span><span class="sxs-lookup"><span data-stu-id="881be-133">HTML/JavaScript (`TaskInfo.url`)</span></span>

<span data-ttu-id="881be-134">После проверки того, что вошел пользователь, вызовите функцию SDK (далее она называется для целей `microsoftTeams.tasks.submitTask()` `submitTask()` читаемости).</span><span class="sxs-lookup"><span data-stu-id="881be-134">Once you've validated what the user has entered you call the `microsoftTeams.tasks.submitTask()` SDK function (referred to hereafter as `submitTask()` for readability purposes).</span></span> <span data-ttu-id="881be-135">Вы можете звонить без параметров, если Teams хотите закрыть модуль задач, но большую часть времени вам нужно будет передать объект или строку `submitTask()` в `submitHandler` ваш .</span><span class="sxs-lookup"><span data-stu-id="881be-135">You can call `submitTask()` without any parameters if you just want Teams to close the task module, but most of the time you'll want to pass an object or a string to your `submitHandler`.</span></span>

<span data-ttu-id="881be-136">Передай результат в качестве первого параметра.</span><span class="sxs-lookup"><span data-stu-id="881be-136">Pass your result as the first parameter.</span></span> <span data-ttu-id="881be-137">Teams будет вызывать, где будет и будет объект `submitHandler` `err` или `null` строка, которую вы `result` передали `submitTask()` .</span><span class="sxs-lookup"><span data-stu-id="881be-137">Teams will invoke `submitHandler` where `err` will be `null` and `result` will be the object/string you passed to `submitTask()`.</span></span> <span data-ttu-id="881be-138">Если вы вызываете с параметром, необходимо передать или массив строк: это позволяет Teams проверить, что приложение, отправляя результат, является тем же, что вызывалось в модуль `submitTask()` `result`  `appId` `appId` задач.</span><span class="sxs-lookup"><span data-stu-id="881be-138">If you do call `submitTask()` with a `result` parameter, you **must** pass an `appId` or an array of `appId` strings: this allows Teams to validate that the app sending the result is the same one which invoked the task module.</span></span>

### <a name="adaptive-card-taskinfocard"></a><span data-ttu-id="881be-139">Адаптивная карта ( `TaskInfo.card` )</span><span class="sxs-lookup"><span data-stu-id="881be-139">Adaptive card (`TaskInfo.card`)</span></span>

<span data-ttu-id="881be-140">Если вы вызывали модуль задач с кнопкой , когда пользователь нажимает кнопку, значения в карточке будут возвращены в качестве `submitHandler` `Action.Submit` значения `result` .</span><span class="sxs-lookup"><span data-stu-id="881be-140">If you invoked the task module with a `submitHandler`, when the user presses an `Action.Submit` button the values in the card will be returned as the value of `result`.</span></span> <span data-ttu-id="881be-141">Если пользователь нажал кнопку Esc или нажал клавишу X, он будет `err` возвращен.</span><span class="sxs-lookup"><span data-stu-id="881be-141">If the user presses the Esc button or presses the X, `err` will be returned instead.</span></span> <span data-ttu-id="881be-142">Кроме того, если приложение содержит бот в дополнение к вкладке, вы можете просто включить бот в качестве значения `appId` `completionBotId` в `TaskInfo` объекте.</span><span class="sxs-lookup"><span data-stu-id="881be-142">Alternatively, if your app contains a bot in addition to a tab you can simply include the `appId` of the bot as the value of `completionBotId` in the `TaskInfo` object.</span></span> <span data-ttu-id="881be-143">При нажатии кнопки в бот будет отправлено тело адаптивной карты (как заполнено `task/submit invoke` `Action.Submit` пользователем).</span><span class="sxs-lookup"><span data-stu-id="881be-143">The Adaptive card body (as filled in by the user) will be sent to the bot via a `task/submit invoke` message when the user presses an `Action.Submit` button.</span></span> <span data-ttu-id="881be-144">Схема объекта, который вы получаете, очень похожа на схему, которую вы получаете для задач/извлечений и [задач/отправки сообщений;](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages) Единственное отличие состоит в том, что схема объекта JSON является объектом  адаптивной карты, а не объектом, содержащим объект адаптивной карты, как когда адаптивные карты используются с [ботами.](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages)</span><span class="sxs-lookup"><span data-stu-id="881be-144">The schema for the object you receive is very similar to [the schema you receive for task/fetch and task/submit messages](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages); the only difference is that the schema of the JSON object is an Adaptive card object as opposed to an object *containing* an Adaptive card object as [when Adaptive cards are used with bots](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages).</span></span>

## <a name="example-submitting-the-result-of-a-task-module"></a><span data-ttu-id="881be-145">Пример: отправка результата модуля задач</span><span class="sxs-lookup"><span data-stu-id="881be-145">Example: submitting the result of a task module</span></span>

<span data-ttu-id="881be-146">Отзыв формы [в модуле задач выше](#example-invoking-a-task-module) с помощью HTML-формы.</span><span class="sxs-lookup"><span data-stu-id="881be-146">Recall the [form in the task module above](#example-invoking-a-task-module) with an HTML form.</span></span> <span data-ttu-id="881be-147">Вот где определена форма:</span><span class="sxs-lookup"><span data-stu-id="881be-147">Here's where the form is defined:</span></span>

```html
<form method="POST" id="customerForm" action="/register" onSubmit="return validateForm()">
```

<span data-ttu-id="881be-148">В этой форме есть пять полей, но нам интересны только значения трех из них для этого примера: `name` `email` и `favoriteBook` .</span><span class="sxs-lookup"><span data-stu-id="881be-148">There are five fields on this form but we're only interested in the values of three of them for this example: `name`, `email`, and `favoriteBook`.</span></span>

<span data-ttu-id="881be-149">Вот `validateForm()` функция, которая `submitTask()` вызывает:</span><span class="sxs-lookup"><span data-stu-id="881be-149">Here's the `validateForm()` function that calls `submitTask()`:</span></span>

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

## <a name="task-module-invocation-errors"></a><span data-ttu-id="881be-150">Ошибки при вызове модуля задач</span><span class="sxs-lookup"><span data-stu-id="881be-150">Task module invocation errors</span></span>

<span data-ttu-id="881be-151">Вот возможные значения, `err` которые могут быть получены `submitHandler` вашим:</span><span class="sxs-lookup"><span data-stu-id="881be-151">Here are the possible values of `err` that can be received by your `submitHandler`:</span></span>

| <span data-ttu-id="881be-152">Проблема</span><span class="sxs-lookup"><span data-stu-id="881be-152">Problem</span></span> | <span data-ttu-id="881be-153">Сообщение об ошибке (значение `err` )</span><span class="sxs-lookup"><span data-stu-id="881be-153">Error message (value of `err`)</span></span> |
| ------- | ------------------------------ |
| <span data-ttu-id="881be-154">Значения для обоих `TaskInfo.url` и `TaskInfo.card` были указаны.</span><span class="sxs-lookup"><span data-stu-id="881be-154">Values for both `TaskInfo.url` and `TaskInfo.card` were specified.</span></span> | <span data-ttu-id="881be-155">"Значения для карты и URL-адреса были указаны.</span><span class="sxs-lookup"><span data-stu-id="881be-155">"Values for both card and url were specified.</span></span> <span data-ttu-id="881be-156">Разрешено одно или другое, но не то и другое".</span><span class="sxs-lookup"><span data-stu-id="881be-156">One or the other, but not both, are allowed."</span></span> |
| <span data-ttu-id="881be-157">Ни `TaskInfo.url` `TaskInfo.card` указанных, ни указанных.</span><span class="sxs-lookup"><span data-stu-id="881be-157">Neither `TaskInfo.url` nor `TaskInfo.card` specified.</span></span> | <span data-ttu-id="881be-158">"Необходимо указать значение для карты или URL-адреса".</span><span class="sxs-lookup"><span data-stu-id="881be-158">"You must specify a value for either card or url."</span></span> |
| <span data-ttu-id="881be-159">Недействительный `appId` .</span><span class="sxs-lookup"><span data-stu-id="881be-159">Invalid `appId`.</span></span> | <span data-ttu-id="881be-160">"Недействительный appId".</span><span class="sxs-lookup"><span data-stu-id="881be-160">"Invalid appId."</span></span> |
| <span data-ttu-id="881be-161">Пользователь нажал кнопку X, закрыв ее.</span><span class="sxs-lookup"><span data-stu-id="881be-161">User pressed X button, closing it.</span></span> | <span data-ttu-id="881be-162">"Пользователь отменил или закрыл модуль задач".</span><span class="sxs-lookup"><span data-stu-id="881be-162">"User cancelled/closed the task module."</span></span> |
