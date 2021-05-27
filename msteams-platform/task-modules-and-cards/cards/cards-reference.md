---
title: Ссылки на карточки
description: Описывает все действия карт и карт, доступные ботам в Teams
localization_priority: Normal
keywords: ссылка на карточки ботов
ms.topic: reference
ms.openlocfilehash: d3f0904326f951475c8a0d3e17daf720d9aad489
ms.sourcegitcommit: c59d90ae03eae32996db49f162855965b55c52fe
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/26/2021
ms.locfileid: "52668864"
---
# <a name="cards-reference"></a><span data-ttu-id="4f35e-104">Ссылки на карточки</span><span class="sxs-lookup"><span data-stu-id="4f35e-104">Cards reference</span></span>

<span data-ttu-id="4f35e-105">Карты, перечисленные в этом документе, поддерживаются в ботах для Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="4f35e-105">The cards listed in this document are supported in bots for Microsoft Teams.</span></span> <span data-ttu-id="4f35e-106">Они основаны на картах, определенных bot Framework (BF), но Teams не поддерживает все карты Bot Framework и вместо этого были добавлены некоторые Teams карты.</span><span class="sxs-lookup"><span data-stu-id="4f35e-106">They are based on cards defined by the Bot Framework (BF), but Teams does not support all Bot Framework cards and instead some Teams cards have been added.</span></span> <span data-ttu-id="4f35e-107">Различия называются в ссылках в этом документе.</span><span class="sxs-lookup"><span data-stu-id="4f35e-107">Differences are called out in the references in this document.</span></span>

## <a name="card-examples"></a><span data-ttu-id="4f35e-108">Примеры карт</span><span class="sxs-lookup"><span data-stu-id="4f35e-108">Card examples</span></span>

<span data-ttu-id="4f35e-109">Дополнительные сведения об использовании карт можно найти в документации для bot Builder SDK v3.</span><span class="sxs-lookup"><span data-stu-id="4f35e-109">You can find additional information on how to use cards in the documentation for the Bot Builder SDK v3.</span></span> <span data-ttu-id="4f35e-110">Примеры кода также доступны в репозитории Microsoft/BotBuilder-Samples на GitHub.</span><span class="sxs-lookup"><span data-stu-id="4f35e-110">Code samples are also available in the Microsoft/BotBuilder-Samples repository on GitHub.</span></span>

