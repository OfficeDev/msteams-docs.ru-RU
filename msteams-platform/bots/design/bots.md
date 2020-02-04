---
title: Рекомендации по проектированию для Боты
description: Описывает рекомендации по созданию Боты
keywords: рекомендации по проектированию Teams Справочник по платформе Боты
ms.openlocfilehash: f59a1e9c280f27567692b4d10341db79d05c3464
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675583"
---
# <a name="start-talking-with-bots"></a><span data-ttu-id="8192e-104">Начало беседы с Боты</span><span class="sxs-lookup"><span data-stu-id="8192e-104">Start talking with bots</span></span>

<span data-ttu-id="8192e-105">Боты — это беседы, которые выполняют узкий или определенный набор задач.</span><span class="sxs-lookup"><span data-stu-id="8192e-105">Bots are conversational apps that perform a narrow or specific set of tasks.</span></span> <span data-ttu-id="8192e-106">Они предоставляют возможность общаться с пользователями, отвечать на них, отвечать на свои вопросы и заблаговременно уведомлять об изменениях.</span><span class="sxs-lookup"><span data-stu-id="8192e-106">They give you an opportunity to communicate with users, respond to their questions, and proactively notify them about changes.</span></span> <span data-ttu-id="8192e-107">Это отличный способ достигать.</span><span class="sxs-lookup"><span data-stu-id="8192e-107">They’re a great way to reach out.</span></span>

---

## <a name="guidelines"></a><span data-ttu-id="8192e-108">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="8192e-108">Guidelines</span></span>

### <a name="avatars"></a><span data-ttu-id="8192e-109">Аватаров</span><span class="sxs-lookup"><span data-stu-id="8192e-109">Avatars</span></span>

<span data-ttu-id="8192e-110">Аватары в Teams создаются в виде шестиугольников, поэтому люди могут быстро сказать, что они говорят на Bot, а не человека.</span><span class="sxs-lookup"><span data-stu-id="8192e-110">Bot avatars in Teams are shaped like hexagons so people can quickly tell that they’re talking to a bot instead of a person.</span></span> <span data-ttu-id="8192e-111">Вы отправите свой аватар в виде квадрата, и мы обрезать его.</span><span class="sxs-lookup"><span data-stu-id="8192e-111">You’ll submit your avatar as a square and we’ll crop it for you.</span></span> <span data-ttu-id="8192e-112">Когда речь идет о аватарах, мы рекомендуем сделать их разборчиво от 2 метров и использовать более высокую контрастность.</span><span class="sxs-lookup"><span data-stu-id="8192e-112">When it comes to avatars, we recommend making yours legible from 2 feet away and using a higher contrast.</span></span>

[!include[Avatar image](~/includes/design/bot-avatar-image.html)]

### <a name="buttons"></a><span data-ttu-id="8192e-113">Кнопки</span><span class="sxs-lookup"><span data-stu-id="8192e-113">Buttons</span></span>

<span data-ttu-id="8192e-114">Поддерживается до шести кнопок для одной карточки.</span><span class="sxs-lookup"><span data-stu-id="8192e-114">We support up to six buttons per card.</span></span> <span data-ttu-id="8192e-115">Будьте лаконичны при написании текста на кнопке и имейте в виду, что большинство кнопок должно только самостоятельно обращаться к задачам.</span><span class="sxs-lookup"><span data-stu-id="8192e-115">Be concise when writing button text, and keep in mind that most buttons should only address the task at hand.</span></span>

### <a name="graphics"></a><span data-ttu-id="8192e-116">Картин</span><span class="sxs-lookup"><span data-stu-id="8192e-116">Graphics</span></span>

<span data-ttu-id="8192e-117">Рисунки — это хороший способ сказать, что не все роботы для ленты должны иметь графический объект, поэтому их следует использовать для достижения максимальной влияния.</span><span class="sxs-lookup"><span data-stu-id="8192e-117">Graphics are a good way to tell a story, but not all bot conversations require graphics, so use them for maximum impact.</span></span>

