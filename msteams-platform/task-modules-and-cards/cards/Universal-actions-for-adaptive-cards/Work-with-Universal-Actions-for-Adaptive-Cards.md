---
title: Работа с универсальными действиями для адаптивных карточек
description: Работа с универсальными действиями для адаптивных карт.
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 4361f1c7774837b728c6382df4e62e00ea912e35
ms.sourcegitcommit: 999f5c607671e088ea8a461fa7dbb63f8d61c39b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/25/2021
ms.locfileid: "52649701"
---
# <a name="work-with-universal-actions-for-adaptive-cards"></a><span data-ttu-id="7a869-103">Работа с универсальными действиями для адаптивных карточек</span><span class="sxs-lookup"><span data-stu-id="7a869-103">Work with Universal Actions for Adaptive Cards</span></span>

<span data-ttu-id="7a869-104">Универсальные действия для адаптивных карт предоставляют способ реализации сценариев, основанных на адаптивной карте, как для Teams, так и для Outlook.</span><span class="sxs-lookup"><span data-stu-id="7a869-104">Universal Actions for Adaptive Cards provides a way to implement Adaptive Card based scenarios for both, Teams and Outlook.</span></span> <span data-ttu-id="7a869-105">В этом документе описывается следующее:</span><span class="sxs-lookup"><span data-stu-id="7a869-105">This document covers the following:</span></span>

