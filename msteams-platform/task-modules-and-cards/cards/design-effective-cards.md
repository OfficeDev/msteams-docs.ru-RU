---
title: Разработка адаптивных карт для приложения
description: Узнайте, как создать адаптивные карты для teams и получить набор пользовательского интерфейса Microsoft Teams.
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 67a2882a0a687d5ccb48759419ecefcdf9396fc3
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020284"
---
# <a name="designing-adaptive-cards-for-your-microsoft-teams-app"></a><span data-ttu-id="b5cd6-103">Разработка адаптивных карт для приложения Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="b5cd6-103">Designing Adaptive Cards for your Microsoft Teams app</span></span>

<span data-ttu-id="b5cd6-104">Адаптивная карта содержит свободный набор элементов карт и необязательный набор действий.</span><span class="sxs-lookup"><span data-stu-id="b5cd6-104">An Adaptive Card contains a freeform body of card elements and optional set of actions.</span></span> <span data-ttu-id="b5cd6-105">Адаптивные карты — это фрагменты контента, которые можно добавить в беседу с помощью бота или расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="b5cd6-105">Adaptive Cards are actionable snippets of content that you can add to a conversation through a bot or messaging extension.</span></span> <span data-ttu-id="b5cd6-106">С помощью текстовых, графических и кнопок эти карточки обеспечивают насыщенную связь для вашей аудитории.</span><span class="sxs-lookup"><span data-stu-id="b5cd6-106">Using text, graphics, and buttons, these cards provide rich communication to your audience.</span></span>

<span data-ttu-id="b5cd6-107">База адаптивной карты используется во многих продуктах Майкрософт, включая Teams.</span><span class="sxs-lookup"><span data-stu-id="b5cd6-107">The Adaptive Card framework is used across many Microsoft products, including Teams.</span></span> <span data-ttu-id="b5cd6-108">Вы можете отправлять карточки внутри сообщений пользователям с помощью ботов или расширений обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="b5cd6-108">You can send cards inside messages to users via bots or messaging extensions.</span></span> <span data-ttu-id="b5cd6-109">Пользователи могут принимать меры на картах при их настоящем действии.</span><span class="sxs-lookup"><span data-stu-id="b5cd6-109">Users can take actions on cards when present.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/adaptive-card-overview.png" alt-text="В примере показана адаптивная карта." border="false":::

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="b5cd6-111">Комплект разработчика для пользовательского интерфейса Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="b5cd6-111">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="b5cd6-112">Дополнительные рекомендации по разработке адаптивных карт в Teams, включая элементы, которые можно захватить и изменить по мере необходимости, можно найти в наборе пользовательского интерфейса Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="b5cd6-112">You can find more comprehensive design guidelines for Adaptive Cards in Teams, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="b5cd6-113">Набор пользовательского интерфейса также охватывает такие важные темы, как темы, доступность и размер отзывчивости.</span><span class="sxs-lookup"><span data-stu-id="b5cd6-113">The UI kit also covers essential topics such as theming, accessibility, and responsive sizing.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b5cd6-114">Получить комплект разработчика для пользовательского интерфейса Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="b5cd6-114">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="adaptive-cards-designer"></a><span data-ttu-id="b5cd6-115">Конструктор адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="b5cd6-115">Adaptive Cards designer</span></span>

<span data-ttu-id="b5cd6-116">Вы также можете приступить к разработке адаптивных карт непосредственно в браузере.</span><span class="sxs-lookup"><span data-stu-id="b5cd6-116">You also can start designing your Adaptive Cards directly in the browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b5cd6-117">Попробуйте конструктор адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="b5cd6-117">Try the Adaptive Cards designer</span></span>](https://adaptivecards.io/designer/)

## <a name="types-of-adaptive-cards"></a><span data-ttu-id="b5cd6-118">Типы адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="b5cd6-118">Types of Adaptive Cards</span></span>