### <a name="responding-to-users-and-failing-gracefully"></a><span data-ttu-id="8192e-118">Реагирование на пользователей и неправильное отработка отказа</span><span class="sxs-lookup"><span data-stu-id="8192e-118">Responding to users and failing gracefully</span></span>

<span data-ttu-id="8192e-119">Ваш робот должен также отвечать на такие вещи, как "Hi", "Справка" и "Спасибо", при этом учитывается распространенные опечатки и коллокуиалисмс.</span><span class="sxs-lookup"><span data-stu-id="8192e-119">Your bot should also be able to respond to things like 'Hi', 'Help', and 'Thanks' while taking common misspellings and colloquialisms into account.</span></span> <span data-ttu-id="8192e-120">Пример:</span><span class="sxs-lookup"><span data-stu-id="8192e-120">For example:</span></span>

#### <a name="x2713-hello"></a><span data-ttu-id="8192e-121">&#x2713; Hello</span><span class="sxs-lookup"><span data-stu-id="8192e-121">&#x2713; Hello</span></span>

<span data-ttu-id="8192e-122">`Hi` `how are you` `howdy`</span><span class="sxs-lookup"><span data-stu-id="8192e-122">`Hi` `how are you` `howdy`</span></span>

#### <a name="x2713-help"></a><span data-ttu-id="8192e-123">Справка по &#x2713;</span><span class="sxs-lookup"><span data-stu-id="8192e-123">&#x2713; Help</span></span>

<span data-ttu-id="8192e-124">`What do you do?` `How does this work?` `What the heck?`</span><span class="sxs-lookup"><span data-stu-id="8192e-124">`What do you do?` `How does this work?` `What the heck?`</span></span>

#### <a name="x2713-thanks"></a><span data-ttu-id="8192e-125">&#x2713; Спасибо</span><span class="sxs-lookup"><span data-stu-id="8192e-125">&#x2713; Thanks</span></span>

<span data-ttu-id="8192e-126">`Thank you` `thankyou` `thx`</span><span class="sxs-lookup"><span data-stu-id="8192e-126">`Thank you` `thankyou` `thx`</span></span>

<span data-ttu-id="8192e-127">Ваш робот должен иметь возможность обрабатывать следующие типы запросов и входных данных:</span><span class="sxs-lookup"><span data-stu-id="8192e-127">Your bot should be able to handle the following types of queries and inputs:</span></span>

* <span data-ttu-id="8192e-128">**Распознанные вопросы**: это "наиболее подходящий сценарий" для пользователей.</span><span class="sxs-lookup"><span data-stu-id="8192e-128">**Recognized questions**: These are the “best case scenario” questions you’d anticipate from users.</span></span>
* <span data-ttu-id="8192e-129">**Распознанные невопросы**: запросы о неподдерживаемых функциях, случайных сведениях о неподдерживаемых возможностях, или, если кто-то хочет выполнить рекурсивный поиск в Bot.</span><span class="sxs-lookup"><span data-stu-id="8192e-129">**Recognized non-questions**: Queries about unsupported functionality, random pieces of information, or when someone wants to curse at your bot.</span></span>
* <span data-ttu-id="8192e-130">**Нераспознанные вопросы**: нечитаемые входные данные (например, гиббериш).</span><span class="sxs-lookup"><span data-stu-id="8192e-130">**Unrecognized questions**: Unintelligible inputs (i.e., gibberish).</span></span>

<span data-ttu-id="8192e-131">Примеры типов индивидуальной и отклика для ленты:</span><span class="sxs-lookup"><span data-stu-id="8192e-131">Examples of bot personality and response types:</span></span>

[!include[Bot responses](~/includes/design/bot-responses-table.html)]

> [!TIP]
> <span data-ttu-id="8192e-132">Когда вы пишете свой сценарий, запросите себя: "будет ли моя фирма извредна, если ответ будет получен и общий?"</span><span class="sxs-lookup"><span data-stu-id="8192e-132">When writing your bot script, ask yourself: “Will my company be embarrassed if a response is screen captured and shared?”</span></span>

