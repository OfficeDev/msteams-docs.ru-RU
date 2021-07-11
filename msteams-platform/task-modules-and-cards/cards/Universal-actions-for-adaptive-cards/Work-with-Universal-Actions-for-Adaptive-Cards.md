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
# <a name="work-with-universal-actions-for-adaptive-cards"></a><span data-ttu-id="49fcc-103">Работа с универсальными действиями для адаптивных карточек</span><span class="sxs-lookup"><span data-stu-id="49fcc-103">Work with Universal Actions for Adaptive Cards</span></span>

<span data-ttu-id="49fcc-104">Универсальные действия для адаптивных карточек предоставляют способ реализации сценариев на основе адаптивных карточек как для Teams, так и для Outlook.</span><span class="sxs-lookup"><span data-stu-id="49fcc-104">Universal Actions for Adaptive Cards provides a way to implement Adaptive Card based scenarios for both, Teams and Outlook.</span></span> <span data-ttu-id="49fcc-105">В этом документе представлены следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="49fcc-105">This document covers the following:</span></span>

* [<span data-ttu-id="49fcc-106">Схема, используемая для универсальных действий для адаптивных карточек</span><span class="sxs-lookup"><span data-stu-id="49fcc-106">Schema used for Universal Actions for Adaptive Cards</span></span>](#schema-for-universal-actions-for-adaptive-cards)
* [<span data-ttu-id="49fcc-107">Модель обновления</span><span class="sxs-lookup"><span data-stu-id="49fcc-107">Refresh model</span></span>](#refresh-model)
* [<span data-ttu-id="49fcc-108">`adaptiveCard/action` запуск действия</span><span class="sxs-lookup"><span data-stu-id="49fcc-108">`adaptiveCard/action` invoke activity</span></span>](#adaptivecardaction-invoke-activity)
* [<span data-ttu-id="49fcc-109">Обратная совместимость</span><span class="sxs-lookup"><span data-stu-id="49fcc-109">Backward compatibility</span></span>](#backward-compatibility)

## <a name="quick-start-guide-to-leverage-universal-actions-for-adaptive-cards-in-teams"></a><span data-ttu-id="49fcc-110">Краткое руководство по использованию универсальных действий для адаптивных карточек в Teams</span><span class="sxs-lookup"><span data-stu-id="49fcc-110">Quick start guide to leverage Universal Actions for Adaptive Cards in Teams</span></span>

1. <span data-ttu-id="49fcc-111">Замените все экземпляры `Action.Submit` на `Action.Execute`, чтобы обновить существующий сценарий в Teams.</span><span class="sxs-lookup"><span data-stu-id="49fcc-111">Replace all instances of `Action.Submit` with `Action.Execute` to update an existing scenario on Teams.</span></span>
2. <span data-ttu-id="49fcc-112">Добавьте предложение `refresh` в адаптивную карточку, если хотите использовать автоматическую модель обновления или если для вашего сценария требуются представления, определенные пользователем.</span><span class="sxs-lookup"><span data-stu-id="49fcc-112">Add a `refresh` clause to your Adaptive Card, if you want to leverage the automatic refresh model or if your scenario requires User Specific Views.</span></span>

    >[!NOTE]
    > <span data-ttu-id="49fcc-113">Укажите свойство `userIds`, чтобы определить, какие пользователи получают автоматические обновления.</span><span class="sxs-lookup"><span data-stu-id="49fcc-113">Specify the `userIds` property to identify, which users get automatic updates.</span></span>

3. <span data-ttu-id="49fcc-114">Обрабатывайте запросы на запуск `adaptiveCard/action` в своем боте.</span><span class="sxs-lookup"><span data-stu-id="49fcc-114">Handle `adaptiveCard/action` invoke requests in your bot.</span></span>
4. <span data-ttu-id="49fcc-115">Используйте контекст запроса на запуск, чтобы ответить с помощью карточек, созданных специально для пользователя.</span><span class="sxs-lookup"><span data-stu-id="49fcc-115">Use the invoke request's context to respond back with cards that are specifically created for a user.</span></span>

    > [!NOTE]
    > <span data-ttu-id="49fcc-116">Каждый раз, когда бот возвращает новую карточку в результате обработки `Action.Execute`, отклик должен соответствовать формату отклика.</span><span class="sxs-lookup"><span data-stu-id="49fcc-116">Whenever your bot returns a new card as a result of processing an `Action.Execute`, the response must conform to the response format.</span></span>

## <a name="schema-for-universal-actions-for-adaptive-cards"></a><span data-ttu-id="49fcc-117">Схема для универсальных действий для адаптивных карточек</span><span class="sxs-lookup"><span data-stu-id="49fcc-117">Schema for Universal Actions for Adaptive Cards</span></span>

<span data-ttu-id="49fcc-118">Универсальные действия для адаптивных карточек представлены в схеме адаптивных карточек версии 1.4.</span><span class="sxs-lookup"><span data-stu-id="49fcc-118">Universal Actions for Adaptive Cards is introduced in the Adaptive Cards schema version 1.4.</span></span> <span data-ttu-id="49fcc-119">Для эффективного использования адаптивной карточки свойство `version` адаптивной карточки должно быть установлено на 1.4.</span><span class="sxs-lookup"><span data-stu-id="49fcc-119">To use Adaptive Card effectively, the `version` property of your Adaptive Card must be set to 1.4.</span></span>

> [!NOTE]
> <span data-ttu-id="49fcc-120">При установке свойства `version` на 1.4 адаптивная карточка становится несовместима с более старыми клиентами платформ или приложений, например с Outlook и Teams, так как они не поддерживают универсальные действия для адаптивных карточек.</span><span class="sxs-lookup"><span data-stu-id="49fcc-120">Setting the `version` property to 1.4 makes your Adaptive Card incompatible with older clients of the platforms or applications, such as Outlook and Teams, as they do not support the Universal Actions for Adaptive Cards.</span></span>

<span data-ttu-id="49fcc-121">Если установить версию карточки меньше 1.4 и использовать одно свойство или оба, `refresh` и `Action.Execute`, происходит следующее:</span><span class="sxs-lookup"><span data-stu-id="49fcc-121">If you set the card version to less than 1.4 and use either or both, `refresh` property and `Action.Execute`, the following happens:</span></span>

| <span data-ttu-id="49fcc-122">Клиент</span><span class="sxs-lookup"><span data-stu-id="49fcc-122">Client</span></span> | <span data-ttu-id="49fcc-123">Поведение</span><span class="sxs-lookup"><span data-stu-id="49fcc-123">Behavior</span></span> |
| :-- | :-- |
| <span data-ttu-id="49fcc-124">Teams</span><span class="sxs-lookup"><span data-stu-id="49fcc-124">Teams</span></span> | <span data-ttu-id="49fcc-125">Карточка перестает работать.</span><span class="sxs-lookup"><span data-stu-id="49fcc-125">Your card stops working.</span></span> <span data-ttu-id="49fcc-126">Карточка не обновляется и `Action.Execute` не обрабатывается в зависимости от версии клиента Teams.</span><span class="sxs-lookup"><span data-stu-id="49fcc-126">Card is not refreshed and `Action.Execute` does not render depending on the version of the Teams client.</span></span> <span data-ttu-id="49fcc-127">Чтобы обеспечить максимальную совместимость в Teams, определите в свойстве отката `Action.Execute` с `Action.Submit`.</span><span class="sxs-lookup"><span data-stu-id="49fcc-127">To ensure maximum compatibility in Teams, define `Action.Execute` with an `Action.Submit` in the fallback property.</span></span> |

<span data-ttu-id="49fcc-128">Дополнительные сведения о поддержке клиентов более старых версий см. в разделе [обратная совместимость](#backward-compatibility).</span><span class="sxs-lookup"><span data-stu-id="49fcc-128">For more information on how to support older clients, see [backward compatibility](#backward-compatibility).</span></span>

### <a name="actionexecute"></a><span data-ttu-id="49fcc-129">Action.Execute</span><span class="sxs-lookup"><span data-stu-id="49fcc-129">Action.Execute</span></span>

<span data-ttu-id="49fcc-130">При разработке адаптивных карточек замените `Action.Submit` и `Action.Http` на `Action.Execute`.</span><span class="sxs-lookup"><span data-stu-id="49fcc-130">When authoring Adaptive Cards, replace `Action.Submit` and `Action.Http` with `Action.Execute`.</span></span> <span data-ttu-id="49fcc-131">Схема для `Action.Execute` аналогична схеме `Action.Submit`.</span><span class="sxs-lookup"><span data-stu-id="49fcc-131">The schema for `Action.Execute` is similar to that of `Action.Submit`.</span></span>

<span data-ttu-id="49fcc-132">Дополнительные сведения см. в разделе [Схема и свойства Action.Execute](/adaptive-cards/authoring-cards/universal-action-model#actionexecute).</span><span class="sxs-lookup"><span data-stu-id="49fcc-132">For more information, see [Action.Execute schema and properties](/adaptive-cards/authoring-cards/universal-action-model#actionexecute).</span></span>

<span data-ttu-id="49fcc-133">Теперь вы можете использовать модель обновления, чтобы разрешить автоматическое обновление адаптивных карточек.</span><span class="sxs-lookup"><span data-stu-id="49fcc-133">Now, you can use the refresh model to allow Adaptive Cards to update automatically.</span></span>

## <a name="refresh-model"></a><span data-ttu-id="49fcc-134">Модель обновления</span><span class="sxs-lookup"><span data-stu-id="49fcc-134">Refresh model</span></span>

<span data-ttu-id="49fcc-135">Чтобы автоматически обновить адаптивную карточку, определите ее свойство `refresh`, которое внедряет действие типа `Action.Execute` и массив `userIds`.</span><span class="sxs-lookup"><span data-stu-id="49fcc-135">To automatically refresh your Adaptive Card, define its `refresh` property, which embeds an action of type `Action.Execute` and an `userIds` array.</span></span>

<span data-ttu-id="49fcc-136">Дополнительные сведения см. в разделе [схема и свойства обновления](/adaptive-cards/authoring-cards/universal-action-model#refresh-mechanism).</span><span class="sxs-lookup"><span data-stu-id="49fcc-136">For more information, see [refresh schema and properties](/adaptive-cards/authoring-cards/universal-action-model#refresh-mechanism).</span></span>

## <a name="user-ids-in-refresh"></a><span data-ttu-id="49fcc-137">Идентификаторы пользователей в процессе обновления</span><span class="sxs-lookup"><span data-stu-id="49fcc-137">User IDs in refresh</span></span>

<span data-ttu-id="49fcc-138">Ниже даны функции UserIds в процессе обновления.</span><span class="sxs-lookup"><span data-stu-id="49fcc-138">The following are the features of UserIds in refresh:</span></span>

* <span data-ttu-id="49fcc-139">UserIds — это массив MRI пользователя, который является частью свойства `refresh` адаптивных карточек.</span><span class="sxs-lookup"><span data-stu-id="49fcc-139">UserIds is an array of user MRI's which is part of the `refresh` property in Adaptive Cards.</span></span>

* <span data-ttu-id="49fcc-140">Если свойство списка `userIds` указано как `userIds: []` в разделе обновления карточки, карточка не обновляется автоматически.</span><span class="sxs-lookup"><span data-stu-id="49fcc-140">If the `userIds` list property is specified as `userIds: []` in the refresh section of the card, the card is not automatically refreshed.</span></span> <span data-ttu-id="49fcc-141">Вместо этого пользователь видит параметр **Обновить карточку** в меню с тремя точками в классическом или веб-приложении и в контекстном меню при длительном нажатии на мобильном устройстве, то есть на Android или iOS, чтобы обновить карточку вручную.</span><span class="sxs-lookup"><span data-stu-id="49fcc-141">Instead, a **Refresh Card** option is displayed to the user in the triple dot menu in web or desktop and in the long press context menu in mobile, that is, Android or iOS to manually refresh the card.</span></span>

* <span data-ttu-id="49fcc-142">Добавлено свойство UserIds, так как каналы в Teams могут включать множество участников.</span><span class="sxs-lookup"><span data-stu-id="49fcc-142">UserIds property is added because channels in Teams can include a large number of members.</span></span> <span data-ttu-id="49fcc-143">Если все участники одновременно просматривают канал, безусловное автоматическое обновление приводит к множеству одновременных вызовов бота.</span><span class="sxs-lookup"><span data-stu-id="49fcc-143">If all members are viewing the channel at the same time, an unconditional automatic refresh results in many concurrent calls to the bot.</span></span> <span data-ttu-id="49fcc-144">Чтобы избежать этого, свойство `userIds` всегда должно быть включено, чтобы определять, какие пользователи должны получать автоматическое обновление при максимуме в *60 (шестьдесят) пользовательских MRI*.</span><span class="sxs-lookup"><span data-stu-id="49fcc-144">To avoid this, the `userIds` property must always be included to identify which users must get an automatic refresh with a maximum of *60 (sixty) user MRIs*.</span></span>

* <span data-ttu-id="49fcc-145">Дополнительные сведения о том, как получить MRI пользователей, участвующих в беседе Teams, для добавления в список userIds в разделе обновления адаптивной карточки, см. в разделе [получить профиль списка участников или пользователя](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile).</span><span class="sxs-lookup"><span data-stu-id="49fcc-145">For more information on how you can fetch Teams conversation member's user MRIs to add in userIds list in refresh section of Adaptive Card, see [fetch roster or user profile](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile).</span></span>

* <span data-ttu-id="49fcc-146">Пример MRI пользователя Teams: `29:1bSnHZ7Js2STWrgk6ScEErLk1Lp2zQuD5H2qQ960rtvstKp8tKLl-3r8b6DoW0QxZimuTxk_kupZ1DBMpvIQQUAZL-PNj0EORDvRZXy8kvWk`</span><span class="sxs-lookup"><span data-stu-id="49fcc-146">Sample Teams user MRI is `29:1bSnHZ7Js2STWrgk6ScEErLk1Lp2zQuD5H2qQ960rtvstKp8tKLl-3r8b6DoW0QxZimuTxk_kupZ1DBMpvIQQUAZL-PNj0EORDvRZXy8kvWk`</span></span>

> [!NOTE]
> <span data-ttu-id="49fcc-147">Свойство `userIds` игнорируется в Outlook, а свойство `refresh` всегда активируется автоматически.</span><span class="sxs-lookup"><span data-stu-id="49fcc-147">The `userIds` property is ignored in Outlook, and the `refresh` property is always automatically activated.</span></span> <span data-ttu-id="49fcc-148">Для Outlook проблемы масштабирования не существует, так как пользователи просматривают карточку в разное время.</span><span class="sxs-lookup"><span data-stu-id="49fcc-148">There is no scale issue in Outlook because users view the card at different times.</span></span>

<span data-ttu-id="49fcc-149">Следующий шаг — использование запуска действия `adaptiveCard/action`, чтобы понять, какой должен быть сделан запрос после выполнения `Action.Execute`.</span><span class="sxs-lookup"><span data-stu-id="49fcc-149">Next step is to use the `adaptiveCard/action` invoke activity to understand what request must be made after `Action.Execute` is executed.</span></span>

## <a name="adaptivecardaction-invoke-activity"></a><span data-ttu-id="49fcc-150">`adaptiveCard/action` запуск действия</span><span class="sxs-lookup"><span data-stu-id="49fcc-150">`adaptiveCard/action` invoke activity</span></span>

<span data-ttu-id="49fcc-151">Когда в клиенте выполняется `Action.Execute`, для вашего бота создается новый тип запуска действия `adaptiveCard/action`.</span><span class="sxs-lookup"><span data-stu-id="49fcc-151">When `Action.Execute` is executed in the client, a new type of Invoke activity `adaptiveCard/action` is made to your bot.</span></span>

<span data-ttu-id="49fcc-152">Дополнительные сведения см. в разделе: [формат запроса и свойства обычного `adaptiveCard/action` запуска действия](/adaptive-cards/authoring-cards/universal-action-model#request-format).</span><span class="sxs-lookup"><span data-stu-id="49fcc-152">For more information, see [request format and properties for a typical `adaptiveCard/action` invoke activity](/adaptive-cards/authoring-cards/universal-action-model#request-format).</span></span>

<span data-ttu-id="49fcc-153">Дополнительные сведения см. в разделе: [формат отклика и свойства обычного `adaptiveCard/action` запуска действия с поддерживаемыми типами отклика](/adaptive-cards/authoring-cards/universal-action-model#response-format).</span><span class="sxs-lookup"><span data-stu-id="49fcc-153">For more information, see [response format and properties for a typical `adaptiveCard/action` invoke activity with supported response types](/adaptive-cards/authoring-cards/universal-action-model#response-format).</span></span>

<span data-ttu-id="49fcc-154">Затем к старым клиентам на разных платформах можно применить обратную совместимость и сделать адаптивную карточку совместимой.</span><span class="sxs-lookup"><span data-stu-id="49fcc-154">Next, you can apply backward compatibility to older clients across different platforms and make your Adaptive Card compatible.</span></span>

## <a name="backward-compatibility"></a><span data-ttu-id="49fcc-155">Обратная совместимость</span><span class="sxs-lookup"><span data-stu-id="49fcc-155">Backward compatibility</span></span>

<span data-ttu-id="49fcc-156">Универсальные действия для адаптивных карточек позволяют задать свойства, которые обеспечивают обратную совместимость с более старыми версиями Outlook и Teams.</span><span class="sxs-lookup"><span data-stu-id="49fcc-156">Universal Actions for Adaptive Cards allows you to set properties that enable backward compatibility with older versions of Outlook and Teams.</span></span>

### <a name="teams"></a><span data-ttu-id="49fcc-157">Teams</span><span class="sxs-lookup"><span data-stu-id="49fcc-157">Teams</span></span>

<span data-ttu-id="49fcc-158">Чтобы обеспечить обратную совместимость адаптивных карточек с более старыми версиями Teams, необходимо включить свойство `fallback` и установить для него значение `Action.Submit`.</span><span class="sxs-lookup"><span data-stu-id="49fcc-158">To ensure backward compatibility of your Adaptive Cards with older versions of Teams, you must include the `fallback` property and set its value to `Action.Submit`.</span></span> <span data-ttu-id="49fcc-159">Кроме того, код бота должен обрабатывать как `Action.Execute`, так и `Action.Submit`.</span><span class="sxs-lookup"><span data-stu-id="49fcc-159">Also, your bot code must process both `Action.Execute` and `Action.Submit`.</span></span>

<span data-ttu-id="49fcc-160">Дополнительные сведения см. в разделе [обратная совместимость в Teams](/adaptive-cards/authoring-cards/universal-action-model#teams).</span><span class="sxs-lookup"><span data-stu-id="49fcc-160">For more information, see [backward compatibility on Teams](/adaptive-cards/authoring-cards/universal-action-model#teams).</span></span>

## <a name="code-sample"></a><span data-ttu-id="49fcc-161">Пример кода</span><span class="sxs-lookup"><span data-stu-id="49fcc-161">Code sample</span></span>

|<span data-ttu-id="49fcc-162">Название примера</span><span class="sxs-lookup"><span data-stu-id="49fcc-162">Sample name</span></span> | <span data-ttu-id="49fcc-163">Описание</span><span class="sxs-lookup"><span data-stu-id="49fcc-163">Description</span></span> | <span data-ttu-id="49fcc-164">.NETCore</span><span class="sxs-lookup"><span data-stu-id="49fcc-164">.NETCore</span></span> |
|----------------|-----------------|--------------|
| <span data-ttu-id="49fcc-165">Бот организации питания Teams</span><span class="sxs-lookup"><span data-stu-id="49fcc-165">Teams catering bot</span></span> | <span data-ttu-id="49fcc-166">Создайте простого бота, который принимает заказы на обед с помощью адаптивных карточек.</span><span class="sxs-lookup"><span data-stu-id="49fcc-166">Create a simple bot that accepts food order using Adaptive Cards.</span></span> |[<span data-ttu-id="49fcc-167">Просмотр</span><span class="sxs-lookup"><span data-stu-id="49fcc-167">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-teams-catering/csharp)|

## <a name="see-also"></a><span data-ttu-id="49fcc-168">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="49fcc-168">See also</span></span>

* [<span data-ttu-id="49fcc-169">Действия адаптивной карточки в Teams</span><span class="sxs-lookup"><span data-stu-id="49fcc-169">Adaptive Card actions in Teams</span></span>](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)
* [<span data-ttu-id="49fcc-170">Как работают боты</span><span class="sxs-lookup"><span data-stu-id="49fcc-170">How bots work</span></span>](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)
