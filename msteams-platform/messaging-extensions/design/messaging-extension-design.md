---
title: Разработка расширения обмена сообщениями
description: Узнайте, как разработать расширение системы обмена сообщениями Teams и получить набор пользовательских интерфейсов Microsoft Teams.
keywords: рекомендации по проектированию Teams Справочник по расширениям обмена сообщениями советы
author: heath-hamilton
ms.author: qinch
ms.topic: conceptual
ms.openlocfilehash: ad628bdaa46058aed4acdcea1a224c7ebfe40f89
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/09/2020
ms.locfileid: "49604855"
---
# <a name="designing-your-microsoft-teams-messaging-extension"></a><span data-ttu-id="c7c1c-104">Разработка расширения обмена сообщениями Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="c7c1c-104">Designing your Microsoft Teams messaging extension</span></span>

<span data-ttu-id="c7c1c-105">Расширения обмена сообщениями — это ярлыки для вставки контента приложения или работы с сообщением без перехода от беседы.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-105">Messaging extensions are shortcuts for inserting app content or acting on a message without navigating away from the conversation.</span></span>

<span data-ttu-id="c7c1c-106">В следующей статье описываются способы добавления и использования расширений обмена сообщениями в Teams, а также управления ими.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-106">To guide your app design, the following information describes and illustrates how people can add, use, and manage messaging extensions in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="c7c1c-107">Набор элементов пользовательского интерфейса Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="c7c1c-107">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="c7c1c-108">Вы можете найти подробные рекомендации по проектированию расширений сообщений, в том числе элементы, которые можно прихватить и изменить при необходимости, в наборе элементов Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-108">You can find comprehensive messaging extension design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c7c1c-109">Получение набора элементов пользовательского интерфейса Microsoft Teams (фигма)</span><span class="sxs-lookup"><span data-stu-id="c7c1c-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-messaging-extension"></a><span data-ttu-id="c7c1c-110">Добавление расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="c7c1c-110">Add a messaging extension</span></span>

<span data-ttu-id="c7c1c-111">Вы можете добавить расширение системы обмена сообщениями в следующих контекстах команд:</span><span class="sxs-lookup"><span data-stu-id="c7c1c-111">You can add a messaging extension in the following Teams contexts:</span></span>

* <span data-ttu-id="c7c1c-112">Из хранилища Teams (AppSource).</span><span class="sxs-lookup"><span data-stu-id="c7c1c-112">From the Teams store (AppSource).</span></span>
* <span data-ttu-id="c7c1c-113">В канале, чате или собрании (до, во время и после) в поле "создание".</span><span class="sxs-lookup"><span data-stu-id="c7c1c-113">In a channel, chat, or meeting (before, during, and after) near the compose box.</span></span> <span data-ttu-id="c7c1c-114">Стоит отметить, что если вы добавите расширение обмена сообщениями в одном из этих мест, то можете использовать его только в этом контексте.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-114">It's worth noting if you add a messaging extension in one of these places, only you can use it in that context.</span></span>

<span data-ttu-id="c7c1c-115">В приведенном ниже примере показано, как добавить расширение обмена сообщениями в канале.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-115">The following example shows how you add a messaging extension in a channel.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/add-in-channel.png" alt-text="Пример показывает, как добавить расширение обмена сообщениями рядом с полем &quot;создание&quot; в канале." border="false":::

## <a name="set-up-a-messaging-extension"></a><span data-ttu-id="c7c1c-117">Настройка расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="c7c1c-117">Set up a messaging extension</span></span>

<span data-ttu-id="c7c1c-118">Проверка подлинности не обязательна, но если ваше приложение аналогично средству отслеживания билетов, для входа в систему можно использовать расширение обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-118">Authentication isn't mandatory, but if your app is something like a ticket tracking tool, you may need people to sign in to use the messaging extension.</span></span>

<span data-ttu-id="c7c1c-119">Для согласованности в приложениях Teams невозможно настроить экран входа.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-119">For consistency across Teams apps, you can't customize the sign-in screen.</span></span> <span data-ttu-id="c7c1c-120">При использовании проверки подлинности с использованием единого входа пользователи автоматически подписываются.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-120">If you use single sign-on (SSO) authentication, users are signed in automatically.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/set-up.png" alt-text="В примере отображается экран Настройка расширения обмена сообщениями с кнопкой входа." border="false":::

