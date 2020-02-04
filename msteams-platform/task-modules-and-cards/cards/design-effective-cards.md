---
title: Разработка эффективных карточек
description: Описывает рекомендации по проектированию для создания карточек.
keywords: рекомендации по проектированию Teams ссылаются на карточки платформы, адаптируемые к легковесным
ms.openlocfilehash: 33ee0b59a3a5a1490d6e2106f8532094ed852598
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675608"
---
# <a name="designing-effective-cards"></a><span data-ttu-id="ab81c-104">Разработка эффективных карточек</span><span class="sxs-lookup"><span data-stu-id="ab81c-104">Designing effective cards</span></span>

<span data-ttu-id="ab81c-105">Карточки — это фрагменты контента, которые можно добавить в беседу с помощью ленты, соединителя или приложения.</span><span class="sxs-lookup"><span data-stu-id="ab81c-105">Cards are actionable snippets of content that you can add to a conversation through a bot, a connector, or app.</span></span> <span data-ttu-id="ab81c-106">С помощью карточек с текстом, рисунками и кнопками можно общаться с аудиторией.</span><span class="sxs-lookup"><span data-stu-id="ab81c-106">Using text, graphics, and buttons, cards allow you to communicate with an audience.</span></span>

<span data-ttu-id="ab81c-107">Наша инфраструктура позволяет избежать затрат на разработку полностью функционального UX.</span><span class="sxs-lookup"><span data-stu-id="ab81c-107">Our card framework eliminates the burden of designing a fully functional UX.</span></span> <span data-ttu-id="ab81c-108">Мы разработали несколько стандартных типов карточек, каждая из которых соответствует поддерживаемым платформам.</span><span class="sxs-lookup"><span data-stu-id="ab81c-108">We developed several standard card types and each one fits within our supported platforms.</span></span> <span data-ttu-id="ab81c-109">Это означает, что макет полностью учитывается, и вам не придется разрабатывать разные итерации карты на разных платформах.</span><span class="sxs-lookup"><span data-stu-id="ab81c-109">This means layout is completely taken care of, and you won’t need to develop different card iterations across platforms.</span></span> <span data-ttu-id="ab81c-110">Вместо этого вы можете сосредоточиться на наборе содержимого.</span><span class="sxs-lookup"><span data-stu-id="ab81c-110">Instead, you can focus on dialing in your content.</span></span>

---

## <a name="guidelines"></a><span data-ttu-id="ab81c-111">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="ab81c-111">Guidelines</span></span>

<span data-ttu-id="ab81c-112">Представьте карточку в ответ на вопрос пользователя или параметр.</span><span class="sxs-lookup"><span data-stu-id="ab81c-112">Think of a card as a response to a user question or a setting.</span></span> <span data-ttu-id="ab81c-113">Карточка может отвечать на прямые вопросы (например, «сколько открытых ошибок?») или к условию (например, "отправлять список моих открытых ошибок в 9 сразу каждый день").</span><span class="sxs-lookup"><span data-stu-id="ab81c-113">A card can respond to a direct question (like, “How many open bugs do I have?”) or to a condition (like, “Send a list of my open bugs at 9 am every day”).</span></span>

> [!TIP]
> <span data-ttu-id="ab81c-114">С помощью одного из наших стандартных типов карточек вы уже знаете, что все ваши ответы будут хорошо отрисовываться на всех поддерживаемых платформах.</span><span class="sxs-lookup"><span data-stu-id="ab81c-114">Using one of our standard card types means you’ll already know that all your responses will render nicely across each supported platform.</span></span>

<span data-ttu-id="ab81c-115">Карточка может содержать любой из следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="ab81c-115">A card could include any of the following elements:</span></span><br />

[!include[Card anatomy](~/includes/design/card-image-anatomy.html)]

1. <span data-ttu-id="ab81c-116">**Текст конверта**: лучше всего подходит для сообщений чата.</span><span class="sxs-lookup"><span data-stu-id="ab81c-116">**Envelope text**: Best used for chat messages.</span></span> <span data-ttu-id="ab81c-117">Например, если вы хотите сказать: "Вот что я нашел!"</span><span class="sxs-lookup"><span data-stu-id="ab81c-117">For example, if you want a bot to say: “Here’s what I found!”</span></span> <span data-ttu-id="ab81c-118">или "время для дайджеста новостей 1:00", это сообщение лучше всего отображать в тексте конверта.</span><span class="sxs-lookup"><span data-stu-id="ab81c-118">or “Time for your 1:00 news digest”, that message is best displayed in envelope text.</span></span>

   <span data-ttu-id="ab81c-119">Текст конверта — это отличный способ вставить в службу небольшое индивидуальность, просто не забывайте, что это довольно короткий.</span><span class="sxs-lookup"><span data-stu-id="ab81c-119">Envelope text is a great way to inject a little personality into your service—just remember to keep it relatively short.</span></span>

