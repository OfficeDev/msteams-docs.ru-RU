---
title: Проектирование расширения обмена сообщениями
description: Узнайте, как разработать расширение обмена сообщениями Teams и получить набор пользовательского интерфейса Microsoft Teams.
keywords: Рекомендации по разработке рекомендаций по расширению справочных сообщений в командах советы по рекомендациям по рекомендациям
author: heath-hamilton
ms.author: qinch
ms.topic: conceptual
ms.openlocfilehash: 747b48e3aeb803f91cfb8d4412c98cb6d52c1fd1
ms.sourcegitcommit: f6e4a303828224a702138753a8e5e27c8a094c82
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/24/2021
ms.locfileid: "51176979"
---
# <a name="designing-your-microsoft-teams-messaging-extension"></a><span data-ttu-id="d19af-104">Разработка расширения обмена сообщениями Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="d19af-104">Designing your Microsoft Teams messaging extension</span></span>

<span data-ttu-id="d19af-105">Расширения обмена сообщениями — это ярлыки для вставки контента приложения или действия в сообщении, не переходя от беседы.</span><span class="sxs-lookup"><span data-stu-id="d19af-105">Messaging extensions are shortcuts for inserting app content or acting on a message without navigating away from the conversation.</span></span>
<span data-ttu-id="d19af-106">Для руководства разработкой приложения в следующих сведениях описывается и иллюстрируется возможность добавления, использования и управления расширениями обмена сообщениями в Teams.</span><span class="sxs-lookup"><span data-stu-id="d19af-106">To guide your app design, the following information describes and illustrates how people can add, use, and manage messaging extensions in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="d19af-107">Набор пользовательского интерфейса Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="d19af-107">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="d19af-108">В наборе пользовательского интерфейса Microsoft Teams можно найти исчерпывающие рекомендации по расширению обмена сообщениями, в том числе элементы, которые можно захватить и изменить по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="d19af-108">You can find comprehensive messaging extension design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d19af-109">Получите набор пользовательского интерфейса Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="d19af-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-messaging-extension"></a><span data-ttu-id="d19af-110">Добавление расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="d19af-110">Add a messaging extension</span></span>

<span data-ttu-id="d19af-111">Расширение обмена сообщениями можно добавить в следующих контекстах Teams:</span><span class="sxs-lookup"><span data-stu-id="d19af-111">You can add a messaging extension in the following Teams contexts:</span></span>

* <span data-ttu-id="d19af-112">Из магазина Teams (AppSource).</span><span class="sxs-lookup"><span data-stu-id="d19af-112">From the Teams store (AppSource).</span></span>
* <span data-ttu-id="d19af-113">В канале, чате или собрании (до, во время и после) рядом с полем составить.</span><span class="sxs-lookup"><span data-stu-id="d19af-113">In a channel, chat, or meeting (before, during, and after) near the compose box.</span></span> <span data-ttu-id="d19af-114">Стоит отметить, что если в одном из этих мест добавлено расширение обмена сообщениями, его можно использовать только в этом контексте.</span><span class="sxs-lookup"><span data-stu-id="d19af-114">It's worth noting if you add a messaging extension in one of these places, only you can use it in that context.</span></span>

<span data-ttu-id="d19af-115">В следующем примере показано, как добавить расширение обмена сообщениями в канал.</span><span class="sxs-lookup"><span data-stu-id="d19af-115">The following example shows how you add a messaging extension in a channel.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/add-in-channel.png" alt-text="В примере показано, как добавить расширение обмена сообщениями рядом с окне составить в канале." border="false":::

## <a name="set-up-a-messaging-extension"></a><span data-ttu-id="d19af-117">Настройка расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="d19af-117">Set up a messaging extension</span></span>

<span data-ttu-id="d19af-118">Проверка подлинности не является обязательной, но если ваше приложение является чем-то вроде средства отслеживания билетов, для использования расширения обмена сообщениями могут потребоваться люди.</span><span class="sxs-lookup"><span data-stu-id="d19af-118">Authentication isn't mandatory, but if your app is something like a ticket tracking tool, you may need people to sign in to use the messaging extension.</span></span>

