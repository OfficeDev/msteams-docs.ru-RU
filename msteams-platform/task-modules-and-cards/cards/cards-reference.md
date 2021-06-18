---
title: Ссылки на карточки
description: Описывает все действия карт и карт, доступные ботам в Teams
localization_priority: Normal
keywords: ссылка на карточки ботов
ms.topic: reference
ms.openlocfilehash: 741980ea79dd23659dd2b8a240d767b8292ca251
ms.sourcegitcommit: 14409950307b135265c8582408be5277b35131dd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/17/2021
ms.locfileid: "52994387"
---
# <a name="cards-reference"></a><span data-ttu-id="c3076-104">Ссылки на карточки</span><span class="sxs-lookup"><span data-stu-id="c3076-104">Cards reference</span></span>

<span data-ttu-id="c3076-105">Карты, перечисленные в этом документе, поддерживаются в ботах для Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="c3076-105">The cards listed in this document are supported in bots for Microsoft Teams.</span></span> <span data-ttu-id="c3076-106">Они основаны на картах, определенных bot Framework (BF), но Teams не поддерживает все карты Bot Framework и вместо этого были добавлены некоторые Teams карты.</span><span class="sxs-lookup"><span data-stu-id="c3076-106">They are based on cards defined by the Bot Framework (BF), but Teams does not support all Bot Framework cards and instead some Teams cards have been added.</span></span> <span data-ttu-id="c3076-107">Различия называются в ссылках в этом документе.</span><span class="sxs-lookup"><span data-stu-id="c3076-107">Differences are called out in the references in this document.</span></span>

## <a name="card-examples"></a><span data-ttu-id="c3076-108">Примеры карт</span><span class="sxs-lookup"><span data-stu-id="c3076-108">Card examples</span></span>

<span data-ttu-id="c3076-109">Дополнительные сведения об использовании карт можно найти в документации для bot Builder SDK v3.</span><span class="sxs-lookup"><span data-stu-id="c3076-109">You can find additional information on how to use cards in the documentation for the Bot Builder SDK v3.</span></span> <span data-ttu-id="c3076-110">Примеры кода также доступны в репозитории Microsoft/BotBuilder-Samples на GitHub.</span><span class="sxs-lookup"><span data-stu-id="c3076-110">Code samples are also available in the Microsoft/BotBuilder-Samples repository on GitHub.</span></span>

