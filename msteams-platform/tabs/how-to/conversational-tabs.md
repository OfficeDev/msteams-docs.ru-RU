---
title: Создание вкладок бесед
author: laujan
description: Создание беседного чата подгруппы для вкладок канала
keywords: группы вкладок канал настраивается
ms.topic: conceptual
ms.author: lomeybur
ms.openlocfilehash: 4171265a3ef4ad917661e258dd7305f82411c5ef
ms.sourcegitcommit: 118f7261d313feeac5b398fef56a44bd90104b2f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/31/2021
ms.locfileid: "52709654"
---
# <a name="create-conversational-tabs"></a><span data-ttu-id="11ea7-104">Создание вкладок бесед</span><span class="sxs-lookup"><span data-stu-id="11ea7-104">Create conversational tabs</span></span>

<span data-ttu-id="11ea7-105">Беседные под-сущности предоставляют пользователям возможность бесед о под-сущностям на вкладке, например о конкретных задачах, пациентах и возможности продаж, а не обсуждать всю вкладку, также известная как сущность.</span><span class="sxs-lookup"><span data-stu-id="11ea7-105">Conversational sub-entities provides a way to allow users to have conversations about sub-entities in your tab, such as specific task, patient, and sales opportunity, instead of discussing the entire tab, also known as entity.</span></span> <span data-ttu-id="11ea7-106">Традиционный канал или настраиваемая вкладка позволяют пользователю беседу о вкладке, но пользователю может потребоваться более целенаправленный разговор.</span><span class="sxs-lookup"><span data-stu-id="11ea7-106">A traditional channel or configurable tab allows the user to have a conversation about a tab, but the user may want a more focused conversation.</span></span> <span data-ttu-id="11ea7-107">Может возникнуть требование для более целенаправленного разговора, если слишком много контента, чтобы иметь централизованную дискуссию, или содержимое со временем изменилось, что делает беседу неактуальной для показанного контента.</span><span class="sxs-lookup"><span data-stu-id="11ea7-107">The requirement for a more focused conversation can arise either, if there is too much content to have a centralized discussion or the content changed over time, making the conversation irrelevant to the content being shown.</span></span> <span data-ttu-id="11ea7-108">Беседные подуряды предоставляют гораздо более целенаправленный диалог для динамических вкладок.</span><span class="sxs-lookup"><span data-stu-id="11ea7-108">Conversational sub-entities provides a much more focused conversation experience for dynamic tabs.</span></span>

<span data-ttu-id="11ea7-109">Беседные подуряды поддерживаются только в каналах.</span><span class="sxs-lookup"><span data-stu-id="11ea7-109">Conversational sub-entities are only supported in channels.</span></span> <span data-ttu-id="11ea7-110">Однако их можно использовать с личной или статической вкладки для  создания или продолжения бесед на вкладке, которая уже закреплена на канале.</span><span class="sxs-lookup"><span data-stu-id="11ea7-110">However, they can be used from a personal or static tab to create or continue conversations in tabs that are *already* pinned to a channel.</span></span> <span data-ttu-id="11ea7-111">Статическая вкладка полезна, если вы хотите предоставить пользователю одно расположение для просмотра и доступа к беседам, происходящим по нескольким каналам.</span><span class="sxs-lookup"><span data-stu-id="11ea7-111">The static tab is useful if you wish to provide one location for a user to view and access conversations happening across multiple channels.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="11ea7-112">Предварительные условия</span><span class="sxs-lookup"><span data-stu-id="11ea7-112">Prerequisites</span></span>

<span data-ttu-id="11ea7-113">Чтобы поддерживать беседные подуч. веб-приложение вкладки должно иметь возможность хранить сопоставление между ↔ беседами в базе данных backend.</span><span class="sxs-lookup"><span data-stu-id="11ea7-113">In order to support conversational sub-entities, your tab web application must have the ability to store a mapping between sub-entities ↔ conversations in a backend database.</span></span> <span data-ttu-id="11ea7-114">Мы предоставляем вам, но это будет ваша ответственность, чтобы сохранить это и вернуть его в Teams для того, чтобы пользователи `conversationId` `conversationId` продолжили разговор.</span><span class="sxs-lookup"><span data-stu-id="11ea7-114">We will provide you with the `conversationId`, but it will be your responsibility to store that `conversationId` and return it to Teams in order for users to continue the conversation.</span></span>

## <a name="start-a-new-conversation"></a><span data-ttu-id="11ea7-115">Начало нового разговора</span><span class="sxs-lookup"><span data-stu-id="11ea7-115">Start a new conversation</span></span>

