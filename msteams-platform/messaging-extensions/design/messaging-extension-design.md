---
title: Проектирование расширения обмена сообщениями
description: Узнайте, как разработать Teams обмена сообщениями и получить Microsoft Teams пользовательского интерфейса.
keywords: команды проектируют руководящие принципы ссылки расширения обмена сообщениями советы наилучшей практике
author: heath-hamilton
localization_priority: Normal
ms.author: qinch
ms.topic: conceptual
ms.openlocfilehash: ed1f0f2eb2ce8d429a8a780bd2c4c4eb421d6d54
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566217"
---
# <a name="designing-your-microsoft-teams-messaging-extension"></a><span data-ttu-id="78bc9-104">Проектирование Microsoft Teams обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="78bc9-104">Designing your Microsoft Teams messaging extension</span></span>

<span data-ttu-id="78bc9-105">Расширения сообщений являются ярлыками для вставки содержимого приложения или действия на сообщении без навигации от разговора.</span><span class="sxs-lookup"><span data-stu-id="78bc9-105">Messaging extensions are shortcuts for inserting app content or acting on a message without navigating away from the conversation.</span></span>
<span data-ttu-id="78bc9-106">Чтобы направлять дизайн приложения, следующая информация описывает и иллюстрирует, как люди могут добавлять, использовать и управлять расширениями обмена сообщениями в Teams.</span><span class="sxs-lookup"><span data-stu-id="78bc9-106">To guide your app design, the following information describes and illustrates how people can add, use, and manage messaging extensions in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="78bc9-107">Комплект разработчика для пользовательского интерфейса Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="78bc9-107">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="78bc9-108">В наборе пользовательского интерфейса можно найти всеобъемлющие рекомендации по проектированию расширения обмена сообщениями, включая элементы, Microsoft Teams которые можно захватить и изменить по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="78bc9-108">You can find comprehensive messaging extension design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="78bc9-109">Получить комплект разработчика для пользовательского интерфейса Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="78bc9-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-messaging-extension"></a><span data-ttu-id="78bc9-110">Добавление расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="78bc9-110">Add a messaging extension</span></span>

<span data-ttu-id="78bc9-111">Вы можете добавить расширение обмена сообщениями в следующих Teams контекстов:</span><span class="sxs-lookup"><span data-stu-id="78bc9-111">You can add a messaging extension in the following Teams contexts:</span></span>

* <span data-ttu-id="78bc9-112">Взять в магазине Teams (AppSource)</span><span class="sxs-lookup"><span data-stu-id="78bc9-112">From the Teams store (AppSource).</span></span>
* <span data-ttu-id="78bc9-113">В канале, чат, или встреча (до, во время и после) возле составить окно.</span><span class="sxs-lookup"><span data-stu-id="78bc9-113">In a channel, chat, or meeting (before, during, and after) near the compose box.</span></span> <span data-ttu-id="78bc9-114">Стоит отметить, что если вы добавите расширение обмена сообщениями в одном из этих мест, только вы можете использовать его в этом контексте.</span><span class="sxs-lookup"><span data-stu-id="78bc9-114">It's worth noting if you add a messaging extension in one of these places, only you can use it in that context.</span></span>

<span data-ttu-id="78bc9-115">В следующем примере показано, как вы добавляете расширение обмена сообщениями в канале:</span><span class="sxs-lookup"><span data-stu-id="78bc9-115">The following example shows how you add a messaging extension in a channel:</span></span>

:::image type="content" source="../../assets/images/messaging-extension/add-in-channel.png" alt-text="Пример показывает, как добавить расширение обмена сообщениями рядом с окном compose в канале." border="false":::

## <a name="set-up-a-messaging-extension"></a><span data-ttu-id="78bc9-117">Настройка расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="78bc9-117">Set up a messaging extension</span></span>

<span data-ttu-id="78bc9-118">Аутентификация не является обязательной, но если ваше приложение является чем-то вроде инструмента отслеживания билетов, вам может понадобиться, чтобы люди войсовы были в том, чтобы использовать расширение обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="78bc9-118">Authentication isn't mandatory, but if your app is something like a ticket tracking tool, you may need people to sign in to use the messaging extension.</span></span>

