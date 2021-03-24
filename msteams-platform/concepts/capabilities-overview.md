---
title: Понимание возможностей приложений Teams
author: heath-hamilton
description: Возможности приложений teams
ms.topic: conceptual
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 5336b36b52cf81be414f18ccaaf9e235c079e626
ms.sourcegitcommit: 49d1ecda14042bf3f368b14c1971618fe979b914
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/23/2021
ms.locfileid: "51034707"
---
# <a name="understanding-teams-app-capabilities"></a><span data-ttu-id="aa8d1-103">Понимание возможностей приложений Teams</span><span class="sxs-lookup"><span data-stu-id="aa8d1-103">Understanding Teams app capabilities</span></span>

<span data-ttu-id="aa8d1-104">*Возможности —* это точки расширения для создания приложений на платформе Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="aa8d1-104">*Capabilities* are the extension points for building apps on the Microsoft Teams platform.</span></span>

<span data-ttu-id="aa8d1-105">Существует несколько способов расширения Teams, поэтому каждое приложение является уникальным: некоторые из них имеют только одну возможность (например, веб-ок), в то время как у других есть несколько способов предоставить пользователям параметры.</span><span class="sxs-lookup"><span data-stu-id="aa8d1-105">There are multiple ways to extend Teams, so every app is unique: Some only have one capability (such as a webhook), while others have a few to give users options.</span></span> <span data-ttu-id="aa8d1-106">Например, ваше приложение может отображать данные в центральном расположении (вкладке) и представлять эти же сведения через диалоговой интерфейс (бот).</span><span class="sxs-lookup"><span data-stu-id="aa8d1-106">For instance, your app could display data in a central location (tab) and present that same information through a conversational interface (bot).</span></span>

<span data-ttu-id="aa8d1-107">Приложение Teams имеет одну или все следующие основные возможности:</span><span class="sxs-lookup"><span data-stu-id="aa8d1-107">Your Teams app have one or all of the following core capabilities:</span></span>

* [<span data-ttu-id="aa8d1-108">Вкладки</span><span class="sxs-lookup"><span data-stu-id="aa8d1-108">Tabs</span></span>](../tabs/what-are-tabs.md)
* [<span data-ttu-id="aa8d1-109">Расширения для системы обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="aa8d1-109">Messaging extensions</span></span>](../messaging-extensions/what-are-messaging-extensions.md)
* [<span data-ttu-id="aa8d1-110">Боты</span><span class="sxs-lookup"><span data-stu-id="aa8d1-110">Bots</span></span>](../bots/what-are-bots.md)
* [<span data-ttu-id="aa8d1-111">Веб-перехватчики и соединительные линии</span><span class="sxs-lookup"><span data-stu-id="aa8d1-111">Webhooks and connectors</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)

<span data-ttu-id="aa8d1-112">Приложение также может воспользоваться расширенными возможностями, такими как [API Microsoft Graph для Teams.](https://docs.microsoft.com/graph/teams-concept-overview)</span><span class="sxs-lookup"><span data-stu-id="aa8d1-112">Your app can also take advantage of advanced capabilities, such as the [Microsoft Graph API for Teams](https://docs.microsoft.com/graph/teams-concept-overview).</span></span>

<span data-ttu-id="aa8d1-113">На следующей иллюстрации см. представление о том, какие возможности будут предоставлять нужные функции в приложении.</span><span class="sxs-lookup"><span data-stu-id="aa8d1-113">See the following illustration to get an idea which capabilities would provide the features you want in your app.</span></span>

:::image type="content" source="../assets/images/capabilities-overview.png" alt-text="Карта разума, иллюстрированная возможностями приложений Teams.":::

## <a name="doing-whats-best-for-your-users"></a><span data-ttu-id="aa8d1-115">Делать то, что лучше для пользователей</span><span class="sxs-lookup"><span data-stu-id="aa8d1-115">Doing what's best for your users</span></span>

<span data-ttu-id="aa8d1-116">Ознакомив себя с разработкой приложения Teams, вы начнете понимать его тонкости.</span><span class="sxs-lookup"><span data-stu-id="aa8d1-116">As you familiarize yourself with Teams app development, you'll begin to understand its subtleties.</span></span> <span data-ttu-id="aa8d1-117">Существует несколько способов создания определенных функций (например, сбора ввода пользователя).</span><span class="sxs-lookup"><span data-stu-id="aa8d1-117">There's more than one way to build certain features (such as collecting user input).</span></span> <span data-ttu-id="aa8d1-118">Например, можно встраить веб-форму в вкладку с помощью `<iframe>` .</span><span class="sxs-lookup"><span data-stu-id="aa8d1-118">For example, you could embed a web-based form in a tab using an `<iframe>`.</span></span> <span data-ttu-id="aa8d1-119">Вы также можете сделать это на вкладке с помощью модуля задач, конвенции об пользовательском интерфейсе Teams, для более родного опыта, который могут предпочитать пользователи.</span><span class="sxs-lookup"><span data-stu-id="aa8d1-119">You could also do this in a tab using a task module, a Teams UI convention, for a more native experience your users may prefer.</span></span>

<span data-ttu-id="aa8d1-120">Выбор правильных возможностей и дизайна сводится к первому пониманию случаев [использования аудитории.](../concepts/design/understand-use-cases.md)</span><span class="sxs-lookup"><span data-stu-id="aa8d1-120">Choosing the right capabilities and design comes down to first [understanding your audience's use cases](../concepts/design/understand-use-cases.md).</span></span>
