---
title: Создание вкладок бесед
author: surbhigupta
description: Создание беседного чата подгруппы для вкладок канала
keywords: группы вкладок канал настраивается
ms.topic: conceptual
ms.author: lomeybur
ms.openlocfilehash: fbc5e90842c892cfb7e14f845563d7d2ffb397bb
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140266"
---
# <a name="create-conversational-tabs"></a><span data-ttu-id="bbf94-104">Создание вкладок бесед</span><span class="sxs-lookup"><span data-stu-id="bbf94-104">Create conversational tabs</span></span>

<span data-ttu-id="bbf94-105">Беседные под-сущности предоставляют пользователям возможность бесед о под-сущностям на вкладке, например о конкретных задачах, пациентах и возможности продаж, а не обсуждать всю вкладку, также известная как сущность.</span><span class="sxs-lookup"><span data-stu-id="bbf94-105">Conversational sub-entities provides a way to allow users to have conversations about sub-entities in your tab, such as specific task, patient, and sales opportunity, instead of discussing the entire tab, also known as entity.</span></span> <span data-ttu-id="bbf94-106">Традиционный канал или настраиваемая вкладка позволяют пользователю беседу о вкладке, но для этого требуется более целенаправленный разговор.</span><span class="sxs-lookup"><span data-stu-id="bbf94-106">A traditional channel or configurable tab allows the user to have a conversation about a tab, but the user requires a more focused conversation.</span></span> <span data-ttu-id="bbf94-107">Может возникнуть требование для более целенаправленного разговора, если слишком много контента, чтобы иметь централизованное обсуждение, или из-за того, что содержимое со временем изменилось, что делает беседу неактуальной для показанного контента.</span><span class="sxs-lookup"><span data-stu-id="bbf94-107">The requirement for a more focused conversation can arise either, if there is too much content to have a centralized discussion or because the content changed over time, making the conversation irrelevant to the content being shown.</span></span> <span data-ttu-id="bbf94-108">Беседные подуряды предоставляют гораздо более целенаправленный диалог для динамических вкладок.</span><span class="sxs-lookup"><span data-stu-id="bbf94-108">Conversational sub-entities provides a much more focused conversation experience for dynamic tabs.</span></span>

<span data-ttu-id="bbf94-109">Беседные подуряды поддерживаются только в каналах.</span><span class="sxs-lookup"><span data-stu-id="bbf94-109">Conversational sub-entities are only supported in channels.</span></span> <span data-ttu-id="bbf94-110">Их можно использовать с личной или статической вкладки для создания или продолжения бесед на вкладке, которая уже закреплена на канале.</span><span class="sxs-lookup"><span data-stu-id="bbf94-110">They can be used from a personal or static tab to create or continue conversations in tabs that are already pinned to a channel.</span></span> <span data-ttu-id="bbf94-111">Статическая вкладка полезна, если необходимо предоставить пользователю одно расположение для просмотра и доступа к беседам, происходящим по нескольким каналам.</span><span class="sxs-lookup"><span data-stu-id="bbf94-111">The static tab is useful if you want to provide one location for a user to view and access conversations happening across multiple channels.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bbf94-112">Необходимые условия</span><span class="sxs-lookup"><span data-stu-id="bbf94-112">Prerequisites</span></span>

<span data-ttu-id="bbf94-113">Чтобы поддерживать беседные подуч. веб-приложение вкладки должно иметь возможность хранить сопоставление между ↔ беседами в базе данных backend.</span><span class="sxs-lookup"><span data-stu-id="bbf94-113">In order to support conversational sub-entities, your tab web application must have the ability to store a mapping between sub-entities ↔ conversations in a backend database.</span></span> <span data-ttu-id="bbf94-114">При условии, но вы должны сохранить его и вернуть его в Teams для того, чтобы пользователи `conversationId` `conversationId` продолжили беседу.</span><span class="sxs-lookup"><span data-stu-id="bbf94-114">The `conversationId` is provided, but you must store that `conversationId` and return it to Teams in order for users to continue the conversation.</span></span>

## <a name="start-a-new-conversation"></a><span data-ttu-id="bbf94-115">Начало нового разговора</span><span class="sxs-lookup"><span data-stu-id="bbf94-115">Start a new conversation</span></span>