* <span data-ttu-id="c3076-111">.NET</span><span class="sxs-lookup"><span data-stu-id="c3076-111">.NET</span></span>
  * <span data-ttu-id="c3076-112">[Добавление карт в виде вложений в сообщения.](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="c3076-112">[Add cards as attachments to messages](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true).</span></span>
  * <span data-ttu-id="c3076-113">[Карты пример кода Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards).</span><span class="sxs-lookup"><span data-stu-id="c3076-113">[Cards sample code Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards).</span></span>

* <span data-ttu-id="c3076-114">Node.js</span><span class="sxs-lookup"><span data-stu-id="c3076-114">Node.js</span></span>
  * <span data-ttu-id="c3076-115">[Добавление карт в виде вложений в сообщения.](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="c3076-115">[Add cards as attachments to messages](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true).</span></span>
  * <span data-ttu-id="c3076-116">[Карты пример кода Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards).</span><span class="sxs-lookup"><span data-stu-id="c3076-116">[Cards sample code Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards).</span></span>

## <a name="types-of-cards"></a><span data-ttu-id="c3076-117">Типы карт</span><span class="sxs-lookup"><span data-stu-id="c3076-117">Types of cards</span></span>

<span data-ttu-id="c3076-118">В этой таблице показаны типы доступных вам карт:</span><span class="sxs-lookup"><span data-stu-id="c3076-118">This table shows the types of cards available to you:</span></span>

| <span data-ttu-id="c3076-119">Тип карты</span><span class="sxs-lookup"><span data-stu-id="c3076-119">Card type</span></span> | <span data-ttu-id="c3076-120">Описание</span><span class="sxs-lookup"><span data-stu-id="c3076-120">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="c3076-121">Адаптивная карта</span><span class="sxs-lookup"><span data-stu-id="c3076-121">Adaptive card</span></span>](#adaptive-card) | <span data-ttu-id="c3076-122">Эта карта является высоко настраиваемой картой, которая может содержать любое сочетание текстов, речи, изображений, кнопок и полей ввода.</span><span class="sxs-lookup"><span data-stu-id="c3076-122">This card is highly customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> |
| [<span data-ttu-id="c3076-123">Карта hero</span><span class="sxs-lookup"><span data-stu-id="c3076-123">Hero card</span></span>](#hero-card) | <span data-ttu-id="c3076-124">Эта карта обычно содержит одно большое изображение, одну или несколько кнопок и небольшое количество текста.</span><span class="sxs-lookup"><span data-stu-id="c3076-124">This card typically contains a single large image, one or more buttons, and a small amount of text.</span></span> |
| [<span data-ttu-id="c3076-125">Карта списка</span><span class="sxs-lookup"><span data-stu-id="c3076-125">List card</span></span>](#list-card) | <span data-ttu-id="c3076-126">Эта карта — это список элементов прокрутки.</span><span class="sxs-lookup"><span data-stu-id="c3076-126">This card is a scrolling list of items.</span></span> |
| [<span data-ttu-id="c3076-127">Office 365 соединители</span><span class="sxs-lookup"><span data-stu-id="c3076-127">Office 365 connector card</span></span>](#office-365-connector-card) | <span data-ttu-id="c3076-128">Эта карта имеет гибкий макет с несколькими разделами, полями, изображениями и действиями.</span><span class="sxs-lookup"><span data-stu-id="c3076-128">This card has a flexible layout with multiple sections, fields, images, and actions.</span></span> |
| [<span data-ttu-id="c3076-129">Карта получения</span><span class="sxs-lookup"><span data-stu-id="c3076-129">Receipt card</span></span>](#receipt-card) | <span data-ttu-id="c3076-130">Эта карта предоставляет квитанцию пользователю.</span><span class="sxs-lookup"><span data-stu-id="c3076-130">This card provides a receipt to the user.</span></span> |
| [<span data-ttu-id="c3076-131">Карточка Signin</span><span class="sxs-lookup"><span data-stu-id="c3076-131">Signin card</span></span>](#signin-card) | <span data-ttu-id="c3076-132">Эта карта позволяет боту запрашивать, чтобы пользователь войди.</span><span class="sxs-lookup"><span data-stu-id="c3076-132">This card enables a bot to request that a user signs in.</span></span> |
| [<span data-ttu-id="c3076-133">Карта эскиза</span><span class="sxs-lookup"><span data-stu-id="c3076-133">Thumbnail card</span></span>](#thumbnail-card) | <span data-ttu-id="c3076-134">Эта карта обычно содержит одно изображение эскиза, короткий текст и одну или несколько кнопок.</span><span class="sxs-lookup"><span data-stu-id="c3076-134">This card typically contains a single thumbnail image, some short text, and one or more buttons.</span></span> |
| [<span data-ttu-id="c3076-135">Коллекции карт</span><span class="sxs-lookup"><span data-stu-id="c3076-135">Card collections</span></span>](#card-collections) | <span data-ttu-id="c3076-136">Эти карты используются для возврата нескольких элементов в одном ответе.</span><span class="sxs-lookup"><span data-stu-id="c3076-136">This cards is used to return multiple items in a single response.</span></span> |

## <a name="common-properties-for-all-cards"></a><span data-ttu-id="c3076-137">Общие свойства для всех карт</span><span class="sxs-lookup"><span data-stu-id="c3076-137">Common properties for all cards</span></span>

### <a name="inline-card-images"></a><span data-ttu-id="c3076-138">Inline card images</span><span class="sxs-lookup"><span data-stu-id="c3076-138">Inline card images</span></span>

<span data-ttu-id="c3076-139">Карта может содержать рядное изображение, включив ссылку на общедоступный образ.</span><span class="sxs-lookup"><span data-stu-id="c3076-139">The card can contain an inline image by including a link to the publicly available image.</span></span> <span data-ttu-id="c3076-140">В целях производительности рекомендуется использовать изображение в общедоступных сетях доставки контента (CDN).</span><span class="sxs-lookup"><span data-stu-id="c3076-140">For performance purposes, it is highly recommended you host the image on a public content-delivery network (CDN).</span></span>

<span data-ttu-id="c3076-141">Изображения масштабироваться или по размеру при сохранении соотношения аспектов для покрытия области изображения.</span><span class="sxs-lookup"><span data-stu-id="c3076-141">Images are scaled up or down in size while maintaining the aspect ratio to cover the image area.</span></span> <span data-ttu-id="c3076-142">Затем изображения обрезаются из центра, чтобы достичь соответствующего соотношения аспектов для карты.</span><span class="sxs-lookup"><span data-stu-id="c3076-142">Images are then cropped from center to achieve the appropriate aspect ratio for the card.</span></span>

<span data-ttu-id="c3076-143">Изображения должны быть не более 1024×1024 в формате PNG, JPEG или GIF и не поддерживают анимированный GIF.</span><span class="sxs-lookup"><span data-stu-id="c3076-143">Images must be at most 1024×1024, in PNG, JPEG, or GIF format, and do not support animated GIF.</span></span>

| <span data-ttu-id="c3076-144">Свойство</span><span class="sxs-lookup"><span data-stu-id="c3076-144">Property</span></span> | <span data-ttu-id="c3076-145">Тип</span><span class="sxs-lookup"><span data-stu-id="c3076-145">Type</span></span>  | <span data-ttu-id="c3076-146">Описание</span><span class="sxs-lookup"><span data-stu-id="c3076-146">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c3076-147">url</span><span class="sxs-lookup"><span data-stu-id="c3076-147">url</span></span> | <span data-ttu-id="c3076-148">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="c3076-148">URL</span></span> | <span data-ttu-id="c3076-149">URL-адрес HTTPS к изображению.</span><span class="sxs-lookup"><span data-stu-id="c3076-149">HTTPS URL to the image.</span></span> |
| <span data-ttu-id="c3076-150">alt</span><span class="sxs-lookup"><span data-stu-id="c3076-150">alt</span></span> | <span data-ttu-id="c3076-151">String</span><span class="sxs-lookup"><span data-stu-id="c3076-151">String</span></span> | <span data-ttu-id="c3076-152">Доступное описание изображения.</span><span class="sxs-lookup"><span data-stu-id="c3076-152">Accessible description of the image.</span></span> |

> [!NOTE]
> <span data-ttu-id="c3076-153">Если карта содержит URL-адрес изображения, который проходит перенаправление перед окончательным изображением, перенаправление в URL-адрес изображения не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="c3076-153">If a card includes an image URL that goes through a redirect before the final image, the redirect in image URL is not supported.</span></span> <span data-ttu-id="c3076-154">Это происходит для изображений, общих в общедоступных облаках.</span><span class="sxs-lookup"><span data-stu-id="c3076-154">This occurs for images shared on the public cloud.</span></span>

### <a name="buttons"></a><span data-ttu-id="c3076-155">Кнопки</span><span class="sxs-lookup"><span data-stu-id="c3076-155">Buttons</span></span>

<span data-ttu-id="c3076-156">Кнопки показаны в нижней части карты.</span><span class="sxs-lookup"><span data-stu-id="c3076-156">Buttons are shown stacked at the bottom of the card.</span></span> <span data-ttu-id="c3076-157">Текст кнопки всегда находится в одной строке и усечен, если текст превышает ширину кнопки.</span><span class="sxs-lookup"><span data-stu-id="c3076-157">Button text is always on a single line and is truncated if the text exceeds the button width.</span></span> <span data-ttu-id="c3076-158">Никаких дополнительных кнопок, помимо максимального числа, поддерживаемого картой, не отображается.</span><span class="sxs-lookup"><span data-stu-id="c3076-158">Any additional buttons beyond the maximum number supported by the card are not shown.</span></span>

<span data-ttu-id="c3076-159">Дополнительные сведения см. в [карточных действиях.](~/task-modules-and-cards/cards/cards-actions.md)</span><span class="sxs-lookup"><span data-stu-id="c3076-159">For more information, see [card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

### <a name="card-formatting"></a><span data-ttu-id="c3076-160">Форматирование карт</span><span class="sxs-lookup"><span data-stu-id="c3076-160">Card formatting</span></span>

<span data-ttu-id="c3076-161">Дополнительные сведения о форматирования текста в картах см. [в документе форматирование карт.](~/task-modules-and-cards/cards/cards-format.md)</span><span class="sxs-lookup"><span data-stu-id="c3076-161">For more information on text formatting in cards, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span>

## <a name="adaptive-card"></a><span data-ttu-id="c3076-162">Адаптивная карта</span><span class="sxs-lookup"><span data-stu-id="c3076-162">Adaptive card</span></span>

<span data-ttu-id="c3076-163">Адаптивная карта — это настраиваемая карта, которая может содержать любое сочетание текстовых, речевого, изображений, кнопок и полей ввода.</span><span class="sxs-lookup"><span data-stu-id="c3076-163">An adaptive card is a customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> <span data-ttu-id="c3076-164">Дополнительные сведения см. в [рублях адаптивных карт v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span><span class="sxs-lookup"><span data-stu-id="c3076-164">For more information, see [adaptive cards v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span></span>

### <a name="support-for-adaptive-cards"></a><span data-ttu-id="c3076-165">Поддержка адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="c3076-165">Support for adaptive cards</span></span>

| <span data-ttu-id="c3076-166">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="c3076-166">Bots in Teams</span></span> | <span data-ttu-id="c3076-167">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="c3076-167">Messaging extensions</span></span>  | <span data-ttu-id="c3076-168">Соединители</span><span class="sxs-lookup"><span data-stu-id="c3076-168">Connectors</span></span> | <span data-ttu-id="c3076-169">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="c3076-169">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c3076-170">✔</span><span class="sxs-lookup"><span data-stu-id="c3076-170">✔</span></span> | <span data-ttu-id="c3076-171">✔</span><span class="sxs-lookup"><span data-stu-id="c3076-171">✔</span></span> | <span data-ttu-id="c3076-172">✖</span><span class="sxs-lookup"><span data-stu-id="c3076-172">✖</span></span> | <span data-ttu-id="c3076-173">✔</span><span class="sxs-lookup"><span data-stu-id="c3076-173">✔</span></span> |

> [!NOTE]
> * <span data-ttu-id="c3076-174">Teams поддерживает v1.2 или более ранние функции адаптивной карты.</span><span class="sxs-lookup"><span data-stu-id="c3076-174">Teams platform supports v1.2 or earlier of adaptive card features.</span></span>
> * <span data-ttu-id="c3076-175">Положительный или разрушительный стиль действий не поддерживается в адаптивных картах на Teams платформе.</span><span class="sxs-lookup"><span data-stu-id="c3076-175">Positive or destructive action styling is not supported in Adaptive Cards on the Teams platform.</span></span>
> * <span data-ttu-id="c3076-176">Элементы мультимедиа в настоящее время не поддерживаются в адаптивных картах на Teams платформе.</span><span class="sxs-lookup"><span data-stu-id="c3076-176">Media elements are currently not supported in Adaptive Cards on the Teams platform.</span></span>

### <a name="example-of-an-adaptive-card"></a><span data-ttu-id="c3076-177">Пример адаптивной карты</span><span class="sxs-lookup"><span data-stu-id="c3076-177">Example of an adaptive card</span></span>

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

#### <a name="additional-information-on-adaptive-cards"></a><span data-ttu-id="c3076-179">Дополнительные сведения о адаптивных картах</span><span class="sxs-lookup"><span data-stu-id="c3076-179">Additional information on adaptive cards</span></span>

<span data-ttu-id="c3076-180">Ссылка на Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="c3076-180">Bot Framework reference:</span></span>

* [<span data-ttu-id="c3076-181">Адаптивные Node.js</span><span class="sxs-lookup"><span data-stu-id="c3076-181">Adaptive cards Node.js</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)
* [<span data-ttu-id="c3076-182">Адаптивная карта C #</span><span class="sxs-lookup"><span data-stu-id="c3076-182">Adaptive card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)

## <a name="hero-card"></a><span data-ttu-id="c3076-183">Карта hero</span><span class="sxs-lookup"><span data-stu-id="c3076-183">Hero card</span></span>

<span data-ttu-id="c3076-184">Карта, которая обычно содержит одно большое изображение, одну или несколько кнопок и текст.</span><span class="sxs-lookup"><span data-stu-id="c3076-184">A card that typically contains a single large image, one or more buttons, and text.</span></span>

### <a name="support-for-hero-cards"></a><span data-ttu-id="c3076-185">Поддержка карт-героев</span><span class="sxs-lookup"><span data-stu-id="c3076-185">Support for hero cards</span></span>

| <span data-ttu-id="c3076-186">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="c3076-186">Bots in Teams</span></span> | <span data-ttu-id="c3076-187">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="c3076-187">Messaging extensions</span></span>  | <span data-ttu-id="c3076-188">Соединители</span><span class="sxs-lookup"><span data-stu-id="c3076-188">Connectors</span></span> | <span data-ttu-id="c3076-189">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="c3076-189">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c3076-190">✔</span><span class="sxs-lookup"><span data-stu-id="c3076-190">✔</span></span> | <span data-ttu-id="c3076-191">✔</span><span class="sxs-lookup"><span data-stu-id="c3076-191">✔</span></span> | <span data-ttu-id="c3076-192">✖</span><span class="sxs-lookup"><span data-stu-id="c3076-192">✖</span></span> | <span data-ttu-id="c3076-193">✔</span><span class="sxs-lookup"><span data-stu-id="c3076-193">✔</span></span> |

### <a name="properties-of-a-hero-card"></a><span data-ttu-id="c3076-194">Свойства карты-героя</span><span class="sxs-lookup"><span data-stu-id="c3076-194">Properties of a hero card</span></span>

| <span data-ttu-id="c3076-195">Свойство</span><span class="sxs-lookup"><span data-stu-id="c3076-195">Property</span></span> | <span data-ttu-id="c3076-196">Тип</span><span class="sxs-lookup"><span data-stu-id="c3076-196">Type</span></span>  | <span data-ttu-id="c3076-197">Описание</span><span class="sxs-lookup"><span data-stu-id="c3076-197">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c3076-198">title</span><span class="sxs-lookup"><span data-stu-id="c3076-198">title</span></span> | <span data-ttu-id="c3076-199">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="c3076-199">Rich text</span></span> | <span data-ttu-id="c3076-200">Название карты.</span><span class="sxs-lookup"><span data-stu-id="c3076-200">Title of the card.</span></span> <span data-ttu-id="c3076-201">Максимум 2 строки.</span><span class="sxs-lookup"><span data-stu-id="c3076-201">Maximum 2 lines.</span></span> |
| <span data-ttu-id="c3076-202">субтитры</span><span class="sxs-lookup"><span data-stu-id="c3076-202">subtitle</span></span> | <span data-ttu-id="c3076-203">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="c3076-203">Rich text</span></span> | <span data-ttu-id="c3076-204">Субтитр карты.</span><span class="sxs-lookup"><span data-stu-id="c3076-204">Subtitle of the card.</span></span> <span data-ttu-id="c3076-205">Максимум 2 строки.</span><span class="sxs-lookup"><span data-stu-id="c3076-205">Maximum 2 lines.</span></span>|
| <span data-ttu-id="c3076-206">текст</span><span class="sxs-lookup"><span data-stu-id="c3076-206">text</span></span> | <span data-ttu-id="c3076-207">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="c3076-207">Rich text</span></span> | <span data-ttu-id="c3076-208">Текст отображается под субтитром.</span><span class="sxs-lookup"><span data-stu-id="c3076-208">Text appears under the subtitle.</span></span> <span data-ttu-id="c3076-209">Параметры форматирования см. [в виде форматирования карт.](~/task-modules-and-cards/cards/cards-format.md)</span><span class="sxs-lookup"><span data-stu-id="c3076-209">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="c3076-210">изображения</span><span class="sxs-lookup"><span data-stu-id="c3076-210">images</span></span> | <span data-ttu-id="c3076-211">Массив изображений</span><span class="sxs-lookup"><span data-stu-id="c3076-211">Array of images</span></span> | <span data-ttu-id="c3076-212">Изображение, отображаемого в верхней части карты.</span><span class="sxs-lookup"><span data-stu-id="c3076-212">Image displayed at the top of the card.</span></span> <span data-ttu-id="c3076-213">Соотношение аспектов 16:9.</span><span class="sxs-lookup"><span data-stu-id="c3076-213">Aspect ratio 16:9.</span></span> |
| <span data-ttu-id="c3076-214">кнопки</span><span class="sxs-lookup"><span data-stu-id="c3076-214">buttons</span></span> | <span data-ttu-id="c3076-215">Массив объектов действий</span><span class="sxs-lookup"><span data-stu-id="c3076-215">Array of action objects</span></span> | <span data-ttu-id="c3076-216">Набор действий, применимых к текущей карте.</span><span class="sxs-lookup"><span data-stu-id="c3076-216">Set of actions applicable to the current card.</span></span> <span data-ttu-id="c3076-217">Максимум 6.</span><span class="sxs-lookup"><span data-stu-id="c3076-217">Maximum 6.</span></span> |
| <span data-ttu-id="c3076-218">нажмите кнопку</span><span class="sxs-lookup"><span data-stu-id="c3076-218">tap</span></span> | <span data-ttu-id="c3076-219">Объект Action</span><span class="sxs-lookup"><span data-stu-id="c3076-219">Action object</span></span> | <span data-ttu-id="c3076-220">Активируется при нажатии на карточку самого пользователя.</span><span class="sxs-lookup"><span data-stu-id="c3076-220">Activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-hero-card"></a><span data-ttu-id="c3076-221">Пример карточки героя</span><span class="sxs-lookup"><span data-stu-id="c3076-221">Example of a hero card</span></span>

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

### <a name="additional-information-on-hero-cards"></a><span data-ttu-id="c3076-223">Дополнительные сведения о картах-героях</span><span class="sxs-lookup"><span data-stu-id="c3076-223">Additional information on hero cards</span></span>

<span data-ttu-id="c3076-224">Ссылка на Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="c3076-224">Bot Framework reference:</span></span>

* [<span data-ttu-id="c3076-225">Карточка героя Node.js</span><span class="sxs-lookup"><span data-stu-id="c3076-225">Hero card Node.js</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-a-hero-card&preserve-view=true)
* [<span data-ttu-id="c3076-226">Карта героя C #</span><span class="sxs-lookup"><span data-stu-id="c3076-226">Hero card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-hero-card&preserve-view=true)

## <a name="list-card"></a><span data-ttu-id="c3076-227">Карта списка</span><span class="sxs-lookup"><span data-stu-id="c3076-227">List card</span></span>

<span data-ttu-id="c3076-228">Карта списка была добавлена Teams для предоставления функций, которые не могут предоставляться в коллекции списков.</span><span class="sxs-lookup"><span data-stu-id="c3076-228">The list card has been added by Teams to provide functions beyond what the list collection can provide.</span></span> <span data-ttu-id="c3076-229">Карта списка содержит список элементов для прокрутки.</span><span class="sxs-lookup"><span data-stu-id="c3076-229">The list card provides a scrolling list of items.</span></span>

### <a name="support-for-list-cards"></a><span data-ttu-id="c3076-230">Поддержка карт списка</span><span class="sxs-lookup"><span data-stu-id="c3076-230">Support for list cards</span></span>

| <span data-ttu-id="c3076-231">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="c3076-231">Bots in Teams</span></span> | <span data-ttu-id="c3076-232">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="c3076-232">Messaging extensions</span></span>  | <span data-ttu-id="c3076-233">Соединители</span><span class="sxs-lookup"><span data-stu-id="c3076-233">Connectors</span></span> | <span data-ttu-id="c3076-234">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="c3076-234">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c3076-235">✔</span><span class="sxs-lookup"><span data-stu-id="c3076-235">✔</span></span> | <span data-ttu-id="c3076-236">✖</span><span class="sxs-lookup"><span data-stu-id="c3076-236">✖</span></span> | <span data-ttu-id="c3076-237">✖</span><span class="sxs-lookup"><span data-stu-id="c3076-237">✖</span></span> |<span data-ttu-id="c3076-238">✔</span><span class="sxs-lookup"><span data-stu-id="c3076-238">✔</span></span> |

### <a name="properties-of-a-list-card"></a><span data-ttu-id="c3076-239">Свойства карты списка</span><span class="sxs-lookup"><span data-stu-id="c3076-239">Properties of a list card</span></span>

| <span data-ttu-id="c3076-240">Свойство</span><span class="sxs-lookup"><span data-stu-id="c3076-240">Property</span></span> | <span data-ttu-id="c3076-241">Тип</span><span class="sxs-lookup"><span data-stu-id="c3076-241">Type</span></span>  | <span data-ttu-id="c3076-242">Описание</span><span class="sxs-lookup"><span data-stu-id="c3076-242">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c3076-243">title</span><span class="sxs-lookup"><span data-stu-id="c3076-243">title</span></span> | <span data-ttu-id="c3076-244">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="c3076-244">Rich text</span></span> | <span data-ttu-id="c3076-245">Название карты.</span><span class="sxs-lookup"><span data-stu-id="c3076-245">Title of the card.</span></span> <span data-ttu-id="c3076-246">Максимум 2 строки.</span><span class="sxs-lookup"><span data-stu-id="c3076-246">Maximum 2 lines.</span></span>|
| <span data-ttu-id="c3076-247">элементы</span><span class="sxs-lookup"><span data-stu-id="c3076-247">items</span></span> | <span data-ttu-id="c3076-248">Массив элементов списка</span><span class="sxs-lookup"><span data-stu-id="c3076-248">Array of list items</span></span> ||
| <span data-ttu-id="c3076-249">кнопки</span><span class="sxs-lookup"><span data-stu-id="c3076-249">buttons</span></span> | <span data-ttu-id="c3076-250">Массив объектов действий</span><span class="sxs-lookup"><span data-stu-id="c3076-250">Array of action objects</span></span> | <span data-ttu-id="c3076-251">Набор действий, применимых к текущей карте.</span><span class="sxs-lookup"><span data-stu-id="c3076-251">Set of actions applicable to the current card.</span></span> <span data-ttu-id="c3076-252">Максимум 6.</span><span class="sxs-lookup"><span data-stu-id="c3076-252">Maximum 6.</span></span> |

### <a name="example-of-a-list-card"></a><span data-ttu-id="c3076-253">Пример карты списка</span><span class="sxs-lookup"><span data-stu-id="c3076-253">Example of a list card</span></span>

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

## <a name="office-365-connector-card"></a><span data-ttu-id="c3076-254">Office 365 соединители</span><span class="sxs-lookup"><span data-stu-id="c3076-254">Office 365 connector card</span></span>

<span data-ttu-id="c3076-255">Соедините Office 365 поддерживается в Teams, а не в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="c3076-255">The Office 365 connector card is supported in Teams, not in Bot Framework.</span></span> <span data-ttu-id="c3076-256">Эта карта обеспечивает гибкую схему с несколькими разделами, полями, изображениями и действиями.</span><span class="sxs-lookup"><span data-stu-id="c3076-256">This card provides a flexible layout with multiple sections, fields, images, and actions.</span></span> <span data-ttu-id="c3076-257">Эта карта инкапсулирует соединителем карту, чтобы она была использована ботами.</span><span class="sxs-lookup"><span data-stu-id="c3076-257">This card encapsulates a connector card so that it can be used by bots.</span></span> <span data-ttu-id="c3076-258">О различиях между соединитеными картами и картой O365 см. в заметках на [Office 365 соединители.](#notes-on-the-office-365-connector-card)</span><span class="sxs-lookup"><span data-stu-id="c3076-258">For differences between connector cards and the O365 card, see [Notes on the Office 365 connector card](#notes-on-the-office-365-connector-card).</span></span>

### <a name="support-for-office-365-connector-cards"></a><span data-ttu-id="c3076-259">Поддержка Office 365 соединители</span><span class="sxs-lookup"><span data-stu-id="c3076-259">Support for Office 365 connector cards</span></span>

| <span data-ttu-id="c3076-260">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="c3076-260">Bots in Teams</span></span> | <span data-ttu-id="c3076-261">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="c3076-261">Messaging extensions</span></span>  | <span data-ttu-id="c3076-262">Соединители</span><span class="sxs-lookup"><span data-stu-id="c3076-262">Connectors</span></span> | <span data-ttu-id="c3076-263">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="c3076-263">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c3076-264">✔</span><span class="sxs-lookup"><span data-stu-id="c3076-264">✔</span></span> | <span data-ttu-id="c3076-265">✔</span><span class="sxs-lookup"><span data-stu-id="c3076-265">✔</span></span> | <span data-ttu-id="c3076-266">✔</span><span class="sxs-lookup"><span data-stu-id="c3076-266">✔</span></span> | <span data-ttu-id="c3076-267">✖</span><span class="sxs-lookup"><span data-stu-id="c3076-267">✖</span></span> |

### <a name="properties-of-the-office-365-connector-card"></a><span data-ttu-id="c3076-268">Свойства карты Office 365 соединители</span><span class="sxs-lookup"><span data-stu-id="c3076-268">Properties of the Office 365 connector card</span></span>

| <span data-ttu-id="c3076-269">Свойство</span><span class="sxs-lookup"><span data-stu-id="c3076-269">Property</span></span> | <span data-ttu-id="c3076-270">Тип</span><span class="sxs-lookup"><span data-stu-id="c3076-270">Type</span></span>  | <span data-ttu-id="c3076-271">Описание</span><span class="sxs-lookup"><span data-stu-id="c3076-271">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c3076-272">title</span><span class="sxs-lookup"><span data-stu-id="c3076-272">title</span></span> | <span data-ttu-id="c3076-273">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="c3076-273">Rich text</span></span> | <span data-ttu-id="c3076-274">Название карты.</span><span class="sxs-lookup"><span data-stu-id="c3076-274">Title of the card.</span></span> <span data-ttu-id="c3076-275">Максимум 2 строки.</span><span class="sxs-lookup"><span data-stu-id="c3076-275">Maximum 2 lines.</span></span> |
| <span data-ttu-id="c3076-276">summary</span><span class="sxs-lookup"><span data-stu-id="c3076-276">summary</span></span> | <span data-ttu-id="c3076-277">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="c3076-277">Rich text</span></span> | <span data-ttu-id="c3076-278">Сводка карты.</span><span class="sxs-lookup"><span data-stu-id="c3076-278">Summary of the card.</span></span> <span data-ttu-id="c3076-279">Максимум 2 строки.</span><span class="sxs-lookup"><span data-stu-id="c3076-279">Maximum 2 lines.</span></span> |
| <span data-ttu-id="c3076-280">текст</span><span class="sxs-lookup"><span data-stu-id="c3076-280">text</span></span> | <span data-ttu-id="c3076-281">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="c3076-281">Rich text</span></span> | <span data-ttu-id="c3076-282">Текст отображается под субтитром.</span><span class="sxs-lookup"><span data-stu-id="c3076-282">Text appears under the subtitle.</span></span> <span data-ttu-id="c3076-283">Параметры форматирования см. [в виде форматирования карт.](~/task-modules-and-cards/cards/cards-format.md)</span><span class="sxs-lookup"><span data-stu-id="c3076-283">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="c3076-284">themeColor</span><span class="sxs-lookup"><span data-stu-id="c3076-284">themeColor</span></span> | <span data-ttu-id="c3076-285">Строка HEX</span><span class="sxs-lookup"><span data-stu-id="c3076-285">HEX string</span></span> | <span data-ttu-id="c3076-286">Цвет, который переопределяет accentColor, предоставленный из манифеста приложения.</span><span class="sxs-lookup"><span data-stu-id="c3076-286">Color that overrides the accentColor provided from the application manifest.</span></span> |

### <a name="notes-on-the-office-365-connector-card"></a><span data-ttu-id="c3076-287">Заметки на Office 365 соединители</span><span class="sxs-lookup"><span data-stu-id="c3076-287">Notes on the Office 365 connector card</span></span>

<span data-ttu-id="c3076-288">Office 365 соединители карточки работают правильно в Microsoft Teams, включая [действия ActionCard](/outlook/actionable-messages/card-reference#actioncard-action).</span><span class="sxs-lookup"><span data-stu-id="c3076-288">Office 365 connector cards function properly in Microsoft Teams, including [ActionCard actions](/outlook/actionable-messages/card-reference#actioncard-action).</span></span>

<span data-ttu-id="c3076-289">Одним из важных отличий между использованием соединитеных карт из соединитетеля и использованием соединитеных карт в боте является обработка действий карт.</span><span class="sxs-lookup"><span data-stu-id="c3076-289">One important difference between using connector cards from a connector and using connector cards in your bot is the handling of card actions.</span></span>

* <span data-ttu-id="c3076-290">Для соединитетеля конечная точка получает полезное сообщение карточки через HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="c3076-290">For a connector, the endpoint receives the card payload through HTTP POST.</span></span>
* <span data-ttu-id="c3076-291">Для бота действие запускает действие, которое отправляет боту только ID действия и `HttpPOST` `invoke` тело.</span><span class="sxs-lookup"><span data-stu-id="c3076-291">For a bot, the `HttpPOST` action triggers an `invoke` activity that sends only the action ID and body to the bot.</span></span>

<span data-ttu-id="c3076-292">Каждая соединитечная карта может отображать не более десяти разделов, а каждый раздел может содержать не более пяти изображений и пять действий.</span><span class="sxs-lookup"><span data-stu-id="c3076-292">Each connector card can display a maximum of ten sections, and each section can contain a maximum of five images and five actions.</span></span>

> [!NOTE]
> <span data-ttu-id="c3076-293">Дополнительные разделы, изображения или действия в сообщении не отображаются.</span><span class="sxs-lookup"><span data-stu-id="c3076-293">Any additional sections, images, or actions in a message do not appear.</span></span>

<span data-ttu-id="c3076-294">Все текстовые поля поддерживают разметку и HTML.</span><span class="sxs-lookup"><span data-stu-id="c3076-294">All text fields support markdown and HTML.</span></span> <span data-ttu-id="c3076-295">Вы можете контролировать, в каких разделах используется разметка или HTML, установив `markdown` свойство в сообщении.</span><span class="sxs-lookup"><span data-stu-id="c3076-295">You can control which sections use markdown or HTML by setting the `markdown` property in a message.</span></span> <span data-ttu-id="c3076-296">По умолчанию `markdown` установлено `true` значение .</span><span class="sxs-lookup"><span data-stu-id="c3076-296">By default, `markdown` is set to `true`.</span></span> <span data-ttu-id="c3076-297">Если вы хотите использовать HTML вместо этого, установите `markdown` `false` .</span><span class="sxs-lookup"><span data-stu-id="c3076-297">If you want to use HTML instead, set `markdown` to `false`.</span></span>

<span data-ttu-id="c3076-298">Если указать `themeColor` свойство, оно переопределит `accentColor` свойство в манифесте приложения.</span><span class="sxs-lookup"><span data-stu-id="c3076-298">If you specify the `themeColor` property, it overrides the `accentColor` property in the app manifest.</span></span>

<span data-ttu-id="c3076-299">Чтобы указать стиль `activityImage` визуализации, можно задать `activityImageType` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c3076-299">To specify the rendering style for `activityImage`, you can set `activityImageType` as follows:</span></span>

| <span data-ttu-id="c3076-300">Значение</span><span class="sxs-lookup"><span data-stu-id="c3076-300">Value</span></span> | <span data-ttu-id="c3076-301">Описание</span><span class="sxs-lookup"><span data-stu-id="c3076-301">Description</span></span> |
| --- | --- |
| `avatar` | <span data-ttu-id="c3076-302">По умолчанию; `activityImage` обрезается как круг.</span><span class="sxs-lookup"><span data-stu-id="c3076-302">Default; `activityImage` is cropped as a circle.</span></span> |
| `article` | <span data-ttu-id="c3076-303">`activityImage` отображается в качестве прямоугольника и сохраняет отношение аспектов.</span><span class="sxs-lookup"><span data-stu-id="c3076-303">`activityImage` is displayed as a rectangle and retains its aspect ratio.</span></span> |

<span data-ttu-id="c3076-304">Другие сведения о свойствах карт соединители см. в справке к карточкам [сообщений.](/outlook/actionable-messages/card-reference)</span><span class="sxs-lookup"><span data-stu-id="c3076-304">For all other details about connector card properties, see [actionable message card reference](/outlook/actionable-messages/card-reference).</span></span> <span data-ttu-id="c3076-305">Единственными свойствами карт соединители, Microsoft Teams которые в настоящее время не поддерживаются, являются следующими:</span><span class="sxs-lookup"><span data-stu-id="c3076-305">The only connector card properties that Microsoft Teams does not currently support are as follows:</span></span>

* `heroImage`
* `hideOriginalBody`
* <span data-ttu-id="c3076-306">`startGroup`всегда рассматривается как `true` в Teams</span><span class="sxs-lookup"><span data-stu-id="c3076-306">`startGroup` always treated as `true` in Teams</span></span>
* `originator`
* `correlationId`

### <a name="example-of-an-office-365-connector-card"></a><span data-ttu-id="c3076-307">Пример карты Office 365 соединители</span><span class="sxs-lookup"><span data-stu-id="c3076-307">Example of an Office 365 connector card</span></span>

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

## <a name="receipt-card"></a><span data-ttu-id="c3076-308">Карта получения</span><span class="sxs-lookup"><span data-stu-id="c3076-308">Receipt card</span></span>

<span data-ttu-id="c3076-309">Teams поддерживает карточку получения.</span><span class="sxs-lookup"><span data-stu-id="c3076-309">Teams supports receipt card.</span></span> <span data-ttu-id="c3076-310">Это карточка, которая позволяет боту предоставлять пользователю квитанцию.</span><span class="sxs-lookup"><span data-stu-id="c3076-310">It is a card that enables a bot to provide a receipt to the user.</span></span> <span data-ttu-id="c3076-311">Обычно он содержит список элементов, которые необходимо включить в квитанцию, например налоговые и общие сведения.</span><span class="sxs-lookup"><span data-stu-id="c3076-311">It typically contains the list of items to include on the receipt, such as tax and total information.</span></span>

### <a name="support-for-receipt-cards"></a><span data-ttu-id="c3076-312">Поддержка карт получения</span><span class="sxs-lookup"><span data-stu-id="c3076-312">Support for receipt cards</span></span>

| <span data-ttu-id="c3076-313">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="c3076-313">Bots in Teams</span></span> | <span data-ttu-id="c3076-314">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="c3076-314">Messaging extensions</span></span>  | <span data-ttu-id="c3076-315">Соединители</span><span class="sxs-lookup"><span data-stu-id="c3076-315">Connectors</span></span> | <span data-ttu-id="c3076-316">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="c3076-316">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c3076-317">✔</span><span class="sxs-lookup"><span data-stu-id="c3076-317">✔</span></span> | <span data-ttu-id="c3076-318">✔</span><span class="sxs-lookup"><span data-stu-id="c3076-318">✔</span></span> | <span data-ttu-id="c3076-319">✖</span><span class="sxs-lookup"><span data-stu-id="c3076-319">✖</span></span> | <span data-ttu-id="c3076-320">✔</span><span class="sxs-lookup"><span data-stu-id="c3076-320">✔</span></span> |

### <a name="example-of-a-receipt-card"></a><span data-ttu-id="c3076-321">Пример карты получения</span><span class="sxs-lookup"><span data-stu-id="c3076-321">Example of a receipt card</span></span>

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

### <a name="additional-information-on-receipt-cards"></a><span data-ttu-id="c3076-323">Дополнительные сведения о карточках получения</span><span class="sxs-lookup"><span data-stu-id="c3076-323">Additional information on receipt cards</span></span>

<span data-ttu-id="c3076-324">Ссылка на Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="c3076-324">Bot Framework reference:</span></span>

* [<span data-ttu-id="c3076-325">Карточка получения Node.js</span><span class="sxs-lookup"><span data-stu-id="c3076-325">Receipt card Node.js</span></span>](/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="c3076-326">Карта получения C #</span><span class="sxs-lookup"><span data-stu-id="c3076-326">Receipt card C#</span></span>](/dotnet/api/microsoft.bot.schema.receiptcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="signin-card"></a><span data-ttu-id="c3076-327">Карточка Signin</span><span class="sxs-lookup"><span data-stu-id="c3076-327">Signin card</span></span>

<span data-ttu-id="c3076-328">Карта Signin позволяет боту запрашивать вход пользователя.</span><span class="sxs-lookup"><span data-stu-id="c3076-328">Signin card enables a bot to request a user to sign in.</span></span> <span data-ttu-id="c3076-329">Поддерживается в Teams в несколько иной форме, чем в bot Framework.</span><span class="sxs-lookup"><span data-stu-id="c3076-329">It is supported in Teams in a slightly different form than is found in the Bot Framework.</span></span> <span data-ttu-id="c3076-330">Карта signin в Teams похожа на карточку signin в bot Framework, за исключением того, что карточка signin в Teams поддерживает только два действия: `signin` и `openUrl` .</span><span class="sxs-lookup"><span data-stu-id="c3076-330">The signin card in Teams is similar to the signin card in the Bot Framework except that the signin card in Teams only supports two actions: `signin` and `openUrl`.</span></span>

<span data-ttu-id="c3076-331">Действие signin можно использовать с любой карты в Teams, а не только с карты signin.</span><span class="sxs-lookup"><span data-stu-id="c3076-331">The signin action can be used from any card in Teams, not just the signin card.</span></span> <span data-ttu-id="c3076-332">Дополнительные сведения о проверке подлинности см. в Microsoft Teams поток проверки [подлинности для ботов.](~/bots/how-to/authentication/auth-flow-bot.md)</span><span class="sxs-lookup"><span data-stu-id="c3076-332">For more information on authentication, see [Microsoft Teams authentication flow for bots](~/bots/how-to/authentication/auth-flow-bot.md).</span></span>

### <a name="support-for-signin-cards"></a><span data-ttu-id="c3076-333">Поддержка подписных карт</span><span class="sxs-lookup"><span data-stu-id="c3076-333">Support for signin cards</span></span>

| <span data-ttu-id="c3076-334">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="c3076-334">Bots in Teams</span></span> | <span data-ttu-id="c3076-335">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="c3076-335">Messaging extensions</span></span>  | <span data-ttu-id="c3076-336">Соединители</span><span class="sxs-lookup"><span data-stu-id="c3076-336">Connectors</span></span> | <span data-ttu-id="c3076-337">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="c3076-337">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c3076-338">✔</span><span class="sxs-lookup"><span data-stu-id="c3076-338">✔</span></span> | <span data-ttu-id="c3076-339">✖</span><span class="sxs-lookup"><span data-stu-id="c3076-339">✖</span></span> | <span data-ttu-id="c3076-340">✖</span><span class="sxs-lookup"><span data-stu-id="c3076-340">✖</span></span> | <span data-ttu-id="c3076-341">✔</span><span class="sxs-lookup"><span data-stu-id="c3076-341">✔</span></span> |

### <a name="additional-information-on-signin-cards"></a><span data-ttu-id="c3076-342">Дополнительные сведения о подписных карточках</span><span class="sxs-lookup"><span data-stu-id="c3076-342">Additional information on signin cards</span></span>

<span data-ttu-id="c3076-343">Ссылка на Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="c3076-343">Bot Framework reference:</span></span>

* [<span data-ttu-id="c3076-344">Карточка signin Node.js</span><span class="sxs-lookup"><span data-stu-id="c3076-344">Signin card Node.js</span></span>](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="c3076-345">Signin card C #</span><span class="sxs-lookup"><span data-stu-id="c3076-345">Signin card C#</span></span>](/dotnet/api/microsoft.bot.schema.signincard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="thumbnail-card"></a><span data-ttu-id="c3076-346">Карта эскиза</span><span class="sxs-lookup"><span data-stu-id="c3076-346">Thumbnail card</span></span>

<span data-ttu-id="c3076-347">Карточка, которая обычно содержит одно изображение эскиза, одну или несколько кнопок и текст.</span><span class="sxs-lookup"><span data-stu-id="c3076-347">A card that typically contains a single thumbnail image, one or more buttons, and text.</span></span>

### <a name="support-for-thumbnail-cards"></a><span data-ttu-id="c3076-348">Поддержка карт эскизов</span><span class="sxs-lookup"><span data-stu-id="c3076-348">Support for thumbnail cards</span></span>

| <span data-ttu-id="c3076-349">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="c3076-349">Bots in Teams</span></span> | <span data-ttu-id="c3076-350">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="c3076-350">Messaging extensions</span></span>  | <span data-ttu-id="c3076-351">Соединители</span><span class="sxs-lookup"><span data-stu-id="c3076-351">Connectors</span></span> | <span data-ttu-id="c3076-352">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="c3076-352">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c3076-353">✔</span><span class="sxs-lookup"><span data-stu-id="c3076-353">✔</span></span> | <span data-ttu-id="c3076-354">✔</span><span class="sxs-lookup"><span data-stu-id="c3076-354">✔</span></span> | <span data-ttu-id="c3076-355">✖</span><span class="sxs-lookup"><span data-stu-id="c3076-355">✖</span></span> | <span data-ttu-id="c3076-356">✔</span><span class="sxs-lookup"><span data-stu-id="c3076-356">✔</span></span> |

![Пример карты эскиза](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a><span data-ttu-id="c3076-358">Свойства карты эскиза</span><span class="sxs-lookup"><span data-stu-id="c3076-358">Properties of a thumbnail card</span></span>

| <span data-ttu-id="c3076-359">Свойство</span><span class="sxs-lookup"><span data-stu-id="c3076-359">Property</span></span> | <span data-ttu-id="c3076-360">Тип</span><span class="sxs-lookup"><span data-stu-id="c3076-360">Type</span></span>  | <span data-ttu-id="c3076-361">Описание</span><span class="sxs-lookup"><span data-stu-id="c3076-361">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c3076-362">title</span><span class="sxs-lookup"><span data-stu-id="c3076-362">title</span></span> | <span data-ttu-id="c3076-363">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="c3076-363">Rich text</span></span> | <span data-ttu-id="c3076-364">Название карты.</span><span class="sxs-lookup"><span data-stu-id="c3076-364">Title of the card.</span></span> <span data-ttu-id="c3076-365">Максимум 2 строки.</span><span class="sxs-lookup"><span data-stu-id="c3076-365">Maximum 2 lines.</span></span>|
| <span data-ttu-id="c3076-366">субтитры</span><span class="sxs-lookup"><span data-stu-id="c3076-366">subtitle</span></span> | <span data-ttu-id="c3076-367">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="c3076-367">Rich text</span></span> | <span data-ttu-id="c3076-368">Субтитр карты.</span><span class="sxs-lookup"><span data-stu-id="c3076-368">Subtitle of the card.</span></span> <span data-ttu-id="c3076-369">Максимум 2 строки.</span><span class="sxs-lookup"><span data-stu-id="c3076-369">Maximum 2 lines.</span></span>|
| <span data-ttu-id="c3076-370">текст</span><span class="sxs-lookup"><span data-stu-id="c3076-370">text</span></span> | <span data-ttu-id="c3076-371">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="c3076-371">Rich text</span></span> | <span data-ttu-id="c3076-372">Текст отображается под субтитром.</span><span class="sxs-lookup"><span data-stu-id="c3076-372">Text appears under the subtitle.</span></span> <span data-ttu-id="c3076-373">Параметры форматирования см. [в виде форматирования карт.](~/task-modules-and-cards/cards/cards-format.md)</span><span class="sxs-lookup"><span data-stu-id="c3076-373">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="c3076-374">изображения</span><span class="sxs-lookup"><span data-stu-id="c3076-374">images</span></span> | <span data-ttu-id="c3076-375">Массив изображений</span><span class="sxs-lookup"><span data-stu-id="c3076-375">Array of images</span></span> | <span data-ttu-id="c3076-376">Изображение, отображаемого в верхней части карты.</span><span class="sxs-lookup"><span data-stu-id="c3076-376">Image displayed at the top of the card.</span></span> <span data-ttu-id="c3076-377">Отношение аспектов 1:1 к квадрату.</span><span class="sxs-lookup"><span data-stu-id="c3076-377">Aspect ratio 1:1 square.</span></span> |
| <span data-ttu-id="c3076-378">кнопки</span><span class="sxs-lookup"><span data-stu-id="c3076-378">buttons</span></span> | <span data-ttu-id="c3076-379">Массив объектов действий</span><span class="sxs-lookup"><span data-stu-id="c3076-379">Array of action objects</span></span> | <span data-ttu-id="c3076-380">Набор действий, применимых к текущей карте.</span><span class="sxs-lookup"><span data-stu-id="c3076-380">Set of actions applicable to the current card.</span></span> <span data-ttu-id="c3076-381">Максимум 6.</span><span class="sxs-lookup"><span data-stu-id="c3076-381">Maximum 6.</span></span> |
| <span data-ttu-id="c3076-382">нажмите кнопку</span><span class="sxs-lookup"><span data-stu-id="c3076-382">tap</span></span> | <span data-ttu-id="c3076-383">Объект Action</span><span class="sxs-lookup"><span data-stu-id="c3076-383">Action object</span></span> | <span data-ttu-id="c3076-384">Активируется при нажатии на карточку самого пользователя.</span><span class="sxs-lookup"><span data-stu-id="c3076-384">Activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-thumbnail-card"></a><span data-ttu-id="c3076-385">Пример карты эскиза</span><span class="sxs-lookup"><span data-stu-id="c3076-385">Example of a thumbnail card</span></span>

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

### <a name="additional-information"></a><span data-ttu-id="c3076-386">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="c3076-386">Additional information</span></span>

<span data-ttu-id="c3076-387">Ссылка на Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="c3076-387">Bot Framework reference:</span></span>

* [<span data-ttu-id="c3076-388">Эскиз карты Node.js</span><span class="sxs-lookup"><span data-stu-id="c3076-388">Thumbnail card Node.js</span></span>](/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="c3076-389">Эскиз карты C #</span><span class="sxs-lookup"><span data-stu-id="c3076-389">Thumbnail card C#</span></span>](/dotnet/api/microsoft.bot.schema.thumbnailcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="card-collections"></a><span data-ttu-id="c3076-390">Коллекции карт</span><span class="sxs-lookup"><span data-stu-id="c3076-390">Card collections</span></span>

<span data-ttu-id="c3076-391">Teams поддерживает коллекции карт.</span><span class="sxs-lookup"><span data-stu-id="c3076-391">Teams supports Card collections.</span></span>

<span data-ttu-id="c3076-392">Коллекции карт включают `builder.AttachmentLayout.carousel` и `builder.AttachmentLayout.list` .</span><span class="sxs-lookup"><span data-stu-id="c3076-392">Card collections include `builder.AttachmentLayout.carousel` and `builder.AttachmentLayout.list`.</span></span> <span data-ttu-id="c3076-393">Эти коллекции содержат адаптивные, герой или эскизные карточки.</span><span class="sxs-lookup"><span data-stu-id="c3076-393">These collections contain adaptive, hero, or thumbnail cards.</span></span>

## <a name="carousel-collection"></a><span data-ttu-id="c3076-394">Коллекция Карусель</span><span class="sxs-lookup"><span data-stu-id="c3076-394">Carousel collection</span></span>

<span data-ttu-id="c3076-395">Макет [карусель показывает](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) карусель карт, необязательно с связанными кнопками действия.</span><span class="sxs-lookup"><span data-stu-id="c3076-395">The [carousel layout](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) shows a carousel of cards, optionally with associated action buttons.</span></span>

### <a name="support-for-carousel-collections"></a><span data-ttu-id="c3076-396">Поддержка коллекций карусель</span><span class="sxs-lookup"><span data-stu-id="c3076-396">Support for carousel collections</span></span>

| <span data-ttu-id="c3076-397">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="c3076-397">Bots in Teams</span></span> | <span data-ttu-id="c3076-398">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="c3076-398">Messaging extensions</span></span>  | <span data-ttu-id="c3076-399">Соединители</span><span class="sxs-lookup"><span data-stu-id="c3076-399">Connectors</span></span> | <span data-ttu-id="c3076-400">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="c3076-400">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c3076-401">✔</span><span class="sxs-lookup"><span data-stu-id="c3076-401">✔</span></span> | <span data-ttu-id="c3076-402">✖</span><span class="sxs-lookup"><span data-stu-id="c3076-402">✖</span></span> | <span data-ttu-id="c3076-403">✖</span><span class="sxs-lookup"><span data-stu-id="c3076-403">✖</span></span> | <span data-ttu-id="c3076-404">✔</span><span class="sxs-lookup"><span data-stu-id="c3076-404">✔</span></span> |

> [!NOTE]
> <span data-ttu-id="c3076-405">Карусель может отображать не более десяти карт на сообщение.</span><span class="sxs-lookup"><span data-stu-id="c3076-405">A carousel can display a maximum of ten cards per message.</span></span>

### <a name="properties-of-a-carousel-card"></a><span data-ttu-id="c3076-406">Свойства карусели</span><span class="sxs-lookup"><span data-stu-id="c3076-406">Properties of a carousel card</span></span>

<span data-ttu-id="c3076-407">Свойства карусельной карты такие же, как и у карт героя и эскизов.</span><span class="sxs-lookup"><span data-stu-id="c3076-407">Properties of a carousel card are same as those of the hero and thumbnail cards.</span></span>

### <a name="example-of-a-carousel-collection"></a><span data-ttu-id="c3076-408">Пример коллекции карусель</span><span class="sxs-lookup"><span data-stu-id="c3076-408">Example of a carousel collection</span></span>

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

### <a name="syntax-for-carousel-collections"></a><span data-ttu-id="c3076-410">Синтаксис для коллекций карусели</span><span class="sxs-lookup"><span data-stu-id="c3076-410">Syntax for carousel collections</span></span>

<span data-ttu-id="c3076-411">`builder.AttachmentLayoutTypes.Carousel` синтаксис для коллекций карусели.</span><span class="sxs-lookup"><span data-stu-id="c3076-411">`builder.AttachmentLayoutTypes.Carousel` is the syntax for carousel collections.</span></span>

## <a name="list-collection"></a><span data-ttu-id="c3076-412">Коллекция списков</span><span class="sxs-lookup"><span data-stu-id="c3076-412">List collection</span></span>

### <a name="support-for-list-collections"></a><span data-ttu-id="c3076-413">Поддержка коллекций списков</span><span class="sxs-lookup"><span data-stu-id="c3076-413">Support for list collections</span></span>

<span data-ttu-id="c3076-414">В макете списка показан вертикально сложенный список карт, необязательно связанный с кнопками действия.</span><span class="sxs-lookup"><span data-stu-id="c3076-414">The list layout shows a vertically stacked list of cards, optionally with associated action buttons.</span></span>

| <span data-ttu-id="c3076-415">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="c3076-415">Bots in Teams</span></span> | <span data-ttu-id="c3076-416">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="c3076-416">Messaging extensions</span></span>  | <span data-ttu-id="c3076-417">Соединители</span><span class="sxs-lookup"><span data-stu-id="c3076-417">Connectors</span></span> | <span data-ttu-id="c3076-418">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="c3076-418">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c3076-419">✔</span><span class="sxs-lookup"><span data-stu-id="c3076-419">✔</span></span> | <span data-ttu-id="c3076-420">✔</span><span class="sxs-lookup"><span data-stu-id="c3076-420">✔</span></span> | <span data-ttu-id="c3076-421">✖</span><span class="sxs-lookup"><span data-stu-id="c3076-421">✖</span></span> | <span data-ttu-id="c3076-422">✔</span><span class="sxs-lookup"><span data-stu-id="c3076-422">✔</span></span> |

### <a name="example-of-a-list-collection"></a><span data-ttu-id="c3076-423">Пример коллекции списков</span><span class="sxs-lookup"><span data-stu-id="c3076-423">Example of a list collection</span></span>

![Пример списка карт](~/assets/images/cards/list.png)

<span data-ttu-id="c3076-425">Свойства такие же, как для карты героя или эскиза.</span><span class="sxs-lookup"><span data-stu-id="c3076-425">Properties are the same as for the hero or thumbnail card.</span></span>

<span data-ttu-id="c3076-426">В списке может отображаться не более десяти карт на сообщение.</span><span class="sxs-lookup"><span data-stu-id="c3076-426">A list can display a maximum of ten cards per message.</span></span>

> [!NOTE]
> <span data-ttu-id="c3076-427">Некоторые сочетания карт списка еще не поддерживаются на iOS и Android.</span><span class="sxs-lookup"><span data-stu-id="c3076-427">Some combinations of list cards are not yet supported on iOS and Android.</span></span>

### <a name="syntax-for-list-collections"></a><span data-ttu-id="c3076-428">Синтаксис для коллекций списков</span><span class="sxs-lookup"><span data-stu-id="c3076-428">Syntax for list collections</span></span>

<span data-ttu-id="c3076-429">`builder.AttachmentLayout.list` синтаксис для коллекций списков.</span><span class="sxs-lookup"><span data-stu-id="c3076-429">`builder.AttachmentLayout.list` is the syntax for list collections.</span></span>

## <a name="cards-not-supported-in-teams"></a><span data-ttu-id="c3076-430">Карты, не поддерживаемые в Teams</span><span class="sxs-lookup"><span data-stu-id="c3076-430">Cards not supported in Teams</span></span>

<span data-ttu-id="c3076-431">Следующие карты реализуются в рамках Bot Framework, но не поддерживаются Teams:</span><span class="sxs-lookup"><span data-stu-id="c3076-431">The following cards are implemented by the Bot Framework, but are not supported by Teams:</span></span>

* <span data-ttu-id="c3076-432">Карты анимации</span><span class="sxs-lookup"><span data-stu-id="c3076-432">Animation cards</span></span>
* <span data-ttu-id="c3076-433">Аудиокарты</span><span class="sxs-lookup"><span data-stu-id="c3076-433">Audio cards</span></span>
* <span data-ttu-id="c3076-434">Видеокарты</span><span class="sxs-lookup"><span data-stu-id="c3076-434">Video cards</span></span>
