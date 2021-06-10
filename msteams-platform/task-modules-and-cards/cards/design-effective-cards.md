---
title: Разработка адаптивных карт для приложения
description: Узнайте, как создать адаптивные карты для Teams и получить Microsoft Teams пользовательского интерфейса.
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: b4d5f43268c7bd5afecb56d26eb0d49ed6c9002b
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630313"
---
# <a name="designing-adaptive-cards-for-your-microsoft-teams-app"></a><span data-ttu-id="4a2d9-103">Разработка адаптивных карт для Microsoft Teams приложения</span><span class="sxs-lookup"><span data-stu-id="4a2d9-103">Designing Adaptive Cards for your Microsoft Teams app</span></span>

<span data-ttu-id="4a2d9-104">Адаптивная карта содержит свободный набор элементов карт и необязательный набор действий.</span><span class="sxs-lookup"><span data-stu-id="4a2d9-104">An Adaptive Card contains a freeform body of card elements and optional set of actions.</span></span> <span data-ttu-id="4a2d9-105">Адаптивные карты — это фрагменты контента, которые можно добавить в беседу с помощью бота или расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="4a2d9-105">Adaptive Cards are actionable snippets of content that you can add to a conversation through a bot or messaging extension.</span></span> <span data-ttu-id="4a2d9-106">С помощью текстовых, графических и кнопок эти карточки обеспечивают насыщенную связь для вашей аудитории.</span><span class="sxs-lookup"><span data-stu-id="4a2d9-106">Using text, graphics, and buttons, these cards provide rich communication to your audience.</span></span>

<span data-ttu-id="4a2d9-107">База адаптивной карты используется во многих продуктах Майкрософт, включая Teams.</span><span class="sxs-lookup"><span data-stu-id="4a2d9-107">The Adaptive Card framework is used across many Microsoft products, including Teams.</span></span> <span data-ttu-id="4a2d9-108">Вы можете отправлять карточки внутри сообщений пользователям с помощью ботов или расширений обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="4a2d9-108">You can send cards inside messages to users via bots or messaging extensions.</span></span> <span data-ttu-id="4a2d9-109">Пользователи также могут принимать меры на картах при их настоящем действии.</span><span class="sxs-lookup"><span data-stu-id="4a2d9-109">Users can also take actions on cards when present.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/adaptive-card-overview.png" alt-text="Пример адаптивной карты." border="false":::

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="4a2d9-111">Комплект разработчика для пользовательского интерфейса Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="4a2d9-111">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="4a2d9-112">Дополнительные рекомендации по разработке адаптивных карт можно найти в Teams, включая элементы, которые можно захватить и изменить по мере необходимости, в Microsoft Teams пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="4a2d9-112">You can find more comprehensive design guidelines for Adaptive Cards in Teams, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="4a2d9-113">Набор пользовательского интерфейса также охватывает такие важные темы, как темы, доступность и размер отзывчивости.</span><span class="sxs-lookup"><span data-stu-id="4a2d9-113">The UI kit also covers essential topics such as theming, accessibility, and responsive sizing.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4a2d9-114">Получить комплект разработчика для пользовательского интерфейса Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="4a2d9-114">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="adaptive-cards-designer"></a><span data-ttu-id="4a2d9-115">Конструктор адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="4a2d9-115">Adaptive Cards designer</span></span>

<span data-ttu-id="4a2d9-116">Вы также можете приступить к разработке адаптивных карт непосредственно в браузере.</span><span class="sxs-lookup"><span data-stu-id="4a2d9-116">You also can start designing your Adaptive Cards directly in the browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4a2d9-117">Попробуйте конструктор адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="4a2d9-117">Try the Adaptive Cards designer</span></span>](https://adaptivecards.io/designer/)

## <a name="types-of-adaptive-cards"></a><span data-ttu-id="4a2d9-118">Типы адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="4a2d9-118">Types of Adaptive Cards</span></span>

### <a name="hero"></a><span data-ttu-id="4a2d9-119">Главный имиджевый баннер</span><span class="sxs-lookup"><span data-stu-id="4a2d9-119">Hero</span></span>

<span data-ttu-id="4a2d9-120">Наша самая большая карта.</span><span class="sxs-lookup"><span data-stu-id="4a2d9-120">Our largest card.</span></span> <span data-ttu-id="4a2d9-121">Используйте для общего доступа к статьям или сценариям, в которых изображение рассказывает большую часть истории.</span><span class="sxs-lookup"><span data-stu-id="4a2d9-121">Use for sharing articles or scenarios where an image tells most of the story.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="4a2d9-122">Desktop</span><span class="sxs-lookup"><span data-stu-id="4a2d9-122">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/hero-card.png" alt-text="В примере показана карта героя адаптивной карты." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="4a2d9-124">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="4a2d9-124">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-hero-card.png" alt-text="В примере показана карта героя адаптивной карты на мобильных устройствах." border="false":::

