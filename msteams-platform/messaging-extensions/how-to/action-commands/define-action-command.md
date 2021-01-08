---
title: Определение команд действий расширения обмена сообщениями
author: clearab
description: Обзор команд действий расширения обмена сообщениями
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: be2135477c4234187f374aef215f90e8329fb74e
ms.sourcegitcommit: 5739245903278d521ec920427248b6b48676e637
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/07/2021
ms.locfileid: "49778403"
---
# <a name="define-messaging-extension-action-commands"></a><span data-ttu-id="89ce3-103">Определение команд действий расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="89ce3-103">Define messaging extension action commands</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="89ce3-104">С помощью команд действий вы можете представить пользователям модальные всплывающие окна (называемые модулем задач в Teams) для сбора или отображения информации, а затем обработать их взаимодействие и отправить информацию обратно в Teams.</span><span class="sxs-lookup"><span data-stu-id="89ce3-104">Action commands allow you present your users with a modal popup (called a task module in Teams) to collect or display information, then process their interaction and send information back to Teams.</span></span> <span data-ttu-id="89ce3-105">Перед созданием команды необходимо решить:</span><span class="sxs-lookup"><span data-stu-id="89ce3-105">Before creating your command you'll need to decide:</span></span>

1. <span data-ttu-id="89ce3-106">Откуда можно запускать команду действия?</span><span class="sxs-lookup"><span data-stu-id="89ce3-106">Where can the action command be triggered from?</span></span>
1. <span data-ttu-id="89ce3-107">Как будет создан модуль задачи?</span><span class="sxs-lookup"><span data-stu-id="89ce3-107">How will the task module be created?</span></span>
1. <span data-ttu-id="89ce3-108">Будет ли отправлено в канал окончательное сообщение или карточка от бота или сообщение или карточка будут вставлены в область составить сообщение для отправки пользователем?</span><span class="sxs-lookup"><span data-stu-id="89ce3-108">Will the final message or card be sent to the channel from a bot, or will the message or card be inserted into the compose message area for the user to submit?</span></span>

## <a name="choose-action-command-invoke-locations"></a><span data-ttu-id="89ce3-109">Выбор местоположений вызова команды действия</span><span class="sxs-lookup"><span data-stu-id="89ce3-109">Choose action command invoke locations</span></span>

<span data-ttu-id="89ce3-110">Первое, что вам нужно решить, — откуда можно инициируете команду действия (или, точнее, *из* нее).</span><span class="sxs-lookup"><span data-stu-id="89ce3-110">The first thing you need to decide is where your action command can be triggered (or more specifically, *invoked*) from.</span></span> <span data-ttu-id="89ce3-111">Указав манифест приложения, команда может быть вызвана из одного или нескольких `context` из следующих мест:</span><span class="sxs-lookup"><span data-stu-id="89ce3-111">By specifying the `context` in your app manifest, your command can be invoked from one or more of the following locations:</span></span>

* <span data-ttu-id="89ce3-112">Кнопки в нижней части области сообщения составить.</span><span class="sxs-lookup"><span data-stu-id="89ce3-112">The buttons at the bottom of the compose message area.</span></span>
* <span data-ttu-id="89ce3-113">По @mentioning приложение в командной окне.</span><span class="sxs-lookup"><span data-stu-id="89ce3-113">By @mentioning your app in the command box.</span></span> <span data-ttu-id="89ce3-114">Примечание. Невозможно ответить сообщением бота, вставленным непосредственно в беседу, если расширение обмена сообщениями вызывается из командного окна.</span><span class="sxs-lookup"><span data-stu-id="89ce3-114">Note: You cannot respond with a bot message inserted directly into the conversation if your messaging extension is invoked from the command box.</span></span>
* <span data-ttu-id="89ce3-115">Непосредственно из существующего сообщения с помощью ... меню переполнения в сообщении.</span><span class="sxs-lookup"><span data-stu-id="89ce3-115">Directly from an existing message via the ... overflow menu on a message.</span></span> <span data-ttu-id="89ce3-116">Примечание. Начальный вызов бота будет включать объект JSON, содержащий сообщение, из которого он был вызван, который можно обработать перед тем, как представить ему модуль задачи.</span><span class="sxs-lookup"><span data-stu-id="89ce3-116">Note: The initial invoke to your bot will include a JSON object containing the message from which it was invoked, which you can process before presenting them with a task module.</span></span>

