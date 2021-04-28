---
title: Боты в Microsoft Teams
author: clearab
description: Обзор ботов в Microsoft Teams.
ms.topic: overview
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 9ba7b6b96a8cbd55fac968975794d7c41d57f514
ms.sourcegitcommit: a732789190f59ec1f3699e8ad2f06387e8fe1458
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/27/2021
ms.locfileid: "52058497"
---
# <a name="bots-in-microsoft-teams"></a><span data-ttu-id="f70d1-103">Боты в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="f70d1-103">Bots in Microsoft Teams</span></span>

<span data-ttu-id="f70d1-104">Бот, также именуемый чат-ботом или чат-ботом, — это приложение, которое выполняет простые и повторяющиеся автоматические задачи, выполняемые пользователями, такими как служба поддержки или служба поддержки.</span><span class="sxs-lookup"><span data-stu-id="f70d1-104">A bot also referred to as a chatbot or conversational bot is an app that runs simple and repetitive automated tasks performed by the users, such as customer service or support staff.</span></span> <span data-ttu-id="f70d1-105">Примеры ботов в повседневном использовании включают боты, которые предоставляют сведения о погоде, делают резервирование на обед или предоставляют сведения о путешествиях.</span><span class="sxs-lookup"><span data-stu-id="f70d1-105">Examples of bots in everyday use include, bots that provide information about the weather, make dinner reservations, or provide travel information.</span></span> <span data-ttu-id="f70d1-106">Взаимодействие бота может быть быстрым вопросом и ответом, или это может быть сложный разговор, который предоставляет доступ к службам.</span><span class="sxs-lookup"><span data-stu-id="f70d1-106">A bot interaction can be a quick question and answer, or it can be a complex conversation that provides access to services.</span></span>

