---
title: Понимание возможностей приложения
author: heath-hamilton
description: Teams возможности приложения
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 209d187681b1370440931fcd40744965395b13e8
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565153"
---
# <a name="understand-microsoft-teams-app-capabilities"></a><span data-ttu-id="429e1-103">Понимание Microsoft Teams приложений</span><span class="sxs-lookup"><span data-stu-id="429e1-103">Understand Microsoft Teams app capabilities</span></span>

<span data-ttu-id="429e1-104">Разминаемость или точки входа — это разные способы, с помощью которых приложение может проявляться к пользователю.</span><span class="sxs-lookup"><span data-stu-id="429e1-104">Extensibility or entry points are different ways in which an app can manifest itself to a user.</span></span> <span data-ttu-id="429e1-105">Например, пользователь может взаимодействовать с приложением на вкладке холста, чтобы сделать действие, или может выбрать то же самое с помощью разговорного бота.</span><span class="sxs-lookup"><span data-stu-id="429e1-105">For example, a user can interact with an app on a canvas tab to do an activity or might choose to do the same using a conversational bot.</span></span> <span data-ttu-id="429e1-106">Различные возможности, используемые для создания приложения Teams, позволяют увеличить область его использования.</span><span class="sxs-lookup"><span data-stu-id="429e1-106">The various capabilities used to build your Teams app allow you to increase its usage scope.</span></span>

<span data-ttu-id="429e1-107">Существует несколько способов расширения Teams, поэтому каждое приложение уникально.</span><span class="sxs-lookup"><span data-stu-id="429e1-107">There are multiple ways to extend Teams, so every app is unique.</span></span> <span data-ttu-id="429e1-108">Некоторые из них имеют только одну возможность, например веб-ок, в то время как другие имеют несколько функций, чтобы предоставить пользователям различные параметры.</span><span class="sxs-lookup"><span data-stu-id="429e1-108">Some only have one capability, such as a webhook, while others have more than one feature to give users various options.</span></span> <span data-ttu-id="429e1-109">Например, приложение может отображать данные в центральном расположении, то есть на вкладке, и представлять ту же информацию через диалоговую интерфейс, то есть **бот.** </span><span class="sxs-lookup"><span data-stu-id="429e1-109">For example, your app can display data in a central location, that is, the **tab** and present that same information through a conversational interface, that is, the **bot**.</span></span>

## <a name="app-capabilities"></a><span data-ttu-id="429e1-110">Возможности приложений</span><span class="sxs-lookup"><span data-stu-id="429e1-110">App capabilities</span></span>

<span data-ttu-id="429e1-111">Ваше Teams приложение имеет один или все следующие основные возможности:</span><span class="sxs-lookup"><span data-stu-id="429e1-111">Your Teams app have one or all of the following core capabilities:</span></span>

* [<span data-ttu-id="429e1-112">Вкладки</span><span class="sxs-lookup"><span data-stu-id="429e1-112">Tabs</span></span>](../tabs/what-are-tabs.md)
* [<span data-ttu-id="429e1-113">Расширения для системы обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="429e1-113">Messaging extensions</span></span>](../messaging-extensions/what-are-messaging-extensions.md)
* [<span data-ttu-id="429e1-114">Боты</span><span class="sxs-lookup"><span data-stu-id="429e1-114">Bots</span></span>](../bots/what-are-bots.md)
* [<span data-ttu-id="429e1-115">Веб-перехватчики и соединительные линии</span><span class="sxs-lookup"><span data-stu-id="429e1-115">Webhooks and connectors</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)

<span data-ttu-id="429e1-116">Ваше приложение также может воспользоваться расширенными возможностями, такими как [API microsoft Graph для Teams.](/graph/teams-concept-overview)</span><span class="sxs-lookup"><span data-stu-id="429e1-116">Your app can also take advantage of advanced capabilities, such as the [Microsoft Graph API for Teams](/graph/teams-concept-overview).</span></span>

<span data-ttu-id="429e1-117">На следующей иллюстрации вы можете узнать, какие функции будут предоставляться в приложении:</span><span class="sxs-lookup"><span data-stu-id="429e1-117">The following illustration gives you an idea of which capabilities will provide the features you want in your app:</span></span>

:::image type="content" source="../assets/images/capabilities-overview.png" alt-text="Карта разума, Teams возможности приложения.":::

## <a name="always-consider-your-user"></a><span data-ttu-id="429e1-119">Всегда учитывайте пользователя</span><span class="sxs-lookup"><span data-stu-id="429e1-119">Always consider your user</span></span>

<span data-ttu-id="429e1-120">Ознакомив себя с разработкой Teams, вы поймете его основные основы.</span><span class="sxs-lookup"><span data-stu-id="429e1-120">As you familiarize yourself with Teams app development, you understand its core fundamentals.</span></span> <span data-ttu-id="429e1-121">Вы понимаете, что существует несколько способов создания определенных функций.</span><span class="sxs-lookup"><span data-stu-id="429e1-121">You understand that there is more than one way to build certain features.</span></span> <span data-ttu-id="429e1-122">В таких сценариях рассмотрим, как можно предоставить пользователю более родной опыт.</span><span class="sxs-lookup"><span data-stu-id="429e1-122">In such scenarios, consider how you can provide a more native experience to your user.</span></span>
<span data-ttu-id="429e1-123">Например, можно собирать входные данные пользователей в форме, построенной в виде вкладки в приложении.</span><span class="sxs-lookup"><span data-stu-id="429e1-123">For example, you can collect user input in a form built as a tab in the app.</span></span> <span data-ttu-id="429e1-124">Это также можно сделать с помощью модуля задач без переключения представлений и нарушения потока работы пользователя.</span><span class="sxs-lookup"><span data-stu-id="429e1-124">You can also do this using a task module without switching views and disrupting user's flow of work.</span></span> <span data-ttu-id="429e1-125">Важно выбрать точки расширения, которые обеспечивают наименьшее отклонение от регулярного потока работы пользователя.</span><span class="sxs-lookup"><span data-stu-id="429e1-125">It is important to choose extension points that provide least deviation from a user's regular flow of work.</span></span>

## <a name="see-also"></a><span data-ttu-id="429e1-126">См. также</span><span class="sxs-lookup"><span data-stu-id="429e1-126">See also</span></span>

[<span data-ttu-id="429e1-127">Создание приложений для Teams</span><span class="sxs-lookup"><span data-stu-id="429e1-127">Build apps for Teams</span></span>](../overview.md)

## <a name="next-step"></a><span data-ttu-id="429e1-128">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="429e1-128">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="429e1-129">Точки входа приложения Teams</span><span class="sxs-lookup"><span data-stu-id="429e1-129">Teams app entry points</span></span>](../concepts/extensibility-points.md)
