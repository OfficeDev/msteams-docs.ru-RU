---
title: Типы карточек
description: Описывает все действия карт и карт, доступные ботам в Teams
localization_priority: Normal
keywords: ссылка на карточки ботов
ms.topic: reference
ms.openlocfilehash: d3b84344eccee7c2595b0e978c72d7e331b198cb
ms.sourcegitcommit: b1f9162a0bbcd276064ae9e4f1e8bccc06cb7035
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/07/2021
ms.locfileid: "53328074"
---
# <a name="types-of-cards"></a><span data-ttu-id="9c437-104">Типы карточек</span><span class="sxs-lookup"><span data-stu-id="9c437-104">Types of cards</span></span>

<span data-ttu-id="9c437-105">Адаптивные, герой, список, Office 365 соединителю, квитанции, знаки и эскизные карты и коллекции карт поддерживаются в ботах для Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="9c437-105">Adaptive, hero, list, Office 365 Connector, receipt, signin, and thumbnail cards and card collections are supported in bots for Microsoft Teams.</span></span> <span data-ttu-id="9c437-106">Они основаны на картах, определенных bot Framework, но Teams не поддерживают все карты Bot Framework и добавили некоторые из них.</span><span class="sxs-lookup"><span data-stu-id="9c437-106">They are based on cards defined by the Bot Framework, but Teams does not support all Bot Framework cards and has added some of its own.</span></span>

<span data-ttu-id="9c437-107">Прежде чем определить различные типы карт, поймите, как создать карточку героя, карту эскиза или адаптивную карту.</span><span class="sxs-lookup"><span data-stu-id="9c437-107">Before you identify the different card types, understand how to create a a hero card, thumbnail card, or Adaptive Card.</span></span>

## <a name="create-a-hero-card-thumbnail-card-or-adaptive-card"></a><span data-ttu-id="9c437-108">Создание карты героя, карты эскиза или адаптивной карты</span><span class="sxs-lookup"><span data-stu-id="9c437-108">Create a hero card, thumbnail card, or Adaptive Card</span></span>

<span data-ttu-id="9c437-109">**Создание карты героя, карты эскиза или адаптивной карты из App Studio**</span><span class="sxs-lookup"><span data-stu-id="9c437-109">**To create a hero card, thumbnail card, or Adaptive Card from App Studio**</span></span>

1. <span data-ttu-id="9c437-110">Перейдите **в App Studio** из Teams.</span><span class="sxs-lookup"><span data-stu-id="9c437-110">Go to **App Studio** from Teams.</span></span>
1. <span data-ttu-id="9c437-111">Выберите **редактор карты**.</span><span class="sxs-lookup"><span data-stu-id="9c437-111">Select **Card editor**.</span></span>
1. <span data-ttu-id="9c437-112">Выберите **Создание новой карты.**</span><span class="sxs-lookup"><span data-stu-id="9c437-112">Select **Create a new card**.</span></span>
1. <span data-ttu-id="9c437-113">Выберите **Создать** для одной из карт карточки **героя,** **эскизной** карты или **адаптивной карты.**</span><span class="sxs-lookup"><span data-stu-id="9c437-113">Select **Create** for one of the cards from **Hero Card**, **Thumbnail Card**, or **Adaptive Card**.</span></span> <span data-ttu-id="9c437-114">Для этой карты показаны сведения о метаданных, кнопки и примеры кода json, csharp и узлов.</span><span class="sxs-lookup"><span data-stu-id="9c437-114">The metadata details, buttons, and json, csharp, and node code examples are shown for that card.</span></span>

    ![Сведения о карточке героя](~/assets/images/Cards/Herocarddetails.png)

1. <span data-ttu-id="9c437-116">Выберите **Отправить мне эту карточку.**</span><span class="sxs-lookup"><span data-stu-id="9c437-116">Select **Send me this card**.</span></span> <span data-ttu-id="9c437-117">Карта отправляется вам в качестве сообщения чата.</span><span class="sxs-lookup"><span data-stu-id="9c437-117">The card is sent to you as a chat message.</span></span>

## <a name="card-examples"></a><span data-ttu-id="9c437-118">Примеры карт</span><span class="sxs-lookup"><span data-stu-id="9c437-118">Card examples</span></span>

<span data-ttu-id="9c437-119">Дополнительные сведения об использовании карт можно найти в документации для bot Builder SDK v3.</span><span class="sxs-lookup"><span data-stu-id="9c437-119">You can find additional information on how to use cards in the documentation for the Bot Builder SDK v3.</span></span> <span data-ttu-id="9c437-120">Примеры кода также доступны в репозитории **Microsoft/BotBuilder-Samples** на GitHub.</span><span class="sxs-lookup"><span data-stu-id="9c437-120">Code samples are also available in the **Microsoft/BotBuilder-Samples** repository on GitHub.</span></span> <span data-ttu-id="9c437-121">Ниже приводится несколько примеров карт:</span><span class="sxs-lookup"><span data-stu-id="9c437-121">Following are a few card examples:</span></span>

