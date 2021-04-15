---
title: Введение карт
description: Описание карт и их использования в ботах, соединителах и расширениях обмена сообщениями
ms.topic: conceptual
keywords: соединители боты-карты обмена сообщениями
ms.openlocfilehash: c2fe0aea142a96643e33e16acc08bcfd8c33e92e
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696460"
---
# <a name="cards"></a><span data-ttu-id="7f526-104">Карточки</span><span class="sxs-lookup"><span data-stu-id="7f526-104">Cards</span></span>

<span data-ttu-id="7f526-105">Карта *—* это контейнер пользовательского интерфейса (пользовательского интерфейса) для коротких или связанных частей информации.</span><span class="sxs-lookup"><span data-stu-id="7f526-105">A *card* is a user-interface (UI) container for short or related pieces of information.</span></span> <span data-ttu-id="7f526-106">Карты могут иметь несколько свойств и вложений.</span><span class="sxs-lookup"><span data-stu-id="7f526-106">Cards can have multiple properties and attachments.</span></span> <span data-ttu-id="7f526-107">Карты могут включать кнопки, которые могут вызывать [действия карты.](~/task-modules-and-cards/cards/cards-actions.md)</span><span class="sxs-lookup"><span data-stu-id="7f526-107">Cards can include buttons which can trigger [Card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

## <a name="adaptive-cards"></a><span data-ttu-id="7f526-108">Адаптивные карты</span><span class="sxs-lookup"><span data-stu-id="7f526-108">Adaptive cards</span></span>

<span data-ttu-id="7f526-109">[Адаптивные карты](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card) — это новая спецификация кросс-продукта для карт в продуктах Майкрософт, включая Bots, Cortana, Outlook и Windows.</span><span class="sxs-lookup"><span data-stu-id="7f526-109">[Adaptive cards](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card) are a new cross product specification for cards in Microsoft products including Bots, Cortana, Outlook, and Windows.</span></span> <span data-ttu-id="7f526-110">Это рекомендуемый тип карты для разработки новых команд.</span><span class="sxs-lookup"><span data-stu-id="7f526-110">They are the recommended card type for new Teams development.</span></span> <span data-ttu-id="7f526-111">Общие сведения из группы адаптивных карт см. в [обзоре адаптивных карт.](/adaptive-cards)</span><span class="sxs-lookup"><span data-stu-id="7f526-111">For general information from the Adaptive cards team see [Adaptive Cards Overview](/adaptive-cards).</span></span> <span data-ttu-id="7f526-112">Адаптивные карты можно использовать везде, где можно использовать существующие карты Hero, карты Office365 и эскизы.</span><span class="sxs-lookup"><span data-stu-id="7f526-112">You can use adaptive cards anywhere you can use existing Hero cards, Office365 cards, and Thumbnail cards.</span></span>

<span data-ttu-id="7f526-113">В дополнение к адаптивным картам Teams поддерживает два других типа карт:</span><span class="sxs-lookup"><span data-stu-id="7f526-113">In addition to Adaptive Cards, Teams supports two other types of cards:</span></span>

* <span data-ttu-id="7f526-114">Соединитетельные карты, используемые в составе соединители Office 365.</span><span class="sxs-lookup"><span data-stu-id="7f526-114">Connector Cards, used as part of Office 365 connectors.</span></span>
* <span data-ttu-id="7f526-115">Простые карты из базы ботов, такие как эскизы и карточки героев.</span><span class="sxs-lookup"><span data-stu-id="7f526-115">Simple cards from the bot framework, such as the thumbnail and hero cards.</span></span>

<span data-ttu-id="7f526-116">Эти типы карт более подробно описаны в [справочной карточке Teams.](~/task-modules-and-cards/cards/cards-reference.md)</span><span class="sxs-lookup"><span data-stu-id="7f526-116">These card types are described more fully in the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md).</span></span>

<span data-ttu-id="7f526-117">Teams использует карты в трех разных местах:</span><span class="sxs-lookup"><span data-stu-id="7f526-117">Teams uses cards in three different places:</span></span>

* <span data-ttu-id="7f526-118">Соединители</span><span class="sxs-lookup"><span data-stu-id="7f526-118">Connectors</span></span>
* <span data-ttu-id="7f526-119">боты;</span><span class="sxs-lookup"><span data-stu-id="7f526-119">Bots</span></span>
* <span data-ttu-id="7f526-120">расширения для обмена сообщениями;</span><span class="sxs-lookup"><span data-stu-id="7f526-120">Messaging extensions</span></span>

## <a name="adaptive-cards-and-incoming-webhooks"></a><span data-ttu-id="7f526-121">Адаптивные карты и входящие веб-окки</span><span class="sxs-lookup"><span data-stu-id="7f526-121">Adaptive cards and incoming webhooks</span></span>

