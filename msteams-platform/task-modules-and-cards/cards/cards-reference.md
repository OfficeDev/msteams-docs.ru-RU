---
title: Справочник по карточкам
description: Описание всех карточек и действий карточек, доступных ботам в Teams
keywords: bots cards reference
ms.topic: reference
ms.openlocfilehash: 839430baa5ce5e8950a21a1472036c6fd96f4edf
ms.sourcegitcommit: 00c657e3bf57d3b92aca7da941cde47a2eeff4d0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/20/2021
ms.locfileid: "49911900"
---
# <a name="cards-reference"></a><span data-ttu-id="c20dd-104">Ссылки на карточки</span><span class="sxs-lookup"><span data-stu-id="c20dd-104">Cards reference</span></span>

<span data-ttu-id="c20dd-105">Карточки, перечисленные в этом разделе, поддерживаются в ботах для Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="c20dd-105">The cards listed in this section are supported in bots for Microsoft Teams.</span></span> <span data-ttu-id="c20dd-106">Они основаны на карточках, определенных в Bot Framework, но Teams не поддерживает все карты Bot Framework и добавил некоторые из них.</span><span class="sxs-lookup"><span data-stu-id="c20dd-106">They are based on cards defined by the Bot Framework, but Teams does not support all Bot Framework cards and has added some of its own.</span></span> <span data-ttu-id="c20dd-107">Различия в ссылках в этом документе называются неявными.</span><span class="sxs-lookup"><span data-stu-id="c20dd-107">Differences are called out in the references in this document.</span></span>

## <a name="card-examples"></a><span data-ttu-id="c20dd-108">Примеры карточки</span><span class="sxs-lookup"><span data-stu-id="c20dd-108">Card examples</span></span>

<span data-ttu-id="c20dd-109">Дополнительные сведения об использовании карточек см. в документации по SDK построитель ботов (v3).</span><span class="sxs-lookup"><span data-stu-id="c20dd-109">You can find additional information on how to use cards in the documentation for the Bot Builder SDK (v3).</span></span> <span data-ttu-id="c20dd-110">Примеры кода также доступны в репозитории Microsoft/BotBuilder-Samples на GitHub.</span><span class="sxs-lookup"><span data-stu-id="c20dd-110">Code samples are also available in the Microsoft/BotBuilder-Samples repository on GitHub.</span></span>

* <span data-ttu-id="c20dd-111">.NET</span><span class="sxs-lookup"><span data-stu-id="c20dd-111">.NET</span></span>
  * [<span data-ttu-id="c20dd-112">Добавление карточек в виде вложений в сообщения</span><span class="sxs-lookup"><span data-stu-id="c20dd-112">Add cards as attachments to messages</span></span>](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments)
  * [<span data-ttu-id="c20dd-113">Пример кода карточек (построитель ботов 3)</span><span class="sxs-lookup"><span data-stu-id="c20dd-113">Cards sample code (Bot Builder v3)</span></span>](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/CSharp/cards-RichCards)
* <span data-ttu-id="c20dd-114">Node.js</span><span class="sxs-lookup"><span data-stu-id="c20dd-114">Node.js</span></span>
  * [<span data-ttu-id="c20dd-115">Добавление карточек в виде вложений в сообщения</span><span class="sxs-lookup"><span data-stu-id="c20dd-115">Add cards as attachments to messages</span></span>](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)
  * [<span data-ttu-id="c20dd-116">Пример кода карточек (построитель ботов 3)</span><span class="sxs-lookup"><span data-stu-id="c20dd-116">Cards sample code (Bot Builder v3)</span></span>](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/Node/cards-RichCards)

## <a name="types-of-cards"></a><span data-ttu-id="c20dd-117">Типы карточек</span><span class="sxs-lookup"><span data-stu-id="c20dd-117">Types of cards</span></span>

<span data-ttu-id="c20dd-118">В этой таблице показаны доступные типы карточек:</span><span class="sxs-lookup"><span data-stu-id="c20dd-118">This table shows the types of cards available to you:</span></span>

