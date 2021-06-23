---
title: Разработка расширения для сообщений
description: Узнайте, как создать расширение для сообщений Teams, и получите комплект разработчика для пользовательского интерфейса Microsoft Teams.
keywords: рекомендации по проектированию teams общие принципы рекомендации и советы для расширений по обмену сообщениями
author: heath-hamilton
localization_priority: Priority
ms.author: qinch
ms.topic: conceptual
ms.openlocfilehash: f4d1ba1e6e0b71b37e2b7b2d2a32fb729822ba1c
ms.sourcegitcommit: 99b1f151e4e36a86c6a5d2ccbde01bf45b61f526
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/21/2021
ms.locfileid: "53037672"
---
# <a name="designing-your-microsoft-teams-messaging-extension"></a><span data-ttu-id="70a3f-104">Разработка расширения Microsoft Teams для сообщений</span><span class="sxs-lookup"><span data-stu-id="70a3f-104">Designing your Microsoft Teams messaging extension</span></span>

<span data-ttu-id="70a3f-105">Расширения для сообщений помогают быстро вставить содержимое приложения или выполнить какие-либо операции с сообщением, не выходя из беседы.</span><span class="sxs-lookup"><span data-stu-id="70a3f-105">Messaging extensions are shortcuts for inserting app content or acting on a message without navigating away from the conversation.</span></span>
<span data-ttu-id="70a3f-106">Далее описано и показано, как добавлять расширения для сообщений, использовать их и управлять ими в Teams.</span><span class="sxs-lookup"><span data-stu-id="70a3f-106">To guide your app design, the following information describes and illustrates how people can add, use, and manage messaging extensions in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="70a3f-107">Комплект разработчика для пользовательского интерфейса Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="70a3f-107">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="70a3f-108">В комплекте разработчика для пользовательского интерфейса Microsoft Teams можно найти полные рекомендации по проектированию расширений для сообщений, в том числе элементы, которые можно взять и изменить нужным образом.</span><span class="sxs-lookup"><span data-stu-id="70a3f-108">You can find comprehensive messaging extension design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="70a3f-109">Получить комплект разработчика для пользовательского интерфейса Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="70a3f-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-messaging-extension"></a><span data-ttu-id="70a3f-110">Добавить расширение для сообщений</span><span class="sxs-lookup"><span data-stu-id="70a3f-110">Add a messaging extension</span></span>

<span data-ttu-id="70a3f-111">Вы можете добавить расширение для сообщений в следующих контекстах Teams:</span><span class="sxs-lookup"><span data-stu-id="70a3f-111">You can add a messaging extension in the following Teams contexts:</span></span>

* <span data-ttu-id="70a3f-112">В магазине Teams.</span><span class="sxs-lookup"><span data-stu-id="70a3f-112">From the Teams store.</span></span>
* <span data-ttu-id="70a3f-113">В канале, чате или собрании (до, во время и после) рядом с полем создания сообщения.</span><span class="sxs-lookup"><span data-stu-id="70a3f-113">In a channel, chat, or meeting (before, during, and after) near the compose box.</span></span> <span data-ttu-id="70a3f-114">Стоит отметить, что если вы добавили расширение для сообщений в одном из этих мест, в этом контексте его сможете использовать только вы.</span><span class="sxs-lookup"><span data-stu-id="70a3f-114">It's worth noting if you add a messaging extension in one of these places, only you can use it in that context.</span></span>

<span data-ttu-id="70a3f-115">В следующем примере показано, как добавить расширение для сообщений в канале:</span><span class="sxs-lookup"><span data-stu-id="70a3f-115">The following example shows how you add a messaging extension in a channel:</span></span>

# <a name="desktop"></a>[<span data-ttu-id="70a3f-116">Классическая версия</span><span class="sxs-lookup"><span data-stu-id="70a3f-116">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/add-in-channel.png" alt-text="В примере показано, как добавить расширение для сообщений рядом с полем создания сообщения в канале." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="70a3f-118">Мобильная версия</span><span class="sxs-lookup"><span data-stu-id="70a3f-118">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-add-in-channel.png" alt-text="В примере показано, как добавить расширение для сообщений рядом с полем создания сообщения в канале на мобильном устройстве." border="false":::

---

## <a name="set-up-a-messaging-extension"></a><span data-ttu-id="70a3f-120">Настройка расширения для сообщений</span><span class="sxs-lookup"><span data-stu-id="70a3f-120">Set up a messaging extension</span></span>

<span data-ttu-id="70a3f-121">Проверка подлинности в принципе не обязательна, но если вы проектируете что-нибудь вроде системы отслеживания запросов, то, возможно, захотите, чтобы пользователи, прежде чем воспользоваться вашим ПО, выполняли вход в систему.</span><span class="sxs-lookup"><span data-stu-id="70a3f-121">Authentication isn't mandatory, but if your app is something like a ticket tracking tool, you may need people to sign in to use the messaging extension.</span></span>

<span data-ttu-id="70a3f-122">Чтобы обеспечить единый дизайн приложений Teams, экран входа менять нельзя.</span><span class="sxs-lookup"><span data-stu-id="70a3f-122">For consistency across Teams apps, you can't customize the sign-in screen.</span></span> <span data-ttu-id="70a3f-123">Если вы используете проверку подлинности с единым входом (SSO), пользователи будут автоматически выполнять вход.</span><span class="sxs-lookup"><span data-stu-id="70a3f-123">If you use single sign-on (SSO) authentication, users are signed in automatically.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="70a3f-124">Классическая версия</span><span class="sxs-lookup"><span data-stu-id="70a3f-124">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/set-up.png" alt-text="В примере показан экран настройки расширения сообщений с кнопкой &quot;Вход&quot;." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="70a3f-126">Мобильная версия</span><span class="sxs-lookup"><span data-stu-id="70a3f-126">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-set-up.png" alt-text="В примере показан экран настройки расширения сообщений с кнопкой &quot;Вход&quot; на мобильном устройстве." border="false":::

