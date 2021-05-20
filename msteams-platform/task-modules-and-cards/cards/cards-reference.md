---
title: Ссылки на карточки
description: Описывает все карты и действия карты, доступные для ботов в Teams
localization_priority: Normal
keywords: Боты карты ссылки
ms.topic: reference
ms.openlocfilehash: cab7f1659759f40beb1aba59531ee6c1a84662c1
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566861"
---
# <a name="cards-reference"></a><span data-ttu-id="0c6fd-104">Ссылки на карточки</span><span class="sxs-lookup"><span data-stu-id="0c6fd-104">Cards reference</span></span>

<span data-ttu-id="0c6fd-105">Карты, перечисленные в этом документе, поддерживаются в ботах в течение Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-105">The cards listed in this document are supported in bots for Microsoft Teams.</span></span> <span data-ttu-id="0c6fd-106">Они основаны на картах, определенных Bot Framework, но Teams не поддерживает все карты Bot Framework, и вместо этого Teams карты были добавлены.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-106">They are based on cards defined by the Bot Framework, but Teams does not support all Bot Framework cards and instead some Teams cards have been added.</span></span> <span data-ttu-id="0c6fd-107">Различия называются в ссылках в этом документе.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-107">Differences are called out in the references in this document.</span></span>

## <a name="card-examples"></a><span data-ttu-id="0c6fd-108">Примеры карт</span><span class="sxs-lookup"><span data-stu-id="0c6fd-108">Card examples</span></span>

<span data-ttu-id="0c6fd-109">Дополнительную информацию о том, как использовать карты, можно найти в документации для Bot Builder SDK v3.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-109">You can find additional information on how to use cards in the documentation for the Bot Builder SDK v3.</span></span> <span data-ttu-id="0c6fd-110">Образцы кода также доступны в репозитории Microsoft/BotBuilder-Samples на GitHub.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-110">Code samples are also available in the Microsoft/BotBuilder-Samples repository on GitHub.</span></span>

