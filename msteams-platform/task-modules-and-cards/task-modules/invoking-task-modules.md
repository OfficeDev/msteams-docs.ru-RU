---
title: Вызов и увольнение модулей задач
description: Вызов и увольнение модулей задач.
author: surbhigupta12
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: a23d5cee3f13967772a4b58ed973bf08906e36a6
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140780"
---
# <a name="invoke-and-dismiss-task-modules"></a><span data-ttu-id="9aced-103">Вызов и увольнение модулей задач</span><span class="sxs-lookup"><span data-stu-id="9aced-103">Invoke and dismiss task modules</span></span>

<span data-ttu-id="9aced-104">Модули задач можно вызывать из вкладок, ботов или глубоких ссылок.</span><span class="sxs-lookup"><span data-stu-id="9aced-104">Task modules can be invoked from tabs, bots, or deep links.</span></span> <span data-ttu-id="9aced-105">Ответ может быть как в HTML, JavaScript, так и в качестве адаптивной карты.</span><span class="sxs-lookup"><span data-stu-id="9aced-105">The response can be either in HTML, JavaScript, or as an Adaptive Card.</span></span> <span data-ttu-id="9aced-106">Существует большая гибкость с точки зрения вызова модулей задач и реагирования на взаимодействие пользователя.</span><span class="sxs-lookup"><span data-stu-id="9aced-106">There is a lot of flexibility in terms of how task modules are invoked and how to deal with the response of the user's interaction.</span></span> <span data-ttu-id="9aced-107">В следующей таблице кратко излагается, как это работает:</span><span class="sxs-lookup"><span data-stu-id="9aced-107">The following table summarizes how this works:</span></span>