## <a name="choose-how-to-build-your-task-module"></a><span data-ttu-id="89ce3-117">Выбор сборки модуля задачи</span><span class="sxs-lookup"><span data-stu-id="89ce3-117">Choose how to build your task module</span></span>

<span data-ttu-id="89ce3-118">Помимо выбора места вызова команды, необходимо также выбрать, как заполнить форму в модуле задачи для пользователей.</span><span class="sxs-lookup"><span data-stu-id="89ce3-118">In addition to choosing where your command can be invoked from, you must also chose how to populate the form in the task module for your users.</span></span> <span data-ttu-id="89ce3-119">Существует три варианта создания формы, которая будет отрисовываться внутри модуля задачи:</span><span class="sxs-lookup"><span data-stu-id="89ce3-119">You have three options for creating the form that is rendered inside the task module:</span></span>

* <span data-ttu-id="89ce3-120">**Статический список параметров** — это самый простой вариант.</span><span class="sxs-lookup"><span data-stu-id="89ce3-120">**Static list of parameters** - This is the simplest option.</span></span> <span data-ttu-id="89ce3-121">Вы можете определить список параметров (полей ввода) в манифесте приложения, который будет отрисовки клиентом Teams.</span><span class="sxs-lookup"><span data-stu-id="89ce3-121">You can define a list of parameters (input fields) in your app manifest the Teams client will render.</span></span> <span data-ttu-id="89ce3-122">Вы не можете управлять форматированием с помощью этого параметра.</span><span class="sxs-lookup"><span data-stu-id="89ce3-122">You cannot control the formatting with this option.</span></span>
* <span data-ttu-id="89ce3-123">**Адаптивная карточка.** Вы можете использовать адаптивную карточку, которая обеспечивает более полный контроль над пользовательским интерфейсом, но ограничивает доступные элементы управления и параметры форматирования.</span><span class="sxs-lookup"><span data-stu-id="89ce3-123">**Adaptive card** - You can choose to use an adaptive card, which provides greater control over the UI, but still limits you on the available controls and formatting options.</span></span>
* <span data-ttu-id="89ce3-124">**Внедренное представление** веб-страницы. Если вам требуется полный контроль над пользовательским интерфейсом и элементами управления, вы можете встраить пользовательское представление веб-страницы в модуль задачи.</span><span class="sxs-lookup"><span data-stu-id="89ce3-124">**Embedded web view** - If you need complete control over the UI and controls, you can choose to embed a custom web view in the task module.</span></span>

<span data-ttu-id="89ce3-125">Если вы решили создать модуль задачи со статическим списком параметров, первым вызовом расширения обмена сообщениями будет отправка модуля задачи пользователем.</span><span class="sxs-lookup"><span data-stu-id="89ce3-125">If you choose to create your task module with a static list of parameters, the first call to your messaging extension will be when a user submits the task module.</span></span> <span data-ttu-id="89ce3-126">При использовании внедренного представления веб-страницы или адаптивной карточки расширению обмена сообщениями потребуется обработать исходное событие вызова от пользователя, создать модуль задачи и вернуть его клиенту.</span><span class="sxs-lookup"><span data-stu-id="89ce3-126">When using an embedded web view or an adaptive card, your messaging extension will need to handle an initial invoke event from the user, create the task module, and return it back to the client.</span></span>

## <a name="choose-how-the-final-message-will-be-sent"></a><span data-ttu-id="89ce3-127">Выбор того, как будет отправлено окончательное сообщение</span><span class="sxs-lookup"><span data-stu-id="89ce3-127">Choose how the final message will be sent</span></span>

<span data-ttu-id="89ce3-128">В большинстве случаев команда действия приведет к вставке карточки в поле составить сообщение.</span><span class="sxs-lookup"><span data-stu-id="89ce3-128">In most cases, your action command will result in a card inserted into the compose message box.</span></span> <span data-ttu-id="89ce3-129">После этого пользователь может отправить его в канал или чат.</span><span class="sxs-lookup"><span data-stu-id="89ce3-129">Your user can then decide to send it into the channel or chat.</span></span> <span data-ttu-id="89ce3-130">В этом случае сообщение поступает от пользователя, и ваш бот не сможет редактировать или обновлять карточку дальше.</span><span class="sxs-lookup"><span data-stu-id="89ce3-130">The message in this case comes from the user, and your bot will not be able to edit or update the card further.</span></span>

