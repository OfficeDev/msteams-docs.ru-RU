---
title: Определение команд действий для расширения обмена сообщениями
author: clearab
description: Обзор расширений обмена сообщениями на платформе Microsoft Teams
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 7eb734258aa34c69fa34d1413b2d3dab88e0113a
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675227"
---
# <a name="define-messaging-extension-action-commands"></a><span data-ttu-id="d9df0-103">Определение команд действий для расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="d9df0-103">Define messaging extension action commands</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="d9df0-104">Команды действий позволяют предоставить пользователям модальное всплывающее окно (называемое модулем задач в Teams) для сбора и отображения информации, а затем обработки их взаимодействия и отправки информации обратно в Teams.</span><span class="sxs-lookup"><span data-stu-id="d9df0-104">Action commands allow you present your users with a modal popup (called a task module in Teams) to collect or display information, then process their interaction and send information back to Teams.</span></span> <span data-ttu-id="d9df0-105">Прежде чем приступать к созданию команды, необходимо принять решение:</span><span class="sxs-lookup"><span data-stu-id="d9df0-105">Before creating your command you'll need to decide:</span></span>

1. <span data-ttu-id="d9df0-106">Откуда можно запустить команду действия?</span><span class="sxs-lookup"><span data-stu-id="d9df0-106">Where can the action command be triggered from?</span></span>
1. <span data-ttu-id="d9df0-107">Как будет создаваться модуль задач?</span><span class="sxs-lookup"><span data-stu-id="d9df0-107">How will the task module be created?</span></span>
1. <span data-ttu-id="d9df0-108">Будет ли Последнее сообщение или карточка отправляться каналу из ленты, или сообщение или карточка будут вставлены в область сообщений для отправки пользователю?</span><span class="sxs-lookup"><span data-stu-id="d9df0-108">Will the final message or card be sent to the channel from a bot, or will the message or card be inserted into the compose message area for the user to submit?</span></span>

## <a name="choose-action-command-invoke-locations"></a><span data-ttu-id="d9df0-109">Выбор мест вызова команды действия</span><span class="sxs-lookup"><span data-stu-id="d9df0-109">Choose action command invoke locations</span></span>

<span data-ttu-id="d9df0-110">В первую очередь необходимо выбрать, где можно запустить команду действия (или более конкретную, *вызвать*ее) из.</span><span class="sxs-lookup"><span data-stu-id="d9df0-110">The first thing you need to decide is where your action command can be triggered (or more specifically, *invoked*) from.</span></span> <span data-ttu-id="d9df0-111">Указав параметр `context` в манифесте приложения, вы можете вызвать команду из одного или нескольких из следующих расположений:</span><span class="sxs-lookup"><span data-stu-id="d9df0-111">By specifying the `context` in your app manifest, your command can be invoked from one or more of the following locations:</span></span>

* <span data-ttu-id="d9df0-112">Кнопки в нижней части области "Создание сообщения".</span><span class="sxs-lookup"><span data-stu-id="d9df0-112">The buttons at the bottom of the compose message area.</span></span>
* <span data-ttu-id="d9df0-113">@Mentioning ваше приложение в поле команда.</span><span class="sxs-lookup"><span data-stu-id="d9df0-113">By @mentioning your app in the command box.</span></span> <span data-ttu-id="d9df0-114">Note: невозможно ответить с сообщением Bot, вставленным непосредственно в беседу, если ваше расширение обмена сообщениями вызвано из командной поля.</span><span class="sxs-lookup"><span data-stu-id="d9df0-114">Note: You cannot respond with a bot message inserted directly into the conversation if your messaging extension is invoked from the command box.</span></span>
* <span data-ttu-id="d9df0-115">Непосредственно из существующего сообщения с помощью... меню переполнения сообщения.</span><span class="sxs-lookup"><span data-stu-id="d9df0-115">Directly from an existing message via the ... overflow menu on a message.</span></span> <span data-ttu-id="d9df0-116">Note: начальный вызов почтового робота будет содержать объект JSON, содержащий сообщение, из которого оно было вызвано, которое можно обработать перед представлением в модуле задачи.</span><span class="sxs-lookup"><span data-stu-id="d9df0-116">Note: The initial invoke to your bot will include a JSON object containing the message from which it was invoked, which you can process before presenting them with a task module.</span></span>

