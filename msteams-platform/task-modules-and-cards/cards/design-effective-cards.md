---
title: Разработка адаптивных карточек для приложения
description: Узнайте, как создать адаптивные карточки для Teams и получить комплект разработчика для пользовательского интерфейса Microsoft Teams.
localization_priority: Priority
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 8e56928da44e22006feb59715c8bdbf821ec4c42
ms.sourcegitcommit: 99b1f151e4e36a86c6a5d2ccbde01bf45b61f526
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/21/2021
ms.locfileid: "53037658"
---
# <a name="designing-adaptive-cards-for-your-microsoft-teams-app"></a><span data-ttu-id="6e1ed-103">Разработка адаптивных карточек для приложения Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="6e1ed-103">Designing Adaptive Cards for your Microsoft Teams app</span></span>

<span data-ttu-id="6e1ed-104">Адаптивная карточка содержит произвольный текст элементов карточки и необязательный набор действий.</span><span class="sxs-lookup"><span data-stu-id="6e1ed-104">An Adaptive Card contains a freeform body of card elements and optional set of actions.</span></span> <span data-ttu-id="6e1ed-105">Адаптивные карточки — это фрагменты содержимого с действиями, которые можно добавить в беседу с помощью бота или расширения для сообщений.</span><span class="sxs-lookup"><span data-stu-id="6e1ed-105">Adaptive Cards are actionable snippets of content that you can add to a conversation through a bot or messaging extension.</span></span> <span data-ttu-id="6e1ed-106">Эти карточки с помощью текста, графики и кнопок обеспечивают широкие возможности взаимодействия с аудиторией.</span><span class="sxs-lookup"><span data-stu-id="6e1ed-106">Using text, graphics, and buttons, these cards provide rich communication to your audience.</span></span>

<span data-ttu-id="6e1ed-107">Инфраструктура адаптивных карточек используется во многих продуктах Майкрософт, включая Teams.</span><span class="sxs-lookup"><span data-stu-id="6e1ed-107">The Adaptive Card framework is used across many Microsoft products, including Teams.</span></span> <span data-ttu-id="6e1ed-108">Вы можете отправлять карточки внутри сообщений пользователям с помощью ботов или расширений для сообщений.</span><span class="sxs-lookup"><span data-stu-id="6e1ed-108">You can send cards inside messages to users via bots or messaging extensions.</span></span> <span data-ttu-id="6e1ed-109">Кроме того, пользователи могут выполнять действия в карточках при их просмотре.</span><span class="sxs-lookup"><span data-stu-id="6e1ed-109">Users can also take actions on cards when present.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/adaptive-card-overview.png" alt-text="Обзор примера адаптивной карточки." border="false":::

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="6e1ed-111">Комплект разработчика для пользовательского интерфейса Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="6e1ed-111">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="6e1ed-112">В комплекте разработчика для пользовательского интерфейса Microsoft Teams можно найти более полные рекомендации по проектированию адаптивных карточек в Teams, в том числе элементы, которые можно изменять по своему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="6e1ed-112">You can find more comprehensive design guidelines for Adaptive Cards in Teams, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="6e1ed-113">В комплекте разработчика для пользовательского интерфейса также охвачены такие важные области, как тема, специальные возможности и адаптивный размер.</span><span class="sxs-lookup"><span data-stu-id="6e1ed-113">The UI kit also covers essential topics such as theming, accessibility, and responsive sizing.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6e1ed-114">Получить комплект разработчика для пользовательского интерфейса Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="6e1ed-114">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="adaptive-cards-designer"></a><span data-ttu-id="6e1ed-115">Конструктор адаптивных карточек</span><span class="sxs-lookup"><span data-stu-id="6e1ed-115">Adaptive Cards designer</span></span>

<span data-ttu-id="6e1ed-116">Вы также можете приступить к разработке адаптивных карточек непосредственно в браузере.</span><span class="sxs-lookup"><span data-stu-id="6e1ed-116">You also can start designing your Adaptive Cards directly in the browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6e1ed-117">Попробовать конструктор адаптивных карточек</span><span class="sxs-lookup"><span data-stu-id="6e1ed-117">Try the Adaptive Cards designer</span></span>](https://adaptivecards.io/designer/)

## <a name="types-of-adaptive-cards"></a><span data-ttu-id="6e1ed-118">Типы адаптивных карточек</span><span class="sxs-lookup"><span data-stu-id="6e1ed-118">Types of Adaptive Cards</span></span>

### <a name="hero"></a><span data-ttu-id="6e1ed-119">Главный имиджевый баннер</span><span class="sxs-lookup"><span data-stu-id="6e1ed-119">Hero</span></span>