---

## <a name="types-of-messaging-extensions"></a><span data-ttu-id="70a3f-128">Типы расширений для сообщений</span><span class="sxs-lookup"><span data-stu-id="70a3f-128">Types of messaging extensions</span></span>

<span data-ttu-id="70a3f-129">В расширениях для сообщений могут быть реализованы команды поиска, команды действий или и то, и другое.</span><span class="sxs-lookup"><span data-stu-id="70a3f-129">Messaging extensions can have search commands, action commands, or both.</span></span> <span data-ttu-id="70a3f-130">Какие именно нужны вам — зависит от функций вашего приложения и их соответствия сценариям использования Teams.</span><span class="sxs-lookup"><span data-stu-id="70a3f-130">Your commands depend on your app's features and how those fit within Teams use cases.</span></span>

### <a name="search-commands"></a><span data-ttu-id="70a3f-131">Команды поиска</span><span class="sxs-lookup"><span data-stu-id="70a3f-131">Search commands</span></span>

<span data-ttu-id="70a3f-132">Расширение для сообщений с поиском может использоваться для быстрого поиска внешнего содержимого и вставки его в сообщение.</span><span class="sxs-lookup"><span data-stu-id="70a3f-132">With search commands, people can use your messaging extension to quickly find external content and insert into a message.</span></span> <span data-ttu-id="70a3f-133">Команды поиска обычно доступны в поле создания сообщения.</span><span class="sxs-lookup"><span data-stu-id="70a3f-133">Search commands are commonly made available in the compose box.</span></span> <span data-ttu-id="70a3f-134">Например, вы можете начать обсуждение или поучаствовать в нем, поделившись содержимым — и при этом не выходя из Teams.</span><span class="sxs-lookup"><span data-stu-id="70a3f-134">For example, you can start or add to a discussion by sharing a piece of content—without ever leaving Teams.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="70a3f-135">Классическая версия</span><span class="sxs-lookup"><span data-stu-id="70a3f-135">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/search-command-type.png" alt-text="В примере показано расширение для сообщений на основе поиска, запущенное из поля создания сообщения." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="70a3f-137">Мобильная версия</span><span class="sxs-lookup"><span data-stu-id="70a3f-137">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-search-command-type.png" alt-text="В примере показано расширение для сообщений на основе поиска, запущенное из поля создания сообщения на мобильном устройстве." border="false":::

---

#### <a name="compose-box-layout-options"></a><span data-ttu-id="70a3f-139">Параметры компоновки поля создания сообщения</span><span class="sxs-lookup"><span data-stu-id="70a3f-139">Compose box layout options</span></span>

<span data-ttu-id="70a3f-140">Результаты поиска расширения сообщений можно выводить в разных конфигурациях, в том числе в виде [таблицы и списка](../../messaging-extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests).</span><span class="sxs-lookup"><span data-stu-id="70a3f-140">You have some options for displaying messaging extension search results, including [list and grid views](../../messaging-extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests).</span></span>

:::image type="content" source="../../assets/images/messaging-extension/search-result-layout.png" alt-text="Иллюстрации, на которых показаны варианты компоновки при выводе результатов поиска из расширения сообщений." border="false":::

### <a name="action-commands"></a><span data-ttu-id="70a3f-142">Команды действий</span><span class="sxs-lookup"><span data-stu-id="70a3f-142">Action commands</span></span>

<span data-ttu-id="70a3f-143">Команды действий позволяют запускать действия и обрабатывать запросы во внешних службах в Teams.</span><span class="sxs-lookup"><span data-stu-id="70a3f-143">Action commands allow people to trigger actions and process requests in external services within Teams.</span></span> <span data-ttu-id="70a3f-144">Например, если ваше приложение отслеживает заказы, пользователь может создать новый заказ, используя содержимое сообщения коллеги прямо в чате.</span><span class="sxs-lookup"><span data-stu-id="70a3f-144">For example, if your app tracks orders, a user could create a new order using the contents of a colleague’s message from right inside their chat.</span></span>

<span data-ttu-id="70a3f-145">Расширения сообщений на основе действий часто требуют, чтобы пользователи заполняли форму или что-либо подобное в модальном окне.</span><span class="sxs-lookup"><span data-stu-id="70a3f-145">Action-based messaging extensions frequently require users to complete a form or some other kind of configuration within a modal.</span></span> <span data-ttu-id="70a3f-146">Такие виды интерфейса можно создавать с помощью [модулей задач](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).</span><span class="sxs-lookup"><span data-stu-id="70a3f-146">You can create these experiences with [task modules](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).</span></span>

## <a name="open-a-messaging-extension"></a><span data-ttu-id="70a3f-147">Открыть расширение для сообщений</span><span class="sxs-lookup"><span data-stu-id="70a3f-147">Open a messaging extension</span></span>

