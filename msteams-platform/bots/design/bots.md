---
title: Создание бота
description: Узнайте, как создать бот Teams, и получите комплект разработчика для пользовательского интерфейса Microsoft Teams.
author: heath-hamilton
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: da289b37340f575eda8eb858b13810df48783728
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566147"
---
# <a name="designing-your-microsoft-teams-bot"></a><span data-ttu-id="4d5df-103">Создание бота Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="4d5df-103">Designing your Microsoft Teams bot</span></span>

<span data-ttu-id="4d5df-104">Боты — это приложения для бесед, которые выполняют определенный набор задач.</span><span class="sxs-lookup"><span data-stu-id="4d5df-104">Bots are conversational apps that perform a specific set of tasks.</span></span> <span data-ttu-id="4d5df-105">Построенные на основе <a href="https://dev.botframework.com/" target="_blank">Microsoft Bot Framework</a>боты общаются с пользователями, отвечают на их вопросы и заблаговременно уведомляют их об изменениях и других событиях.</span><span class="sxs-lookup"><span data-stu-id="4d5df-105">Based on the <a href="https://dev.botframework.com/" target="_blank">Microsoft Bot Framework</a>, bots communicate with users, respond to their questions, and proactively notify them about changes and other events.</span></span> <span data-ttu-id="4d5df-106">Это отличный способ связи с пользователями.</span><span class="sxs-lookup"><span data-stu-id="4d5df-106">They're a great way to reach out.</span></span>

<span data-ttu-id="4d5df-107">Далее описано и показано, как люди могут добавлять ботов, использовать их и управлять ими в Teams. Это может помочь вам в создании приложения.</span><span class="sxs-lookup"><span data-stu-id="4d5df-107">To guide your app design, the following information describes and illustrates how people can add, use, and manage bots in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="4d5df-108">Комплект разработчика для пользовательского интерфейса Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="4d5df-108">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="4d5df-109">В комплекте разработчика для пользовательского интерфейса Microsoft Teams можно найти более полные рекомендации по проектированию ботов, в том числе элементы, которые можно взять и изменить так, как нужно вам.</span><span class="sxs-lookup"><span data-stu-id="4d5df-109">You can find more comprehensive bot design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4d5df-110">Получить комплект разработчика для пользовательского интерфейса Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="4d5df-110">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-bot"></a><span data-ttu-id="4d5df-111">Добавить бота</span><span class="sxs-lookup"><span data-stu-id="4d5df-111">Add a bot</span></span>

<span data-ttu-id="4d5df-112">Боты доступны в чатах, каналах и личных приложениях.</span><span class="sxs-lookup"><span data-stu-id="4d5df-112">Bots are available in chats, channels, and personal apps.</span></span> <span data-ttu-id="4d5df-113">Бота можно добавить одним из указанных ниже способов.</span><span class="sxs-lookup"><span data-stu-id="4d5df-113">You can add a bot one of the following ways:</span></span>

* <span data-ttu-id="4d5df-114">Взять в магазине Teams (AppSource)</span><span class="sxs-lookup"><span data-stu-id="4d5df-114">From the Teams store (AppSource).</span></span>
* <span data-ttu-id="4d5df-115">Использовать всплывающее окно приложения. Для этого выберите значок **Дополнительные** в левой части экрана Teams.</span><span class="sxs-lookup"><span data-stu-id="4d5df-115">Using the app flyout by selecting the **More** icon on the left side of Teams.</span></span>
* <span data-ttu-id="4d5df-116">С помощью @упоминания в новом чате или поле "Создать" (в следующем примере показано, как это можно сделать в групповом чате).</span><span class="sxs-lookup"><span data-stu-id="4d5df-116">With an @mention in the new chat or compose box (the following example shows how you can do this in a group chat).</span></span>

    :::image type="content" source="../../assets/images/bots/add-bot-chat-at-mention.png" alt-text="В примере показано, как добавить бота в групповой чат с помощью @упоминания." border="false":::

## <a name="introduce-a-bot"></a><span data-ttu-id="4d5df-118">Представление бота</span><span class="sxs-lookup"><span data-stu-id="4d5df-118">Introduce a bot</span></span>

<span data-ttu-id="4d5df-119">Очень важно, чтобы бот сам себя представлял и объяснял, что он умеет делать.</span><span class="sxs-lookup"><span data-stu-id="4d5df-119">It’s critical that your bot introduces itself and describes what it can do.</span></span> <span data-ttu-id="4d5df-120">Первоначальный обмен репликами с ботом помогает пользователям понять, что с ним делать, узнать его ограничения и, что самое важное, освоиться с ним.</span><span class="sxs-lookup"><span data-stu-id="4d5df-120">This initial exchange helps people understand what to do with the bot, find out its limitations and, most importantly, get comfortable interacting with it.</span></span>

### <a name="welcome-message-in-a-one-on-one-chat"></a><span data-ttu-id="4d5df-121">Приветствие в чате один на один</span><span class="sxs-lookup"><span data-stu-id="4d5df-121">Welcome message in a one-on-one chat</span></span>