<span data-ttu-id="89ce3-131">Если расширение обмена сообщениями запускается из окна составить или непосредственно из сообщения, веб-служба может вставить окончательный ответ непосредственно в канал или чат.</span><span class="sxs-lookup"><span data-stu-id="89ce3-131">If your messaging extension is triggered from the compose box or directly from a message, your web service can insert the final response directly into the channel or chat.</span></span> <span data-ttu-id="89ce3-132">В этом случае адаптивная карточка поступает от бота, бот сможет обновить ее, а при необходимости бот также сможет ответить на беседу.</span><span class="sxs-lookup"><span data-stu-id="89ce3-132">In this case, the adaptive card comes from the bot, the bot will be able to update it, and the bot can also reply to the conversation thread if needed.</span></span> <span data-ttu-id="89ce3-133">Вам потребуется добавить объект в манифест приложения, используя тот же ИД и `bot` определив соответствующие области.</span><span class="sxs-lookup"><span data-stu-id="89ce3-133">You will need to add the `bot` object to your app manifest using the same Id and defining the appropriate scopes.</span></span>

## <a name="add-the-command-to-your-app-manifest"></a><span data-ttu-id="89ce3-134">Добавление команды в манифест приложения</span><span class="sxs-lookup"><span data-stu-id="89ce3-134">Add the command to your app manifest</span></span>

<span data-ttu-id="89ce3-135">Теперь, когда вы решили, как пользователи будут взаимодействовать с вашей командой действий, пришло время добавить ее в манифест приложения.</span><span class="sxs-lookup"><span data-stu-id="89ce3-135">Now that you've decided how users will interact with your action command, it is time to add it to your app manifest.</span></span> <span data-ttu-id="89ce3-136">Для этого вы добавите новый объект на верхний уровень `composeExtension` манифеста приложения JSON.</span><span class="sxs-lookup"><span data-stu-id="89ce3-136">To do this you'll add a new `composeExtension` object to the top level of your app manifest JSON.</span></span> <span data-ttu-id="89ce3-137">Это можно сделать с помощью App Studio или вручную.</span><span class="sxs-lookup"><span data-stu-id="89ce3-137">You can either do so with the help of App Studio, or manually.</span></span>

### <a name="create-a-command-using-app-studio"></a><span data-ttu-id="89ce3-138">Создание команды с помощью App Studio</span><span class="sxs-lookup"><span data-stu-id="89ce3-138">Create a command using App Studio</span></span>

<span data-ttu-id="89ce3-139">В следующих шагах предполагается, что вы уже [создали расширение для обмена сообщениями.](~/messaging-extensions/how-to/create-messaging-extension.md)</span><span class="sxs-lookup"><span data-stu-id="89ce3-139">The following steps assume you've already [created a messaging extension](~/messaging-extensions/how-to/create-messaging-extension.md).</span></span>