<span data-ttu-id="11ea7-116">Чтобы начать новый разговор, используйте `openConversation()` функцию.</span><span class="sxs-lookup"><span data-stu-id="11ea7-116">To start a new conversation, you use the `openConversation()` function.</span></span> <span data-ttu-id="11ea7-117">При запуске и продолжении беседы все обрабатываются этим методом, однако входы в функцию изменяются в зависимости от действий, которые необходимо принять.</span><span class="sxs-lookup"><span data-stu-id="11ea7-117">Starting and continuing a conversation are all handled by this method, however, the inputs to the function change depending on which action you want to take.</span></span> <span data-ttu-id="11ea7-118">С точки зрения пользователей это открывает панель бесед справа от экрана, чтобы начать беседу или продолжить беседу.</span><span class="sxs-lookup"><span data-stu-id="11ea7-118">From the users perspective, this opens the conversation panel to the right of the screen, either to initiate a conversation or continue a conversation.</span></span>

``` javascript
microsoftTeams.conversations.openConversation(openConversationRequest);
```

<span data-ttu-id="11ea7-119">**openConversation** принимает следующие входные данные для начала беседы в канале:</span><span class="sxs-lookup"><span data-stu-id="11ea7-119">**openConversation** takes the following inputs to start a conversation in a channel:</span></span>

* <span data-ttu-id="11ea7-120">**subEntityId.** Это ID конкретной подгруппы.</span><span class="sxs-lookup"><span data-stu-id="11ea7-120">**subEntityId**: This is the ID of your specific sub-entity.</span></span> <span data-ttu-id="11ea7-121">Например, задача-123.</span><span class="sxs-lookup"><span data-stu-id="11ea7-121">For example, task-123.</span></span>
* <span data-ttu-id="11ea7-122">**entityId.** Это ID экземпляра вкладки, когда он был создан.</span><span class="sxs-lookup"><span data-stu-id="11ea7-122">**entityId**: This is the ID of the tab instance when it was created.</span></span> <span data-ttu-id="11ea7-123">ID имеет важное значение для ссылки на тот же экземпляр вкладки.</span><span class="sxs-lookup"><span data-stu-id="11ea7-123">The ID is important to refer back to the same tab instance.</span></span>
* <span data-ttu-id="11ea7-124">**channelId.** Это канал, в котором находится экземпляр вкладки.</span><span class="sxs-lookup"><span data-stu-id="11ea7-124">**channelId**: This is the channel in which the tab instance resides.</span></span>
   > [!NOTE]
   > <span data-ttu-id="11ea7-125">ChannelId **необязателен** для вкладок канала.</span><span class="sxs-lookup"><span data-stu-id="11ea7-125">The **channelId** is optional for channel tabs.</span></span> <span data-ttu-id="11ea7-126">Однако рекомендуется сохранить реализацию по каналам и статическим вкладкам одинаково.</span><span class="sxs-lookup"><span data-stu-id="11ea7-126">However, it is recommended if you wish to keep your implementation across channel and static tabs the same.</span></span>
* <span data-ttu-id="11ea7-127">**название.** Это название, которое отображается пользователю в панели чата.</span><span class="sxs-lookup"><span data-stu-id="11ea7-127">**title**: This is the title that is shown to the user in the chat panel.</span></span>

<span data-ttu-id="11ea7-128">Большинство из этих значений также можно получить из `getContext` API.</span><span class="sxs-lookup"><span data-stu-id="11ea7-128">Most of these values can also be retrieved from the `getContext` API.</span></span>

```javascript
microsoftTeams.conversations.openConversation({“subEntityId”:”task-1”, “entityId”: “tabInstanceId-1”, “channelId”: ”19:baa6e71f65b948d189bf5c892baa8e5a@thread.skype”, “title”: "Task Title”});
```

<span data-ttu-id="11ea7-129">Это откроет панель беседы.</span><span class="sxs-lookup"><span data-stu-id="11ea7-129">This will open the conversation panel.</span></span>

![Сущностями conversationl - Начните беседу](~/assets/images/tabs/conversational-subentities/start-conversation.png)

<span data-ttu-id="11ea7-131">Если пользователь начинает беседу, важно прослушивать вызов этого события, чтобы получить и сохранить **conversationId:**</span><span class="sxs-lookup"><span data-stu-id="11ea7-131">If the user starts a conversation, it’s important to listen for the callback of that event in order to retrieve and save the **conversationId**:</span></span>

```javascript
microsoftTeams.conversations.onStartConversation = (conversationResponse) => {
    // console.log(conversationReponse.conversationId)
};
```

<span data-ttu-id="11ea7-132">Объект содержит сведения, связанные с только что `conversationReponse` запущенным разговором.</span><span class="sxs-lookup"><span data-stu-id="11ea7-132">The `conversationReponse` object contains information related to the conversation that was just started.</span></span> <span data-ttu-id="11ea7-133">Мы рекомендуем сохранить все свойства этого объекта отклика для повторного использования позже.</span><span class="sxs-lookup"><span data-stu-id="11ea7-133">We recommend you save all the properties of this response object for reuse later.</span></span>