<span data-ttu-id="4d5df-122">В личных контекстах приветствия задают тон бота.</span><span class="sxs-lookup"><span data-stu-id="4d5df-122">In personal contexts, welcome messages set your bot's tone.</span></span> <span data-ttu-id="4d5df-123">Сообщение включает в себя приветствие, что бот может сделать, и некоторые предложения о том, как взаимодействовать.</span><span class="sxs-lookup"><span data-stu-id="4d5df-123">The message includes a greeting, what the bot can do, and some suggestions for how to interact.</span></span> <span data-ttu-id="4d5df-124">Например, "Попробуй спросить меня о ...".</span><span class="sxs-lookup"><span data-stu-id="4d5df-124">For example, “Try asking me about …”.</span></span> <span data-ttu-id="4d5df-125">По возможности эти предложения должны возвращать готовые ответы, чтобы пользователю не обязательно было входить в систему.</span><span class="sxs-lookup"><span data-stu-id="4d5df-125">If possible, these suggestions should return stored responses without having to sign in.</span></span>

:::image type="content" source="../../assets/images/bots/bot-personal-welcome.png" alt-text="В примере показано представление бота в личном приложении." border="false":::

### <a name="introductions-in-group-chats-and-channels"></a><span data-ttu-id="4d5df-127">Представление бота в групповых чатах и каналах</span><span class="sxs-lookup"><span data-stu-id="4d5df-127">Introductions in group chats and channels</span></span>

<span data-ttu-id="4d5df-128">Представление бота в групповых чатах и каналах должно немного отличаться от представления в личном контексте (например, в личном приложении).</span><span class="sxs-lookup"><span data-stu-id="4d5df-128">Your bot's introduction should be slightly different in group chats and channels compared to a personal context (like a personal app).</span></span> <span data-ttu-id="4d5df-129">В реальной жизни, войдя в комнату, заполненную людьми, вы бы не стали приветствовать тех, кто там уже находится; вместо этого вы бы представились.</span><span class="sxs-lookup"><span data-stu-id="4d5df-129">In real life, if you entered a room full of people; you’d introduce yourself instead of welcoming everyone who’s already there.</span></span> <span data-ttu-id="4d5df-130">То же самое надо воплотить в конструкции бота.</span><span class="sxs-lookup"><span data-stu-id="4d5df-130">Carry that thinking into your bot design.</span></span>

:::image type="content" source="../../assets/images/bots/bot-group-welcome.png" alt-text="В примере показано представление бота в контексте совместной работы." border="false":::

### <a name="bot-authentication-with-single-sign-on"></a><span data-ttu-id="4d5df-132">Проверка подлинности бота при едином входе</span><span class="sxs-lookup"><span data-stu-id="4d5df-132">Bot authentication with single sign-on</span></span>

<span data-ttu-id="4d5df-133">Когда человек посылает сообщение боту, для использования всех функций бота человеку может потребоваться войти в систему.</span><span class="sxs-lookup"><span data-stu-id="4d5df-133">When a person messages a bot, sign in may be required use all its features.</span></span> <span data-ttu-id="4d5df-134">Вы можете упростить процесс проверки подлинности, используя единый вход.</span><span class="sxs-lookup"><span data-stu-id="4d5df-134">You can simplify the authentication process using single sign-on (SSO).</span></span>

<span data-ttu-id="4d5df-135">Не забывайте: в командном меню бота (**Что я умею делать?**) необходимо также предоставить команду для выхода из системы.</span><span class="sxs-lookup"><span data-stu-id="4d5df-135">Don’t forget: In the bot command menu (**What can I do?**), you must also provide a command to sign out.</span></span>

:::image type="content" source="../../assets/images/bots/bot-sso-example.png" alt-text="В примере показан бот с кнопкой для входа в систему." border="false":::

### <a name="tours"></a><span data-ttu-id="4d5df-137">Обзоры</span><span class="sxs-lookup"><span data-stu-id="4d5df-137">Tours</span></span>

<span data-ttu-id="4d5df-138">Вы можете включить обзорное видео с приветствиями и указать, отвечает ли бот на что-нибудь вроде команды "справка".</span><span class="sxs-lookup"><span data-stu-id="4d5df-138">You can include a tour with welcome messages and if the bot responds to something like a “help” command.</span></span> <span data-ttu-id="4d5df-139">Обзор — самый эффективный способ описать, что может сделать бот.</span><span class="sxs-lookup"><span data-stu-id="4d5df-139">A tour is the most effective way to describe what your bot can do.</span></span> <span data-ttu-id="4d5df-140">Если это применимо, они также отлично под названием описывают другие функции вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="4d5df-140">If applicable, they’re also great for describing your app’s other features.</span></span> <span data-ttu-id="4d5df-141">Например, включите скриншоты расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="4d5df-141">For example, include screenshots of your messaging extension.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4d5df-142">Обзоры должны быть доступны пользователям без входа в систему.</span><span class="sxs-lookup"><span data-stu-id="4d5df-142">Tours should be accessible without having to sign in.</span></span>

#### <a name="one-on-one-chats"></a><span data-ttu-id="4d5df-143">Чаты один на один</span><span class="sxs-lookup"><span data-stu-id="4d5df-143">One-on-one chats</span></span>

<span data-ttu-id="4d5df-144">В личном приложении карусель может предоставить эффективный обзор бота и любых других функций приложения.</span><span class="sxs-lookup"><span data-stu-id="4d5df-144">In a personal app, a carousel can provide an effective overview of your bot and any other features of your app.</span></span> <span data-ttu-id="4d5df-145">Включая кнопки, которые позволяют пользователям пробовать команды ботов, рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="4d5df-145">Including buttons the let users try bot commands is encouraged.</span></span> <span data-ttu-id="4d5df-146">Например, **Создайте задачу.**</span><span class="sxs-lookup"><span data-stu-id="4d5df-146">For example, **Create a task**.</span></span>