<span data-ttu-id="70a3f-148">Поле создания сообщения и сами сообщения или записи являются основным контекстом, в котором используются расширения для сообщений.</span><span class="sxs-lookup"><span data-stu-id="70a3f-148">The compose box and messages or posts are the primary contexts where people use messaging extensions.</span></span>

### <a name="from-the-compose-box"></a><span data-ttu-id="70a3f-149">Из поля создания сообщения</span><span class="sxs-lookup"><span data-stu-id="70a3f-149">From the compose box</span></span>

<span data-ttu-id="70a3f-150">После того как вы добавите свое расширение для сообщений, пользователи смогут открывать его, выбрав значок приложения, расположенный ниже поля создания сообщения.</span><span class="sxs-lookup"><span data-stu-id="70a3f-150">Once added, users can open your messaging extension by selecting your app icon below the compose box.</span></span> <span data-ttu-id="70a3f-151">В этих примерах расширение содержит и команду поиска, и команду действий.</span><span class="sxs-lookup"><span data-stu-id="70a3f-151">In these examples, the extension has search and action commands.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="70a3f-152">Классическая версия</span><span class="sxs-lookup"><span data-stu-id="70a3f-152">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/open-from-compose-box.png" alt-text="В примере показано, как открыть расширение для сообщений из поля создания сообщения." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="70a3f-154">Мобильная версия</span><span class="sxs-lookup"><span data-stu-id="70a3f-154">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-open-from-compose-box.png" alt-text="В примере показано, как открыть расширение для обмена сообщениями из поля создания сообщения на мобильном устройстве." border="false":::

---

### <a name="from-a-chat-message-or-channel-post"></a><span data-ttu-id="70a3f-156">Из сообщения чата или публикации канала</span><span class="sxs-lookup"><span data-stu-id="70a3f-156">From a chat message or channel post</span></span>

После того как вы добавите свое расширение для сообщений, пользователи смогут открывать его, выбрав значок **Еще**:::image type="icon" source="../../assets/icons/teams-client-more.png"::: в сообщении чата или публикации канала, чтобы найти команды действий. <span data-ttu-id="70a3f-158">В зависимости от того, как используется ваше расширение, оно может быть указано в списке **Дополнительные действия**.</span><span class="sxs-lookup"><span data-stu-id="70a3f-158">Your extension may be listed under **More actions** based on usage.</span></span>

> [!NOTE]
> <span data-ttu-id="70a3f-159">Поддержка дополнительных действий из сообщения чата или записи канала недоступна на мобильной платформе Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="70a3f-159">Support for more actions from a chat message or channel post is not available on Microsoft Teams mobile platform.</span></span> 

#### <a name="chat-message"></a><span data-ttu-id="70a3f-160">Сообщение чата</span><span class="sxs-lookup"><span data-stu-id="70a3f-160">Chat message</span></span>

# <a name="desktop"></a>[<span data-ttu-id="70a3f-161">Классическая версия</span><span class="sxs-lookup"><span data-stu-id="70a3f-161">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/open-from-chat-message.png" alt-text="В примере показано, как открыть расширение для сообщений из сообщения чата." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="70a3f-163">Мобильная версия</span><span class="sxs-lookup"><span data-stu-id="70a3f-163">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-open-from-chat-post.png" alt-text="В примере показано, как открыть расширение для сообщений из сообщения чата на мобильном устройстве." border="false":::

---
':::image type="content" source="../../assets/images/messaging-extension/open-from-channel-post.png" alt-text="Example shows how to open a messaging extension from a channel post on mobile." border="false"::': null
':::image type="content" source="../../assets/images/messaging-extension/mobile-open-from-channel-post.png" alt-text="Example shows how to open a messaging extension from a channel post on mobile." border="false"::': null
---

## <a name="use-a-messaging-extension"></a><span data-ttu-id="70a3f-165">Использование расширения для сообщений</span><span class="sxs-lookup"><span data-stu-id="70a3f-165">Use a messaging extension</span></span>

<span data-ttu-id="70a3f-166">В следующих сценариях показаны основные способы использования расширений для сообщений.</span><span class="sxs-lookup"><span data-stu-id="70a3f-166">The following scenarios show the primary ways people use messaging extensions.</span></span>

### <a name="insert-content-into-a-message"></a><span data-ttu-id="70a3f-167">Вставка контента в сообщение</span><span class="sxs-lookup"><span data-stu-id="70a3f-167">Insert content into a message</span></span>

<span data-ttu-id="70a3f-168">**1. Выберите расширение для сообщений**.</span><span class="sxs-lookup"><span data-stu-id="70a3f-168">**1. Select a messaging extension**.</span></span> <span data-ttu-id="70a3f-169">Пользователи могут искать контент, которым они хотят поделиться, прямо из поля создания сообщения.</span><span class="sxs-lookup"><span data-stu-id="70a3f-169">Users can search for the content they want to share from the compose box.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="70a3f-170">Классическая версия</span><span class="sxs-lookup"><span data-stu-id="70a3f-170">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/insert-content-search.png" alt-text="В примере показано, как пользователь ищет контент для вставки прямо из поля создания сообщения." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="70a3f-172">Мобильная версия</span><span class="sxs-lookup"><span data-stu-id="70a3f-172">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-insert-content-search.png" alt-text="В примере показано, как пользователь ищет контент для вставки прямо из поля создания сообщения на мобильном устройстве." border="false":::

---

