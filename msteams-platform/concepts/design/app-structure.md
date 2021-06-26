---
title: Разработка приложения — понимание структуры приложения
description: Поймите, что можно и не можете настроить в Microsoft Teams при разработке приложения.
author: heath-hamilton
ms.topic: conceptual
localization_priority: Normal
ms.author: surbhigupta
ms.openlocfilehash: a574ebeb5416e614152bb24d52cc798f0032943c
ms.sourcegitcommit: 0fe60b3fd406a5768b18977df53d1f4c665e5300
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/25/2021
ms.locfileid: "53133416"
---
# <a name="understand-the-microsoft-teams-app-structure"></a><span data-ttu-id="9f83d-103">Понимание структуры Microsoft Teams приложения</span><span class="sxs-lookup"><span data-stu-id="9f83d-103">Understand the Microsoft Teams app structure</span></span>

<span data-ttu-id="9f83d-104">При создании приложения важно знать, что можно и не можете настроить в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="9f83d-104">When building your app, it's important to know what you can and can't customize in Microsoft Teams.</span></span> <span data-ttu-id="9f83d-105">Эти сведения помогут вам лучше понять, какие части приложения вы контролируете.</span><span class="sxs-lookup"><span data-stu-id="9f83d-105">This information can help you better understand which parts of the app experience you control.</span></span>

<span data-ttu-id="9f83d-106">На следующих телефреймах покажите:</span><span class="sxs-lookup"><span data-stu-id="9f83d-106">The following wireframes show you:</span></span>

* <span data-ttu-id="9f83d-107">Поверхности, которые можно настроить в каждом Teams приложения (описанные в розовом цвете).</span><span class="sxs-lookup"><span data-stu-id="9f83d-107">The surfaces you can customize in each Teams app capability (outlined in pink).</span></span>
* <span data-ttu-id="9f83d-108">Области, поддерживаемые каждой возможностью.</span><span class="sxs-lookup"><span data-stu-id="9f83d-108">The scopes each capability supports.</span></span>

> [!TIP]
> <span data-ttu-id="9f83d-109">**Что означает область?**</span><span class="sxs-lookup"><span data-stu-id="9f83d-109">**What does scope mean?**</span></span> <span data-ttu-id="9f83d-110">Область — это область в Teams, где люди могут использовать ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="9f83d-110">A scope is an area in Teams where people can use your app.</span></span> <span data-ttu-id="9f83d-111">Приложения могут иметь одну или несколько областей, включая личные, каналы, чаты и собрания.</span><span class="sxs-lookup"><span data-stu-id="9f83d-111">Apps can have one or many scopes, including personal, channels, chats, and meetings.</span></span>

## <a name="personal-apps"></a><span data-ttu-id="9f83d-112">Персональные приложения</span><span class="sxs-lookup"><span data-stu-id="9f83d-112">Personal apps</span></span>

<span data-ttu-id="9f83d-113">Личные приложения предоставляют большой холст для содержимого приложения для отдельных пользователей.</span><span class="sxs-lookup"><span data-stu-id="9f83d-113">Personal apps provide a large canvas to host your app content for individual users.</span></span>

<span data-ttu-id="9f83d-114">***Поддерживаемые области:** Personal*</span><span class="sxs-lookup"><span data-stu-id="9f83d-114">\***Supported scopes**: Personal\*</span></span>

# <a name="desktop"></a>[<span data-ttu-id="9f83d-115">Классическая версия</span><span class="sxs-lookup"><span data-stu-id="9f83d-115">Desktop</span></span>](#tab/desktop)

<span data-ttu-id="9f83d-116">Холст — это iframe, поэтому вы можете полностью настроить его.</span><span class="sxs-lookup"><span data-stu-id="9f83d-116">The canvas is an iframe so you can completely customize the experience.</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-personal-apps-desktop.png" alt-text="Концептуальное изображение, показывающая области переднего Teams, которые разработчики могут настраивать для личных приложений на рабочем столе." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="9f83d-118">Мобильная версия</span><span class="sxs-lookup"><span data-stu-id="9f83d-118">Mobile</span></span>](#tab/mobile)

<span data-ttu-id="9f83d-119">Холст — это веб-просмотр, поэтому вы можете полностью настроить его.</span><span class="sxs-lookup"><span data-stu-id="9f83d-119">The canvas is a webview so you can completely customize the experience.</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-personal-apps-mobile.png" alt-text="Концептуальное изображение, показывающая области переднего Teams, которые разработчики могут настраивать для личных приложений на мобильных устройствах." border="false":::