<span data-ttu-id="78bc9-119">Для согласованности Teams приложениях нельзя настроить экран ва-во.</span><span class="sxs-lookup"><span data-stu-id="78bc9-119">For consistency across Teams apps, you can't customize the sign-in screen.</span></span> <span data-ttu-id="78bc9-120">Если вы используете один знак проверки подлинности (SSO), пользователи вписываются автоматически.</span><span class="sxs-lookup"><span data-stu-id="78bc9-120">If you use single sign-on (SSO) authentication, users are signed in automatically.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/set-up.png" alt-text="Пример показывает экран настройки расширения обмена сообщениями с кнопкой ввеся." border="false":::

## <a name="types-of-messaging-extensions"></a><span data-ttu-id="78bc9-122">Типы расширений обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="78bc9-122">Types of messaging extensions</span></span>

<span data-ttu-id="78bc9-123">Расширения сообщений могут иметь команды поиска, команды действий или и то, и другое.</span><span class="sxs-lookup"><span data-stu-id="78bc9-123">Messaging extensions can have search commands, action commands, or both.</span></span> <span data-ttu-id="78bc9-124">Ваши команды зависят от функций приложения и от того, как они вписываются в Teams случаев использования.</span><span class="sxs-lookup"><span data-stu-id="78bc9-124">Your commands depend on your app's features and how those fit within Teams use cases.</span></span>

### <a name="search-commands"></a><span data-ttu-id="78bc9-125">Команды поиска</span><span class="sxs-lookup"><span data-stu-id="78bc9-125">Search commands</span></span>

<span data-ttu-id="78bc9-126">С помощью команд поиска люди могут использовать расширение обмена сообщениями для быстрого поиска внешнего содержимого и вставки в сообщение.</span><span class="sxs-lookup"><span data-stu-id="78bc9-126">With search commands, people can use your messaging extension to quickly find external content and insert into a message.</span></span> <span data-ttu-id="78bc9-127">Команды поиска обычно доступны в поле для составления.</span><span class="sxs-lookup"><span data-stu-id="78bc9-127">Search commands are commonly made available in the compose box.</span></span> <span data-ttu-id="78bc9-128">Например, можно начать или добавить к обсуждению, поделившись частью контента, не выходя из Teams.</span><span class="sxs-lookup"><span data-stu-id="78bc9-128">For example, you can start or add to a discussion by sharing a piece of content—without ever leaving Teams.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/search-command-type.png" alt-text="Пример показывает расширение обмена сообщениями на основе поиска, запущенного из окна compose." border="false":::

#### <a name="compose-box-layout-options"></a><span data-ttu-id="78bc9-130">Составить параметры макета коробки</span><span class="sxs-lookup"><span data-stu-id="78bc9-130">Compose box layout options</span></span>

<span data-ttu-id="78bc9-131">У вас есть несколько вариантов отображения результатов поиска расширения обмена сообщениями, включая [список и просмотры сетки.](../../messaging-extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests)</span><span class="sxs-lookup"><span data-stu-id="78bc9-131">You have some options for displaying messaging extension search results, including [list and grid views](../../messaging-extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests).</span></span>

:::image type="content" source="../../assets/images/messaging-extension/search-result-layout.png" alt-text="Иллюстрации, показывающие параметры макета для результатов поиска расширения обмена сообщениями." border="false":::

### <a name="action-commands"></a><span data-ttu-id="78bc9-133">Команды действий</span><span class="sxs-lookup"><span data-stu-id="78bc9-133">Action commands</span></span>

<span data-ttu-id="78bc9-134">Команды действий позволяют людям инициировать действия и обрабатывать запросы во внешних службах в Teams.</span><span class="sxs-lookup"><span data-stu-id="78bc9-134">Action commands allow people to trigger actions and process requests in external services within Teams.</span></span> <span data-ttu-id="78bc9-135">Например, если приложение отслеживает заказы, пользователь может создать новый порядок, используя содержимое сообщения коллеги прямо в чате.</span><span class="sxs-lookup"><span data-stu-id="78bc9-135">For example, if your app tracks orders, a user could create a new order using the contents of a colleague’s message from right inside their chat.</span></span>

<span data-ttu-id="78bc9-136">Расширения обмена сообщениями на основе действий часто требуют от пользователей завершения формы или какой-либо другой конфигурации в моде.</span><span class="sxs-lookup"><span data-stu-id="78bc9-136">Action-based messaging extensions frequently require users to complete a form or some other kind of configuration within a modal.</span></span> <span data-ttu-id="78bc9-137">Вы можете создать эти опыты с [модулями задач.](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)</span><span class="sxs-lookup"><span data-stu-id="78bc9-137">You can create these experiences with [task modules](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).</span></span>

