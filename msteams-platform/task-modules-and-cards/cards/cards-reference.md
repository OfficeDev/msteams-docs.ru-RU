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
# <a name="cards-reference"></a><span data-ttu-id="a890c-104">Ссылки на карточки</span><span class="sxs-lookup"><span data-stu-id="a890c-104">Cards reference</span></span>

<span data-ttu-id="a890c-105">Карты, перечисленные в этом документе, поддерживаются в ботах для Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="a890c-105">The cards listed in this document are supported in bots for Microsoft Teams.</span></span> <span data-ttu-id="a890c-106">Они основаны на картах, определенных bot Framework (BF), но Teams не поддерживает все карты Bot Framework и вместо этого были добавлены некоторые Teams карты.</span><span class="sxs-lookup"><span data-stu-id="a890c-106">They are based on cards defined by the Bot Framework (BF), but Teams does not support all Bot Framework cards and instead some Teams cards have been added.</span></span> <span data-ttu-id="a890c-107">Различия называются в ссылках в этом документе.</span><span class="sxs-lookup"><span data-stu-id="a890c-107">Differences are called out in the references in this document.</span></span>

## <a name="card-examples"></a><span data-ttu-id="a890c-108">Примеры карт</span><span class="sxs-lookup"><span data-stu-id="a890c-108">Card examples</span></span>

<span data-ttu-id="a890c-109">Дополнительные сведения об использовании карт можно найти в документации для bot Builder SDK v3.</span><span class="sxs-lookup"><span data-stu-id="a890c-109">You can find additional information on how to use cards in the documentation for the Bot Builder SDK v3.</span></span> <span data-ttu-id="a890c-110">Примеры кода также доступны в репозитории Microsoft/BotBuilder-Samples на GitHub.</span><span class="sxs-lookup"><span data-stu-id="a890c-110">Code samples are also available in the Microsoft/BotBuilder-Samples repository on GitHub.</span></span>

