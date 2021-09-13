---
title: Карточки
description: Описание карт и их использования в ботах, соединители и расширениях обмена сообщениями
ms.localizationpriority: medium
keywords: соединители боты-карты обмена сообщениями
ms.topic: overview
ms.openlocfilehash: 345e37a9af00c2f3300cc76f4b44b83cc47d0392
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/12/2021
ms.locfileid: "59157579"
---
# <a name="cards"></a>Карточки

Карта — это контейнер пользовательского интерфейса (пользовательского интерфейса) для коротких или связанных частей информации. Карты могут иметь несколько свойств и вложений и могут включать кнопки, которые запускают [действия карт.](~/task-modules-and-cards/cards/cards-actions.md) С помощью карт можно организовать информацию в группы и предоставить пользователям возможность взаимодействовать с определенными частями информации.

Боты для Teams поддерживают следующие типы карт: адаптивная карта, карта героя, карта списка, Office 365 соединительные карты, карточка получения, карточка подписи, эскизная карта и коллекции карт. В зависимости от типа карты можно добавить в карты форматирование текста с помощью Markdown или HTML. Карты, используемые ботами и расширениями обмена сообщениями в Microsoft Teams, добавляют и реагируют на действия этих карт, `openUrl` , , , и `messageBack` `imBack` `invoke` `signin` .

Teams использует карты в трех разных местах:

* Connectors
* боты;
* расширения для обмена сообщениями;

## <a name="cards-in-connectors"></a>Карты в соединители

Сначала карты определялись как часть Outlook Office 365 и теперь используются в Office 365 соединители. Как и Office 365 приложений, Teams поддерживает соединители. Дополнительные сведения см. [в Office 365 соединители для Teams.](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) Спецификацию для карт в соединителках можно найти в справке к карточкам [сообщений.](/outlook/actionable-messages/card-reference)

## <a name="cards-in-bots"></a>Карты в ботах

В Microsoft Bot Framework расширяется спецификация карт, добавляя набор предопределяемых карт, которые боты могут использовать в качестве части бот-сообщений. Teams поддерживает ботов с помощью Bot Framework, но поддерживает другой набор этих карт. Общие сведения о картах в Bot Framework можно найти в добавлении вложения с богатыми [картами в сообщения.](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards) Эти карты в Teams.

Боты в Teams могут использовать простые карты, соединительные карты или адаптивные карты. [Типы карт предоставляют](~/task-modules-and-cards/cards/cards-reference.md) сведения о картах, поддерживаемых ботами в Teams.

## <a name="cards-in-messaging-extensions"></a>Карты в расширениях обмена сообщениями

[Расширения обмена сообщениями также](~/messaging-extensions/what-are-messaging-extensions.md) могут возвращать карточку. Расширения обмена сообщениями могут использовать простые карты, соединительные карты или адаптивные карты. Эти карты находятся в [типах карт.](~/task-modules-and-cards/cards/cards-reference.md)

## <a name="types-of-cards"></a>Типы карточек

Все карты, используемые Teams, перечислены в [типах карт.](~/task-modules-and-cards/cards/cards-reference.md) В этой ссылке также описываются различия между картами Bot Framework и картами в Teams.

## <a name="adaptive-cards"></a>Адаптивные карточки

> [!VIDEO https://www.youtube-nocookie.com/embed/J12lKt717Ws]

[Адаптивные карты](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card) — это новая спецификация кросс-продукта для карт в продуктах Майкрософт, включая ботов, Кортана, Outlook и Windows. Это рекомендуемый тип карты для Teams разработки. Общие сведения из группы адаптивных карт см. в [обзоре Адаптивные карты.](/adaptive-cards) Адаптивные карты можно использовать везде, где вы используете существующие карты героев, Office 365 и эскизные карты.

Помимо адаптивных карт, Teams поддерживает два других типа карт:

* Соединитетельные карточки. Используется в Office 365 соединители.
* Простые карты. Используется из bot Framework, например эскизы и карточки героев.

### <a name="adaptive-cards-and-incoming-webhooks"></a>Адаптивные карты и входящие веб-окки

> [!VIDEO https://www.youtube-nocookie.com/embed/y5pbJI43Zvg]

> [!NOTE]
> * Все элементы схемы адаптивной карты, за `Action.Submit` исключением, полностью поддерживаются.
> * Поддерживаемые действия [**Action.OpenURL,**](https://adaptivecards.io/explorer/Action.OpenUrl.html) [**Action.ShowCard,**](https://adaptivecards.io/explorer/Action.ShowCard.html) [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html)иAction.Exe [**мило**](/adaptive-cards/authoring-cards/universal-action-model#actionexecute).

Адаптивные карты с входящие веб-окки позволяют использовать богатые и гибкие возможности адаптивных карт. Он отправляет данные с помощью входящих веб-Teams из веб-службы.

## <a name="see-also"></a>См. также

* [Формат карты в Teams](~/task-modules-and-cards/cards/cards-format.md)
* [Дизайн адаптивных карт](~/task-modules-and-cards/cards/design-effective-cards.md)

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Типы карточек](~/task-modules-and-cards/cards/cards-reference.md)