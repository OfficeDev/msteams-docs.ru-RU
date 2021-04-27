---
title: Определение команд действий расширения обмена сообщениями
author: clearab
description: Обзор команд действий расширения обмена сообщениями
localization_priority: Normal
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: f49e821ecb98659b4cfd68f93b37f1a8f611a9fb
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020718"
---
# <a name="define-messaging-extension-action-commands"></a><span data-ttu-id="915f0-103">Определение команд действий расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="915f0-103">Define messaging extension action commands</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="915f0-104">Команды действий позволяют представить пользователям модальный всплывающий модуль, называемый модулем задач в Teams.</span><span class="sxs-lookup"><span data-stu-id="915f0-104">Action commands allow you to present your users with a modal popup called a task module in Teams.</span></span> <span data-ttu-id="915f0-105">Модуль задач собирает или отображает сведения, обрабатывает взаимодействие и отправляет информацию обратно в Teams.</span><span class="sxs-lookup"><span data-stu-id="915f0-105">The task module collects or displays information, processes the interaction and sends the information back to Teams.</span></span> <span data-ttu-id="915f0-106">В этом документе приводятся инструкции по выбору расположения команд действий, созданию модуля задач, отправке окончательного сообщения или карточки, созданию команды действий с помощью студии приложения или созданию его вручную.</span><span class="sxs-lookup"><span data-stu-id="915f0-106">This document guides you on how to select action command invoke locations, create your task module, send final message, or card, create action command using app studio, or create it manually.</span></span> 

<span data-ttu-id="915f0-107">Перед созданием команды действий необходимо определиться со следующими факторами:</span><span class="sxs-lookup"><span data-stu-id="915f0-107">Before creating the action command you must decide the following factors:</span></span>