<span data-ttu-id="6e1ed-120">Наша самая большая карточка.</span><span class="sxs-lookup"><span data-stu-id="6e1ed-120">Our largest card.</span></span> <span data-ttu-id="6e1ed-121">Используется для публикации статей или сценариев, в которых изображение играет важнейшую роль.</span><span class="sxs-lookup"><span data-stu-id="6e1ed-121">Use for sharing articles or scenarios where an image tells most of the story.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="6e1ed-122">Компьютер</span><span class="sxs-lookup"><span data-stu-id="6e1ed-122">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/hero-card.png" alt-text="Пример адаптивной карточки главного имиджевого баннера." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="6e1ed-124">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="6e1ed-124">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-hero-card.png" alt-text="Пример адаптивной карточки главного имиджевого баннера на мобильном устройстве." border="false":::

---

### <a name="thumbnail"></a><span data-ttu-id="6e1ed-126">Эскиз</span><span class="sxs-lookup"><span data-stu-id="6e1ed-126">Thumbnail</span></span>

<span data-ttu-id="6e1ed-127">Используется для отправки простого сообщения с действиями.</span><span class="sxs-lookup"><span data-stu-id="6e1ed-127">Use for sending a simple actionable message.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="6e1ed-128">Компьютер</span><span class="sxs-lookup"><span data-stu-id="6e1ed-128">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/thumbnail-card.png" alt-text="Пример адаптивной карточки эскиза." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="6e1ed-130">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="6e1ed-130">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-thumbnail-card.png" alt-text="Пример адаптивной карточки эскиза на мобильном устройстве." border="false":::

---

### <a name="list"></a><span data-ttu-id="6e1ed-132">Список</span><span class="sxs-lookup"><span data-stu-id="6e1ed-132">List</span></span>

<span data-ttu-id="6e1ed-133">Используется в сценариях, где пользователь должен выбирать элемент из списка, а элементам не требуется подробное объяснение.</span><span class="sxs-lookup"><span data-stu-id="6e1ed-133">Use in scenarios where you want the user to pick an item from a list, but the items don’t need a lot of explanation.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="6e1ed-134">Компьютер</span><span class="sxs-lookup"><span data-stu-id="6e1ed-134">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/list-card.png" alt-text="Пример адаптивной карточки списка." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="6e1ed-136">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="6e1ed-136">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-list-card.png" alt-text="Пример адаптивной карточки списка на мобильном устройстве." border="false":::

---
Use for news digests and round-up posts. Note: We recommend the thumbnail card for a single update or news item.
':::image type="content" source="../../assets/images/adaptive-cards/digest-card.png" alt-text="Example shows an Adaptive Card digest card." border="false"::': null
':::image type="content" source="../../assets/images/adaptive-cards/mobile-digest-card.png" alt-text="Example shows an Adaptive Card digest card on mobile." border="false"::': null
---

### <a name="media"></a><span data-ttu-id="6e1ed-138">Мультимедиа</span><span class="sxs-lookup"><span data-stu-id="6e1ed-138">Media</span></span>

<span data-ttu-id="6e1ed-139">Используется при объединении текста и мультимедиа, например звука или видео.</span><span class="sxs-lookup"><span data-stu-id="6e1ed-139">Use when you want to combine text and media, like audio or video.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="6e1ed-140">Компьютер</span><span class="sxs-lookup"><span data-stu-id="6e1ed-140">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/media-card.png" alt-text="Пример адаптивной карточки мультимедиа." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="6e1ed-142">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="6e1ed-142">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-media-card.png" alt-text="Пример адаптивной карточки мультимедиа на мобильном устройстве." border="false":::

---

### <a name="people"></a><span data-ttu-id="6e1ed-144">Люди</span><span class="sxs-lookup"><span data-stu-id="6e1ed-144">People</span></span>

<span data-ttu-id="6e1ed-145">Лучше всего использовать для эффективного уведомления о тех, кто участвует в задаче.</span><span class="sxs-lookup"><span data-stu-id="6e1ed-145">Best used when you to efficiently convey who's involved with a task.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="6e1ed-146">Компьютер</span><span class="sxs-lookup"><span data-stu-id="6e1ed-146">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/people-card.png" alt-text="Пример адаптивной карточки людей." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="6e1ed-148">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="6e1ed-148">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-people-card.png" alt-text="Пример адаптивной карточки людей на мобильном устройстве." border="false":::

---

### <a name="request-ticket"></a><span data-ttu-id="6e1ed-150">Запрос</span><span class="sxs-lookup"><span data-stu-id="6e1ed-150">Request ticket</span></span>