## <a name="types-of-messaging-extensions"></a><span data-ttu-id="c7c1c-122">Типы расширений обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="c7c1c-122">Types of messaging extensions</span></span>

<span data-ttu-id="c7c1c-123">Расширения для обмена сообщениями могут иметь команды поиска, команды действий или и то, и другое.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-123">Messaging extensions can have search commands, action commands, or both.</span></span> <span data-ttu-id="c7c1c-124">Ваши команды зависят от компонентов приложения и от того, как они соответствуют вариантам использования в Teams.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-124">Your commands depend on your app's features and how those fit within Teams use cases.</span></span>

### <a name="search-commands"></a><span data-ttu-id="c7c1c-125">Команды поиска</span><span class="sxs-lookup"><span data-stu-id="c7c1c-125">Search commands</span></span>

<span data-ttu-id="c7c1c-126">С помощью команд поиска пользователи могут быстро находить внешний контент и вставлять их в сообщения с помощью расширения для обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-126">With search commands, people can use your messaging extension to quickly find external content and insert into a message.</span></span> <span data-ttu-id="c7c1c-127">Команды поиска обычно становятся доступными в поле "создание".</span><span class="sxs-lookup"><span data-stu-id="c7c1c-127">Search commands are commonly made available in the compose box.</span></span> <span data-ttu-id="c7c1c-128">Например, вы можете начать или добавить обсуждение, выполнив общий доступ к содержимому, не покидая Teams.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-128">For example, you can start or add to a discussion by sharing a piece of content—without ever leaving Teams.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/search-command-type.png" alt-text="В примере показано расширение обмена сообщениями на основе поиска, запущенное из поля создать." border="false":::

#### <a name="compose-box-layout-options"></a><span data-ttu-id="c7c1c-130">Параметры макета поля создания</span><span class="sxs-lookup"><span data-stu-id="c7c1c-130">Compose box layout options</span></span>

<span data-ttu-id="c7c1c-131">Существует несколько способов отображения результатов поиска для расширения системы обмена сообщениями, в том числе [представления списка и таблицы](../../messaging-Ask about extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests).</span><span class="sxs-lookup"><span data-stu-id="c7c1c-131">You have some options for displaying messaging extension search results, including [list and grid views](../../messaging-Ask about extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests).</span></span>

:::image type="content" source="../../assets/images/messaging-extension/search-result-layout.png" alt-text="Иллюстрация, на которой показаны параметры макета для результатов поиска расширения системы обмена сообщениями." border="false":::

### <a name="action-commands"></a><span data-ttu-id="c7c1c-133">Команды действий</span><span class="sxs-lookup"><span data-stu-id="c7c1c-133">Action commands</span></span>

<span data-ttu-id="c7c1c-134">Команды действий позволяют пользователям запускать действия и обрабатывать запросы во внешних службах в Teams.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-134">Action commands allow people to trigger actions and process requests in external services within Teams.</span></span> <span data-ttu-id="c7c1c-135">Например, если ваше приложение отслеживает заказы, пользователь может создать новый заказ, используя содержимое сообщения коллеги непосредственно внутри разговора.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-135">For example, if your app tracks orders, a user could create a new order using the contents of a colleague’s message from right inside their chat.</span></span>

<span data-ttu-id="c7c1c-136">Расширения для обмена сообщениями на основе действий часто требуют, чтобы пользователи выполнили форму или другой тип конфигурации в модальном виде.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-136">Action-based messaging extensions frequently require users to complete a form or some other kind of configuration within a modal.</span></span> <span data-ttu-id="c7c1c-137">Эти возможности можно создавать с помощью [модулей задач](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).</span><span class="sxs-lookup"><span data-stu-id="c7c1c-137">You can create these experiences with [task modules](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).</span></span>