### <a name="hero"></a><span data-ttu-id="b5cd6-119">Главный имиджевый баннер</span><span class="sxs-lookup"><span data-stu-id="b5cd6-119">Hero</span></span>

<span data-ttu-id="b5cd6-120">Наша самая большая карта.</span><span class="sxs-lookup"><span data-stu-id="b5cd6-120">Our largest card.</span></span> <span data-ttu-id="b5cd6-121">Используйте для общего доступа к статьям или сценариям, в которых изображение рассказывает большую часть истории.</span><span class="sxs-lookup"><span data-stu-id="b5cd6-121">Use for sharing articles or scenarios where an image tells most of the story.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/hero-card.png" alt-text="В примере показана адаптивная карта." border="false":::

### <a name="thumbnail"></a><span data-ttu-id="b5cd6-123">Эскиз</span><span class="sxs-lookup"><span data-stu-id="b5cd6-123">Thumbnail</span></span>

<span data-ttu-id="b5cd6-124">Используйте для отправки простого действия сообщения.</span><span class="sxs-lookup"><span data-stu-id="b5cd6-124">Use for sending a simple actionable message.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/thumbnail-card.png" alt-text="Пример адаптивной карты." border="false":::

### <a name="list"></a><span data-ttu-id="b5cd6-126">List</span><span class="sxs-lookup"><span data-stu-id="b5cd6-126">List</span></span>

<span data-ttu-id="b5cd6-127">Используйте в сценариях, в которых пользователь должен выбрать элемент из списка, но для этих элементов не требуется много объяснений.</span><span class="sxs-lookup"><span data-stu-id="b5cd6-127">Use in scenarios where you want the user to pick an item from a list, but the items don’t need a lot of explanation.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/list-card.png" alt-text="Пример адаптивной карты." border="false":::

### <a name="digest"></a><span data-ttu-id="b5cd6-129">Digest</span><span class="sxs-lookup"><span data-stu-id="b5cd6-129">Digest</span></span>

<span data-ttu-id="b5cd6-130">Используйте для дайджестов новостей и публикаций обнаглеть.</span><span class="sxs-lookup"><span data-stu-id="b5cd6-130">Use for news digests and round-up posts.</span></span> <span data-ttu-id="b5cd6-131">Примечание. Рекомендуется использовать карту эскиза для одного обновления или элемента новостей.</span><span class="sxs-lookup"><span data-stu-id="b5cd6-131">Note: We recommend the thumbnail card for a single update or news item.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/digest-card.png" alt-text="На рисунке показана адаптивная карта." border="false":::

### <a name="media"></a><span data-ttu-id="b5cd6-133">Мультимедиа</span><span class="sxs-lookup"><span data-stu-id="b5cd6-133">Media</span></span>

<span data-ttu-id="b5cd6-134">Используйте, когда нужно сочетать текст и носители, например аудио или видео.</span><span class="sxs-lookup"><span data-stu-id="b5cd6-134">Use when you want to combine text and media, like audio or video.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/media-card.png" alt-text="На рисунке показана адаптивная карта." border="false":::

### <a name="people"></a><span data-ttu-id="b5cd6-136">Люди</span><span class="sxs-lookup"><span data-stu-id="b5cd6-136">People</span></span>

<span data-ttu-id="b5cd6-137">Лучше всего использовать для эффективного передачи данных о том, кто участвует в работе с задачей.</span><span class="sxs-lookup"><span data-stu-id="b5cd6-137">Best used when you to efficiently convey who's involved with a task.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/people-card.png" alt-text="Иллюстрация адаптивной карты." border="false":::

### <a name="request-ticket"></a><span data-ttu-id="b5cd6-139">Запрос билета</span><span class="sxs-lookup"><span data-stu-id="b5cd6-139">Request ticket</span></span>

<span data-ttu-id="b5cd6-140">Используйте для получения быстрых входных данных от пользователя, чтобы автоматически создать задачу или билет.</span><span class="sxs-lookup"><span data-stu-id="b5cd6-140">Use to get quick inputs from a user to automatically create a task or ticket.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/request-ticket-card.png" alt-text="Иллюстрация адаптивной карты." border="false":::