<span data-ttu-id="d19af-119">Чтобы обеспечить согласованность в приложениях Teams, нельзя настроить экран входного знака.</span><span class="sxs-lookup"><span data-stu-id="d19af-119">For consistency across Teams apps, you can't customize the sign-in screen.</span></span> <span data-ttu-id="d19af-120">При использовании проверки подлинности с одним входом (SSO) пользователи автоматически подписываются.</span><span class="sxs-lookup"><span data-stu-id="d19af-120">If you use single sign-on (SSO) authentication, users are signed in automatically.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/set-up.png" alt-text="В примере показан экран установки расширения обмена сообщениями с кнопкой вход." border="false":::

## <a name="types-of-messaging-extensions"></a><span data-ttu-id="d19af-122">Типы расширений обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="d19af-122">Types of messaging extensions</span></span>

<span data-ttu-id="d19af-123">Расширения обмена сообщениями могут иметь команды поиска, команды действий или оба.</span><span class="sxs-lookup"><span data-stu-id="d19af-123">Messaging extensions can have search commands, action commands, or both.</span></span> <span data-ttu-id="d19af-124">Ваши команды зависят от функций приложения и от того, как те, которые подходят в Teams, используют случаи.</span><span class="sxs-lookup"><span data-stu-id="d19af-124">Your commands depend on your app's features and how those fit within Teams use cases.</span></span>

### <a name="search-commands"></a><span data-ttu-id="d19af-125">Команды поиска</span><span class="sxs-lookup"><span data-stu-id="d19af-125">Search commands</span></span>

<span data-ttu-id="d19af-126">С помощью команд поиска люди могут использовать расширение обмена сообщениями для быстрого поиска внешнего контента и вставки в сообщение.</span><span class="sxs-lookup"><span data-stu-id="d19af-126">With search commands, people can use your messaging extension to quickly find external content and insert into a message.</span></span> <span data-ttu-id="d19af-127">Команды поиска обычно доступны в окне составить.</span><span class="sxs-lookup"><span data-stu-id="d19af-127">Search commands are commonly made available in the compose box.</span></span> <span data-ttu-id="d19af-128">Например, вы можете начать или добавить в дискуссию, поделившись частью контента, не покидая Teams.</span><span class="sxs-lookup"><span data-stu-id="d19af-128">For example, you can start or add to a discussion by sharing a piece of content—without ever leaving Teams.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/search-command-type.png" alt-text="В примере показано расширение обмена сообщениями на основе поиска, запущенное из окна составить." border="false":::

#### <a name="compose-box-layout-options"></a><span data-ttu-id="d19af-130">Параметры композитного макета полей</span><span class="sxs-lookup"><span data-stu-id="d19af-130">Compose box layout options</span></span>

<span data-ttu-id="d19af-131">У вас есть несколько вариантов отображения результатов поиска расширения обмена сообщениями, включая [представления списков и сетки.](../../messaging-Ask about extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests)</span><span class="sxs-lookup"><span data-stu-id="d19af-131">You have some options for displaying messaging extension search results, including [list and grid views](../../messaging-Ask about extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests).</span></span>

:::image type="content" source="../../assets/images/messaging-extension/search-result-layout.png" alt-text="На иллюстрациях показаны параметры макета результатов поиска расширения обмена сообщениями." border="false":::

### <a name="action-commands"></a><span data-ttu-id="d19af-133">Команды действий</span><span class="sxs-lookup"><span data-stu-id="d19af-133">Action commands</span></span>

<span data-ttu-id="d19af-134">Команды действий позволяют пользователям запускать действия и обрабатывать запросы во внешних службах в Teams.</span><span class="sxs-lookup"><span data-stu-id="d19af-134">Action commands allow people to trigger actions and process requests in external services within Teams.</span></span> <span data-ttu-id="d19af-135">Например, если приложение отслеживает заказы, пользователь может создать новый порядок с помощью содержимого сообщения коллеги прямо в чате.</span><span class="sxs-lookup"><span data-stu-id="d19af-135">For example, if your app tracks orders, a user could create a new order using the contents of a colleague’s message from right inside their chat.</span></span>

<span data-ttu-id="d19af-136">Расширения обмена сообщениями на основе действий часто требуют, чтобы пользователи заполняли форму или другую конфигурацию в модале.</span><span class="sxs-lookup"><span data-stu-id="d19af-136">Action-based messaging extensions frequently require users to complete a form or some other kind of configuration within a modal.</span></span> <span data-ttu-id="d19af-137">Эти возможности можно создавать с помощью [модулей задач.](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)</span><span class="sxs-lookup"><span data-stu-id="d19af-137">You can create these experiences with [task modules](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).</span></span>

