---
title: Проектирование расширения обмена сообщениями
description: Узнайте, как создать расширение Teams обмена сообщениями и получить Microsoft Teams пользовательского интерфейса.
keywords: Рекомендации по разработке рекомендаций по расширению справочных сообщений в командах советы по рекомендациям по рекомендациям
author: heath-hamilton
localization_priority: Normal
ms.author: qinch
ms.topic: conceptual
ms.openlocfilehash: fd870d8e10ef74c36f8f6d145d48980f53e9303c
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/24/2021
ms.locfileid: "52631074"
---
# <a name="designing-your-microsoft-teams-messaging-extension"></a><span data-ttu-id="9cc94-104">Разработка расширения Microsoft Teams обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="9cc94-104">Designing your Microsoft Teams messaging extension</span></span>

<span data-ttu-id="9cc94-105">Расширения обмена сообщениями — это ярлыки для вставки контента приложения или действия в сообщении, не переходя от беседы.</span><span class="sxs-lookup"><span data-stu-id="9cc94-105">Messaging extensions are shortcuts for inserting app content or acting on a message without navigating away from the conversation.</span></span>
<span data-ttu-id="9cc94-106">Для руководства разработкой приложения в следующих сведениях описывается и иллюстрируется возможность добавления, использования и управления расширениями обмена сообщениями в Teams.</span><span class="sxs-lookup"><span data-stu-id="9cc94-106">To guide your app design, the following information describes and illustrates how people can add, use, and manage messaging extensions in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="9cc94-107">Комплект разработчика для пользовательского интерфейса Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="9cc94-107">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="9cc94-108">В наборе пользовательского интерфейса можно найти всесторонние рекомендации по расширению обмена сообщениями Microsoft Teams, в том числе элементы, которые можно захватить и изменить по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="9cc94-108">You can find comprehensive messaging extension design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9cc94-109">Получить комплект разработчика для пользовательского интерфейса Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="9cc94-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-messaging-extension"></a><span data-ttu-id="9cc94-110">Добавление расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="9cc94-110">Add a messaging extension</span></span>

<span data-ttu-id="9cc94-111">Расширение обмена сообщениями можно добавить в следующих Teams контекстах:</span><span class="sxs-lookup"><span data-stu-id="9cc94-111">You can add a messaging extension in the following Teams contexts:</span></span>

* <span data-ttu-id="9cc94-112">Из Teams магазина.</span><span class="sxs-lookup"><span data-stu-id="9cc94-112">From the Teams store.</span></span>
* <span data-ttu-id="9cc94-113">В канале, чате или собрании (до, во время и после) рядом с полем составить.</span><span class="sxs-lookup"><span data-stu-id="9cc94-113">In a channel, chat, or meeting (before, during, and after) near the compose box.</span></span> <span data-ttu-id="9cc94-114">Стоит отметить, что если в одном из этих мест добавлено расширение обмена сообщениями, его можно использовать только в этом контексте.</span><span class="sxs-lookup"><span data-stu-id="9cc94-114">It's worth noting if you add a messaging extension in one of these places, only you can use it in that context.</span></span>

<span data-ttu-id="9cc94-115">В следующем примере показано, как добавить расширение обмена сообщениями в канале:</span><span class="sxs-lookup"><span data-stu-id="9cc94-115">The following example shows how you add a messaging extension in a channel:</span></span>

# <a name="desktop"></a>[<span data-ttu-id="9cc94-116">Desktop</span><span class="sxs-lookup"><span data-stu-id="9cc94-116">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/add-in-channel.png" alt-text="В примере показано, как добавить расширение обмена сообщениями рядом с окне составить в канале." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="9cc94-118">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="9cc94-118">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-add-in-channel.png" alt-text="В примере показано, как добавить расширение обмена сообщениями рядом с окне составить в канале на мобильном телефоне." border="false":::

---

## <a name="set-up-a-messaging-extension"></a><span data-ttu-id="9cc94-120">Настройка расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="9cc94-120">Set up a messaging extension</span></span>

<span data-ttu-id="9cc94-121">Проверка подлинности не является обязательной, но если ваше приложение является чем-то вроде средства отслеживания билетов, для использования расширения обмена сообщениями могут потребоваться люди.</span><span class="sxs-lookup"><span data-stu-id="9cc94-121">Authentication isn't mandatory, but if your app is something like a ticket tracking tool, you may need people to sign in to use the messaging extension.</span></span>

<span data-ttu-id="9cc94-122">Чтобы обеспечить согласованность Teams приложений, нельзя настроить экран входного знака.</span><span class="sxs-lookup"><span data-stu-id="9cc94-122">For consistency across Teams apps, you can't customize the sign-in screen.</span></span> <span data-ttu-id="9cc94-123">При использовании проверки подлинности с одним входом (SSO) пользователи автоматически подписываются.</span><span class="sxs-lookup"><span data-stu-id="9cc94-123">If you use single sign-on (SSO) authentication, users are signed in automatically.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="9cc94-124">Desktop</span><span class="sxs-lookup"><span data-stu-id="9cc94-124">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/set-up.png" alt-text="В примере показан экран установки расширения обмена сообщениями с кнопкой вход." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="9cc94-126">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="9cc94-126">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-set-up.png" alt-text="В примере показан экран установки расширения обмена сообщениями с кнопкой вход на мобильный телефон." border="false":::

