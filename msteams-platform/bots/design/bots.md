---
title: Рекомендации по проектированию для Боты
description: Описывает рекомендации по созданию Боты
keywords: рекомендации по проектированию Teams Справочник по платформе Боты
ms.openlocfilehash: 4f474278b37058f61886a620af634780d2e3cb19
ms.sourcegitcommit: d0ca6a4856ffd03d197d47338e633126723fa78a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/15/2020
ms.locfileid: "45137677"
---
# <a name="start-talking-with-bots"></a><span data-ttu-id="1d014-104">Начало беседы с Боты</span><span class="sxs-lookup"><span data-stu-id="1d014-104">Start talking with bots</span></span>

<span data-ttu-id="1d014-105">Боты — это беседы, которые выполняют узкий или определенный набор задач.</span><span class="sxs-lookup"><span data-stu-id="1d014-105">Bots are conversational apps that perform a narrow or specific set of tasks.</span></span> <span data-ttu-id="1d014-106">Они предоставляют возможность общаться с пользователями, отвечать на них, отвечать на свои вопросы и заблаговременно уведомлять об изменениях.</span><span class="sxs-lookup"><span data-stu-id="1d014-106">They give you an opportunity to communicate with users, respond to their questions, and proactively notify them about changes.</span></span> <span data-ttu-id="1d014-107">Это отличный способ достигать.</span><span class="sxs-lookup"><span data-stu-id="1d014-107">They’re a great way to reach out.</span></span>

---

## <a name="guidelines"></a><span data-ttu-id="1d014-108">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="1d014-108">Guidelines</span></span>

### <a name="avatars"></a><span data-ttu-id="1d014-109">Аватаров</span><span class="sxs-lookup"><span data-stu-id="1d014-109">Avatars</span></span>

<span data-ttu-id="1d014-110">Аватары в Teams создаются в виде шестиугольников, поэтому люди могут быстро сказать, что они говорят на Bot, а не человека.</span><span class="sxs-lookup"><span data-stu-id="1d014-110">Bot avatars in Teams are shaped like hexagons so people can quickly tell that they’re talking to a bot instead of a person.</span></span> <span data-ttu-id="1d014-111">Вы отправите свой аватар в виде квадрата, и мы обрезать его.</span><span class="sxs-lookup"><span data-stu-id="1d014-111">You’ll submit your avatar as a square and we’ll crop it for you.</span></span> <span data-ttu-id="1d014-112">Когда речь идет о аватарах, мы рекомендуем сделать их разборчиво от 2 метров и использовать более высокую контрастность.</span><span class="sxs-lookup"><span data-stu-id="1d014-112">When it comes to avatars, we recommend making yours legible from 2 feet away and using a higher contrast.</span></span>

[!include[Avatar image](~/includes/design/bot-avatar-image.html)]

### <a name="buttons"></a><span data-ttu-id="1d014-113">Кнопки</span><span class="sxs-lookup"><span data-stu-id="1d014-113">Buttons</span></span>

<span data-ttu-id="1d014-114">Поддерживается до шести кнопок для одной карточки.</span><span class="sxs-lookup"><span data-stu-id="1d014-114">We support up to six buttons per card.</span></span> <span data-ttu-id="1d014-115">Будьте лаконичны при написании текста на кнопке и имейте в виду, что большинство кнопок должно только самостоятельно обращаться к задачам.</span><span class="sxs-lookup"><span data-stu-id="1d014-115">Be concise when writing button text, and keep in mind that most buttons should only address the task at hand.</span></span>

### <a name="graphics"></a><span data-ttu-id="1d014-116">Картин</span><span class="sxs-lookup"><span data-stu-id="1d014-116">Graphics</span></span>

<span data-ttu-id="1d014-117">Рисунки — это хороший способ сказать, что не все роботы для ленты должны иметь графический объект, поэтому их следует использовать для достижения максимальной влияния.</span><span class="sxs-lookup"><span data-stu-id="1d014-117">Graphics are a good way to tell a story, but not all bot conversations require graphics, so use them for maximum impact.</span></span>