### <a name="understanding-what-users-are-trying-to-say"></a><span data-ttu-id="8192e-133">Общие сведения о том, что пользователи пытаются сказать</span><span class="sxs-lookup"><span data-stu-id="8192e-133">Understanding what users are trying to say</span></span>

#### <a name="use-a-thesaurus-for-synonyms"></a><span data-ttu-id="8192e-134">Использование тезауруса для синонимов</span><span class="sxs-lookup"><span data-stu-id="8192e-134">Use a thesaurus for synonyms</span></span>

<span data-ttu-id="8192e-135">При мозговых задолженностей Используйте тезаурус и получите людей от максимально возможного количества фоновых рисунков, чтобы вы могли создавать различные интерпретации каждого запроса.</span><span class="sxs-lookup"><span data-stu-id="8192e-135">When brainstorming variants, use a thesaurus and get people from as many different backgrounds as possible to help you generate different interpretations of each query.</span></span>

#### <a name="make-use-of-telemetry-and-interviews"></a><span data-ttu-id="8192e-136">Использование телеметрии и интервью</span><span class="sxs-lookup"><span data-stu-id="8192e-136">Make use of telemetry and interviews</span></span>

<span data-ttu-id="8192e-137">Сведения о том, что говорят пользователи, и каковы их цели при опросе ленты.</span><span class="sxs-lookup"><span data-stu-id="8192e-137">Find out what users are saying and what was their intent when querying your bot.</span></span> <span data-ttu-id="8192e-138">Это будет непрерывный процесс, когда вы получаете пользователей в различных местоположениях и типах компаний.</span><span class="sxs-lookup"><span data-stu-id="8192e-138">This will be an ongoing process as you get users in different locations and types of companies.</span></span> <span data-ttu-id="8192e-139">Вы можете выполнить тонкую настройку распознавания языка и соответствия намерения языку интеллектуальной службы ([Луис](/azure/cognitive-services/luis/what-is-luis)).</span><span class="sxs-lookup"><span data-stu-id="8192e-139">You can fine-tune language recognition and intent mapping with Language Understanding Intelligent Service ([LUIS](/azure/cognitive-services/luis/what-is-luis)).</span></span>

### <a name="how-often-should-you-use-your-bot-to-reach-out-to-a-user"></a><span data-ttu-id="8192e-140">Как часто следует использовать ваш Bot для доступа к пользователю?</span><span class="sxs-lookup"><span data-stu-id="8192e-140">How often should you use your bot to reach out to a user?</span></span>

#### <a name="x2713-when-a-state-has-changed"></a><span data-ttu-id="8192e-141">&#x2713; при изменении состояния</span><span class="sxs-lookup"><span data-stu-id="8192e-141">&#x2713; When a state has changed</span></span>

<span data-ttu-id="8192e-142">Например, если назначение помечено как завершенное, при изменении ошибки, при появления новых социальных сетей или при завершении опроса.</span><span class="sxs-lookup"><span data-stu-id="8192e-142">For example, if an assignment is marked as complete, when a bug changes, when new social media is available, or when a poll has been completed.</span></span>

#### <a name="x2713-when-the-timing-is-right"></a><span data-ttu-id="8192e-143">&#x2713;, когда выполняется правильная продолжительность</span><span class="sxs-lookup"><span data-stu-id="8192e-143">&#x2713; When the timing is right</span></span>

<span data-ttu-id="8192e-144">Ваш Bot может вести себя как ежедневный дайджест, отправляя уведомление пользователю или каналу по определенной частоте.</span><span class="sxs-lookup"><span data-stu-id="8192e-144">Your bot can act like a daily digest, sending a notification to the user or channel at a specific frequency.</span></span>

<span data-ttu-id="8192e-145">Оставить пользователя в элементе управления.</span><span class="sxs-lookup"><span data-stu-id="8192e-145">Leave the user in control.</span></span> <span data-ttu-id="8192e-146">Предоставьте параметры уведомлений, которые включают частоту и приоритет.</span><span class="sxs-lookup"><span data-stu-id="8192e-146">Provide notification settings that include frequency and priority.</span></span>

[!include[Bot notification](~/includes/design/bot-notification-image.html)]