## <a name="open-a-messaging-extension"></a><span data-ttu-id="d19af-138">Откройте расширение обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="d19af-138">Open a messaging extension</span></span>

<span data-ttu-id="d19af-139">Основной контекст, в котором люди используют расширения обмена сообщениями, — это шкатулка и сообщения.</span><span class="sxs-lookup"><span data-stu-id="d19af-139">The compose box and messages/posts are the primary contexts where people use messaging extensions.</span></span>

### <a name="from-the-compose-box"></a><span data-ttu-id="d19af-140">Из окне композит</span><span class="sxs-lookup"><span data-stu-id="d19af-140">From the compose box</span></span>

<span data-ttu-id="d19af-141">После добавления пользователи могут открыть расширение обмена сообщениями, выбрав значок приложения под полем составить.</span><span class="sxs-lookup"><span data-stu-id="d19af-141">Once added, users can open your messaging extension by selecting your app icon below the compose box.</span></span> <span data-ttu-id="d19af-142">В этом примере расширение имеет команды поиска и действий.</span><span class="sxs-lookup"><span data-stu-id="d19af-142">In this example, the extension has search and action commands.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/open-from-compose-box.png" alt-text="В примере показано, как открыть расширение обмена сообщениями из окна составить." border="false":::

### <a name="from-a-chat-message-or-channel-post"></a><span data-ttu-id="d19af-144">Из сообщения чата или сообщения канала</span><span class="sxs-lookup"><span data-stu-id="d19af-144">From a chat message or channel post</span></span>

После добавления пользователи могут выбрать значок **More** в сообщении чата или сообщении канала, чтобы найти команды действий :::image type="icon" source="../../assets/icons/teams-client-more.png"::: вашего расширения. <span data-ttu-id="d19af-146">Расширение может быть перечислены в **статье Дополнительные действия,** основанные на использовании.</span><span class="sxs-lookup"><span data-stu-id="d19af-146">Your extension may be listed under **More actions** based on usage.</span></span>

> [!NOTE]
> <span data-ttu-id="d19af-147">Поддержка дополнительных действий из сообщения чата или сообщения канала недоступна на мобильной платформе Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="d19af-147">Support for more actions from a chat message or channel post is not available on Microsoft Teams mobile platform.</span></span> 

#### <a name="chat-message"></a><span data-ttu-id="d19af-148">Сообщение чата</span><span class="sxs-lookup"><span data-stu-id="d19af-148">Chat message</span></span>

:::image type="content" source="../../assets/images/messaging-extension/open-from-chat-message.png" alt-text="В примере показано, как открыть расширение обмена сообщениями из сообщения чата." border="false":::

#### <a name="channel-post"></a><span data-ttu-id="d19af-150">Сообщение канала</span><span class="sxs-lookup"><span data-stu-id="d19af-150">Channel post</span></span>

:::image type="content" source="../../assets/images/messaging-extension/open-from-channel-post.png" alt-text="В примере показано, как открыть расширение обмена сообщениями из сообщения канала." border="false":::

## <a name="use-a-messaging-extension"></a><span data-ttu-id="d19af-152">Использование расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="d19af-152">Use a messaging extension</span></span>

<span data-ttu-id="d19af-153">В следующих сценариях покажут основные способы использования расширений обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="d19af-153">The following scenarios show the primary ways people use messaging extensions.</span></span>

### <a name="insert-content-into-a-message"></a><span data-ttu-id="d19af-154">Вставка контента в сообщение</span><span class="sxs-lookup"><span data-stu-id="d19af-154">Insert content into a message</span></span>

<span data-ttu-id="d19af-155">**1. Выберите расширение обмена сообщениями.**</span><span class="sxs-lookup"><span data-stu-id="d19af-155">**1. Select a messaging extension**.</span></span> <span data-ttu-id="d19af-156">Пользователи могут искать содержимое, которое они хотят поделиться из окна составить.</span><span class="sxs-lookup"><span data-stu-id="d19af-156">Users can search for the content they want to share from the compose box.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/insert-content-search.png" alt-text="В примере показано, как пользователь ищет содержимое для вставки из окне композитной записи." border="false":::