## <a name="open-a-messaging-extension"></a><span data-ttu-id="78bc9-138">Открыть расширение обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="78bc9-138">Open a messaging extension</span></span>

<span data-ttu-id="78bc9-139">Составной ящик и сообщения или сообщения являются основными контекстами, в которых люди используют расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="78bc9-139">The compose box and messages or posts are the primary contexts where people use messaging extensions.</span></span>

### <a name="from-the-compose-box"></a><span data-ttu-id="78bc9-140">Из коробки для сочинения</span><span class="sxs-lookup"><span data-stu-id="78bc9-140">From the compose box</span></span>

<span data-ttu-id="78bc9-141">После добавления пользователи могут открыть расширение обмена сообщениями, выбрав значок приложения ниже коробки compose.</span><span class="sxs-lookup"><span data-stu-id="78bc9-141">Once added, users can open your messaging extension by selecting your app icon below the compose box.</span></span> <span data-ttu-id="78bc9-142">В этом примере расширение имеет команды поиска и действия:</span><span class="sxs-lookup"><span data-stu-id="78bc9-142">In this example, the extension has search and action commands:</span></span>

:::image type="content" source="../../assets/images/messaging-extension/open-from-compose-box.png" alt-text="Пример показывает, как открыть расширение обмена сообщениями из окна compose." border="false":::

### <a name="from-a-chat-message-or-channel-post"></a><span data-ttu-id="78bc9-144">Из сообщения чата или сообщения канала</span><span class="sxs-lookup"><span data-stu-id="78bc9-144">From a chat message or channel post</span></span>

После добавления пользователи могут выбрать **значок More** :::image type="icon" source="../../assets/icons/teams-client-more.png"::: в сообщении чата или сообщении канала, чтобы найти команды действий вашего расширения. <span data-ttu-id="78bc9-146">Ваше расширение может быть перечислено в соответствии с **более действиями,** основанными на использовании.</span><span class="sxs-lookup"><span data-stu-id="78bc9-146">Your extension may be listed under **More actions** based on usage.</span></span>

> [!NOTE]
> <span data-ttu-id="78bc9-147">Поддержка дополнительных действий из сообщения чата или сообщения канала недоступна на Microsoft Teams платформе.</span><span class="sxs-lookup"><span data-stu-id="78bc9-147">Support for more actions from a chat message or channel post is not available on Microsoft Teams mobile platform.</span></span> 

#### <a name="chat-message"></a><span data-ttu-id="78bc9-148">Сообщение чата</span><span class="sxs-lookup"><span data-stu-id="78bc9-148">Chat message</span></span>

:::image type="content" source="../../assets/images/messaging-extension/open-from-chat-message.png" alt-text="Пример показывает, как открыть расширение обмена сообщениями из сообщения чата." border="false":::

#### <a name="channel-post"></a><span data-ttu-id="78bc9-150">Почта канала</span><span class="sxs-lookup"><span data-stu-id="78bc9-150">Channel post</span></span>

:::image type="content" source="../../assets/images/messaging-extension/open-from-channel-post.png" alt-text="Пример показывает, как открыть расширение обмена сообщениями с поста канала." border="false":::

## <a name="use-a-messaging-extension"></a><span data-ttu-id="78bc9-152">Использование расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="78bc9-152">Use a messaging extension</span></span>

<span data-ttu-id="78bc9-153">Следующие сценарии показывают основные способы использования расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="78bc9-153">The following scenarios show the primary ways people use messaging extensions.</span></span>

### <a name="insert-content-into-a-message"></a><span data-ttu-id="78bc9-154">Вставьте содержимое в сообщение</span><span class="sxs-lookup"><span data-stu-id="78bc9-154">Insert content into a message</span></span>

<span data-ttu-id="78bc9-155">**1. Выберите расширение обмена сообщениями.**</span><span class="sxs-lookup"><span data-stu-id="78bc9-155">**1. Select a messaging extension**.</span></span> <span data-ttu-id="78bc9-156">Пользователи могут искать содержимое, которое они хотят поделиться из окна compose.</span><span class="sxs-lookup"><span data-stu-id="78bc9-156">Users can search for the content they want to share from the compose box.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/insert-content-search.png" alt-text="Пример показывает пользователя, ищуго содержимое для вставки из окна compose." border="false":::