---

## <a name="using-tabs"></a><span data-ttu-id="8192e-147">Использование вкладок</span><span class="sxs-lookup"><span data-stu-id="8192e-147">Using tabs</span></span>

<span data-ttu-id="8192e-148">С помощью вкладок вы намерены, чтобы использовать роботы.</span><span class="sxs-lookup"><span data-stu-id="8192e-148">Tabs make your bot much more functional.</span></span> <span data-ttu-id="8192e-149">С помощью вкладок можно создавать следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="8192e-149">With tabs, you can create the following:</span></span>

### <a name="x2713-a-place-to-host-standing-queries"></a><span data-ttu-id="8192e-150">&#x2713; места для размещения зафиксированных запросов</span><span class="sxs-lookup"><span data-stu-id="8192e-150">&#x2713; A place to host standing queries</span></span>

<span data-ttu-id="8192e-151">В личных беседах между Bot и одним человеком на вкладках могут быть размещены сведения и списки, относящиеся к пользователю.</span><span class="sxs-lookup"><span data-stu-id="8192e-151">In personal conversations between a bot and a single person, tabs can house user-specific information and lists.</span></span> <span data-ttu-id="8192e-152">Кроме того, они хорошо подходят для обслуживания ответов от Bot к часто задаваемым вопросам (FAQ), поэтому пользователям не нужно запрашивать.</span><span class="sxs-lookup"><span data-stu-id="8192e-152">They’re also a good place to maintain bot responses to frequently-asked questions (FAQs) — so users don’t need to keep asking.</span></span>

### <a name="x2713-a-place-to-finish-a-conversation"></a><span data-ttu-id="8192e-153">&#x2713; места для завершения беседы</span><span class="sxs-lookup"><span data-stu-id="8192e-153">&#x2713; A place to finish a conversation</span></span>

<span data-ttu-id="8192e-154">Вы можете создать ссылку на вкладку в карточке.</span><span class="sxs-lookup"><span data-stu-id="8192e-154">You can link to a tab from a card.</span></span> <span data-ttu-id="8192e-155">Если у ленты есть ответ, для выполнения которого требуется еще несколько действий, можно создать ссылку на вкладку для выполнения задачи или процесса.</span><span class="sxs-lookup"><span data-stu-id="8192e-155">If your bot provides an answer that requires a few more steps, it can link to a tab to complete the task or flow.</span></span>

### <a name="x2713-a-place-to-provide-some-help"></a><span data-ttu-id="8192e-156">&#x2713; место для предоставления справки</span><span class="sxs-lookup"><span data-stu-id="8192e-156">&#x2713; A place to provide some help</span></span>

<span data-ttu-id="8192e-157">Добавление вкладки, в которой пользователи посвящены обмену данными с Bot.</span><span class="sxs-lookup"><span data-stu-id="8192e-157">Add a tab that educates users about how to communicate with your bot.</span></span> <span data-ttu-id="8192e-158">Вы можете предоставить некоторый контекст для того, что он делает или часто задаваемые вопросы.</span><span class="sxs-lookup"><span data-stu-id="8192e-158">You can provide some context for what it does or FAQs.</span></span>

![Предоставление справки](~/assets/images/framework/framework_bots_tbot-help.png)

> [!TIP]
> <span data-ttu-id="8192e-160">Внедрение частей сайта на вкладке поможет другим пользователям поддерживать контекст беседы, когда они используют службу.</span><span class="sxs-lookup"><span data-stu-id="8192e-160">Embedding parts of your site in a tab will help someone maintain the context of a conversation as they use your service.</span></span> <span data-ttu-id="8192e-161">Он устраняет потребность в запуске службы в браузере и переключение между приложениями.</span><span class="sxs-lookup"><span data-stu-id="8192e-161">It removes the need to launch your service in a browser and switch back and forth between apps.</span></span>

---

## <a name="best-practices"></a><span data-ttu-id="8192e-162">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="8192e-162">Best practices</span></span>

