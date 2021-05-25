---
title: Создание бота
description: Узнайте, как создать бот Teams, и получите комплект разработчика для пользовательского интерфейса Microsoft Teams.
author: heath-hamilton
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 98e36bf55e61ef59261959021409d9e60d8542f5
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630122"
---
# <a name="designing-your-microsoft-teams-bot"></a><span data-ttu-id="59925-103">Создание бота Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="59925-103">Designing your Microsoft Teams bot</span></span>

<span data-ttu-id="59925-104">Боты — это приложения для бесед, которые выполняют определенный набор задач.</span><span class="sxs-lookup"><span data-stu-id="59925-104">Bots are conversational apps that perform a specific set of tasks.</span></span> <span data-ttu-id="59925-105">Построенные на основе <a href="https://dev.botframework.com/" target="_blank">Microsoft Bot Framework</a>боты общаются с пользователями, отвечают на их вопросы и заблаговременно уведомляют их об изменениях и других событиях.</span><span class="sxs-lookup"><span data-stu-id="59925-105">Based on the <a href="https://dev.botframework.com/" target="_blank">Microsoft Bot Framework</a>, bots communicate with users, respond to their questions, and proactively notify them about changes and other events.</span></span> <span data-ttu-id="59925-106">Это отличный способ связи с пользователями.</span><span class="sxs-lookup"><span data-stu-id="59925-106">They're a great way to reach out.</span></span>

<span data-ttu-id="59925-107">Далее описано и показано, как люди могут добавлять ботов, использовать их и управлять ими в Teams. Это может помочь вам в создании приложения.</span><span class="sxs-lookup"><span data-stu-id="59925-107">To guide your app design, the following information describes and illustrates how people can add, use, and manage bots in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="59925-108">Комплект разработчика для пользовательского интерфейса Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="59925-108">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="59925-109">В комплекте разработчика для пользовательского интерфейса Microsoft Teams можно найти более полные рекомендации по проектированию ботов, в том числе элементы, которые можно взять и изменить так, как нужно вам.</span><span class="sxs-lookup"><span data-stu-id="59925-109">You can find more comprehensive bot design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="59925-110">Получить комплект разработчика для пользовательского интерфейса Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="59925-110">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-bot"></a><span data-ttu-id="59925-111">Добавить бота</span><span class="sxs-lookup"><span data-stu-id="59925-111">Add a bot</span></span>

