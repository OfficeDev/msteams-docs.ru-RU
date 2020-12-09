---
title: Разработка адаптивных карточек для приложения
description: Узнайте, как разрабатывать адаптивные карты для Teams и как получить набор пользовательских интерфейсов Microsoft Teams.
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: bd48846284620415cc8cadabc59f2ab7b61d5189
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/09/2020
ms.locfileid: "49604556"
---
# <a name="designing-adaptive-cards-for-your-microsoft-teams-app"></a><span data-ttu-id="7d215-103">Разработка адаптивных карточек для приложения Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="7d215-103">Designing Adaptive Cards for your Microsoft Teams app</span></span>

<span data-ttu-id="7d215-104">Адаптивная карта содержит основной текст элементов карточки и необязательный набор действий.</span><span class="sxs-lookup"><span data-stu-id="7d215-104">An Adaptive Card contains a freeform body of card elements and optional set of actions.</span></span> <span data-ttu-id="7d215-105">Адаптивные карты — это фрагменты контента, которые можно добавить в беседу с помощью расширения Bot или системы обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="7d215-105">Adaptive Cards are actionable snippets of content that you can add to a conversation through a bot or messaging extension.</span></span> <span data-ttu-id="7d215-106">С помощью текста, рисунков и кнопок эти карточки предоставляют широкие возможности для общения с аудиторией.</span><span class="sxs-lookup"><span data-stu-id="7d215-106">Using text, graphics, and buttons, these cards provide rich communication to your audience.</span></span>

<span data-ttu-id="7d215-107">Инфраструктура адаптивной карточки используется во многих продуктах Майкрософт, в том числе в Teams.</span><span class="sxs-lookup"><span data-stu-id="7d215-107">The Adaptive Card framework is used across many Microsoft products, including Teams.</span></span> <span data-ttu-id="7d215-108">Вы можете отправлять карточки внутри сообщений пользователям с помощью боты или расширений системы обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="7d215-108">You can send cards inside messages to users via bots or messaging extensions.</span></span> <span data-ttu-id="7d215-109">Пользователи могут выполнять действия с карточками, если они есть.</span><span class="sxs-lookup"><span data-stu-id="7d215-109">Users can take actions on cards when present.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/adaptive-card-overview.png" alt-text="В примере показана Адаптивная карта." border="false":::

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="7d215-111">Набор элементов пользовательского интерфейса Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="7d215-111">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="7d215-112">Вы можете найти более подробные рекомендации по проектированию адаптивных карточек в Teams, в том числе элементы, которые можно изменять и изменять по мере необходимости, в наборе UI Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="7d215-112">You can find more comprehensive design guidelines for Adaptive Cards in Teams, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="7d215-113">Кроме того, в набор элементов пользовательского интерфейса посвящены важные темы, такие как такие как, Специальные возможности, Специальные возможности и масштабирование.</span><span class="sxs-lookup"><span data-stu-id="7d215-113">The UI kit also covers essential topics such as theming, accessibility, and responsive sizing.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7d215-114">Получение набора элементов пользовательского интерфейса Microsoft Teams (фигма)</span><span class="sxs-lookup"><span data-stu-id="7d215-114">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="adaptive-cards-designer"></a><span data-ttu-id="7d215-115">Конструктор адаптивных карточек</span><span class="sxs-lookup"><span data-stu-id="7d215-115">Adaptive Cards designer</span></span>

<span data-ttu-id="7d215-116">Вы также можете начать разработку адаптивных карт непосредственно в браузере.</span><span class="sxs-lookup"><span data-stu-id="7d215-116">You also can start designing your Adaptive Cards directly in the browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7d215-117">Попробуйте конструктор адаптивных карточек</span><span class="sxs-lookup"><span data-stu-id="7d215-117">Try the Adaptive Cards designer</span></span>](https://adaptivecards.io/designer/)