* <span data-ttu-id="9c437-122">.NET</span><span class="sxs-lookup"><span data-stu-id="9c437-122">.NET</span></span>
  * <span data-ttu-id="9c437-123">[Добавление карт в виде вложений в сообщения.](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="9c437-123">[Add cards as attachments to messages](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true).</span></span>
  * <span data-ttu-id="9c437-124">[Карты пример кода Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards).</span><span class="sxs-lookup"><span data-stu-id="9c437-124">[Cards sample code Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards).</span></span>

* <span data-ttu-id="9c437-125">Node.js</span><span class="sxs-lookup"><span data-stu-id="9c437-125">Node.js</span></span>
  * <span data-ttu-id="9c437-126">[Добавление карт в виде вложений в сообщения.](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="9c437-126">[Add cards as attachments to messages](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true).</span></span>
  * <span data-ttu-id="9c437-127">[Карты пример кода Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards).</span><span class="sxs-lookup"><span data-stu-id="9c437-127">[Cards sample code Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards).</span></span>

## <a name="card-types"></a><span data-ttu-id="9c437-128">Типы карт</span><span class="sxs-lookup"><span data-stu-id="9c437-128">Card types</span></span>

<span data-ttu-id="9c437-129">Вы можете определять и использовать различные типы карт в зависимости от требований к приложению.</span><span class="sxs-lookup"><span data-stu-id="9c437-129">You can identify and use different types of cards based on your application requirements.</span></span> <span data-ttu-id="9c437-130">В следующей таблице показаны типы доступных вам карт:</span><span class="sxs-lookup"><span data-stu-id="9c437-130">The following table shows the types of cards available to you:</span></span>

| <span data-ttu-id="9c437-131">Тип карты</span><span class="sxs-lookup"><span data-stu-id="9c437-131">Card type</span></span> | <span data-ttu-id="9c437-132">Описание</span><span class="sxs-lookup"><span data-stu-id="9c437-132">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="9c437-133">Адаптивная карта</span><span class="sxs-lookup"><span data-stu-id="9c437-133">Adaptive Card</span></span>](#adaptive-card) | <span data-ttu-id="9c437-134">Эта карта очень настраиваема и может содержать любое сочетание текстов, речи, изображений, кнопок и полей ввода.</span><span class="sxs-lookup"><span data-stu-id="9c437-134">This card is highly customizable and can contain any combination of text, speech, images, buttons, and input fields.</span></span> |
| [<span data-ttu-id="9c437-135">Карта hero</span><span class="sxs-lookup"><span data-stu-id="9c437-135">Hero card</span></span>](#hero-card) | <span data-ttu-id="9c437-136">Эта карта обычно содержит одно большое изображение, одну или несколько кнопок и небольшое количество текста.</span><span class="sxs-lookup"><span data-stu-id="9c437-136">This card typically contains a single large image, one or more buttons, and a small amount of text.</span></span> |
| [<span data-ttu-id="9c437-137">Карта списка</span><span class="sxs-lookup"><span data-stu-id="9c437-137">List card</span></span>](#list-card) | <span data-ttu-id="9c437-138">Эта карта содержит список элементов прокрутки.</span><span class="sxs-lookup"><span data-stu-id="9c437-138">This card contains a scrolling list of items.</span></span> |
| [<span data-ttu-id="9c437-139">Office 365 Карта Connector</span><span class="sxs-lookup"><span data-stu-id="9c437-139">Office 365 Connector card</span></span>](#office-365-connector-card) | <span data-ttu-id="9c437-140">Эта карта имеет гибкий макет с несколькими разделами, полями, изображениями и действиями.</span><span class="sxs-lookup"><span data-stu-id="9c437-140">This card has a flexible layout with multiple sections, fields, images, and actions.</span></span> |
| [<span data-ttu-id="9c437-141">Карта получения</span><span class="sxs-lookup"><span data-stu-id="9c437-141">Receipt card</span></span>](#receipt-card) | <span data-ttu-id="9c437-142">Эта карта предоставляет квитанцию пользователю.</span><span class="sxs-lookup"><span data-stu-id="9c437-142">This card provides a receipt to the user.</span></span> |
| [<span data-ttu-id="9c437-143">Карточка Signin</span><span class="sxs-lookup"><span data-stu-id="9c437-143">Signin card</span></span>](#signin-card) | <span data-ttu-id="9c437-144">Эта карта позволяет боту запрашивать, чтобы пользователь войди.</span><span class="sxs-lookup"><span data-stu-id="9c437-144">This card enables a bot to request that a user signs in.</span></span> |
| [<span data-ttu-id="9c437-145">Карта эскиза</span><span class="sxs-lookup"><span data-stu-id="9c437-145">Thumbnail card</span></span>](#thumbnail-card) | <span data-ttu-id="9c437-146">Эта карта обычно содержит одно изображение эскиза, короткий текст и одну или несколько кнопок.</span><span class="sxs-lookup"><span data-stu-id="9c437-146">This card typically contains a single thumbnail image, some short text, and one or more buttons.</span></span> |
| [<span data-ttu-id="9c437-147">Коллекции карт</span><span class="sxs-lookup"><span data-stu-id="9c437-147">Card collections</span></span>](#card-collections) | <span data-ttu-id="9c437-148">Эта коллекция карт используется для возврата нескольких элементов в одном ответе.</span><span class="sxs-lookup"><span data-stu-id="9c437-148">This card collection is used to return multiple items in a single response.</span></span> |

## <a name="features-that-support-different-card-types"></a><span data-ttu-id="9c437-149">Функции, поддерживаюные различные типы карт</span><span class="sxs-lookup"><span data-stu-id="9c437-149">Features that support different card types</span></span>

| <span data-ttu-id="9c437-150">Тип карты</span><span class="sxs-lookup"><span data-stu-id="9c437-150">Card type</span></span> | <span data-ttu-id="9c437-151">Боты</span><span class="sxs-lookup"><span data-stu-id="9c437-151">Bots</span></span> | <span data-ttu-id="9c437-152">Предварительные просмотры расширения сообщений</span><span class="sxs-lookup"><span data-stu-id="9c437-152">Message extension previews</span></span> | <span data-ttu-id="9c437-153">Результаты расширения сообщений</span><span class="sxs-lookup"><span data-stu-id="9c437-153">Message extension results</span></span> | <span data-ttu-id="9c437-154">Модули задач</span><span class="sxs-lookup"><span data-stu-id="9c437-154">Task modules</span></span> | <span data-ttu-id="9c437-155">Исходяние веб-ок</span><span class="sxs-lookup"><span data-stu-id="9c437-155">Outgoing Webhooks</span></span> | <span data-ttu-id="9c437-156">Входящие веб-окки</span><span class="sxs-lookup"><span data-stu-id="9c437-156">Incoming Webhooks</span></span> | <span data-ttu-id="9c437-157">Соединители O365</span><span class="sxs-lookup"><span data-stu-id="9c437-157">O365 Connectors</span></span> |
| --- | --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="9c437-158">Адаптивная карта</span><span class="sxs-lookup"><span data-stu-id="9c437-158">Adaptive Card</span></span> | <span data-ttu-id="9c437-159">✔</span><span class="sxs-lookup"><span data-stu-id="9c437-159">✔</span></span> | <span data-ttu-id="9c437-160">✖</span><span class="sxs-lookup"><span data-stu-id="9c437-160">✖</span></span> | <span data-ttu-id="9c437-161">✔</span><span class="sxs-lookup"><span data-stu-id="9c437-161">✔</span></span> | <span data-ttu-id="9c437-162">✔</span><span class="sxs-lookup"><span data-stu-id="9c437-162">✔</span></span> | <span data-ttu-id="9c437-163">✔</span><span class="sxs-lookup"><span data-stu-id="9c437-163">✔</span></span> | <span data-ttu-id="9c437-164">✔</span><span class="sxs-lookup"><span data-stu-id="9c437-164">✔</span></span> | <span data-ttu-id="9c437-165">✖</span><span class="sxs-lookup"><span data-stu-id="9c437-165">✖</span></span> |
| <span data-ttu-id="9c437-166">Карта соединители O365</span><span class="sxs-lookup"><span data-stu-id="9c437-166">O365 Connector card</span></span> | <span data-ttu-id="9c437-167">✔</span><span class="sxs-lookup"><span data-stu-id="9c437-167">✔</span></span> | <span data-ttu-id="9c437-168">✖</span><span class="sxs-lookup"><span data-stu-id="9c437-168">✖</span></span> | <span data-ttu-id="9c437-169">✔</span><span class="sxs-lookup"><span data-stu-id="9c437-169">✔</span></span> | <span data-ttu-id="9c437-170">✖</span><span class="sxs-lookup"><span data-stu-id="9c437-170">✖</span></span> | <span data-ttu-id="9c437-171">✔</span><span class="sxs-lookup"><span data-stu-id="9c437-171">✔</span></span> | <span data-ttu-id="9c437-172">✔</span><span class="sxs-lookup"><span data-stu-id="9c437-172">✔</span></span> | <span data-ttu-id="9c437-173">✔</span><span class="sxs-lookup"><span data-stu-id="9c437-173">✔</span></span> |
| <span data-ttu-id="9c437-174">Карта hero</span><span class="sxs-lookup"><span data-stu-id="9c437-174">Hero card</span></span> | <span data-ttu-id="9c437-175">✔</span><span class="sxs-lookup"><span data-stu-id="9c437-175">✔</span></span> | <span data-ttu-id="9c437-176">✔</span><span class="sxs-lookup"><span data-stu-id="9c437-176">✔</span></span> | <span data-ttu-id="9c437-177">✔</span><span class="sxs-lookup"><span data-stu-id="9c437-177">✔</span></span> | <span data-ttu-id="9c437-178">✖</span><span class="sxs-lookup"><span data-stu-id="9c437-178">✖</span></span> | <span data-ttu-id="9c437-179">✔</span><span class="sxs-lookup"><span data-stu-id="9c437-179">✔</span></span> | <span data-ttu-id="9c437-180">✔</span><span class="sxs-lookup"><span data-stu-id="9c437-180">✔</span></span> | <span data-ttu-id="9c437-181">✖</span><span class="sxs-lookup"><span data-stu-id="9c437-181">✖</span></span> |
| <span data-ttu-id="9c437-182">Карта эскиза</span><span class="sxs-lookup"><span data-stu-id="9c437-182">Thumbnail card</span></span> | <span data-ttu-id="9c437-183">✔</span><span class="sxs-lookup"><span data-stu-id="9c437-183">✔</span></span> | <span data-ttu-id="9c437-184">✔</span><span class="sxs-lookup"><span data-stu-id="9c437-184">✔</span></span> | <span data-ttu-id="9c437-185">✔</span><span class="sxs-lookup"><span data-stu-id="9c437-185">✔</span></span> | <span data-ttu-id="9c437-186">✖</span><span class="sxs-lookup"><span data-stu-id="9c437-186">✖</span></span> | <span data-ttu-id="9c437-187">✔</span><span class="sxs-lookup"><span data-stu-id="9c437-187">✔</span></span> | <span data-ttu-id="9c437-188">✔</span><span class="sxs-lookup"><span data-stu-id="9c437-188">✔</span></span> | <span data-ttu-id="9c437-189">✖</span><span class="sxs-lookup"><span data-stu-id="9c437-189">✖</span></span> |
| <span data-ttu-id="9c437-190">Карта списка</span><span class="sxs-lookup"><span data-stu-id="9c437-190">List card</span></span> | <span data-ttu-id="9c437-191">✔</span><span class="sxs-lookup"><span data-stu-id="9c437-191">✔</span></span> | <span data-ttu-id="9c437-192">✖</span><span class="sxs-lookup"><span data-stu-id="9c437-192">✖</span></span> | <span data-ttu-id="9c437-193">✖</span><span class="sxs-lookup"><span data-stu-id="9c437-193">✖</span></span> | <span data-ttu-id="9c437-194">✖</span><span class="sxs-lookup"><span data-stu-id="9c437-194">✖</span></span> | <span data-ttu-id="9c437-195">✔</span><span class="sxs-lookup"><span data-stu-id="9c437-195">✔</span></span> | <span data-ttu-id="9c437-196">✔</span><span class="sxs-lookup"><span data-stu-id="9c437-196">✔</span></span> | <span data-ttu-id="9c437-197">✖</span><span class="sxs-lookup"><span data-stu-id="9c437-197">✖</span></span> |
| <span data-ttu-id="9c437-198">Карта получения</span><span class="sxs-lookup"><span data-stu-id="9c437-198">Receipt card</span></span> | <span data-ttu-id="9c437-199">✔</span><span class="sxs-lookup"><span data-stu-id="9c437-199">✔</span></span> | <span data-ttu-id="9c437-200">✖</span><span class="sxs-lookup"><span data-stu-id="9c437-200">✖</span></span> | <span data-ttu-id="9c437-201">✖</span><span class="sxs-lookup"><span data-stu-id="9c437-201">✖</span></span> | <span data-ttu-id="9c437-202">✖</span><span class="sxs-lookup"><span data-stu-id="9c437-202">✖</span></span> | <span data-ttu-id="9c437-203">✖</span><span class="sxs-lookup"><span data-stu-id="9c437-203">✖</span></span> | <span data-ttu-id="9c437-204">✔</span><span class="sxs-lookup"><span data-stu-id="9c437-204">✔</span></span> | <span data-ttu-id="9c437-205">✖</span><span class="sxs-lookup"><span data-stu-id="9c437-205">✖</span></span> |
| <span data-ttu-id="9c437-206">Карточка Signin</span><span class="sxs-lookup"><span data-stu-id="9c437-206">Signin card</span></span> | <span data-ttu-id="9c437-207">✔</span><span class="sxs-lookup"><span data-stu-id="9c437-207">✔</span></span> | <span data-ttu-id="9c437-208">✖</span><span class="sxs-lookup"><span data-stu-id="9c437-208">✖</span></span> | <span data-ttu-id="9c437-209">✖</span><span class="sxs-lookup"><span data-stu-id="9c437-209">✖</span></span> | <span data-ttu-id="9c437-210">✖</span><span class="sxs-lookup"><span data-stu-id="9c437-210">✖</span></span> | <span data-ttu-id="9c437-211">✖</span><span class="sxs-lookup"><span data-stu-id="9c437-211">✖</span></span> | <span data-ttu-id="9c437-212">✖</span><span class="sxs-lookup"><span data-stu-id="9c437-212">✖</span></span> | <span data-ttu-id="9c437-213">✖</span><span class="sxs-lookup"><span data-stu-id="9c437-213">✖</span></span> |

> [!NOTE]
> <span data-ttu-id="9c437-214">Для адаптивных карт в входящих веб-оках все элементы схемы адаптивной карты, за исключением, `Action.Submit` полностью поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="9c437-214">For Adaptive Cards in Incoming Webhooks, all native Adaptive Card schema elements, except `Action.Submit`, are fully supported.</span></span> <span data-ttu-id="9c437-215">Поддерживаемые действия [**Action.OpenURL,**](https://adaptivecards.io/explorer/Action.OpenUrl.html) [**Action.ShowCard,**](https://adaptivecards.io/explorer/Action.ShowCard.html) [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html)иAction.Exe [**мило**](/adaptive-cards/authoring-cards/universal-action-model#actionexecute).</span><span class="sxs-lookup"><span data-stu-id="9c437-215">The supported actions are [**Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html), [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html), [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html), and [**Action.Execute**](/adaptive-cards/authoring-cards/universal-action-model#actionexecute).</span></span>

## <a name="common-properties-for-all-cards"></a><span data-ttu-id="9c437-216">Общие свойства для всех карт</span><span class="sxs-lookup"><span data-stu-id="9c437-216">Common properties for all cards</span></span>

<span data-ttu-id="9c437-217">Вы можете пройти через некоторые общие свойства, применимые к всем картам.</span><span class="sxs-lookup"><span data-stu-id="9c437-217">You can go through some common properties that are applicable to all cards.</span></span>

### <a name="inline-card-images"></a><span data-ttu-id="9c437-218">Inline card images</span><span class="sxs-lookup"><span data-stu-id="9c437-218">Inline card images</span></span>

<span data-ttu-id="9c437-219">Карта может содержать рядное изображение, включив ссылку на общедоступный образ.</span><span class="sxs-lookup"><span data-stu-id="9c437-219">The card can contain an inline image by including a link to the publicly available image.</span></span> <span data-ttu-id="9c437-220">В целях производительности рекомендуется разогласить изображение в общедоступных сеть доставки содержимого (CDN).</span><span class="sxs-lookup"><span data-stu-id="9c437-220">For performance purposes, it is highly recommended you host the image on a public Content Delivery Network (CDN).</span></span>

<span data-ttu-id="9c437-221">Для поддержания соотношения аспектов для покрытия области изображений масштабы изображения масштабирования или сухую величину.</span><span class="sxs-lookup"><span data-stu-id="9c437-221">Images are scaled up or down in size to maintain the aspect ratio for covering the image area.</span></span> <span data-ttu-id="9c437-222">Затем изображения обрезаются из центра, чтобы достичь соответствующего соотношения аспектов для карты.</span><span class="sxs-lookup"><span data-stu-id="9c437-222">Images are then cropped from center to achieve the appropriate aspect ratio for the card.</span></span>

<span data-ttu-id="9c437-223">Изображения должны быть не более 1024×1024 и в формате PNG, JPEG или GIF.</span><span class="sxs-lookup"><span data-stu-id="9c437-223">Images must be at most 1024×1024 and in PNG, JPEG, or GIF format.</span></span> <span data-ttu-id="9c437-224">Анимированный GIF не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="9c437-224">Animated GIF is not supported.</span></span>

<span data-ttu-id="9c437-225">В следующей таблице ниже огонек содержится следующее:</span><span class="sxs-lookup"><span data-stu-id="9c437-225">The following table provides the properties of inline card images:</span></span>

| <span data-ttu-id="9c437-226">Свойство</span><span class="sxs-lookup"><span data-stu-id="9c437-226">Property</span></span> | <span data-ttu-id="9c437-227">Тип</span><span class="sxs-lookup"><span data-stu-id="9c437-227">Type</span></span>  | <span data-ttu-id="9c437-228">Описание</span><span class="sxs-lookup"><span data-stu-id="9c437-228">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9c437-229">url</span><span class="sxs-lookup"><span data-stu-id="9c437-229">url</span></span> | <span data-ttu-id="9c437-230">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="9c437-230">URL</span></span> | <span data-ttu-id="9c437-231">URL-адрес HTTPS к изображению.</span><span class="sxs-lookup"><span data-stu-id="9c437-231">HTTPS URL to the image.</span></span> |
| <span data-ttu-id="9c437-232">alt</span><span class="sxs-lookup"><span data-stu-id="9c437-232">alt</span></span> | <span data-ttu-id="9c437-233">String</span><span class="sxs-lookup"><span data-stu-id="9c437-233">String</span></span> | <span data-ttu-id="9c437-234">Доступное описание изображения.</span><span class="sxs-lookup"><span data-stu-id="9c437-234">Accessible description of the image.</span></span> |

> [!NOTE]
> <span data-ttu-id="9c437-235">Если карта содержит URL-адрес изображения, перенаправленный перед окончательным изображением, перенаправление URL-адреса изображения не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="9c437-235">If a card includes an image URL that is redirected before the final image, the redirect in image URL is not supported.</span></span> <span data-ttu-id="9c437-236">Это происходит для изображений, общих в общедоступных облаках.</span><span class="sxs-lookup"><span data-stu-id="9c437-236">This occurs for images shared on the public cloud.</span></span>

### <a name="buttons"></a><span data-ttu-id="9c437-237">Кнопки</span><span class="sxs-lookup"><span data-stu-id="9c437-237">Buttons</span></span>

<span data-ttu-id="9c437-238">Кнопки показаны в нижней части карты.</span><span class="sxs-lookup"><span data-stu-id="9c437-238">Buttons are shown stacked at the bottom of the card.</span></span> <span data-ttu-id="9c437-239">Текст кнопки всегда находится в одной строке и усечен, если текст превышает ширину кнопки.</span><span class="sxs-lookup"><span data-stu-id="9c437-239">Button text is always on a single line and is truncated if the text exceeds the button width.</span></span> <span data-ttu-id="9c437-240">Никаких дополнительных кнопок, помимо максимального числа, поддерживаемого картой, не отображается.</span><span class="sxs-lookup"><span data-stu-id="9c437-240">Any additional buttons beyond the maximum number supported by the card are not shown.</span></span>

<span data-ttu-id="9c437-241">Дополнительные сведения см. в [карточных действиях.](~/task-modules-and-cards/cards/cards-actions.md)</span><span class="sxs-lookup"><span data-stu-id="9c437-241">For more information, see [card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

### <a name="card-formatting"></a><span data-ttu-id="9c437-242">Форматирование карт</span><span class="sxs-lookup"><span data-stu-id="9c437-242">Card formatting</span></span>

<span data-ttu-id="9c437-243">Дополнительные сведения о форматирования текста в картах см. [в документе форматирование карт.](~/task-modules-and-cards/cards/cards-format.md)</span><span class="sxs-lookup"><span data-stu-id="9c437-243">For more information on text formatting in cards, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span>

<span data-ttu-id="9c437-244">После определения общих свойств для всех карт теперь можно работать с адаптивными картами, которые помогают повысить вовлеченность и эффективность, добавив свой полезный контент непосредственно в приложения, которые вы используете.</span><span class="sxs-lookup"><span data-stu-id="9c437-244">After identifying the common properties for all cards, you can now work with Adaptive Cards, which help you increase engagement and efficiency by adding your actionable content directly into the apps you use.</span></span>

## <a name="adaptive-card"></a><span data-ttu-id="9c437-245">Адаптивная карта</span><span class="sxs-lookup"><span data-stu-id="9c437-245">Adaptive Card</span></span>

> [!VIDEO https://www.youtube-nocookie.com/embed/J12lKt717Ws]

<span data-ttu-id="9c437-246">Адаптивная карта — это настраиваемая карточка, которая может содержать любое сочетание текстов, речи, изображений, кнопок и полей ввода.</span><span class="sxs-lookup"><span data-stu-id="9c437-246">An Adaptive Card is a customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> <span data-ttu-id="9c437-247">Дополнительные сведения см. в [рублях Адаптивные карты v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span><span class="sxs-lookup"><span data-stu-id="9c437-247">For more information, see [Adaptive Cards v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span></span>

### <a name="support-for-adaptive-cards"></a><span data-ttu-id="9c437-248">Поддержка адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="9c437-248">Support for Adaptive Cards</span></span>

<span data-ttu-id="9c437-249">В следующей таблице представлены функции, поддерживаюющие адаптивные карты:</span><span class="sxs-lookup"><span data-stu-id="9c437-249">The following table provides the features that support Adaptive Cards:</span></span>

| <span data-ttu-id="9c437-250">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="9c437-250">Bots in Teams</span></span> | <span data-ttu-id="9c437-251">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="9c437-251">Messaging extensions</span></span>  | <span data-ttu-id="9c437-252">Соединители</span><span class="sxs-lookup"><span data-stu-id="9c437-252">Connectors</span></span> | <span data-ttu-id="9c437-253">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="9c437-253">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="9c437-254">✔</span><span class="sxs-lookup"><span data-stu-id="9c437-254">✔</span></span> | <span data-ttu-id="9c437-255">✔</span><span class="sxs-lookup"><span data-stu-id="9c437-255">✔</span></span> | <span data-ttu-id="9c437-256">✖</span><span class="sxs-lookup"><span data-stu-id="9c437-256">✖</span></span> | <span data-ttu-id="9c437-257">✔</span><span class="sxs-lookup"><span data-stu-id="9c437-257">✔</span></span> |

> [!NOTE]
> * <span data-ttu-id="9c437-258">Teams поддерживает v1.2 или более ранние функции адаптивной карты.</span><span class="sxs-lookup"><span data-stu-id="9c437-258">Teams platform supports v1.2 or earlier of Adaptive Card features.</span></span>
> * <span data-ttu-id="9c437-259">Положительный или разрушительный стиль действий не поддерживается в адаптивных картах на Teams платформе.</span><span class="sxs-lookup"><span data-stu-id="9c437-259">Positive or destructive action styling is not supported in Adaptive Cards on the Teams platform.</span></span>
> * <span data-ttu-id="9c437-260">Элементы мультимедиа в настоящее время не поддерживаются в адаптивной карте на Teams платформе.</span><span class="sxs-lookup"><span data-stu-id="9c437-260">Media elements are currently not supported in Adaptive Card on the Teams platform.</span></span>

### <a name="example-of-adaptive-card"></a><span data-ttu-id="9c437-261">Пример адаптивной карты</span><span class="sxs-lookup"><span data-stu-id="9c437-261">Example of Adaptive Card</span></span>

![Пример адаптивной карты](~/assets/images/cards/adaptivecard.png)

<span data-ttu-id="9c437-263">В следующем коде показан пример адаптивной карты:</span><span class="sxs-lookup"><span data-stu-id="9c437-263">The following code shows an example of an Adaptive Card:</span></span>

```json
{
  "contentType": "application/vnd.microsoft.card.adaptive",
  "content": {
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "type": "AdaptiveCard",
    "version": "1.0",
    "body": [
      {
        "type": "Container",
        "items": [
          {
            "type": "TextBlock",
            "text": "Publish Adaptive Card schema",
            "weight": "bolder",
            "size": "medium"
          },
          {
            "type": "ColumnSet",
            "columns": [
              {
                "type": "Column",
                "width": "auto",
                "items": [
                  {
                    "type": "Image",
                    "url": "https://pbs.twimg.com/profile_images/3647943215/d7f12830b3c17a5a9e4afcc370e3a37e_400x400.jpeg",
                    "size": "small",
                    "style": "person"
                  }
                ]
              },
              {
                "type": "Column",
                "width": "stretch",
                "items": [
                  {
                    "type": "TextBlock",
                    "text": "Matt Hidinger",
                    "weight": "bolder",
                    "wrap": true
                  },
                  {
                    "type": "TextBlock",
                    "spacing": "none",
                    "text": "Created {{DATE(2017-02-14T06:08:39Z, SHORT)}}",
                    "isSubtle": true,
                    "wrap": true
                  }
                ]
              }
            ]
          }
        ]
      },
      {
        "type": "Container",
        "items": [
          {
            "type": "TextBlock",
            "text": "Now that we have defined the main rules and features of the format, we need to produce a schema and publish it to GitHub. The schema will be the starting point of our reference documentation.",
            "wrap": true
          },
          {
            "type": "FactSet",
            "facts": [
              {
                "title": "Board:",
                "value": "Adaptive Card"
              },
              {
                "title": "List:",
                "value": "Backlog"
              },
              {
                "title": "Assigned to:",
                "value": "Matt Hidinger"
              },
              {
                "title": "Due date:",
                "value": "Not set"
              }
            ]
          }
        ]
      }
    ],
    "actions": [
      {
        "type": "Action.ShowCard",
        "title": "Set due date",
        "card": {
          "type": "AdaptiveCard",
          "body": [
            {
              "type": "Input.Date",
              "id": "dueDate"
            }
          ],
          "actions": [
            {
              "type": "Action.Submit",
              "title": "OK"
            }
          ]
        }
      },
      {
        "type": "Action.ShowCard",
        "title": "Comment",
        "card": {
          "type": "AdaptiveCard",
          "body": [
            {
              "type": "Input.Text",
              "id": "comment",
              "isMultiline": true,
              "placeholder": "Enter your comment"
            }
          ],
          "actions": [
            {
              "type": "Action.Submit",
              "title": "OK"
            }
          ]
        }
      }
    ]
  }  
}
```

#### <a name="additional-information-on-adaptive-cards"></a><span data-ttu-id="9c437-264">Дополнительные сведения о адаптивных картах</span><span class="sxs-lookup"><span data-stu-id="9c437-264">Additional information on Adaptive Cards</span></span>

<span data-ttu-id="9c437-265">Ссылка на Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="9c437-265">Bot Framework reference:</span></span>

* [<span data-ttu-id="9c437-266">Узел адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="9c437-266">Adaptive Cards Node</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)
* [<span data-ttu-id="9c437-267">Адаптивная карта C #</span><span class="sxs-lookup"><span data-stu-id="9c437-267">Adaptive Card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)

<span data-ttu-id="9c437-268">Теперь вы можете работать с картой героя, которая является многоцелевой картой, используемой для визуального выделения потенциального выбора пользователя.</span><span class="sxs-lookup"><span data-stu-id="9c437-268">You can now work with a hero card, which is a multipurpose card used to visually highlight a potential user selection.</span></span>

## <a name="hero-card"></a><span data-ttu-id="9c437-269">Карта hero</span><span class="sxs-lookup"><span data-stu-id="9c437-269">Hero card</span></span>

<span data-ttu-id="9c437-270">Карта, которая обычно содержит одно большое изображение, одну или несколько кнопок и текст.</span><span class="sxs-lookup"><span data-stu-id="9c437-270">A card that typically contains a single large image, one or more buttons, and text.</span></span>

### <a name="support-for-hero-cards"></a><span data-ttu-id="9c437-271">Поддержка карт-героев</span><span class="sxs-lookup"><span data-stu-id="9c437-271">Support for hero cards</span></span>

<span data-ttu-id="9c437-272">В следующей таблице представлены функции, поддерживают карты героев:</span><span class="sxs-lookup"><span data-stu-id="9c437-272">The following table provides the features that support hero cards:</span></span>

| <span data-ttu-id="9c437-273">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="9c437-273">Bots in Teams</span></span> | <span data-ttu-id="9c437-274">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="9c437-274">Messaging extensions</span></span>  | <span data-ttu-id="9c437-275">Соединители</span><span class="sxs-lookup"><span data-stu-id="9c437-275">Connectors</span></span> | <span data-ttu-id="9c437-276">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="9c437-276">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="9c437-277">✔</span><span class="sxs-lookup"><span data-stu-id="9c437-277">✔</span></span> | <span data-ttu-id="9c437-278">✔</span><span class="sxs-lookup"><span data-stu-id="9c437-278">✔</span></span> | <span data-ttu-id="9c437-279">✖</span><span class="sxs-lookup"><span data-stu-id="9c437-279">✖</span></span> | <span data-ttu-id="9c437-280">✔</span><span class="sxs-lookup"><span data-stu-id="9c437-280">✔</span></span> |

### <a name="properties-of-a-hero-card"></a><span data-ttu-id="9c437-281">Свойства карты-героя</span><span class="sxs-lookup"><span data-stu-id="9c437-281">Properties of a hero card</span></span>

<span data-ttu-id="9c437-282">В следующей таблице огосяты свойства карточки героя:</span><span class="sxs-lookup"><span data-stu-id="9c437-282">The following table provides the properties of a hero card:</span></span>

| <span data-ttu-id="9c437-283">Свойство</span><span class="sxs-lookup"><span data-stu-id="9c437-283">Property</span></span> | <span data-ttu-id="9c437-284">Тип</span><span class="sxs-lookup"><span data-stu-id="9c437-284">Type</span></span>  | <span data-ttu-id="9c437-285">Описание</span><span class="sxs-lookup"><span data-stu-id="9c437-285">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9c437-286">title</span><span class="sxs-lookup"><span data-stu-id="9c437-286">title</span></span> | <span data-ttu-id="9c437-287">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="9c437-287">Rich text</span></span> | <span data-ttu-id="9c437-288">Название карты.</span><span class="sxs-lookup"><span data-stu-id="9c437-288">Title of the card.</span></span> <span data-ttu-id="9c437-289">Максимум две строки.</span><span class="sxs-lookup"><span data-stu-id="9c437-289">Maximum two lines.</span></span> |
| <span data-ttu-id="9c437-290">субтитры</span><span class="sxs-lookup"><span data-stu-id="9c437-290">subtitle</span></span> | <span data-ttu-id="9c437-291">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="9c437-291">Rich text</span></span> | <span data-ttu-id="9c437-292">Субтитр карты.</span><span class="sxs-lookup"><span data-stu-id="9c437-292">Subtitle of the card.</span></span> <span data-ttu-id="9c437-293">Максимум две строки.</span><span class="sxs-lookup"><span data-stu-id="9c437-293">Maximum two lines.</span></span>|
| <span data-ttu-id="9c437-294">текст</span><span class="sxs-lookup"><span data-stu-id="9c437-294">text</span></span> | <span data-ttu-id="9c437-295">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="9c437-295">Rich text</span></span> | <span data-ttu-id="9c437-296">Текст отображается под субтитром.</span><span class="sxs-lookup"><span data-stu-id="9c437-296">Text appears under the subtitle.</span></span> <span data-ttu-id="9c437-297">Параметры форматирования см. [в виде форматирования карт.](~/task-modules-and-cards/cards/cards-format.md)</span><span class="sxs-lookup"><span data-stu-id="9c437-297">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="9c437-298">изображения</span><span class="sxs-lookup"><span data-stu-id="9c437-298">images</span></span> | <span data-ttu-id="9c437-299">Массив изображений</span><span class="sxs-lookup"><span data-stu-id="9c437-299">Array of images</span></span> | <span data-ttu-id="9c437-300">Изображение, отображаемого в верхней части карты.</span><span class="sxs-lookup"><span data-stu-id="9c437-300">Image displayed at the top of the card.</span></span> <span data-ttu-id="9c437-301">Соотношение аспектов 16:9.</span><span class="sxs-lookup"><span data-stu-id="9c437-301">Aspect ratio 16:9.</span></span> |
| <span data-ttu-id="9c437-302">кнопки</span><span class="sxs-lookup"><span data-stu-id="9c437-302">buttons</span></span> | <span data-ttu-id="9c437-303">Массив объектов действий</span><span class="sxs-lookup"><span data-stu-id="9c437-303">Array of action objects</span></span> | <span data-ttu-id="9c437-304">Набор действий, применимых к текущей карте.</span><span class="sxs-lookup"><span data-stu-id="9c437-304">Set of actions applicable to the current card.</span></span> <span data-ttu-id="9c437-305">Максимум шесть.</span><span class="sxs-lookup"><span data-stu-id="9c437-305">Maximum six.</span></span> |
| <span data-ttu-id="9c437-306">нажмите кнопку</span><span class="sxs-lookup"><span data-stu-id="9c437-306">tap</span></span> | <span data-ttu-id="9c437-307">Объект Action</span><span class="sxs-lookup"><span data-stu-id="9c437-307">Action object</span></span> | <span data-ttu-id="9c437-308">Активируется при нажатии на карточку самого пользователя.</span><span class="sxs-lookup"><span data-stu-id="9c437-308">Activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-hero-card"></a><span data-ttu-id="9c437-309">Пример карточки героя</span><span class="sxs-lookup"><span data-stu-id="9c437-309">Example of a hero card</span></span>

![Пример карточки героя](~/assets/images/cards/hero.png)

<span data-ttu-id="9c437-311">В следующем коде показан пример карты героя:</span><span class="sxs-lookup"><span data-stu-id="9c437-311">The following code shows an example of a hero card:</span></span>

```json
{
   "contentType": "application/vnd.microsoft.card.hero",
   "content": {
     "title": "Seattle Center Monorail",
     "subtitle": "Seattle Center Monorail",
     "text": "The Seattle Center Monorail is an elevated train line between Seattle Center (near the Space Needle) and downtown Seattle. It was built for the 1962 World's Fair. Its original two trains, completed in 1961, are still in service.",
     "images": [
       {
         "url":"https://upload.wikimedia.org/wikipedia/commons/thumb/4/49/Seattle_monorail01_2008-02-25.jpg/1024px-Seattle_monorail01_2008-02-25.jpg"
       }
     ],
    "buttons": [
      {
         "type": "openUrl",
         "title": "Official website",
         "value": "https://www.seattlemonorail.com"
       },
      {
        "type": "openUrl",
        "title": "Wikipeda page",
        "value": "https://en.wikipedia.org/wiki/Seattle_Center_Monorail"
       }
     ]
   }
}

```

### <a name="additional-information-on-hero-cards"></a><span data-ttu-id="9c437-312">Дополнительные сведения о картах-героях</span><span class="sxs-lookup"><span data-stu-id="9c437-312">Additional information on hero cards</span></span>

<span data-ttu-id="9c437-313">Ссылка на Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="9c437-313">Bot Framework reference:</span></span>

* [<span data-ttu-id="9c437-314">Карточка героя Node.js</span><span class="sxs-lookup"><span data-stu-id="9c437-314">Hero card Node.js</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-a-hero-card&preserve-view=true)
* [<span data-ttu-id="9c437-315">Карта героя C #</span><span class="sxs-lookup"><span data-stu-id="9c437-315">Hero card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-hero-card&preserve-view=true)

## <a name="list-card"></a><span data-ttu-id="9c437-316">Карта списка</span><span class="sxs-lookup"><span data-stu-id="9c437-316">List card</span></span>

<span data-ttu-id="9c437-317">Карта списка была добавлена Teams для предоставления функций, которые не могут предоставляться в коллекции списков.</span><span class="sxs-lookup"><span data-stu-id="9c437-317">The list card has been added by Teams to provide functions beyond what the list collection can provide.</span></span> <span data-ttu-id="9c437-318">Карта списка содержит список элементов для прокрутки.</span><span class="sxs-lookup"><span data-stu-id="9c437-318">The list card provides a scrolling list of items.</span></span>

### <a name="support-for-list-cards"></a><span data-ttu-id="9c437-319">Поддержка карт списка</span><span class="sxs-lookup"><span data-stu-id="9c437-319">Support for list cards</span></span>

<span data-ttu-id="9c437-320">В следующей таблице представлены функции, поддерживают карты списков:</span><span class="sxs-lookup"><span data-stu-id="9c437-320">The following table provides the features that support list cards:</span></span>

| <span data-ttu-id="9c437-321">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="9c437-321">Bots in Teams</span></span> | <span data-ttu-id="9c437-322">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="9c437-322">Messaging extensions</span></span>  | <span data-ttu-id="9c437-323">Соединители</span><span class="sxs-lookup"><span data-stu-id="9c437-323">Connectors</span></span> | <span data-ttu-id="9c437-324">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="9c437-324">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="9c437-325">✔</span><span class="sxs-lookup"><span data-stu-id="9c437-325">✔</span></span> | <span data-ttu-id="9c437-326">✖</span><span class="sxs-lookup"><span data-stu-id="9c437-326">✖</span></span> | <span data-ttu-id="9c437-327">✖</span><span class="sxs-lookup"><span data-stu-id="9c437-327">✖</span></span> |<span data-ttu-id="9c437-328">✔</span><span class="sxs-lookup"><span data-stu-id="9c437-328">✔</span></span> |

### <a name="properties-of-a-list-card"></a><span data-ttu-id="9c437-329">Свойства карты списка</span><span class="sxs-lookup"><span data-stu-id="9c437-329">Properties of a list card</span></span>

<span data-ttu-id="9c437-330">Следующая таблица содержит свойства карты списка:</span><span class="sxs-lookup"><span data-stu-id="9c437-330">The following table provides the properties of a list card:</span></span>

| <span data-ttu-id="9c437-331">Свойство</span><span class="sxs-lookup"><span data-stu-id="9c437-331">Property</span></span> | <span data-ttu-id="9c437-332">Тип</span><span class="sxs-lookup"><span data-stu-id="9c437-332">Type</span></span>  | <span data-ttu-id="9c437-333">Описание</span><span class="sxs-lookup"><span data-stu-id="9c437-333">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9c437-334">title</span><span class="sxs-lookup"><span data-stu-id="9c437-334">title</span></span> | <span data-ttu-id="9c437-335">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="9c437-335">Rich text</span></span> | <span data-ttu-id="9c437-336">Название карты.</span><span class="sxs-lookup"><span data-stu-id="9c437-336">Title of the card.</span></span> <span data-ttu-id="9c437-337">Максимум 2 строки.</span><span class="sxs-lookup"><span data-stu-id="9c437-337">Maximum 2 lines.</span></span>|
| <span data-ttu-id="9c437-338">элементы</span><span class="sxs-lookup"><span data-stu-id="9c437-338">items</span></span> | <span data-ttu-id="9c437-339">Массив элементов списка</span><span class="sxs-lookup"><span data-stu-id="9c437-339">Array of list items</span></span> | <span data-ttu-id="9c437-340">Набор элементов, применимых к карте.</span><span class="sxs-lookup"><span data-stu-id="9c437-340">Set of items applicable to the card.</span></span>|
| <span data-ttu-id="9c437-341">кнопки</span><span class="sxs-lookup"><span data-stu-id="9c437-341">buttons</span></span> | <span data-ttu-id="9c437-342">Массив объектов действий</span><span class="sxs-lookup"><span data-stu-id="9c437-342">Array of action objects</span></span> | <span data-ttu-id="9c437-343">Набор действий, применимых к текущей карте.</span><span class="sxs-lookup"><span data-stu-id="9c437-343">Set of actions applicable to the current card.</span></span> <span data-ttu-id="9c437-344">Максимум 6.</span><span class="sxs-lookup"><span data-stu-id="9c437-344">Maximum 6.</span></span> |

### <a name="example-of-a-list-card"></a><span data-ttu-id="9c437-345">Пример карты списка</span><span class="sxs-lookup"><span data-stu-id="9c437-345">Example of a list card</span></span>

<span data-ttu-id="9c437-346">В следующем коде показан пример карты списка:</span><span class="sxs-lookup"><span data-stu-id="9c437-346">The following code shows an example of a list card:</span></span>

```json
{
  "contentType": "application/vnd.microsoft.teams.card.list",
  "content": {
    "title": "Card title",
    "items": [
      {
        "type": "file",
        "id": "https://contoso.sharepoint.com/teams/new/Shared%20Documents/Report.xlsx",
        "title": "Report",
        "subtitle": "teams > new > design",
        "tap": {
          "type": "imBack",
          "value": "editOnline https://contoso.sharepoint.com/teams/new/Shared%20Documents/Report.xlsx"
        }
      },
      {
        "type": "resultItem",
        "icon": "https://cdn2.iconfinder.com/data/icons/social-icons-33/128/Trello-128.png",
        "title": "Trello title",
        "subtitle": "A Trello subtitle",
        "tap": {
          "type": "openUrl",
          "value": "http://trello.com"
        }
      },
      {
        "type": "section",
        "title": "Manager"
      },
      {
        "type": "person",
        "id": "JohnDoe@contoso.com",
        "title": "John Doe",
        "subtitle": "Manager",
        "tap": {
          "type": "imBack",
          "value": "whois JohnDoe@contoso.com"
        }
      }
    ],
    "buttons": [
      {
        "type": "imBack",
        "title": "Select",
        "value": "whois"
      }
    ]
  }
}
```

## <a name="office-365-connector-card"></a><span data-ttu-id="9c437-347">Office 365 соединители</span><span class="sxs-lookup"><span data-stu-id="9c437-347">Office 365 connector card</span></span>

<span data-ttu-id="9c437-348">Вы можете работать с Office 365 connector, которая обеспечивает гибкий макет и это отличный способ получения полезной информации.</span><span class="sxs-lookup"><span data-stu-id="9c437-348">You can work with an Office 365 Connector card that provides a flexible layout and is a great way to get useful information.</span></span> <span data-ttu-id="9c437-349">Соедините Office 365 поддерживается в Teams, а не в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="9c437-349">The Office 365 connector card is supported in Teams, not in Bot Framework.</span></span> <span data-ttu-id="9c437-350">Эта карта обеспечивает гибкую схему с несколькими разделами, полями, изображениями и действиями.</span><span class="sxs-lookup"><span data-stu-id="9c437-350">This card provides a flexible layout with multiple sections, fields, images, and actions.</span></span> <span data-ttu-id="9c437-351">Эта карта содержит соединителивую карту, чтобы она была использована ботами.</span><span class="sxs-lookup"><span data-stu-id="9c437-351">This card contains a connector card so that it can be used by bots.</span></span> <span data-ttu-id="9c437-352">О различиях между соединитеными картами и Office 365 соединитетелем см. в дополнительных сведениях о Office 365 [соединители.](#additional-information-on-the-office-365-connector-card)</span><span class="sxs-lookup"><span data-stu-id="9c437-352">For differences between connector cards and the Office 365 Connector card, see [Additional information on the Office 365 Connector card](#additional-information-on-the-office-365-connector-card).</span></span>

### <a name="support-for-office-365-connector-cards"></a><span data-ttu-id="9c437-353">Поддержка Office 365 соединители</span><span class="sxs-lookup"><span data-stu-id="9c437-353">Support for Office 365 Connector cards</span></span>

<span data-ttu-id="9c437-354">В следующей таблице представлены функции, поддерживают Office 365 соединители:</span><span class="sxs-lookup"><span data-stu-id="9c437-354">The following table provides the features that support Office 365 Connector cards:</span></span>

| <span data-ttu-id="9c437-355">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="9c437-355">Bots in Teams</span></span> | <span data-ttu-id="9c437-356">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="9c437-356">Messaging extensions</span></span>  | <span data-ttu-id="9c437-357">Соединители</span><span class="sxs-lookup"><span data-stu-id="9c437-357">Connectors</span></span> | <span data-ttu-id="9c437-358">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="9c437-358">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="9c437-359">✔</span><span class="sxs-lookup"><span data-stu-id="9c437-359">✔</span></span> | <span data-ttu-id="9c437-360">✔</span><span class="sxs-lookup"><span data-stu-id="9c437-360">✔</span></span> | <span data-ttu-id="9c437-361">✔</span><span class="sxs-lookup"><span data-stu-id="9c437-361">✔</span></span> | <span data-ttu-id="9c437-362">✖</span><span class="sxs-lookup"><span data-stu-id="9c437-362">✖</span></span> |

### <a name="properties-of-the-office-365-connector-card"></a><span data-ttu-id="9c437-363">Свойства карты Office 365 соединители</span><span class="sxs-lookup"><span data-stu-id="9c437-363">Properties of the Office 365 Connector card</span></span>

<span data-ttu-id="9c437-364">В следующей таблице ниже огосяты свойства Office 365 соединители:</span><span class="sxs-lookup"><span data-stu-id="9c437-364">The following table provides the properties of the Office 365 connector card:</span></span>

| <span data-ttu-id="9c437-365">Свойство</span><span class="sxs-lookup"><span data-stu-id="9c437-365">Property</span></span> | <span data-ttu-id="9c437-366">Тип</span><span class="sxs-lookup"><span data-stu-id="9c437-366">Type</span></span>  | <span data-ttu-id="9c437-367">Описание</span><span class="sxs-lookup"><span data-stu-id="9c437-367">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9c437-368">title</span><span class="sxs-lookup"><span data-stu-id="9c437-368">title</span></span> | <span data-ttu-id="9c437-369">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="9c437-369">Rich text</span></span> | <span data-ttu-id="9c437-370">Название карты.</span><span class="sxs-lookup"><span data-stu-id="9c437-370">Title of the card.</span></span> <span data-ttu-id="9c437-371">Максимум две строки.</span><span class="sxs-lookup"><span data-stu-id="9c437-371">Maximum two lines.</span></span> |
| <span data-ttu-id="9c437-372">summary</span><span class="sxs-lookup"><span data-stu-id="9c437-372">summary</span></span> | <span data-ttu-id="9c437-373">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="9c437-373">Rich text</span></span> | <span data-ttu-id="9c437-374">Сводка карты.</span><span class="sxs-lookup"><span data-stu-id="9c437-374">Summary of the card.</span></span> <span data-ttu-id="9c437-375">Максимум две строки.</span><span class="sxs-lookup"><span data-stu-id="9c437-375">Maximum two lines.</span></span> |
| <span data-ttu-id="9c437-376">текст</span><span class="sxs-lookup"><span data-stu-id="9c437-376">text</span></span> | <span data-ttu-id="9c437-377">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="9c437-377">Rich text</span></span> | <span data-ttu-id="9c437-378">Текст отображается под субтитром.</span><span class="sxs-lookup"><span data-stu-id="9c437-378">Text appears under the subtitle.</span></span> <span data-ttu-id="9c437-379">Параметры форматирования см. [в виде форматирования карт.](~/task-modules-and-cards/cards/cards-format.md)</span><span class="sxs-lookup"><span data-stu-id="9c437-379">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="9c437-380">themeColor</span><span class="sxs-lookup"><span data-stu-id="9c437-380">themeColor</span></span> | <span data-ttu-id="9c437-381">Строка HEX</span><span class="sxs-lookup"><span data-stu-id="9c437-381">HEX string</span></span> | <span data-ttu-id="9c437-382">Цвет, который `accentColor` переопределяет предоставленные из манифеста приложения.</span><span class="sxs-lookup"><span data-stu-id="9c437-382">Color that overrides the `accentColor` provided from the application manifest.</span></span> |

### <a name="additional-information-on-the-office-365-connector-card"></a><span data-ttu-id="9c437-383">Дополнительные сведения о Office 365 соединители</span><span class="sxs-lookup"><span data-stu-id="9c437-383">Additional information on the Office 365 Connector card</span></span>

<span data-ttu-id="9c437-384">Office 365 Соединитетельные карты правильно функционируют в Microsoft Teams, включая [ `ActionCard` действия.](/outlook/actionable-messages/card-reference#actioncard-action)</span><span class="sxs-lookup"><span data-stu-id="9c437-384">Office 365 Connector cards function properly in Microsoft Teams, including [`ActionCard` actions](/outlook/actionable-messages/card-reference#actioncard-action).</span></span>

<span data-ttu-id="9c437-385">Важное отличие между использованием соединитеных карт из соединитетеля и использованием соединитеных карт в боте — обработка действий карт.</span><span class="sxs-lookup"><span data-stu-id="9c437-385">The important difference between using connector cards from a connector and using connector cards in your bot is the handling of card actions.</span></span> <span data-ttu-id="9c437-386">В следующей таблице перечислены различия:</span><span class="sxs-lookup"><span data-stu-id="9c437-386">The following table lists the difference:</span></span>

| <span data-ttu-id="9c437-387">Connector</span><span class="sxs-lookup"><span data-stu-id="9c437-387">Connector</span></span> | <span data-ttu-id="9c437-388">Bot</span><span class="sxs-lookup"><span data-stu-id="9c437-388">Bot</span></span> |
| --- | --- |
| <span data-ttu-id="9c437-389">Конечная точка получает полезной нагрузки карточки через HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="9c437-389">The endpoint receives the card payload through HTTP POST.</span></span> | <span data-ttu-id="9c437-390">Действие запускает действие, которое отправляет боту только ID действия `HttpPOST` `invoke` и тело.</span><span class="sxs-lookup"><span data-stu-id="9c437-390">The `HttpPOST` action triggers an `invoke` activity that sends only the action ID and body to the bot.</span></span>|

<span data-ttu-id="9c437-391">Каждая соединитечная карта может отображать не более десяти разделов, а каждый раздел может содержать не более пяти изображений и пять действий.</span><span class="sxs-lookup"><span data-stu-id="9c437-391">Each connector card can display a maximum of ten sections, and each section can contain a maximum of five images and five actions.</span></span>

> [!NOTE]
> <span data-ttu-id="9c437-392">Дополнительные разделы, изображения или действия в сообщении не отображаются.</span><span class="sxs-lookup"><span data-stu-id="9c437-392">Any additional sections, images, or actions in a message do not appear.</span></span>

<span data-ttu-id="9c437-393">Все текстовые поля поддерживают Markdown и HTML.</span><span class="sxs-lookup"><span data-stu-id="9c437-393">All text fields support Markdown and HTML.</span></span> <span data-ttu-id="9c437-394">Вы можете контролировать, какие разделы используют Markdown или HTML, установив `markdown` свойство в сообщении.</span><span class="sxs-lookup"><span data-stu-id="9c437-394">You can control which sections use Markdown or HTML by setting the `markdown` property in a message.</span></span> <span data-ttu-id="9c437-395">По умолчанию `markdown` установлено `true` значение .</span><span class="sxs-lookup"><span data-stu-id="9c437-395">By default, `markdown` is set to `true`.</span></span> <span data-ttu-id="9c437-396">Если вы хотите использовать HTML вместо этого, установите `markdown` `false` .</span><span class="sxs-lookup"><span data-stu-id="9c437-396">If you want to use HTML instead, set `markdown` to `false`.</span></span>

<span data-ttu-id="9c437-397">Если указать `themeColor` свойство, оно переопределит `accentColor` свойство в манифесте приложения.</span><span class="sxs-lookup"><span data-stu-id="9c437-397">If you specify the `themeColor` property, it overrides the `accentColor` property in the app manifest.</span></span>

<span data-ttu-id="9c437-398">Чтобы указать стиль визуализации, можно задать, `activityImage` `activityImageType` как показано в следующей таблице:</span><span class="sxs-lookup"><span data-stu-id="9c437-398">To specify the rendering style for `activityImage`, you can set `activityImageType` as shown in the following table:</span></span>

| <span data-ttu-id="9c437-399">Значение</span><span class="sxs-lookup"><span data-stu-id="9c437-399">Value</span></span> | <span data-ttu-id="9c437-400">Описание</span><span class="sxs-lookup"><span data-stu-id="9c437-400">Description</span></span> |
| --- | --- |
| `avatar` | <span data-ttu-id="9c437-401">По умолчанию `activityImage` обрезается как круг.</span><span class="sxs-lookup"><span data-stu-id="9c437-401">Default, `activityImage` is cropped as a circle.</span></span> |
| `article` | <span data-ttu-id="9c437-402">`activityImage` отображается в качестве прямоугольника и сохраняет отношение аспектов.</span><span class="sxs-lookup"><span data-stu-id="9c437-402">`activityImage` is displayed as a rectangle and retains its aspect ratio.</span></span> |

<span data-ttu-id="9c437-403">Другие сведения о свойствах карт соединители см. в справке к карточкам [сообщений.](/outlook/actionable-messages/card-reference)</span><span class="sxs-lookup"><span data-stu-id="9c437-403">For all other details about connector card properties, see [actionable message card reference](/outlook/actionable-messages/card-reference).</span></span> <span data-ttu-id="9c437-404">Единственными свойствами карт соединители, Teams которые в настоящее время не поддерживаются, являются следующими:</span><span class="sxs-lookup"><span data-stu-id="9c437-404">The only connector card properties that Teams does not currently support are as follows:</span></span>

* `heroImage`
* `hideOriginalBody`
* <span data-ttu-id="9c437-405">`startGroup`всегда рассматривается как `true` в Teams</span><span class="sxs-lookup"><span data-stu-id="9c437-405">`startGroup` always treated as `true` in Teams</span></span>
* `originator`
* `correlationId`

### <a name="example-of-an-office-365-connector-card"></a><span data-ttu-id="9c437-406">Пример карты Office 365 соединители</span><span class="sxs-lookup"><span data-stu-id="9c437-406">Example of an Office 365 Connector card</span></span>

<span data-ttu-id="9c437-407">В следующем коде показан пример карты Office 365 соединители:</span><span class="sxs-lookup"><span data-stu-id="9c437-407">The following code shows an example of an Office 365 Connector card:</span></span>

```json
{
  "contentType": "application/vnd.microsoft.teams.card.o365connector",
  "content": {
    "@type": "MessageCard",
    "@context": "http://schema.org/extensions",
    "summary": "John Doe commented on Trello",
    "title": "Project Tango",
    "sections": [
        {
            "activityTitle": "John Doe commented",
            "activitySubtitle": "On Project Tango",
            "activityText": "\"Here are the designs\"",
            "activityImage": "http://connectorsdemo.azurewebsites.net/images/MSC12_Oscar_002.jpg"
        },
        {
            "title": "Details",
            "facts": [
                {
                    "name": "Labels",
                    "value": "Designs, redlines"
                },
                {
                    "name": "Due date",
                    "value": "Dec 7, 2016"
                },
                {
                    "name": "Attachments",
                    "value": "[final.jpg](http://connectorsdemo.azurewebsites.net/images/WIN14_Jan_04.jpg)"
                }
            ]
        },
        {
            "title": "Images",
            "images": [
                {
                    "image":"http://connectorsdemo.azurewebsites.net/images/MicrosoftSurface_024_Cafe_OH-06315_VS_R1c.jpg"
                },
                {
                    "image":"http://connectorsdemo.azurewebsites.net/images/WIN12_Scene_01.jpg"
                },
                {
                    "image":"http://connectorsdemo.azurewebsites.net/images/WIN12_Anthony_02.jpg"
                }
            ]
        }
    ],
    "potentialAction": [
        {
            "@context": "http://schema.org",
            "@type": "ViewAction",
            "name": "View in Trello",
            "target": [
                "https://trello.com/c/1101/"
            ]
        }
    ]
  }
}
```

## <a name="receipt-card"></a><span data-ttu-id="9c437-408">Карта получения</span><span class="sxs-lookup"><span data-stu-id="9c437-408">Receipt card</span></span>

<span data-ttu-id="9c437-409">Teams поддерживает карточку получения.</span><span class="sxs-lookup"><span data-stu-id="9c437-409">Teams supports receipt card.</span></span> <span data-ttu-id="9c437-410">Это карточка, которая позволяет боту предоставлять пользователю квитанцию.</span><span class="sxs-lookup"><span data-stu-id="9c437-410">It is a card that enables a bot to provide a receipt to the user.</span></span> <span data-ttu-id="9c437-411">Обычно он содержит список элементов, которые необходимо включить в квитанцию, например налоговые и общие сведения.</span><span class="sxs-lookup"><span data-stu-id="9c437-411">It typically contains the list of items to include on the receipt, such as tax and total information.</span></span>

### <a name="support-for-receipt-cards"></a><span data-ttu-id="9c437-412">Поддержка карт получения</span><span class="sxs-lookup"><span data-stu-id="9c437-412">Support for receipt cards</span></span>

<span data-ttu-id="9c437-413">В следующей таблице представлены функции, поддерживают карты получения:</span><span class="sxs-lookup"><span data-stu-id="9c437-413">The following table provides the features that support receipt cards:</span></span>

| <span data-ttu-id="9c437-414">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="9c437-414">Bots in Teams</span></span> | <span data-ttu-id="9c437-415">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="9c437-415">Messaging extensions</span></span>  | <span data-ttu-id="9c437-416">Соединители</span><span class="sxs-lookup"><span data-stu-id="9c437-416">Connectors</span></span> | <span data-ttu-id="9c437-417">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="9c437-417">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="9c437-418">✔</span><span class="sxs-lookup"><span data-stu-id="9c437-418">✔</span></span> | <span data-ttu-id="9c437-419">✔</span><span class="sxs-lookup"><span data-stu-id="9c437-419">✔</span></span> | <span data-ttu-id="9c437-420">✖</span><span class="sxs-lookup"><span data-stu-id="9c437-420">✖</span></span> | <span data-ttu-id="9c437-421">✔</span><span class="sxs-lookup"><span data-stu-id="9c437-421">✔</span></span> |

### <a name="example-of-a-receipt-card"></a><span data-ttu-id="9c437-422">Пример карты получения</span><span class="sxs-lookup"><span data-stu-id="9c437-422">Example of a receipt card</span></span>

![Пример карты получения](~/assets/images/cards/receipt.png)

<span data-ttu-id="9c437-424">В следующем коде показан пример карточки получения:</span><span class="sxs-lookup"><span data-stu-id="9c437-424">The following code shows an example of a receipt card:</span></span>

```json
{
  "contentType": "application/vnd.microsoft.card.receipt",
  "content": {
    "title": "John Doe",
    "facts": [
      {
        "key": "Order Number",
        "value": "1234"
      },
      {
        "key": "Payment Method",
        "value": "VISA 5555-****"
      }
    ],
    "items": [
      {
        "title": "Data Transfer",
        "image": {
          "url": "https://github.com/amido/azure-vector-icons/raw/master/renders/traffic-manager.png"
        },
        "price": "$ 38.45",
        "quantity": "368"
      },
      {
        "title": "App Service",
        "image": {
          "url": "https://github.com/amido/azure-vector-icons/raw/master/renders/cloud-service.png"
        },
        "price": "$ 45.00",
        "quantity": "720"
      }
    ],
    "total": "$ 90.95",
    "tax": "$ 7.50",
    "buttons": [
      {
        "type": "openUrl",
        "title": "More information",
        "image": "https://account.windowsazure.com/content/6.10.1.38-.8225.160809-1618/aux-pre/images/offer-icon-freetrial.png",
        "value": "https://azure.microsoft.com/en-us/pricing/"
      }
    ]
  }
}
```

### <a name="additional-information-on-receipt-cards"></a><span data-ttu-id="9c437-425">Дополнительные сведения о карточках получения</span><span class="sxs-lookup"><span data-stu-id="9c437-425">Additional information on receipt cards</span></span>

<span data-ttu-id="9c437-426">Ссылка на Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="9c437-426">Bot Framework reference:</span></span>

* [<span data-ttu-id="9c437-427">Карточка получения Node.js</span><span class="sxs-lookup"><span data-stu-id="9c437-427">Receipt card Node.js</span></span>](/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="9c437-428">Карта получения C #</span><span class="sxs-lookup"><span data-stu-id="9c437-428">Receipt card C#</span></span>](/dotnet/api/microsoft.bot.schema.receiptcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="signin-card"></a><span data-ttu-id="9c437-429">Карточка Signin</span><span class="sxs-lookup"><span data-stu-id="9c437-429">Signin card</span></span>

<span data-ttu-id="9c437-430">Карта signin в Teams похожа на карточку signin в Bot Framework, за исключением того, что карта signin в Teams поддерживает только два действия `signin` и `openUrl` .</span><span class="sxs-lookup"><span data-stu-id="9c437-430">The signin card in Teams is similar to the signin card in the Bot Framework except that the signin card in Teams only supports two actions `signin` and `openUrl`.</span></span>

<span data-ttu-id="9c437-431">Действие signin можно использовать с любой карты в Teams, а не только с карты signin.</span><span class="sxs-lookup"><span data-stu-id="9c437-431">The signin action can be used from any card in Teams, not just the signin card.</span></span> <span data-ttu-id="9c437-432">Дополнительные сведения см. [в Teams поток проверки подлинности для ботов.](~/bots/how-to/authentication/auth-flow-bot.md)</span><span class="sxs-lookup"><span data-stu-id="9c437-432">For more information, see [Teams authentication flow for bots](~/bots/how-to/authentication/auth-flow-bot.md).</span></span>

### <a name="support-for-signin-cards"></a><span data-ttu-id="9c437-433">Поддержка подписных карт</span><span class="sxs-lookup"><span data-stu-id="9c437-433">Support for signin cards</span></span>

<span data-ttu-id="9c437-434">В следующей таблице представлены функции, поддерживают знаковые карточки:</span><span class="sxs-lookup"><span data-stu-id="9c437-434">The following table provides the features that support signin cards:</span></span>

| <span data-ttu-id="9c437-435">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="9c437-435">Bots in Teams</span></span> | <span data-ttu-id="9c437-436">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="9c437-436">Messaging extensions</span></span>  | <span data-ttu-id="9c437-437">Соединители</span><span class="sxs-lookup"><span data-stu-id="9c437-437">Connectors</span></span> | <span data-ttu-id="9c437-438">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="9c437-438">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="9c437-439">✔</span><span class="sxs-lookup"><span data-stu-id="9c437-439">✔</span></span> | <span data-ttu-id="9c437-440">✖</span><span class="sxs-lookup"><span data-stu-id="9c437-440">✖</span></span> | <span data-ttu-id="9c437-441">✖</span><span class="sxs-lookup"><span data-stu-id="9c437-441">✖</span></span> | <span data-ttu-id="9c437-442">✔</span><span class="sxs-lookup"><span data-stu-id="9c437-442">✔</span></span> |

### <a name="additional-information-on-signin-cards"></a><span data-ttu-id="9c437-443">Дополнительные сведения о подписных карточках</span><span class="sxs-lookup"><span data-stu-id="9c437-443">Additional information on signin cards</span></span>

<span data-ttu-id="9c437-444">Ссылка на Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="9c437-444">Bot Framework reference:</span></span>

* [<span data-ttu-id="9c437-445">Карточка signin Node.js</span><span class="sxs-lookup"><span data-stu-id="9c437-445">Signin card Node.js</span></span>](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="9c437-446">Signin card C #</span><span class="sxs-lookup"><span data-stu-id="9c437-446">Signin card C#</span></span>](/dotnet/api/microsoft.bot.schema.signincard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="thumbnail-card"></a><span data-ttu-id="9c437-447">Карта эскиза</span><span class="sxs-lookup"><span data-stu-id="9c437-447">Thumbnail card</span></span>

<span data-ttu-id="9c437-448">Вы можете работать с картой эскизов, которая используется для отправки простого действия сообщения.</span><span class="sxs-lookup"><span data-stu-id="9c437-448">You can work with a thumbnail card that is used for sending a simple actionable message.</span></span> <span data-ttu-id="9c437-449">Карточка, которая обычно содержит одно изображение эскиза, одну или несколько кнопок и текст.</span><span class="sxs-lookup"><span data-stu-id="9c437-449">A card that typically contains a single thumbnail image, one or more buttons, and text.</span></span>

### <a name="support-for-thumbnail-cards"></a><span data-ttu-id="9c437-450">Поддержка карт эскизов</span><span class="sxs-lookup"><span data-stu-id="9c437-450">Support for thumbnail cards</span></span>

<span data-ttu-id="9c437-451">В следующей таблице представлены функции, поддерживают эскизные карты:</span><span class="sxs-lookup"><span data-stu-id="9c437-451">The following table provides the features that support thumbnail cards:</span></span>

| <span data-ttu-id="9c437-452">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="9c437-452">Bots in Teams</span></span> | <span data-ttu-id="9c437-453">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="9c437-453">Messaging extensions</span></span>  | <span data-ttu-id="9c437-454">Соединители</span><span class="sxs-lookup"><span data-stu-id="9c437-454">Connectors</span></span> | <span data-ttu-id="9c437-455">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="9c437-455">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="9c437-456">✔</span><span class="sxs-lookup"><span data-stu-id="9c437-456">✔</span></span> | <span data-ttu-id="9c437-457">✔</span><span class="sxs-lookup"><span data-stu-id="9c437-457">✔</span></span> | <span data-ttu-id="9c437-458">✖</span><span class="sxs-lookup"><span data-stu-id="9c437-458">✖</span></span> | <span data-ttu-id="9c437-459">✔</span><span class="sxs-lookup"><span data-stu-id="9c437-459">✔</span></span> |

![Пример карты эскиза](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a><span data-ttu-id="9c437-461">Свойства карты эскиза</span><span class="sxs-lookup"><span data-stu-id="9c437-461">Properties of a thumbnail card</span></span>

<span data-ttu-id="9c437-462">Следующая таблица содержит свойства карты эскиза:</span><span class="sxs-lookup"><span data-stu-id="9c437-462">The following table provides the properties of a thumbnail card:</span></span>

| <span data-ttu-id="9c437-463">Свойство</span><span class="sxs-lookup"><span data-stu-id="9c437-463">Property</span></span> | <span data-ttu-id="9c437-464">Тип</span><span class="sxs-lookup"><span data-stu-id="9c437-464">Type</span></span>  | <span data-ttu-id="9c437-465">Описание</span><span class="sxs-lookup"><span data-stu-id="9c437-465">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9c437-466">title</span><span class="sxs-lookup"><span data-stu-id="9c437-466">title</span></span> | <span data-ttu-id="9c437-467">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="9c437-467">Rich text</span></span> | <span data-ttu-id="9c437-468">Название карты.</span><span class="sxs-lookup"><span data-stu-id="9c437-468">Title of the card.</span></span> <span data-ttu-id="9c437-469">Максимум 2 строки.</span><span class="sxs-lookup"><span data-stu-id="9c437-469">Maximum 2 lines.</span></span>|
| <span data-ttu-id="9c437-470">субтитры</span><span class="sxs-lookup"><span data-stu-id="9c437-470">subtitle</span></span> | <span data-ttu-id="9c437-471">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="9c437-471">Rich text</span></span> | <span data-ttu-id="9c437-472">Субтитр карты.</span><span class="sxs-lookup"><span data-stu-id="9c437-472">Subtitle of the card.</span></span> <span data-ttu-id="9c437-473">Максимум 2 строки.</span><span class="sxs-lookup"><span data-stu-id="9c437-473">Maximum 2 lines.</span></span>|
| <span data-ttu-id="9c437-474">текст</span><span class="sxs-lookup"><span data-stu-id="9c437-474">text</span></span> | <span data-ttu-id="9c437-475">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="9c437-475">Rich text</span></span> | <span data-ttu-id="9c437-476">Текст отображается под субтитром.</span><span class="sxs-lookup"><span data-stu-id="9c437-476">Text appears under the subtitle.</span></span> <span data-ttu-id="9c437-477">Параметры форматирования см. [в виде форматирования карт.](~/task-modules-and-cards/cards/cards-format.md)</span><span class="sxs-lookup"><span data-stu-id="9c437-477">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="9c437-478">изображения</span><span class="sxs-lookup"><span data-stu-id="9c437-478">images</span></span> | <span data-ttu-id="9c437-479">Массив изображений</span><span class="sxs-lookup"><span data-stu-id="9c437-479">Array of images</span></span> | <span data-ttu-id="9c437-480">Изображение, отображаемого в верхней части карты.</span><span class="sxs-lookup"><span data-stu-id="9c437-480">Image displayed at the top of the card.</span></span> <span data-ttu-id="9c437-481">Отношение аспектов 1:1 к квадрату.</span><span class="sxs-lookup"><span data-stu-id="9c437-481">Aspect ratio 1:1 square.</span></span> |
| <span data-ttu-id="9c437-482">кнопки</span><span class="sxs-lookup"><span data-stu-id="9c437-482">buttons</span></span> | <span data-ttu-id="9c437-483">Массив объектов действий</span><span class="sxs-lookup"><span data-stu-id="9c437-483">Array of action objects</span></span> | <span data-ttu-id="9c437-484">Набор действий, применимых к текущей карте.</span><span class="sxs-lookup"><span data-stu-id="9c437-484">Set of actions applicable to the current card.</span></span> <span data-ttu-id="9c437-485">Максимум 6.</span><span class="sxs-lookup"><span data-stu-id="9c437-485">Maximum 6.</span></span> |
| <span data-ttu-id="9c437-486">нажмите кнопку</span><span class="sxs-lookup"><span data-stu-id="9c437-486">tap</span></span> | <span data-ttu-id="9c437-487">Объект Action</span><span class="sxs-lookup"><span data-stu-id="9c437-487">Action object</span></span> | <span data-ttu-id="9c437-488">Активируется при нажатии на карточку самого пользователя.</span><span class="sxs-lookup"><span data-stu-id="9c437-488">Activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-thumbnail-card"></a><span data-ttu-id="9c437-489">Пример карты эскиза</span><span class="sxs-lookup"><span data-stu-id="9c437-489">Example of a thumbnail card</span></span>

<span data-ttu-id="9c437-490">В следующем коде показан пример карты эскиза:</span><span class="sxs-lookup"><span data-stu-id="9c437-490">The following code shows an example of a thumbnail card:</span></span>

```json
{
  "contentType": "application/vnd.microsoft.card.thumbnail",
  "content": {
    "title": "Bender",
    "subtitle": "tale of a robot who dared to love",
    "text": "Bender Bending Rodríguez is a main character in the animated television series Futurama. He was created by series creators Matt Groening and David X. Cohen, and is voiced by John DiMaggio",
    "images": [
      {
        "url": "https://upload.wikimedia.org/wikipedia/en/a/a6/Bender_Rodriguez.png",
        "alt": "Bender Rodríguez"
      }
    ],
    "buttons": [
      {
        "type": "imBack",
        "title": "Thumbs Up",
        "image": "http://moopz.com/assets_c/2012/06/emoji-thumbs-up-150-thumb-autox125-140616.jpg",
        "value": "I like it"
      },
      {
        "type": "imBack",
        "title": "Thumbs Down",
        "image": "http://yourfaceisstupid.com/wp-content/uploads/2014/08/thumbs-down.png",
        "value": "I don't like it"
      },
      {
        "type": "openUrl",
        "title": "I feel lucky",
        "image": "http://thumb9.shutterstock.com/photos/thumb_large/683806/148441982.jpg",
        "value": "https://www.bing.com/images/search?q=bender&qpvt=bender&qpvt=bender&qpvt=bender&FORM=IGRE"
      }
    ],
    "tap": {
      "type": "imBack",
      "value": "Tapped it!"
    }
  }
}
```

### <a name="additional-information"></a><span data-ttu-id="9c437-491">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="9c437-491">Additional information</span></span>

<span data-ttu-id="9c437-492">Ссылка на Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="9c437-492">Bot Framework reference:</span></span>

* [<span data-ttu-id="9c437-493">Эскиз карты Node.js</span><span class="sxs-lookup"><span data-stu-id="9c437-493">Thumbnail card Node.js</span></span>](/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="9c437-494">Эскиз карты C #</span><span class="sxs-lookup"><span data-stu-id="9c437-494">Thumbnail card C#</span></span>](/dotnet/api/microsoft.bot.schema.thumbnailcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="card-collections"></a><span data-ttu-id="9c437-495">Коллекции карт</span><span class="sxs-lookup"><span data-stu-id="9c437-495">Card collections</span></span>

<span data-ttu-id="9c437-496">Вы можете работать с коллекциями карт, которые включают карусель и коллекции списков.</span><span class="sxs-lookup"><span data-stu-id="9c437-496">You can work with card collections that include carousel and list collections.</span></span> <span data-ttu-id="9c437-497">Teams поддерживает коллекции карт.</span><span class="sxs-lookup"><span data-stu-id="9c437-497">Teams supports card collections.</span></span> <span data-ttu-id="9c437-498">Коллекции карт включают `builder.AttachmentLayout.carousel` и `builder.AttachmentLayout.list` .</span><span class="sxs-lookup"><span data-stu-id="9c437-498">Card collections include `builder.AttachmentLayout.carousel` and `builder.AttachmentLayout.list`.</span></span> <span data-ttu-id="9c437-499">Эти коллекции содержат адаптивные, герой или эскизные карточки.</span><span class="sxs-lookup"><span data-stu-id="9c437-499">These collections contain Adaptive, hero, or thumbnail cards.</span></span>

### <a name="carousel-collection"></a><span data-ttu-id="9c437-500">Коллекция Карусель</span><span class="sxs-lookup"><span data-stu-id="9c437-500">Carousel collection</span></span>

<span data-ttu-id="9c437-501">Макет [карусель показывает](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) карусель карт, необязательно с связанными кнопками действия.</span><span class="sxs-lookup"><span data-stu-id="9c437-501">The [carousel layout](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) shows a carousel of cards, optionally with associated action buttons.</span></span>

#### <a name="support-for-carousel-collections"></a><span data-ttu-id="9c437-502">Поддержка коллекций карусель</span><span class="sxs-lookup"><span data-stu-id="9c437-502">Support for carousel collections</span></span>

<span data-ttu-id="9c437-503">В следующей таблице представлены функции, поддерживают коллекции карусель:</span><span class="sxs-lookup"><span data-stu-id="9c437-503">The following table provides the features that support carousel collections:</span></span>

| <span data-ttu-id="9c437-504">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="9c437-504">Bots in Teams</span></span> | <span data-ttu-id="9c437-505">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="9c437-505">Messaging extensions</span></span>  | <span data-ttu-id="9c437-506">Соединители</span><span class="sxs-lookup"><span data-stu-id="9c437-506">Connectors</span></span> | <span data-ttu-id="9c437-507">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="9c437-507">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="9c437-508">✔</span><span class="sxs-lookup"><span data-stu-id="9c437-508">✔</span></span> | <span data-ttu-id="9c437-509">✖</span><span class="sxs-lookup"><span data-stu-id="9c437-509">✖</span></span> | <span data-ttu-id="9c437-510">✖</span><span class="sxs-lookup"><span data-stu-id="9c437-510">✖</span></span> | <span data-ttu-id="9c437-511">✔</span><span class="sxs-lookup"><span data-stu-id="9c437-511">✔</span></span> |

> [!NOTE]
> <span data-ttu-id="9c437-512">Карусель может отображать не более десяти карт на сообщение.</span><span class="sxs-lookup"><span data-stu-id="9c437-512">A carousel can display a maximum of ten cards per message.</span></span>

#### <a name="properties-of-a-carousel-card"></a><span data-ttu-id="9c437-513">Свойства карусели</span><span class="sxs-lookup"><span data-stu-id="9c437-513">Properties of a carousel card</span></span>

<span data-ttu-id="9c437-514">Свойства карусельной карты такие же, как и у карт героя и эскиза.</span><span class="sxs-lookup"><span data-stu-id="9c437-514">Properties of a carousel card are same as the hero and thumbnail cards.</span></span>

#### <a name="example-of-a-carousel-collection"></a><span data-ttu-id="9c437-515">Пример коллекции карусель</span><span class="sxs-lookup"><span data-stu-id="9c437-515">Example of a carousel collection</span></span>

![Пример карусели карт](~/assets/images/cards/carousel.png)

<span data-ttu-id="9c437-517">В следующем коде показан пример коллекции карусели:</span><span class="sxs-lookup"><span data-stu-id="9c437-517">The following code shows an example of a carousel collection:</span></span>

```json
{
 "attachmentLayout": "carousel",
 "attachments":[
    {
      "contentType": "application/vnd.microsoft.card.adaptive",
      "content": {
        "type": "AdaptiveCard",
        "version": "1.0",
        "body": [
          {
            "type": "Container",
            "items": [
              {
                "type": "TextBlock",
                "size": "extraLarge",
                "weight": "bolder",
                "text": "Welcome to Employee Connect",
                "height": "stretch"
              },
              {
                "type": "TextBlock",
                "size": "medium",
                "weight": "bolder",
                "text": "Add events to your calendar",
                "height": "stretch"
              },
              {
                "type": "TextBlock",
                "weight": "bolder",
                "text": "The bot can send \r\rnotification to remind \r\ryou about the latest \r\revents and trainings.",
                "wrap": true,
                "height": "stretch"
              },
              {
                "type": "ColumnSet",
                "columns": [
                  {
                    "type": "Column",
                    "items": [],
                    "height": "stretch"
                  }
                ]
              },
              {
                "type": "ColumnSet",
                "columns": [
                  {
                    "type": "Column",
                    "items": [],
                    "height": "stretch"
                  }
                ]
              }
            ]
          }
        ],
        "actions": [
          {
            "type": "Action.Submit",
            "title": "Let's get started"
          }
        ]
      }
    },
    {
      "contentType": "application/vnd.microsoft.card.adaptive",
      "content": {
        "type": "AdaptiveCard",
        "version": "1.2",
        "body": [
          {
            "type": "Container",
            "items": [
              {
                "type": "TextBlock",
                "size": "large",
                "weight": "bolder",
                "text": "Employee connect"
              },
              {
                "type": "TextBlock",
                "text": "The bot can send notifications \r\rto remind you about the latest \r\r events and trainings",
                "wrap": true,
                "maxWidth": 2
              },
              {
                "type": "ColumnSet",
                "columns": [
                  {
                    "type": "Column",
                    "items": [],
                    "height": "stretch"
                  }
                ]
              },
              {
                "type": "ColumnSet",
                "columns": [
                  {
                    "type": "Column",
                    "items": [],
                    "height": "stretch"
                  }
                ]
              }
            ]
          }
        ],
        "actions": [
          {
            "type": "Action.Submit",
            "title": "Let's get started"
          }
        ]
      }
    },
    {
      "contentType": "application/vnd.microsoft.card.adaptive",
      "content": {
        "type": "AdaptiveCard",
        "version": "1.0",
        "body": [
          {
            "type": "Container",
            "items": [
              {
                "type": "TextBlock",
                "size": "large",
                "weight": "bolder",
                "text": "Employee Connect final"
              },
              {
                "type": "TextBlock",
                "weight": "bolder",
                "text": "Create and manage your tasks",
                "wrap": true
              },
              {
                "type": "TextBlock",
                "text": "The app identifies all your pending tasks \r\r and helps you manage everything at \r\r one place.",
                "wrap": true
              },
              {
                "type": "TextBlock",
                "weight": "bolder",
                "text": "Try these commands \r\r- Pending Submissions \r\r- Pending Approvals- My Tools",
                "wrap": true,
                "height": "stretch"
              }
            ]
          }
        ],
        "actions": [
          {
            "type": "Action.Submit",
            "title": "Let's get started"
          }
        ]
      }
    }
  ]
}
```

#### <a name="syntax-for-carousel-collections"></a><span data-ttu-id="9c437-518">Синтаксис для коллекций карусели</span><span class="sxs-lookup"><span data-stu-id="9c437-518">Syntax for carousel collections</span></span>

<span data-ttu-id="9c437-519">`builder.AttachmentLayoutTypes.Carousel` синтаксис для коллекций карусели.</span><span class="sxs-lookup"><span data-stu-id="9c437-519">`builder.AttachmentLayoutTypes.Carousel` is the syntax for carousel collections.</span></span>

### <a name="list-collection"></a><span data-ttu-id="9c437-520">Коллекция списков</span><span class="sxs-lookup"><span data-stu-id="9c437-520">List collection</span></span>

<span data-ttu-id="9c437-521">В макете списка показан вертикально сложенный список карт, необязательно связанный с кнопками действия.</span><span class="sxs-lookup"><span data-stu-id="9c437-521">The list layout shows a vertically stacked list of cards, optionally with associated action buttons.</span></span>

#### <a name="support-for-list-collections"></a><span data-ttu-id="9c437-522">Поддержка коллекций списков</span><span class="sxs-lookup"><span data-stu-id="9c437-522">Support for list collections</span></span>

<span data-ttu-id="9c437-523">В следующей таблице представлены функции, поддерживают коллекции списков:</span><span class="sxs-lookup"><span data-stu-id="9c437-523">The following table provides the features that support list collections:</span></span>

| <span data-ttu-id="9c437-524">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="9c437-524">Bots in Teams</span></span> | <span data-ttu-id="9c437-525">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="9c437-525">Messaging extensions</span></span>  | <span data-ttu-id="9c437-526">Соединители</span><span class="sxs-lookup"><span data-stu-id="9c437-526">Connectors</span></span> | <span data-ttu-id="9c437-527">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="9c437-527">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="9c437-528">✔</span><span class="sxs-lookup"><span data-stu-id="9c437-528">✔</span></span> | <span data-ttu-id="9c437-529">✔</span><span class="sxs-lookup"><span data-stu-id="9c437-529">✔</span></span> | <span data-ttu-id="9c437-530">✖</span><span class="sxs-lookup"><span data-stu-id="9c437-530">✖</span></span> | <span data-ttu-id="9c437-531">✔</span><span class="sxs-lookup"><span data-stu-id="9c437-531">✔</span></span> |

#### <a name="example-of-a-list-collection"></a><span data-ttu-id="9c437-532">Пример коллекции списков</span><span class="sxs-lookup"><span data-stu-id="9c437-532">Example of a list collection</span></span>

![Пример списка карт](~/assets/images/cards/list.png)

<span data-ttu-id="9c437-534">Свойства коллекций списков одинаковы с картами героя или эскиза.</span><span class="sxs-lookup"><span data-stu-id="9c437-534">Properties of list collections are same as the hero or thumbnail cards.</span></span>

<span data-ttu-id="9c437-535">В списке может отображаться не более десяти карт на сообщение.</span><span class="sxs-lookup"><span data-stu-id="9c437-535">A list can display a maximum of ten cards per message.</span></span>

> [!NOTE]
> <span data-ttu-id="9c437-536">Некоторые сочетания карт списка еще не поддерживаются на iOS и Android.</span><span class="sxs-lookup"><span data-stu-id="9c437-536">Some combinations of list cards are not yet supported on iOS and Android.</span></span>

#### <a name="syntax-for-list-collections"></a><span data-ttu-id="9c437-537">Синтаксис для коллекций списков</span><span class="sxs-lookup"><span data-stu-id="9c437-537">Syntax for list collections</span></span>

<span data-ttu-id="9c437-538">`builder.AttachmentLayout.list` синтаксис для коллекций списков.</span><span class="sxs-lookup"><span data-stu-id="9c437-538">`builder.AttachmentLayout.list` is the syntax for list collections.</span></span>

## <a name="cards-not-supported-in-teams"></a><span data-ttu-id="9c437-539">Карты, не поддерживаемые в Teams</span><span class="sxs-lookup"><span data-stu-id="9c437-539">Cards not supported in Teams</span></span>

<span data-ttu-id="9c437-540">Следующие карты реализуются в рамках Bot Framework, но не поддерживаются Teams:</span><span class="sxs-lookup"><span data-stu-id="9c437-540">The following cards are implemented by the Bot Framework, but are not supported by Teams:</span></span>

* <span data-ttu-id="9c437-541">Карты анимации</span><span class="sxs-lookup"><span data-stu-id="9c437-541">Animation cards</span></span>
* <span data-ttu-id="9c437-542">Аудиокарты</span><span class="sxs-lookup"><span data-stu-id="9c437-542">Audio cards</span></span>
* <span data-ttu-id="9c437-543">Видеокарты</span><span class="sxs-lookup"><span data-stu-id="9c437-543">Video cards</span></span>

## <a name="see-also"></a><span data-ttu-id="9c437-544">См. также</span><span class="sxs-lookup"><span data-stu-id="9c437-544">See also</span></span>

* [<span data-ttu-id="9c437-545">Модули задач</span><span class="sxs-lookup"><span data-stu-id="9c437-545">Task modules</span></span>](~/task-modules-and-cards/what-are-task-modules.md)
* [<span data-ttu-id="9c437-546">Форматные карты</span><span class="sxs-lookup"><span data-stu-id="9c437-546">Format cards</span></span>](~/task-modules-and-cards/cards/cards-format.md)
