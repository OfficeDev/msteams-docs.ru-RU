---
title: Общие сведения о возможностях приложений Teams
author: heath-hamilton
description: Описание возможностей приложений Teams
ms.topic: conceptual
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: e7a6fe61fa5c74547ce20cc895afdd044f35e512
ms.sourcegitcommit: 1aa0b172931d0f81db346452788c41dc4a6717b9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/22/2020
ms.locfileid: "48210357"
---
# <a name="understanding-teams-app-capabilities"></a><span data-ttu-id="ec3cc-103">Общие сведения о возможностях приложений Teams</span><span class="sxs-lookup"><span data-stu-id="ec3cc-103">Understanding Teams app capabilities</span></span>

<span data-ttu-id="ec3cc-104">*Возможности* — это точки расширения для создания приложений на платформе Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="ec3cc-104">*Capabilities* are the extension points for building apps on the Microsoft Teams platform.</span></span>

<span data-ttu-id="ec3cc-105">Существует несколько способов расширения Teams, поэтому каждое приложение является уникальным: только одна возможность (например, веб-перехватчик), а другие пользователи предоставляют несколько вариантов.</span><span class="sxs-lookup"><span data-stu-id="ec3cc-105">There are multiple ways to extend Teams, so every app is unique: Some only have one capability (such as a webhook), while others have a few to give users options.</span></span> <span data-ttu-id="ec3cc-106">Например, ваше приложение может отображать данные в центральном расположении (на вкладке) и показывать эти данные через интерфейс для общения (Bot).</span><span class="sxs-lookup"><span data-stu-id="ec3cc-106">For instance, your app could display data in a central location (tab) and present that same information through a conversational interface (bot).</span></span>

<span data-ttu-id="ec3cc-107">Приложение Teams может иметь один или все из следующих основных возможностей:</span><span class="sxs-lookup"><span data-stu-id="ec3cc-107">Your Teams app can have one or all of the following core capabilities:</span></span>

* [<span data-ttu-id="ec3cc-108">Tabs</span><span class="sxs-lookup"><span data-stu-id="ec3cc-108">Tabs</span></span>](../tabs/what-are-tabs.md)
* [<span data-ttu-id="ec3cc-109">Расширения для системы обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="ec3cc-109">Messaging extensions</span></span>](../messaging-extensions/what-are-messaging-extensions.md)
* [<span data-ttu-id="ec3cc-110">Боты</span><span class="sxs-lookup"><span data-stu-id="ec3cc-110">Bots</span></span>](../bots/what-are-bots.md)
* [<span data-ttu-id="ec3cc-111">Веб-перехватчики и соединительные линии</span><span class="sxs-lookup"><span data-stu-id="ec3cc-111">Webhooks and connectors</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)

<span data-ttu-id="ec3cc-112">Ваше приложение также может использовать расширенные возможности, такие как [API Microsoft Graph для Teams](https://docs.microsoft.com/graph/teams-concept-overview).</span><span class="sxs-lookup"><span data-stu-id="ec3cc-112">Your app can also can take advantage of advanced capabilities, such as the [Microsoft Graph API for Teams](https://docs.microsoft.com/graph/teams-concept-overview).</span></span>

<span data-ttu-id="ec3cc-113">На приведенном ниже рисунке вы найдете представление о возможностях, которые будут предоставлять вам необходимые функции в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="ec3cc-113">See the following illustration to get an idea which capabilities would provide the features you want in your app.</span></span>

:::image type="content" source="../assets/images/capabilities-overview.png" alt-text="Обратите внимание на карту, иллюстрирующие возможности приложений Teams.":::

## <a name="doing-whats-best-for-your-users"></a><span data-ttu-id="ec3cc-115">Как лучше всего подходит для пользователей</span><span class="sxs-lookup"><span data-stu-id="ec3cc-115">Doing what's best for your users</span></span>

<span data-ttu-id="ec3cc-116">Как вы ознакомитесь с разработкой приложений Teams, вы начнете понимание его тонкостей.</span><span class="sxs-lookup"><span data-stu-id="ec3cc-116">As you familiarize yourself with Teams app development, you'll begin to understand its subtleties.</span></span> <span data-ttu-id="ec3cc-117">Существует несколько способов создания определенных компонентов (например, сбора данных, вводимых пользователем).</span><span class="sxs-lookup"><span data-stu-id="ec3cc-117">There's more than one way to build certain features (such as collecting user input).</span></span> <span data-ttu-id="ec3cc-118">Например, вы можете внедрить веб-форму на вкладку с помощью элемента `<iframe>` .</span><span class="sxs-lookup"><span data-stu-id="ec3cc-118">For example, you could embed a web-based form in a tab using an `<iframe>`.</span></span> <span data-ttu-id="ec3cc-119">Вы также можете сделать это на вкладке, используя модуль задач, соглашение о пользовательском интерфейсе Teams для более собственной работы пользователей.</span><span class="sxs-lookup"><span data-stu-id="ec3cc-119">You could also do this in a tab using a task module, a Teams UI convention, for a more native experience your users may prefer.</span></span>

<span data-ttu-id="ec3cc-120">Выбор правильных возможностей и дизайна сводится к [пониманию вариантов использования аудитории](../concepts/design/understand-use-cases.md).</span><span class="sxs-lookup"><span data-stu-id="ec3cc-120">Choosing the right capabilities and design comes down to first [understanding your audience's use cases](../concepts/design/understand-use-cases.md).</span></span>
