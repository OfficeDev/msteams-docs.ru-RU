---
title: Общие сведения о возможностях приложений Teams
author: heath-hamilton
description: Общие сведения о возможностях и точках расширения Teams
ms.topic: overview
ms.author: v-heha
ms.openlocfilehash: f83cf0240b32d35028135b48e7d4c56b939777a9
ms.sourcegitcommit: e8dfcb167274e996395b77d65999991a18f2051a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/15/2020
ms.locfileid: "47819083"
---
# <a name="understanding-teams-app-capabilities"></a><span data-ttu-id="154d9-103">Общие сведения о возможностях приложений Teams</span><span class="sxs-lookup"><span data-stu-id="154d9-103">Understanding Teams app capabilities</span></span>

<span data-ttu-id="154d9-104">*Возможности* — это точки расширения для создания приложений на платформе Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="154d9-104">*Capabilities* are the extension points for building apps on the Microsoft Teams platform.</span></span>

<span data-ttu-id="154d9-105">Существует несколько способов расширения клиента Teams, поэтому каждое приложение является уникальным: только одна возможность (например, веб-перехватчик), а другие пользователи предоставляют несколько вариантов.</span><span class="sxs-lookup"><span data-stu-id="154d9-105">There are multiple ways to extend the Teams client, so every app is unique: Some only have one capability (such as a webhook), while others have a few to give users options.</span></span> <span data-ttu-id="154d9-106">Например, ваше приложение может отображать данные в центральном расположении (на вкладке) и показывать эти данные через интерфейс для общения (Bot).</span><span class="sxs-lookup"><span data-stu-id="154d9-106">For instance, your app could display data in a central location (tab) and present that same information through a conversational interface (bot).</span></span>

<span data-ttu-id="154d9-107">Приложение Teams может иметь один или все из следующих основных возможностей:</span><span class="sxs-lookup"><span data-stu-id="154d9-107">Your Teams app can have one or all of the following core capabilities:</span></span>

* [<span data-ttu-id="154d9-108">Tabs</span><span class="sxs-lookup"><span data-stu-id="154d9-108">Tabs</span></span>](../tabs/what-are-tabs.md)
* [<span data-ttu-id="154d9-109">Расширения для системы обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="154d9-109">Messaging extensions</span></span>](../messaging-extensions/what-are-messaging-extensions.md)
* [<span data-ttu-id="154d9-110">Веб-перехватчики и соединительные линии</span><span class="sxs-lookup"><span data-stu-id="154d9-110">Webhooks and connectors</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)
* [<span data-ttu-id="154d9-111">Боты</span><span class="sxs-lookup"><span data-stu-id="154d9-111">Bots</span></span>](../bots/what-are-bots.md)

<span data-ttu-id="154d9-112">Ваше приложение также может использовать расширенные возможности, такие как [REST API Microsoft Graph](../graph-api/rsc/resource-specific-consent.md).</span><span class="sxs-lookup"><span data-stu-id="154d9-112">Your app can also can take advantage of advanced capabilities, such as the [Microsoft Graph REST API](../graph-api/rsc/resource-specific-consent.md).</span></span>

<span data-ttu-id="154d9-113">На приведенном ниже рисунке вы найдете представление о возможностях, которые будут предоставлять вам необходимые функции в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="154d9-113">See the following illustration to get an idea which capabilities would provide the features you want in your app.</span></span>

![Карта, иллюстрирующая возможности приложений Teams](doc-links/images/capabilities-overview.png)

## <a name="doing-whats-best-for-your-users"></a><span data-ttu-id="154d9-115">Как лучше всего подходит для пользователей</span><span class="sxs-lookup"><span data-stu-id="154d9-115">Doing what's best for your users</span></span>

<span data-ttu-id="154d9-116">Как вы ознакомитесь с разработкой приложений Teams, вы начнете понимание его тонкостей.</span><span class="sxs-lookup"><span data-stu-id="154d9-116">As you familiarize yourself with Teams app development, you'll begin to understand its subtleties.</span></span> <span data-ttu-id="154d9-117">Существует несколько способов создания определенных компонентов (например, сбора данных, вводимых пользователем).</span><span class="sxs-lookup"><span data-stu-id="154d9-117">There's more than one way to build certain features (such as collecting user input).</span></span> <span data-ttu-id="154d9-118">Например, вы можете внедрить веб-форму на вкладку с помощью элемента `<iframe>` .</span><span class="sxs-lookup"><span data-stu-id="154d9-118">For example, you could embed a web-based form in a tab using an `<iframe>`.</span></span> <span data-ttu-id="154d9-119">Вы также можете сделать это на вкладке, используя модуль задач, соглашение о пользовательском интерфейсе Teams для более собственной работы пользователей.</span><span class="sxs-lookup"><span data-stu-id="154d9-119">You could also do this in a tab using a task module, a Teams UI convention, for a more native experience your users may prefer.</span></span>

<span data-ttu-id="154d9-120">Чтобы [понять варианты использования аудитории](../concepts/design/understand-use-cases.md), необходимо выбрать правильное сочетание возможностей и правил пользовательского интерфейса, элементов управления и элементов.</span><span class="sxs-lookup"><span data-stu-id="154d9-120">Choosing the right combination of capabilities and UI conventions, controls, and elements comes down to first [understanding your audience's use cases](../concepts/design/understand-use-cases.md).</span></span>

## <a name="learn-more"></a><span data-ttu-id="154d9-121">Подробнее</span><span class="sxs-lookup"><span data-stu-id="154d9-121">Learn more</span></span>

* [<span data-ttu-id="154d9-122">Начало планирования приложения</span><span class="sxs-lookup"><span data-stu-id="154d9-122">Start planning your app</span></span>](../concepts/extensibility-points.md)