### <a name="imageset"></a><span data-ttu-id="b5cd6-142">ImageSet</span><span class="sxs-lookup"><span data-stu-id="b5cd6-142">ImageSet</span></span>

<span data-ttu-id="b5cd6-143">Используйте для отправки нескольких эскизов изображений.</span><span class="sxs-lookup"><span data-stu-id="b5cd6-143">Use to send multiple image thumbnails.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/image-set-card.png" alt-text="Пример адаптивной карты." border="false":::

### <a name="actionset"></a><span data-ttu-id="b5cd6-145">ActionSet</span><span class="sxs-lookup"><span data-stu-id="b5cd6-145">ActionSet</span></span>

<span data-ttu-id="b5cd6-146">Используйте для выбора кнопки пользователю, а затем соберем дополнительный ввод пользователя с той же карты.</span><span class="sxs-lookup"><span data-stu-id="b5cd6-146">Use when you want to the user to select a button, then gather addition user input from the same card.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/action-set-card.png" alt-text="В примере показана адаптивная карта." border="false":::

### <a name="choiceset"></a><span data-ttu-id="b5cd6-148">ChoiceSet</span><span class="sxs-lookup"><span data-stu-id="b5cd6-148">ChoiceSet</span></span>

<span data-ttu-id="b5cd6-149">Используйте для сбора нескольких входных данных от пользователя.</span><span class="sxs-lookup"><span data-stu-id="b5cd6-149">Use to gather multiple inputs from the user.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/choice-set-card.png" alt-text="В примере отображается адаптивная карта." border="false":::

## <a name="anatomy"></a><span data-ttu-id="b5cd6-151">Анатомия</span><span class="sxs-lookup"><span data-stu-id="b5cd6-151">Anatomy</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/anatomy.png" alt-text="Иллюстрация, показывающая анатомию пользовательского интерфейса адаптивной карты." border="false":::

<span data-ttu-id="b5cd6-153">Адаптивные карты имеют большую гибкость.</span><span class="sxs-lookup"><span data-stu-id="b5cd6-153">Adaptive Cards have a lot of flexibility.</span></span> <span data-ttu-id="b5cd6-154">Но как минимум мы настоятельно рекомендуем включить в каждую карту следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="b5cd6-154">But at minimum, we strongly suggest including the following components in every card:</span></span>

|<span data-ttu-id="b5cd6-155">Счетчик</span><span class="sxs-lookup"><span data-stu-id="b5cd6-155">Counter</span></span>|<span data-ttu-id="b5cd6-156">Описание</span><span class="sxs-lookup"><span data-stu-id="b5cd6-156">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="b5cd6-157">A</span><span class="sxs-lookup"><span data-stu-id="b5cd6-157">A</span></span>|<span data-ttu-id="b5cd6-158">**Заглавная:** Сделать заглавные заготки четкими и краткими, но описательными.</span><span class="sxs-lookup"><span data-stu-id="b5cd6-158">**Header**: Make headers clear and concise, yet descriptive.</span></span>|
|<span data-ttu-id="b5cd6-159">B</span><span class="sxs-lookup"><span data-stu-id="b5cd6-159">B</span></span>|<span data-ttu-id="b5cd6-160">**Копия тела.** Используйте для передачи слишком длинных или недостаточно важных деталей для включаемой в заголовок.</span><span class="sxs-lookup"><span data-stu-id="b5cd6-160">**Body copy**: Use to convey detail that is either too long or not important enough to include in the header.</span></span>|
|<span data-ttu-id="b5cd6-161">C</span><span class="sxs-lookup"><span data-stu-id="b5cd6-161">C</span></span>|<span data-ttu-id="b5cd6-162">**Основные** действия. В качестве наилучшей практики включаем 1-3 основных действия.</span><span class="sxs-lookup"><span data-stu-id="b5cd6-162">**Primary actions**: As a best practice, include 1-3 primary actions.</span></span> <span data-ttu-id="b5cd6-163">Разрешено не более шести.</span><span class="sxs-lookup"><span data-stu-id="b5cd6-163">A maximum of six are allowed.</span></span>|

