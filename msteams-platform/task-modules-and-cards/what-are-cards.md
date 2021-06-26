---
title: Карточки
description: Описание карт и их использования в ботах, соединители и расширениях обмена сообщениями
localization_priority: Normal
keywords: соединители боты-карты обмена сообщениями
ms.topic: overview
ms.openlocfilehash: f895423e5755dd85a7618b8907c4c3b0acbc3cf4
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140546"
---
# <a name="cards"></a><span data-ttu-id="812ad-104">Карточки</span><span class="sxs-lookup"><span data-stu-id="812ad-104">Cards</span></span>

<span data-ttu-id="812ad-105">Карта — это контейнер пользовательского интерфейса (пользовательского интерфейса) для коротких или связанных частей информации.</span><span class="sxs-lookup"><span data-stu-id="812ad-105">A card is a user interface (UI) container for short or related pieces of information.</span></span> <span data-ttu-id="812ad-106">Карты могут иметь несколько свойств и вложений и могут включать кнопки, которые запускают [действия карт.](~/task-modules-and-cards/cards/cards-actions.md)</span><span class="sxs-lookup"><span data-stu-id="812ad-106">Cards can have multiple properties and attachments and can include buttons, which trigger [card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span> <span data-ttu-id="812ad-107">С помощью карт можно организовать информацию в группы и предоставить пользователям возможность взаимодействовать с определенными частями информации.</span><span class="sxs-lookup"><span data-stu-id="812ad-107">Using cards, you can organize information into groups and give users the opportunity to interact with specific parts of the information.</span></span>

<span data-ttu-id="812ad-108">Боты для Teams поддерживают следующие типы карт: адаптивная карта, карта героя, карта списка, Office 365 соединительные карты, карточка получения, карточка подписи, эскизная карта и коллекции карт.</span><span class="sxs-lookup"><span data-stu-id="812ad-108">The bots for Teams support the following types of cards: Adaptive Card, hero card, list card, Office 365 Connector card, receipt card, signin card, thumbnail card, and card collections.</span></span> <span data-ttu-id="812ad-109">В зависимости от типа карты можно добавить в карты форматирование текста с помощью Markdown или HTML.</span><span class="sxs-lookup"><span data-stu-id="812ad-109">You can add rich text formatting to your cards using either Markdown or HTML, depending on the card type.</span></span> <span data-ttu-id="812ad-110">Карты, используемые ботами и расширениями обмена сообщениями в Microsoft Teams, добавляют и реагируют на действия этих карт, `openUrl` , , , и `messageBack` `imBack` `invoke` `signin` .</span><span class="sxs-lookup"><span data-stu-id="812ad-110">Cards used by bots and messaging extensions in Microsoft Teams, add and respond to these card actions, `openUrl`, `messageBack`, `imBack`, `invoke`, and `signin`.</span></span>

<span data-ttu-id="812ad-111">Teams использует карты в трех разных местах:</span><span class="sxs-lookup"><span data-stu-id="812ad-111">Teams uses cards in three different places:</span></span>

* <span data-ttu-id="812ad-112">Соединители</span><span class="sxs-lookup"><span data-stu-id="812ad-112">Connectors</span></span>
* <span data-ttu-id="812ad-113">боты;</span><span class="sxs-lookup"><span data-stu-id="812ad-113">Bots</span></span>
* <span data-ttu-id="812ad-114">расширения для обмена сообщениями;</span><span class="sxs-lookup"><span data-stu-id="812ad-114">Messaging extensions</span></span>

## <a name="cards-in-connectors"></a><span data-ttu-id="812ad-115">Карты в соединители</span><span class="sxs-lookup"><span data-stu-id="812ad-115">Cards in connectors</span></span>

<span data-ttu-id="812ad-116">Сначала карты определялись как часть Outlook Office 365 и теперь используются в Office 365 соединители.</span><span class="sxs-lookup"><span data-stu-id="812ad-116">Cards were first defined as part of Outlook and Office 365 and are now used as part of Office 365 Connectors.</span></span> <span data-ttu-id="812ad-117">Как и Office 365 приложений, Teams поддерживает соединители.</span><span class="sxs-lookup"><span data-stu-id="812ad-117">Like many Office 365 applications, Teams supports connectors.</span></span> <span data-ttu-id="812ad-118">Дополнительные сведения см. [в Office 365 соединители для Teams.](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)</span><span class="sxs-lookup"><span data-stu-id="812ad-118">For more information, see [Office 365 Connectors for Teams](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md).</span></span> <span data-ttu-id="812ad-119">Спецификацию для карт в соединителках можно найти в справке к карточкам [сообщений.](/outlook/actionable-messages/card-reference)</span><span class="sxs-lookup"><span data-stu-id="812ad-119">You can find the specification for cards in connectors in [actionable message card reference](/outlook/actionable-messages/card-reference).</span></span>

## <a name="cards-in-bots"></a><span data-ttu-id="812ad-120">Карты в ботах</span><span class="sxs-lookup"><span data-stu-id="812ad-120">Cards in bots</span></span>

<span data-ttu-id="812ad-121">В Microsoft Bot Framework расширяется спецификация карт, добавляя набор предопределяемых карт, которые боты могут использовать в качестве части бот-сообщений.</span><span class="sxs-lookup"><span data-stu-id="812ad-121">The Microsoft Bot Framework extends the cards specification by adding a set of predefined cards that bots can use as part of bot messages.</span></span> <span data-ttu-id="812ad-122">Teams поддерживает ботов с помощью Bot Framework, но поддерживает другой набор этих карт.</span><span class="sxs-lookup"><span data-stu-id="812ad-122">Teams supports bots using the Bot Framework, but it supports a different set of these cards.</span></span> <span data-ttu-id="812ad-123">Общие сведения о картах в Bot Framework можно найти в добавлении вложения с богатыми [картами в сообщения.](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)</span><span class="sxs-lookup"><span data-stu-id="812ad-123">General information on cards in Bot Framework can be found in [add rich card attachments to messages](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards).</span></span> <span data-ttu-id="812ad-124">Эти карты в Teams.</span><span class="sxs-lookup"><span data-stu-id="812ad-124">These cards are called simple cards in Teams.</span></span>

<span data-ttu-id="812ad-125">Боты в Teams могут использовать простые карты, соединительные карты или адаптивные карты.</span><span class="sxs-lookup"><span data-stu-id="812ad-125">Bots in Teams can use simple cards, connector cards, or Adaptive Cards.</span></span> <span data-ttu-id="812ad-126">[Типы карт предоставляют](~/task-modules-and-cards/cards/cards-reference.md) сведения о картах, поддерживаемых ботами в Teams.</span><span class="sxs-lookup"><span data-stu-id="812ad-126">[Types of cards](~/task-modules-and-cards/cards/cards-reference.md) provides information on cards, supported by bots in Teams.</span></span>

## <a name="cards-in-messaging-extensions"></a><span data-ttu-id="812ad-127">Карты в расширениях обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="812ad-127">Cards in messaging extensions</span></span>

<span data-ttu-id="812ad-128">[Расширения обмена сообщениями также](~/messaging-extensions/what-are-messaging-extensions.md) могут возвращать карточку.</span><span class="sxs-lookup"><span data-stu-id="812ad-128">[Messaging extensions](~/messaging-extensions/what-are-messaging-extensions.md) can also return a card.</span></span> <span data-ttu-id="812ad-129">Расширения обмена сообщениями могут использовать простые карты, соединительные карты или адаптивные карты.</span><span class="sxs-lookup"><span data-stu-id="812ad-129">Messaging extensions can use simple cards, connector cards, or Adaptive Cards.</span></span> <span data-ttu-id="812ad-130">Эти карты находятся в [типах карт.](~/task-modules-and-cards/cards/cards-reference.md)</span><span class="sxs-lookup"><span data-stu-id="812ad-130">These cards are found in [types of cards](~/task-modules-and-cards/cards/cards-reference.md).</span></span>

## <a name="types-of-cards"></a><span data-ttu-id="812ad-131">Типы карт</span><span class="sxs-lookup"><span data-stu-id="812ad-131">Types of cards</span></span>

<span data-ttu-id="812ad-132">Все карты, используемые Teams, перечислены в [типах карт.](~/task-modules-and-cards/cards/cards-reference.md)</span><span class="sxs-lookup"><span data-stu-id="812ad-132">All cards used by Teams are listed in [types of cards](~/task-modules-and-cards/cards/cards-reference.md).</span></span> <span data-ttu-id="812ad-133">В этой ссылке также описываются различия между картами Bot Framework и картами в Teams.</span><span class="sxs-lookup"><span data-stu-id="812ad-133">This reference also describes differences between Bot Framework cards and cards in Teams.</span></span>

## <a name="adaptive-cards"></a><span data-ttu-id="812ad-134">Адаптивные карточки</span><span class="sxs-lookup"><span data-stu-id="812ad-134">Adaptive Cards</span></span>

> [!VIDEO https://www.youtube-nocookie.com/embed/J12lKt717Ws]

<span data-ttu-id="812ad-135">[Адаптивные карты](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card) — это новая спецификация кросс-продукта для карт в продуктах Майкрософт, включая ботов, Кортана, Outlook и Windows.</span><span class="sxs-lookup"><span data-stu-id="812ad-135">[Adaptive Cards](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card) are a new cross product specification for cards in Microsoft products including bots, Cortana, Outlook, and Windows.</span></span> <span data-ttu-id="812ad-136">Это рекомендуемый тип карты для Teams разработки.</span><span class="sxs-lookup"><span data-stu-id="812ad-136">They are the recommended card type for new Teams development.</span></span> <span data-ttu-id="812ad-137">Общие сведения из группы адаптивных карт см. в [обзоре Адаптивные карты.](/adaptive-cards)</span><span class="sxs-lookup"><span data-stu-id="812ad-137">For general information from the Adaptive Cards team, see [Adaptive Cards overview](/adaptive-cards).</span></span> <span data-ttu-id="812ad-138">Адаптивные карты можно использовать везде, где вы используете существующие карты героев, Office 365 и эскизные карты.</span><span class="sxs-lookup"><span data-stu-id="812ad-138">You can use Adaptive Cards anywhere you use existing hero cards, Office 365 cards, and thumbnail cards.</span></span>

<span data-ttu-id="812ad-139">Помимо адаптивных карт, Teams поддерживает два других типа карт:</span><span class="sxs-lookup"><span data-stu-id="812ad-139">In addition to Adaptive Cards, Teams supports two other types of cards:</span></span>

* <span data-ttu-id="812ad-140">Соединитетельные карточки. Используется в Office 365 соединители.</span><span class="sxs-lookup"><span data-stu-id="812ad-140">Connector cards: Used as part of Office 365 Connectors.</span></span>
* <span data-ttu-id="812ad-141">Простые карты. Используется из bot Framework, например эскизы и карточки героев.</span><span class="sxs-lookup"><span data-stu-id="812ad-141">Simple cards: Used from the Bot Framework, such as the thumbnail and hero cards.</span></span>

### <a name="adaptive-cards-and-incoming-webhooks"></a><span data-ttu-id="812ad-142">Адаптивные карты и входящие веб-окки</span><span class="sxs-lookup"><span data-stu-id="812ad-142">Adaptive Cards and Incoming Webhooks</span></span>

> [!VIDEO https://www.youtube-nocookie.com/embed/y5pbJI43Zvg]

> [!NOTE]
> * <span data-ttu-id="812ad-143">Все элементы схемы адаптивной карты, за `Action.Submit` исключением, полностью поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="812ad-143">All native Adaptive Card schema elements, except `Action.Submit`, are fully supported.</span></span>
> * <span data-ttu-id="812ad-144">Поддерживаемые действия [**Action.OpenURL,**](https://adaptivecards.io/explorer/Action.OpenUrl.html) [**Action.ShowCard,**](https://adaptivecards.io/explorer/Action.ShowCard.html) [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html)иAction.Exe [**мило**](/adaptive-cards/authoring-cards/universal-action-model#actionexecute).</span><span class="sxs-lookup"><span data-stu-id="812ad-144">The supported actions are [**Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html), [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html), [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html), and [**Action.Execute**](/adaptive-cards/authoring-cards/universal-action-model#actionexecute).</span></span>

<span data-ttu-id="812ad-145">Адаптивные карты с входящие веб-окки позволяют использовать богатые и гибкие возможности адаптивных карт.</span><span class="sxs-lookup"><span data-stu-id="812ad-145">Adaptive Cards with Incoming Webhooks enables you to use the rich and flexible capabilities of Adaptive Cards.</span></span> <span data-ttu-id="812ad-146">Он отправляет данные с помощью входящих веб-Teams из веб-службы.</span><span class="sxs-lookup"><span data-stu-id="812ad-146">It sends data using Incoming Webhooks in Teams from their web service.</span></span>

## <a name="see-also"></a><span data-ttu-id="812ad-147">См. также</span><span class="sxs-lookup"><span data-stu-id="812ad-147">See also</span></span>

* [<span data-ttu-id="812ad-148">Формат карты в Teams</span><span class="sxs-lookup"><span data-stu-id="812ad-148">Format cards in Teams</span></span>](~/task-modules-and-cards/cards/cards-format.md)
* [<span data-ttu-id="812ad-149">Дизайн адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="812ad-149">Design Adaptive Cards</span></span>](~/task-modules-and-cards/cards/design-effective-cards.md)

## <a name="next-step"></a><span data-ttu-id="812ad-150">Следующий этап</span><span class="sxs-lookup"><span data-stu-id="812ad-150">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="812ad-151">Типы карт</span><span class="sxs-lookup"><span data-stu-id="812ad-151">Types of cards</span></span>](~/task-modules-and-cards/cards/cards-reference.md)