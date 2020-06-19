---
title: Использование модулей задач на вкладках Microsoft Teams
description: Сведения о том, как вызывать модули задач из вкладок Teams с помощью клиентского пакета SDK Microsoft Teams.
keywords: модули задач вкладки Teams клиентский пакет SDK
ms.openlocfilehash: e10958195713f338a9b5e0a0672d8b6a29da9264
ms.sourcegitcommit: 2a84a3c8b10771e37ce51bf603a967633947a3e4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/10/2020
ms.locfileid: "44801200"
---
# <a name="using-task-modules-in-tabs"></a><span data-ttu-id="54cd3-104">Использование модулей задач на вкладках</span><span class="sxs-lookup"><span data-stu-id="54cd3-104">Using task modules in tabs</span></span>

<span data-ttu-id="54cd3-105">Добавление модуля задач на вкладку может значительно упростить взаимодействие пользователя с рабочими процессами, требующими ввода данных.</span><span class="sxs-lookup"><span data-stu-id="54cd3-105">Adding a task module to your tab can greatly simplify your user's experience for any workflows that require data input.</span></span> <span data-ttu-id="54cd3-106">Модули задач позволяют собирать свои данные в всплывающем окне, поддерживающем Teams.</span><span class="sxs-lookup"><span data-stu-id="54cd3-106">Task modules allow you to gather their input in a Teams-aware popup.</span></span> <span data-ttu-id="54cd3-107">Хорошим примером является редактирование карточек планировщика; для создания аналогичных возможностей можно использовать модули задач.</span><span class="sxs-lookup"><span data-stu-id="54cd3-107">A good example of this is editing Planner cards; you can use task modules to create a similar experience.</span></span>

<span data-ttu-id="54cd3-108">Для поддержки функции модуля задач в [клиентский пакет SDK Microsoft Teams](/javascript/api/overview/msteams-client)добавлены две новые функции:</span><span class="sxs-lookup"><span data-stu-id="54cd3-108">To support the task module feature, two new functions were added to the [Microsoft Teams client SDK](/javascript/api/overview/msteams-client):</span></span>

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

<span data-ttu-id="54cd3-109">Давайте посмотрим, как работает каждый из них.</span><span class="sxs-lookup"><span data-stu-id="54cd3-109">Let's see how each of them work.</span></span>

## <a name="invoking-a-task-module-from-a-tab"></a><span data-ttu-id="54cd3-110">Вызов модуля задачи из вкладки</span><span class="sxs-lookup"><span data-stu-id="54cd3-110">Invoking a task module from a tab</span></span>

<span data-ttu-id="54cd3-111">Чтобы вызвать модуль задач на вкладке, используйте `microsoftTeams.tasks.startTask()` передачу [объекта таскинфо](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) и необязательную `submitHandler` функцию обратного вызова.</span><span class="sxs-lookup"><span data-stu-id="54cd3-111">To invoke a task module from a tab use `microsoftTeams.tasks.startTask()` passing a [TaskInfo object](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) and an optional `submitHandler` callback function.</span></span> <span data-ttu-id="54cd3-112">Как было сказано ранее, следует учитывать два случая:</span><span class="sxs-lookup"><span data-stu-id="54cd3-112">As described earlier, there are two cases to consider:</span></span>