1. <span data-ttu-id="89ce3-140">В клиенте Microsoft Teams откройте **App Studio** и выберите вкладку **"Редактор** манифеста".</span><span class="sxs-lookup"><span data-stu-id="89ce3-140">From the Microsoft Teams client, open **App Studio** and select the **Manifest Editor** tab.</span></span>
2. <span data-ttu-id="89ce3-141">Если вы уже создали пакет приложения в App Studio, вы выбрали его из списка.</span><span class="sxs-lookup"><span data-stu-id="89ce3-141">If you've already created your app package in App Studio, chose it from the list.</span></span> <span data-ttu-id="89ce3-142">В этом случае можно импортировать существующий пакет приложения.</span><span class="sxs-lookup"><span data-stu-id="89ce3-142">If not, you can import an existing app package.</span></span>
3. <span data-ttu-id="89ce3-143">Нажмите **кнопку "Добавить"** в разделе "Команда".</span><span class="sxs-lookup"><span data-stu-id="89ce3-143">Click the **Add** button in the Command section.</span></span>
4. <span data-ttu-id="89ce3-144">Choose **Allow users to trigger actions in external services while inside of Teams**.</span><span class="sxs-lookup"><span data-stu-id="89ce3-144">Choose **Allow users to trigger actions in external services while inside of Teams**.</span></span>
5. <span data-ttu-id="89ce3-145">Если вы хотите использовать статический набор параметров для создания модуля задачи, выберите этот параметр.</span><span class="sxs-lookup"><span data-stu-id="89ce3-145">If you want to use a static set of parameters to create your task module, select that option.</span></span> <span data-ttu-id="89ce3-146">В противном случае выберите **"Получить динамический набор параметров" от бота.**</span><span class="sxs-lookup"><span data-stu-id="89ce3-146">Otherwise, choose to **Fetch a dynamic set of parameters from your bot**.</span></span>
6. <span data-ttu-id="89ce3-147">Добавьте **ид команды** и **заголовок.**</span><span class="sxs-lookup"><span data-stu-id="89ce3-147">Add a **Command Id** and a **Title**.</span></span>
7. <span data-ttu-id="89ce3-148">Выберите, откуда должна запускаться команда действий.</span><span class="sxs-lookup"><span data-stu-id="89ce3-148">Select where you want your action command to be triggered from.</span></span>
8. <span data-ttu-id="89ce3-149">Если вы используете параметры для модуля задачи, добавьте первый из них.</span><span class="sxs-lookup"><span data-stu-id="89ce3-149">If you're using parameters for your task module, add the first one.</span></span>
9. <span data-ttu-id="89ce3-150">Нажмите кнопку Save (Сохранить)</span><span class="sxs-lookup"><span data-stu-id="89ce3-150">Click Save</span></span>
10. <span data-ttu-id="89ce3-151">Если необходимо добавить дополнительные параметры, нажмите **кнопку** "Добавить" в разделе **"Параметры",** чтобы добавить их.</span><span class="sxs-lookup"><span data-stu-id="89ce3-151">If you need to add more parameters, click the **Add** button in the **Parameters** section to add them.</span></span>

### <a name="manually-create-a-command"></a><span data-ttu-id="89ce3-152">Создание команды вручную</span><span class="sxs-lookup"><span data-stu-id="89ce3-152">Manually create a command</span></span>

<span data-ttu-id="89ce3-153">Чтобы вручную добавить команду расширения сообщений на основе действий в манифест приложения, необходимо добавить в массив объектов параметры, которые следует `composeExtension.commands` использовать.</span><span class="sxs-lookup"><span data-stu-id="89ce3-153">To manually add your action-based messaging extension command to your app manifest, you'll need to add the follow parameters to your `composeExtension.commands` array of objects.</span></span>