### <a name="onboarding-users"></a><span data-ttu-id="1d014-118">Встроенные пользователи</span><span class="sxs-lookup"><span data-stu-id="1d014-118">Onboarding users</span></span>

<span data-ttu-id="1d014-119">Очень важно, чтобы Боты представлю себя и преддавала возможности для пользователей.</span><span class="sxs-lookup"><span data-stu-id="1d014-119">It is critical that bots introduce themselves and convey what they can do for users.</span></span> <span data-ttu-id="1d014-120">Это *значение* помогает пользователям разобралось, что делать с Bot, где ограничения могут надержаться, и, что самое важное, помогает пользователям обеспечить взаимодействие с компьютером, который не будет интуитивно интуитивно понятен для реальных людей.</span><span class="sxs-lookup"><span data-stu-id="1d014-120">This *value exchange* helps users understand what to do with the bot, where the limitations may lie, and, most importantly, helps users tolerate the interaction with a machine that won’t be as intuitive as a real person .</span></span> <span data-ttu-id="1d014-121">Кроме того, он предоставляет разрешения на доступ к данным пользователя в Exchange для фактического значения, предоставляемого службой.</span><span class="sxs-lookup"><span data-stu-id="1d014-121">Additionally, it grants permission to user data in exchange for the real value the service provides.</span></span>

#### <a name="welcome-messages"></a><span data-ttu-id="1d014-122">Приветственные сообщения</span><span class="sxs-lookup"><span data-stu-id="1d014-122">Welcome messages</span></span>

<span data-ttu-id="1d014-123">Приветственные сообщения — это лучший способ задать тон для Bot и использовать их в личных и коллективных и групповых сценариях.</span><span class="sxs-lookup"><span data-stu-id="1d014-123">Welcome messages are the best way to set your bot's tone and should be used in personal and team or group scenarios.</span></span> <span data-ttu-id="1d014-124">В сообщении указывается, что делает Bot, и некоторые распространенные способы взаимодействия с ним.</span><span class="sxs-lookup"><span data-stu-id="1d014-124">The message states what the bot does and some common ways to interact with it.</span></span> <span data-ttu-id="1d014-125">Использование определенных возможностей например, "*попробовать запрашивать....*"</span><span class="sxs-lookup"><span data-stu-id="1d014-125">Use specific capability examples like,  “*Try asking ….*”</span></span> <span data-ttu-id="1d014-126">в маркированном списке.</span><span class="sxs-lookup"><span data-stu-id="1d014-126">in a bulleted list.</span></span> <span data-ttu-id="1d014-127">По мере возможности эти предложения должны возвращать сохраненные ответы.</span><span class="sxs-lookup"><span data-stu-id="1d014-127">Whenever possible, these suggestions should return stored responses.</span></span> <span data-ttu-id="1d014-128">Очень важно, чтобы примеры возможностей работали без необходимости входа пользователей.</span><span class="sxs-lookup"><span data-stu-id="1d014-128">It's critical that the capability examples work without requiring users to sign in.</span></span>

#### <a name="tours"></a><span data-ttu-id="1d014-129">Обзоры</span><span class="sxs-lookup"><span data-stu-id="1d014-129">Tours</span></span>

<span data-ttu-id="1d014-130">Включите атрибут " *Обзор* " с приветственными сообщениями и ответами на пользовательский ввод в "*Справка*".</span><span class="sxs-lookup"><span data-stu-id="1d014-130">Include a *Take a tour* attribute with welcome messages and responses to user input equivalent to “*help*”.</span></span> <span data-ttu-id="1d014-131">Это самый эффективный способ, позволяющий пользователям узнать, что можно сделать с помощью Bot.</span><span class="sxs-lookup"><span data-stu-id="1d014-131">This is the most effective way to let users learn what a bot can do.</span></span> <span data-ttu-id="1d014-132">Почтовые точки в одном-одном интерфейсе — это отличный способ сообщить эту историю и включить *попытаться связать ее* с примерами возможных ответов.</span><span class="sxs-lookup"><span data-stu-id="1d014-132">Carousels in one-to-one experiences are an excellent way to tell this story and including *Try it* buttons linking to  examples of possible responses is encouraged.</span></span> <span data-ttu-id="1d014-133">Обзоры также являются отличными местами для общения с другими функциями приложения.</span><span class="sxs-lookup"><span data-stu-id="1d014-133">Tours are also great places to talk about an app’s other features.</span></span> <span data-ttu-id="1d014-134">Например, вы можете включить снимки экрана расширения для обмена сообщениями и вкладок Teams.</span><span class="sxs-lookup"><span data-stu-id="1d014-134">For example, you can include screenshots of messaging extensions and Teams tabs.</span></span>  <span data-ttu-id="1d014-135">Пользователям не нужно выполнять вход в систему для доступа и использовать обзор.</span><span class="sxs-lookup"><span data-stu-id="1d014-135">Users shouldn't have to sign in to access and use a tour.</span></span>

