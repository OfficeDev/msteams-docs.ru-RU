---
title: Введение карт
description: Описание карт и их использования в ботах, соединителах и расширениях обмена сообщениями
localization_priority: Normal
ms.topic: conceptual
keywords: соединители боты-карты обмена сообщениями
ms.openlocfilehash: 77dcbb7d0472b584623e878df956a6165296f4cf
ms.sourcegitcommit: 1256639fa424e3833b44207ce847a245824d48e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/29/2021
ms.locfileid: "52088754"
---
# <a name="cards"></a><span data-ttu-id="8e286-104">Карточки</span><span class="sxs-lookup"><span data-stu-id="8e286-104">Cards</span></span>

<span data-ttu-id="8e286-105">Карта *—* это контейнер пользовательского интерфейса (пользовательского интерфейса) для коротких или связанных частей информации.</span><span class="sxs-lookup"><span data-stu-id="8e286-105">A *card* is a user-interface (UI) container for short or related pieces of information.</span></span> <span data-ttu-id="8e286-106">Карты могут иметь несколько свойств и вложений.</span><span class="sxs-lookup"><span data-stu-id="8e286-106">Cards can have multiple properties and attachments.</span></span> <span data-ttu-id="8e286-107">Карты могут включать кнопки, которые могут вызывать [действия карты.](~/task-modules-and-cards/cards/cards-actions.md)</span><span class="sxs-lookup"><span data-stu-id="8e286-107">Cards can include buttons which can trigger [Card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

## <a name="adaptive-cards"></a><span data-ttu-id="8e286-108">Адаптивные карты</span><span class="sxs-lookup"><span data-stu-id="8e286-108">Adaptive cards</span></span>

<span data-ttu-id="8e286-109">[Адаптивные карты](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card) — это новая спецификация кросс-продукта для карт в продуктах Майкрософт, включая Bots, Cortana, Outlook и Windows.</span><span class="sxs-lookup"><span data-stu-id="8e286-109">[Adaptive cards](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card) are a new cross product specification for cards in Microsoft products including Bots, Cortana, Outlook, and Windows.</span></span> <span data-ttu-id="8e286-110">Это рекомендуемый тип карты для Teams разработки.</span><span class="sxs-lookup"><span data-stu-id="8e286-110">They are the recommended card type for new Teams development.</span></span> <span data-ttu-id="8e286-111">Общие сведения из группы адаптивных карт см. в [обзоре адаптивных карт.](/adaptive-cards)</span><span class="sxs-lookup"><span data-stu-id="8e286-111">For general information from the Adaptive cards team see [Adaptive Cards Overview](/adaptive-cards).</span></span> <span data-ttu-id="8e286-112">Адаптивные карты можно использовать везде, где можно использовать существующие карты Hero, карты Office365 и эскизы.</span><span class="sxs-lookup"><span data-stu-id="8e286-112">You can use adaptive cards anywhere you can use existing Hero cards, Office365 cards, and Thumbnail cards.</span></span>

<span data-ttu-id="8e286-113">Помимо адаптивных карт, Teams поддерживает два других типа карт:</span><span class="sxs-lookup"><span data-stu-id="8e286-113">In addition to Adaptive Cards, Teams supports two other types of cards:</span></span>

* <span data-ttu-id="8e286-114">Соединитетельные карты, используемые в Office 365 соединители.</span><span class="sxs-lookup"><span data-stu-id="8e286-114">Connector Cards, used as part of Office 365 connectors.</span></span>
* <span data-ttu-id="8e286-115">Простые карты из базы ботов, такие как эскизы и карточки героев.</span><span class="sxs-lookup"><span data-stu-id="8e286-115">Simple cards from the bot framework, such as the thumbnail and hero cards.</span></span>

<span data-ttu-id="8e286-116">Эти типы карт более подробно описаны в [справочной Teams карточки.](~/task-modules-and-cards/cards/cards-reference.md)</span><span class="sxs-lookup"><span data-stu-id="8e286-116">These card types are described more fully in the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md).</span></span>

<span data-ttu-id="8e286-117">Teams использует карты в трех разных местах:</span><span class="sxs-lookup"><span data-stu-id="8e286-117">Teams uses cards in three different places:</span></span>

* <span data-ttu-id="8e286-118">Соединители</span><span class="sxs-lookup"><span data-stu-id="8e286-118">Connectors</span></span>
* <span data-ttu-id="8e286-119">боты;</span><span class="sxs-lookup"><span data-stu-id="8e286-119">Bots</span></span>
* <span data-ttu-id="8e286-120">расширения для обмена сообщениями;</span><span class="sxs-lookup"><span data-stu-id="8e286-120">Messaging extensions</span></span>

## <a name="adaptive-cards-and-incoming-webhooks"></a><span data-ttu-id="8e286-121">Адаптивные карты и входящие веб-окки</span><span class="sxs-lookup"><span data-stu-id="8e286-121">Adaptive cards and incoming webhooks</span></span>

