---
title: Разработка ленты
description: Узнайте, как разработать робот команд и получить набор UI Microsoft Teams.
author: heath-hamilton
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: d1a7470f4986de22ecca7071823b620cb0234abb
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/09/2020
ms.locfileid: "49605495"
---
# <a name="designing-your-microsoft-teams-bot"></a><span data-ttu-id="4cc72-103">Разработка ленты Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="4cc72-103">Designing your Microsoft Teams bot</span></span>

<span data-ttu-id="4cc72-104">Боты — это беседы, которые выполняют определенный набор задач.</span><span class="sxs-lookup"><span data-stu-id="4cc72-104">Bots are conversational apps that perform a specific set of tasks.</span></span> <span data-ttu-id="4cc72-105">С учетом <a href="https://dev.botframework.com/" target="_blank">Microsoft Bot Framework</a>, Боты общаться с пользователями, отвечать на свои вопросы и заблаговременно уведомлять об изменениях и событиях.</span><span class="sxs-lookup"><span data-stu-id="4cc72-105">Based on the <a href="https://dev.botframework.com/" target="_blank">Microsoft Bot Framework</a>, bots communicate with users, respond to their questions, and proactively notify them about changes and other events.</span></span> <span data-ttu-id="4cc72-106">Это отличный способ достигать.</span><span class="sxs-lookup"><span data-stu-id="4cc72-106">They're a great way to reach out.</span></span>

<span data-ttu-id="4cc72-107">В следующей статье описываются способы добавления, использования и управления боты в Teams, а также сведения по разработке приложений.</span><span class="sxs-lookup"><span data-stu-id="4cc72-107">To guide your app design, the following information describes and illustrates how people can add, use, and manage bots in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="4cc72-108">Набор элементов пользовательского интерфейса Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="4cc72-108">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="4cc72-109">В наборе UI Microsoft Teams вы найдете более исчерпывающие инструкции для Bot, в том числе элементы, которые можно изменять и изменять по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="4cc72-109">You can find more comprehensive bot design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4cc72-110">Получение набора элементов пользовательского интерфейса Microsoft Teams (фигма)</span><span class="sxs-lookup"><span data-stu-id="4cc72-110">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-bot"></a><span data-ttu-id="4cc72-111">Добавление ленты</span><span class="sxs-lookup"><span data-stu-id="4cc72-111">Add a bot</span></span>

<span data-ttu-id="4cc72-112">Боты доступны в беседах, каналах и персональных приложениях.</span><span class="sxs-lookup"><span data-stu-id="4cc72-112">Bots are available in chats, channels, and personal apps.</span></span> <span data-ttu-id="4cc72-113">Вы можете добавить элемент Bot одним из следующих способов:</span><span class="sxs-lookup"><span data-stu-id="4cc72-113">You can add a bot one of the following ways:</span></span>

* <span data-ttu-id="4cc72-114">Из хранилища Teams (AppSource).</span><span class="sxs-lookup"><span data-stu-id="4cc72-114">From the Teams store (AppSource).</span></span>
* <span data-ttu-id="4cc72-115">С помощью всплывающего меню приложения выберите значок **больше** в левой части Teams.</span><span class="sxs-lookup"><span data-stu-id="4cc72-115">Using the app flyout by selecting the **More** icon on the left side of Teams.</span></span>
* <span data-ttu-id="4cc72-116">С @mention в новом поле чата или создания (в приведенном ниже примере показано, как это можно сделать в разделе групповой чат).</span><span class="sxs-lookup"><span data-stu-id="4cc72-116">With an @mention in the new chat or compose box (the following example shows how you can do this in a group chat).</span></span>

:::image type="content" source="../../assets/images/bots/add-bot-chat-at-mention.png" alt-text="В примере показано, как добавить Bot в чат группы с помощью @mention." border="false":::

## <a name="introduce-a-bot"></a><span data-ttu-id="4cc72-118">Введение ленты</span><span class="sxs-lookup"><span data-stu-id="4cc72-118">Introduce a bot</span></span>

<span data-ttu-id="4cc72-119">Крайне важно, чтобы ваш робот появилось в самом коде, и описывает его возможности.</span><span class="sxs-lookup"><span data-stu-id="4cc72-119">It’s critical that your bot introduces itself and describes what it can do.</span></span> <span data-ttu-id="4cc72-120">Этот первоначальный сервер Exchange помогает людям разобраться, что делать с роботом, узнать об его ограничениях и, что самое важное, получить удобное взаимодействие с ИТ.</span><span class="sxs-lookup"><span data-stu-id="4cc72-120">This initial exchange helps people understand what to do with the bot, find out its limitations and, most importantly, get comfortable interacting with it.</span></span>

### <a name="welcome-message-in-a-one-on-one-chat"></a><span data-ttu-id="4cc72-121">Приветственное сообщение в беседе "один к одному"</span><span class="sxs-lookup"><span data-stu-id="4cc72-121">Welcome message in a one-on-one chat</span></span>

<span data-ttu-id="4cc72-122">В личных контекстах приветственные сообщения задают тон для Bot.</span><span class="sxs-lookup"><span data-stu-id="4cc72-122">In personal contexts, welcome messages set your bot's tone.</span></span> <span data-ttu-id="4cc72-123">Сообщение включает приветствие, действия, которые может выполнять Bot, и некоторые предложения по взаимодействию (например, "попытаться запрашивать о...").</span><span class="sxs-lookup"><span data-stu-id="4cc72-123">The message includes a greeting, what the bot can do, and some suggestions for how to interact (for example, “Try asking me about …”).</span></span> <span data-ttu-id="4cc72-124">Если это возможно, эти предложения должны возвращать сохраненные ответы, не входя в систему.</span><span class="sxs-lookup"><span data-stu-id="4cc72-124">If possible, these suggestions should return stored responses without having to sign in.</span></span>