---

## <a name="tabs"></a><span data-ttu-id="9f83d-121">Вкладки</span><span class="sxs-lookup"><span data-stu-id="9f83d-121">Tabs</span></span>

<span data-ttu-id="9f83d-122">Вкладки предоставляют большой холст для содержимого приложения для группы пользователей.</span><span class="sxs-lookup"><span data-stu-id="9f83d-122">Tabs provide a large canvas to host your app content for a group of users.</span></span> <span data-ttu-id="9f83d-123">Вы можете включить вкладки в общих пространствах, таких как каналы, чаты и приглашения на собрания.</span><span class="sxs-lookup"><span data-stu-id="9f83d-123">You can include tabs in shared spaces such as channels, chats, and meeting invites.</span></span>

<span data-ttu-id="9f83d-124">***Поддерживаемые области:** каналы, чаты, собрания*</span><span class="sxs-lookup"><span data-stu-id="9f83d-124">\***Supported scopes**: Channels, Chats, Meetings\*</span></span>

# <a name="desktop"></a>[<span data-ttu-id="9f83d-125">Классическая версия</span><span class="sxs-lookup"><span data-stu-id="9f83d-125">Desktop</span></span>](#tab/desktop)

<span data-ttu-id="9f83d-126">Холст — это iframe, поэтому вы можете полностью настроить его.</span><span class="sxs-lookup"><span data-stu-id="9f83d-126">The canvas is an iframe so you can completely customize the experience.</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-tabs-desktop.png" alt-text="Концептуальное изображение, показывающая области переднего Teams, которые разработчики могут настраивать для вкладок на рабочем столе." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="9f83d-128">Мобильная версия</span><span class="sxs-lookup"><span data-stu-id="9f83d-128">Mobile</span></span>](#tab/mobile)

<span data-ttu-id="9f83d-129">Холст — это веб-просмотр, поэтому вы можете полностью настроить его.</span><span class="sxs-lookup"><span data-stu-id="9f83d-129">The canvas is a webview so you can completely customize the experience.</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-tabs-mobile.png" alt-text="Концептуальное изображение, показывающая области переднего Teams, которые разработчики могут настраивать для вкладок на мобильных устройствах." border="false":::

---

## <a name="bots"></a><span data-ttu-id="9f83d-131">Боты</span><span class="sxs-lookup"><span data-stu-id="9f83d-131">Bots</span></span>

<span data-ttu-id="9f83d-132">Боты — это диалоговые приложения, которые Teams с родными функциями обмена сообщениями, поэтому работа пользовательского интерфейса обрабатывается для вас.</span><span class="sxs-lookup"><span data-stu-id="9f83d-132">Bots are conversational apps that integrate with Teams native messaging features, so the UI work is handled for you.</span></span> <span data-ttu-id="9f83d-133">С точки зрения разработки все еще существуют возможности для добавления индивидуальности, пользовательских функций и богатых сведений с помощью поддержки обработки естественных языков (NLP) и платформы Адаптивные карты.</span><span class="sxs-lookup"><span data-stu-id="9f83d-133">From a design standpoint, there are still opportunities to add personality, custom functionality, and rich, actionable information with our natural language processing (NLP) support and Adaptive Cards platform.</span></span>

<span data-ttu-id="9f83d-134">***Поддерживаемые области:** личные, каналы, чаты, собрания*</span><span class="sxs-lookup"><span data-stu-id="9f83d-134">\***Supported scopes**: Personal, Channels, Chats, Meetings\*</span></span>

# <a name="desktop"></a>[<span data-ttu-id="9f83d-135">Классическая версия</span><span class="sxs-lookup"><span data-stu-id="9f83d-135">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/design-guidelines/app-structure-bots-desktop.png" alt-text="Концептуальное изображение, показывающая области переднего Teams, которые разработчики могут настраивать для ботов на рабочем столе." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="9f83d-137">Мобильная версия</span><span class="sxs-lookup"><span data-stu-id="9f83d-137">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/design-guidelines/app-structure-bots-mobile.png" alt-text="Концептуальное изображение, показывающая области переднего Teams, которые разработчики могут настраивать для ботов на мобильных устройствах." border="false":::

---