### <a name="x2713-bots-arent-assistants"></a><span data-ttu-id="8192e-163">&#x2713; Боты не отображаются помощниками</span><span class="sxs-lookup"><span data-stu-id="8192e-163">&#x2713; Bots aren’t assistants</span></span>

<span data-ttu-id="8192e-164">В отличие от агентов, например Кортаны, Боты выступает специалистами.</span><span class="sxs-lookup"><span data-stu-id="8192e-164">Unlike agents, e.g., Cortana, bots act as specialists.</span></span>

### <a name="x2713-discourage-chitchat"></a><span data-ttu-id="8192e-165">&#x2713; препятствовать читчат</span><span class="sxs-lookup"><span data-stu-id="8192e-165">&#x2713; Discourage chitchat</span></span>

<span data-ttu-id="8192e-166">Если ваш Bot не создан для беседы, Узнайте о способах перенаправления читчат к завершению задачи.</span><span class="sxs-lookup"><span data-stu-id="8192e-166">Unless your bot is built for conversation, find ways to redirect chitchat toward task completion.</span></span>

### <a name="x2713-introduce-some-personality"></a><span data-ttu-id="8192e-167">&#x2713; ввести некоторые личные данные</span><span class="sxs-lookup"><span data-stu-id="8192e-167">&#x2713; Introduce some personality</span></span>

<span data-ttu-id="8192e-168">Следите за тем, чтобы вы поделились с голосовым прозначением продукта.</span><span class="sxs-lookup"><span data-stu-id="8192e-168">Keep your bot personality consistent with the voice of your product.</span></span> <span data-ttu-id="8192e-169">Представьте себе, что вы говорите в своей компании.</span><span class="sxs-lookup"><span data-stu-id="8192e-169">Think of your bot as speaking for your company.</span></span>

### <a name="x2713-maintain-tone"></a><span data-ttu-id="8192e-170">&#x2713; обслуживание тонового набора</span><span class="sxs-lookup"><span data-stu-id="8192e-170">&#x2713; Maintain tone</span></span>

<span data-ttu-id="8192e-171">Определите, что ваш тон должен быть понятным и светлым, "только факты" или "супер случай".</span><span class="sxs-lookup"><span data-stu-id="8192e-171">Determine whether you want your tone to be friendly and light, “just the facts”, or super quirky.</span></span>

### <a name="x2713-encourage-easy-task-flow"></a><span data-ttu-id="8192e-172">&#x2713; упрощения процесса упрощения задач</span><span class="sxs-lookup"><span data-stu-id="8192e-172">&#x2713; Encourage easy task flow</span></span>

<span data-ttu-id="8192e-173">Поддержка взаимодействия с несколькими переворотами в то же время и разрешение на полностью сформированные вопросы.</span><span class="sxs-lookup"><span data-stu-id="8192e-173">Support multi-turn interactions while still allowing for fully formed questions.</span></span> <span data-ttu-id="8192e-174">Если предполагается, что следующий шаг позволит пользователям значительно упростить процесс перехода между потоками задач.</span><span class="sxs-lookup"><span data-stu-id="8192e-174">Anticipating the next step will help users get through task flows much easier.</span></span>

<span data-ttu-id="8192e-175">Если для выполнения задачи пользователь выполняет несколько действий, разрешите ему выполнить все действия, но закончите их быстрее.</span><span class="sxs-lookup"><span data-stu-id="8192e-175">If a user takes several steps to complete a task, allow your bot to take them through each step, but finish by having it suggest a quicker path.</span></span> <span data-ttu-id="8192e-176">Например, если пользователь применяет несколько бесед для установки собрания (сначала укажите собрание, а затем укажите, кому присвоено время, а затем укажите дату), закончите беседу следующим предложением: следующий раз, попробуйте может "запланировать собрание с Бобом по адресу 1:00 завтра".</span><span class="sxs-lookup"><span data-stu-id="8192e-176">For example, if a user has taken several conversational turns to set a meeting (by first specifying a meeting, then identifying with whom, then stating the time, then stating the day), finish the conversation with the following suggestion: Next time, try asking if you can ‘schedule a meeting with Bob at 1:00 tomorrow’.</span></span>