## <a name="continue-a-conversation"></a><span data-ttu-id="11ea7-134">Продолжение беседы</span><span class="sxs-lookup"><span data-stu-id="11ea7-134">Continue a conversation</span></span>

<span data-ttu-id="11ea7-135">После начала беседы последующие вызовы требуют, чтобы вы также предоставили те же входные данные, что и при запуске нового разговора вкладки канала, но также включают `openConversation()` **в себя conversationId** [](#Starting a new channel tab conversation).</span><span class="sxs-lookup"><span data-stu-id="11ea7-135">After a conversation starts, subsequent calls to `openConversation()` requires that you also provide the same inputs as in [Starting a new channel tab conversation](#Starting a new channel tab conversation), but also include the **conversationId**.</span></span> <span data-ttu-id="11ea7-136">Панель бесед открывается для пользователя с учетом соответствующего разговора.</span><span class="sxs-lookup"><span data-stu-id="11ea7-136">The conversation panel opens for the user with the appropriate conversation in view.</span></span> <span data-ttu-id="11ea7-137">Пользователи могут видеть новые или входящие сообщения в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="11ea7-137">Users are able to see new or incoming messages in real-time.</span></span>

![Сущностями sub Conversationl — продолжить беседу](~/assets/images/tabs/conversational-subentities/continue-conversation.png)

## <a name="enhance-a-conversation"></a><span data-ttu-id="11ea7-139">Повышение эффективности беседы</span><span class="sxs-lookup"><span data-stu-id="11ea7-139">Enhance a conversation</span></span>

<span data-ttu-id="11ea7-140">Наконец, важно, чтобы вкладка потребляла [глубокие ссылки на подгруппу.](~/concepts/build-and-test/deep-links.md)</span><span class="sxs-lookup"><span data-stu-id="11ea7-140">Finally, it’s important that your tab consumes [deeplinks to your sub-entity](~/concepts/build-and-test/deep-links.md).</span></span> <span data-ttu-id="11ea7-141">Например, пользователь щелкнув глубокий буклет вкладки из беседы канала.</span><span class="sxs-lookup"><span data-stu-id="11ea7-141">For example, user clicking the tab chiclet deeplink from the channel conversation.</span></span> <span data-ttu-id="11ea7-142">Ожидается, что вы получите глубокую ссылку, откройте эту подгруппу, а затем откроете панель бесед для этого конкретного подуряда.</span><span class="sxs-lookup"><span data-stu-id="11ea7-142">The expected behavior is for you to receive the deeplink, open that sub-entity, and then open the conversation panel for that specific sub-entity.</span></span>

<span data-ttu-id="11ea7-143">Чтобы поддерживать беседующих суб-сущностям с личной или статической вкладки, вам не нужно ничего менять в своей реализации.</span><span class="sxs-lookup"><span data-stu-id="11ea7-143">To support conversational sub-entities from your personal or static tab, you do not have to change anything about your implementation.</span></span> <span data-ttu-id="11ea7-144">Мы поддерживаем только начало или продолжение бесед со вкладок канала, которые уже закреплены.</span><span class="sxs-lookup"><span data-stu-id="11ea7-144">We only support starting or continuing conversations from channel tabs that are already pinned.</span></span> <span data-ttu-id="11ea7-145">Поддержка статических вкладок позволяет предоставить пользователям единое расположение для взаимодействия со всеми подуч.</span><span class="sxs-lookup"><span data-stu-id="11ea7-145">Supporting static tabs allow you to provide a single location for your users to interact with all your sub-entities.</span></span> <span data-ttu-id="11ea7-146">Однако при открытии представления беседы на статической вкладке важно сохранить вкладку , и когда вкладка изначально создается в канале, чтобы иметь правильные `subEntityId` `entityId` `channelId` свойства.</span><span class="sxs-lookup"><span data-stu-id="11ea7-146">It is, however, important that you save the `subEntityId`, `entityId`, and `channelId` when your tab is originally created in a channel in order for you to have the right properties when opening the conversation view in a static tab.</span></span>

## <a name="close-a-conversation"></a><span data-ttu-id="11ea7-147">Закрыть беседу</span><span class="sxs-lookup"><span data-stu-id="11ea7-147">Close a conversation</span></span>

<span data-ttu-id="11ea7-148">Можно вручную закрыть представление беседы, позвонив в `closeConversation()` функцию.</span><span class="sxs-lookup"><span data-stu-id="11ea7-148">You can manually close the conversation view by calling the `closeConversation()` function.</span></span>

```javascript
microsoftTeams.conversations.closeConversation();
```

<span data-ttu-id="11ea7-149">Вы также можете прослушивать событие, когда пользователь закрывает представление беседы.</span><span class="sxs-lookup"><span data-stu-id="11ea7-149">You can also listen for an event when the conversation view is closed by a user.</span></span>

```javascript
microsoftTeams.conversations.onCloseConversation = (conversationResponse) => {
    // console.log(conversationResponse)
};
```
