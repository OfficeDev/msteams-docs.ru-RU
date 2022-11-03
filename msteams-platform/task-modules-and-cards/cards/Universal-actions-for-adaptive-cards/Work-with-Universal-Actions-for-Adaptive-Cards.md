---
title: Работа с универсальными действиями для адаптивных карточек
description: Узнайте, как работать с универсальными действиями для адаптивных карточек, включая схему для универсальных действий для адаптивных карточек, модель обновления и обратную совместимость.
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: d723b565cadfacc550cd4fd9c8648149e9d164e2
ms.sourcegitcommit: c3601696cced9aadc764f1e734646ee7711f154c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/03/2022
ms.locfileid: "68833011"
---
# <a name="work-with-universal-actions-for-adaptive-cards"></a>Работа с универсальными действиями для адаптивных карточек

Universal Actions for Adaptive Cards provide a way to implement Adaptive Card based scenarios for both, Teams and Outlook. This document covers the following topics:

* [Схема, используемая для универсальных действий для адаптивных карточек](#schema-for-universal-actions-for-adaptive-cards)
* [Модель обновления](#refresh-model)
* [Действие вызова `adaptiveCard/action`](#adaptivecardaction-invoke-activity)
* [Обратная совместимость](#backward-compatibility)

## <a name="quick-start-guide-to-use-universal-actions-for-adaptive-cards-in-teams"></a>Краткое руководство по использованию универсальных действий для адаптивных карточек в Teams

1. Замените все экземпляры `Action.Submit` на `Action.Execute`, чтобы обновить существующий сценарий в Teams.
2. Добавьте предложение `refresh` в адаптивную карточку, если хотите использовать автоматическую модель обновления или если для вашего сценария требуются представления, определенные пользователем.

    >[!NOTE]
    > `userIds` Укажите свойство , чтобы определить, какие пользователи получают автоматические обновления.

3. Обрабатывайте запросы вызова `adaptiveCard/action` в своем боте.
4. Используйте контекст запроса вызова, чтобы ответить с помощью карточек, созданных для пользователя.

    > [!NOTE]
    > Каждый раз, когда бот возвращает новую карточку в результате обработки `Action.Execute`, отклик должен соответствовать формату отклика.

## <a name="schema-for-universal-actions-for-adaptive-cards"></a>Схема для универсальных действий для адаптивных карточек

Универсальные действия для адаптивных карточек представлены в схеме адаптивных карточек версии 1.4. Для эффективного использования адаптивной карточки свойство `version` адаптивной карточки должно быть установлено на 1.4.

> [!NOTE]
> При установке свойства `version` на 1.4 адаптивная карточка становится несовместима с более старыми клиентами платформ или приложений, например с Outlook и Teams, так как они не поддерживают универсальные действия для адаптивных карточек.

Если установить версию карточки меньше 1.4 и использовать одно свойство или оба, `refresh` и `Action.Execute`, происходит следующее:

| Клиент | Поведение |
| :-- | :-- |
| Teams | Карточка перестает работать. Карточка не обновляется и `Action.Execute` не отображается в зависимости от версии клиента Teams. Чтобы обеспечить максимальную совместимость в Teams, определите `Action.Execute` с `Action.Submit` в свойстве отката. |

Дополнительные сведения о поддержке клиентов более старых версий см. в разделе [обратная совместимость](#backward-compatibility).

### <a name="actionexecute"></a>Action.Execute

При разработке адаптивных карточек замените `Action.Submit` и `Action.Http` на `Action.Execute`. Схема для `Action.Execute` аналогична схеме `Action.Submit`.

Дополнительные сведения см. в разделе [Схема и свойства Action.Execute](/adaptive-cards/authoring-cards/universal-action-model#actionexecute).

Теперь вы можете использовать модель обновления, чтобы разрешить автоматическое обновление адаптивных карточек.

## <a name="refresh-model"></a>Модель обновления

Чтобы автоматически обновить адаптивную карточку, определите ее свойство `refresh`, которое внедряет действие типа `Action.Execute` и массив `userIds`.

Дополнительные сведения см. в разделе [схема и свойства обновления](/adaptive-cards/authoring-cards/universal-action-model#refresh-mechanism).

## <a name="user-ids-in-refresh"></a>Идентификаторы пользователей в процессе обновления

Ниже описаны особенности UserIds в процессе обновления.

* UserIds — это массив MRI пользователя, который является частью свойства `refresh` адаптивных карточек.

* `userIds` Если свойство списка указано как `userIds: []` в разделе обновления карточки, карточка не обновляется автоматически. Вместо этого параметр **Обновить карточку** отображается для пользователя в меню с тремя точками в веб-клиенте Teams или на рабочем столе, а также в контекстном меню с длинным нажатием на мобильных устройствах Teams, то есть Android или iOS, чтобы обновить карточку вручную. Кроме того, вы можете пропустить `userIds` свойство обновления в целом, если сценарий включает <=60 участников в групповых чатах или каналах Teams. Клиент Teams автоматически вызывает вызовы обновления для всех пользователей, если группа или канал имеет <=60 пользователей.

* Добавлено свойство UserIds, так как каналы в Teams могут включать множество участников. Если все участники одновременно просматривают канал, безусловное автоматическое обновление приводит к множеству одновременных вызовов бота. Свойство `userIds` всегда должно быть включено, чтобы определять, какие пользователи должны получать автоматическое обновление при максимуме в *60 (шестьдесят) пользовательских MRI*.

* You can fetch Teams conversation member's user MRIs. For more information on how to add in userIds list in refresh section of Adaptive Card, see [fetch roster or user profile](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile).

 Вы можете получить MRI пользователя для канала, группового чата или индивидуального чата, используя следующий пример.

 1. С помощью TurnContext  

     `userMRI= turnContext.Activity.From.Id`

 1. С помощью метода GetMemberAsync
  
     `var member = await TeamsInfo.GetMemberAsync(turnContext, turnContext.Activity.From.Id, cancellationToken);var userMRI = member.Id;`

* Пример MRI пользователя Teams: `29:1bSnHZ7Js2STWrgk6ScEErLk1Lp2zQuD5H2qQ960rtvstKp8tKLl-3r8b6DoW0QxZimuTxk_kupZ1DBMpvIQQUAZL-PNj0EORDvRZXy8kvWk`

> [!NOTE]
> Свойство `userIds` игнорируется в Outlook, а свойство `refresh` всегда активируется автоматически. Для Outlook проблемы масштабирования не существует, так как пользователи просматривают карточку в разное время.

Следующий шаг — использование запуска действия `adaptiveCard/action`, чтобы понять, какой должен быть сделан запрос после выполнения `Action.Execute`.

## <a name="adaptivecardaction-invoke-activity"></a>`adaptiveCard/action` запуск действия

Когда в клиенте выполняется `Action.Execute`, для вашего бота создается новый тип запуска действия `adaptiveCard/action`.

Дополнительные сведения см. в разделе: [формат запроса и свойства обычного действия вызова `adaptiveCard/action`](/adaptive-cards/authoring-cards/universal-action-model#request-format).

Дополнительные сведения см. в разделе: [формат отклика и свойства обычного действия вызова `adaptiveCard/action` с поддерживаемыми типами отклика](/adaptive-cards/authoring-cards/universal-action-model#response-format).

Затем к старым клиентам на разных платформах можно применить обратную совместимость и сделать адаптивную карточку совместимой.

## <a name="backward-compatibility"></a>Обратная совместимость

Универсальные действия для адаптивных карточек позволяют задать свойства, которые обеспечивают обратную совместимость с более старыми версиями Outlook и Teams.

### <a name="teams"></a>Teams

To ensure backward compatibility of your Adaptive Cards with older versions of Teams, you must include the `fallback` property and set its value to `Action.Submit`. Also, your bot code must process both `Action.Execute` and `Action.Submit`.

Дополнительные сведения см. в разделе [обратная совместимость в Teams](/adaptive-cards/authoring-cards/universal-action-model#teams).

## <a name="code-samples"></a>Примеры кода

|Название примера | Описание | .NETCore | Node.js |
|----------------|-----------------|--------------|--------------|
| Бот организации питания Teams | Создание бота, который принимает заказы на обед с помощью адаптивных карточек. |[Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-teams-catering/csharp)| Н/Д |
| Адаптивные карточки последовательных рабочих процессов | Демонстрация реализации последовательных рабочих процессов, пользовательских представлений и актуальных адаптивных карточек в ботах. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/csharp) | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/nodejs) |

## <a name="see-also"></a>Дополнительные ресурсы

* [Действия адаптивной карточки в Teams](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)
* [Как работают боты](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)
* [Последовательные рабочие процессы](~/task-modules-and-cards/cards/universal-actions-for-adaptive-cards/sequential-workflows.md)
* [Актуальные карточки](~/task-modules-and-cards/cards/universal-actions-for-adaptive-cards/up-to-date-views.md)
* [Отзывы о завершении формы](~/bots/how-to/conversations/conversation-messages.md#form-completion-feedback)