## <a name="choose-how-to-build-your-task-module"></a><span data-ttu-id="d9df0-117">Выбор способа построения модуля задач</span><span class="sxs-lookup"><span data-stu-id="d9df0-117">Choose how to build your task module</span></span>

<span data-ttu-id="d9df0-118">В дополнение к выбору того, откуда может вызываться команда, необходимо также выбрать способ заполнения формы в модуле задач для пользователей.</span><span class="sxs-lookup"><span data-stu-id="d9df0-118">In addition to choosing where your command can be invoked from, you must also chose how to populate the form in the task module for your users.</span></span> <span data-ttu-id="d9df0-119">Существует три варианта создания формы, отображаемой в модуле задачи:</span><span class="sxs-lookup"><span data-stu-id="d9df0-119">You have three options for creating the form that is rendered inside the task module:</span></span>

* <span data-ttu-id="d9df0-120">**Статический список параметров** — это самый простой вариант.</span><span class="sxs-lookup"><span data-stu-id="d9df0-120">**Static list of parameters** - This is the simplest option.</span></span> <span data-ttu-id="d9df0-121">Вы можете определить список параметров (полей ввода) в манифесте приложения, который будет отображаться клиентом Teams.</span><span class="sxs-lookup"><span data-stu-id="d9df0-121">You can define a list of parameters (input fields) in your app manifest the Teams client will render.</span></span> <span data-ttu-id="d9df0-122">Вы не можете управлять форматированием с помощью этого параметра.</span><span class="sxs-lookup"><span data-stu-id="d9df0-122">You cannot control the formatting with this option.</span></span>
* <span data-ttu-id="d9df0-123">**Адаптивная карта** — вы можете выбрать использование адаптивной карточки, которая обеспечивает больший контроль над пользовательским интерфейсом, но по-прежнему ограничит доступ к доступным элементам управления и параметрам форматирования.</span><span class="sxs-lookup"><span data-stu-id="d9df0-123">**Adaptive card** - You can choose to use an adaptive card, which provides greater control over the UI, but still limits you on the available controls and formatting options.</span></span>
* <span data-ttu-id="d9df0-124">**Встроенное представление веб-сайта** — если вам требуется полный контроль над пользовательским интерфейсом и элементами управления, можно выбрать внедрение настраиваемого веб-представления в модуль задачи.</span><span class="sxs-lookup"><span data-stu-id="d9df0-124">**Embedded web view** - If you need complete control over the UI and controls, you can choose to embed a custom web view in the task module.</span></span>

<span data-ttu-id="d9df0-125">Если вы решили создать модуль задач со статическим списком параметров, первый вызов расширения системы обмена сообщениями будет выполняться, когда пользователь отправит модуль задачи.</span><span class="sxs-lookup"><span data-stu-id="d9df0-125">If you choose to create your task module with a static list of parameters, the first call to your messaging extension will be when a user submits the task module.</span></span> <span data-ttu-id="d9df0-126">При использовании встроенного веб-представления или адаптивной карточки ваше расширение системы обмена сообщениями должно обрабатывать начальное событие Invoke от пользователя, создавать модуль задач и возвращать его обратно клиенту.</span><span class="sxs-lookup"><span data-stu-id="d9df0-126">When using an embedded web view or an adaptive card, your messaging extension will need to handle an initial invoke event from the user, create the task module, and return it back to the client.</span></span>

## <a name="choose-how-the-final-message-will-be-sent"></a><span data-ttu-id="d9df0-127">Выбор способа отправки итогового сообщения</span><span class="sxs-lookup"><span data-stu-id="d9df0-127">Choose how the final message will be sent</span></span>