## <a name="open-a-messaging-extension"></a><span data-ttu-id="c7c1c-138">Открытие расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="c7c1c-138">Open a messaging extension</span></span>

<span data-ttu-id="c7c1c-139">Поле создания и сообщения/записи — это основные контексты, в которых люди используют расширения для обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-139">The compose box and messages/posts are the primary contexts where people use messaging extensions.</span></span>

### <a name="from-the-compose-box"></a><span data-ttu-id="c7c1c-140">Из поля "создание"</span><span class="sxs-lookup"><span data-stu-id="c7c1c-140">From the compose box</span></span>

<span data-ttu-id="c7c1c-141">После добавления пользователи могут открыть свой модуль обмена сообщениями, выбрав значок приложения под полем "создание".</span><span class="sxs-lookup"><span data-stu-id="c7c1c-141">Once added, users can open your messaging extension by selecting your app icon below the compose box.</span></span> <span data-ttu-id="c7c1c-142">В этом примере у расширения есть команды поиска и действий.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-142">In this example, the extension has search and action commands.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/open-from-compose-box.png" alt-text="В примере показано, как открыть расширение системы обмена сообщениями из поля &quot;создание&quot;." border="false":::

### <a name="from-a-chat-message-or-channel-post"></a><span data-ttu-id="c7c1c-144">Из сообщения чата или записи в канале</span><span class="sxs-lookup"><span data-stu-id="c7c1c-144">From a chat message or channel post</span></span>

После добавления пользователи могут выбрать значок **More (дополнительные** ) :::image type="icon" source="../../assets/icons/teams-client-more.png"::: в сообщении чата или канале POST, чтобы найти команды действий расширения. <span data-ttu-id="c7c1c-146">Ваш добавочный номер может отображаться в разделе **Дополнительные действия** в зависимости от использования.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-146">Your extension may be listed under **More actions** based on usage.</span></span>

#### <a name="chat-message"></a><span data-ttu-id="c7c1c-147">Сообщение чата</span><span class="sxs-lookup"><span data-stu-id="c7c1c-147">Chat message</span></span>

:::image type="content" source="../../assets/images/messaging-extension/open-from-chat-message.png" alt-text="В примере показано, как открыть расширение обмена сообщениями из сообщения чата." border="false":::

#### <a name="channel-post"></a><span data-ttu-id="c7c1c-149">POST канала</span><span class="sxs-lookup"><span data-stu-id="c7c1c-149">Channel post</span></span>

:::image type="content" source="../../assets/images/messaging-extension/open-from-channel-post.png" alt-text="В примере показано, как открыть расширение обмена сообщениями из канала POST." border="false":::

## <a name="use-a-messaging-extension"></a><span data-ttu-id="c7c1c-151">Использование расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="c7c1c-151">Use a messaging extension</span></span>

<span data-ttu-id="c7c1c-152">В следующих сценариях показаны основные способы использования расширений обмена сообщениями для пользователей.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-152">The following scenarios show the primary ways people use messaging extensions.</span></span>

### <a name="insert-content-into-a-message"></a><span data-ttu-id="c7c1c-153">Вставка контента в сообщение</span><span class="sxs-lookup"><span data-stu-id="c7c1c-153">Insert content into a message</span></span>

<span data-ttu-id="c7c1c-154">**1. Выберите расширение системы обмена сообщениями**.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-154">**1. Select a messaging extension**.</span></span> <span data-ttu-id="c7c1c-155">Пользователи могут искать контент, к которому они хотят предоставить доступ, из поля "создание".</span><span class="sxs-lookup"><span data-stu-id="c7c1c-155">Users can search for the content they want to share from the compose box.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/insert-content-search.png" alt-text="Пример показывает, как пользователь выполняет поиск контента для вставки из поля &quot;создание&quot;." border="false":::

<span data-ttu-id="c7c1c-157">**2. Вставьте контент**.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-157">**2. Insert content**.</span></span> <span data-ttu-id="c7c1c-158">После публикации другие пользователи могут ответить или выбрать контент, чтобы просмотреть дополнительные сведения в приложении.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-158">Once posted, others can reply or select the content to see more information in your app.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/insert-content-posted.png" alt-text="Пример показывает, что пользователь разбивает контент в беседе канала." border="false":::