| <span data-ttu-id="c20dd-119">Тип карточки</span><span class="sxs-lookup"><span data-stu-id="c20dd-119">Card type</span></span> | <span data-ttu-id="c20dd-120">Description</span><span class="sxs-lookup"><span data-stu-id="c20dd-120">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="c20dd-121">Адаптивная карточка</span><span class="sxs-lookup"><span data-stu-id="c20dd-121">Adaptive card</span></span>](#adaptive-card) | <span data-ttu-id="c20dd-122">Карточка с высокой настройкой, которая может содержать любое сочетание текста, речи, изображений, кнопок и полей ввода.</span><span class="sxs-lookup"><span data-stu-id="c20dd-122">Highly customizable card that can contain any combination of text, speech, images, buttons and input fields.</span></span> |
| [<span data-ttu-id="c20dd-123">Карточка "Главного"</span><span class="sxs-lookup"><span data-stu-id="c20dd-123">Hero card</span></span>](#hero-card) | <span data-ttu-id="c20dd-124">Обычно содержит одно большое изображение, одну или несколько кнопок и небольшой объем текста.</span><span class="sxs-lookup"><span data-stu-id="c20dd-124">Typically contains a single large image, one or more buttons, and a small amount of text.</span></span> |
| [<span data-ttu-id="c20dd-125">Карточка списка</span><span class="sxs-lookup"><span data-stu-id="c20dd-125">List card</span></span>](#list-card) | <span data-ttu-id="c20dd-126">Список прокрутки элементов.</span><span class="sxs-lookup"><span data-stu-id="c20dd-126">A scrolling list of items.</span></span> |
| [<span data-ttu-id="c20dd-127">Карточка соединители Office 365</span><span class="sxs-lookup"><span data-stu-id="c20dd-127">Office 365 connector card</span></span>](#office-365-connector-card) | <span data-ttu-id="c20dd-128">Гибкий макет с несколькими разделами, полями, изображениями и действиями.</span><span class="sxs-lookup"><span data-stu-id="c20dd-128">Flexible layout with multiple sections, fields, images and actions.</span></span> |
| [<span data-ttu-id="c20dd-129">Чековая карта</span><span class="sxs-lookup"><span data-stu-id="c20dd-129">Receipt card</span></span>](#receipt-card) | <span data-ttu-id="c20dd-130">Предоставляет пользователю квитанцию.</span><span class="sxs-lookup"><span data-stu-id="c20dd-130">Provides a receipt to the user.</span></span> |
| [<span data-ttu-id="c20dd-131">Карточка для подписи</span><span class="sxs-lookup"><span data-stu-id="c20dd-131">Signin card</span></span>](#signin-card) | <span data-ttu-id="c20dd-132">Позволяет боту запрашивать вход пользователя.</span><span class="sxs-lookup"><span data-stu-id="c20dd-132">Enables a bot to request that a user sign in.</span></span> |
| [<span data-ttu-id="c20dd-133">Эскиз карточки</span><span class="sxs-lookup"><span data-stu-id="c20dd-133">Thumbnail card</span></span>](#thumbnail-card) | <span data-ttu-id="c20dd-134">Обычно содержит один эскиз, короткий текст и одну или несколько кнопок.</span><span class="sxs-lookup"><span data-stu-id="c20dd-134">Typically contains a single thumbnail image, some short text, and one or more buttons.</span></span> |
| [<span data-ttu-id="c20dd-135">Коллекции карт</span><span class="sxs-lookup"><span data-stu-id="c20dd-135">Card collections</span></span>](#card-collections) | <span data-ttu-id="c20dd-136">Используется для возврата нескольких элементов в одном ответе.</span><span class="sxs-lookup"><span data-stu-id="c20dd-136">Used to return multiple items in a single response.</span></span> |

## <a name="common-properties-for-all-cards"></a><span data-ttu-id="c20dd-137">Общие свойства для всех карточек</span><span class="sxs-lookup"><span data-stu-id="c20dd-137">Common properties for all cards</span></span>

### <a name="inline-card-images"></a><span data-ttu-id="c20dd-138">Inline card images</span><span class="sxs-lookup"><span data-stu-id="c20dd-138">Inline card images</span></span>

<span data-ttu-id="c20dd-139">Карточка может содержать в себе изображение, включив ссылку на общедоступный образ.</span><span class="sxs-lookup"><span data-stu-id="c20dd-139">The card can contain an inline image by including a link to the publicly available image.</span></span> <span data-ttu-id="c20dd-140">В целях производительности настоятельно рекомендуется использовать образ в общедоступных сетях доставки содержимого (CDN).</span><span class="sxs-lookup"><span data-stu-id="c20dd-140">For performance purposes, it is highly recommended you host the image on a public content-delivery network (CDN).</span></span>

<span data-ttu-id="c20dd-141">Изображения масштабются вверх или вниз по размеру, сохраняя пропорции для покрытия области изображения, а затем обрезаются из центра, чтобы получить соответствующие пропорции для карточки.</span><span class="sxs-lookup"><span data-stu-id="c20dd-141">Images are scaled up or down in size while maintaining the aspect ratio to cover the image area, and then cropped from center to achieve the appropriate aspect ratio for the card.</span></span>

<span data-ttu-id="c20dd-142">Изображения должны иметь не более 1024×1024 в формате PNG, JPEG или GIF, а анимированный GIF не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="c20dd-142">Images must be at most 1024×1024, in PNG, JPEG, or GIF format, and animated GIF is not supported.</span></span>

| <span data-ttu-id="c20dd-143">Свойство</span><span class="sxs-lookup"><span data-stu-id="c20dd-143">Property</span></span> | <span data-ttu-id="c20dd-144">Тип</span><span class="sxs-lookup"><span data-stu-id="c20dd-144">Type</span></span>  | <span data-ttu-id="c20dd-145">Описание</span><span class="sxs-lookup"><span data-stu-id="c20dd-145">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c20dd-146">url</span><span class="sxs-lookup"><span data-stu-id="c20dd-146">url</span></span> | <span data-ttu-id="c20dd-147">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="c20dd-147">URL</span></span> | <span data-ttu-id="c20dd-148">URL-адрес HTTPS изображения</span><span class="sxs-lookup"><span data-stu-id="c20dd-148">HTTPS URL to the image</span></span> |
| <span data-ttu-id="c20dd-149">alt</span><span class="sxs-lookup"><span data-stu-id="c20dd-149">alt</span></span> | <span data-ttu-id="c20dd-150">String</span><span class="sxs-lookup"><span data-stu-id="c20dd-150">String</span></span> | <span data-ttu-id="c20dd-151">Доступное описание изображения</span><span class="sxs-lookup"><span data-stu-id="c20dd-151">Accessible description of the image</span></span> |

### <a name="buttons"></a><span data-ttu-id="c20dd-152">Кнопки</span><span class="sxs-lookup"><span data-stu-id="c20dd-152">Buttons</span></span>

<span data-ttu-id="c20dd-153">Кнопки показаны в нижней части карточки.</span><span class="sxs-lookup"><span data-stu-id="c20dd-153">Buttons are shown stacked at the bottom of the card.</span></span> <span data-ttu-id="c20dd-154">Текст кнопки всегда находится в одной строке и будет усечен, если текст превышает ширину кнопки.</span><span class="sxs-lookup"><span data-stu-id="c20dd-154">Button text is always on a single line and will be truncated if the text exceeds the button width.</span></span> <span data-ttu-id="c20dd-155">Дополнительные кнопки, которые выходят за пределы максимального числа, поддерживаемого картой, не будут показаны.</span><span class="sxs-lookup"><span data-stu-id="c20dd-155">Any additional buttons beyond the maximum number supported by the card will not be shown.</span></span>

<span data-ttu-id="c20dd-156">Дополнительные [сведения см.](~/task-modules-and-cards/cards/cards-actions.md) в действиях карточки.</span><span class="sxs-lookup"><span data-stu-id="c20dd-156">See [Card Actions](~/task-modules-and-cards/cards/cards-actions.md) for more information.</span></span>

### <a name="card-formatting"></a><span data-ttu-id="c20dd-157">Форматирование карт</span><span class="sxs-lookup"><span data-stu-id="c20dd-157">Card formatting</span></span>

<span data-ttu-id="c20dd-158">Дополнительные [сведения о форматирование](~/task-modules-and-cards/cards/cards-format.md) текста в карточках см. в документе "Форматирование карточек".</span><span class="sxs-lookup"><span data-stu-id="c20dd-158">See [Card Formatting](~/task-modules-and-cards/cards/cards-format.md) for more information on text formatting in cards.</span></span>

## <a name="adaptive-card"></a><span data-ttu-id="c20dd-159">Адаптивная карточка</span><span class="sxs-lookup"><span data-stu-id="c20dd-159">Adaptive card</span></span>

<span data-ttu-id="c20dd-160">Адаптивная карточка — это настраиваемая карточка, которая может содержать любое сочетание текста, речи, изображений, кнопок и полей ввода.</span><span class="sxs-lookup"><span data-stu-id="c20dd-160">An adaptive card is a customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> <span data-ttu-id="c20dd-161">См. ["Адаптивные карточки" 1.2.0.](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0)</span><span class="sxs-lookup"><span data-stu-id="c20dd-161">See [Adaptive Cards v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span></span>

### <a name="support-for-adaptive-cards"></a><span data-ttu-id="c20dd-162">Поддержка адаптивных карточек</span><span class="sxs-lookup"><span data-stu-id="c20dd-162">Support for adaptive cards</span></span>

| <span data-ttu-id="c20dd-163">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="c20dd-163">Bots in Teams</span></span> | <span data-ttu-id="c20dd-164">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="c20dd-164">Messaging extensions</span></span>  | <span data-ttu-id="c20dd-165">Соединители</span><span class="sxs-lookup"><span data-stu-id="c20dd-165">Connectors</span></span> | <span data-ttu-id="c20dd-166">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="c20dd-166">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c20dd-167">✔</span><span class="sxs-lookup"><span data-stu-id="c20dd-167">✔</span></span> | <span data-ttu-id="c20dd-168">✔</span><span class="sxs-lookup"><span data-stu-id="c20dd-168">✔</span></span> | <span data-ttu-id="c20dd-169">✖</span><span class="sxs-lookup"><span data-stu-id="c20dd-169">✖</span></span> | <span data-ttu-id="c20dd-170">✔</span><span class="sxs-lookup"><span data-stu-id="c20dd-170">✔</span></span> |

> [!NOTE]
> * <span data-ttu-id="c20dd-171">Платформа Teams поддерживает 1.2 или более ранние возможности адаптивной карточки.</span><span class="sxs-lookup"><span data-stu-id="c20dd-171">Teams platform supports v1.2 or earlier of Adaptive card features.</span></span>
> * <span data-ttu-id="c20dd-172">Элементы мультимедиа в настоящее время не поддерживаются в адаптивной карточке 1.2 на платформе Teams.</span><span class="sxs-lookup"><span data-stu-id="c20dd-172">Media elements are currently not supported in Adaptive card v1.2 on the Teams platform.</span></span>

### <a name="example-of-an-adaptive-card"></a><span data-ttu-id="c20dd-173">Пример адаптивной карточки</span><span class="sxs-lookup"><span data-stu-id="c20dd-173">Example of an adaptive card</span></span>

![Пример адаптивной карточки](~/assets/images/cards/adaptivecard.png)

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

#### <a name="additional-information-on-adaptive-cards"></a><span data-ttu-id="c20dd-175">Дополнительные сведения об адаптивных карточках</span><span class="sxs-lookup"><span data-stu-id="c20dd-175">Additional information on adaptive cards</span></span>

* [<span data-ttu-id="c20dd-176">Обзор адаптивных карточек</span><span class="sxs-lookup"><span data-stu-id="c20dd-176">Adaptive cards overview</span></span>](/adaptive-cards/)
* [<span data-ttu-id="c20dd-177">Действия адаптивной карточки в Teams</span><span class="sxs-lookup"><span data-stu-id="c20dd-177">Adaptive card actions in Teams</span></span>](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)

## <a name="hero-card"></a><span data-ttu-id="c20dd-178">Карточка "Главного"</span><span class="sxs-lookup"><span data-stu-id="c20dd-178">Hero card</span></span>

<span data-ttu-id="c20dd-179">Карточка, которая обычно содержит одно большое изображение, одну или несколько кнопок и текста.</span><span class="sxs-lookup"><span data-stu-id="c20dd-179">A card that typically contains a single large image, one or more buttons and text.</span></span>

### <a name="support-for-hero-cards"></a><span data-ttu-id="c20dd-180">Поддержка главного карточка</span><span class="sxs-lookup"><span data-stu-id="c20dd-180">Support for hero cards</span></span>

| <span data-ttu-id="c20dd-181">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="c20dd-181">Bots in Teams</span></span> | <span data-ttu-id="c20dd-182">Расширения для сообщений</span><span class="sxs-lookup"><span data-stu-id="c20dd-182">Messaging Extensions</span></span>  | <span data-ttu-id="c20dd-183">Соединители</span><span class="sxs-lookup"><span data-stu-id="c20dd-183">Connectors</span></span> | <span data-ttu-id="c20dd-184">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="c20dd-184">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c20dd-185">✔</span><span class="sxs-lookup"><span data-stu-id="c20dd-185">✔</span></span> | <span data-ttu-id="c20dd-186">✔</span><span class="sxs-lookup"><span data-stu-id="c20dd-186">✔</span></span> | <span data-ttu-id="c20dd-187">✖</span><span class="sxs-lookup"><span data-stu-id="c20dd-187">✖</span></span> | <span data-ttu-id="c20dd-188">✔</span><span class="sxs-lookup"><span data-stu-id="c20dd-188">✔</span></span> |

### <a name="properties-of-a-hero-card"></a><span data-ttu-id="c20dd-189">Свойства главного карточки</span><span class="sxs-lookup"><span data-stu-id="c20dd-189">Properties of a hero card</span></span>

| <span data-ttu-id="c20dd-190">Свойство</span><span class="sxs-lookup"><span data-stu-id="c20dd-190">Property</span></span> | <span data-ttu-id="c20dd-191">Тип</span><span class="sxs-lookup"><span data-stu-id="c20dd-191">Type</span></span>  | <span data-ttu-id="c20dd-192">Описание</span><span class="sxs-lookup"><span data-stu-id="c20dd-192">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c20dd-193">title</span><span class="sxs-lookup"><span data-stu-id="c20dd-193">title</span></span> | <span data-ttu-id="c20dd-194">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="c20dd-194">Rich text</span></span> | <span data-ttu-id="c20dd-195">Название карточки.</span><span class="sxs-lookup"><span data-stu-id="c20dd-195">Title of the card.</span></span> <span data-ttu-id="c20dd-196">Не более 2 строк.</span><span class="sxs-lookup"><span data-stu-id="c20dd-196">Maximum 2 lines.</span></span> |
| <span data-ttu-id="c20dd-197">subtitle</span><span class="sxs-lookup"><span data-stu-id="c20dd-197">subtitle</span></span> | <span data-ttu-id="c20dd-198">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="c20dd-198">Rich text</span></span> | <span data-ttu-id="c20dd-199">Субтитры на карточке.</span><span class="sxs-lookup"><span data-stu-id="c20dd-199">Subtitle of the card.</span></span> <span data-ttu-id="c20dd-200">Не более 2 строк.</span><span class="sxs-lookup"><span data-stu-id="c20dd-200">Maximum 2 lines.</span></span>|
| <span data-ttu-id="c20dd-201">текст</span><span class="sxs-lookup"><span data-stu-id="c20dd-201">text</span></span> | <span data-ttu-id="c20dd-202">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="c20dd-202">Rich text</span></span> | <span data-ttu-id="c20dd-203">Текст отображается сразу под субтитром; См. [параметры форматирования](~/task-modules-and-cards/cards/cards-format.md) карточки.</span><span class="sxs-lookup"><span data-stu-id="c20dd-203">Text appears just below the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options.</span></span> |
| <span data-ttu-id="c20dd-204">images</span><span class="sxs-lookup"><span data-stu-id="c20dd-204">images</span></span> | <span data-ttu-id="c20dd-205">Массив изображений</span><span class="sxs-lookup"><span data-stu-id="c20dd-205">Array of images</span></span> | <span data-ttu-id="c20dd-206">Изображение, отображаемого в верхней части карточки.</span><span class="sxs-lookup"><span data-stu-id="c20dd-206">Image displayed at top of card.</span></span> <span data-ttu-id="c20dd-207">Пропорции 16:9.</span><span class="sxs-lookup"><span data-stu-id="c20dd-207">Aspect ratio 16:9.</span></span> |
| <span data-ttu-id="c20dd-208">buttons</span><span class="sxs-lookup"><span data-stu-id="c20dd-208">buttons</span></span> | <span data-ttu-id="c20dd-209">Массив объектов действий</span><span class="sxs-lookup"><span data-stu-id="c20dd-209">Array of action objects</span></span> | <span data-ttu-id="c20dd-210">Набор действий, применимых к текущей карточке.</span><span class="sxs-lookup"><span data-stu-id="c20dd-210">Set of actions applicable to the current card.</span></span> <span data-ttu-id="c20dd-211">Максимум 6.</span><span class="sxs-lookup"><span data-stu-id="c20dd-211">Maximum 6.</span></span> |
| <span data-ttu-id="c20dd-212">tap</span><span class="sxs-lookup"><span data-stu-id="c20dd-212">tap</span></span> | <span data-ttu-id="c20dd-213">Объект Action</span><span class="sxs-lookup"><span data-stu-id="c20dd-213">Action object</span></span> | <span data-ttu-id="c20dd-214">Это действие будет активировано, когда пользователь коснитесь самой карточки.</span><span class="sxs-lookup"><span data-stu-id="c20dd-214">This action will be activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-hero-card"></a><span data-ttu-id="c20dd-215">Пример главного карточки</span><span class="sxs-lookup"><span data-stu-id="c20dd-215">Example of a hero card</span></span>

![Пример главного карточки](~/assets/images/cards/hero.png)

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

### <a name="additional-information-on-hero-cards"></a><span data-ttu-id="c20dd-217">Дополнительные сведения о главного карточках</span><span class="sxs-lookup"><span data-stu-id="c20dd-217">Additional information on hero cards</span></span>

<span data-ttu-id="c20dd-218">Справка по Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="c20dd-218">Bot Framework reference:</span></span>

* [<span data-ttu-id="c20dd-219">Узел главного карточки</span><span class="sxs-lookup"><span data-stu-id="c20dd-219">Hero card Node</span></span>](https://docs.microsoft.com/javascript/api/botframework-schema/herocard)
* [<span data-ttu-id="c20dd-220">Главный карточка C #</span><span class="sxs-lookup"><span data-stu-id="c20dd-220">Hero card C#</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.herocard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="list-card"></a><span data-ttu-id="c20dd-221">Карточка списка</span><span class="sxs-lookup"><span data-stu-id="c20dd-221">List card</span></span>

<span data-ttu-id="c20dd-222">Карточка списка была добавлена в Teams для предоставления функций, которые выходят за рамки того, что может предоставить коллекция списков.</span><span class="sxs-lookup"><span data-stu-id="c20dd-222">The list card has been added by Teams to provide functions beyond what the list collection can provide.</span></span> <span data-ttu-id="c20dd-223">На карточке списка содержится прокручивающийся список элементов.</span><span class="sxs-lookup"><span data-stu-id="c20dd-223">The list card provides a scrolling list of items.</span></span>

### <a name="support-for-list-cards"></a><span data-ttu-id="c20dd-224">Поддержка карточек списков</span><span class="sxs-lookup"><span data-stu-id="c20dd-224">Support for list cards</span></span>

| <span data-ttu-id="c20dd-225">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="c20dd-225">Bots in Teams</span></span> | <span data-ttu-id="c20dd-226">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="c20dd-226">Messaging extensions</span></span>  | <span data-ttu-id="c20dd-227">Соединители</span><span class="sxs-lookup"><span data-stu-id="c20dd-227">Connectors</span></span> | <span data-ttu-id="c20dd-228">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="c20dd-228">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c20dd-229">✔</span><span class="sxs-lookup"><span data-stu-id="c20dd-229">✔</span></span> | <span data-ttu-id="c20dd-230">✖</span><span class="sxs-lookup"><span data-stu-id="c20dd-230">✖</span></span> | <span data-ttu-id="c20dd-231">✖</span><span class="sxs-lookup"><span data-stu-id="c20dd-231">✖</span></span> |<span data-ttu-id="c20dd-232">✔</span><span class="sxs-lookup"><span data-stu-id="c20dd-232">✔</span></span> |

### <a name="properties-of-a-list-card"></a><span data-ttu-id="c20dd-233">Свойства карточки списка</span><span class="sxs-lookup"><span data-stu-id="c20dd-233">Properties of a list card</span></span>

| <span data-ttu-id="c20dd-234">Свойство</span><span class="sxs-lookup"><span data-stu-id="c20dd-234">Property</span></span> | <span data-ttu-id="c20dd-235">Тип</span><span class="sxs-lookup"><span data-stu-id="c20dd-235">Type</span></span>  | <span data-ttu-id="c20dd-236">Описание</span><span class="sxs-lookup"><span data-stu-id="c20dd-236">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c20dd-237">title</span><span class="sxs-lookup"><span data-stu-id="c20dd-237">title</span></span> | <span data-ttu-id="c20dd-238">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="c20dd-238">Rich text</span></span> | <span data-ttu-id="c20dd-239">Название карточки.</span><span class="sxs-lookup"><span data-stu-id="c20dd-239">Title of the card.</span></span> <span data-ttu-id="c20dd-240">Не более 2 строк.</span><span class="sxs-lookup"><span data-stu-id="c20dd-240">Maximum 2 lines.</span></span>|
| <span data-ttu-id="c20dd-241">items</span><span class="sxs-lookup"><span data-stu-id="c20dd-241">items</span></span> | <span data-ttu-id="c20dd-242">Массив элементов списка</span><span class="sxs-lookup"><span data-stu-id="c20dd-242">Array of list items</span></span>  ||
| <span data-ttu-id="c20dd-243">buttons</span><span class="sxs-lookup"><span data-stu-id="c20dd-243">buttons</span></span> | <span data-ttu-id="c20dd-244">Массив объектов действий</span><span class="sxs-lookup"><span data-stu-id="c20dd-244">Array of action objects</span></span> | <span data-ttu-id="c20dd-245">Набор действий, применимых к текущей карточке.</span><span class="sxs-lookup"><span data-stu-id="c20dd-245">Set of actions applicable to the current card.</span></span> <span data-ttu-id="c20dd-246">Максимум 6.</span><span class="sxs-lookup"><span data-stu-id="c20dd-246">Maximum 6.</span></span> |

### <a name="example-of-a-list-card"></a><span data-ttu-id="c20dd-247">Пример карточки списка</span><span class="sxs-lookup"><span data-stu-id="c20dd-247">Example of a list card</span></span>

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

## <a name="office-365-connector-card"></a><span data-ttu-id="c20dd-248">Карточка соединители Office 365</span><span class="sxs-lookup"><span data-stu-id="c20dd-248">Office 365 connector card</span></span>

<span data-ttu-id="c20dd-249">Карточка соединители Office 365 поддерживается в Teams, а не в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="c20dd-249">The Office 365 Connector card is supported in Teams, not in Bot Framework.</span></span> <span data-ttu-id="c20dd-250">Эта карточка предоставляет гибкий макет с несколькими разделами, полями, изображениями и действиями.</span><span class="sxs-lookup"><span data-stu-id="c20dd-250">This card provides a flexible layout with multiple sections, fields, images, and actions.</span></span> <span data-ttu-id="c20dd-251">Эта карточка инкапсулирует карточку соединителя, чтобы ее могли использовать боты.</span><span class="sxs-lookup"><span data-stu-id="c20dd-251">This card encapsulates a connector card so that it can be used by bots.</span></span> <span data-ttu-id="c20dd-252">Различия между карточками соединители и картой O365 см. в разделе примечаний.</span><span class="sxs-lookup"><span data-stu-id="c20dd-252">See the notes section for differences between connector cards and the O365 card.</span></span>

### <a name="support-for-office-365-connector-cards"></a><span data-ttu-id="c20dd-253">Поддержка карточек соединители Office 365</span><span class="sxs-lookup"><span data-stu-id="c20dd-253">Support for Office 365 connector cards</span></span>

| <span data-ttu-id="c20dd-254">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="c20dd-254">Bots in Teams</span></span> | <span data-ttu-id="c20dd-255">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="c20dd-255">Messaging extensions</span></span>  | <span data-ttu-id="c20dd-256">Соединители</span><span class="sxs-lookup"><span data-stu-id="c20dd-256">Connectors</span></span> | <span data-ttu-id="c20dd-257">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="c20dd-257">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c20dd-258">✔</span><span class="sxs-lookup"><span data-stu-id="c20dd-258">✔</span></span> | <span data-ttu-id="c20dd-259">✔</span><span class="sxs-lookup"><span data-stu-id="c20dd-259">✔</span></span> | <span data-ttu-id="c20dd-260">✔</span><span class="sxs-lookup"><span data-stu-id="c20dd-260">✔</span></span> | <span data-ttu-id="c20dd-261">✖</span><span class="sxs-lookup"><span data-stu-id="c20dd-261">✖</span></span> |

### <a name="properties-of-the-office-365-connector-card"></a><span data-ttu-id="c20dd-262">Свойства карточки соединители Office 365</span><span class="sxs-lookup"><span data-stu-id="c20dd-262">Properties of the Office 365 connector card</span></span>

| <span data-ttu-id="c20dd-263">Свойство</span><span class="sxs-lookup"><span data-stu-id="c20dd-263">Property</span></span> | <span data-ttu-id="c20dd-264">Тип</span><span class="sxs-lookup"><span data-stu-id="c20dd-264">Type</span></span>  | <span data-ttu-id="c20dd-265">Описание</span><span class="sxs-lookup"><span data-stu-id="c20dd-265">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c20dd-266">title</span><span class="sxs-lookup"><span data-stu-id="c20dd-266">title</span></span> | <span data-ttu-id="c20dd-267">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="c20dd-267">Rich text</span></span> | <span data-ttu-id="c20dd-268">Название карточки.</span><span class="sxs-lookup"><span data-stu-id="c20dd-268">Title of the card.</span></span> <span data-ttu-id="c20dd-269">Не более 2 строк.</span><span class="sxs-lookup"><span data-stu-id="c20dd-269">Maximum 2 lines.</span></span> |
| <span data-ttu-id="c20dd-270">summary</span><span class="sxs-lookup"><span data-stu-id="c20dd-270">summary</span></span> | <span data-ttu-id="c20dd-271">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="c20dd-271">Rich text</span></span> | <span data-ttu-id="c20dd-272">Сводка карточки.</span><span class="sxs-lookup"><span data-stu-id="c20dd-272">Summary of the card.</span></span> <span data-ttu-id="c20dd-273">Не более 2 строк.</span><span class="sxs-lookup"><span data-stu-id="c20dd-273">Maximum 2 lines.</span></span> |
| <span data-ttu-id="c20dd-274">текст</span><span class="sxs-lookup"><span data-stu-id="c20dd-274">text</span></span> | <span data-ttu-id="c20dd-275">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="c20dd-275">Rich text</span></span> | <span data-ttu-id="c20dd-276">Текст отображается сразу под субтитром; См. [параметры форматирования](~/task-modules-and-cards/cards/cards-format.md) карточки.</span><span class="sxs-lookup"><span data-stu-id="c20dd-276">Text appears just below the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options.</span></span> |
| <span data-ttu-id="c20dd-277">themeColor</span><span class="sxs-lookup"><span data-stu-id="c20dd-277">themeColor</span></span> | <span data-ttu-id="c20dd-278">Строка HEX</span><span class="sxs-lookup"><span data-stu-id="c20dd-278">HEX string</span></span> | <span data-ttu-id="c20dd-279">Цвет, который переопределит accentColor, предоставленный из манифеста приложения.</span><span class="sxs-lookup"><span data-stu-id="c20dd-279">Color that overrides the accentColor provided from the application manifest.</span></span> |

### <a name="notes-on-the-office-365-connector-card"></a><span data-ttu-id="c20dd-280">Примечания на карточке соединители Office 365</span><span class="sxs-lookup"><span data-stu-id="c20dd-280">Notes on the Office 365 connector card</span></span>

<span data-ttu-id="c20dd-281">Карточки соединители Office 365 правильно работают в Microsoft Teams, включая [действия ActionCard.](/outlook/actionable-messages/card-reference#actioncard-action)</span><span class="sxs-lookup"><span data-stu-id="c20dd-281">Office 365 connector cards function properly in Microsoft Teams, including [ActionCard actions](/outlook/actionable-messages/card-reference#actioncard-action).</span></span>

<span data-ttu-id="c20dd-282">Одно из важных отличий между использованием карточек соединители из соединители и карточек соединители в боте обработка действий карт.</span><span class="sxs-lookup"><span data-stu-id="c20dd-282">One important difference between using connector cards from a connector and using connector cards in your bot is the handling of card actions.</span></span>

* <span data-ttu-id="c20dd-283">Для соединители конечная точка получает полезной нагрузки карточки через HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="c20dd-283">For a connector, the endpoint receives the card payload via HTTP POST.</span></span>
* <span data-ttu-id="c20dd-284">Для бота действие запускает действие, которое отправляет боту только ИД и `HttpPOST` `invoke` тело действия.</span><span class="sxs-lookup"><span data-stu-id="c20dd-284">For a bot, the `HttpPOST` action triggers an `invoke` activity that sends only the action ID and body to the bot.</span></span>

<span data-ttu-id="c20dd-285">Каждая карточка соединители может отображать не более 10 разделов, а каждый раздел может содержать не более 5 изображений и 5 действий.</span><span class="sxs-lookup"><span data-stu-id="c20dd-285">Each connector card can display a maximum of 10 sections, and each section can contain a maximum of 5 images and 5 actions.</span></span>

> [!NOTE]
> <span data-ttu-id="c20dd-286">Дополнительные разделы, изображения или действия в сообщении не отображаются.</span><span class="sxs-lookup"><span data-stu-id="c20dd-286">Any additional sections, images, or actions in a message will not appear.</span></span>

<span data-ttu-id="c20dd-287">Все текстовые поля поддерживают Markdown и HTML.</span><span class="sxs-lookup"><span data-stu-id="c20dd-287">All text fields support Markdown and HTML.</span></span> <span data-ttu-id="c20dd-288">Вы можете управлять тем, в каких разделах используется Markdown или HTML, установив `markdown` свойство в сообщении.</span><span class="sxs-lookup"><span data-stu-id="c20dd-288">You can control which sections use Markdown or HTML by setting the `markdown` property in a message.</span></span> <span data-ttu-id="c20dd-289">По умолчанию установлено значение ; если вы хотите использовать `markdown` `true` HTML, установите `markdown` значение `false` .</span><span class="sxs-lookup"><span data-stu-id="c20dd-289">By default, `markdown` is set to `true`; if you want to use HTML instead, set `markdown` to `false`.</span></span>

<span data-ttu-id="c20dd-290">Если указать `themeColor` свойство, оно переопределит `accentColor` свойство в манифесте приложения.</span><span class="sxs-lookup"><span data-stu-id="c20dd-290">If you specify the `themeColor` property, it overrides the `accentColor` property in the app manifest.</span></span>

<span data-ttu-id="c20dd-291">Чтобы указать стиль отрисовки, `activityImage` можно `activityImageType` задать:</span><span class="sxs-lookup"><span data-stu-id="c20dd-291">To specify the rendering style for `activityImage`, you can set `activityImageType` as follows:</span></span>

| <span data-ttu-id="c20dd-292">Значение</span><span class="sxs-lookup"><span data-stu-id="c20dd-292">Value</span></span> | <span data-ttu-id="c20dd-293">Описание</span><span class="sxs-lookup"><span data-stu-id="c20dd-293">Description</span></span> |
| --- | --- |
| `avatar` | <span data-ttu-id="c20dd-294">По умолчанию; `activityImage` будет обрезана в круге.</span><span class="sxs-lookup"><span data-stu-id="c20dd-294">Default; `activityImage` will be cropped as a circle.</span></span> |
| `article` | <span data-ttu-id="c20dd-295">`activityImage` будет отображаться в качестве прямоугольника и сохранять его пропорции.</span><span class="sxs-lookup"><span data-stu-id="c20dd-295">`activityImage` will be displayed as a rectangle and retain its aspect ratio.</span></span> |

<span data-ttu-id="c20dd-296">Все остальные сведения о свойствах карточки соединители см. в справочнике по карточкам сообщений с [действиями.](/outlook/actionable-messages/card-reference)</span><span class="sxs-lookup"><span data-stu-id="c20dd-296">For all other details about connector card properties, see the [Actionable message card reference](/outlook/actionable-messages/card-reference).</span></span> <span data-ttu-id="c20dd-297">Единственными свойствами карточки соединитела, которые в настоящее время не поддерживаются Microsoft Teams, являются:</span><span class="sxs-lookup"><span data-stu-id="c20dd-297">The only connector card properties that Microsoft Teams does not currently support are as follows:</span></span>

* `heroImage`
* `hideOriginalBody`
* <span data-ttu-id="c20dd-298">`startGroup` (всегда рассматривается как `true` в Teams)</span><span class="sxs-lookup"><span data-stu-id="c20dd-298">`startGroup` (always treated as `true` in Teams)</span></span>
* `originator`
* `correlationId`

### <a name="example-of-an-office-365-connector-card"></a><span data-ttu-id="c20dd-299">Пример карточки соединители Office 365</span><span class="sxs-lookup"><span data-stu-id="c20dd-299">Example of an Office 365 connector card</span></span>

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

## <a name="receipt-card"></a><span data-ttu-id="c20dd-300">Чековая карта</span><span class="sxs-lookup"><span data-stu-id="c20dd-300">Receipt card</span></span>

<span data-ttu-id="c20dd-301">Teams поддерживает карточку квитанции.</span><span class="sxs-lookup"><span data-stu-id="c20dd-301">Teams supports receipt card.</span></span> <span data-ttu-id="c20dd-302">Это карточка, которая позволяет боту предоставлять пользователю квитанцию.</span><span class="sxs-lookup"><span data-stu-id="c20dd-302">It is a card that enables a bot to provide a receipt to the user.</span></span> <span data-ttu-id="c20dd-303">Как правило, он содержит список элементов, которые необходимо включить в квитанцию, например сведения о налогах и совокупной информации.</span><span class="sxs-lookup"><span data-stu-id="c20dd-303">It typically contains the list of items to include on the receipt, such as tax and total information.</span></span>

### <a name="support-for-receipt-cards"></a><span data-ttu-id="c20dd-304">Поддержка квитанций</span><span class="sxs-lookup"><span data-stu-id="c20dd-304">Support for receipt cards</span></span>

| <span data-ttu-id="c20dd-305">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="c20dd-305">Bots in Teams</span></span> | <span data-ttu-id="c20dd-306">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="c20dd-306">Messaging extensions</span></span>  | <span data-ttu-id="c20dd-307">Соединители</span><span class="sxs-lookup"><span data-stu-id="c20dd-307">Connectors</span></span> | <span data-ttu-id="c20dd-308">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="c20dd-308">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c20dd-309">✔</span><span class="sxs-lookup"><span data-stu-id="c20dd-309">✔</span></span> | <span data-ttu-id="c20dd-310">✔</span><span class="sxs-lookup"><span data-stu-id="c20dd-310">✔</span></span> | <span data-ttu-id="c20dd-311">✖</span><span class="sxs-lookup"><span data-stu-id="c20dd-311">✖</span></span> | <span data-ttu-id="c20dd-312">✔</span><span class="sxs-lookup"><span data-stu-id="c20dd-312">✔</span></span> |

### <a name="example-of-a-receipt-card"></a><span data-ttu-id="c20dd-313">Пример карты квитанции</span><span class="sxs-lookup"><span data-stu-id="c20dd-313">Example of a receipt card</span></span>

![Пример карты квитанции](~/assets/images/cards/receipt.png)

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

### <a name="additional-information-on-receipt-cards"></a><span data-ttu-id="c20dd-315">Дополнительные сведения о карточках квитанций</span><span class="sxs-lookup"><span data-stu-id="c20dd-315">Additional information on receipt cards</span></span>

<span data-ttu-id="c20dd-316">Справка по Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="c20dd-316">Bot Framework reference:</span></span>

* [<span data-ttu-id="c20dd-317">Узел карточки квитанции</span><span class="sxs-lookup"><span data-stu-id="c20dd-317">Receipt card Node</span></span>](https://docs.microsoft.com/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="c20dd-318">Чековая карта C #</span><span class="sxs-lookup"><span data-stu-id="c20dd-318">Receipt card C#</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.receiptcard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="signin-card"></a><span data-ttu-id="c20dd-319">Карточка для подписи</span><span class="sxs-lookup"><span data-stu-id="c20dd-319">Signin card</span></span>

<span data-ttu-id="c20dd-320">Карточка для подписи позволяет боту запрашивать вход пользователя.</span><span class="sxs-lookup"><span data-stu-id="c20dd-320">Signin card enables a bot to request a user to sign in.</span></span> <span data-ttu-id="c20dd-321">Поддерживается в Teams в несколько другом формате, чем в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="c20dd-321">Supported in Teams in a slightly different form than is found in the Bot Framework.</span></span> <span data-ttu-id="c20dd-322">Карточка для регистрации в Teams похожа на карточку для регистрации в Bot Framework, за исключением того, что карточка для регистрации в Teams поддерживает только два действия: `signin` и `openUrl` .</span><span class="sxs-lookup"><span data-stu-id="c20dd-322">The signin card in Teams is similar to the signin card in the Bot Framework except that the signin card in Teams only supports two actions: `signin` and `openUrl`.</span></span>

<span data-ttu-id="c20dd-323">Действие *для регистрации можно* использовать с любой карточки в Teams, а не только с карточки для регистрации.</span><span class="sxs-lookup"><span data-stu-id="c20dd-323">The *signin action* can be used from any card in Teams, not just the signin card.</span></span> <span data-ttu-id="c20dd-324">Дополнительные сведения о проверке подлинности см. в потоке проверки [подлинности Microsoft Teams для ботов.](~/bots/how-to/authentication/auth-flow-bot.md)</span><span class="sxs-lookup"><span data-stu-id="c20dd-324">For more details on authentication, see [Microsoft Teams authentication flow for bots](~/bots/how-to/authentication/auth-flow-bot.md).</span></span>

### <a name="support-for-signin-cards"></a><span data-ttu-id="c20dd-325">Поддержка карточек для регистрации</span><span class="sxs-lookup"><span data-stu-id="c20dd-325">Support for Signin cards</span></span>

| <span data-ttu-id="c20dd-326">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="c20dd-326">Bots in Teams</span></span> | <span data-ttu-id="c20dd-327">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="c20dd-327">Messaging extensions</span></span>  | <span data-ttu-id="c20dd-328">Соединители</span><span class="sxs-lookup"><span data-stu-id="c20dd-328">Connectors</span></span> | <span data-ttu-id="c20dd-329">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="c20dd-329">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c20dd-330">✔</span><span class="sxs-lookup"><span data-stu-id="c20dd-330">✔</span></span> | <span data-ttu-id="c20dd-331">✖</span><span class="sxs-lookup"><span data-stu-id="c20dd-331">✖</span></span> | <span data-ttu-id="c20dd-332">✖</span><span class="sxs-lookup"><span data-stu-id="c20dd-332">✖</span></span> | <span data-ttu-id="c20dd-333">✔</span><span class="sxs-lookup"><span data-stu-id="c20dd-333">✔</span></span> |

### <a name="additional-information-on-signin-cards"></a><span data-ttu-id="c20dd-334">Дополнительные сведения о карточках для регистрации</span><span class="sxs-lookup"><span data-stu-id="c20dd-334">Additional information on signin cards</span></span>

<span data-ttu-id="c20dd-335">Справка по Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="c20dd-335">Bot Framework reference:</span></span>

* [<span data-ttu-id="c20dd-336">Узел карточки для подписи</span><span class="sxs-lookup"><span data-stu-id="c20dd-336">Signin card Node</span></span>](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="c20dd-337">Карточка для подписи C #</span><span class="sxs-lookup"><span data-stu-id="c20dd-337">Signin card C#</span></span>](/dotnet/api/microsoft.bot.connector.signincard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="thumbnail-card"></a><span data-ttu-id="c20dd-338">Эскиз карточки</span><span class="sxs-lookup"><span data-stu-id="c20dd-338">Thumbnail card</span></span>

<span data-ttu-id="c20dd-339">Карточка, которая обычно содержит один эскиз, одну или несколько кнопок и текст.</span><span class="sxs-lookup"><span data-stu-id="c20dd-339">A card that typically contains a single thumbnail image, one or more buttons, and text.</span></span>

### <a name="support-for-thumbnail-cards"></a><span data-ttu-id="c20dd-340">Поддержка эскизов карточек</span><span class="sxs-lookup"><span data-stu-id="c20dd-340">Support for thumbnail cards</span></span>

| <span data-ttu-id="c20dd-341">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="c20dd-341">Bots in Teams</span></span> | <span data-ttu-id="c20dd-342">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="c20dd-342">Messaging extensions</span></span>  | <span data-ttu-id="c20dd-343">Соединители</span><span class="sxs-lookup"><span data-stu-id="c20dd-343">Connectors</span></span> | <span data-ttu-id="c20dd-344">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="c20dd-344">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c20dd-345">✔</span><span class="sxs-lookup"><span data-stu-id="c20dd-345">✔</span></span> | <span data-ttu-id="c20dd-346">✔</span><span class="sxs-lookup"><span data-stu-id="c20dd-346">✔</span></span> | <span data-ttu-id="c20dd-347">✖</span><span class="sxs-lookup"><span data-stu-id="c20dd-347">✖</span></span> | <span data-ttu-id="c20dd-348">✔</span><span class="sxs-lookup"><span data-stu-id="c20dd-348">✔</span></span> |

![Пример карточки эскиза](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a><span data-ttu-id="c20dd-350">Свойства карточки эскиза</span><span class="sxs-lookup"><span data-stu-id="c20dd-350">Properties of a thumbnail card</span></span>

| <span data-ttu-id="c20dd-351">Свойство</span><span class="sxs-lookup"><span data-stu-id="c20dd-351">Property</span></span> | <span data-ttu-id="c20dd-352">Тип</span><span class="sxs-lookup"><span data-stu-id="c20dd-352">Type</span></span>  | <span data-ttu-id="c20dd-353">Описание</span><span class="sxs-lookup"><span data-stu-id="c20dd-353">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c20dd-354">title</span><span class="sxs-lookup"><span data-stu-id="c20dd-354">title</span></span> | <span data-ttu-id="c20dd-355">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="c20dd-355">Rich text</span></span> | <span data-ttu-id="c20dd-356">Название карточки.</span><span class="sxs-lookup"><span data-stu-id="c20dd-356">Title of the card.</span></span> <span data-ttu-id="c20dd-357">Не более 2 строк.</span><span class="sxs-lookup"><span data-stu-id="c20dd-357">Maximum 2 lines.</span></span>|
| <span data-ttu-id="c20dd-358">subtitle</span><span class="sxs-lookup"><span data-stu-id="c20dd-358">subtitle</span></span> | <span data-ttu-id="c20dd-359">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="c20dd-359">Rich text</span></span> | <span data-ttu-id="c20dd-360">Субтитры на карточке.</span><span class="sxs-lookup"><span data-stu-id="c20dd-360">Subtitle of the card.</span></span> <span data-ttu-id="c20dd-361">Не более 2 строк.</span><span class="sxs-lookup"><span data-stu-id="c20dd-361">Maximum 2 lines.</span></span>|
| <span data-ttu-id="c20dd-362">текст</span><span class="sxs-lookup"><span data-stu-id="c20dd-362">text</span></span> | <span data-ttu-id="c20dd-363">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="c20dd-363">Rich text</span></span> | <span data-ttu-id="c20dd-364">Текст отображается сразу под субтитром; См. [параметры форматирования](~/task-modules-and-cards/cards/cards-format.md) карточки.</span><span class="sxs-lookup"><span data-stu-id="c20dd-364">Text appears just below the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options.</span></span> |
| <span data-ttu-id="c20dd-365">images</span><span class="sxs-lookup"><span data-stu-id="c20dd-365">images</span></span> | <span data-ttu-id="c20dd-366">Массив изображений</span><span class="sxs-lookup"><span data-stu-id="c20dd-366">Array of images</span></span> | <span data-ttu-id="c20dd-367">Изображение, отображаемого в верхней части карточки.</span><span class="sxs-lookup"><span data-stu-id="c20dd-367">Image displayed at top of card.</span></span> <span data-ttu-id="c20dd-368">Пропорции 1:1 (квадрат).</span><span class="sxs-lookup"><span data-stu-id="c20dd-368">Aspect ratio 1:1 (square).</span></span> |
| <span data-ttu-id="c20dd-369">buttons</span><span class="sxs-lookup"><span data-stu-id="c20dd-369">buttons</span></span> | <span data-ttu-id="c20dd-370">Массив объектов действий</span><span class="sxs-lookup"><span data-stu-id="c20dd-370">Array of action objects</span></span> | <span data-ttu-id="c20dd-371">Набор действий, применимых к текущей карточке.</span><span class="sxs-lookup"><span data-stu-id="c20dd-371">Set of actions applicable to the current card.</span></span> <span data-ttu-id="c20dd-372">Максимум 6.</span><span class="sxs-lookup"><span data-stu-id="c20dd-372">Maximum 6.</span></span> |
| <span data-ttu-id="c20dd-373">tap</span><span class="sxs-lookup"><span data-stu-id="c20dd-373">tap</span></span> | <span data-ttu-id="c20dd-374">Объект Action</span><span class="sxs-lookup"><span data-stu-id="c20dd-374">Action object</span></span> | <span data-ttu-id="c20dd-375">Это действие будет активировано, когда пользователь коснитесь самой карточки.</span><span class="sxs-lookup"><span data-stu-id="c20dd-375">This action will be activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-thumbnail-card"></a><span data-ttu-id="c20dd-376">Пример карточки эскиза</span><span class="sxs-lookup"><span data-stu-id="c20dd-376">Example of a thumbnail card</span></span>

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

### <a name="additional-information"></a><span data-ttu-id="c20dd-377">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="c20dd-377">Additional information</span></span>

<span data-ttu-id="c20dd-378">Справка по Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="c20dd-378">Bot Framework reference:</span></span>

* [<span data-ttu-id="c20dd-379">Узел эскиза карточки</span><span class="sxs-lookup"><span data-stu-id="c20dd-379">Thumbnail card Node</span></span>](https://docs.microsoft.com/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="c20dd-380">Эскиз карточки C #</span><span class="sxs-lookup"><span data-stu-id="c20dd-380">Thumbnail card C#</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.thumbnailcard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="card-collections"></a><span data-ttu-id="c20dd-381">Коллекции карт</span><span class="sxs-lookup"><span data-stu-id="c20dd-381">Card collections</span></span>

<span data-ttu-id="c20dd-382">Teams поддерживает коллекции карт.</span><span class="sxs-lookup"><span data-stu-id="c20dd-382">Teams supports Card collections.</span></span>

<span data-ttu-id="c20dd-383">Коллекции карт: `builder.AttachmentLayout.carousel` и `builder.AttachmentLayout.list` .</span><span class="sxs-lookup"><span data-stu-id="c20dd-383">Card collections: `builder.AttachmentLayout.carousel` and `builder.AttachmentLayout.list`.</span></span> <span data-ttu-id="c20dd-384">Эти коллекции содержат адаптивные, главного или эскизные карточки.</span><span class="sxs-lookup"><span data-stu-id="c20dd-384">These collections contain adaptive, hero, or thumbnail cards.</span></span>

## <a name="carousel-collection"></a><span data-ttu-id="c20dd-385">Коллекция карусели</span><span class="sxs-lookup"><span data-stu-id="c20dd-385">Carousel collection</span></span>

<span data-ttu-id="c20dd-386">На [макете карусели](/azure/bot-service/dotnet/bot-builder-dotnet-add-rich-card-attachments?view=azure-bot-service-3.0&preserve-view=true) показана карусели карт, при желании с связанными кнопками действий.</span><span class="sxs-lookup"><span data-stu-id="c20dd-386">The [carousel layout](/azure/bot-service/dotnet/bot-builder-dotnet-add-rich-card-attachments?view=azure-bot-service-3.0&preserve-view=true) shows a carousel of cards, optionally with associated action buttons.</span></span>

### <a name="support-for-carousel-collections"></a><span data-ttu-id="c20dd-387">Поддержка коллекций карусели</span><span class="sxs-lookup"><span data-stu-id="c20dd-387">Support for carousel collections</span></span>

| <span data-ttu-id="c20dd-388">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="c20dd-388">Bots in Teams</span></span> | <span data-ttu-id="c20dd-389">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="c20dd-389">Messaging extensions</span></span>  | <span data-ttu-id="c20dd-390">Соединители</span><span class="sxs-lookup"><span data-stu-id="c20dd-390">Connectors</span></span> | <span data-ttu-id="c20dd-391">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="c20dd-391">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c20dd-392">✔</span><span class="sxs-lookup"><span data-stu-id="c20dd-392">✔</span></span> | <span data-ttu-id="c20dd-393">✖</span><span class="sxs-lookup"><span data-stu-id="c20dd-393">✖</span></span> | <span data-ttu-id="c20dd-394">✖</span><span class="sxs-lookup"><span data-stu-id="c20dd-394">✖</span></span> | <span data-ttu-id="c20dd-395">✔</span><span class="sxs-lookup"><span data-stu-id="c20dd-395">✔</span></span> |

> [!NOTE]
> <span data-ttu-id="c20dd-396">Карусель может отображать не более 10 карт на сообщение.</span><span class="sxs-lookup"><span data-stu-id="c20dd-396">A carousel can display a maximum of 10 cards per message.</span></span>

### <a name="properties-of-a-carousel-card"></a><span data-ttu-id="c20dd-397">Свойства карусели</span><span class="sxs-lookup"><span data-stu-id="c20dd-397">Properties of a carousel card</span></span>

<span data-ttu-id="c20dd-398">Свойства карточки карусели такие же, как и у карт "Hero" и "Thumbnail".</span><span class="sxs-lookup"><span data-stu-id="c20dd-398">Properties of a Carousel card are same as those of the Hero and Thumbnail cards.</span></span>

### <a name="example-of-a-carousel-collection"></a><span data-ttu-id="c20dd-399">Пример коллекции карусели</span><span class="sxs-lookup"><span data-stu-id="c20dd-399">Example of a carousel collection</span></span>

![Пример карусели карточек](~/assets/images/cards/carousel.png)

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

### <a name="syntax-for-carousel-collections"></a><span data-ttu-id="c20dd-401">Синтаксис для коллекций карусели</span><span class="sxs-lookup"><span data-stu-id="c20dd-401">Syntax for carousel collections</span></span>

`builder.AttachmentLayoutTypes.Carousel`

## <a name="list-collection"></a><span data-ttu-id="c20dd-402">Коллекция list</span><span class="sxs-lookup"><span data-stu-id="c20dd-402">List collection</span></span>

### <a name="support-for-list-collections"></a><span data-ttu-id="c20dd-403">Поддержка коллекций списков</span><span class="sxs-lookup"><span data-stu-id="c20dd-403">Support for list collections</span></span>

<span data-ttu-id="c20dd-404">В макете списка показан вертикально сложенный список карточек с кнопками, связанными с ними.</span><span class="sxs-lookup"><span data-stu-id="c20dd-404">The list layout shows a vertically stacked list of cards, optionally with associated action buttons.</span></span>

| <span data-ttu-id="c20dd-405">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="c20dd-405">Bots in Teams</span></span> | <span data-ttu-id="c20dd-406">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="c20dd-406">Messaging extensions</span></span>  | <span data-ttu-id="c20dd-407">Соединители</span><span class="sxs-lookup"><span data-stu-id="c20dd-407">Connectors</span></span> | <span data-ttu-id="c20dd-408">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="c20dd-408">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c20dd-409">✔</span><span class="sxs-lookup"><span data-stu-id="c20dd-409">✔</span></span> | <span data-ttu-id="c20dd-410">✔</span><span class="sxs-lookup"><span data-stu-id="c20dd-410">✔</span></span> | <span data-ttu-id="c20dd-411">✖</span><span class="sxs-lookup"><span data-stu-id="c20dd-411">✖</span></span> | <span data-ttu-id="c20dd-412">✔</span><span class="sxs-lookup"><span data-stu-id="c20dd-412">✔</span></span> |

### <a name="example-of-a-list-collection"></a><span data-ttu-id="c20dd-413">Пример коллекции списков</span><span class="sxs-lookup"><span data-stu-id="c20dd-413">Example of a list collection</span></span>

![Пример списка карточек](~/assets/images/cards/list.png)

<span data-ttu-id="c20dd-415">Свойства такие же, как для главного или эскиза карточки.</span><span class="sxs-lookup"><span data-stu-id="c20dd-415">Properties are the same as for the hero or thumbnail card.</span></span>

<span data-ttu-id="c20dd-416">В списке может отображаться не более 10 карт на сообщение.</span><span class="sxs-lookup"><span data-stu-id="c20dd-416">A list can display a maximum of 10 cards per message.</span></span>

> [!NOTE]
> <span data-ttu-id="c20dd-417">Некоторые сочетания карточек списков пока не поддерживаются в iOS и Android.</span><span class="sxs-lookup"><span data-stu-id="c20dd-417">Some combinations of list cards are not yet supported on iOS and Android.</span></span>

### <a name="syntax-for-list-collections"></a><span data-ttu-id="c20dd-418">Синтаксис для коллекций списков</span><span class="sxs-lookup"><span data-stu-id="c20dd-418">Syntax for list collections</span></span>

`builder.AttachmentLayout.list`

## <a name="cards-not-supported-in-teams"></a><span data-ttu-id="c20dd-419">Карточки не поддерживаются в Teams</span><span class="sxs-lookup"><span data-stu-id="c20dd-419">Cards not supported in Teams</span></span>

<span data-ttu-id="c20dd-420">Следующие карточки реализованы в Bot Framework, но НЕ поддерживаются Teams.</span><span class="sxs-lookup"><span data-stu-id="c20dd-420">The following cards are implemented by the Bot Framework, but are NOT supported by Teams.</span></span>

* <span data-ttu-id="c20dd-421">Карты анимации</span><span class="sxs-lookup"><span data-stu-id="c20dd-421">Animation cards</span></span>
* <span data-ttu-id="c20dd-422">Аудиокарты</span><span class="sxs-lookup"><span data-stu-id="c20dd-422">Audio cards</span></span>
* <span data-ttu-id="c20dd-423">Видеокарты</span><span class="sxs-lookup"><span data-stu-id="c20dd-423">Video cards</span></span>