<span data-ttu-id="d9df0-128">В большинстве случаев команда действия приведет к вставке карточки в окно сообщения создать.</span><span class="sxs-lookup"><span data-stu-id="d9df0-128">In most cases, your action command will result in a card inserted into the compose message box.</span></span> <span data-ttu-id="d9df0-129">Пользователь может принять решение отправить его в канал или чат.</span><span class="sxs-lookup"><span data-stu-id="d9df0-129">Your user can then decide to send it into the channel or chat.</span></span> <span data-ttu-id="d9df0-130">Сообщение в этом случае поступает от пользователя, и у вас не будет возможность изменить открытку или изменить ее.</span><span class="sxs-lookup"><span data-stu-id="d9df0-130">The message in this case comes from the user, and your bot will not be able to edit or update the card further.</span></span>

<span data-ttu-id="d9df0-131">Если расширение системы обмена сообщениями запускается из поля создать или напрямую из сообщения, веб-служба может вставить конечный ответ непосредственно в канал или чат.</span><span class="sxs-lookup"><span data-stu-id="d9df0-131">If your messaging extension is triggered from the compose box or directly from a message, your web service can insert the final response directly into the channel or chat.</span></span> <span data-ttu-id="d9df0-132">В этом случае Адаптивная карта поступает от Bot, а Bot может обновляться, и при необходимости она также может отвечать на поток бесед.</span><span class="sxs-lookup"><span data-stu-id="d9df0-132">In this case, the adaptive card comes from the bot, the bot will be able to update it, and can the bot can also reply to the conversation thread if needed.</span></span> <span data-ttu-id="d9df0-133">Вам потребуется добавить `bot` объект в манифест приложения с помощью того же идентификатора и определить соответствующие области.</span><span class="sxs-lookup"><span data-stu-id="d9df0-133">You will need to add the `bot` object to your app manifest using the same Id and defining the appropriate scopes.</span></span>

## <a name="add-the-command-to-your-app-manifest"></a><span data-ttu-id="d9df0-134">Добавление команды в манифест приложения</span><span class="sxs-lookup"><span data-stu-id="d9df0-134">Add the command to your app manifest</span></span>

<span data-ttu-id="d9df0-135">Теперь, когда вы решили, как пользователи будут взаимодействовать с командой действия, необходимо добавить его в манифест приложения.</span><span class="sxs-lookup"><span data-stu-id="d9df0-135">Now that you've decided how users will interact with your action command, it is time to add it to your app manifest.</span></span> <span data-ttu-id="d9df0-136">Чтобы сделать это, добавьте новый `composeExtension` объект на верхний уровень манифеста приложения JSON.</span><span class="sxs-lookup"><span data-stu-id="d9df0-136">To do this you'll add a new `composeExtension` object to the top level of your app manifest JSON.</span></span> <span data-ttu-id="d9df0-137">Это можно сделать с помощью App Studio или вручную.</span><span class="sxs-lookup"><span data-stu-id="d9df0-137">You can either do so with the help of App Studio, or manually.</span></span>

### <a name="create-a-command-using-app-studio"></a><span data-ttu-id="d9df0-138">Создание команды с помощью App Studio</span><span class="sxs-lookup"><span data-stu-id="d9df0-138">Create a command using App Studio</span></span>

<span data-ttu-id="d9df0-139">В следующих действиях предполагается, что вы уже [создали расширение системы обмена сообщениями](~/messaging-extensions/how-to/create-messaging-extension.md).</span><span class="sxs-lookup"><span data-stu-id="d9df0-139">The following steps assume you've already [created a messaging extension](~/messaging-extensions/how-to/create-messaging-extension.md).</span></span>