<span data-ttu-id="1d014-136">Когда обзоры используются в сценариях группы или групп, они должны открываться в модуле задач, чтобы не добавим в текущие связи между пользователями больше шума карты.</span><span class="sxs-lookup"><span data-stu-id="1d014-136">When tours are used in team or group scenarios, they should open in a task module so as not to add more card noise to the ongoing conversations between users.</span></span>

### <a name="responding-to-users-and-failing-gracefully"></a><span data-ttu-id="1d014-137">Реагирование на пользователей и неправильное отработка отказа</span><span class="sxs-lookup"><span data-stu-id="1d014-137">Responding to users and failing gracefully</span></span>

<span data-ttu-id="1d014-138">Ваш робот также должен иметь возможность отвечать на такие вещи, как "*Привет*", "*Справка*" и "*спасибо*", при этом учитывается типичные опечатки и коллокуиалисмс.</span><span class="sxs-lookup"><span data-stu-id="1d014-138">Your bot should also be able to respond to things like "*Hi*", "*Help*", and "*Thanks*" while taking common misspellings and colloquialisms into account.</span></span> <span data-ttu-id="1d014-139">Пример:</span><span class="sxs-lookup"><span data-stu-id="1d014-139">For example:</span></span>

#### <a name="x2713-hello"></a><span data-ttu-id="1d014-140">&#x2713; Hello</span><span class="sxs-lookup"><span data-stu-id="1d014-140">&#x2713; Hello</span></span>

<span data-ttu-id="1d014-141">`"Hi"`  `"How are you"`  `"Howdy"`</span><span class="sxs-lookup"><span data-stu-id="1d014-141">`"Hi"`  `"How are you"`  `"Howdy"`</span></span>

#### <a name="x2713-help"></a><span data-ttu-id="1d014-142">Справка по &#x2713;</span><span class="sxs-lookup"><span data-stu-id="1d014-142">&#x2713; Help</span></span>

<span data-ttu-id="1d014-143">`"What do you do?"`  `"How does this work?"`  `"What the heck?"`</span><span class="sxs-lookup"><span data-stu-id="1d014-143">`"What do you do?"`  `"How does this work?"`  `"What the heck?"`</span></span>

#### <a name="x2713-thanks"></a><span data-ttu-id="1d014-144">&#x2713; Спасибо</span><span class="sxs-lookup"><span data-stu-id="1d014-144">&#x2713; Thanks</span></span>

<span data-ttu-id="1d014-145">`"Thank you"`  `"Thankyou"`  `"Thx"`</span><span class="sxs-lookup"><span data-stu-id="1d014-145">`"Thank you"`  `"Thankyou"`  `"Thx"`</span></span>

<span data-ttu-id="1d014-146">Ваш робот должен иметь возможность обрабатывать следующие типы запросов и входных данных:</span><span class="sxs-lookup"><span data-stu-id="1d014-146">Your bot should be able to handle the following types of queries and inputs:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="1d014-147">**Распознанные вопросы**.</span><span class="sxs-lookup"><span data-stu-id="1d014-147">**Recognized questions**.</span></span> <span data-ttu-id="1d014-148">Это наиболее подходящие вопросы, которые могут ожидать пользователи.</span><span class="sxs-lookup"><span data-stu-id="1d014-148">These are the “best case scenario” questions you would expect from users.</span></span>
> * <span data-ttu-id="1d014-149">**Распознаваемые несвязанные вопросы**.</span><span class="sxs-lookup"><span data-stu-id="1d014-149">**Recognized non-questions**.</span></span> <span data-ttu-id="1d014-150">Запросы о неподдерживаемых функциях и/или случайных, несвязанных или ненормативных записях.</span><span class="sxs-lookup"><span data-stu-id="1d014-150">Queries about unsupported functionality and/or random, unrelated , or profane entries.</span></span>
> * <span data-ttu-id="1d014-151">**Неизвестные вопросы**: нечитаемые входные или нечитаемые элементы или нонсенсе.</span><span class="sxs-lookup"><span data-stu-id="1d014-151">**Unrecognized questions**: Input or entries that are unintelligible, meaningless, or nonsense.</span></span>

