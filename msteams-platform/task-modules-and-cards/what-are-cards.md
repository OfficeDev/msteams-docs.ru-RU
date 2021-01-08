---
title: Знакомство с карточками
description: Описывает карточки и их использования в ботах, соединителах и расширениях обмена сообщениями
keywords: соединители боты карточки обмена сообщениями
ms.openlocfilehash: 00c649a1339f05b782e03a2c0db5cba2445f66bc
ms.sourcegitcommit: 23ceb25d07a76f03ffe92cf1ac578b7c50b0bafc
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/07/2021
ms.locfileid: "49777926"
---
# <a name="cards"></a>Карточки

*Карточка* — это контейнер пользовательского интерфейса для коротких или связанных сведений. Карточки могут иметь несколько свойств и вложений. Карточки могут включать кнопки, которые могут [запускать действия карточки.](~/task-modules-and-cards/cards/cards-actions.md)

## <a name="adaptive-cards"></a>Адаптивные карточки

[Адаптивные карточки](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card) — это новая спецификация для разных продуктов в продуктах Майкрософт, включая ботов, Кортану, Outlook и Windows. Это рекомендуемый тип карточки для новой разработки Teams. Общие сведения о группе адаптивных карточек см. в [обзоре адаптивных карточек.](/adaptive-cards) Вы можете использовать адаптивные карточки в любом месте, где можно использовать существующие карточки Hero, Office365 и Thumbnail.

Помимо адаптивных карточек, Teams поддерживает два других типа карточек:

* Карточки соединители, используемые в составе соединитеев Office 365.
* Простые карточки из структуры бота, такие как эскиз и карточки главного пальца.

Эти типы карт более подробно описаны в справочнике [по карточкам Teams.](~/task-modules-and-cards/cards/cards-reference.md)

Teams использует карточки в трех разных местах:

* Соединители
* боты;
* расширения для обмена сообщениями;

## <a name="adaptive-cards-and-incoming-webhooks"></a>Адаптивные карточки и входящие веб-hooks

> [!NOTE]
>
> ✔ Все встроенные элементы схемы адаптивной карточки, кроме `Action.Submit`, полностью поддерживаются.
>
> ✔ поддерживаемые [**действия: Action.OpenURL,**](https://adaptivecards.io/explorer/Action.OpenUrl.html) [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html)и [**Action.ToggleVisibility.**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html)

## <a name="cards-in-connectors"></a>Карточки в соединители

Карточки сначала были определены как часть Outlook и Office 365 и используются как часть соединители Office 365. Как и многие приложения Office 365, Teams поддерживает соединители. Вы можете узнать больше о соединителках в соединителках [Office 365](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)для Microsoft Teams и найти спецификацию карточек в соединителках в справочнике по карточкам сообщений с [действиями.](/outlook/actionable-messages/card-reference)

## <a name="cards-in-bots"></a>Карточки в ботах

Microsoft Bot Framework расширила спецификацию карточек, добавив набор предопределельных карточек, которые боты могут использовать в сообщениях ботов. Teams поддерживает ботов с помощью Bot Framework, но поддерживает несколько другой набор этих карточек. Общие сведения о карточках в Bot Framework можно найти в файле "Добавление вложений в виде [информативных карточек в сообщения".](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards) В Teams такие карточки *называются простыми* карточками.

Боты в Teams могут использовать любые типы карт: простые, соединительные или адаптивные. Карточки, поддерживаемые ботами в Teams, подробно описаны в справочнике по [карточкам Teams.](~/task-modules-and-cards/cards/cards-reference.md)  

## <a name="cards-in-messaging-extensions"></a>Карточки в расширениях обмена сообщениями

[Расширения обмена сообщениями также](~/messaging-extensions/what-are-messaging-extensions.md) могут возвращать карточку. Расширения обмена сообщениями могут использовать любые типы карт: простые, соединительные или адаптивные. Эти карточки находятся в справочнике [по карточкам Teams.](~/task-modules-and-cards/cards/cards-reference.md)

## <a name="card-reference"></a>Справочник по карточкам

Все карты, используемые Teams, перечислены в справочнике [по карточкам Teams.](~/task-modules-and-cards/cards/cards-reference.md) В этом справочнике также описываются различия между карточками Bot Framework и карточками в Teams.