1. <span data-ttu-id="d9df0-140">В клиенте Microsoft Teams откройте **app Studio** и выберите вкладку **редактор манифестов** .</span><span class="sxs-lookup"><span data-stu-id="d9df0-140">From the Microsoft Teams client, open **App Studio** and select the **Manifest Editor** tab.</span></span>
2. <span data-ttu-id="d9df0-141">Если вы уже создали пакет приложения в App Studio, выберите его из списка.</span><span class="sxs-lookup"><span data-stu-id="d9df0-141">If you've already created your app package in App Studio, chose it from the list.</span></span> <span data-ttu-id="d9df0-142">В противном случае вы можете импортировать существующий пакет приложения.</span><span class="sxs-lookup"><span data-stu-id="d9df0-142">If not, you can import an existing app package.</span></span>
3. <span data-ttu-id="d9df0-143">Нажмите кнопку **Add (добавить** ) в разделе Command (Добавить).</span><span class="sxs-lookup"><span data-stu-id="d9df0-143">Click the **Add** button in the Command section.</span></span>
4. <span data-ttu-id="d9df0-144">Выберите **Разрешить пользователям активировать действия во внешних службах в Teams**.</span><span class="sxs-lookup"><span data-stu-id="d9df0-144">Choose **Allow users to trigger actions in external services while inside of Teams**.</span></span>
5. <span data-ttu-id="d9df0-145">Если вы хотите использовать статический набор параметров для создания модуля задачи, выберите этот параметр.</span><span class="sxs-lookup"><span data-stu-id="d9df0-145">If you want to use a static set of parameters to create your task module, select that option.</span></span> <span data-ttu-id="d9df0-146">В противном случае выберите вариант для **выборки динамического набора параметров из ленты**.</span><span class="sxs-lookup"><span data-stu-id="d9df0-146">Otherwise, choose to **Fetch a dynamic set of parameters from your bot**.</span></span>
6. <span data-ttu-id="d9df0-147">Добавьте **идентификатор команды** и **название**.</span><span class="sxs-lookup"><span data-stu-id="d9df0-147">Add a **Command Id** and a **Title**.</span></span>
7. <span data-ttu-id="d9df0-148">Выберите место, с которого будет запускаться команда действия.</span><span class="sxs-lookup"><span data-stu-id="d9df0-148">Select where you want your action command to be triggered from.</span></span>
8. <span data-ttu-id="d9df0-149">Если вы используете параметры для модуля задачи, добавьте первый из них.</span><span class="sxs-lookup"><span data-stu-id="d9df0-149">If you're using parameters for your task module, add the first one.</span></span>
9. <span data-ttu-id="d9df0-150">Нажмите кнопку Save (Сохранить)</span><span class="sxs-lookup"><span data-stu-id="d9df0-150">Click Save</span></span>
10. <span data-ttu-id="d9df0-151">Если требуется добавить дополнительные параметры, нажмите кнопку **Добавить** в разделе **Параметры** , чтобы добавить их.</span><span class="sxs-lookup"><span data-stu-id="d9df0-151">If you need to add more parameters, click the **Add** button in the **Parameters** section to add them.</span></span>

### <a name="manually-create-a-command"></a><span data-ttu-id="d9df0-152">Создание команды вручную</span><span class="sxs-lookup"><span data-stu-id="d9df0-152">Manually create a command</span></span>

<span data-ttu-id="d9df0-153">Чтобы вручную добавить команду расширения обмена сообщениями на основе действий в манифест приложения, необходимо добавить к `composeExtension.commands` массиву объектов следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="d9df0-153">To manually add your action-based messaging extension command to your app manifest, you'll need to add the follow parameters to your `composeExtension.commands` array of objects.</span></span>