| <span data-ttu-id="89ce3-154">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="89ce3-154">Property name</span></span> | <span data-ttu-id="89ce3-155">Назначение</span><span class="sxs-lookup"><span data-stu-id="89ce3-155">Purpose</span></span> | <span data-ttu-id="89ce3-156">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="89ce3-156">Required?</span></span> | <span data-ttu-id="89ce3-157">Минимальная версия манифеста</span><span class="sxs-lookup"><span data-stu-id="89ce3-157">Minimum manifest version</span></span> |
|---|---|---|---|
| `id` | <span data-ttu-id="89ce3-158">Уникальный ИД, присвоенный этой команде.</span><span class="sxs-lookup"><span data-stu-id="89ce3-158">Unique ID that you assign to this command.</span></span> <span data-ttu-id="89ce3-159">Запрос пользователя будет включать этот ИД.</span><span class="sxs-lookup"><span data-stu-id="89ce3-159">The user request will include this ID.</span></span> | <span data-ttu-id="89ce3-160">Да</span><span class="sxs-lookup"><span data-stu-id="89ce3-160">Yes</span></span> | <span data-ttu-id="89ce3-161">1.0</span><span class="sxs-lookup"><span data-stu-id="89ce3-161">1.0</span></span> |
| `title` | <span data-ttu-id="89ce3-162">Имя команды.</span><span class="sxs-lookup"><span data-stu-id="89ce3-162">Command name.</span></span> <span data-ttu-id="89ce3-163">Это значение отображается в пользовательском интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="89ce3-163">This value appears in the UI.</span></span> | <span data-ttu-id="89ce3-164">Да</span><span class="sxs-lookup"><span data-stu-id="89ce3-164">Yes</span></span> | <span data-ttu-id="89ce3-165">1.0</span><span class="sxs-lookup"><span data-stu-id="89ce3-165">1.0</span></span> |
| `type` | <span data-ttu-id="89ce3-166">Необходимое значение — `action`.</span><span class="sxs-lookup"><span data-stu-id="89ce3-166">Must be `action`</span></span> | <span data-ttu-id="89ce3-167">Нет</span><span class="sxs-lookup"><span data-stu-id="89ce3-167">No</span></span> | <span data-ttu-id="89ce3-168">1.4</span><span class="sxs-lookup"><span data-stu-id="89ce3-168">1.4</span></span> |
| `fetchTask` | <span data-ttu-id="89ce3-169">`true` для адаптивной карточки или внедренного представления веб-страницы для модуля задачи, статического списка параметров или при загрузке представления `false` веб-страницы `taskInfo`</span><span class="sxs-lookup"><span data-stu-id="89ce3-169">`true` for an adaptive card or embedded web view for your task module, `false` for a static list of parameters or when loading the web view by a `taskInfo`</span></span> | <span data-ttu-id="89ce3-170">Нет</span><span class="sxs-lookup"><span data-stu-id="89ce3-170">No</span></span> | <span data-ttu-id="89ce3-171">1.4</span><span class="sxs-lookup"><span data-stu-id="89ce3-171">1.4</span></span> |
| `context` | <span data-ttu-id="89ce3-172">Необязательный массив значений, определяющий, откуда можно вызывать расширение обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="89ce3-172">Optional array of values that defines where the messaging extension can be invoked from.</span></span> <span data-ttu-id="89ce3-173">Возможные значения: `message` `compose` , или `commandBox` .</span><span class="sxs-lookup"><span data-stu-id="89ce3-173">Possible values are `message`, `compose`, or `commandBox`.</span></span> <span data-ttu-id="89ce3-174">Значение по умолчанию: `["compose", "commandBox"]`.</span><span class="sxs-lookup"><span data-stu-id="89ce3-174">Default is `["compose", "commandBox"]`.</span></span> | <span data-ttu-id="89ce3-175">Нет</span><span class="sxs-lookup"><span data-stu-id="89ce3-175">No</span></span> | <span data-ttu-id="89ce3-176">1.5</span><span class="sxs-lookup"><span data-stu-id="89ce3-176">1.5</span></span> |

<span data-ttu-id="89ce3-177">Если вы используете статический список параметров, вы также добавим их.</span><span class="sxs-lookup"><span data-stu-id="89ce3-177">If you are using a static list of parameters, you'll add them as well.</span></span>