:::image type="content" source="../../assets/images/bots/bot-personal-welcome.png" alt-text="В примере показано введение в личное приложение." border="false":::

### <a name="introductions-in-group-chats-and-channels"></a><span data-ttu-id="4cc72-126">Введение в групповых беседах и каналах</span><span class="sxs-lookup"><span data-stu-id="4cc72-126">Introductions in group chats and channels</span></span>

<span data-ttu-id="4cc72-127">Введение в групповые беседы и каналы в сравнении с персональным контекстом (например, личное приложение) должно быть немного отличаться.</span><span class="sxs-lookup"><span data-stu-id="4cc72-127">Your bot's introduction should be slightly little different in group chats and channels compared to a personal context (like a personal app).</span></span> <span data-ttu-id="4cc72-128">В реальной жизни, если вы ввели комнату, заполненную пользователями; Вы не велкоминг всех пользователей, которые уже есть.</span><span class="sxs-lookup"><span data-stu-id="4cc72-128">In real life, if you entered a room full of people; you’d introduce yourself instead of welcoming everyone who’s already there.</span></span> <span data-ttu-id="4cc72-129">Подумаем, что вы подумываете в своем botном дизайне.</span><span class="sxs-lookup"><span data-stu-id="4cc72-129">Carry that thinking into your bot design.</span></span>

:::image type="content" source="../../assets/images/bots/bot-group-welcome.png" alt-text="В примере показано введение в контексте для коллективной работы." border="false":::

### <a name="bot-authentication-with-single-sign-on"></a><span data-ttu-id="4cc72-131">Однократная проверка подлинности с единым входом</span><span class="sxs-lookup"><span data-stu-id="4cc72-131">Bot authentication with single sign-on</span></span>

<span data-ttu-id="4cc72-132">Когда пользователь почтовы почтовых роботов, для входа может потребоваться использовать все его функции.</span><span class="sxs-lookup"><span data-stu-id="4cc72-132">When a person messages a bot, sign in may be required use all its features.</span></span> <span data-ttu-id="4cc72-133">Вы можете упростить процесс проверки подлинности с помощью единого входа (SSO).</span><span class="sxs-lookup"><span data-stu-id="4cc72-133">You can simplify the authentication process using single sign-on (SSO).</span></span>

<span data-ttu-id="4cc72-134">Не забывайте: в меню команд Bot (**что можно делать?**) также необходимо указать команду для выхода.</span><span class="sxs-lookup"><span data-stu-id="4cc72-134">Don’t forget: In the bot command menu (**What can I do?**), you must also provide a command to sign out.</span></span>

:::image type="content" source="../../assets/images/bots/bot-sso-example.png" alt-text="Пример: Bot с кнопкой входа." border="false":::

### <a name="tours"></a><span data-ttu-id="4cc72-136">Обзоры</span><span class="sxs-lookup"><span data-stu-id="4cc72-136">Tours</span></span>

<span data-ttu-id="4cc72-137">Вы можете включить учебник с приветственными сообщениями и, если она отвечает на что-то вроде команды "Справка".</span><span class="sxs-lookup"><span data-stu-id="4cc72-137">You can include a tour with welcome messages and if the bot responds to something like a “help” command.</span></span> <span data-ttu-id="4cc72-138">Обзор — это наиболее эффективный способ описать действия, которые может выполнять Bot.</span><span class="sxs-lookup"><span data-stu-id="4cc72-138">A tour is the most effective way to describe what your bot can do.</span></span> <span data-ttu-id="4cc72-139">Если это возможно, они также прекрасно подходят для описания других функций приложения (например, для включения снимков экрана расширения обмена сообщениями).</span><span class="sxs-lookup"><span data-stu-id="4cc72-139">If applicable, they’re also great for describing your app’s other features (for example, include screenshots of your messaging extension).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4cc72-140">Обзоры должны быть доступны без входа в систему.</span><span class="sxs-lookup"><span data-stu-id="4cc72-140">Tours should be accessible without having to sign in.</span></span>

#### <a name="one-on-one-chats"></a><span data-ttu-id="4cc72-141">Беседы "один к одному"</span><span class="sxs-lookup"><span data-stu-id="4cc72-141">One-on-one chats</span></span>

<span data-ttu-id="4cc72-142">В персональном приложении обойма может быть эффективным обзором ленты и другими функциями приложения.</span><span class="sxs-lookup"><span data-stu-id="4cc72-142">In a personal app, a carousel can provide an effective overview of your bot and any other features of your app.</span></span> <span data-ttu-id="4cc72-143">В том числе кнопки Разрешить пользователям попытаться выполнить команды Bot (например, **создать задачу**).</span><span class="sxs-lookup"><span data-stu-id="4cc72-143">Including buttons the let users try bot commands is encouraged (for example, **Create a task**).</span></span>

:::image type="content" source="../../assets/images/bots/bot-tour-personal.png" alt-text="В примере показан обзор ленты в одном сеансе." border="false":::

#### <a name="channels-and-group-chats"></a><span data-ttu-id="4cc72-145">Каналы и беседы групп</span><span class="sxs-lookup"><span data-stu-id="4cc72-145">Channels and group chats</span></span>