---

## <a name="types-of-messaging-extensions"></a><span data-ttu-id="9cc94-128">Типы расширений обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="9cc94-128">Types of messaging extensions</span></span>

<span data-ttu-id="9cc94-129">Расширения обмена сообщениями могут иметь команды поиска, команды действий или оба.</span><span class="sxs-lookup"><span data-stu-id="9cc94-129">Messaging extensions can have search commands, action commands, or both.</span></span> <span data-ttu-id="9cc94-130">Ваши команды зависят от функций приложения и от того, как они подходят Teams случаях.</span><span class="sxs-lookup"><span data-stu-id="9cc94-130">Your commands depend on your app's features and how those fit within Teams use cases.</span></span>

### <a name="search-commands"></a><span data-ttu-id="9cc94-131">Команды поиска</span><span class="sxs-lookup"><span data-stu-id="9cc94-131">Search commands</span></span>

<span data-ttu-id="9cc94-132">С помощью команд поиска люди могут использовать расширение обмена сообщениями для быстрого поиска внешнего контента и вставки в сообщение.</span><span class="sxs-lookup"><span data-stu-id="9cc94-132">With search commands, people can use your messaging extension to quickly find external content and insert into a message.</span></span> <span data-ttu-id="9cc94-133">Команды поиска обычно доступны в окне составить.</span><span class="sxs-lookup"><span data-stu-id="9cc94-133">Search commands are commonly made available in the compose box.</span></span> <span data-ttu-id="9cc94-134">Например, вы можете начать или добавить в обсуждение, поделившись частью контента, не покидая Teams.</span><span class="sxs-lookup"><span data-stu-id="9cc94-134">For example, you can start or add to a discussion by sharing a piece of content—without ever leaving Teams.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="9cc94-135">Desktop</span><span class="sxs-lookup"><span data-stu-id="9cc94-135">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/search-command-type.png" alt-text="В примере показано расширение обмена сообщениями на основе поиска, запущенное из окна составить." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="9cc94-137">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="9cc94-137">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-search-command-type.png" alt-text="В примере показано расширение обмена сообщениями на основе поиска, запущенное из окна составить на мобильных устройствах." border="false":::

---

#### <a name="compose-box-layout-options"></a><span data-ttu-id="9cc94-139">Параметры композитного макета полей</span><span class="sxs-lookup"><span data-stu-id="9cc94-139">Compose box layout options</span></span>

<span data-ttu-id="9cc94-140">У вас есть несколько вариантов отображения результатов поиска расширения обмена сообщениями, включая [представления списков и сетки.](../../messaging-extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests)</span><span class="sxs-lookup"><span data-stu-id="9cc94-140">You have some options for displaying messaging extension search results, including [list and grid views](../../messaging-extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests).</span></span>

:::image type="content" source="../../assets/images/messaging-extension/search-result-layout.png" alt-text="На иллюстрациях показаны параметры макета результатов поиска расширения обмена сообщениями." border="false":::

### <a name="action-commands"></a><span data-ttu-id="9cc94-142">Команды действий</span><span class="sxs-lookup"><span data-stu-id="9cc94-142">Action commands</span></span>

<span data-ttu-id="9cc94-143">Команды действий позволяют пользователям запускать действия и обрабатывать запросы во внешних службах в Teams.</span><span class="sxs-lookup"><span data-stu-id="9cc94-143">Action commands allow people to trigger actions and process requests in external services within Teams.</span></span> <span data-ttu-id="9cc94-144">Например, если приложение отслеживает заказы, пользователь может создать новый порядок с помощью содержимого сообщения коллеги прямо в чате.</span><span class="sxs-lookup"><span data-stu-id="9cc94-144">For example, if your app tracks orders, a user could create a new order using the contents of a colleague’s message from right inside their chat.</span></span>

<span data-ttu-id="9cc94-145">Расширения обмена сообщениями на основе действий часто требуют, чтобы пользователи заполняли форму или другую конфигурацию в модале.</span><span class="sxs-lookup"><span data-stu-id="9cc94-145">Action-based messaging extensions frequently require users to complete a form or some other kind of configuration within a modal.</span></span> <span data-ttu-id="9cc94-146">Эти возможности можно создавать с помощью [модулей задач.](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)</span><span class="sxs-lookup"><span data-stu-id="9cc94-146">You can create these experiences with [task modules](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).</span></span>

## <a name="open-a-messaging-extension"></a><span data-ttu-id="9cc94-147">Откройте расширение обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="9cc94-147">Open a messaging extension</span></span>

<span data-ttu-id="9cc94-148">Основной контекст, в котором люди используют расширения обмена сообщениями, — это шкатулка, а также сообщения или сообщения.</span><span class="sxs-lookup"><span data-stu-id="9cc94-148">The compose box and messages or posts are the primary contexts where people use messaging extensions.</span></span>