2. <span data-ttu-id="ab81c-120">**Название**: ваш заголовок всегда будет самым большим в карточке текстом.</span><span class="sxs-lookup"><span data-stu-id="ab81c-120">**Title**: Your title will always be the largest text in your card.</span></span> <span data-ttu-id="ab81c-121">Он также выступает в качестве «обработчика», поэтому попробуйте оставить название коротким, запоминающим и легким для сканирования.</span><span class="sxs-lookup"><span data-stu-id="ab81c-121">It also serves as your “hook”, so try to keep the title short, memorable, and easy to scan.</span></span>

3. <span data-ttu-id="ab81c-122">Подзаголовок: лучше всего подходит для присвоения атрибутов, рекламных **заголовков**или дополнительной директивы.</span><span class="sxs-lookup"><span data-stu-id="ab81c-122">**Subtitle**: Best used for attribution, taglines, or as a secondary directive.</span></span> <span data-ttu-id="ab81c-123">Этот компонент отображается непосредственно под заголовком.</span><span class="sxs-lookup"><span data-stu-id="ab81c-123">This component appears just below your title.</span></span>

4. <span data-ttu-id="ab81c-124">**Image**: изображения масштабируются в соответствии с их контейнером.</span><span class="sxs-lookup"><span data-stu-id="ab81c-124">**Image**: Images scale to fit their container.</span></span> <span data-ttu-id="ab81c-125">Для карточек главный Имиджевый баннер задана максимальная ширина 420px, эскизы имеют максимальную ширину 100px, а представления списков разрешены только для интервалами по 32 в режиме рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="ab81c-125">Hero cards have a max width of 420px, thumbnails have a max width of 100px, and list views only allow for 32px in desktop mode.</span></span>

5. <span data-ttu-id="ab81c-126">**Text**: наиболее подходящий для обычного текста в тексте карточки.</span><span class="sxs-lookup"><span data-stu-id="ab81c-126">**Text**: Best used for plain text in the body of your card.</span></span> <span data-ttu-id="ab81c-127">Максимальная длина зависит от выбранного типа карты.</span><span class="sxs-lookup"><span data-stu-id="ab81c-127">Your max length depends on the card type you’ve selected.</span></span>

6. <span data-ttu-id="ab81c-128">**Кнопки**: наилучшим образом использовать для открытия веб-страниц, вкладок или дополнительного содержимого чата.</span><span class="sxs-lookup"><span data-stu-id="ab81c-128">**Buttons**: Best used to open web pages, tabs, or additional chat content.</span></span> <span data-ttu-id="ab81c-129">Не забудьте оставить текст кнопки короче и в точке.</span><span class="sxs-lookup"><span data-stu-id="ab81c-129">Make sure to keep your button text short and to the point.</span></span>

   <span data-ttu-id="ab81c-130">Вы можете включить до 6 кнопок на карточку, но мы рекомендуем использовать следующую философскую философию.</span><span class="sxs-lookup"><span data-stu-id="ab81c-130">You can include up to 6 buttons per card, but we’d recommend following a ‘less is more’ philosophy here.</span></span>

7. <span data-ttu-id="ab81c-131">**Коснитесь области**: это доступная для щелчка область карточки.</span><span class="sxs-lookup"><span data-stu-id="ab81c-131">**Tap region**: This is the clickable region of your card.</span></span> <span data-ttu-id="ab81c-132">Большинству пользователей будет необходимо автоматически щелкать изображения, поэтому постарайтесь и создавать текст, чтобы они знали, где они должны быть нажаты или нажаты.</span><span class="sxs-lookup"><span data-stu-id="ab81c-132">Most users will want to click on images automatically, so try and craft your text so they know where they should tap or click.</span></span>