<span data-ttu-id="1d014-152">Примеры типов индивидуальной и отклика для ленты:</span><span class="sxs-lookup"><span data-stu-id="1d014-152">Examples of bot personality and response types:</span></span>

[!include[Bot responses](~/includes/design/bot-responses-table.html)]

> [!TIP]
> <span data-ttu-id="1d014-153">Когда вы пишете свой сценарий, запросите себя: "будет ли моя фирма извредна, если ответ будет получен и общий?"</span><span class="sxs-lookup"><span data-stu-id="1d014-153">When writing your bot script, ask yourself: “Will my company be embarrassed if a response is screen captured and shared?”</span></span>

### <a name="understanding-what-users-are-trying-to-say"></a><span data-ttu-id="1d014-154">Общие сведения о том, что пользователи пытаются сказать</span><span class="sxs-lookup"><span data-stu-id="1d014-154">Understanding what users are trying to say</span></span>

#### <a name="use-a-thesaurus-for-synonyms"></a><span data-ttu-id="1d014-155">Использование тезауруса для синонимов</span><span class="sxs-lookup"><span data-stu-id="1d014-155">Use a thesaurus for synonyms</span></span>

<span data-ttu-id="1d014-156">При мозговых задолженностей Используйте тезаурус и получите людей от максимально возможного количества фоновых рисунков, чтобы вы могли создавать различные интерпретации каждого запроса.</span><span class="sxs-lookup"><span data-stu-id="1d014-156">When brainstorming variants, use a thesaurus and get people from as many different backgrounds as possible to help you generate different interpretations of each query.</span></span>

#### <a name="make-use-of-telemetry-and-interviews"></a><span data-ttu-id="1d014-157">Использование телеметрии и интервью</span><span class="sxs-lookup"><span data-stu-id="1d014-157">Make use of telemetry and interviews</span></span>

<span data-ttu-id="1d014-158">Сведения о том, что говорят пользователи, и каковы их цели при опросе ленты.</span><span class="sxs-lookup"><span data-stu-id="1d014-158">Find out what users are saying and what was their intent when querying your bot.</span></span> <span data-ttu-id="1d014-159">Это будет непрерывный процесс, когда вы получаете пользователей в различных местоположениях и типах компаний.</span><span class="sxs-lookup"><span data-stu-id="1d014-159">This will be an ongoing process as you get users in different locations and types of companies.</span></span> <span data-ttu-id="1d014-160">Вы можете выполнить тонкую настройку распознавания языка и соответствия намерения языку интеллектуальной службы ([Луис](/azure/cognitive-services/luis/what-is-luis)).</span><span class="sxs-lookup"><span data-stu-id="1d014-160">You can fine-tune language recognition and intent mapping with Language Understanding Intelligent Service ([LUIS](/azure/cognitive-services/luis/what-is-luis)).</span></span>

### <a name="how-often-should-you-use-your-bot-to-reach-out-to-a-user"></a><span data-ttu-id="1d014-161">Как часто следует использовать ваш Bot для доступа к пользователю?</span><span class="sxs-lookup"><span data-stu-id="1d014-161">How often should you use your bot to reach out to a user?</span></span>

#### <a name="x2713-when-a-state-has-changed"></a><span data-ttu-id="1d014-162">&#x2713; при изменении состояния</span><span class="sxs-lookup"><span data-stu-id="1d014-162">&#x2713; When a state has changed</span></span>