### <a name="take-action-on-a-message"></a><span data-ttu-id="c7c1c-160">Выполнение действий с сообщением</span><span class="sxs-lookup"><span data-stu-id="c7c1c-160">Take action on a message</span></span>

<span data-ttu-id="c7c1c-161">**1. Выберите расширение системы обмена сообщениями**.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-161">**1. Select a messaging extension**.</span></span> <span data-ttu-id="c7c1c-162">Ваше приложение может включать одну или несколько команд действий.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-162">Your app can include one or more action commands.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/select-action-command.png" alt-text="Пример показывает, как пользователь выбирает команду действия расширения системы обмена сообщениями." border="false":::

<span data-ttu-id="c7c1c-164">**2. Выполните действие**.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-164">**2. Complete the action**.</span></span> <span data-ttu-id="c7c1c-165">Ваше приложение может получать и обрабатывать любые контент или данные, отправленные действием Message.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-165">Your app can receive and process any content or data sent by the message action.</span></span> <span data-ttu-id="c7c1c-166">Это позволяет пользователям оставить беседу в беседе и, в следующем примере, не беспокоиться о вводе информации непосредственно в приложении.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-166">This allows users to remain in their conversation and, the following example, not worry about entering information directly in your app.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/complete-action-command.png" alt-text="Пример показывает, как пользователь выполняет поиск контента для вставки из поля &quot;создание&quot;." border="false":::

### <a name="preview-links"></a><span data-ttu-id="c7c1c-168">Ссылки для предварительного просмотра</span><span class="sxs-lookup"><span data-stu-id="c7c1c-168">Preview links</span></span>

<span data-ttu-id="c7c1c-169">Расширения обмена сообщениями также позволяют вставлять в сообщение ссылки на распознаваемые URL-адреса (Эта возможность называется [Link унфурлинг](../../messaging-extensions/how-to/link-unfurling.md).)</span><span class="sxs-lookup"><span data-stu-id="c7c1c-169">Messaging extensions also allow you to insert rich links from a recognized URL into a message (this capability is called [link unfurling](../../messaging-extensions/how-to/link-unfurling.md).)</span></span>

<span data-ttu-id="c7c1c-170">**1. Вставьте распознанную ссылку** в поле "создание".</span><span class="sxs-lookup"><span data-stu-id="c7c1c-170">**1. Paste a recognized link** in the compose box.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/paste-preview-link.png" alt-text="В примере показано, как пользователь вставил ссылку в поле компост." border="false":::

<span data-ttu-id="c7c1c-172">**2. Вставьте контент**.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-172">**2. Insert content**.</span></span> <span data-ttu-id="c7c1c-173">Если ваше приложение распознает URL-адрес в поле "создание", он отображает ссылку в виде карточки, которая обеспечивает полный предварительный просмотр веб-контента.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-173">If your app recognizes the URL in the compose box, it renders the link as a card that provides a content-rich preview of the web content.</span></span> <span data-ttu-id="c7c1c-174">(См. [рекомендации по проектированию адаптивных карточек](../../task-modules-and-cards/cards/design-effective-cards.md) для получения дополнительной информации.)</span><span class="sxs-lookup"><span data-stu-id="c7c1c-174">(See [Adaptive Cards design guidelines](../../task-modules-and-cards/cards/design-effective-cards.md) for more information.)</span></span>

:::image type="content" source="../../assets/images/messaging-extension/insert-preview-link.png" alt-text="В примере показано, как URL-адрес, так как он распознается вашим приложением, включает в себя некоторый обширный контент в поле &quot;создание&quot;." border="false":::

## <a name="manage-a-messaging-extension"></a><span data-ttu-id="c7c1c-176">Управление расширением обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="c7c1c-176">Manage a messaging extension</span></span>

<span data-ttu-id="c7c1c-177">Щелкнув значок правой кнопкой мыши, пользователи могут закреплять, удалять или настраивать расширение системы обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-177">By right clicking your icon, users can pin, remove, or configure your messaging extension.</span></span>