<span data-ttu-id="70a3f-174">**2. Вставьте контент**.</span><span class="sxs-lookup"><span data-stu-id="70a3f-174">**2. Insert content**.</span></span> <span data-ttu-id="70a3f-175">После публикации пользователи люди могут ответить или выбрать содержимое, чтобы увидеть дополнительную информацию в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="70a3f-175">Once posted, others can reply or select the content to see more information in your app.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="70a3f-176">Классическая версия</span><span class="sxs-lookup"><span data-stu-id="70a3f-176">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/insert-content-posted.png" alt-text="В примере показан пользователь, публикующий контент в беседе в канале." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="70a3f-178">Мобильная версия</span><span class="sxs-lookup"><span data-stu-id="70a3f-178">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-insert-content-posted.png" alt-text="В примере показан пользователь, публикующий контент в беседе в канале на мобильном устройстве." border="false":::

---

### <a name="take-action-on-a-message"></a><span data-ttu-id="70a3f-180">Действия с сообщениями</span><span class="sxs-lookup"><span data-stu-id="70a3f-180">Take action on a message</span></span>

<span data-ttu-id="70a3f-181">**1. Выберите расширение для сообщений**.</span><span class="sxs-lookup"><span data-stu-id="70a3f-181">**1. Select a messaging extension**.</span></span> <span data-ttu-id="70a3f-182">Ваше приложение может включать одну или несколько команд действий.</span><span class="sxs-lookup"><span data-stu-id="70a3f-182">Your app can include one or more action commands.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="70a3f-183">Классическая версия</span><span class="sxs-lookup"><span data-stu-id="70a3f-183">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/select-action-command.png" alt-text="В примере показано, как пользователь выбирает команду действия расширения обмена сообщениями." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="70a3f-185">Мобильная версия</span><span class="sxs-lookup"><span data-stu-id="70a3f-185">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-select-action-command.png" alt-text="В примере показано, как пользователь выбирает команду действия расширения обмена сообщениями на мобильном устройстве" border="false":::.

---

<span data-ttu-id="70a3f-187">**2. Закончите действие**.</span><span class="sxs-lookup"><span data-stu-id="70a3f-187">**2. Complete the action**.</span></span> <span data-ttu-id="70a3f-188">Ваше приложение может получать и обрабатывать любой контент или данные, отправленные действием сообщения.</span><span class="sxs-lookup"><span data-stu-id="70a3f-188">Your app can receive and process any content or data sent by the message action.</span></span> <span data-ttu-id="70a3f-189">Это позволяет пользователям оставаться в беседе и, как показано в следующем примере, не затруднять себя вводом сведений непосредственно в приложении.</span><span class="sxs-lookup"><span data-stu-id="70a3f-189">This allows users to remain in their conversation and, the following example, not worry about entering information directly in your app.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="70a3f-190">Классическая версия</span><span class="sxs-lookup"><span data-stu-id="70a3f-190">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/complete-action-command.png" alt-text="Пример действия с сообщением." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="70a3f-192">Мобильная версия</span><span class="sxs-lookup"><span data-stu-id="70a3f-192">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-complete-action-command.png" alt-text="Пример действия с сообщением на мобильном устройстве" border="false":::.

---

### <a name="preview-links"></a><span data-ttu-id="70a3f-194">Предварительный просмотр ссылок</span><span class="sxs-lookup"><span data-stu-id="70a3f-194">Preview links</span></span>

<span data-ttu-id="70a3f-195">Расширения для сообщений также позволяют вставлять в сообщение форматированные ссылки с контентом с распознаваемых URL-адресов (эта возможность называется [развертыванием ссылки](../../messaging-extensions/how-to/link-unfurling.md)).</span><span class="sxs-lookup"><span data-stu-id="70a3f-195">Messaging extensions also allow you to insert rich links from a recognized URL into a message (this capability is called [link unfurling](../../messaging-extensions/how-to/link-unfurling.md).)</span></span>

<span data-ttu-id="70a3f-196">**1. Вставьте распознаваемую ссылку** в поле создания сообщения.</span><span class="sxs-lookup"><span data-stu-id="70a3f-196">**1. Paste a recognized link** in the compose box.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="70a3f-197">Классическая версия</span><span class="sxs-lookup"><span data-stu-id="70a3f-197">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/paste-preview-link.png" alt-text="В примере показано, как пользователь вставляет ссылку в поле создания сообщения" border="false":::.

# <a name="mobile"></a>[<span data-ttu-id="70a3f-199">Мобильная версия</span><span class="sxs-lookup"><span data-stu-id="70a3f-199">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-paste-preview-link.png" alt-text="В примере показано, как пользователь вставляет ссылку в поле создания сообщения на мобильном устройстве" border="false":::.

---

<span data-ttu-id="70a3f-201">**2. Вставьте контент**.</span><span class="sxs-lookup"><span data-stu-id="70a3f-201">**2. Insert content**.</span></span> <span data-ttu-id="70a3f-202">Если ваше приложение распознает URL-адрес в поле создания сообщения, оно сформирует ссылку в виде карточки, которая обеспечивает предварительный просмотр веб-контента в форматированном виде.</span><span class="sxs-lookup"><span data-stu-id="70a3f-202">If your app recognizes the URL in the compose box, it renders the link as a card that provides a content-rich preview of the web content.</span></span> <span data-ttu-id="70a3f-203">(Подробности см. в разделе [Рекомендации по созданию адаптивных карточек](../../task-modules-and-cards/cards/design-effective-cards.md).)</span><span class="sxs-lookup"><span data-stu-id="70a3f-203">(See [Adaptive Cards design guidelines](../../task-modules-and-cards/cards/design-effective-cards.md) for more information.)</span></span>