<span data-ttu-id="1d014-163">Например, если назначение помечено как завершенное, при изменении ошибки, при появления новых социальных сетей или при завершении опроса.</span><span class="sxs-lookup"><span data-stu-id="1d014-163">For example, if an assignment is marked as complete, when a bug changes, when new social media is available, or when a poll has been completed.</span></span>

#### <a name="x2713-when-the-timing-is-right"></a><span data-ttu-id="1d014-164">&#x2713;, когда выполняется правильная продолжительность</span><span class="sxs-lookup"><span data-stu-id="1d014-164">&#x2713; When the timing is right</span></span>

<span data-ttu-id="1d014-165">Ваш Bot может вести себя как ежедневный дайджест, отправляя уведомление пользователю или каналу по определенной частоте.</span><span class="sxs-lookup"><span data-stu-id="1d014-165">Your bot can act like a daily digest, sending a notification to the user or channel at a specific frequency.</span></span>

<span data-ttu-id="1d014-166">Оставить пользователя в элементе управления.</span><span class="sxs-lookup"><span data-stu-id="1d014-166">Leave the user in control.</span></span> <span data-ttu-id="1d014-167">Предоставьте параметры уведомлений, которые включают частоту и приоритет.</span><span class="sxs-lookup"><span data-stu-id="1d014-167">Provide notification settings that include frequency and priority.</span></span>

[!include[Bot notification](~/includes/design/bot-notification-image.html)]

---

## <a name="using-tabs"></a><span data-ttu-id="1d014-168">Использование вкладок</span><span class="sxs-lookup"><span data-stu-id="1d014-168">Using tabs</span></span>

<span data-ttu-id="1d014-169">С помощью вкладок вы намерены, чтобы использовать роботы.</span><span class="sxs-lookup"><span data-stu-id="1d014-169">Tabs make your bot much more functional.</span></span> <span data-ttu-id="1d014-170">С помощью вкладок можно создавать следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="1d014-170">With tabs, you can create the following:</span></span>

### <a name="x2713-a-place-to-host-standing-queries"></a><span data-ttu-id="1d014-171">&#x2713; места для размещения зафиксированных запросов</span><span class="sxs-lookup"><span data-stu-id="1d014-171">&#x2713; A place to host standing queries</span></span>

<span data-ttu-id="1d014-172">В личных беседах между Bot и одним человеком вкладки могут содержать сведения и списки, относящиеся к пользователю.</span><span class="sxs-lookup"><span data-stu-id="1d014-172">In personal conversations between a bot and a single person, tabs can contain user-specific information and lists.</span></span> <span data-ttu-id="1d014-173">Кроме того, они хорошо подходят для обслуживания ответов от Bot к часто задаваемым вопросам (FAQ), поэтому пользователям не нужно запрашивать.</span><span class="sxs-lookup"><span data-stu-id="1d014-173">They’re also a good place to maintain bot responses to frequently-asked questions (FAQs) — so users don’t need to keep asking.</span></span>

### <a name="x2713-a-place-to-finish-a-conversation"></a><span data-ttu-id="1d014-174">&#x2713; места для завершения беседы</span><span class="sxs-lookup"><span data-stu-id="1d014-174">&#x2713; A place to finish a conversation</span></span>

<span data-ttu-id="1d014-175">Вы можете создать ссылку на вкладку в карточке.</span><span class="sxs-lookup"><span data-stu-id="1d014-175">You can link to a tab from a card.</span></span> <span data-ttu-id="1d014-176">Если у ленты есть ответ, для выполнения которого требуется еще несколько действий, можно создать ссылку на вкладку для выполнения задачи или процесса.</span><span class="sxs-lookup"><span data-stu-id="1d014-176">If your bot provides an answer that requires a few more steps, it can link to a tab to complete the task or flow.</span></span> <span data-ttu-id="1d014-177">Например, в ответ на "как форматировать iPhone?" хорошим ответом может быть карточка, которая описывает первые несколько шагов и имеет кнопку для *большего числа* действий, а затем предоставляет пользователю доступ к вкладке " *Справка* " ленты и детальным ссылкам на конкретные инструкции.</span><span class="sxs-lookup"><span data-stu-id="1d014-177">For instance, in response to, "How do I format my iPhone?", a good response might be a card which outlines the first few steps and has a button for *Show more* that then takes the user to the bot's *Help* tab and deep links to the specific instructions.</span></span>