### <a name="from-the-compose-box"></a><span data-ttu-id="9cc94-149">Из окне композит</span><span class="sxs-lookup"><span data-stu-id="9cc94-149">From the compose box</span></span>

<span data-ttu-id="9cc94-150">После добавления пользователи могут открыть расширение обмена сообщениями, выбрав значок приложения под полем составить.</span><span class="sxs-lookup"><span data-stu-id="9cc94-150">Once added, users can open your messaging extension by selecting your app icon below the compose box.</span></span> <span data-ttu-id="9cc94-151">В этих примерах расширение имеет команды поиска и действий.</span><span class="sxs-lookup"><span data-stu-id="9cc94-151">In these examples, the extension has search and action commands.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="9cc94-152">Desktop</span><span class="sxs-lookup"><span data-stu-id="9cc94-152">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/open-from-compose-box.png" alt-text="В примере показано, как открыть расширение обмена сообщениями из окна составить." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="9cc94-154">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="9cc94-154">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-open-from-compose-box.png" alt-text="В примере показано, как открыть расширение обмена сообщениями из окна составить на мобильном телефоне." border="false":::

---

### <a name="from-a-chat-message-or-channel-post"></a><span data-ttu-id="9cc94-156">Из сообщения чата или сообщения канала</span><span class="sxs-lookup"><span data-stu-id="9cc94-156">From a chat message or channel post</span></span>

После добавления пользователи могут выбрать значок **More** в сообщении чата или сообщении канала, чтобы найти команды действий :::image type="icon" source="../../assets/icons/teams-client-more.png"::: вашего расширения. <span data-ttu-id="9cc94-158">Расширение может быть перечислены в **статье Дополнительные действия,** основанные на использовании.</span><span class="sxs-lookup"><span data-stu-id="9cc94-158">Your extension may be listed under **More actions** based on usage.</span></span>

> [!NOTE]
> <span data-ttu-id="9cc94-159">Поддержка дополнительных действий из сообщения чата или сообщения канала недоступна на Microsoft Teams платформе.</span><span class="sxs-lookup"><span data-stu-id="9cc94-159">Support for more actions from a chat message or channel post is not available on Microsoft Teams mobile platform.</span></span> 

#### <a name="chat-message"></a><span data-ttu-id="9cc94-160">Сообщение чата</span><span class="sxs-lookup"><span data-stu-id="9cc94-160">Chat message</span></span>

# <a name="desktop"></a>[<span data-ttu-id="9cc94-161">Desktop</span><span class="sxs-lookup"><span data-stu-id="9cc94-161">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/open-from-chat-message.png" alt-text="В примере показано, как открыть расширение обмена сообщениями из сообщения чата." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="9cc94-163">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="9cc94-163">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-open-from-chat-post.png" alt-text="В примере показано, как открыть расширение обмена сообщениями из сообщения чата на мобильном телефоне." border="false":::

---
':::image type="content" source="../../assets/images/messaging-extension/open-from-channel-post.png" alt-text="Example shows how to open a messaging extension from a channel post on mobile." border="false"::': null
':::image type="content" source="../../assets/images/messaging-extension/mobile-open-from-channel-post.png" alt-text="Example shows how to open a messaging extension from a channel post on mobile." border="false"::': null
---

## <a name="use-a-messaging-extension"></a><span data-ttu-id="9cc94-165">Использование расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="9cc94-165">Use a messaging extension</span></span>

<span data-ttu-id="9cc94-166">В следующих сценариях покажут основные способы использования расширений обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="9cc94-166">The following scenarios show the primary ways people use messaging extensions.</span></span>

### <a name="insert-content-into-a-message"></a><span data-ttu-id="9cc94-167">Вставка контента в сообщение</span><span class="sxs-lookup"><span data-stu-id="9cc94-167">Insert content into a message</span></span>

<span data-ttu-id="9cc94-168">**1. Выберите расширение обмена сообщениями.**</span><span class="sxs-lookup"><span data-stu-id="9cc94-168">**1. Select a messaging extension**.</span></span> <span data-ttu-id="9cc94-169">Пользователи могут искать содержимое, которое они хотят поделиться из окна составить.</span><span class="sxs-lookup"><span data-stu-id="9cc94-169">Users can search for the content they want to share from the compose box.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="9cc94-170">Desktop</span><span class="sxs-lookup"><span data-stu-id="9cc94-170">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/insert-content-search.png" alt-text="В примере показано, как пользователь ищет содержимое для вставки из окне композитной записи." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="9cc94-172">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="9cc94-172">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-insert-content-search.png" alt-text="В примере показано, как пользователь ищет контент для вставки из окна записи на мобильном телефоне." border="false":::

---

<span data-ttu-id="9cc94-174">**2. Вставьте содержимое**.</span><span class="sxs-lookup"><span data-stu-id="9cc94-174">**2. Insert content**.</span></span> <span data-ttu-id="9cc94-175">После публикации другие могут отвечать или выбирать содержимое, чтобы увидеть дополнительные сведения в приложении.</span><span class="sxs-lookup"><span data-stu-id="9cc94-175">Once posted, others can reply or select the content to see more information in your app.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="9cc94-176">Desktop</span><span class="sxs-lookup"><span data-stu-id="9cc94-176">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/insert-content-posted.png" alt-text="В примере показана публикация контента пользователя в разговоре с каналом." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="9cc94-178">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="9cc94-178">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-insert-content-posted.png" alt-text="В примере показана публикация контента пользователя в разговоре по каналу на мобильном телефоне." border="false":::