<span data-ttu-id="6e1ed-151">Используется для быстрого получения входных данных от пользователя с целью автоматического создания задачи или запроса.</span><span class="sxs-lookup"><span data-stu-id="6e1ed-151">Use to get quick inputs from a user to automatically create a task or ticket.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="6e1ed-152">Компьютер</span><span class="sxs-lookup"><span data-stu-id="6e1ed-152">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/request-ticket-card.png" alt-text="Пример адаптивной карточки запроса." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="6e1ed-154">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="6e1ed-154">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-request-ticket-card.png" alt-text="Пример адаптивной карточки запроса на мобильном устройстве." border="false":::

---

### <a name="image-set"></a><span data-ttu-id="6e1ed-156">Набор изображений</span><span class="sxs-lookup"><span data-stu-id="6e1ed-156">Image set</span></span>

<span data-ttu-id="6e1ed-157">Используется для отправки нескольких эскизов изображений.</span><span class="sxs-lookup"><span data-stu-id="6e1ed-157">Use to send multiple image thumbnails.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="6e1ed-158">Компьютер</span><span class="sxs-lookup"><span data-stu-id="6e1ed-158">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/image-set-card.png" alt-text="Пример адаптивной карточки набора изображений." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="6e1ed-160">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="6e1ed-160">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-image-set-card.png" alt-text="Пример адаптивной карточки набора изображений на мобильном устройстве." border="false":::

---

### <a name="action-set"></a><span data-ttu-id="6e1ed-162">Набор действий</span><span class="sxs-lookup"><span data-stu-id="6e1ed-162">Action set</span></span>

<span data-ttu-id="6e1ed-163">Используется, когда пользователю нужно нажимать кнопку с последующим сбором дополнительных входных данных пользователя с той же карточки.</span><span class="sxs-lookup"><span data-stu-id="6e1ed-163">Use when you want to the user to select a button, then gather addition user input from the same card.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="6e1ed-164">Компьютер</span><span class="sxs-lookup"><span data-stu-id="6e1ed-164">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/action-set-card.png" alt-text="Пример адаптивной карточки набора действий." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="6e1ed-166">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="6e1ed-166">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-action-set-card.png" alt-text="Пример адаптивной карточки набора действий на мобильном устройстве." border="false":::

---

### <a name="choice-set"></a><span data-ttu-id="6e1ed-168">Набор вариантов</span><span class="sxs-lookup"><span data-stu-id="6e1ed-168">Choice set</span></span>

<span data-ttu-id="6e1ed-169">Используется для сбора нескольких входных данных от пользователя.</span><span class="sxs-lookup"><span data-stu-id="6e1ed-169">Use to gather multiple inputs from the user.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="6e1ed-170">Компьютер</span><span class="sxs-lookup"><span data-stu-id="6e1ed-170">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/choice-set-card.png" alt-text="Пример адаптивной карточки набора вариантов." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="6e1ed-172">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="6e1ed-172">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-choice-set-card.png" alt-text="Пример адаптивной карточки набора вариантов на мобильном устройстве." border="false":::

---

## <a name="anatomy"></a><span data-ttu-id="6e1ed-174">Структура</span><span class="sxs-lookup"><span data-stu-id="6e1ed-174">Anatomy</span></span>

<span data-ttu-id="6e1ed-175">Адаптивные карточки обладают большой гибкостью.</span><span class="sxs-lookup"><span data-stu-id="6e1ed-175">Adaptive Cards have a lot of flexibility.</span></span> <span data-ttu-id="6e1ed-176">Но как минимум мы настоятельно рекомендуем включать следующие компоненты в каждую карточку.</span><span class="sxs-lookup"><span data-stu-id="6e1ed-176">But at minimum, we strongly suggest including the following components in every card.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="6e1ed-177">Компьютер</span><span class="sxs-lookup"><span data-stu-id="6e1ed-177">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/anatomy.png" alt-text="Пример адаптивной карточки структуры." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="6e1ed-179">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="6e1ed-179">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-anatomy.png" alt-text="Пример адаптивной карточки структуры на мобильном устройстве." border="false":::

---

|<span data-ttu-id="6e1ed-181">Счетчик</span><span class="sxs-lookup"><span data-stu-id="6e1ed-181">Counter</span></span>|<span data-ttu-id="6e1ed-182">Описание</span><span class="sxs-lookup"><span data-stu-id="6e1ed-182">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="6e1ed-183">A</span><span class="sxs-lookup"><span data-stu-id="6e1ed-183">A</span></span>|<span data-ttu-id="6e1ed-184">**Заголовок**. Создавайте ясные и четкие заголовки.</span><span class="sxs-lookup"><span data-stu-id="6e1ed-184">**Header**: Make your headers clear and concise.</span></span>|
|<span data-ttu-id="6e1ed-185">Б</span><span class="sxs-lookup"><span data-stu-id="6e1ed-185">B</span></span>|<span data-ttu-id="6e1ed-186">**Копия основного текста**. Сообщайте сведения, слишком длинные или недостаточно важные для включения в заголовок.</span><span class="sxs-lookup"><span data-stu-id="6e1ed-186">**Body copy**: Convey details that are either too long or not important enough to include in the header.</span></span>|
|<span data-ttu-id="6e1ed-187">В</span><span class="sxs-lookup"><span data-stu-id="6e1ed-187">C</span></span>|<span data-ttu-id="6e1ed-188">**Основные действия**. Рекомендуется включить от 1 до 3 основных действий.</span><span class="sxs-lookup"><span data-stu-id="6e1ed-188">**Primary actions**: As a best practice, include 1-3 primary actions.</span></span> <span data-ttu-id="6e1ed-189">Вы можете выбрать до шести действий.</span><span class="sxs-lookup"><span data-stu-id="6e1ed-189">You can have up to six.</span></span>|