## <a name="anatomy"></a><span data-ttu-id="c7c1c-178">Составляющие</span><span class="sxs-lookup"><span data-stu-id="c7c1c-178">Anatomy</span></span>

### <a name="messaging-extension-in-the-compose-box"></a><span data-ttu-id="c7c1c-179">Расширение обмена сообщениями в поле "создание"</span><span class="sxs-lookup"><span data-stu-id="c7c1c-179">Messaging extension in the compose box</span></span>

<span data-ttu-id="c7c1c-180">Ниже приведен пример расширения обмена сообщениями, открытого из поля "создание".</span><span class="sxs-lookup"><span data-stu-id="c7c1c-180">The following example is a messaging extension opened from the compose box.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/anatomy-compose.png" alt-text="Иллюстрация, демонстрирующая пользовательский интерфейс расширения для обмена сообщениями в поле &quot;создание&quot;." border="false":::

|<span data-ttu-id="c7c1c-182">Счетчик</span><span class="sxs-lookup"><span data-stu-id="c7c1c-182">Counter</span></span>|<span data-ttu-id="c7c1c-183">Описание</span><span class="sxs-lookup"><span data-stu-id="c7c1c-183">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="c7c1c-184">1</span><span class="sxs-lookup"><span data-stu-id="c7c1c-184">1</span></span>|<span data-ttu-id="c7c1c-185">**Логотип приложения**: значок цвета эмблемы приложения.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-185">**App logo**: Color icon of your app logo.</span></span>|
|<span data-ttu-id="c7c1c-186">2 </span><span class="sxs-lookup"><span data-stu-id="c7c1c-186">2</span></span>|<span data-ttu-id="c7c1c-187">**Имя приложения**: полное имя приложения.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-187">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="c7c1c-188">3 </span><span class="sxs-lookup"><span data-stu-id="c7c1c-188">3</span></span>|<span data-ttu-id="c7c1c-189">**Значок меню команд действий (необязательно)**: открывает список команд действий для расширения системы обмена сообщениями (если вы указали его).</span><span class="sxs-lookup"><span data-stu-id="c7c1c-189">**Action commands menu icon (optional)**: Opens a list of action commands for your messaging extension (if you specify any).</span></span>
|<span data-ttu-id="c7c1c-190">4 </span><span class="sxs-lookup"><span data-stu-id="c7c1c-190">4</span></span>|<span data-ttu-id="c7c1c-191">**Поле поиска**: позволяет пользователям находить контент приложений, которые они хотят вставить.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-191">**Search box**: Allows users to find app content they want to insert.</span></span>|
|<span data-ttu-id="c7c1c-192">5 </span><span class="sxs-lookup"><span data-stu-id="c7c1c-192">5</span></span>|<span data-ttu-id="c7c1c-193">**Меню вкладок (необязательно)**: предоставляет несколько категорий контента.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-193">**Tab menu (optional)**: Provides multiple content categories.</span></span>|
|<span data-ttu-id="c7c1c-194">6 </span><span class="sxs-lookup"><span data-stu-id="c7c1c-194">6</span></span>|<span data-ttu-id="c7c1c-195">**Меню команд действий (необязательно)**: отображает список команд действий (если вы указали их).</span><span class="sxs-lookup"><span data-stu-id="c7c1c-195">**Action commands menu (optional)**: Displays list of action commands (if you specify any).</span></span>|
|<span data-ttu-id="c7c1c-196">7 </span><span class="sxs-lookup"><span data-stu-id="c7c1c-196">7</span></span>|<span data-ttu-id="c7c1c-197">**Контент приложения**: в первую очередь для отображения результатов поиска.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-197">**App content**: Primarily to display search results.</span></span> <span data-ttu-id="c7c1c-198">В этом примере используется макет списка (макет сетки — другой вариант).</span><span class="sxs-lookup"><span data-stu-id="c7c1c-198">The example here is using the list layout (grid layout is another option).</span></span>|
|<span data-ttu-id="c7c1c-199">8 </span><span class="sxs-lookup"><span data-stu-id="c7c1c-199">8</span></span>|<span data-ttu-id="c7c1c-200">**Логотип приложения**: значок структуры эмблемы приложения.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-200">**App logo**: Outline icon of your app logo.</span></span>|