| <span data-ttu-id="d9df0-154">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="d9df0-154">Property name</span></span> | <span data-ttu-id="d9df0-155">Назначение</span><span class="sxs-lookup"><span data-stu-id="d9df0-155">Purpose</span></span> | <span data-ttu-id="d9df0-156">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="d9df0-156">Required?</span></span> | <span data-ttu-id="d9df0-157">Минимальная версия манифеста</span><span class="sxs-lookup"><span data-stu-id="d9df0-157">Minimum manifest version</span></span> |
|---|---|---|---|
| `id` | <span data-ttu-id="d9df0-158">Уникальный идентификатор, назначенный этой команде.</span><span class="sxs-lookup"><span data-stu-id="d9df0-158">Unique ID that you assign to this command.</span></span> <span data-ttu-id="d9df0-159">Запрос пользователя будет включать этот идентификатор.</span><span class="sxs-lookup"><span data-stu-id="d9df0-159">The user request will include this ID.</span></span> | <span data-ttu-id="d9df0-160">Да</span><span class="sxs-lookup"><span data-stu-id="d9df0-160">Yes</span></span> | <span data-ttu-id="d9df0-161">1.0</span><span class="sxs-lookup"><span data-stu-id="d9df0-161">1.0</span></span> |
| `title` | <span data-ttu-id="d9df0-162">Имя команды.</span><span class="sxs-lookup"><span data-stu-id="d9df0-162">Command name.</span></span> <span data-ttu-id="d9df0-163">Это значение отображается в пользовательском интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="d9df0-163">This value appears in the UI.</span></span> | <span data-ttu-id="d9df0-164">Да</span><span class="sxs-lookup"><span data-stu-id="d9df0-164">Yes</span></span> | <span data-ttu-id="d9df0-165">1.0</span><span class="sxs-lookup"><span data-stu-id="d9df0-165">1.0</span></span> |
| `type` | <span data-ttu-id="d9df0-166">Необходимое значение — `action`.</span><span class="sxs-lookup"><span data-stu-id="d9df0-166">Must be `action`</span></span> | <span data-ttu-id="d9df0-167">Нет</span><span class="sxs-lookup"><span data-stu-id="d9df0-167">No</span></span> | <span data-ttu-id="d9df0-168">1.4</span><span class="sxs-lookup"><span data-stu-id="d9df0-168">1.4</span></span> |
| `fetchTask` | <span data-ttu-id="d9df0-169">`true`для адаптивной карточки или встроенного веб-представления для модуля задач `false` , для статического списка параметров или при загрузке веб-представления с помощью`taskInfo`</span><span class="sxs-lookup"><span data-stu-id="d9df0-169">`true` for an adaptive card or embedded web view for your task module, `false` for a static list of parameters or when loading the web view by a `taskInfo`</span></span> | <span data-ttu-id="d9df0-170">Нет</span><span class="sxs-lookup"><span data-stu-id="d9df0-170">No</span></span> | <span data-ttu-id="d9df0-171">1.4</span><span class="sxs-lookup"><span data-stu-id="d9df0-171">1.4</span></span> |
| `context` | <span data-ttu-id="d9df0-172">Необязательный массив значений, определяющий расположение, из которого может вызываться расширение обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="d9df0-172">Optional array of values that defines where the messaging extension can be invoked from.</span></span> <span data-ttu-id="d9df0-173">Возможные значения: `message`, `compose`, или `commandBox`.</span><span class="sxs-lookup"><span data-stu-id="d9df0-173">Possible values are `message`, `compose`, or `commandBox`.</span></span> <span data-ttu-id="d9df0-174">Значение по умолчанию: `["compose", "commandBox"]`.</span><span class="sxs-lookup"><span data-stu-id="d9df0-174">Default is `["compose", "commandBox"]`.</span></span> | <span data-ttu-id="d9df0-175">Нет</span><span class="sxs-lookup"><span data-stu-id="d9df0-175">No</span></span> | <span data-ttu-id="d9df0-176">1.5</span><span class="sxs-lookup"><span data-stu-id="d9df0-176">1.5</span></span> |

<span data-ttu-id="d9df0-177">Если вы используете статический список параметров, вы также добавите их.</span><span class="sxs-lookup"><span data-stu-id="d9df0-177">If you are using a static list of parameters, you'll add them as well.</span></span>