<span data-ttu-id="bbf94-116">Чтобы начать новый разговор, используйте `openConversation()` функцию.</span><span class="sxs-lookup"><span data-stu-id="bbf94-116">To start a new conversation, use the `openConversation()` function.</span></span> <span data-ttu-id="bbf94-117">Запуск и продолжение беседы обрабатываются этим методом.</span><span class="sxs-lookup"><span data-stu-id="bbf94-117">Starting and continuing a conversation are all handled by this method.</span></span> <span data-ttu-id="bbf94-118">Входные данные в функцию изменяются в зависимости от действий, которые необходимо принять.</span><span class="sxs-lookup"><span data-stu-id="bbf94-118">The inputs to the function change depending on which action you want to take.</span></span> <span data-ttu-id="bbf94-119">С точки зрения пользователей это открывает панель бесед справа от экрана, чтобы начать беседу или продолжить беседу.</span><span class="sxs-lookup"><span data-stu-id="bbf94-119">From the users perspective, this opens the conversation panel to the right of the screen, either to initiate a conversation or continue a conversation.</span></span>

``` javascript
microsoftTeams.conversations.openConversation(openConversationRequest);
```

<span data-ttu-id="bbf94-120">**openConversation** принимает следующие входные данные для начала беседы в канале:</span><span class="sxs-lookup"><span data-stu-id="bbf94-120">**openConversation** takes the following inputs to start a conversation in a channel:</span></span>

* <span data-ttu-id="bbf94-121">**subEntityId.** Это ID конкретной подгруппы.</span><span class="sxs-lookup"><span data-stu-id="bbf94-121">**subEntityId**: This is the ID of your specific sub-entity.</span></span> <span data-ttu-id="bbf94-122">Например, задача-123.</span><span class="sxs-lookup"><span data-stu-id="bbf94-122">For example, task-123.</span></span>
* <span data-ttu-id="bbf94-123">**entityId.** Это ID экземпляра вкладки, когда он был создан.</span><span class="sxs-lookup"><span data-stu-id="bbf94-123">**entityId**: This is the ID of the tab instance when it was created.</span></span> <span data-ttu-id="bbf94-124">ID имеет важное значение для ссылки на тот же экземпляр вкладки.</span><span class="sxs-lookup"><span data-stu-id="bbf94-124">The ID is important to refer back to the same tab instance.</span></span>
* <span data-ttu-id="bbf94-125">**channelId.** Это канал, в котором находится экземпляр вкладки.</span><span class="sxs-lookup"><span data-stu-id="bbf94-125">**channelId**: This is the channel in which the tab instance resides.</span></span>
   > [!NOTE]
   > <span data-ttu-id="bbf94-126">ChannelId **необязателен** для вкладок канала.</span><span class="sxs-lookup"><span data-stu-id="bbf94-126">The **channelId** is optional for channel tabs.</span></span> <span data-ttu-id="bbf94-127">Однако рекомендуется сохранить реализацию на канале и в статических вкладок одинаково.</span><span class="sxs-lookup"><span data-stu-id="bbf94-127">However, it is recommended if you want to keep your implementation across channel and static tabs the same.</span></span>
* <span data-ttu-id="bbf94-128">**название.** Это название, которое отображается пользователю в панели чата.</span><span class="sxs-lookup"><span data-stu-id="bbf94-128">**title**: This is the title that is shown to the user in the chat panel.</span></span>

<span data-ttu-id="bbf94-129">Большинство из этих значений также можно получить из `getContext` API.</span><span class="sxs-lookup"><span data-stu-id="bbf94-129">Most of these values can also be retrieved from the `getContext` API.</span></span>

```javascript
microsoftTeams.conversations.openConversation({“subEntityId”:”task-1”, “entityId”: “tabInstanceId-1”, “channelId”: ”19:baa6e71f65b948d189bf5c892baa8e5a@thread.skype”, “title”: "Task Title”});
```

<span data-ttu-id="bbf94-130">На следующем изображении показана панель бесед:</span><span class="sxs-lookup"><span data-stu-id="bbf94-130">The following image shows the conversation panel:</span></span>

![Беседные подуряды — начните беседу](~/assets/images/tabs/conversational-subentities/start-conversation.png)

<span data-ttu-id="bbf94-132">Если пользователь начинает беседу, важно прослушивать вызов этого события, чтобы получить и сохранить **conversationId:**</span><span class="sxs-lookup"><span data-stu-id="bbf94-132">If the user starts a conversation, it is important to listen for the callback of that event in order to retrieve and save the **conversationId**:</span></span>

```javascript
microsoftTeams.conversations.onStartConversation = (conversationResponse) => {
    // console.log(conversationReponse.conversationId)
};
```