### <a name="messaging-extension-management-menu"></a><span data-ttu-id="c7c1c-201">Меню управления расширениями обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="c7c1c-201">Messaging extension management menu</span></span>

:::image type="content" source="../../assets/images/messaging-extension/anatomy-management-menu.png" alt-text="Иллюстрация, на которой показана структура пользовательского интерфейса меню управления расширениями для обмена сообщениями." border="false":::

|<span data-ttu-id="c7c1c-203">Счетчик</span><span class="sxs-lookup"><span data-stu-id="c7c1c-203">Counter</span></span>|<span data-ttu-id="c7c1c-204">Описание</span><span class="sxs-lookup"><span data-stu-id="c7c1c-204">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="c7c1c-205">1</span><span class="sxs-lookup"><span data-stu-id="c7c1c-205">1</span></span>|<span data-ttu-id="c7c1c-206">**Открепить**: доступно, если пользователь закрепляет ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-206">**Unpin**: Available if the user has pinned your app.</span></span>|
|<span data-ttu-id="c7c1c-207">2 </span><span class="sxs-lookup"><span data-stu-id="c7c1c-207">2</span></span>|<span data-ttu-id="c7c1c-208">**Удалить**: удаляет расширение обмена сообщениями из канала, чата или собрания.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-208">**Remove**: Removes the messaging extension from the channel, chat, or meeting.</span></span>|

## <a name="best-practices"></a><span data-ttu-id="c7c1c-209">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="c7c1c-209">Best practices</span></span>

### <a name="setup-and-general-usage"></a><span data-ttu-id="c7c1c-210">Настройка и общие сведения об использовании</span><span class="sxs-lookup"><span data-stu-id="c7c1c-210">Setup and general usage</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-do.png" alt-text="Пример, в котором показана рекомендация расширения для обмена сообщениями." border="false":::

#### <a name="do-integrate-with-single-sign-on"></a><span data-ttu-id="c7c1c-212">Do: интеграция с единым входом</span><span class="sxs-lookup"><span data-stu-id="c7c1c-212">Do: Integrate with single-sign on</span></span>

<span data-ttu-id="c7c1c-213">ЕДИНЫЙ вход упрощает, ускоряет и обеспечивает безопасность процесса входа.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-213">SSO makes the sign-in process easier, faster, and secure.</span></span> <span data-ttu-id="c7c1c-214">Кроме того, если пользователь уже выполнил вход в личное приложение, ему не придется повторно выполнять вход для доступа к расширению системы обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-214">Also, if a user has already signed in to your personal app, they don’t have to also sign in again to access the messaging extension.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-dont.png" alt-text="Пример, в котором показана рекомендация расширения для обмена сообщениями." border="false":::

#### <a name="dont-take-users-away-from-the-conversation"></a><span data-ttu-id="c7c1c-216">Не отвлекайте пользователей от беседы.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-216">Don't: Take users away from the conversation</span></span>

<span data-ttu-id="c7c1c-217">Расширения обмена сообщениями — это те, которые предположительно уменьшают контекстное переключение.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-217">Messaging extensions are shortcuts that are supposed reduce context switching.</span></span> <span data-ttu-id="c7c1c-218">Ваш добавочный номер не должен, например, направлять пользователей на веб-страницу за пределами Teams.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-218">Your extension should not, for example, direct users to a webpage outside Teams.</span></span>

   :::column-end:::
:::row-end:::

#### <a name="do-highlight-your-messaging-extension"></a><span data-ttu-id="c7c1c-219">Do: выделите свой добавочный номер для обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="c7c1c-219">Do: Highlight your messaging extension</span></span>

<span data-ttu-id="c7c1c-220">Расширения обмена сообщениями не всегда просты в поиске.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-220">Messaging extensions aren't always easy to find.</span></span> <span data-ttu-id="c7c1c-221">Включите снимки экрана, которые можно использовать на странице сведений о приложении.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-221">Include screenshots of how to use it in your app details page.</span></span> <span data-ttu-id="c7c1c-222">Если ваше приложение также содержит Bot, вы можете включить справочную документацию по расширению системы обмена сообщениями в начальном начальном экране ленты.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-222">If your app also includes a bot, you can include messaging extension help documentation in a bot welcome tour.</span></span>