* <span data-ttu-id="0c6fd-111">.NET</span><span class="sxs-lookup"><span data-stu-id="0c6fd-111">.NET</span></span>
  * <span data-ttu-id="0c6fd-112">[Добавить карты в качестве вложений в сообщения.](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="0c6fd-112">[Add cards as attachments to messages](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true).</span></span>
  * <span data-ttu-id="0c6fd-113">[Карты образец кода Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards).</span><span class="sxs-lookup"><span data-stu-id="0c6fd-113">[Cards sample code Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards).</span></span>

* <span data-ttu-id="0c6fd-114">Node.js</span><span class="sxs-lookup"><span data-stu-id="0c6fd-114">Node.js</span></span>
  * <span data-ttu-id="0c6fd-115">[Добавить карты в качестве вложений в сообщения.](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="0c6fd-115">[Add cards as attachments to messages](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true).</span></span>
  * <span data-ttu-id="0c6fd-116">[Карты образец кода Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards).</span><span class="sxs-lookup"><span data-stu-id="0c6fd-116">[Cards sample code Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards).</span></span>

## <a name="types-of-cards"></a><span data-ttu-id="0c6fd-117">Типы карт</span><span class="sxs-lookup"><span data-stu-id="0c6fd-117">Types of cards</span></span>

<span data-ttu-id="0c6fd-118">В этой таблице показаны доступные вам типы карт:</span><span class="sxs-lookup"><span data-stu-id="0c6fd-118">This table shows the types of cards available to you:</span></span>

| <span data-ttu-id="0c6fd-119">Тип карты</span><span class="sxs-lookup"><span data-stu-id="0c6fd-119">Card type</span></span> | <span data-ttu-id="0c6fd-120">Описание</span><span class="sxs-lookup"><span data-stu-id="0c6fd-120">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="0c6fd-121">Адаптивная карта</span><span class="sxs-lookup"><span data-stu-id="0c6fd-121">Adaptive card</span></span>](#adaptive-card) | <span data-ttu-id="0c6fd-122">Эта карта является очень настраиваемой картой, которая может содержать любую комбинацию текстовых, речеспособных, изображений, кнопок и входных полей.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-122">This card is highly customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> |
| [<span data-ttu-id="0c6fd-123">Карта героя</span><span class="sxs-lookup"><span data-stu-id="0c6fd-123">Hero card</span></span>](#hero-card) | <span data-ttu-id="0c6fd-124">Эта карта обычно содержит одно большое изображение, одну или несколько кнопок и небольшое количество текста.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-124">This card typically contains a single large image, one or more buttons, and a small amount of text.</span></span> |
| [<span data-ttu-id="0c6fd-125">Карта списка</span><span class="sxs-lookup"><span data-stu-id="0c6fd-125">List card</span></span>](#list-card) | <span data-ttu-id="0c6fd-126">Эта карта является прокруткой списка элементов.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-126">This card is a scrolling list of items.</span></span> |
| [<span data-ttu-id="0c6fd-127">Office 365-карта</span><span class="sxs-lookup"><span data-stu-id="0c6fd-127">Office 365 connector card</span></span>](#office-365-connector-card) | <span data-ttu-id="0c6fd-128">Эта карта имеет гибкую компоновку с несколькими разделами, полями, изображениями и действиями.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-128">This card has a flexible layout with multiple sections, fields, images, and actions.</span></span> |
| [<span data-ttu-id="0c6fd-129">Квитанция карты</span><span class="sxs-lookup"><span data-stu-id="0c6fd-129">Receipt card</span></span>](#receipt-card) | <span data-ttu-id="0c6fd-130">Эта карта предоставляет квитанцию пользователю.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-130">This card provides a receipt to the user.</span></span> |
| [<span data-ttu-id="0c6fd-131">Карта Сигнина</span><span class="sxs-lookup"><span data-stu-id="0c6fd-131">Signin card</span></span>](#signin-card) | <span data-ttu-id="0c6fd-132">Эта карта позволяет боту запрашивать, чтобы пользователь влиться.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-132">This card enables a bot to request that a user signs in.</span></span> |
| [<span data-ttu-id="0c6fd-133">Thumbnail карты</span><span class="sxs-lookup"><span data-stu-id="0c6fd-133">Thumbnail card</span></span>](#thumbnail-card) | <span data-ttu-id="0c6fd-134">Эта карта обычно содержит одно изображение эскиза, короткий текст и одну или несколько кнопок.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-134">This card typically contains a single thumbnail image, some short text, and one or more buttons.</span></span> |
| [<span data-ttu-id="0c6fd-135">Коллекции карт</span><span class="sxs-lookup"><span data-stu-id="0c6fd-135">Card collections</span></span>](#card-collections) | <span data-ttu-id="0c6fd-136">Эта карточка используется для возврата нескольких элементов в одном ответе.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-136">This cards is used to return multiple items in a single response.</span></span> |

## <a name="common-properties-for-all-cards"></a><span data-ttu-id="0c6fd-137">Общие свойства для всех карт</span><span class="sxs-lookup"><span data-stu-id="0c6fd-137">Common properties for all cards</span></span>

### <a name="inline-card-images"></a><span data-ttu-id="0c6fd-138">Изображения стационарных карт</span><span class="sxs-lookup"><span data-stu-id="0c6fd-138">Inline card images</span></span>

<span data-ttu-id="0c6fd-139">Карта может содержать рядное изображение, включив ссылку на общедоступное изображение.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-139">The card can contain an inline image by including a link to the publicly available image.</span></span> <span data-ttu-id="0c6fd-140">Для целей производительности настоятельно рекомендуется разместить изображение в общедоступной сети доставки контента (CDN).</span><span class="sxs-lookup"><span data-stu-id="0c6fd-140">For performance purposes, it is highly recommended you host the image on a public content-delivery network (CDN).</span></span>

<span data-ttu-id="0c6fd-141">Изображения масштабируются или уменьшены в размерах при сохранении соотношения сторон для покрытия области изображения.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-141">Images are scaled up or down in size while maintaining the aspect ratio to cover the image area.</span></span> <span data-ttu-id="0c6fd-142">Изображения затем обрезаются из центра для достижения соответствующего соотношения сторон для карты.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-142">Images are then cropped from center to achieve the appropriate aspect ratio for the card.</span></span>

<span data-ttu-id="0c6fd-143">Изображения должны быть не более 1024×1024, в формате PNG, JPEG или GIF, и не поддерживать анимированный GIF.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-143">Images must be at most 1024×1024, in PNG, JPEG, or GIF format, and do not support animated GIF.</span></span>

| <span data-ttu-id="0c6fd-144">Свойство</span><span class="sxs-lookup"><span data-stu-id="0c6fd-144">Property</span></span> | <span data-ttu-id="0c6fd-145">Тип</span><span class="sxs-lookup"><span data-stu-id="0c6fd-145">Type</span></span>  | <span data-ttu-id="0c6fd-146">Описание</span><span class="sxs-lookup"><span data-stu-id="0c6fd-146">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0c6fd-147">url</span><span class="sxs-lookup"><span data-stu-id="0c6fd-147">url</span></span> | <span data-ttu-id="0c6fd-148">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="0c6fd-148">URL</span></span> | <span data-ttu-id="0c6fd-149">URL-адрес HTTPS на изображение.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-149">HTTPS URL to the image.</span></span> |
| <span data-ttu-id="0c6fd-150">alt</span><span class="sxs-lookup"><span data-stu-id="0c6fd-150">alt</span></span> | <span data-ttu-id="0c6fd-151">String</span><span class="sxs-lookup"><span data-stu-id="0c6fd-151">String</span></span> | <span data-ttu-id="0c6fd-152">Доступное описание изображения.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-152">Accessible description of the image.</span></span> |

> [!NOTE]
> <span data-ttu-id="0c6fd-153">Если карта включает URL-адрес изображения, который проходит через перенаправление перед окончательным изображением, перенаправление URL-адреса изображения не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-153">If a card includes an image URL that goes through a redirect before the final image, the redirect in image URL is not supported.</span></span> <span data-ttu-id="0c6fd-154">Это происходит для изображений, еханых в общедоступных облаках.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-154">This occurs for images shared on the public cloud.</span></span>

### <a name="buttons"></a><span data-ttu-id="0c6fd-155">Кнопки</span><span class="sxs-lookup"><span data-stu-id="0c6fd-155">Buttons</span></span>

<span data-ttu-id="0c6fd-156">Кнопки отображаются уложенными в нижней части карты.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-156">Buttons are shown stacked at the bottom of the card.</span></span> <span data-ttu-id="0c6fd-157">Текст кнопки всегда находится на одной строке и усечен, если текст превышает ширину кнопки.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-157">Button text is always on a single line and is truncated if the text exceeds the button width.</span></span> <span data-ttu-id="0c6fd-158">Дополнительные кнопки, выходящие за рамки максимального числа, поддерживаемого картой, не отображаются.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-158">Any additional buttons beyond the maximum number supported by the card are not shown.</span></span>

<span data-ttu-id="0c6fd-159">Для получения дополнительной информации, [смотрите действия карты](~/task-modules-and-cards/cards/cards-actions.md).</span><span class="sxs-lookup"><span data-stu-id="0c6fd-159">For more information, see [card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

### <a name="card-formatting"></a><span data-ttu-id="0c6fd-160">Форматирование карт</span><span class="sxs-lookup"><span data-stu-id="0c6fd-160">Card formatting</span></span>

<span data-ttu-id="0c6fd-161">Для получения дополнительной информации о форматировании текста в картах, [см.](~/task-modules-and-cards/cards/cards-format.md)</span><span class="sxs-lookup"><span data-stu-id="0c6fd-161">For more information on text formatting in cards, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span>

## <a name="adaptive-card"></a><span data-ttu-id="0c6fd-162">Адаптивная карта</span><span class="sxs-lookup"><span data-stu-id="0c6fd-162">Adaptive card</span></span>

<span data-ttu-id="0c6fd-163">Адаптивная карта представляет собой настраиваемую карту, которая может содержать любую комбинацию текстовых, речеспособных, изображений, кнопок и полей ввода.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-163">An adaptive card is a customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> <span data-ttu-id="0c6fd-164">Для получения дополнительной информации [см.](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0)</span><span class="sxs-lookup"><span data-stu-id="0c6fd-164">For more information, see [adaptive cards v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span></span>

### <a name="support-for-adaptive-cards"></a><span data-ttu-id="0c6fd-165">Поддержка адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="0c6fd-165">Support for adaptive cards</span></span>

| <span data-ttu-id="0c6fd-166">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="0c6fd-166">Bots in Teams</span></span> | <span data-ttu-id="0c6fd-167">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="0c6fd-167">Messaging extensions</span></span>  | <span data-ttu-id="0c6fd-168">Соединители</span><span class="sxs-lookup"><span data-stu-id="0c6fd-168">Connectors</span></span> | <span data-ttu-id="0c6fd-169">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="0c6fd-169">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0c6fd-170">✔</span><span class="sxs-lookup"><span data-stu-id="0c6fd-170">✔</span></span> | <span data-ttu-id="0c6fd-171">✔</span><span class="sxs-lookup"><span data-stu-id="0c6fd-171">✔</span></span> | <span data-ttu-id="0c6fd-172">✖</span><span class="sxs-lookup"><span data-stu-id="0c6fd-172">✖</span></span> | <span data-ttu-id="0c6fd-173">✔</span><span class="sxs-lookup"><span data-stu-id="0c6fd-173">✔</span></span> |

> [!NOTE]
> * <span data-ttu-id="0c6fd-174">Teams поддерживает v1.2 или более ранние функции адаптивной карты.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-174">Teams platform supports v1.2 or earlier of adaptive card features.</span></span>
> * <span data-ttu-id="0c6fd-175">Медиа-элементы в настоящее время не поддерживаются в адаптивной карте v1.2 Teams платформы.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-175">Media elements are currently not supported in adaptive card v1.2 on the Teams platform.</span></span>

### <a name="example-of-an-adaptive-card"></a><span data-ttu-id="0c6fd-176">Пример адаптивной карты</span><span class="sxs-lookup"><span data-stu-id="0c6fd-176">Example of an adaptive card</span></span>

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

#### <a name="additional-information-on-adaptive-cards"></a><span data-ttu-id="0c6fd-178">Дополнительная информация об адаптивных картах</span><span class="sxs-lookup"><span data-stu-id="0c6fd-178">Additional information on adaptive cards</span></span>

<span data-ttu-id="0c6fd-179">Ссылка на Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="0c6fd-179">Bot Framework reference:</span></span>

* [<span data-ttu-id="0c6fd-180">Адаптивные карты Node.js</span><span class="sxs-lookup"><span data-stu-id="0c6fd-180">Adaptive cards Node.js</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)
* [<span data-ttu-id="0c6fd-181">Адаптивная карта C #</span><span class="sxs-lookup"><span data-stu-id="0c6fd-181">Adaptive card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)

## <a name="hero-card"></a><span data-ttu-id="0c6fd-182">Карта героя</span><span class="sxs-lookup"><span data-stu-id="0c6fd-182">Hero card</span></span>

<span data-ttu-id="0c6fd-183">Карта, которая обычно содержит одно большое изображение, одну или несколько кнопок и текст.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-183">A card that typically contains a single large image, one or more buttons, and text.</span></span>

### <a name="support-for-hero-cards"></a><span data-ttu-id="0c6fd-184">Поддержка карт героев</span><span class="sxs-lookup"><span data-stu-id="0c6fd-184">Support for hero cards</span></span>

| <span data-ttu-id="0c6fd-185">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="0c6fd-185">Bots in Teams</span></span> | <span data-ttu-id="0c6fd-186">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="0c6fd-186">Messaging extensions</span></span>  | <span data-ttu-id="0c6fd-187">Соединители</span><span class="sxs-lookup"><span data-stu-id="0c6fd-187">Connectors</span></span> | <span data-ttu-id="0c6fd-188">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="0c6fd-188">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0c6fd-189">✔</span><span class="sxs-lookup"><span data-stu-id="0c6fd-189">✔</span></span> | <span data-ttu-id="0c6fd-190">✔</span><span class="sxs-lookup"><span data-stu-id="0c6fd-190">✔</span></span> | <span data-ttu-id="0c6fd-191">✖</span><span class="sxs-lookup"><span data-stu-id="0c6fd-191">✖</span></span> | <span data-ttu-id="0c6fd-192">✔</span><span class="sxs-lookup"><span data-stu-id="0c6fd-192">✔</span></span> |

### <a name="properties-of-a-hero-card"></a><span data-ttu-id="0c6fd-193">Свойства карты героя</span><span class="sxs-lookup"><span data-stu-id="0c6fd-193">Properties of a hero card</span></span>

| <span data-ttu-id="0c6fd-194">Свойство</span><span class="sxs-lookup"><span data-stu-id="0c6fd-194">Property</span></span> | <span data-ttu-id="0c6fd-195">Тип</span><span class="sxs-lookup"><span data-stu-id="0c6fd-195">Type</span></span>  | <span data-ttu-id="0c6fd-196">Описание</span><span class="sxs-lookup"><span data-stu-id="0c6fd-196">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0c6fd-197">title</span><span class="sxs-lookup"><span data-stu-id="0c6fd-197">title</span></span> | <span data-ttu-id="0c6fd-198">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="0c6fd-198">Rich text</span></span> | <span data-ttu-id="0c6fd-199">Название карты.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-199">Title of the card.</span></span> <span data-ttu-id="0c6fd-200">Максимум 2 строки.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-200">Maximum 2 lines.</span></span> |
| <span data-ttu-id="0c6fd-201">подзаголовок</span><span class="sxs-lookup"><span data-stu-id="0c6fd-201">subtitle</span></span> | <span data-ttu-id="0c6fd-202">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="0c6fd-202">Rich text</span></span> | <span data-ttu-id="0c6fd-203">Подзаголовок карты.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-203">Subtitle of the card.</span></span> <span data-ttu-id="0c6fd-204">Максимум 2 строки.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-204">Maximum 2 lines.</span></span>|
| <span data-ttu-id="0c6fd-205">текст</span><span class="sxs-lookup"><span data-stu-id="0c6fd-205">text</span></span> | <span data-ttu-id="0c6fd-206">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="0c6fd-206">Rich text</span></span> | <span data-ttu-id="0c6fd-207">Текст появляется под подзаголовком.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-207">Text appears under the subtitle.</span></span> <span data-ttu-id="0c6fd-208">Для форматирования опций [см.](~/task-modules-and-cards/cards/cards-format.md)</span><span class="sxs-lookup"><span data-stu-id="0c6fd-208">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="0c6fd-209">Изображения</span><span class="sxs-lookup"><span data-stu-id="0c6fd-209">images</span></span> | <span data-ttu-id="0c6fd-210">Массив изображений</span><span class="sxs-lookup"><span data-stu-id="0c6fd-210">Array of images</span></span> | <span data-ttu-id="0c6fd-211">Изображение отображается в верхней части карты.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-211">Image displayed at the top of the card.</span></span> <span data-ttu-id="0c6fd-212">Соотношение сторон 16:9.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-212">Aspect ratio 16:9.</span></span> |
| <span data-ttu-id="0c6fd-213">Кнопки</span><span class="sxs-lookup"><span data-stu-id="0c6fd-213">buttons</span></span> | <span data-ttu-id="0c6fd-214">Массив объектов действия</span><span class="sxs-lookup"><span data-stu-id="0c6fd-214">Array of action objects</span></span> | <span data-ttu-id="0c6fd-215">Набор действий, применимых к текущей карте.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-215">Set of actions applicable to the current card.</span></span> <span data-ttu-id="0c6fd-216">Максимум 6.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-216">Maximum 6.</span></span> |
| <span data-ttu-id="0c6fd-217">кран</span><span class="sxs-lookup"><span data-stu-id="0c6fd-217">tap</span></span> | <span data-ttu-id="0c6fd-218">Объект Action</span><span class="sxs-lookup"><span data-stu-id="0c6fd-218">Action object</span></span> | <span data-ttu-id="0c6fd-219">Активируется при нажатии пользователя на сам карту.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-219">Activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-hero-card"></a><span data-ttu-id="0c6fd-220">Пример карты героя</span><span class="sxs-lookup"><span data-stu-id="0c6fd-220">Example of a hero card</span></span>

![Пример карты героя](~/assets/images/cards/hero.png)

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

### <a name="additional-information-on-hero-cards"></a><span data-ttu-id="0c6fd-222">Дополнительная информация о картах героев</span><span class="sxs-lookup"><span data-stu-id="0c6fd-222">Additional information on hero cards</span></span>

<span data-ttu-id="0c6fd-223">Ссылка на Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="0c6fd-223">Bot Framework reference:</span></span>

* [<span data-ttu-id="0c6fd-224">Герой карты Node.js</span><span class="sxs-lookup"><span data-stu-id="0c6fd-224">Hero card Node.js</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-a-hero-card&preserve-view=true)
* [<span data-ttu-id="0c6fd-225">Карта героя C #</span><span class="sxs-lookup"><span data-stu-id="0c6fd-225">Hero card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-hero-card&preserve-view=true)

## <a name="list-card"></a><span data-ttu-id="0c6fd-226">Карта списка</span><span class="sxs-lookup"><span data-stu-id="0c6fd-226">List card</span></span>

<span data-ttu-id="0c6fd-227">Карта списка была добавлена в систему, Teams функции сверх того, что может предоставить коллекция списков.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-227">The list card has been added by Teams to provide functions beyond what the list collection can provide.</span></span> <span data-ttu-id="0c6fd-228">Карта списка содержит список элементов для прокрутки.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-228">The list card provides a scrolling list of items.</span></span>

### <a name="support-for-list-cards"></a><span data-ttu-id="0c6fd-229">Поддержка карт списков</span><span class="sxs-lookup"><span data-stu-id="0c6fd-229">Support for list cards</span></span>

| <span data-ttu-id="0c6fd-230">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="0c6fd-230">Bots in Teams</span></span> | <span data-ttu-id="0c6fd-231">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="0c6fd-231">Messaging extensions</span></span>  | <span data-ttu-id="0c6fd-232">Соединители</span><span class="sxs-lookup"><span data-stu-id="0c6fd-232">Connectors</span></span> | <span data-ttu-id="0c6fd-233">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="0c6fd-233">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0c6fd-234">✔</span><span class="sxs-lookup"><span data-stu-id="0c6fd-234">✔</span></span> | <span data-ttu-id="0c6fd-235">✖</span><span class="sxs-lookup"><span data-stu-id="0c6fd-235">✖</span></span> | <span data-ttu-id="0c6fd-236">✖</span><span class="sxs-lookup"><span data-stu-id="0c6fd-236">✖</span></span> |<span data-ttu-id="0c6fd-237">✔</span><span class="sxs-lookup"><span data-stu-id="0c6fd-237">✔</span></span> |

### <a name="properties-of-a-list-card"></a><span data-ttu-id="0c6fd-238">Свойства карты списка</span><span class="sxs-lookup"><span data-stu-id="0c6fd-238">Properties of a list card</span></span>

| <span data-ttu-id="0c6fd-239">Свойство</span><span class="sxs-lookup"><span data-stu-id="0c6fd-239">Property</span></span> | <span data-ttu-id="0c6fd-240">Тип</span><span class="sxs-lookup"><span data-stu-id="0c6fd-240">Type</span></span>  | <span data-ttu-id="0c6fd-241">Описание</span><span class="sxs-lookup"><span data-stu-id="0c6fd-241">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0c6fd-242">title</span><span class="sxs-lookup"><span data-stu-id="0c6fd-242">title</span></span> | <span data-ttu-id="0c6fd-243">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="0c6fd-243">Rich text</span></span> | <span data-ttu-id="0c6fd-244">Название карты.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-244">Title of the card.</span></span> <span data-ttu-id="0c6fd-245">Максимум 2 строки.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-245">Maximum 2 lines.</span></span>|
| <span data-ttu-id="0c6fd-246">элементы</span><span class="sxs-lookup"><span data-stu-id="0c6fd-246">items</span></span> | <span data-ttu-id="0c6fd-247">Массив элементов списка</span><span class="sxs-lookup"><span data-stu-id="0c6fd-247">Array of list items</span></span> ||
| <span data-ttu-id="0c6fd-248">Кнопки</span><span class="sxs-lookup"><span data-stu-id="0c6fd-248">buttons</span></span> | <span data-ttu-id="0c6fd-249">Массив объектов действия</span><span class="sxs-lookup"><span data-stu-id="0c6fd-249">Array of action objects</span></span> | <span data-ttu-id="0c6fd-250">Набор действий, применимых к текущей карте.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-250">Set of actions applicable to the current card.</span></span> <span data-ttu-id="0c6fd-251">Максимум 6.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-251">Maximum 6.</span></span> |

### <a name="example-of-a-list-card"></a><span data-ttu-id="0c6fd-252">Пример карты списка</span><span class="sxs-lookup"><span data-stu-id="0c6fd-252">Example of a list card</span></span>

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

## <a name="office-365-connector-card"></a><span data-ttu-id="0c6fd-253">Office 365-карта</span><span class="sxs-lookup"><span data-stu-id="0c6fd-253">Office 365 connector card</span></span>

<span data-ttu-id="0c6fd-254">Карта Office 365 разъем поддерживается в Teams, а не в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-254">The Office 365 connector card is supported in Teams, not in Bot Framework.</span></span> <span data-ttu-id="0c6fd-255">Эта карта обеспечивает гибкую компоновку с несколькими разделами, полями, изображениями и действиями.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-255">This card provides a flexible layout with multiple sections, fields, images, and actions.</span></span> <span data-ttu-id="0c6fd-256">Эта карта инкапсулирует разъем карты, так что он может быть использован ботов.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-256">This card encapsulates a connector card so that it can be used by bots.</span></span> <span data-ttu-id="0c6fd-257">Различия между разъемами и картой O365 см. [Примечания на Office 365 разъема.](#notes-on-the-office-365-connector-card)</span><span class="sxs-lookup"><span data-stu-id="0c6fd-257">For differences between connector cards and the O365 card, see [Notes on the Office 365 connector card](#notes-on-the-office-365-connector-card).</span></span>

### <a name="support-for-office-365-connector-cards"></a><span data-ttu-id="0c6fd-258">Поддержка Office 365 разъемов</span><span class="sxs-lookup"><span data-stu-id="0c6fd-258">Support for Office 365 connector cards</span></span>

| <span data-ttu-id="0c6fd-259">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="0c6fd-259">Bots in Teams</span></span> | <span data-ttu-id="0c6fd-260">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="0c6fd-260">Messaging extensions</span></span>  | <span data-ttu-id="0c6fd-261">Соединители</span><span class="sxs-lookup"><span data-stu-id="0c6fd-261">Connectors</span></span> | <span data-ttu-id="0c6fd-262">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="0c6fd-262">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0c6fd-263">✔</span><span class="sxs-lookup"><span data-stu-id="0c6fd-263">✔</span></span> | <span data-ttu-id="0c6fd-264">✔</span><span class="sxs-lookup"><span data-stu-id="0c6fd-264">✔</span></span> | <span data-ttu-id="0c6fd-265">✔</span><span class="sxs-lookup"><span data-stu-id="0c6fd-265">✔</span></span> | <span data-ttu-id="0c6fd-266">✖</span><span class="sxs-lookup"><span data-stu-id="0c6fd-266">✖</span></span> |

### <a name="properties-of-the-office-365-connector-card"></a><span data-ttu-id="0c6fd-267">Свойства Office 365 карты</span><span class="sxs-lookup"><span data-stu-id="0c6fd-267">Properties of the Office 365 connector card</span></span>

| <span data-ttu-id="0c6fd-268">Свойство</span><span class="sxs-lookup"><span data-stu-id="0c6fd-268">Property</span></span> | <span data-ttu-id="0c6fd-269">Тип</span><span class="sxs-lookup"><span data-stu-id="0c6fd-269">Type</span></span>  | <span data-ttu-id="0c6fd-270">Описание</span><span class="sxs-lookup"><span data-stu-id="0c6fd-270">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0c6fd-271">title</span><span class="sxs-lookup"><span data-stu-id="0c6fd-271">title</span></span> | <span data-ttu-id="0c6fd-272">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="0c6fd-272">Rich text</span></span> | <span data-ttu-id="0c6fd-273">Название карты.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-273">Title of the card.</span></span> <span data-ttu-id="0c6fd-274">Максимум 2 строки.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-274">Maximum 2 lines.</span></span> |
| <span data-ttu-id="0c6fd-275">summary</span><span class="sxs-lookup"><span data-stu-id="0c6fd-275">summary</span></span> | <span data-ttu-id="0c6fd-276">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="0c6fd-276">Rich text</span></span> | <span data-ttu-id="0c6fd-277">Резюме карты.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-277">Summary of the card.</span></span> <span data-ttu-id="0c6fd-278">Максимум 2 строки.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-278">Maximum 2 lines.</span></span> |
| <span data-ttu-id="0c6fd-279">текст</span><span class="sxs-lookup"><span data-stu-id="0c6fd-279">text</span></span> | <span data-ttu-id="0c6fd-280">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="0c6fd-280">Rich text</span></span> | <span data-ttu-id="0c6fd-281">Текст появляется под подзаголовком.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-281">Text appears under the subtitle.</span></span> <span data-ttu-id="0c6fd-282">Для форматирования опций [см.](~/task-modules-and-cards/cards/cards-format.md)</span><span class="sxs-lookup"><span data-stu-id="0c6fd-282">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="0c6fd-283">themeColor</span><span class="sxs-lookup"><span data-stu-id="0c6fd-283">themeColor</span></span> | <span data-ttu-id="0c6fd-284">Строка HEX</span><span class="sxs-lookup"><span data-stu-id="0c6fd-284">HEX string</span></span> | <span data-ttu-id="0c6fd-285">Цвет, переопределяет акцентColor, предоставленный из манифеста приложения.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-285">Color that overrides the accentColor provided from the application manifest.</span></span> |

### <a name="notes-on-the-office-365-connector-card"></a><span data-ttu-id="0c6fd-286">Заметки на Office 365 разъеме карты</span><span class="sxs-lookup"><span data-stu-id="0c6fd-286">Notes on the Office 365 connector card</span></span>

<span data-ttu-id="0c6fd-287">Office 365 разъем карты функционируют должным образом в Microsoft Teams, в том [числе ActionCard действия](/outlook/actionable-messages/card-reference#actioncard-action).</span><span class="sxs-lookup"><span data-stu-id="0c6fd-287">Office 365 connector cards function properly in Microsoft Teams, including [ActionCard actions](/outlook/actionable-messages/card-reference#actioncard-action).</span></span>

<span data-ttu-id="0c6fd-288">Одним из важных различий между использованием разъемных карт из разъема и использованием разъемных карт в вашем боте является обработка действий карты.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-288">One important difference between using connector cards from a connector and using connector cards in your bot is the handling of card actions.</span></span>

* <span data-ttu-id="0c6fd-289">Для разъема конечная точка получает полезную нагрузку карты через HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-289">For a connector, the endpoint receives the card payload through HTTP POST.</span></span>
* <span data-ttu-id="0c6fd-290">Для бота действие `HttpPOST` запускает действие, `invoke` которое отправляет боту только идентификатор действия и тело.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-290">For a bot, the `HttpPOST` action triggers an `invoke` activity that sends only the action ID and body to the bot.</span></span>

<span data-ttu-id="0c6fd-291">Каждая карта разъема может отображать не более десяти разделов, и каждый раздел может содержать не более пяти изображений и пять действий.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-291">Each connector card can display a maximum of ten sections, and each section can contain a maximum of five images and five actions.</span></span>

> [!NOTE]
> <span data-ttu-id="0c6fd-292">Любые дополнительные разделы, изображения или действия в сообщении не отображаются.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-292">Any additional sections, images, or actions in a message do not appear.</span></span>

<span data-ttu-id="0c6fd-293">Все текстовые поля поддерживают разметку и HTML.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-293">All text fields support markdown and HTML.</span></span> <span data-ttu-id="0c6fd-294">Вы можете контролировать, какие разделы используют разметку или HTML, установив `markdown` свойство в сообщении.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-294">You can control which sections use markdown or HTML by setting the `markdown` property in a message.</span></span> <span data-ttu-id="0c6fd-295">По `markdown` умолчанию устанавливается `true` .</span><span class="sxs-lookup"><span data-stu-id="0c6fd-295">By default, `markdown` is set to `true`.</span></span> <span data-ttu-id="0c6fd-296">Если вы хотите использовать HTML вместо этого, `markdown` установите на `false` .</span><span class="sxs-lookup"><span data-stu-id="0c6fd-296">If you want to use HTML instead, set `markdown` to `false`.</span></span>

<span data-ttu-id="0c6fd-297">Если вы `themeColor` указываете свойство, оно переопределяет `accentColor` свойство в манифесте приложения.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-297">If you specify the `themeColor` property, it overrides the `accentColor` property in the app manifest.</span></span>

<span data-ttu-id="0c6fd-298">Чтобы указать стиль рендеринга `activityImage` для, вы можете установить `activityImageType` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="0c6fd-298">To specify the rendering style for `activityImage`, you can set `activityImageType` as follows:</span></span>

| <span data-ttu-id="0c6fd-299">Значение</span><span class="sxs-lookup"><span data-stu-id="0c6fd-299">Value</span></span> | <span data-ttu-id="0c6fd-300">Описание</span><span class="sxs-lookup"><span data-stu-id="0c6fd-300">Description</span></span> |
| --- | --- |
| `avatar` | <span data-ttu-id="0c6fd-301">По умолчанию; `activityImage` обрезается как круг.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-301">Default; `activityImage` is cropped as a circle.</span></span> |
| `article` | <span data-ttu-id="0c6fd-302">`activityImage` отображается как прямоугольник и сохраняет свое соотношение сторон.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-302">`activityImage` is displayed as a rectangle and retains its aspect ratio.</span></span> |

<span data-ttu-id="0c6fd-303">Для всех других деталей о свойствах разъемной карты, смотрите [действий ссылку карты сообщения.](/outlook/actionable-messages/card-reference)</span><span class="sxs-lookup"><span data-stu-id="0c6fd-303">For all other details about connector card properties, see [actionable message card reference](/outlook/actionable-messages/card-reference).</span></span> <span data-ttu-id="0c6fd-304">Единственными свойствами разъемной карты, которые Microsoft Teams в настоящее время не поддерживают, являются следующие:</span><span class="sxs-lookup"><span data-stu-id="0c6fd-304">The only connector card properties that Microsoft Teams does not currently support are as follows:</span></span>

* `heroImage`
* `hideOriginalBody`
* <span data-ttu-id="0c6fd-305">`startGroup`всегда рассматривается `true` как в Teams</span><span class="sxs-lookup"><span data-stu-id="0c6fd-305">`startGroup` always treated as `true` in Teams</span></span>
* `originator`
* `correlationId`

### <a name="example-of-an-office-365-connector-card"></a><span data-ttu-id="0c6fd-306">Пример карты Office 365 разъема</span><span class="sxs-lookup"><span data-stu-id="0c6fd-306">Example of an Office 365 connector card</span></span>

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

## <a name="receipt-card"></a><span data-ttu-id="0c6fd-307">Квитанция карты</span><span class="sxs-lookup"><span data-stu-id="0c6fd-307">Receipt card</span></span>

<span data-ttu-id="0c6fd-308">Teams поддерживает квитанцию.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-308">Teams supports receipt card.</span></span> <span data-ttu-id="0c6fd-309">Это карта, которая позволяет боту предоставить квитанцию пользователю.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-309">It is a card that enables a bot to provide a receipt to the user.</span></span> <span data-ttu-id="0c6fd-310">Как правило, он содержит список товаров, которые можно включить в квитанцию, такие как налог и общая информация.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-310">It typically contains the list of items to include on the receipt, such as tax and total information.</span></span>

### <a name="support-for-receipt-cards"></a><span data-ttu-id="0c6fd-311">Поддержка квитанций</span><span class="sxs-lookup"><span data-stu-id="0c6fd-311">Support for receipt cards</span></span>

| <span data-ttu-id="0c6fd-312">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="0c6fd-312">Bots in Teams</span></span> | <span data-ttu-id="0c6fd-313">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="0c6fd-313">Messaging extensions</span></span>  | <span data-ttu-id="0c6fd-314">Соединители</span><span class="sxs-lookup"><span data-stu-id="0c6fd-314">Connectors</span></span> | <span data-ttu-id="0c6fd-315">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="0c6fd-315">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0c6fd-316">✔</span><span class="sxs-lookup"><span data-stu-id="0c6fd-316">✔</span></span> | <span data-ttu-id="0c6fd-317">✔</span><span class="sxs-lookup"><span data-stu-id="0c6fd-317">✔</span></span> | <span data-ttu-id="0c6fd-318">✖</span><span class="sxs-lookup"><span data-stu-id="0c6fd-318">✖</span></span> | <span data-ttu-id="0c6fd-319">✔</span><span class="sxs-lookup"><span data-stu-id="0c6fd-319">✔</span></span> |

### <a name="example-of-a-receipt-card"></a><span data-ttu-id="0c6fd-320">Пример квитанции</span><span class="sxs-lookup"><span data-stu-id="0c6fd-320">Example of a receipt card</span></span>

![Пример квитанции](~/assets/images/cards/receipt.png)

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

### <a name="additional-information-on-receipt-cards"></a><span data-ttu-id="0c6fd-322">Дополнительная информация о квитанциях</span><span class="sxs-lookup"><span data-stu-id="0c6fd-322">Additional information on receipt cards</span></span>

<span data-ttu-id="0c6fd-323">Ссылка на Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="0c6fd-323">Bot Framework reference:</span></span>

* [<span data-ttu-id="0c6fd-324">Квитанция по Node.js</span><span class="sxs-lookup"><span data-stu-id="0c6fd-324">Receipt card Node.js</span></span>](/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="0c6fd-325">Квитанция карты C #</span><span class="sxs-lookup"><span data-stu-id="0c6fd-325">Receipt card C#</span></span>](/dotnet/api/microsoft.bot.schema.receiptcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="signin-card"></a><span data-ttu-id="0c6fd-326">Карта Сигнина</span><span class="sxs-lookup"><span data-stu-id="0c6fd-326">Signin card</span></span>

<span data-ttu-id="0c6fd-327">Карта Signin позволяет боту запросить у пользователя регистрацию.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-327">Signin card enables a bot to request a user to sign in.</span></span> <span data-ttu-id="0c6fd-328">Он поддерживается в Teams в несколько иной форме, чем это имеется в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-328">It is supported in Teams in a slightly different form than is found in the Bot Framework.</span></span> <span data-ttu-id="0c6fd-329">Карта signin в Teams похожа на карту signin в Bot Framework, за исключением того, что карта signin в Teams поддерживает только два действия: `signin` и `openUrl` .</span><span class="sxs-lookup"><span data-stu-id="0c6fd-329">The signin card in Teams is similar to the signin card in the Bot Framework except that the signin card in Teams only supports two actions: `signin` and `openUrl`.</span></span>

<span data-ttu-id="0c6fd-330">Действия signin можно использовать с любой карты в Teams, а не только с карты signin.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-330">The signin action can be used from any card in Teams, not just the signin card.</span></span> <span data-ttu-id="0c6fd-331">Для получения дополнительной информации об аутентификации [Microsoft Teams потока аутентификации для ботов.](~/bots/how-to/authentication/auth-flow-bot.md)</span><span class="sxs-lookup"><span data-stu-id="0c6fd-331">For more information on authentication, see [Microsoft Teams authentication flow for bots](~/bots/how-to/authentication/auth-flow-bot.md).</span></span>

### <a name="support-for-signin-cards"></a><span data-ttu-id="0c6fd-332">Поддержка подписных карт</span><span class="sxs-lookup"><span data-stu-id="0c6fd-332">Support for signin cards</span></span>

| <span data-ttu-id="0c6fd-333">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="0c6fd-333">Bots in Teams</span></span> | <span data-ttu-id="0c6fd-334">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="0c6fd-334">Messaging extensions</span></span>  | <span data-ttu-id="0c6fd-335">Соединители</span><span class="sxs-lookup"><span data-stu-id="0c6fd-335">Connectors</span></span> | <span data-ttu-id="0c6fd-336">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="0c6fd-336">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0c6fd-337">✔</span><span class="sxs-lookup"><span data-stu-id="0c6fd-337">✔</span></span> | <span data-ttu-id="0c6fd-338">✖</span><span class="sxs-lookup"><span data-stu-id="0c6fd-338">✖</span></span> | <span data-ttu-id="0c6fd-339">✖</span><span class="sxs-lookup"><span data-stu-id="0c6fd-339">✖</span></span> | <span data-ttu-id="0c6fd-340">✔</span><span class="sxs-lookup"><span data-stu-id="0c6fd-340">✔</span></span> |

### <a name="additional-information-on-signin-cards"></a><span data-ttu-id="0c6fd-341">Дополнительная информация о карточках signin</span><span class="sxs-lookup"><span data-stu-id="0c6fd-341">Additional information on signin cards</span></span>

<span data-ttu-id="0c6fd-342">Ссылка на Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="0c6fd-342">Bot Framework reference:</span></span>

* [<span data-ttu-id="0c6fd-343">Сигнин карточный Node.js</span><span class="sxs-lookup"><span data-stu-id="0c6fd-343">Signin card Node.js</span></span>](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="0c6fd-344">Сигнин-карта C #</span><span class="sxs-lookup"><span data-stu-id="0c6fd-344">Signin card C#</span></span>](/dotnet/api/microsoft.bot.schema.signincard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="thumbnail-card"></a><span data-ttu-id="0c6fd-345">Thumbnail карты</span><span class="sxs-lookup"><span data-stu-id="0c6fd-345">Thumbnail card</span></span>

<span data-ttu-id="0c6fd-346">Карта, которая обычно содержит одно изображение эскиза, одну или несколько кнопок и текст.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-346">A card that typically contains a single thumbnail image, one or more buttons, and text.</span></span>

### <a name="support-for-thumbnail-cards"></a><span data-ttu-id="0c6fd-347">Поддержка эскизных карт</span><span class="sxs-lookup"><span data-stu-id="0c6fd-347">Support for thumbnail cards</span></span>

| <span data-ttu-id="0c6fd-348">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="0c6fd-348">Bots in Teams</span></span> | <span data-ttu-id="0c6fd-349">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="0c6fd-349">Messaging extensions</span></span>  | <span data-ttu-id="0c6fd-350">Соединители</span><span class="sxs-lookup"><span data-stu-id="0c6fd-350">Connectors</span></span> | <span data-ttu-id="0c6fd-351">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="0c6fd-351">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0c6fd-352">✔</span><span class="sxs-lookup"><span data-stu-id="0c6fd-352">✔</span></span> | <span data-ttu-id="0c6fd-353">✔</span><span class="sxs-lookup"><span data-stu-id="0c6fd-353">✔</span></span> | <span data-ttu-id="0c6fd-354">✖</span><span class="sxs-lookup"><span data-stu-id="0c6fd-354">✖</span></span> | <span data-ttu-id="0c6fd-355">✔</span><span class="sxs-lookup"><span data-stu-id="0c6fd-355">✔</span></span> |

![Пример карты эскиза](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a><span data-ttu-id="0c6fd-357">Свойства эскизной карты</span><span class="sxs-lookup"><span data-stu-id="0c6fd-357">Properties of a thumbnail card</span></span>

| <span data-ttu-id="0c6fd-358">Свойство</span><span class="sxs-lookup"><span data-stu-id="0c6fd-358">Property</span></span> | <span data-ttu-id="0c6fd-359">Тип</span><span class="sxs-lookup"><span data-stu-id="0c6fd-359">Type</span></span>  | <span data-ttu-id="0c6fd-360">Описание</span><span class="sxs-lookup"><span data-stu-id="0c6fd-360">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0c6fd-361">title</span><span class="sxs-lookup"><span data-stu-id="0c6fd-361">title</span></span> | <span data-ttu-id="0c6fd-362">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="0c6fd-362">Rich text</span></span> | <span data-ttu-id="0c6fd-363">Название карты.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-363">Title of the card.</span></span> <span data-ttu-id="0c6fd-364">Максимум 2 строки.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-364">Maximum 2 lines.</span></span>|
| <span data-ttu-id="0c6fd-365">подзаголовок</span><span class="sxs-lookup"><span data-stu-id="0c6fd-365">subtitle</span></span> | <span data-ttu-id="0c6fd-366">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="0c6fd-366">Rich text</span></span> | <span data-ttu-id="0c6fd-367">Подзаголовок карты.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-367">Subtitle of the card.</span></span> <span data-ttu-id="0c6fd-368">Максимум 2 строки.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-368">Maximum 2 lines.</span></span>|
| <span data-ttu-id="0c6fd-369">текст</span><span class="sxs-lookup"><span data-stu-id="0c6fd-369">text</span></span> | <span data-ttu-id="0c6fd-370">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="0c6fd-370">Rich text</span></span> | <span data-ttu-id="0c6fd-371">Текст появляется под подзаголовком.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-371">Text appears under the subtitle.</span></span> <span data-ttu-id="0c6fd-372">Для форматирования опций [см.](~/task-modules-and-cards/cards/cards-format.md)</span><span class="sxs-lookup"><span data-stu-id="0c6fd-372">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="0c6fd-373">Изображения</span><span class="sxs-lookup"><span data-stu-id="0c6fd-373">images</span></span> | <span data-ttu-id="0c6fd-374">Массив изображений</span><span class="sxs-lookup"><span data-stu-id="0c6fd-374">Array of images</span></span> | <span data-ttu-id="0c6fd-375">Изображение отображается в верхней части карты.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-375">Image displayed at the top of the card.</span></span> <span data-ttu-id="0c6fd-376">Соотношение аспектов 1:1 квадрат.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-376">Aspect ratio 1:1 square.</span></span> |
| <span data-ttu-id="0c6fd-377">Кнопки</span><span class="sxs-lookup"><span data-stu-id="0c6fd-377">buttons</span></span> | <span data-ttu-id="0c6fd-378">Массив объектов действия</span><span class="sxs-lookup"><span data-stu-id="0c6fd-378">Array of action objects</span></span> | <span data-ttu-id="0c6fd-379">Набор действий, применимых к текущей карте.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-379">Set of actions applicable to the current card.</span></span> <span data-ttu-id="0c6fd-380">Максимум 6.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-380">Maximum 6.</span></span> |
| <span data-ttu-id="0c6fd-381">кран</span><span class="sxs-lookup"><span data-stu-id="0c6fd-381">tap</span></span> | <span data-ttu-id="0c6fd-382">Объект Action</span><span class="sxs-lookup"><span data-stu-id="0c6fd-382">Action object</span></span> | <span data-ttu-id="0c6fd-383">Активируется при нажатии пользователя на сам карту.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-383">Activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-thumbnail-card"></a><span data-ttu-id="0c6fd-384">Пример карты эскиза</span><span class="sxs-lookup"><span data-stu-id="0c6fd-384">Example of a thumbnail card</span></span>

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

### <a name="additional-information"></a><span data-ttu-id="0c6fd-385">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="0c6fd-385">Additional information</span></span>

<span data-ttu-id="0c6fd-386">Ссылка на Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="0c6fd-386">Bot Framework reference:</span></span>

* [<span data-ttu-id="0c6fd-387">Thumbnail карты Node.js</span><span class="sxs-lookup"><span data-stu-id="0c6fd-387">Thumbnail card Node.js</span></span>](/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="0c6fd-388">Thumbnail карты C #</span><span class="sxs-lookup"><span data-stu-id="0c6fd-388">Thumbnail card C#</span></span>](/dotnet/api/microsoft.bot.schema.thumbnailcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="card-collections"></a><span data-ttu-id="0c6fd-389">Коллекции карт</span><span class="sxs-lookup"><span data-stu-id="0c6fd-389">Card collections</span></span>

<span data-ttu-id="0c6fd-390">Teams поддерживает коллекции карт.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-390">Teams supports Card collections.</span></span>

<span data-ttu-id="0c6fd-391">Коллекции карт включают `builder.AttachmentLayout.carousel` и `builder.AttachmentLayout.list` .</span><span class="sxs-lookup"><span data-stu-id="0c6fd-391">Card collections include `builder.AttachmentLayout.carousel` and `builder.AttachmentLayout.list`.</span></span> <span data-ttu-id="0c6fd-392">Эти коллекции содержат адаптивные, геройские или эскизные карты.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-392">These collections contain adaptive, hero, or thumbnail cards.</span></span>

## <a name="carousel-collection"></a><span data-ttu-id="0c6fd-393">Коллекция каруселей</span><span class="sxs-lookup"><span data-stu-id="0c6fd-393">Carousel collection</span></span>

<span data-ttu-id="0c6fd-394">Макет [карусели показывает](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) карусель карт, дополнительно с связанными кнопками действия.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-394">The [carousel layout](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) shows a carousel of cards, optionally with associated action buttons.</span></span>

### <a name="support-for-carousel-collections"></a><span data-ttu-id="0c6fd-395">Поддержка коллекций каруселей</span><span class="sxs-lookup"><span data-stu-id="0c6fd-395">Support for carousel collections</span></span>

| <span data-ttu-id="0c6fd-396">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="0c6fd-396">Bots in Teams</span></span> | <span data-ttu-id="0c6fd-397">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="0c6fd-397">Messaging extensions</span></span>  | <span data-ttu-id="0c6fd-398">Соединители</span><span class="sxs-lookup"><span data-stu-id="0c6fd-398">Connectors</span></span> | <span data-ttu-id="0c6fd-399">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="0c6fd-399">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0c6fd-400">✔</span><span class="sxs-lookup"><span data-stu-id="0c6fd-400">✔</span></span> | <span data-ttu-id="0c6fd-401">✖</span><span class="sxs-lookup"><span data-stu-id="0c6fd-401">✖</span></span> | <span data-ttu-id="0c6fd-402">✖</span><span class="sxs-lookup"><span data-stu-id="0c6fd-402">✖</span></span> | <span data-ttu-id="0c6fd-403">✔</span><span class="sxs-lookup"><span data-stu-id="0c6fd-403">✔</span></span> |

> [!NOTE]
> <span data-ttu-id="0c6fd-404">Карусель может отображать не более десяти карт на одно сообщение.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-404">A carousel can display a maximum of ten cards per message.</span></span>

### <a name="properties-of-a-carousel-card"></a><span data-ttu-id="0c6fd-405">Свойства карусели карты</span><span class="sxs-lookup"><span data-stu-id="0c6fd-405">Properties of a carousel card</span></span>

<span data-ttu-id="0c6fd-406">Свойства карты карусели такие же, как у героя и эскизных карт.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-406">Properties of a carousel card are same as those of the hero and thumbnail cards.</span></span>

### <a name="example-of-a-carousel-collection"></a><span data-ttu-id="0c6fd-407">Пример коллекции каруселей</span><span class="sxs-lookup"><span data-stu-id="0c6fd-407">Example of a carousel collection</span></span>

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

### <a name="syntax-for-carousel-collections"></a><span data-ttu-id="0c6fd-409">Синтаксис для коллекций каруселей</span><span class="sxs-lookup"><span data-stu-id="0c6fd-409">Syntax for carousel collections</span></span>

<span data-ttu-id="0c6fd-410">`builder.AttachmentLayoutTypes.Carousel` является синтаксисом для коллекций каруселей.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-410">`builder.AttachmentLayoutTypes.Carousel` is the syntax for carousel collections.</span></span>

## <a name="list-collection"></a><span data-ttu-id="0c6fd-411">Коллекция списков</span><span class="sxs-lookup"><span data-stu-id="0c6fd-411">List collection</span></span>

### <a name="support-for-list-collections"></a><span data-ttu-id="0c6fd-412">Поддержка коллекций списков</span><span class="sxs-lookup"><span data-stu-id="0c6fd-412">Support for list collections</span></span>

<span data-ttu-id="0c6fd-413">Макет списка показывает вертикально сложенный список карт, дополнительно с связанными кнопками действия.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-413">The list layout shows a vertically stacked list of cards, optionally with associated action buttons.</span></span>

| <span data-ttu-id="0c6fd-414">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="0c6fd-414">Bots in Teams</span></span> | <span data-ttu-id="0c6fd-415">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="0c6fd-415">Messaging extensions</span></span>  | <span data-ttu-id="0c6fd-416">Соединители</span><span class="sxs-lookup"><span data-stu-id="0c6fd-416">Connectors</span></span> | <span data-ttu-id="0c6fd-417">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="0c6fd-417">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0c6fd-418">✔</span><span class="sxs-lookup"><span data-stu-id="0c6fd-418">✔</span></span> | <span data-ttu-id="0c6fd-419">✔</span><span class="sxs-lookup"><span data-stu-id="0c6fd-419">✔</span></span> | <span data-ttu-id="0c6fd-420">✖</span><span class="sxs-lookup"><span data-stu-id="0c6fd-420">✖</span></span> | <span data-ttu-id="0c6fd-421">✔</span><span class="sxs-lookup"><span data-stu-id="0c6fd-421">✔</span></span> |

### <a name="example-of-a-list-collection"></a><span data-ttu-id="0c6fd-422">Пример коллекции списков</span><span class="sxs-lookup"><span data-stu-id="0c6fd-422">Example of a list collection</span></span>

![Пример списка карт](~/assets/images/cards/list.png)

<span data-ttu-id="0c6fd-424">Свойства такие же, как для героя или эскиз карты.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-424">Properties are the same as for the hero or thumbnail card.</span></span>

<span data-ttu-id="0c6fd-425">Список может отображать не более десяти карт на одно сообщение.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-425">A list can display a maximum of ten cards per message.</span></span>

> [!NOTE]
> <span data-ttu-id="0c6fd-426">Некоторые комбинации карт списка пока не поддерживаются на iOS и Android.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-426">Some combinations of list cards are not yet supported on iOS and Android.</span></span>

### <a name="syntax-for-list-collections"></a><span data-ttu-id="0c6fd-427">Синтаксис для коллекций списков</span><span class="sxs-lookup"><span data-stu-id="0c6fd-427">Syntax for list collections</span></span>

<span data-ttu-id="0c6fd-428">`builder.AttachmentLayout.list` является синтаксисом для коллекций списков.</span><span class="sxs-lookup"><span data-stu-id="0c6fd-428">`builder.AttachmentLayout.list` is the syntax for list collections.</span></span>

## <a name="cards-not-supported-in-teams"></a><span data-ttu-id="0c6fd-429">Карты, не поддерживаемые в Teams</span><span class="sxs-lookup"><span data-stu-id="0c6fd-429">Cards not supported in Teams</span></span>

<span data-ttu-id="0c6fd-430">Следующие карты реализованы Bot Framework, но не поддерживаются Teams:</span><span class="sxs-lookup"><span data-stu-id="0c6fd-430">The following cards are implemented by the Bot Framework, but are not supported by Teams:</span></span>

* <span data-ttu-id="0c6fd-431">Анимационные карты</span><span class="sxs-lookup"><span data-stu-id="0c6fd-431">Animation cards</span></span>
* <span data-ttu-id="0c6fd-432">Аудиокарты</span><span class="sxs-lookup"><span data-stu-id="0c6fd-432">Audio cards</span></span>
* <span data-ttu-id="0c6fd-433">Видеокарты</span><span class="sxs-lookup"><span data-stu-id="0c6fd-433">Video cards</span></span>