<span data-ttu-id="d19af-158">**2. Вставьте содержимое**.</span><span class="sxs-lookup"><span data-stu-id="d19af-158">**2. Insert content**.</span></span> <span data-ttu-id="d19af-159">После публикации другие могут отвечать или выбирать содержимое, чтобы увидеть дополнительные сведения в приложении.</span><span class="sxs-lookup"><span data-stu-id="d19af-159">Once posted, others can reply or select the content to see more information in your app.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/insert-content-posted.png" alt-text="В примере показана публикация контента пользователя в разговоре с каналом." border="false":::

### <a name="take-action-on-a-message"></a><span data-ttu-id="d19af-161">Действие по сообщению</span><span class="sxs-lookup"><span data-stu-id="d19af-161">Take action on a message</span></span>

<span data-ttu-id="d19af-162">**1. Выберите расширение обмена сообщениями.**</span><span class="sxs-lookup"><span data-stu-id="d19af-162">**1. Select a messaging extension**.</span></span> <span data-ttu-id="d19af-163">Ваше приложение может включать одну или несколько команд действий.</span><span class="sxs-lookup"><span data-stu-id="d19af-163">Your app can include one or more action commands.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/select-action-command.png" alt-text="В примере показано, как пользователь выбирает команду действий по расширению обмена сообщениями." border="false":::

<span data-ttu-id="d19af-165">**2. Завершить действие**.</span><span class="sxs-lookup"><span data-stu-id="d19af-165">**2. Complete the action**.</span></span> <span data-ttu-id="d19af-166">Ваше приложение может получать и обрабатывать любое содержимое или данные, отправленные действием сообщения.</span><span class="sxs-lookup"><span data-stu-id="d19af-166">Your app can receive and process any content or data sent by the message action.</span></span> <span data-ttu-id="d19af-167">Это позволяет пользователям оставаться в беседе и, в следующем примере, не беспокоиться о вводе сведений непосредственно в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="d19af-167">This allows users to remain in their conversation and, the following example, not worry about entering information directly in your app.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/complete-action-command.png" alt-text="В примере показано, как пользователь ищет содержимое для вставки из окне композитной записи." border="false":::

### <a name="preview-links"></a><span data-ttu-id="d19af-169">Предварительные ссылки</span><span class="sxs-lookup"><span data-stu-id="d19af-169">Preview links</span></span>

<span data-ttu-id="d19af-170">Расширения обмена сообщениями также позволяют вставлять богатые ссылки из распознаемого URL-адреса в сообщение (эта возможность называется [unfurling link unfurling.)](../../messaging-extensions/how-to/link-unfurling.md)</span><span class="sxs-lookup"><span data-stu-id="d19af-170">Messaging extensions also allow you to insert rich links from a recognized URL into a message (this capability is called [link unfurling](../../messaging-extensions/how-to/link-unfurling.md).)</span></span>

<span data-ttu-id="d19af-171">**1. Вклеить распознаемую ссылку** в поле составить.</span><span class="sxs-lookup"><span data-stu-id="d19af-171">**1. Paste a recognized link** in the compose box.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/paste-preview-link.png" alt-text="В примере показано, как пользователь вклеит ссылку в поле компоста." border="false":::

<span data-ttu-id="d19af-173">**2. Вставьте содержимое**.</span><span class="sxs-lookup"><span data-stu-id="d19af-173">**2. Insert content**.</span></span> <span data-ttu-id="d19af-174">Если ваше приложение распознает URL-адрес в окне композит, оно отрисовка ссылки в качестве карточки, которая обеспечивает богатый контентом предварительный просмотр веб-контента.</span><span class="sxs-lookup"><span data-stu-id="d19af-174">If your app recognizes the URL in the compose box, it renders the link as a card that provides a content-rich preview of the web content.</span></span> <span data-ttu-id="d19af-175">[(Дополнительные сведения](../../task-modules-and-cards/cards/design-effective-cards.md) см. в рекомендациях по разработке адаптивных карт.)</span><span class="sxs-lookup"><span data-stu-id="d19af-175">(See [Adaptive Cards design guidelines](../../task-modules-and-cards/cards/design-effective-cards.md) for more information.)</span></span>

:::image type="content" source="../../assets/images/messaging-extension/insert-preview-link.png" alt-text="В примере показано, как URL-адрес, так как он распознается вашим приложением, содержит в окне композитного контента некоторое содержимое." border="false":::

## <a name="manage-a-messaging-extension"></a><span data-ttu-id="d19af-177">Управление расширением обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="d19af-177">Manage a messaging extension</span></span>