<span data-ttu-id="78bc9-158">**2. Вставьте содержимое**.</span><span class="sxs-lookup"><span data-stu-id="78bc9-158">**2. Insert content**.</span></span> <span data-ttu-id="78bc9-159">После опубликования другие могут ответить или выбрать содержимое, чтобы увидеть больше информации в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="78bc9-159">Once posted, others can reply or select the content to see more information in your app.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/insert-content-posted.png" alt-text="Пример показывает пользователя, размещая содержимое в разговоре с каналом." border="false":::

### <a name="take-action-on-a-message"></a><span data-ttu-id="78bc9-161">Принять меры по сообщению</span><span class="sxs-lookup"><span data-stu-id="78bc9-161">Take action on a message</span></span>

<span data-ttu-id="78bc9-162">**1. Выберите расширение обмена сообщениями.**</span><span class="sxs-lookup"><span data-stu-id="78bc9-162">**1. Select a messaging extension**.</span></span> <span data-ttu-id="78bc9-163">Ваше приложение может включать одну или несколько команд действий.</span><span class="sxs-lookup"><span data-stu-id="78bc9-163">Your app can include one or more action commands.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/select-action-command.png" alt-text="На примере показан пользователь, выбираюющий команду действий расширения обмена сообщениями." border="false":::

<span data-ttu-id="78bc9-165">**2. Завершите действие**.</span><span class="sxs-lookup"><span data-stu-id="78bc9-165">**2. Complete the action**.</span></span> <span data-ttu-id="78bc9-166">Ваше приложение может получать и обрабатывать любой контент или данные, отправленные действиями сообщения.</span><span class="sxs-lookup"><span data-stu-id="78bc9-166">Your app can receive and process any content or data sent by the message action.</span></span> <span data-ttu-id="78bc9-167">Это позволяет пользователям оставаться в разговоре и, на следующем примере, не беспокоиться о вводе информации непосредственно в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="78bc9-167">This allows users to remain in their conversation and, the following example, not worry about entering information directly in your app.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/complete-action-command.png" alt-text="Пример того, как принять меры по сообщению." border="false":::

### <a name="preview-links"></a><span data-ttu-id="78bc9-169">Предварительные ссылки</span><span class="sxs-lookup"><span data-stu-id="78bc9-169">Preview links</span></span>

<span data-ttu-id="78bc9-170">Расширения обмена сообщениями также позволяют вставлять богатые ссылки из распознаемого URL-адреса в сообщение (эта возможность [называется разворачивание ссылки](../../messaging-extensions/how-to/link-unfurling.md).)</span><span class="sxs-lookup"><span data-stu-id="78bc9-170">Messaging extensions also allow you to insert rich links from a recognized URL into a message (this capability is called [link unfurling](../../messaging-extensions/how-to/link-unfurling.md).)</span></span>

<span data-ttu-id="78bc9-171">**1. Вставьте признанную ссылку** в поле для составления.</span><span class="sxs-lookup"><span data-stu-id="78bc9-171">**1. Paste a recognized link** in the compose box.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/paste-preview-link.png" alt-text="Пример показывает, как пользователь вставки ссылку в поле компоста." border="false":::

<span data-ttu-id="78bc9-173">**2. Вставьте содержимое**.</span><span class="sxs-lookup"><span data-stu-id="78bc9-173">**2. Insert content**.</span></span> <span data-ttu-id="78bc9-174">Если ваше приложение распознает URL-адрес в поле compose, оно отображает ссылку как карту, которая обеспечивает богатый контентом предварительный просмотр веб-контента.</span><span class="sxs-lookup"><span data-stu-id="78bc9-174">If your app recognizes the URL in the compose box, it renders the link as a card that provides a content-rich preview of the web content.</span></span> <span data-ttu-id="78bc9-175">(См. [Руководящие принципы по разработке адаптивных](../../task-modules-and-cards/cards/design-effective-cards.md) карт для получения дополнительной информации.)</span><span class="sxs-lookup"><span data-stu-id="78bc9-175">(See [Adaptive Cards design guidelines](../../task-modules-and-cards/cards/design-effective-cards.md) for more information.)</span></span>

:::image type="content" source="../../assets/images/messaging-extension/insert-preview-link.png" alt-text="Пример показывает, как URL-адрес, так как он распознается вашим приложением, включает в себя некоторые богатые содержание в поле compose." border="false":::

