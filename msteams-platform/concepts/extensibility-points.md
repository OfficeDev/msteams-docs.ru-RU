---
title: Точки входа для приложений Teams
author: heath-hamilton
description: В этой статье описано, где люди могут найти и использовать ваше приложение в Teams.
ms.topic: conceptual
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 72ce2620160f854bbe458821db01e91d2d9f62cd
ms.sourcegitcommit: 098d38dd947e87e69d289b99e807bea2d95c42f9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/18/2020
ms.locfileid: "49713629"
---
# <a name="entry-points-for-teams-apps"></a><span data-ttu-id="e0572-103">Точки входа для приложений Teams</span><span class="sxs-lookup"><span data-stu-id="e0572-103">Entry points for Teams apps</span></span>

<span data-ttu-id="e0572-104">Платформа Teams предоставляет гибкий набор точек входа, где люди могут обнаружить и использовать ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="e0572-104">The Teams platform provides a flexible set of entry points where people can discover and use your app.</span></span> <span data-ttu-id="e0572-105">Ваше приложение может быть таким же простым, как внедренный существующий веб-контент на вкладке или как многогранное приложение, с которым пользователи взаимодействуют в нескольких контекстах.</span><span class="sxs-lookup"><span data-stu-id="e0572-105">Your app can be as simple as embedding existing web content in a tab or a multi-faceted app that users interact with across several contexts.</span></span>

<span data-ttu-id="e0572-106">Наиболее успешные приложения похожи на собственные приложения Teams, поэтому важно тщательно спланировать точки входа приложения.</span><span class="sxs-lookup"><span data-stu-id="e0572-106">The most successful apps feel native to Teams, so it's important to carefully plan your app's entry points.</span></span>

## <a name="teams-channels-and-chats"></a><span data-ttu-id="e0572-107">Команды, каналы и чаты</span><span class="sxs-lookup"><span data-stu-id="e0572-107">Teams, channels, and chats</span></span>

<span data-ttu-id="e0572-108">Команды, каналы и чаты — это пространства для совместной работы.</span><span class="sxs-lookup"><span data-stu-id="e0572-108">Teams, channels, and chats are collaboration spaces.</span></span> <span data-ttu-id="e0572-109">Приложения в этих контекстах доступны всем в этом пространстве и обычно предназначены для дополнительных рабочих процессов или разблокировки новых социальных взаимодействий.</span><span class="sxs-lookup"><span data-stu-id="e0572-109">Apps in these contexts are available to everyone in that space and typically focus on additional workflows or unlocking new social interactions.</span></span>

<span data-ttu-id="e0572-110">Вот как возможности приложений Teams часто используются в контекстах совместной работы:</span><span class="sxs-lookup"><span data-stu-id="e0572-110">Here's how Teams app capabilities are commonly used in collaborative contexts:</span></span>

* <span data-ttu-id="e0572-111">[**Вкладки**](~/tabs/what-are-tabs.md) предоставляют полноэкранный внедренный веб-интерфейс, настроенный для команды, канала или группового чата.</span><span class="sxs-lookup"><span data-stu-id="e0572-111">[**Tabs**](~/tabs/what-are-tabs.md) provide a full-screen embedded web experience configured for the team, channel, or group chat.</span></span> <span data-ttu-id="e0572-112">Все участники взаимодействуют в одном веб-контенте, поэтому обычно используется одностраничное приложение без сохранения состояния.</span><span class="sxs-lookup"><span data-stu-id="e0572-112">All members interact with the same web-based content, so a stateless single page app experience is typical.</span></span>

* <span data-ttu-id="e0572-113">[**Расширения для сообщений**](~/messaging-extensions/what-are-messaging-extensions.md) — это ярлыки для вставки внешнего содержимого в беседу или выполнения действий с сообщениями, не выходя из Teams.</span><span class="sxs-lookup"><span data-stu-id="e0572-113">[**Messaging extensions**](~/messaging-extensions/what-are-messaging-extensions.md) are shortcuts for inserting external content into a conversation or taking action on messages without leaving Teams.</span></span> <span data-ttu-id="e0572-114">Развертывание ссылок обеспечивает форматированное содержимое при совместном использовании контента с общего URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="e0572-114">Link unfurling provides rich content when sharing content from a common URL.</span></span>