1. [<span data-ttu-id="915f0-108">Откуда можно запускать команду действий?</span><span class="sxs-lookup"><span data-stu-id="915f0-108">Where can the action command be triggered from?</span></span>](#select-action-command-invoke-locations)
1. [<span data-ttu-id="915f0-109">Как будет создан модуль задач?</span><span class="sxs-lookup"><span data-stu-id="915f0-109">How will the task module be created?</span></span>](#select-how-to-create-your-task-module)
1. [<span data-ttu-id="915f0-110">Будет ли отправлено окончательное сообщение или карточка в канал от бота, или сообщение или карточка будут вставлены в область композитного сообщения для отправки пользователем?</span><span class="sxs-lookup"><span data-stu-id="915f0-110">Will the final message or card be sent to the channel from a bot, or will the message or card be inserted into the compose message area for the user to submit?</span></span>](#select-how-the-final-message-is-sent)

## <a name="select-action-command-invoke-locations"></a><span data-ttu-id="915f0-111">Выберите расположения команд действий, вызываемой</span><span class="sxs-lookup"><span data-stu-id="915f0-111">Select action command invoke locations</span></span>

<span data-ttu-id="915f0-112">Сначала необходимо определить расположение, откуда должна вызываться команда действий.</span><span class="sxs-lookup"><span data-stu-id="915f0-112">First, you must decide the location from where your action command must be invoked.</span></span> <span data-ttu-id="915f0-113">Указав манифест приложения, можно вызвать команду из одного или нескольких `context` следующих местоположений:</span><span class="sxs-lookup"><span data-stu-id="915f0-113">By specifying the `context` in your app manifest, your command can be invoked from one or more of the following locations:</span></span>

* <span data-ttu-id="915f0-114">Область составить сообщение. Кнопки в нижней части области составить сообщение.</span><span class="sxs-lookup"><span data-stu-id="915f0-114">Compose message area: The buttons at the bottom of the compose message area.</span></span>
* <span data-ttu-id="915f0-115">Командный окне. @mentioning приложение в командном окне.</span><span class="sxs-lookup"><span data-stu-id="915f0-115">Command box: By @mentioning your app in the command box.</span></span> 
   > [!NOTE]
   > <span data-ttu-id="915f0-116">Если расширение обмена сообщениями вызывается из командного окна, вы не можете отвечать сообщением бота, вставленным непосредственно в беседу.</span><span class="sxs-lookup"><span data-stu-id="915f0-116">If messaging extension is invoked from the command box, you cannot respond with a bot message inserted directly into the conversation.</span></span>

* <span data-ttu-id="915f0-117">Сообщение. Непосредственно из существующего сообщения через меню `...` переполнения сообщения.</span><span class="sxs-lookup"><span data-stu-id="915f0-117">Message: Directly from an existing message through the `...` overflow menu on a message.</span></span> 
    > [!NOTE] 
    > <span data-ttu-id="915f0-118">Начальный вызов бота включает объект JSON, содержащий сообщение, из которого он был вызван.</span><span class="sxs-lookup"><span data-stu-id="915f0-118">The initial invoke to your bot includes a JSON object containing the message from which it was invoked.</span></span> <span data-ttu-id="915f0-119">Вы можете обработать сообщение перед тем, как представить его с помощью модуля задач.</span><span class="sxs-lookup"><span data-stu-id="915f0-119">You can process the message before presenting them with a task module.</span></span>

<span data-ttu-id="915f0-120">На следующем изображении отображаются расположения, из которых вызывается команда действий:</span><span class="sxs-lookup"><span data-stu-id="915f0-120">The following image displays the locations from where action command is invoked:</span></span>

![Команда действий вызывает расположения](~/assets/images/messaging-extension-invoke-locations.png)

## <a name="select-how-to-create-your-task-module"></a><span data-ttu-id="915f0-122">Выберите, как создать модуль задач</span><span class="sxs-lookup"><span data-stu-id="915f0-122">Select how to create your task module</span></span>

<span data-ttu-id="915f0-123">Помимо выбора, из чего можно вызвать команду, необходимо также выбрать, как заполнить форму в модуле задач для пользователей.</span><span class="sxs-lookup"><span data-stu-id="915f0-123">In addition to selecting where your command can be invoked from, you must also select how to populate the form in the task module for your users.</span></span> <span data-ttu-id="915f0-124">У вас есть следующие три варианта создания формы, отрисовываемой внутри модуля задач:</span><span class="sxs-lookup"><span data-stu-id="915f0-124">You have the following three options for creating the form that is rendered inside the task module:</span></span>   

* <span data-ttu-id="915f0-125">**Статический список параметров.** Это самый простой метод.</span><span class="sxs-lookup"><span data-stu-id="915f0-125">**Static list of parameters**: This is the simplest method.</span></span> <span data-ttu-id="915f0-126">Вы можете определить список параметров в манифесте клиента Teams, но в данном случае не можете управлять форматированием.</span><span class="sxs-lookup"><span data-stu-id="915f0-126">You can define a list of parameters in your app manifest the Teams client renders, but cannot control the formatting in this case.</span></span>
* <span data-ttu-id="915f0-127">**Адаптивная** карта. Можно выбрать адаптивную карту, которая обеспечивает более полный контроль над пользовательским интерфейсом, но по-прежнему ограничивает доступные параметры управления и форматирования.</span><span class="sxs-lookup"><span data-stu-id="915f0-127">**Adaptive Card**:  You can select to use an Adaptive Card, which provides greater control over the UI, but still limits you on the available controls and formatting options.</span></span>
* <span data-ttu-id="915f0-128">**Встроенное представление** веб-сайта. Вы можете встраить настраиваемый веб-просмотр в модуль задач, чтобы иметь полный контроль над пользовательским интерфейсом и средствами управления.</span><span class="sxs-lookup"><span data-stu-id="915f0-128">**Embedded web view**: You can select to embed a custom web view in the task module to have a complete control over the UI and controls.</span></span> 

<span data-ttu-id="915f0-129">Если вы выберете для создания модуля задач со статическим списком параметров и при отправке пользователем модуля задач, будет вызвано расширение обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="915f0-129">If you select to create the task module with a static list of parameters and when the user submits the task module, the messaging extension is called.</span></span> <span data-ttu-id="915f0-130">При использовании встроенного веб-представления или адаптивной карты расширение обмена сообщениями должно обрабатывать начальное событие вызова от пользователя, создавать модуль задач и возвращать его клиенту.</span><span class="sxs-lookup"><span data-stu-id="915f0-130">When using an embedded web view or an Adaptive Card, your messaging extension must handle an initial invoke event from the user, create the task module, and return it back to the client.</span></span>

## <a name="select-how-the-final-message-is-sent"></a><span data-ttu-id="915f0-131">Выберите, как отправляется окончательное сообщение</span><span class="sxs-lookup"><span data-stu-id="915f0-131">Select how the final message is sent</span></span>

<span data-ttu-id="915f0-132">В большинстве случаев команда действий приводит к вставки карты в поле составить сообщение.</span><span class="sxs-lookup"><span data-stu-id="915f0-132">In most cases, the action command results in a card inserted into the compose message box.</span></span> <span data-ttu-id="915f0-133">Пользователь может отправить его в канал или чат.</span><span class="sxs-lookup"><span data-stu-id="915f0-133">The user can send it into the channel or chat.</span></span> <span data-ttu-id="915f0-134">В этом случае сообщение поступает от пользователя, и бот не может изменить или обновить карту далее.</span><span class="sxs-lookup"><span data-stu-id="915f0-134">In this case, the message comes from the user, and the bot cannot edit or update the card further.</span></span>

<span data-ttu-id="915f0-135">Если расширение обмена сообщениями вызывается из окна составить или непосредственно из сообщения, веб-служба может вставить окончательный ответ непосредственно в канал или чат.</span><span class="sxs-lookup"><span data-stu-id="915f0-135">If the messaging extension is invoked from the compose box or directly from a message, your web service can insert the final response directly into the channel or chat.</span></span> <span data-ttu-id="915f0-136">В этом случае адаптивная карта поступает от бота, бот обновляет ее и при необходимости отвечает на поток беседы.</span><span class="sxs-lookup"><span data-stu-id="915f0-136">In this case, the Adaptive Card comes from the bot, the bot updates it, and replies to the conversation thread if needed.</span></span> <span data-ttu-id="915f0-137">Необходимо добавить объект в манифест приложения с помощью того же `bot` ID и определить соответствующие области.</span><span class="sxs-lookup"><span data-stu-id="915f0-137">You must add the `bot` object to the app manifest using  the same ID and defining the appropriate scopes.</span></span>

## <a name="add-the-action-command-to-your-app-manifest"></a><span data-ttu-id="915f0-138">Добавление команды действий в манифест приложения</span><span class="sxs-lookup"><span data-stu-id="915f0-138">Add the action command to your app manifest</span></span>

<span data-ttu-id="915f0-139">Чтобы добавить команду действий в манифест приложения, необходимо добавить новый объект на верхний уровень `composeExtension` манифеста приложения JSON.</span><span class="sxs-lookup"><span data-stu-id="915f0-139">To add the action command to the app manifest, you must add a new `composeExtension` object to the top level of the app manifest JSON.</span></span> <span data-ttu-id="915f0-140">Для этого можно использовать один из следующих способов:</span><span class="sxs-lookup"><span data-stu-id="915f0-140">You can use one of the following ways to do so:</span></span>

* [<span data-ttu-id="915f0-141">Создание команды действий с помощью App Studio</span><span class="sxs-lookup"><span data-stu-id="915f0-141">Create an action command using App Studio</span></span>](#create-an-action-command-using-app-studio)
* [<span data-ttu-id="915f0-142">Создание команды действий вручную</span><span class="sxs-lookup"><span data-stu-id="915f0-142">Create an action command manually</span></span>](#create-an-action-command-manually)

### <a name="create-an-action-command-using-app-studio"></a><span data-ttu-id="915f0-143">Создание команды действий с помощью App Studio</span><span class="sxs-lookup"><span data-stu-id="915f0-143">Create an action command using App Studio</span></span>

> [!NOTE]
> <span data-ttu-id="915f0-144">Обязательным условием для создания команды действий является то, что вы уже создали расширение обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="915f0-144">The prerequisite to create an action command is that you have already created a messaging extension.</span></span> <span data-ttu-id="915f0-145">Сведения о создании расширения обмена сообщениями см. в сообщении о создании расширения [обмена сообщениями.](~/messaging-extensions/how-to/create-messaging-extension.md)</span><span class="sxs-lookup"><span data-stu-id="915f0-145">For information on how to create a messaging extension, see [create a messaging extension](~/messaging-extensions/how-to/create-messaging-extension.md).</span></span>

<span data-ttu-id="915f0-146">**Создание команды действий**</span><span class="sxs-lookup"><span data-stu-id="915f0-146">**To create an action command**</span></span>

1. <span data-ttu-id="915f0-147">Откройте **App Studio** от клиента Microsoft Teams и выберите вкладку Редактор **Манифеста.**</span><span class="sxs-lookup"><span data-stu-id="915f0-147">Open **App Studio** from the Microsoft Teams client and select the **Manifest editor** tab.</span></span>
1. <span data-ttu-id="915f0-148">Если вы уже создали пакет приложений в **App Studio,** выберите его из списка.</span><span class="sxs-lookup"><span data-stu-id="915f0-148">If you already created your app package in **App Studio**, select it from the list.</span></span> <span data-ttu-id="915f0-149">Если вы не создали пакет приложений, импортировать существующий пакет.</span><span class="sxs-lookup"><span data-stu-id="915f0-149">If you have not created an app package, import an existing one.</span></span>
1. <span data-ttu-id="915f0-150">После импорта пакета приложений выберите расширения **обмена** сообщениями в **статье Capabilities.**</span><span class="sxs-lookup"><span data-stu-id="915f0-150">After importing an app package, select **Messaging extensions** under **Capabilities**.</span></span> <span data-ttu-id="915f0-151">Вы получите всплывающее окно, чтобы настроить расширение обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="915f0-151">You get a pop-up window to set up the messaging extension.</span></span>
1. <span data-ttu-id="915f0-152">Выберите **Настройка в** окне, чтобы включить расширение обмена сообщениями в приложение.</span><span class="sxs-lookup"><span data-stu-id="915f0-152">Select **Set up** in the window to include the messaging extension in your app experience.</span></span> <span data-ttu-id="915f0-153">На следующем изображении отображается окно расширения обмена сообщениями:</span><span class="sxs-lookup"><span data-stu-id="915f0-153">The following image displays the messaging extension set up window:</span></span>

    <img src="~/assets/images/messaging-extension/messaging-extension-set-up.png" alt="messaging extension set up" width="500"/>
    
1. <span data-ttu-id="915f0-154">Для создания расширения обмена сообщениями необходим зарегистрированный бот Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="915f0-154">To create a messaging extension, you need a Microsoft registered bot.</span></span> <span data-ttu-id="915f0-155">Можно использовать существующий бот или создать новый бот.</span><span class="sxs-lookup"><span data-stu-id="915f0-155">You can either use an existing bot or create a new bot.</span></span> <span data-ttu-id="915f0-156">Выберите **создание нового варианта бота,** назови имя нового бота и выберите **Create**.</span><span class="sxs-lookup"><span data-stu-id="915f0-156">Select **Create new bot** option, give a name for the new bot, and select **Create**.</span></span> <span data-ttu-id="915f0-157">На следующем изображении отображается создание бота для расширения обмена сообщениями:</span><span class="sxs-lookup"><span data-stu-id="915f0-157">The following image displays bot creation for messaging extension:</span></span>

    <img src="~/assets/images/messaging-extension/create-bot-for-messaging-extension.png" alt="create bot for messaging extension" width="500"/>

1. <span data-ttu-id="915f0-158">Выберите **Добавить** в **разделе Команда** страницы расширения обмена сообщениями, чтобы включить команды, которые решают поведение расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="915f0-158">Select **Add** in the **Command section** of the messaging extensions page to include the commands which decides the behaviour of messaging extension.</span></span>   
<span data-ttu-id="915f0-159">На следующем изображении отображается добавление команд для расширения обмена сообщениями:</span><span class="sxs-lookup"><span data-stu-id="915f0-159">The following image displays command addition for messaging extension:</span></span>

   <img src="~/assets/images/messaging-extension/include-command.png" alt="include command" width="500"/>

1. <span data-ttu-id="915f0-160">Выберите **Разрешить пользователям запускать действия во внешних службах, находясь внутри Teams.**</span><span class="sxs-lookup"><span data-stu-id="915f0-160">Select **Allow users to trigger actions in external services while inside of Teams**.</span></span> <span data-ttu-id="915f0-161">На следующем изображении отображается выбор команд действий:</span><span class="sxs-lookup"><span data-stu-id="915f0-161">The following image displays the action command selection:</span></span>

    <img src="~/assets/images/messaging-extension/action-command-selection.png" alt="action command selection" width="500"/>
    
1. <span data-ttu-id="915f0-162">Чтобы использовать статический набор параметров для создания модуля задач, выберите Определение набора статических параметров **для команды.**</span><span class="sxs-lookup"><span data-stu-id="915f0-162">To use a static set of parameters to create your task module, select **Define a set of static parameters for the command**.</span></span> 

    <span data-ttu-id="915f0-163">На следующем изображении отображается выбор статических параметров команды действий:</span><span class="sxs-lookup"><span data-stu-id="915f0-163">The following image displays the action command static parameter selection:</span></span>

   <img src="~/assets/images/messaging-extension/action-command-static-parameter-selection.png" alt="action command static parameter selection" width="500"/> 
   
    <span data-ttu-id="915f0-164">На следующем изображении отображается пример статического параметра:</span><span class="sxs-lookup"><span data-stu-id="915f0-164">The following image displays an example static parameter set-up:</span></span> 

   <img src="~/assets/images/messaging-extension/setting-up-of-static-parameter.png" alt="action command static parameter set-up" width="500"/>

    <span data-ttu-id="915f0-165">На следующем изображении отображается пример тестирования статических параметров:</span><span class="sxs-lookup"><span data-stu-id="915f0-165">The following image displays an example static parameter testing:</span></span>

   <img src="~/assets/images/messaging-extension/static-parameter-testing.png" alt="action command static parameter testing" width="500"/>

1. <span data-ttu-id="915f0-166">Чтобы использовать динамические параметры, выберите для получения динамического набора **параметров из бота.**</span><span class="sxs-lookup"><span data-stu-id="915f0-166">To use dynamic parameters, select to **Fetch a dynamic set of parameters from your bot**.</span></span> <span data-ttu-id="915f0-167">На следующем изображении отображается выбор параметров команды действий:</span><span class="sxs-lookup"><span data-stu-id="915f0-167">The following image displays the action command parameter selection:</span></span>

    <img src="~/assets/images/messaging-extension/action-command-dynamic-parameter-selection.png" alt="action command dynamic parameter selection" width="500"/>
    
1. <span data-ttu-id="915f0-168">Добавление **командного и** **заголовок**.</span><span class="sxs-lookup"><span data-stu-id="915f0-168">Add a **Command Id** and a **Title**.</span></span>
1. <span data-ttu-id="915f0-169">Выберите расположение, в котором необходимо вызвать команду действий.</span><span class="sxs-lookup"><span data-stu-id="915f0-169">Select the location from where you want to invoke the action command.</span></span> <span data-ttu-id="915f0-170">На следующем изображении отображается расположение вызова команды действий:</span><span class="sxs-lookup"><span data-stu-id="915f0-170">The following image displays the action command invoke location:</span></span>

    <img src="~/assets/images/messaging-extension/action-command-invoke-location.png" alt="action command invoke location" width="500"/>

1. <span data-ttu-id="915f0-171">Нажмите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="915f0-171">Select **Save**.</span></span>
1. <span data-ttu-id="915f0-172">Чтобы добавить дополнительные параметры, выберите кнопку **Добавить** в разделе **Параметры.**</span><span class="sxs-lookup"><span data-stu-id="915f0-172">To add more parameters, select the **Add** button in the **Parameters** section.</span></span>

### <a name="create-an-action-command-manually"></a><span data-ttu-id="915f0-173">Создание команды действий вручную</span><span class="sxs-lookup"><span data-stu-id="915f0-173">Create an action command manually</span></span>

<span data-ttu-id="915f0-174">Чтобы вручную добавить команду расширения обмена сообщениями на основе действий в манифест приложения, необходимо добавить в массив объектов следующие `composeExtension.commands` параметры:</span><span class="sxs-lookup"><span data-stu-id="915f0-174">To manually add your action-based messaging extension command to your app manifest, you must add the following parameters to the `composeExtension.commands` array of objects:</span></span>

| <span data-ttu-id="915f0-175">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="915f0-175">Property name</span></span> | <span data-ttu-id="915f0-176">Назначение</span><span class="sxs-lookup"><span data-stu-id="915f0-176">Purpose</span></span> | <span data-ttu-id="915f0-177">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="915f0-177">Required?</span></span> | <span data-ttu-id="915f0-178">Минимальная версия манифеста</span><span class="sxs-lookup"><span data-stu-id="915f0-178">Minimum manifest version</span></span> |
|---|---|---|---|
| `id` | <span data-ttu-id="915f0-179">Это свойство — уникальный ID, который вы назначаете этой команде.</span><span class="sxs-lookup"><span data-stu-id="915f0-179">This property is an unique ID that you assign to this command.</span></span> <span data-ttu-id="915f0-180">Запрос пользователя включает этот ID.</span><span class="sxs-lookup"><span data-stu-id="915f0-180">The user request includes this ID.</span></span> | <span data-ttu-id="915f0-181">Да</span><span class="sxs-lookup"><span data-stu-id="915f0-181">Yes</span></span> | <span data-ttu-id="915f0-182">1.0</span><span class="sxs-lookup"><span data-stu-id="915f0-182">1.0</span></span> |
| `title` | <span data-ttu-id="915f0-183">Это свойство — командное имя.</span><span class="sxs-lookup"><span data-stu-id="915f0-183">This property is a command name.</span></span> <span data-ttu-id="915f0-184">Это значение отображается в пользовательском интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="915f0-184">This value appears in the UI.</span></span> | <span data-ttu-id="915f0-185">Да</span><span class="sxs-lookup"><span data-stu-id="915f0-185">Yes</span></span> | <span data-ttu-id="915f0-186">1.0</span><span class="sxs-lookup"><span data-stu-id="915f0-186">1.0</span></span> |
| `type` | <span data-ttu-id="915f0-187">Это свойство должно быть `action` .</span><span class="sxs-lookup"><span data-stu-id="915f0-187">This property must be an `action`.</span></span> | <span data-ttu-id="915f0-188">Нет</span><span class="sxs-lookup"><span data-stu-id="915f0-188">No</span></span> | <span data-ttu-id="915f0-189">1.4</span><span class="sxs-lookup"><span data-stu-id="915f0-189">1.4</span></span> |
| `fetchTask` | <span data-ttu-id="915f0-190">Это свойство предназначено для адаптивной карты или встроенного веб-представления для модуля задач, а также для статичного списка параметров или при загрузке `true` `false` веб-представления с помощью `taskInfo` .</span><span class="sxs-lookup"><span data-stu-id="915f0-190">This property is set to `true` for an adaptive card or embedded web view for your task module, and`false` for a static list of parameters or when loading the web view by a `taskInfo`.</span></span> | <span data-ttu-id="915f0-191">Нет</span><span class="sxs-lookup"><span data-stu-id="915f0-191">No</span></span> | <span data-ttu-id="915f0-192">1.4</span><span class="sxs-lookup"><span data-stu-id="915f0-192">1.4</span></span> |
| `context` | <span data-ttu-id="915f0-193">Это свойство — необязательный массив значений, определяющий, откуда вызывается расширение обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="915f0-193">This property is an optional array of values that defines where the messaging extension is invoked from.</span></span> <span data-ttu-id="915f0-194">Возможные значения — `message`, `compose` и `commandBox`.</span><span class="sxs-lookup"><span data-stu-id="915f0-194">The possible values are `message`, `compose`, or `commandBox`.</span></span> <span data-ttu-id="915f0-195">Значение по умолчанию — `["compose", "commandBox"]`.</span><span class="sxs-lookup"><span data-stu-id="915f0-195">The default value is `["compose", "commandBox"]`.</span></span> | <span data-ttu-id="915f0-196">Нет</span><span class="sxs-lookup"><span data-stu-id="915f0-196">No</span></span> | <span data-ttu-id="915f0-197">1.5</span><span class="sxs-lookup"><span data-stu-id="915f0-197">1.5</span></span> |

<span data-ttu-id="915f0-198">Если используется статический список параметров, необходимо также добавить следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="915f0-198">If you are using a static list of parameters, you must also add the following parameters:</span></span>

| <span data-ttu-id="915f0-199">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="915f0-199">Property name</span></span> | <span data-ttu-id="915f0-200">Назначение</span><span class="sxs-lookup"><span data-stu-id="915f0-200">Purpose</span></span> | <span data-ttu-id="915f0-201">Требуется?</span><span class="sxs-lookup"><span data-stu-id="915f0-201">Is required?</span></span> | <span data-ttu-id="915f0-202">Минимальная версия манифеста</span><span class="sxs-lookup"><span data-stu-id="915f0-202">Minimum manifest version</span></span> |
|---|---|---|---|
| `parameters` | <span data-ttu-id="915f0-203">Это свойство описывает статический список параметров для команды.</span><span class="sxs-lookup"><span data-stu-id="915f0-203">This property describes the static list of parameters for the command.</span></span> <span data-ttu-id="915f0-204">Используйте только `fetchTask` `false` тогда, когда это .</span><span class="sxs-lookup"><span data-stu-id="915f0-204">Only use when `fetchTask` is `false`.</span></span> | <span data-ttu-id="915f0-205">Нет</span><span class="sxs-lookup"><span data-stu-id="915f0-205">No</span></span> | <span data-ttu-id="915f0-206">1.0</span><span class="sxs-lookup"><span data-stu-id="915f0-206">1.0</span></span> |
| `parameter.name` | <span data-ttu-id="915f0-207">Это свойство описывает имя параметра.</span><span class="sxs-lookup"><span data-stu-id="915f0-207">This property describes the name of the parameter.</span></span> <span data-ttu-id="915f0-208">Это отправляется в службу в запросе пользователя.</span><span class="sxs-lookup"><span data-stu-id="915f0-208">This is sent to your service in the user request.</span></span> | <span data-ttu-id="915f0-209">Да</span><span class="sxs-lookup"><span data-stu-id="915f0-209">Yes</span></span> | <span data-ttu-id="915f0-210">1.0</span><span class="sxs-lookup"><span data-stu-id="915f0-210">1.0</span></span> |
| `parameter.description` | <span data-ttu-id="915f0-211">Это свойство описывает цели параметра или пример значения, которое должно быть предоставлено.</span><span class="sxs-lookup"><span data-stu-id="915f0-211">This property describes the parameter’s purposes or example of the value that should be provided.</span></span> <span data-ttu-id="915f0-212">Это значение отображается в пользовательском интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="915f0-212">This value appears in the UI.</span></span> | <span data-ttu-id="915f0-213">Да</span><span class="sxs-lookup"><span data-stu-id="915f0-213">Yes</span></span> | <span data-ttu-id="915f0-214">1.0</span><span class="sxs-lookup"><span data-stu-id="915f0-214">1.0</span></span> |
| `parameter.title` | <span data-ttu-id="915f0-215">Это свойство — короткое удобное название параметра или метка.</span><span class="sxs-lookup"><span data-stu-id="915f0-215">This property is a short user-friendly parameter title or label.</span></span> | <span data-ttu-id="915f0-216">Да</span><span class="sxs-lookup"><span data-stu-id="915f0-216">Yes</span></span> | <span data-ttu-id="915f0-217">1.0</span><span class="sxs-lookup"><span data-stu-id="915f0-217">1.0</span></span> |
| `parameter.inputType` | <span data-ttu-id="915f0-218">Это свойство задалось типу входных данных.</span><span class="sxs-lookup"><span data-stu-id="915f0-218">This property is set to the type of input required.</span></span> <span data-ttu-id="915f0-219">Возможные значения включают `text` , , , , `textarea` `number` `date` `time` `toggle` .</span><span class="sxs-lookup"><span data-stu-id="915f0-219">The possible values include `text`, `textarea`, `number`, `date`, `time`, `toggle`.</span></span> <span data-ttu-id="915f0-220">По умолчанию установлено `text` значение .</span><span class="sxs-lookup"><span data-stu-id="915f0-220">The default value is set to `text`.</span></span> | <span data-ttu-id="915f0-221">Нет</span><span class="sxs-lookup"><span data-stu-id="915f0-221">No</span></span> | <span data-ttu-id="915f0-222">1.4</span><span class="sxs-lookup"><span data-stu-id="915f0-222">1.4</span></span> |

<span data-ttu-id="915f0-223">Если вы используете встроенное веб-представление, можно дополнительно добавить объект для получения веб-представления без вызова `taskInfo` бота напрямую.</span><span class="sxs-lookup"><span data-stu-id="915f0-223">If you are using an embedded web view, you can optionally add the `taskInfo` object to fetch your web view without calling your bot directly.</span></span> <span data-ttu-id="915f0-224">При выборе этого параметра поведение аналогично использованию статического списка параметров.</span><span class="sxs-lookup"><span data-stu-id="915f0-224">If you select this option, the behavior is similar to that of using a static list of parameters.</span></span> <span data-ttu-id="915f0-225">В том, что первое взаимодействие с ботом отвечает на действие отправки [модуля задач.](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)</span><span class="sxs-lookup"><span data-stu-id="915f0-225">In that the first interaction with your bot is [responding to the task module submit action](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md).</span></span> <span data-ttu-id="915f0-226">Если вы используете `taskInfo` объект, необходимо установить `fetchTask` параметр `false` .</span><span class="sxs-lookup"><span data-stu-id="915f0-226">If you are using a `taskInfo` object, you must set the `fetchTask` parameter to `false`.</span></span>

| <span data-ttu-id="915f0-227">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="915f0-227">Property name</span></span> | <span data-ttu-id="915f0-228">Назначение</span><span class="sxs-lookup"><span data-stu-id="915f0-228">Purpose</span></span> | <span data-ttu-id="915f0-229">Требуется?</span><span class="sxs-lookup"><span data-stu-id="915f0-229">Is required?</span></span> | <span data-ttu-id="915f0-230">Минимальная версия манифеста</span><span class="sxs-lookup"><span data-stu-id="915f0-230">Minimum manifest version</span></span> |
|---|---|---|---|
|`taskInfo`|<span data-ttu-id="915f0-231">Укажите модуль задач для предварительной загрузки при использовании команды расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="915f0-231">Specify the task module to preload when using a messaging extension command.</span></span> | <span data-ttu-id="915f0-232">Нет</span><span class="sxs-lookup"><span data-stu-id="915f0-232">No</span></span> | <span data-ttu-id="915f0-233">1.4</span><span class="sxs-lookup"><span data-stu-id="915f0-233">1.4</span></span> |
|`taskInfo.title`|<span data-ttu-id="915f0-234">Начальное название модуля задач.</span><span class="sxs-lookup"><span data-stu-id="915f0-234">Initial task module title.</span></span> |<span data-ttu-id="915f0-235">Нет</span><span class="sxs-lookup"><span data-stu-id="915f0-235">No</span></span> | <span data-ttu-id="915f0-236">1.4</span><span class="sxs-lookup"><span data-stu-id="915f0-236">1.4</span></span> |
|`taskInfo.width`|<span data-ttu-id="915f0-237">Ширина модуля задач, число пикселей или макет по умолчанию, например `large` `medium` , или `small` .</span><span class="sxs-lookup"><span data-stu-id="915f0-237">Task module width, either a number in pixels or default layout such as `large`, `medium`, or `small`.</span></span> |<span data-ttu-id="915f0-238">Нет</span><span class="sxs-lookup"><span data-stu-id="915f0-238">No</span></span> | <span data-ttu-id="915f0-239">1.4</span><span class="sxs-lookup"><span data-stu-id="915f0-239">1.4</span></span> |
|`taskInfo.height`|<span data-ttu-id="915f0-240">Высота модуля задач, число пикселей или макет по умолчанию, например `large` `medium` , или `small` .</span><span class="sxs-lookup"><span data-stu-id="915f0-240">Task module height, either a number in pixels or default layout such as `large`, `medium`, or `small`.</span></span>|<span data-ttu-id="915f0-241">Нет</span><span class="sxs-lookup"><span data-stu-id="915f0-241">No</span></span> | <span data-ttu-id="915f0-242">1.4</span><span class="sxs-lookup"><span data-stu-id="915f0-242">1.4</span></span> |
|`taskInfo.url`|<span data-ttu-id="915f0-243">Начальный URL-адрес веб-просмотра.</span><span class="sxs-lookup"><span data-stu-id="915f0-243">Initial web view URL.</span></span>|<span data-ttu-id="915f0-244">Нет</span><span class="sxs-lookup"><span data-stu-id="915f0-244">No</span></span> | <span data-ttu-id="915f0-245">1.4</span><span class="sxs-lookup"><span data-stu-id="915f0-245">1.4</span></span> | 

#### <a name="app-manifest-example"></a><span data-ttu-id="915f0-246">Пример манифеста приложения</span><span class="sxs-lookup"><span data-stu-id="915f0-246">App manifest example</span></span>

<span data-ttu-id="915f0-247">В следующем разделе приводится пример объекта, `composeExtensions` определяющий две команды действий.</span><span class="sxs-lookup"><span data-stu-id="915f0-247">The following section is an example of a `composeExtensions` object defining two action commands.</span></span> <span data-ttu-id="915f0-248">Это не пример полного манифеста.</span><span class="sxs-lookup"><span data-stu-id="915f0-248">It is not an example of the complete manifest.</span></span> <span data-ttu-id="915f0-249">Полную схему манифеста приложения см. в [схеме манифеста приложения:](~/resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="915f0-249">For the complete app manifest schema, see [app manifest schema](~/resources/schema/manifest-schema.md):</span></span>

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

## <a name="code-sample"></a><span data-ttu-id="915f0-250">Пример кода</span><span class="sxs-lookup"><span data-stu-id="915f0-250">Code sample</span></span>

| <span data-ttu-id="915f0-251">Имя образца</span><span class="sxs-lookup"><span data-stu-id="915f0-251">Sample Name</span></span>           | <span data-ttu-id="915f0-252">Описание</span><span class="sxs-lookup"><span data-stu-id="915f0-252">Description</span></span> | <span data-ttu-id="915f0-253">.NET</span><span class="sxs-lookup"><span data-stu-id="915f0-253">.NET</span></span>    | <span data-ttu-id="915f0-254">Node.js</span><span class="sxs-lookup"><span data-stu-id="915f0-254">Node.js</span></span>   |   
|:---------------------|:--------------|:---------|:--------|
|<span data-ttu-id="915f0-255">Действие расширения обмена сообщениями teams</span><span class="sxs-lookup"><span data-stu-id="915f0-255">Teams messaging extension action</span></span>| <span data-ttu-id="915f0-256">Описывает, как определить команды действий, создать модуль задач и реагировать на отправку действия модуля задач.</span><span class="sxs-lookup"><span data-stu-id="915f0-256">Describes how to define action commands, create task module, and  respond to task module submit action.</span></span> |[<span data-ttu-id="915f0-257">View</span><span class="sxs-lookup"><span data-stu-id="915f0-257">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[<span data-ttu-id="915f0-258">View</span><span class="sxs-lookup"><span data-stu-id="915f0-258">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | 
|<span data-ttu-id="915f0-259">Командный поиск расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="915f0-259">Teams messaging extension search</span></span>   |  <span data-ttu-id="915f0-260">Описывает, как определить команды поиска и реагировать на поиски.</span><span class="sxs-lookup"><span data-stu-id="915f0-260">Describes how to define search commands and respond to searches.</span></span>        |[<span data-ttu-id="915f0-261">View</span><span class="sxs-lookup"><span data-stu-id="915f0-261">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[<span data-ttu-id="915f0-262">View</span><span class="sxs-lookup"><span data-stu-id="915f0-262">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="next-step"></a><span data-ttu-id="915f0-263">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="915f0-263">Next step</span></span>

<span data-ttu-id="915f0-264">Если вы используете адаптивную карту или встроенное веб-представление без объекта, следующий шаг: `taskInfo`</span><span class="sxs-lookup"><span data-stu-id="915f0-264">If you are using either an Adaptive Card or an embedded web view without a `taskInfo` object, the next step is to:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="915f0-265">Создание и реагирование с помощью модуля задач</span><span class="sxs-lookup"><span data-stu-id="915f0-265">Create and respond with a task module</span></span>](~/messaging-extensions/how-to/action-commands/create-task-module.md)

<span data-ttu-id="915f0-266">Если вы используете параметры или встроенное веб-представление с `taskInfo` объектом, следующим шагом будет следующее:</span><span class="sxs-lookup"><span data-stu-id="915f0-266">If you are using the parameters or an embedded web view with a `taskInfo` object, the next step is to:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="915f0-267">Ответ на отправку модуля задач</span><span class="sxs-lookup"><span data-stu-id="915f0-267">Respond to task module submit</span></span>](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)