> [!NOTE]
>
> <span data-ttu-id="8e286-122">✔ Все встроенные элементы схемы адаптивной карточки, кроме `Action.Submit`, полностью поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="8e286-122">✔ All native adaptive card schema elements, except `Action.Submit`, are fully supported.</span></span>
>
> <span data-ttu-id="8e286-123">✔ поддерживаемые действия [**Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html), [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html), [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html) [**иAction.Exeмило**](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#actionexecute).</span><span class="sxs-lookup"><span data-stu-id="8e286-123">✔ The supported actions are [**Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html), [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html), [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html) and [**Action.Execute**](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#actionexecute).</span></span>

## <a name="cards-in-connectors"></a><span data-ttu-id="8e286-124">Карты в соединители</span><span class="sxs-lookup"><span data-stu-id="8e286-124">Cards in Connectors</span></span>

<span data-ttu-id="8e286-125">Сначала карты определялись как часть Outlook Office 365 и используются в Office 365 соединители.</span><span class="sxs-lookup"><span data-stu-id="8e286-125">Cards were first defined as part of Outlook and Office 365, and are used as part of Office 365 Connectors.</span></span> <span data-ttu-id="8e286-126">Как и многие Office 365 приложения, Teams поддерживает соединители.</span><span class="sxs-lookup"><span data-stu-id="8e286-126">Like many Office 365 applications, Teams supports Connectors.</span></span> <span data-ttu-id="8e286-127">Дополнительные данные о соединителках можно узнать в [Office 365](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)соединители для Microsoft Teams, а также найти спецификацию для карт в соединители в справке карточки [actionable message card.](/outlook/actionable-messages/card-reference)</span><span class="sxs-lookup"><span data-stu-id="8e286-127">You can learn more about Connectors in [Office 365 Connectors for Microsoft Teams](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md), and find the specification for cards in connectors in [Actionable message card reference](/outlook/actionable-messages/card-reference).</span></span>

## <a name="cards-in-bots"></a><span data-ttu-id="8e286-128">Карты в ботах</span><span class="sxs-lookup"><span data-stu-id="8e286-128">Cards in Bots</span></span>

<span data-ttu-id="8e286-129">В Microsoft Bot Framework расширена спецификация карт, добавив набор предопределяемых карт, которые боты могут использовать в качестве части бот-сообщений.</span><span class="sxs-lookup"><span data-stu-id="8e286-129">The Microsoft Bot Framework extended the cards specification by adding a set of predefined cards that bots could use as part of bot messages.</span></span> <span data-ttu-id="8e286-130">Teams поддерживает ботов с помощью Bot Framework, но поддерживает несколько другой набор этих карт.</span><span class="sxs-lookup"><span data-stu-id="8e286-130">Teams supports bots using the Bot Framework but it supports a slightly different set of these cards.</span></span> <span data-ttu-id="8e286-131">Общие сведения о картах в Bot Framework можно найти в [приложении Add rich card attachments to messages.](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)</span><span class="sxs-lookup"><span data-stu-id="8e286-131">General information on cards in Bot Framework can be found in [Add rich card attachments to messages](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards).</span></span> <span data-ttu-id="8e286-132">Эти карты называются *простыми картами* в Teams.</span><span class="sxs-lookup"><span data-stu-id="8e286-132">These cards are called *simple cards* in Teams.</span></span>

<span data-ttu-id="8e286-133">Боты в Teams могут использовать любой тип карты: простой, соединительные или адаптивные.</span><span class="sxs-lookup"><span data-stu-id="8e286-133">Bots in Teams can use any type of card: simple, connector or adaptive.</span></span> <span data-ttu-id="8e286-134">Карты, поддерживаемые ботами в Teams, подробно описаны в Teams справки по [карточкам.](~/task-modules-and-cards/cards/cards-reference.md)</span><span class="sxs-lookup"><span data-stu-id="8e286-134">Cards that are supported by bots in Teams are detailed in [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md).</span></span>  

## <a name="cards-in-messaging-extensions"></a><span data-ttu-id="8e286-135">Карты в расширениях обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="8e286-135">Cards in Messaging Extensions</span></span>

<span data-ttu-id="8e286-136">[Расширения обмена сообщениями также](~/messaging-extensions/what-are-messaging-extensions.md) могут возвращать карточку.</span><span class="sxs-lookup"><span data-stu-id="8e286-136">[Messaging Extensions](~/messaging-extensions/what-are-messaging-extensions.md) can also return a card.</span></span> <span data-ttu-id="8e286-137">Расширения обмена сообщениями могут использовать любые типы карт: простые, соединительные или адаптивные.</span><span class="sxs-lookup"><span data-stu-id="8e286-137">Messaging extensions can use any type of card: simple, connector or adaptive.</span></span> <span data-ttu-id="8e286-138">Эти карты находятся в [справочной Teams карточки](~/task-modules-and-cards/cards/cards-reference.md).</span><span class="sxs-lookup"><span data-stu-id="8e286-138">These cards are found in the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md).</span></span>

## <a name="card-reference"></a><span data-ttu-id="8e286-139">Ссылка на карточку</span><span class="sxs-lookup"><span data-stu-id="8e286-139">Card reference</span></span>

<span data-ttu-id="8e286-140">Все карты, используемые Teams, перечислены в справочнике [Teams карточки.](~/task-modules-and-cards/cards/cards-reference.md)</span><span class="sxs-lookup"><span data-stu-id="8e286-140">All cards used by Teams are listed in the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md).</span></span> <span data-ttu-id="8e286-141">В этой ссылке также описываются различия между картами Bot Framework и картами в Teams.</span><span class="sxs-lookup"><span data-stu-id="8e286-141">This reference also describes differences between Bot Framework cards and cards in Teams.</span></span>