* <span data-ttu-id="e0572-115">[**Боты**](~/bots/what-are-bots.md) взаимодействуют с участниками беседы через чат и реагируют на события (например, путем добавления нового участника или переименования канала).</span><span class="sxs-lookup"><span data-stu-id="e0572-115">[**Bots**](~/bots/what-are-bots.md) interact with members of the conversation through chat and responding to events (like adding a new member or renaming a channel).</span></span> <span data-ttu-id="e0572-116">Беседы с ботом в этих контекстах видны всем участникам команды, канала или группы, поэтому беседы с ботом должны быть актуальны для всех.</span><span class="sxs-lookup"><span data-stu-id="e0572-116">Conversations with a bot in these contexts are visible to all members of the team, channel, or group, so bot conversations should be relevant to everyone.</span></span>

* <span data-ttu-id="e0572-117">[**Веб-перехватчики и соединители**](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) позволяют внешним службам публиковать сообщения в беседе, а пользователям — отправлять сообщения в службу.</span><span class="sxs-lookup"><span data-stu-id="e0572-117">[**Webhooks and connectors**](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) allow an external service to post messages into a conversation and users to send messages to a service.</span></span>

* <span data-ttu-id="e0572-118">[**REST API Microsoft Graph**](https://docs.microsoft.com/graph/teams-concept-overview) для получения данных о командах, каналах и групповых чатах, чтобы автоматизировать процессы Teams и управлять ими.</span><span class="sxs-lookup"><span data-stu-id="e0572-118">[**Microsoft Graph REST API**](https://docs.microsoft.com/graph/teams-concept-overview) for getting data about teams, channels, and group chats to help automate and manage Teams processes.</span></span>

## <a name="personal-apps"></a><span data-ttu-id="e0572-119">Персональные приложения</span><span class="sxs-lookup"><span data-stu-id="e0572-119">Personal apps</span></span>

<span data-ttu-id="e0572-120">[Персональные приложения](~/concepts/design/personal-apps.md) ориентированы на взаимодействие с одним пользователем.</span><span class="sxs-lookup"><span data-stu-id="e0572-120">[Personal apps](~/concepts/design/personal-apps.md) focus on interactions with a single user.</span></span> <span data-ttu-id="e0572-121">Интерфейс в этом контексте уникален для каждого пользователя.</span><span class="sxs-lookup"><span data-stu-id="e0572-121">The experience in this context is unique to each user.</span></span>

<span data-ttu-id="e0572-122">Вот как возможности Teams часто используются в персональных контекстах:</span><span class="sxs-lookup"><span data-stu-id="e0572-122">Here's how Teams capabilities are commonly used in personal contexts:</span></span>

* <span data-ttu-id="e0572-123">[**Боты**](~/bots/what-are-bots.md) могут вести индивидуальные беседы с пользователем.</span><span class="sxs-lookup"><span data-stu-id="e0572-123">[**Bots**](~/bots/what-are-bots.md) have one-on-one conversations with a user.</span></span> <span data-ttu-id="e0572-124">Боты, требующие многоходовых бесед или предоставляющие уведомления, нужные только определенному пользователю, лучше всего подходят для личных приложений.</span><span class="sxs-lookup"><span data-stu-id="e0572-124">Bots that require multi-turn conversations or provide notifications relevant only to a specific user are best suited in personal apps.</span></span>

* <span data-ttu-id="e0572-125">[**Вкладки**](~/tabs/what-are-tabs.md) предоставляют полноэкранный внедренный веб-интерфейс, понятный пользователю, который просматривает их.</span><span class="sxs-lookup"><span data-stu-id="e0572-125">[**Tabs**](~/tabs/what-are-tabs.md) provide a full-screen embedded web experience that's meaningful to the user looking at it.</span></span>

## <a name="examples"></a><span data-ttu-id="e0572-126">Примеры</span><span class="sxs-lookup"><span data-stu-id="e0572-126">Examples</span></span>

<span data-ttu-id="e0572-127">Рекомендации по разработке приложений Teams содержат подробные визуальные элементы, демонстрирующие, где люди могут найти и использовать приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="e0572-127">The Teams app design guidelines provide detailed visuals showing you where people can find and use Teams apps.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e0572-128">См. рекомендации по разработке приложений Teams</span><span class="sxs-lookup"><span data-stu-id="e0572-128">See the Teams app design guidelines</span></span>](../concepts/design/design-teams-app-overview.md)