## <a name="manage-a-messaging-extension"></a><span data-ttu-id="78bc9-177">Управление расширением обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="78bc9-177">Manage a messaging extension</span></span>

<span data-ttu-id="78bc9-178">При правильном нажатии на значок пользователи могут закрепить, удалить или настроить расширение обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="78bc9-178">By right clicking your icon, users can pin, remove, or configure your messaging extension.</span></span>

## <a name="anatomy"></a><span data-ttu-id="78bc9-179">Анатомия</span><span class="sxs-lookup"><span data-stu-id="78bc9-179">Anatomy</span></span>

### <a name="messaging-extension-in-the-compose-box"></a><span data-ttu-id="78bc9-180">Расширение сообщений в поле для составления</span><span class="sxs-lookup"><span data-stu-id="78bc9-180">Messaging extension in the compose box</span></span>

<span data-ttu-id="78bc9-181">Следующим примером является расширение обмена сообщениями, открытое из окна compose.</span><span class="sxs-lookup"><span data-stu-id="78bc9-181">The following example is a messaging extension opened from the compose box.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/anatomy-compose.png" alt-text="Иллюстрация, показывающая анатомию пользовательского интерфейса расширения обмена сообщениями в поле compose." border="false":::

|<span data-ttu-id="78bc9-183">Счетчик</span><span class="sxs-lookup"><span data-stu-id="78bc9-183">Counter</span></span>|<span data-ttu-id="78bc9-184">Описание</span><span class="sxs-lookup"><span data-stu-id="78bc9-184">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="78bc9-185">1</span><span class="sxs-lookup"><span data-stu-id="78bc9-185">1</span></span>|<span data-ttu-id="78bc9-186">**Логотип приложения**: Цвет значка логотипа приложения.</span><span class="sxs-lookup"><span data-stu-id="78bc9-186">**App logo**: Color icon of your app logo.</span></span>|
|<span data-ttu-id="78bc9-187">2</span><span class="sxs-lookup"><span data-stu-id="78bc9-187">2</span></span>|<span data-ttu-id="78bc9-188">**Название приложения**: Полное название приложения.</span><span class="sxs-lookup"><span data-stu-id="78bc9-188">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="78bc9-189">3</span><span class="sxs-lookup"><span data-stu-id="78bc9-189">3</span></span>|<span data-ttu-id="78bc9-190">**Значок меню команды action (необязательно)**: Открывает список команд действий для расширения обмена сообщениями (если вы укажете их).</span><span class="sxs-lookup"><span data-stu-id="78bc9-190">**Action commands menu icon (optional)**: Opens a list of action commands for your messaging extension (if you specify any).</span></span>
|<span data-ttu-id="78bc9-191">4 </span><span class="sxs-lookup"><span data-stu-id="78bc9-191">4</span></span>|<span data-ttu-id="78bc9-192">**Окно поиска**: Позволяет пользователям находить содержимое приложения, которое они хотят вставить.</span><span class="sxs-lookup"><span data-stu-id="78bc9-192">**Search box**: Allows users to find app content they want to insert.</span></span>|
|<span data-ttu-id="78bc9-193">5 </span><span class="sxs-lookup"><span data-stu-id="78bc9-193">5</span></span>|<span data-ttu-id="78bc9-194">**Меню вкладок (необязательно)**: Предоставляет несколько категорий контента.</span><span class="sxs-lookup"><span data-stu-id="78bc9-194">**Tab menu (optional)**: Provides multiple content categories.</span></span>|
|<span data-ttu-id="78bc9-195">6 </span><span class="sxs-lookup"><span data-stu-id="78bc9-195">6</span></span>|<span data-ttu-id="78bc9-196">**Меню команд действий (необязательно)**: Отображает список команд действий (если вы укажете их).</span><span class="sxs-lookup"><span data-stu-id="78bc9-196">**Action commands menu (optional)**: Displays list of action commands (if you specify any).</span></span>|
|<span data-ttu-id="78bc9-197">7 </span><span class="sxs-lookup"><span data-stu-id="78bc9-197">7</span></span>|<span data-ttu-id="78bc9-198">**Содержимое приложения**: В первую очередь для отображения результатов поиска.</span><span class="sxs-lookup"><span data-stu-id="78bc9-198">**App content**: Primarily to display search results.</span></span> <span data-ttu-id="78bc9-199">Пример здесь использует макет списка (сетка макет является еще одним вариантом).</span><span class="sxs-lookup"><span data-stu-id="78bc9-199">The example here is using the list layout (grid layout is another option).</span></span>|
|<span data-ttu-id="78bc9-200">8 </span><span class="sxs-lookup"><span data-stu-id="78bc9-200">8</span></span>|<span data-ttu-id="78bc9-201">**Логотип приложения**: Контур значок логотипа приложения.</span><span class="sxs-lookup"><span data-stu-id="78bc9-201">**App logo**: Outline icon of your app logo.</span></span>|