## <a name="types-of-adaptive-cards"></a><span data-ttu-id="7d215-118">Типы адаптивных карточек</span><span class="sxs-lookup"><span data-stu-id="7d215-118">Types of Adaptive Cards</span></span>

### <a name="hero"></a><span data-ttu-id="7d215-119">Главный имиджевый баннер</span><span class="sxs-lookup"><span data-stu-id="7d215-119">Hero</span></span>

<span data-ttu-id="7d215-120">Самая крупная карточка.</span><span class="sxs-lookup"><span data-stu-id="7d215-120">Our largest card.</span></span> <span data-ttu-id="7d215-121">Используйте для предоставления общего доступа к статьям или сценариям, в которых изображение покажет большую часть статьи.</span><span class="sxs-lookup"><span data-stu-id="7d215-121">Use for sharing articles or scenarios where an image tells most of the story.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/hero-card.png" alt-text="В примере показана Адаптивная карта." border="false":::

### <a name="thumbnail"></a><span data-ttu-id="7d215-123">Thumbnail</span><span class="sxs-lookup"><span data-stu-id="7d215-123">Thumbnail</span></span>

<span data-ttu-id="7d215-124">Используется для отправки простого сообщения с действиями.</span><span class="sxs-lookup"><span data-stu-id="7d215-124">Use for sending a simple actionable message.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/thumbnail-card.png" alt-text="В примере показана Адаптивная карта." border="false":::

### <a name="list"></a><span data-ttu-id="7d215-126">Список</span><span class="sxs-lookup"><span data-stu-id="7d215-126">List</span></span>

<span data-ttu-id="7d215-127">Используйте в сценариях, где пользователь должен выбрать элемент из списка, но для этих элементов не требуется много объяснений.</span><span class="sxs-lookup"><span data-stu-id="7d215-127">Use in scenarios where you want the user to pick an item from a list, but the items don’t need a lot of explanation.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/list-card.png" alt-text="В примере показана Адаптивная карта." border="false":::

### <a name="digest"></a><span data-ttu-id="7d215-129">Digest</span><span class="sxs-lookup"><span data-stu-id="7d215-129">Digest</span></span>

<span data-ttu-id="7d215-130">Используется для дайджестов новостей и сообщений округления.</span><span class="sxs-lookup"><span data-stu-id="7d215-130">Use for news digests and round-up posts.</span></span> <span data-ttu-id="7d215-131">Примечание: рекомендуем использовать карточку эскиза для одного обновления или элемента новостей.</span><span class="sxs-lookup"><span data-stu-id="7d215-131">Note: We recommend the thumbnail card for a single update or news item.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/digest-card.png" alt-text="В примере показана Адаптивная карта." border="false":::

### <a name="media"></a><span data-ttu-id="7d215-133">СМИ</span><span class="sxs-lookup"><span data-stu-id="7d215-133">Media</span></span>

<span data-ttu-id="7d215-134">Используется, когда требуется объединить текст и мультимедиа, например, аудио или видео.</span><span class="sxs-lookup"><span data-stu-id="7d215-134">Use when you want to combine text and media, like audio or video.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/media-card.png" alt-text="В примере показана Адаптивная карта." border="false":::

### <a name="people"></a><span data-ttu-id="7d215-136">Люди</span><span class="sxs-lookup"><span data-stu-id="7d215-136">People</span></span>

<span data-ttu-id="7d215-137">Лучше всего подходит для эффективной передачи сведений о том, кто участвует в задаче.</span><span class="sxs-lookup"><span data-stu-id="7d215-137">Best used when you to efficiently convey who's involved with a task.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/people-card.png" alt-text="В примере показана Адаптивная карта." border="false":::

### <a name="request-ticket"></a><span data-ttu-id="7d215-139">Билет запроса</span><span class="sxs-lookup"><span data-stu-id="7d215-139">Request ticket</span></span>

