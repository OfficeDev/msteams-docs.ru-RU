---
title: Разработка приложения — понимание структуры приложения
description: Поймите, что можно и не можете настроить в Microsoft Teams при разработке приложения.
author: heath-hamilton
ms.topic: conceptual
localization_priority: Normal
ms.author: surbhigupta
ms.openlocfilehash: bf84ad1d52cf46e9242bf4122dc5e900461ab806
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/24/2021
ms.locfileid: "52631390"
---
# <a name="understand-the-microsoft-teams-app-structure"></a><span data-ttu-id="1d5a9-103">Понимание структуры Microsoft Teams приложения</span><span class="sxs-lookup"><span data-stu-id="1d5a9-103">Understand the Microsoft Teams app structure</span></span>

<span data-ttu-id="1d5a9-104">При создании приложения важно знать, что можно и не можете настроить в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="1d5a9-104">When building your app, it's important to know what you can and can't customize in Microsoft Teams.</span></span> <span data-ttu-id="1d5a9-105">Эти сведения помогут вам лучше понять, какие части приложения вы контролируете.</span><span class="sxs-lookup"><span data-stu-id="1d5a9-105">This information can help you better understand which parts of the app experience you control.</span></span>

<span data-ttu-id="1d5a9-106">На следующих телефреймах покажите:</span><span class="sxs-lookup"><span data-stu-id="1d5a9-106">The following wireframes show you:</span></span>

* <span data-ttu-id="1d5a9-107">Поверхности, которые можно настроить в каждом Teams приложения (описанные синим цветом).</span><span class="sxs-lookup"><span data-stu-id="1d5a9-107">The surfaces you can customize in each Teams app capability (outlined in blue).</span></span>
* <span data-ttu-id="1d5a9-108">Области, поддерживаемые каждой возможностью.</span><span class="sxs-lookup"><span data-stu-id="1d5a9-108">The scopes each capability supports.</span></span>

> [!NOTE]
> <span data-ttu-id="1d5a9-109">**Что означает область?**</span><span class="sxs-lookup"><span data-stu-id="1d5a9-109">**What does scope mean?**</span></span> <span data-ttu-id="1d5a9-110">Область — это область в Teams, где люди могут использовать ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="1d5a9-110">A scope is an area in Teams where people can use your app.</span></span> <span data-ttu-id="1d5a9-111">Приложения могут иметь одну или несколько областей, включая личные, каналы, чаты и собрания.</span><span class="sxs-lookup"><span data-stu-id="1d5a9-111">Apps can have one or many scopes, including personal, channels, chats, and meetings.</span></span>

## <a name="personal-apps"></a><span data-ttu-id="1d5a9-112">Персональные приложения</span><span class="sxs-lookup"><span data-stu-id="1d5a9-112">Personal apps</span></span>

<span data-ttu-id="1d5a9-113">Личные приложения предоставляют большой холст для содержимого приложения для отдельных пользователей.</span><span class="sxs-lookup"><span data-stu-id="1d5a9-113">Personal apps provide a large canvas to host your app content for individual users.</span></span> <span data-ttu-id="1d5a9-114">Холст — это iframe, поэтому вы можете полностью настроить его.</span><span class="sxs-lookup"><span data-stu-id="1d5a9-114">The canvas is an iframe so you can completely customize the experience.</span></span>

<span data-ttu-id="1d5a9-115">***Поддерживаемые области:** Personal*</span><span class="sxs-lookup"><span data-stu-id="1d5a9-115">\***Supported scopes**: Personal\*</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-personal-apps.png" alt-text="Концептуальное изображение, показывающая области переднего Teams, которые разработчики могут настраивать для личных приложений." border="false":::

## <a name="tabs"></a><span data-ttu-id="1d5a9-117">Вкладки</span><span class="sxs-lookup"><span data-stu-id="1d5a9-117">Tabs</span></span>

<span data-ttu-id="1d5a9-118">Вкладки предоставляют большой холст для содержимого приложения для группы пользователей.</span><span class="sxs-lookup"><span data-stu-id="1d5a9-118">Tabs provide a large canvas to host your app content for a group of users.</span></span> <span data-ttu-id="1d5a9-119">Вы можете включить вкладки в общих пространствах, таких как каналы, чаты и приглашения на собрания.</span><span class="sxs-lookup"><span data-stu-id="1d5a9-119">You can include tabs in shared spaces such as channels, chats, and meeting invites.</span></span> <span data-ttu-id="1d5a9-120">Холст — это iframe, поэтому вы можете полностью настроить его.</span><span class="sxs-lookup"><span data-stu-id="1d5a9-120">The canvas is an iframe so you can completely customize the experience.</span></span>