## <a name="best-practices"></a><span data-ttu-id="b5cd6-164">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="b5cd6-164">Best practices</span></span>

### <a name="primary-and-secondary-actions"></a><span data-ttu-id="b5cd6-165">Первичные и вторичные действия</span><span class="sxs-lookup"><span data-stu-id="b5cd6-165">Primary and secondary actions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-do.png" alt-text="Пример наилучшей практики адаптивных карт." border="false":::

#### <a name="do-use-up-to-six-primary-actions"></a><span data-ttu-id="b5cd6-167">Do: Используйте до шести основных действий</span><span class="sxs-lookup"><span data-stu-id="b5cd6-167">Do: Use up to six primary actions</span></span>

<span data-ttu-id="b5cd6-168">Хотя адаптивные карты могут поддерживать шесть основных действий, большинству карт это не нужно.</span><span class="sxs-lookup"><span data-stu-id="b5cd6-168">While Adaptive Cards can support six primary actions, most cards don’t need that.</span></span> <span data-ttu-id="b5cd6-169">Действия должны быть четкими, краткими и прямыми.</span><span class="sxs-lookup"><span data-stu-id="b5cd6-169">Actions should be clear, concise, and straight forward.</span></span> <span data-ttu-id="b5cd6-170">Меньше больше.</span><span class="sxs-lookup"><span data-stu-id="b5cd6-170">Less is more.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-dont.png" alt-text="В примере показана лучшая практика адаптивных карт." border="false":::

#### <a name="dont-use-more-than-six-primary-actions"></a><span data-ttu-id="b5cd6-172">Не используйте более шести основных действий</span><span class="sxs-lookup"><span data-stu-id="b5cd6-172">Don't: Use more than six primary actions</span></span>

<span data-ttu-id="b5cd6-173">Адаптивные карты должны представлять быстрое и оперативное содержимое.</span><span class="sxs-lookup"><span data-stu-id="b5cd6-173">Adaptive Cards should present quick, actionable content.</span></span> <span data-ttu-id="b5cd6-174">Слишком много действий может переполохить пользователя.</span><span class="sxs-lookup"><span data-stu-id="b5cd6-174">Too many actions can overwhelm a user.</span></span>

   :::column-end:::
:::row-end:::

### <a name="frequency"></a><span data-ttu-id="b5cd6-175">Частота</span><span class="sxs-lookup"><span data-stu-id="b5cd6-175">Frequency</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/frequency-do.png" alt-text="Иллюстрация с лучшими примерами адаптивных карт." border="false":::

#### <a name="do-be-concise"></a><span data-ttu-id="b5cd6-177">Do: Быть кратким</span><span class="sxs-lookup"><span data-stu-id="b5cd6-177">Do: Be concise</span></span>

<span data-ttu-id="b5cd6-178">Можно легко отправить несколько карт в беседу, но после того, как карты прокрутки из виду, они становятся менее полезными.</span><span class="sxs-lookup"><span data-stu-id="b5cd6-178">It's easy to send multiple cards into a conversation, but once cards scroll out of view, they become less useful.</span></span> <span data-ttu-id="b5cd6-179">Попробуйте ограничиться основными.</span><span class="sxs-lookup"><span data-stu-id="b5cd6-179">Try to limit yourself to the essentials.</span></span> <span data-ttu-id="b5cd6-180">Это особенно актуально в канале, где пользователи менее терпимо воспринимают то, что они воспринимают как "шум".</span><span class="sxs-lookup"><span data-stu-id="b5cd6-180">This is especially true in a channel where users have less tolerance for what they perceive as "noise".</span></span>