:::image type="content" source="../../assets/images/bots/bot-tour-personal.png" alt-text="В примере показан видеообзор бота в чате с одним человеком." border="false":::

#### <a name="channels-and-group-chats"></a><span data-ttu-id="4d5df-148">Каналы и групповые чаты</span><span class="sxs-lookup"><span data-stu-id="4d5df-148">Channels and group chats</span></span>

<span data-ttu-id="4d5df-149">В каналах и групповых чатах видеообзор должен открываться в модальном режиме (также известном как [модуль задач](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) чтобы не прерывать текущие беседы.</span><span class="sxs-lookup"><span data-stu-id="4d5df-149">In channels and group chats, a tour should open in a modal (also known as a [task module](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) so it doesn’t interrupt ongoing conversations.</span></span> <span data-ttu-id="4d5df-150">Это также дает возможность реализовать в обзоре представления на основе ролей.</span><span class="sxs-lookup"><span data-stu-id="4d5df-150">This also gives you the option to implement role-based views for your tour.</span></span>

:::image type="content" source="../../assets/images/bots/bot-tour-channel.png" alt-text="В примере показан видеообзор бота в канале." border="false":::

## <a name="chat-with-a-bot"></a><span data-ttu-id="4d5df-152">Чат с ботом</span><span class="sxs-lookup"><span data-stu-id="4d5df-152">Chat with a bot</span></span>

<span data-ttu-id="4d5df-153">Боты интегрируются непосредственно в структуру обмена сообщениями Teams.</span><span class="sxs-lookup"><span data-stu-id="4d5df-153">Bots integrate directly into Team’s messaging framework.</span></span> <span data-ttu-id="4d5df-154">Пользователи могут общаться с ботом, чтобы получать ответы на свои вопросы, или вводить с клавиатуры команды, чтобы бот выполнял узкий или определенный набор задач.</span><span class="sxs-lookup"><span data-stu-id="4d5df-154">Users can chat with a bot to get their questions answered or type commands to have the bot perform a narrow or specific set of tasks.</span></span> <span data-ttu-id="4d5df-155">Боты могут заблаговременно уведомлять пользователей об изменениях или обновлениях приложения через чат.</span><span class="sxs-lookup"><span data-stu-id="4d5df-155">Bots can proactively notify users about changes or updates to your app via chat.</span></span>

### <a name="chat-with-a-bot-in-different-contexts"></a><span data-ttu-id="4d5df-156">Чат с ботом в разных контекстах</span><span class="sxs-lookup"><span data-stu-id="4d5df-156">Chat with a bot in different contexts</span></span>

<span data-ttu-id="4d5df-157">Ботов можно использовать в следующих контекстах:</span><span class="sxs-lookup"><span data-stu-id="4d5df-157">You can use bots in the following contexts:</span></span>

* <span data-ttu-id="4d5df-158">**Личные приложения**. В личном приложении у бота есть специальная вкладка чата.</span><span class="sxs-lookup"><span data-stu-id="4d5df-158">**Personal apps**: In a personal app, a bot has a dedicated chat tab.</span></span>
* <span data-ttu-id="4d5df-159">**Приватный чат**: пользователь может начать приватную беседу с ботом.</span><span class="sxs-lookup"><span data-stu-id="4d5df-159">**One-on-one chat**: A user can initiate a private conversation with a bot.</span></span> <span data-ttu-id="4d5df-160">Это то же самое, что и использование бота в личном приложении.</span><span class="sxs-lookup"><span data-stu-id="4d5df-160">It's the same experience as using a bot in a personal app.</span></span>
* <span data-ttu-id="4d5df-161">**Групповой чат**: люди могут взаимодействовать с ботом в групповом чате, @упоминая бота.</span><span class="sxs-lookup"><span data-stu-id="4d5df-161">**Group chat**: People can interact with a bot in a group chat by @mentioning the bot.</span></span>
* <span data-ttu-id="4d5df-162">**Канал**: люди могут взаимодействовать с ботом в канале.</span><span class="sxs-lookup"><span data-stu-id="4d5df-162">**Channel**: People can interact with a bot in a channel.</span></span> <span data-ttu-id="4d5df-163">@упоминанием имени бота в поле "Создать".</span><span class="sxs-lookup"><span data-stu-id="4d5df-163">by @mentioning the bot name in the compose box.</span></span> <span data-ttu-id="4d5df-164">Помните, что в этом контексте бот доступен всей группе, а не только каналу.</span><span class="sxs-lookup"><span data-stu-id="4d5df-164">Remember, in this context, the bot is available to the entire team, not just the channel.</span></span>

### <a name="anatomy"></a><span data-ttu-id="4d5df-165">Анатомия</span><span class="sxs-lookup"><span data-stu-id="4d5df-165">Anatomy</span></span>

:::image type="content" source="../../assets/images/bots/bot-anatomy.png" alt-text="В примере показана структурная анатомия бота." border="false":::

|<span data-ttu-id="4d5df-167">Счетчик</span><span class="sxs-lookup"><span data-stu-id="4d5df-167">Counter</span></span>|<span data-ttu-id="4d5df-168">Описание</span><span class="sxs-lookup"><span data-stu-id="4d5df-168">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="4d5df-169">1</span><span class="sxs-lookup"><span data-stu-id="4d5df-169">1</span></span>|<span data-ttu-id="4d5df-170">**Имя и значок приложения**</span><span class="sxs-lookup"><span data-stu-id="4d5df-170">**App name and icon**</span></span>|
|<span data-ttu-id="4d5df-171">2</span><span class="sxs-lookup"><span data-stu-id="4d5df-171">2</span></span>|<span data-ttu-id="4d5df-172">**Вкладка чата**: открывает пространство для общения с ботом (только для личных приложений).</span><span class="sxs-lookup"><span data-stu-id="4d5df-172">**Chat tab**: Opens the space to talk with your bot (applicable only to personal apps).</span></span>|
|<span data-ttu-id="4d5df-173">3</span><span class="sxs-lookup"><span data-stu-id="4d5df-173">3</span></span>|<span data-ttu-id="4d5df-174">**Настраиваемые вкладки**: открывает другое содержимое, связанное с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="4d5df-174">**Custom tabs**: Opens other content related to your app.</span></span>|
|<span data-ttu-id="4d5df-175">4 </span><span class="sxs-lookup"><span data-stu-id="4d5df-175">4</span></span>|<span data-ttu-id="4d5df-176">**Сведения**: выводит на экран основные сведения о приложении.</span><span class="sxs-lookup"><span data-stu-id="4d5df-176">**About tab**: Displays basic information about your app.</span></span>|
|<span data-ttu-id="4d5df-177">5 </span><span class="sxs-lookup"><span data-stu-id="4d5df-177">5</span></span>|<span data-ttu-id="4d5df-178">**Пузырек чата**: беседы ботов используют структуру обмена сообщениями Teams.</span><span class="sxs-lookup"><span data-stu-id="4d5df-178">**Chat bubble**: Bot conversations use the Teams messaging framework.</span></span>|
|<span data-ttu-id="4d5df-179">6 </span><span class="sxs-lookup"><span data-stu-id="4d5df-179">6</span></span>|<span data-ttu-id="4d5df-180">**Адаптивная карточка**: если ответы бота содержат адаптивные карточки, то карточка занимает всю ширину пузырька чата.</span><span class="sxs-lookup"><span data-stu-id="4d5df-180">**Adaptive Card**: If your bot’s responses include Adaptive Cards, the card takes up the full width of the chat bubble.</span></span>|
|<span data-ttu-id="4d5df-181">7 </span><span class="sxs-lookup"><span data-stu-id="4d5df-181">7</span></span>|<span data-ttu-id="4d5df-182">**Меню команд**: отображает стандартные команды бота (определенные вами).</span><span class="sxs-lookup"><span data-stu-id="4d5df-182">**Command menu**: Displays your bot's standard commands (defined by you).</span></span>

### <a name="command-menu"></a><span data-ttu-id="4d5df-183">Меню команд</span><span class="sxs-lookup"><span data-stu-id="4d5df-183">Command menu</span></span>

<span data-ttu-id="4d5df-184">В командном меню содержится список слов или фраз, на которые бот должен отвечать всегда.</span><span class="sxs-lookup"><span data-stu-id="4d5df-184">The command menu provides a list of words or phrases you want your bot to always respond to.</span></span> <span data-ttu-id="4d5df-185">Меню команд отображается над полем "Создать", когда кто-нибудь беседует с ботом.</span><span class="sxs-lookup"><span data-stu-id="4d5df-185">The command menu displays above the compose box when someone is conversing with a bot.</span></span> <span data-ttu-id="4d5df-186">При выборе команды она вставляется в сообщение.</span><span class="sxs-lookup"><span data-stu-id="4d5df-186">When a command is selected, it gets inserted into a message.</span></span>

<span data-ttu-id="4d5df-187">Список команд должен быть кратким.</span><span class="sxs-lookup"><span data-stu-id="4d5df-187">The list of commands should be brief.</span></span> <span data-ttu-id="4d5df-188">Меню предназначено только для выделения основных функций бота.</span><span class="sxs-lookup"><span data-stu-id="4d5df-188">The menu is only meant to highlight your bot’s primary features.</span></span> <span data-ttu-id="4d5df-189">Команды также должны быть краткими.</span><span class="sxs-lookup"><span data-stu-id="4d5df-189">Keep commands concise, too.</span></span> <span data-ttu-id="4d5df-190">Например, создайте команду **Помоги** вместо **Вы бы не могли мне помочь?**</span><span class="sxs-lookup"><span data-stu-id="4d5df-190">For example, create a command called **Help** instead of **Can you please help me**?</span></span>
<span data-ttu-id="4d5df-191">Меню команд должно всегда быть доступно независимо от состояния беседы.</span><span class="sxs-lookup"><span data-stu-id="4d5df-191">The command menu must always be available regardless of the state of the conversation.</span></span>

:::image type="content" source="../../assets/images/bots/bot-command-menu.png" alt-text="В примере показано меню команд бота." border="false":::

## <a name="understand-what-people-are-saying"></a><span data-ttu-id="4d5df-193">Понимание того, что говорят люди</span><span class="sxs-lookup"><span data-stu-id="4d5df-193">Understand what people are saying</span></span>

<span data-ttu-id="4d5df-194">Используйте толковый словарь и попросите людей из разных слоев общества и с разным уровнем образования (столько, сколько удастся найти), чтобы помочь вам выработать различные интерпретации стандартных запросов.</span><span class="sxs-lookup"><span data-stu-id="4d5df-194">Use a thesaurus and get people from as many different backgrounds as possible to help you generate different interpretations of standard queries.</span></span>

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

### <a name="extract-intent-and-data-from-messages"></a><span data-ttu-id="4d5df-198">Извлечение намерения и данных из сообщений</span><span class="sxs-lookup"><span data-stu-id="4d5df-198">Extract intent and data from messages</span></span>

<span data-ttu-id="4d5df-199">Разрабатывайте бот так, чтобы он умел понимать намерения, то есть понимать, чего хочет пользователь от бота в ответ на сообщение или запрос.</span><span class="sxs-lookup"><span data-stu-id="4d5df-199">Design your bot to recognize intent, which captures what someone wants from a bot in response to a message or query.</span></span> <span data-ttu-id="4d5df-200">Цель классифицирует сообщение или запрос как одно действие с одним или более объектами данных, на которые влияет это действие.</span><span class="sxs-lookup"><span data-stu-id="4d5df-200">Intent classifies a message or query as a single action with one or more data objects that are affected by the action.</span></span> 

<span data-ttu-id="4d5df-201">В следующих примерах излагаются намерения пользователей и данные в сообщениях, отправленных ботам:</span><span class="sxs-lookup"><span data-stu-id="4d5df-201">The following examples outline the user intent and data in messages sent to bots:</span></span>

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

### <a name="analyze-and-improve"></a><span data-ttu-id="4d5df-205">Анализируйте и совершенствуйте</span><span class="sxs-lookup"><span data-stu-id="4d5df-205">Analyze and improve</span></span>

<span data-ttu-id="4d5df-206">Узнавайте, что говорят пользователи при чате с ботом.</span><span class="sxs-lookup"><span data-stu-id="4d5df-206">Learn what users say when chatting with your bot.</span></span> <span data-ttu-id="4d5df-207">Это будет непрерывный итеративный процесс по мере роста пользовательской базы в разных расположениях и организациях.</span><span class="sxs-lookup"><span data-stu-id="4d5df-207">This will be an ongoing, iterative process as your user base grows in different locations and orgs.</span></span> <span data-ttu-id="4d5df-208">Оттачивать умение бота распознавать язык и намерения можно с помощью Microsoft Language Understanding (LUIS).</span><span class="sxs-lookup"><span data-stu-id="4d5df-208">You can tune your bot's language recognition and intent mapping with Microsoft Language Understanding (LUIS).</span></span>

* <span data-ttu-id="4d5df-209">[Понимание LUIS](/azure/cognitive-services/luis/artificial-intelligence). Узнайте, как LUIS использует ИИ для понимания естественного языка (NLU), чтобы оперировать данными приложения.</span><span class="sxs-lookup"><span data-stu-id="4d5df-209">[Understanding LUIS](/azure/cognitive-services/luis/artificial-intelligence): Find out how LUIS uses AI to provide natural language understanding (NLU) to your app data.</span></span>
* <span data-ttu-id="4d5df-210">[Интеграция с LUIS](https://www.luis.ai/). Вы можете добавлять боту возможности естественного языка, не создавая сложных моделей машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="4d5df-210">[Integrating with LUIS](https://www.luis.ai/): Add natural language capabilities to your bot without the complex process of creating machine learning models.</span></span>

## <a name="use-cases"></a><span data-ttu-id="4d5df-211">Варианты использования</span><span class="sxs-lookup"><span data-stu-id="4d5df-211">Use cases</span></span>

### <a name="simple-queries"></a><span data-ttu-id="4d5df-212">Простые запросы</span><span class="sxs-lookup"><span data-stu-id="4d5df-212">Simple queries</span></span>

<span data-ttu-id="4d5df-213">Боты могут доставлять точное соответствие запросу или группе родственных соответствий, чтобы устранить двойственность.</span><span class="sxs-lookup"><span data-stu-id="4d5df-213">Bots can deliver an exact match to a query or a group of related matches to help with disambiguation.</span></span> <span data-ttu-id="4d5df-214">Для получения родственных соответствий группируйте содержимое с помощью карточки списка.</span><span class="sxs-lookup"><span data-stu-id="4d5df-214">For related matches, group the content using a list card.</span></span>

:::image type="content" source="../../assets/images/bots/bot-simple-query.png" alt-text="В примере показано взаимодействие с ботом для выполнения простого запроса." border="false":::

### <a name="multi-turn-interactions"></a><span data-ttu-id="4d5df-216">Взаимодействие с несколькими поворотами</span><span class="sxs-lookup"><span data-stu-id="4d5df-216">Multi-turn interactions</span></span>

<span data-ttu-id="4d5df-217">Бот может поддерживать выполнение запросов и отвечать вопросы, но он также должен уметь обрабатывать взаимодействия с несколькими поворотами.</span><span class="sxs-lookup"><span data-stu-id="4d5df-217">While your bot can support complete requests and questions, it should also be able to handle multi-turn interactions.</span></span> <span data-ttu-id="4d5df-218">Если бот предугадывает возможные дальнейшие действия пользователя, людям будет намного проще выполнить задание. Для них это легче, чем сразу составить сложный запрос.</span><span class="sxs-lookup"><span data-stu-id="4d5df-218">Anticipating possible next steps makes it much easier for people to a complete task flow (rather than expecting them to craft a comprehensive request).</span></span>

<span data-ttu-id="4d5df-219">В следующем примере бот отвечает на каждое сообщение вариантами того, что может захотеть сделать дальше:</span><span class="sxs-lookup"><span data-stu-id="4d5df-219">In the following example, the bot responds to each message with options for what might want to do next:</span></span>

:::image type="content" source="../../assets/images/bots/bot-multi-turn.png" alt-text="В примере показано взаимодействие с ботом с несколькими поворотами." border="false":::

### <a name="reach-out-to-users"></a><span data-ttu-id="4d5df-221">Инициируйте общение с пользователями</span><span class="sxs-lookup"><span data-stu-id="4d5df-221">Reach out to users</span></span>

<span data-ttu-id="4d5df-222">С помощью проактивных сообщений бот может действовать как дайджест, который с определенной периодичностью отправляет уведомления, актуальные для отдельного лица, группового чата или канала.</span><span class="sxs-lookup"><span data-stu-id="4d5df-222">With proactive messaging, your bot can act like a digest that sends notifications relevant to an individual, group chat, or channel at a specific frequency.</span></span> <span data-ttu-id="4d5df-223">Бот может отправить сообщение, если что-то изменилось в документе или когда завершено рабочее задание.</span><span class="sxs-lookup"><span data-stu-id="4d5df-223">A bot may send a message when something has changed in a document or a work item is closed.</span></span>

<span data-ttu-id="4d5df-224">В следующем примере пользователь получает уведомление о всплывающих уведомлениях о том, что бот отправил им сообщение в другом канале:</span><span class="sxs-lookup"><span data-stu-id="4d5df-224">In the following example, a user gets a toast notification that a bot messaged them in another channel:</span></span>

:::image type="content" source="../../assets/images/bots/bot-proactive-message-toast.png" alt-text="В примере показано всплывающее уведомление бота, который проактивно посылает сообщение пользователю из другого канала." border="false":::

<span data-ttu-id="4d5df-226">Теперь в этом канале пользователь может прочитать свое сообщение от бота.</span><span class="sxs-lookup"><span data-stu-id="4d5df-226">Now in that channel, the user can read their message from the bot.</span></span>

:::image type="content" source="../../assets/images/bots/bot-proactive-message.png" alt-text="В примере показано, как пользователь смотрит на проактивные сообщения бота." border="false":::

### <a name="use-tabs-with-bots"></a><span data-ttu-id="4d5df-228">Использование вкладок с ботами</span><span class="sxs-lookup"><span data-stu-id="4d5df-228">Use tabs with bots</span></span>

<span data-ttu-id="4d5df-229">Вкладка упрощает работу с ботом.</span><span class="sxs-lookup"><span data-stu-id="4d5df-229">A tab can make your bot easier to use.</span></span> <span data-ttu-id="4d5df-230">Например, если ваш бот может создавать рабочие элементы, было бы неплохо показать все эти элементы в центральном месте внутри вкладки. Для получения дополнительной информации [можно посмотреть вкладки проектирования.](../../tabs/design/tabs.md)</span><span class="sxs-lookup"><span data-stu-id="4d5df-230">For example, if your bot can create work items, it would be nice to show all those items in a central location inside a tab. For more information, See [designing tabs](../../tabs/design/tabs.md).</span></span>

:::image type="content" source="../../assets/images/bots/bot-with-tab.png" alt-text="В примере показано, как вкладка помогает упорядочизировать содержимое бота." border="false":::

## <a name="manage-a-bot"></a><span data-ttu-id="4d5df-232">Управление ботом</span><span class="sxs-lookup"><span data-stu-id="4d5df-232">Manage a bot</span></span>

<span data-ttu-id="4d5df-233">Пользователи должны иметь возможность менять настройки бота.</span><span class="sxs-lookup"><span data-stu-id="4d5df-233">Users should be able to change a bot's settings.</span></span> <span data-ttu-id="4d5df-234">Эту функцию можно предоставить с помощью команд бота, но обычно эффективнее включать все параметры в [модуль задач](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) (как показано в следующем примере).</span><span class="sxs-lookup"><span data-stu-id="4d5df-234">You can provide this functionality with bot commands, but it's usually more efficient to include all settings in a [task module](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) (as shown in the following example).</span></span>

:::image type="content" source="../../assets/images/bots/manage-bot-task-module.png" alt-text="В примере показан модуль задач для настройки параметров бота." border="false":::

## <a name="best-practices"></a><span data-ttu-id="4d5df-236">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="4d5df-236">Best practices</span></span>

<span data-ttu-id="4d5df-237">Используйте эти рекомендации для создания качественного приложения.</span><span class="sxs-lookup"><span data-stu-id="4d5df-237">Use these recommendations to create a quality app experience.</span></span>

### <a name="content"></a><span data-ttu-id="4d5df-238">Статья</span><span class="sxs-lookup"><span data-stu-id="4d5df-238">Content</span></span>

:::image type="content" source="../../assets/images/bots/bot-content-persona-do.png" alt-text="Пример, показывающий бота наилучшей практики для создания четкой персоной." border="false":::

#### <a name="do-establish-a-clear-persona"></a><span data-ttu-id="4d5df-240">Как надо: создать отчетливо выраженную личность</span><span class="sxs-lookup"><span data-stu-id="4d5df-240">Do: Establish a clear persona</span></span>

<span data-ttu-id="4d5df-241">Как держится ваш бот? Разговаривает двружелюбно и легко? Сухо излагает факты? А может, он со странностями?</span><span class="sxs-lookup"><span data-stu-id="4d5df-241">Is your bot's tone friendly and light, “just the facts”, or super quirky?</span></span> <span data-ttu-id="4d5df-242">Как он должен реагировать в различных сценариях?</span><span class="sxs-lookup"><span data-stu-id="4d5df-242">How should it respond in different scenarios?</span></span> <span data-ttu-id="4d5df-243">Если вы заранее продумаете и документируете личность бота, вам будет проще написать для него ответы, звучащие естественно и связно.</span><span class="sxs-lookup"><span data-stu-id="4d5df-243">Planning and documenting your bot's persona makes it easier to write responses that seem natural and cohesive.</span></span>

<span data-ttu-id="4d5df-244">Узнайте больше о написании ботов в статье <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">Комплект разработчика пользовательских интерфейсов Microsoft Teams (Figma).</a></span><span class="sxs-lookup"><span data-stu-id="4d5df-244">See more about writing for bots in the <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">Microsoft Teams UI Kit (Figma).</a></span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-convey-do.png" alt-text="Пример, показывающий, чтобы четко передать, что ваш бот может сделать." border="false":::

#### <a name="do-clearly-convey-what-your-bot-can-do"></a><span data-ttu-id="4d5df-246">Как надо: четко обозначьте, что умеет делать ваш бот</span><span class="sxs-lookup"><span data-stu-id="4d5df-246">Do: Clearly convey what your bot can do</span></span>

<span data-ttu-id="4d5df-247">Приветствия и обзоры помогают пользователям понять, что они могут делать с вашим ботом.</span><span class="sxs-lookup"><span data-stu-id="4d5df-247">Welcome messages and tours help people understand what they can do with your bot.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-convey-dont.png" alt-text="Пример, показывающий, чтобы не скрывать особенности вашего бота." border="false":::

#### <a name="dont-obscure-your-bots-features"></a><span data-ttu-id="4d5df-249">Как не надо: скрывать функции бота</span><span class="sxs-lookup"><span data-stu-id="4d5df-249">Don't: Obscure your bot's features</span></span>

<span data-ttu-id="4d5df-250">Первые впечатления очень важны.</span><span class="sxs-lookup"><span data-stu-id="4d5df-250">First impressions matter.</span></span> <span data-ttu-id="4d5df-251">Увидев ничего не говорящее сообщение о входе, люди, скорее всего, растеряются или заподозрят неладное.</span><span class="sxs-lookup"><span data-stu-id="4d5df-251">People will likely be confused or suspicious when presented with a nondescript sign-in message.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-understand-do.png" alt-text="Пример, показывающий, что ваш бот должен распознавать не вопросы." border="false":::

#### <a name="do-recognize-non-questions"></a><span data-ttu-id="4d5df-253">Как надо: распознавать вопросы, которые не являются вопросами</span><span class="sxs-lookup"><span data-stu-id="4d5df-253">Do: Recognize non-questions</span></span>

<span data-ttu-id="4d5df-254">Бот должен уметь отвечать на такие сообщения, как "Привет", "Помоги" и "Спасибо", а также вносить поправки на распространенные опечатки и разговорные выражения.</span><span class="sxs-lookup"><span data-stu-id="4d5df-254">Your bot should be able to respond to messages like "Hi", "Help", and "Thanks" while also accounting for common misspellings and colloquialisms.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-understand-dont.png" alt-text="Пример, показывающий, что следует избегать неуклюжих ответов на простые сообщения бота." border="false":::

#### <a name="dont-miss-out-on-opportunities-to-delight"></a><span data-ttu-id="4d5df-256">Как не надо: не упускайте случая порадовать пользователей</span><span class="sxs-lookup"><span data-stu-id="4d5df-256">Don't: Miss out on opportunities to delight</span></span>

<span data-ttu-id="4d5df-257">Некоторые люди ожидают, что беседы с ботом будут идти естественно, совсем как с живым человеком.</span><span class="sxs-lookup"><span data-stu-id="4d5df-257">Some people expect conversations to flow naturally like they would with a real person.</span></span> <span data-ttu-id="4d5df-258">Постарайтесь избежать неуклюжих ответов на простые сообщения.</span><span class="sxs-lookup"><span data-stu-id="4d5df-258">Try to avoid clumsy responses to simple messages.</span></span>

   :::column-end:::
:::row-end:::

### <a name="troubleshooting"></a><span data-ttu-id="4d5df-259">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="4d5df-259">Troubleshooting</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-help-do.png" alt-text="Пример, показывающий ботов, должен помочь пользователям понять, как использовать ботов." border="false":::

#### <a name="do-provide-help"></a><span data-ttu-id="4d5df-261">Как надо: предоставляйте помощь</span><span class="sxs-lookup"><span data-stu-id="4d5df-261">Do: Provide help</span></span>

<span data-ttu-id="4d5df-262">Если ваш бот не может выполнить запрос, дайте пользователю возможность научиться взаимодействию с ботом.</span><span class="sxs-lookup"><span data-stu-id="4d5df-262">If your bot can’t satisfy a request, provide ways for a user to educate themselves about interacting with your bot.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-help-dont.png" alt-text="Пример, показывающий ваш бот не должен прядь пользователей." border="false":::

#### <a name="dont-leave-users-stranded"></a><span data-ttu-id="4d5df-264">Как не надо: не бросайте пользователей в беде</span><span class="sxs-lookup"><span data-stu-id="4d5df-264">Don't: Leave users stranded</span></span>

<span data-ttu-id="4d5df-265">Люди быстро перестанут общаться с ботом, если не смогут устранить его неполадки.</span><span class="sxs-lookup"><span data-stu-id="4d5df-265">People will quickly abandon your bot if they can’t troubleshoot issues.</span></span>

   :::column-end:::
:::row-end:::

### <a name="complex-interactions"></a><span data-ttu-id="4d5df-266">Сложные взаимодействия</span><span class="sxs-lookup"><span data-stu-id="4d5df-266">Complex interactions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-interactions-do.png" alt-text="Пример, показывающий, что вы можете использовать модули задач или вкладки с ботом для сложных взаимодействий." border="false":::

#### <a name="do-use-task-modules-or-tabs"></a><span data-ttu-id="4d5df-268">Как надо: используйте модули задач или вкладки</span><span class="sxs-lookup"><span data-stu-id="4d5df-268">Do: Use task modules or tabs</span></span>

<span data-ttu-id="4d5df-269">Если бот предоставляет ответ, требующий выполнения еще нескольких действий, вы можете для завершения действия или последовательности действий предоставить ссылку на модуль задач или вкладку.</span><span class="sxs-lookup"><span data-stu-id="4d5df-269">If your bot provides an answer that requires a few more steps, you can link to a task module or tab to complete the task or flow.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-interactions-dont.png" alt-text="Пример, показывающий, как ваш бот должен избегать многоступенчатых взаимодействий." border="false":::

#### <a name="dont-make-multi-turn-interactions-tedious"></a><span data-ttu-id="4d5df-271">Как не надо: не делайте взаимодействие с несколькими поворотами утомительными</span><span class="sxs-lookup"><span data-stu-id="4d5df-271">Don't: Make multi-turn interactions tedious</span></span>

<span data-ttu-id="4d5df-272">Если пользователю для выполнения одной задачи приходится вести пространные беседы, это слишком долго и сложно.</span><span class="sxs-lookup"><span data-stu-id="4d5df-272">An extensive conversation to complete a single task is slow and overly complex.</span></span> <span data-ttu-id="4d5df-273">Кроме того, разработчик должен учитывать изменения состояния (например, когда время беседы истекло или пользователь отправил сообщение "Отмена").</span><span class="sxs-lookup"><span data-stu-id="4d5df-273">It also requires the developer to account for state changes (such as the conversation timing out or you sending a “Cancel” message).</span></span>

   :::column-end:::
:::row-end:::

### <a name="privacy"></a><span data-ttu-id="4d5df-274">Конфиденциальность</span><span class="sxs-lookup"><span data-stu-id="4d5df-274">Privacy</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-privacy-do.png" alt-text="Пример, показывающий, как боты должны показывать личную информацию только в личном контексте." border="false":::

#### <a name="do-only-show-sensitive-info-in-a-personal-context"></a><span data-ttu-id="4d5df-276">Как надо: показывать конфиденциальную информацию только в личном контексте</span><span class="sxs-lookup"><span data-stu-id="4d5df-276">Do: Only show sensitive info in a personal context</span></span>

<span data-ttu-id="4d5df-277">Если бот находится в групповом чате или канале, для просмотра конфиденциальной информации рекомендуется направлять пользователей в приватное расположение (например, модуль задач, вкладку или браузер).</span><span class="sxs-lookup"><span data-stu-id="4d5df-277">If your bot is in a group chat or channel, we recommend directing users to a private location (such as a task module, tab, or browser) to view sensitive information.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-privacy-dont.png" alt-text="Пример, показывающий, как боты не должны раскрывать конфиденциальную информацию группе или людям." border="false":::

#### <a name="dont-some-content-isnt-meant-to-be-seen-by-everyone"></a><span data-ttu-id="4d5df-279">Как не надо: некоторые данные предназначены не для всех</span><span class="sxs-lookup"><span data-stu-id="4d5df-279">Don't: Some content isn’t meant to be seen by everyone</span></span>

<span data-ttu-id="4d5df-280">Бот не должен раскрывать конфиденциальную информацию группе людей.</span><span class="sxs-lookup"><span data-stu-id="4d5df-280">Your bot shouldn’t reveal sensitive information to a group of people.</span></span>

   :::column-end:::
:::row-end:::

## <a name="see-also"></a><span data-ttu-id="4d5df-281">См. также</span><span class="sxs-lookup"><span data-stu-id="4d5df-281">See also</span></span>

<span data-ttu-id="4d5df-282">Вот еще рекомендации, которые могут быть полезными при разработке бота:</span><span class="sxs-lookup"><span data-stu-id="4d5df-282">These other guidelines may help with your bot design:</span></span>

* [<span data-ttu-id="4d5df-283">Проектирование личного приложения</span><span class="sxs-lookup"><span data-stu-id="4d5df-283">Designing your personal app</span></span>](../../concepts/design/personal-apps.md)
* [<span data-ttu-id="4d5df-284">Проектирование адаптивной карточки</span><span class="sxs-lookup"><span data-stu-id="4d5df-284">Designing Adaptive Cards</span></span>](../../task-modules-and-cards/cards/design-effective-cards.md)
* [<span data-ttu-id="4d5df-285">Проектирование модулей задач</span><span class="sxs-lookup"><span data-stu-id="4d5df-285">Designing task modules</span></span>](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)