## <a name="messaging-extensions"></a><span data-ttu-id="9f83d-139">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="9f83d-139">Messaging extensions</span></span>

<span data-ttu-id="9f83d-140">Расширения для сообщений помогают быстро вставить содержимое приложения или выполнить какие-либо операции с сообщением, не выходя из беседы.</span><span class="sxs-lookup"><span data-stu-id="9f83d-140">Messaging extensions are shortcuts for inserting app content or acting on a message without navigating away from the conversation.</span></span> <span data-ttu-id="9f83d-141">Расширения обмена сообщениями на основе действий дают дополнительный контроль над опытом, а Teams обрабатывают большую часть отрисовок для расширений обмена сообщениями на основе поиска.</span><span class="sxs-lookup"><span data-stu-id="9f83d-141">Action-based messaging extensions give you more control of the experience, while Teams handles much of what renders for search-based messaging extensions.</span></span>

<span data-ttu-id="9f83d-142">***Поддерживаемые области:** личные, каналы, чаты, собрания*</span><span class="sxs-lookup"><span data-stu-id="9f83d-142">\***Supported scopes**: Personal, Channels, Chats, Meetings\*</span></span>

# <a name="desktop"></a>[<span data-ttu-id="9f83d-143">Классическая версия</span><span class="sxs-lookup"><span data-stu-id="9f83d-143">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/design-guidelines/app-structure-messaging-exetensions-desktop.png" alt-text="Концептуальное изображение, показывающая области переднего Teams, которые разработчики могут настраивать для расширений обмена сообщениями на рабочем столе." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="9f83d-145">Мобильная версия</span><span class="sxs-lookup"><span data-stu-id="9f83d-145">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/design-guidelines/app-structure-messaging-exetensions-mobile.png" alt-text="Концептуальное изображение, показывающая области переднего Teams, которые разработчики могут настраивать для расширений обмена сообщениями на мобильных устройствах." border="false":::

---

## <a name="meeting-extensions"></a><span data-ttu-id="9f83d-147">Расширения для собраний</span><span class="sxs-lookup"><span data-stu-id="9f83d-147">Meeting extensions</span></span>

<span data-ttu-id="9f83d-148">Расширения собраний — это приложения для расширения живых собраний.</span><span class="sxs-lookup"><span data-stu-id="9f83d-148">Meeting extensions are apps to enhance live meetings.</span></span> <span data-ttu-id="9f83d-149">Содержимое приложения можно использовать в нескольких сценариях, в том числе до, во время и после собраний.</span><span class="sxs-lookup"><span data-stu-id="9f83d-149">You can host your app content in several scenarios, including before, during, and after meetings.</span></span>

<span data-ttu-id="9f83d-150">***Поддерживаемые области:** Собрания, чаты*</span><span class="sxs-lookup"><span data-stu-id="9f83d-150">\***Supported scopes**: Meetings, Chats\*</span></span>

# <a name="desktop"></a>[<span data-ttu-id="9f83d-151">Классическая версия</span><span class="sxs-lookup"><span data-stu-id="9f83d-151">Desktop</span></span>](#tab/desktop)

<span data-ttu-id="9f83d-152">Поверхность — это iframe, позволяющий настраивать опыт, но имейте в виду, что во время собраний эти приложения используют темную тему и узки.</span><span class="sxs-lookup"><span data-stu-id="9f83d-152">The surface is an iframe, allowing you to customize the experience, but keep in mind that during meetings these apps use dark theme and are narrow.</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-meeting-exetensions-desktop.png" alt-text="Концептуальное изображение, показывающая области переднего Teams, которые разработчики могут настроить для расширений собраний на рабочем столе." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="9f83d-154">Мобильная версия</span><span class="sxs-lookup"><span data-stu-id="9f83d-154">Mobile</span></span>](#tab/mobile)

<span data-ttu-id="9f83d-155">Поверхность — это веб-просмотр, позволяющий настраивать опыт, но имейте в виду, что во время собраний в этих приложениях используется темная тема.</span><span class="sxs-lookup"><span data-stu-id="9f83d-155">The surface is a webview, allowing you to customize the experience, but keep in mind that during meetings these apps use dark theme.</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-meeting-exetensions-mobile.png" alt-text="Концептуальное изображение, показывающая области переднего Teams, которые разработчики могут настраивать для расширений собраний на мобильных устройствах." border="false":::

---
