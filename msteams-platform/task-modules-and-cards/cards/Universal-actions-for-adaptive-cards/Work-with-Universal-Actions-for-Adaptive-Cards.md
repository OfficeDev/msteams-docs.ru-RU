---
title: Работа с универсальными действиями для адаптивных карточек
description: Работа с универсальными действиями для адаптивных карточек.
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 4361f1c7774837b728c6382df4e62e00ea912e35
ms.sourcegitcommit: 999f5c607671e088ea8a461fa7dbb63f8d61c39b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/25/2021
ms.locfileid: "52649701"
---
# <a name="work-with-universal-actions-for-adaptive-cards"></a>Работа с универсальными действиями для адаптивных карточек

Универсальные действия для адаптивных карточек предоставляют способ реализации сценариев на основе адаптивных карточек как для Teams, так и для Outlook. В этом документе представлены следующие сведения:

* [Схема, используемая для универсальных действий для адаптивных карточек](#schema-for-universal-actions-for-adaptive-cards)
* [Модель обновления](#refresh-model)
* [`adaptiveCard/action` запуск действия](#adaptivecardaction-invoke-activity)
* [Обратная совместимость](#backward-compatibility)

## <a name="quick-start-guide-to-leverage-universal-actions-for-adaptive-cards-in-teams"></a>Краткое руководство по использованию универсальных действий для адаптивных карточек в Teams

1. Замените все экземпляры `Action.Submit` на `Action.Execute`, чтобы обновить существующий сценарий в Teams.
2. Добавьте предложение `refresh` в адаптивную карточку, если хотите использовать автоматическую модель обновления или если для вашего сценария требуются представления, определенные пользователем.

    >[!NOTE]
    > Укажите свойство `userIds`, чтобы определить, какие пользователи получают автоматические обновления.

3. Обрабатывайте запросы на запуск `adaptiveCard/action` в своем боте.
4. Используйте контекст запроса на запуск, чтобы ответить с помощью карточек, созданных специально для пользователя.

    > [!NOTE]
    > Каждый раз, когда бот возвращает новую карточку в результате обработки `Action.Execute`, отклик должен соответствовать формату отклика.

## <a name="schema-for-universal-actions-for-adaptive-cards"></a>Схема для универсальных действий для адаптивных карточек

Универсальные действия для адаптивных карточек представлены в схеме адаптивных карточек версии 1.4. Для эффективного использования адаптивной карточки свойство `version` адаптивной карточки должно быть установлено на 1.4.

> [!NOTE]
> При установке свойства `version` на 1.4 адаптивная карточка становится несовместима с более старыми клиентами платформ или приложений, например с Outlook и Teams, так как они не поддерживают универсальные действия для адаптивных карточек.

Если установить версию карточки меньше 1.4 и использовать одно свойство или оба, `refresh` и `Action.Execute`, происходит следующее:

| Клиент | Поведение |
| :-- | :-- |
| Teams | Карточка перестает работать. Карточка не обновляется и `Action.Execute` не обрабатывается в зависимости от версии клиента Teams. Чтобы обеспечить максимальную совместимость в Teams, определите в свойстве отката `Action.Execute` с `Action.Submit`. |

Дополнительные сведения о поддержке клиентов более старых версий см. в разделе [обратная совместимость](#backward-compatibility).

### <a name="actionexecute"></a>Action.Execute

При разработке адаптивных карточек замените `Action.Submit` и `Action.Http` на `Action.Execute`. Схема для `Action.Execute` аналогична схеме `Action.Submit`.

Дополнительные сведения см. в разделе [Схема и свойства Action.Execute](/adaptive-cards/authoring-cards/universal-action-model#actionexecute).

Теперь вы можете использовать модель обновления, чтобы разрешить автоматическое обновление адаптивных карточек.

## <a name="refresh-model"></a>Модель обновления

Чтобы автоматически обновить адаптивную карточку, определите ее свойство `refresh`, которое внедряет действие типа `Action.Execute` и массив `userIds`.

Дополнительные сведения см. в разделе [схема и свойства обновления](/adaptive-cards/authoring-cards/universal-action-model#refresh-mechanism).

## <a name="user-ids-in-refresh"></a>Идентификаторы пользователей в процессе обновления

Ниже даны функции UserIds в процессе обновления.

* UserIds — это массив MRI пользователя, который является частью свойства `refresh` адаптивных карточек.

* Если свойство списка `userIds` указано как `userIds: []` в разделе обновления карточки, карточка не обновляется автоматически. Вместо этого пользователь видит параметр **Обновить карточку** в меню с тремя точками в классическом или веб-приложении и в контекстном меню при длительном нажатии на мобильном устройстве, то есть на Android или iOS, чтобы обновить карточку вручную.

* Добавлено свойство UserIds, так как каналы в Teams могут включать множество участников. Если все участники одновременно просматривают канал, безусловное автоматическое обновление приводит к множеству одновременных вызовов бота. Чтобы избежать этого, свойство `userIds` всегда должно быть включено, чтобы определять, какие пользователи должны получать автоматическое обновление при максимуме в *60 (шестьдесят) пользовательских MRI*.

* Дополнительные сведения о том, как получить MRI пользователей, участвующих в беседе Teams, для добавления в список userIds в разделе обновления адаптивной карточки, см. в разделе [получить профиль списка участников или пользователя](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile).

* Пример MRI пользователя Teams: `29:1bSnHZ7Js2STWrgk6ScEErLk1Lp2zQuD5H2qQ960rtvstKp8tKLl-3r8b6DoW0QxZimuTxk_kupZ1DBMpvIQQUAZL-PNj0EORDvRZXy8kvWk`

> [!NOTE]
> Свойство `userIds` игнорируется в Outlook, а свойство `refresh` всегда активируется автоматически. Для Outlook проблемы масштабирования не существует, так как пользователи просматривают карточку в разное время.

Следующий шаг — использование запуска действия `adaptiveCard/action`, чтобы понять, какой должен быть сделан запрос после выполнения `Action.Execute`.

## <a name="adaptivecardaction-invoke-activity"></a>`adaptiveCard/action` запуск действия

Когда в клиенте выполняется `Action.Execute`, для вашего бота создается новый тип запуска действия `adaptiveCard/action`.

Дополнительные сведения см. в разделе: [формат запроса и свойства обычного `adaptiveCard/action` запуска действия](/adaptive-cards/authoring-cards/universal-action-model#request-format).

Дополнительные сведения см. в разделе: [формат отклика и свойства обычного `adaptiveCard/action` запуска действия с поддерживаемыми типами отклика](/adaptive-cards/authoring-cards/universal-action-model#response-format).

Затем к старым клиентам на разных платформах можно применить обратную совместимость и сделать адаптивную карточку совместимой.

## <a name="backward-compatibility"></a>Обратная совместимость

Универсальные действия для адаптивных карточек позволяют задать свойства, которые обеспечивают обратную совместимость с более старыми версиями Outlook и Teams.

### <a name="teams"></a>Teams

Чтобы обеспечить обратную совместимость адаптивных карточек с более старыми версиями Teams, необходимо включить свойство `fallback` и установить для него значение `Action.Submit`. Кроме того, код бота должен обрабатывать как `Action.Execute`, так и `Action.Submit`.

Дополнительные сведения см. в разделе [обратная совместимость в Teams](/adaptive-cards/authoring-cards/universal-action-model#teams).

## <a name="code-sample"></a>Пример кода

|Название примера | Описание | .NETCore |
|----------------|-----------------|--------------|
| Бот организации питания Teams | Создайте простого бота, который принимает заказы на обед с помощью адаптивных карточек. |[Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-teams-catering/csharp)|

## <a name="see-also"></a>Дополнительные ресурсы

* [Действия адаптивной карточки в Teams](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)
* [Как работают боты](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)