<span data-ttu-id="d19af-178">Щелкнув правой кнопкой мыши значок, пользователи могут прикрепить, удалить или настроить расширение обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="d19af-178">By right clicking your icon, users can pin, remove, or configure your messaging extension.</span></span>

## <a name="anatomy"></a><span data-ttu-id="d19af-179">Анатомия</span><span class="sxs-lookup"><span data-stu-id="d19af-179">Anatomy</span></span>

### <a name="messaging-extension-in-the-compose-box"></a><span data-ttu-id="d19af-180">Расширение обмена сообщениями в окне составить</span><span class="sxs-lookup"><span data-stu-id="d19af-180">Messaging extension in the compose box</span></span>

<span data-ttu-id="d19af-181">В следующем примере можно привести расширение обмена сообщениями, открытое из окна составить.</span><span class="sxs-lookup"><span data-stu-id="d19af-181">The following example is a messaging extension opened from the compose box.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/anatomy-compose.png" alt-text="Иллюстрация, показывающая анатомию пользовательского интерфейса расширения обмена сообщениями в окне составить." border="false":::

|<span data-ttu-id="d19af-183">Счетчик</span><span class="sxs-lookup"><span data-stu-id="d19af-183">Counter</span></span>|<span data-ttu-id="d19af-184">Описание</span><span class="sxs-lookup"><span data-stu-id="d19af-184">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="d19af-185">1</span><span class="sxs-lookup"><span data-stu-id="d19af-185">1</span></span>|<span data-ttu-id="d19af-186">**Логотип приложения.** Значок цвета логотипа приложения.</span><span class="sxs-lookup"><span data-stu-id="d19af-186">**App logo**: Color icon of your app logo.</span></span>|
|<span data-ttu-id="d19af-187">2</span><span class="sxs-lookup"><span data-stu-id="d19af-187">2</span></span>|<span data-ttu-id="d19af-188">**Имя приложения.** Полное имя вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="d19af-188">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="d19af-189">3</span><span class="sxs-lookup"><span data-stu-id="d19af-189">3</span></span>|<span data-ttu-id="d19af-190">**Значок меню action commands (необязательный)**: Открывает список команд действий для расширения обмена сообщениями (если вы указываете их).</span><span class="sxs-lookup"><span data-stu-id="d19af-190">**Action commands menu icon (optional)**: Opens a list of action commands for your messaging extension (if you specify any).</span></span>
|<span data-ttu-id="d19af-191">4 </span><span class="sxs-lookup"><span data-stu-id="d19af-191">4</span></span>|<span data-ttu-id="d19af-192">**Поле поиска.** Позволяет пользователям находить содержимое приложения, которое они хотят вставить.</span><span class="sxs-lookup"><span data-stu-id="d19af-192">**Search box**: Allows users to find app content they want to insert.</span></span>|
|<span data-ttu-id="d19af-193">5 </span><span class="sxs-lookup"><span data-stu-id="d19af-193">5</span></span>|<span data-ttu-id="d19af-194">**Меню Tab (необязательный)**: предоставляет несколько категорий контента.</span><span class="sxs-lookup"><span data-stu-id="d19af-194">**Tab menu (optional)**: Provides multiple content categories.</span></span>|
|<span data-ttu-id="d19af-195">6 </span><span class="sxs-lookup"><span data-stu-id="d19af-195">6</span></span>|<span data-ttu-id="d19af-196">**Меню команд действий (необязательный)**: отображает список команд действий (если указаны какие-либо).</span><span class="sxs-lookup"><span data-stu-id="d19af-196">**Action commands menu (optional)**: Displays list of action commands (if you specify any).</span></span>|
|<span data-ttu-id="d19af-197">7 </span><span class="sxs-lookup"><span data-stu-id="d19af-197">7</span></span>|<span data-ttu-id="d19af-198">**Содержимое приложения.** В первую очередь для отображения результатов поиска.</span><span class="sxs-lookup"><span data-stu-id="d19af-198">**App content**: Primarily to display search results.</span></span> <span data-ttu-id="d19af-199">В этом примере используется макет списка (макет сетки — это другой вариант).</span><span class="sxs-lookup"><span data-stu-id="d19af-199">The example here is using the list layout (grid layout is another option).</span></span>|
|<span data-ttu-id="d19af-200">8 </span><span class="sxs-lookup"><span data-stu-id="d19af-200">8</span></span>|<span data-ttu-id="d19af-201">**Логотип приложения.** Значок контура логотипа приложения.</span><span class="sxs-lookup"><span data-stu-id="d19af-201">**App logo**: Outline icon of your app logo.</span></span>|