<span data-ttu-id="4cc72-146">В каналах и беседах групп обзор должен быть открыт в модальном (также называемом [модуле задачи](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) ), чтобы не прерывать текущие беседы.</span><span class="sxs-lookup"><span data-stu-id="4cc72-146">In channels and group chats, a tour should open in a modal (also known as a [task module](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) so it doesn’t interrupt ongoing conversations.</span></span> <span data-ttu-id="4cc72-147">Это также дает возможность реализовать представления, основанные на ролях, для обзора.</span><span class="sxs-lookup"><span data-stu-id="4cc72-147">This also gives you the option to implement role-based views for your tour.</span></span>

:::image type="content" source="../../assets/images/bots/bot-tour-channel.png" alt-text="В примере показан обзор канала." border="false":::

## <a name="chat-with-a-bot"></a><span data-ttu-id="4cc72-149">Чат с Bot</span><span class="sxs-lookup"><span data-stu-id="4cc72-149">Chat with a bot</span></span>

<span data-ttu-id="4cc72-150">Боты интегрируются непосредственно в среду обмена сообщениями группы.</span><span class="sxs-lookup"><span data-stu-id="4cc72-150">Bots integrate directly into Team’s messaging framework.</span></span> <span data-ttu-id="4cc72-151">Пользователи могут обмениваться сообщениями с помощью программы Bot, чтобы получить ответы на свои вопросы или команды ввода, чтобы они могли выполнять задачи с узким или определенным набором задач.</span><span class="sxs-lookup"><span data-stu-id="4cc72-151">Users can chat with a bot to get their questions answered or type commands to have the bot perform a narrow or specific set of tasks.</span></span> <span data-ttu-id="4cc72-152">Боты может заблаговременно уведомлять пользователей об изменениях и обновлениях приложения с помощью чата.</span><span class="sxs-lookup"><span data-stu-id="4cc72-152">Bots can proactively notify users about changes or updates to your app via chat.</span></span>

### <a name="chat-with-a-bot-in-different-contexts"></a><span data-ttu-id="4cc72-153">Чат с помощью программы Bot в различных контекстах</span><span class="sxs-lookup"><span data-stu-id="4cc72-153">Chat with a bot in different contexts</span></span>

<span data-ttu-id="4cc72-154">Боты можно использовать в следующих контекстах:</span><span class="sxs-lookup"><span data-stu-id="4cc72-154">You can use bots in the following contexts:</span></span>

* <span data-ttu-id="4cc72-155">**Персональные приложения**: в личном приложении у пользователя Bot есть выделенная вкладка Chat.</span><span class="sxs-lookup"><span data-stu-id="4cc72-155">**Personal apps**: In a personal app, a bot has a dedicated chat tab.</span></span>
* <span data-ttu-id="4cc72-156">**Беседа одним** из следующих пользователей: пользователь может инициировать частные беседы с помощью Bot.</span><span class="sxs-lookup"><span data-stu-id="4cc72-156">**One-on-one chat**: A user can initiate a private conversation with a bot.</span></span> <span data-ttu-id="4cc72-157">Это то же самое, что и использование программы Bot в личном приложении.</span><span class="sxs-lookup"><span data-stu-id="4cc72-157">It's the same experience as using a bot in a personal app.</span></span>
* <span data-ttu-id="4cc72-158">**Групповой чат**: люди могут взаимодействовать с программой Bot в разделе chat, @mentioning с помощью ленты.</span><span class="sxs-lookup"><span data-stu-id="4cc72-158">**Group chat**: People can interact with a bot in a group chat by @mentioning the bot.</span></span>
* <span data-ttu-id="4cc72-159">**Канал**: люди могут взаимодействовать с роботом в канале.</span><span class="sxs-lookup"><span data-stu-id="4cc72-159">**Channel**: People can interact with a bot in a channel.</span></span> <span data-ttu-id="4cc72-160">, @mentioning имя Bot в поле Создать.</span><span class="sxs-lookup"><span data-stu-id="4cc72-160">by @mentioning the bot name in the compose box.</span></span> <span data-ttu-id="4cc72-161">Помните, что в этом контексте Bot доступен для всей команды, а не только для канала.</span><span class="sxs-lookup"><span data-stu-id="4cc72-161">Remember, in this context, the bot is available to the entire team, not just the channel.</span></span>

### <a name="anatomy"></a><span data-ttu-id="4cc72-162">Составляющие</span><span class="sxs-lookup"><span data-stu-id="4cc72-162">Anatomy</span></span>

:::image type="content" source="../../assets/images/bots/bot-anatomy.png" alt-text="В примере показана структурная структура Bot." border="false":::

|<span data-ttu-id="4cc72-164">Счетчик</span><span class="sxs-lookup"><span data-stu-id="4cc72-164">Counter</span></span>|<span data-ttu-id="4cc72-165">Описание</span><span class="sxs-lookup"><span data-stu-id="4cc72-165">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="4cc72-166">1</span><span class="sxs-lookup"><span data-stu-id="4cc72-166">1</span></span>|<span data-ttu-id="4cc72-167">**Имя и значок приложения**</span><span class="sxs-lookup"><span data-stu-id="4cc72-167">**App name and icon**</span></span>|
|<span data-ttu-id="4cc72-168">2 </span><span class="sxs-lookup"><span data-stu-id="4cc72-168">2</span></span>|<span data-ttu-id="4cc72-169">**Вкладка "чат**": открывает пространство для взаимодействия с Bot (применяется только к личным приложениям).</span><span class="sxs-lookup"><span data-stu-id="4cc72-169">**Chat tab**: Opens the space to talk with your bot (applicable only to personal apps).</span></span>|
|<span data-ttu-id="4cc72-170">3 </span><span class="sxs-lookup"><span data-stu-id="4cc72-170">3</span></span>|<span data-ttu-id="4cc72-171">**Настраиваемые вкладки**: открывает другое содержимое, связанное с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="4cc72-171">**Custom tabs**: Opens other content related to your app.</span></span>|
|<span data-ttu-id="4cc72-172">4 </span><span class="sxs-lookup"><span data-stu-id="4cc72-172">4</span></span>|<span data-ttu-id="4cc72-173">**Сведения о вкладке**: отображение основных сведений о приложении.</span><span class="sxs-lookup"><span data-stu-id="4cc72-173">**About tab**: Displays basic information about your app.</span></span>|
|<span data-ttu-id="4cc72-174">5 </span><span class="sxs-lookup"><span data-stu-id="4cc72-174">5</span></span>|<span data-ttu-id="4cc72-175">Подсистема **чата**: беседы в Bot используют платформу обмена сообщениями Teams.</span><span class="sxs-lookup"><span data-stu-id="4cc72-175">**Chat bubble**: Bot conversations use the Teams messaging framework.</span></span>|
|<span data-ttu-id="4cc72-176">6 </span><span class="sxs-lookup"><span data-stu-id="4cc72-176">6</span></span>|<span data-ttu-id="4cc72-177">**Адаптивная карта**: Если в качестве ответов для ленты используются адаптивные карты, карточка занимает всю ширину пузырька.</span><span class="sxs-lookup"><span data-stu-id="4cc72-177">**Adaptive Card**: If your bot’s responses include Adaptive Cards, the card takes up the full width of the chat bubble.</span></span>|
|<span data-ttu-id="4cc72-178">7 </span><span class="sxs-lookup"><span data-stu-id="4cc72-178">7</span></span>|<span data-ttu-id="4cc72-179">**Командное меню**: отображает стандартные команды ленты (определенные пользователем).</span><span class="sxs-lookup"><span data-stu-id="4cc72-179">**Command menu**: Displays your bot's standard commands (defined by you).</span></span>

### <a name="command-menu"></a><span data-ttu-id="4cc72-180">Меню команд</span><span class="sxs-lookup"><span data-stu-id="4cc72-180">Command menu</span></span>

<span data-ttu-id="4cc72-181">Меню команд содержит список слов или фраз, на которые должен отвечать пользователь с помощью ленты.</span><span class="sxs-lookup"><span data-stu-id="4cc72-181">The command menu provides a list of words or phrases you want your bot to always respond to.</span></span> <span data-ttu-id="4cc72-182">Меню команды отображается над полем "создание", когда кто-то работает с роботом.</span><span class="sxs-lookup"><span data-stu-id="4cc72-182">The command menu displays above the compose box when someone is conversing with a bot.</span></span> <span data-ttu-id="4cc72-183">При выборе команды она вставляется в сообщение.</span><span class="sxs-lookup"><span data-stu-id="4cc72-183">When a command is selected, it gets inserted into a message.</span></span>

<span data-ttu-id="4cc72-184">Список команд должен быть кратким.</span><span class="sxs-lookup"><span data-stu-id="4cc72-184">The list of commands should be brief.</span></span> <span data-ttu-id="4cc72-185">Меню предназначено только для выделения основных компонентов для ленты.</span><span class="sxs-lookup"><span data-stu-id="4cc72-185">The menu is only meant to highlight your bot’s primary features.</span></span> <span data-ttu-id="4cc72-186">Отследите, чтобы команды были краткими.</span><span class="sxs-lookup"><span data-stu-id="4cc72-186">Keep commands concise, too.</span></span> <span data-ttu-id="4cc72-187">Например, вместо того, **чтобы помочь вам**, создайте команду **Help** (Справка).</span><span class="sxs-lookup"><span data-stu-id="4cc72-187">For example, create a command called **Help** instead of **Can you please help me**?</span></span>
<span data-ttu-id="4cc72-188">Меню команд всегда должно быть доступно независимо от состояния беседы.</span><span class="sxs-lookup"><span data-stu-id="4cc72-188">The command menu must always be available regardless of the state of the conversation.</span></span>

:::image type="content" source="../../assets/images/bots/bot-command-menu.png" alt-text="В примере показана Командная меню Bot." border="false":::

## <a name="understand-what-people-are-saying"></a><span data-ttu-id="4cc72-190">Сведения о том, что говорят люди</span><span class="sxs-lookup"><span data-stu-id="4cc72-190">Understand what people are saying</span></span>

<span data-ttu-id="4cc72-191">Используйте тезаурус и получайте людей от максимально возможного количества фоновых рисунков, чтобы вы могли создавать различные интерпретации стандартных запросов.</span><span class="sxs-lookup"><span data-stu-id="4cc72-191">Use a thesaurus and get people from as many different backgrounds as possible to help you generate different interpretations of standard queries.</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-hello.png" alt-text="Иллюстрация, на которой показано, как Bot может интерпретировать &quot;Hello&quot;." border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-help.png" alt-text="Иллюстрация, на которой показано, как робот может интерпретировать &quot;Help&quot;." border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-thanks.png" alt-text="Иллюстрация, на которой показано, как с помощью Bot можно интерпретировать &quot;Спасибо&quot;." border="false":::
   :::column-end:::
:::row-end:::

### <a name="extract-intent-and-data-from-messages"></a><span data-ttu-id="4cc72-195">Извлечение намерения и данных из сообщений</span><span class="sxs-lookup"><span data-stu-id="4cc72-195">Extract intent and data from messages</span></span>

<span data-ttu-id="4cc72-196">Разработайте Bot для распознавания намерения, в результате чего в ответе на сообщение или запрос записывается кто-то из них.</span><span class="sxs-lookup"><span data-stu-id="4cc72-196">Design your bot to recognize intent, which captures what someone wants from a bot in response to a message or query.</span></span> <span data-ttu-id="4cc72-197">Назначение классифицирует сообщение или запрос как одно действие с одним или несколькими объектами данных, на которые влияет действие.</span><span class="sxs-lookup"><span data-stu-id="4cc72-197">Intent classifies a message or query as a single action with one or more data objects that are affected by the action.</span></span> 

<span data-ttu-id="4cc72-198">В приведенных ниже примерах описаны намерения пользователя и данные в сообщениях, отправляемых в Боты.</span><span class="sxs-lookup"><span data-stu-id="4cc72-198">The following examples outline the user intent and data in messages sent to bots.</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-1.png" alt-text="Пример, отображаемый в предложении &quot;Book a Flight to Сиэтл&quot;, цель пользователя — &quot;книга&quot;, а данные &quot;Москва&quot;." border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-2.png" alt-text="Пример, отображаемый в предложении &quot;при открытии хранилища&quot;, цель пользователя — &quot;when&quot;, а данные — &quot;Open&quot;." border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-3.png" alt-text="Пример, отображаемый в предложении &quot;планирование собрания на 1pm с Бобом в дистрибутиве&quot;, цель пользователя — &quot;планирование собрания&quot;, а данные — &quot;1pm&quot; и &quot;Bob в рассылке&quot;." border="false":::
   :::column-end:::
:::row-end:::

### <a name="analyze-and-improve"></a><span data-ttu-id="4cc72-202">Анализ и усовершенствование</span><span class="sxs-lookup"><span data-stu-id="4cc72-202">Analyze and improve</span></span>

<span data-ttu-id="4cc72-203">Сведения о том, что говорят пользователи при разговоре с Bot.</span><span class="sxs-lookup"><span data-stu-id="4cc72-203">Learn what users say when chatting with your bot.</span></span> <span data-ttu-id="4cc72-204">Это непрерывный, итеративный процесс, при котором пользовательская база растет в разных местах и организаций.</span><span class="sxs-lookup"><span data-stu-id="4cc72-204">This will be an ongoing, iterative process as your user base grows in different locations and orgs.</span></span> <span data-ttu-id="4cc72-205">Вы можете настроить распознавание языка и назначения языка для Bot с помощью средства понимания языка Майкрософт (Луис).</span><span class="sxs-lookup"><span data-stu-id="4cc72-205">You can tune your bot's language recognition and intent mapping with Microsoft Language Understanding (LUIS).</span></span>

* <span data-ttu-id="4cc72-206">[Общие сведения о Луис](https://docs.microsoft.com/azure/cognitive-services/luis/artificial-intelligence): сведения о том, как Луис использует AI для обеспечения естественного понимания языка (НЛУ) данных приложения.</span><span class="sxs-lookup"><span data-stu-id="4cc72-206">[Understanding LUIS](https://docs.microsoft.com/azure/cognitive-services/luis/artificial-intelligence): Find out how LUIS uses AI to provide natural language understanding (NLU) to your app data.</span></span>
* <span data-ttu-id="4cc72-207">[Интеграция с Луис](https://www.luis.ai/): Добавление функций естественных языков в Bot без сложного процесса создания моделей машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="4cc72-207">[Integrating with LUIS](https://www.luis.ai/): Add natural language capabilities to your bot without the complex process of creating machine learning models.</span></span>

## <a name="use-cases"></a><span data-ttu-id="4cc72-208">Варианты использования</span><span class="sxs-lookup"><span data-stu-id="4cc72-208">Use cases</span></span>

### <a name="simple-queries"></a><span data-ttu-id="4cc72-209">Простые запросы</span><span class="sxs-lookup"><span data-stu-id="4cc72-209">Simple queries</span></span>

<span data-ttu-id="4cc72-210">Боты может обеспечить точное соответствие запросу или группе связанных соответствий для упрощения устранения неоднозначности.</span><span class="sxs-lookup"><span data-stu-id="4cc72-210">Bots can deliver an exact match to a query or a group of related matches to help with disambiguation.</span></span> <span data-ttu-id="4cc72-211">Для связанных совпадений сгруппируйте контент с помощью карточки списка.</span><span class="sxs-lookup"><span data-stu-id="4cc72-211">For related matches, group the content using a list card.</span></span>

:::image type="content" source="../../assets/images/bots/bot-simple-query.png" alt-text="В примере показан простой запрос взаимодействия с роботом." border="false":::

### <a name="multi-turn-interactions"></a><span data-ttu-id="4cc72-213">Взаимодействие с несколькими переворотами</span><span class="sxs-lookup"><span data-stu-id="4cc72-213">Multi-turn interactions</span></span>

<span data-ttu-id="4cc72-214">В то время как ваш робот может поддерживать полные запросы и вопросы, он также должен иметь возможность управлять несколькими интерактивными взаимодействиями.</span><span class="sxs-lookup"><span data-stu-id="4cc72-214">While your bot can support complete requests and questions, it should also be able to handle multi-turn interactions.</span></span> <span data-ttu-id="4cc72-215">Ожидаемые дальнейшие действия значительно облегчают для людей весь рабочий процесс (а не предоставляя им исчерпывающий запрос).</span><span class="sxs-lookup"><span data-stu-id="4cc72-215">Anticipating possible next steps makes it much easier for people to a complete task flow (rather than expecting them to craft a comprehensive request).</span></span>

<span data-ttu-id="4cc72-216">В следующем примере Bot реагирует на каждое сообщение с вариантами, которые могут потребоваться далее.</span><span class="sxs-lookup"><span data-stu-id="4cc72-216">In the following example, the bot responds to each message with options for what might want to do next.</span></span>

:::image type="content" source="../../assets/images/bots/bot-multi-turn.png" alt-text="Пример многофакторного взаимодействия с Bot." border="false":::

### <a name="reach-out-to-users"></a><span data-ttu-id="4cc72-218">Доступ к пользователям</span><span class="sxs-lookup"><span data-stu-id="4cc72-218">Reach out to users</span></span>

<span data-ttu-id="4cc72-219">С помощью упреждающего обмена сообщениями Bot могут выполнять функции, которые отправляют уведомления, относящиеся к отдельному, групповому разговору или каналу с определенной частотой.</span><span class="sxs-lookup"><span data-stu-id="4cc72-219">With proactive messaging, your bot can act like a digest that sends notifications relevant to an individual, group chat, or channel at a specific frequency.</span></span> <span data-ttu-id="4cc72-220">С помощью ленты Bot можно отправить сообщение, когда в документе изменилось какое-либо изменение или закрыть рабочий элемент.</span><span class="sxs-lookup"><span data-stu-id="4cc72-220">A bot may send a message when something has changed in a document or a work item is closed.</span></span>

<span data-ttu-id="4cc72-221">В следующем примере пользователь получает всплывающее уведомление о том, что в канале с сообщением Bot помещается в другом канале.</span><span class="sxs-lookup"><span data-stu-id="4cc72-221">In the following example, a user gets a toast notification that a bot messaged them in another channel.</span></span>

:::image type="content" source="../../assets/images/bots/bot-proactive-message-toast.png" alt-text="В примере показано всплывающее уведомление о неактивном обмене сообщениями с пользователем из другого канала." border="false":::

<span data-ttu-id="4cc72-223">Теперь пользователь может прочитать сообщение из Bot-канала.</span><span class="sxs-lookup"><span data-stu-id="4cc72-223">Now in that channel, the user can read their message from the bot.</span></span>

:::image type="content" source="../../assets/images/bots/bot-proactive-message.png" alt-text="Пример показывает, что пользователь просматривает упреждающее сообщение." border="false":::

### <a name="use-tabs-with-bots"></a><span data-ttu-id="4cc72-225">Использование вкладок с Боты</span><span class="sxs-lookup"><span data-stu-id="4cc72-225">Use tabs with bots</span></span>

<span data-ttu-id="4cc72-226">С помощью вкладки можно упростить использование ленты.</span><span class="sxs-lookup"><span data-stu-id="4cc72-226">A tab can make your bot easier to use.</span></span> <span data-ttu-id="4cc72-227">Например, если ваш Bot может создавать рабочие элементы, было бы неплохо Показать все эти элементы в центральном расположении внутри вкладки. Подробнее о [проектировании вкладок](../../tabs/design/tabs.md).</span><span class="sxs-lookup"><span data-stu-id="4cc72-227">For example, if your bot can create work items, it would be nice to show all those items in a central location inside a tab. See more about [designing tabs](../../tabs/design/tabs.md).</span></span>

:::image type="content" source="../../assets/images/bots/bot-with-tab.png" alt-text="В примере показано, как можно управлять контентом Bot с помощью вкладки." border="false":::

## <a name="manage-a-bot"></a><span data-ttu-id="4cc72-229">Управление Bot</span><span class="sxs-lookup"><span data-stu-id="4cc72-229">Manage a bot</span></span>

<span data-ttu-id="4cc72-230">Пользователи должны иметь возможность изменять параметры ленты.</span><span class="sxs-lookup"><span data-stu-id="4cc72-230">Users should be able to change a bot's settings.</span></span> <span data-ttu-id="4cc72-231">Вы можете предоставить эту функцию с помощью команд Bot, но обычно более эффективно включать все параметры в [модуль задач](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) (как показано в следующем примере).</span><span class="sxs-lookup"><span data-stu-id="4cc72-231">You can provide this functionality with bot commands, but it's usually more efficient to include all settings in a [task module](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) (as shown in the following example).</span></span>

:::image type="content" source="../../assets/images/bots/manage-bot-task-module.png" alt-text="В примере показан модуль задачи для настройки параметров Bot." border="false":::

## <a name="best-practices"></a><span data-ttu-id="4cc72-233">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="4cc72-233">Best practices</span></span>

### <a name="content"></a><span data-ttu-id="4cc72-234">Содержимое</span><span class="sxs-lookup"><span data-stu-id="4cc72-234">Content</span></span>

:::image type="content" source="../../assets/images/bots/bot-content-persona-do.png" alt-text="Пример, в котором показана рекомендуемая практика." border="false":::

#### <a name="do-establish-a-clear-persona"></a><span data-ttu-id="4cc72-236">Do: создание понятного пользователя</span><span class="sxs-lookup"><span data-stu-id="4cc72-236">Do: Establish a clear persona</span></span>

<span data-ttu-id="4cc72-237">Является ли ваш Bot понятным и светлым, "только факты", или очень тонкой?</span><span class="sxs-lookup"><span data-stu-id="4cc72-237">Is your bot's tone friendly and light, “just the facts”, or super quirky?</span></span> <span data-ttu-id="4cc72-238">Как он должен реагировать в различных сценариях?</span><span class="sxs-lookup"><span data-stu-id="4cc72-238">How should it respond in different scenarios?</span></span> <span data-ttu-id="4cc72-239">Планирование и документирование персонажа пользователя с пользовательским роботом упрощает написание откликов, которые кажутся естественными и взаимосвязаны.</span><span class="sxs-lookup"><span data-stu-id="4cc72-239">Planning and documenting your bot's persona makes it easier to write responses that seem natural and cohesive.</span></span>

<span data-ttu-id="4cc72-240">Дополнительные сведения о написании для боты можно найти в <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">наборе элементов Microsoft Teams Kit (фигма).</a></span><span class="sxs-lookup"><span data-stu-id="4cc72-240">See more about writing for bots in the <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">Microsoft Teams UI Kit (Figma).</a></span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-convey-do.png" alt-text="Пример, в котором показана рекомендуемая практика." border="false":::

#### <a name="do-clearly-convey-what-your-bot-can-do"></a><span data-ttu-id="4cc72-242">Сделать: ясно укажите действия, которые может выполнять Bot</span><span class="sxs-lookup"><span data-stu-id="4cc72-242">Do: Clearly convey what your bot can do</span></span>

<span data-ttu-id="4cc72-243">Приветственные сообщения и обзоры помогают людям узнать, что можно делать с помощью программы Bot.</span><span class="sxs-lookup"><span data-stu-id="4cc72-243">Welcome messages and tours help people understand what they can do with your bot.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-convey-dont.png" alt-text="Пример, в котором показана рекомендуемая практика." border="false":::

#### <a name="dont-obscure-your-bots-features"></a><span data-ttu-id="4cc72-245">Не закрывать функции для ленты.</span><span class="sxs-lookup"><span data-stu-id="4cc72-245">Don't: Obscure your bot's features</span></span>

<span data-ttu-id="4cc72-246">Первое впечатление.</span><span class="sxs-lookup"><span data-stu-id="4cc72-246">First impressions matter.</span></span> <span data-ttu-id="4cc72-247">Пользователи, скорее всего, будут путать или подозрительны, если вы увидите сообщение для входа в нондескрипт.</span><span class="sxs-lookup"><span data-stu-id="4cc72-247">People will likely be confused or suspicious when presented with a nondescript sign-in message.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-understand-do.png" alt-text="Пример, в котором показана рекомендуемая практика." border="false":::

#### <a name="do-recognize-non-questions"></a><span data-ttu-id="4cc72-249">Do: распознать несвязанные вопросы</span><span class="sxs-lookup"><span data-stu-id="4cc72-249">Do: Recognize non-questions</span></span>

<span data-ttu-id="4cc72-250">Ваш робот должен иметь возможность отвечать на такие сообщения, как "Привет", "Справка" и "Спасибо", а также учет типичных ошибок и коллокуиалисмс.</span><span class="sxs-lookup"><span data-stu-id="4cc72-250">Your bot should be able to respond to messages like "Hi", "Help", and "Thanks" while also accounting for common misspellings and colloquialisms.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-understand-dont.png" alt-text="Пример, в котором показана рекомендуемая практика." border="false":::

#### <a name="dont-miss-out-on-opportunities-to-delight"></a><span data-ttu-id="4cc72-252">Не: пропустите возможности сведения</span><span class="sxs-lookup"><span data-stu-id="4cc72-252">Don't: Miss out on opportunities to delight</span></span>

<span data-ttu-id="4cc72-253">Некоторые люди ожидают, что беседы работают естественным образом с реальным человеком.</span><span class="sxs-lookup"><span data-stu-id="4cc72-253">Some people expect conversations to flow naturally like they would with a real person.</span></span> <span data-ttu-id="4cc72-254">Постарайтесь избежать ответов клумси на простые сообщения.</span><span class="sxs-lookup"><span data-stu-id="4cc72-254">Try to avoid clumsy responses to simple messages.</span></span>

   :::column-end:::
:::row-end:::

### <a name="troubleshooting"></a><span data-ttu-id="4cc72-255">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="4cc72-255">Troubleshooting</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-help-do.png" alt-text="Пример, в котором показана рекомендуемая практика." border="false":::

#### <a name="do-provide-help"></a><span data-ttu-id="4cc72-257">Do: предоставление справки</span><span class="sxs-lookup"><span data-stu-id="4cc72-257">Do: Provide help</span></span>

<span data-ttu-id="4cc72-258">Если ваш робот не может удовлетворить запрос, предоставьте пользователю способы взаимодействия с роботом.</span><span class="sxs-lookup"><span data-stu-id="4cc72-258">If your bot can’t satisfy a request, provide ways for a user to educate themselves about interacting with your bot.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-help-dont.png" alt-text="Пример, в котором показана рекомендуемая практика." border="false":::

#### <a name="dont-leave-users-stranded"></a><span data-ttu-id="4cc72-260">Не: оставляйте потерянных пользователей</span><span class="sxs-lookup"><span data-stu-id="4cc72-260">Don't: Leave users stranded</span></span>

<span data-ttu-id="4cc72-261">Пользователи смогут быстро отказаться от работы с роботом, если они не могут устранить неполадки.</span><span class="sxs-lookup"><span data-stu-id="4cc72-261">People will quickly abandon your bot if they can’t troubleshoot issues.</span></span>

   :::column-end:::
:::row-end:::

### <a name="complex-interactions"></a><span data-ttu-id="4cc72-262">Сложные взаимодействия</span><span class="sxs-lookup"><span data-stu-id="4cc72-262">Complex interactions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-interactions-do.png" alt-text="Пример, в котором показана рекомендуемая практика." border="false":::

#### <a name="do-use-task-modules-or-tabs"></a><span data-ttu-id="4cc72-264">Do: использование модулей задач или вкладок</span><span class="sxs-lookup"><span data-stu-id="4cc72-264">Do: Use task modules or tabs</span></span>

<span data-ttu-id="4cc72-265">Если у ленты есть ответ, требующий еще несколько действий, можно создать ссылку на модуль задачи или вкладку для завершения задачи или процесса.</span><span class="sxs-lookup"><span data-stu-id="4cc72-265">If your bot provides an answer that requires a few more steps, you can link to a task module or tab to complete the task or flow.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-interactions-dont.png" alt-text="Пример, в котором показана рекомендуемая практика." border="false":::

#### <a name="dont-make-multi-turn-interactions-tedious"></a><span data-ttu-id="4cc72-267">Не: утомительные взаимодействия с несколькими переворотами</span><span class="sxs-lookup"><span data-stu-id="4cc72-267">Don't: Make multi-turn interactions tedious</span></span>

<span data-ttu-id="4cc72-268">Обширная беседа для выполнения одной задачи очень мала и слишком сложна.</span><span class="sxs-lookup"><span data-stu-id="4cc72-268">An extensive conversation to complete a single task is slow and overly complex.</span></span> <span data-ttu-id="4cc72-269">Кроме того, необходимо, чтобы разработчик заменил изменения состояний (например, время ожидания беседы или отправка сообщения "Отмена").</span><span class="sxs-lookup"><span data-stu-id="4cc72-269">It also requires the developer to account for state changes (such as the conversation timing out or you sending a “Cancel” message).</span></span>

   :::column-end:::
:::row-end:::

### <a name="privacy"></a><span data-ttu-id="4cc72-270">Конфиденциальность</span><span class="sxs-lookup"><span data-stu-id="4cc72-270">Privacy</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-privacy-do.png" alt-text="Пример, в котором показана рекомендуемая практика." border="false":::

#### <a name="do-only-show-sensitive-info-in-a-personal-context"></a><span data-ttu-id="4cc72-272">Do: показывать только конфиденциальные данные в личном контексте</span><span class="sxs-lookup"><span data-stu-id="4cc72-272">Do: Only show sensitive info in a personal context</span></span>

<span data-ttu-id="4cc72-273">Если в качестве ленты используется групповой чат или канал, рекомендуется направить пользователей в частное расположение (например, модуль задачи, вкладку или браузер) для просмотра конфиденциальной информации.</span><span class="sxs-lookup"><span data-stu-id="4cc72-273">If your bot is in a group chat or channel, we recommend directing users to a private location (such as a task module, tab, or browser) to view sensitive information.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-privacy-dont.png" alt-text="Пример, в котором показана рекомендуемая практика." border="false":::

#### <a name="dont-some-content-isnt-meant-to-be-seen-by-everyone"></a><span data-ttu-id="4cc72-275">Не так: часть контента не должна отображаться для всех пользователей</span><span class="sxs-lookup"><span data-stu-id="4cc72-275">Don't: Some content isn’t meant to be seen by everyone</span></span>

<span data-ttu-id="4cc72-276">Ваш робот не должен раскрывать конфиденциальную информацию группе людей.</span><span class="sxs-lookup"><span data-stu-id="4cc72-276">Your bot shouldn’t reveal sensitive information to a group of people.</span></span>

   :::column-end:::
:::row-end:::

## <a name="learn-more"></a><span data-ttu-id="4cc72-277">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="4cc72-277">Learn more</span></span>

<span data-ttu-id="4cc72-278">Следующие рекомендации могут помочь вам в работе с Bot:</span><span class="sxs-lookup"><span data-stu-id="4cc72-278">These other guidelines may help with your bot design:</span></span>

* [<span data-ttu-id="4cc72-279">Разработка личного приложения</span><span class="sxs-lookup"><span data-stu-id="4cc72-279">Designing your personal app</span></span>](../../concepts/design/personal-apps.md)
* [<span data-ttu-id="4cc72-280">Разработка адаптивных карточек</span><span class="sxs-lookup"><span data-stu-id="4cc72-280">Designing Adaptive Cards</span></span>](../../task-modules-and-cards/cards/design-effective-cards.md)
* [<span data-ttu-id="4cc72-281">Разработка модулей задач</span><span class="sxs-lookup"><span data-stu-id="4cc72-281">Designing task modules</span></span>](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)

## <a name="validate-your-design"></a><span data-ttu-id="4cc72-282">Проверка проекта</span><span class="sxs-lookup"><span data-stu-id="4cc72-282">Validate your design</span></span>

<span data-ttu-id="4cc72-283">Если вы планируете опубликовать свое приложение в AppSource, следует изучить проблемы, которые обычно приводят к сбою приложений во время отправки.</span><span class="sxs-lookup"><span data-stu-id="4cc72-283">If you plan to publish your app to AppSource, you should understand the design issues that commonly cause apps to fail during submission.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4cc72-284">Проверка рекомендаций по проверке макета</span><span class="sxs-lookup"><span data-stu-id="4cc72-284">Check design validation guidelines</span></span>](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