| <span data-ttu-id="9aced-108">Вызывается с помощью</span><span class="sxs-lookup"><span data-stu-id="9aced-108">Invoked using</span></span> | <span data-ttu-id="9aced-109">Модуль задач с HTML или JavaScript</span><span class="sxs-lookup"><span data-stu-id="9aced-109">Task module with HTML or JavaScript</span></span> | <span data-ttu-id="9aced-110">Модуль задач с адаптивной картой</span><span class="sxs-lookup"><span data-stu-id="9aced-110">Task module with Adaptive Card</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9aced-111">JavaScript на вкладке</span><span class="sxs-lookup"><span data-stu-id="9aced-111">JavaScript in a tab</span></span> | <span data-ttu-id="9aced-112">1. Используйте функцию Teams SDK с необязательной функцией `tasks.startTask()` `submitHandler(err, result)` вызова.</span><span class="sxs-lookup"><span data-stu-id="9aced-112">1. Use the Teams client SDK function `tasks.startTask()` with an optional `submitHandler(err, result)` callback function.</span></span> <br/><br/> <span data-ttu-id="9aced-113">2. В коде модуля задач, когда пользователь выполнил действия, вызываем функцию Teams SDK с объектом `tasks.submitTask()` `result` в качестве параметра.</span><span class="sxs-lookup"><span data-stu-id="9aced-113">2. In the task module code, when the user has performed the actions, call the Teams SDK function `tasks.submitTask()` with a `result` object as a parameter.</span></span> <span data-ttu-id="9aced-114">Если был указан вызов, Teams вызывает его `submitHandler` в качестве `tasks.startTask()` `result` параметра.</span><span class="sxs-lookup"><span data-stu-id="9aced-114">If a `submitHandler` callback was specified in `tasks.startTask()`, Teams calls it with `result` as a parameter.</span></span> <span data-ttu-id="9aced-115">Если при призыве произошла ошибка, функция `tasks.startTask()` `submitHandler` называется `err` строкой.</span><span class="sxs-lookup"><span data-stu-id="9aced-115">If there was an error when invoking `tasks.startTask()`, the `submitHandler` function is called with an `err` string instead.</span></span> <br/><br/> <span data-ttu-id="9aced-116">3. Вы также можете указать при `completionBotId` вызове `teams.startTask()` .</span><span class="sxs-lookup"><span data-stu-id="9aced-116">3. You can also specify a `completionBotId` when calling `teams.startTask()`.</span></span> <span data-ttu-id="9aced-117">Затем вместо `result` этого отправляется бот.</span><span class="sxs-lookup"><span data-stu-id="9aced-117">Then the `result` is sent to the bot instead.</span></span> | <span data-ttu-id="9aced-118">1. Вызов Teams клиентской SDK-функции с объектом TaskInfo и содержащим JSON для адаптивной карты, чтобы показать в всплывающее всплывающее представление модуля `tasks.startTask()` [](#the-taskinfo-object) `TaskInfo.card` задач.</span><span class="sxs-lookup"><span data-stu-id="9aced-118">1. Call the Teams client SDK function `tasks.startTask()` with a [TaskInfo object](#the-taskinfo-object) and `TaskInfo.card` containing the JSON for the Adaptive Card to show in the task module pop-up.</span></span> <br/><br/> <span data-ttu-id="9aced-119">2. Если вызов был указан в , Teams вызывает его строкой, если произошла ошибка при вызове или если пользователь закрывает всплывающее всплывающее сообщение модуля задач с помощью X в правом верхнем `submitHandler` `tasks.startTask()` `err` `tasks.startTask()` ряду.</span><span class="sxs-lookup"><span data-stu-id="9aced-119">2. If a `submitHandler` callback was specified in `tasks.startTask()`, Teams calls it with an `err` string, if there was an error when invoking `tasks.startTask()` or if the user closes the task module pop-up using the X at the upper right.</span></span> <br/><br/> <span data-ttu-id="9aced-120">3. Если пользователь нажимает кнопку, его объект возвращается `Action.Submit` `data` в качестве значения `result` .</span><span class="sxs-lookup"><span data-stu-id="9aced-120">3. If the user presses an `Action.Submit` button then its `data` object is returned as the value of `result`.</span></span> |
| <span data-ttu-id="9aced-121">Кнопка карточки бота</span><span class="sxs-lookup"><span data-stu-id="9aced-121">Bot card button</span></span> | <span data-ttu-id="9aced-122">1. Кнопки бот-карты в зависимости от типа кнопки могут вызывать модули задач двумя способами: URL-адресом глубокой ссылки или отправкой `task/fetch` сообщения.</span><span class="sxs-lookup"><span data-stu-id="9aced-122">1. Bot card buttons, depending on the type of button, can invoke task modules in two ways, a deep link URL or by sending a `task/fetch` message.</span></span> <br/><br/> <span data-ttu-id="9aced-123">2. Если действие кнопки является типом кнопки для адаптивных карт, событие HTTP POST отправляется `type` `task/fetch` `Action.Submit` `task/fetch invoke` боту.</span><span class="sxs-lookup"><span data-stu-id="9aced-123">2. If the button's action `type` is `task/fetch` that is `Action.Submit` button type for Adaptive Cards, a `task/fetch invoke` event that is an HTTP POST is sent to the bot.</span></span> <span data-ttu-id="9aced-124">Бот отвечает на СООБЩЕНИЕ с помощью HTTP 200 и тело отклика, содержащее оболочку вокруг объекта [TaskInfo.](#the-taskinfo-object)</span><span class="sxs-lookup"><span data-stu-id="9aced-124">The bot responds to the POST with HTTP 200 and the response body containing a wrapper around the [TaskInfo object](#the-taskinfo-object).</span></span> <span data-ttu-id="9aced-125">Дополнительные сведения см. [в ссылке `task/fetch` на ссылку на модуль задач с помощью ](~/task-modules-and-cards/task-modules/task-modules-bots.md#invoke-a-task-module-using-taskfetch).</span><span class="sxs-lookup"><span data-stu-id="9aced-125">For more information, see [invoking a task module using `task/fetch`](~/task-modules-and-cards/task-modules/task-modules-bots.md#invoke-a-task-module-using-taskfetch).</span></span> <span data-ttu-id="9aced-126">Teams отображает модуль задач.</span><span class="sxs-lookup"><span data-stu-id="9aced-126">Teams displays the task module.</span></span> <br/><br/> <span data-ttu-id="9aced-127">3. После выполнения действий пользователем вызываем Teams SDK с объектом `tasks.submitTask()` `result` в качестве параметра.</span><span class="sxs-lookup"><span data-stu-id="9aced-127">3. After the user has performed the actions, call the Teams SDK function `tasks.submitTask()` with a `result` object as a parameter.</span></span> <span data-ttu-id="9aced-128">Бот получает `task/submit invoke` сообщение, содержаное `result` объект.</span><span class="sxs-lookup"><span data-stu-id="9aced-128">The bot receives a `task/submit invoke` message that contains the `result` object.</span></span> <br/><br/> <span data-ttu-id="9aced-129">4. У вас есть три различных способа ответа на сообщение, не делая ничего, что является успешно выполненной задачей, отобразив сообщение пользователю в всплывающее окно или путем запроса другого окна модуля `task/submit` задач.</span><span class="sxs-lookup"><span data-stu-id="9aced-129">4. You have three different ways to respond to the `task/submit` message, by doing nothing that is the task completed successfully, by displaying a message to the user in a pop-up window, or by invoking another task module window.</span></span> <span data-ttu-id="9aced-130">Дополнительные сведения см. в [подробном обсуждении. `task/submit` ](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit)</span><span class="sxs-lookup"><span data-stu-id="9aced-130">For more information, see [detailed discussion on `task/submit`](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit).</span></span> | <ul><li> <span data-ttu-id="9aced-131">Как и кнопки на картах Bot Framework, кнопки адаптивных карт поддерживают два способа вызова модулей задач, глубокие ссылки URL-адресов с кнопками и использование `Action.openUrl` `task/fetch` `Action.Submit` кнопок.</span><span class="sxs-lookup"><span data-stu-id="9aced-131">Like buttons on Bot Framework cards, buttons on Adaptive Cards support two ways of invoking task modules, deep link URLs with `Action.openUrl` buttons, and `task/fetch` using `Action.Submit` buttons.</span></span> </li></ul> <br/><br/> <ul><li> <span data-ttu-id="9aced-132">Модули задач с адаптивными картами работают очень похоже на HTML или JavaScript.</span><span class="sxs-lookup"><span data-stu-id="9aced-132">Task modules with Adaptive Cards work very similarly to the HTML or JavaScript case.</span></span> <span data-ttu-id="9aced-133">Главное отличие состоит в том, что, поскольку при использовании адаптивных карт javaScript нет javaScript, звонить `tasks.submitTask()` нельзя.</span><span class="sxs-lookup"><span data-stu-id="9aced-133">The major difference is that since there is no JavaScript when you are using Adaptive Cards, there is no way to call `tasks.submitTask()`.</span></span> <span data-ttu-id="9aced-134">Вместо этого Teams принимает объект и возвращает его в качестве `data` `Action.Submit` полезной нагрузки `task/submit` события.</span><span class="sxs-lookup"><span data-stu-id="9aced-134">Instead, Teams takes the `data` object from `Action.Submit` and returns it as the payload of the `task/submit` event.</span></span> <span data-ttu-id="9aced-135">Дополнительные сведения см. [в дополнительных `task/submit` сведениях. ](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit)</span><span class="sxs-lookup"><span data-stu-id="9aced-135">For more information, see [flexibility of `task/submit`](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit).</span></span> </li></ul> |
| <span data-ttu-id="9aced-136">URL-адрес глубокой ссылки</span><span class="sxs-lookup"><span data-stu-id="9aced-136">Deep link URL</span></span> <br/>[<span data-ttu-id="9aced-137">синтаксис URL-адреса</span><span class="sxs-lookup"><span data-stu-id="9aced-137">URL syntax</span></span>](#task-module-deep-link-syntax) | <span data-ttu-id="9aced-138">1. Teams вызывает модуль задач, который является URL-адресом, который отображается внутри указанного в параметре `<iframe>` `url` глубокой ссылки.</span><span class="sxs-lookup"><span data-stu-id="9aced-138">1. Teams invokes the task module that is the URL that appears inside the `<iframe>` specified in the `url` parameter of the deep link.</span></span> <span data-ttu-id="9aced-139">Нет `submitHandler` вызова.</span><span class="sxs-lookup"><span data-stu-id="9aced-139">There is no `submitHandler` callback.</span></span> <br/><br/> <span data-ttu-id="9aced-140">2. В JavaScript страницы в модуле задач позвоните, чтобы закрыть его с объектом в качестве параметра, так же, как при вызове его с вкладки или кнопки карты `tasks.submitTask()` `result` бота.</span><span class="sxs-lookup"><span data-stu-id="9aced-140">2. Within the JavaScript of the page in the task module, call `tasks.submitTask()` to close it with a `result` object as a parameter, the same as when invoking it from a tab or a bot card button.</span></span> <span data-ttu-id="9aced-141">Однако логика завершения несколько отличается.</span><span class="sxs-lookup"><span data-stu-id="9aced-141">However, completion logic is slightly different.</span></span> <span data-ttu-id="9aced-142">Если логика завершения находится на клиенте, если бота нет, нет вызова, поэтому любая логика завершения должна быть в коде, предшествующего `submitHandler` `tasks.submitTask()` вызову.</span><span class="sxs-lookup"><span data-stu-id="9aced-142">If your completion logic resides on the client that is if there is no bot, there is no `submitHandler` callback, so any completion logic must be in the code preceding the call to `tasks.submitTask()`.</span></span> <span data-ttu-id="9aced-143">Ошибки вызовов сообщаются только через консоль.</span><span class="sxs-lookup"><span data-stu-id="9aced-143">Invocation errors are only reported through the console.</span></span> <span data-ttu-id="9aced-144">Если у вас есть бот, можно указать параметр в глубокой ссылке, чтобы `completionBotId` отправить `result` объект через `task/submit` событие.</span><span class="sxs-lookup"><span data-stu-id="9aced-144">If you have a bot, then you can specify a `completionBotId` parameter in the deep link to send the `result` object through a `task/submit` event.</span></span> | <span data-ttu-id="9aced-145">1. Teams вызывает модуль задач, который является телом карточки JSON адаптивной карты, заданным как url-кодированное значение параметра `card` глубокой ссылки.</span><span class="sxs-lookup"><span data-stu-id="9aced-145">1. Teams invokes the task module that is the JSON card body of the Adaptive Card that is specified as a URL-encoded value of the `card` parameter of the deep link.</span></span> <br/><br/> <span data-ttu-id="9aced-146">2. Пользователь закрывает модуль задач, выбрав X в правом верхнем справа от модуля задачи или нажав кнопку `Action.Submit` на карточке.</span><span class="sxs-lookup"><span data-stu-id="9aced-146">2. The user closes the task module by selecting the X at the upper right of the task module or by pressing an `Action.Submit` button on the card.</span></span> <span data-ttu-id="9aced-147">Так как нет вызова, у пользователя должен быть бот для отправки значения `submitHandler` полей адаптивной карты.</span><span class="sxs-lookup"><span data-stu-id="9aced-147">Since there is no `submitHandler` to call, the user must have a bot to send the value of the Adaptive Card fields.</span></span> <span data-ttu-id="9aced-148">Пользователь должен использовать параметр в глубокой ссылке, чтобы указать бота, чтобы отправить данные `completionBotId` с помощью `task/submit invoke` события.</span><span class="sxs-lookup"><span data-stu-id="9aced-148">The user must use the `completionBotId` parameter in the deep link to specify the bot to send the data to using a `task/submit invoke` event.</span></span> |

> [!NOTE]
> <span data-ttu-id="9aced-149">Призыв к модульу задач из JavaScript не поддерживается на мобильных устройствах.</span><span class="sxs-lookup"><span data-stu-id="9aced-149">Invoking a task module from JavaScript is not supported on mobile.</span></span>

<span data-ttu-id="9aced-150">В следующем разделе указывается объект, который определяет `TaskInfo` определенные атрибуты для модуля задач.</span><span class="sxs-lookup"><span data-stu-id="9aced-150">The next section specifies the `TaskInfo` object that defines certain attributes for a task module.</span></span>

## <a name="the-taskinfo-object"></a><span data-ttu-id="9aced-151">Объект TaskInfo</span><span class="sxs-lookup"><span data-stu-id="9aced-151">The TaskInfo object</span></span>

<span data-ttu-id="9aced-152">Объект `TaskInfo` содержит метаданные для модуля задач.</span><span class="sxs-lookup"><span data-stu-id="9aced-152">The `TaskInfo` object contains the metadata for a task module.</span></span> <span data-ttu-id="9aced-153">Определите `url` для встроенного iFrame или `card` адаптивной карты.</span><span class="sxs-lookup"><span data-stu-id="9aced-153">Define the `url` for an embedded iFrame or `card` for an Adaptive Card.</span></span> <span data-ttu-id="9aced-154">В следующей таблице содержится определение объекта:</span><span class="sxs-lookup"><span data-stu-id="9aced-154">The following table provides the object definition:</span></span>

| <span data-ttu-id="9aced-155">Атрибут</span><span class="sxs-lookup"><span data-stu-id="9aced-155">Attribute</span></span> | <span data-ttu-id="9aced-156">Тип</span><span class="sxs-lookup"><span data-stu-id="9aced-156">Type</span></span> | <span data-ttu-id="9aced-157">Описание</span><span class="sxs-lookup"><span data-stu-id="9aced-157">Description</span></span> |
| --- | --- | --- |
| `title` | <span data-ttu-id="9aced-158">string</span><span class="sxs-lookup"><span data-stu-id="9aced-158">string</span></span> | <span data-ttu-id="9aced-159">Этот атрибут отображается ниже имени приложения и справа от значка приложения.</span><span class="sxs-lookup"><span data-stu-id="9aced-159">This attribute appears below the app name and to the right of the app icon.</span></span> |
| `height` | <span data-ttu-id="9aced-160">number или string</span><span class="sxs-lookup"><span data-stu-id="9aced-160">number or string</span></span> | <span data-ttu-id="9aced-161">Этот атрибут может быть числом, представляющим высоту модуля задач в пикселях, или `small` , `medium` или `large` .</span><span class="sxs-lookup"><span data-stu-id="9aced-161">This attribute can be a number representing the task module's height in pixels, or `small`, `medium`, or `large`.</span></span> <span data-ttu-id="9aced-162">Дополнительные сведения см. [в деле размеров модуля задач.](#task-module-sizing)</span><span class="sxs-lookup"><span data-stu-id="9aced-162">For more information, see [task module sizing](#task-module-sizing).</span></span> |
| `width` | <span data-ttu-id="9aced-163">number или string</span><span class="sxs-lookup"><span data-stu-id="9aced-163">number or string</span></span> | <span data-ttu-id="9aced-164">Этот атрибут может быть числом, представляющим ширину модуля задач в пикселях, или `small` `medium` , или `large` .</span><span class="sxs-lookup"><span data-stu-id="9aced-164">This attribute can be a number representing the task module's width in pixels, or `small`, `medium`, or `large`.</span></span> <span data-ttu-id="9aced-165">Дополнительные сведения см. [в деле размеров модуля задач.](#task-module-sizing)</span><span class="sxs-lookup"><span data-stu-id="9aced-165">For more information, see [task module sizing](#task-module-sizing).</span></span> |
| `url` | <span data-ttu-id="9aced-166">string</span><span class="sxs-lookup"><span data-stu-id="9aced-166">string</span></span> | <span data-ttu-id="9aced-167">Этот атрибут — URL-адрес страницы, загружаемой в `<iframe>` модуль задач.</span><span class="sxs-lookup"><span data-stu-id="9aced-167">This attribute is the URL of the page loaded as an `<iframe>` inside the task module.</span></span> <span data-ttu-id="9aced-168">Домен URL-адреса должен быть в массиве [validDomains](~/resources/schema/manifest-schema.md#validdomains) приложения в манифесте приложения.</span><span class="sxs-lookup"><span data-stu-id="9aced-168">The URL's domain must be in the app's [validDomains array](~/resources/schema/manifest-schema.md#validdomains) in your app's manifest.</span></span> |
| `card` | <span data-ttu-id="9aced-169">Адаптивная карта или вложение бота адаптивной карты</span><span class="sxs-lookup"><span data-stu-id="9aced-169">Adaptive Card or Adaptive Card bot card attachment</span></span> | <span data-ttu-id="9aced-170">Этот атрибут — JSON для адаптивной карты, которая появится в модуле задач.</span><span class="sxs-lookup"><span data-stu-id="9aced-170">This attribute is the JSON for the Adaptive Card to appear in the task module.</span></span> <span data-ttu-id="9aced-171">Если пользователь отзовется от бота, используйте адаптивную карту JSON в объекте Bot `attachment` Framework.</span><span class="sxs-lookup"><span data-stu-id="9aced-171">If the user is invoking from a bot, use the Adaptive Card JSON in a Bot Framework `attachment` object.</span></span> <span data-ttu-id="9aced-172">На вкладке пользователь должен использовать адаптивную карту.</span><span class="sxs-lookup"><span data-stu-id="9aced-172">From a tab, the user must use an Adaptive Card.</span></span> <span data-ttu-id="9aced-173">Дополнительные сведения см. в [вложении в бот-карту Adaptive Card или Adaptive Card.](#adaptive-card-or-adaptive-card-bot-card-attachment)</span><span class="sxs-lookup"><span data-stu-id="9aced-173">For more information, see [Adaptive Card or Adaptive Card bot card attachment](#adaptive-card-or-adaptive-card-bot-card-attachment)</span></span> |
| `fallbackUrl` | <span data-ttu-id="9aced-174">string</span><span class="sxs-lookup"><span data-stu-id="9aced-174">string</span></span> | <span data-ttu-id="9aced-175">Этот атрибут открывает URL-адрес на вкладке браузера, если клиент не поддерживает функцию модуля задач.</span><span class="sxs-lookup"><span data-stu-id="9aced-175">This attribute opens the URL in a browser tab, if a client does not support the task module feature.</span></span> |
| `completionBotId` | <span data-ttu-id="9aced-176">string</span><span class="sxs-lookup"><span data-stu-id="9aced-176">string</span></span> | <span data-ttu-id="9aced-177">Этот атрибут указывает бот-ID приложения для отправки результатов взаимодействия пользователя с модулем задач.</span><span class="sxs-lookup"><span data-stu-id="9aced-177">This attribute specifies a bot App ID to send the result of the user's interaction with the task module.</span></span> <span data-ttu-id="9aced-178">Если указано, бот получает событие с объектом `task/submit invoke` JSON в полезной нагрузке события.</span><span class="sxs-lookup"><span data-stu-id="9aced-178">If specified, the bot receives a `task/submit invoke` event with a JSON object in the event payload.</span></span> |

> [!NOTE]
> <span data-ttu-id="9aced-179">Функция модуля задач требует, чтобы домены всех URL-адресов, которые необходимо загрузить, были включены в массив `validDomains` манифеста приложения.</span><span class="sxs-lookup"><span data-stu-id="9aced-179">The task module feature requires that the domains of any URLs you want to load are included in the `validDomains` array in your app's manifest.</span></span>

<span data-ttu-id="9aced-180">В следующем разделе указывается размер модуля задач, который позволяет пользователю устанавливать высоту и ширину модуля задач.</span><span class="sxs-lookup"><span data-stu-id="9aced-180">The next section specifies task module sizing that enables the user to set the height and width of the task module.</span></span>

## <a name="task-module-sizing"></a><span data-ttu-id="9aced-181">Размер модуля задач</span><span class="sxs-lookup"><span data-stu-id="9aced-181">Task module sizing</span></span>

<span data-ttu-id="9aced-182">Использование целого набора для и , задает высоту и ширину модуля `TaskInfo.width` `TaskInfo.height` задач в пикселях.</span><span class="sxs-lookup"><span data-stu-id="9aced-182">Using integers for `TaskInfo.width` and `TaskInfo.height`, sets the height and width of the task module in pixels.</span></span> <span data-ttu-id="9aced-183">Однако в зависимости от размера окна и разрешения экрана команды они уменьшаются пропорционально при сохранении соотношения аспектов шириной или высотой.</span><span class="sxs-lookup"><span data-stu-id="9aced-183">However, depending on the size of the Team's window and screen resolution they are reduced proportionally while maintaining the aspect ratio that is width or height.</span></span>

<span data-ttu-id="9aced-184">Если и являются , или , размер красного прямоугольника в следующем изображении является частью доступного `TaskInfo.width` `TaskInfo.height` `"small"` `"medium"` `"large"` пространства, 20%, 50%, и 60% для `width` и 20%, 50%, и 66% для `height` :</span><span class="sxs-lookup"><span data-stu-id="9aced-184">If `TaskInfo.width` and `TaskInfo.height` are `"small"`, `"medium"`, or `"large"`, the size of the red rectangle in the following image is a proportion of the available space, 20%, 50%, and 60% for `width` and 20%, 50%, and 66% for `height`:</span></span>

![Пример модуля задач](~/assets/images/task-module/task-module-example.png)

<span data-ttu-id="9aced-186">Модули задач, вызываемые со вкладки, можно динамически реамизировать.</span><span class="sxs-lookup"><span data-stu-id="9aced-186">Task modules invoked from a tab can be dynamically resized.</span></span> <span data-ttu-id="9aced-187">После вызова можно вызвать, где свойства высоты и ширины объекта `tasks.startTask()` `tasks.updateTask(newSize)` newSize соответствуют спецификации TaskInfo, например `{ height: 'medium', width: 'medium' }` .</span><span class="sxs-lookup"><span data-stu-id="9aced-187">After calling `tasks.startTask()` you can call `tasks.updateTask(newSize)` where height and width properties on the newSize object conform to the TaskInfo specification, for example `{ height: 'medium', width: 'medium' }`.</span></span>

<span data-ttu-id="9aced-188">В следующем разделе приводится пример встраив модулей задач в видео YouTube и PowerApp.</span><span class="sxs-lookup"><span data-stu-id="9aced-188">The next section provides examples of embedding task modules in a YouTube video and a PowerApp.</span></span>

## <a name="task-module-css-for-html-or-javascript-task-modules"></a><span data-ttu-id="9aced-189">Модуль задач CSS для модулей задач HTML или JavaScript</span><span class="sxs-lookup"><span data-stu-id="9aced-189">Task module CSS for HTML or JavaScript task modules</span></span>

<span data-ttu-id="9aced-190">Модули задач на основе HTML или JavaScript имеют доступ ко всей области модуля задач ниже заголовка.</span><span class="sxs-lookup"><span data-stu-id="9aced-190">HTML or JavaScript-based task modules have access to the entire area of the task module below the header.</span></span> <span data-ttu-id="9aced-191">Хотя это обеспечивает большую гибкость, если вы хотите, чтобы обивка по краям совпадала с элементами заголовки и избегала ненужных свитков, пользователь должен предоставить правильный CSS.</span><span class="sxs-lookup"><span data-stu-id="9aced-191">While that offers a great deal of flexibility, if you want padding around the edges to align with the header elements and avoid unnecessary scroll bars, the user must provide the right CSS.</span></span> <span data-ttu-id="9aced-192">В следующих разделах вы можете привести несколько примеров для нескольких примеров использования.</span><span class="sxs-lookup"><span data-stu-id="9aced-192">The next sections provide some examples for a few use cases.</span></span>

<span data-ttu-id="9aced-193">**Пример 1. Видео На YouTube**</span><span class="sxs-lookup"><span data-stu-id="9aced-193">**Example 1: YouTube video**</span></span>

<span data-ttu-id="9aced-194">YouTube предлагает возможность встраить видео на веб-страницах.</span><span class="sxs-lookup"><span data-stu-id="9aced-194">YouTube offers the ability to embed videos on web pages.</span></span> <span data-ttu-id="9aced-195">Легко встраить видео на веб-страницах в модуль задач с помощью простой веб-страницы забоя.</span><span class="sxs-lookup"><span data-stu-id="9aced-195">It is easy to embed videos on web pages in a task module using a simple stub web page.</span></span>

![Видео YouTube](~/assets/images/task-module/youtube-example.png)

<span data-ttu-id="9aced-197">В следующем коде приводится пример HTML для веб-страницы без CSS:</span><span class="sxs-lookup"><span data-stu-id="9aced-197">The following code provides an example of the HTML for the web page without the CSS:</span></span>

```html
<!DOCTYPE html>
<html lang="en">
<head>
  ⋮
</head>
<body>
  <div id="embed-container">
    <iframe width="1000" height="700" src="https://www.youtube.com/embed/rd0Rd8w3FZ0" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen=""></iframe>
  </div>
</body>
</html>
```

<span data-ttu-id="9aced-198">В следующем коде приводится пример CSS:</span><span class="sxs-lookup"><span data-stu-id="9aced-198">The following code provides an example of the CSS:</span></span>

```css
#embed-container iframe {
    position: absolute;
    top: 0;
    left: 0;
    width: 95%;
    height: 95%;
    padding-left: 20px;
    padding-right: 20px;
    padding-top: 10px;
    padding-bottom: 10px;
    border-style: none;
}
```

<span data-ttu-id="9aced-199">**Пример 2. PowerApp**</span><span class="sxs-lookup"><span data-stu-id="9aced-199">**Example 2: PowerApp**</span></span>

<span data-ttu-id="9aced-200">Для встраить PowerApp пользователь может использовать тот же подход.</span><span class="sxs-lookup"><span data-stu-id="9aced-200">The user can use the same approach to embed a PowerApp as well.</span></span> <span data-ttu-id="9aced-201">Поскольку высота или ширина любого отдельного PowerApp настраиваются, пользователь может настроить высоту и ширину для достижения нужной презентации.</span><span class="sxs-lookup"><span data-stu-id="9aced-201">As the height or width of any individual PowerApp is customizable, the user can adjust the height and width to achieve the desired presentation.</span></span>

![PowerApp управления активами](~/assets/images/task-module/powerapp-example.png)

<span data-ttu-id="9aced-203">В следующем коде приводится пример HTML для PowerApp:</span><span class="sxs-lookup"><span data-stu-id="9aced-203">The following code provides an example of the HTML for PowerApp:</span></span>

```html
<iframe width="720" height="520" src="https://web.powerapps.com/webplayer/iframeapp?source=iframe&screenColor=rgba(104,101,171,1)&appId=/providers/Microsoft.PowerApps/apps/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"></iframe>
```

<span data-ttu-id="9aced-204">В следующем коде приводится пример CSS:</span><span class="sxs-lookup"><span data-stu-id="9aced-204">The following code provides an example of the CSS:</span></span>

```css
#embed-container iframe {
    position: absolute;
    top: 0;
    left: 0;
    width: 94%;
    height: 95%;
    padding-left: 20px;
    padding-right: 20px;
    padding-top: 10px;
    padding-bottom: 10px;
    border-style: none;
}
```

<span data-ttu-id="9aced-205">В следующем разделе приводится подробная информация об отзове вашей карты с помощью адаптивной карты или вложения бот-карты адаптивной карты.</span><span class="sxs-lookup"><span data-stu-id="9aced-205">The next section provides details on invoking your card using Adaptive Card or Adaptive Card bot card attachment.</span></span>

## <a name="adaptive-card-or-adaptive-card-bot-card-attachment"></a><span data-ttu-id="9aced-206">Адаптивная карта или вложение бота адаптивной карты</span><span class="sxs-lookup"><span data-stu-id="9aced-206">Adaptive Card or Adaptive Card bot card attachment</span></span>

<span data-ttu-id="9aced-207">В зависимости от того, как вы назовете, необходимо использовать адаптивную карту или вложение бота адаптивной карты, которая является адаптивной картой, завернутой в объект `card` вложения.</span><span class="sxs-lookup"><span data-stu-id="9aced-207">Depending on how you are invoking your `card`, you must use either an Adaptive Card or an Adaptive Card bot card attachment, which is an Adaptive Card wrapped in an attachment object.</span></span>

<span data-ttu-id="9aced-208">При наводке со вкладки пользователю необходимо использовать адаптивную карту.</span><span class="sxs-lookup"><span data-stu-id="9aced-208">When you are invoking from a tab, the user must use an Adaptive Card.</span></span>

<span data-ttu-id="9aced-209">В следующем коде приводится пример адаптивной карты:</span><span class="sxs-lookup"><span data-stu-id="9aced-209">The following code provides an example of an Adaptive Card:</span></span>

```json
{
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
}
```

<span data-ttu-id="9aced-210">В следующем коде приводится пример вложения бот-карты адаптивной карты при наложении от бота:</span><span class="sxs-lookup"><span data-stu-id="9aced-210">The following code provides an example of an Adaptive Card bot card attachment when you are invoking from a bot:</span></span>

```json
{
    "contentType": "application/vnd.microsoft.card.adaptive",
    "content": {
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
    }
}
```

<span data-ttu-id="9aced-211">В следующем разделе приводится подробная информация о синтаксисе глубокой ссылки модуля задач, включая `TaskInfo` объект и `APP_ID` `BOT_APP_ID` .</span><span class="sxs-lookup"><span data-stu-id="9aced-211">The next section provides details on task module deep link syntax including the `TaskInfo` object and `APP_ID` and `BOT_APP_ID`.</span></span>

## <a name="task-module-deep-link-syntax"></a><span data-ttu-id="9aced-212">Синтаксис глубокой ссылки модуля задач</span><span class="sxs-lookup"><span data-stu-id="9aced-212">Task module deep link syntax</span></span>

<span data-ttu-id="9aced-213">Глубокая ссылка модуля задач — это сериализация объекта TaskInfo со следующими двумя другими деталями и необязательно `APP_ID` `BOT_APP_ID` :</span><span class="sxs-lookup"><span data-stu-id="9aced-213">A task module deep link is a serialization of the TaskInfo object with the following two other details, `APP_ID` and optionally the `BOT_APP_ID`:</span></span>

`https://teams.microsoft.com/l/task/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

`https://teams.microsoft.com/l/task/APP_ID?card=<TaskInfo.card>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

<span data-ttu-id="9aced-214">Для типов данных и допустимых значений `<TaskInfo.url>` для , , , и , `<TaskInfo.card>` `<TaskInfo.height>` `<TaskInfo.width>` `<TaskInfo.title>` [см. объект TaskInfo](#the-taskinfo-object).</span><span class="sxs-lookup"><span data-stu-id="9aced-214">For the data types and allowable values for `<TaskInfo.url>`, `<TaskInfo.card>`, `<TaskInfo.height>`, `<TaskInfo.width>`, and `<TaskInfo.title>`, see [TaskInfo object](#the-taskinfo-object).</span></span>

> [!TIP]
> <span data-ttu-id="9aced-215">URL-адрес кодирует глубокую ссылку при использовании `card` параметра, например [ `encodeURI()` ](https://www.w3schools.com/jsref/jsref_encodeURI.asp)функции JavaScript.</span><span class="sxs-lookup"><span data-stu-id="9aced-215">URL encode the deep link when using the `card` parameter, for example, JavaScript's [`encodeURI()` function](https://www.w3schools.com/jsref/jsref_encodeURI.asp).</span></span>

<span data-ttu-id="9aced-216">В следующей таблице приводится информация о `APP_ID` `BOT_APP_ID` и:</span><span class="sxs-lookup"><span data-stu-id="9aced-216">The following table provides information on `APP_ID` and `BOT_APP_ID`:</span></span>

| <span data-ttu-id="9aced-217">Значение</span><span class="sxs-lookup"><span data-stu-id="9aced-217">Value</span></span> | <span data-ttu-id="9aced-218">Тип</span><span class="sxs-lookup"><span data-stu-id="9aced-218">Type</span></span> | <span data-ttu-id="9aced-219">Обязательный</span><span class="sxs-lookup"><span data-stu-id="9aced-219">Required</span></span> | <span data-ttu-id="9aced-220">Описание</span><span class="sxs-lookup"><span data-stu-id="9aced-220">Description</span></span> |
| --- | --- | --- | --- |
| `APP_ID` | <span data-ttu-id="9aced-221">string</span><span class="sxs-lookup"><span data-stu-id="9aced-221">string</span></span> | <span data-ttu-id="9aced-222">Да</span><span class="sxs-lookup"><span data-stu-id="9aced-222">Yes</span></span> | <span data-ttu-id="9aced-223">ID [приложения,](~/resources/schema/manifest-schema.md#id) выдавлив модуль задач.</span><span class="sxs-lookup"><span data-stu-id="9aced-223">The [ID](~/resources/schema/manifest-schema.md#id) of the app invoking the task module.</span></span> <span data-ttu-id="9aced-224">Массив [validDomains в](~/resources/schema/manifest-schema.md#validdomains) манифесте для должен содержать домен, если `APP_ID` находится в `url` `url` URL-адресе.</span><span class="sxs-lookup"><span data-stu-id="9aced-224">The [validDomains array](~/resources/schema/manifest-schema.md#validdomains) in the manifest for `APP_ID` must contain the domain for `url` if `url` is in the URL.</span></span> <span data-ttu-id="9aced-225">ID приложения уже известен, когда модуль задач вызывается со вкладки или бота, поэтому он не включен `TaskInfo` в .</span><span class="sxs-lookup"><span data-stu-id="9aced-225">The app ID is already known when a task module is invoked from a tab or a bot, which is why it is not included in `TaskInfo`.</span></span> |
| `BOT_APP_ID` | <span data-ttu-id="9aced-226">string</span><span class="sxs-lookup"><span data-stu-id="9aced-226">string</span></span> | <span data-ttu-id="9aced-227">Нет</span><span class="sxs-lookup"><span data-stu-id="9aced-227">No</span></span> | <span data-ttu-id="9aced-228">Если задано значение, объект отправляется с `completionBotId` `result` помощью сообщения `task/submit invoke` указанному боту.</span><span class="sxs-lookup"><span data-stu-id="9aced-228">If a value for `completionBotId` is specified, the `result` object is sent using a `task/submit invoke` message to the specified bot.</span></span> <span data-ttu-id="9aced-229">`BOT_APP_ID` должно быть указано как бот в манифесте приложения, то есть вы не можете отправить его любому боту.</span><span class="sxs-lookup"><span data-stu-id="9aced-229">`BOT_APP_ID` must be specified as a bot in the app's manifest, that is you cannot send it to any bot.</span></span> |

> [!NOTE]
> <span data-ttu-id="9aced-230">`APP_ID` и может быть одинаковым во многих случаях, если у приложения есть рекомендуемый бот для использования в качестве `BOT_APP_ID` ID приложения, если он есть.</span><span class="sxs-lookup"><span data-stu-id="9aced-230">`APP_ID` and `BOT_APP_ID` can be the same in many cases, if an app has a recommended bot to use as an app's ID if there is one.</span></span>

<span data-ttu-id="9aced-231">В следующем разделе приводится подробная информация об использовании клавиатуры с модулем задач вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="9aced-231">The next section provides details on using a keyboard with your app's task module.</span></span>

## <a name="keyboard-and-accessibility-guidelines"></a><span data-ttu-id="9aced-232">Рекомендации по клавиатуре и доступности</span><span class="sxs-lookup"><span data-stu-id="9aced-232">Keyboard and accessibility guidelines</span></span>

<span data-ttu-id="9aced-233">С помощью модулей задач на основе HTML или JavaScript необходимо убедиться, что модуль задач вашего приложения можно использовать с помощью клавиатуры.</span><span class="sxs-lookup"><span data-stu-id="9aced-233">With HTML or JavaScript-based task modules, you must ensure your app's task module can be used with a keyboard.</span></span> <span data-ttu-id="9aced-234">Программы чтения с экрана также зависят от возможности навигации с помощью клавиатуры.</span><span class="sxs-lookup"><span data-stu-id="9aced-234">Screen reader programs also depend on the ability to navigate using the keyboard.</span></span> <span data-ttu-id="9aced-235">Это включает в себя следующие две вещи:</span><span class="sxs-lookup"><span data-stu-id="9aced-235">This includes the following two things:</span></span>

* <span data-ttu-id="9aced-236">Использование [атрибута tabindex в](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/tabindex) тегах HTML для управления элементами, которые могут быть сфокусированы.</span><span class="sxs-lookup"><span data-stu-id="9aced-236">Using the [tabindex attribute](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/tabindex) in your HTML tags to control which elements can be focused.</span></span> <span data-ttu-id="9aced-237">Кроме того, используйте атрибут tabindex, чтобы определить, где он участвует в последовательной навигации клавиатуры обычно с <kbd>клавишами Tab</kbd> и <kbd>Shift-Tab.</kbd></span><span class="sxs-lookup"><span data-stu-id="9aced-237">Also, use tabindex attribute to identify where it participates in sequential keyboard navigation usually with the <kbd>Tab</kbd> and <kbd>Shift-Tab</kbd> keys.</span></span>
* <span data-ttu-id="9aced-238">Обработка <kbd>ключа Esc</kbd> в JavaScript для модуля задач.</span><span class="sxs-lookup"><span data-stu-id="9aced-238">Handling the <kbd>Esc</kbd> key in the JavaScript for your task module.</span></span> <span data-ttu-id="9aced-239">В следующем коде приводится пример обработки ключа <kbd>Esc:</kbd></span><span class="sxs-lookup"><span data-stu-id="9aced-239">The following code provides an example of how to handle the <kbd>Esc</kbd> key:</span></span>

    ```javascript
    // Handle the Esc key
    document.onkeyup = function(event) {
    if ((event.key === 27) || (event.key === "Escape")) {
      microsoftTeams.submitTask(null); // this will return an err object to the completionHandler()
      }
    }
    ```

<span data-ttu-id="9aced-240">Microsoft Teams обеспечивает правильную работу навигации по клавиатуре из заголовка модуля задач в HTML и наоборот.</span><span class="sxs-lookup"><span data-stu-id="9aced-240">Microsoft Teams ensures that keyboard navigation works properly from the task module header into your HTML and vice-versa.</span></span>

## <a name="code-sample"></a><span data-ttu-id="9aced-241">Пример кода</span><span class="sxs-lookup"><span data-stu-id="9aced-241">Code sample</span></span>

|<span data-ttu-id="9aced-242">Пример имени</span><span class="sxs-lookup"><span data-stu-id="9aced-242">Sample name</span></span> | <span data-ttu-id="9aced-243">Description</span><span class="sxs-lookup"><span data-stu-id="9aced-243">Description</span></span> | <span data-ttu-id="9aced-244">.NET</span><span class="sxs-lookup"><span data-stu-id="9aced-244">.NET</span></span> | <span data-ttu-id="9aced-245">Node.js</span><span class="sxs-lookup"><span data-stu-id="9aced-245">Node.js</span></span>|
|----------------|-----------------|--------------|----------------|
|<span data-ttu-id="9aced-246">Пример модуля задач bots-V4</span><span class="sxs-lookup"><span data-stu-id="9aced-246">Task module sample bots-V4</span></span> | <span data-ttu-id="9aced-247">Примеры для создания модулей задач.</span><span class="sxs-lookup"><span data-stu-id="9aced-247">Samples for creating task modules.</span></span> |[<span data-ttu-id="9aced-248">View</span><span class="sxs-lookup"><span data-stu-id="9aced-248">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/54.teams-task-module)|[<span data-ttu-id="9aced-249">View</span><span class="sxs-lookup"><span data-stu-id="9aced-249">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/54.teams-task-module)|
|<span data-ttu-id="9aced-250">Пример вкладок модуля задач и ботов-V3</span><span class="sxs-lookup"><span data-stu-id="9aced-250">Task module sample tabs and bots-V3</span></span> | <span data-ttu-id="9aced-251">Примеры для создания модулей задач.</span><span class="sxs-lookup"><span data-stu-id="9aced-251">Samples for creating task modules.</span></span> |[<span data-ttu-id="9aced-252">View</span><span class="sxs-lookup"><span data-stu-id="9aced-252">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/csharp)|[<span data-ttu-id="9aced-253">View</span><span class="sxs-lookup"><span data-stu-id="9aced-253">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/nodejs)| 

## <a name="see-also"></a><span data-ttu-id="9aced-254">См. также</span><span class="sxs-lookup"><span data-stu-id="9aced-254">See also</span></span>

* [<span data-ttu-id="9aced-255">Запрос разрешений устройства</span><span class="sxs-lookup"><span data-stu-id="9aced-255">Request device permissions</span></span>](~/concepts/device-capabilities/native-device-permissions.md)
* [<span data-ttu-id="9aced-256">Интеграция возможностей мультимедиа</span><span class="sxs-lookup"><span data-stu-id="9aced-256">Integrate media capabilities</span></span>](~/concepts/device-capabilities/mobile-camera-image-permissions.md)
* [<span data-ttu-id="9aced-257">Интеграция возможностей сканера QR или штрихкодов в Teams</span><span class="sxs-lookup"><span data-stu-id="9aced-257">Integrate QR or barcode scanner capability in Teams</span></span>](~/concepts/device-capabilities/qr-barcode-scanner-capability.md)
* [<span data-ttu-id="9aced-258">Интеграция возможностей расположения в Teams</span><span class="sxs-lookup"><span data-stu-id="9aced-258">Integrate location capabilities in Teams</span></span>](~/concepts/device-capabilities/location-capability.md)

## <a name="next-step"></a><span data-ttu-id="9aced-259">Следующий этап</span><span class="sxs-lookup"><span data-stu-id="9aced-259">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9aced-260">Использование модулей задач на вкладке</span><span class="sxs-lookup"><span data-stu-id="9aced-260">Use task modules in tabs</span></span>](~/task-modules-and-cards/task-modules/task-modules-tabs.md)