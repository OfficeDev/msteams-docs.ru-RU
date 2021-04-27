---
title: Введение карт
description: Описание карт и их использования в ботах, соединителах и расширениях обмена сообщениями
localization_priority: Normal
ms.topic: conceptual
keywords: соединители боты-карты обмена сообщениями
ms.openlocfilehash: acf5dc95b742a433c092be9e293d589b5919bb4d
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020270"
---
# <a name="cards"></a>Карточки

Карта *—* это контейнер пользовательского интерфейса (пользовательского интерфейса) для коротких или связанных частей информации. Карты могут иметь несколько свойств и вложений. Карты могут включать кнопки, которые могут вызывать [действия карты.](~/task-modules-and-cards/cards/cards-actions.md)

## <a name="adaptive-cards"></a>Адаптивные карты

[Адаптивные карты](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card) — это новая спецификация кросс-продукта для карт в продуктах Майкрософт, включая Bots, Cortana, Outlook и Windows. Это рекомендуемый тип карты для разработки новых команд. Общие сведения из группы адаптивных карт см. в [обзоре адаптивных карт.](/adaptive-cards) Адаптивные карты можно использовать везде, где можно использовать существующие карты Hero, карты Office365 и эскизы.

В дополнение к адаптивным картам Teams поддерживает два других типа карт:

* Соединитетельные карты, используемые в составе соединители Office 365.
* Простые карты из базы ботов, такие как эскизы и карточки героев.

Эти типы карт более подробно описаны в [справочной карточке Teams.](~/task-modules-and-cards/cards/cards-reference.md)

Teams использует карты в трех разных местах:

* Соединители
* боты;
* расширения для обмена сообщениями;

## <a name="adaptive-cards-and-incoming-webhooks"></a>Адаптивные карты и входящие веб-окки

> [!NOTE]
>
> ✔ Все встроенные элементы схемы адаптивной карточки, кроме `Action.Submit`, полностью поддерживаются.
>
> ✔ поддерживаемые действия [**Action.OpenURL,**](https://adaptivecards.io/explorer/Action.OpenUrl.html) [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html)и [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html).

## <a name="cards-in-connectors"></a>Карты в соединители

Сначала карты были определены как часть Outlook и Office 365 и используются в составе соединители Office 365. Как и многие приложения Office 365, Teams поддерживает соединители. Дополнительные данные о соединителках [в Office 365 соединители](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)для Microsoft Teams, а также спецификации для карт в соединителках в справочной карточке [actionable message.](/outlook/actionable-messages/card-reference)

## <a name="cards-in-bots"></a>Карты в ботах

Microsoft Bot Framework расширила спецификацию карт, добавив набор предопределяемых карт, которые боты могли использовать в качестве части бот-сообщений. Teams поддерживает ботов с помощью Bot Framework, но поддерживает несколько другой набор этих карт. Общие сведения о картах в Bot Framework можно найти в [приложении Add rich card attachments to messages.](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards) Эти карты в Teams *называются простыми* картами.

Боты в Teams могут использовать любой тип карты: простой, соединительные или адаптивные. Карты, поддерживаемые ботами в Teams, подробно описаны в [справке по картам Teams.](~/task-modules-and-cards/cards/cards-reference.md)  

## <a name="cards-in-messaging-extensions"></a>Карты в расширениях обмена сообщениями

[Расширения обмена сообщениями также](~/messaging-extensions/what-are-messaging-extensions.md) могут возвращать карточку. Расширения обмена сообщениями могут использовать любые типы карт: простые, соединительные или адаптивные. Эти карточки находятся в [справке по карточкам Teams.](~/task-modules-and-cards/cards/cards-reference.md)

## <a name="card-reference"></a>Ссылка на карточку

Все карты, используемые Teams, перечислены в [справочной карточке Teams.](~/task-modules-and-cards/cards/cards-reference.md) В этой ссылке также описываются различия между картами Bot Framework и картами в Teams.