> [!TIP]
> <span data-ttu-id="ab81c-133">Нет необходимости включать каждый элемент в каждую создаваемую карточку.</span><span class="sxs-lookup"><span data-stu-id="ab81c-133">There’s no need to include every element in each card you create.</span></span> <span data-ttu-id="ab81c-134">Разрешите вашему контенту задиктовать свои элементы.</span><span class="sxs-lookup"><span data-stu-id="ab81c-134">Let your content dictate your elements.</span></span>

---

## <a name="types-of-cards"></a><span data-ttu-id="ab81c-135">Типы карточек</span><span class="sxs-lookup"><span data-stu-id="ab81c-135">Types of cards</span></span>

### <a name="hero"></a><span data-ttu-id="ab81c-136">Главный имиджевый баннер</span><span class="sxs-lookup"><span data-stu-id="ab81c-136">Hero</span></span>

<span data-ttu-id="ab81c-137">Самая крупная карточка.</span><span class="sxs-lookup"><span data-stu-id="ab81c-137">Our largest card.</span></span> <span data-ttu-id="ab81c-138">Лучше всего подходит для статей, длинных описаний или сценариев, в которых изображение относится к большинству материала.</span><span class="sxs-lookup"><span data-stu-id="ab81c-138">Best used for articles, long descriptions, or scenarios where your image is telling most of the story.</span></span>

[!include[Card anatomy](~/includes/design/card-image-hero.html)]

### <a name="thumbnail"></a><span data-ttu-id="ab81c-139">Thumbnail</span><span class="sxs-lookup"><span data-stu-id="ab81c-139">Thumbnail</span></span>

<span data-ttu-id="ab81c-140">Короткие и неблагоприятные.</span><span class="sxs-lookup"><span data-stu-id="ab81c-140">Short and sweet.</span></span> <span data-ttu-id="ab81c-141">Эти карты идеально подходят для коротких ответов, или если вы хотите вернуть сразу несколько карточек, чтобы пользователь мог выбрать один из вариантов.</span><span class="sxs-lookup"><span data-stu-id="ab81c-141">These cards are ideal for short answers, or if you want to return several cards at once so the user can choose from a bunch of options.</span></span> <span data-ttu-id="ab81c-142">Мы думаем, что это отличный способ глубокой ссылки на другую вкладку или веб-службу.</span><span class="sxs-lookup"><span data-stu-id="ab81c-142">We think these are a great way to deep link to another tab or a web service.</span></span>

[!include[Card anatomy](~/includes/design/card-image-thumbnail.html)]

### <a name="sign-in"></a><span data-ttu-id="ab81c-143">Вход</span><span class="sxs-lookup"><span data-stu-id="ab81c-143">Sign in</span></span>

<span data-ttu-id="ab81c-144">Некоторые службы требуют, чтобы пользователи выполняли вход независимо от нашей проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="ab81c-144">Some services require users to sign in independently of our authentication.</span></span> <span data-ttu-id="ab81c-145">В этом событии Вы хотите представить карточку входа, прежде чем пользователь сможет подключиться к службе.</span><span class="sxs-lookup"><span data-stu-id="ab81c-145">In that event, you would present a sign-in card before the user can connect to your service.</span></span>

[!include[Card anatomy](~/includes/design/card-image-signin.html)]

> [!TIP]
> <span data-ttu-id="ab81c-146">Ограничьте дополнительные карты входа, так как они значительно замедлены для новых пользователей.</span><span class="sxs-lookup"><span data-stu-id="ab81c-146">Limit the occurrences of an additional sign-in card since they pose a significant speed bump for new users.</span></span>

---

## <a name="card-collections"></a><span data-ttu-id="ab81c-147">Коллекции карточек</span><span class="sxs-lookup"><span data-stu-id="ab81c-147">Card collections</span></span>

<span data-ttu-id="ab81c-148">Кроме того, у нас есть стандартные типы карточек, которые лучше всего подходят для одновременного отображения нескольких фрагментов контента или быстрого выполнения.</span><span class="sxs-lookup"><span data-stu-id="ab81c-148">We also have standard card types that are best used when you want to present several pieces of content at once or in quick succession.</span></span> <span data-ttu-id="ab81c-149">Для этой цели у нас есть обойма, дайджест, список и то, что мы вызываем с помощью функции объединения с подходящей копией.</span><span class="sxs-lookup"><span data-stu-id="ab81c-149">For that purpose, we have a carousel, a digest, a list, and what we call a ‘bubble merge’.</span></span>