<span data-ttu-id="7d215-140">Используется для получения быстрых входных данных пользователя для автоматического создания задачи или билета.</span><span class="sxs-lookup"><span data-stu-id="7d215-140">Use to get quick inputs from a user to automatically create a task or ticket.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/request-ticket-card.png" alt-text="В примере показана Адаптивная карта." border="false":::

### <a name="imageset"></a><span data-ttu-id="7d215-142">Image</span><span class="sxs-lookup"><span data-stu-id="7d215-142">ImageSet</span></span>

<span data-ttu-id="7d215-143">Используется для отправки нескольких эскизов изображений.</span><span class="sxs-lookup"><span data-stu-id="7d215-143">Use to send multiple image thumbnails.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/image-set-card.png" alt-text="В примере показана Адаптивная карта." border="false":::

### <a name="actionset"></a><span data-ttu-id="7d215-145">ActionSet</span><span class="sxs-lookup"><span data-stu-id="7d215-145">ActionSet</span></span>

<span data-ttu-id="7d215-146">Используйте, когда вы хотите, чтобы пользователь выберет кнопку, а затем собирает данные, вводимые пользователем, из одной карточки.</span><span class="sxs-lookup"><span data-stu-id="7d215-146">Use when you want to the user to select a button, then gather addition user input from the same card.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/action-set-card.png" alt-text="В примере показана Адаптивная карта." border="false":::

### <a name="choiceset"></a><span data-ttu-id="7d215-148">Выбор</span><span class="sxs-lookup"><span data-stu-id="7d215-148">ChoiceSet</span></span>

<span data-ttu-id="7d215-149">Используется для сбора нескольких входных данных от пользователя.</span><span class="sxs-lookup"><span data-stu-id="7d215-149">Use to gather multiple inputs from the user.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/choice-set-card.png" alt-text="В примере показана Адаптивная карта." border="false":::

## <a name="anatomy"></a><span data-ttu-id="7d215-151">Составляющие</span><span class="sxs-lookup"><span data-stu-id="7d215-151">Anatomy</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/anatomy.png" alt-text="Иллюстрация, демонстрирующая пользовательский интерфейс для адаптивной карточки." border="false":::

<span data-ttu-id="7d215-153">Адаптивные карты имеют множество гибкости.</span><span class="sxs-lookup"><span data-stu-id="7d215-153">Adaptive Cards have a lot of flexibility.</span></span> <span data-ttu-id="7d215-154">Но как минимум, настоятельно рекомендуется включить следующие компоненты в каждую карточку:</span><span class="sxs-lookup"><span data-stu-id="7d215-154">But at a minimum, we strongly suggest including the following components in every card:</span></span>

|<span data-ttu-id="7d215-155">Счетчик</span><span class="sxs-lookup"><span data-stu-id="7d215-155">Counter</span></span>|<span data-ttu-id="7d215-156">Описание</span><span class="sxs-lookup"><span data-stu-id="7d215-156">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="7d215-157">A</span><span class="sxs-lookup"><span data-stu-id="7d215-157">A</span></span>|<span data-ttu-id="7d215-158">**Верхний колонтитул**: Сделайте заголовки четкими и краткими, но с описанием.</span><span class="sxs-lookup"><span data-stu-id="7d215-158">**Header**: Make headers clear and concise, yet descriptive.</span></span>|
|<span data-ttu-id="7d215-159">B</span><span class="sxs-lookup"><span data-stu-id="7d215-159">B</span></span>|<span data-ttu-id="7d215-160">**Копия текста**: используется для передачи сведений, которые слишком длинны или не имеют достаточного значения для включения в заголовок.</span><span class="sxs-lookup"><span data-stu-id="7d215-160">**Body copy**: Use to convey detail that is either too long or not important enough to include in the header.</span></span>|
|<span data-ttu-id="7d215-161">C</span><span class="sxs-lookup"><span data-stu-id="7d215-161">C</span></span>|<span data-ttu-id="7d215-162">**Основные действия**: рекомендуется включить основные действия 1-3.</span><span class="sxs-lookup"><span data-stu-id="7d215-162">**Primary actions**: As a best practice, include 1-3 primary actions.</span></span> <span data-ttu-id="7d215-163">Разрешено не более шести.</span><span class="sxs-lookup"><span data-stu-id="7d215-163">A maximum of six are allowed.</span></span>|