# <a name="desktop"></a>[<span data-ttu-id="70a3f-204">Классическая версия</span><span class="sxs-lookup"><span data-stu-id="70a3f-204">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/insert-preview-link.png" alt-text="В примере показано, как URL-адрес, распознанный приложением, включает в поле создания сообщения часть контента" border="false":::.

# <a name="mobile"></a>[<span data-ttu-id="70a3f-206">Мобильная версия</span><span class="sxs-lookup"><span data-stu-id="70a3f-206">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-insert-preview-link.png" alt-text="В примере показано, как URL-адрес, распознанный приложением, включает в поле создания сообщения часть контента на мобильном устройстве" border="false":::.

---

## <a name="manage-a-messaging-extension"></a><span data-ttu-id="70a3f-208">Управление расширением для сообщений</span><span class="sxs-lookup"><span data-stu-id="70a3f-208">Manage a messaging extension</span></span>

<span data-ttu-id="70a3f-209">Щелкнув значок правой кнопкой мыши, пользователи смогут закрепить, удалить или настроить ваше расширение для сообщений.</span><span class="sxs-lookup"><span data-stu-id="70a3f-209">By right clicking your icon, users can pin, remove, or configure your messaging extension.</span></span>

## <a name="anatomy"></a><span data-ttu-id="70a3f-210">Структура</span><span class="sxs-lookup"><span data-stu-id="70a3f-210">Anatomy</span></span>

### <a name="messaging-extension-in-the-compose-box"></a><span data-ttu-id="70a3f-211">Расширение для сообщений в поле создания сообщения</span><span class="sxs-lookup"><span data-stu-id="70a3f-211">Messaging extension in the compose box</span></span>

<span data-ttu-id="70a3f-212">Следующий пример — расширение для сообщений, открытое из поля создания сообщения.</span><span class="sxs-lookup"><span data-stu-id="70a3f-212">The following example is a messaging extension opened from the compose box.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="70a3f-213">Классическая версия</span><span class="sxs-lookup"><span data-stu-id="70a3f-213">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/anatomy-compose.png" alt-text="Иллюстрация, показывающая структуру пользовательского интерфейса расширения для сообщений в поле создания сообщения" border="false":::.

|<span data-ttu-id="70a3f-215">Счетчик</span><span class="sxs-lookup"><span data-stu-id="70a3f-215">Counter</span></span>|<span data-ttu-id="70a3f-216">Описание</span><span class="sxs-lookup"><span data-stu-id="70a3f-216">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="70a3f-217">1</span><span class="sxs-lookup"><span data-stu-id="70a3f-217">1</span></span>|<span data-ttu-id="70a3f-218">**Логотип приложения**: цветной значок логотипа приложения.</span><span class="sxs-lookup"><span data-stu-id="70a3f-218">**App logo**: Color icon of your app logo.</span></span>|
|<span data-ttu-id="70a3f-219">2.</span><span class="sxs-lookup"><span data-stu-id="70a3f-219">2</span></span>|<span data-ttu-id="70a3f-220">**Имя приложения**: полное имя приложения.</span><span class="sxs-lookup"><span data-stu-id="70a3f-220">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="70a3f-221">3</span><span class="sxs-lookup"><span data-stu-id="70a3f-221">3</span></span>|<span data-ttu-id="70a3f-222">**Значок меню команд действий (необязательно)**: открывает список команд действий данного расширения для сообщений (если вы их указали).</span><span class="sxs-lookup"><span data-stu-id="70a3f-222">**Action commands menu icon (optional)**: Opens a list of action commands for your messaging extension (if you specify any).</span></span>
|<span data-ttu-id="70a3f-223">4</span><span class="sxs-lookup"><span data-stu-id="70a3f-223">4</span></span>|<span data-ttu-id="70a3f-224">**Поле поиска**: позволяет пользователям находить контент приложения для последующей вставки.</span><span class="sxs-lookup"><span data-stu-id="70a3f-224">**Search box**: Allows users to find app content they want to insert.</span></span>|
|<span data-ttu-id="70a3f-225">5</span><span class="sxs-lookup"><span data-stu-id="70a3f-225">5</span></span>|<span data-ttu-id="70a3f-226">**Меню вкладок (необязательно)**: предоставляет несколько категорий контента.</span><span class="sxs-lookup"><span data-stu-id="70a3f-226">**Tab menu (optional)**: Provides multiple content categories.</span></span>|
|<span data-ttu-id="70a3f-227">6</span><span class="sxs-lookup"><span data-stu-id="70a3f-227">6</span></span>|<span data-ttu-id="70a3f-228">**Меню команд действий (необязательно)**: выводит на экран список команд действий (если вы их указали).</span><span class="sxs-lookup"><span data-stu-id="70a3f-228">**Action commands menu (optional)**: Displays list of action commands (if you specify any).</span></span>|
|<span data-ttu-id="70a3f-229">7</span><span class="sxs-lookup"><span data-stu-id="70a3f-229">7</span></span>|<span data-ttu-id="70a3f-230">**Контент приложения**: в основном для отображения результатов поиска.</span><span class="sxs-lookup"><span data-stu-id="70a3f-230">**App content**: Primarily to display search results.</span></span> <span data-ttu-id="70a3f-231">В этом примере используется компоновка списка (другой вариант — табличная компоновка).</span><span class="sxs-lookup"><span data-stu-id="70a3f-231">The example here is using the list layout (grid layout is another option).</span></span>|
|<span data-ttu-id="70a3f-232">8</span><span class="sxs-lookup"><span data-stu-id="70a3f-232">8</span></span>|<span data-ttu-id="70a3f-233">**Логотип приложения**: контурный значок логотипа приложения.</span><span class="sxs-lookup"><span data-stu-id="70a3f-233">**App logo**: Outline icon of your app logo.</span></span>|

