---
title: Работа с универсальными действиями для адаптивных карт
description: Работа с универсальными действиями для адаптивных карт.
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 8c260a4893d38ad365cbb3bdd5a7613a1b42654f
ms.sourcegitcommit: 1256639fa424e3833b44207ce847a245824d48e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/29/2021
ms.locfileid: "52088872"
---
# <a name="work-with-universal-actions-for-adaptive-cards"></a>Работа с универсальными действиями для адаптивных карт

Универсальные действия для адаптивных карт предоставляют способ реализации сценариев, основанных на адаптивной карте, как для Teams, так и для Outlook. В этом документе описывается следующее:

* [Схема, используемая для универсальных действий для адаптивных карт](#schema-for-universal-actions-for-adaptive-cards)
* [Модель обновления](#refresh-model)
* [`adaptiveCard/action` вызов активности](#adaptivecardaction-invoke-activity)
* [Обратная совместимость](#backward-compatibility)

## <a name="quick-start-guide-to-leverage-universal-actions-for-adaptive-cards-in-teams"></a>Руководство по быстрому началу использования универсальных действий для адаптивных карт в Teams

1. Замените все `Action.Submit` экземпляры, `Action.Execute` чтобы обновить существующий сценарий в Teams.
2. Добавьте пункт в адаптивную карту, если вы хотите использовать модель автоматического обновления или если для сценария `refresh` требуются пользовательские представления.

    >[!NOTE]
    > Укажите `userIds` свойство для определения, какие пользователи получают автоматические обновления.

3. Обработка `adaptiveCard/action` запросов вызова в боте.
4. Используйте контекст запроса на вызов, чтобы ответить на них картами, специально созданными для пользователя.

    > [!NOTE]
    > Всякий раз, когда бот возвращает новую карту в результате обработки, ответ должен `Action.Execute` соответствовать формату ответа.

## <a name="schema-for-universal-actions-for-adaptive-cards"></a>Схема универсальных действий для адаптивных карт

Универсальные действия для адаптивных карт представлены в схеме адаптивных карт версии 1.4. Для эффективного использования адаптивной карты необходимо установить свойство адаптивной карты `version` 1.4.

> [!NOTE]
> Настройка свойства 1.4 делает адаптивную карту несовместимой со старыми клиентами платформ или приложений, таких как Outlook и Teams, так как они не поддерживают универсальные действия для адаптивных `version` карт.

Если вы установите версию карты меньше 1.4 и используете свойство или оба свойства, и `refresh` `Action.Execute` произойдет следующее:

| Client | Поведение |
| :-- | :-- |
| Teams | Карта перестает работать. Карта не обновляется и не отрисовка в зависимости от версии Teams `Action.Execute` клиента. Чтобы обеспечить максимальную совместимость Teams, `Action.Execute` определите с `Action.Submit` свойством отката. |

Дополнительные сведения о поддержке старых клиентов см. в обратной [совместимости.](#backward-compatibility)

### <a name="actionexecute"></a>Action.Exeмило

При авторе адаптивных карт замените `Action.Submit` и `Action.Http` с помощью `Action.Execute` . Схема похожа на схему `Action.Execute` `Action.Submit` .

Дополнительные сведения см. [вAction.Exeсхеме и свойствах.](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#actionexecute)

Теперь модель обновления позволяет автоматически обновлять адаптивные карты.

## <a name="refresh-model"></a>Модель обновления

Чтобы автоматически обновить адаптивную карту, определите ее свойство, в которое встраиваться действие `refresh` типа `Action.Execute` и `userIds` массива.

Дополнительные сведения см. в [обновленной схеме и свойствах.](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#refresh-mechanism)

## <a name="user-ids-in-refresh"></a>Пользовательские ID в обновлении

Ниже представлены функции UserIds в обновлении:

* UserIds — это массив МРТ пользователя, который входит в свойство `refresh` адаптивных карт.

* Если свойство списка указывается как в разделе обновления карты, карта не обновляется `userIds` `userIds: []` автоматически. Вместо этого  пользователю в меню тройной точки в интернете или на рабочем столе отображается параметр "Карточка обновления", а в меню контекста длинного пресса в мобильном телефоне, то есть Android или iOS, чтобы вручную обновить карту.

* Свойство UserIds добавляется, так как каналы в Teams могут включать большое количество участников. Если все участники одновременно просматривают канал, безусловное автоматическое обновление приводит к много одновечерным вызовам бота. Чтобы избежать этого, свойство всегда должно быть включено, чтобы определить, какие пользователи должны получать автоматическое обновление с максимальным `userIds` *количеством 60 (шестидесяти) пользовательских МРИС.*

* Дополнительные сведения о том, как можно Teams пользовательские МРИ участника беседы, чтобы добавить в список userIds в разделе обновление адаптивной карты, см. в статье Fetch [roster or user profile.](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile)

* Пример Teams МРТ пользователя`29:1bSnHZ7Js2STWrgk6ScEErLk1Lp2zQuD5H2qQ960rtvstKp8tKLl-3r8b6DoW0QxZimuTxk_kupZ1DBMpvIQQUAZL-PNj0EORDvRZXy8kvWk`

> [!NOTE]
> Свойство игнорируется в Outlook, и свойство всегда `userIds` `refresh` автоматически активируется. Проблема масштабирования в Outlook, так как пользователи просматривают карту в разное время.

Следующий шаг — использование действия вызова, чтобы понять, какой запрос должен быть выполнен после `adaptiveCard/action` `Action.Execute` выполнения.

## <a name="adaptivecardaction-invoke-activity"></a>`adaptiveCard/action` вызов активности

При выполнении в клиенте для бота выполняется новый тип действия `Action.Execute` `adaptiveCard/action` Invoke.

Дополнительные сведения см. в примере формата запросов и свойств типичной активности [ `adaptiveCard/action` вызова.](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#request-format)

Дополнительные сведения см. в примере формата отклика и свойств типичной активности вызова с [ `adaptiveCard/action` поддерживаемых типов откликов.](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#response-format)

Далее можно применить обратную совместимость к старым клиентам на разных платформах и сделать адаптивную карту совместимой.

## <a name="backward-compatibility"></a>Обратная совместимость

Универсальные действия для адаптивных карт позволяют устанавливать свойства, которые позволяют обратной совместимости со старыми версиями Outlook и Teams.

### <a name="teams"></a>Teams

Чтобы обеспечить обратную совместимость адаптивных карт с более старыми версиями Teams, необходимо включить свойство и установить `fallback` его значение `Action.Submit` . Кроме того, код бота должен обрабатывать и `Action.Execute` `Action.Submit` .

Дополнительные сведения см. в [Teams.](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#teams)

## <a name="see-also"></a>См. также

* [Действия адаптивной карты в Teams](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)
* [Как работают боты](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)