| <span data-ttu-id="89ce3-178">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="89ce3-178">Property name</span></span> | <span data-ttu-id="89ce3-179">Назначение</span><span class="sxs-lookup"><span data-stu-id="89ce3-179">Purpose</span></span> | <span data-ttu-id="89ce3-180">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="89ce3-180">Required?</span></span> | <span data-ttu-id="89ce3-181">Минимальная версия манифеста</span><span class="sxs-lookup"><span data-stu-id="89ce3-181">Minimum manifest version</span></span> |
|---|---|---|---|
| `parameters` | <span data-ttu-id="89ce3-182">Статический список параметров для команды.</span><span class="sxs-lookup"><span data-stu-id="89ce3-182">Static list of parameters for the command.</span></span> <span data-ttu-id="89ce3-183">Используйте только в `fetchTask` том случае, если `false`</span><span class="sxs-lookup"><span data-stu-id="89ce3-183">Only use when `fetchTask` is `false`</span></span> | <span data-ttu-id="89ce3-184">Нет</span><span class="sxs-lookup"><span data-stu-id="89ce3-184">No</span></span> | <span data-ttu-id="89ce3-185">1.0</span><span class="sxs-lookup"><span data-stu-id="89ce3-185">1.0</span></span> |
| `parameter.name` | <span data-ttu-id="89ce3-186">Имя параметра.</span><span class="sxs-lookup"><span data-stu-id="89ce3-186">The name of the parameter.</span></span> <span data-ttu-id="89ce3-187">Он отправляется службе в запросе пользователя.</span><span class="sxs-lookup"><span data-stu-id="89ce3-187">This is sent to your service in the user request.</span></span> | <span data-ttu-id="89ce3-188">Да</span><span class="sxs-lookup"><span data-stu-id="89ce3-188">Yes</span></span> | <span data-ttu-id="89ce3-189">1.0</span><span class="sxs-lookup"><span data-stu-id="89ce3-189">1.0</span></span> |
| `parameter.description` | <span data-ttu-id="89ce3-190">Описывает цели этого параметра или пример значения, которое должно быть предоставлено.</span><span class="sxs-lookup"><span data-stu-id="89ce3-190">Describes this parameter’s purposes or example of the value that should be provided.</span></span> <span data-ttu-id="89ce3-191">Это значение отображается в пользовательском интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="89ce3-191">This value appears in the UI.</span></span> | <span data-ttu-id="89ce3-192">Да</span><span class="sxs-lookup"><span data-stu-id="89ce3-192">Yes</span></span> | <span data-ttu-id="89ce3-193">1.0</span><span class="sxs-lookup"><span data-stu-id="89ce3-193">1.0</span></span> |
| `parameter.title` | <span data-ttu-id="89ce3-194">Короткое название или метка удобного параметра.</span><span class="sxs-lookup"><span data-stu-id="89ce3-194">Short user-friendly parameter title or label.</span></span> | <span data-ttu-id="89ce3-195">Да</span><span class="sxs-lookup"><span data-stu-id="89ce3-195">Yes</span></span> | <span data-ttu-id="89ce3-196">1.0</span><span class="sxs-lookup"><span data-stu-id="89ce3-196">1.0</span></span> |
| `parameter.inputType` | <span data-ttu-id="89ce3-197">Установите требуемого типа ввода.</span><span class="sxs-lookup"><span data-stu-id="89ce3-197">Set to the type of input required.</span></span> <span data-ttu-id="89ce3-198">Возможные значения: `text` `textarea` , , `number` `date` `time` `toggle` .</span><span class="sxs-lookup"><span data-stu-id="89ce3-198">Possible values include `text`, `textarea`, `number`, `date`, `time`, `toggle`.</span></span> <span data-ttu-id="89ce3-199">Значение по умолчанию: `text`</span><span class="sxs-lookup"><span data-stu-id="89ce3-199">Default is set to `text`</span></span> | <span data-ttu-id="89ce3-200">Нет</span><span class="sxs-lookup"><span data-stu-id="89ce3-200">No</span></span> | <span data-ttu-id="89ce3-201">1.4</span><span class="sxs-lookup"><span data-stu-id="89ce3-201">1.4</span></span> |

<span data-ttu-id="89ce3-202">При использовании внедренного представления веб-страницы можно при желании добавить объект для получения представления веб-страницы, не вызывая `taskInfo` бота напрямую.</span><span class="sxs-lookup"><span data-stu-id="89ce3-202">If you are using an embedded web view, you can optionally add the `taskInfo` object to fetch your web view without calling your bot directly.</span></span> <span data-ttu-id="89ce3-203">Если вы решили использовать этот параметр, поведение аналогично использованию статического списка параметров, так как первое взаимодействие с ботом будет отвечать на действие отправки модуля [задачи.](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)</span><span class="sxs-lookup"><span data-stu-id="89ce3-203">If you choose to use this option, the behavior is similar to using a static list of parameters in that the first interaction with your bot will be [responding to the task module submit action](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md).</span></span> <span data-ttu-id="89ce3-204">Если вы используете `taskInfo` объект, не забудьте также установить для `fetchTask` параметра `false` ..</span><span class="sxs-lookup"><span data-stu-id="89ce3-204">If you are using a `taskInfo` object, be sure to also set the `fetchTask` parameter to `false`.</span></span>