| <span data-ttu-id="d9df0-178">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="d9df0-178">Property name</span></span> | <span data-ttu-id="d9df0-179">Назначение</span><span class="sxs-lookup"><span data-stu-id="d9df0-179">Purpose</span></span> | <span data-ttu-id="d9df0-180">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="d9df0-180">Required?</span></span> | <span data-ttu-id="d9df0-181">Минимальная версия манифеста</span><span class="sxs-lookup"><span data-stu-id="d9df0-181">Minimum manifest version</span></span> |
|---|---|---|---|
| `parameters` | <span data-ttu-id="d9df0-182">Статический список параметров для команды.</span><span class="sxs-lookup"><span data-stu-id="d9df0-182">Static list of parameters for the command.</span></span> <span data-ttu-id="d9df0-183">Используйте, только `fetchTask` когда —`false`</span><span class="sxs-lookup"><span data-stu-id="d9df0-183">Only use when `fetchTask` is `false`</span></span> | <span data-ttu-id="d9df0-184">Нет</span><span class="sxs-lookup"><span data-stu-id="d9df0-184">No</span></span> | <span data-ttu-id="d9df0-185">1.0</span><span class="sxs-lookup"><span data-stu-id="d9df0-185">1.0</span></span> |
| `parameter.name` | <span data-ttu-id="d9df0-186">Имя параметра.</span><span class="sxs-lookup"><span data-stu-id="d9df0-186">The name of the parameter.</span></span> <span data-ttu-id="d9df0-187">Он отправляется службе по запросу пользователя.</span><span class="sxs-lookup"><span data-stu-id="d9df0-187">This is sent to your service in the user request.</span></span> | <span data-ttu-id="d9df0-188">Да</span><span class="sxs-lookup"><span data-stu-id="d9df0-188">Yes</span></span> | <span data-ttu-id="d9df0-189">1.0</span><span class="sxs-lookup"><span data-stu-id="d9df0-189">1.0</span></span> |
| `parameter.description` | <span data-ttu-id="d9df0-190">Описывает назначение этого параметра или пример значения, которое следует предоставить.</span><span class="sxs-lookup"><span data-stu-id="d9df0-190">Describes this parameter’s purposes or example of the value that should be provided.</span></span> <span data-ttu-id="d9df0-191">Это значение отображается в пользовательском интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="d9df0-191">This value appears in the UI.</span></span> | <span data-ttu-id="d9df0-192">Да</span><span class="sxs-lookup"><span data-stu-id="d9df0-192">Yes</span></span> | <span data-ttu-id="d9df0-193">1.0</span><span class="sxs-lookup"><span data-stu-id="d9df0-193">1.0</span></span> |
| `parameter.title` | <span data-ttu-id="d9df0-194">Краткий заголовком или меткой с понятным пользователем параметром.</span><span class="sxs-lookup"><span data-stu-id="d9df0-194">Short user-friendly parameter title or label.</span></span> | <span data-ttu-id="d9df0-195">Да</span><span class="sxs-lookup"><span data-stu-id="d9df0-195">Yes</span></span> | <span data-ttu-id="d9df0-196">1.0</span><span class="sxs-lookup"><span data-stu-id="d9df0-196">1.0</span></span> |
| `parameter.inputType` | <span data-ttu-id="d9df0-197">Укажите требуемый тип ввода.</span><span class="sxs-lookup"><span data-stu-id="d9df0-197">Set to the type of input required.</span></span> <span data-ttu-id="d9df0-198">Возможные значения: `text`, `textarea`, `number`, `date`, `time`, `toggle`.</span><span class="sxs-lookup"><span data-stu-id="d9df0-198">Possible values include `text`, `textarea`, `number`, `date`, `time`, `toggle`.</span></span> <span data-ttu-id="d9df0-199">Значение по умолчанию:`text`</span><span class="sxs-lookup"><span data-stu-id="d9df0-199">Default is set to `text`</span></span> | <span data-ttu-id="d9df0-200">Нет</span><span class="sxs-lookup"><span data-stu-id="d9df0-200">No</span></span> | <span data-ttu-id="d9df0-201">1.4</span><span class="sxs-lookup"><span data-stu-id="d9df0-201">1.4</span></span> |