## <a name="best-practices"></a><span data-ttu-id="6e1ed-190">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="6e1ed-190">Best practices</span></span>

<span data-ttu-id="6e1ed-191">Используйте эти рекомендации для создания качественных приложений.</span><span class="sxs-lookup"><span data-stu-id="6e1ed-191">Use these recommendations to create a quality app experience.</span></span>

### <a name="primary-and-secondary-actions"></a><span data-ttu-id="6e1ed-192">Основные и вспомогательные действия</span><span class="sxs-lookup"><span data-stu-id="6e1ed-192">Primary and secondary actions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-do.png" alt-text="Рекомендация о включении в адаптивную карточку только небольшого набора действий." border="false":::

#### <a name="do-use-up-to-six-primary-actions"></a><span data-ttu-id="6e1ed-194">Рекомендуется: используйте до шести основных действий</span><span class="sxs-lookup"><span data-stu-id="6e1ed-194">Do: Use up to six primary actions</span></span>

<span data-ttu-id="6e1ed-195">Адаптивные карточки могут поддерживать шесть основных действий, но большинству карточек это не требуется.</span><span class="sxs-lookup"><span data-stu-id="6e1ed-195">While Adaptive Cards can support six primary actions, most cards don’t need that.</span></span> <span data-ttu-id="6e1ed-196">Действия должны быть четкими, краткими и простыми.</span><span class="sxs-lookup"><span data-stu-id="6e1ed-196">Actions should be clear, concise, and straight forward.</span></span> <span data-ttu-id="6e1ed-197">Чем меньше, тем лучше.</span><span class="sxs-lookup"><span data-stu-id="6e1ed-197">Less is more.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-dont.png" alt-text="Рекомендация о том, как не перегружать пользователей слишком большим количеством действий на адаптивной карточке." border="false":::

#### <a name="dont-use-more-than-six-primary-actions"></a><span data-ttu-id="6e1ed-199">Не рекомендуется: используйте более шести основных действий</span><span class="sxs-lookup"><span data-stu-id="6e1ed-199">Don't: Use more than six primary actions</span></span>

<span data-ttu-id="6e1ed-200">Адаптивные карточки должны представлять быстрое интерактивное содержимое.</span><span class="sxs-lookup"><span data-stu-id="6e1ed-200">Adaptive Cards should present quick, actionable content.</span></span> <span data-ttu-id="6e1ed-201">Слишком много действий могут перегружать пользователя.</span><span class="sxs-lookup"><span data-stu-id="6e1ed-201">Too many actions can overwhelm a user.</span></span>

   :::column-end:::
:::row-end:::

### <a name="frequency"></a><span data-ttu-id="6e1ed-202">Частота</span><span class="sxs-lookup"><span data-stu-id="6e1ed-202">Frequency</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/frequency-do.png" alt-text="Рекомендация по частоте использования адаптивной карточки." border="false":::

#### <a name="do-be-concise"></a><span data-ttu-id="6e1ed-204">Рекомендуется: будьте краткими</span><span class="sxs-lookup"><span data-stu-id="6e1ed-204">Do: Be concise</span></span>

<span data-ttu-id="6e1ed-205">В беседу можно легко отправить несколько карточек, но после прокрутки и исчезновения карточек с экрана они становятся менее полезными.</span><span class="sxs-lookup"><span data-stu-id="6e1ed-205">It's easy to send multiple cards into a conversation, but once cards scroll out of view, they become less useful.</span></span> <span data-ttu-id="6e1ed-206">Попробуйте ограничиться основными моментами.</span><span class="sxs-lookup"><span data-stu-id="6e1ed-206">Try to limit yourself to the essentials.</span></span> <span data-ttu-id="6e1ed-207">Это особенно актуально в каналах, где пользователи более склонны воспринимать элементы как ненужный "шум".</span><span class="sxs-lookup"><span data-stu-id="6e1ed-207">This is especially true in a channel where users have less tolerance for what they perceive as "noise".</span></span>