---

### <a name="take-action-on-a-message"></a><span data-ttu-id="9cc94-180">Действие по сообщению</span><span class="sxs-lookup"><span data-stu-id="9cc94-180">Take action on a message</span></span>

<span data-ttu-id="9cc94-181">**1. Выберите расширение обмена сообщениями.**</span><span class="sxs-lookup"><span data-stu-id="9cc94-181">**1. Select a messaging extension**.</span></span> <span data-ttu-id="9cc94-182">Ваше приложение может включать одну или несколько команд действий.</span><span class="sxs-lookup"><span data-stu-id="9cc94-182">Your app can include one or more action commands.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="9cc94-183">Desktop</span><span class="sxs-lookup"><span data-stu-id="9cc94-183">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/select-action-command.png" alt-text="В примере показано, как пользователь выбирает команду действий по расширению обмена сообщениями." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="9cc94-185">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="9cc94-185">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-select-action-command.png" alt-text="В примере показано, как пользователь выбирает команду действий по расширению обмена сообщениями на мобильном телефоне." border="false":::

---

<span data-ttu-id="9cc94-187">**2. Завершить действие**.</span><span class="sxs-lookup"><span data-stu-id="9cc94-187">**2. Complete the action**.</span></span> <span data-ttu-id="9cc94-188">Ваше приложение может получать и обрабатывать любое содержимое или данные, отправленные действием сообщения.</span><span class="sxs-lookup"><span data-stu-id="9cc94-188">Your app can receive and process any content or data sent by the message action.</span></span> <span data-ttu-id="9cc94-189">Это позволяет пользователям оставаться в беседе и, в следующем примере, не беспокоиться о вводе сведений непосредственно в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="9cc94-189">This allows users to remain in their conversation and, the following example, not worry about entering information directly in your app.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="9cc94-190">Desktop</span><span class="sxs-lookup"><span data-stu-id="9cc94-190">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/complete-action-command.png" alt-text="Пример действий по сообщению." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="9cc94-192">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="9cc94-192">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-complete-action-command.png" alt-text="Пример действий по сообщению на мобильных устройствах." border="false":::

---

### <a name="preview-links"></a><span data-ttu-id="9cc94-194">Предварительные ссылки</span><span class="sxs-lookup"><span data-stu-id="9cc94-194">Preview links</span></span>

<span data-ttu-id="9cc94-195">Расширения обмена сообщениями также позволяют вставлять богатые ссылки из распознаемого URL-адреса в сообщение (эта возможность называется [unfurling link unfurling.)](../../messaging-extensions/how-to/link-unfurling.md)</span><span class="sxs-lookup"><span data-stu-id="9cc94-195">Messaging extensions also allow you to insert rich links from a recognized URL into a message (this capability is called [link unfurling](../../messaging-extensions/how-to/link-unfurling.md).)</span></span>

<span data-ttu-id="9cc94-196">**1. Вклеить распознаемую ссылку** в поле составить.</span><span class="sxs-lookup"><span data-stu-id="9cc94-196">**1. Paste a recognized link** in the compose box.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="9cc94-197">Desktop</span><span class="sxs-lookup"><span data-stu-id="9cc94-197">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/paste-preview-link.png" alt-text="В примере показано, как пользователь вклеит ссылку в поле компоста." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="9cc94-199">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="9cc94-199">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-paste-preview-link.png" alt-text="В примере показано, как пользователь вклеит ссылку в поле компоста на мобильный телефон." border="false":::

---

<span data-ttu-id="9cc94-201">**2. Вставьте содержимое**.</span><span class="sxs-lookup"><span data-stu-id="9cc94-201">**2. Insert content**.</span></span> <span data-ttu-id="9cc94-202">Если ваше приложение распознает URL-адрес в окне композит, оно отрисовка ссылки в качестве карточки, которая обеспечивает богатый контентом предварительный просмотр веб-контента.</span><span class="sxs-lookup"><span data-stu-id="9cc94-202">If your app recognizes the URL in the compose box, it renders the link as a card that provides a content-rich preview of the web content.</span></span> <span data-ttu-id="9cc94-203">[(Дополнительные сведения](../../task-modules-and-cards/cards/design-effective-cards.md) см. в рекомендациях по разработке адаптивных карт.)</span><span class="sxs-lookup"><span data-stu-id="9cc94-203">(See [Adaptive Cards design guidelines](../../task-modules-and-cards/cards/design-effective-cards.md) for more information.)</span></span>

# <a name="desktop"></a>[<span data-ttu-id="9cc94-204">Desktop</span><span class="sxs-lookup"><span data-stu-id="9cc94-204">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/insert-preview-link.png" alt-text="В примере показано, как URL-адрес, так как он распознается вашим приложением, содержит в окне композитного контента некоторое содержимое." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="9cc94-206">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="9cc94-206">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-insert-preview-link.png" alt-text="В примере показано, как URL-адрес, так как он распознается вашим приложением, содержит некоторые материалы в поле составить на мобильных устройствах." border="false":::

