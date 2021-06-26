---
title: Типы карт
description: Описывает все действия карт и карт, доступные ботам в Teams
localization_priority: Normal
keywords: ссылка на карточки ботов
ms.topic: reference
ms.openlocfilehash: be38454daac519530d0fdf10b5170e128219f6fc
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140501"
---
# <a name="types-of-cards"></a><span data-ttu-id="08c07-104">Типы карт</span><span class="sxs-lookup"><span data-stu-id="08c07-104">Types of cards</span></span>

<span data-ttu-id="08c07-105">Адаптивные, герой, список, Office 365 соединителю, квитанции, знаки и эскизные карты и коллекции карт поддерживаются в ботах для Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="08c07-105">Adaptive, hero, list, Office 365 Connector, receipt, signin, and thumbnail cards and card collections are supported in bots for Microsoft Teams.</span></span> <span data-ttu-id="08c07-106">Они основаны на картах, определенных bot Framework, но Teams не поддерживают все карты Bot Framework и добавили некоторые из них.</span><span class="sxs-lookup"><span data-stu-id="08c07-106">They are based on cards defined by the Bot Framework, but Teams does not support all Bot Framework cards and has added some of its own.</span></span>

<span data-ttu-id="08c07-107">Прежде чем определить различные типы карт, поймите, как создать карточку героя, карту эскиза или адаптивную карту.</span><span class="sxs-lookup"><span data-stu-id="08c07-107">Before you identify the different card types, understand how to create a a hero card, thumbnail card, or Adaptive Card.</span></span>

## <a name="create-a-hero-card-thumbnail-card-or-adaptive-card"></a><span data-ttu-id="08c07-108">Создание карты героя, карты эскиза или адаптивной карты</span><span class="sxs-lookup"><span data-stu-id="08c07-108">Create a hero card, thumbnail card, or Adaptive Card</span></span>

<span data-ttu-id="08c07-109">**Создание карты героя, карты эскиза или адаптивной карты из App Studio**</span><span class="sxs-lookup"><span data-stu-id="08c07-109">**To create a hero card, thumbnail card, or Adaptive Card from App Studio**</span></span>

1. <span data-ttu-id="08c07-110">Перейдите **в App Studio** из Teams.</span><span class="sxs-lookup"><span data-stu-id="08c07-110">Go to **App Studio** from Teams.</span></span>
1. <span data-ttu-id="08c07-111">Выберите **редактор карты**.</span><span class="sxs-lookup"><span data-stu-id="08c07-111">Select **Card editor**.</span></span>
1. <span data-ttu-id="08c07-112">Выберите **Создание новой карты.**</span><span class="sxs-lookup"><span data-stu-id="08c07-112">Select **Create a new card**.</span></span>
1. <span data-ttu-id="08c07-113">Выберите **Создать** для одной из карт карточки **героя,** **эскизной** карты или **адаптивной карты.**</span><span class="sxs-lookup"><span data-stu-id="08c07-113">Select **Create** for one of the cards from **Hero Card**, **Thumbnail Card**, or **Adaptive Card**.</span></span> <span data-ttu-id="08c07-114">Для этой карты показаны сведения о метаданных, кнопки и примеры кода json, csharp и узлов.</span><span class="sxs-lookup"><span data-stu-id="08c07-114">The metadata details, buttons, and json, csharp, and node code examples are shown for that card.</span></span>

    ![Сведения о карточке героя](~/assets/images/Cards/Herocarddetails.png)

1. <span data-ttu-id="08c07-116">Выберите **Отправить мне эту карточку.**</span><span class="sxs-lookup"><span data-stu-id="08c07-116">Select **Send me this card**.</span></span> <span data-ttu-id="08c07-117">Карта отправляется вам в качестве сообщения чата.</span><span class="sxs-lookup"><span data-stu-id="08c07-117">The card is sent to you as a chat message.</span></span>

## <a name="card-examples"></a><span data-ttu-id="08c07-118">Примеры карт</span><span class="sxs-lookup"><span data-stu-id="08c07-118">Card examples</span></span>

<span data-ttu-id="08c07-119">Дополнительные сведения об использовании карт можно найти в документации для bot Builder SDK v3.</span><span class="sxs-lookup"><span data-stu-id="08c07-119">You can find additional information on how to use cards in the documentation for the Bot Builder SDK v3.</span></span> <span data-ttu-id="08c07-120">Примеры кода также доступны в репозитории **Microsoft/BotBuilder-Samples** на GitHub.</span><span class="sxs-lookup"><span data-stu-id="08c07-120">Code samples are also available in the **Microsoft/BotBuilder-Samples** repository on GitHub.</span></span> <span data-ttu-id="08c07-121">Ниже приводится несколько примеров карт:</span><span class="sxs-lookup"><span data-stu-id="08c07-121">Following are a few card examples:</span></span>