<span data-ttu-id="d9df0-202">При использовании внедренного веб-представления можно дополнительно добавить `taskInfo` объект для извлечения веб-представления, не обращаясь непосредственно к объекту Bot.</span><span class="sxs-lookup"><span data-stu-id="d9df0-202">If you are using an embedded web view, you can optionally add the `taskInfo` object to fetch your web view without calling your bot directly.</span></span> <span data-ttu-id="d9df0-203">Если выбран этот параметр, поведение аналогично статическому списку параметров в том, что первое взаимодействие с роботом будет [отвечать на действия по отсылке модуля задач](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md).</span><span class="sxs-lookup"><span data-stu-id="d9df0-203">If you choose to use this option, the behavior is similar to using a static list of parameters in that the first interaction with your bot will be [responding to the task module submit action](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md).</span></span> <span data-ttu-id="d9df0-204">Если вы используете `taskInfo` объект, обязательно задайте для `fetchTask` `false`параметра значение.</span><span class="sxs-lookup"><span data-stu-id="d9df0-204">If you are using a `taskInfo` object, be sure to also set the `fetchTask` parameter to `false`.</span></span>

| <span data-ttu-id="d9df0-205">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="d9df0-205">Property name</span></span> | <span data-ttu-id="d9df0-206">Назначение</span><span class="sxs-lookup"><span data-stu-id="d9df0-206">Purpose</span></span> | <span data-ttu-id="d9df0-207">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="d9df0-207">Required?</span></span> | <span data-ttu-id="d9df0-208">Минимальная версия манифеста</span><span class="sxs-lookup"><span data-stu-id="d9df0-208">Minimum manifest version</span></span> |
|---|---|---|---|
|`taskInfo`|<span data-ttu-id="d9df0-209">Указание модуля задач для предварительной загрузки при использовании команды расширения системы обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="d9df0-209">Specify the task module to preload when using a messaging extension command</span></span>| <span data-ttu-id="d9df0-210">Нет</span><span class="sxs-lookup"><span data-stu-id="d9df0-210">No</span></span> | <span data-ttu-id="d9df0-211">1.4</span><span class="sxs-lookup"><span data-stu-id="d9df0-211">1.4</span></span> |
|`taskInfo.title`|<span data-ttu-id="d9df0-212">Заголовок исходного модуля задач</span><span class="sxs-lookup"><span data-stu-id="d9df0-212">Initial task module title</span></span>|<span data-ttu-id="d9df0-213">Нет</span><span class="sxs-lookup"><span data-stu-id="d9df0-213">No</span></span> | <span data-ttu-id="d9df0-214">1.4</span><span class="sxs-lookup"><span data-stu-id="d9df0-214">1.4</span></span> |
|`taskInfo.width`|<span data-ttu-id="d9df0-215">Ширина модуля задачи — число в пикселях или макет по умолчанию, например "крупный", "средний" или "Малый"</span><span class="sxs-lookup"><span data-stu-id="d9df0-215">Task module width - either a number in pixels or default layout such as 'large', 'medium', or 'small'</span></span>|<span data-ttu-id="d9df0-216">Нет</span><span class="sxs-lookup"><span data-stu-id="d9df0-216">No</span></span> | <span data-ttu-id="d9df0-217">1.4</span><span class="sxs-lookup"><span data-stu-id="d9df0-217">1.4</span></span> |
|`taskInfo.height`|<span data-ttu-id="d9df0-218">Высота модуля задачи — число в пикселях или макет по умолчанию, например "крупный", "средний" или "Малый"</span><span class="sxs-lookup"><span data-stu-id="d9df0-218">Task module height - either a number in pixels or default layout such as 'large', 'medium', or 'small'</span></span>|<span data-ttu-id="d9df0-219">Нет</span><span class="sxs-lookup"><span data-stu-id="d9df0-219">No</span></span> | <span data-ttu-id="d9df0-220">1.4</span><span class="sxs-lookup"><span data-stu-id="d9df0-220">1.4</span></span> |
|`taskInfo.url`|<span data-ttu-id="d9df0-221">URL-адрес начального представления в Интернете</span><span class="sxs-lookup"><span data-stu-id="d9df0-221">Initial web view URL</span></span>|<span data-ttu-id="d9df0-222">Нет</span><span class="sxs-lookup"><span data-stu-id="d9df0-222">No</span></span> | <span data-ttu-id="d9df0-223">1.4</span><span class="sxs-lookup"><span data-stu-id="d9df0-223">1.4</span></span> |