## <a name="best-practices"></a><span data-ttu-id="7d215-164">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="7d215-164">Best practices</span></span>

### <a name="primary-and-secondary-actions"></a><span data-ttu-id="7d215-165">Основные и дополнительные действия</span><span class="sxs-lookup"><span data-stu-id="7d215-165">Primary and secondary actions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-do.png" alt-text="Пример, в котором показано, как добиться адаптивных карт." border="false":::

#### <a name="do-use-up-to-six-primary-actions"></a><span data-ttu-id="7d215-167">Do: использование до шести основных действий</span><span class="sxs-lookup"><span data-stu-id="7d215-167">Do: Use up to six primary actions</span></span>

<span data-ttu-id="7d215-168">Хотя адаптивные карты могут поддерживать шесть основных действий, большинство карт это не требуется.</span><span class="sxs-lookup"><span data-stu-id="7d215-168">While Adaptive Cards can support six primary actions, most cards don’t need that.</span></span> <span data-ttu-id="7d215-169">Действия должны быть ясными, краткими и прямыми вперед.</span><span class="sxs-lookup"><span data-stu-id="7d215-169">Actions should be clear, concise, and straight forward.</span></span> <span data-ttu-id="7d215-170">Меньше.</span><span class="sxs-lookup"><span data-stu-id="7d215-170">Less is more.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-dont.png" alt-text="Пример, в котором показано, как добиться адаптивных карт." border="false":::

#### <a name="dont-use-more-than-six-primary-actions"></a><span data-ttu-id="7d215-172">Не используйте более шести основных действий.</span><span class="sxs-lookup"><span data-stu-id="7d215-172">Don't: Use more than six primary actions</span></span>

<span data-ttu-id="7d215-173">Адаптивные карты должны представлять собой быстро выполняемое интерактивное содержимое.</span><span class="sxs-lookup"><span data-stu-id="7d215-173">Adaptive Cards should present quick, actionable content.</span></span> <span data-ttu-id="7d215-174">Слишком много действий может перегрузить пользователя.</span><span class="sxs-lookup"><span data-stu-id="7d215-174">Too many actions can overwhelm a user.</span></span>

   :::column-end:::
:::row-end:::

### <a name="frequency"></a><span data-ttu-id="7d215-175">Частота</span><span class="sxs-lookup"><span data-stu-id="7d215-175">Frequency</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/frequency-do.png" alt-text="Пример, в котором показано, как добиться адаптивных карт." border="false":::

#### <a name="do-be-concise"></a><span data-ttu-id="7d215-177">Do: будет кратким</span><span class="sxs-lookup"><span data-stu-id="7d215-177">Do: Be concise</span></span>

<span data-ttu-id="7d215-178">Вы можете легко отправить несколько карточек в беседу, но после того, как карточки пропрокручиваются из представления, они становятся менее удобными.</span><span class="sxs-lookup"><span data-stu-id="7d215-178">It's easy to send multiple cards into a conversation, but once cards scroll out of view, they become less useful.</span></span> <span data-ttu-id="7d215-179">Попробуйте ограничиться основными сведениями.</span><span class="sxs-lookup"><span data-stu-id="7d215-179">Try to limit yourself to the essentials.</span></span> <span data-ttu-id="7d215-180">Это особенно справедливо в канале, где пользователи имеют меньшую отклонения для того, что они считают "шумом".</span><span class="sxs-lookup"><span data-stu-id="7d215-180">This is especially true in a channel where users have less tolerance for what they perceive as "noise".</span></span>