# <a name="mobile"></a>[<span data-ttu-id="70a3f-234">Мобильная версия</span><span class="sxs-lookup"><span data-stu-id="70a3f-234">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-anatomy-compose.png" alt-text="Иллюстрация, показывающая структуру пользовательского интерфейса расширения для сообщений в поле создания сообщения на мобильном устройстве" border="false":::.

|<span data-ttu-id="70a3f-236">Счетчик</span><span class="sxs-lookup"><span data-stu-id="70a3f-236">Counter</span></span>|<span data-ttu-id="70a3f-237">Описание</span><span class="sxs-lookup"><span data-stu-id="70a3f-237">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="70a3f-238">1</span><span class="sxs-lookup"><span data-stu-id="70a3f-238">1</span></span>|<span data-ttu-id="70a3f-239">**Имя приложения**: полное имя приложения.</span><span class="sxs-lookup"><span data-stu-id="70a3f-239">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="70a3f-240">2.</span><span class="sxs-lookup"><span data-stu-id="70a3f-240">2</span></span>|<span data-ttu-id="70a3f-241">**Значок меню команд действий (необязательно)**: открывает список команд действий данного расширения для сообщений (если вы их указали).</span><span class="sxs-lookup"><span data-stu-id="70a3f-241">**Action commands menu icon (optional)**: Opens a list of action commands for your messaging extension (if you specify any).</span></span>
|<span data-ttu-id="70a3f-242">3</span><span class="sxs-lookup"><span data-stu-id="70a3f-242">3</span></span>|<span data-ttu-id="70a3f-243">**Поле поиска**: позволяет пользователям находить контент приложения для последующей вставки.</span><span class="sxs-lookup"><span data-stu-id="70a3f-243">**Search box**: Allows users to find app content they want to insert.</span></span>|
|<span data-ttu-id="70a3f-244">4</span><span class="sxs-lookup"><span data-stu-id="70a3f-244">4</span></span>|<span data-ttu-id="70a3f-245">**Меню вкладок (необязательно)**: предоставляет несколько категорий контента.</span><span class="sxs-lookup"><span data-stu-id="70a3f-245">**Tab menu (optional)**: Provides multiple content categories.</span></span>|
|<span data-ttu-id="70a3f-246">5</span><span class="sxs-lookup"><span data-stu-id="70a3f-246">5</span></span>|<span data-ttu-id="70a3f-247">**Меню команд действий (необязательно)**: выводит на экран список команд действий (если вы их указали).</span><span class="sxs-lookup"><span data-stu-id="70a3f-247">**Action commands menu (optional)**: Displays list of action commands (if you specify any).</span></span>|
|<span data-ttu-id="70a3f-248">6</span><span class="sxs-lookup"><span data-stu-id="70a3f-248">6</span></span>|<span data-ttu-id="70a3f-249">**Контент приложения**: в основном для отображения результатов поиска.</span><span class="sxs-lookup"><span data-stu-id="70a3f-249">**App content**: Primarily to display search results.</span></span>|

---

### <a name="messaging-extension-management-menu"></a><span data-ttu-id="70a3f-250">Меню управления расширениями сообщений</span><span class="sxs-lookup"><span data-stu-id="70a3f-250">Messaging extension management menu</span></span>

:::image type="content" source="../../assets/images/messaging-extension/anatomy-management-menu.png" alt-text="Иллюстрация, показывающая структуру пользовательского интерфейса меню расширения для сообщений" border="false":::.

|<span data-ttu-id="70a3f-252">Счетчик</span><span class="sxs-lookup"><span data-stu-id="70a3f-252">Counter</span></span>|<span data-ttu-id="70a3f-253">Описание</span><span class="sxs-lookup"><span data-stu-id="70a3f-253">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="70a3f-254">1</span><span class="sxs-lookup"><span data-stu-id="70a3f-254">1</span></span>|<span data-ttu-id="70a3f-255">**Открепить**: доступно, если пользователь закрепил ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="70a3f-255">**Unpin**: Available if the user has pinned your app.</span></span>|
|<span data-ttu-id="70a3f-256">2.</span><span class="sxs-lookup"><span data-stu-id="70a3f-256">2</span></span>|<span data-ttu-id="70a3f-257">**Удалить**: удаляет расширение для сообщений из канала, чата или собрания.</span><span class="sxs-lookup"><span data-stu-id="70a3f-257">**Remove**: Removes the messaging extension from the channel, chat, or meeting.</span></span>|

## <a name="best-practices"></a><span data-ttu-id="70a3f-258">Рекомендованные методики</span><span class="sxs-lookup"><span data-stu-id="70a3f-258">Best practices</span></span>

<span data-ttu-id="70a3f-259">Используйте эти рекомендации для создания качественных приложений.</span><span class="sxs-lookup"><span data-stu-id="70a3f-259">Use these recommendations to create a quality app experience.</span></span>