> [!NOTE]
>
> <span data-ttu-id="7f526-122">✔ Все встроенные элементы схемы адаптивной карточки, кроме `Action.Submit`, полностью поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="7f526-122">✔ All native adaptive card schema elements, except `Action.Submit`, are fully supported.</span></span>
>
> <span data-ttu-id="7f526-123">✔ поддерживаемые действия [**Action.OpenURL,**](https://adaptivecards.io/explorer/Action.OpenUrl.html) [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html)и [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html).</span><span class="sxs-lookup"><span data-stu-id="7f526-123">✔ The supported actions are [**Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html), [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html), and [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html).</span></span>

## <a name="cards-in-connectors"></a><span data-ttu-id="7f526-124">Карты в соединители</span><span class="sxs-lookup"><span data-stu-id="7f526-124">Cards in Connectors</span></span>

<span data-ttu-id="7f526-125">Сначала карты были определены как часть Outlook и Office 365 и используются в составе соединители Office 365.</span><span class="sxs-lookup"><span data-stu-id="7f526-125">Cards were first defined as part of Outlook and Office 365, and are used as part of Office 365 Connectors.</span></span> <span data-ttu-id="7f526-126">Как и многие приложения Office 365, Teams поддерживает соединители.</span><span class="sxs-lookup"><span data-stu-id="7f526-126">Like many Office 365 applications, Teams supports Connectors.</span></span> <span data-ttu-id="7f526-127">Дополнительные данные о соединителках [в Office 365 соединители](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)для Microsoft Teams, а также спецификации для карт в соединителках в справочной карточке [actionable message.](/outlook/actionable-messages/card-reference)</span><span class="sxs-lookup"><span data-stu-id="7f526-127">You can learn more about Connectors in [Office 365 Connectors for Microsoft Teams](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md), and find the specification for cards in connectors in [Actionable message card reference](/outlook/actionable-messages/card-reference).</span></span>

## <a name="cards-in-bots"></a><span data-ttu-id="7f526-128">Карты в ботах</span><span class="sxs-lookup"><span data-stu-id="7f526-128">Cards in Bots</span></span>

<span data-ttu-id="7f526-129">Microsoft Bot Framework расширила спецификацию карт, добавив набор предопределяемых карт, которые боты могли использовать в качестве части бот-сообщений.</span><span class="sxs-lookup"><span data-stu-id="7f526-129">The Microsoft Bot Framework extended the cards specification by adding a set of predefined cards that bots could use as part of bot messages.</span></span> <span data-ttu-id="7f526-130">Teams поддерживает ботов с помощью Bot Framework, но поддерживает несколько другой набор этих карт.</span><span class="sxs-lookup"><span data-stu-id="7f526-130">Teams supports bots using the Bot Framework but it supports a slightly different set of these cards.</span></span> <span data-ttu-id="7f526-131">Общие сведения о картах в Bot Framework можно найти в [приложении Add rich card attachments to messages.](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)</span><span class="sxs-lookup"><span data-stu-id="7f526-131">General information on cards in Bot Framework can be found in [Add rich card attachments to messages](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards).</span></span> <span data-ttu-id="7f526-132">Эти карты в Teams *называются простыми* картами.</span><span class="sxs-lookup"><span data-stu-id="7f526-132">These cards are called *simple cards* in Teams.</span></span>

<span data-ttu-id="7f526-133">Боты в Teams могут использовать любой тип карты: простой, соединительные или адаптивные.</span><span class="sxs-lookup"><span data-stu-id="7f526-133">Bots in Teams can use any type of card: simple, connector or adaptive.</span></span> <span data-ttu-id="7f526-134">Карты, поддерживаемые ботами в Teams, подробно описаны в [справке по картам Teams.](~/task-modules-and-cards/cards/cards-reference.md)</span><span class="sxs-lookup"><span data-stu-id="7f526-134">Cards that are supported by bots in Teams are detailed in [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md).</span></span>  

## <a name="cards-in-messaging-extensions"></a><span data-ttu-id="7f526-135">Карты в расширениях обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="7f526-135">Cards in Messaging Extensions</span></span>

<span data-ttu-id="7f526-136">[Расширения обмена сообщениями также](~/messaging-extensions/what-are-messaging-extensions.md) могут возвращать карточку.</span><span class="sxs-lookup"><span data-stu-id="7f526-136">[Messaging Extensions](~/messaging-extensions/what-are-messaging-extensions.md) can also return a card.</span></span> <span data-ttu-id="7f526-137">Расширения обмена сообщениями могут использовать любые типы карт: простые, соединительные или адаптивные.</span><span class="sxs-lookup"><span data-stu-id="7f526-137">Messaging extensions can use any type of card: simple, connector or adaptive.</span></span> <span data-ttu-id="7f526-138">Эти карточки находятся в [справке по карточкам Teams.](~/task-modules-and-cards/cards/cards-reference.md)</span><span class="sxs-lookup"><span data-stu-id="7f526-138">These cards are found in the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md).</span></span>

## <a name="card-reference"></a><span data-ttu-id="7f526-139">Ссылка на карточку</span><span class="sxs-lookup"><span data-stu-id="7f526-139">Card reference</span></span>

<span data-ttu-id="7f526-140">Все карты, используемые Teams, перечислены в [справочной карточке Teams.](~/task-modules-and-cards/cards/cards-reference.md)</span><span class="sxs-lookup"><span data-stu-id="7f526-140">All cards used by Teams are listed in the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md).</span></span> <span data-ttu-id="7f526-141">В этой ссылке также описываются различия между картами Bot Framework и картами в Teams.</span><span class="sxs-lookup"><span data-stu-id="7f526-141">This reference also describes differences between Bot Framework cards and cards in Teams.</span></span>