---

## <a name="manage-a-messaging-extension"></a><span data-ttu-id="9cc94-208">Управление расширением обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="9cc94-208">Manage a messaging extension</span></span>

<span data-ttu-id="9cc94-209">Щелкнув правой кнопкой мыши значок, пользователи могут прикрепить, удалить или настроить расширение обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="9cc94-209">By right clicking your icon, users can pin, remove, or configure your messaging extension.</span></span>

## <a name="anatomy"></a><span data-ttu-id="9cc94-210">Анатомия</span><span class="sxs-lookup"><span data-stu-id="9cc94-210">Anatomy</span></span>

### <a name="messaging-extension-in-the-compose-box"></a><span data-ttu-id="9cc94-211">Расширение обмена сообщениями в окне составить</span><span class="sxs-lookup"><span data-stu-id="9cc94-211">Messaging extension in the compose box</span></span>

<span data-ttu-id="9cc94-212">В следующем примере можно привести расширение обмена сообщениями, открытое из окна составить.</span><span class="sxs-lookup"><span data-stu-id="9cc94-212">The following example is a messaging extension opened from the compose box.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="9cc94-213">Desktop</span><span class="sxs-lookup"><span data-stu-id="9cc94-213">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/anatomy-compose.png" alt-text="Иллюстрация, показывающая анатомию пользовательского интерфейса расширения обмена сообщениями в окне составить." border="false":::

|<span data-ttu-id="9cc94-215">Счетчик</span><span class="sxs-lookup"><span data-stu-id="9cc94-215">Counter</span></span>|<span data-ttu-id="9cc94-216">Описание</span><span class="sxs-lookup"><span data-stu-id="9cc94-216">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="9cc94-217">1</span><span class="sxs-lookup"><span data-stu-id="9cc94-217">1</span></span>|<span data-ttu-id="9cc94-218">**Логотип приложения.** Значок цвета логотипа приложения.</span><span class="sxs-lookup"><span data-stu-id="9cc94-218">**App logo**: Color icon of your app logo.</span></span>|
|<span data-ttu-id="9cc94-219">2</span><span class="sxs-lookup"><span data-stu-id="9cc94-219">2</span></span>|<span data-ttu-id="9cc94-220">**Имя приложения.** Полное имя вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="9cc94-220">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="9cc94-221">3</span><span class="sxs-lookup"><span data-stu-id="9cc94-221">3</span></span>|<span data-ttu-id="9cc94-222">**Значок меню action commands (необязательный)**: Открывает список команд действий для расширения обмена сообщениями (если вы указываете их).</span><span class="sxs-lookup"><span data-stu-id="9cc94-222">**Action commands menu icon (optional)**: Opens a list of action commands for your messaging extension (if you specify any).</span></span>
|<span data-ttu-id="9cc94-223">4 </span><span class="sxs-lookup"><span data-stu-id="9cc94-223">4</span></span>|<span data-ttu-id="9cc94-224">**Поле поиска.** Позволяет пользователям находить содержимое приложения, которое они хотят вставить.</span><span class="sxs-lookup"><span data-stu-id="9cc94-224">**Search box**: Allows users to find app content they want to insert.</span></span>|
|<span data-ttu-id="9cc94-225">5 </span><span class="sxs-lookup"><span data-stu-id="9cc94-225">5</span></span>|<span data-ttu-id="9cc94-226">**Меню Tab (необязательный)**: предоставляет несколько категорий контента.</span><span class="sxs-lookup"><span data-stu-id="9cc94-226">**Tab menu (optional)**: Provides multiple content categories.</span></span>|
|<span data-ttu-id="9cc94-227">6 </span><span class="sxs-lookup"><span data-stu-id="9cc94-227">6</span></span>|<span data-ttu-id="9cc94-228">**Меню команд действий (необязательный)**: отображает список команд действий (если указаны какие-либо).</span><span class="sxs-lookup"><span data-stu-id="9cc94-228">**Action commands menu (optional)**: Displays list of action commands (if you specify any).</span></span>|
|<span data-ttu-id="9cc94-229">7 </span><span class="sxs-lookup"><span data-stu-id="9cc94-229">7</span></span>|<span data-ttu-id="9cc94-230">**Содержимое приложения.** В первую очередь для отображения результатов поиска.</span><span class="sxs-lookup"><span data-stu-id="9cc94-230">**App content**: Primarily to display search results.</span></span> <span data-ttu-id="9cc94-231">В этом примере используется макет списка (макет сетки — это другой вариант).</span><span class="sxs-lookup"><span data-stu-id="9cc94-231">The example here is using the list layout (grid layout is another option).</span></span>|
|<span data-ttu-id="9cc94-232">8 </span><span class="sxs-lookup"><span data-stu-id="9cc94-232">8</span></span>|<span data-ttu-id="9cc94-233">**Логотип приложения.** Значок контура логотипа приложения.</span><span class="sxs-lookup"><span data-stu-id="9cc94-233">**App logo**: Outline icon of your app logo.</span></span>|