### <a name="setup-and-general-usage"></a><span data-ttu-id="70a3f-260">Настройка и общее использование</span><span class="sxs-lookup"><span data-stu-id="70a3f-260">Setup and general usage</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-do.png" alt-text="Пример настройки и общего использования" border="false":::.

#### <a name="do-integrate-with-single-sign-on"></a><span data-ttu-id="70a3f-262">Нужно: интегрироваться с единым входом</span><span class="sxs-lookup"><span data-stu-id="70a3f-262">Do: Integrate with single-sign on</span></span>

<span data-ttu-id="70a3f-263">SSO делает вход проще, быстрее и надежнее.</span><span class="sxs-lookup"><span data-stu-id="70a3f-263">SSO makes the sign-in process easier, faster, and secure.</span></span> <span data-ttu-id="70a3f-264">Кроме того, если пользователь уже выполнил вход в ваше личное приложение, повторный вход для доступа к расширению для сообщений уже не нужен.</span><span class="sxs-lookup"><span data-stu-id="70a3f-264">Also, if a user has already signed in to your personal app, they don’t have to also sign in again to access the messaging extension.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-dont.png" alt-text="Пример интеграции с единым входом" border="false":::.

#### <a name="dont-take-users-away-from-the-conversation"></a><span data-ttu-id="70a3f-266">Нельзя: заставлять пользователей выходить из беседы</span><span class="sxs-lookup"><span data-stu-id="70a3f-266">Don't: Take users away from the conversation</span></span>

<span data-ttu-id="70a3f-267">Расширения для сообщений — это средства упрощения работы, позволяющие свести к минимуму переключение контекста.</span><span class="sxs-lookup"><span data-stu-id="70a3f-267">Messaging extensions are shortcuts that are supposed reduce context switching.</span></span> <span data-ttu-id="70a3f-268">Например, расширение не должно направлять пользователей на веб-страницу за пределами Teams.</span><span class="sxs-lookup"><span data-stu-id="70a3f-268">Your extension should not, for example, direct users to a webpage outside Teams.</span></span>

   :::column-end:::
:::row-end:::

#### <a name="do-highlight-your-messaging-extension"></a><span data-ttu-id="70a3f-269">Нужно: сделать расширение для сообщений броским</span><span class="sxs-lookup"><span data-stu-id="70a3f-269">Do: Highlight your messaging extension</span></span>

<span data-ttu-id="70a3f-270">Расширение для сообщений не всегда легко заметить.</span><span class="sxs-lookup"><span data-stu-id="70a3f-270">Messaging extensions aren't always easy to find.</span></span> <span data-ttu-id="70a3f-271">Добавьте на страницу сведений о приложении снимки экрана, показывающие, как использовать ваше расширение для сообщений.</span><span class="sxs-lookup"><span data-stu-id="70a3f-271">Include screenshots of how to use it in your app details page.</span></span> <span data-ttu-id="70a3f-272">Если приложение также содержит бот, вы можете добавить документацию по расширению для сообщений в приветственный обзор бота.</span><span class="sxs-lookup"><span data-stu-id="70a3f-272">If your app also includes a bot, you can include messaging extension help documentation in a bot welcome tour.</span></span>

### <a name="templating"></a><span data-ttu-id="70a3f-273">Шаблоны</span><span class="sxs-lookup"><span data-stu-id="70a3f-273">Templating</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-do.png" alt-text="Пример шаблона" border="false":::.

#### <a name="do-let-teams-handle-some-of-the-design-work-if-possible"></a><span data-ttu-id="70a3f-275">Нужно: по возможности перекладывать работу на Teams</span><span class="sxs-lookup"><span data-stu-id="70a3f-275">Do: Let Teams handle some of the design work if possible</span></span>

<span data-ttu-id="70a3f-276">Если это имеет смысл для ваших сценариев, рассмотрите возможность создания расширения для сообщений на основе поиска.</span><span class="sxs-lookup"><span data-stu-id="70a3f-276">If it makes sense for your use cases, consider creating a search-based messaging extension.</span></span> <span data-ttu-id="70a3f-277">Teams отрисовывает такие расширения, используя встроенную тему и с учетом специальных возможностей.</span><span class="sxs-lookup"><span data-stu-id="70a3f-277">Teams renders these types of extensions with built-in theming and accessibility.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-dont.png" alt-text="Пример подхода к проектированию" border="false":::

#### <a name="dont-embed-your-entire-app-in-a-task-module"></a><span data-ttu-id="70a3f-279">Нельзя: встраивать все приложение целиком в модуль задач</span><span class="sxs-lookup"><span data-stu-id="70a3f-279">Don't: Embed your entire app in a task module</span></span>

<span data-ttu-id="70a3f-280">Если вашему расширению обмена сообщениями требуются команды действий, сделайте очень простой модуль задач и выводите на экран только компоненты, необходимые для выполнения действия.</span><span class="sxs-lookup"><span data-stu-id="70a3f-280">If your messaging extension requires action commands, keep the task module simple and display only the components required to complete the action.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="70a3f-281">Визуальные темы</span><span class="sxs-lookup"><span data-stu-id="70a3f-281">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-do.png" alt-text="Пример визуальной темы" border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a><span data-ttu-id="70a3f-283">Нужно: использовать преимущества цветовых маркеров Teams</span><span class="sxs-lookup"><span data-stu-id="70a3f-283">Do: Take advantage of Teams color tokens</span></span>

