---
title: Справка по картам
description: Описание всех действий карт и карт, доступных ботам в Teams
keywords: ссылка на карточки ботов
ms.topic: reference
ms.openlocfilehash: 5cb289738f379dedf53f3a96a7dcff61b908e901
ms.sourcegitcommit: 1ce74ed167bb81bf09f7f6f8d518093efafb549e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/16/2021
ms.locfileid: "50827937"
---
# <a name="cards-reference"></a><span data-ttu-id="544dc-104">Ссылки на карточки</span><span class="sxs-lookup"><span data-stu-id="544dc-104">Cards reference</span></span>

<span data-ttu-id="544dc-105">Карты, перечисленные в этом разделе, поддерживаются в ботах для Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="544dc-105">The cards listed in this section are supported in bots for Microsoft Teams.</span></span> <span data-ttu-id="544dc-106">Они основаны на картах, определенных bot Framework, но Teams не поддерживает все карты Bot Framework и добавляет некоторые из них.</span><span class="sxs-lookup"><span data-stu-id="544dc-106">They are based on cards defined by the Bot Framework, but Teams does not support all Bot Framework cards and has added some of its own.</span></span> <span data-ttu-id="544dc-107">Различия называются в ссылках в этом документе.</span><span class="sxs-lookup"><span data-stu-id="544dc-107">Differences are called out in the references in this document.</span></span>

## <a name="card-examples"></a><span data-ttu-id="544dc-108">Примеры карт</span><span class="sxs-lookup"><span data-stu-id="544dc-108">Card examples</span></span>

<span data-ttu-id="544dc-109">Дополнительные сведения об использовании карт можно найти в документации по SDK Bot Builder (v3).</span><span class="sxs-lookup"><span data-stu-id="544dc-109">You can find additional information on how to use cards in the documentation for the Bot Builder SDK (v3).</span></span> <span data-ttu-id="544dc-110">Примеры кода также доступны в репозитории Microsoft/BotBuilder-Samples на GitHub.</span><span class="sxs-lookup"><span data-stu-id="544dc-110">Code samples are also available in the Microsoft/BotBuilder-Samples repository on GitHub.</span></span>

* <span data-ttu-id="544dc-111">.NET</span><span class="sxs-lookup"><span data-stu-id="544dc-111">.NET</span></span>
  * [<span data-ttu-id="544dc-112">Добавление карт в виде вложений в сообщения</span><span class="sxs-lookup"><span data-stu-id="544dc-112">Add cards as attachments to messages</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)
  * [<span data-ttu-id="544dc-113">Пример кода карт (Bot Builder v4)</span><span class="sxs-lookup"><span data-stu-id="544dc-113">Cards sample code (Bot Builder v4)</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards)

* <span data-ttu-id="544dc-114">Node.js</span><span class="sxs-lookup"><span data-stu-id="544dc-114">Node.js</span></span>
  * [<span data-ttu-id="544dc-115">Добавление карт в виде вложений в сообщения</span><span class="sxs-lookup"><span data-stu-id="544dc-115">Add cards as attachments to messages</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)
  * [<span data-ttu-id="544dc-116">Пример кода карт (Bot Builder v4)</span><span class="sxs-lookup"><span data-stu-id="544dc-116">Cards sample code (Bot Builder v4)</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards)

## <a name="types-of-cards"></a><span data-ttu-id="544dc-117">Типы карт</span><span class="sxs-lookup"><span data-stu-id="544dc-117">Types of cards</span></span>

<span data-ttu-id="544dc-118">В этой таблице показаны типы доступных вам карт:</span><span class="sxs-lookup"><span data-stu-id="544dc-118">This table shows the types of cards available to you:</span></span>