### <a name="x2713-a-place-to-host-a-settings-page"></a><span data-ttu-id="1d014-178">&#x2713; места для размещения страницы параметров</span><span class="sxs-lookup"><span data-stu-id="1d014-178">&#x2713; A place to host a settings page</span></span>

<span data-ttu-id="1d014-179">Боты должен иметь некоторый пользовательский элемент управления.</span><span class="sxs-lookup"><span data-stu-id="1d014-179">Bots should have some user control.</span></span> <span data-ttu-id="1d014-180">Для многих Боты это разрешено через интерфейс Chat; Тем не менее, трудно запомнить эти параметры.</span><span class="sxs-lookup"><span data-stu-id="1d014-180">For many bots it is allowed through a chat interface; however, it's hard to remember those settings.</span></span> <span data-ttu-id="1d014-181">На вкладке Параметры можно отображать параметры пользователей, позволять пользователям менять их все одновременно, а также может быть хорошей точкой для более сложных пользовательских поведений.</span><span class="sxs-lookup"><span data-stu-id="1d014-181">A settings tab can display users settings, allow users to change them all at once, and may also be a good hand-off point for more complex bot custom behaviors.</span></span>

### <a name="x2713-a-place-to-provide-some-help"></a><span data-ttu-id="1d014-182">&#x2713; место для предоставления справки</span><span class="sxs-lookup"><span data-stu-id="1d014-182">&#x2713; A place to provide some help</span></span>

<span data-ttu-id="1d014-183">Добавление вкладки, в которой пользователи посвящены обмену данными с Bot.</span><span class="sxs-lookup"><span data-stu-id="1d014-183">Add a tab that educates users about how to communicate with your bot.</span></span> <span data-ttu-id="1d014-184">Вы можете предоставить некоторый контекст для того, что он делает или часто задаваемые вопросы.</span><span class="sxs-lookup"><span data-stu-id="1d014-184">You can provide some context for what it does or FAQs.</span></span>

![Предоставление справки](~/assets/images/framework/framework_bots_tbot-help.png)

> [!TIP]
> <span data-ttu-id="1d014-186">Внедрение частей сайта на вкладку поможет пользователям сохранить контекст беседы, когда они используют вашу службу.</span><span class="sxs-lookup"><span data-stu-id="1d014-186">Embedding parts of your site in a tab will help users maintain the context of a conversation as they use your service.</span></span> <span data-ttu-id="1d014-187">Он устраняет потребность в запуске службы в браузере и переключение между приложениями.</span><span class="sxs-lookup"><span data-stu-id="1d014-187">It removes the need to launch your service in a browser and switch back and forth between apps.</span></span>

---

## <a name="bots-in-channels"></a><span data-ttu-id="1d014-188">Боты в каналах</span><span class="sxs-lookup"><span data-stu-id="1d014-188">Bots in channels</span></span>

<span data-ttu-id="1d014-189">Вызов ленты в канале может осуществляться с помощью `@mention` .</span><span class="sxs-lookup"><span data-stu-id="1d014-189">Invoking a bot in a channel can be accomplished by `@mention`.</span></span> <span data-ttu-id="1d014-190">Диалоговое окно "bot" должно быть уникальным в случае каналов и групп vs. сценарии "один к одному", и в основном рекомендуется рассмотреть отдельные подходы.</span><span class="sxs-lookup"><span data-stu-id="1d014-190">Bot dialog should be unique in channels and groups vs. one-to-one scenarios and it's generally a good idea to consider separate approaches.</span></span> <span data-ttu-id="1d014-191">Это особенно справедливо в следующих случаях:</span><span class="sxs-lookup"><span data-stu-id="1d014-191">This is especially true in the following cases:</span></span>

### <a name="sensitive-data-sent-by-a-bot"></a><span data-ttu-id="1d014-192">Конфиденциальные данные, отправленные с помощью Bot</span><span class="sxs-lookup"><span data-stu-id="1d014-192">Sensitive data sent by a bot</span></span>