# <a name="mobile"></a>[<span data-ttu-id="9cc94-234">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="9cc94-234">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-anatomy-compose.png" alt-text="Иллюстрация, показывающая анатомию пользовательского интерфейса расширения обмена сообщениями в поле составить на мобильных устройствах." border="false":::

|<span data-ttu-id="9cc94-236">Счетчик</span><span class="sxs-lookup"><span data-stu-id="9cc94-236">Counter</span></span>|<span data-ttu-id="9cc94-237">Описание</span><span class="sxs-lookup"><span data-stu-id="9cc94-237">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="9cc94-238">1</span><span class="sxs-lookup"><span data-stu-id="9cc94-238">1</span></span>|<span data-ttu-id="9cc94-239">**Имя приложения.** Полное имя вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="9cc94-239">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="9cc94-240">2</span><span class="sxs-lookup"><span data-stu-id="9cc94-240">2</span></span>|<span data-ttu-id="9cc94-241">**Значок меню action commands (необязательный)**: Открывает список команд действий для расширения обмена сообщениями (если вы указываете их).</span><span class="sxs-lookup"><span data-stu-id="9cc94-241">**Action commands menu icon (optional)**: Opens a list of action commands for your messaging extension (if you specify any).</span></span>
|<span data-ttu-id="9cc94-242">3</span><span class="sxs-lookup"><span data-stu-id="9cc94-242">3</span></span>|<span data-ttu-id="9cc94-243">**Поле поиска.** Позволяет пользователям находить содержимое приложения, которое они хотят вставить.</span><span class="sxs-lookup"><span data-stu-id="9cc94-243">**Search box**: Allows users to find app content they want to insert.</span></span>|
|<span data-ttu-id="9cc94-244">4 </span><span class="sxs-lookup"><span data-stu-id="9cc94-244">4</span></span>|<span data-ttu-id="9cc94-245">**Меню Tab (необязательный)**: предоставляет несколько категорий контента.</span><span class="sxs-lookup"><span data-stu-id="9cc94-245">**Tab menu (optional)**: Provides multiple content categories.</span></span>|
|<span data-ttu-id="9cc94-246">5 </span><span class="sxs-lookup"><span data-stu-id="9cc94-246">5</span></span>|<span data-ttu-id="9cc94-247">**Меню команд действий (необязательный)**: отображает список команд действий (если указаны какие-либо).</span><span class="sxs-lookup"><span data-stu-id="9cc94-247">**Action commands menu (optional)**: Displays list of action commands (if you specify any).</span></span>|
|<span data-ttu-id="9cc94-248">6 </span><span class="sxs-lookup"><span data-stu-id="9cc94-248">6</span></span>|<span data-ttu-id="9cc94-249">**Содержимое приложения.** В первую очередь для отображения результатов поиска.</span><span class="sxs-lookup"><span data-stu-id="9cc94-249">**App content**: Primarily to display search results.</span></span>|

---

### <a name="messaging-extension-management-menu"></a><span data-ttu-id="9cc94-250">Меню управления расширением обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="9cc94-250">Messaging extension management menu</span></span>

:::image type="content" source="../../assets/images/messaging-extension/anatomy-management-menu.png" alt-text="Иллюстрация, показывающая анатомию пользовательского интерфейса меню управления расширением обмена сообщениями." border="false":::

|<span data-ttu-id="9cc94-252">Счетчик</span><span class="sxs-lookup"><span data-stu-id="9cc94-252">Counter</span></span>|<span data-ttu-id="9cc94-253">Описание</span><span class="sxs-lookup"><span data-stu-id="9cc94-253">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="9cc94-254">1</span><span class="sxs-lookup"><span data-stu-id="9cc94-254">1</span></span>|<span data-ttu-id="9cc94-255">**Unpin.** Доступно, если пользователь прикрепил приложение.</span><span class="sxs-lookup"><span data-stu-id="9cc94-255">**Unpin**: Available if the user has pinned your app.</span></span>|
|<span data-ttu-id="9cc94-256">2</span><span class="sxs-lookup"><span data-stu-id="9cc94-256">2</span></span>|<span data-ttu-id="9cc94-257">**Удаление.** Удаляет расширение обмена сообщениями из канала, чата или собрания.</span><span class="sxs-lookup"><span data-stu-id="9cc94-257">**Remove**: Removes the messaging extension from the channel, chat, or meeting.</span></span>|

## <a name="best-practices"></a><span data-ttu-id="9cc94-258">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="9cc94-258">Best practices</span></span>

<span data-ttu-id="9cc94-259">Используйте эти рекомендации для создания качественного приложения.</span><span class="sxs-lookup"><span data-stu-id="9cc94-259">Use these recommendations to create a quality app experience.</span></span>

### <a name="setup-and-general-usage"></a><span data-ttu-id="9cc94-260">Настройка и общее использование</span><span class="sxs-lookup"><span data-stu-id="9cc94-260">Setup and general usage</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-do.png" alt-text="Пример установки и общего использования." border="false":::