---

### <a name="thumbnail"></a><span data-ttu-id="4a2d9-126">Эскиз</span><span class="sxs-lookup"><span data-stu-id="4a2d9-126">Thumbnail</span></span>

<span data-ttu-id="4a2d9-127">Используйте для отправки простого действия сообщения.</span><span class="sxs-lookup"><span data-stu-id="4a2d9-127">Use for sending a simple actionable message.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="4a2d9-128">Desktop</span><span class="sxs-lookup"><span data-stu-id="4a2d9-128">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/thumbnail-card.png" alt-text="В примере показана карта адаптивной карты." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="4a2d9-130">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="4a2d9-130">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-thumbnail-card.png" alt-text="В примере показана карта адаптивных карт на мобильных устройствах." border="false":::

---

### <a name="list"></a><span data-ttu-id="4a2d9-132">List</span><span class="sxs-lookup"><span data-stu-id="4a2d9-132">List</span></span>

<span data-ttu-id="4a2d9-133">Используйте в сценариях, в которых пользователь должен выбрать элемент из списка, но для этих элементов не требуется много объяснений.</span><span class="sxs-lookup"><span data-stu-id="4a2d9-133">Use in scenarios where you want the user to pick an item from a list, but the items don’t need a lot of explanation.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="4a2d9-134">Desktop</span><span class="sxs-lookup"><span data-stu-id="4a2d9-134">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/list-card.png" alt-text="В примере показана карта списка адаптивной карты." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="4a2d9-136">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="4a2d9-136">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-list-card.png" alt-text="В примере показана карта списка адаптивных карт на мобильном телефоне." border="false":::

---

### Digest

Use for news digests and round-up posts. Note: We recommend the thumbnail card for a single update or news item.

# [Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/digest-card.png" alt-text="Example shows an Adaptive Card digest card." border="false":::

# [Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-digest-card.png" alt-text="Example shows an Adaptive Card digest card on mobile." border="false":::

---

### <a name="media"></a><span data-ttu-id="4a2d9-138">Мультимедиа</span><span class="sxs-lookup"><span data-stu-id="4a2d9-138">Media</span></span>

<span data-ttu-id="4a2d9-139">Используйте, когда нужно сочетать текст и носители, например аудио или видео.</span><span class="sxs-lookup"><span data-stu-id="4a2d9-139">Use when you want to combine text and media, like audio or video.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="4a2d9-140">Desktop</span><span class="sxs-lookup"><span data-stu-id="4a2d9-140">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/media-card.png" alt-text="В примере показана медиакарда Adaptive Card." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="4a2d9-142">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="4a2d9-142">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-media-card.png" alt-text="В примере показана медиакарда Adaptive Card на мобильном телефоне." border="false":::

---

### <a name="people"></a><span data-ttu-id="4a2d9-144">Люди</span><span class="sxs-lookup"><span data-stu-id="4a2d9-144">People</span></span>

<span data-ttu-id="4a2d9-145">Лучше всего использовать для эффективного передачи данных о том, кто участвует в работе с задачей.</span><span class="sxs-lookup"><span data-stu-id="4a2d9-145">Best used when you to efficiently convey who's involved with a task.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="4a2d9-146">Desktop</span><span class="sxs-lookup"><span data-stu-id="4a2d9-146">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/people-card.png" alt-text="В примере показана карточка людей адаптивной карты." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="4a2d9-148">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="4a2d9-148">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-people-card.png" alt-text="В примере показана карточка людей адаптивной карты на мобильных устройствах." border="false":::

---

### <a name="request-ticket"></a><span data-ttu-id="4a2d9-150">Запрос билета</span><span class="sxs-lookup"><span data-stu-id="4a2d9-150">Request ticket</span></span>

<span data-ttu-id="4a2d9-151">Используйте для получения быстрых входных данных от пользователя, чтобы автоматически создать задачу или билет.</span><span class="sxs-lookup"><span data-stu-id="4a2d9-151">Use to get quick inputs from a user to automatically create a task or ticket.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="4a2d9-152">Desktop</span><span class="sxs-lookup"><span data-stu-id="4a2d9-152">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/request-ticket-card.png" alt-text="В примере показана карточка запроса на адаптивную карту." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="4a2d9-154">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="4a2d9-154">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-request-ticket-card.png" alt-text="В примере показана карточка для запроса билетов адаптивной карты на мобильный телефон." border="false":::