### <a name="messaging-extension-management-menu"></a><span data-ttu-id="d19af-202">Меню управления расширением обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="d19af-202">Messaging extension management menu</span></span>

:::image type="content" source="../../assets/images/messaging-extension/anatomy-management-menu.png" alt-text="Иллюстрация, показывающая анатомию пользовательского интерфейса меню управления расширением обмена сообщениями." border="false":::

|<span data-ttu-id="d19af-204">Счетчик</span><span class="sxs-lookup"><span data-stu-id="d19af-204">Counter</span></span>|<span data-ttu-id="d19af-205">Описание</span><span class="sxs-lookup"><span data-stu-id="d19af-205">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="d19af-206">1</span><span class="sxs-lookup"><span data-stu-id="d19af-206">1</span></span>|<span data-ttu-id="d19af-207">**Unpin.** Доступно, если пользователь прикрепил приложение.</span><span class="sxs-lookup"><span data-stu-id="d19af-207">**Unpin**: Available if the user has pinned your app.</span></span>|
|<span data-ttu-id="d19af-208">2</span><span class="sxs-lookup"><span data-stu-id="d19af-208">2</span></span>|<span data-ttu-id="d19af-209">**Удаление.** Удаляет расширение обмена сообщениями из канала, чата или собрания.</span><span class="sxs-lookup"><span data-stu-id="d19af-209">**Remove**: Removes the messaging extension from the channel, chat, or meeting.</span></span>|

## <a name="best-practices"></a><span data-ttu-id="d19af-210">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="d19af-210">Best practices</span></span>

### <a name="setup-and-general-usage"></a><span data-ttu-id="d19af-211">Настройка и общее использование</span><span class="sxs-lookup"><span data-stu-id="d19af-211">Setup and general usage</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-do.png" alt-text="Пример наилучшей практики расширения обмена сообщениями." border="false":::

#### <a name="do-integrate-with-single-sign-on"></a><span data-ttu-id="d19af-213">Do: Интеграция с одним входом</span><span class="sxs-lookup"><span data-stu-id="d19af-213">Do: Integrate with single-sign on</span></span>

<span data-ttu-id="d19af-214">SSO упрощает процесс регистрации, быстрее и обеспечивает безопасность.</span><span class="sxs-lookup"><span data-stu-id="d19af-214">SSO makes the sign-in process easier, faster, and secure.</span></span> <span data-ttu-id="d19af-215">Кроме того, если пользователь уже зарегистрировался в вашем личном приложении, для доступа к расширению обмена сообщениями также не нужно снова входить.</span><span class="sxs-lookup"><span data-stu-id="d19af-215">Also, if a user has already signed in to your personal app, they don’t have to also sign in again to access the messaging extension.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-dont.png" alt-text="Пример наилучшей практики расширения обмена сообщениями." border="false":::

#### <a name="dont-take-users-away-from-the-conversation"></a><span data-ttu-id="d19af-217">Не: отбирайте пользователей из беседы</span><span class="sxs-lookup"><span data-stu-id="d19af-217">Don't: Take users away from the conversation</span></span>

<span data-ttu-id="d19af-218">Расширения обмена сообщениями — это ярлыки, которые, как предполагается, уменьшают переключение контекста.</span><span class="sxs-lookup"><span data-stu-id="d19af-218">Messaging extensions are shortcuts that are supposed reduce context switching.</span></span> <span data-ttu-id="d19af-219">Например, расширение не должно направлять пользователей на веб-страницу за пределами Teams.</span><span class="sxs-lookup"><span data-stu-id="d19af-219">Your extension should not, for example, direct users to a webpage outside Teams.</span></span>

   :::column-end:::
:::row-end:::

#### <a name="do-highlight-your-messaging-extension"></a><span data-ttu-id="d19af-220">Do: Highlight your messaging extension</span><span class="sxs-lookup"><span data-stu-id="d19af-220">Do: Highlight your messaging extension</span></span>