#### <a name="do-integrate-with-single-sign-on"></a><span data-ttu-id="9cc94-262">Do: Интеграция с одним входом</span><span class="sxs-lookup"><span data-stu-id="9cc94-262">Do: Integrate with single-sign on</span></span>

<span data-ttu-id="9cc94-263">SSO упрощает процесс регистрации, быстрее и обеспечивает безопасность.</span><span class="sxs-lookup"><span data-stu-id="9cc94-263">SSO makes the sign-in process easier, faster, and secure.</span></span> <span data-ttu-id="9cc94-264">Кроме того, если пользователь уже зарегистрировался в вашем личном приложении, для доступа к расширению обмена сообщениями также не нужно снова входить.</span><span class="sxs-lookup"><span data-stu-id="9cc94-264">Also, if a user has already signed in to your personal app, they don’t have to also sign in again to access the messaging extension.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-dont.png" alt-text="Пример интеграции с одним входом." border="false":::

#### <a name="dont-take-users-away-from-the-conversation"></a><span data-ttu-id="9cc94-266">Не: отбирайте пользователей из беседы</span><span class="sxs-lookup"><span data-stu-id="9cc94-266">Don't: Take users away from the conversation</span></span>

<span data-ttu-id="9cc94-267">Расширения обмена сообщениями — это ярлыки, которые, как предполагается, уменьшают переключение контекста.</span><span class="sxs-lookup"><span data-stu-id="9cc94-267">Messaging extensions are shortcuts that are supposed reduce context switching.</span></span> <span data-ttu-id="9cc94-268">Например, расширение не должно направлять пользователей на веб-страницу за пределами Teams.</span><span class="sxs-lookup"><span data-stu-id="9cc94-268">Your extension should not, for example, direct users to a webpage outside Teams.</span></span>

   :::column-end:::
:::row-end:::

#### <a name="do-highlight-your-messaging-extension"></a><span data-ttu-id="9cc94-269">Do: Highlight your messaging extension</span><span class="sxs-lookup"><span data-stu-id="9cc94-269">Do: Highlight your messaging extension</span></span>

<span data-ttu-id="9cc94-270">Расширения обмена сообщениями не всегда легко найти.</span><span class="sxs-lookup"><span data-stu-id="9cc94-270">Messaging extensions aren't always easy to find.</span></span> <span data-ttu-id="9cc94-271">Включите скриншоты использования этого приложения на странице сведения о приложении.</span><span class="sxs-lookup"><span data-stu-id="9cc94-271">Include screenshots of how to use it in your app details page.</span></span> <span data-ttu-id="9cc94-272">Если в вашем приложении также есть бот, вы можете включить документацию по расширению обмена сообщениями в приветственный тур бота.</span><span class="sxs-lookup"><span data-stu-id="9cc94-272">If your app also includes a bot, you can include messaging extension help documentation in a bot welcome tour.</span></span>

### <a name="templating"></a><span data-ttu-id="9cc94-273">Templating</span><span class="sxs-lookup"><span data-stu-id="9cc94-273">Templating</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-do.png" alt-text="Пример шаблона." border="false":::

#### <a name="do-let-teams-handle-some-of-the-design-work-if-possible"></a><span data-ttu-id="9cc94-275">Do: по возможности Teams некоторые работы по проектированию</span><span class="sxs-lookup"><span data-stu-id="9cc94-275">Do: Let Teams handle some of the design work if possible</span></span>

<span data-ttu-id="9cc94-276">Если это имеет смысл для случаев использования, рассмотрите возможность создания расширения обмена сообщениями на основе поиска.</span><span class="sxs-lookup"><span data-stu-id="9cc94-276">If it makes sense for your use cases, consider creating a search-based messaging extension.</span></span> <span data-ttu-id="9cc94-277">Teams эти типы расширений со встроенной темой и доступностью.</span><span class="sxs-lookup"><span data-stu-id="9cc94-277">Teams renders these types of extensions with built-in theming and accessibility.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-dont.png" alt-text="Пример обработки работ по проектированию." border="false":::

#### <a name="dont-embed-your-entire-app-in-a-task-module"></a><span data-ttu-id="9cc94-279">Не: встраить все приложение в модуль задач</span><span class="sxs-lookup"><span data-stu-id="9cc94-279">Don't: Embed your entire app in a task module</span></span>

<span data-ttu-id="9cc94-280">Если расширение обмена сообщениями требует команд действий, сохраняйте простой модуль задач и отображайте только компоненты, необходимые для выполнения действия.</span><span class="sxs-lookup"><span data-stu-id="9cc94-280">If your messaging extension requires action commands, keep the task module simple and display only the components required to complete the action.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="9cc94-281">Темы</span><span class="sxs-lookup"><span data-stu-id="9cc94-281">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-do.png" alt-text="Пример на теме." border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a><span data-ttu-id="9cc94-283">Do: Воспользоваться преимуществами Teams цветовых маркеров</span><span class="sxs-lookup"><span data-stu-id="9cc94-283">Do: Take advantage of Teams color tokens</span></span>