---

### <a name="image-set"></a><span data-ttu-id="4a2d9-156">Набор изображений</span><span class="sxs-lookup"><span data-stu-id="4a2d9-156">Image set</span></span>

<span data-ttu-id="4a2d9-157">Используйте для отправки нескольких эскизов изображений.</span><span class="sxs-lookup"><span data-stu-id="4a2d9-157">Use to send multiple image thumbnails.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="4a2d9-158">Desktop</span><span class="sxs-lookup"><span data-stu-id="4a2d9-158">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/image-set-card.png" alt-text="В примере показана карта набора изображений адаптивной карты." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="4a2d9-160">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="4a2d9-160">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-image-set-card.png" alt-text="В примере показана карта набора изображений адаптивной карты на мобильных устройствах." border="false":::

---

### <a name="action-set"></a><span data-ttu-id="4a2d9-162">Набор действий</span><span class="sxs-lookup"><span data-stu-id="4a2d9-162">Action set</span></span>

<span data-ttu-id="4a2d9-163">Используйте для выбора кнопки пользователю, а затем соберем дополнительный ввод пользователя с той же карты.</span><span class="sxs-lookup"><span data-stu-id="4a2d9-163">Use when you want to the user to select a button, then gather addition user input from the same card.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="4a2d9-164">Desktop</span><span class="sxs-lookup"><span data-stu-id="4a2d9-164">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/action-set-card.png" alt-text="В примере показана карта набора действий адаптивной карты." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="4a2d9-166">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="4a2d9-166">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-action-set-card.png" alt-text="В примере показана карта набора действий адаптивной карты на мобильном телефоне." border="false":::

---

### <a name="choice-set"></a><span data-ttu-id="4a2d9-168">Набор выбора</span><span class="sxs-lookup"><span data-stu-id="4a2d9-168">Choice set</span></span>

<span data-ttu-id="4a2d9-169">Используйте для сбора нескольких входных данных от пользователя.</span><span class="sxs-lookup"><span data-stu-id="4a2d9-169">Use to gather multiple inputs from the user.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="4a2d9-170">Desktop</span><span class="sxs-lookup"><span data-stu-id="4a2d9-170">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/choice-set-card.png" alt-text="В примере показана карта выбора адаптивной карты." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="4a2d9-172">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="4a2d9-172">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-choice-set-card.png" alt-text="В примере показана карта выбора адаптивной карты на мобильном телефоне." border="false":::

---

## <a name="anatomy"></a><span data-ttu-id="4a2d9-174">Анатомия</span><span class="sxs-lookup"><span data-stu-id="4a2d9-174">Anatomy</span></span>

<span data-ttu-id="4a2d9-175">Адаптивные карты имеют большую гибкость.</span><span class="sxs-lookup"><span data-stu-id="4a2d9-175">Adaptive Cards have a lot of flexibility.</span></span> <span data-ttu-id="4a2d9-176">Но как минимум мы настоятельно рекомендуем включить следующие компоненты в каждую карту.</span><span class="sxs-lookup"><span data-stu-id="4a2d9-176">But at minimum, we strongly suggest including the following components in every card.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="4a2d9-177">Desktop</span><span class="sxs-lookup"><span data-stu-id="4a2d9-177">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/anatomy.png" alt-text="В EExample показана анатомия адаптивной карты." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="4a2d9-179">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="4a2d9-179">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-anatomy.png" alt-text="В примере показана анатомия адаптивной карты на мобильных устройствах." border="false":::

---

|<span data-ttu-id="4a2d9-181">Счетчик</span><span class="sxs-lookup"><span data-stu-id="4a2d9-181">Counter</span></span>|<span data-ttu-id="4a2d9-182">Описание</span><span class="sxs-lookup"><span data-stu-id="4a2d9-182">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="4a2d9-183">A</span><span class="sxs-lookup"><span data-stu-id="4a2d9-183">A</span></span>|<span data-ttu-id="4a2d9-184">**Заглавка.** Сделайте заготки четкими и краткими.</span><span class="sxs-lookup"><span data-stu-id="4a2d9-184">**Header**: Make your headers clear and concise.</span></span>|
|<span data-ttu-id="4a2d9-185">B</span><span class="sxs-lookup"><span data-stu-id="4a2d9-185">B</span></span>|<span data-ttu-id="4a2d9-186">**Копия тела.** Передай сведения, которые слишком длинные или недостаточно важные, чтобы включить в заголовник.</span><span class="sxs-lookup"><span data-stu-id="4a2d9-186">**Body copy**: Convey details that are either too long or not important enough to include in the header.</span></span>|
|<span data-ttu-id="4a2d9-187">C</span><span class="sxs-lookup"><span data-stu-id="4a2d9-187">C</span></span>|<span data-ttu-id="4a2d9-188">**Основные** действия. В качестве наилучшей практики включаем 1-3 основных действия.</span><span class="sxs-lookup"><span data-stu-id="4a2d9-188">**Primary actions**: As a best practice, include 1-3 primary actions.</span></span> <span data-ttu-id="4a2d9-189">Вы можете иметь до шести.</span><span class="sxs-lookup"><span data-stu-id="4a2d9-189">You can have up to six.</span></span>|