<span data-ttu-id="1d014-193">Хотя пользователи в команде могут быть известны службе, фактические роли пользователей не могут.</span><span class="sxs-lookup"><span data-stu-id="1d014-193">While the users in a team can be known to the service, the actual user roles cannot.</span></span> <span data-ttu-id="1d014-194">Это означает, что, например, в сценарии образования, включающем Буллинг, родительские контактные данные и контактные данные учащегося, не будут совместно использоваться в параметрах группы.</span><span class="sxs-lookup"><span data-stu-id="1d014-194">This means that, for example, in an education scenario involving bullying, parent and student contact information wouldn't be shared in a team setting.</span></span> <span data-ttu-id="1d014-195">Вместо этого сообщением в роботе может быть "два происшествия Буллинг сегодня", а также кнопка для отображения сведений.</span><span class="sxs-lookup"><span data-stu-id="1d014-195">Instead the bot's message might be,"Two bullying incidents occurred today" along with a button to show details.</span></span>

<span data-ttu-id="1d014-196">Запуск сведений на веб-странице или модуль задачи может запрашивать учетные данные пользователя или запросы к индексу для ролей пользователей, связанных с учетными записями AAD.</span><span class="sxs-lookup"><span data-stu-id="1d014-196">Launching details in a web page, or a task module can prompt for user credentials or query against an index for user roles paired with AAD accounts.</span></span> <span data-ttu-id="1d014-197">В обоих этих параметрах данные находятся в области личных представлений, и утечки данных не будут.</span><span class="sxs-lookup"><span data-stu-id="1d014-197">In both of these options the data is in a private view scope and there will be no data leakage.</span></span> <span data-ttu-id="1d014-198">Если одни и те же данные отправляются в сеансе "один к одному" между пользователем и Bot, данные отображаются только для пользователя в этом контексте и, таким образом, безопасны для полного отображения в сообщении Bot.</span><span class="sxs-lookup"><span data-stu-id="1d014-198">If the same data is sent in a one-to-one chat between a user and the bot, the data is only visible to the user in that context and is, therefore safe, to fully display in the bot message.</span></span> <span data-ttu-id="1d014-199">Следует избегать перехода от канала к разговору "один к одному", так как такая принудительная Навигация очень сильно нарушена.</span><span class="sxs-lookup"><span data-stu-id="1d014-199">Taking users from a channel to a one-to-one chat should be avoided however as that forced navigation is highly disruptive.</span></span>

### <a name="sending-cards-as-a-response-to-interactions"></a><span data-ttu-id="1d014-200">Отправка карточек в качестве ответа на диалоги</span><span class="sxs-lookup"><span data-stu-id="1d014-200">Sending cards as a response to interactions</span></span>

<span data-ttu-id="1d014-201">При отправке карточки обоймы в ответ на ознакомление с одним и тем же разговором по принципу "один к одному" в активном канале могут *воздействовать* десятки или сотни *обзоров* в активном канале с большим количеством пользователей.</span><span class="sxs-lookup"><span data-stu-id="1d014-201">While sending a carousel card in response to *Take a tour* in a one-to-one chat is perfectly acceptable, the same pattern could yield tens or hundreds of *tour carousels* in an active channel with lots of users.</span></span> <span data-ttu-id="1d014-202">Чтобы избежать этого, вторичные карточки должны размещаться в модуле задачи.</span><span class="sxs-lookup"><span data-stu-id="1d014-202">To avoid this, secondary cards should be hosted in a task module.</span></span> <span data-ttu-id="1d014-203">Этот шаблон позволяет пользователям в контексте канала поддерживать очистку канала от лишних откликов ленты и при необходимости рассматривает различные роли пользователей при отображении *обзора* .</span><span class="sxs-lookup"><span data-stu-id="1d014-203">This pattern keeps users in context with the channel, keeps the channel clean of excessive bot responses, and can optionally consider different user roles when the *tour* is shown.</span></span>

## <a name="useful-tips"></a><span data-ttu-id="1d014-204">Полезные советы</span><span class="sxs-lookup"><span data-stu-id="1d014-204">Useful tips</span></span>