| <span data-ttu-id="89ce3-205">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="89ce3-205">Property name</span></span> | <span data-ttu-id="89ce3-206">Назначение</span><span class="sxs-lookup"><span data-stu-id="89ce3-206">Purpose</span></span> | <span data-ttu-id="89ce3-207">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="89ce3-207">Required?</span></span> | <span data-ttu-id="89ce3-208">Минимальная версия манифеста</span><span class="sxs-lookup"><span data-stu-id="89ce3-208">Minimum manifest version</span></span> |
|---|---|---|---|
|`taskInfo`|<span data-ttu-id="89ce3-209">Указание модуля задачи для предварительной загрузки при использовании команды расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="89ce3-209">Specify the task module to preload when using a messaging extension command</span></span>| <span data-ttu-id="89ce3-210">Нет</span><span class="sxs-lookup"><span data-stu-id="89ce3-210">No</span></span> | <span data-ttu-id="89ce3-211">1.4</span><span class="sxs-lookup"><span data-stu-id="89ce3-211">1.4</span></span> |
|`taskInfo.title`|<span data-ttu-id="89ce3-212">Заголовок модуля начальной задачи</span><span class="sxs-lookup"><span data-stu-id="89ce3-212">Initial task module title</span></span>|<span data-ttu-id="89ce3-213">Нет</span><span class="sxs-lookup"><span data-stu-id="89ce3-213">No</span></span> | <span data-ttu-id="89ce3-214">1.4</span><span class="sxs-lookup"><span data-stu-id="89ce3-214">1.4</span></span> |
|`taskInfo.width`|<span data-ttu-id="89ce3-215">Ширина модуля задачи — число в пикселях или макет по умолчанию, например "большой", "средний" или "маленький".</span><span class="sxs-lookup"><span data-stu-id="89ce3-215">Task module width - either a number in pixels or default layout such as 'large', 'medium', or 'small'</span></span>|<span data-ttu-id="89ce3-216">Нет</span><span class="sxs-lookup"><span data-stu-id="89ce3-216">No</span></span> | <span data-ttu-id="89ce3-217">1.4</span><span class="sxs-lookup"><span data-stu-id="89ce3-217">1.4</span></span> |
|`taskInfo.height`|<span data-ttu-id="89ce3-218">Высота модуля задачи — число в пикселях или макет по умолчанию, например "большой", "средний" или "маленький".</span><span class="sxs-lookup"><span data-stu-id="89ce3-218">Task module height - either a number in pixels or default layout such as 'large', 'medium', or 'small'</span></span>|<span data-ttu-id="89ce3-219">Нет</span><span class="sxs-lookup"><span data-stu-id="89ce3-219">No</span></span> | <span data-ttu-id="89ce3-220">1.4</span><span class="sxs-lookup"><span data-stu-id="89ce3-220">1.4</span></span> |
|`taskInfo.url`|<span data-ttu-id="89ce3-221">Исходный URL-адрес представления веб-страницы</span><span class="sxs-lookup"><span data-stu-id="89ce3-221">Initial web view URL</span></span>|<span data-ttu-id="89ce3-222">Нет</span><span class="sxs-lookup"><span data-stu-id="89ce3-222">No</span></span> | <span data-ttu-id="89ce3-223">1.4</span><span class="sxs-lookup"><span data-stu-id="89ce3-223">1.4</span></span> |

#### <a name="app-manifest-example"></a><span data-ttu-id="89ce3-224">Пример манифеста приложения</span><span class="sxs-lookup"><span data-stu-id="89ce3-224">App manifest example</span></span>

<span data-ttu-id="89ce3-225">Ниже приведен пример объекта, `composeExtensions` определяющий две команды действий.</span><span class="sxs-lookup"><span data-stu-id="89ce3-225">The below is an example of a `composeExtensions` object defining two action commands.</span></span> <span data-ttu-id="89ce3-226">Это не пример полного манифеста. Полную схему манифеста приложения см. в схеме [манифеста приложения.](~/resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="89ce3-226">It is not an example of the complete manifest, for the full app manifest schema see: [App manifest schema](~/resources/schema/manifest-schema.md).</span></span>

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
        "fetchTask": true,
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

## <a name="next-steps"></a><span data-ttu-id="89ce3-227">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="89ce3-227">Next steps</span></span>

<span data-ttu-id="89ce3-228">Если вы используете адаптивную карту или внедренное представление веб-страницы без объекта, вам `taskInfo` необходимо:</span><span class="sxs-lookup"><span data-stu-id="89ce3-228">If you are using either an adaptive card or an embedded web view without a `taskInfo` object, you'll want to:</span></span>

* [<span data-ttu-id="89ce3-229">Создание модуля задачи и реагирование на него</span><span class="sxs-lookup"><span data-stu-id="89ce3-229">Create and respond with a task module</span></span>](~/messaging-extensions/how-to/action-commands/create-task-module.md)

<span data-ttu-id="89ce3-230">Если вы используете параметры или внедренное представление веб-страницы с объектом, следующим шагом будет `taskInfo` следующее:</span><span class="sxs-lookup"><span data-stu-id="89ce3-230">If you are using parameters or an embedded web view with a `taskInfo` object, the next step for you is to:</span></span>

* [<span data-ttu-id="89ce3-231">Реагирование на отправку модуля задачи</span><span class="sxs-lookup"><span data-stu-id="89ce3-231">Respond to task module submit</span></span>](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