## <a name="best-practices"></a><span data-ttu-id="4a2d9-190">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="4a2d9-190">Best practices</span></span>

<span data-ttu-id="4a2d9-191">Используйте эти рекомендации для создания качественного приложения.</span><span class="sxs-lookup"><span data-stu-id="4a2d9-191">Use these recommendations to create a quality app experience.</span></span>

### <a name="primary-and-secondary-actions"></a><span data-ttu-id="4a2d9-192">Первичные и вторичные действия</span><span class="sxs-lookup"><span data-stu-id="4a2d9-192">Primary and secondary actions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-do.png" alt-text="Передовая практика по включению в адаптивную карту только небольшого набора действий." border="false":::

#### <a name="do-use-up-to-six-primary-actions"></a><span data-ttu-id="4a2d9-194">Do: Используйте до шести основных действий</span><span class="sxs-lookup"><span data-stu-id="4a2d9-194">Do: Use up to six primary actions</span></span>

<span data-ttu-id="4a2d9-195">Хотя адаптивные карты могут поддерживать шесть основных действий, большинству карт это не нужно.</span><span class="sxs-lookup"><span data-stu-id="4a2d9-195">While Adaptive Cards can support six primary actions, most cards don’t need that.</span></span> <span data-ttu-id="4a2d9-196">Действия должны быть четкими, краткими и прямыми.</span><span class="sxs-lookup"><span data-stu-id="4a2d9-196">Actions should be clear, concise, and straight forward.</span></span> <span data-ttu-id="4a2d9-197">Меньше больше.</span><span class="sxs-lookup"><span data-stu-id="4a2d9-197">Less is more.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-dont.png" alt-text="Лучшая практика о том, как не перегружать пользователей слишком большим количеством действий на адаптивной карте." border="false":::

#### <a name="dont-use-more-than-six-primary-actions"></a><span data-ttu-id="4a2d9-199">Не используйте более шести основных действий</span><span class="sxs-lookup"><span data-stu-id="4a2d9-199">Don't: Use more than six primary actions</span></span>

<span data-ttu-id="4a2d9-200">Адаптивные карты должны представлять быстрое и оперативное содержимое.</span><span class="sxs-lookup"><span data-stu-id="4a2d9-200">Adaptive Cards should present quick, actionable content.</span></span> <span data-ttu-id="4a2d9-201">Слишком много действий может переполохить пользователя.</span><span class="sxs-lookup"><span data-stu-id="4a2d9-201">Too many actions can overwhelm a user.</span></span>

   :::column-end:::
:::row-end:::

### <a name="frequency"></a><span data-ttu-id="4a2d9-202">Частота</span><span class="sxs-lookup"><span data-stu-id="4a2d9-202">Frequency</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/frequency-do.png" alt-text="Лучшая практика по частоте адаптивной карты." border="false":::

#### <a name="do-be-concise"></a><span data-ttu-id="4a2d9-204">Do: Быть кратким</span><span class="sxs-lookup"><span data-stu-id="4a2d9-204">Do: Be concise</span></span>

<span data-ttu-id="4a2d9-205">Можно легко отправить несколько карт в беседу, но после того, как карты прокрутки из виду, они становятся менее полезными.</span><span class="sxs-lookup"><span data-stu-id="4a2d9-205">It's easy to send multiple cards into a conversation, but once cards scroll out of view, they become less useful.</span></span> <span data-ttu-id="4a2d9-206">Попробуйте ограничиться основными.</span><span class="sxs-lookup"><span data-stu-id="4a2d9-206">Try to limit yourself to the essentials.</span></span> <span data-ttu-id="4a2d9-207">Это особенно актуально в канале, где пользователи менее терпимо воспринимают то, что они воспринимают как "шум".</span><span class="sxs-lookup"><span data-stu-id="4a2d9-207">This is especially true in a channel where users have less tolerance for what they perceive as "noise".</span></span>