* [<span data-ttu-id="7a869-106">Схема, используемая для универсальных действий для адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="7a869-106">Schema used for Universal Actions for Adaptive Cards</span></span>](#schema-for-universal-actions-for-adaptive-cards)
* [<span data-ttu-id="7a869-107">Модель обновления</span><span class="sxs-lookup"><span data-stu-id="7a869-107">Refresh model</span></span>](#refresh-model)
* [<span data-ttu-id="7a869-108">`adaptiveCard/action` вызов активности</span><span class="sxs-lookup"><span data-stu-id="7a869-108">`adaptiveCard/action` invoke activity</span></span>](#adaptivecardaction-invoke-activity)
* [<span data-ttu-id="7a869-109">Обратная совместимость</span><span class="sxs-lookup"><span data-stu-id="7a869-109">Backward compatibility</span></span>](#backward-compatibility)

## <a name="quick-start-guide-to-leverage-universal-actions-for-adaptive-cards-in-teams"></a><span data-ttu-id="7a869-110">Руководство по быстрому началу использования универсальных действий для адаптивных карт в Teams</span><span class="sxs-lookup"><span data-stu-id="7a869-110">Quick start guide to leverage Universal Actions for Adaptive Cards in Teams</span></span>

1. <span data-ttu-id="7a869-111">Замените все `Action.Submit` экземпляры, `Action.Execute` чтобы обновить существующий сценарий в Teams.</span><span class="sxs-lookup"><span data-stu-id="7a869-111">Replace all instances of `Action.Submit` with `Action.Execute` to update an existing scenario on Teams.</span></span>
2. <span data-ttu-id="7a869-112">Добавьте пункт в адаптивную карту, если вы хотите использовать модель автоматического обновления или если для сценария `refresh` требуются пользовательские представления.</span><span class="sxs-lookup"><span data-stu-id="7a869-112">Add a `refresh` clause to your Adaptive Card, if you want to leverage the automatic refresh model or if your scenario requires User Specific Views.</span></span>

    >[!NOTE]
    > <span data-ttu-id="7a869-113">Укажите `userIds` свойство для определения, какие пользователи получают автоматические обновления.</span><span class="sxs-lookup"><span data-stu-id="7a869-113">Specify the `userIds` property to identify, which users get automatic updates.</span></span>

3. <span data-ttu-id="7a869-114">Обработка `adaptiveCard/action` запросов вызова в боте.</span><span class="sxs-lookup"><span data-stu-id="7a869-114">Handle `adaptiveCard/action` invoke requests in your bot.</span></span>
4. <span data-ttu-id="7a869-115">Используйте контекст запроса на вызов, чтобы ответить на них картами, специально созданными для пользователя.</span><span class="sxs-lookup"><span data-stu-id="7a869-115">Use the invoke request's context to respond back with cards that are specifically created for a user.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7a869-116">Всякий раз, когда бот возвращает новую карту в результате обработки, ответ должен `Action.Execute` соответствовать формату ответа.</span><span class="sxs-lookup"><span data-stu-id="7a869-116">Whenever your bot returns a new card as a result of processing an `Action.Execute`, the response must conform to the response format.</span></span>

## <a name="schema-for-universal-actions-for-adaptive-cards"></a><span data-ttu-id="7a869-117">Схема универсальных действий для адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="7a869-117">Schema for Universal Actions for Adaptive Cards</span></span>

<span data-ttu-id="7a869-118">Универсальные действия для адаптивных карт представлены в схеме адаптивных карт версии 1.4.</span><span class="sxs-lookup"><span data-stu-id="7a869-118">Universal Actions for Adaptive Cards is introduced in the Adaptive Cards schema version 1.4.</span></span> <span data-ttu-id="7a869-119">Для эффективного использования адаптивной карты необходимо установить свойство адаптивной карты `version` 1.4.</span><span class="sxs-lookup"><span data-stu-id="7a869-119">To use Adaptive Card effectively, the `version` property of your Adaptive Card must be set to 1.4.</span></span>

> [!NOTE]
> <span data-ttu-id="7a869-120">Настройка свойства 1.4 делает адаптивную карту несовместимой со старыми клиентами платформ или приложений, таких как Outlook и Teams, так как они не поддерживают универсальные действия для адаптивных `version` карт.</span><span class="sxs-lookup"><span data-stu-id="7a869-120">Setting the `version` property to 1.4 makes your Adaptive Card incompatible with older clients of the platforms or applications, such as Outlook and Teams, as they do not support the Universal Actions for Adaptive Cards.</span></span>

<span data-ttu-id="7a869-121">Если вы установите версию карты меньше 1.4 и используете свойство или оба свойства, и `refresh` `Action.Execute` произойдет следующее:</span><span class="sxs-lookup"><span data-stu-id="7a869-121">If you set the card version to less than 1.4 and use either or both, `refresh` property and `Action.Execute`, the following happens:</span></span>

| <span data-ttu-id="7a869-122">Клиент</span><span class="sxs-lookup"><span data-stu-id="7a869-122">Client</span></span> | <span data-ttu-id="7a869-123">Поведение</span><span class="sxs-lookup"><span data-stu-id="7a869-123">Behavior</span></span> |
| :-- | :-- |
| <span data-ttu-id="7a869-124">Teams</span><span class="sxs-lookup"><span data-stu-id="7a869-124">Teams</span></span> | <span data-ttu-id="7a869-125">Карта перестает работать.</span><span class="sxs-lookup"><span data-stu-id="7a869-125">Your card stops working.</span></span> <span data-ttu-id="7a869-126">Карта не обновляется и не отрисовка в зависимости от версии Teams `Action.Execute` клиента.</span><span class="sxs-lookup"><span data-stu-id="7a869-126">Card is not refreshed and `Action.Execute` does not render depending on the version of the Teams client.</span></span> <span data-ttu-id="7a869-127">Чтобы обеспечить максимальную совместимость Teams, `Action.Execute` определите с `Action.Submit` свойством отката.</span><span class="sxs-lookup"><span data-stu-id="7a869-127">To ensure maximum compatibility in Teams, define `Action.Execute` with an `Action.Submit` in the fallback property.</span></span> |

<span data-ttu-id="7a869-128">Дополнительные сведения о поддержке старых клиентов см. в обратной [совместимости.](#backward-compatibility)</span><span class="sxs-lookup"><span data-stu-id="7a869-128">For more information on how to support older clients, see [backward compatibility](#backward-compatibility).</span></span>

### <a name="actionexecute"></a><span data-ttu-id="7a869-129">Action.Exeмило</span><span class="sxs-lookup"><span data-stu-id="7a869-129">Action.Execute</span></span>

<span data-ttu-id="7a869-130">При авторе адаптивных карт замените `Action.Submit` и `Action.Http` с помощью `Action.Execute` .</span><span class="sxs-lookup"><span data-stu-id="7a869-130">When authoring Adaptive Cards, replace `Action.Submit` and `Action.Http` with `Action.Execute`.</span></span> <span data-ttu-id="7a869-131">Схема похожа на схему `Action.Execute` `Action.Submit` .</span><span class="sxs-lookup"><span data-stu-id="7a869-131">The schema for `Action.Execute` is similar to that of `Action.Submit`.</span></span>

<span data-ttu-id="7a869-132">Дополнительные сведения см. [вAction.Exeсхеме и свойствах.](/adaptive-cards/authoring-cards/universal-action-model#actionexecute)</span><span class="sxs-lookup"><span data-stu-id="7a869-132">For more information, see [Action.Execute schema and properties](/adaptive-cards/authoring-cards/universal-action-model#actionexecute).</span></span>

<span data-ttu-id="7a869-133">Теперь модель обновления позволяет автоматически обновлять адаптивные карты.</span><span class="sxs-lookup"><span data-stu-id="7a869-133">Now, you can use the refresh model to allow Adaptive Cards to update automatically.</span></span>

## <a name="refresh-model"></a><span data-ttu-id="7a869-134">Модель обновления</span><span class="sxs-lookup"><span data-stu-id="7a869-134">Refresh model</span></span>

<span data-ttu-id="7a869-135">Чтобы автоматически обновить адаптивную карту, определите ее свойство, в которое встраиваться действие `refresh` типа `Action.Execute` и `userIds` массива.</span><span class="sxs-lookup"><span data-stu-id="7a869-135">To automatically refresh your Adaptive Card, define its `refresh` property, which embeds an action of type `Action.Execute` and an `userIds` array.</span></span>

<span data-ttu-id="7a869-136">Дополнительные сведения см. в [обновленной схеме и свойствах.](/adaptive-cards/authoring-cards/universal-action-model#refresh-mechanism)</span><span class="sxs-lookup"><span data-stu-id="7a869-136">For more information, see [refresh schema and properties](/adaptive-cards/authoring-cards/universal-action-model#refresh-mechanism).</span></span>

## <a name="user-ids-in-refresh"></a><span data-ttu-id="7a869-137">Пользовательские ID в обновлении</span><span class="sxs-lookup"><span data-stu-id="7a869-137">User IDs in refresh</span></span>

<span data-ttu-id="7a869-138">Ниже представлены функции UserIds в обновлении:</span><span class="sxs-lookup"><span data-stu-id="7a869-138">The following are the features of UserIds in refresh:</span></span>

* <span data-ttu-id="7a869-139">UserIds — это массив МРТ пользователя, который входит в свойство `refresh` адаптивных карт.</span><span class="sxs-lookup"><span data-stu-id="7a869-139">UserIds is an array of user MRI's which is part of the `refresh` property in Adaptive Cards.</span></span>

* <span data-ttu-id="7a869-140">Если свойство списка указывается как в разделе обновления карты, карта не обновляется `userIds` `userIds: []` автоматически.</span><span class="sxs-lookup"><span data-stu-id="7a869-140">If the `userIds` list property is specified as `userIds: []` in the refresh section of the card, the card is not automatically refreshed.</span></span> <span data-ttu-id="7a869-141">Вместо этого  пользователю в меню тройной точки в интернете или на рабочем столе отображается параметр "Карточка обновления", а в меню контекста длинного пресса в мобильном телефоне, то есть Android или iOS, чтобы вручную обновить карту.</span><span class="sxs-lookup"><span data-stu-id="7a869-141">Instead, a **Refresh Card** option is displayed to the user in the triple dot menu in web or desktop and in the long press context menu in mobile, that is, Android or iOS to manually refresh the card.</span></span>

* <span data-ttu-id="7a869-142">Свойство UserIds добавляется, так как каналы в Teams могут включать большое количество участников.</span><span class="sxs-lookup"><span data-stu-id="7a869-142">UserIds property is added because channels in Teams can include a large number of members.</span></span> <span data-ttu-id="7a869-143">Если все участники одновременно просматривают канал, безусловное автоматическое обновление приводит к много одновечерным вызовам бота.</span><span class="sxs-lookup"><span data-stu-id="7a869-143">If all members are viewing the channel at the same time, an unconditional automatic refresh results in many concurrent calls to the bot.</span></span> <span data-ttu-id="7a869-144">Чтобы избежать этого, свойство всегда должно быть включено, чтобы определить, какие пользователи должны получать автоматическое обновление с максимальным `userIds` *количеством 60 (шестидесяти) пользовательских МРИС.*</span><span class="sxs-lookup"><span data-stu-id="7a869-144">To avoid this, the `userIds` property must always be included to identify which users must get an automatic refresh with a maximum of *60 (sixty) user MRIs*.</span></span>

* <span data-ttu-id="7a869-145">Дополнительные сведения о том, как можно Teams пользовательские МРИ участника беседы, чтобы добавить в список userIds в разделе обновление адаптивной карты, см. в статье Fetch [roster or user profile.](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile)</span><span class="sxs-lookup"><span data-stu-id="7a869-145">For more information on how you can fetch Teams conversation member's user MRIs to add in userIds list in refresh section of Adaptive Card, see [fetch roster or user profile](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile).</span></span>

* <span data-ttu-id="7a869-146">Пример Teams МРТ пользователя`29:1bSnHZ7Js2STWrgk6ScEErLk1Lp2zQuD5H2qQ960rtvstKp8tKLl-3r8b6DoW0QxZimuTxk_kupZ1DBMpvIQQUAZL-PNj0EORDvRZXy8kvWk`</span><span class="sxs-lookup"><span data-stu-id="7a869-146">Sample Teams user MRI is `29:1bSnHZ7Js2STWrgk6ScEErLk1Lp2zQuD5H2qQ960rtvstKp8tKLl-3r8b6DoW0QxZimuTxk_kupZ1DBMpvIQQUAZL-PNj0EORDvRZXy8kvWk`</span></span>

> [!NOTE]
> <span data-ttu-id="7a869-147">Свойство игнорируется в Outlook, и свойство всегда `userIds` `refresh` автоматически активируется.</span><span class="sxs-lookup"><span data-stu-id="7a869-147">The `userIds` property is ignored in Outlook, and the `refresh` property is always automatically activated.</span></span> <span data-ttu-id="7a869-148">Проблема масштабирования в Outlook, так как пользователи просматривают карту в разное время.</span><span class="sxs-lookup"><span data-stu-id="7a869-148">There is no scale issue in Outlook because users view the card at different times.</span></span>

<span data-ttu-id="7a869-149">Следующий шаг — использование действия вызова, чтобы понять, какой запрос должен быть выполнен после `adaptiveCard/action` `Action.Execute` выполнения.</span><span class="sxs-lookup"><span data-stu-id="7a869-149">Next step is to use the `adaptiveCard/action` invoke activity to understand what request must be made after `Action.Execute` is executed.</span></span>

## <a name="adaptivecardaction-invoke-activity"></a><span data-ttu-id="7a869-150">`adaptiveCard/action` вызов активности</span><span class="sxs-lookup"><span data-stu-id="7a869-150">`adaptiveCard/action` invoke activity</span></span>

<span data-ttu-id="7a869-151">При выполнении в клиенте для бота выполняется новый тип действия `Action.Execute` `adaptiveCard/action` Invoke.</span><span class="sxs-lookup"><span data-stu-id="7a869-151">When `Action.Execute` is executed in the client, a new type of Invoke activity `adaptiveCard/action` is made to your bot.</span></span>

<span data-ttu-id="7a869-152">Дополнительные сведения см. в примере формата запросов и свойств типичной активности [ `adaptiveCard/action` вызова.](/adaptive-cards/authoring-cards/universal-action-model#request-format)</span><span class="sxs-lookup"><span data-stu-id="7a869-152">For more information, see [request format and properties for a typical `adaptiveCard/action` invoke activity](/adaptive-cards/authoring-cards/universal-action-model#request-format).</span></span>

<span data-ttu-id="7a869-153">Дополнительные сведения см. в примере формата отклика и свойств типичной активности вызова с [ `adaptiveCard/action` поддерживаемых типов откликов.](/adaptive-cards/authoring-cards/universal-action-model#response-format)</span><span class="sxs-lookup"><span data-stu-id="7a869-153">For more information, see [response format and properties for a typical `adaptiveCard/action` invoke activity with supported response types](/adaptive-cards/authoring-cards/universal-action-model#response-format).</span></span>

<span data-ttu-id="7a869-154">Далее можно применить обратную совместимость к старым клиентам на разных платформах и сделать адаптивную карту совместимой.</span><span class="sxs-lookup"><span data-stu-id="7a869-154">Next, you can apply backward compatibility to older clients across different platforms and make your Adaptive Card compatible.</span></span>

## <a name="backward-compatibility"></a><span data-ttu-id="7a869-155">Обратная совместимость</span><span class="sxs-lookup"><span data-stu-id="7a869-155">Backward compatibility</span></span>

<span data-ttu-id="7a869-156">Универсальные действия для адаптивных карт позволяют устанавливать свойства, которые позволяют обратной совместимости со старыми версиями Outlook и Teams.</span><span class="sxs-lookup"><span data-stu-id="7a869-156">Universal Actions for Adaptive Cards allows you to set properties that enable backward compatibility with older versions of Outlook and Teams.</span></span>

### <a name="teams"></a><span data-ttu-id="7a869-157">Teams</span><span class="sxs-lookup"><span data-stu-id="7a869-157">Teams</span></span>

<span data-ttu-id="7a869-158">Чтобы обеспечить обратную совместимость адаптивных карт с более старыми версиями Teams, необходимо включить свойство и установить `fallback` его значение `Action.Submit` .</span><span class="sxs-lookup"><span data-stu-id="7a869-158">To ensure backward compatibility of your Adaptive Cards with older versions of Teams, you must include the `fallback` property and set its value to `Action.Submit`.</span></span> <span data-ttu-id="7a869-159">Кроме того, код бота должен обрабатывать и `Action.Execute` `Action.Submit` .</span><span class="sxs-lookup"><span data-stu-id="7a869-159">Also, your bot code must process both `Action.Execute` and `Action.Submit`.</span></span>

<span data-ttu-id="7a869-160">Дополнительные сведения см. в [Teams.](/adaptive-cards/authoring-cards/universal-action-model#teams)</span><span class="sxs-lookup"><span data-stu-id="7a869-160">For more information, see [backward compatibility on Teams](/adaptive-cards/authoring-cards/universal-action-model#teams).</span></span>

## <a name="code-sample"></a><span data-ttu-id="7a869-161">Пример кода</span><span class="sxs-lookup"><span data-stu-id="7a869-161">Code sample</span></span>

|<span data-ttu-id="7a869-162">Пример имени</span><span class="sxs-lookup"><span data-stu-id="7a869-162">Sample name</span></span> | <span data-ttu-id="7a869-163">Описание</span><span class="sxs-lookup"><span data-stu-id="7a869-163">Description</span></span> | <span data-ttu-id="7a869-164">. NETCore</span><span class="sxs-lookup"><span data-stu-id="7a869-164">.NETCore</span></span> |
|----------------|-----------------|--------------|
| <span data-ttu-id="7a869-165">Teams питания бот</span><span class="sxs-lookup"><span data-stu-id="7a869-165">Teams catering bot</span></span> | <span data-ttu-id="7a869-166">Создайте простой бот, который принимает порядок питания с помощью адаптивных карт.</span><span class="sxs-lookup"><span data-stu-id="7a869-166">Create a simple bot that accepts food order using Adaptive Cards.</span></span> |[<span data-ttu-id="7a869-167">View</span><span class="sxs-lookup"><span data-stu-id="7a869-167">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-teams-catering/csharp)|

## <a name="see-also"></a><span data-ttu-id="7a869-168">См. также</span><span class="sxs-lookup"><span data-stu-id="7a869-168">See also</span></span>

* [<span data-ttu-id="7a869-169">Действия адаптивной карты в Teams</span><span class="sxs-lookup"><span data-stu-id="7a869-169">Adaptive Card actions in Teams</span></span>](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)
* [<span data-ttu-id="7a869-170">Как работают боты</span><span class="sxs-lookup"><span data-stu-id="7a869-170">How bots work</span></span>](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)
