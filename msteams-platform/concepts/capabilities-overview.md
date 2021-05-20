---
title: Понимание возможностей приложения
author: heath-hamilton
description: Teams приложения объяснил
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
# <a name="understand-microsoft-teams-app-capabilities"></a><span data-ttu-id="2caaf-103">Понимание Microsoft Teams приложения</span><span class="sxs-lookup"><span data-stu-id="2caaf-103">Understand Microsoft Teams app capabilities</span></span>

<span data-ttu-id="2caaf-104">Возможность или точки входа – это разные способы, с помощью которых приложение может проявляться к пользователю.</span><span class="sxs-lookup"><span data-stu-id="2caaf-104">Extensibility or entry points are different ways in which an app can manifest itself to a user.</span></span> <span data-ttu-id="2caaf-105">Например, пользователь может взаимодействовать с приложением на вкладке холста, чтобы вылаской деятельности или может сделать то же самое с помощью разговорного бота.</span><span class="sxs-lookup"><span data-stu-id="2caaf-105">For example, a user can interact with an app on a canvas tab to do an activity or might choose to do the same using a conversational bot.</span></span> <span data-ttu-id="2caaf-106">Различные возможности, используемые для создания Teams приложения, позволяют увеличить его объем использования.</span><span class="sxs-lookup"><span data-stu-id="2caaf-106">The various capabilities used to build your Teams app allow you to increase its usage scope.</span></span>

<span data-ttu-id="2caaf-107">Существует несколько способов расширения Teams, поэтому каждое приложение уникально.</span><span class="sxs-lookup"><span data-stu-id="2caaf-107">There are multiple ways to extend Teams, so every app is unique.</span></span> <span data-ttu-id="2caaf-108">Некоторые из них имеют только одну возможность, такие как webhook, в то время как другие имеют более чем одну функцию, чтобы дать пользователям различные варианты.</span><span class="sxs-lookup"><span data-stu-id="2caaf-108">Some only have one capability, such as a webhook, while others have more than one feature to give users various options.</span></span> <span data-ttu-id="2caaf-109">Например, приложение может отображать данные в центральном месте, то есть на **вкладке,** и представлять ту же информацию через разговорный интерфейс, то есть **бота.**</span><span class="sxs-lookup"><span data-stu-id="2caaf-109">For example, your app can display data in a central location, that is, the **tab** and present that same information through a conversational interface, that is, the **bot**.</span></span>

## <a name="app-capabilities"></a><span data-ttu-id="2caaf-110">Возможности приложений</span><span class="sxs-lookup"><span data-stu-id="2caaf-110">App capabilities</span></span>

<span data-ttu-id="2caaf-111">Ваше Teams приложение имеет одну или все следующие основные возможности:</span><span class="sxs-lookup"><span data-stu-id="2caaf-111">Your Teams app have one or all of the following core capabilities:</span></span>

* [<span data-ttu-id="2caaf-112">Вкладки</span><span class="sxs-lookup"><span data-stu-id="2caaf-112">Tabs</span></span>](../tabs/what-are-tabs.md)
* [<span data-ttu-id="2caaf-113">Расширения для системы обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="2caaf-113">Messaging extensions</span></span>](../messaging-extensions/what-are-messaging-extensions.md)
* [<span data-ttu-id="2caaf-114">Боты</span><span class="sxs-lookup"><span data-stu-id="2caaf-114">Bots</span></span>](../bots/what-are-bots.md)
* [<span data-ttu-id="2caaf-115">Веб-перехватчики и соединительные линии</span><span class="sxs-lookup"><span data-stu-id="2caaf-115">Webhooks and connectors</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)

<span data-ttu-id="2caaf-116">Ваше приложение также может воспользоваться преимуществами передовых возможностей, таких как [API Microsoft Graph для Teams.](/graph/teams-concept-overview)</span><span class="sxs-lookup"><span data-stu-id="2caaf-116">Your app can also take advantage of advanced capabilities, such as the [Microsoft Graph API for Teams](/graph/teams-concept-overview).</span></span>

<span data-ttu-id="2caaf-117">Следующая иллюстрация дает вам представление о том, какие возможности обеспечат функции, которые вы хотите в вашем приложении:</span><span class="sxs-lookup"><span data-stu-id="2caaf-117">The following illustration gives you an idea of which capabilities will provide the features you want in your app:</span></span>

:::image type="content" source="../assets/images/capabilities-overview.png" alt-text="Карта разума, иллюстрирующая Teams возможностей приложения.":::

## <a name="always-consider-your-user"></a><span data-ttu-id="2caaf-119">Всегда учитывайте вашего пользователя</span><span class="sxs-lookup"><span data-stu-id="2caaf-119">Always consider your user</span></span>

<span data-ttu-id="2caaf-120">Знакомясь с Teams приложения, вы понимаете его основные основы.</span><span class="sxs-lookup"><span data-stu-id="2caaf-120">As you familiarize yourself with Teams app development, you understand its core fundamentals.</span></span> <span data-ttu-id="2caaf-121">Вы понимаете, что существует несколько способов создания определенных функций.</span><span class="sxs-lookup"><span data-stu-id="2caaf-121">You understand that there is more than one way to build certain features.</span></span> <span data-ttu-id="2caaf-122">В таких сценариях, подумайте, как вы можете предоставить более родной опыт для вашего пользователя.</span><span class="sxs-lookup"><span data-stu-id="2caaf-122">In such scenarios, consider how you can provide a more native experience to your user.</span></span>
<span data-ttu-id="2caaf-123">Например, можно собирать пользовательский ввод в форме, построенной в виде вкладки в приложении.</span><span class="sxs-lookup"><span data-stu-id="2caaf-123">For example, you can collect user input in a form built as a tab in the app.</span></span> <span data-ttu-id="2caaf-124">Вы также можете сделать это с помощью модуля задач, не переключая представления и нарушая поток работы пользователя.</span><span class="sxs-lookup"><span data-stu-id="2caaf-124">You can also do this using a task module without switching views and disrupting user's flow of work.</span></span> <span data-ttu-id="2caaf-125">Важно выбрать точки расширения, которые обеспечивают наименьшее отклонение от обычного потока работы пользователя.</span><span class="sxs-lookup"><span data-stu-id="2caaf-125">It is important to choose extension points that provide least deviation from a user's regular flow of work.</span></span>

## <a name="see-also"></a><span data-ttu-id="2caaf-126">См. также</span><span class="sxs-lookup"><span data-stu-id="2caaf-126">See also</span></span>

[<span data-ttu-id="2caaf-127">Создание приложений для Teams</span><span class="sxs-lookup"><span data-stu-id="2caaf-127">Build apps for Teams</span></span>](../overview.md)

## <a name="next-step"></a><span data-ttu-id="2caaf-128">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="2caaf-128">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2caaf-129">Точки входа приложения Teams</span><span class="sxs-lookup"><span data-stu-id="2caaf-129">Teams app entry points</span></span>](../concepts/extensibility-points.md)