### <a name="templating"></a><span data-ttu-id="c7c1c-223">Создание</span><span class="sxs-lookup"><span data-stu-id="c7c1c-223">Templating</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-do.png" alt-text="Пример, в котором показана рекомендация расширения для обмена сообщениями." border="false":::

#### <a name="do-let-teams-handle-some-of-the-design-work-if-possible"></a><span data-ttu-id="c7c1c-225">Do: разрешить командам по возможности обрабатывать некоторые задачи по проектированию</span><span class="sxs-lookup"><span data-stu-id="c7c1c-225">Do: Let Teams handle some of the design work if possible</span></span>

<span data-ttu-id="c7c1c-226">Если это имеет смысл для вариантов использования, рекомендуется создать расширение для обмена сообщениями на основе поиска.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-226">If it makes sense for your use cases, consider creating a search-based messaging extension.</span></span> <span data-ttu-id="c7c1c-227">Teams отрисовывает эти типы расширений с помощью встроенных функций и специальных возможностей.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-227">Teams renders these types of extensions with built-in theming and accessibility.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-dont.png" alt-text="Пример, в котором показана рекомендация расширения для обмена сообщениями." border="false":::

#### <a name="dont-embed-your-entire-app-in-a-task-module"></a><span data-ttu-id="c7c1c-229">Не все: внедрите приложение в модуль задач</span><span class="sxs-lookup"><span data-stu-id="c7c1c-229">Don't: Embed your entire app in a task module</span></span>

<span data-ttu-id="c7c1c-230">Если для расширения системы обмена сообщениями требуются команды действий, оставьте модуль задач простым и отобразите только компоненты, необходимые для выполнения действия.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-230">If your messaging extension requires action commands, keep the task module simple and display only the components required to complete the action.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="c7c1c-231">Темы</span><span class="sxs-lookup"><span data-stu-id="c7c1c-231">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-do.png" alt-text="Пример, в котором показана рекомендация расширения для обмена сообщениями." border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a><span data-ttu-id="c7c1c-233">Do: Воспользуйтесь преимуществами цветовых маркеров для Teams</span><span class="sxs-lookup"><span data-stu-id="c7c1c-233">Do: Take advantage of Teams color tokens</span></span>

<span data-ttu-id="c7c1c-234">У каждой темы Teams есть своя цветовая схема.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-234">Each Teams theme has its own color scheme.</span></span> <span data-ttu-id="c7c1c-235">Для автоматической обработки изменений темы используйте <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">маркеры цветов (пользовательский интерфейс Fluent)</a> .</span><span class="sxs-lookup"><span data-stu-id="c7c1c-235">To handle theme changes automatically, use <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a> in your design.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-dont.png" alt-text="Пример, в котором показана рекомендация расширения для обмена сообщениями." border="false":::

#### <a name="dont-hard-code-color-values"></a><span data-ttu-id="c7c1c-237">Не: значения цвета жесткого кода</span><span class="sxs-lookup"><span data-stu-id="c7c1c-237">Don't: Hard code color values</span></span>

<span data-ttu-id="c7c1c-238">Если вы не используете цветовые маркеры для работы с группами, ваши макеты будут менее масштабируемыми и занимать больше времени на управление.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-238">If you don't use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::

### <a name="actions"></a><span data-ttu-id="c7c1c-239">Действия</span><span class="sxs-lookup"><span data-stu-id="c7c1c-239">Actions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-do.png" alt-text="Пример, в котором показана рекомендация расширения для обмена сообщениями." border="false":::

#### <a name="do-include-action-commands-that-make-sense-in-context"></a><span data-ttu-id="c7c1c-241">Do: Включение команд действий, которые имеют смысл в контексте</span><span class="sxs-lookup"><span data-stu-id="c7c1c-241">Do: Include action commands that make sense in context</span></span>

