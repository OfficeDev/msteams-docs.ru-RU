---
title: Общие сведения о возможностях приложений Teams
author: heath-hamilton
description: ''
ms.topic: overview
ms.author: heath-hamilton
ms.openlocfilehash: 580d75b648bde1caf0e85647c89635804c91fb70
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/12/2020
ms.locfileid: "46652153"
---
# <a name="understanding-teams-app-capabilities"></a><span data-ttu-id="3e48d-102">Общие сведения о возможностях приложений Teams</span><span class="sxs-lookup"><span data-stu-id="3e48d-102">Understanding Teams app capabilities</span></span>

<span data-ttu-id="3e48d-103">*Возможности* — это точки расширения для создания приложений на платформе Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="3e48d-103">*Capabilities* are the extension points for building apps on the Microsoft Teams platform.</span></span>

<span data-ttu-id="3e48d-104">Существует несколько способов расширения клиента Teams, поэтому каждое приложение является уникальным: только одна возможность (например, веб-перехватчик), а другие пользователи предоставляют несколько вариантов.</span><span class="sxs-lookup"><span data-stu-id="3e48d-104">There are multiple ways to extend the Teams client, so every app is unique: Some only have one capability (such as a webhook), while others have a few to give users options.</span></span> <span data-ttu-id="3e48d-105">Например, ваше приложение может отображать данные в центральном расположении (на вкладке) и показывать эти данные через интерфейс для общения (Bot).</span><span class="sxs-lookup"><span data-stu-id="3e48d-105">For instance, your app could display data in a central location (tab) and present that same information through a conversational interface (bot).</span></span>

<span data-ttu-id="3e48d-106">Приложение Teams может иметь один или все из следующих основных возможностей:</span><span class="sxs-lookup"><span data-stu-id="3e48d-106">Your Teams app can have one or all of the following core capabilities:</span></span>

* [<span data-ttu-id="3e48d-107">Tabs</span><span class="sxs-lookup"><span data-stu-id="3e48d-107">Tabs</span></span>](../tabs/what-are-tabs.md)
* [<span data-ttu-id="3e48d-108">Расширения для системы обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="3e48d-108">Messaging extensions</span></span>](../messaging-extensions/what-are-messaging-extensions.md)
* [<span data-ttu-id="3e48d-109">Веб-перехватчики и соединительные линии</span><span class="sxs-lookup"><span data-stu-id="3e48d-109">Webhooks and connectors</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)
* [<span data-ttu-id="3e48d-110">Боты</span><span class="sxs-lookup"><span data-stu-id="3e48d-110">Bots</span></span>](../bots/what-are-bots.md)

<span data-ttu-id="3e48d-111">Ваше приложение также может использовать расширенные возможности, такие как [REST API Microsoft Graph](../graph-api/rsc/resource-specific-consent.md).</span><span class="sxs-lookup"><span data-stu-id="3e48d-111">Your app can also can take advantage of advanced capabilities, such as the [Microsoft Graph REST API](../graph-api/rsc/resource-specific-consent.md).</span></span>

<span data-ttu-id="3e48d-112">На приведенном ниже рисунке вы найдете представление о возможностях, которые будут предоставлять вам необходимые функции в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="3e48d-112">See the following illustration to get an idea which capabilities would provide the features you want in your app.</span></span>

![Карта, иллюстрирующая возможности приложений Teams](doc-links/images/capabilities-overview.png)

## <a name="doing-whats-best-for-your-users"></a><span data-ttu-id="3e48d-114">Как лучше всего подходит для пользователей</span><span class="sxs-lookup"><span data-stu-id="3e48d-114">Doing what's best for your users</span></span>

<span data-ttu-id="3e48d-115">Как вы ознакомитесь с разработкой приложений Teams, вы начнете понимание его тонкостей.</span><span class="sxs-lookup"><span data-stu-id="3e48d-115">As you familiarize yourself with Teams app development, you'll begin to understand its subtleties.</span></span> <span data-ttu-id="3e48d-116">Существует несколько способов создания определенных компонентов (например, сбора данных, вводимых пользователем).</span><span class="sxs-lookup"><span data-stu-id="3e48d-116">There's more than one way to build certain features (such as collecting user input).</span></span> <span data-ttu-id="3e48d-117">Например, вы можете внедрить веб-форму на вкладку с помощью элемента `<iframe>` .</span><span class="sxs-lookup"><span data-stu-id="3e48d-117">For example, you could embed a web-based form in a tab using an `<iframe>`.</span></span> <span data-ttu-id="3e48d-118">Вы также можете сделать это на вкладке, используя модуль задач, соглашение о пользовательском интерфейсе Teams для более собственной работы пользователей.</span><span class="sxs-lookup"><span data-stu-id="3e48d-118">You could also do this in a tab using a task module, a Teams UI convention, for a more native experience your users may prefer.</span></span>

<span data-ttu-id="3e48d-119">Чтобы [понять варианты использования аудитории](../concepts/design/understand-use-cases.md), необходимо выбрать правильное сочетание возможностей и правил пользовательского интерфейса, элементов управления и элементов.</span><span class="sxs-lookup"><span data-stu-id="3e48d-119">Choosing the right combination of capabilities and UI conventions, controls, and elements comes down to first [understanding your audience's use cases](../concepts/design/understand-use-cases.md).</span></span>

## <a name="learn-more"></a><span data-ttu-id="3e48d-120">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="3e48d-120">Learn more</span></span>

* [<span data-ttu-id="3e48d-121">Начало планирования приложения</span><span class="sxs-lookup"><span data-stu-id="3e48d-121">Start planning your app</span></span>](../concepts/extensibility-points.md)