<span data-ttu-id="59925-112">Боты доступны в чатах, каналах и личных приложениях.</span><span class="sxs-lookup"><span data-stu-id="59925-112">Bots are available in chats, channels, and personal apps.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="59925-113">Desktop</span><span class="sxs-lookup"><span data-stu-id="59925-113">Desktop</span></span>](#tab/desktop)

<span data-ttu-id="59925-114">Пользователи могут добавить бот один из следующих способов:</span><span class="sxs-lookup"><span data-stu-id="59925-114">Users can add a bot one of the following ways:</span></span>

* <span data-ttu-id="59925-115">Из Teams магазина.</span><span class="sxs-lookup"><span data-stu-id="59925-115">From the Teams store.</span></span>
* <span data-ttu-id="59925-116">Использовать всплывающее окно приложения. Для этого выберите значок **Дополнительные** в левой части экрана Teams.</span><span class="sxs-lookup"><span data-stu-id="59925-116">Using the app flyout by selecting the **More** icon on the left side of Teams.</span></span>
* <span data-ttu-id="59925-117">С помощью @упоминания в новом чате или поле "Создать" (в следующем примере показано, как это можно сделать в групповом чате).</span><span class="sxs-lookup"><span data-stu-id="59925-117">With an @mention in the new chat or compose box (the following example shows how you can do this in a group chat).</span></span>

    :::image type="content" source="../../assets/images/bots/add-bot-chat-at-mention.png" alt-text="В примере показано, как добавить бота в групповой чат с помощью @упоминания." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="59925-119">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="59925-119">Mobile</span></span>](#tab/mobile)

<span data-ttu-id="59925-120">Пользователи могут получать доступ к ботам, добавленным на рабочем столе с помощью @mention.</span><span class="sxs-lookup"><span data-stu-id="59925-120">Users can access bots that were added on desktop with an @mention.</span></span>

:::image type="content" source="../../assets/images/bots/mobile-access-bot-chat-at-mention.png" alt-text="В примере показано, как получить доступ к мобильному боту в групповом чате с помощью @mention." border="false":::

---

## <a name="introduce-a-bot"></a><span data-ttu-id="59925-122">Представление бота</span><span class="sxs-lookup"><span data-stu-id="59925-122">Introduce a bot</span></span>

<span data-ttu-id="59925-123">Очень важно, чтобы бот сам себя представлял и объяснял, что он умеет делать.</span><span class="sxs-lookup"><span data-stu-id="59925-123">It’s critical that your bot introduces itself and describes what it can do.</span></span> <span data-ttu-id="59925-124">Первоначальный обмен репликами с ботом помогает пользователям понять, что с ним делать, узнать его ограничения и, что самое важное, освоиться с ним.</span><span class="sxs-lookup"><span data-stu-id="59925-124">This initial exchange helps people understand what to do with the bot, find out its limitations and, most importantly, get comfortable interacting with it.</span></span>

### <a name="welcome-message-in-a-one-on-one-chat"></a><span data-ttu-id="59925-125">Приветствие в чате один на один</span><span class="sxs-lookup"><span data-stu-id="59925-125">Welcome message in a one-on-one chat</span></span>

<span data-ttu-id="59925-126">В личных контекстах приветствия задают тон бота.</span><span class="sxs-lookup"><span data-stu-id="59925-126">In personal contexts, welcome messages set your bot's tone.</span></span> <span data-ttu-id="59925-127">В сообщении содержится приветствие, то, что бот может сделать, и некоторые предложения по взаимодействию.</span><span class="sxs-lookup"><span data-stu-id="59925-127">The message includes a greeting, what the bot can do, and some suggestions for how to interact.</span></span> <span data-ttu-id="59925-128">Например, "Попробуйте спросить меня о ...".</span><span class="sxs-lookup"><span data-stu-id="59925-128">For example, “Try asking me about …”.</span></span> <span data-ttu-id="59925-129">По возможности эти предложения должны возвращать готовые ответы, чтобы пользователю не обязательно было входить в систему.</span><span class="sxs-lookup"><span data-stu-id="59925-129">If possible, these suggestions should return stored responses without having to sign in.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="59925-130">Desktop</span><span class="sxs-lookup"><span data-stu-id="59925-130">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-personal-welcome.png" alt-text="В примере показано представление бота в личном приложении." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="59925-132">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="59925-132">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-personal-welcome.png" alt-text="В примере показано введение бота в личном приложении на мобильных устройствах." border="false":::

---

### <a name="welcome-message-in-channels-and-group-chats"></a><span data-ttu-id="59925-134">Приветствие в каналах и групповых чатах</span><span class="sxs-lookup"><span data-stu-id="59925-134">Welcome message in channels and group chats</span></span>

<span data-ttu-id="59925-135">Введение бота должно немного отличаться в каналах и групповых чатах по сравнению с личным пространством (например, личным приложением).</span><span class="sxs-lookup"><span data-stu-id="59925-135">Your bot's introduction should be slightly different in channels and group chats compared to a personal space (like a personal app).</span></span> <span data-ttu-id="59925-136">В реальной жизни, войдя в комнату, заполненную людьми, вы бы не стали приветствовать тех, кто там уже находится; вместо этого вы бы представились.</span><span class="sxs-lookup"><span data-stu-id="59925-136">In real life, if you entered a room full of people; you’d introduce yourself instead of welcoming everyone who’s already there.</span></span> <span data-ttu-id="59925-137">То же самое надо воплотить в конструкции бота.</span><span class="sxs-lookup"><span data-stu-id="59925-137">Carry that thinking into your bot design.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="59925-138">Desktop</span><span class="sxs-lookup"><span data-stu-id="59925-138">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-group-welcome.png" alt-text="В примере показано представление бота в контексте совместной работы." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="59925-140">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="59925-140">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-group-welcome.png" alt-text="В примере показано введение бота в контексте совместной работы на мобильных устройствах." border="false":::

---

### <a name="bot-authentication-with-single-sign-on"></a><span data-ttu-id="59925-142">Проверка подлинности бота при едином входе</span><span class="sxs-lookup"><span data-stu-id="59925-142">Bot authentication with single sign-on</span></span>

<span data-ttu-id="59925-143">Когда человек посылает сообщение боту, для использования всех функций бота человеку может потребоваться войти в систему.</span><span class="sxs-lookup"><span data-stu-id="59925-143">When a person messages a bot, sign in may be required use all its features.</span></span> <span data-ttu-id="59925-144">Вы можете упростить процесс проверки подлинности, используя единый вход.</span><span class="sxs-lookup"><span data-stu-id="59925-144">You can simplify the authentication process using single sign-on (SSO).</span></span>

<span data-ttu-id="59925-145">Не забывайте: в командном меню бота (**Что я умею делать?**) необходимо также предоставить команду для выхода из системы.</span><span class="sxs-lookup"><span data-stu-id="59925-145">Don’t forget: In the bot command menu (**What can I do?**), you must also provide a command to sign out.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="59925-146">Desktop</span><span class="sxs-lookup"><span data-stu-id="59925-146">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-sso-example.png" alt-text="В примере показан бот с кнопкой для входа в систему." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="59925-148">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="59925-148">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-sso-example.png" alt-text="В примере показан бот с кнопкой вход на мобильный телефон." border="false":::

---

### <a name="tours"></a><span data-ttu-id="59925-150">Обзоры</span><span class="sxs-lookup"><span data-stu-id="59925-150">Tours</span></span>

<span data-ttu-id="59925-151">Вы можете включить обзорное видео с приветствиями и указать, отвечает ли бот на что-нибудь вроде команды "справка".</span><span class="sxs-lookup"><span data-stu-id="59925-151">You can include a tour with welcome messages and if the bot responds to something like a “help” command.</span></span> <span data-ttu-id="59925-152">Обзор — самый эффективный способ описать, что может сделать бот.</span><span class="sxs-lookup"><span data-stu-id="59925-152">A tour is the most effective way to describe what your bot can do.</span></span> <span data-ttu-id="59925-153">Если применимо, они также отлично подходит для описания других функций приложения.</span><span class="sxs-lookup"><span data-stu-id="59925-153">If applicable, they’re also great for describing your app’s other features.</span></span> <span data-ttu-id="59925-154">Например, включите скриншоты расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="59925-154">For example, include screenshots of your messaging extension.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="59925-155">Обзоры должны быть доступны пользователям без входа в систему.</span><span class="sxs-lookup"><span data-stu-id="59925-155">Tours should be accessible without having to sign in.</span></span>

#### <a name="one-on-one-chats"></a><span data-ttu-id="59925-156">Чаты один на один</span><span class="sxs-lookup"><span data-stu-id="59925-156">One-on-one chats</span></span>

<span data-ttu-id="59925-157">В личном приложении карусель может предоставить эффективный обзор бота и любых других функций приложения.</span><span class="sxs-lookup"><span data-stu-id="59925-157">In a personal app, a carousel can provide an effective overview of your bot and any other features of your app.</span></span> <span data-ttu-id="59925-158">Рекомендуется включить кнопки, которые пользователи могут попробовать команды ботов.</span><span class="sxs-lookup"><span data-stu-id="59925-158">Including buttons the let users try bot commands is encouraged.</span></span> <span data-ttu-id="59925-159">Например, **создание задачи.**</span><span class="sxs-lookup"><span data-stu-id="59925-159">For example, **Create a task**.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="59925-160">Desktop</span><span class="sxs-lookup"><span data-stu-id="59925-160">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-tour-personal.png" alt-text="В примере показан видеообзор бота в чате с одним человеком." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="59925-162">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="59925-162">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-tour-personal.png" alt-text="В примере показана экскурсия по ботам в чате один на один на мобильном телефоне." border="false":::

---

#### <a name="channels-and-group-chats"></a><span data-ttu-id="59925-164">Каналы и групповые чаты</span><span class="sxs-lookup"><span data-stu-id="59925-164">Channels and group chats</span></span>

<span data-ttu-id="59925-165">В каналах и групповых чатах видеообзор должен открываться в модальном режиме (также известном как [модуль задач](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) чтобы не прерывать текущие беседы.</span><span class="sxs-lookup"><span data-stu-id="59925-165">In channels and group chats, a tour should open in a modal (also known as a [task module](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) so it doesn’t interrupt ongoing conversations.</span></span> <span data-ttu-id="59925-166">Это также дает возможность реализовать в обзоре представления на основе ролей.</span><span class="sxs-lookup"><span data-stu-id="59925-166">This also gives you the option to implement role-based views for your tour.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="59925-167">Desktop</span><span class="sxs-lookup"><span data-stu-id="59925-167">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-tour-channel.png" alt-text="В примере показан видеообзор бота в канале." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="59925-169">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="59925-169">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-tour-channel.png" alt-text="В примере показана экскурсия бота в канале на мобильных устройствах." border="false":::

---

## <a name="chat-with-a-bot"></a><span data-ttu-id="59925-171">Чат с ботом</span><span class="sxs-lookup"><span data-stu-id="59925-171">Chat with a bot</span></span>

<span data-ttu-id="59925-172">Боты интегрируются непосредственно в структуру обмена сообщениями Teams.</span><span class="sxs-lookup"><span data-stu-id="59925-172">Bots integrate directly into Team’s messaging framework.</span></span> <span data-ttu-id="59925-173">Пользователи могут общаться с ботом, чтобы получать ответы на свои вопросы, или вводить с клавиатуры команды, чтобы бот выполнял узкий или определенный набор задач.</span><span class="sxs-lookup"><span data-stu-id="59925-173">Users can chat with a bot to get their questions answered or type commands to have the bot perform a narrow or specific set of tasks.</span></span> <span data-ttu-id="59925-174">Боты могут заблаговременно уведомлять пользователей об изменениях или обновлениях приложения через чат.</span><span class="sxs-lookup"><span data-stu-id="59925-174">Bots can proactively notify users about changes or updates to your app via chat.</span></span>

### <a name="chat-with-a-bot-in-different-contexts"></a><span data-ttu-id="59925-175">Чат с ботом в разных контекстах</span><span class="sxs-lookup"><span data-stu-id="59925-175">Chat with a bot in different contexts</span></span>

<span data-ttu-id="59925-176">Ботов можно использовать в следующих контекстах:</span><span class="sxs-lookup"><span data-stu-id="59925-176">You can use bots in the following contexts:</span></span>

* <span data-ttu-id="59925-177">**Личные приложения**. В личном приложении у бота есть специальная вкладка чата.</span><span class="sxs-lookup"><span data-stu-id="59925-177">**Personal apps**: In a personal app, a bot has a dedicated chat tab.</span></span>
* <span data-ttu-id="59925-178">**Приватный чат**: пользователь может начать приватную беседу с ботом.</span><span class="sxs-lookup"><span data-stu-id="59925-178">**One-on-one chat**: A user can initiate a private conversation with a bot.</span></span> <span data-ttu-id="59925-179">Это то же самое, что и использование бота в личном приложении.</span><span class="sxs-lookup"><span data-stu-id="59925-179">It's the same experience as using a bot in a personal app.</span></span>
* <span data-ttu-id="59925-180">**Групповой чат**: люди могут взаимодействовать с ботом в групповом чате, @упоминая бота.</span><span class="sxs-lookup"><span data-stu-id="59925-180">**Group chat**: People can interact with a bot in a group chat by @mentioning the bot.</span></span>
* <span data-ttu-id="59925-181">**Канал**: люди могут взаимодействовать с ботом в канале.</span><span class="sxs-lookup"><span data-stu-id="59925-181">**Channel**: People can interact with a bot in a channel.</span></span> <span data-ttu-id="59925-182">@упоминанием имени бота в поле "Создать".</span><span class="sxs-lookup"><span data-stu-id="59925-182">by @mentioning the bot name in the compose box.</span></span> <span data-ttu-id="59925-183">Помните, что в этом контексте бот доступен всей группе, а не только каналу.</span><span class="sxs-lookup"><span data-stu-id="59925-183">Remember, in this context, the bot is available to the entire team, not just the channel.</span></span>

### <a name="anatomy"></a><span data-ttu-id="59925-184">Анатомия</span><span class="sxs-lookup"><span data-stu-id="59925-184">Anatomy</span></span>

# <a name="desktop"></a>[<span data-ttu-id="59925-185">Desktop</span><span class="sxs-lookup"><span data-stu-id="59925-185">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-anatomy.png" alt-text="В примере показана структурная анатомия бота." border="false":::

|<span data-ttu-id="59925-187">Счетчик</span><span class="sxs-lookup"><span data-stu-id="59925-187">Counter</span></span>|<span data-ttu-id="59925-188">Описание</span><span class="sxs-lookup"><span data-stu-id="59925-188">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="59925-189">1</span><span class="sxs-lookup"><span data-stu-id="59925-189">1</span></span>|<span data-ttu-id="59925-190">**Имя и значок приложения**</span><span class="sxs-lookup"><span data-stu-id="59925-190">**App name and icon**</span></span>|
|<span data-ttu-id="59925-191">2</span><span class="sxs-lookup"><span data-stu-id="59925-191">2</span></span>|<span data-ttu-id="59925-192">**Вкладка чата**: открывает пространство для общения с ботом (только для личных приложений).</span><span class="sxs-lookup"><span data-stu-id="59925-192">**Chat tab**: Opens the space to talk with your bot (applicable only to personal apps).</span></span>|
|<span data-ttu-id="59925-193">3</span><span class="sxs-lookup"><span data-stu-id="59925-193">3</span></span>|<span data-ttu-id="59925-194">**Настраиваемые вкладки**: открывает другое содержимое, связанное с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="59925-194">**Custom tabs**: Opens other content related to your app.</span></span>|
|<span data-ttu-id="59925-195">4 </span><span class="sxs-lookup"><span data-stu-id="59925-195">4</span></span>|<span data-ttu-id="59925-196">**Сведения**: выводит на экран основные сведения о приложении.</span><span class="sxs-lookup"><span data-stu-id="59925-196">**About tab**: Displays basic information about your app.</span></span>|
|<span data-ttu-id="59925-197">5 </span><span class="sxs-lookup"><span data-stu-id="59925-197">5</span></span>|<span data-ttu-id="59925-198">**Пузырек чата**: беседы ботов используют структуру обмена сообщениями Teams.</span><span class="sxs-lookup"><span data-stu-id="59925-198">**Chat bubble**: Bot conversations use the Teams messaging framework.</span></span>|
|<span data-ttu-id="59925-199">6 </span><span class="sxs-lookup"><span data-stu-id="59925-199">6</span></span>|<span data-ttu-id="59925-200">**Адаптивная карта.** Если ответы бота включают адаптивные карты, карта занимает полную ширину пузыря чата.</span><span class="sxs-lookup"><span data-stu-id="59925-200">**Adaptive Card**: If your bot's responses include Adaptive Cards, the card takes up the full width of the chat bubble.</span></span>|
|<span data-ttu-id="59925-201">7 </span><span class="sxs-lookup"><span data-stu-id="59925-201">7</span></span>|<span data-ttu-id="59925-202">**Меню команд**: отображает стандартные команды бота (определенные вами).</span><span class="sxs-lookup"><span data-stu-id="59925-202">**Command menu**: Displays your bot's standard commands (defined by you).</span></span>|

# <a name="mobile"></a>[<span data-ttu-id="59925-203">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="59925-203">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-anatomy.png" alt-text="В примере показана структурная анатомия мобильного бота." border="false":::

|<span data-ttu-id="59925-205">Счетчик</span><span class="sxs-lookup"><span data-stu-id="59925-205">Counter</span></span>|<span data-ttu-id="59925-206">Описание</span><span class="sxs-lookup"><span data-stu-id="59925-206">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="59925-207">1</span><span class="sxs-lookup"><span data-stu-id="59925-207">1</span></span>|<span data-ttu-id="59925-208">**Имя и значок приложения**</span><span class="sxs-lookup"><span data-stu-id="59925-208">**App name and icon**</span></span>|
|<span data-ttu-id="59925-209">2</span><span class="sxs-lookup"><span data-stu-id="59925-209">2</span></span>|<span data-ttu-id="59925-210">**Вкладка чата**: открывает пространство для общения с ботом (только для личных приложений).</span><span class="sxs-lookup"><span data-stu-id="59925-210">**Chat tab**: Opens the space to talk with your bot (applicable only to personal apps).</span></span>|
|<span data-ttu-id="59925-211">3</span><span class="sxs-lookup"><span data-stu-id="59925-211">3</span></span>|<span data-ttu-id="59925-212">**Настраиваемые вкладки**: открывает другое содержимое, связанное с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="59925-212">**Custom tabs**: Opens other content related to your app.</span></span>|
|<span data-ttu-id="59925-213">4 </span><span class="sxs-lookup"><span data-stu-id="59925-213">4</span></span>|<span data-ttu-id="59925-214">**Пузырек чата**: беседы ботов используют структуру обмена сообщениями Teams.</span><span class="sxs-lookup"><span data-stu-id="59925-214">**Chat bubble**: Bot conversations use the Teams messaging framework.</span></span>|
|<span data-ttu-id="59925-215">5 </span><span class="sxs-lookup"><span data-stu-id="59925-215">5</span></span>|<span data-ttu-id="59925-216">**Адаптивная карта.** Если ответы бота включают адаптивные карты, карта занимает полную ширину пузыря чата.</span><span class="sxs-lookup"><span data-stu-id="59925-216">**Adaptive Card**: If your bot's responses include Adaptive Cards, the card takes up the full width of the chat bubble.</span></span>|

---

### <a name="command-menu"></a><span data-ttu-id="59925-217">Меню команд</span><span class="sxs-lookup"><span data-stu-id="59925-217">Command menu</span></span>

<span data-ttu-id="59925-218">В командном меню содержится список слов или фраз, на которые бот должен отвечать всегда.</span><span class="sxs-lookup"><span data-stu-id="59925-218">The command menu provides a list of words or phrases you want your bot to always respond to.</span></span> <span data-ttu-id="59925-219">Меню команд отображается над полем "Создать", когда кто-нибудь беседует с ботом.</span><span class="sxs-lookup"><span data-stu-id="59925-219">The command menu displays above the compose box when someone is conversing with a bot.</span></span> <span data-ttu-id="59925-220">При выборе команды она вставляется в сообщение.</span><span class="sxs-lookup"><span data-stu-id="59925-220">When a command is selected, it gets inserted into a message.</span></span>

<span data-ttu-id="59925-221">Список команд должен быть кратким.</span><span class="sxs-lookup"><span data-stu-id="59925-221">The list of commands should be brief.</span></span> <span data-ttu-id="59925-222">Меню предназначено только для выделения основных функций бота.</span><span class="sxs-lookup"><span data-stu-id="59925-222">The menu is only meant to highlight your bot’s primary features.</span></span> <span data-ttu-id="59925-223">Команды также должны быть краткими.</span><span class="sxs-lookup"><span data-stu-id="59925-223">Keep commands concise, too.</span></span> <span data-ttu-id="59925-224">Например, создайте команду **Помоги** вместо **Вы бы не могли мне помочь?**</span><span class="sxs-lookup"><span data-stu-id="59925-224">For example, create a command called **Help** instead of **Can you please help me**?</span></span>
<span data-ttu-id="59925-225">Меню команд должно всегда быть доступно независимо от состояния беседы.</span><span class="sxs-lookup"><span data-stu-id="59925-225">The command menu must always be available regardless of the state of the conversation.</span></span>

:::image type="content" source="../../assets/images/bots/bot-command-menu.png" alt-text="В примере показано меню команд бота." border="false":::

## <a name="understand-what-people-are-saying"></a><span data-ttu-id="59925-227">Понимание того, что говорят люди</span><span class="sxs-lookup"><span data-stu-id="59925-227">Understand what people are saying</span></span>

<span data-ttu-id="59925-228">Используйте толковый словарь и попросите людей из разных слоев общества и с разным уровнем образования (столько, сколько удастся найти), чтобы помочь вам выработать различные интерпретации стандартных запросов.</span><span class="sxs-lookup"><span data-stu-id="59925-228">Use a thesaurus and get people from as many different backgrounds as possible to help you generate different interpretations of standard queries.</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-hello.png" alt-text="Иллюстрация того, как бот может интерпретировать &quot;Привет&quot;." border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-help.png" alt-text="Иллюстрация того, как бот может интерпретировать &quot;Помоги&quot;." border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-thanks.png" alt-text="Иллюстрация того, как бот может интерпретировать &quot;Спасибо&quot;." border="false":::
   :::column-end:::
:::row-end:::

### <a name="extract-intent-and-data-from-messages"></a><span data-ttu-id="59925-232">Извлечение намерения и данных из сообщений</span><span class="sxs-lookup"><span data-stu-id="59925-232">Extract intent and data from messages</span></span>

<span data-ttu-id="59925-233">Разрабатывайте бот так, чтобы он умел понимать намерения, то есть понимать, чего хочет пользователь от бота в ответ на сообщение или запрос.</span><span class="sxs-lookup"><span data-stu-id="59925-233">Design your bot to recognize intent, which captures what someone wants from a bot in response to a message or query.</span></span> <span data-ttu-id="59925-234">Цель классифицирует сообщение или запрос как одно действие с одним или более объектами данных, на которые влияет это действие.</span><span class="sxs-lookup"><span data-stu-id="59925-234">Intent classifies a message or query as a single action with one or more data objects that are affected by the action.</span></span> 

<span data-ttu-id="59925-235">В следующих примерах описаны намерения пользователя и данные в сообщениях, отправленных ботам:</span><span class="sxs-lookup"><span data-stu-id="59925-235">The following examples outline the user intent and data in messages sent to bots:</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-1.png" alt-text="В предложении &quot;Забронировать рейс в Сиэтл&quot; намерение пользователя — &quot;забронировать рейс&quot;, а данные — &quot;Сиэтл&quot;." border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-2.png" alt-text="В предложении &quot;Когда открыт магазин&quot; намерение пользователя — &quot;когда&quot;, а данные — &quot;открыт&quot;." border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-3.png" alt-text="В предложении &quot;Запланировать встречу с Бобом из отдела распространения на 13:00&quot;, намерение пользователя — &quot;запланировать встречу&quot;, а данные — &quot;13:00&quot; и &quot;Боб из отдела распространения&quot;." border="false":::
   :::column-end:::
:::row-end:::

### <a name="analyze-and-improve"></a><span data-ttu-id="59925-239">Анализируйте и совершенствуйте</span><span class="sxs-lookup"><span data-stu-id="59925-239">Analyze and improve</span></span>

<span data-ttu-id="59925-240">Узнавайте, что говорят пользователи при чате с ботом.</span><span class="sxs-lookup"><span data-stu-id="59925-240">Learn what users say when chatting with your bot.</span></span> <span data-ttu-id="59925-241">Это будет непрерывный итеративный процесс по мере роста пользовательской базы в разных расположениях и организациях.</span><span class="sxs-lookup"><span data-stu-id="59925-241">This will be an ongoing, iterative process as your user base grows in different locations and orgs.</span></span> <span data-ttu-id="59925-242">Оттачивать умение бота распознавать язык и намерения можно с помощью Microsoft Language Understanding (LUIS).</span><span class="sxs-lookup"><span data-stu-id="59925-242">You can tune your bot's language recognition and intent mapping with Microsoft Language Understanding (LUIS).</span></span>

* <span data-ttu-id="59925-243">[Понимание LUIS](/azure/cognitive-services/luis/artificial-intelligence). Узнайте, как LUIS использует ИИ для понимания естественного языка (NLU), чтобы оперировать данными приложения.</span><span class="sxs-lookup"><span data-stu-id="59925-243">[Understanding LUIS](/azure/cognitive-services/luis/artificial-intelligence): Find out how LUIS uses AI to provide natural language understanding (NLU) to your app data.</span></span>
* <span data-ttu-id="59925-244">[Интеграция с LUIS](https://www.luis.ai/). Вы можете добавлять боту возможности естественного языка, не создавая сложных моделей машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="59925-244">[Integrating with LUIS](https://www.luis.ai/): Add natural language capabilities to your bot without the complex process of creating machine learning models.</span></span>

## <a name="use-cases"></a><span data-ttu-id="59925-245">Варианты использования</span><span class="sxs-lookup"><span data-stu-id="59925-245">Use cases</span></span>

### <a name="simple-queries"></a><span data-ttu-id="59925-246">Простые запросы</span><span class="sxs-lookup"><span data-stu-id="59925-246">Simple queries</span></span>

<span data-ttu-id="59925-247">Боты могут доставлять точное соответствие запросу или группе родственных соответствий, чтобы устранить двойственность.</span><span class="sxs-lookup"><span data-stu-id="59925-247">Bots can deliver an exact match to a query or a group of related matches to help with disambiguation.</span></span> <span data-ttu-id="59925-248">Для получения родственных соответствий группируйте содержимое с помощью карточки списка.</span><span class="sxs-lookup"><span data-stu-id="59925-248">For related matches, group the content using a list card.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="59925-249">Desktop</span><span class="sxs-lookup"><span data-stu-id="59925-249">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-simple-query.png" alt-text="В примере показано взаимодействие с ботом для выполнения простого запроса." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="59925-251">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="59925-251">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-simple-query.png" alt-text="В примере показано простое взаимодействие запроса с ботом на мобильных устройствах." border="false":::

---

### <a name="multi-turn-interactions"></a><span data-ttu-id="59925-253">Взаимодействие с несколькими поворотами</span><span class="sxs-lookup"><span data-stu-id="59925-253">Multi-turn interactions</span></span>

<span data-ttu-id="59925-254">Бот может поддерживать выполнение запросов и отвечать вопросы, но он также должен уметь обрабатывать взаимодействия с несколькими поворотами.</span><span class="sxs-lookup"><span data-stu-id="59925-254">While your bot can support complete requests and questions, it should also be able to handle multi-turn interactions.</span></span> <span data-ttu-id="59925-255">Если бот предугадывает возможные дальнейшие действия пользователя, людям будет намного проще выполнить задание. Для них это легче, чем сразу составить сложный запрос.</span><span class="sxs-lookup"><span data-stu-id="59925-255">Anticipating possible next steps makes it much easier for people to a complete task flow (rather than expecting them to craft a comprehensive request).</span></span>

<span data-ttu-id="59925-256">В следующих примерах бот отвечает на каждое сообщение с вариантами того, что может потребоваться сделать дальше.</span><span class="sxs-lookup"><span data-stu-id="59925-256">In the following examples, the bot responds to each message with options for what might want to do next.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="59925-257">Desktop</span><span class="sxs-lookup"><span data-stu-id="59925-257">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-multi-turn.png" alt-text="В примере показано взаимодействие с ботом с несколькими поворотами." border="false":::


# <a name="mobile"></a>[<span data-ttu-id="59925-259">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="59925-259">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-multi-turn.png" alt-text="В примере показано многоступенчатое взаимодействие с ботом на мобильных устройствах." border="false":::


---

### <a name="reach-out-to-users"></a><span data-ttu-id="59925-261">Инициируйте общение с пользователями</span><span class="sxs-lookup"><span data-stu-id="59925-261">Reach out to users</span></span>

<span data-ttu-id="59925-262">С помощью проактивных сообщений бот может действовать как дайджест, который с определенной периодичностью отправляет уведомления, актуальные для отдельного лица, группового чата или канала.</span><span class="sxs-lookup"><span data-stu-id="59925-262">With proactive messaging, your bot can act like a digest that sends notifications relevant to an individual, group chat, or channel at a specific frequency.</span></span> <span data-ttu-id="59925-263">Бот может отправить сообщение, если что-то изменилось в документе или когда завершено рабочее задание.</span><span class="sxs-lookup"><span data-stu-id="59925-263">A bot may send a message when something has changed in a document or a work item is closed.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="59925-264">Desktop</span><span class="sxs-lookup"><span data-stu-id="59925-264">Desktop</span></span>](#tab/desktop)

<span data-ttu-id="59925-265">В следующем примере пользователь получает всплывающее уведомление о том, что бот передает им сообщения в другом канале.</span><span class="sxs-lookup"><span data-stu-id="59925-265">In the following example, the user gets a toast notification that a bot messaged them in another channel.</span></span>

:::image type="content" source="../../assets/images/bots/bot-proactive-message-toast.png" alt-text="В примере показано всплывающее уведомление бота, который проактивно посылает сообщение пользователю из другого канала." border="false":::

<span data-ttu-id="59925-267">Теперь в этом канале пользователь может прочитать свое сообщение от бота.</span><span class="sxs-lookup"><span data-stu-id="59925-267">Now in that channel, the user can read their message from the bot.</span></span>

:::image type="content" source="../../assets/images/bots/bot-proactive-message.png" alt-text="В примере показано, как пользователь смотрит на проактивные сообщения бота." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="59925-269">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="59925-269">Mobile</span></span>](#tab/mobile)

<span data-ttu-id="59925-270">В следующем примере пользователь получает уведомление о том, что бот передает их в другом канале.</span><span class="sxs-lookup"><span data-stu-id="59925-270">In the following example, the user gets a notification that a bot messaged them in another channel.</span></span>

:::image type="content" source="../../assets/images/bots/mobile-bot-proactive-message-toast.png" alt-text="В примере показан тост бота, который активно передает сообщения пользователю из другого канала на мобильных устройствах." border="false":::

<span data-ttu-id="59925-272">Теперь в этом канале пользователь может прочитать свое сообщение от бота.</span><span class="sxs-lookup"><span data-stu-id="59925-272">Now in that channel, the user can read their message from the bot.</span></span>

:::image type="content" source="../../assets/images/bots/mobile-bot-proactive-message.png" alt-text="В примере показано, как пользователь смотрит на проактивное сообщение бота на мобильных устройствах." border="false":::

---

### <a name="use-tabs-with-bots"></a><span data-ttu-id="59925-274">Использование вкладок с ботами</span><span class="sxs-lookup"><span data-stu-id="59925-274">Use tabs with bots</span></span>

<span data-ttu-id="59925-275">В личных приложениях вкладка может дополнять то, что может сделать бот.</span><span class="sxs-lookup"><span data-stu-id="59925-275">In personal apps, a tab can complement what your bot can do.</span></span> <span data-ttu-id="59925-276">Например, если бот может создавать рабочие элементы, хорошо показать все эти элементы в центральном расположении на вкладке. Дополнительные сведения [о разработке вкладок](../../tabs/design/tabs.md).</span><span class="sxs-lookup"><span data-stu-id="59925-276">For example, if your bot can create work items, it would be nice to show all those items in a central location inside a tab. See more about [designing tabs](../../tabs/design/tabs.md).</span></span>

# <a name="desktop"></a>[<span data-ttu-id="59925-277">Desktop</span><span class="sxs-lookup"><span data-stu-id="59925-277">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-with-tab.png" alt-text="В примере показано, как вкладка помогает упорядочизировать содержимое бота." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="59925-279">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="59925-279">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-with-tab.png" alt-text="В примере показано, как вкладка может помочь организовать содержимое бота на мобильных устройствах." border="false":::

---

## <a name="manage-a-bot"></a><span data-ttu-id="59925-281">Управление ботом</span><span class="sxs-lookup"><span data-stu-id="59925-281">Manage a bot</span></span>

<span data-ttu-id="59925-282">Пользователи должны иметь возможность менять настройки бота.</span><span class="sxs-lookup"><span data-stu-id="59925-282">Users should be able to change a bot's settings.</span></span> <span data-ttu-id="59925-283">Эту функцию можно предоставить с помощью команд бота, но обычно эффективнее включать все параметры в [модуль задач](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) (как показано в следующем примере).</span><span class="sxs-lookup"><span data-stu-id="59925-283">You can provide this functionality with bot commands, but it's usually more efficient to include all settings in a [task module](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) (as shown in the following example).</span></span>

:::image type="content" source="../../assets/images/bots/manage-bot-task-module.png" alt-text="В примере показан модуль задач для настройки параметров бота." border="false":::

## <a name="best-practices"></a><span data-ttu-id="59925-285">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="59925-285">Best practices</span></span>

<span data-ttu-id="59925-286">Используйте эти рекомендации для создания качественного приложения.</span><span class="sxs-lookup"><span data-stu-id="59925-286">Use these recommendations to create a quality app experience.</span></span>

### <a name="content"></a><span data-ttu-id="59925-287">Статья</span><span class="sxs-lookup"><span data-stu-id="59925-287">Content</span></span>

:::image type="content" source="../../assets/images/bots/bot-content-persona-do.png" alt-text="Пример, показывающий лучшую практику бота для создания четкого человека." border="false":::

#### <a name="do-establish-a-clear-persona"></a><span data-ttu-id="59925-289">Как надо: создать отчетливо выраженную личность</span><span class="sxs-lookup"><span data-stu-id="59925-289">Do: Establish a clear persona</span></span>

<span data-ttu-id="59925-290">Как держится ваш бот? Разговаривает двружелюбно и легко? Сухо излагает факты? А может, он со странностями?</span><span class="sxs-lookup"><span data-stu-id="59925-290">Is your bot's tone friendly and light, “just the facts”, or super quirky?</span></span> <span data-ttu-id="59925-291">Как он должен реагировать в различных сценариях?</span><span class="sxs-lookup"><span data-stu-id="59925-291">How should it respond in different scenarios?</span></span> <span data-ttu-id="59925-292">Если вы заранее продумаете и документируете личность бота, вам будет проще написать для него ответы, звучащие естественно и связно.</span><span class="sxs-lookup"><span data-stu-id="59925-292">Planning and documenting your bot's persona makes it easier to write responses that seem natural and cohesive.</span></span>

<span data-ttu-id="59925-293">Узнайте больше о написании ботов в статье <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">Комплект разработчика пользовательских интерфейсов Microsoft Teams (Figma).</a></span><span class="sxs-lookup"><span data-stu-id="59925-293">See more about writing for bots in the <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">Microsoft Teams UI Kit (Figma).</a></span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-convey-do.png" alt-text="Пример, показывающий четкое отображение того, что может сделать бот." border="false":::

#### <a name="do-clearly-convey-what-your-bot-can-do"></a><span data-ttu-id="59925-295">Как надо: четко обозначьте, что умеет делать ваш бот</span><span class="sxs-lookup"><span data-stu-id="59925-295">Do: Clearly convey what your bot can do</span></span>

<span data-ttu-id="59925-296">Приветствия и обзоры помогают пользователям понять, что они могут делать с вашим ботом.</span><span class="sxs-lookup"><span data-stu-id="59925-296">Welcome messages and tours help people understand what they can do with your bot.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-convey-dont.png" alt-text="Пример, показывающий, что функции бота не заслонятся." border="false":::

#### <a name="dont-obscure-your-bots-features"></a><span data-ttu-id="59925-298">Как не надо: скрывать функции бота</span><span class="sxs-lookup"><span data-stu-id="59925-298">Don't: Obscure your bot's features</span></span>

<span data-ttu-id="59925-299">Первые впечатления очень важны.</span><span class="sxs-lookup"><span data-stu-id="59925-299">First impressions matter.</span></span> <span data-ttu-id="59925-300">Увидев ничего не говорящее сообщение о входе, люди, скорее всего, растеряются или заподозрят неладное.</span><span class="sxs-lookup"><span data-stu-id="59925-300">People will likely be confused or suspicious when presented with a nondescript sign-in message.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-understand-do.png" alt-text="Пример, показывающий, что бот должен распознавать не вопросы." border="false":::

#### <a name="do-recognize-non-questions"></a><span data-ttu-id="59925-302">Как надо: распознавать вопросы, которые не являются вопросами</span><span class="sxs-lookup"><span data-stu-id="59925-302">Do: Recognize non-questions</span></span>

<span data-ttu-id="59925-303">Бот должен уметь отвечать на такие сообщения, как "Привет", "Помоги" и "Спасибо", а также вносить поправки на распространенные опечатки и разговорные выражения.</span><span class="sxs-lookup"><span data-stu-id="59925-303">Your bot should be able to respond to messages like "Hi", "Help", and "Thanks" while also accounting for common misspellings and colloquialisms.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-understand-dont.png" alt-text="Пример, показывающий, что следует избегать неуклюжих ответов на простые сообщения ботов." border="false":::

#### <a name="dont-miss-out-on-opportunities-to-delight"></a><span data-ttu-id="59925-305">Как не надо: не упускайте случая порадовать пользователей</span><span class="sxs-lookup"><span data-stu-id="59925-305">Don't: Miss out on opportunities to delight</span></span>

<span data-ttu-id="59925-306">Некоторые люди ожидают, что беседы с ботом будут идти естественно, совсем как с живым человеком.</span><span class="sxs-lookup"><span data-stu-id="59925-306">Some people expect conversations to flow naturally like they would with a real person.</span></span> <span data-ttu-id="59925-307">Постарайтесь избежать неуклюжих ответов на простые сообщения.</span><span class="sxs-lookup"><span data-stu-id="59925-307">Try to avoid clumsy responses to simple messages.</span></span>

   :::column-end:::
:::row-end:::

### <a name="troubleshooting"></a><span data-ttu-id="59925-308">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="59925-308">Troubleshooting</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-help-do.png" alt-text="Пример, в котором показаны боты, должен помочь пользователям понять, как использовать ботов." border="false":::

#### <a name="do-provide-help"></a><span data-ttu-id="59925-310">Как надо: предоставляйте помощь</span><span class="sxs-lookup"><span data-stu-id="59925-310">Do: Provide help</span></span>

<span data-ttu-id="59925-311">Если ваш бот не может выполнить запрос, дайте пользователю возможность научиться взаимодействию с ботом.</span><span class="sxs-lookup"><span data-stu-id="59925-311">If your bot can’t satisfy a request, provide ways for a user to educate themselves about interacting with your bot.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-help-dont.png" alt-text="Пример, показывающий, что пользователь бота не должен прядить пользователей." border="false":::

#### <a name="dont-leave-users-stranded"></a><span data-ttu-id="59925-313">Как не надо: не бросайте пользователей в беде</span><span class="sxs-lookup"><span data-stu-id="59925-313">Don't: Leave users stranded</span></span>

<span data-ttu-id="59925-314">Люди быстро перестанут общаться с ботом, если не смогут устранить его неполадки.</span><span class="sxs-lookup"><span data-stu-id="59925-314">People will quickly abandon your bot if they can’t troubleshoot issues.</span></span>

   :::column-end:::
:::row-end:::

### <a name="complex-interactions"></a><span data-ttu-id="59925-315">Сложные взаимодействия</span><span class="sxs-lookup"><span data-stu-id="59925-315">Complex interactions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-interactions-do.png" alt-text="Пример, показывающий, что вы можете использовать модули задач или вкладки с ботом для сложных взаимодействий." border="false":::

#### <a name="do-use-task-modules-or-tabs"></a><span data-ttu-id="59925-317">Как надо: используйте модули задач или вкладки</span><span class="sxs-lookup"><span data-stu-id="59925-317">Do: Use task modules or tabs</span></span>

<span data-ttu-id="59925-318">Если бот предоставляет ответ, требующий выполнения еще нескольких действий, вы можете для завершения действия или последовательности действий предоставить ссылку на модуль задач или вкладку.</span><span class="sxs-lookup"><span data-stu-id="59925-318">If your bot provides an answer that requires a few more steps, you can link to a task module or tab to complete the task or flow.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-interactions-dont.png" alt-text="Пример, показывающий, как бот должен избегать многовекового взаимодействия." border="false":::

#### <a name="dont-make-multi-turn-interactions-tedious"></a><span data-ttu-id="59925-320">Как не надо: не делайте взаимодействие с несколькими поворотами утомительными</span><span class="sxs-lookup"><span data-stu-id="59925-320">Don't: Make multi-turn interactions tedious</span></span>

<span data-ttu-id="59925-321">Если пользователю для выполнения одной задачи приходится вести пространные беседы, это слишком долго и сложно.</span><span class="sxs-lookup"><span data-stu-id="59925-321">An extensive conversation to complete a single task is slow and overly complex.</span></span> <span data-ttu-id="59925-322">Кроме того, разработчик должен учитывать изменения состояния (например, когда время беседы истекло или пользователь отправил сообщение "Отмена").</span><span class="sxs-lookup"><span data-stu-id="59925-322">It also requires the developer to account for state changes (such as the conversation timing out or you sending a “Cancel” message).</span></span>

   :::column-end:::
:::row-end:::

### <a name="privacy"></a><span data-ttu-id="59925-323">Конфиденциальность</span><span class="sxs-lookup"><span data-stu-id="59925-323">Privacy</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-privacy-do.png" alt-text="Пример, показывающий, как боты должны показывать закрытые сведения только в личном контексте." border="false":::

#### <a name="do-only-show-sensitive-info-in-a-personal-context"></a><span data-ttu-id="59925-325">Как надо: показывать конфиденциальную информацию только в личном контексте</span><span class="sxs-lookup"><span data-stu-id="59925-325">Do: Only show sensitive info in a personal context</span></span>

<span data-ttu-id="59925-326">Если бот находится в групповом чате или канале, для просмотра конфиденциальной информации рекомендуется направлять пользователей в приватное расположение (например, модуль задач, вкладку или браузер).</span><span class="sxs-lookup"><span data-stu-id="59925-326">If your bot is in a group chat or channel, we recommend directing users to a private location (such as a task module, tab, or browser) to view sensitive information.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-privacy-dont.png" alt-text="Пример, показывающий, как боты не должны раскрывать конфиденциальные сведения группе или людям." border="false":::

#### <a name="dont-some-content-isnt-meant-to-be-seen-by-everyone"></a><span data-ttu-id="59925-328">Как не надо: некоторые данные предназначены не для всех</span><span class="sxs-lookup"><span data-stu-id="59925-328">Don't: Some content isn’t meant to be seen by everyone</span></span>

<span data-ttu-id="59925-329">Бот не должен раскрывать конфиденциальную информацию группе людей.</span><span class="sxs-lookup"><span data-stu-id="59925-329">Your bot shouldn’t reveal sensitive information to a group of people.</span></span>

   :::column-end:::
:::row-end:::

## <a name="see-also"></a><span data-ttu-id="59925-330">См. также</span><span class="sxs-lookup"><span data-stu-id="59925-330">See also</span></span>

<span data-ttu-id="59925-331">Вот еще рекомендации, которые могут быть полезными при разработке бота:</span><span class="sxs-lookup"><span data-stu-id="59925-331">These other guidelines may help with your bot design:</span></span>

* [<span data-ttu-id="59925-332">Проектирование личного приложения</span><span class="sxs-lookup"><span data-stu-id="59925-332">Designing your personal app</span></span>](../../concepts/design/personal-apps.md)
* [<span data-ttu-id="59925-333">Проектирование адаптивной карточки</span><span class="sxs-lookup"><span data-stu-id="59925-333">Designing Adaptive Cards</span></span>](../../task-modules-and-cards/cards/design-effective-cards.md)
* [<span data-ttu-id="59925-334">Проектирование модулей задач</span><span class="sxs-lookup"><span data-stu-id="59925-334">Designing task modules</span></span>](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)