#### <a name="app-manifest-example"></a><span data-ttu-id="d9df0-224">Пример манифеста приложения</span><span class="sxs-lookup"><span data-stu-id="d9df0-224">App manifest example</span></span>

<span data-ttu-id="d9df0-225">Ниже приведен пример `composeExtensions` объекта, определяющего две команды действия.</span><span class="sxs-lookup"><span data-stu-id="d9df0-225">The below is an example of a `composeExtensions` object defining two action commands.</span></span> <span data-ttu-id="d9df0-226">Это не пример полного манифеста для полной схемы манифеста приложения: [схема манифеста приложения](~/resources/schema/manifest-schema.md).</span><span class="sxs-lookup"><span data-stu-id="d9df0-226">It is not an example of the complete manifest, for the full app manifest schema see: [App manifest schema](~/resources/schema/manifest-schema.md).</span></span>

```json
...
"composeExtensions": [
  {
    "botId": "12a3c29f-1fc5-4d97-a142-12bb662b7b23",
    "canUpdateConfiguration": true,
    "commands": [
      {
        "id": "addTodo",
        "description": "Create a To Do item",
        "title": "Create To Do",
        "type": "action",
        "context": ["commandBox", "message", "compose"],
        "fetchTask": false,
        "parameters": [
          {
            "name": "Name",
            "description": "To Do Title",
            "title": "Title",
            "inputType": "text"
          },
          {
            "name": "Description",
            "description": "Description of the task",
            "title": "Description",
            "inputType": "textarea"
          },
          {
            "name": "Date",
            "description": "Due date for the task",
            "title": "Date",
            "inputType": "date"
          }
        ]
      },
      {
        "id": "reassignTodo",
        "description": "Reassign a todo item",
        "title": "Reassign a todo item",
        "type": "action",
        "fetchTask": true,
      }
    ]
  }
]
...
```

## <a name="next-steps"></a><span data-ttu-id="d9df0-227">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d9df0-227">Next steps</span></span>

<span data-ttu-id="d9df0-228">Если вы используете адаптивную карту или встроенное веб-представление без `taskInfo` объекта, вам нужно выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="d9df0-228">If you are using either an adaptive card or an embedded web view without a `taskInfo` object, you'll want to:</span></span>

* [<span data-ttu-id="d9df0-229">Создание модуля задачи и ответ на него</span><span class="sxs-lookup"><span data-stu-id="d9df0-229">Create and respond with a task module</span></span>](~/messaging-extensions/how-to/action-commands/create-task-module.md)

<span data-ttu-id="d9df0-230">Если вы используете параметры или внедренное веб-представление с `taskInfo` объектом, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="d9df0-230">If you are using parameters or an embedded web view with a `taskInfo` object, the next step for you is to:</span></span>

* [<span data-ttu-id="d9df0-231">Отклик на отправку модуля задачи</span><span class="sxs-lookup"><span data-stu-id="d9df0-231">Respond to task module submit</span></span>](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