<span data-ttu-id="d19af-221">Расширения обмена сообщениями не всегда легко найти.</span><span class="sxs-lookup"><span data-stu-id="d19af-221">Messaging extensions aren't always easy to find.</span></span> <span data-ttu-id="d19af-222">Включите скриншоты использования этого приложения на странице сведения о приложении.</span><span class="sxs-lookup"><span data-stu-id="d19af-222">Include screenshots of how to use it in your app details page.</span></span> <span data-ttu-id="d19af-223">Если в вашем приложении также есть бот, вы можете включить документацию по расширению обмена сообщениями в приветственный тур бота.</span><span class="sxs-lookup"><span data-stu-id="d19af-223">If your app also includes a bot, you can include messaging extension help documentation in a bot welcome tour.</span></span>

### <a name="templating"></a><span data-ttu-id="d19af-224">Templating</span><span class="sxs-lookup"><span data-stu-id="d19af-224">Templating</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-do.png" alt-text="Пример наилучшей практики расширения обмена сообщениями." border="false":::

#### <a name="do-let-teams-handle-some-of-the-design-work-if-possible"></a><span data-ttu-id="d19af-226">Do. Пусть Teams обрабатывает некоторые из работ по проектированию, если это возможно</span><span class="sxs-lookup"><span data-stu-id="d19af-226">Do: Let Teams handle some of the design work if possible</span></span>

<span data-ttu-id="d19af-227">Если это имеет смысл для случаев использования, рассмотрите возможность создания расширения обмена сообщениями на основе поиска.</span><span class="sxs-lookup"><span data-stu-id="d19af-227">If it makes sense for your use cases, consider creating a search-based messaging extension.</span></span> <span data-ttu-id="d19af-228">Teams передает эти типы расширений со встроенной темой и доступностью.</span><span class="sxs-lookup"><span data-stu-id="d19af-228">Teams renders these types of extensions with built-in theming and accessibility.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-dont.png" alt-text="Пример наилучшей практики расширения обмена сообщениями." border="false":::

#### <a name="dont-embed-your-entire-app-in-a-task-module"></a><span data-ttu-id="d19af-230">Не: встраить все приложение в модуль задач</span><span class="sxs-lookup"><span data-stu-id="d19af-230">Don't: Embed your entire app in a task module</span></span>

<span data-ttu-id="d19af-231">Если расширение обмена сообщениями требует команд действий, сохраняйте простой модуль задач и отображайте только компоненты, необходимые для выполнения действия.</span><span class="sxs-lookup"><span data-stu-id="d19af-231">If your messaging extension requires action commands, keep the task module simple and display only the components required to complete the action.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="d19af-232">Темы</span><span class="sxs-lookup"><span data-stu-id="d19af-232">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-do.png" alt-text="Пример наилучшей практики расширения обмена сообщениями." border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a><span data-ttu-id="d19af-234">Do: Воспользоваться преимуществами маркеров цвета Teams</span><span class="sxs-lookup"><span data-stu-id="d19af-234">Do: Take advantage of Teams color tokens</span></span>

<span data-ttu-id="d19af-235">Каждая тема Teams имеет свою цветовую схему.</span><span class="sxs-lookup"><span data-stu-id="d19af-235">Each Teams theme has its own color scheme.</span></span> <span data-ttu-id="d19af-236">Чтобы автоматически обрабатывать изменения темы, используйте маркеры цвета <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">(Fluent UI)</a> в своем дизайне.</span><span class="sxs-lookup"><span data-stu-id="d19af-236">To handle theme changes automatically, use <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a> in your design.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-dont.png" alt-text="Пример наилучшей практики расширения обмена сообщениями." border="false":::

#### <a name="dont-hard-code-color-values"></a><span data-ttu-id="d19af-238">Не: значения цвета жесткого кода</span><span class="sxs-lookup"><span data-stu-id="d19af-238">Don't: Hard code color values</span></span>

<span data-ttu-id="d19af-239">Если вы не используете цветные маркеры Teams, ваши проекты будут менее масштабируемыми и на управление ими будет уйма времени.</span><span class="sxs-lookup"><span data-stu-id="d19af-239">If you don't use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::

### <a name="actions"></a><span data-ttu-id="d19af-240">Действия</span><span class="sxs-lookup"><span data-stu-id="d19af-240">Actions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-do.png" alt-text="Пример наилучшей практики расширения обмена сообщениями." border="false":::

#### <a name="do-include-action-commands-that-make-sense-in-context"></a><span data-ttu-id="d19af-242">Do: Включить команды действий, которые в контексте являются смыслом</span><span class="sxs-lookup"><span data-stu-id="d19af-242">Do: Include action commands that make sense in context</span></span>