### <a name="messaging-extension-management-menu"></a><span data-ttu-id="78bc9-202">Меню управления расширением сообщений</span><span class="sxs-lookup"><span data-stu-id="78bc9-202">Messaging extension management menu</span></span>

:::image type="content" source="../../assets/images/messaging-extension/anatomy-management-menu.png" alt-text="Иллюстрация, показывающая анатомию пользовательского интерфейса меню управления расширением обмена сообщениями." border="false":::

|<span data-ttu-id="78bc9-204">Счетчик</span><span class="sxs-lookup"><span data-stu-id="78bc9-204">Counter</span></span>|<span data-ttu-id="78bc9-205">Описание</span><span class="sxs-lookup"><span data-stu-id="78bc9-205">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="78bc9-206">1</span><span class="sxs-lookup"><span data-stu-id="78bc9-206">1</span></span>|<span data-ttu-id="78bc9-207">**Unpin**: Доступно, если пользователь прикрепил ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="78bc9-207">**Unpin**: Available if the user has pinned your app.</span></span>|
|<span data-ttu-id="78bc9-208">2</span><span class="sxs-lookup"><span data-stu-id="78bc9-208">2</span></span>|<span data-ttu-id="78bc9-209">**Удалить**: Удаляет расширение обмена сообщениями из канала, чата или собрания.</span><span class="sxs-lookup"><span data-stu-id="78bc9-209">**Remove**: Removes the messaging extension from the channel, chat, or meeting.</span></span>|

## <a name="best-practices"></a><span data-ttu-id="78bc9-210">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="78bc9-210">Best practices</span></span>

<span data-ttu-id="78bc9-211">Используйте эти рекомендации для создания качественного приложения.</span><span class="sxs-lookup"><span data-stu-id="78bc9-211">Use these recommendations to create a quality app experience.</span></span>

### <a name="setup-and-general-usage"></a><span data-ttu-id="78bc9-212">Настройка и общее использование</span><span class="sxs-lookup"><span data-stu-id="78bc9-212">Setup and general usage</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-do.png" alt-text="Пример по настройке и общему использованию." border="false":::

#### <a name="do-integrate-with-single-sign-on"></a><span data-ttu-id="78bc9-214">У: Интеграция с одним знаком на</span><span class="sxs-lookup"><span data-stu-id="78bc9-214">Do: Integrate with single-sign on</span></span>

<span data-ttu-id="78bc9-215">SSO упрощает, быстрее и обеспечивает безопасность процесса вовсяться.</span><span class="sxs-lookup"><span data-stu-id="78bc9-215">SSO makes the sign-in process easier, faster, and secure.</span></span> <span data-ttu-id="78bc9-216">Кроме того, если пользователь уже в подписался на ваше личное приложение, он не должен также войти в систему снова, чтобы получить доступ к расширению обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="78bc9-216">Also, if a user has already signed in to your personal app, they don’t have to also sign in again to access the messaging extension.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-dont.png" alt-text="Пример интеграции с одним знаком." border="false":::

#### <a name="dont-take-users-away-from-the-conversation"></a><span data-ttu-id="78bc9-218">Не: Увечьте пользователей от разговора</span><span class="sxs-lookup"><span data-stu-id="78bc9-218">Don't: Take users away from the conversation</span></span>

<span data-ttu-id="78bc9-219">Расширения сообщений являются ярлыками, которые должны уменьшить переключение контекста.</span><span class="sxs-lookup"><span data-stu-id="78bc9-219">Messaging extensions are shortcuts that are supposed reduce context switching.</span></span> <span data-ttu-id="78bc9-220">Ваше расширение не должно, например, направлять пользователей на веб-страницу за пределами Teams.</span><span class="sxs-lookup"><span data-stu-id="78bc9-220">Your extension should not, for example, direct users to a webpage outside Teams.</span></span>

   :::column-end:::