1. <span data-ttu-id="54cd3-113">Значение равно `TaskInfo.url` URL-адресу.</span><span class="sxs-lookup"><span data-stu-id="54cd3-113">The value of `TaskInfo.url` is set to a URL.</span></span> <span data-ttu-id="54cd3-114">Откроется окно модуль задачи, в котором `TaskModule.url` она загружена `<iframe>` .</span><span class="sxs-lookup"><span data-stu-id="54cd3-114">The task module window appears and `TaskModule.url` is loaded as an `<iframe>` inside it.</span></span> <span data-ttu-id="54cd3-115">На этой странице должен вызываться JavaScript `microsoftTeams.initialize()` .</span><span class="sxs-lookup"><span data-stu-id="54cd3-115">JavaScript on that page should call `microsoftTeams.initialize()`.</span></span> <span data-ttu-id="54cd3-116">Если `submitHandler` на странице имеется функция и возникает ошибка при вызове `microsoftTeams.tasks.startTask()` , `submitHandler` вызывается параметр WITH `err` Set to String Error, указывающий на ошибку, как описано [ниже](#task-module-invocation-errors).</span><span class="sxs-lookup"><span data-stu-id="54cd3-116">If there is a `submitHandler` function on the page and there is an error when invoking `microsoftTeams.tasks.startTask()`, then `submitHandler` is invoked with `err` set to the error string indicating the error as described [below](#task-module-invocation-errors).</span></span>
1. <span data-ttu-id="54cd3-117">Значение `taskInfo.card` — это [Формат JSON для адаптивной карточки](~/task-modules-and-cards/what-are-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment).</span><span class="sxs-lookup"><span data-stu-id="54cd3-117">The value of `taskInfo.card` is the [JSON for an Adaptive card](~/task-modules-and-cards/what-are-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment).</span></span> <span data-ttu-id="54cd3-118">В этом случае, очевидно, не существует функции JavaScript, `submitHandler` которая вызывается, когда пользователь закрывает или нажимает кнопку на адаптивной карточке; единственный способ получить значение, введенное пользователем, — передать результат в Bot.</span><span class="sxs-lookup"><span data-stu-id="54cd3-118">In this case there's obviously not any JavaScript `submitHandler` function to call when the user closes or presses a button on the Adaptive card; the only way to receive what the user entered is by passing the result to a bot.</span></span> <span data-ttu-id="54cd3-119">Чтобы использовать модуль задачи адаптивной карточки на вкладке, ваше приложение должно включать Bot для получения информации от пользователя.</span><span class="sxs-lookup"><span data-stu-id="54cd3-119">To use an Adaptive card task module from a tab your app must include a bot to get any information back from the user.</span></span> <span data-ttu-id="54cd3-120">Это объясняется ниже.</span><span class="sxs-lookup"><span data-stu-id="54cd3-120">This is explained below.</span></span>

## <a name="example-invoking-a-task-module"></a><span data-ttu-id="54cd3-121">Пример: вызов модуля задачи</span><span class="sxs-lookup"><span data-stu-id="54cd3-121">Example: Invoking a task module</span></span>

<span data-ttu-id="54cd3-122">Приведенный ниже код передается из [примера модуля задач](~/task-modules-and-cards/what-are-task-modules.md#task-module-samples).</span><span class="sxs-lookup"><span data-stu-id="54cd3-122">The code below is adapted from [the task module sample](~/task-modules-and-cards/what-are-task-modules.md#task-module-samples).</span></span> <span data-ttu-id="54cd3-123">Вот как выглядит модуль задачи:</span><span class="sxs-lookup"><span data-stu-id="54cd3-123">Here's what the task module looks like:</span></span>

![Модуль задачи — настраиваемая форма](~/assets/images/task-module/task-module-custom-form.png)

<span data-ttu-id="54cd3-125">Это `submitHandler` очень простая программа, которая просто отображает значение `err` или `result` в консоли:</span><span class="sxs-lookup"><span data-stu-id="54cd3-125">The `submitHandler` is very simple; it just echoes the value of `err` or `result` to the console:</span></span>

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

## <a name="submitting-the-result-of-a-task-module"></a><span data-ttu-id="54cd3-126">Отправка результата модуля задачи</span><span class="sxs-lookup"><span data-stu-id="54cd3-126">Submitting the result of a task module</span></span>

<span data-ttu-id="54cd3-127">`submitHandler`Функция используется с `TaskInfo.url` .</span><span class="sxs-lookup"><span data-stu-id="54cd3-127">The `submitHandler` function is used with `TaskInfo.url`.</span></span> <span data-ttu-id="54cd3-128">`submitHandler`Функция находится на `TaskInfo.url` веб-странице.</span><span class="sxs-lookup"><span data-stu-id="54cd3-128">The `submitHandler` function resides in the `TaskInfo.url` web page.</span></span> <span data-ttu-id="54cd3-129">При возникновении ошибки при вызове модуля задач `submitHandler` функция будет сразу же вызываться со `err` строкой, указывающей, какая [Ошибка возникла](#task-module-invocation-errors).</span><span class="sxs-lookup"><span data-stu-id="54cd3-129">If there's an error when invoking the task module your `submitHandler` function will be immediately invoked with an `err` string indicating which [error occurred](#task-module-invocation-errors).</span></span> <span data-ttu-id="54cd3-130">`submitHandler`Функция также вызывается с помощью `err` строки, когда пользователь нажимает клавишу X в верхнем правом углу модуля задач.</span><span class="sxs-lookup"><span data-stu-id="54cd3-130">The `submitHandler` function is also called with an `err` string when the user presses the X at the upper right of task module.</span></span>

<span data-ttu-id="54cd3-131">Если нет ошибки вызова, а пользователь не нажмет клавишу X, то при завершении работы пользователь нажимает кнопку.</span><span class="sxs-lookup"><span data-stu-id="54cd3-131">If there's no invocation error and the user doesn't press X to dismiss it, the user presses a button when finished.</span></span> <span data-ttu-id="54cd3-132">В зависимости от того, является ли URL-адрес или Адаптивная карта в модуле задач, происходит следующее:</span><span class="sxs-lookup"><span data-stu-id="54cd3-132">Depending on whether it's a URL or an Adaptive card in the task module, here's what happens:</span></span>

### <a name="htmljavascript-taskinfourl"></a><span data-ttu-id="54cd3-133">HTML/JavaScript ( `TaskInfo.url` )</span><span class="sxs-lookup"><span data-stu-id="54cd3-133">HTML/JavaScript (`TaskInfo.url`)</span></span>

<span data-ttu-id="54cd3-134">После проверки того, что ввел пользователь, вы вызываете `microsoftTeams.tasks.submitTask()` функцию SDK (которая называется "в дальнейшем `submitTask()` " для удобства чтения).</span><span class="sxs-lookup"><span data-stu-id="54cd3-134">Once you've validated what the user has entered you call the `microsoftTeams.tasks.submitTask()` SDK function (referred to hereafter as `submitTask()` for readability purposes).</span></span> <span data-ttu-id="54cd3-135">Вы можете вызвать `submitTask()` без параметров, если вы хотите, чтобы команда закрывала модуль задач, но в большинстве случаев требуется передать объект или строку в `submitHandler` .</span><span class="sxs-lookup"><span data-stu-id="54cd3-135">You can call `submitTask()` without any parameters if you just want Teams to close the task module, but most of the time you'll want to pass an object or a string to your `submitHandler`.</span></span>

<span data-ttu-id="54cd3-136">Передайте результат в качестве первого параметра.</span><span class="sxs-lookup"><span data-stu-id="54cd3-136">Pass your result as the first parameter.</span></span> <span data-ttu-id="54cd3-137">Teams вызовет, `submitHandler` где `err` будет использоваться `null` `result` объект или строка, которые вы передали `submitTask()` .</span><span class="sxs-lookup"><span data-stu-id="54cd3-137">Teams will invoke `submitHandler` where `err` will be `null` and `result` will be the object/string you passed to `submitTask()`.</span></span> <span data-ttu-id="54cd3-138">При вызове `submitTask()` с `result` параметром **необходимо** передать объект `appId` или массив `appId` строк: Это позволяет Teams проверить, что приложение отправляет результат, то же, что вызвало модуль задачи.</span><span class="sxs-lookup"><span data-stu-id="54cd3-138">If you do call `submitTask()` with a `result` parameter, you **must** pass an `appId` or an array of `appId` strings: this allows Teams to validate that the app sending the result is the same one which invoked the task module.</span></span>

### <a name="adaptive-card-taskinfocard"></a><span data-ttu-id="54cd3-139">Адаптивная карта ( `TaskInfo.card` )</span><span class="sxs-lookup"><span data-stu-id="54cd3-139">Adaptive card (`TaskInfo.card`)</span></span>

<span data-ttu-id="54cd3-140">Если вы вызвали модуль Task с параметром `submitHandler` , когда пользователь нажимает кнопку, `Action.Submit` значения в карточке будут возвращены как значение `result` .</span><span class="sxs-lookup"><span data-stu-id="54cd3-140">If you invoked the task module with a `submitHandler`, when the user presses an `Action.Submit` button the values in the card will be returned as the value of `result`.</span></span> <span data-ttu-id="54cd3-141">Если пользователь нажимает кнопку ESC или нажимает клавишу X, `err` возвращается вместо него.</span><span class="sxs-lookup"><span data-stu-id="54cd3-141">If the user presses the Esc button or presses the X, `err` will be returned instead.</span></span> <span data-ttu-id="54cd3-142">Кроме того, если ваше приложение содержит Bot в дополнение к вкладке, можно просто включить `appId` объект Bot в качестве значения `completionBotId` в `TaskInfo` объект.</span><span class="sxs-lookup"><span data-stu-id="54cd3-142">Alternatively, if your app contains a bot in addition to a tab you can simply include the `appId` of the bot as the value of `completionBotId` in the `TaskInfo` object.</span></span> <span data-ttu-id="54cd3-143">Текст адаптивной карточки (которая заполняется пользователем) будет отправлен в объект Bot через `task/submit invoke` сообщение, когда пользователь нажимает `Action.Submit` кнопку.</span><span class="sxs-lookup"><span data-stu-id="54cd3-143">The Adaptive card body (as filled in by the user) will be sent to the bot via a `task/submit invoke` message when the user presses an `Action.Submit` button.</span></span> <span data-ttu-id="54cd3-144">Схема получаемого объекта очень похожа на [схему, полученную для сообщений Task/Receive и Task/отправить](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages). Единственное отличие состоит в том, что схема объекта JSON является объектом адаптивной карточки, а не объектом, *содержащим* объект адаптивной карточки, как [при использовании адаптивных карточек с Боты](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages).</span><span class="sxs-lookup"><span data-stu-id="54cd3-144">The schema for the object you receive is very similar to [the schema you receive for task/fetch and task/submit messages](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages); the only difference is that the schema of the JSON object is an Adaptive card object as opposed to an object *containing* an Adaptive card object as [when Adaptive cards are used with bots](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages).</span></span>

## <a name="example-submitting-the-result-of-a-task-module"></a><span data-ttu-id="54cd3-145">Пример: отправка результата модуля задачи</span><span class="sxs-lookup"><span data-stu-id="54cd3-145">Example: submitting the result of a task module</span></span>

<span data-ttu-id="54cd3-146">Подпомните [форму в модуле задач выше](#example-invoking-a-task-module) с HTML-формой.</span><span class="sxs-lookup"><span data-stu-id="54cd3-146">Recall the [form in the task module above](#example-invoking-a-task-module) with an HTML form.</span></span> <span data-ttu-id="54cd3-147">Ниже показано, где определяется форма:</span><span class="sxs-lookup"><span data-stu-id="54cd3-147">Here's where the form is defined:</span></span>

```html
<form method="POST" id="customerForm" action="/register" onSubmit="return validateForm()">
```

<span data-ttu-id="54cd3-148">В этой форме имеется пять полей, но для этого примера требуются только значения трех из них: `name` , `email` и `favoriteBook` .</span><span class="sxs-lookup"><span data-stu-id="54cd3-148">There are five fields on this form but we're only interested in the values of three of them for this example: `name`, `email`, and `favoriteBook`.</span></span>

<span data-ttu-id="54cd3-149">Вот `validateForm()` функция, которая вызывает `submitTask()` :</span><span class="sxs-lookup"><span data-stu-id="54cd3-149">Here's the `validateForm()` function that calls `submitTask()`:</span></span>

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

## <a name="task-module-invocation-errors"></a><span data-ttu-id="54cd3-150">Ошибки вызовов модулей задач</span><span class="sxs-lookup"><span data-stu-id="54cd3-150">Task module invocation errors</span></span>

<span data-ttu-id="54cd3-151">Ниже приведены возможные значения `err` , которые могут быть получены `submitHandler` :</span><span class="sxs-lookup"><span data-stu-id="54cd3-151">Here are the possible values of `err` that can be received by your `submitHandler`:</span></span>

| <span data-ttu-id="54cd3-152">Проблема</span><span class="sxs-lookup"><span data-stu-id="54cd3-152">Problem</span></span> | <span data-ttu-id="54cd3-153">Сообщение об ошибке (значение `err` )</span><span class="sxs-lookup"><span data-stu-id="54cd3-153">Error message (value of `err`)</span></span> |
| ------- | ------------------------------ |
| <span data-ttu-id="54cd3-154">Указаны значения для обоих типов `TaskInfo.url` `TaskInfo.card` .</span><span class="sxs-lookup"><span data-stu-id="54cd3-154">Values for both `TaskInfo.url` and `TaskInfo.card` were specified.</span></span> | <span data-ttu-id="54cd3-155">"Указаны значения для карты и URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="54cd3-155">"Values for both card and url were specified.</span></span> <span data-ttu-id="54cd3-156">Разрешены только один или другой, но не оба. "</span><span class="sxs-lookup"><span data-stu-id="54cd3-156">One or the other, but not both, are allowed."</span></span> |
| <span data-ttu-id="54cd3-157">Ни `TaskInfo.url` значение `TaskInfo.card` , ни не указано.</span><span class="sxs-lookup"><span data-stu-id="54cd3-157">Neither `TaskInfo.url` nor `TaskInfo.card` specified.</span></span> | <span data-ttu-id="54cd3-158">"Необходимо указать значение для каждой из карточек или URL-адреса".</span><span class="sxs-lookup"><span data-stu-id="54cd3-158">"You must specify a value for either card or url."</span></span> |
| <span data-ttu-id="54cd3-159">Недопустимый `appId` .</span><span class="sxs-lookup"><span data-stu-id="54cd3-159">Invalid `appId`.</span></span> | <span data-ttu-id="54cd3-160">"Недопустимый appId."</span><span class="sxs-lookup"><span data-stu-id="54cd3-160">"Invalid appId."</span></span> |
| <span data-ttu-id="54cd3-161">Нажатая пользователем кнопка X, закрывающая ее.</span><span class="sxs-lookup"><span data-stu-id="54cd3-161">User pressed X button, closing it.</span></span> | <span data-ttu-id="54cd3-162">"Пользователь отменил/закрыл модуль задач".</span><span class="sxs-lookup"><span data-stu-id="54cd3-162">"User cancelled/closed the task module."</span></span> |