* <span data-ttu-id="4f35e-111">.NET</span><span class="sxs-lookup"><span data-stu-id="4f35e-111">.NET</span></span>
  * <span data-ttu-id="4f35e-112">[Добавление карт в виде вложений в сообщения.](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="4f35e-112">[Add cards as attachments to messages](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true).</span></span>
  * <span data-ttu-id="4f35e-113">[Карты пример кода Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards).</span><span class="sxs-lookup"><span data-stu-id="4f35e-113">[Cards sample code Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards).</span></span>

* <span data-ttu-id="4f35e-114">Node.js</span><span class="sxs-lookup"><span data-stu-id="4f35e-114">Node.js</span></span>
  * <span data-ttu-id="4f35e-115">[Добавление карт в виде вложений в сообщения.](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="4f35e-115">[Add cards as attachments to messages](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true).</span></span>
  * <span data-ttu-id="4f35e-116">[Карты пример кода Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards).</span><span class="sxs-lookup"><span data-stu-id="4f35e-116">[Cards sample code Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards).</span></span>

## <a name="types-of-cards"></a><span data-ttu-id="4f35e-117">Типы карт</span><span class="sxs-lookup"><span data-stu-id="4f35e-117">Types of cards</span></span>

<span data-ttu-id="4f35e-118">В этой таблице показаны типы доступных вам карт:</span><span class="sxs-lookup"><span data-stu-id="4f35e-118">This table shows the types of cards available to you:</span></span>

| <span data-ttu-id="4f35e-119">Тип карты</span><span class="sxs-lookup"><span data-stu-id="4f35e-119">Card type</span></span> | <span data-ttu-id="4f35e-120">Описание</span><span class="sxs-lookup"><span data-stu-id="4f35e-120">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="4f35e-121">Адаптивная карта</span><span class="sxs-lookup"><span data-stu-id="4f35e-121">Adaptive card</span></span>](#adaptive-card) | <span data-ttu-id="4f35e-122">Эта карта является высоко настраиваемой картой, которая может содержать любое сочетание текстов, речи, изображений, кнопок и полей ввода.</span><span class="sxs-lookup"><span data-stu-id="4f35e-122">This card is highly customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> |
| [<span data-ttu-id="4f35e-123">Карта hero</span><span class="sxs-lookup"><span data-stu-id="4f35e-123">Hero card</span></span>](#hero-card) | <span data-ttu-id="4f35e-124">Эта карта обычно содержит одно большое изображение, одну или несколько кнопок и небольшое количество текста.</span><span class="sxs-lookup"><span data-stu-id="4f35e-124">This card typically contains a single large image, one or more buttons, and a small amount of text.</span></span> |
| [<span data-ttu-id="4f35e-125">Карта списка</span><span class="sxs-lookup"><span data-stu-id="4f35e-125">List card</span></span>](#list-card) | <span data-ttu-id="4f35e-126">Эта карта — это список элементов прокрутки.</span><span class="sxs-lookup"><span data-stu-id="4f35e-126">This card is a scrolling list of items.</span></span> |
| [<span data-ttu-id="4f35e-127">Office 365 соединители</span><span class="sxs-lookup"><span data-stu-id="4f35e-127">Office 365 connector card</span></span>](#office-365-connector-card) | <span data-ttu-id="4f35e-128">Эта карта имеет гибкий макет с несколькими разделами, полями, изображениями и действиями.</span><span class="sxs-lookup"><span data-stu-id="4f35e-128">This card has a flexible layout with multiple sections, fields, images, and actions.</span></span> |
| [<span data-ttu-id="4f35e-129">Карта получения</span><span class="sxs-lookup"><span data-stu-id="4f35e-129">Receipt card</span></span>](#receipt-card) | <span data-ttu-id="4f35e-130">Эта карта предоставляет квитанцию пользователю.</span><span class="sxs-lookup"><span data-stu-id="4f35e-130">This card provides a receipt to the user.</span></span> |
| [<span data-ttu-id="4f35e-131">Карточка Signin</span><span class="sxs-lookup"><span data-stu-id="4f35e-131">Signin card</span></span>](#signin-card) | <span data-ttu-id="4f35e-132">Эта карта позволяет боту запрашивать, чтобы пользователь войди.</span><span class="sxs-lookup"><span data-stu-id="4f35e-132">This card enables a bot to request that a user signs in.</span></span> |
| [<span data-ttu-id="4f35e-133">Карта эскиза</span><span class="sxs-lookup"><span data-stu-id="4f35e-133">Thumbnail card</span></span>](#thumbnail-card) | <span data-ttu-id="4f35e-134">Эта карта обычно содержит одно изображение эскиза, короткий текст и одну или несколько кнопок.</span><span class="sxs-lookup"><span data-stu-id="4f35e-134">This card typically contains a single thumbnail image, some short text, and one or more buttons.</span></span> |
| [<span data-ttu-id="4f35e-135">Коллекции карт</span><span class="sxs-lookup"><span data-stu-id="4f35e-135">Card collections</span></span>](#card-collections) | <span data-ttu-id="4f35e-136">Эти карты используются для возврата нескольких элементов в одном ответе.</span><span class="sxs-lookup"><span data-stu-id="4f35e-136">This cards is used to return multiple items in a single response.</span></span> |

## <a name="common-properties-for-all-cards"></a><span data-ttu-id="4f35e-137">Общие свойства для всех карт</span><span class="sxs-lookup"><span data-stu-id="4f35e-137">Common properties for all cards</span></span>

### <a name="inline-card-images"></a><span data-ttu-id="4f35e-138">Inline card images</span><span class="sxs-lookup"><span data-stu-id="4f35e-138">Inline card images</span></span>

<span data-ttu-id="4f35e-139">Карта может содержать рядное изображение, включив ссылку на общедоступный образ.</span><span class="sxs-lookup"><span data-stu-id="4f35e-139">The card can contain an inline image by including a link to the publicly available image.</span></span> <span data-ttu-id="4f35e-140">В целях производительности рекомендуется использовать изображение в общедоступных сетях доставки контента (CDN).</span><span class="sxs-lookup"><span data-stu-id="4f35e-140">For performance purposes, it is highly recommended you host the image on a public content-delivery network (CDN).</span></span>

<span data-ttu-id="4f35e-141">Изображения масштабироваться или по размеру при сохранении соотношения аспектов для покрытия области изображения.</span><span class="sxs-lookup"><span data-stu-id="4f35e-141">Images are scaled up or down in size while maintaining the aspect ratio to cover the image area.</span></span> <span data-ttu-id="4f35e-142">Затем изображения обрезаются из центра, чтобы достичь соответствующего соотношения аспектов для карты.</span><span class="sxs-lookup"><span data-stu-id="4f35e-142">Images are then cropped from center to achieve the appropriate aspect ratio for the card.</span></span>

<span data-ttu-id="4f35e-143">Изображения должны быть не более 1024×1024 в формате PNG, JPEG или GIF и не поддерживают анимированный GIF.</span><span class="sxs-lookup"><span data-stu-id="4f35e-143">Images must be at most 1024×1024, in PNG, JPEG, or GIF format, and do not support animated GIF.</span></span>

| <span data-ttu-id="4f35e-144">Свойство</span><span class="sxs-lookup"><span data-stu-id="4f35e-144">Property</span></span> | <span data-ttu-id="4f35e-145">Тип</span><span class="sxs-lookup"><span data-stu-id="4f35e-145">Type</span></span>  | <span data-ttu-id="4f35e-146">Описание</span><span class="sxs-lookup"><span data-stu-id="4f35e-146">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4f35e-147">url</span><span class="sxs-lookup"><span data-stu-id="4f35e-147">url</span></span> | <span data-ttu-id="4f35e-148">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="4f35e-148">URL</span></span> | <span data-ttu-id="4f35e-149">URL-адрес HTTPS к изображению.</span><span class="sxs-lookup"><span data-stu-id="4f35e-149">HTTPS URL to the image.</span></span> |
| <span data-ttu-id="4f35e-150">alt</span><span class="sxs-lookup"><span data-stu-id="4f35e-150">alt</span></span> | <span data-ttu-id="4f35e-151">String</span><span class="sxs-lookup"><span data-stu-id="4f35e-151">String</span></span> | <span data-ttu-id="4f35e-152">Доступное описание изображения.</span><span class="sxs-lookup"><span data-stu-id="4f35e-152">Accessible description of the image.</span></span> |

> [!NOTE]
> <span data-ttu-id="4f35e-153">Если карта содержит URL-адрес изображения, который проходит перенаправление перед окончательным изображением, перенаправление в URL-адрес изображения не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="4f35e-153">If a card includes an image URL that goes through a redirect before the final image, the redirect in image URL is not supported.</span></span> <span data-ttu-id="4f35e-154">Это происходит для изображений, общих в общедоступных облаках.</span><span class="sxs-lookup"><span data-stu-id="4f35e-154">This occurs for images shared on the public cloud.</span></span>

### <a name="buttons"></a><span data-ttu-id="4f35e-155">Кнопки</span><span class="sxs-lookup"><span data-stu-id="4f35e-155">Buttons</span></span>

<span data-ttu-id="4f35e-156">Кнопки показаны в нижней части карты.</span><span class="sxs-lookup"><span data-stu-id="4f35e-156">Buttons are shown stacked at the bottom of the card.</span></span> <span data-ttu-id="4f35e-157">Текст кнопки всегда находится в одной строке и усечен, если текст превышает ширину кнопки.</span><span class="sxs-lookup"><span data-stu-id="4f35e-157">Button text is always on a single line and is truncated if the text exceeds the button width.</span></span> <span data-ttu-id="4f35e-158">Никаких дополнительных кнопок, помимо максимального числа, поддерживаемого картой, не отображается.</span><span class="sxs-lookup"><span data-stu-id="4f35e-158">Any additional buttons beyond the maximum number supported by the card are not shown.</span></span>

<span data-ttu-id="4f35e-159">Дополнительные сведения см. в [карточных действиях.](~/task-modules-and-cards/cards/cards-actions.md)</span><span class="sxs-lookup"><span data-stu-id="4f35e-159">For more information, see [card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

### <a name="card-formatting"></a><span data-ttu-id="4f35e-160">Форматирование карт</span><span class="sxs-lookup"><span data-stu-id="4f35e-160">Card formatting</span></span>

<span data-ttu-id="4f35e-161">Дополнительные сведения о форматирования текста в картах см. [в документе форматирование карт.](~/task-modules-and-cards/cards/cards-format.md)</span><span class="sxs-lookup"><span data-stu-id="4f35e-161">For more information on text formatting in cards, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span>

## <a name="adaptive-card"></a><span data-ttu-id="4f35e-162">Адаптивная карта</span><span class="sxs-lookup"><span data-stu-id="4f35e-162">Adaptive card</span></span>

<span data-ttu-id="4f35e-163">Адаптивная карта — это настраиваемая карта, которая может содержать любое сочетание текстовых, речевого, изображений, кнопок и полей ввода.</span><span class="sxs-lookup"><span data-stu-id="4f35e-163">An adaptive card is a customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> <span data-ttu-id="4f35e-164">Дополнительные сведения см. в [рублях адаптивных карт v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span><span class="sxs-lookup"><span data-stu-id="4f35e-164">For more information, see [adaptive cards v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span></span>

### <a name="support-for-adaptive-cards"></a><span data-ttu-id="4f35e-165">Поддержка адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="4f35e-165">Support for adaptive cards</span></span>

| <span data-ttu-id="4f35e-166">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="4f35e-166">Bots in Teams</span></span> | <span data-ttu-id="4f35e-167">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="4f35e-167">Messaging extensions</span></span>  | <span data-ttu-id="4f35e-168">Соединители</span><span class="sxs-lookup"><span data-stu-id="4f35e-168">Connectors</span></span> | <span data-ttu-id="4f35e-169">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="4f35e-169">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4f35e-170">✔</span><span class="sxs-lookup"><span data-stu-id="4f35e-170">✔</span></span> | <span data-ttu-id="4f35e-171">✔</span><span class="sxs-lookup"><span data-stu-id="4f35e-171">✔</span></span> | <span data-ttu-id="4f35e-172">✖</span><span class="sxs-lookup"><span data-stu-id="4f35e-172">✖</span></span> | <span data-ttu-id="4f35e-173">✔</span><span class="sxs-lookup"><span data-stu-id="4f35e-173">✔</span></span> |

> [!NOTE]
> * <span data-ttu-id="4f35e-174">Teams поддерживает v1.2 или более ранние функции адаптивной карты.</span><span class="sxs-lookup"><span data-stu-id="4f35e-174">Teams platform supports v1.2 or earlier of adaptive card features.</span></span>
> * <span data-ttu-id="4f35e-175">Элементы мультимедиа в настоящее время не поддерживаются в адаптивной карте v1.2 на Teams платформе.</span><span class="sxs-lookup"><span data-stu-id="4f35e-175">Media elements are currently not supported in adaptive card v1.2 on the Teams platform.</span></span>

### <a name="example-of-an-adaptive-card"></a><span data-ttu-id="4f35e-176">Пример адаптивной карты</span><span class="sxs-lookup"><span data-stu-id="4f35e-176">Example of an adaptive card</span></span>

![Пример адаптивной карты](~/assets/images/cards/adaptivecard.png)

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

#### <a name="additional-information-on-adaptive-cards"></a><span data-ttu-id="4f35e-178">Дополнительные сведения о адаптивных картах</span><span class="sxs-lookup"><span data-stu-id="4f35e-178">Additional information on adaptive cards</span></span>

<span data-ttu-id="4f35e-179">Ссылка на Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="4f35e-179">Bot Framework reference:</span></span>

* [<span data-ttu-id="4f35e-180">Адаптивные Node.js</span><span class="sxs-lookup"><span data-stu-id="4f35e-180">Adaptive cards Node.js</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)
* [<span data-ttu-id="4f35e-181">Адаптивная карта C #</span><span class="sxs-lookup"><span data-stu-id="4f35e-181">Adaptive card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)

## <a name="hero-card"></a><span data-ttu-id="4f35e-182">Карта hero</span><span class="sxs-lookup"><span data-stu-id="4f35e-182">Hero card</span></span>

<span data-ttu-id="4f35e-183">Карта, которая обычно содержит одно большое изображение, одну или несколько кнопок и текст.</span><span class="sxs-lookup"><span data-stu-id="4f35e-183">A card that typically contains a single large image, one or more buttons, and text.</span></span>

### <a name="support-for-hero-cards"></a><span data-ttu-id="4f35e-184">Поддержка карт-героев</span><span class="sxs-lookup"><span data-stu-id="4f35e-184">Support for hero cards</span></span>

| <span data-ttu-id="4f35e-185">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="4f35e-185">Bots in Teams</span></span> | <span data-ttu-id="4f35e-186">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="4f35e-186">Messaging extensions</span></span>  | <span data-ttu-id="4f35e-187">Соединители</span><span class="sxs-lookup"><span data-stu-id="4f35e-187">Connectors</span></span> | <span data-ttu-id="4f35e-188">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="4f35e-188">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4f35e-189">✔</span><span class="sxs-lookup"><span data-stu-id="4f35e-189">✔</span></span> | <span data-ttu-id="4f35e-190">✔</span><span class="sxs-lookup"><span data-stu-id="4f35e-190">✔</span></span> | <span data-ttu-id="4f35e-191">✖</span><span class="sxs-lookup"><span data-stu-id="4f35e-191">✖</span></span> | <span data-ttu-id="4f35e-192">✔</span><span class="sxs-lookup"><span data-stu-id="4f35e-192">✔</span></span> |

### <a name="properties-of-a-hero-card"></a><span data-ttu-id="4f35e-193">Свойства карты-героя</span><span class="sxs-lookup"><span data-stu-id="4f35e-193">Properties of a hero card</span></span>

| <span data-ttu-id="4f35e-194">Свойство</span><span class="sxs-lookup"><span data-stu-id="4f35e-194">Property</span></span> | <span data-ttu-id="4f35e-195">Тип</span><span class="sxs-lookup"><span data-stu-id="4f35e-195">Type</span></span>  | <span data-ttu-id="4f35e-196">Описание</span><span class="sxs-lookup"><span data-stu-id="4f35e-196">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4f35e-197">title</span><span class="sxs-lookup"><span data-stu-id="4f35e-197">title</span></span> | <span data-ttu-id="4f35e-198">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="4f35e-198">Rich text</span></span> | <span data-ttu-id="4f35e-199">Название карты.</span><span class="sxs-lookup"><span data-stu-id="4f35e-199">Title of the card.</span></span> <span data-ttu-id="4f35e-200">Максимум 2 строки.</span><span class="sxs-lookup"><span data-stu-id="4f35e-200">Maximum 2 lines.</span></span> |
| <span data-ttu-id="4f35e-201">субтитры</span><span class="sxs-lookup"><span data-stu-id="4f35e-201">subtitle</span></span> | <span data-ttu-id="4f35e-202">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="4f35e-202">Rich text</span></span> | <span data-ttu-id="4f35e-203">Субтитр карты.</span><span class="sxs-lookup"><span data-stu-id="4f35e-203">Subtitle of the card.</span></span> <span data-ttu-id="4f35e-204">Максимум 2 строки.</span><span class="sxs-lookup"><span data-stu-id="4f35e-204">Maximum 2 lines.</span></span>|
| <span data-ttu-id="4f35e-205">текст</span><span class="sxs-lookup"><span data-stu-id="4f35e-205">text</span></span> | <span data-ttu-id="4f35e-206">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="4f35e-206">Rich text</span></span> | <span data-ttu-id="4f35e-207">Текст отображается под субтитром.</span><span class="sxs-lookup"><span data-stu-id="4f35e-207">Text appears under the subtitle.</span></span> <span data-ttu-id="4f35e-208">Параметры форматирования см. [в виде форматирования карт.](~/task-modules-and-cards/cards/cards-format.md)</span><span class="sxs-lookup"><span data-stu-id="4f35e-208">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="4f35e-209">изображения</span><span class="sxs-lookup"><span data-stu-id="4f35e-209">images</span></span> | <span data-ttu-id="4f35e-210">Массив изображений</span><span class="sxs-lookup"><span data-stu-id="4f35e-210">Array of images</span></span> | <span data-ttu-id="4f35e-211">Изображение, отображаемого в верхней части карты.</span><span class="sxs-lookup"><span data-stu-id="4f35e-211">Image displayed at the top of the card.</span></span> <span data-ttu-id="4f35e-212">Соотношение аспектов 16:9.</span><span class="sxs-lookup"><span data-stu-id="4f35e-212">Aspect ratio 16:9.</span></span> |
| <span data-ttu-id="4f35e-213">кнопки</span><span class="sxs-lookup"><span data-stu-id="4f35e-213">buttons</span></span> | <span data-ttu-id="4f35e-214">Массив объектов действий</span><span class="sxs-lookup"><span data-stu-id="4f35e-214">Array of action objects</span></span> | <span data-ttu-id="4f35e-215">Набор действий, применимых к текущей карте.</span><span class="sxs-lookup"><span data-stu-id="4f35e-215">Set of actions applicable to the current card.</span></span> <span data-ttu-id="4f35e-216">Максимум 6.</span><span class="sxs-lookup"><span data-stu-id="4f35e-216">Maximum 6.</span></span> |
| <span data-ttu-id="4f35e-217">нажмите кнопку</span><span class="sxs-lookup"><span data-stu-id="4f35e-217">tap</span></span> | <span data-ttu-id="4f35e-218">Объект Action</span><span class="sxs-lookup"><span data-stu-id="4f35e-218">Action object</span></span> | <span data-ttu-id="4f35e-219">Активируется при нажатии на карточку самого пользователя.</span><span class="sxs-lookup"><span data-stu-id="4f35e-219">Activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-hero-card"></a><span data-ttu-id="4f35e-220">Пример карточки героя</span><span class="sxs-lookup"><span data-stu-id="4f35e-220">Example of a hero card</span></span>

![Пример карточки героя](~/assets/images/cards/hero.png)

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

### <a name="additional-information-on-hero-cards"></a><span data-ttu-id="4f35e-222">Дополнительные сведения о картах-героях</span><span class="sxs-lookup"><span data-stu-id="4f35e-222">Additional information on hero cards</span></span>

<span data-ttu-id="4f35e-223">Ссылка на Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="4f35e-223">Bot Framework reference:</span></span>

* [<span data-ttu-id="4f35e-224">Карточка героя Node.js</span><span class="sxs-lookup"><span data-stu-id="4f35e-224">Hero card Node.js</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-a-hero-card&preserve-view=true)
* [<span data-ttu-id="4f35e-225">Карта героя C #</span><span class="sxs-lookup"><span data-stu-id="4f35e-225">Hero card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-hero-card&preserve-view=true)

## <a name="list-card"></a><span data-ttu-id="4f35e-226">Карта списка</span><span class="sxs-lookup"><span data-stu-id="4f35e-226">List card</span></span>

<span data-ttu-id="4f35e-227">Карта списка была добавлена Teams для предоставления функций, которые не могут предоставляться в коллекции списков.</span><span class="sxs-lookup"><span data-stu-id="4f35e-227">The list card has been added by Teams to provide functions beyond what the list collection can provide.</span></span> <span data-ttu-id="4f35e-228">Карта списка содержит список элементов для прокрутки.</span><span class="sxs-lookup"><span data-stu-id="4f35e-228">The list card provides a scrolling list of items.</span></span>

### <a name="support-for-list-cards"></a><span data-ttu-id="4f35e-229">Поддержка карт списка</span><span class="sxs-lookup"><span data-stu-id="4f35e-229">Support for list cards</span></span>

| <span data-ttu-id="4f35e-230">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="4f35e-230">Bots in Teams</span></span> | <span data-ttu-id="4f35e-231">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="4f35e-231">Messaging extensions</span></span>  | <span data-ttu-id="4f35e-232">Соединители</span><span class="sxs-lookup"><span data-stu-id="4f35e-232">Connectors</span></span> | <span data-ttu-id="4f35e-233">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="4f35e-233">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4f35e-234">✔</span><span class="sxs-lookup"><span data-stu-id="4f35e-234">✔</span></span> | <span data-ttu-id="4f35e-235">✖</span><span class="sxs-lookup"><span data-stu-id="4f35e-235">✖</span></span> | <span data-ttu-id="4f35e-236">✖</span><span class="sxs-lookup"><span data-stu-id="4f35e-236">✖</span></span> |<span data-ttu-id="4f35e-237">✔</span><span class="sxs-lookup"><span data-stu-id="4f35e-237">✔</span></span> |

### <a name="properties-of-a-list-card"></a><span data-ttu-id="4f35e-238">Свойства карты списка</span><span class="sxs-lookup"><span data-stu-id="4f35e-238">Properties of a list card</span></span>

| <span data-ttu-id="4f35e-239">Свойство</span><span class="sxs-lookup"><span data-stu-id="4f35e-239">Property</span></span> | <span data-ttu-id="4f35e-240">Тип</span><span class="sxs-lookup"><span data-stu-id="4f35e-240">Type</span></span>  | <span data-ttu-id="4f35e-241">Описание</span><span class="sxs-lookup"><span data-stu-id="4f35e-241">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4f35e-242">title</span><span class="sxs-lookup"><span data-stu-id="4f35e-242">title</span></span> | <span data-ttu-id="4f35e-243">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="4f35e-243">Rich text</span></span> | <span data-ttu-id="4f35e-244">Название карты.</span><span class="sxs-lookup"><span data-stu-id="4f35e-244">Title of the card.</span></span> <span data-ttu-id="4f35e-245">Максимум 2 строки.</span><span class="sxs-lookup"><span data-stu-id="4f35e-245">Maximum 2 lines.</span></span>|
| <span data-ttu-id="4f35e-246">элементы</span><span class="sxs-lookup"><span data-stu-id="4f35e-246">items</span></span> | <span data-ttu-id="4f35e-247">Массив элементов списка</span><span class="sxs-lookup"><span data-stu-id="4f35e-247">Array of list items</span></span> ||
| <span data-ttu-id="4f35e-248">кнопки</span><span class="sxs-lookup"><span data-stu-id="4f35e-248">buttons</span></span> | <span data-ttu-id="4f35e-249">Массив объектов действий</span><span class="sxs-lookup"><span data-stu-id="4f35e-249">Array of action objects</span></span> | <span data-ttu-id="4f35e-250">Набор действий, применимых к текущей карте.</span><span class="sxs-lookup"><span data-stu-id="4f35e-250">Set of actions applicable to the current card.</span></span> <span data-ttu-id="4f35e-251">Максимум 6.</span><span class="sxs-lookup"><span data-stu-id="4f35e-251">Maximum 6.</span></span> |

### <a name="example-of-a-list-card"></a><span data-ttu-id="4f35e-252">Пример карты списка</span><span class="sxs-lookup"><span data-stu-id="4f35e-252">Example of a list card</span></span>

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

## <a name="office-365-connector-card"></a><span data-ttu-id="4f35e-253">Office 365 соединители</span><span class="sxs-lookup"><span data-stu-id="4f35e-253">Office 365 connector card</span></span>

<span data-ttu-id="4f35e-254">Соедините Office 365 поддерживается в Teams, а не в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="4f35e-254">The Office 365 connector card is supported in Teams, not in Bot Framework.</span></span> <span data-ttu-id="4f35e-255">Эта карта обеспечивает гибкую схему с несколькими разделами, полями, изображениями и действиями.</span><span class="sxs-lookup"><span data-stu-id="4f35e-255">This card provides a flexible layout with multiple sections, fields, images, and actions.</span></span> <span data-ttu-id="4f35e-256">Эта карта инкапсулирует соединителем карту, чтобы она была использована ботами.</span><span class="sxs-lookup"><span data-stu-id="4f35e-256">This card encapsulates a connector card so that it can be used by bots.</span></span> <span data-ttu-id="4f35e-257">О различиях между соединитеными картами и картой O365 см. в заметках на [Office 365 соединители.](#notes-on-the-office-365-connector-card)</span><span class="sxs-lookup"><span data-stu-id="4f35e-257">For differences between connector cards and the O365 card, see [Notes on the Office 365 connector card](#notes-on-the-office-365-connector-card).</span></span>

### <a name="support-for-office-365-connector-cards"></a><span data-ttu-id="4f35e-258">Поддержка Office 365 соединители</span><span class="sxs-lookup"><span data-stu-id="4f35e-258">Support for Office 365 connector cards</span></span>

| <span data-ttu-id="4f35e-259">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="4f35e-259">Bots in Teams</span></span> | <span data-ttu-id="4f35e-260">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="4f35e-260">Messaging extensions</span></span>  | <span data-ttu-id="4f35e-261">Соединители</span><span class="sxs-lookup"><span data-stu-id="4f35e-261">Connectors</span></span> | <span data-ttu-id="4f35e-262">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="4f35e-262">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4f35e-263">✔</span><span class="sxs-lookup"><span data-stu-id="4f35e-263">✔</span></span> | <span data-ttu-id="4f35e-264">✔</span><span class="sxs-lookup"><span data-stu-id="4f35e-264">✔</span></span> | <span data-ttu-id="4f35e-265">✔</span><span class="sxs-lookup"><span data-stu-id="4f35e-265">✔</span></span> | <span data-ttu-id="4f35e-266">✖</span><span class="sxs-lookup"><span data-stu-id="4f35e-266">✖</span></span> |

### <a name="properties-of-the-office-365-connector-card"></a><span data-ttu-id="4f35e-267">Свойства карты Office 365 соединители</span><span class="sxs-lookup"><span data-stu-id="4f35e-267">Properties of the Office 365 connector card</span></span>

| <span data-ttu-id="4f35e-268">Свойство</span><span class="sxs-lookup"><span data-stu-id="4f35e-268">Property</span></span> | <span data-ttu-id="4f35e-269">Тип</span><span class="sxs-lookup"><span data-stu-id="4f35e-269">Type</span></span>  | <span data-ttu-id="4f35e-270">Описание</span><span class="sxs-lookup"><span data-stu-id="4f35e-270">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4f35e-271">title</span><span class="sxs-lookup"><span data-stu-id="4f35e-271">title</span></span> | <span data-ttu-id="4f35e-272">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="4f35e-272">Rich text</span></span> | <span data-ttu-id="4f35e-273">Название карты.</span><span class="sxs-lookup"><span data-stu-id="4f35e-273">Title of the card.</span></span> <span data-ttu-id="4f35e-274">Максимум 2 строки.</span><span class="sxs-lookup"><span data-stu-id="4f35e-274">Maximum 2 lines.</span></span> |
| <span data-ttu-id="4f35e-275">summary</span><span class="sxs-lookup"><span data-stu-id="4f35e-275">summary</span></span> | <span data-ttu-id="4f35e-276">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="4f35e-276">Rich text</span></span> | <span data-ttu-id="4f35e-277">Сводка карты.</span><span class="sxs-lookup"><span data-stu-id="4f35e-277">Summary of the card.</span></span> <span data-ttu-id="4f35e-278">Максимум 2 строки.</span><span class="sxs-lookup"><span data-stu-id="4f35e-278">Maximum 2 lines.</span></span> |
| <span data-ttu-id="4f35e-279">текст</span><span class="sxs-lookup"><span data-stu-id="4f35e-279">text</span></span> | <span data-ttu-id="4f35e-280">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="4f35e-280">Rich text</span></span> | <span data-ttu-id="4f35e-281">Текст отображается под субтитром.</span><span class="sxs-lookup"><span data-stu-id="4f35e-281">Text appears under the subtitle.</span></span> <span data-ttu-id="4f35e-282">Параметры форматирования см. [в виде форматирования карт.](~/task-modules-and-cards/cards/cards-format.md)</span><span class="sxs-lookup"><span data-stu-id="4f35e-282">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="4f35e-283">themeColor</span><span class="sxs-lookup"><span data-stu-id="4f35e-283">themeColor</span></span> | <span data-ttu-id="4f35e-284">Строка HEX</span><span class="sxs-lookup"><span data-stu-id="4f35e-284">HEX string</span></span> | <span data-ttu-id="4f35e-285">Цвет, который переопределяет accentColor, предоставленный из манифеста приложения.</span><span class="sxs-lookup"><span data-stu-id="4f35e-285">Color that overrides the accentColor provided from the application manifest.</span></span> |

### <a name="notes-on-the-office-365-connector-card"></a><span data-ttu-id="4f35e-286">Заметки на Office 365 соединители</span><span class="sxs-lookup"><span data-stu-id="4f35e-286">Notes on the Office 365 connector card</span></span>

<span data-ttu-id="4f35e-287">Office 365 соединители карточки работают правильно в Microsoft Teams, включая [действия ActionCard](/outlook/actionable-messages/card-reference#actioncard-action).</span><span class="sxs-lookup"><span data-stu-id="4f35e-287">Office 365 connector cards function properly in Microsoft Teams, including [ActionCard actions](/outlook/actionable-messages/card-reference#actioncard-action).</span></span>

<span data-ttu-id="4f35e-288">Одним из важных отличий между использованием соединитеных карт из соединитетеля и использованием соединитеных карт в боте является обработка действий карт.</span><span class="sxs-lookup"><span data-stu-id="4f35e-288">One important difference between using connector cards from a connector and using connector cards in your bot is the handling of card actions.</span></span>

* <span data-ttu-id="4f35e-289">Для соединитетеля конечная точка получает полезное сообщение карточки через HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="4f35e-289">For a connector, the endpoint receives the card payload through HTTP POST.</span></span>
* <span data-ttu-id="4f35e-290">Для бота действие запускает действие, которое отправляет боту только ID действия и `HttpPOST` `invoke` тело.</span><span class="sxs-lookup"><span data-stu-id="4f35e-290">For a bot, the `HttpPOST` action triggers an `invoke` activity that sends only the action ID and body to the bot.</span></span>

<span data-ttu-id="4f35e-291">Каждая соединитечная карта может отображать не более десяти разделов, а каждый раздел может содержать не более пяти изображений и пять действий.</span><span class="sxs-lookup"><span data-stu-id="4f35e-291">Each connector card can display a maximum of ten sections, and each section can contain a maximum of five images and five actions.</span></span>

> [!NOTE]
> <span data-ttu-id="4f35e-292">Дополнительные разделы, изображения или действия в сообщении не отображаются.</span><span class="sxs-lookup"><span data-stu-id="4f35e-292">Any additional sections, images, or actions in a message do not appear.</span></span>

<span data-ttu-id="4f35e-293">Все текстовые поля поддерживают разметку и HTML.</span><span class="sxs-lookup"><span data-stu-id="4f35e-293">All text fields support markdown and HTML.</span></span> <span data-ttu-id="4f35e-294">Вы можете контролировать, в каких разделах используется разметка или HTML, установив `markdown` свойство в сообщении.</span><span class="sxs-lookup"><span data-stu-id="4f35e-294">You can control which sections use markdown or HTML by setting the `markdown` property in a message.</span></span> <span data-ttu-id="4f35e-295">По умолчанию `markdown` установлено `true` значение .</span><span class="sxs-lookup"><span data-stu-id="4f35e-295">By default, `markdown` is set to `true`.</span></span> <span data-ttu-id="4f35e-296">Если вы хотите использовать HTML вместо этого, установите `markdown` `false` .</span><span class="sxs-lookup"><span data-stu-id="4f35e-296">If you want to use HTML instead, set `markdown` to `false`.</span></span>

<span data-ttu-id="4f35e-297">Если указать `themeColor` свойство, оно переопределит `accentColor` свойство в манифесте приложения.</span><span class="sxs-lookup"><span data-stu-id="4f35e-297">If you specify the `themeColor` property, it overrides the `accentColor` property in the app manifest.</span></span>

<span data-ttu-id="4f35e-298">Чтобы указать стиль `activityImage` визуализации, можно задать `activityImageType` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="4f35e-298">To specify the rendering style for `activityImage`, you can set `activityImageType` as follows:</span></span>

| <span data-ttu-id="4f35e-299">Значение</span><span class="sxs-lookup"><span data-stu-id="4f35e-299">Value</span></span> | <span data-ttu-id="4f35e-300">Описание</span><span class="sxs-lookup"><span data-stu-id="4f35e-300">Description</span></span> |
| --- | --- |
| `avatar` | <span data-ttu-id="4f35e-301">По умолчанию; `activityImage` обрезается как круг.</span><span class="sxs-lookup"><span data-stu-id="4f35e-301">Default; `activityImage` is cropped as a circle.</span></span> |
| `article` | <span data-ttu-id="4f35e-302">`activityImage` отображается в качестве прямоугольника и сохраняет отношение аспектов.</span><span class="sxs-lookup"><span data-stu-id="4f35e-302">`activityImage` is displayed as a rectangle and retains its aspect ratio.</span></span> |

<span data-ttu-id="4f35e-303">Другие сведения о свойствах карт соединители см. в справке к карточкам [сообщений.](/outlook/actionable-messages/card-reference)</span><span class="sxs-lookup"><span data-stu-id="4f35e-303">For all other details about connector card properties, see [actionable message card reference](/outlook/actionable-messages/card-reference).</span></span> <span data-ttu-id="4f35e-304">Единственными свойствами карт соединители, Microsoft Teams которые в настоящее время не поддерживаются, являются следующими:</span><span class="sxs-lookup"><span data-stu-id="4f35e-304">The only connector card properties that Microsoft Teams does not currently support are as follows:</span></span>

* `heroImage`
* `hideOriginalBody`
* <span data-ttu-id="4f35e-305">`startGroup`всегда рассматривается как `true` в Teams</span><span class="sxs-lookup"><span data-stu-id="4f35e-305">`startGroup` always treated as `true` in Teams</span></span>
* `originator`
* `correlationId`

### <a name="example-of-an-office-365-connector-card"></a><span data-ttu-id="4f35e-306">Пример карты Office 365 соединители</span><span class="sxs-lookup"><span data-stu-id="4f35e-306">Example of an Office 365 connector card</span></span>

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

## <a name="receipt-card"></a><span data-ttu-id="4f35e-307">Карта получения</span><span class="sxs-lookup"><span data-stu-id="4f35e-307">Receipt card</span></span>

<span data-ttu-id="4f35e-308">Teams поддерживает карточку получения.</span><span class="sxs-lookup"><span data-stu-id="4f35e-308">Teams supports receipt card.</span></span> <span data-ttu-id="4f35e-309">Это карточка, которая позволяет боту предоставлять пользователю квитанцию.</span><span class="sxs-lookup"><span data-stu-id="4f35e-309">It is a card that enables a bot to provide a receipt to the user.</span></span> <span data-ttu-id="4f35e-310">Обычно он содержит список элементов, которые необходимо включить в квитанцию, например налоговые и общие сведения.</span><span class="sxs-lookup"><span data-stu-id="4f35e-310">It typically contains the list of items to include on the receipt, such as tax and total information.</span></span>

### <a name="support-for-receipt-cards"></a><span data-ttu-id="4f35e-311">Поддержка карт получения</span><span class="sxs-lookup"><span data-stu-id="4f35e-311">Support for receipt cards</span></span>

| <span data-ttu-id="4f35e-312">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="4f35e-312">Bots in Teams</span></span> | <span data-ttu-id="4f35e-313">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="4f35e-313">Messaging extensions</span></span>  | <span data-ttu-id="4f35e-314">Соединители</span><span class="sxs-lookup"><span data-stu-id="4f35e-314">Connectors</span></span> | <span data-ttu-id="4f35e-315">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="4f35e-315">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4f35e-316">✔</span><span class="sxs-lookup"><span data-stu-id="4f35e-316">✔</span></span> | <span data-ttu-id="4f35e-317">✔</span><span class="sxs-lookup"><span data-stu-id="4f35e-317">✔</span></span> | <span data-ttu-id="4f35e-318">✖</span><span class="sxs-lookup"><span data-stu-id="4f35e-318">✖</span></span> | <span data-ttu-id="4f35e-319">✔</span><span class="sxs-lookup"><span data-stu-id="4f35e-319">✔</span></span> |

### <a name="example-of-a-receipt-card"></a><span data-ttu-id="4f35e-320">Пример карты получения</span><span class="sxs-lookup"><span data-stu-id="4f35e-320">Example of a receipt card</span></span>

![Пример карты получения](~/assets/images/cards/receipt.png)

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

### <a name="additional-information-on-receipt-cards"></a><span data-ttu-id="4f35e-322">Дополнительные сведения о карточках получения</span><span class="sxs-lookup"><span data-stu-id="4f35e-322">Additional information on receipt cards</span></span>

<span data-ttu-id="4f35e-323">Ссылка на Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="4f35e-323">Bot Framework reference:</span></span>

* [<span data-ttu-id="4f35e-324">Карточка получения Node.js</span><span class="sxs-lookup"><span data-stu-id="4f35e-324">Receipt card Node.js</span></span>](/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="4f35e-325">Карта получения C #</span><span class="sxs-lookup"><span data-stu-id="4f35e-325">Receipt card C#</span></span>](/dotnet/api/microsoft.bot.schema.receiptcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="signin-card"></a><span data-ttu-id="4f35e-326">Карточка Signin</span><span class="sxs-lookup"><span data-stu-id="4f35e-326">Signin card</span></span>

<span data-ttu-id="4f35e-327">Карта Signin позволяет боту запрашивать вход пользователя.</span><span class="sxs-lookup"><span data-stu-id="4f35e-327">Signin card enables a bot to request a user to sign in.</span></span> <span data-ttu-id="4f35e-328">Поддерживается в Teams в несколько иной форме, чем в bot Framework.</span><span class="sxs-lookup"><span data-stu-id="4f35e-328">It is supported in Teams in a slightly different form than is found in the Bot Framework.</span></span> <span data-ttu-id="4f35e-329">Карта signin в Teams похожа на карточку signin в bot Framework, за исключением того, что карточка signin в Teams поддерживает только два действия: `signin` и `openUrl` .</span><span class="sxs-lookup"><span data-stu-id="4f35e-329">The signin card in Teams is similar to the signin card in the Bot Framework except that the signin card in Teams only supports two actions: `signin` and `openUrl`.</span></span>

<span data-ttu-id="4f35e-330">Действие signin можно использовать с любой карты в Teams, а не только с карты signin.</span><span class="sxs-lookup"><span data-stu-id="4f35e-330">The signin action can be used from any card in Teams, not just the signin card.</span></span> <span data-ttu-id="4f35e-331">Дополнительные сведения о проверке подлинности см. в Microsoft Teams поток проверки [подлинности для ботов.](~/bots/how-to/authentication/auth-flow-bot.md)</span><span class="sxs-lookup"><span data-stu-id="4f35e-331">For more information on authentication, see [Microsoft Teams authentication flow for bots](~/bots/how-to/authentication/auth-flow-bot.md).</span></span>

### <a name="support-for-signin-cards"></a><span data-ttu-id="4f35e-332">Поддержка подписных карт</span><span class="sxs-lookup"><span data-stu-id="4f35e-332">Support for signin cards</span></span>

| <span data-ttu-id="4f35e-333">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="4f35e-333">Bots in Teams</span></span> | <span data-ttu-id="4f35e-334">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="4f35e-334">Messaging extensions</span></span>  | <span data-ttu-id="4f35e-335">Соединители</span><span class="sxs-lookup"><span data-stu-id="4f35e-335">Connectors</span></span> | <span data-ttu-id="4f35e-336">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="4f35e-336">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4f35e-337">✔</span><span class="sxs-lookup"><span data-stu-id="4f35e-337">✔</span></span> | <span data-ttu-id="4f35e-338">✖</span><span class="sxs-lookup"><span data-stu-id="4f35e-338">✖</span></span> | <span data-ttu-id="4f35e-339">✖</span><span class="sxs-lookup"><span data-stu-id="4f35e-339">✖</span></span> | <span data-ttu-id="4f35e-340">✔</span><span class="sxs-lookup"><span data-stu-id="4f35e-340">✔</span></span> |

### <a name="additional-information-on-signin-cards"></a><span data-ttu-id="4f35e-341">Дополнительные сведения о подписных карточках</span><span class="sxs-lookup"><span data-stu-id="4f35e-341">Additional information on signin cards</span></span>

<span data-ttu-id="4f35e-342">Ссылка на Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="4f35e-342">Bot Framework reference:</span></span>

* [<span data-ttu-id="4f35e-343">Карточка signin Node.js</span><span class="sxs-lookup"><span data-stu-id="4f35e-343">Signin card Node.js</span></span>](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="4f35e-344">Signin card C #</span><span class="sxs-lookup"><span data-stu-id="4f35e-344">Signin card C#</span></span>](/dotnet/api/microsoft.bot.schema.signincard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="thumbnail-card"></a><span data-ttu-id="4f35e-345">Карта эскиза</span><span class="sxs-lookup"><span data-stu-id="4f35e-345">Thumbnail card</span></span>

<span data-ttu-id="4f35e-346">Карточка, которая обычно содержит одно изображение эскиза, одну или несколько кнопок и текст.</span><span class="sxs-lookup"><span data-stu-id="4f35e-346">A card that typically contains a single thumbnail image, one or more buttons, and text.</span></span>

### <a name="support-for-thumbnail-cards"></a><span data-ttu-id="4f35e-347">Поддержка карт эскизов</span><span class="sxs-lookup"><span data-stu-id="4f35e-347">Support for thumbnail cards</span></span>

| <span data-ttu-id="4f35e-348">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="4f35e-348">Bots in Teams</span></span> | <span data-ttu-id="4f35e-349">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="4f35e-349">Messaging extensions</span></span>  | <span data-ttu-id="4f35e-350">Соединители</span><span class="sxs-lookup"><span data-stu-id="4f35e-350">Connectors</span></span> | <span data-ttu-id="4f35e-351">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="4f35e-351">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4f35e-352">✔</span><span class="sxs-lookup"><span data-stu-id="4f35e-352">✔</span></span> | <span data-ttu-id="4f35e-353">✔</span><span class="sxs-lookup"><span data-stu-id="4f35e-353">✔</span></span> | <span data-ttu-id="4f35e-354">✖</span><span class="sxs-lookup"><span data-stu-id="4f35e-354">✖</span></span> | <span data-ttu-id="4f35e-355">✔</span><span class="sxs-lookup"><span data-stu-id="4f35e-355">✔</span></span> |

![Пример карты эскиза](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a><span data-ttu-id="4f35e-357">Свойства карты эскиза</span><span class="sxs-lookup"><span data-stu-id="4f35e-357">Properties of a thumbnail card</span></span>

| <span data-ttu-id="4f35e-358">Свойство</span><span class="sxs-lookup"><span data-stu-id="4f35e-358">Property</span></span> | <span data-ttu-id="4f35e-359">Тип</span><span class="sxs-lookup"><span data-stu-id="4f35e-359">Type</span></span>  | <span data-ttu-id="4f35e-360">Описание</span><span class="sxs-lookup"><span data-stu-id="4f35e-360">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4f35e-361">title</span><span class="sxs-lookup"><span data-stu-id="4f35e-361">title</span></span> | <span data-ttu-id="4f35e-362">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="4f35e-362">Rich text</span></span> | <span data-ttu-id="4f35e-363">Название карты.</span><span class="sxs-lookup"><span data-stu-id="4f35e-363">Title of the card.</span></span> <span data-ttu-id="4f35e-364">Максимум 2 строки.</span><span class="sxs-lookup"><span data-stu-id="4f35e-364">Maximum 2 lines.</span></span>|
| <span data-ttu-id="4f35e-365">субтитры</span><span class="sxs-lookup"><span data-stu-id="4f35e-365">subtitle</span></span> | <span data-ttu-id="4f35e-366">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="4f35e-366">Rich text</span></span> | <span data-ttu-id="4f35e-367">Субтитр карты.</span><span class="sxs-lookup"><span data-stu-id="4f35e-367">Subtitle of the card.</span></span> <span data-ttu-id="4f35e-368">Максимум 2 строки.</span><span class="sxs-lookup"><span data-stu-id="4f35e-368">Maximum 2 lines.</span></span>|
| <span data-ttu-id="4f35e-369">текст</span><span class="sxs-lookup"><span data-stu-id="4f35e-369">text</span></span> | <span data-ttu-id="4f35e-370">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="4f35e-370">Rich text</span></span> | <span data-ttu-id="4f35e-371">Текст отображается под субтитром.</span><span class="sxs-lookup"><span data-stu-id="4f35e-371">Text appears under the subtitle.</span></span> <span data-ttu-id="4f35e-372">Параметры форматирования см. [в виде форматирования карт.](~/task-modules-and-cards/cards/cards-format.md)</span><span class="sxs-lookup"><span data-stu-id="4f35e-372">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="4f35e-373">изображения</span><span class="sxs-lookup"><span data-stu-id="4f35e-373">images</span></span> | <span data-ttu-id="4f35e-374">Массив изображений</span><span class="sxs-lookup"><span data-stu-id="4f35e-374">Array of images</span></span> | <span data-ttu-id="4f35e-375">Изображение, отображаемого в верхней части карты.</span><span class="sxs-lookup"><span data-stu-id="4f35e-375">Image displayed at the top of the card.</span></span> <span data-ttu-id="4f35e-376">Отношение аспектов 1:1 к квадрату.</span><span class="sxs-lookup"><span data-stu-id="4f35e-376">Aspect ratio 1:1 square.</span></span> |
| <span data-ttu-id="4f35e-377">кнопки</span><span class="sxs-lookup"><span data-stu-id="4f35e-377">buttons</span></span> | <span data-ttu-id="4f35e-378">Массив объектов действий</span><span class="sxs-lookup"><span data-stu-id="4f35e-378">Array of action objects</span></span> | <span data-ttu-id="4f35e-379">Набор действий, применимых к текущей карте.</span><span class="sxs-lookup"><span data-stu-id="4f35e-379">Set of actions applicable to the current card.</span></span> <span data-ttu-id="4f35e-380">Максимум 6.</span><span class="sxs-lookup"><span data-stu-id="4f35e-380">Maximum 6.</span></span> |
| <span data-ttu-id="4f35e-381">нажмите кнопку</span><span class="sxs-lookup"><span data-stu-id="4f35e-381">tap</span></span> | <span data-ttu-id="4f35e-382">Объект Action</span><span class="sxs-lookup"><span data-stu-id="4f35e-382">Action object</span></span> | <span data-ttu-id="4f35e-383">Активируется при нажатии на карточку самого пользователя.</span><span class="sxs-lookup"><span data-stu-id="4f35e-383">Activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-thumbnail-card"></a><span data-ttu-id="4f35e-384">Пример карты эскиза</span><span class="sxs-lookup"><span data-stu-id="4f35e-384">Example of a thumbnail card</span></span>

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

### <a name="additional-information"></a><span data-ttu-id="4f35e-385">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="4f35e-385">Additional information</span></span>

<span data-ttu-id="4f35e-386">Ссылка на Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="4f35e-386">Bot Framework reference:</span></span>

* [<span data-ttu-id="4f35e-387">Эскиз карты Node.js</span><span class="sxs-lookup"><span data-stu-id="4f35e-387">Thumbnail card Node.js</span></span>](/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="4f35e-388">Эскиз карты C #</span><span class="sxs-lookup"><span data-stu-id="4f35e-388">Thumbnail card C#</span></span>](/dotnet/api/microsoft.bot.schema.thumbnailcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="card-collections"></a><span data-ttu-id="4f35e-389">Коллекции карт</span><span class="sxs-lookup"><span data-stu-id="4f35e-389">Card collections</span></span>

<span data-ttu-id="4f35e-390">Teams поддерживает коллекции карт.</span><span class="sxs-lookup"><span data-stu-id="4f35e-390">Teams supports Card collections.</span></span>

<span data-ttu-id="4f35e-391">Коллекции карт включают `builder.AttachmentLayout.carousel` и `builder.AttachmentLayout.list` .</span><span class="sxs-lookup"><span data-stu-id="4f35e-391">Card collections include `builder.AttachmentLayout.carousel` and `builder.AttachmentLayout.list`.</span></span> <span data-ttu-id="4f35e-392">Эти коллекции содержат адаптивные, герой или эскизные карточки.</span><span class="sxs-lookup"><span data-stu-id="4f35e-392">These collections contain adaptive, hero, or thumbnail cards.</span></span>

## <a name="carousel-collection"></a><span data-ttu-id="4f35e-393">Коллекция Карусель</span><span class="sxs-lookup"><span data-stu-id="4f35e-393">Carousel collection</span></span>

<span data-ttu-id="4f35e-394">Макет [карусель показывает](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) карусель карт, необязательно с связанными кнопками действия.</span><span class="sxs-lookup"><span data-stu-id="4f35e-394">The [carousel layout](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) shows a carousel of cards, optionally with associated action buttons.</span></span>

### <a name="support-for-carousel-collections"></a><span data-ttu-id="4f35e-395">Поддержка коллекций карусель</span><span class="sxs-lookup"><span data-stu-id="4f35e-395">Support for carousel collections</span></span>

| <span data-ttu-id="4f35e-396">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="4f35e-396">Bots in Teams</span></span> | <span data-ttu-id="4f35e-397">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="4f35e-397">Messaging extensions</span></span>  | <span data-ttu-id="4f35e-398">Соединители</span><span class="sxs-lookup"><span data-stu-id="4f35e-398">Connectors</span></span> | <span data-ttu-id="4f35e-399">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="4f35e-399">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4f35e-400">✔</span><span class="sxs-lookup"><span data-stu-id="4f35e-400">✔</span></span> | <span data-ttu-id="4f35e-401">✖</span><span class="sxs-lookup"><span data-stu-id="4f35e-401">✖</span></span> | <span data-ttu-id="4f35e-402">✖</span><span class="sxs-lookup"><span data-stu-id="4f35e-402">✖</span></span> | <span data-ttu-id="4f35e-403">✔</span><span class="sxs-lookup"><span data-stu-id="4f35e-403">✔</span></span> |

> [!NOTE]
> <span data-ttu-id="4f35e-404">Карусель может отображать не более десяти карт на сообщение.</span><span class="sxs-lookup"><span data-stu-id="4f35e-404">A carousel can display a maximum of ten cards per message.</span></span>

### <a name="properties-of-a-carousel-card"></a><span data-ttu-id="4f35e-405">Свойства карусели</span><span class="sxs-lookup"><span data-stu-id="4f35e-405">Properties of a carousel card</span></span>

<span data-ttu-id="4f35e-406">Свойства карусельной карты такие же, как и у карт героя и эскизов.</span><span class="sxs-lookup"><span data-stu-id="4f35e-406">Properties of a carousel card are same as those of the hero and thumbnail cards.</span></span>

### <a name="example-of-a-carousel-collection"></a><span data-ttu-id="4f35e-407">Пример коллекции карусель</span><span class="sxs-lookup"><span data-stu-id="4f35e-407">Example of a carousel collection</span></span>

![Пример карусели карт](~/assets/images/cards/carousel.png)

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

### <a name="syntax-for-carousel-collections"></a><span data-ttu-id="4f35e-409">Синтаксис для коллекций карусели</span><span class="sxs-lookup"><span data-stu-id="4f35e-409">Syntax for carousel collections</span></span>

<span data-ttu-id="4f35e-410">`builder.AttachmentLayoutTypes.Carousel` синтаксис для коллекций карусели.</span><span class="sxs-lookup"><span data-stu-id="4f35e-410">`builder.AttachmentLayoutTypes.Carousel` is the syntax for carousel collections.</span></span>

## <a name="list-collection"></a><span data-ttu-id="4f35e-411">Коллекция списков</span><span class="sxs-lookup"><span data-stu-id="4f35e-411">List collection</span></span>

### <a name="support-for-list-collections"></a><span data-ttu-id="4f35e-412">Поддержка коллекций списков</span><span class="sxs-lookup"><span data-stu-id="4f35e-412">Support for list collections</span></span>

<span data-ttu-id="4f35e-413">В макете списка показан вертикально сложенный список карт, необязательно связанный с кнопками действия.</span><span class="sxs-lookup"><span data-stu-id="4f35e-413">The list layout shows a vertically stacked list of cards, optionally with associated action buttons.</span></span>

| <span data-ttu-id="4f35e-414">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="4f35e-414">Bots in Teams</span></span> | <span data-ttu-id="4f35e-415">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="4f35e-415">Messaging extensions</span></span>  | <span data-ttu-id="4f35e-416">Соединители</span><span class="sxs-lookup"><span data-stu-id="4f35e-416">Connectors</span></span> | <span data-ttu-id="4f35e-417">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="4f35e-417">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4f35e-418">✔</span><span class="sxs-lookup"><span data-stu-id="4f35e-418">✔</span></span> | <span data-ttu-id="4f35e-419">✔</span><span class="sxs-lookup"><span data-stu-id="4f35e-419">✔</span></span> | <span data-ttu-id="4f35e-420">✖</span><span class="sxs-lookup"><span data-stu-id="4f35e-420">✖</span></span> | <span data-ttu-id="4f35e-421">✔</span><span class="sxs-lookup"><span data-stu-id="4f35e-421">✔</span></span> |

### <a name="example-of-a-list-collection"></a><span data-ttu-id="4f35e-422">Пример коллекции списков</span><span class="sxs-lookup"><span data-stu-id="4f35e-422">Example of a list collection</span></span>

![Пример списка карт](~/assets/images/cards/list.png)

<span data-ttu-id="4f35e-424">Свойства такие же, как для карты героя или эскиза.</span><span class="sxs-lookup"><span data-stu-id="4f35e-424">Properties are the same as for the hero or thumbnail card.</span></span>

<span data-ttu-id="4f35e-425">В списке может отображаться не более десяти карт на сообщение.</span><span class="sxs-lookup"><span data-stu-id="4f35e-425">A list can display a maximum of ten cards per message.</span></span>

> [!NOTE]
> <span data-ttu-id="4f35e-426">Некоторые сочетания карт списка еще не поддерживаются на iOS и Android.</span><span class="sxs-lookup"><span data-stu-id="4f35e-426">Some combinations of list cards are not yet supported on iOS and Android.</span></span>

### <a name="syntax-for-list-collections"></a><span data-ttu-id="4f35e-427">Синтаксис для коллекций списков</span><span class="sxs-lookup"><span data-stu-id="4f35e-427">Syntax for list collections</span></span>

<span data-ttu-id="4f35e-428">`builder.AttachmentLayout.list` синтаксис для коллекций списков.</span><span class="sxs-lookup"><span data-stu-id="4f35e-428">`builder.AttachmentLayout.list` is the syntax for list collections.</span></span>

## <a name="cards-not-supported-in-teams"></a><span data-ttu-id="4f35e-429">Карты, не поддерживаемые в Teams</span><span class="sxs-lookup"><span data-stu-id="4f35e-429">Cards not supported in Teams</span></span>

<span data-ttu-id="4f35e-430">Следующие карты реализуются в рамках Bot Framework, но не поддерживаются Teams:</span><span class="sxs-lookup"><span data-stu-id="4f35e-430">The following cards are implemented by the Bot Framework, but are not supported by Teams:</span></span>

* <span data-ttu-id="4f35e-431">Карты анимации</span><span class="sxs-lookup"><span data-stu-id="4f35e-431">Animation cards</span></span>
* <span data-ttu-id="4f35e-432">Аудиокарты</span><span class="sxs-lookup"><span data-stu-id="4f35e-432">Audio cards</span></span>
* <span data-ttu-id="4f35e-433">Видеокарты</span><span class="sxs-lookup"><span data-stu-id="4f35e-433">Video cards</span></span>
