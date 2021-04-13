---
title: Точки входа для приложений Teams
author: heath-hamilton
description: В этой статье описано, где люди могут найти и использовать ваше приложение в Teams.
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: f61e5b5c05855c0a3a766920095cf46f699f08a6
ms.sourcegitcommit: 9404c2e3a30887b9e17e0c89b12dd26fd9b8033e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2021
ms.locfileid: "51654358"
---
# <a name="entry-points-for-teams-apps"></a><span data-ttu-id="f1630-103">Точки входа для приложений Teams</span><span class="sxs-lookup"><span data-stu-id="f1630-103">Entry points for Teams apps</span></span>

<span data-ttu-id="f1630-104">Платформа Teams предоставляет гибкий набор точек входа, таких как команда, канал и чат, где люди могут обнаружить и использовать ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="f1630-104">The Teams platform provides a flexible set of entry points, such as team, channel, and chat where people can discover and use your app.</span></span> <span data-ttu-id="f1630-105">Ваше приложение может быть таким же простым, как внедренный существующий веб-контент на вкладке или как многогранное приложение, с которым пользователи взаимодействуют в нескольких контекстах.</span><span class="sxs-lookup"><span data-stu-id="f1630-105">Your app can be as simple as embedding existing web content in a tab or a multi-faceted app that users interact with across several contexts.</span></span>
<span data-ttu-id="f1630-106">Наиболее успешные приложения являются родными для Teams, поэтому тщательно выберите точки входа вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="f1630-106">The most successful apps are native to Teams, so choose your app's entry points carefully.</span></span>

## <a name="shared-app-experiences"></a><span data-ttu-id="f1630-107">Общие впечатления от приложения</span><span class="sxs-lookup"><span data-stu-id="f1630-107">Shared app experiences</span></span>

<span data-ttu-id="f1630-108">Пространство для совместной работы — это пространство для команд, каналов и чатов.</span><span class="sxs-lookup"><span data-stu-id="f1630-108">Team, channel, and chat are collaboration spaces.</span></span> <span data-ttu-id="f1630-109">Приложения в этих контекстах доступны всем в этом пространстве.</span><span class="sxs-lookup"><span data-stu-id="f1630-109">Apps in these contexts are available to everyone in that space.</span></span> <span data-ttu-id="f1630-110">Пространства совместной работы обычно фокусируется на дополнительных процессах или на разблокирование новых социальных взаимодействий.</span><span class="sxs-lookup"><span data-stu-id="f1630-110">Collaboration spaces typically focus on additional workflows or unlocking new social interactions.</span></span>

<span data-ttu-id="f1630-111">В следующем списке показано, как возможности приложений Teams обычно используются в контекстах совместной работы:</span><span class="sxs-lookup"><span data-stu-id="f1630-111">The following list shows how Teams app capabilities are commonly used in collaborative contexts:</span></span>

* <span data-ttu-id="f1630-112">[**Вкладки**](~/tabs/what-are-tabs.md) предоставляют полноэкранный внедренный веб-интерфейс, настроенный для команды, канала или группового чата.</span><span class="sxs-lookup"><span data-stu-id="f1630-112">[**Tabs**](~/tabs/what-are-tabs.md) provide a full-screen embedded web experience configured for the team, channel, or group chat.</span></span> <span data-ttu-id="f1630-113">Все участники взаимодействуют с одним и тем же веб-контентом, поэтому типична одно-страничная возможность приложения без состояния.</span><span class="sxs-lookup"><span data-stu-id="f1630-113">All members interact with the same web-based content, so a stateless single-page app experience is typical.</span></span>

* <span data-ttu-id="f1630-114">[**Расширения для сообщений**](~/messaging-extensions/what-are-messaging-extensions.md) — это ярлыки для вставки внешнего содержимого в беседу или выполнения действий с сообщениями, не выходя из Teams.</span><span class="sxs-lookup"><span data-stu-id="f1630-114">[**Messaging extensions**](~/messaging-extensions/what-are-messaging-extensions.md) are shortcuts for inserting external content into a conversation or taking action on messages without leaving Teams.</span></span> <span data-ttu-id="f1630-115">[Разгрузка ссылок обеспечивает](~/messaging-extensions/how-to/link-unfurling.md) богатый контент при совместном использовании контента из общего URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="f1630-115">[Link unfurling](~/messaging-extensions/how-to/link-unfurling.md) provides rich content when sharing content from a common URL.</span></span>