### <a name="carousel"></a><span data-ttu-id="ab81c-150">Карусель</span><span class="sxs-lookup"><span data-stu-id="ab81c-150">Carousel</span></span>

<span data-ttu-id="ab81c-151">Лучше всего подходит для статей, покупок и обзора карточек.</span><span class="sxs-lookup"><span data-stu-id="ab81c-151">Best used for articles, shopping, and browsing through cards.</span></span>

[!include[Card anatomy](~/includes/design/card-image-carousel.html)]

> [!TIP]
> <span data-ttu-id="ab81c-152">Обойма будет максимальной высотой самой большой карточки.</span><span class="sxs-lookup"><span data-stu-id="ab81c-152">The carousel will be the max height of your largest card.</span></span> <span data-ttu-id="ab81c-153">Рекомендуется использовать одни и те же типы карточек и поля контента по всему.</span><span class="sxs-lookup"><span data-stu-id="ab81c-153">We recommend using the same card type and content fields throughout.</span></span>

### <a name="digest"></a><span data-ttu-id="ab81c-154">Digest</span><span class="sxs-lookup"><span data-stu-id="ab81c-154">Digest</span></span>

<span data-ttu-id="ab81c-155">Лучше всего подходит для новостей, дайджестов и всякий раз, когда необходимо, чтобы пользователь одновременно просматривает несколько карточек.</span><span class="sxs-lookup"><span data-stu-id="ab81c-155">Best used for news, digests, and whenever you want the user to view multiple cards at once.</span></span> <span data-ttu-id="ab81c-156">Рекомендуется использовать карты эскизов для дайджестов.</span><span class="sxs-lookup"><span data-stu-id="ab81c-156">We recommend using thumbnail cards for digests.</span></span>

[!include[Card anatomy](~/includes/design/card-image-digest.html)]

### <a name="lists"></a><span data-ttu-id="ab81c-157">Списки</span><span class="sxs-lookup"><span data-stu-id="ab81c-157">Lists</span></span>

<span data-ttu-id="ab81c-158">Списки — это отличный способ представить прочитаемым набор объектов в сценарии "Выбор одного из этих элементов".</span><span class="sxs-lookup"><span data-stu-id="ab81c-158">Lists are a great way to present a scannable set of objects in a “pick one of these” scenario.</span></span> <span data-ttu-id="ab81c-159">Списки лучше всего использовать для элементов, для которых не требуется много объяснений.</span><span class="sxs-lookup"><span data-stu-id="ab81c-159">Lists are best used for items that don’t need a lot of explanation.</span></span>

[!include[Card anatomy](~/includes/design/card-image-list.html)]

### <a name="bubble-merge"></a><span data-ttu-id="ab81c-160">Слияние пузырьков</span><span class="sxs-lookup"><span data-stu-id="ab81c-160">Bubble merge</span></span>

<span data-ttu-id="ab81c-161">Некоторые интересные эффекты можно достигнуть, отправив один главный Имиджевый баннер и несколько эскизов в быструю удачную отправку.</span><span class="sxs-lookup"><span data-stu-id="ab81c-161">Some interesting effects can be achieved by sending one hero and several thumbnails in quick succession.</span></span> <span data-ttu-id="ab81c-162">Рекомендуется использовать этот подход, если вы хотите обслуживать основной результат, но добавить еще несколько связанных элементов.</span><span class="sxs-lookup"><span data-stu-id="ab81c-162">We recommend this approach when you want to serve a main result but include a few more related items.</span></span>

[!include[Card anatomy](~/includes/design/card-image-bubble-merge.html)]

---

## <a name="best-practices"></a><span data-ttu-id="ab81c-163">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="ab81c-163">Best practices</span></span>

### <a name="keep-the-noise-down"></a><span data-ttu-id="ab81c-164">Оставить шум вниз</span><span class="sxs-lookup"><span data-stu-id="ab81c-164">Keep the noise down</span></span>

<span data-ttu-id="ab81c-165">Вы можете легко отправить несколько карточек в беседу, но после того, как карточки пропрокручиваются из представления, они становятся менее удобными.</span><span class="sxs-lookup"><span data-stu-id="ab81c-165">It’s easy to send multiple cards into a conversation, but once cards scroll out of view, they become less useful.</span></span> <span data-ttu-id="ab81c-166">Попробуйте ограничиться основными сведениями.</span><span class="sxs-lookup"><span data-stu-id="ab81c-166">Try to limit yourself to the essentials.</span></span> <span data-ttu-id="ab81c-167">Это особенно справедливо в канале, где пользователи имеют меньшую отклонения для того, что они считают "шумом".</span><span class="sxs-lookup"><span data-stu-id="ab81c-167">This is especially true in a channel where users have less tolerance for what they perceive as “noise”.</span></span>