| <span data-ttu-id="544dc-119">Тип карты</span><span class="sxs-lookup"><span data-stu-id="544dc-119">Card type</span></span> | <span data-ttu-id="544dc-120">Описание</span><span class="sxs-lookup"><span data-stu-id="544dc-120">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="544dc-121">Адаптивная карта</span><span class="sxs-lookup"><span data-stu-id="544dc-121">Adaptive card</span></span>](#adaptive-card) | <span data-ttu-id="544dc-122">Высоко настраиваемая карта, которая может содержать любое сочетание текстов, речи, изображений, кнопок и полей ввода.</span><span class="sxs-lookup"><span data-stu-id="544dc-122">Highly customizable card that can contain any combination of text, speech, images, buttons and input fields.</span></span> |
| [<span data-ttu-id="544dc-123">Карта hero</span><span class="sxs-lookup"><span data-stu-id="544dc-123">Hero card</span></span>](#hero-card) | <span data-ttu-id="544dc-124">Обычно содержит одно большое изображение, одну или несколько кнопок и небольшое количество текста.</span><span class="sxs-lookup"><span data-stu-id="544dc-124">Typically contains a single large image, one or more buttons, and a small amount of text.</span></span> |
| [<span data-ttu-id="544dc-125">Карта списка</span><span class="sxs-lookup"><span data-stu-id="544dc-125">List card</span></span>](#list-card) | <span data-ttu-id="544dc-126">Список элементов прокрутки.</span><span class="sxs-lookup"><span data-stu-id="544dc-126">A scrolling list of items.</span></span> |
| [<span data-ttu-id="544dc-127">Соединитечная карта Office 365</span><span class="sxs-lookup"><span data-stu-id="544dc-127">Office 365 connector card</span></span>](#office-365-connector-card) | <span data-ttu-id="544dc-128">Гибкая схема с несколькими разделами, полями, изображениями и действиями.</span><span class="sxs-lookup"><span data-stu-id="544dc-128">Flexible layout with multiple sections, fields, images and actions.</span></span> |
| [<span data-ttu-id="544dc-129">Карта получения</span><span class="sxs-lookup"><span data-stu-id="544dc-129">Receipt card</span></span>](#receipt-card) | <span data-ttu-id="544dc-130">Предоставляет квитанцию пользователю.</span><span class="sxs-lookup"><span data-stu-id="544dc-130">Provides a receipt to the user.</span></span> |
| [<span data-ttu-id="544dc-131">Карточка Signin</span><span class="sxs-lookup"><span data-stu-id="544dc-131">Signin card</span></span>](#signin-card) | <span data-ttu-id="544dc-132">Позволяет боту запрашивать вход пользователя.</span><span class="sxs-lookup"><span data-stu-id="544dc-132">Enables a bot to request that a user sign in.</span></span> |
| [<span data-ttu-id="544dc-133">Карта эскиза</span><span class="sxs-lookup"><span data-stu-id="544dc-133">Thumbnail card</span></span>](#thumbnail-card) | <span data-ttu-id="544dc-134">Обычно содержит одно изображение эскиза, короткий текст и одну или несколько кнопок.</span><span class="sxs-lookup"><span data-stu-id="544dc-134">Typically contains a single thumbnail image, some short text, and one or more buttons.</span></span> |
| [<span data-ttu-id="544dc-135">Коллекции карт</span><span class="sxs-lookup"><span data-stu-id="544dc-135">Card collections</span></span>](#card-collections) | <span data-ttu-id="544dc-136">Используется для возврата нескольких элементов в одном ответе.</span><span class="sxs-lookup"><span data-stu-id="544dc-136">Used to return multiple items in a single response.</span></span> |

## <a name="common-properties-for-all-cards"></a><span data-ttu-id="544dc-137">Общие свойства для всех карт</span><span class="sxs-lookup"><span data-stu-id="544dc-137">Common properties for all cards</span></span>

### <a name="inline-card-images"></a><span data-ttu-id="544dc-138">Inline card images</span><span class="sxs-lookup"><span data-stu-id="544dc-138">Inline card images</span></span>

<span data-ttu-id="544dc-139">Карта может содержать рядное изображение, включив ссылку на общедоступный образ.</span><span class="sxs-lookup"><span data-stu-id="544dc-139">The card can contain an inline image by including a link to the publicly available image.</span></span> <span data-ttu-id="544dc-140">В целях производительности рекомендуется использовать изображение в сети доставки контента общего содержимого (CDN).</span><span class="sxs-lookup"><span data-stu-id="544dc-140">For performance purposes, it is highly recommended you host the image on a public content-delivery network (CDN).</span></span>

<span data-ttu-id="544dc-141">Изображения масштабирования или вниз в размерах при сохранении соотношения аспектов для покрытия области изображения, а затем обрезаны из центра, чтобы достичь соответствующего соотношения аспектов для карты.</span><span class="sxs-lookup"><span data-stu-id="544dc-141">Images are scaled up or down in size while maintaining the aspect ratio to cover the image area, and then cropped from center to achieve the appropriate aspect ratio for the card.</span></span>

<span data-ttu-id="544dc-142">Изображения должны быть не более 1024×1024 в формате PNG, JPEG или GIF, а анимированный GIF не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="544dc-142">Images must be at most 1024×1024, in PNG, JPEG, or GIF format, and animated GIF is not supported.</span></span>

| <span data-ttu-id="544dc-143">Свойство</span><span class="sxs-lookup"><span data-stu-id="544dc-143">Property</span></span> | <span data-ttu-id="544dc-144">Тип</span><span class="sxs-lookup"><span data-stu-id="544dc-144">Type</span></span>  | <span data-ttu-id="544dc-145">Описание</span><span class="sxs-lookup"><span data-stu-id="544dc-145">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="544dc-146">url</span><span class="sxs-lookup"><span data-stu-id="544dc-146">url</span></span> | <span data-ttu-id="544dc-147">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="544dc-147">URL</span></span> | <span data-ttu-id="544dc-148">URL-адрес HTTPS к изображению</span><span class="sxs-lookup"><span data-stu-id="544dc-148">HTTPS URL to the image</span></span> |
| <span data-ttu-id="544dc-149">alt</span><span class="sxs-lookup"><span data-stu-id="544dc-149">alt</span></span> | <span data-ttu-id="544dc-150">Строка</span><span class="sxs-lookup"><span data-stu-id="544dc-150">String</span></span> | <span data-ttu-id="544dc-151">Доступное описание изображения</span><span class="sxs-lookup"><span data-stu-id="544dc-151">Accessible description of the image</span></span> |

### <a name="buttons"></a><span data-ttu-id="544dc-152">Кнопки</span><span class="sxs-lookup"><span data-stu-id="544dc-152">Buttons</span></span>

<span data-ttu-id="544dc-153">Кнопки показаны в нижней части карты.</span><span class="sxs-lookup"><span data-stu-id="544dc-153">Buttons are shown stacked at the bottom of the card.</span></span> <span data-ttu-id="544dc-154">Текст кнопки всегда находится в одной строке и будет усечен, если текст превышает ширину кнопки.</span><span class="sxs-lookup"><span data-stu-id="544dc-154">Button text is always on a single line and will be truncated if the text exceeds the button width.</span></span> <span data-ttu-id="544dc-155">Не будут показаны дополнительные кнопки, которые выходят за пределы максимального числа, поддерживаемого картой.</span><span class="sxs-lookup"><span data-stu-id="544dc-155">Any additional buttons beyond the maximum number supported by the card will not be shown.</span></span>

<span data-ttu-id="544dc-156">Дополнительные [сведения см.](~/task-modules-and-cards/cards/cards-actions.md) в карточных действиях.</span><span class="sxs-lookup"><span data-stu-id="544dc-156">See [Card Actions](~/task-modules-and-cards/cards/cards-actions.md) for more information.</span></span>

### <a name="card-formatting"></a><span data-ttu-id="544dc-157">Форматирование карт</span><span class="sxs-lookup"><span data-stu-id="544dc-157">Card formatting</span></span>

<span data-ttu-id="544dc-158">Дополнительные [сведения о формате](~/task-modules-and-cards/cards/cards-format.md) текстового форматирования в картах см. в документе "Форматирование карт".</span><span class="sxs-lookup"><span data-stu-id="544dc-158">See [Card Formatting](~/task-modules-and-cards/cards/cards-format.md) for more information on text formatting in cards.</span></span>

## <a name="adaptive-card"></a><span data-ttu-id="544dc-159">Адаптивная карта</span><span class="sxs-lookup"><span data-stu-id="544dc-159">Adaptive card</span></span>

<span data-ttu-id="544dc-160">Адаптивная карта — это настраиваемая карта, которая может содержать любое сочетание текстовых, речевого, изображений, кнопок и полей ввода.</span><span class="sxs-lookup"><span data-stu-id="544dc-160">An adaptive card is a customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> <span data-ttu-id="544dc-161">См. [адаптивные карты v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span><span class="sxs-lookup"><span data-stu-id="544dc-161">See [Adaptive Cards v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span></span>

### <a name="support-for-adaptive-cards"></a><span data-ttu-id="544dc-162">Поддержка адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="544dc-162">Support for adaptive cards</span></span>

| <span data-ttu-id="544dc-163">Боты в teams</span><span class="sxs-lookup"><span data-stu-id="544dc-163">Bots in Teams</span></span> | <span data-ttu-id="544dc-164">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="544dc-164">Messaging extensions</span></span>  | <span data-ttu-id="544dc-165">Соединители</span><span class="sxs-lookup"><span data-stu-id="544dc-165">Connectors</span></span> | <span data-ttu-id="544dc-166">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="544dc-166">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="544dc-167">✔</span><span class="sxs-lookup"><span data-stu-id="544dc-167">✔</span></span> | <span data-ttu-id="544dc-168">✔</span><span class="sxs-lookup"><span data-stu-id="544dc-168">✔</span></span> | <span data-ttu-id="544dc-169">✖</span><span class="sxs-lookup"><span data-stu-id="544dc-169">✖</span></span> | <span data-ttu-id="544dc-170">✔</span><span class="sxs-lookup"><span data-stu-id="544dc-170">✔</span></span> |

> [!NOTE]
> * <span data-ttu-id="544dc-171">Платформа Teams поддерживает v1.2 или более ранние функции адаптивной карты.</span><span class="sxs-lookup"><span data-stu-id="544dc-171">Teams platform supports v1.2 or earlier of Adaptive card features.</span></span>
> * <span data-ttu-id="544dc-172">Элементы мультимедиа в настоящее время не поддерживаются в адаптивной карте v1.2 на платформе Teams.</span><span class="sxs-lookup"><span data-stu-id="544dc-172">Media elements are currently not supported in Adaptive card v1.2 on the Teams platform.</span></span>

### <a name="example-of-an-adaptive-card"></a><span data-ttu-id="544dc-173">Пример адаптивной карты</span><span class="sxs-lookup"><span data-stu-id="544dc-173">Example of an adaptive card</span></span>

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

#### <a name="additional-information-on-adaptive-cards"></a><span data-ttu-id="544dc-175">Дополнительные сведения о адаптивных картах</span><span class="sxs-lookup"><span data-stu-id="544dc-175">Additional information on adaptive cards</span></span>

<span data-ttu-id="544dc-176">Ссылка на Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="544dc-176">Bot Framework reference:</span></span>

* [<span data-ttu-id="544dc-177">Узел адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="544dc-177">Adaptive cards Node</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)
* [<span data-ttu-id="544dc-178">Адаптивная карта C #</span><span class="sxs-lookup"><span data-stu-id="544dc-178">Adaptive card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)

## <a name="hero-card"></a><span data-ttu-id="544dc-179">Карта hero</span><span class="sxs-lookup"><span data-stu-id="544dc-179">Hero card</span></span>

<span data-ttu-id="544dc-180">Карта, которая обычно содержит одно большое изображение, одну или несколько кнопок и текст.</span><span class="sxs-lookup"><span data-stu-id="544dc-180">A card that typically contains a single large image, one or more buttons and text.</span></span>

### <a name="support-for-hero-cards"></a><span data-ttu-id="544dc-181">Поддержка карт-героев</span><span class="sxs-lookup"><span data-stu-id="544dc-181">Support for hero cards</span></span>

| <span data-ttu-id="544dc-182">Боты в teams</span><span class="sxs-lookup"><span data-stu-id="544dc-182">Bots in Teams</span></span> | <span data-ttu-id="544dc-183">Расширения для сообщений</span><span class="sxs-lookup"><span data-stu-id="544dc-183">Messaging Extensions</span></span>  | <span data-ttu-id="544dc-184">Соединители</span><span class="sxs-lookup"><span data-stu-id="544dc-184">Connectors</span></span> | <span data-ttu-id="544dc-185">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="544dc-185">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="544dc-186">✔</span><span class="sxs-lookup"><span data-stu-id="544dc-186">✔</span></span> | <span data-ttu-id="544dc-187">✔</span><span class="sxs-lookup"><span data-stu-id="544dc-187">✔</span></span> | <span data-ttu-id="544dc-188">✖</span><span class="sxs-lookup"><span data-stu-id="544dc-188">✖</span></span> | <span data-ttu-id="544dc-189">✔</span><span class="sxs-lookup"><span data-stu-id="544dc-189">✔</span></span> |

### <a name="properties-of-a-hero-card"></a><span data-ttu-id="544dc-190">Свойства карты-героя</span><span class="sxs-lookup"><span data-stu-id="544dc-190">Properties of a hero card</span></span>

| <span data-ttu-id="544dc-191">Свойство</span><span class="sxs-lookup"><span data-stu-id="544dc-191">Property</span></span> | <span data-ttu-id="544dc-192">Тип</span><span class="sxs-lookup"><span data-stu-id="544dc-192">Type</span></span>  | <span data-ttu-id="544dc-193">Описание</span><span class="sxs-lookup"><span data-stu-id="544dc-193">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="544dc-194">title</span><span class="sxs-lookup"><span data-stu-id="544dc-194">title</span></span> | <span data-ttu-id="544dc-195">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="544dc-195">Rich text</span></span> | <span data-ttu-id="544dc-196">Название карты.</span><span class="sxs-lookup"><span data-stu-id="544dc-196">Title of the card.</span></span> <span data-ttu-id="544dc-197">Максимум 2 строки.</span><span class="sxs-lookup"><span data-stu-id="544dc-197">Maximum 2 lines.</span></span> |
| <span data-ttu-id="544dc-198">субтитры</span><span class="sxs-lookup"><span data-stu-id="544dc-198">subtitle</span></span> | <span data-ttu-id="544dc-199">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="544dc-199">Rich text</span></span> | <span data-ttu-id="544dc-200">Субтитр карты.</span><span class="sxs-lookup"><span data-stu-id="544dc-200">Subtitle of the card.</span></span> <span data-ttu-id="544dc-201">Максимум 2 строки.</span><span class="sxs-lookup"><span data-stu-id="544dc-201">Maximum 2 lines.</span></span>|
| <span data-ttu-id="544dc-202">текст</span><span class="sxs-lookup"><span data-stu-id="544dc-202">text</span></span> | <span data-ttu-id="544dc-203">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="544dc-203">Rich text</span></span> | <span data-ttu-id="544dc-204">Текст отображается под субтитром; см. [форматирование карт](~/task-modules-and-cards/cards/cards-format.md) для параметров форматирования.</span><span class="sxs-lookup"><span data-stu-id="544dc-204">Text appears under the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options.</span></span> |
| <span data-ttu-id="544dc-205">изображения</span><span class="sxs-lookup"><span data-stu-id="544dc-205">images</span></span> | <span data-ttu-id="544dc-206">Массив изображений</span><span class="sxs-lookup"><span data-stu-id="544dc-206">Array of images</span></span> | <span data-ttu-id="544dc-207">Изображение, отображаемого в верхней части карты.</span><span class="sxs-lookup"><span data-stu-id="544dc-207">Image displayed at top of card.</span></span> <span data-ttu-id="544dc-208">Соотношение аспектов 16:9.</span><span class="sxs-lookup"><span data-stu-id="544dc-208">Aspect ratio 16:9.</span></span> |
| <span data-ttu-id="544dc-209">кнопки</span><span class="sxs-lookup"><span data-stu-id="544dc-209">buttons</span></span> | <span data-ttu-id="544dc-210">Массив объектов действий</span><span class="sxs-lookup"><span data-stu-id="544dc-210">Array of action objects</span></span> | <span data-ttu-id="544dc-211">Набор действий, применимых к текущей карте.</span><span class="sxs-lookup"><span data-stu-id="544dc-211">Set of actions applicable to the current card.</span></span> <span data-ttu-id="544dc-212">Максимум 6.</span><span class="sxs-lookup"><span data-stu-id="544dc-212">Maximum 6.</span></span> |
| <span data-ttu-id="544dc-213">нажмите кнопку</span><span class="sxs-lookup"><span data-stu-id="544dc-213">tap</span></span> | <span data-ttu-id="544dc-214">Объект Action</span><span class="sxs-lookup"><span data-stu-id="544dc-214">Action object</span></span> | <span data-ttu-id="544dc-215">Это действие будет активировано, когда пользователь нажмет на карточку.</span><span class="sxs-lookup"><span data-stu-id="544dc-215">This action will be activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-hero-card"></a><span data-ttu-id="544dc-216">Пример карточки героя</span><span class="sxs-lookup"><span data-stu-id="544dc-216">Example of a hero card</span></span>

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

### <a name="additional-information-on-hero-cards"></a><span data-ttu-id="544dc-218">Дополнительные сведения о картах-героях</span><span class="sxs-lookup"><span data-stu-id="544dc-218">Additional information on hero cards</span></span>

<span data-ttu-id="544dc-219">Ссылка на Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="544dc-219">Bot Framework reference:</span></span>

* [<span data-ttu-id="544dc-220">Узел карточки героя</span><span class="sxs-lookup"><span data-stu-id="544dc-220">Hero card Node</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-a-hero-card&preserve-view=true)
* [<span data-ttu-id="544dc-221">Карта героя C #</span><span class="sxs-lookup"><span data-stu-id="544dc-221">Hero card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-hero-card&preserve-view=true)

## <a name="list-card"></a><span data-ttu-id="544dc-222">Карта списка</span><span class="sxs-lookup"><span data-stu-id="544dc-222">List card</span></span>

<span data-ttu-id="544dc-223">Карточка списка была добавлена teams для предоставления функций, не в том, что может предоставить коллекция списков.</span><span class="sxs-lookup"><span data-stu-id="544dc-223">The list card has been added by Teams to provide functions beyond what the list collection can provide.</span></span> <span data-ttu-id="544dc-224">Карта списка содержит список элементов для прокрутки.</span><span class="sxs-lookup"><span data-stu-id="544dc-224">The list card provides a scrolling list of items.</span></span>

### <a name="support-for-list-cards"></a><span data-ttu-id="544dc-225">Поддержка карт списка</span><span class="sxs-lookup"><span data-stu-id="544dc-225">Support for list cards</span></span>

| <span data-ttu-id="544dc-226">Боты в teams</span><span class="sxs-lookup"><span data-stu-id="544dc-226">Bots in Teams</span></span> | <span data-ttu-id="544dc-227">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="544dc-227">Messaging extensions</span></span>  | <span data-ttu-id="544dc-228">Соединители</span><span class="sxs-lookup"><span data-stu-id="544dc-228">Connectors</span></span> | <span data-ttu-id="544dc-229">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="544dc-229">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="544dc-230">✔</span><span class="sxs-lookup"><span data-stu-id="544dc-230">✔</span></span> | <span data-ttu-id="544dc-231">✖</span><span class="sxs-lookup"><span data-stu-id="544dc-231">✖</span></span> | <span data-ttu-id="544dc-232">✖</span><span class="sxs-lookup"><span data-stu-id="544dc-232">✖</span></span> |<span data-ttu-id="544dc-233">✔</span><span class="sxs-lookup"><span data-stu-id="544dc-233">✔</span></span> |

### <a name="properties-of-a-list-card"></a><span data-ttu-id="544dc-234">Свойства карты списка</span><span class="sxs-lookup"><span data-stu-id="544dc-234">Properties of a list card</span></span>

| <span data-ttu-id="544dc-235">Свойство</span><span class="sxs-lookup"><span data-stu-id="544dc-235">Property</span></span> | <span data-ttu-id="544dc-236">Тип</span><span class="sxs-lookup"><span data-stu-id="544dc-236">Type</span></span>  | <span data-ttu-id="544dc-237">Описание</span><span class="sxs-lookup"><span data-stu-id="544dc-237">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="544dc-238">title</span><span class="sxs-lookup"><span data-stu-id="544dc-238">title</span></span> | <span data-ttu-id="544dc-239">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="544dc-239">Rich text</span></span> | <span data-ttu-id="544dc-240">Название карты.</span><span class="sxs-lookup"><span data-stu-id="544dc-240">Title of the card.</span></span> <span data-ttu-id="544dc-241">Максимум 2 строки.</span><span class="sxs-lookup"><span data-stu-id="544dc-241">Maximum 2 lines.</span></span>|
| <span data-ttu-id="544dc-242">items</span><span class="sxs-lookup"><span data-stu-id="544dc-242">items</span></span> | <span data-ttu-id="544dc-243">Массив элементов списка</span><span class="sxs-lookup"><span data-stu-id="544dc-243">Array of list items</span></span>  ||
| <span data-ttu-id="544dc-244">кнопки</span><span class="sxs-lookup"><span data-stu-id="544dc-244">buttons</span></span> | <span data-ttu-id="544dc-245">Массив объектов действий</span><span class="sxs-lookup"><span data-stu-id="544dc-245">Array of action objects</span></span> | <span data-ttu-id="544dc-246">Набор действий, применимых к текущей карте.</span><span class="sxs-lookup"><span data-stu-id="544dc-246">Set of actions applicable to the current card.</span></span> <span data-ttu-id="544dc-247">Максимум 6.</span><span class="sxs-lookup"><span data-stu-id="544dc-247">Maximum 6.</span></span> |

### <a name="example-of-a-list-card"></a><span data-ttu-id="544dc-248">Пример карты списка</span><span class="sxs-lookup"><span data-stu-id="544dc-248">Example of a list card</span></span>

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

## <a name="office-365-connector-card"></a><span data-ttu-id="544dc-249">Соединитечная карта Office 365</span><span class="sxs-lookup"><span data-stu-id="544dc-249">Office 365 connector card</span></span>

<span data-ttu-id="544dc-250">Соединитечная карта Office 365 поддерживается в Teams, а не в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="544dc-250">The Office 365 Connector card is supported in Teams, not in Bot Framework.</span></span> <span data-ttu-id="544dc-251">Эта карта обеспечивает гибкую схему с несколькими разделами, полями, изображениями и действиями.</span><span class="sxs-lookup"><span data-stu-id="544dc-251">This card provides a flexible layout with multiple sections, fields, images, and actions.</span></span> <span data-ttu-id="544dc-252">Эта карта инкапсулирует соединителем карту, чтобы она была использована ботами.</span><span class="sxs-lookup"><span data-stu-id="544dc-252">This card encapsulates a connector card so that it can be used by bots.</span></span> <span data-ttu-id="544dc-253">В разделе заметки можно узнать о различиях между соединитеными картами и картой O365.</span><span class="sxs-lookup"><span data-stu-id="544dc-253">See the notes section for differences between connector cards and the O365 card.</span></span>

### <a name="support-for-office-365-connector-cards"></a><span data-ttu-id="544dc-254">Поддержка соединитеных карт Office 365</span><span class="sxs-lookup"><span data-stu-id="544dc-254">Support for Office 365 connector cards</span></span>

| <span data-ttu-id="544dc-255">Боты в teams</span><span class="sxs-lookup"><span data-stu-id="544dc-255">Bots in Teams</span></span> | <span data-ttu-id="544dc-256">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="544dc-256">Messaging extensions</span></span>  | <span data-ttu-id="544dc-257">Соединители</span><span class="sxs-lookup"><span data-stu-id="544dc-257">Connectors</span></span> | <span data-ttu-id="544dc-258">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="544dc-258">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="544dc-259">✔</span><span class="sxs-lookup"><span data-stu-id="544dc-259">✔</span></span> | <span data-ttu-id="544dc-260">✔</span><span class="sxs-lookup"><span data-stu-id="544dc-260">✔</span></span> | <span data-ttu-id="544dc-261">✔</span><span class="sxs-lookup"><span data-stu-id="544dc-261">✔</span></span> | <span data-ttu-id="544dc-262">✖</span><span class="sxs-lookup"><span data-stu-id="544dc-262">✖</span></span> |

### <a name="properties-of-the-office-365-connector-card"></a><span data-ttu-id="544dc-263">Свойства соединитеной карты Office 365</span><span class="sxs-lookup"><span data-stu-id="544dc-263">Properties of the Office 365 connector card</span></span>

| <span data-ttu-id="544dc-264">Свойство</span><span class="sxs-lookup"><span data-stu-id="544dc-264">Property</span></span> | <span data-ttu-id="544dc-265">Тип</span><span class="sxs-lookup"><span data-stu-id="544dc-265">Type</span></span>  | <span data-ttu-id="544dc-266">Описание</span><span class="sxs-lookup"><span data-stu-id="544dc-266">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="544dc-267">title</span><span class="sxs-lookup"><span data-stu-id="544dc-267">title</span></span> | <span data-ttu-id="544dc-268">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="544dc-268">Rich text</span></span> | <span data-ttu-id="544dc-269">Название карты.</span><span class="sxs-lookup"><span data-stu-id="544dc-269">Title of the card.</span></span> <span data-ttu-id="544dc-270">Максимум 2 строки.</span><span class="sxs-lookup"><span data-stu-id="544dc-270">Maximum 2 lines.</span></span> |
| <span data-ttu-id="544dc-271">summary</span><span class="sxs-lookup"><span data-stu-id="544dc-271">summary</span></span> | <span data-ttu-id="544dc-272">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="544dc-272">Rich text</span></span> | <span data-ttu-id="544dc-273">Сводка карты.</span><span class="sxs-lookup"><span data-stu-id="544dc-273">Summary of the card.</span></span> <span data-ttu-id="544dc-274">Максимум 2 строки.</span><span class="sxs-lookup"><span data-stu-id="544dc-274">Maximum 2 lines.</span></span> |
| <span data-ttu-id="544dc-275">текст</span><span class="sxs-lookup"><span data-stu-id="544dc-275">text</span></span> | <span data-ttu-id="544dc-276">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="544dc-276">Rich text</span></span> | <span data-ttu-id="544dc-277">Текст отображается под субтитром; см. [форматирование карт](~/task-modules-and-cards/cards/cards-format.md) для параметров форматирования.</span><span class="sxs-lookup"><span data-stu-id="544dc-277">Text appears under the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options.</span></span> |
| <span data-ttu-id="544dc-278">themeColor</span><span class="sxs-lookup"><span data-stu-id="544dc-278">themeColor</span></span> | <span data-ttu-id="544dc-279">Строка HEX</span><span class="sxs-lookup"><span data-stu-id="544dc-279">HEX string</span></span> | <span data-ttu-id="544dc-280">Цвет, который переопределяет accentColor, предоставленный из манифеста приложения.</span><span class="sxs-lookup"><span data-stu-id="544dc-280">Color that overrides the accentColor provided from the application manifest.</span></span> |

### <a name="notes-on-the-office-365-connector-card"></a><span data-ttu-id="544dc-281">Заметки на соединители office 365</span><span class="sxs-lookup"><span data-stu-id="544dc-281">Notes on the Office 365 connector card</span></span>

<span data-ttu-id="544dc-282">Соединитетельные карточки Office 365 правильно функционируют в Microsoft Teams, включая [действия ActionCard.](/outlook/actionable-messages/card-reference#actioncard-action)</span><span class="sxs-lookup"><span data-stu-id="544dc-282">Office 365 connector cards function properly in Microsoft Teams, including [ActionCard actions](/outlook/actionable-messages/card-reference#actioncard-action).</span></span>

<span data-ttu-id="544dc-283">Одним из важных отличий между использованием соединитеных карт из соединитетеля и использованием соединитеных карт в боте является обработка действий карт.</span><span class="sxs-lookup"><span data-stu-id="544dc-283">One important difference between using connector cards from a connector and using connector cards in your bot is the handling of card actions.</span></span>

* <span data-ttu-id="544dc-284">Для соединитетеля конечная точка получает полезное сообщение карточки через HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="544dc-284">For a connector, the endpoint receives the card payload through HTTP POST.</span></span>
* <span data-ttu-id="544dc-285">Для бота действие запускает действие, которое отправляет боту только ID действия и `HttpPOST` `invoke` тело.</span><span class="sxs-lookup"><span data-stu-id="544dc-285">For a bot, the `HttpPOST` action triggers an `invoke` activity that sends only the action ID and body to the bot.</span></span>

<span data-ttu-id="544dc-286">Каждая соединитечная карта может отображать не более 10 разделов, а каждый раздел может содержать не более 5 изображений и 5 действий.</span><span class="sxs-lookup"><span data-stu-id="544dc-286">Each connector card can display a maximum of 10 sections, and each section can contain a maximum of 5 images and 5 actions.</span></span>

> [!NOTE]
> <span data-ttu-id="544dc-287">Дополнительные разделы, изображения или действия в сообщении не отображаются.</span><span class="sxs-lookup"><span data-stu-id="544dc-287">Any additional sections, images, or actions in a message will not appear.</span></span>

<span data-ttu-id="544dc-288">Все текстовые поля поддерживают Markdown и HTML.</span><span class="sxs-lookup"><span data-stu-id="544dc-288">All text fields support Markdown and HTML.</span></span> <span data-ttu-id="544dc-289">Вы можете контролировать, какие разделы используют Markdown или HTML, установив `markdown` свойство в сообщении.</span><span class="sxs-lookup"><span data-stu-id="544dc-289">You can control which sections use Markdown or HTML by setting the `markdown` property in a message.</span></span> <span data-ttu-id="544dc-290">По умолчанию установлено значение; если вы хотите использовать `markdown` `true` HTML вместо этого, установите `markdown` значение `false` .</span><span class="sxs-lookup"><span data-stu-id="544dc-290">By default, `markdown` is set to `true`; if you want to use HTML instead, set `markdown` to `false`.</span></span>

<span data-ttu-id="544dc-291">Если указать `themeColor` свойство, оно переопределит `accentColor` свойство в манифесте приложения.</span><span class="sxs-lookup"><span data-stu-id="544dc-291">If you specify the `themeColor` property, it overrides the `accentColor` property in the app manifest.</span></span>

<span data-ttu-id="544dc-292">Чтобы указать стиль `activityImage` визуализации, можно задать `activityImageType` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="544dc-292">To specify the rendering style for `activityImage`, you can set `activityImageType` as follows:</span></span>

| <span data-ttu-id="544dc-293">Значение</span><span class="sxs-lookup"><span data-stu-id="544dc-293">Value</span></span> | <span data-ttu-id="544dc-294">Описание</span><span class="sxs-lookup"><span data-stu-id="544dc-294">Description</span></span> |
| --- | --- |
| `avatar` | <span data-ttu-id="544dc-295">По умолчанию; `activityImage` будет обрезана как круг.</span><span class="sxs-lookup"><span data-stu-id="544dc-295">Default; `activityImage` will be cropped as a circle.</span></span> |
| `article` | <span data-ttu-id="544dc-296">`activityImage` будет отображаться в качестве прямоугольника и сохранит соотношение аспектов.</span><span class="sxs-lookup"><span data-stu-id="544dc-296">`activityImage` will be displayed as a rectangle and retain its aspect ratio.</span></span> |

<span data-ttu-id="544dc-297">Другие сведения о свойствах карт соединители см. в справке к карточке [actionable message.](/outlook/actionable-messages/card-reference)</span><span class="sxs-lookup"><span data-stu-id="544dc-297">For all other details about connector card properties, see the [Actionable message card reference](/outlook/actionable-messages/card-reference).</span></span> <span data-ttu-id="544dc-298">Единственными свойствами карт соединители, которые microsoft Teams в настоящее время не поддерживает, являются:</span><span class="sxs-lookup"><span data-stu-id="544dc-298">The only connector card properties that Microsoft Teams does not currently support are as follows:</span></span>

* `heroImage`
* `hideOriginalBody`
* <span data-ttu-id="544dc-299">`startGroup` (всегда рассматривается как `true` в Teams)</span><span class="sxs-lookup"><span data-stu-id="544dc-299">`startGroup` (always treated as `true` in Teams)</span></span>
* `originator`
* `correlationId`

### <a name="example-of-an-office-365-connector-card"></a><span data-ttu-id="544dc-300">Пример соединитеной карты Office 365</span><span class="sxs-lookup"><span data-stu-id="544dc-300">Example of an Office 365 connector card</span></span>

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

## <a name="receipt-card"></a><span data-ttu-id="544dc-301">Карта получения</span><span class="sxs-lookup"><span data-stu-id="544dc-301">Receipt card</span></span>

<span data-ttu-id="544dc-302">Teams поддерживает карточку получения.</span><span class="sxs-lookup"><span data-stu-id="544dc-302">Teams supports receipt card.</span></span> <span data-ttu-id="544dc-303">Это карточка, которая позволяет боту предоставлять пользователю квитанцию.</span><span class="sxs-lookup"><span data-stu-id="544dc-303">It is a card that enables a bot to provide a receipt to the user.</span></span> <span data-ttu-id="544dc-304">Обычно он содержит список элементов, которые необходимо включить в квитанцию, например налоговые и общие сведения.</span><span class="sxs-lookup"><span data-stu-id="544dc-304">It typically contains the list of items to include on the receipt, such as tax and total information.</span></span>

### <a name="support-for-receipt-cards"></a><span data-ttu-id="544dc-305">Поддержка карт получения</span><span class="sxs-lookup"><span data-stu-id="544dc-305">Support for receipt cards</span></span>

| <span data-ttu-id="544dc-306">Боты в teams</span><span class="sxs-lookup"><span data-stu-id="544dc-306">Bots in Teams</span></span> | <span data-ttu-id="544dc-307">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="544dc-307">Messaging extensions</span></span>  | <span data-ttu-id="544dc-308">Соединители</span><span class="sxs-lookup"><span data-stu-id="544dc-308">Connectors</span></span> | <span data-ttu-id="544dc-309">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="544dc-309">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="544dc-310">✔</span><span class="sxs-lookup"><span data-stu-id="544dc-310">✔</span></span> | <span data-ttu-id="544dc-311">✔</span><span class="sxs-lookup"><span data-stu-id="544dc-311">✔</span></span> | <span data-ttu-id="544dc-312">✖</span><span class="sxs-lookup"><span data-stu-id="544dc-312">✖</span></span> | <span data-ttu-id="544dc-313">✔</span><span class="sxs-lookup"><span data-stu-id="544dc-313">✔</span></span> |

### <a name="example-of-a-receipt-card"></a><span data-ttu-id="544dc-314">Пример карты получения</span><span class="sxs-lookup"><span data-stu-id="544dc-314">Example of a receipt card</span></span>

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

### <a name="additional-information-on-receipt-cards"></a><span data-ttu-id="544dc-316">Дополнительные сведения о карточках получения</span><span class="sxs-lookup"><span data-stu-id="544dc-316">Additional information on receipt cards</span></span>

<span data-ttu-id="544dc-317">Ссылка на Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="544dc-317">Bot Framework reference:</span></span>

* [<span data-ttu-id="544dc-318">Узел карты получения</span><span class="sxs-lookup"><span data-stu-id="544dc-318">Receipt card Node</span></span>](/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="544dc-319">Карта получения C #</span><span class="sxs-lookup"><span data-stu-id="544dc-319">Receipt card C#</span></span>](/dotnet/api/microsoft.bot.schema.receiptcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="signin-card"></a><span data-ttu-id="544dc-320">Карточка Signin</span><span class="sxs-lookup"><span data-stu-id="544dc-320">Signin card</span></span>

<span data-ttu-id="544dc-321">Карта Signin позволяет боту запрашивать вход пользователя.</span><span class="sxs-lookup"><span data-stu-id="544dc-321">Signin card enables a bot to request a user to sign in.</span></span> <span data-ttu-id="544dc-322">Поддерживается в Teams в несколько иной форме, чем в bot Framework.</span><span class="sxs-lookup"><span data-stu-id="544dc-322">Supported in Teams in a slightly different form than is found in the Bot Framework.</span></span> <span data-ttu-id="544dc-323">Карточка signin в Teams похожа на карточку signin в bot Framework, за исключением того, что карточка signin в Teams поддерживает только два действия: `signin` и `openUrl` .</span><span class="sxs-lookup"><span data-stu-id="544dc-323">The signin card in Teams is similar to the signin card in the Bot Framework except that the signin card in Teams only supports two actions: `signin` and `openUrl`.</span></span>

<span data-ttu-id="544dc-324">Действие **signin можно** использовать с любой карты в Teams, а не только с карты signin.</span><span class="sxs-lookup"><span data-stu-id="544dc-324">The **signin action** can be used from any card in Teams, not just the signin card.</span></span> <span data-ttu-id="544dc-325">Дополнительные сведения о проверке подлинности см. в [материале Microsoft Teams authentication flow for bots.](~/bots/how-to/authentication/auth-flow-bot.md)</span><span class="sxs-lookup"><span data-stu-id="544dc-325">For more details on authentication, see [Microsoft Teams authentication flow for bots](~/bots/how-to/authentication/auth-flow-bot.md).</span></span>

### <a name="support-for-signin-cards"></a><span data-ttu-id="544dc-326">Поддержка карт Signin</span><span class="sxs-lookup"><span data-stu-id="544dc-326">Support for Signin cards</span></span>

| <span data-ttu-id="544dc-327">Боты в teams</span><span class="sxs-lookup"><span data-stu-id="544dc-327">Bots in Teams</span></span> | <span data-ttu-id="544dc-328">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="544dc-328">Messaging extensions</span></span>  | <span data-ttu-id="544dc-329">Соединители</span><span class="sxs-lookup"><span data-stu-id="544dc-329">Connectors</span></span> | <span data-ttu-id="544dc-330">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="544dc-330">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="544dc-331">✔</span><span class="sxs-lookup"><span data-stu-id="544dc-331">✔</span></span> | <span data-ttu-id="544dc-332">✖</span><span class="sxs-lookup"><span data-stu-id="544dc-332">✖</span></span> | <span data-ttu-id="544dc-333">✖</span><span class="sxs-lookup"><span data-stu-id="544dc-333">✖</span></span> | <span data-ttu-id="544dc-334">✔</span><span class="sxs-lookup"><span data-stu-id="544dc-334">✔</span></span> |

### <a name="additional-information-on-signin-cards"></a><span data-ttu-id="544dc-335">Дополнительные сведения о подписных карточках</span><span class="sxs-lookup"><span data-stu-id="544dc-335">Additional information on signin cards</span></span>

<span data-ttu-id="544dc-336">Ссылка на Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="544dc-336">Bot Framework reference:</span></span>

* [<span data-ttu-id="544dc-337">Узел карточки Signin</span><span class="sxs-lookup"><span data-stu-id="544dc-337">Signin card Node</span></span>](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="544dc-338">Signin card C #</span><span class="sxs-lookup"><span data-stu-id="544dc-338">Signin card C#</span></span>](/dotnet/api/microsoft.bot.schema.signincard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="thumbnail-card"></a><span data-ttu-id="544dc-339">Карта эскиза</span><span class="sxs-lookup"><span data-stu-id="544dc-339">Thumbnail card</span></span>

<span data-ttu-id="544dc-340">Карточка, которая обычно содержит одно изображение эскиза, одну или несколько кнопок и текст.</span><span class="sxs-lookup"><span data-stu-id="544dc-340">A card that typically contains a single thumbnail image, one or more buttons, and text.</span></span>

### <a name="support-for-thumbnail-cards"></a><span data-ttu-id="544dc-341">Поддержка карт эскизов</span><span class="sxs-lookup"><span data-stu-id="544dc-341">Support for thumbnail cards</span></span>

| <span data-ttu-id="544dc-342">Боты в teams</span><span class="sxs-lookup"><span data-stu-id="544dc-342">Bots in Teams</span></span> | <span data-ttu-id="544dc-343">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="544dc-343">Messaging extensions</span></span>  | <span data-ttu-id="544dc-344">Соединители</span><span class="sxs-lookup"><span data-stu-id="544dc-344">Connectors</span></span> | <span data-ttu-id="544dc-345">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="544dc-345">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="544dc-346">✔</span><span class="sxs-lookup"><span data-stu-id="544dc-346">✔</span></span> | <span data-ttu-id="544dc-347">✔</span><span class="sxs-lookup"><span data-stu-id="544dc-347">✔</span></span> | <span data-ttu-id="544dc-348">✖</span><span class="sxs-lookup"><span data-stu-id="544dc-348">✖</span></span> | <span data-ttu-id="544dc-349">✔</span><span class="sxs-lookup"><span data-stu-id="544dc-349">✔</span></span> |

![Пример карты эскиза](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a><span data-ttu-id="544dc-351">Свойства карты эскиза</span><span class="sxs-lookup"><span data-stu-id="544dc-351">Properties of a thumbnail card</span></span>

| <span data-ttu-id="544dc-352">Свойство</span><span class="sxs-lookup"><span data-stu-id="544dc-352">Property</span></span> | <span data-ttu-id="544dc-353">Тип</span><span class="sxs-lookup"><span data-stu-id="544dc-353">Type</span></span>  | <span data-ttu-id="544dc-354">Описание</span><span class="sxs-lookup"><span data-stu-id="544dc-354">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="544dc-355">title</span><span class="sxs-lookup"><span data-stu-id="544dc-355">title</span></span> | <span data-ttu-id="544dc-356">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="544dc-356">Rich text</span></span> | <span data-ttu-id="544dc-357">Название карты.</span><span class="sxs-lookup"><span data-stu-id="544dc-357">Title of the card.</span></span> <span data-ttu-id="544dc-358">Максимум 2 строки.</span><span class="sxs-lookup"><span data-stu-id="544dc-358">Maximum 2 lines.</span></span>|
| <span data-ttu-id="544dc-359">субтитры</span><span class="sxs-lookup"><span data-stu-id="544dc-359">subtitle</span></span> | <span data-ttu-id="544dc-360">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="544dc-360">Rich text</span></span> | <span data-ttu-id="544dc-361">Субтитр карты.</span><span class="sxs-lookup"><span data-stu-id="544dc-361">Subtitle of the card.</span></span> <span data-ttu-id="544dc-362">Максимум 2 строки.</span><span class="sxs-lookup"><span data-stu-id="544dc-362">Maximum 2 lines.</span></span>|
| <span data-ttu-id="544dc-363">текст</span><span class="sxs-lookup"><span data-stu-id="544dc-363">text</span></span> | <span data-ttu-id="544dc-364">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="544dc-364">Rich text</span></span> | <span data-ttu-id="544dc-365">Текст отображается под субтитром; см. [форматирование карт](~/task-modules-and-cards/cards/cards-format.md) для параметров форматирования.</span><span class="sxs-lookup"><span data-stu-id="544dc-365">Text appears under the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options.</span></span> |
| <span data-ttu-id="544dc-366">изображения</span><span class="sxs-lookup"><span data-stu-id="544dc-366">images</span></span> | <span data-ttu-id="544dc-367">Массив изображений</span><span class="sxs-lookup"><span data-stu-id="544dc-367">Array of images</span></span> | <span data-ttu-id="544dc-368">Изображение, отображаемого в верхней части карты.</span><span class="sxs-lookup"><span data-stu-id="544dc-368">Image displayed at top of card.</span></span> <span data-ttu-id="544dc-369">Отношение аспектов 1:1 (квадрат).</span><span class="sxs-lookup"><span data-stu-id="544dc-369">Aspect ratio 1:1 (square).</span></span> |
| <span data-ttu-id="544dc-370">кнопки</span><span class="sxs-lookup"><span data-stu-id="544dc-370">buttons</span></span> | <span data-ttu-id="544dc-371">Массив объектов действий</span><span class="sxs-lookup"><span data-stu-id="544dc-371">Array of action objects</span></span> | <span data-ttu-id="544dc-372">Набор действий, применимых к текущей карте.</span><span class="sxs-lookup"><span data-stu-id="544dc-372">Set of actions applicable to the current card.</span></span> <span data-ttu-id="544dc-373">Максимум 6.</span><span class="sxs-lookup"><span data-stu-id="544dc-373">Maximum 6.</span></span> |
| <span data-ttu-id="544dc-374">нажмите кнопку</span><span class="sxs-lookup"><span data-stu-id="544dc-374">tap</span></span> | <span data-ttu-id="544dc-375">Объект Action</span><span class="sxs-lookup"><span data-stu-id="544dc-375">Action object</span></span> | <span data-ttu-id="544dc-376">Это действие будет активировано, когда пользователь нажмет на карточку.</span><span class="sxs-lookup"><span data-stu-id="544dc-376">This action will be activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-thumbnail-card"></a><span data-ttu-id="544dc-377">Пример карты эскиза</span><span class="sxs-lookup"><span data-stu-id="544dc-377">Example of a thumbnail card</span></span>

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

### <a name="additional-information"></a><span data-ttu-id="544dc-378">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="544dc-378">Additional information</span></span>

<span data-ttu-id="544dc-379">Ссылка на Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="544dc-379">Bot Framework reference:</span></span>

* [<span data-ttu-id="544dc-380">Узел карты эскиза</span><span class="sxs-lookup"><span data-stu-id="544dc-380">Thumbnail card Node</span></span>](/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="544dc-381">Эскиз карты C #</span><span class="sxs-lookup"><span data-stu-id="544dc-381">Thumbnail card C#</span></span>](/dotnet/api/microsoft.bot.schema.thumbnailcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="card-collections"></a><span data-ttu-id="544dc-382">Коллекции карт</span><span class="sxs-lookup"><span data-stu-id="544dc-382">Card collections</span></span>

<span data-ttu-id="544dc-383">Teams поддерживает коллекции карт.</span><span class="sxs-lookup"><span data-stu-id="544dc-383">Teams supports Card collections.</span></span>

<span data-ttu-id="544dc-384">Коллекции карт: `builder.AttachmentLayout.carousel` и `builder.AttachmentLayout.list` .</span><span class="sxs-lookup"><span data-stu-id="544dc-384">Card collections: `builder.AttachmentLayout.carousel` and `builder.AttachmentLayout.list`.</span></span> <span data-ttu-id="544dc-385">Эти коллекции содержат адаптивные, герой или эскизные карточки.</span><span class="sxs-lookup"><span data-stu-id="544dc-385">These collections contain adaptive, hero, or thumbnail cards.</span></span>

## <a name="carousel-collection"></a><span data-ttu-id="544dc-386">Коллекция Карусель</span><span class="sxs-lookup"><span data-stu-id="544dc-386">Carousel collection</span></span>

<span data-ttu-id="544dc-387">Макет [карусель показывает](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) карусель карт, необязательно с связанными кнопками действия.</span><span class="sxs-lookup"><span data-stu-id="544dc-387">The [carousel layout](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) shows a carousel of cards, optionally with associated action buttons.</span></span>

### <a name="support-for-carousel-collections"></a><span data-ttu-id="544dc-388">Поддержка коллекций карусель</span><span class="sxs-lookup"><span data-stu-id="544dc-388">Support for carousel collections</span></span>

| <span data-ttu-id="544dc-389">Боты в teams</span><span class="sxs-lookup"><span data-stu-id="544dc-389">Bots in Teams</span></span> | <span data-ttu-id="544dc-390">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="544dc-390">Messaging extensions</span></span>  | <span data-ttu-id="544dc-391">Соединители</span><span class="sxs-lookup"><span data-stu-id="544dc-391">Connectors</span></span> | <span data-ttu-id="544dc-392">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="544dc-392">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="544dc-393">✔</span><span class="sxs-lookup"><span data-stu-id="544dc-393">✔</span></span> | <span data-ttu-id="544dc-394">✖</span><span class="sxs-lookup"><span data-stu-id="544dc-394">✖</span></span> | <span data-ttu-id="544dc-395">✖</span><span class="sxs-lookup"><span data-stu-id="544dc-395">✖</span></span> | <span data-ttu-id="544dc-396">✔</span><span class="sxs-lookup"><span data-stu-id="544dc-396">✔</span></span> |

> [!NOTE]
> <span data-ttu-id="544dc-397">Карусель может отображать не более 10 карт на сообщение.</span><span class="sxs-lookup"><span data-stu-id="544dc-397">A carousel can display a maximum of 10 cards per message.</span></span>

### <a name="properties-of-a-carousel-card"></a><span data-ttu-id="544dc-398">Свойства карусели</span><span class="sxs-lookup"><span data-stu-id="544dc-398">Properties of a carousel card</span></span>

<span data-ttu-id="544dc-399">Свойства карусельной карты такие же, как и у карт Hero и Thumbnail.</span><span class="sxs-lookup"><span data-stu-id="544dc-399">Properties of a Carousel card are same as those of the Hero and Thumbnail cards.</span></span>

### <a name="example-of-a-carousel-collection"></a><span data-ttu-id="544dc-400">Пример коллекции карусель</span><span class="sxs-lookup"><span data-stu-id="544dc-400">Example of a carousel collection</span></span>

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

### <a name="syntax-for-carousel-collections"></a><span data-ttu-id="544dc-402">Синтаксис для коллекций карусели</span><span class="sxs-lookup"><span data-stu-id="544dc-402">Syntax for carousel collections</span></span>

`builder.AttachmentLayoutTypes.Carousel`

## <a name="list-collection"></a><span data-ttu-id="544dc-403">Коллекция списков</span><span class="sxs-lookup"><span data-stu-id="544dc-403">List collection</span></span>

### <a name="support-for-list-collections"></a><span data-ttu-id="544dc-404">Поддержка коллекций списков</span><span class="sxs-lookup"><span data-stu-id="544dc-404">Support for list collections</span></span>

<span data-ttu-id="544dc-405">В макете списка показан вертикально сложенный список карт, необязательно связанный с кнопками действия.</span><span class="sxs-lookup"><span data-stu-id="544dc-405">The list layout shows a vertically stacked list of cards, optionally with associated action buttons.</span></span>

| <span data-ttu-id="544dc-406">Боты в teams</span><span class="sxs-lookup"><span data-stu-id="544dc-406">Bots in Teams</span></span> | <span data-ttu-id="544dc-407">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="544dc-407">Messaging extensions</span></span>  | <span data-ttu-id="544dc-408">Соединители</span><span class="sxs-lookup"><span data-stu-id="544dc-408">Connectors</span></span> | <span data-ttu-id="544dc-409">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="544dc-409">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="544dc-410">✔</span><span class="sxs-lookup"><span data-stu-id="544dc-410">✔</span></span> | <span data-ttu-id="544dc-411">✔</span><span class="sxs-lookup"><span data-stu-id="544dc-411">✔</span></span> | <span data-ttu-id="544dc-412">✖</span><span class="sxs-lookup"><span data-stu-id="544dc-412">✖</span></span> | <span data-ttu-id="544dc-413">✔</span><span class="sxs-lookup"><span data-stu-id="544dc-413">✔</span></span> |

### <a name="example-of-a-list-collection"></a><span data-ttu-id="544dc-414">Пример коллекции списков</span><span class="sxs-lookup"><span data-stu-id="544dc-414">Example of a list collection</span></span>

![Пример списка карт](~/assets/images/cards/list.png)

<span data-ttu-id="544dc-416">Свойства такие же, как для карты героя или эскиза.</span><span class="sxs-lookup"><span data-stu-id="544dc-416">Properties are the same as for the hero or thumbnail card.</span></span>

<span data-ttu-id="544dc-417">В списке может отображаться не более 10 карт на сообщение.</span><span class="sxs-lookup"><span data-stu-id="544dc-417">A list can display a maximum of 10 cards per message.</span></span>

> [!NOTE]
> <span data-ttu-id="544dc-418">Некоторые сочетания карт списка еще не поддерживаются на iOS и Android.</span><span class="sxs-lookup"><span data-stu-id="544dc-418">Some combinations of list cards are not yet supported on iOS and Android.</span></span>

### <a name="syntax-for-list-collections"></a><span data-ttu-id="544dc-419">Синтаксис для коллекций списков</span><span class="sxs-lookup"><span data-stu-id="544dc-419">Syntax for list collections</span></span>

`builder.AttachmentLayout.list`

## <a name="cards-not-supported-in-teams"></a><span data-ttu-id="544dc-420">Карты, не поддерживаемые в Teams</span><span class="sxs-lookup"><span data-stu-id="544dc-420">Cards not supported in Teams</span></span>

<span data-ttu-id="544dc-421">Следующие карты реализованы командной структурой, но не поддерживаются teams.</span><span class="sxs-lookup"><span data-stu-id="544dc-421">The following cards are implemented by the Bot Framework, but are NOT supported by Teams.</span></span>

* <span data-ttu-id="544dc-422">Карты анимации</span><span class="sxs-lookup"><span data-stu-id="544dc-422">Animation cards</span></span>
* <span data-ttu-id="544dc-423">Аудиокарты</span><span class="sxs-lookup"><span data-stu-id="544dc-423">Audio cards</span></span>
* <span data-ttu-id="544dc-424">Видеокарты</span><span class="sxs-lookup"><span data-stu-id="544dc-424">Video cards</span></span>