* <span data-ttu-id="f1630-116">[**Боты**](~/bots/what-are-bots.md) взаимодействуют с участниками беседы с помощью чата и реагирования на события, такие как добавление нового участника или переименование канала.</span><span class="sxs-lookup"><span data-stu-id="f1630-116">[**Bots**](~/bots/what-are-bots.md) interact with members of the conversation through chat and responding to events, such as adding a new member or renaming a channel.</span></span> 
   > [!NOTE]
   > <span data-ttu-id="f1630-117">Беседы с ботом в этих контекстах видны всем членам команды, канала или группы, поэтому беседы ботов должны быть актуальны для всех.</span><span class="sxs-lookup"><span data-stu-id="f1630-117">Conversations with a bot in these contexts are visible to all members of the team, channel, or group, so bot conversations must be relevant to everyone.</span></span>

* <span data-ttu-id="f1630-118">[**Веб-перехватчики и соединители**](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) позволяют внешним службам публиковать сообщения в беседе, а пользователям — отправлять сообщения в службу.</span><span class="sxs-lookup"><span data-stu-id="f1630-118">[**Webhooks and connectors**](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) allow an external service to post messages into a conversation and users to send messages to a service.</span></span>

* <span data-ttu-id="f1630-119">[**REST API Microsoft Graph**](https://docs.microsoft.com/graph/teams-concept-overview) для получения данных о командах, каналах и групповых чатах, чтобы автоматизировать процессы Teams и управлять ими.</span><span class="sxs-lookup"><span data-stu-id="f1630-119">[**Microsoft Graph REST API**](https://docs.microsoft.com/graph/teams-concept-overview) for getting data about teams, channels, and group chats to help automate and manage Teams processes.</span></span>

## <a name="personal-app-experiences"></a><span data-ttu-id="f1630-120">Личные впечатления от приложения</span><span class="sxs-lookup"><span data-stu-id="f1630-120">Personal app experiences</span></span>

<span data-ttu-id="f1630-121">[Персональные приложения](../concepts/design/personal-apps.md) ориентированы на взаимодействие с одним пользователем.</span><span class="sxs-lookup"><span data-stu-id="f1630-121">[Personal apps](../concepts/design/personal-apps.md) focus on interactions with a single user.</span></span> <span data-ttu-id="f1630-122">Интерфейс в этом контексте уникален для каждого пользователя.</span><span class="sxs-lookup"><span data-stu-id="f1630-122">The experience in this context is unique to each user.</span></span>

<span data-ttu-id="f1630-123">В следующем списке показано, как возможности Teams обычно используются в личных контекстах:</span><span class="sxs-lookup"><span data-stu-id="f1630-123">The following list shows how Teams capabilities are commonly used in personal contexts:</span></span>

* <span data-ttu-id="f1630-124">[**Боты**](~/bots/what-are-bots.md) могут вести индивидуальные беседы с пользователем.</span><span class="sxs-lookup"><span data-stu-id="f1630-124">[**Bots**](~/bots/what-are-bots.md) have one-on-one conversations with a user.</span></span> <span data-ttu-id="f1630-125">Боты, требующие многоходовых бесед или предоставляющие уведомления, нужные только определенному пользователю, лучше всего подходят для личных приложений.</span><span class="sxs-lookup"><span data-stu-id="f1630-125">Bots that require multi-turn conversations or provide notifications relevant only to a specific user are best suited in personal apps.</span></span>

* <span data-ttu-id="f1630-126">[**Вкладки**](~/tabs/what-are-tabs.md) предоставляют встроенный полноэкранный веб-интерфейс, который имеет значение для пользователя, который смотрит на него.</span><span class="sxs-lookup"><span data-stu-id="f1630-126">[**Tabs**](~/tabs/what-are-tabs.md) provide a full-screen embedded web experience that is meaningful to the user looking at it.</span></span>

## <a name="see-also"></a><span data-ttu-id="f1630-127">См. также</span><span class="sxs-lookup"><span data-stu-id="f1630-127">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f1630-128">Инструкции по разработке приложений teams</span><span class="sxs-lookup"><span data-stu-id="f1630-128">Teams app design guidelines</span></span>](../concepts/design/design-teams-app-overview.md)

## <a name="next-step"></a><span data-ttu-id="f1630-129">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="f1630-129">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f1630-130">Понимание случаев использования</span><span class="sxs-lookup"><span data-stu-id="f1630-130">Understand use cases</span></span>](../concepts/design/understand-use-cases.md)