<span data-ttu-id="1d5a9-121">***Поддерживаемые области:** каналы, чаты, собрания*</span><span class="sxs-lookup"><span data-stu-id="1d5a9-121">\***Supported scopes**: Channels, Chats, Meetings\*</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-tabs.png" alt-text="Концептуальное изображение, показывающая области переднего Teams, которые разработчики могут настраивать для вкладок." border="false":::

## <a name="bots"></a><span data-ttu-id="1d5a9-123">Боты</span><span class="sxs-lookup"><span data-stu-id="1d5a9-123">Bots</span></span>

<span data-ttu-id="1d5a9-124">Боты — это диалоговые приложения, которые Teams с родными функциями обмена сообщениями, поэтому работа пользовательского интерфейса обрабатывается для вас.</span><span class="sxs-lookup"><span data-stu-id="1d5a9-124">Bots are conversational apps that integrate with Teams native messaging features, so the UI work is handled for you.</span></span> <span data-ttu-id="1d5a9-125">С точки зрения разработки все еще существуют возможности для добавления индивидуальности, пользовательских функций и богатых сведений с помощью поддержки обработки естественных языков (NLP) и платформы Адаптивные карты.</span><span class="sxs-lookup"><span data-stu-id="1d5a9-125">From a design standpoint, there are still opportunities to add personality, custom functionality, and rich, actionable information with our natural language processing (NLP) support and Adaptive Cards platform.</span></span>

<span data-ttu-id="1d5a9-126">***Поддерживаемые области:** личные, каналы, чаты, собрания*</span><span class="sxs-lookup"><span data-stu-id="1d5a9-126">\***Supported scopes**: Personal, Channels, Chats, Meetings\*</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-bots.png" alt-text="Концептуальное изображение, показывающая области переднего Teams, которые разработчики могут настроить для ботов." border="false":::

## <a name="messaging-extensions"></a><span data-ttu-id="1d5a9-128">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="1d5a9-128">Messaging extensions</span></span>

<span data-ttu-id="1d5a9-129">Расширения обмена сообщениями — это ярлыки для вставки контента приложения или действия в сообщении, не переходя от беседы.</span><span class="sxs-lookup"><span data-stu-id="1d5a9-129">Messaging extensions are shortcuts for inserting app content or acting on a message without navigating away from the conversation.</span></span> <span data-ttu-id="1d5a9-130">Расширения обмена сообщениями на основе действий дают дополнительный контроль над опытом, а Teams обрабатывают большую часть отрисовок для расширений обмена сообщениями на основе поиска.</span><span class="sxs-lookup"><span data-stu-id="1d5a9-130">Action-based messaging extensions give you more control of the experience, while Teams handles much of what renders for search-based messaging extensions.</span></span>

<span data-ttu-id="1d5a9-131">***Поддерживаемые области:** личные, каналы, чаты, собрания*</span><span class="sxs-lookup"><span data-stu-id="1d5a9-131">\***Supported scopes**: Personal, Channels, Chats, Meetings\*</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-messaging-exetensions.png" alt-text="Концептуальное изображение, показывающая области переднего Teams, которые разработчики могут настраивать для расширений обмена сообщениями." border="false":::

## <a name="meeting-extensions"></a><span data-ttu-id="1d5a9-133">Расширения для собраний</span><span class="sxs-lookup"><span data-stu-id="1d5a9-133">Meeting extensions</span></span>

<span data-ttu-id="1d5a9-134">Расширения собраний — это приложения для расширения живых собраний.</span><span class="sxs-lookup"><span data-stu-id="1d5a9-134">Meeting extensions are apps to enhance live meetings.</span></span> <span data-ttu-id="1d5a9-135">Содержимое приложения можно использовать в нескольких сценариях, в том числе до, во время и после собраний.</span><span class="sxs-lookup"><span data-stu-id="1d5a9-135">You can host your app content in several scenarios, including before, during, and after meetings.</span></span> <span data-ttu-id="1d5a9-136">Поверхность — это ифрам, позволяющий настраивать опыт, но имейте в виду, что эти приложения темные и узкие во время собраний.</span><span class="sxs-lookup"><span data-stu-id="1d5a9-136">The surface is an iframe, allowing you to customize the experience, but keep in mind that these apps are dark themed and narrow during meetings.</span></span>

<span data-ttu-id="1d5a9-137">***Поддерживаемые области:** Собрания, чаты*</span><span class="sxs-lookup"><span data-stu-id="1d5a9-137">\***Supported scopes**: Meetings, Chats\*</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-meeting-exetensions.png" alt-text="Концептуальное изображение, показывающая области переднего Teams, которые разработчики могут настроить для расширений собраний." border="false":::