> [!VIDEO https://www.youtube-nocookie.com/embed/zSIysk0yL0Q]

<span data-ttu-id="f70d1-107">Боты для общения позволяют пользователям взаимодействовать с веб-службой с помощью текста, интерактивных карт и модулей задач.</span><span class="sxs-lookup"><span data-stu-id="f70d1-107">Conversational bots allow users to interact with your web service through text, interactive cards, and task modules.</span></span>

![Вызов бота с помощью текста](~/assets/images/invokebotwithtext.png)

![Вызов бота с помощью карты](~/assets/images/invokebotwithcard.png)

<img src="~/assets/images/task-module-example.png" alt="Invoke bot using task module" width="400"/>

<span data-ttu-id="f70d1-110">Диалоговые боты невероятно гибки и могут быть масштабными для обработки нескольких простых команд или сложных задач с питанием от искусственного интеллекта и обработки на естественном языке.</span><span class="sxs-lookup"><span data-stu-id="f70d1-110">Conversational bots are incredibly flexible and can be scoped to handle a few simple commands, or complex, artificial-intelligence-powered, and natural-language-processing tasks.</span></span> <span data-ttu-id="f70d1-111">Они могут быть одним из аспектов более крупного приложения или полностью автономными.</span><span class="sxs-lookup"><span data-stu-id="f70d1-111">They can be one aspect of a larger application, or be completely stand-alone.</span></span>

<span data-ttu-id="f70d1-112">Поиск правильного сочетания модулей карт, текста и задач — это ключ к созданию полезного бота.</span><span class="sxs-lookup"><span data-stu-id="f70d1-112">Finding the right mix of cards, text, and task modules are key to create a useful bot.</span></span> <span data-ttu-id="f70d1-113">На следующем изображении показан пользователь, беседующий с ботом в чате один к одному с помощью текстовых и интерактивных карт:</span><span class="sxs-lookup"><span data-stu-id="f70d1-113">The following image shows a user conversing with a bot in a one-to-one chat using both, text and interactive cards:</span></span>

:::image type="content" source="~/assets/images/FAQPlusEndUser.gif" alt-text="Пример бота faQ" border="true":::

<span data-ttu-id="f70d1-115">Каждое взаимодействие между пользователем и ботом представлено как действие.</span><span class="sxs-lookup"><span data-stu-id="f70d1-115">Every interaction between the user and the bot is represented as an activity.</span></span> <span data-ttu-id="f70d1-116">Когда бот получает действие, он передает его обработчику действий.</span><span class="sxs-lookup"><span data-stu-id="f70d1-116">When a bot receives an activity, it passes it on to its activity handlers.</span></span> <span data-ttu-id="f70d1-117">Дополнительные сведения см. в [том, как обработчики действий ботов.](~/bots/bot-basics.md)</span><span class="sxs-lookup"><span data-stu-id="f70d1-117">For more information, see [bot activity handlers](~/bots/bot-basics.md).</span></span> 

<span data-ttu-id="f70d1-118">Кроме того, боты — это приложения, которые имеют разговорный интерфейс.</span><span class="sxs-lookup"><span data-stu-id="f70d1-118">In addition, bots are apps that have a conversational interface.</span></span> <span data-ttu-id="f70d1-119">Вы можете взаимодействовать с ботом с помощью текстовых, интерактивных карт и речи.</span><span class="sxs-lookup"><span data-stu-id="f70d1-119">You can interact with a bot using text, interactive cards, and speech.</span></span> <span data-ttu-id="f70d1-120">Бот ведет себя по-разному в зависимости от того, является ли беседа каналом или групповой беседой, или это беседа один к одному.</span><span class="sxs-lookup"><span data-stu-id="f70d1-120">A bot behaves differently depending on whether the conversation is a channel or group chat conversation, or it is a one-to-one conversation.</span></span> <span data-ttu-id="f70d1-121">Беседы обрабатываются через соединители Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="f70d1-121">Conversations are handled through the Bot Framework connector.</span></span> <span data-ttu-id="f70d1-122">Дополнительные сведения см. в основных [сведениях.](~/bots/how-to/conversations/conversation-basics.md)</span><span class="sxs-lookup"><span data-stu-id="f70d1-122">For more information, see [conversation basics](~/bots/how-to/conversations/conversation-basics.md).</span></span>

<span data-ttu-id="f70d1-123">Для доступа к соответствующему контенту и улучшения работы с ботом требуется контекстная информация, например сведения о профиле пользователя.</span><span class="sxs-lookup"><span data-stu-id="f70d1-123">Your bot requires contextual information, such as user profile details to access relevant content and enhance the bot experience.</span></span> <span data-ttu-id="f70d1-124">Дополнительные сведения см. в [контексте Teams.](~/bots/how-to/get-teams-context.md)</span><span class="sxs-lookup"><span data-stu-id="f70d1-124">For more information, see [get Teams context](~/bots/how-to/get-teams-context.md).</span></span> 

<span data-ttu-id="f70d1-125">Вы также можете отправлять и получать файлы через бот с помощью API Graph или API-API-бота Teams.</span><span class="sxs-lookup"><span data-stu-id="f70d1-125">You can also send and receive files through the bot using Graph APIs or Teams bot APIs.</span></span> <span data-ttu-id="f70d1-126">Дополнительные сведения см. в [материалах отправки и получения файлов через бот.](~/bots/how-to/bots-filesv4.md)</span><span class="sxs-lookup"><span data-stu-id="f70d1-126">For more information, see [send and receive files through the bot](~/bots/how-to/bots-filesv4.md).</span></span>

<span data-ttu-id="f70d1-127">Кроме того, ограничение скорости используется для оптимизации ботов, используемых для приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="f70d1-127">In addition, rate limiting is used to optimize bots used for your Teams application.</span></span> <span data-ttu-id="f70d1-128">Для защиты Microsoft Teams и ее пользователей API-бота предоставляют ограничение скорости для входящих запросов.</span><span class="sxs-lookup"><span data-stu-id="f70d1-128">To protect Microsoft Teams and its users, the bot APIs provide a rate limit for incoming requests.</span></span> <span data-ttu-id="f70d1-129">Дополнительные сведения см. в [дополнительных сведениях об оптимизации бота с ограничением скорости в Teams.](~/bots/how-to/rate-limit.md)</span><span class="sxs-lookup"><span data-stu-id="f70d1-129">For more information, see [optimize your bot with rate limiting in Teams](~/bots/how-to/rate-limit.md).</span></span>

<span data-ttu-id="f70d1-130">С помощью API Microsoft Graph для звонков и собраний в Интернете приложения Microsoft Teams теперь могут взаимодействовать с пользователями с помощью голосовых и видеосвязи.</span><span class="sxs-lookup"><span data-stu-id="f70d1-130">With Microsoft Graph APIs for calls and online meetings, Microsoft Teams apps can now interact with users using voice and video.</span></span> <span data-ttu-id="f70d1-131">Дополнительные сведения см. в [ботах вызовов и собраний.](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)</span><span class="sxs-lookup"><span data-stu-id="f70d1-131">For more information, see [calls and meetings bots](~/bots/calls-and-meetings/calls-meetings-bots-overview.md).</span></span> 

<span data-ttu-id="f70d1-132">Вы можете использовать API бота Teams для получения сведений для одного или более членов чата или группы.</span><span class="sxs-lookup"><span data-stu-id="f70d1-132">You can use the Teams bot APIs to get information for one or more members of a chat or team.</span></span> <span data-ttu-id="f70d1-133">Дополнительные сведения см. в дополнительных сведениях об изменениях [API-API бота Teams для получения участников группы или чата.](~/resources/team-chat-member-api-changes.md)</span><span class="sxs-lookup"><span data-stu-id="f70d1-133">For more information, see [changes to Teams bot APIs for fetching team or chat members](~/resources/team-chat-member-api-changes.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="f70d1-134">См. также</span><span class="sxs-lookup"><span data-stu-id="f70d1-134">See also</span></span>

- [<span data-ttu-id="f70d1-135">Создать бота для Teams</span><span class="sxs-lookup"><span data-stu-id="f70d1-135">Create a bot for Teams</span></span>](~/bots/how-to/create-a-bot-for-teams.md)

## <a name="next-step"></a><span data-ttu-id="f70d1-136">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="f70d1-136">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f70d1-137">Боты и пакеты SDK</span><span class="sxs-lookup"><span data-stu-id="f70d1-137">Bots and SDKs</span></span>](~/bots/bot-features.md)