<span data-ttu-id="9cc94-284">Каждая Teams имеет свою цветовую схему.</span><span class="sxs-lookup"><span data-stu-id="9cc94-284">Each Teams theme has its own color scheme.</span></span> <span data-ttu-id="9cc94-285">Чтобы автоматически обрабатывать изменения темы, используйте маркеры цвета <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">(Fluent UI)</a> в своем дизайне.</span><span class="sxs-lookup"><span data-stu-id="9cc94-285">To handle theme changes automatically, use <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a> in your design.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-dont.png" alt-text="Пример с цветными маркерами." border="false":::

#### <a name="dont-hard-code-color-values"></a><span data-ttu-id="9cc94-287">Не: значения цвета жесткого кода</span><span class="sxs-lookup"><span data-stu-id="9cc94-287">Don't: Hard code color values</span></span>

<span data-ttu-id="9cc94-288">Если вы не используете маркеры Teams цвета, ваши проекты будут менее масштабируемыми и у вас будет больше времени для управления.</span><span class="sxs-lookup"><span data-stu-id="9cc94-288">If you don't use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::

### <a name="actions"></a><span data-ttu-id="9cc94-289">Действия</span><span class="sxs-lookup"><span data-stu-id="9cc94-289">Actions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-do.png" alt-text="Пример действий." border="false":::

#### <a name="do-include-action-commands-that-make-sense-in-context"></a><span data-ttu-id="9cc94-291">Do: Включить команды действий, которые в контексте являются смыслом</span><span class="sxs-lookup"><span data-stu-id="9cc94-291">Do: Include action commands that make sense in context</span></span>

<span data-ttu-id="9cc94-292">Действия сообщения должны относиться к тем, на что смотрит пользователь.</span><span class="sxs-lookup"><span data-stu-id="9cc94-292">Message actions should relate to what a user is looking at.</span></span> <span data-ttu-id="9cc94-293">Например, укажи пользователям ярлык для создания проблемы или рабочих элементов с помощью текста в чьей-либо публикации.</span><span class="sxs-lookup"><span data-stu-id="9cc94-293">For example, provide users a shortcut for creating an issue or work item using the text in someone’s post.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-dont.png" alt-text="Пример команд действий." border="false":::

#### <a name="dont-include-actions-commands-that-arent-contextual"></a><span data-ttu-id="9cc94-295">Не: включайте не контекстуальные команды действий</span><span class="sxs-lookup"><span data-stu-id="9cc94-295">Don't: Include actions commands that aren't contextual</span></span>

<span data-ttu-id="9cc94-296">Действие сообщения для **просмотра панели мониторинга** может показаться отключенным от большинства бесед.</span><span class="sxs-lookup"><span data-stu-id="9cc94-296">A message action to **View your dashboard** would probably seem disconnected from most conversations.</span></span>

   :::column-end:::
:::row-end:::

### <a name="searches"></a><span data-ttu-id="9cc94-297">Поиск</span><span class="sxs-lookup"><span data-stu-id="9cc94-297">Searches</span></span>

#### <a name="do-show-search-results-while-typing"></a><span data-ttu-id="9cc94-298">Do: Показать результаты поиска при вводе</span><span class="sxs-lookup"><span data-stu-id="9cc94-298">Do: Show search results while typing</span></span>

<span data-ttu-id="9cc94-299">Предоставление предлагаемых результатов поиска при введите пользователей.</span><span class="sxs-lookup"><span data-stu-id="9cc94-299">Provide suggested search results while users type.</span></span> <span data-ttu-id="9cc94-300">Они могут быстрее находить нужный контент с минимальным количеством символов.</span><span class="sxs-lookup"><span data-stu-id="9cc94-300">They may find the content they need faster with minimal amount of characters.</span></span>

#### <a name="dont-require-users-to-submit-a-query"></a><span data-ttu-id="9cc94-301">Не: требовать от пользователей отправки запроса</span><span class="sxs-lookup"><span data-stu-id="9cc94-301">Don't: Require users to submit a query</span></span>

<span data-ttu-id="9cc94-302">Вы можете заставить пользователей нажать клавишу или выбрать кнопку для отправки запросов в ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="9cc94-302">You can make users press a key or select a button to send queries to your app.</span></span> <span data-ttu-id="9cc94-303">Хотя это может быть проще в службе служб приложений, люди могут быть смущены тем, что они не видят результатов поиска в режиме реального времени, как они введите.</span><span class="sxs-lookup"><span data-stu-id="9cc94-303">While that may be easier on your app services service, people may be confused that they're not seeing real-time search results as they type.</span></span>

#### <a name="do-consider-zero-term-queries"></a><span data-ttu-id="9cc94-304">Do: Рассмотрите запросы с нулевым сроком</span><span class="sxs-lookup"><span data-stu-id="9cc94-304">Do: Consider zero-term queries</span></span>

<span data-ttu-id="9cc94-305">Например, перед тем, как пользователь записывает что-либо в поле поиска, отобразите то, что он последний раз просматривал в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="9cc94-305">For example, before a user writes anything in the search box, display what they last viewed on your app.</span></span> <span data-ttu-id="9cc94-306">Вполне возможно, что они хотят вставить этот контент в беседу.</span><span class="sxs-lookup"><span data-stu-id="9cc94-306">It's possible that they want to insert that content into their conversation.</span></span>