:::row-end:::

#### <a name="do-highlight-your-messaging-extension"></a><span data-ttu-id="78bc9-221">У: Выделите расширение обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="78bc9-221">Do: Highlight your messaging extension</span></span>

<span data-ttu-id="78bc9-222">Расширения обмена сообщениями не всегда легко найти.</span><span class="sxs-lookup"><span data-stu-id="78bc9-222">Messaging extensions aren't always easy to find.</span></span> <span data-ttu-id="78bc9-223">Включите скриншоты того, как использовать его на странице деталей приложения.</span><span class="sxs-lookup"><span data-stu-id="78bc9-223">Include screenshots of how to use it in your app details page.</span></span> <span data-ttu-id="78bc9-224">Если ваше приложение также включает в себя бота, вы можете включить документацию по расширению обмена сообщениями в приветственный тур бота.</span><span class="sxs-lookup"><span data-stu-id="78bc9-224">If your app also includes a bot, you can include messaging extension help documentation in a bot welcome tour.</span></span>

### <a name="templating"></a><span data-ttu-id="78bc9-225">Темплятирование</span><span class="sxs-lookup"><span data-stu-id="78bc9-225">Templating</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-do.png" alt-text="Пример по шаблонам." border="false":::

#### <a name="do-let-teams-handle-some-of-the-design-work-if-possible"></a><span data-ttu-id="78bc9-227">У: Давайте Teams некоторые из проектных работ, если это возможно</span><span class="sxs-lookup"><span data-stu-id="78bc9-227">Do: Let Teams handle some of the design work if possible</span></span>

<span data-ttu-id="78bc9-228">Если это имеет смысл для ваших случаев использования, подумайте о создании расширения обмена сообщениями на основе поиска.</span><span class="sxs-lookup"><span data-stu-id="78bc9-228">If it makes sense for your use cases, consider creating a search-based messaging extension.</span></span> <span data-ttu-id="78bc9-229">Teams делает эти типы расширений встроенной темой и доступностью.</span><span class="sxs-lookup"><span data-stu-id="78bc9-229">Teams renders these types of extensions with built-in theming and accessibility.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-dont.png" alt-text="Пример по обработке проектных работ." border="false":::

#### <a name="dont-embed-your-entire-app-in-a-task-module"></a><span data-ttu-id="78bc9-231">Не встраивайте все приложение в модуль задач</span><span class="sxs-lookup"><span data-stu-id="78bc9-231">Don't: Embed your entire app in a task module</span></span>

<span data-ttu-id="78bc9-232">Если расширение обмена сообщениями требует команд действий, держите модуль задачи простым и отображайте только компоненты, необходимые для завершения действия.</span><span class="sxs-lookup"><span data-stu-id="78bc9-232">If your messaging extension requires action commands, keep the task module simple and display only the components required to complete the action.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="78bc9-233">Темы</span><span class="sxs-lookup"><span data-stu-id="78bc9-233">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-do.png" alt-text="Пример по их метью." border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a><span data-ttu-id="78bc9-235">Do: Воспользуйтесь Teams цветных жетонов</span><span class="sxs-lookup"><span data-stu-id="78bc9-235">Do: Take advantage of Teams color tokens</span></span>

<span data-ttu-id="78bc9-236">Каждая Teams имеет свою цветовую гамму.</span><span class="sxs-lookup"><span data-stu-id="78bc9-236">Each Teams theme has its own color scheme.</span></span> <span data-ttu-id="78bc9-237">Для автоматического обработки изменений темы <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">используйте цветовые жетоны (Fluent UI)</a> в своем дизайне.</span><span class="sxs-lookup"><span data-stu-id="78bc9-237">To handle theme changes automatically, use <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a> in your design.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-dont.png" alt-text="Пример цветовых жетонов." border="false":::

#### <a name="dont-hard-code-color-values"></a><span data-ttu-id="78bc9-239">Не: Значения цвета жесткого кода</span><span class="sxs-lookup"><span data-stu-id="78bc9-239">Don't: Hard code color values</span></span>

<span data-ttu-id="78bc9-240">Если вы не используете Teams, ваши проекты будут менее масштабируемыми и потребуется больше времени для управления.</span><span class="sxs-lookup"><span data-stu-id="78bc9-240">If you don't use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::

