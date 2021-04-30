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
# <a name="cards"></a>Карточки

Карта *—* это контейнер пользовательского интерфейса (пользовательского интерфейса) для коротких или связанных частей информации. Карты могут иметь несколько свойств и вложений. Карты могут включать кнопки, которые могут вызывать [действия карты.](~/task-modules-and-cards/cards/cards-actions.md)

## <a name="adaptive-cards"></a>Адаптивные карты

[Адаптивные карты](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card) — это новая спецификация кросс-продукта для карт в продуктах Майкрософт, включая Bots, Cortana, Outlook и Windows. Это рекомендуемый тип карты для Teams разработки. Общие сведения из группы адаптивных карт см. в [обзоре адаптивных карт.](/adaptive-cards) Адаптивные карты можно использовать везде, где можно использовать существующие карты Hero, карты Office365 и эскизы.

Помимо адаптивных карт, Teams поддерживает два других типа карт:

* Соединитетельные карты, используемые в Office 365 соединители.
* Простые карты из базы ботов, такие как эскизы и карточки героев.

Эти типы карт более подробно описаны в [справочной Teams карточки.](~/task-modules-and-cards/cards/cards-reference.md)

Teams использует карты в трех разных местах:

* Соединители
* боты;
* расширения для обмена сообщениями;

## <a name="adaptive-cards-and-incoming-webhooks"></a>Адаптивные карты и входящие веб-окки

> [!NOTE]
>
> ✔ Все встроенные элементы схемы адаптивной карточки, кроме `Action.Submit`, полностью поддерживаются.
>
> ✔ поддерживаемые действия [**Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html), [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html), [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html) [**иAction.Exeмило**](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#actionexecute).

## <a name="cards-in-connectors"></a>Карты в соединители

Сначала карты определялись как часть Outlook Office 365 и используются в Office 365 соединители. Как и многие Office 365 приложения, Teams поддерживает соединители. Дополнительные данные о соединителках можно узнать в [Office 365](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)соединители для Microsoft Teams, а также найти спецификацию для карт в соединители в справке карточки [actionable message card.](/outlook/actionable-messages/card-reference)

## <a name="cards-in-bots"></a>Карты в ботах

В Microsoft Bot Framework расширена спецификация карт, добавив набор предопределяемых карт, которые боты могут использовать в качестве части бот-сообщений. Teams поддерживает ботов с помощью Bot Framework, но поддерживает несколько другой набор этих карт. Общие сведения о картах в Bot Framework можно найти в [приложении Add rich card attachments to messages.](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards) Эти карты называются *простыми картами* в Teams.

Боты в Teams могут использовать любой тип карты: простой, соединительные или адаптивные. Карты, поддерживаемые ботами в Teams, подробно описаны в Teams справки по [карточкам.](~/task-modules-and-cards/cards/cards-reference.md)  

## <a name="cards-in-messaging-extensions"></a>Карты в расширениях обмена сообщениями

[Расширения обмена сообщениями также](~/messaging-extensions/what-are-messaging-extensions.md) могут возвращать карточку. Расширения обмена сообщениями могут использовать любые типы карт: простые, соединительные или адаптивные. Эти карты находятся в [справочной Teams карточки](~/task-modules-and-cards/cards/cards-reference.md).

## <a name="card-reference"></a>Ссылка на карточку

Все карты, используемые Teams, перечислены в справочнике [Teams карточки.](~/task-modules-and-cards/cards/cards-reference.md) В этой ссылке также описываются различия между картами Bot Framework и картами в Teams.