### <a name="test-on-mobile"></a><span data-ttu-id="ab81c-168">Проверка на мобильных устройствах</span><span class="sxs-lookup"><span data-stu-id="ab81c-168">Test on mobile</span></span>

<span data-ttu-id="ab81c-169">Мобильные среды имеют ограниченный объем и пропускную способность, поэтому следует соблюдать осторожность, включая изображения с превышением размера и большие наборы данных в списках и лентах.</span><span class="sxs-lookup"><span data-stu-id="ab81c-169">Mobile environments are space- and bandwidth-constrained, so be cautious about including oversized images and large data sets in lists and carousels.</span></span> <span data-ttu-id="ab81c-170">Кроме того, ширина и длина заголовка будут обрезаны на мобильном устройстве, поэтому необходимо проследить за другим делом.</span><span class="sxs-lookup"><span data-stu-id="ab81c-170">Also, title widths and text lengths will truncate on mobile, so that’s another thing to keep an eye on.</span></span>

### <a name="check-your-graphics"></a><span data-ttu-id="ab81c-171">Проверка графики</span><span class="sxs-lookup"><span data-stu-id="ab81c-171">Check your graphics</span></span>

<span data-ttu-id="ab81c-172">Графические объекты будут масштабироваться, поэтому не забудьте просмотреть их на всех платформах.</span><span class="sxs-lookup"><span data-stu-id="ab81c-172">Graphics are going to scale, so be sure to preview them on all platforms.</span></span>

### <a name="avoid-including-text-in-a-graphic"></a><span data-ttu-id="ab81c-173">Избегайте включения текста в графику</span><span class="sxs-lookup"><span data-stu-id="ab81c-173">Avoid including text in a graphic</span></span>

<span data-ttu-id="ab81c-174">Все, что должно быть прочитано пользователем, должно быть включено в текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="ab81c-174">Anything that needs to be read by a user should be included in a text field.</span></span> <span data-ttu-id="ab81c-175">После динамического масштабирования изображения любой текст, добавляемый к рисунку, может стать нечитаемым.</span><span class="sxs-lookup"><span data-stu-id="ab81c-175">Once an image is dynamically scaled, any text you add to a graphic may become unintelligible.</span></span>

### <a name="use-mentions-if-you-want-the-attention-of-specific-users"></a><span data-ttu-id="ab81c-176">Используйте упоминания, если вы хотите уделить особое внимание определенным пользователям.</span><span class="sxs-lookup"><span data-stu-id="ab81c-176">Use mentions if you want the attention of specific users</span></span>

> [!NOTE]
> <span data-ttu-id="ab81c-177">Упоминание поддержки в карточках в настоящее время поддерживается только в [режиме предварительного просмотра разработчика](~/resources/dev-preview/developer-preview-intro.md) .</span><span class="sxs-lookup"><span data-stu-id="ab81c-177">Mention support in cards is currently supported in [Developer Preview](~/resources/dev-preview/developer-preview-intro.md) only.</span></span>

<span data-ttu-id="ab81c-178">Упоминание — это отличный способ уведомления определенных пользователей в команде или группе чата.</span><span class="sxs-lookup"><span data-stu-id="ab81c-178">Mentions are a great way to notify specific users in a Team or group chat.</span></span> <span data-ttu-id="ab81c-179">Вы можете включить упоминание в карточку в таких сценариях, как задача, назначенная пользователю или предоставляющая благодарностью участнику.</span><span class="sxs-lookup"><span data-stu-id="ab81c-179">You can include a mention in card in scenarios like, a task thats assigned to a user or giving Kudos to a teammate.</span></span> <span data-ttu-id="ab81c-180">Сведения о том, как включить упоминание в карточки на [странице форматирования карты](~/task-modules-and-cards/cards/cards-format.md).</span><span class="sxs-lookup"><span data-stu-id="ab81c-180">Learn how to include mentions in cards in the [card formatting page](~/task-modules-and-cards/cards/cards-format.md).</span></span> 