### <a name="actions"></a><span data-ttu-id="78bc9-241">Действия</span><span class="sxs-lookup"><span data-stu-id="78bc9-241">Actions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-do.png" alt-text="Пример действий." border="false":::

#### <a name="do-include-action-commands-that-make-sense-in-context"></a><span data-ttu-id="78bc9-243">У: Включите команды действий, которые имеют смысл в контексте</span><span class="sxs-lookup"><span data-stu-id="78bc9-243">Do: Include action commands that make sense in context</span></span>

<span data-ttu-id="78bc9-244">Действия сообщения должны относиться к тому, на что смотрит пользователь.</span><span class="sxs-lookup"><span data-stu-id="78bc9-244">Message actions should relate to what a user is looking at.</span></span> <span data-ttu-id="78bc9-245">Например, предоставьте пользователям ярлык для создания проблемы или рабочего элемента с помощью текста в чьей-то должности.</span><span class="sxs-lookup"><span data-stu-id="78bc9-245">For example, provide users a shortcut for creating an issue or work item using the text in someone’s post.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-dont.png" alt-text="Пример команд действий." border="false":::

#### <a name="dont-include-actions-commands-that-arent-contextual"></a><span data-ttu-id="78bc9-247">Не: Включите команды действий, которые не являются контекстуальными</span><span class="sxs-lookup"><span data-stu-id="78bc9-247">Don't: Include actions commands that aren't contextual</span></span>

<span data-ttu-id="78bc9-248">Действия сообщения для просмотра **панели мониторинга, вероятно,** кажутся отключенными от большинства разговоров.</span><span class="sxs-lookup"><span data-stu-id="78bc9-248">A message action to **View your dashboard** would probably seem disconnected from most conversations.</span></span>

   :::column-end:::
:::row-end:::

### <a name="searches"></a><span data-ttu-id="78bc9-249">Поиск</span><span class="sxs-lookup"><span data-stu-id="78bc9-249">Searches</span></span>

#### <a name="do-show-search-results-while-typing"></a><span data-ttu-id="78bc9-250">У: Показать результаты поиска при вводе</span><span class="sxs-lookup"><span data-stu-id="78bc9-250">Do: Show search results while typing</span></span>

<span data-ttu-id="78bc9-251">Предоставьте предлагаемые результаты поиска во время ввеха пользователей.</span><span class="sxs-lookup"><span data-stu-id="78bc9-251">Provide suggested search results while users type.</span></span> <span data-ttu-id="78bc9-252">Они могут найти содержимое, которое им нужно быстрее с минимальным количеством символов.</span><span class="sxs-lookup"><span data-stu-id="78bc9-252">They may find the content they need faster with minimal amount of characters.</span></span>

#### <a name="dont-require-users-to-submit-a-query"></a><span data-ttu-id="78bc9-253">Не: Требовать от пользователей отправки запроса</span><span class="sxs-lookup"><span data-stu-id="78bc9-253">Don't: Require users to submit a query</span></span>

<span data-ttu-id="78bc9-254">Вы можете заставить пользователей нажать клавишу или выбрать кнопку для отправки запросов в ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="78bc9-254">You can make users press a key or select a button to send queries to your app.</span></span> <span data-ttu-id="78bc9-255">Хотя служба служб приложений может быть проще, люди могут быть смущены тем, что они не видят результатов поиска в режиме реального времени при их типе.</span><span class="sxs-lookup"><span data-stu-id="78bc9-255">While that may be easier on your app services service, people may be confused that they're not seeing real-time search results as they type.</span></span>

#### <a name="do-consider-zero-term-queries"></a><span data-ttu-id="78bc9-256">У: Рассмотрим нулевой срок запросов</span><span class="sxs-lookup"><span data-stu-id="78bc9-256">Do: Consider zero-term queries</span></span>

<span data-ttu-id="78bc9-257">Например, прежде чем пользователь написыт что-либо в поле поиска, отобразить то, что он в последний раз просматривается в приложении.</span><span class="sxs-lookup"><span data-stu-id="78bc9-257">For example, before a user writes anything in the search box, display what they last viewed on your app.</span></span> <span data-ttu-id="78bc9-258">Вполне возможно, что они хотят, чтобы вставить этот контент в их разговор.</span><span class="sxs-lookup"><span data-stu-id="78bc9-258">It's possible that they want to insert that content into their conversation.</span></span>