* <span data-ttu-id="08c07-122">.NET</span><span class="sxs-lookup"><span data-stu-id="08c07-122">.NET</span></span>
  * <span data-ttu-id="08c07-123">[Добавление карт в виде вложений в сообщения.](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="08c07-123">[Add cards as attachments to messages](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true).</span></span>
  * <span data-ttu-id="08c07-124">[Карты пример кода Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards).</span><span class="sxs-lookup"><span data-stu-id="08c07-124">[Cards sample code Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards).</span></span>

* <span data-ttu-id="08c07-125">Node.js</span><span class="sxs-lookup"><span data-stu-id="08c07-125">Node.js</span></span>
  * <span data-ttu-id="08c07-126">[Добавление карт в виде вложений в сообщения.](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="08c07-126">[Add cards as attachments to messages](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true).</span></span>
  * <span data-ttu-id="08c07-127">[Карты пример кода Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards).</span><span class="sxs-lookup"><span data-stu-id="08c07-127">[Cards sample code Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards).</span></span>

## <a name="card-types"></a><span data-ttu-id="08c07-128">Типы карт</span><span class="sxs-lookup"><span data-stu-id="08c07-128">Card types</span></span>

<span data-ttu-id="08c07-129">Вы можете определять и использовать различные типы карт в зависимости от требований к приложению.</span><span class="sxs-lookup"><span data-stu-id="08c07-129">You can identify and use different types of cards based on your application requirements.</span></span> <span data-ttu-id="08c07-130">В следующей таблице показаны типы доступных вам карт:</span><span class="sxs-lookup"><span data-stu-id="08c07-130">The following table shows the types of cards available to you:</span></span>

| <span data-ttu-id="08c07-131">Тип карты</span><span class="sxs-lookup"><span data-stu-id="08c07-131">Card type</span></span> | <span data-ttu-id="08c07-132">Description</span><span class="sxs-lookup"><span data-stu-id="08c07-132">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="08c07-133">Адаптивная карта</span><span class="sxs-lookup"><span data-stu-id="08c07-133">Adaptive Card</span></span>](#adaptive-card) | <span data-ttu-id="08c07-134">Эта карта очень настраиваема и может содержать любое сочетание текстов, речи, изображений, кнопок и полей ввода.</span><span class="sxs-lookup"><span data-stu-id="08c07-134">This card is highly customizable and can contain any combination of text, speech, images, buttons, and input fields.</span></span> |
| [<span data-ttu-id="08c07-135">Карта hero</span><span class="sxs-lookup"><span data-stu-id="08c07-135">Hero card</span></span>](#hero-card) | <span data-ttu-id="08c07-136">Эта карта обычно содержит одно большое изображение, одну или несколько кнопок и небольшое количество текста.</span><span class="sxs-lookup"><span data-stu-id="08c07-136">This card typically contains a single large image, one or more buttons, and a small amount of text.</span></span> |
| [<span data-ttu-id="08c07-137">Карта списка</span><span class="sxs-lookup"><span data-stu-id="08c07-137">List card</span></span>](#list-card) | <span data-ttu-id="08c07-138">Эта карта содержит список элементов прокрутки.</span><span class="sxs-lookup"><span data-stu-id="08c07-138">This card contains a scrolling list of items.</span></span> |
| [<span data-ttu-id="08c07-139">Office 365 Карта Connector</span><span class="sxs-lookup"><span data-stu-id="08c07-139">Office 365 Connector card</span></span>](#office-365-connector-card) | <span data-ttu-id="08c07-140">Эта карта имеет гибкий макет с несколькими разделами, полями, изображениями и действиями.</span><span class="sxs-lookup"><span data-stu-id="08c07-140">This card has a flexible layout with multiple sections, fields, images, and actions.</span></span> |
| [<span data-ttu-id="08c07-141">Карта получения</span><span class="sxs-lookup"><span data-stu-id="08c07-141">Receipt card</span></span>](#receipt-card) | <span data-ttu-id="08c07-142">Эта карта предоставляет квитанцию пользователю.</span><span class="sxs-lookup"><span data-stu-id="08c07-142">This card provides a receipt to the user.</span></span> |
| [<span data-ttu-id="08c07-143">Карточка Signin</span><span class="sxs-lookup"><span data-stu-id="08c07-143">Signin card</span></span>](#signin-card) | <span data-ttu-id="08c07-144">Эта карта позволяет боту запрашивать, чтобы пользователь войди.</span><span class="sxs-lookup"><span data-stu-id="08c07-144">This card enables a bot to request that a user signs in.</span></span> |
| [<span data-ttu-id="08c07-145">Карта эскиза</span><span class="sxs-lookup"><span data-stu-id="08c07-145">Thumbnail card</span></span>](#thumbnail-card) | <span data-ttu-id="08c07-146">Эта карта обычно содержит одно изображение эскиза, короткий текст и одну или несколько кнопок.</span><span class="sxs-lookup"><span data-stu-id="08c07-146">This card typically contains a single thumbnail image, some short text, and one or more buttons.</span></span> |
| [<span data-ttu-id="08c07-147">Коллекции карт</span><span class="sxs-lookup"><span data-stu-id="08c07-147">Card collections</span></span>](#card-collections) | <span data-ttu-id="08c07-148">Эта коллекция карт используется для возврата нескольких элементов в одном ответе.</span><span class="sxs-lookup"><span data-stu-id="08c07-148">This card collection is used to return multiple items in a single response.</span></span> |

## <a name="common-properties-for-all-cards"></a><span data-ttu-id="08c07-149">Общие свойства для всех карт</span><span class="sxs-lookup"><span data-stu-id="08c07-149">Common properties for all cards</span></span>

<span data-ttu-id="08c07-150">Вы можете пройти через некоторые общие свойства, применимые к всем картам.</span><span class="sxs-lookup"><span data-stu-id="08c07-150">You can go through some common properties that are applicable to all cards.</span></span>

### <a name="inline-card-images"></a><span data-ttu-id="08c07-151">Inline card images</span><span class="sxs-lookup"><span data-stu-id="08c07-151">Inline card images</span></span>

<span data-ttu-id="08c07-152">Карта может содержать рядное изображение, включив ссылку на общедоступный образ.</span><span class="sxs-lookup"><span data-stu-id="08c07-152">The card can contain an inline image by including a link to the publicly available image.</span></span> <span data-ttu-id="08c07-153">В целях производительности рекомендуется разогласить изображение в общедоступных сеть доставки содержимого (CDN).</span><span class="sxs-lookup"><span data-stu-id="08c07-153">For performance purposes, it is highly recommended you host the image on a public Content Delivery Network (CDN).</span></span>

<span data-ttu-id="08c07-154">Для поддержания соотношения аспектов для покрытия области изображений масштабы изображения масштабирования или сухую величину.</span><span class="sxs-lookup"><span data-stu-id="08c07-154">Images are scaled up or down in size to maintain the aspect ratio for covering the image area.</span></span> <span data-ttu-id="08c07-155">Затем изображения обрезаются из центра, чтобы достичь соответствующего соотношения аспектов для карты.</span><span class="sxs-lookup"><span data-stu-id="08c07-155">Images are then cropped from center to achieve the appropriate aspect ratio for the card.</span></span>

<span data-ttu-id="08c07-156">Изображения должны быть не более 1024×1024 и в формате PNG, JPEG или GIF.</span><span class="sxs-lookup"><span data-stu-id="08c07-156">Images must be at most 1024×1024 and in PNG, JPEG, or GIF format.</span></span> <span data-ttu-id="08c07-157">Анимированный GIF не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="08c07-157">Animated GIF is not supported.</span></span>

<span data-ttu-id="08c07-158">В следующей таблице ниже огонек содержится следующее:</span><span class="sxs-lookup"><span data-stu-id="08c07-158">The following table provides the properties of inline card images:</span></span>

| <span data-ttu-id="08c07-159">Свойство</span><span class="sxs-lookup"><span data-stu-id="08c07-159">Property</span></span> | <span data-ttu-id="08c07-160">Тип</span><span class="sxs-lookup"><span data-stu-id="08c07-160">Type</span></span>  | <span data-ttu-id="08c07-161">Описание</span><span class="sxs-lookup"><span data-stu-id="08c07-161">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="08c07-162">url</span><span class="sxs-lookup"><span data-stu-id="08c07-162">url</span></span> | <span data-ttu-id="08c07-163">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="08c07-163">URL</span></span> | <span data-ttu-id="08c07-164">URL-адрес HTTPS к изображению.</span><span class="sxs-lookup"><span data-stu-id="08c07-164">HTTPS URL to the image.</span></span> |
| <span data-ttu-id="08c07-165">alt</span><span class="sxs-lookup"><span data-stu-id="08c07-165">alt</span></span> | <span data-ttu-id="08c07-166">String</span><span class="sxs-lookup"><span data-stu-id="08c07-166">String</span></span> | <span data-ttu-id="08c07-167">Доступное описание изображения.</span><span class="sxs-lookup"><span data-stu-id="08c07-167">Accessible description of the image.</span></span> |

> [!NOTE]
> <span data-ttu-id="08c07-168">Если карта содержит URL-адрес изображения, перенаправленный перед окончательным изображением, перенаправление URL-адреса изображения не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="08c07-168">If a card includes an image URL that is redirected before the final image, the redirect in image URL is not supported.</span></span> <span data-ttu-id="08c07-169">Это происходит для изображений, общих в общедоступных облаках.</span><span class="sxs-lookup"><span data-stu-id="08c07-169">This occurs for images shared on the public cloud.</span></span>

### <a name="buttons"></a><span data-ttu-id="08c07-170">Кнопки</span><span class="sxs-lookup"><span data-stu-id="08c07-170">Buttons</span></span>

<span data-ttu-id="08c07-171">Кнопки показаны в нижней части карты.</span><span class="sxs-lookup"><span data-stu-id="08c07-171">Buttons are shown stacked at the bottom of the card.</span></span> <span data-ttu-id="08c07-172">Текст кнопки всегда находится в одной строке и усечен, если текст превышает ширину кнопки.</span><span class="sxs-lookup"><span data-stu-id="08c07-172">Button text is always on a single line and is truncated if the text exceeds the button width.</span></span> <span data-ttu-id="08c07-173">Никаких дополнительных кнопок, помимо максимального числа, поддерживаемого картой, не отображается.</span><span class="sxs-lookup"><span data-stu-id="08c07-173">Any additional buttons beyond the maximum number supported by the card are not shown.</span></span>

<span data-ttu-id="08c07-174">Дополнительные сведения см. в [карточных действиях.](~/task-modules-and-cards/cards/cards-actions.md)</span><span class="sxs-lookup"><span data-stu-id="08c07-174">For more information, see [card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

### <a name="card-formatting"></a><span data-ttu-id="08c07-175">Форматирование карт</span><span class="sxs-lookup"><span data-stu-id="08c07-175">Card formatting</span></span>

<span data-ttu-id="08c07-176">Дополнительные сведения о форматирования текста в картах см. [в документе форматирование карт.](~/task-modules-and-cards/cards/cards-format.md)</span><span class="sxs-lookup"><span data-stu-id="08c07-176">For more information on text formatting in cards, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span>

<span data-ttu-id="08c07-177">После определения общих свойств для всех карт теперь можно работать с адаптивными картами, которые помогают повысить вовлеченность и эффективность, добавив свой полезный контент непосредственно в приложения, которые вы используете.</span><span class="sxs-lookup"><span data-stu-id="08c07-177">After identifying the common properties for all cards, you can now work with Adaptive Cards, which help you increase engagement and efficiency by adding your actionable content directly into the apps you use.</span></span>

## <a name="adaptive-card"></a><span data-ttu-id="08c07-178">Адаптивная карта</span><span class="sxs-lookup"><span data-stu-id="08c07-178">Adaptive Card</span></span>

> [!VIDEO https://www.youtube-nocookie.com/embed/J12lKt717Ws]

<span data-ttu-id="08c07-179">Адаптивная карта — это настраиваемая карточка, которая может содержать любое сочетание текстов, речи, изображений, кнопок и полей ввода.</span><span class="sxs-lookup"><span data-stu-id="08c07-179">An Adaptive Card is a customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> <span data-ttu-id="08c07-180">Дополнительные сведения см. в [рублях Адаптивные карты v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span><span class="sxs-lookup"><span data-stu-id="08c07-180">For more information, see [Adaptive Cards v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span></span>

### <a name="support-for-adaptive-cards"></a><span data-ttu-id="08c07-181">Поддержка адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="08c07-181">Support for Adaptive Cards</span></span>

<span data-ttu-id="08c07-182">В следующей таблице представлены функции, поддерживаюющие адаптивные карты:</span><span class="sxs-lookup"><span data-stu-id="08c07-182">The following table provides the features that support Adaptive Cards:</span></span>

| <span data-ttu-id="08c07-183">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="08c07-183">Bots in Teams</span></span> | <span data-ttu-id="08c07-184">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="08c07-184">Messaging extensions</span></span>  | <span data-ttu-id="08c07-185">Соединители</span><span class="sxs-lookup"><span data-stu-id="08c07-185">Connectors</span></span> | <span data-ttu-id="08c07-186">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="08c07-186">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="08c07-187">✔</span><span class="sxs-lookup"><span data-stu-id="08c07-187">✔</span></span> | <span data-ttu-id="08c07-188">✔</span><span class="sxs-lookup"><span data-stu-id="08c07-188">✔</span></span> | <span data-ttu-id="08c07-189">✖</span><span class="sxs-lookup"><span data-stu-id="08c07-189">✖</span></span> | <span data-ttu-id="08c07-190">✔</span><span class="sxs-lookup"><span data-stu-id="08c07-190">✔</span></span> |

> [!NOTE]
> * <span data-ttu-id="08c07-191">Teams поддерживает v1.2 или более ранние функции адаптивной карты.</span><span class="sxs-lookup"><span data-stu-id="08c07-191">Teams platform supports v1.2 or earlier of Adaptive Card features.</span></span>
> * <span data-ttu-id="08c07-192">Положительный или разрушительный стиль действий не поддерживается в адаптивных картах на Teams платформе.</span><span class="sxs-lookup"><span data-stu-id="08c07-192">Positive or destructive action styling is not supported in Adaptive Cards on the Teams platform.</span></span>
> * <span data-ttu-id="08c07-193">Элементы мультимедиа в настоящее время не поддерживаются в адаптивной карте на Teams платформе.</span><span class="sxs-lookup"><span data-stu-id="08c07-193">Media elements are currently not supported in Adaptive Card on the Teams platform.</span></span>

### <a name="example-of-adaptive-card"></a><span data-ttu-id="08c07-194">Пример адаптивной карты</span><span class="sxs-lookup"><span data-stu-id="08c07-194">Example of Adaptive Card</span></span>

![Пример адаптивной карты](~/assets/images/cards/adaptivecard.png)

<span data-ttu-id="08c07-196">В следующем коде показан пример адаптивной карты:</span><span class="sxs-lookup"><span data-stu-id="08c07-196">The following code shows an example of an Adaptive Card:</span></span>

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

#### <a name="additional-information-on-adaptive-cards"></a><span data-ttu-id="08c07-197">Дополнительные сведения о адаптивных картах</span><span class="sxs-lookup"><span data-stu-id="08c07-197">Additional information on Adaptive Cards</span></span>

<span data-ttu-id="08c07-198">Ссылка на Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="08c07-198">Bot Framework reference:</span></span>

* [<span data-ttu-id="08c07-199">Узел адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="08c07-199">Adaptive Cards Node</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)
* [<span data-ttu-id="08c07-200">Адаптивная карта C #</span><span class="sxs-lookup"><span data-stu-id="08c07-200">Adaptive Card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)

<span data-ttu-id="08c07-201">Теперь вы можете работать с картой героя, которая является многоцелевой картой, используемой для визуального выделения потенциального выбора пользователя.</span><span class="sxs-lookup"><span data-stu-id="08c07-201">You can now work with a hero card, which is a multipurpose card used to visually highlight a potential user selection.</span></span>

## <a name="hero-card"></a><span data-ttu-id="08c07-202">Карта hero</span><span class="sxs-lookup"><span data-stu-id="08c07-202">Hero card</span></span>

<span data-ttu-id="08c07-203">Карта, которая обычно содержит одно большое изображение, одну или несколько кнопок и текст.</span><span class="sxs-lookup"><span data-stu-id="08c07-203">A card that typically contains a single large image, one or more buttons, and text.</span></span>

### <a name="support-for-hero-cards"></a><span data-ttu-id="08c07-204">Поддержка карт-героев</span><span class="sxs-lookup"><span data-stu-id="08c07-204">Support for hero cards</span></span>

<span data-ttu-id="08c07-205">В следующей таблице представлены функции, поддерживают карты героев:</span><span class="sxs-lookup"><span data-stu-id="08c07-205">The following table provides the features that support hero cards:</span></span>

| <span data-ttu-id="08c07-206">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="08c07-206">Bots in Teams</span></span> | <span data-ttu-id="08c07-207">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="08c07-207">Messaging extensions</span></span>  | <span data-ttu-id="08c07-208">Соединители</span><span class="sxs-lookup"><span data-stu-id="08c07-208">Connectors</span></span> | <span data-ttu-id="08c07-209">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="08c07-209">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="08c07-210">✔</span><span class="sxs-lookup"><span data-stu-id="08c07-210">✔</span></span> | <span data-ttu-id="08c07-211">✔</span><span class="sxs-lookup"><span data-stu-id="08c07-211">✔</span></span> | <span data-ttu-id="08c07-212">✖</span><span class="sxs-lookup"><span data-stu-id="08c07-212">✖</span></span> | <span data-ttu-id="08c07-213">✔</span><span class="sxs-lookup"><span data-stu-id="08c07-213">✔</span></span> |

### <a name="properties-of-a-hero-card"></a><span data-ttu-id="08c07-214">Свойства карты-героя</span><span class="sxs-lookup"><span data-stu-id="08c07-214">Properties of a hero card</span></span>

<span data-ttu-id="08c07-215">В следующей таблице огосяты свойства карточки героя:</span><span class="sxs-lookup"><span data-stu-id="08c07-215">The following table provides the properties of a hero card:</span></span>

| <span data-ttu-id="08c07-216">Свойство</span><span class="sxs-lookup"><span data-stu-id="08c07-216">Property</span></span> | <span data-ttu-id="08c07-217">Тип</span><span class="sxs-lookup"><span data-stu-id="08c07-217">Type</span></span>  | <span data-ttu-id="08c07-218">Описание</span><span class="sxs-lookup"><span data-stu-id="08c07-218">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="08c07-219">title</span><span class="sxs-lookup"><span data-stu-id="08c07-219">title</span></span> | <span data-ttu-id="08c07-220">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="08c07-220">Rich text</span></span> | <span data-ttu-id="08c07-221">Название карты.</span><span class="sxs-lookup"><span data-stu-id="08c07-221">Title of the card.</span></span> <span data-ttu-id="08c07-222">Максимум две строки.</span><span class="sxs-lookup"><span data-stu-id="08c07-222">Maximum two lines.</span></span> |
| <span data-ttu-id="08c07-223">субтитры</span><span class="sxs-lookup"><span data-stu-id="08c07-223">subtitle</span></span> | <span data-ttu-id="08c07-224">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="08c07-224">Rich text</span></span> | <span data-ttu-id="08c07-225">Субтитр карты.</span><span class="sxs-lookup"><span data-stu-id="08c07-225">Subtitle of the card.</span></span> <span data-ttu-id="08c07-226">Максимум две строки.</span><span class="sxs-lookup"><span data-stu-id="08c07-226">Maximum two lines.</span></span>|
| <span data-ttu-id="08c07-227">текст</span><span class="sxs-lookup"><span data-stu-id="08c07-227">text</span></span> | <span data-ttu-id="08c07-228">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="08c07-228">Rich text</span></span> | <span data-ttu-id="08c07-229">Текст отображается под субтитром.</span><span class="sxs-lookup"><span data-stu-id="08c07-229">Text appears under the subtitle.</span></span> <span data-ttu-id="08c07-230">Параметры форматирования см. [в виде форматирования карт.](~/task-modules-and-cards/cards/cards-format.md)</span><span class="sxs-lookup"><span data-stu-id="08c07-230">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="08c07-231">изображения</span><span class="sxs-lookup"><span data-stu-id="08c07-231">images</span></span> | <span data-ttu-id="08c07-232">Массив изображений</span><span class="sxs-lookup"><span data-stu-id="08c07-232">Array of images</span></span> | <span data-ttu-id="08c07-233">Изображение, отображаемого в верхней части карты.</span><span class="sxs-lookup"><span data-stu-id="08c07-233">Image displayed at the top of the card.</span></span> <span data-ttu-id="08c07-234">Соотношение аспектов 16:9.</span><span class="sxs-lookup"><span data-stu-id="08c07-234">Aspect ratio 16:9.</span></span> |
| <span data-ttu-id="08c07-235">кнопки</span><span class="sxs-lookup"><span data-stu-id="08c07-235">buttons</span></span> | <span data-ttu-id="08c07-236">Массив объектов действий</span><span class="sxs-lookup"><span data-stu-id="08c07-236">Array of action objects</span></span> | <span data-ttu-id="08c07-237">Набор действий, применимых к текущей карте.</span><span class="sxs-lookup"><span data-stu-id="08c07-237">Set of actions applicable to the current card.</span></span> <span data-ttu-id="08c07-238">Максимум шесть.</span><span class="sxs-lookup"><span data-stu-id="08c07-238">Maximum six.</span></span> |
| <span data-ttu-id="08c07-239">нажмите кнопку</span><span class="sxs-lookup"><span data-stu-id="08c07-239">tap</span></span> | <span data-ttu-id="08c07-240">Объект Action</span><span class="sxs-lookup"><span data-stu-id="08c07-240">Action object</span></span> | <span data-ttu-id="08c07-241">Активируется при нажатии на карточку самого пользователя.</span><span class="sxs-lookup"><span data-stu-id="08c07-241">Activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-hero-card"></a><span data-ttu-id="08c07-242">Пример карточки героя</span><span class="sxs-lookup"><span data-stu-id="08c07-242">Example of a hero card</span></span>

![Пример карточки героя](~/assets/images/cards/hero.png)

<span data-ttu-id="08c07-244">В следующем коде показан пример карты героя:</span><span class="sxs-lookup"><span data-stu-id="08c07-244">The following code shows an example of a hero card:</span></span>

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

### <a name="additional-information-on-hero-cards"></a><span data-ttu-id="08c07-245">Дополнительные сведения о картах-героях</span><span class="sxs-lookup"><span data-stu-id="08c07-245">Additional information on hero cards</span></span>

<span data-ttu-id="08c07-246">Ссылка на Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="08c07-246">Bot Framework reference:</span></span>

* [<span data-ttu-id="08c07-247">Карточка героя Node.js</span><span class="sxs-lookup"><span data-stu-id="08c07-247">Hero card Node.js</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-a-hero-card&preserve-view=true)
* [<span data-ttu-id="08c07-248">Карта героя C #</span><span class="sxs-lookup"><span data-stu-id="08c07-248">Hero card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-hero-card&preserve-view=true)

## <a name="list-card"></a><span data-ttu-id="08c07-249">Карта списка</span><span class="sxs-lookup"><span data-stu-id="08c07-249">List card</span></span>

<span data-ttu-id="08c07-250">Карта списка была добавлена Teams для предоставления функций, которые не могут предоставляться в коллекции списков.</span><span class="sxs-lookup"><span data-stu-id="08c07-250">The list card has been added by Teams to provide functions beyond what the list collection can provide.</span></span> <span data-ttu-id="08c07-251">Карта списка содержит список элементов для прокрутки.</span><span class="sxs-lookup"><span data-stu-id="08c07-251">The list card provides a scrolling list of items.</span></span>

### <a name="support-for-list-cards"></a><span data-ttu-id="08c07-252">Поддержка карт списка</span><span class="sxs-lookup"><span data-stu-id="08c07-252">Support for list cards</span></span>

<span data-ttu-id="08c07-253">В следующей таблице представлены функции, поддерживают карты списков:</span><span class="sxs-lookup"><span data-stu-id="08c07-253">The following table provides the features that support list cards:</span></span>

| <span data-ttu-id="08c07-254">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="08c07-254">Bots in Teams</span></span> | <span data-ttu-id="08c07-255">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="08c07-255">Messaging extensions</span></span>  | <span data-ttu-id="08c07-256">Соединители</span><span class="sxs-lookup"><span data-stu-id="08c07-256">Connectors</span></span> | <span data-ttu-id="08c07-257">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="08c07-257">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="08c07-258">✔</span><span class="sxs-lookup"><span data-stu-id="08c07-258">✔</span></span> | <span data-ttu-id="08c07-259">✖</span><span class="sxs-lookup"><span data-stu-id="08c07-259">✖</span></span> | <span data-ttu-id="08c07-260">✖</span><span class="sxs-lookup"><span data-stu-id="08c07-260">✖</span></span> |<span data-ttu-id="08c07-261">✔</span><span class="sxs-lookup"><span data-stu-id="08c07-261">✔</span></span> |

### <a name="properties-of-a-list-card"></a><span data-ttu-id="08c07-262">Свойства карты списка</span><span class="sxs-lookup"><span data-stu-id="08c07-262">Properties of a list card</span></span>

<span data-ttu-id="08c07-263">Следующая таблица содержит свойства карты списка:</span><span class="sxs-lookup"><span data-stu-id="08c07-263">The following table provides the properties of a list card:</span></span>

| <span data-ttu-id="08c07-264">Свойство</span><span class="sxs-lookup"><span data-stu-id="08c07-264">Property</span></span> | <span data-ttu-id="08c07-265">Тип</span><span class="sxs-lookup"><span data-stu-id="08c07-265">Type</span></span>  | <span data-ttu-id="08c07-266">Описание</span><span class="sxs-lookup"><span data-stu-id="08c07-266">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="08c07-267">title</span><span class="sxs-lookup"><span data-stu-id="08c07-267">title</span></span> | <span data-ttu-id="08c07-268">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="08c07-268">Rich text</span></span> | <span data-ttu-id="08c07-269">Название карты.</span><span class="sxs-lookup"><span data-stu-id="08c07-269">Title of the card.</span></span> <span data-ttu-id="08c07-270">Максимум 2 строки.</span><span class="sxs-lookup"><span data-stu-id="08c07-270">Maximum 2 lines.</span></span>|
| <span data-ttu-id="08c07-271">элементы</span><span class="sxs-lookup"><span data-stu-id="08c07-271">items</span></span> | <span data-ttu-id="08c07-272">Массив элементов списка</span><span class="sxs-lookup"><span data-stu-id="08c07-272">Array of list items</span></span> | <span data-ttu-id="08c07-273">Набор элементов, применимых к карте.</span><span class="sxs-lookup"><span data-stu-id="08c07-273">Set of items applicable to the card.</span></span>|
| <span data-ttu-id="08c07-274">кнопки</span><span class="sxs-lookup"><span data-stu-id="08c07-274">buttons</span></span> | <span data-ttu-id="08c07-275">Массив объектов действий</span><span class="sxs-lookup"><span data-stu-id="08c07-275">Array of action objects</span></span> | <span data-ttu-id="08c07-276">Набор действий, применимых к текущей карте.</span><span class="sxs-lookup"><span data-stu-id="08c07-276">Set of actions applicable to the current card.</span></span> <span data-ttu-id="08c07-277">Максимум 6.</span><span class="sxs-lookup"><span data-stu-id="08c07-277">Maximum 6.</span></span> |

### <a name="example-of-a-list-card"></a><span data-ttu-id="08c07-278">Пример карты списка</span><span class="sxs-lookup"><span data-stu-id="08c07-278">Example of a list card</span></span>

<span data-ttu-id="08c07-279">В следующем коде показан пример карты списка:</span><span class="sxs-lookup"><span data-stu-id="08c07-279">The following code shows an example of a list card:</span></span>

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

## <a name="office-365-connector-card"></a><span data-ttu-id="08c07-280">Office 365 соединители</span><span class="sxs-lookup"><span data-stu-id="08c07-280">Office 365 connector card</span></span>

<span data-ttu-id="08c07-281">Вы можете работать с Office 365 connector, которая обеспечивает гибкий макет и это отличный способ получения полезной информации.</span><span class="sxs-lookup"><span data-stu-id="08c07-281">You can work with an Office 365 Connector card that provides a flexible layout and is a great way to get useful information.</span></span> <span data-ttu-id="08c07-282">Соедините Office 365 поддерживается в Teams, а не в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="08c07-282">The Office 365 connector card is supported in Teams, not in Bot Framework.</span></span> <span data-ttu-id="08c07-283">Эта карта обеспечивает гибкую схему с несколькими разделами, полями, изображениями и действиями.</span><span class="sxs-lookup"><span data-stu-id="08c07-283">This card provides a flexible layout with multiple sections, fields, images, and actions.</span></span> <span data-ttu-id="08c07-284">Эта карта содержит соединителивую карту, чтобы она была использована ботами.</span><span class="sxs-lookup"><span data-stu-id="08c07-284">This card contains a connector card so that it can be used by bots.</span></span> <span data-ttu-id="08c07-285">О различиях между соединитеными картами и Office 365 соединитетелем см. в дополнительных сведениях о Office 365 [соединители.](#additional-information-on-the-office-365-connector-card)</span><span class="sxs-lookup"><span data-stu-id="08c07-285">For differences between connector cards and the Office 365 Connector card, see [Additional information on the Office 365 Connector card](#additional-information-on-the-office-365-connector-card).</span></span>

### <a name="support-for-office-365-connector-cards"></a><span data-ttu-id="08c07-286">Поддержка Office 365 соединители</span><span class="sxs-lookup"><span data-stu-id="08c07-286">Support for Office 365 Connector cards</span></span>

<span data-ttu-id="08c07-287">В следующей таблице представлены функции, поддерживают Office 365 соединители:</span><span class="sxs-lookup"><span data-stu-id="08c07-287">The following table provides the features that support Office 365 Connector cards:</span></span>

| <span data-ttu-id="08c07-288">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="08c07-288">Bots in Teams</span></span> | <span data-ttu-id="08c07-289">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="08c07-289">Messaging extensions</span></span>  | <span data-ttu-id="08c07-290">Соединители</span><span class="sxs-lookup"><span data-stu-id="08c07-290">Connectors</span></span> | <span data-ttu-id="08c07-291">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="08c07-291">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="08c07-292">✔</span><span class="sxs-lookup"><span data-stu-id="08c07-292">✔</span></span> | <span data-ttu-id="08c07-293">✔</span><span class="sxs-lookup"><span data-stu-id="08c07-293">✔</span></span> | <span data-ttu-id="08c07-294">✔</span><span class="sxs-lookup"><span data-stu-id="08c07-294">✔</span></span> | <span data-ttu-id="08c07-295">✖</span><span class="sxs-lookup"><span data-stu-id="08c07-295">✖</span></span> |

### <a name="properties-of-the-office-365-connector-card"></a><span data-ttu-id="08c07-296">Свойства карты Office 365 соединители</span><span class="sxs-lookup"><span data-stu-id="08c07-296">Properties of the Office 365 Connector card</span></span>

<span data-ttu-id="08c07-297">В следующей таблице ниже огосяты свойства Office 365 соединители:</span><span class="sxs-lookup"><span data-stu-id="08c07-297">The following table provides the properties of the Office 365 connector card:</span></span>

| <span data-ttu-id="08c07-298">Свойство</span><span class="sxs-lookup"><span data-stu-id="08c07-298">Property</span></span> | <span data-ttu-id="08c07-299">Тип</span><span class="sxs-lookup"><span data-stu-id="08c07-299">Type</span></span>  | <span data-ttu-id="08c07-300">Описание</span><span class="sxs-lookup"><span data-stu-id="08c07-300">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="08c07-301">title</span><span class="sxs-lookup"><span data-stu-id="08c07-301">title</span></span> | <span data-ttu-id="08c07-302">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="08c07-302">Rich text</span></span> | <span data-ttu-id="08c07-303">Название карты.</span><span class="sxs-lookup"><span data-stu-id="08c07-303">Title of the card.</span></span> <span data-ttu-id="08c07-304">Максимум две строки.</span><span class="sxs-lookup"><span data-stu-id="08c07-304">Maximum two lines.</span></span> |
| <span data-ttu-id="08c07-305">summary</span><span class="sxs-lookup"><span data-stu-id="08c07-305">summary</span></span> | <span data-ttu-id="08c07-306">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="08c07-306">Rich text</span></span> | <span data-ttu-id="08c07-307">Сводка карты.</span><span class="sxs-lookup"><span data-stu-id="08c07-307">Summary of the card.</span></span> <span data-ttu-id="08c07-308">Максимум две строки.</span><span class="sxs-lookup"><span data-stu-id="08c07-308">Maximum two lines.</span></span> |
| <span data-ttu-id="08c07-309">текст</span><span class="sxs-lookup"><span data-stu-id="08c07-309">text</span></span> | <span data-ttu-id="08c07-310">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="08c07-310">Rich text</span></span> | <span data-ttu-id="08c07-311">Текст отображается под субтитром.</span><span class="sxs-lookup"><span data-stu-id="08c07-311">Text appears under the subtitle.</span></span> <span data-ttu-id="08c07-312">Параметры форматирования см. [в виде форматирования карт.](~/task-modules-and-cards/cards/cards-format.md)</span><span class="sxs-lookup"><span data-stu-id="08c07-312">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="08c07-313">themeColor</span><span class="sxs-lookup"><span data-stu-id="08c07-313">themeColor</span></span> | <span data-ttu-id="08c07-314">Строка HEX</span><span class="sxs-lookup"><span data-stu-id="08c07-314">HEX string</span></span> | <span data-ttu-id="08c07-315">Цвет, который `accentColor` переопределяет предоставленные из манифеста приложения.</span><span class="sxs-lookup"><span data-stu-id="08c07-315">Color that overrides the `accentColor` provided from the application manifest.</span></span> |

### <a name="additional-information-on-the-office-365-connector-card"></a><span data-ttu-id="08c07-316">Дополнительные сведения о Office 365 соединители</span><span class="sxs-lookup"><span data-stu-id="08c07-316">Additional information on the Office 365 Connector card</span></span>

<span data-ttu-id="08c07-317">Office 365 Соединитетельные карты правильно функционируют в Microsoft Teams, включая [ `ActionCard` действия.](/outlook/actionable-messages/card-reference#actioncard-action)</span><span class="sxs-lookup"><span data-stu-id="08c07-317">Office 365 Connector cards function properly in Microsoft Teams, including [`ActionCard` actions](/outlook/actionable-messages/card-reference#actioncard-action).</span></span>

<span data-ttu-id="08c07-318">Важное отличие между использованием соединитеных карт из соединитетеля и использованием соединитеных карт в боте — обработка действий карт.</span><span class="sxs-lookup"><span data-stu-id="08c07-318">The important difference between using connector cards from a connector and using connector cards in your bot is the handling of card actions.</span></span> <span data-ttu-id="08c07-319">В следующей таблице перечислены различия:</span><span class="sxs-lookup"><span data-stu-id="08c07-319">The following table lists the difference:</span></span>

| <span data-ttu-id="08c07-320">Соединитель</span><span class="sxs-lookup"><span data-stu-id="08c07-320">Connector</span></span> | <span data-ttu-id="08c07-321">Бот</span><span class="sxs-lookup"><span data-stu-id="08c07-321">Bot</span></span> |
| --- | --- |
| <span data-ttu-id="08c07-322">Конечная точка получает полезной нагрузки карточки через HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="08c07-322">The endpoint receives the card payload through HTTP POST.</span></span> | <span data-ttu-id="08c07-323">Действие запускает действие, которое отправляет боту только ID действия `HttpPOST` `invoke` и тело.</span><span class="sxs-lookup"><span data-stu-id="08c07-323">The `HttpPOST` action triggers an `invoke` activity that sends only the action ID and body to the bot.</span></span>|

<span data-ttu-id="08c07-324">Каждая соединитечная карта может отображать не более десяти разделов, а каждый раздел может содержать не более пяти изображений и пять действий.</span><span class="sxs-lookup"><span data-stu-id="08c07-324">Each connector card can display a maximum of ten sections, and each section can contain a maximum of five images and five actions.</span></span>

> [!NOTE]
> <span data-ttu-id="08c07-325">Дополнительные разделы, изображения или действия в сообщении не отображаются.</span><span class="sxs-lookup"><span data-stu-id="08c07-325">Any additional sections, images, or actions in a message do not appear.</span></span>

<span data-ttu-id="08c07-326">Все текстовые поля поддерживают Markdown и HTML.</span><span class="sxs-lookup"><span data-stu-id="08c07-326">All text fields support Markdown and HTML.</span></span> <span data-ttu-id="08c07-327">Вы можете контролировать, какие разделы используют Markdown или HTML, установив `markdown` свойство в сообщении.</span><span class="sxs-lookup"><span data-stu-id="08c07-327">You can control which sections use Markdown or HTML by setting the `markdown` property in a message.</span></span> <span data-ttu-id="08c07-328">По умолчанию `markdown` установлено `true` значение .</span><span class="sxs-lookup"><span data-stu-id="08c07-328">By default, `markdown` is set to `true`.</span></span> <span data-ttu-id="08c07-329">Если вы хотите использовать HTML вместо этого, установите `markdown` `false` .</span><span class="sxs-lookup"><span data-stu-id="08c07-329">If you want to use HTML instead, set `markdown` to `false`.</span></span>

<span data-ttu-id="08c07-330">Если указать `themeColor` свойство, оно переопределит `accentColor` свойство в манифесте приложения.</span><span class="sxs-lookup"><span data-stu-id="08c07-330">If you specify the `themeColor` property, it overrides the `accentColor` property in the app manifest.</span></span>

<span data-ttu-id="08c07-331">Чтобы указать стиль визуализации, можно задать, `activityImage` `activityImageType` как показано в следующей таблице:</span><span class="sxs-lookup"><span data-stu-id="08c07-331">To specify the rendering style for `activityImage`, you can set `activityImageType` as shown in the following table:</span></span>

| <span data-ttu-id="08c07-332">Значение</span><span class="sxs-lookup"><span data-stu-id="08c07-332">Value</span></span> | <span data-ttu-id="08c07-333">Описание</span><span class="sxs-lookup"><span data-stu-id="08c07-333">Description</span></span> |
| --- | --- |
| `avatar` | <span data-ttu-id="08c07-334">По умолчанию `activityImage` обрезается как круг.</span><span class="sxs-lookup"><span data-stu-id="08c07-334">Default, `activityImage` is cropped as a circle.</span></span> |
| `article` | <span data-ttu-id="08c07-335">`activityImage` отображается в качестве прямоугольника и сохраняет отношение аспектов.</span><span class="sxs-lookup"><span data-stu-id="08c07-335">`activityImage` is displayed as a rectangle and retains its aspect ratio.</span></span> |

<span data-ttu-id="08c07-336">Другие сведения о свойствах карт соединители см. в справке к карточкам [сообщений.](/outlook/actionable-messages/card-reference)</span><span class="sxs-lookup"><span data-stu-id="08c07-336">For all other details about connector card properties, see [actionable message card reference](/outlook/actionable-messages/card-reference).</span></span> <span data-ttu-id="08c07-337">Единственными свойствами карт соединители, Teams которые в настоящее время не поддерживаются, являются следующими:</span><span class="sxs-lookup"><span data-stu-id="08c07-337">The only connector card properties that Teams does not currently support are as follows:</span></span>

* `heroImage`
* `hideOriginalBody`
* <span data-ttu-id="08c07-338">`startGroup`всегда рассматривается как `true` в Teams</span><span class="sxs-lookup"><span data-stu-id="08c07-338">`startGroup` always treated as `true` in Teams</span></span>
* `originator`
* `correlationId`

### <a name="example-of-an-office-365-connector-card"></a><span data-ttu-id="08c07-339">Пример карты Office 365 соединители</span><span class="sxs-lookup"><span data-stu-id="08c07-339">Example of an Office 365 Connector card</span></span>

<span data-ttu-id="08c07-340">В следующем коде показан пример карты Office 365 соединители:</span><span class="sxs-lookup"><span data-stu-id="08c07-340">The following code shows an example of an Office 365 Connector card:</span></span>

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

## <a name="receipt-card"></a><span data-ttu-id="08c07-341">Карта получения</span><span class="sxs-lookup"><span data-stu-id="08c07-341">Receipt card</span></span>

<span data-ttu-id="08c07-342">Teams поддерживает карточку получения.</span><span class="sxs-lookup"><span data-stu-id="08c07-342">Teams supports receipt card.</span></span> <span data-ttu-id="08c07-343">Это карточка, которая позволяет боту предоставлять пользователю квитанцию.</span><span class="sxs-lookup"><span data-stu-id="08c07-343">It is a card that enables a bot to provide a receipt to the user.</span></span> <span data-ttu-id="08c07-344">Обычно он содержит список элементов, которые необходимо включить в квитанцию, например налоговые и общие сведения.</span><span class="sxs-lookup"><span data-stu-id="08c07-344">It typically contains the list of items to include on the receipt, such as tax and total information.</span></span>

### <a name="support-for-receipt-cards"></a><span data-ttu-id="08c07-345">Поддержка карт получения</span><span class="sxs-lookup"><span data-stu-id="08c07-345">Support for receipt cards</span></span>

<span data-ttu-id="08c07-346">В следующей таблице представлены функции, поддерживают карты получения:</span><span class="sxs-lookup"><span data-stu-id="08c07-346">The following table provides the features that support receipt cards:</span></span>

| <span data-ttu-id="08c07-347">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="08c07-347">Bots in Teams</span></span> | <span data-ttu-id="08c07-348">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="08c07-348">Messaging extensions</span></span>  | <span data-ttu-id="08c07-349">Соединители</span><span class="sxs-lookup"><span data-stu-id="08c07-349">Connectors</span></span> | <span data-ttu-id="08c07-350">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="08c07-350">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="08c07-351">✔</span><span class="sxs-lookup"><span data-stu-id="08c07-351">✔</span></span> | <span data-ttu-id="08c07-352">✔</span><span class="sxs-lookup"><span data-stu-id="08c07-352">✔</span></span> | <span data-ttu-id="08c07-353">✖</span><span class="sxs-lookup"><span data-stu-id="08c07-353">✖</span></span> | <span data-ttu-id="08c07-354">✔</span><span class="sxs-lookup"><span data-stu-id="08c07-354">✔</span></span> |

### <a name="example-of-a-receipt-card"></a><span data-ttu-id="08c07-355">Пример карты получения</span><span class="sxs-lookup"><span data-stu-id="08c07-355">Example of a receipt card</span></span>

![Пример карты получения](~/assets/images/cards/receipt.png)

<span data-ttu-id="08c07-357">В следующем коде показан пример карточки получения:</span><span class="sxs-lookup"><span data-stu-id="08c07-357">The following code shows an example of a receipt card:</span></span>

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

### <a name="additional-information-on-receipt-cards"></a><span data-ttu-id="08c07-358">Дополнительные сведения о карточках получения</span><span class="sxs-lookup"><span data-stu-id="08c07-358">Additional information on receipt cards</span></span>

<span data-ttu-id="08c07-359">Ссылка на Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="08c07-359">Bot Framework reference:</span></span>

* [<span data-ttu-id="08c07-360">Карточка получения Node.js</span><span class="sxs-lookup"><span data-stu-id="08c07-360">Receipt card Node.js</span></span>](/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="08c07-361">Карта получения C #</span><span class="sxs-lookup"><span data-stu-id="08c07-361">Receipt card C#</span></span>](/dotnet/api/microsoft.bot.schema.receiptcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="signin-card"></a><span data-ttu-id="08c07-362">Карточка Signin</span><span class="sxs-lookup"><span data-stu-id="08c07-362">Signin card</span></span>

<span data-ttu-id="08c07-363">Карта signin в Teams похожа на карточку signin в Bot Framework, за исключением того, что карта signin в Teams поддерживает только два действия `signin` и `openUrl` .</span><span class="sxs-lookup"><span data-stu-id="08c07-363">The signin card in Teams is similar to the signin card in the Bot Framework except that the signin card in Teams only supports two actions `signin` and `openUrl`.</span></span>

<span data-ttu-id="08c07-364">Действие signin можно использовать с любой карты в Teams, а не только с карты signin.</span><span class="sxs-lookup"><span data-stu-id="08c07-364">The signin action can be used from any card in Teams, not just the signin card.</span></span> <span data-ttu-id="08c07-365">Дополнительные сведения см. [в Teams поток проверки подлинности для ботов.](~/bots/how-to/authentication/auth-flow-bot.md)</span><span class="sxs-lookup"><span data-stu-id="08c07-365">For more information, see [Teams authentication flow for bots](~/bots/how-to/authentication/auth-flow-bot.md).</span></span>

### <a name="support-for-signin-cards"></a><span data-ttu-id="08c07-366">Поддержка подписных карт</span><span class="sxs-lookup"><span data-stu-id="08c07-366">Support for signin cards</span></span>

<span data-ttu-id="08c07-367">В следующей таблице представлены функции, поддерживают знаковые карточки:</span><span class="sxs-lookup"><span data-stu-id="08c07-367">The following table provides the features that support signin cards:</span></span>

| <span data-ttu-id="08c07-368">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="08c07-368">Bots in Teams</span></span> | <span data-ttu-id="08c07-369">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="08c07-369">Messaging extensions</span></span>  | <span data-ttu-id="08c07-370">Соединители</span><span class="sxs-lookup"><span data-stu-id="08c07-370">Connectors</span></span> | <span data-ttu-id="08c07-371">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="08c07-371">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="08c07-372">✔</span><span class="sxs-lookup"><span data-stu-id="08c07-372">✔</span></span> | <span data-ttu-id="08c07-373">✖</span><span class="sxs-lookup"><span data-stu-id="08c07-373">✖</span></span> | <span data-ttu-id="08c07-374">✖</span><span class="sxs-lookup"><span data-stu-id="08c07-374">✖</span></span> | <span data-ttu-id="08c07-375">✔</span><span class="sxs-lookup"><span data-stu-id="08c07-375">✔</span></span> |

### <a name="additional-information-on-signin-cards"></a><span data-ttu-id="08c07-376">Дополнительные сведения о подписных карточках</span><span class="sxs-lookup"><span data-stu-id="08c07-376">Additional information on signin cards</span></span>

<span data-ttu-id="08c07-377">Ссылка на Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="08c07-377">Bot Framework reference:</span></span>

* [<span data-ttu-id="08c07-378">Карточка signin Node.js</span><span class="sxs-lookup"><span data-stu-id="08c07-378">Signin card Node.js</span></span>](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="08c07-379">Signin card C #</span><span class="sxs-lookup"><span data-stu-id="08c07-379">Signin card C#</span></span>](/dotnet/api/microsoft.bot.schema.signincard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="thumbnail-card"></a><span data-ttu-id="08c07-380">Карта эскиза</span><span class="sxs-lookup"><span data-stu-id="08c07-380">Thumbnail card</span></span>

<span data-ttu-id="08c07-381">Вы можете работать с картой эскизов, которая используется для отправки простого действия сообщения.</span><span class="sxs-lookup"><span data-stu-id="08c07-381">You can work with a thumbnail card that is used for sending a simple actionable message.</span></span> <span data-ttu-id="08c07-382">Карточка, которая обычно содержит одно изображение эскиза, одну или несколько кнопок и текст.</span><span class="sxs-lookup"><span data-stu-id="08c07-382">A card that typically contains a single thumbnail image, one or more buttons, and text.</span></span>

### <a name="support-for-thumbnail-cards"></a><span data-ttu-id="08c07-383">Поддержка карт эскизов</span><span class="sxs-lookup"><span data-stu-id="08c07-383">Support for thumbnail cards</span></span>

<span data-ttu-id="08c07-384">В следующей таблице представлены функции, поддерживают эскизные карты:</span><span class="sxs-lookup"><span data-stu-id="08c07-384">The following table provides the features that support thumbnail cards:</span></span>

| <span data-ttu-id="08c07-385">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="08c07-385">Bots in Teams</span></span> | <span data-ttu-id="08c07-386">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="08c07-386">Messaging extensions</span></span>  | <span data-ttu-id="08c07-387">Соединители</span><span class="sxs-lookup"><span data-stu-id="08c07-387">Connectors</span></span> | <span data-ttu-id="08c07-388">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="08c07-388">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="08c07-389">✔</span><span class="sxs-lookup"><span data-stu-id="08c07-389">✔</span></span> | <span data-ttu-id="08c07-390">✔</span><span class="sxs-lookup"><span data-stu-id="08c07-390">✔</span></span> | <span data-ttu-id="08c07-391">✖</span><span class="sxs-lookup"><span data-stu-id="08c07-391">✖</span></span> | <span data-ttu-id="08c07-392">✔</span><span class="sxs-lookup"><span data-stu-id="08c07-392">✔</span></span> |

![Пример карты эскиза](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a><span data-ttu-id="08c07-394">Свойства карты эскиза</span><span class="sxs-lookup"><span data-stu-id="08c07-394">Properties of a thumbnail card</span></span>

<span data-ttu-id="08c07-395">Следующая таблица содержит свойства карты эскиза:</span><span class="sxs-lookup"><span data-stu-id="08c07-395">The following table provides the properties of a thumbnail card:</span></span>

| <span data-ttu-id="08c07-396">Свойство</span><span class="sxs-lookup"><span data-stu-id="08c07-396">Property</span></span> | <span data-ttu-id="08c07-397">Тип</span><span class="sxs-lookup"><span data-stu-id="08c07-397">Type</span></span>  | <span data-ttu-id="08c07-398">Описание</span><span class="sxs-lookup"><span data-stu-id="08c07-398">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="08c07-399">title</span><span class="sxs-lookup"><span data-stu-id="08c07-399">title</span></span> | <span data-ttu-id="08c07-400">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="08c07-400">Rich text</span></span> | <span data-ttu-id="08c07-401">Название карты.</span><span class="sxs-lookup"><span data-stu-id="08c07-401">Title of the card.</span></span> <span data-ttu-id="08c07-402">Максимум 2 строки.</span><span class="sxs-lookup"><span data-stu-id="08c07-402">Maximum 2 lines.</span></span>|
| <span data-ttu-id="08c07-403">субтитры</span><span class="sxs-lookup"><span data-stu-id="08c07-403">subtitle</span></span> | <span data-ttu-id="08c07-404">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="08c07-404">Rich text</span></span> | <span data-ttu-id="08c07-405">Субтитр карты.</span><span class="sxs-lookup"><span data-stu-id="08c07-405">Subtitle of the card.</span></span> <span data-ttu-id="08c07-406">Максимум 2 строки.</span><span class="sxs-lookup"><span data-stu-id="08c07-406">Maximum 2 lines.</span></span>|
| <span data-ttu-id="08c07-407">текст</span><span class="sxs-lookup"><span data-stu-id="08c07-407">text</span></span> | <span data-ttu-id="08c07-408">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="08c07-408">Rich text</span></span> | <span data-ttu-id="08c07-409">Текст отображается под субтитром.</span><span class="sxs-lookup"><span data-stu-id="08c07-409">Text appears under the subtitle.</span></span> <span data-ttu-id="08c07-410">Параметры форматирования см. [в виде форматирования карт.](~/task-modules-and-cards/cards/cards-format.md)</span><span class="sxs-lookup"><span data-stu-id="08c07-410">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="08c07-411">изображения</span><span class="sxs-lookup"><span data-stu-id="08c07-411">images</span></span> | <span data-ttu-id="08c07-412">Массив изображений</span><span class="sxs-lookup"><span data-stu-id="08c07-412">Array of images</span></span> | <span data-ttu-id="08c07-413">Изображение, отображаемого в верхней части карты.</span><span class="sxs-lookup"><span data-stu-id="08c07-413">Image displayed at the top of the card.</span></span> <span data-ttu-id="08c07-414">Отношение аспектов 1:1 к квадрату.</span><span class="sxs-lookup"><span data-stu-id="08c07-414">Aspect ratio 1:1 square.</span></span> |
| <span data-ttu-id="08c07-415">кнопки</span><span class="sxs-lookup"><span data-stu-id="08c07-415">buttons</span></span> | <span data-ttu-id="08c07-416">Массив объектов действий</span><span class="sxs-lookup"><span data-stu-id="08c07-416">Array of action objects</span></span> | <span data-ttu-id="08c07-417">Набор действий, применимых к текущей карте.</span><span class="sxs-lookup"><span data-stu-id="08c07-417">Set of actions applicable to the current card.</span></span> <span data-ttu-id="08c07-418">Максимум 6.</span><span class="sxs-lookup"><span data-stu-id="08c07-418">Maximum 6.</span></span> |
| <span data-ttu-id="08c07-419">нажмите кнопку</span><span class="sxs-lookup"><span data-stu-id="08c07-419">tap</span></span> | <span data-ttu-id="08c07-420">Объект Action</span><span class="sxs-lookup"><span data-stu-id="08c07-420">Action object</span></span> | <span data-ttu-id="08c07-421">Активируется при нажатии на карточку самого пользователя.</span><span class="sxs-lookup"><span data-stu-id="08c07-421">Activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-thumbnail-card"></a><span data-ttu-id="08c07-422">Пример карты эскиза</span><span class="sxs-lookup"><span data-stu-id="08c07-422">Example of a thumbnail card</span></span>

<span data-ttu-id="08c07-423">В следующем коде показан пример карты эскиза:</span><span class="sxs-lookup"><span data-stu-id="08c07-423">The following code shows an example of a thumbnail card:</span></span>

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

### <a name="additional-information"></a><span data-ttu-id="08c07-424">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="08c07-424">Additional information</span></span>

<span data-ttu-id="08c07-425">Ссылка на Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="08c07-425">Bot Framework reference:</span></span>

* [<span data-ttu-id="08c07-426">Эскиз карты Node.js</span><span class="sxs-lookup"><span data-stu-id="08c07-426">Thumbnail card Node.js</span></span>](/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="08c07-427">Эскиз карты C #</span><span class="sxs-lookup"><span data-stu-id="08c07-427">Thumbnail card C#</span></span>](/dotnet/api/microsoft.bot.schema.thumbnailcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="card-collections"></a><span data-ttu-id="08c07-428">Коллекции карт</span><span class="sxs-lookup"><span data-stu-id="08c07-428">Card collections</span></span>

<span data-ttu-id="08c07-429">Вы можете работать с коллекциями карт, которые включают карусель и коллекции списков.</span><span class="sxs-lookup"><span data-stu-id="08c07-429">You can work with card collections that include carousel and list collections.</span></span> <span data-ttu-id="08c07-430">Teams поддерживает коллекции карт.</span><span class="sxs-lookup"><span data-stu-id="08c07-430">Teams supports card collections.</span></span> <span data-ttu-id="08c07-431">Коллекции карт включают `builder.AttachmentLayout.carousel` и `builder.AttachmentLayout.list` .</span><span class="sxs-lookup"><span data-stu-id="08c07-431">Card collections include `builder.AttachmentLayout.carousel` and `builder.AttachmentLayout.list`.</span></span> <span data-ttu-id="08c07-432">Эти коллекции содержат адаптивные, герой или эскизные карточки.</span><span class="sxs-lookup"><span data-stu-id="08c07-432">These collections contain Adaptive, hero, or thumbnail cards.</span></span>

### <a name="carousel-collection"></a><span data-ttu-id="08c07-433">Коллекция Карусель</span><span class="sxs-lookup"><span data-stu-id="08c07-433">Carousel collection</span></span>

<span data-ttu-id="08c07-434">Макет [карусель показывает](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) карусель карт, необязательно с связанными кнопками действия.</span><span class="sxs-lookup"><span data-stu-id="08c07-434">The [carousel layout](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) shows a carousel of cards, optionally with associated action buttons.</span></span>

#### <a name="support-for-carousel-collections"></a><span data-ttu-id="08c07-435">Поддержка коллекций карусель</span><span class="sxs-lookup"><span data-stu-id="08c07-435">Support for carousel collections</span></span>

<span data-ttu-id="08c07-436">В следующей таблице представлены функции, поддерживают коллекции карусель:</span><span class="sxs-lookup"><span data-stu-id="08c07-436">The following table provides the features that support carousel collections:</span></span>

| <span data-ttu-id="08c07-437">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="08c07-437">Bots in Teams</span></span> | <span data-ttu-id="08c07-438">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="08c07-438">Messaging extensions</span></span>  | <span data-ttu-id="08c07-439">Соединители</span><span class="sxs-lookup"><span data-stu-id="08c07-439">Connectors</span></span> | <span data-ttu-id="08c07-440">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="08c07-440">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="08c07-441">✔</span><span class="sxs-lookup"><span data-stu-id="08c07-441">✔</span></span> | <span data-ttu-id="08c07-442">✖</span><span class="sxs-lookup"><span data-stu-id="08c07-442">✖</span></span> | <span data-ttu-id="08c07-443">✖</span><span class="sxs-lookup"><span data-stu-id="08c07-443">✖</span></span> | <span data-ttu-id="08c07-444">✔</span><span class="sxs-lookup"><span data-stu-id="08c07-444">✔</span></span> |

> [!NOTE]
> <span data-ttu-id="08c07-445">Карусель может отображать не более десяти карт на сообщение.</span><span class="sxs-lookup"><span data-stu-id="08c07-445">A carousel can display a maximum of ten cards per message.</span></span>

#### <a name="properties-of-a-carousel-card"></a><span data-ttu-id="08c07-446">Свойства карусели</span><span class="sxs-lookup"><span data-stu-id="08c07-446">Properties of a carousel card</span></span>

<span data-ttu-id="08c07-447">Свойства карусельной карты такие же, как и у карт героя и эскиза.</span><span class="sxs-lookup"><span data-stu-id="08c07-447">Properties of a carousel card are same as the hero and thumbnail cards.</span></span>

#### <a name="example-of-a-carousel-collection"></a><span data-ttu-id="08c07-448">Пример коллекции карусель</span><span class="sxs-lookup"><span data-stu-id="08c07-448">Example of a carousel collection</span></span>

![Пример карусели карт](~/assets/images/cards/carousel.png)

<span data-ttu-id="08c07-450">В следующем коде показан пример коллекции карусели:</span><span class="sxs-lookup"><span data-stu-id="08c07-450">The following code shows an example of a carousel collection:</span></span>

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

#### <a name="syntax-for-carousel-collections"></a><span data-ttu-id="08c07-451">Синтаксис для коллекций карусели</span><span class="sxs-lookup"><span data-stu-id="08c07-451">Syntax for carousel collections</span></span>

<span data-ttu-id="08c07-452">`builder.AttachmentLayoutTypes.Carousel` синтаксис для коллекций карусели.</span><span class="sxs-lookup"><span data-stu-id="08c07-452">`builder.AttachmentLayoutTypes.Carousel` is the syntax for carousel collections.</span></span>

### <a name="list-collection"></a><span data-ttu-id="08c07-453">Коллекция списков</span><span class="sxs-lookup"><span data-stu-id="08c07-453">List collection</span></span>

<span data-ttu-id="08c07-454">В макете списка показан вертикально сложенный список карт, необязательно связанный с кнопками действия.</span><span class="sxs-lookup"><span data-stu-id="08c07-454">The list layout shows a vertically stacked list of cards, optionally with associated action buttons.</span></span>

#### <a name="support-for-list-collections"></a><span data-ttu-id="08c07-455">Поддержка коллекций списков</span><span class="sxs-lookup"><span data-stu-id="08c07-455">Support for list collections</span></span>

<span data-ttu-id="08c07-456">В следующей таблице представлены функции, поддерживают коллекции списков:</span><span class="sxs-lookup"><span data-stu-id="08c07-456">The following table provides the features that support list collections:</span></span>

| <span data-ttu-id="08c07-457">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="08c07-457">Bots in Teams</span></span> | <span data-ttu-id="08c07-458">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="08c07-458">Messaging extensions</span></span>  | <span data-ttu-id="08c07-459">Соединители</span><span class="sxs-lookup"><span data-stu-id="08c07-459">Connectors</span></span> | <span data-ttu-id="08c07-460">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="08c07-460">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="08c07-461">✔</span><span class="sxs-lookup"><span data-stu-id="08c07-461">✔</span></span> | <span data-ttu-id="08c07-462">✔</span><span class="sxs-lookup"><span data-stu-id="08c07-462">✔</span></span> | <span data-ttu-id="08c07-463">✖</span><span class="sxs-lookup"><span data-stu-id="08c07-463">✖</span></span> | <span data-ttu-id="08c07-464">✔</span><span class="sxs-lookup"><span data-stu-id="08c07-464">✔</span></span> |

#### <a name="example-of-a-list-collection"></a><span data-ttu-id="08c07-465">Пример коллекции списков</span><span class="sxs-lookup"><span data-stu-id="08c07-465">Example of a list collection</span></span>

![Пример списка карт](~/assets/images/cards/list.png)

<span data-ttu-id="08c07-467">Свойства коллекций списков одинаковы с картами героя или эскиза.</span><span class="sxs-lookup"><span data-stu-id="08c07-467">Properties of list collections are same as the hero or thumbnail cards.</span></span>

<span data-ttu-id="08c07-468">В списке может отображаться не более десяти карт на сообщение.</span><span class="sxs-lookup"><span data-stu-id="08c07-468">A list can display a maximum of ten cards per message.</span></span>

> [!NOTE]
> <span data-ttu-id="08c07-469">Некоторые сочетания карт списка еще не поддерживаются на iOS и Android.</span><span class="sxs-lookup"><span data-stu-id="08c07-469">Some combinations of list cards are not yet supported on iOS and Android.</span></span>

#### <a name="syntax-for-list-collections"></a><span data-ttu-id="08c07-470">Синтаксис для коллекций списков</span><span class="sxs-lookup"><span data-stu-id="08c07-470">Syntax for list collections</span></span>

<span data-ttu-id="08c07-471">`builder.AttachmentLayout.list` синтаксис для коллекций списков.</span><span class="sxs-lookup"><span data-stu-id="08c07-471">`builder.AttachmentLayout.list` is the syntax for list collections.</span></span>

## <a name="cards-not-supported-in-teams"></a><span data-ttu-id="08c07-472">Карты, не поддерживаемые в Teams</span><span class="sxs-lookup"><span data-stu-id="08c07-472">Cards not supported in Teams</span></span>

<span data-ttu-id="08c07-473">Следующие карты реализуются в рамках Bot Framework, но не поддерживаются Teams:</span><span class="sxs-lookup"><span data-stu-id="08c07-473">The following cards are implemented by the Bot Framework, but are not supported by Teams:</span></span>

* <span data-ttu-id="08c07-474">Карты анимации</span><span class="sxs-lookup"><span data-stu-id="08c07-474">Animation cards</span></span>
* <span data-ttu-id="08c07-475">Аудиокарты</span><span class="sxs-lookup"><span data-stu-id="08c07-475">Audio cards</span></span>
* <span data-ttu-id="08c07-476">Видеокарты</span><span class="sxs-lookup"><span data-stu-id="08c07-476">Video cards</span></span>

## <a name="see-also"></a><span data-ttu-id="08c07-477">См. также</span><span class="sxs-lookup"><span data-stu-id="08c07-477">See also</span></span>

* [<span data-ttu-id="08c07-478">Модули задач</span><span class="sxs-lookup"><span data-stu-id="08c07-478">Task modules</span></span>](~/task-modules-and-cards/what-are-task-modules.md)
* [<span data-ttu-id="08c07-479">Форматные карты</span><span class="sxs-lookup"><span data-stu-id="08c07-479">Format cards</span></span>](~/task-modules-and-cards/cards/cards-format.md)