<span data-ttu-id="c7c1c-242">Действия с сообщениями должны относиться к тем, что пользователь ищет.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-242">Message actions should relate to what a user is looking at.</span></span> <span data-ttu-id="c7c1c-243">Например, предоставьте пользователям ярлык для создания вопроса или рабочего элемента с помощью текста в записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-243">For example, provide users a shortcut for creating an issue or work item using the text in someone’s post.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-dont.png" alt-text="Пример, в котором показана рекомендация расширения для обмена сообщениями." border="false":::

#### <a name="dont-include-actions-commands-that-arent-contextual"></a><span data-ttu-id="c7c1c-245">Не: включить команды действий, не являющиеся контекстными</span><span class="sxs-lookup"><span data-stu-id="c7c1c-245">Don't: Include actions commands that aren't contextual</span></span>

<span data-ttu-id="c7c1c-246">Действие с сообщением для **просмотра панели мониторинга** , скорее всего, не будет отсоединено от большинства бесед.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-246">A message action to **View your dashboard** would probably seem disconnected from most conversations.</span></span>

   :::column-end:::
:::row-end:::

### <a name="searches"></a><span data-ttu-id="c7c1c-247">Выполняет</span><span class="sxs-lookup"><span data-stu-id="c7c1c-247">Searches</span></span>

#### <a name="do-show-search-results-while-typing"></a><span data-ttu-id="c7c1c-248">Do: отображение результатов поиска при вводе текста</span><span class="sxs-lookup"><span data-stu-id="c7c1c-248">Do: Show search results while typing</span></span>

<span data-ttu-id="c7c1c-249">Предоставление предлагаемых результатов поиска при вводе пользователями.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-249">Provide suggested search results while users type.</span></span> <span data-ttu-id="c7c1c-250">Они могут находить нужные вам материалы быстрее с минимальным количеством символов.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-250">They may find the content they need faster with minimal amount of characters.</span></span>

#### <a name="dont-require-users-to-submit-a-query"></a><span data-ttu-id="c7c1c-251">Не требовать от пользователей отправки запроса.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-251">Don't: Require users to submit a query</span></span>

<span data-ttu-id="c7c1c-252">Вы можете сделать так, чтобы пользователи нажмет клавишу или выбрали кнопку для отправки запросов в свое приложение.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-252">You can make users press a key or select a button to send queries to your app.</span></span> <span data-ttu-id="c7c1c-253">Несмотря на то, что вы можете упростить работу со службой приложений, люди могут запутать, что они не видят результаты поиска в реальном времени по мере их ввода.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-253">While that may be easier on your app services service, people may be confused that they're not seeing real-time search results as they type.</span></span>

#### <a name="do-consider-zero-term-queries"></a><span data-ttu-id="c7c1c-254">Do: рассмотрение нулевых терминов запросов</span><span class="sxs-lookup"><span data-stu-id="c7c1c-254">Do: Consider zero-term queries</span></span>

<span data-ttu-id="c7c1c-255">Например, прежде чем пользователь запишет что-либо в поле поиска, отобразите сведения о последнем просмотре в приложении.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-255">For example, before a user writes anything in the search box, display what they last viewed on your app.</span></span> <span data-ttu-id="c7c1c-256">Возможно, они хотят вставить это содержимое в беседу.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-256">It's possible that they want to insert that content into their conversation.</span></span>

## <a name="validate-your-design"></a><span data-ttu-id="c7c1c-257">Проверка проекта</span><span class="sxs-lookup"><span data-stu-id="c7c1c-257">Validate your design</span></span>

<span data-ttu-id="c7c1c-258">Если вы планируете опубликовать свое приложение в AppSource, следует изучить проблемы, которые обычно приводят к сбою приложений во время отправки.</span><span class="sxs-lookup"><span data-stu-id="c7c1c-258">If you plan to publish your app to AppSource, you should understand the design issues that commonly cause apps to fail during submission.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c7c1c-259">Проверка рекомендаций по проверке макета</span><span class="sxs-lookup"><span data-stu-id="c7c1c-259">Check design validation guidelines</span></span>](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