* <span data-ttu-id="a890c-111">.NET</span><span class="sxs-lookup"><span data-stu-id="a890c-111">.NET</span></span>
  * <span data-ttu-id="a890c-112">[Добавление карт в виде вложений в сообщения.](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="a890c-112">[Add cards as attachments to messages](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true).</span></span>
  * <span data-ttu-id="a890c-113">[Карты пример кода Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards).</span><span class="sxs-lookup"><span data-stu-id="a890c-113">[Cards sample code Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards).</span></span>

* <span data-ttu-id="a890c-114">Node.js</span><span class="sxs-lookup"><span data-stu-id="a890c-114">Node.js</span></span>
  * <span data-ttu-id="a890c-115">[Добавление карт в виде вложений в сообщения.](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="a890c-115">[Add cards as attachments to messages](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true).</span></span>
  * <span data-ttu-id="a890c-116">[Карты пример кода Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards).</span><span class="sxs-lookup"><span data-stu-id="a890c-116">[Cards sample code Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards).</span></span>

## <a name="types-of-cards"></a><span data-ttu-id="a890c-117">Типы карт</span><span class="sxs-lookup"><span data-stu-id="a890c-117">Types of cards</span></span>

<span data-ttu-id="a890c-118">В этой таблице показаны типы доступных вам карт:</span><span class="sxs-lookup"><span data-stu-id="a890c-118">This table shows the types of cards available to you:</span></span>

| <span data-ttu-id="a890c-119">Тип карты</span><span class="sxs-lookup"><span data-stu-id="a890c-119">Card type</span></span> | <span data-ttu-id="a890c-120">Описание</span><span class="sxs-lookup"><span data-stu-id="a890c-120">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="a890c-121">Адаптивная карта</span><span class="sxs-lookup"><span data-stu-id="a890c-121">Adaptive card</span></span>](#adaptive-card) | <span data-ttu-id="a890c-122">Эта карта является высоко настраиваемой картой, которая может содержать любое сочетание текстов, речи, изображений, кнопок и полей ввода.</span><span class="sxs-lookup"><span data-stu-id="a890c-122">This card is highly customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> |
| [<span data-ttu-id="a890c-123">Карта hero</span><span class="sxs-lookup"><span data-stu-id="a890c-123">Hero card</span></span>](#hero-card) | <span data-ttu-id="a890c-124">Эта карта обычно содержит одно большое изображение, одну или несколько кнопок и небольшое количество текста.</span><span class="sxs-lookup"><span data-stu-id="a890c-124">This card typically contains a single large image, one or more buttons, and a small amount of text.</span></span> |
| [<span data-ttu-id="a890c-125">Карта списка</span><span class="sxs-lookup"><span data-stu-id="a890c-125">List card</span></span>](#list-card) | <span data-ttu-id="a890c-126">Эта карта — это список элементов прокрутки.</span><span class="sxs-lookup"><span data-stu-id="a890c-126">This card is a scrolling list of items.</span></span> |
| [<span data-ttu-id="a890c-127">Office 365 соединители</span><span class="sxs-lookup"><span data-stu-id="a890c-127">Office 365 connector card</span></span>](#office-365-connector-card) | <span data-ttu-id="a890c-128">Эта карта имеет гибкий макет с несколькими разделами, полями, изображениями и действиями.</span><span class="sxs-lookup"><span data-stu-id="a890c-128">This card has a flexible layout with multiple sections, fields, images, and actions.</span></span> |
| [<span data-ttu-id="a890c-129">Карта получения</span><span class="sxs-lookup"><span data-stu-id="a890c-129">Receipt card</span></span>](#receipt-card) | <span data-ttu-id="a890c-130">Эта карта предоставляет квитанцию пользователю.</span><span class="sxs-lookup"><span data-stu-id="a890c-130">This card provides a receipt to the user.</span></span> |
| [<span data-ttu-id="a890c-131">Карточка Signin</span><span class="sxs-lookup"><span data-stu-id="a890c-131">Signin card</span></span>](#signin-card) | <span data-ttu-id="a890c-132">Эта карта позволяет боту запрашивать, чтобы пользователь войди.</span><span class="sxs-lookup"><span data-stu-id="a890c-132">This card enables a bot to request that a user signs in.</span></span> |
| [<span data-ttu-id="a890c-133">Карта эскиза</span><span class="sxs-lookup"><span data-stu-id="a890c-133">Thumbnail card</span></span>](#thumbnail-card) | <span data-ttu-id="a890c-134">Эта карта обычно содержит одно изображение эскиза, короткий текст и одну или несколько кнопок.</span><span class="sxs-lookup"><span data-stu-id="a890c-134">This card typically contains a single thumbnail image, some short text, and one or more buttons.</span></span> |
| [<span data-ttu-id="a890c-135">Коллекции карт</span><span class="sxs-lookup"><span data-stu-id="a890c-135">Card collections</span></span>](#card-collections) | <span data-ttu-id="a890c-136">Эти карты используются для возврата нескольких элементов в одном ответе.</span><span class="sxs-lookup"><span data-stu-id="a890c-136">This cards is used to return multiple items in a single response.</span></span> |

## <a name="common-properties-for-all-cards"></a><span data-ttu-id="a890c-137">Общие свойства для всех карт</span><span class="sxs-lookup"><span data-stu-id="a890c-137">Common properties for all cards</span></span>

### <a name="inline-card-images"></a><span data-ttu-id="a890c-138">Inline card images</span><span class="sxs-lookup"><span data-stu-id="a890c-138">Inline card images</span></span>

<span data-ttu-id="a890c-139">Карта может содержать рядное изображение, включив ссылку на общедоступный образ.</span><span class="sxs-lookup"><span data-stu-id="a890c-139">The card can contain an inline image by including a link to the publicly available image.</span></span> <span data-ttu-id="a890c-140">В целях производительности рекомендуется использовать изображение в общедоступных сетях доставки контента (CDN).</span><span class="sxs-lookup"><span data-stu-id="a890c-140">For performance purposes, it is highly recommended you host the image on a public content-delivery network (CDN).</span></span>

<span data-ttu-id="a890c-141">Изображения масштабироваться или по размеру при сохранении соотношения аспектов для покрытия области изображения.</span><span class="sxs-lookup"><span data-stu-id="a890c-141">Images are scaled up or down in size while maintaining the aspect ratio to cover the image area.</span></span> <span data-ttu-id="a890c-142">Затем изображения обрезаются из центра, чтобы достичь соответствующего соотношения аспектов для карты.</span><span class="sxs-lookup"><span data-stu-id="a890c-142">Images are then cropped from center to achieve the appropriate aspect ratio for the card.</span></span>

<span data-ttu-id="a890c-143">Изображения должны быть не более 1024×1024 в формате PNG, JPEG или GIF и не поддерживают анимированный GIF.</span><span class="sxs-lookup"><span data-stu-id="a890c-143">Images must be at most 1024×1024, in PNG, JPEG, or GIF format, and do not support animated GIF.</span></span>

| <span data-ttu-id="a890c-144">Свойство</span><span class="sxs-lookup"><span data-stu-id="a890c-144">Property</span></span> | <span data-ttu-id="a890c-145">Тип</span><span class="sxs-lookup"><span data-stu-id="a890c-145">Type</span></span>  | <span data-ttu-id="a890c-146">Описание</span><span class="sxs-lookup"><span data-stu-id="a890c-146">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a890c-147">url</span><span class="sxs-lookup"><span data-stu-id="a890c-147">url</span></span> | <span data-ttu-id="a890c-148">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="a890c-148">URL</span></span> | <span data-ttu-id="a890c-149">URL-адрес HTTPS к изображению.</span><span class="sxs-lookup"><span data-stu-id="a890c-149">HTTPS URL to the image.</span></span> |
| <span data-ttu-id="a890c-150">alt</span><span class="sxs-lookup"><span data-stu-id="a890c-150">alt</span></span> | <span data-ttu-id="a890c-151">String</span><span class="sxs-lookup"><span data-stu-id="a890c-151">String</span></span> | <span data-ttu-id="a890c-152">Доступное описание изображения.</span><span class="sxs-lookup"><span data-stu-id="a890c-152">Accessible description of the image.</span></span> |

> [!NOTE]
> <span data-ttu-id="a890c-153">Если карта содержит URL-адрес изображения, который проходит перенаправление перед окончательным изображением, перенаправление в URL-адрес изображения не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="a890c-153">If a card includes an image URL that goes through a redirect before the final image, the redirect in image URL is not supported.</span></span> <span data-ttu-id="a890c-154">Это происходит для изображений, общих в общедоступных облаках.</span><span class="sxs-lookup"><span data-stu-id="a890c-154">This occurs for images shared on the public cloud.</span></span>

### <a name="buttons"></a><span data-ttu-id="a890c-155">Кнопки</span><span class="sxs-lookup"><span data-stu-id="a890c-155">Buttons</span></span>

<span data-ttu-id="a890c-156">Кнопки показаны в нижней части карты.</span><span class="sxs-lookup"><span data-stu-id="a890c-156">Buttons are shown stacked at the bottom of the card.</span></span> <span data-ttu-id="a890c-157">Текст кнопки всегда находится в одной строке и усечен, если текст превышает ширину кнопки.</span><span class="sxs-lookup"><span data-stu-id="a890c-157">Button text is always on a single line and is truncated if the text exceeds the button width.</span></span> <span data-ttu-id="a890c-158">Никаких дополнительных кнопок, помимо максимального числа, поддерживаемого картой, не отображается.</span><span class="sxs-lookup"><span data-stu-id="a890c-158">Any additional buttons beyond the maximum number supported by the card are not shown.</span></span>

<span data-ttu-id="a890c-159">Дополнительные сведения см. в [карточных действиях.](~/task-modules-and-cards/cards/cards-actions.md)</span><span class="sxs-lookup"><span data-stu-id="a890c-159">For more information, see [card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

### <a name="card-formatting"></a><span data-ttu-id="a890c-160">Форматирование карт</span><span class="sxs-lookup"><span data-stu-id="a890c-160">Card formatting</span></span>

<span data-ttu-id="a890c-161">Дополнительные сведения о форматирования текста в картах см. [в документе форматирование карт.](~/task-modules-and-cards/cards/cards-format.md)</span><span class="sxs-lookup"><span data-stu-id="a890c-161">For more information on text formatting in cards, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span>

## <a name="adaptive-card"></a><span data-ttu-id="a890c-162">Адаптивная карта</span><span class="sxs-lookup"><span data-stu-id="a890c-162">Adaptive card</span></span>

<span data-ttu-id="a890c-163">Адаптивная карта — это настраиваемая карта, которая может содержать любое сочетание текстовых, речевого, изображений, кнопок и полей ввода.</span><span class="sxs-lookup"><span data-stu-id="a890c-163">An adaptive card is a customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> <span data-ttu-id="a890c-164">Дополнительные сведения см. в [рублях адаптивных карт v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span><span class="sxs-lookup"><span data-stu-id="a890c-164">For more information, see [adaptive cards v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span></span>

### <a name="support-for-adaptive-cards"></a><span data-ttu-id="a890c-165">Поддержка адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="a890c-165">Support for adaptive cards</span></span>

| <span data-ttu-id="a890c-166">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="a890c-166">Bots in Teams</span></span> | <span data-ttu-id="a890c-167">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="a890c-167">Messaging extensions</span></span>  | <span data-ttu-id="a890c-168">Соединители</span><span class="sxs-lookup"><span data-stu-id="a890c-168">Connectors</span></span> | <span data-ttu-id="a890c-169">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="a890c-169">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a890c-170">✔</span><span class="sxs-lookup"><span data-stu-id="a890c-170">✔</span></span> | <span data-ttu-id="a890c-171">✔</span><span class="sxs-lookup"><span data-stu-id="a890c-171">✔</span></span> | <span data-ttu-id="a890c-172">✖</span><span class="sxs-lookup"><span data-stu-id="a890c-172">✖</span></span> | <span data-ttu-id="a890c-173">✔</span><span class="sxs-lookup"><span data-stu-id="a890c-173">✔</span></span> |

> [!NOTE]
> * <span data-ttu-id="a890c-174">Teams поддерживает v1.2 или более ранние функции адаптивной карты.</span><span class="sxs-lookup"><span data-stu-id="a890c-174">Teams platform supports v1.2 or earlier of adaptive card features.</span></span>
> * <span data-ttu-id="a890c-175">Элементы мультимедиа в настоящее время не поддерживаются в адаптивной карте v1.2 на Teams платформе.</span><span class="sxs-lookup"><span data-stu-id="a890c-175">Media elements are currently not supported in adaptive card v1.2 on the Teams platform.</span></span>

### <a name="example-of-an-adaptive-card"></a><span data-ttu-id="a890c-176">Пример адаптивной карты</span><span class="sxs-lookup"><span data-stu-id="a890c-176">Example of an adaptive card</span></span>

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

#### <a name="additional-information-on-adaptive-cards"></a><span data-ttu-id="a890c-178">Дополнительные сведения о адаптивных картах</span><span class="sxs-lookup"><span data-stu-id="a890c-178">Additional information on adaptive cards</span></span>

<span data-ttu-id="a890c-179">Ссылка на Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="a890c-179">Bot Framework reference:</span></span>

* [<span data-ttu-id="a890c-180">Адаптивные Node.js</span><span class="sxs-lookup"><span data-stu-id="a890c-180">Adaptive cards Node.js</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)
* [<span data-ttu-id="a890c-181">Адаптивная карта C #</span><span class="sxs-lookup"><span data-stu-id="a890c-181">Adaptive card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)

## <a name="hero-card"></a><span data-ttu-id="a890c-182">Карта hero</span><span class="sxs-lookup"><span data-stu-id="a890c-182">Hero card</span></span>

<span data-ttu-id="a890c-183">Карта, которая обычно содержит одно большое изображение, одну или несколько кнопок и текст.</span><span class="sxs-lookup"><span data-stu-id="a890c-183">A card that typically contains a single large image, one or more buttons, and text.</span></span>

### <a name="support-for-hero-cards"></a><span data-ttu-id="a890c-184">Поддержка карт-героев</span><span class="sxs-lookup"><span data-stu-id="a890c-184">Support for hero cards</span></span>

| <span data-ttu-id="a890c-185">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="a890c-185">Bots in Teams</span></span> | <span data-ttu-id="a890c-186">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="a890c-186">Messaging extensions</span></span>  | <span data-ttu-id="a890c-187">Соединители</span><span class="sxs-lookup"><span data-stu-id="a890c-187">Connectors</span></span> | <span data-ttu-id="a890c-188">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="a890c-188">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a890c-189">✔</span><span class="sxs-lookup"><span data-stu-id="a890c-189">✔</span></span> | <span data-ttu-id="a890c-190">✔</span><span class="sxs-lookup"><span data-stu-id="a890c-190">✔</span></span> | <span data-ttu-id="a890c-191">✖</span><span class="sxs-lookup"><span data-stu-id="a890c-191">✖</span></span> | <span data-ttu-id="a890c-192">✔</span><span class="sxs-lookup"><span data-stu-id="a890c-192">✔</span></span> |

### <a name="properties-of-a-hero-card"></a><span data-ttu-id="a890c-193">Свойства карты-героя</span><span class="sxs-lookup"><span data-stu-id="a890c-193">Properties of a hero card</span></span>

| <span data-ttu-id="a890c-194">Свойство</span><span class="sxs-lookup"><span data-stu-id="a890c-194">Property</span></span> | <span data-ttu-id="a890c-195">Тип</span><span class="sxs-lookup"><span data-stu-id="a890c-195">Type</span></span>  | <span data-ttu-id="a890c-196">Описание</span><span class="sxs-lookup"><span data-stu-id="a890c-196">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a890c-197">title</span><span class="sxs-lookup"><span data-stu-id="a890c-197">title</span></span> | <span data-ttu-id="a890c-198">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="a890c-198">Rich text</span></span> | <span data-ttu-id="a890c-199">Название карты.</span><span class="sxs-lookup"><span data-stu-id="a890c-199">Title of the card.</span></span> <span data-ttu-id="a890c-200">Максимум 2 строки.</span><span class="sxs-lookup"><span data-stu-id="a890c-200">Maximum 2 lines.</span></span> |
| <span data-ttu-id="a890c-201">субтитры</span><span class="sxs-lookup"><span data-stu-id="a890c-201">subtitle</span></span> | <span data-ttu-id="a890c-202">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="a890c-202">Rich text</span></span> | <span data-ttu-id="a890c-203">Субтитр карты.</span><span class="sxs-lookup"><span data-stu-id="a890c-203">Subtitle of the card.</span></span> <span data-ttu-id="a890c-204">Максимум 2 строки.</span><span class="sxs-lookup"><span data-stu-id="a890c-204">Maximum 2 lines.</span></span>|
| <span data-ttu-id="a890c-205">текст</span><span class="sxs-lookup"><span data-stu-id="a890c-205">text</span></span> | <span data-ttu-id="a890c-206">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="a890c-206">Rich text</span></span> | <span data-ttu-id="a890c-207">Текст отображается под субтитром.</span><span class="sxs-lookup"><span data-stu-id="a890c-207">Text appears under the subtitle.</span></span> <span data-ttu-id="a890c-208">Параметры форматирования см. [в виде форматирования карт.](~/task-modules-and-cards/cards/cards-format.md)</span><span class="sxs-lookup"><span data-stu-id="a890c-208">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="a890c-209">изображения</span><span class="sxs-lookup"><span data-stu-id="a890c-209">images</span></span> | <span data-ttu-id="a890c-210">Массив изображений</span><span class="sxs-lookup"><span data-stu-id="a890c-210">Array of images</span></span> | <span data-ttu-id="a890c-211">Изображение, отображаемого в верхней части карты.</span><span class="sxs-lookup"><span data-stu-id="a890c-211">Image displayed at the top of the card.</span></span> <span data-ttu-id="a890c-212">Соотношение аспектов 16:9.</span><span class="sxs-lookup"><span data-stu-id="a890c-212">Aspect ratio 16:9.</span></span> |
| <span data-ttu-id="a890c-213">кнопки</span><span class="sxs-lookup"><span data-stu-id="a890c-213">buttons</span></span> | <span data-ttu-id="a890c-214">Массив объектов действий</span><span class="sxs-lookup"><span data-stu-id="a890c-214">Array of action objects</span></span> | <span data-ttu-id="a890c-215">Набор действий, применимых к текущей карте.</span><span class="sxs-lookup"><span data-stu-id="a890c-215">Set of actions applicable to the current card.</span></span> <span data-ttu-id="a890c-216">Максимум 6.</span><span class="sxs-lookup"><span data-stu-id="a890c-216">Maximum 6.</span></span> |
| <span data-ttu-id="a890c-217">нажмите кнопку</span><span class="sxs-lookup"><span data-stu-id="a890c-217">tap</span></span> | <span data-ttu-id="a890c-218">Объект Action</span><span class="sxs-lookup"><span data-stu-id="a890c-218">Action object</span></span> | <span data-ttu-id="a890c-219">Активируется при нажатии на карточку самого пользователя.</span><span class="sxs-lookup"><span data-stu-id="a890c-219">Activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-hero-card"></a><span data-ttu-id="a890c-220">Пример карточки героя</span><span class="sxs-lookup"><span data-stu-id="a890c-220">Example of a hero card</span></span>

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

### <a name="additional-information-on-hero-cards"></a><span data-ttu-id="a890c-222">Дополнительные сведения о картах-героях</span><span class="sxs-lookup"><span data-stu-id="a890c-222">Additional information on hero cards</span></span>

<span data-ttu-id="a890c-223">Ссылка на Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="a890c-223">Bot Framework reference:</span></span>

* [<span data-ttu-id="a890c-224">Карточка героя Node.js</span><span class="sxs-lookup"><span data-stu-id="a890c-224">Hero card Node.js</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-a-hero-card&preserve-view=true)
* [<span data-ttu-id="a890c-225">Карта героя C #</span><span class="sxs-lookup"><span data-stu-id="a890c-225">Hero card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-hero-card&preserve-view=true)

## <a name="list-card"></a><span data-ttu-id="a890c-226">Карта списка</span><span class="sxs-lookup"><span data-stu-id="a890c-226">List card</span></span>

<span data-ttu-id="a890c-227">Карта списка была добавлена Teams для предоставления функций, которые не могут предоставляться в коллекции списков.</span><span class="sxs-lookup"><span data-stu-id="a890c-227">The list card has been added by Teams to provide functions beyond what the list collection can provide.</span></span> <span data-ttu-id="a890c-228">Карта списка содержит список элементов для прокрутки.</span><span class="sxs-lookup"><span data-stu-id="a890c-228">The list card provides a scrolling list of items.</span></span>

### <a name="support-for-list-cards"></a><span data-ttu-id="a890c-229">Поддержка карт списка</span><span class="sxs-lookup"><span data-stu-id="a890c-229">Support for list cards</span></span>

| <span data-ttu-id="a890c-230">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="a890c-230">Bots in Teams</span></span> | <span data-ttu-id="a890c-231">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="a890c-231">Messaging extensions</span></span>  | <span data-ttu-id="a890c-232">Соединители</span><span class="sxs-lookup"><span data-stu-id="a890c-232">Connectors</span></span> | <span data-ttu-id="a890c-233">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="a890c-233">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a890c-234">✔</span><span class="sxs-lookup"><span data-stu-id="a890c-234">✔</span></span> | <span data-ttu-id="a890c-235">✖</span><span class="sxs-lookup"><span data-stu-id="a890c-235">✖</span></span> | <span data-ttu-id="a890c-236">✖</span><span class="sxs-lookup"><span data-stu-id="a890c-236">✖</span></span> |<span data-ttu-id="a890c-237">✔</span><span class="sxs-lookup"><span data-stu-id="a890c-237">✔</span></span> |

### <a name="properties-of-a-list-card"></a><span data-ttu-id="a890c-238">Свойства карты списка</span><span class="sxs-lookup"><span data-stu-id="a890c-238">Properties of a list card</span></span>

| <span data-ttu-id="a890c-239">Свойство</span><span class="sxs-lookup"><span data-stu-id="a890c-239">Property</span></span> | <span data-ttu-id="a890c-240">Тип</span><span class="sxs-lookup"><span data-stu-id="a890c-240">Type</span></span>  | <span data-ttu-id="a890c-241">Описание</span><span class="sxs-lookup"><span data-stu-id="a890c-241">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a890c-242">title</span><span class="sxs-lookup"><span data-stu-id="a890c-242">title</span></span> | <span data-ttu-id="a890c-243">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="a890c-243">Rich text</span></span> | <span data-ttu-id="a890c-244">Название карты.</span><span class="sxs-lookup"><span data-stu-id="a890c-244">Title of the card.</span></span> <span data-ttu-id="a890c-245">Максимум 2 строки.</span><span class="sxs-lookup"><span data-stu-id="a890c-245">Maximum 2 lines.</span></span>|
| <span data-ttu-id="a890c-246">элементы</span><span class="sxs-lookup"><span data-stu-id="a890c-246">items</span></span> | <span data-ttu-id="a890c-247">Массив элементов списка</span><span class="sxs-lookup"><span data-stu-id="a890c-247">Array of list items</span></span> ||
| <span data-ttu-id="a890c-248">кнопки</span><span class="sxs-lookup"><span data-stu-id="a890c-248">buttons</span></span> | <span data-ttu-id="a890c-249">Массив объектов действий</span><span class="sxs-lookup"><span data-stu-id="a890c-249">Array of action objects</span></span> | <span data-ttu-id="a890c-250">Набор действий, применимых к текущей карте.</span><span class="sxs-lookup"><span data-stu-id="a890c-250">Set of actions applicable to the current card.</span></span> <span data-ttu-id="a890c-251">Максимум 6.</span><span class="sxs-lookup"><span data-stu-id="a890c-251">Maximum 6.</span></span> |

### <a name="example-of-a-list-card"></a><span data-ttu-id="a890c-252">Пример карты списка</span><span class="sxs-lookup"><span data-stu-id="a890c-252">Example of a list card</span></span>

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

## <a name="office-365-connector-card"></a><span data-ttu-id="a890c-253">Office 365 соединители</span><span class="sxs-lookup"><span data-stu-id="a890c-253">Office 365 connector card</span></span>

<span data-ttu-id="a890c-254">Соедините Office 365 поддерживается в Teams, а не в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="a890c-254">The Office 365 connector card is supported in Teams, not in Bot Framework.</span></span> <span data-ttu-id="a890c-255">Эта карта обеспечивает гибкую схему с несколькими разделами, полями, изображениями и действиями.</span><span class="sxs-lookup"><span data-stu-id="a890c-255">This card provides a flexible layout with multiple sections, fields, images, and actions.</span></span> <span data-ttu-id="a890c-256">Эта карта инкапсулирует соединителем карту, чтобы она была использована ботами.</span><span class="sxs-lookup"><span data-stu-id="a890c-256">This card encapsulates a connector card so that it can be used by bots.</span></span> <span data-ttu-id="a890c-257">О различиях между соединитеными картами и картой O365 см. в заметках на [Office 365 соединители.](#notes-on-the-office-365-connector-card)</span><span class="sxs-lookup"><span data-stu-id="a890c-257">For differences between connector cards and the O365 card, see [Notes on the Office 365 connector card](#notes-on-the-office-365-connector-card).</span></span>

### <a name="support-for-office-365-connector-cards"></a><span data-ttu-id="a890c-258">Поддержка Office 365 соединители</span><span class="sxs-lookup"><span data-stu-id="a890c-258">Support for Office 365 connector cards</span></span>

| <span data-ttu-id="a890c-259">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="a890c-259">Bots in Teams</span></span> | <span data-ttu-id="a890c-260">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="a890c-260">Messaging extensions</span></span>  | <span data-ttu-id="a890c-261">Соединители</span><span class="sxs-lookup"><span data-stu-id="a890c-261">Connectors</span></span> | <span data-ttu-id="a890c-262">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="a890c-262">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a890c-263">✔</span><span class="sxs-lookup"><span data-stu-id="a890c-263">✔</span></span> | <span data-ttu-id="a890c-264">✔</span><span class="sxs-lookup"><span data-stu-id="a890c-264">✔</span></span> | <span data-ttu-id="a890c-265">✔</span><span class="sxs-lookup"><span data-stu-id="a890c-265">✔</span></span> | <span data-ttu-id="a890c-266">✖</span><span class="sxs-lookup"><span data-stu-id="a890c-266">✖</span></span> |

### <a name="properties-of-the-office-365-connector-card"></a><span data-ttu-id="a890c-267">Свойства карты Office 365 соединители</span><span class="sxs-lookup"><span data-stu-id="a890c-267">Properties of the Office 365 connector card</span></span>

| <span data-ttu-id="a890c-268">Свойство</span><span class="sxs-lookup"><span data-stu-id="a890c-268">Property</span></span> | <span data-ttu-id="a890c-269">Тип</span><span class="sxs-lookup"><span data-stu-id="a890c-269">Type</span></span>  | <span data-ttu-id="a890c-270">Описание</span><span class="sxs-lookup"><span data-stu-id="a890c-270">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a890c-271">title</span><span class="sxs-lookup"><span data-stu-id="a890c-271">title</span></span> | <span data-ttu-id="a890c-272">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="a890c-272">Rich text</span></span> | <span data-ttu-id="a890c-273">Название карты.</span><span class="sxs-lookup"><span data-stu-id="a890c-273">Title of the card.</span></span> <span data-ttu-id="a890c-274">Максимум 2 строки.</span><span class="sxs-lookup"><span data-stu-id="a890c-274">Maximum 2 lines.</span></span> |
| <span data-ttu-id="a890c-275">summary</span><span class="sxs-lookup"><span data-stu-id="a890c-275">summary</span></span> | <span data-ttu-id="a890c-276">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="a890c-276">Rich text</span></span> | <span data-ttu-id="a890c-277">Сводка карты.</span><span class="sxs-lookup"><span data-stu-id="a890c-277">Summary of the card.</span></span> <span data-ttu-id="a890c-278">Максимум 2 строки.</span><span class="sxs-lookup"><span data-stu-id="a890c-278">Maximum 2 lines.</span></span> |
| <span data-ttu-id="a890c-279">текст</span><span class="sxs-lookup"><span data-stu-id="a890c-279">text</span></span> | <span data-ttu-id="a890c-280">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="a890c-280">Rich text</span></span> | <span data-ttu-id="a890c-281">Текст отображается под субтитром.</span><span class="sxs-lookup"><span data-stu-id="a890c-281">Text appears under the subtitle.</span></span> <span data-ttu-id="a890c-282">Параметры форматирования см. [в виде форматирования карт.](~/task-modules-and-cards/cards/cards-format.md)</span><span class="sxs-lookup"><span data-stu-id="a890c-282">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="a890c-283">themeColor</span><span class="sxs-lookup"><span data-stu-id="a890c-283">themeColor</span></span> | <span data-ttu-id="a890c-284">Строка HEX</span><span class="sxs-lookup"><span data-stu-id="a890c-284">HEX string</span></span> | <span data-ttu-id="a890c-285">Цвет, который переопределяет accentColor, предоставленный из манифеста приложения.</span><span class="sxs-lookup"><span data-stu-id="a890c-285">Color that overrides the accentColor provided from the application manifest.</span></span> |

### <a name="notes-on-the-office-365-connector-card"></a><span data-ttu-id="a890c-286">Заметки на Office 365 соединители</span><span class="sxs-lookup"><span data-stu-id="a890c-286">Notes on the Office 365 connector card</span></span>

<span data-ttu-id="a890c-287">Office 365 соединители карточки работают правильно в Microsoft Teams, включая [действия ActionCard](/outlook/actionable-messages/card-reference#actioncard-action).</span><span class="sxs-lookup"><span data-stu-id="a890c-287">Office 365 connector cards function properly in Microsoft Teams, including [ActionCard actions](/outlook/actionable-messages/card-reference#actioncard-action).</span></span>

<span data-ttu-id="a890c-288">Одним из важных отличий между использованием соединитеных карт из соединитетеля и использованием соединитеных карт в боте является обработка действий карт.</span><span class="sxs-lookup"><span data-stu-id="a890c-288">One important difference between using connector cards from a connector and using connector cards in your bot is the handling of card actions.</span></span>

* <span data-ttu-id="a890c-289">Для соединитетеля конечная точка получает полезное сообщение карточки через HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="a890c-289">For a connector, the endpoint receives the card payload through HTTP POST.</span></span>
* <span data-ttu-id="a890c-290">Для бота действие запускает действие, которое отправляет боту только ID действия и `HttpPOST` `invoke` тело.</span><span class="sxs-lookup"><span data-stu-id="a890c-290">For a bot, the `HttpPOST` action triggers an `invoke` activity that sends only the action ID and body to the bot.</span></span>

<span data-ttu-id="a890c-291">Каждая соединитечная карта может отображать не более десяти разделов, а каждый раздел может содержать не более пяти изображений и пять действий.</span><span class="sxs-lookup"><span data-stu-id="a890c-291">Each connector card can display a maximum of ten sections, and each section can contain a maximum of five images and five actions.</span></span>

> [!NOTE]
> <span data-ttu-id="a890c-292">Дополнительные разделы, изображения или действия в сообщении не отображаются.</span><span class="sxs-lookup"><span data-stu-id="a890c-292">Any additional sections, images, or actions in a message do not appear.</span></span>

<span data-ttu-id="a890c-293">Все текстовые поля поддерживают разметку и HTML.</span><span class="sxs-lookup"><span data-stu-id="a890c-293">All text fields support markdown and HTML.</span></span> <span data-ttu-id="a890c-294">Вы можете контролировать, в каких разделах используется разметка или HTML, установив `markdown` свойство в сообщении.</span><span class="sxs-lookup"><span data-stu-id="a890c-294">You can control which sections use markdown or HTML by setting the `markdown` property in a message.</span></span> <span data-ttu-id="a890c-295">По умолчанию `markdown` установлено `true` значение .</span><span class="sxs-lookup"><span data-stu-id="a890c-295">By default, `markdown` is set to `true`.</span></span> <span data-ttu-id="a890c-296">Если вы хотите использовать HTML вместо этого, установите `markdown` `false` .</span><span class="sxs-lookup"><span data-stu-id="a890c-296">If you want to use HTML instead, set `markdown` to `false`.</span></span>

<span data-ttu-id="a890c-297">Если указать `themeColor` свойство, оно переопределит `accentColor` свойство в манифесте приложения.</span><span class="sxs-lookup"><span data-stu-id="a890c-297">If you specify the `themeColor` property, it overrides the `accentColor` property in the app manifest.</span></span>

<span data-ttu-id="a890c-298">Чтобы указать стиль `activityImage` визуализации, можно задать `activityImageType` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a890c-298">To specify the rendering style for `activityImage`, you can set `activityImageType` as follows:</span></span>

| <span data-ttu-id="a890c-299">Значение</span><span class="sxs-lookup"><span data-stu-id="a890c-299">Value</span></span> | <span data-ttu-id="a890c-300">Описание</span><span class="sxs-lookup"><span data-stu-id="a890c-300">Description</span></span> |
| --- | --- |
| `avatar` | <span data-ttu-id="a890c-301">По умолчанию; `activityImage` обрезается как круг.</span><span class="sxs-lookup"><span data-stu-id="a890c-301">Default; `activityImage` is cropped as a circle.</span></span> |
| `article` | <span data-ttu-id="a890c-302">`activityImage` отображается в качестве прямоугольника и сохраняет отношение аспектов.</span><span class="sxs-lookup"><span data-stu-id="a890c-302">`activityImage` is displayed as a rectangle and retains its aspect ratio.</span></span> |

<span data-ttu-id="a890c-303">Другие сведения о свойствах карт соединители см. в справке к карточкам [сообщений.](/outlook/actionable-messages/card-reference)</span><span class="sxs-lookup"><span data-stu-id="a890c-303">For all other details about connector card properties, see [actionable message card reference](/outlook/actionable-messages/card-reference).</span></span> <span data-ttu-id="a890c-304">Единственными свойствами карт соединители, Microsoft Teams которые в настоящее время не поддерживаются, являются следующими:</span><span class="sxs-lookup"><span data-stu-id="a890c-304">The only connector card properties that Microsoft Teams does not currently support are as follows:</span></span>

* `heroImage`
* `hideOriginalBody`
* <span data-ttu-id="a890c-305">`startGroup`всегда рассматривается как `true` в Teams</span><span class="sxs-lookup"><span data-stu-id="a890c-305">`startGroup` always treated as `true` in Teams</span></span>
* `originator`
* `correlationId`

### <a name="example-of-an-office-365-connector-card"></a><span data-ttu-id="a890c-306">Пример карты Office 365 соединители</span><span class="sxs-lookup"><span data-stu-id="a890c-306">Example of an Office 365 connector card</span></span>

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

## <a name="receipt-card"></a><span data-ttu-id="a890c-307">Карта получения</span><span class="sxs-lookup"><span data-stu-id="a890c-307">Receipt card</span></span>

<span data-ttu-id="a890c-308">Teams поддерживает карточку получения.</span><span class="sxs-lookup"><span data-stu-id="a890c-308">Teams supports receipt card.</span></span> <span data-ttu-id="a890c-309">Это карточка, которая позволяет боту предоставлять пользователю квитанцию.</span><span class="sxs-lookup"><span data-stu-id="a890c-309">It is a card that enables a bot to provide a receipt to the user.</span></span> <span data-ttu-id="a890c-310">Обычно он содержит список элементов, которые необходимо включить в квитанцию, например налоговые и общие сведения.</span><span class="sxs-lookup"><span data-stu-id="a890c-310">It typically contains the list of items to include on the receipt, such as tax and total information.</span></span>

### <a name="support-for-receipt-cards"></a><span data-ttu-id="a890c-311">Поддержка карт получения</span><span class="sxs-lookup"><span data-stu-id="a890c-311">Support for receipt cards</span></span>

| <span data-ttu-id="a890c-312">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="a890c-312">Bots in Teams</span></span> | <span data-ttu-id="a890c-313">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="a890c-313">Messaging extensions</span></span>  | <span data-ttu-id="a890c-314">Соединители</span><span class="sxs-lookup"><span data-stu-id="a890c-314">Connectors</span></span> | <span data-ttu-id="a890c-315">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="a890c-315">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a890c-316">✔</span><span class="sxs-lookup"><span data-stu-id="a890c-316">✔</span></span> | <span data-ttu-id="a890c-317">✔</span><span class="sxs-lookup"><span data-stu-id="a890c-317">✔</span></span> | <span data-ttu-id="a890c-318">✖</span><span class="sxs-lookup"><span data-stu-id="a890c-318">✖</span></span> | <span data-ttu-id="a890c-319">✔</span><span class="sxs-lookup"><span data-stu-id="a890c-319">✔</span></span> |

### <a name="example-of-a-receipt-card"></a><span data-ttu-id="a890c-320">Пример карты получения</span><span class="sxs-lookup"><span data-stu-id="a890c-320">Example of a receipt card</span></span>

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

### <a name="additional-information-on-receipt-cards"></a><span data-ttu-id="a890c-322">Дополнительные сведения о карточках получения</span><span class="sxs-lookup"><span data-stu-id="a890c-322">Additional information on receipt cards</span></span>

<span data-ttu-id="a890c-323">Ссылка на Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="a890c-323">Bot Framework reference:</span></span>

* [<span data-ttu-id="a890c-324">Карточка получения Node.js</span><span class="sxs-lookup"><span data-stu-id="a890c-324">Receipt card Node.js</span></span>](/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="a890c-325">Карта получения C #</span><span class="sxs-lookup"><span data-stu-id="a890c-325">Receipt card C#</span></span>](/dotnet/api/microsoft.bot.schema.receiptcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="signin-card"></a><span data-ttu-id="a890c-326">Карточка Signin</span><span class="sxs-lookup"><span data-stu-id="a890c-326">Signin card</span></span>

<span data-ttu-id="a890c-327">Карта Signin позволяет боту запрашивать вход пользователя.</span><span class="sxs-lookup"><span data-stu-id="a890c-327">Signin card enables a bot to request a user to sign in.</span></span> <span data-ttu-id="a890c-328">Поддерживается в Teams в несколько иной форме, чем в bot Framework.</span><span class="sxs-lookup"><span data-stu-id="a890c-328">It is supported in Teams in a slightly different form than is found in the Bot Framework.</span></span> <span data-ttu-id="a890c-329">Карта signin в Teams похожа на карточку signin в bot Framework, за исключением того, что карточка signin в Teams поддерживает только два действия: `signin` и `openUrl` .</span><span class="sxs-lookup"><span data-stu-id="a890c-329">The signin card in Teams is similar to the signin card in the Bot Framework except that the signin card in Teams only supports two actions: `signin` and `openUrl`.</span></span>

<span data-ttu-id="a890c-330">Действие signin можно использовать с любой карты в Teams, а не только с карты signin.</span><span class="sxs-lookup"><span data-stu-id="a890c-330">The signin action can be used from any card in Teams, not just the signin card.</span></span> <span data-ttu-id="a890c-331">Дополнительные сведения о проверке подлинности см. в Microsoft Teams поток проверки [подлинности для ботов.](~/bots/how-to/authentication/auth-flow-bot.md)</span><span class="sxs-lookup"><span data-stu-id="a890c-331">For more information on authentication, see [Microsoft Teams authentication flow for bots](~/bots/how-to/authentication/auth-flow-bot.md).</span></span>

### <a name="support-for-signin-cards"></a><span data-ttu-id="a890c-332">Поддержка подписных карт</span><span class="sxs-lookup"><span data-stu-id="a890c-332">Support for signin cards</span></span>

| <span data-ttu-id="a890c-333">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="a890c-333">Bots in Teams</span></span> | <span data-ttu-id="a890c-334">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="a890c-334">Messaging extensions</span></span>  | <span data-ttu-id="a890c-335">Соединители</span><span class="sxs-lookup"><span data-stu-id="a890c-335">Connectors</span></span> | <span data-ttu-id="a890c-336">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="a890c-336">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a890c-337">✔</span><span class="sxs-lookup"><span data-stu-id="a890c-337">✔</span></span> | <span data-ttu-id="a890c-338">✖</span><span class="sxs-lookup"><span data-stu-id="a890c-338">✖</span></span> | <span data-ttu-id="a890c-339">✖</span><span class="sxs-lookup"><span data-stu-id="a890c-339">✖</span></span> | <span data-ttu-id="a890c-340">✔</span><span class="sxs-lookup"><span data-stu-id="a890c-340">✔</span></span> |

### <a name="additional-information-on-signin-cards"></a><span data-ttu-id="a890c-341">Дополнительные сведения о подписных карточках</span><span class="sxs-lookup"><span data-stu-id="a890c-341">Additional information on signin cards</span></span>

<span data-ttu-id="a890c-342">Ссылка на Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="a890c-342">Bot Framework reference:</span></span>

* [<span data-ttu-id="a890c-343">Карточка signin Node.js</span><span class="sxs-lookup"><span data-stu-id="a890c-343">Signin card Node.js</span></span>](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="a890c-344">Signin card C #</span><span class="sxs-lookup"><span data-stu-id="a890c-344">Signin card C#</span></span>](/dotnet/api/microsoft.bot.schema.signincard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="thumbnail-card"></a><span data-ttu-id="a890c-345">Карта эскиза</span><span class="sxs-lookup"><span data-stu-id="a890c-345">Thumbnail card</span></span>

<span data-ttu-id="a890c-346">Карточка, которая обычно содержит одно изображение эскиза, одну или несколько кнопок и текст.</span><span class="sxs-lookup"><span data-stu-id="a890c-346">A card that typically contains a single thumbnail image, one or more buttons, and text.</span></span>

### <a name="support-for-thumbnail-cards"></a><span data-ttu-id="a890c-347">Поддержка карт эскизов</span><span class="sxs-lookup"><span data-stu-id="a890c-347">Support for thumbnail cards</span></span>

| <span data-ttu-id="a890c-348">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="a890c-348">Bots in Teams</span></span> | <span data-ttu-id="a890c-349">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="a890c-349">Messaging extensions</span></span>  | <span data-ttu-id="a890c-350">Соединители</span><span class="sxs-lookup"><span data-stu-id="a890c-350">Connectors</span></span> | <span data-ttu-id="a890c-351">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="a890c-351">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a890c-352">✔</span><span class="sxs-lookup"><span data-stu-id="a890c-352">✔</span></span> | <span data-ttu-id="a890c-353">✔</span><span class="sxs-lookup"><span data-stu-id="a890c-353">✔</span></span> | <span data-ttu-id="a890c-354">✖</span><span class="sxs-lookup"><span data-stu-id="a890c-354">✖</span></span> | <span data-ttu-id="a890c-355">✔</span><span class="sxs-lookup"><span data-stu-id="a890c-355">✔</span></span> |

![Пример карты эскиза](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a><span data-ttu-id="a890c-357">Свойства карты эскиза</span><span class="sxs-lookup"><span data-stu-id="a890c-357">Properties of a thumbnail card</span></span>

| <span data-ttu-id="a890c-358">Свойство</span><span class="sxs-lookup"><span data-stu-id="a890c-358">Property</span></span> | <span data-ttu-id="a890c-359">Тип</span><span class="sxs-lookup"><span data-stu-id="a890c-359">Type</span></span>  | <span data-ttu-id="a890c-360">Описание</span><span class="sxs-lookup"><span data-stu-id="a890c-360">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a890c-361">title</span><span class="sxs-lookup"><span data-stu-id="a890c-361">title</span></span> | <span data-ttu-id="a890c-362">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="a890c-362">Rich text</span></span> | <span data-ttu-id="a890c-363">Название карты.</span><span class="sxs-lookup"><span data-stu-id="a890c-363">Title of the card.</span></span> <span data-ttu-id="a890c-364">Максимум 2 строки.</span><span class="sxs-lookup"><span data-stu-id="a890c-364">Maximum 2 lines.</span></span>|
| <span data-ttu-id="a890c-365">субтитры</span><span class="sxs-lookup"><span data-stu-id="a890c-365">subtitle</span></span> | <span data-ttu-id="a890c-366">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="a890c-366">Rich text</span></span> | <span data-ttu-id="a890c-367">Субтитр карты.</span><span class="sxs-lookup"><span data-stu-id="a890c-367">Subtitle of the card.</span></span> <span data-ttu-id="a890c-368">Максимум 2 строки.</span><span class="sxs-lookup"><span data-stu-id="a890c-368">Maximum 2 lines.</span></span>|
| <span data-ttu-id="a890c-369">текст</span><span class="sxs-lookup"><span data-stu-id="a890c-369">text</span></span> | <span data-ttu-id="a890c-370">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="a890c-370">Rich text</span></span> | <span data-ttu-id="a890c-371">Текст отображается под субтитром.</span><span class="sxs-lookup"><span data-stu-id="a890c-371">Text appears under the subtitle.</span></span> <span data-ttu-id="a890c-372">Параметры форматирования см. [в виде форматирования карт.](~/task-modules-and-cards/cards/cards-format.md)</span><span class="sxs-lookup"><span data-stu-id="a890c-372">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="a890c-373">изображения</span><span class="sxs-lookup"><span data-stu-id="a890c-373">images</span></span> | <span data-ttu-id="a890c-374">Массив изображений</span><span class="sxs-lookup"><span data-stu-id="a890c-374">Array of images</span></span> | <span data-ttu-id="a890c-375">Изображение, отображаемого в верхней части карты.</span><span class="sxs-lookup"><span data-stu-id="a890c-375">Image displayed at the top of the card.</span></span> <span data-ttu-id="a890c-376">Отношение аспектов 1:1 к квадрату.</span><span class="sxs-lookup"><span data-stu-id="a890c-376">Aspect ratio 1:1 square.</span></span> |
| <span data-ttu-id="a890c-377">кнопки</span><span class="sxs-lookup"><span data-stu-id="a890c-377">buttons</span></span> | <span data-ttu-id="a890c-378">Массив объектов действий</span><span class="sxs-lookup"><span data-stu-id="a890c-378">Array of action objects</span></span> | <span data-ttu-id="a890c-379">Набор действий, применимых к текущей карте.</span><span class="sxs-lookup"><span data-stu-id="a890c-379">Set of actions applicable to the current card.</span></span> <span data-ttu-id="a890c-380">Максимум 6.</span><span class="sxs-lookup"><span data-stu-id="a890c-380">Maximum 6.</span></span> |
| <span data-ttu-id="a890c-381">нажмите кнопку</span><span class="sxs-lookup"><span data-stu-id="a890c-381">tap</span></span> | <span data-ttu-id="a890c-382">Объект Action</span><span class="sxs-lookup"><span data-stu-id="a890c-382">Action object</span></span> | <span data-ttu-id="a890c-383">Активируется при нажатии на карточку самого пользователя.</span><span class="sxs-lookup"><span data-stu-id="a890c-383">Activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-thumbnail-card"></a><span data-ttu-id="a890c-384">Пример карты эскиза</span><span class="sxs-lookup"><span data-stu-id="a890c-384">Example of a thumbnail card</span></span>

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

### <a name="additional-information"></a><span data-ttu-id="a890c-385">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="a890c-385">Additional information</span></span>

<span data-ttu-id="a890c-386">Ссылка на Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="a890c-386">Bot Framework reference:</span></span>

* [<span data-ttu-id="a890c-387">Эскиз карты Node.js</span><span class="sxs-lookup"><span data-stu-id="a890c-387">Thumbnail card Node.js</span></span>](/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="a890c-388">Эскиз карты C #</span><span class="sxs-lookup"><span data-stu-id="a890c-388">Thumbnail card C#</span></span>](/dotnet/api/microsoft.bot.schema.thumbnailcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="card-collections"></a><span data-ttu-id="a890c-389">Коллекции карт</span><span class="sxs-lookup"><span data-stu-id="a890c-389">Card collections</span></span>

<span data-ttu-id="a890c-390">Teams поддерживает коллекции карт.</span><span class="sxs-lookup"><span data-stu-id="a890c-390">Teams supports Card collections.</span></span>

<span data-ttu-id="a890c-391">Коллекции карт включают `builder.AttachmentLayout.carousel` и `builder.AttachmentLayout.list` .</span><span class="sxs-lookup"><span data-stu-id="a890c-391">Card collections include `builder.AttachmentLayout.carousel` and `builder.AttachmentLayout.list`.</span></span> <span data-ttu-id="a890c-392">Эти коллекции содержат адаптивные, герой или эскизные карточки.</span><span class="sxs-lookup"><span data-stu-id="a890c-392">These collections contain adaptive, hero, or thumbnail cards.</span></span>

## <a name="carousel-collection"></a><span data-ttu-id="a890c-393">Коллекция Карусель</span><span class="sxs-lookup"><span data-stu-id="a890c-393">Carousel collection</span></span>

<span data-ttu-id="a890c-394">Макет [карусель показывает](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) карусель карт, необязательно с связанными кнопками действия.</span><span class="sxs-lookup"><span data-stu-id="a890c-394">The [carousel layout](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) shows a carousel of cards, optionally with associated action buttons.</span></span>

### <a name="support-for-carousel-collections"></a><span data-ttu-id="a890c-395">Поддержка коллекций карусель</span><span class="sxs-lookup"><span data-stu-id="a890c-395">Support for carousel collections</span></span>

| <span data-ttu-id="a890c-396">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="a890c-396">Bots in Teams</span></span> | <span data-ttu-id="a890c-397">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="a890c-397">Messaging extensions</span></span>  | <span data-ttu-id="a890c-398">Соединители</span><span class="sxs-lookup"><span data-stu-id="a890c-398">Connectors</span></span> | <span data-ttu-id="a890c-399">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="a890c-399">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a890c-400">✔</span><span class="sxs-lookup"><span data-stu-id="a890c-400">✔</span></span> | <span data-ttu-id="a890c-401">✖</span><span class="sxs-lookup"><span data-stu-id="a890c-401">✖</span></span> | <span data-ttu-id="a890c-402">✖</span><span class="sxs-lookup"><span data-stu-id="a890c-402">✖</span></span> | <span data-ttu-id="a890c-403">✔</span><span class="sxs-lookup"><span data-stu-id="a890c-403">✔</span></span> |

> [!NOTE]
> <span data-ttu-id="a890c-404">Карусель может отображать не более десяти карт на сообщение.</span><span class="sxs-lookup"><span data-stu-id="a890c-404">A carousel can display a maximum of ten cards per message.</span></span>

### <a name="properties-of-a-carousel-card"></a><span data-ttu-id="a890c-405">Свойства карусели</span><span class="sxs-lookup"><span data-stu-id="a890c-405">Properties of a carousel card</span></span>

<span data-ttu-id="a890c-406">Свойства карусельной карты такие же, как и у карт героя и эскизов.</span><span class="sxs-lookup"><span data-stu-id="a890c-406">Properties of a carousel card are same as those of the hero and thumbnail cards.</span></span>

### <a name="example-of-a-carousel-collection"></a><span data-ttu-id="a890c-407">Пример коллекции карусель</span><span class="sxs-lookup"><span data-stu-id="a890c-407">Example of a carousel collection</span></span>

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

### <a name="syntax-for-carousel-collections"></a><span data-ttu-id="a890c-409">Синтаксис для коллекций карусели</span><span class="sxs-lookup"><span data-stu-id="a890c-409">Syntax for carousel collections</span></span>

<span data-ttu-id="a890c-410">`builder.AttachmentLayoutTypes.Carousel` синтаксис для коллекций карусели.</span><span class="sxs-lookup"><span data-stu-id="a890c-410">`builder.AttachmentLayoutTypes.Carousel` is the syntax for carousel collections.</span></span>

## <a name="list-collection"></a><span data-ttu-id="a890c-411">Коллекция списков</span><span class="sxs-lookup"><span data-stu-id="a890c-411">List collection</span></span>

### <a name="support-for-list-collections"></a><span data-ttu-id="a890c-412">Поддержка коллекций списков</span><span class="sxs-lookup"><span data-stu-id="a890c-412">Support for list collections</span></span>

<span data-ttu-id="a890c-413">В макете списка показан вертикально сложенный список карт, необязательно связанный с кнопками действия.</span><span class="sxs-lookup"><span data-stu-id="a890c-413">The list layout shows a vertically stacked list of cards, optionally with associated action buttons.</span></span>

| <span data-ttu-id="a890c-414">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="a890c-414">Bots in Teams</span></span> | <span data-ttu-id="a890c-415">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="a890c-415">Messaging extensions</span></span>  | <span data-ttu-id="a890c-416">Соединители</span><span class="sxs-lookup"><span data-stu-id="a890c-416">Connectors</span></span> | <span data-ttu-id="a890c-417">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="a890c-417">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a890c-418">✔</span><span class="sxs-lookup"><span data-stu-id="a890c-418">✔</span></span> | <span data-ttu-id="a890c-419">✔</span><span class="sxs-lookup"><span data-stu-id="a890c-419">✔</span></span> | <span data-ttu-id="a890c-420">✖</span><span class="sxs-lookup"><span data-stu-id="a890c-420">✖</span></span> | <span data-ttu-id="a890c-421">✔</span><span class="sxs-lookup"><span data-stu-id="a890c-421">✔</span></span> |

### <a name="example-of-a-list-collection"></a><span data-ttu-id="a890c-422">Пример коллекции списков</span><span class="sxs-lookup"><span data-stu-id="a890c-422">Example of a list collection</span></span>

![Пример списка карт](~/assets/images/cards/list.png)

<span data-ttu-id="a890c-424">Свойства такие же, как для карты героя или эскиза.</span><span class="sxs-lookup"><span data-stu-id="a890c-424">Properties are the same as for the hero or thumbnail card.</span></span>

<span data-ttu-id="a890c-425">В списке может отображаться не более десяти карт на сообщение.</span><span class="sxs-lookup"><span data-stu-id="a890c-425">A list can display a maximum of ten cards per message.</span></span>

> [!NOTE]
> <span data-ttu-id="a890c-426">Некоторые сочетания карт списка еще не поддерживаются на iOS и Android.</span><span class="sxs-lookup"><span data-stu-id="a890c-426">Some combinations of list cards are not yet supported on iOS and Android.</span></span>

### <a name="syntax-for-list-collections"></a><span data-ttu-id="a890c-427">Синтаксис для коллекций списков</span><span class="sxs-lookup"><span data-stu-id="a890c-427">Syntax for list collections</span></span>

<span data-ttu-id="a890c-428">`builder.AttachmentLayout.list` синтаксис для коллекций списков.</span><span class="sxs-lookup"><span data-stu-id="a890c-428">`builder.AttachmentLayout.list` is the syntax for list collections.</span></span>

## <a name="cards-not-supported-in-teams"></a><span data-ttu-id="a890c-429">Карты, не поддерживаемые в Teams</span><span class="sxs-lookup"><span data-stu-id="a890c-429">Cards not supported in Teams</span></span>

<span data-ttu-id="a890c-430">Следующие карты реализуются в рамках Bot Framework, но не поддерживаются Teams:</span><span class="sxs-lookup"><span data-stu-id="a890c-430">The following cards are implemented by the Bot Framework, but are not supported by Teams:</span></span>

* <span data-ttu-id="a890c-431">Карты анимации</span><span class="sxs-lookup"><span data-stu-id="a890c-431">Animation cards</span></span>
* <span data-ttu-id="a890c-432">Аудиокарты</span><span class="sxs-lookup"><span data-stu-id="a890c-432">Audio cards</span></span>
* <span data-ttu-id="a890c-433">Видеокарты</span><span class="sxs-lookup"><span data-stu-id="a890c-433">Video cards</span></span>