<span data-ttu-id="70a3f-284">Каждая тема Teams имеет собственную цветовую схему.</span><span class="sxs-lookup"><span data-stu-id="70a3f-284">Each Teams theme has its own color scheme.</span></span> <span data-ttu-id="70a3f-285">Чтобы автоматически обрабатывать изменения темы, используйте в дизайне <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">цветовые маркеры (Fluent UI)</a>.</span><span class="sxs-lookup"><span data-stu-id="70a3f-285">To handle theme changes automatically, use <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a> in your design.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-dont.png" alt-text="Пример использования цветовых маркеров" border="false":::

#### <a name="dont-hard-code-color-values"></a><span data-ttu-id="70a3f-287">Нельзя: жестко задавать значения цветов прямо в коде</span><span class="sxs-lookup"><span data-stu-id="70a3f-287">Don't: Hard code color values</span></span>

<span data-ttu-id="70a3f-288">Если вы не используете цветовые маркеры Teams, ваши макеты будут менее масштабируемыми и управление ими будет отнимать больше времени.</span><span class="sxs-lookup"><span data-stu-id="70a3f-288">If you don't use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::

### <a name="actions"></a><span data-ttu-id="70a3f-289">Действия</span><span class="sxs-lookup"><span data-stu-id="70a3f-289">Actions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-do.png" alt-text="Пример работы с действиями" border="false":::

#### <a name="do-include-action-commands-that-make-sense-in-context"></a><span data-ttu-id="70a3f-291">Нужно: реализовать команды действий, имеющие смысл в данном контексте</span><span class="sxs-lookup"><span data-stu-id="70a3f-291">Do: Include action commands that make sense in context</span></span>

<span data-ttu-id="70a3f-292">Предлагаемые действия с сообщениями должны быть связаны с тем, что сейчас просматривает пользователь.</span><span class="sxs-lookup"><span data-stu-id="70a3f-292">Message actions should relate to what a user is looking at.</span></span> <span data-ttu-id="70a3f-293">Например, вы можете предоставить пользователям средство для быстрой регистрации проблемы или создания рабочего запроса на основе чужого сообщения.</span><span class="sxs-lookup"><span data-stu-id="70a3f-293">For example, provide users a shortcut for creating an issue or work item using the text in someone’s post.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-dont.png" alt-text="Пример работы с командами действий" border="false":::

#### <a name="dont-include-actions-commands-that-arent-contextual"></a><span data-ttu-id="70a3f-295">Нельзя: создавать команды действий, которые никак не связаны с контекстом.</span><span class="sxs-lookup"><span data-stu-id="70a3f-295">Don't: Include actions commands that aren't contextual</span></span>

<span data-ttu-id="70a3f-296">Действие **Открыть панель управления** будет выглядеть неуместно в большинстве бесед.</span><span class="sxs-lookup"><span data-stu-id="70a3f-296">A message action to **View your dashboard** would probably seem disconnected from most conversations.</span></span>

   :::column-end:::
:::row-end:::

### <a name="searches"></a><span data-ttu-id="70a3f-297">Поиск</span><span class="sxs-lookup"><span data-stu-id="70a3f-297">Searches</span></span>

#### <a name="do-show-search-results-while-typing"></a><span data-ttu-id="70a3f-298">Нужно: показывать результаты поиска по мере того, как пользователь вводит поисковый запрос</span><span class="sxs-lookup"><span data-stu-id="70a3f-298">Do: Show search results while typing</span></span>

<span data-ttu-id="70a3f-299">Показывайте предлагаемые результаты поиска сразу, пока пользователь печатает.</span><span class="sxs-lookup"><span data-stu-id="70a3f-299">Provide suggested search results while users type.</span></span> <span data-ttu-id="70a3f-300">Это позволит быстрее находить нужное содержимое, введя при этом меньше символов.</span><span class="sxs-lookup"><span data-stu-id="70a3f-300">They may find the content they need faster with minimal amount of characters.</span></span>

#### <a name="dont-require-users-to-submit-a-query"></a><span data-ttu-id="70a3f-301">Нельзя: требовать от пользователей отправки запроса</span><span class="sxs-lookup"><span data-stu-id="70a3f-301">Don't: Require users to submit a query</span></span>

<span data-ttu-id="70a3f-302">Вы можете заставить пользователей нажимать клавишу или кнопку для отправки запросов в ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="70a3f-302">You can make users press a key or select a button to send queries to your app.</span></span> <span data-ttu-id="70a3f-303">Хотя так может быть проще для службы приложений, пользователя может запутать то, что результаты поиска не выводятся в режиме реального времени по мере ввода запроса.</span><span class="sxs-lookup"><span data-stu-id="70a3f-303">While that may be easier on your app services service, people may be confused that they're not seeing real-time search results as they type.</span></span>

#### <a name="do-consider-zero-term-queries"></a><span data-ttu-id="70a3f-304">Нужно: рассмотрите возможность реализации запросов при пустом вводе</span><span class="sxs-lookup"><span data-stu-id="70a3f-304">Do: Consider zero-term queries</span></span>

<span data-ttu-id="70a3f-305">Например, пока пользователь еще не успел ничего ввести в поле поиска, покажите то, что он недавно просматривал в приложении.</span><span class="sxs-lookup"><span data-stu-id="70a3f-305">For example, before a user writes anything in the search box, display what they last viewed on your app.</span></span> <span data-ttu-id="70a3f-306">Возможно, пользователь хочет вставить в беседу.именно это.</span><span class="sxs-lookup"><span data-stu-id="70a3f-306">It's possible that they want to insert that content into their conversation.</span></span>