### <a name="x2713-remember-bots-arent-assistants"></a><span data-ttu-id="1d014-205">&#x2713; Помните, что боты не помощники</span><span class="sxs-lookup"><span data-stu-id="1d014-205">&#x2713; Remember, bots aren’t assistants</span></span>

<span data-ttu-id="1d014-206">В отличие от агентов, например Кортаны, Боты выступает специалистами.</span><span class="sxs-lookup"><span data-stu-id="1d014-206">Unlike agents, e.g., Cortana, bots act as specialists.</span></span>

### <a name="x2713-discourage-chitchat"></a><span data-ttu-id="1d014-207">&#x2713; препятствовать читчат</span><span class="sxs-lookup"><span data-stu-id="1d014-207">&#x2713; Discourage chitchat</span></span>

<span data-ttu-id="1d014-208">Если ваш Bot не создан для беседы, Узнайте о способах перенаправления читчат к завершению задачи.</span><span class="sxs-lookup"><span data-stu-id="1d014-208">Unless your bot is built for conversation, find ways to redirect chitchat toward task completion.</span></span>

### <a name="x2713-introduce-some-personality"></a><span data-ttu-id="1d014-209">&#x2713; ввести некоторые личные данные</span><span class="sxs-lookup"><span data-stu-id="1d014-209">&#x2713; Introduce some personality</span></span>

<span data-ttu-id="1d014-210">Следите за тем, чтобы вы поделились с голосовым прозначением продукта.</span><span class="sxs-lookup"><span data-stu-id="1d014-210">Keep your bot personality consistent with the voice of your product.</span></span> <span data-ttu-id="1d014-211">Представьте себе, что вы говорите в своей компании.</span><span class="sxs-lookup"><span data-stu-id="1d014-211">Think of your bot as speaking for your company.</span></span>

### <a name="x2713-maintain-tone"></a><span data-ttu-id="1d014-212">&#x2713; обслуживание тонового набора</span><span class="sxs-lookup"><span data-stu-id="1d014-212">&#x2713; Maintain tone</span></span>

<span data-ttu-id="1d014-213">Определите, что ваш тон должен быть понятным и светлым, "только факты" или "супер случай".</span><span class="sxs-lookup"><span data-stu-id="1d014-213">Determine whether you want your tone to be friendly and light, “just the facts”, or super quirky.</span></span>

### <a name="x2713-encourage-easy-task-flow"></a><span data-ttu-id="1d014-214">&#x2713; упрощения процесса упрощения задач</span><span class="sxs-lookup"><span data-stu-id="1d014-214">&#x2713; Encourage easy task flow</span></span>

<span data-ttu-id="1d014-215">Поддержка взаимодействия с несколькими переворотами в то же время и разрешение на полностью сформированные вопросы.</span><span class="sxs-lookup"><span data-stu-id="1d014-215">Support multi-turn interactions while still allowing for fully formed questions.</span></span> <span data-ttu-id="1d014-216">Если предполагается, что следующий шаг позволит пользователям значительно упростить процесс перехода между потоками задач.</span><span class="sxs-lookup"><span data-stu-id="1d014-216">Anticipating the next step will help users get through task flows much easier.</span></span>

<span data-ttu-id="1d014-217">Если для выполнения задачи пользователь выполняет несколько действий, разрешите ему выполнить все действия, но закончите их быстрее.</span><span class="sxs-lookup"><span data-stu-id="1d014-217">If a user takes several steps to complete a task, allow your bot to take them through each step, but finish by having it suggest a quicker path.</span></span> <span data-ttu-id="1d014-218">Например, если пользователь запустил несколько бесед для установки собрания (сначала укажите собрание, а затем укажите, кому присвоено время, а затем — Дата дня), закончите беседу следующим предложением: в следующий раз попробуйте указать, можно ли планировать собрание с Бобом по адресу 1:00 завтра.</span><span class="sxs-lookup"><span data-stu-id="1d014-218">For example, if a user has taken several conversational turns to set a meeting (by first specifying a meeting, then identifying with whom, then stating the time, then stating the day), finish the conversation with the following suggestion: Next time, try asking if you can ‘schedule a meeting with Bob at 1:00 tomorrow’.</span></span>