<span data-ttu-id="d19af-243">Действия сообщения должны относиться к тем, на что смотрит пользователь.</span><span class="sxs-lookup"><span data-stu-id="d19af-243">Message actions should relate to what a user is looking at.</span></span> <span data-ttu-id="d19af-244">Например, укажи пользователям ярлык для создания проблемы или рабочих элементов с помощью текста в чьей-либо публикации.</span><span class="sxs-lookup"><span data-stu-id="d19af-244">For example, provide users a shortcut for creating an issue or work item using the text in someone’s post.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-dont.png" alt-text="Пример наилучшей практики расширения обмена сообщениями." border="false":::

#### <a name="dont-include-actions-commands-that-arent-contextual"></a><span data-ttu-id="d19af-246">Не: включайте не контекстуальные команды действий</span><span class="sxs-lookup"><span data-stu-id="d19af-246">Don't: Include actions commands that aren't contextual</span></span>

<span data-ttu-id="d19af-247">Действие сообщения для **просмотра панели мониторинга** может показаться отключенным от большинства бесед.</span><span class="sxs-lookup"><span data-stu-id="d19af-247">A message action to **View your dashboard** would probably seem disconnected from most conversations.</span></span>

   :::column-end:::
:::row-end:::

### <a name="searches"></a><span data-ttu-id="d19af-248">Поиск</span><span class="sxs-lookup"><span data-stu-id="d19af-248">Searches</span></span>

#### <a name="do-show-search-results-while-typing"></a><span data-ttu-id="d19af-249">Do: Показать результаты поиска при вводе</span><span class="sxs-lookup"><span data-stu-id="d19af-249">Do: Show search results while typing</span></span>

<span data-ttu-id="d19af-250">Предоставление предлагаемых результатов поиска при введите пользователей.</span><span class="sxs-lookup"><span data-stu-id="d19af-250">Provide suggested search results while users type.</span></span> <span data-ttu-id="d19af-251">Они могут быстрее находить нужный контент с минимальным количеством символов.</span><span class="sxs-lookup"><span data-stu-id="d19af-251">They may find the content they need faster with minimal amount of characters.</span></span>

#### <a name="dont-require-users-to-submit-a-query"></a><span data-ttu-id="d19af-252">Не: требовать от пользователей отправки запроса</span><span class="sxs-lookup"><span data-stu-id="d19af-252">Don't: Require users to submit a query</span></span>

<span data-ttu-id="d19af-253">Вы можете заставить пользователей нажать клавишу или выбрать кнопку для отправки запросов в ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="d19af-253">You can make users press a key or select a button to send queries to your app.</span></span> <span data-ttu-id="d19af-254">Хотя это может быть проще в службе служб приложений, люди могут быть смущены тем, что они не видят результатов поиска в режиме реального времени, как они введите.</span><span class="sxs-lookup"><span data-stu-id="d19af-254">While that may be easier on your app services service, people may be confused that they're not seeing real-time search results as they type.</span></span>

#### <a name="do-consider-zero-term-queries"></a><span data-ttu-id="d19af-255">Do: Рассмотрите запросы с нулевым сроком</span><span class="sxs-lookup"><span data-stu-id="d19af-255">Do: Consider zero-term queries</span></span>

<span data-ttu-id="d19af-256">Например, перед тем, как пользователь записывает что-либо в поле поиска, отобразите то, что он последний раз просматривал в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="d19af-256">For example, before a user writes anything in the search box, display what they last viewed on your app.</span></span> <span data-ttu-id="d19af-257">Вполне возможно, что они хотят вставить этот контент в беседу.</span><span class="sxs-lookup"><span data-stu-id="d19af-257">It's possible that they want to insert that content into their conversation.</span></span>

## <a name="validate-your-design"></a><span data-ttu-id="d19af-258">Проверка дизайна</span><span class="sxs-lookup"><span data-stu-id="d19af-258">Validate your design</span></span>

<span data-ttu-id="d19af-259">Если вы планируете опубликовать приложение в AppSource, необходимо понять проблемы проектирования, которые обычно приводят к сбойу приложений во время отправки.</span><span class="sxs-lookup"><span data-stu-id="d19af-259">If you plan to publish your app to AppSource, you should understand the design issues that commonly cause apps to fail during submission.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d19af-260">Проверка рекомендаций по проверке конструкции</span><span class="sxs-lookup"><span data-stu-id="d19af-260">Check design validation guidelines</span></span>](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
