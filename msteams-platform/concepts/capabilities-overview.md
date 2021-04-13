---
title: Понимание возможностей приложения
author: heath-hamilton
description: Возможности приложений teams
ms.topic: conceptual
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 6d08d06c55aed4b531fba4bb533c896c13073cfc
ms.sourcegitcommit: 9404c2e3a30887b9e17e0c89b12dd26fd9b8033e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2021
ms.locfileid: "51654435"
---
# <a name="understand-microsoft-teams-app-capabilities"></a><span data-ttu-id="2b8eb-103">Понимание возможностей приложений Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="2b8eb-103">Understand Microsoft Teams app capabilities</span></span>

<span data-ttu-id="2b8eb-104">Разминаемость или точки входа — это разные способы, с помощью которых приложение может проявляться к пользователю.</span><span class="sxs-lookup"><span data-stu-id="2b8eb-104">Extensibility or entry points are different ways in which an app can manifest itself to a user.</span></span> <span data-ttu-id="2b8eb-105">Например, пользователь может взаимодействовать с приложением на вкладке холста, чтобы сделать действие, или может выбрать то же самое с помощью разговорного бота.</span><span class="sxs-lookup"><span data-stu-id="2b8eb-105">For example, a user can interact with an app on a canvas tab to do an activity or might choose to do the same using a conversational bot.</span></span> <span data-ttu-id="2b8eb-106">Различные возможности, используемые для создания приложения Teams, позволяют увеличить область его использования.</span><span class="sxs-lookup"><span data-stu-id="2b8eb-106">The various capabilities used to build your Teams app allow you to increase its usage scope.</span></span>

<span data-ttu-id="2b8eb-107">Существует несколько способов расширения Teams, поэтому каждое приложение является уникальным.</span><span class="sxs-lookup"><span data-stu-id="2b8eb-107">There are multiple ways to extend Teams, so every app is unique.</span></span> <span data-ttu-id="2b8eb-108">Некоторые из них имеют только одну возможность, например веб-ок, в то время как другие имеют несколько функций, чтобы предоставить пользователям различные параметры.</span><span class="sxs-lookup"><span data-stu-id="2b8eb-108">Some only have one capability, such as a webhook, while others have more than one feature to give users various options.</span></span> <span data-ttu-id="2b8eb-109">Например, приложение может отображать данные в центральном расположении, то есть на вкладке, и представлять ту же информацию через диалоговую интерфейс, то есть **бот.** </span><span class="sxs-lookup"><span data-stu-id="2b8eb-109">For example, your app can display data in a central location, that is, the **tab** and present that same information through a conversational interface, that is, the **bot**.</span></span>

## <a name="app-capabilities"></a><span data-ttu-id="2b8eb-110">Возможности приложений</span><span class="sxs-lookup"><span data-stu-id="2b8eb-110">App capabilities</span></span>

<span data-ttu-id="2b8eb-111">Приложение Teams имеет одну или все следующие основные возможности:</span><span class="sxs-lookup"><span data-stu-id="2b8eb-111">Your Teams app have one or all of the following core capabilities:</span></span>

* [<span data-ttu-id="2b8eb-112">Tabs</span><span class="sxs-lookup"><span data-stu-id="2b8eb-112">Tabs</span></span>](../tabs/what-are-tabs.md)
* [<span data-ttu-id="2b8eb-113">Расширения для системы обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="2b8eb-113">Messaging extensions</span></span>](../messaging-extensions/what-are-messaging-extensions.md)
* [<span data-ttu-id="2b8eb-114">Боты</span><span class="sxs-lookup"><span data-stu-id="2b8eb-114">Bots</span></span>](../bots/what-are-bots.md)
* [<span data-ttu-id="2b8eb-115">Веб-перехватчики и соединительные линии</span><span class="sxs-lookup"><span data-stu-id="2b8eb-115">Webhooks and connectors</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)

<span data-ttu-id="2b8eb-116">Приложение также может воспользоваться расширенными возможностями, такими как [API Microsoft Graph для Teams.](https://docs.microsoft.com/graph/teams-concept-overview)</span><span class="sxs-lookup"><span data-stu-id="2b8eb-116">Your app can also take advantage of advanced capabilities, such as the [Microsoft Graph API for Teams](https://docs.microsoft.com/graph/teams-concept-overview).</span></span>

<span data-ttu-id="2b8eb-117">На следующей иллюстрации вы можете узнать, какие функции будут предоставляться в приложении.</span><span class="sxs-lookup"><span data-stu-id="2b8eb-117">The following illustration gives you an idea of which capabilities will provide the features you want in your app.</span></span>

:::image type="content" source="../assets/images/capabilities-overview.png" alt-text="Карта разума, иллюстрированная возможностями приложений Teams.":::

## <a name="always-consider-your-user"></a><span data-ttu-id="2b8eb-119">Всегда учитывайте пользователя</span><span class="sxs-lookup"><span data-stu-id="2b8eb-119">Always consider your user</span></span>

<span data-ttu-id="2b8eb-120">Ознакомив себя с разработкой приложений Teams, вы поймете его основные основы.</span><span class="sxs-lookup"><span data-stu-id="2b8eb-120">As you familiarize yourself with Teams app development, you understand its core fundamentals.</span></span> <span data-ttu-id="2b8eb-121">Вы понимаете, что существует несколько способов создания определенных функций.</span><span class="sxs-lookup"><span data-stu-id="2b8eb-121">You understand that there is more than one way to build certain features.</span></span> <span data-ttu-id="2b8eb-122">В таких сценариях рассмотрим, как можно предоставить пользователю более родной опыт.</span><span class="sxs-lookup"><span data-stu-id="2b8eb-122">In such scenarios, consider how you can provide a more native experience to your user.</span></span>
<span data-ttu-id="2b8eb-123">Например, можно собирать входные данные пользователей в форме, построенной в виде вкладки в приложении.</span><span class="sxs-lookup"><span data-stu-id="2b8eb-123">For example, you can collect user input in a form built as a tab in the app.</span></span> <span data-ttu-id="2b8eb-124">Это также можно сделать с помощью модуля задач без переключения представлений и нарушения потока работы пользователя.</span><span class="sxs-lookup"><span data-stu-id="2b8eb-124">You can also do this using a task module without switching views and disrupting user's flow of work.</span></span> <span data-ttu-id="2b8eb-125">Важно выбрать точки расширения, которые обеспечивают наименьшее отклонение от регулярного потока работы пользователя.</span><span class="sxs-lookup"><span data-stu-id="2b8eb-125">It is important to choose extension points that provide least deviation from a user's regular flow of work.</span></span>

## <a name="see-also"></a><span data-ttu-id="2b8eb-126">См. также</span><span class="sxs-lookup"><span data-stu-id="2b8eb-126">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2b8eb-127">Создание приложений для teams</span><span class="sxs-lookup"><span data-stu-id="2b8eb-127">Build apps for Teams</span></span>](../overview.md)
## <a name="next-step"></a><span data-ttu-id="2b8eb-128">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="2b8eb-128">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2b8eb-129">Точки входа приложения Teams</span><span class="sxs-lookup"><span data-stu-id="2b8eb-129">Teams app entry points</span></span>](../concepts/extensibility-points.md)