<span data-ttu-id="bbf94-133">Объект `conversationResponse` содержит сведения, связанные с запущенным разговором.</span><span class="sxs-lookup"><span data-stu-id="bbf94-133">The `conversationResponse` object contains information related to the conversation that was started.</span></span> <span data-ttu-id="bbf94-134">Рекомендуется сохранить все свойства этого объекта отклика для более позднего использования.</span><span class="sxs-lookup"><span data-stu-id="bbf94-134">It is recommended that you save all the properties of this response object for later use.</span></span>

## <a name="continue-a-conversation"></a><span data-ttu-id="bbf94-135">Продолжение беседы</span><span class="sxs-lookup"><span data-stu-id="bbf94-135">Continue a conversation</span></span>

<span data-ttu-id="bbf94-136">После начала беседы последующие вызовы требуют, чтобы вы также предоставили те же входные данные, что и при запуске нового разговора, но также включали `openConversation()` **в себя conversationId** [](#start-a-new-conversation).</span><span class="sxs-lookup"><span data-stu-id="bbf94-136">After a conversation starts, subsequent calls to `openConversation()` requires that you also provide the same inputs as in [start a new conversation](#start-a-new-conversation), but also include the **conversationId**.</span></span> <span data-ttu-id="bbf94-137">Панель бесед открывается для пользователя с учетом соответствующего разговора.</span><span class="sxs-lookup"><span data-stu-id="bbf94-137">The conversation panel opens for the user with the appropriate conversation in view.</span></span> <span data-ttu-id="bbf94-138">Пользователи могут видеть новые или входящие сообщения в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="bbf94-138">Users are able to see new or incoming messages in real-time.</span></span>

<span data-ttu-id="bbf94-139">На следующем изображении показана панель беседы с соответствующей беседой:</span><span class="sxs-lookup"><span data-stu-id="bbf94-139">The following image shows the conversation panel with the appropriate conversation:</span></span>

![Беседные подуряды — продолжить беседу](~/assets/images/tabs/conversational-subentities/continue-conversation.png)

## <a name="enhance-a-conversation"></a><span data-ttu-id="bbf94-141">Повышение эффективности беседы</span><span class="sxs-lookup"><span data-stu-id="bbf94-141">Enhance a conversation</span></span>

<span data-ttu-id="bbf94-142">Важно, чтобы вкладка включала [глубокие ссылки на подгруппу.](~/concepts/build-and-test/deep-links.md)</span><span class="sxs-lookup"><span data-stu-id="bbf94-142">It is important that your tab includes [deeplinks to your sub-entity](~/concepts/build-and-test/deep-links.md).</span></span> <span data-ttu-id="bbf94-143">Например, пользователь, выбрав диплинк вкладки шиклета из беседы на канале.</span><span class="sxs-lookup"><span data-stu-id="bbf94-143">For example, user selecting the tab chiclet deeplink from the channel conversation.</span></span> <span data-ttu-id="bbf94-144">Ожидаемое поведение — получение deeplink, открытие этой подгруппы, а затем открытие панели беседы для этого подуряда.</span><span class="sxs-lookup"><span data-stu-id="bbf94-144">The expected behavior is to receive the deeplink, open that sub-entity, and then open the conversation panel for that sub-entity.</span></span>

<span data-ttu-id="bbf94-145">Чтобы поддерживать беседующих суб-сущностям с личной или статической вкладки, вам не нужно ничего менять в реализации.</span><span class="sxs-lookup"><span data-stu-id="bbf94-145">To support conversational sub-entities from your personal or static tab, you do not have to change anything in your implementation.</span></span> <span data-ttu-id="bbf94-146">Мы поддерживаем только начало или продолжение бесед со вкладок канала, которые уже закреплены.</span><span class="sxs-lookup"><span data-stu-id="bbf94-146">We only support starting or continuing conversations from channel tabs that are already pinned.</span></span> <span data-ttu-id="bbf94-147">Поддержка статических вкладок позволяет предоставить пользователям единое расположение для взаимодействия со всеми подуч.</span><span class="sxs-lookup"><span data-stu-id="bbf94-147">Supporting static tabs allows you to provide a single location for your users to interact with all your sub-entities.</span></span> <span data-ttu-id="bbf94-148">Важно сохранить , и когда вкладка изначально создается в канале, чтобы иметь правильные свойства при открытии представления беседы на статической `subEntityId` `entityId` `channelId` вкладке.</span><span class="sxs-lookup"><span data-stu-id="bbf94-148">It is important that you save the `subEntityId`, `entityId`, and `channelId` when your tab is originally created in a channel to have the right properties when opening the conversation view in a static tab.</span></span>

## <a name="close-a-conversation"></a><span data-ttu-id="bbf94-149">Закрыть беседу</span><span class="sxs-lookup"><span data-stu-id="bbf94-149">Close a conversation</span></span>

<span data-ttu-id="bbf94-150">Можно вручную закрыть представление беседы, позвонив в `closeConversation()` функцию.</span><span class="sxs-lookup"><span data-stu-id="bbf94-150">You can manually close the conversation view by calling the `closeConversation()` function.</span></span>

```javascript
microsoftTeams.conversations.closeConversation();
```

<span data-ttu-id="bbf94-151">Вы также можете прослушивать событие, когда пользователь закрывает представление беседы.</span><span class="sxs-lookup"><span data-stu-id="bbf94-151">You can also listen for an event when the conversation view is closed by a user.</span></span>

```javascript
microsoftTeams.conversations.onCloseConversation = (conversationResponse) => {
    // console.log(conversationResponse)
};
```

## <a name="see-also"></a><span data-ttu-id="bbf94-152">См. также</span><span class="sxs-lookup"><span data-stu-id="bbf94-152">See also</span></span>

* [<span data-ttu-id="bbf94-153">Teams вкладки</span><span class="sxs-lookup"><span data-stu-id="bbf94-153">Teams tabs</span></span>](~/tabs/what-are-tabs.md)
* [<span data-ttu-id="bbf94-154">Необходимые условия</span><span class="sxs-lookup"><span data-stu-id="bbf94-154">Prerequisites</span></span>](~/tabs/how-to/tab-requirements.md)
* [<span data-ttu-id="bbf94-155">Создать личную вкладку</span><span class="sxs-lookup"><span data-stu-id="bbf94-155">Create a personal tab</span></span>](~/tabs/how-to/create-personal-tab.md)
* [<span data-ttu-id="bbf94-156">Создание вкладки канала или группы</span><span class="sxs-lookup"><span data-stu-id="bbf94-156">Create a channel or group tab</span></span>](~/tabs/how-to/create-channel-group-tab.md)
* [<span data-ttu-id="bbf94-157">Создать страницу контента</span><span class="sxs-lookup"><span data-stu-id="bbf94-157">Create a content page</span></span>](~/tabs/how-to/create-tab-pages/content-page.md)
* [<span data-ttu-id="bbf94-158">Создать страницу конфигурации</span><span class="sxs-lookup"><span data-stu-id="bbf94-158">Create a configuration page</span></span>](~/tabs/how-to/create-tab-pages/configuration-page.md)
* [<span data-ttu-id="bbf94-159">Создание страницы удаления для вкладки</span><span class="sxs-lookup"><span data-stu-id="bbf94-159">Create a removal page for your tab</span></span>](~/tabs/how-to/create-tab-pages/removal-page.md)
* [<span data-ttu-id="bbf94-160">Вкладки на мобильных устройствах</span><span class="sxs-lookup"><span data-stu-id="bbf94-160">Tabs on mobile</span></span>](~/tabs/design/tabs-mobile.md)
* [<span data-ttu-id="bbf94-161">Получение контекста для вкладки</span><span class="sxs-lookup"><span data-stu-id="bbf94-161">Get context for your tab</span></span>](~/tabs/how-to/access-teams-context.md)
* [<span data-ttu-id="bbf94-162">Создание вкладок с использованием адаптивных карточек</span><span class="sxs-lookup"><span data-stu-id="bbf94-162">Build tabs with Adaptive Cards</span></span>](~/tabs/how-to/build-adaptive-card-tabs.md)
* [<span data-ttu-id="bbf94-163">Предварительный просмотр для ссылки "Вкладки" и представление стадий</span><span class="sxs-lookup"><span data-stu-id="bbf94-163">Tabs link unfurling and Stage View</span></span>](~/tabs/tabs-link-unfurling.md)

## <a name="next-step"></a><span data-ttu-id="bbf94-164">Следующий этап</span><span class="sxs-lookup"><span data-stu-id="bbf94-164">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bbf94-165">Изменения полей вкладок</span><span class="sxs-lookup"><span data-stu-id="bbf94-165">Tab margin changes</span></span>](~/resources/removing-tab-margins.md)