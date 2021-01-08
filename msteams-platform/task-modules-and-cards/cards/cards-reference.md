---
title: Справочник по карточкам
description: Описание всех карточек и действий карточек, доступных ботам в Teams
keywords: bots cards reference
ms.openlocfilehash: 22a4faa932173387cbefe900e30106d063c49e50
ms.sourcegitcommit: 5739245903278d521ec920427248b6b48676e637
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/07/2021
ms.locfileid: "49778396"
---
# <a name="cards-reference"></a><span data-ttu-id="3b7eb-104">Справочник по карточкам</span><span class="sxs-lookup"><span data-stu-id="3b7eb-104">Cards Reference</span></span>

<span data-ttu-id="3b7eb-105">Карточки, перечисленные в этом разделе, поддерживаются в ботах для Teams.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-105">The cards listed in this section are supported in bots for Teams.</span></span> <span data-ttu-id="3b7eb-106">Они основаны на карточках, определенных в Bot Framework, но Teams не поддерживает все карточки Bot Framework и добавил некоторые из них.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-106">They are based on cards defined by the Bot Framework, but Teams does not support all Bot Framework cards and has added some of its own.</span></span> <span data-ttu-id="3b7eb-107">Различия вызваны в ссылках ниже.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-107">Differences are called out in the references below.</span></span>

## <a name="card-examples"></a><span data-ttu-id="3b7eb-108">Примеры карт</span><span class="sxs-lookup"><span data-stu-id="3b7eb-108">Card examples</span></span>

<span data-ttu-id="3b7eb-109">Дополнительные сведения об использовании карточек можно найти в документации для SDK построитель ботов (v3).</span><span class="sxs-lookup"><span data-stu-id="3b7eb-109">You can find additional information on how to use cards in the documentation for the Bot Builder SDK (v3).</span></span> <span data-ttu-id="3b7eb-110">Кроме того, примеры кода доступны в репозитории Microsoft/BotBuilder-Samples на GitHub.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-110">There are also code samples available in the Microsoft/BotBuilder-Samples repository on GitHub.</span></span>

* <span data-ttu-id="3b7eb-111">.NET</span><span class="sxs-lookup"><span data-stu-id="3b7eb-111">.NET</span></span>
  * [<span data-ttu-id="3b7eb-112">Добавление карточек в виде вложений в сообщения</span><span class="sxs-lookup"><span data-stu-id="3b7eb-112">Add cards as attachments to messages</span></span>](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments)
  * [<span data-ttu-id="3b7eb-113">Пример кода карточек (построитель ботов 3)</span><span class="sxs-lookup"><span data-stu-id="3b7eb-113">Cards sample code (Bot Builder v3)</span></span>](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/CSharp/cards-RichCards)
* <span data-ttu-id="3b7eb-114">Node.js</span><span class="sxs-lookup"><span data-stu-id="3b7eb-114">Node.js</span></span>
  * [<span data-ttu-id="3b7eb-115">Добавление карточек в виде вложений в сообщения</span><span class="sxs-lookup"><span data-stu-id="3b7eb-115">Add cards as attachments to messages</span></span>](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)
  * [<span data-ttu-id="3b7eb-116">Пример кода карточек (построитель ботов 3)</span><span class="sxs-lookup"><span data-stu-id="3b7eb-116">Cards sample code (Bot Builder v3)</span></span>](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/Node/cards-RichCards)

## <a name="types-of-cards"></a><span data-ttu-id="3b7eb-117">Типы карточек</span><span class="sxs-lookup"><span data-stu-id="3b7eb-117">Types of cards</span></span>

<span data-ttu-id="3b7eb-118">В этой таблице показаны типы доступных карточек.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-118">This table shows the types of cards available to you.</span></span>

| <span data-ttu-id="3b7eb-119">Тип карточки</span><span class="sxs-lookup"><span data-stu-id="3b7eb-119">Card Type</span></span> | <span data-ttu-id="3b7eb-120">Описание</span><span class="sxs-lookup"><span data-stu-id="3b7eb-120">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="3b7eb-121">Адаптивная карточка</span><span class="sxs-lookup"><span data-stu-id="3b7eb-121">Adaptive Card</span></span>](#adaptive-card) | <span data-ttu-id="3b7eb-122">Карточка с высокой настройкой, которая может содержать любое сочетание текста, речи, изображений, кнопок и полей ввода.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-122">Highly customizable card that can contain any combination of text, speech, images, buttons and input fields.</span></span> |
| [<span data-ttu-id="3b7eb-123">Hero Card</span><span class="sxs-lookup"><span data-stu-id="3b7eb-123">Hero Card</span></span>](#hero-card) | <span data-ttu-id="3b7eb-124">Обычно содержит одно большое изображение, одну или несколько кнопок и небольшой объем текста.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-124">Typically contains a single large image, one or more buttons, and a small amount of text.</span></span> |
| [<span data-ttu-id="3b7eb-125">Карточка списка</span><span class="sxs-lookup"><span data-stu-id="3b7eb-125">List Card</span></span>](#list-card) | <span data-ttu-id="3b7eb-126">Список прокрутки элементов.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-126">A scrolling list of items.</span></span> |
| [<span data-ttu-id="3b7eb-127">Карточка соединители Office 365</span><span class="sxs-lookup"><span data-stu-id="3b7eb-127">Office 365 Connector Card</span></span>](#office-365-connector-card) | <span data-ttu-id="3b7eb-128">Гибкий макет с несколькими разделами, полями, изображениями и действиями.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-128">Flexible layout with multiple sections, fields, images and actions.</span></span> |
| [<span data-ttu-id="3b7eb-129">Чековая карта</span><span class="sxs-lookup"><span data-stu-id="3b7eb-129">Receipt Card</span></span>](#receipt-card) | <span data-ttu-id="3b7eb-130">Предоставляет пользователю квитанцию.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-130">Provides a receipt to the user.</span></span> |
| [<span data-ttu-id="3b7eb-131">Карточка для подписи</span><span class="sxs-lookup"><span data-stu-id="3b7eb-131">Signin Card</span></span>](#signin-card) | <span data-ttu-id="3b7eb-132">Позволяет боту запрашивать вход пользователя.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-132">Enables a bot to request that a user sign in.</span></span> |
| [<span data-ttu-id="3b7eb-133">Thumbnail Card</span><span class="sxs-lookup"><span data-stu-id="3b7eb-133">Thumbnail Card</span></span>](#thumbnail-card) | <span data-ttu-id="3b7eb-134">Обычно содержит один эскиз, короткий текст и одну или несколько кнопок.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-134">Typically contains a single thumbnail image, some short text, and one or more buttons.</span></span> |
| [<span data-ttu-id="3b7eb-135">Коллекции карт</span><span class="sxs-lookup"><span data-stu-id="3b7eb-135">Card Collections</span></span>](#card-collections) | <span data-ttu-id="3b7eb-136">Используется для возврата нескольких элементов в одном ответе</span><span class="sxs-lookup"><span data-stu-id="3b7eb-136">Used to return multiple items in a single response</span></span> |

## <a name="common-properties-for-all-cards"></a><span data-ttu-id="3b7eb-137">Общие свойства для всех карточек</span><span class="sxs-lookup"><span data-stu-id="3b7eb-137">Common properties for all cards</span></span>

### <a name="inline-card-images"></a><span data-ttu-id="3b7eb-138">Inline card images</span><span class="sxs-lookup"><span data-stu-id="3b7eb-138">Inline card images</span></span>

<span data-ttu-id="3b7eb-139">Карточка может содержать в себе изображение, включив ссылку на общедоступный образ.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-139">Your card can contain an inline image by including a link to your publicly available image.</span></span> <span data-ttu-id="3b7eb-140">В целях производительности мы настоятельно рекомендуем вам проводить образ в общедоступных сетях доставки содержимого (CDN).</span><span class="sxs-lookup"><span data-stu-id="3b7eb-140">For performance purposes we highly recommend you host your image on a public content-delivery network (CDN).</span></span>

<span data-ttu-id="3b7eb-141">Изображения масштабются вверх или вниз по размеру, сохраняя пропорции для покрытия области изображения, а затем обрезаются от центра, чтобы добиться соответствующего пропорций карточки.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-141">Images are scaled up or down in size while maintaining the aspect ratio to cover the image area, and then cropped from center to achieve the appropriate aspect ratio for the card.</span></span>

<span data-ttu-id="3b7eb-142">Изображения должны иметь не более 1024×1024 в формате PNG, JPEG или GIF; анимированное GIF официально не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-142">Images must be at most 1024×1024 in PNG, JPEG, or GIF format; animated GIF is not officially supported.</span></span>

| <span data-ttu-id="3b7eb-143">Свойство</span><span class="sxs-lookup"><span data-stu-id="3b7eb-143">Property</span></span> | <span data-ttu-id="3b7eb-144">Тип</span><span class="sxs-lookup"><span data-stu-id="3b7eb-144">Type</span></span>  | <span data-ttu-id="3b7eb-145">Описание</span><span class="sxs-lookup"><span data-stu-id="3b7eb-145">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b7eb-146">url</span><span class="sxs-lookup"><span data-stu-id="3b7eb-146">url</span></span> | <span data-ttu-id="3b7eb-147">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="3b7eb-147">URL</span></span> | <span data-ttu-id="3b7eb-148">URL-адрес ИЗОБРАЖЕНИЯ ПО HTTPS</span><span class="sxs-lookup"><span data-stu-id="3b7eb-148">HTTPS URL to the image</span></span> |
| <span data-ttu-id="3b7eb-149">alt</span><span class="sxs-lookup"><span data-stu-id="3b7eb-149">alt</span></span> | <span data-ttu-id="3b7eb-150">String</span><span class="sxs-lookup"><span data-stu-id="3b7eb-150">String</span></span> | <span data-ttu-id="3b7eb-151">Доступное описание изображения</span><span class="sxs-lookup"><span data-stu-id="3b7eb-151">Accessible description of the image</span></span> |

### <a name="buttons"></a><span data-ttu-id="3b7eb-152">Кнопки</span><span class="sxs-lookup"><span data-stu-id="3b7eb-152">Buttons</span></span>

<span data-ttu-id="3b7eb-153">Кнопки показаны в нижней части карточки.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-153">Buttons are shown stacked at the bottom of the card.</span></span> <span data-ttu-id="3b7eb-154">Текст кнопки всегда находится в одной строке и будет усечен, если текст превышает ширину кнопки.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-154">Button text is always on a single line and will be truncated if the text exceeds the button width.</span></span> <span data-ttu-id="3b7eb-155">Дополнительные кнопки, которые выходят за пределы максимального числа, поддерживаемого картой, не будут показаны.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-155">Any additional buttons beyond the maximum number supported by the card will not be shown.</span></span>

<span data-ttu-id="3b7eb-156">Дополнительные [сведения см.](~/task-modules-and-cards/cards/cards-actions.md) в действиях карточки.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-156">See [Card Actions](~/task-modules-and-cards/cards/cards-actions.md) for more information.</span></span>

### <a name="card-formatting"></a><span data-ttu-id="3b7eb-157">Форматирование карт</span><span class="sxs-lookup"><span data-stu-id="3b7eb-157">Card Formatting</span></span>

<span data-ttu-id="3b7eb-158">Дополнительные [сведения о форматирование](~/task-modules-and-cards/cards/cards-format.md) текста в карточках см. в документе "Форматирование карточек".</span><span class="sxs-lookup"><span data-stu-id="3b7eb-158">See [Card Formatting](~/task-modules-and-cards/cards/cards-format.md) for more information on text formatting in cards.</span></span>

## <a name="adaptive-card"></a><span data-ttu-id="3b7eb-159">Адаптивная карточка</span><span class="sxs-lookup"><span data-stu-id="3b7eb-159">Adaptive card</span></span>

<span data-ttu-id="3b7eb-160">Настраиваемая карточка, которая может содержать любое сочетание текста, речи, изображений, кнопок и полей ввода.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-160">A customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> <span data-ttu-id="3b7eb-161">*См.* ["Адаптивные карточки" 1.2.0.](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0)</span><span class="sxs-lookup"><span data-stu-id="3b7eb-161">*See* [Adaptive Cards v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span></span>

### <a name="support-for-adaptive-cards"></a><span data-ttu-id="3b7eb-162">Поддержка адаптивных карточек</span><span class="sxs-lookup"><span data-stu-id="3b7eb-162">Support for Adaptive cards</span></span>

| <span data-ttu-id="3b7eb-163">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="3b7eb-163">Bots in Teams</span></span> | <span data-ttu-id="3b7eb-164">Расширения для сообщений</span><span class="sxs-lookup"><span data-stu-id="3b7eb-164">Messaging Extensions</span></span>  | <span data-ttu-id="3b7eb-165">Соединители</span><span class="sxs-lookup"><span data-stu-id="3b7eb-165">Connectors</span></span> | <span data-ttu-id="3b7eb-166">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="3b7eb-166">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b7eb-167">✔</span><span class="sxs-lookup"><span data-stu-id="3b7eb-167">✔</span></span> | <span data-ttu-id="3b7eb-168">✔</span><span class="sxs-lookup"><span data-stu-id="3b7eb-168">✔</span></span> | <span data-ttu-id="3b7eb-169">✖</span><span class="sxs-lookup"><span data-stu-id="3b7eb-169">✖</span></span> | <span data-ttu-id="3b7eb-170">✔</span><span class="sxs-lookup"><span data-stu-id="3b7eb-170">✔</span></span> |
|

> [!NOTE]
> * <span data-ttu-id="3b7eb-171">Платформа Teams поддерживает функции адаптивной карточки 1.2 или более ранней.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-171">Teams platform supports v1.2 or earlier of Adaptive card features.</span></span>
> * <span data-ttu-id="3b7eb-172">Элементы мультимедиа в настоящее время не поддерживаются в адаптивной карточке 1.2 на платформе Teams.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-172">Media elements are currently not supported in Adaptive card v1.2 on the Teams platform.</span></span>
### <a name="example-adaptive-card"></a><span data-ttu-id="3b7eb-173">Пример адаптивной карточки</span><span class="sxs-lookup"><span data-stu-id="3b7eb-173">Example Adaptive card</span></span>

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

#### <a name="for-more-information-on-adaptive-cards"></a><span data-ttu-id="3b7eb-175">Дополнительные сведения об адаптивных карточках</span><span class="sxs-lookup"><span data-stu-id="3b7eb-175">For more information on Adaptive cards</span></span>

* [<span data-ttu-id="3b7eb-176">Обзор адаптивных карточек</span><span class="sxs-lookup"><span data-stu-id="3b7eb-176">Adaptive Cards Overview</span></span>](/adaptive-cards/)
* [<span data-ttu-id="3b7eb-177">Действия адаптивной карточки в Teams</span><span class="sxs-lookup"><span data-stu-id="3b7eb-177">Adaptive card actions in Teams</span></span>](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)

## <a name="hero-card"></a><span data-ttu-id="3b7eb-178">Карточка "Главного"</span><span class="sxs-lookup"><span data-stu-id="3b7eb-178">Hero card</span></span>

<span data-ttu-id="3b7eb-179">Карточка, которая обычно содержит одно большое изображение, одну или несколько кнопок и текста.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-179">A card that typically contains a single large image, one or more buttons and text.</span></span>

### <a name="support-for-hero-cards"></a><span data-ttu-id="3b7eb-180">Поддержка карточек "Главного"</span><span class="sxs-lookup"><span data-stu-id="3b7eb-180">Support for Hero cards</span></span>

| <span data-ttu-id="3b7eb-181">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="3b7eb-181">Bots in Teams</span></span> | <span data-ttu-id="3b7eb-182">Расширения для сообщений</span><span class="sxs-lookup"><span data-stu-id="3b7eb-182">Messaging Extensions</span></span>  | <span data-ttu-id="3b7eb-183">Соединители</span><span class="sxs-lookup"><span data-stu-id="3b7eb-183">Connectors</span></span> | <span data-ttu-id="3b7eb-184">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="3b7eb-184">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b7eb-185">✔</span><span class="sxs-lookup"><span data-stu-id="3b7eb-185">✔</span></span> | <span data-ttu-id="3b7eb-186">✔</span><span class="sxs-lookup"><span data-stu-id="3b7eb-186">✔</span></span> | <span data-ttu-id="3b7eb-187">✖</span><span class="sxs-lookup"><span data-stu-id="3b7eb-187">✖</span></span> | <span data-ttu-id="3b7eb-188">✔</span><span class="sxs-lookup"><span data-stu-id="3b7eb-188">✔</span></span> |
|

### <a name="properties-of-a-hero-card"></a><span data-ttu-id="3b7eb-189">Свойства карточки "Hero"</span><span class="sxs-lookup"><span data-stu-id="3b7eb-189">Properties of a Hero card</span></span>

| <span data-ttu-id="3b7eb-190">Свойство</span><span class="sxs-lookup"><span data-stu-id="3b7eb-190">Property</span></span> | <span data-ttu-id="3b7eb-191">Тип</span><span class="sxs-lookup"><span data-stu-id="3b7eb-191">Type</span></span>  | <span data-ttu-id="3b7eb-192">Описание</span><span class="sxs-lookup"><span data-stu-id="3b7eb-192">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b7eb-193">title</span><span class="sxs-lookup"><span data-stu-id="3b7eb-193">title</span></span> | <span data-ttu-id="3b7eb-194">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="3b7eb-194">Rich text</span></span> | <span data-ttu-id="3b7eb-195">Название карточки.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-195">Title of the card.</span></span> <span data-ttu-id="3b7eb-196">Не более 2 строк.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-196">Maximum 2 lines.</span></span> |
| <span data-ttu-id="3b7eb-197">subtitle</span><span class="sxs-lookup"><span data-stu-id="3b7eb-197">subtitle</span></span> | <span data-ttu-id="3b7eb-198">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="3b7eb-198">Rich text</span></span> | <span data-ttu-id="3b7eb-199">Субтитры на карточке.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-199">Subtitle of the card.</span></span> <span data-ttu-id="3b7eb-200">Не более 2 строк.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-200">Maximum 2 lines.</span></span>|
| <span data-ttu-id="3b7eb-201">текст</span><span class="sxs-lookup"><span data-stu-id="3b7eb-201">text</span></span> | <span data-ttu-id="3b7eb-202">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="3b7eb-202">Rich text</span></span> | <span data-ttu-id="3b7eb-203">Текст отображается сразу под субтитром; См. [параметры форматирования](~/task-modules-and-cards/cards/cards-format.md) карточки</span><span class="sxs-lookup"><span data-stu-id="3b7eb-203">Text appears just below the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options</span></span> |
| <span data-ttu-id="3b7eb-204">images</span><span class="sxs-lookup"><span data-stu-id="3b7eb-204">images</span></span> | <span data-ttu-id="3b7eb-205">Массив изображений</span><span class="sxs-lookup"><span data-stu-id="3b7eb-205">Array of images</span></span> | <span data-ttu-id="3b7eb-206">Изображение, отображаемого в верхней части карточки.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-206">Image displayed at top of card.</span></span> <span data-ttu-id="3b7eb-207">Пропорции 16:9</span><span class="sxs-lookup"><span data-stu-id="3b7eb-207">Aspect ratio 16:9</span></span> |
| <span data-ttu-id="3b7eb-208">buttons</span><span class="sxs-lookup"><span data-stu-id="3b7eb-208">buttons</span></span> | <span data-ttu-id="3b7eb-209">Массив объектов действий</span><span class="sxs-lookup"><span data-stu-id="3b7eb-209">Array of action objects</span></span> | <span data-ttu-id="3b7eb-210">Набор действий, применимых к текущей карточке.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-210">Set of actions applicable to the current card.</span></span> <span data-ttu-id="3b7eb-211">Максимум 6</span><span class="sxs-lookup"><span data-stu-id="3b7eb-211">Maximum 6</span></span> |
| <span data-ttu-id="3b7eb-212">tap</span><span class="sxs-lookup"><span data-stu-id="3b7eb-212">tap</span></span> | <span data-ttu-id="3b7eb-213">Объект Action</span><span class="sxs-lookup"><span data-stu-id="3b7eb-213">Action object</span></span> | <span data-ttu-id="3b7eb-214">Это действие будет активировано, когда пользователь коснитесь самой карточки</span><span class="sxs-lookup"><span data-stu-id="3b7eb-214">This action will be activated when the user taps on the card itself</span></span> |
|

### <a name="example-hero-card"></a><span data-ttu-id="3b7eb-215">Пример карточки "Образец"</span><span class="sxs-lookup"><span data-stu-id="3b7eb-215">Example Hero card</span></span>

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

### <a name="for-more-information-on-hero-cards"></a><span data-ttu-id="3b7eb-217">Дополнительные сведения о картах Hero</span><span class="sxs-lookup"><span data-stu-id="3b7eb-217">For more information on Hero cards</span></span>

<span data-ttu-id="3b7eb-218">Справка по Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="3b7eb-218">Bot Framework reference:</span></span>

* [<span data-ttu-id="3b7eb-219">Узел главного карточки</span><span class="sxs-lookup"><span data-stu-id="3b7eb-219">Hero card Node</span></span>](https://docs.microsoft.com/javascript/api/botframework-schema/herocard)
* [<span data-ttu-id="3b7eb-220">Главный карточка C #</span><span class="sxs-lookup"><span data-stu-id="3b7eb-220">Hero card C#</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.herocard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="list-card"></a><span data-ttu-id="3b7eb-221">Карточка списка</span><span class="sxs-lookup"><span data-stu-id="3b7eb-221">List card</span></span>

<span data-ttu-id="3b7eb-222">Карточка списка была добавлена в Teams для предоставления функций, которые выходят за рамки того, что может предоставить коллекция списков.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-222">The list card has been added by Teams to provide functions beyond what the list collection can provide.</span></span> <span data-ttu-id="3b7eb-223">На карточке списка содержится прокручивающийся список элементов.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-223">The list card provides a scrolling list of items.</span></span>

### <a name="support-for-list-cards"></a><span data-ttu-id="3b7eb-224">Поддержка карточек списков</span><span class="sxs-lookup"><span data-stu-id="3b7eb-224">Support for List cards</span></span>

| <span data-ttu-id="3b7eb-225">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="3b7eb-225">Bots in Teams</span></span> | <span data-ttu-id="3b7eb-226">Расширения для сообщений</span><span class="sxs-lookup"><span data-stu-id="3b7eb-226">Messaging Extensions</span></span>  | <span data-ttu-id="3b7eb-227">Соединители</span><span class="sxs-lookup"><span data-stu-id="3b7eb-227">Connectors</span></span> | <span data-ttu-id="3b7eb-228">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="3b7eb-228">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b7eb-229">✔</span><span class="sxs-lookup"><span data-stu-id="3b7eb-229">✔</span></span> | <span data-ttu-id="3b7eb-230">✖</span><span class="sxs-lookup"><span data-stu-id="3b7eb-230">✖</span></span> | <span data-ttu-id="3b7eb-231">✖</span><span class="sxs-lookup"><span data-stu-id="3b7eb-231">✖</span></span> |<span data-ttu-id="3b7eb-232">✔</span><span class="sxs-lookup"><span data-stu-id="3b7eb-232">✔</span></span> |
|

### <a name="properties-of-a-list-card"></a><span data-ttu-id="3b7eb-233">Свойства карточки списка</span><span class="sxs-lookup"><span data-stu-id="3b7eb-233">Properties of a List card</span></span>

| <span data-ttu-id="3b7eb-234">Свойство</span><span class="sxs-lookup"><span data-stu-id="3b7eb-234">Property</span></span> | <span data-ttu-id="3b7eb-235">Тип</span><span class="sxs-lookup"><span data-stu-id="3b7eb-235">Type</span></span>  | <span data-ttu-id="3b7eb-236">Описание</span><span class="sxs-lookup"><span data-stu-id="3b7eb-236">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b7eb-237">title</span><span class="sxs-lookup"><span data-stu-id="3b7eb-237">title</span></span> | <span data-ttu-id="3b7eb-238">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="3b7eb-238">Rich text</span></span> | <span data-ttu-id="3b7eb-239">Название карточки.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-239">Title of the card.</span></span> <span data-ttu-id="3b7eb-240">Не более 2 строк.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-240">Maximum 2 lines.</span></span>|
| <span data-ttu-id="3b7eb-241">items</span><span class="sxs-lookup"><span data-stu-id="3b7eb-241">items</span></span> | <span data-ttu-id="3b7eb-242">Массив элементов списка</span><span class="sxs-lookup"><span data-stu-id="3b7eb-242">Array of list items</span></span>  ||
| <span data-ttu-id="3b7eb-243">buttons</span><span class="sxs-lookup"><span data-stu-id="3b7eb-243">buttons</span></span> | <span data-ttu-id="3b7eb-244">Массив объектов действий</span><span class="sxs-lookup"><span data-stu-id="3b7eb-244">Array of action objects</span></span> | <span data-ttu-id="3b7eb-245">Набор действий, применимых к текущей карточке.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-245">Set of actions applicable to the current card.</span></span> <span data-ttu-id="3b7eb-246">Максимум 6.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-246">Maximum 6.</span></span> |

### <a name="example-list-card"></a><span data-ttu-id="3b7eb-247">Пример карточки списка</span><span class="sxs-lookup"><span data-stu-id="3b7eb-247">Example List card</span></span>

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

## <a name="office-365-connector-card"></a><span data-ttu-id="3b7eb-248">Карточка соединители Office 365</span><span class="sxs-lookup"><span data-stu-id="3b7eb-248">Office 365 connector card</span></span>

<span data-ttu-id="3b7eb-249">Поддерживается в Teams, а не в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-249">Supported in Teams, not in Bot Framework.</span></span>

<span data-ttu-id="3b7eb-250">Карточка соединители Office 365 предоставляет гибкий макет с несколькими разделами, полями, изображениями и действиями.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-250">The Office 365 Connector card provides a flexible layout with multiple sections, fields, images, and actions.</span></span> <span data-ttu-id="3b7eb-251">Эта карточка инкапсулирует карточку соединителя, чтобы ее могли использовать боты.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-251">This card encapsulates a connector card so that it can be used by bots.</span></span> <span data-ttu-id="3b7eb-252">Различия между карточками соединители и картой O365 см. в разделе примечаний.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-252">See the notes section for differences between connector cards and the O365 card.</span></span>

### <a name="support-for-office-365-connector-cards"></a><span data-ttu-id="3b7eb-253">Поддержка карточек соединители Office 365</span><span class="sxs-lookup"><span data-stu-id="3b7eb-253">Support for Office 365 connector cards</span></span>

| <span data-ttu-id="3b7eb-254">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="3b7eb-254">Bots in Teams</span></span> | <span data-ttu-id="3b7eb-255">Расширения для сообщений</span><span class="sxs-lookup"><span data-stu-id="3b7eb-255">Messaging Extensions</span></span>  | <span data-ttu-id="3b7eb-256">Соединители</span><span class="sxs-lookup"><span data-stu-id="3b7eb-256">Connectors</span></span> | <span data-ttu-id="3b7eb-257">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="3b7eb-257">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b7eb-258">✔</span><span class="sxs-lookup"><span data-stu-id="3b7eb-258">✔</span></span> | <span data-ttu-id="3b7eb-259">✔</span><span class="sxs-lookup"><span data-stu-id="3b7eb-259">✔</span></span> | <span data-ttu-id="3b7eb-260">✔</span><span class="sxs-lookup"><span data-stu-id="3b7eb-260">✔</span></span> | <span data-ttu-id="3b7eb-261">✖</span><span class="sxs-lookup"><span data-stu-id="3b7eb-261">✖</span></span> |
|

### <a name="properties-of-the-office-365-connector-card"></a><span data-ttu-id="3b7eb-262">Свойства карточки соединители Office 365</span><span class="sxs-lookup"><span data-stu-id="3b7eb-262">Properties of the Office 365 connector card</span></span>

| <span data-ttu-id="3b7eb-263">Свойство</span><span class="sxs-lookup"><span data-stu-id="3b7eb-263">Property</span></span> | <span data-ttu-id="3b7eb-264">Тип</span><span class="sxs-lookup"><span data-stu-id="3b7eb-264">Type</span></span>  | <span data-ttu-id="3b7eb-265">Описание</span><span class="sxs-lookup"><span data-stu-id="3b7eb-265">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b7eb-266">title</span><span class="sxs-lookup"><span data-stu-id="3b7eb-266">title</span></span> | <span data-ttu-id="3b7eb-267">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="3b7eb-267">Rich text</span></span> | <span data-ttu-id="3b7eb-268">Название карточки.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-268">Title of the card.</span></span> <span data-ttu-id="3b7eb-269">Не более 2 строк.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-269">Maximum 2 lines.</span></span> |
| <span data-ttu-id="3b7eb-270">summary</span><span class="sxs-lookup"><span data-stu-id="3b7eb-270">summary</span></span> | <span data-ttu-id="3b7eb-271">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="3b7eb-271">Rich text</span></span> | <span data-ttu-id="3b7eb-272">Сводка карточки.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-272">Summary of the card.</span></span> <span data-ttu-id="3b7eb-273">Не более 2 строк.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-273">Maximum 2 lines.</span></span> |
| <span data-ttu-id="3b7eb-274">текст</span><span class="sxs-lookup"><span data-stu-id="3b7eb-274">text</span></span> | <span data-ttu-id="3b7eb-275">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="3b7eb-275">Rich text</span></span> | <span data-ttu-id="3b7eb-276">Текст отображается сразу под субтитром; См. [параметры форматирования](~/task-modules-and-cards/cards/cards-format.md) карточки</span><span class="sxs-lookup"><span data-stu-id="3b7eb-276">Text appears just below the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options</span></span> |
| <span data-ttu-id="3b7eb-277">themeColor</span><span class="sxs-lookup"><span data-stu-id="3b7eb-277">themeColor</span></span> | <span data-ttu-id="3b7eb-278">Строка HEX</span><span class="sxs-lookup"><span data-stu-id="3b7eb-278">HEX string</span></span> | <span data-ttu-id="3b7eb-279">цвет, который переопределит accentColor, предоставленный из манифеста приложения</span><span class="sxs-lookup"><span data-stu-id="3b7eb-279">color that overrides the accentColor provided from the application manifest</span></span> |

### <a name="notes-on-the-office-365-connector-card"></a><span data-ttu-id="3b7eb-280">Примечания на карточке соединители Office 365</span><span class="sxs-lookup"><span data-stu-id="3b7eb-280">Notes on the Office 365 connector card</span></span>

<span data-ttu-id="3b7eb-281">Карточки соединители Office 365 правильно работают в Microsoft Teams, включая [действия ActionCard.](/outlook/actionable-messages/card-reference#actioncard-action)</span><span class="sxs-lookup"><span data-stu-id="3b7eb-281">Office 365 Connector cards function properly on Microsoft Teams, including [ActionCard actions](/outlook/actionable-messages/card-reference#actioncard-action).</span></span>

<span data-ttu-id="3b7eb-282">Одно из важных отличий между использованием карточек соединители из соединители и карточек соединители в боте обработка действий карт.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-282">One important difference between using Connector cards from a Connector and using Connector cards in your bot is the handling of card actions.</span></span>

* <span data-ttu-id="3b7eb-283">Для соединители конечная точка получает полезной нагрузки карточки через HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-283">For a Connector, the endpoint receives the card payload via HTTP POST.</span></span>
* <span data-ttu-id="3b7eb-284">Для бота действие запускает действие, которое отправляет боту только ИД и `HttpPOST` `invoke` тело действия.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-284">For a bot, the `HttpPOST` action triggers an `invoke` activity that sends only the action ID and body to the bot.</span></span>

<span data-ttu-id="3b7eb-285">Каждая карточка соединители может отображать не более 10 разделов, а каждый раздел может содержать не более 5 изображений и 5 действий.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-285">Each Connector card can display a maximum of 10 sections, and each section can contain a maximum of 5 images and 5 actions.</span></span>

> [!NOTE]
> <span data-ttu-id="3b7eb-286">Дополнительные разделы, изображения или действия в сообщении не отображаются.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-286">Any additional sections, images, or actions in a message will not appear.</span></span>

<span data-ttu-id="3b7eb-287">Все текстовые поля поддерживают Markdown и HTML.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-287">All text fields support Markdown and HTML.</span></span> <span data-ttu-id="3b7eb-288">Вы можете управлять тем, в каких разделах используется Markdown или HTML, установив `markdown` свойство в сообщении.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-288">You can control which sections use Markdown or HTML by setting the `markdown` property in a message.</span></span> <span data-ttu-id="3b7eb-289">По умолчанию установлено значение ; если вы хотите использовать `markdown` `true` HTML, установите `markdown` значение `false` .</span><span class="sxs-lookup"><span data-stu-id="3b7eb-289">By default, `markdown` is set to `true`; if you want to use HTML instead, set `markdown` to `false`.</span></span>

<span data-ttu-id="3b7eb-290">Если указать `themeColor` свойство, оно переопределит `accentColor` свойство в манифесте приложения.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-290">If you specify the `themeColor` property, it overrides the `accentColor` property in the app manifest.</span></span>

<span data-ttu-id="3b7eb-291">Чтобы указать стиль отрисовки, `activityImage` можно задать его следующим `activityImageType` образом.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-291">To specify the rendering style for `activityImage`, you can set `activityImageType` as follows.</span></span>

| <span data-ttu-id="3b7eb-292">Значение</span><span class="sxs-lookup"><span data-stu-id="3b7eb-292">Value</span></span> | <span data-ttu-id="3b7eb-293">Описание</span><span class="sxs-lookup"><span data-stu-id="3b7eb-293">Description</span></span> |
| --- | --- |
| `avatar` | <span data-ttu-id="3b7eb-294">По умолчанию; `activityImage` будет обрезана в круге</span><span class="sxs-lookup"><span data-stu-id="3b7eb-294">Default; `activityImage` will be cropped as a circle</span></span> |
| `article` | <span data-ttu-id="3b7eb-295">`activityImage` будет отображаться как прямоугольник с сохранением пропорций</span><span class="sxs-lookup"><span data-stu-id="3b7eb-295">`activityImage` will be displayed as a rectangle and retain its aspect ratio</span></span> |

<span data-ttu-id="3b7eb-296">Все остальные сведения о свойствах карточки соединители см. в справочнике по карточкам [сообщений с действиями.](/outlook/actionable-messages/card-reference)</span><span class="sxs-lookup"><span data-stu-id="3b7eb-296">For all other details about Connector card properties, see the [Actionable message card reference](/outlook/actionable-messages/card-reference).</span></span> <span data-ttu-id="3b7eb-297">Единственными свойствами карточки соединитела, которые в настоящее время не поддерживаются Microsoft Teams, являются:</span><span class="sxs-lookup"><span data-stu-id="3b7eb-297">The only Connector card properties that Microsoft Teams does not currently support are as follows:</span></span>

* `heroImage`
* `hideOriginalBody`
* <span data-ttu-id="3b7eb-298">`startGroup` (всегда рассматривается как `true` в Teams)</span><span class="sxs-lookup"><span data-stu-id="3b7eb-298">`startGroup` (always treated as `true` in Teams)</span></span>
* `originator`
* `correlationId`

### <a name="example-office-365-connector-card"></a><span data-ttu-id="3b7eb-299">Пример карточки соединители Office 365</span><span class="sxs-lookup"><span data-stu-id="3b7eb-299">Example Office 365 connector card</span></span>

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

## <a name="receipt-card"></a><span data-ttu-id="3b7eb-300">Чековая карта</span><span class="sxs-lookup"><span data-stu-id="3b7eb-300">Receipt card</span></span>

<span data-ttu-id="3b7eb-301">Поддерживается в Teams.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-301">Supported in Teams.</span></span>

<span data-ttu-id="3b7eb-302">Карточка, которая позволяет боту предоставлять пользователю квитанцию.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-302">A card that enables a bot to provide a receipt to the user.</span></span> <span data-ttu-id="3b7eb-303">Обычно он содержит список элементов, которые необходимо включить в квитанцию, налог и общую информацию, а также другой текст.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-303">It typically contains the list of items to include on the receipt, tax and total information, and other text.</span></span>

### <a name="support-for-receipts-cards"></a><span data-ttu-id="3b7eb-304">Поддержка карточек квитанций</span><span class="sxs-lookup"><span data-stu-id="3b7eb-304">Support for Receipts cards</span></span>

| <span data-ttu-id="3b7eb-305">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="3b7eb-305">Bots in Teams</span></span> | <span data-ttu-id="3b7eb-306">Расширения для сообщений</span><span class="sxs-lookup"><span data-stu-id="3b7eb-306">Messaging Extensions</span></span>  | <span data-ttu-id="3b7eb-307">Соединители</span><span class="sxs-lookup"><span data-stu-id="3b7eb-307">Connectors</span></span> | <span data-ttu-id="3b7eb-308">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="3b7eb-308">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b7eb-309">✔</span><span class="sxs-lookup"><span data-stu-id="3b7eb-309">✔</span></span> | <span data-ttu-id="3b7eb-310">✔</span><span class="sxs-lookup"><span data-stu-id="3b7eb-310">✔</span></span> | <span data-ttu-id="3b7eb-311">✖</span><span class="sxs-lookup"><span data-stu-id="3b7eb-311">✖</span></span> | <span data-ttu-id="3b7eb-312">✔</span><span class="sxs-lookup"><span data-stu-id="3b7eb-312">✔</span></span> |
|

### <a name="for-more-information-on-receipt-cards"></a><span data-ttu-id="3b7eb-313">Дополнительные сведения о карточках квитанций</span><span class="sxs-lookup"><span data-stu-id="3b7eb-313">For more information on Receipt cards</span></span>

<span data-ttu-id="3b7eb-314">Справка по Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="3b7eb-314">Bot Framework reference:</span></span>

* [<span data-ttu-id="3b7eb-315">Узел карточки квитанции</span><span class="sxs-lookup"><span data-stu-id="3b7eb-315">Receipt card Node</span></span>](https://docs.microsoft.com/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="3b7eb-316">Чековая карта C #</span><span class="sxs-lookup"><span data-stu-id="3b7eb-316">Receipt card C#</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.receiptcard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="signin-card"></a><span data-ttu-id="3b7eb-317">Карточка для подписи</span><span class="sxs-lookup"><span data-stu-id="3b7eb-317">Signin card</span></span>

<span data-ttu-id="3b7eb-318">Карточка, которая позволяет боту запрашивать вход пользователя.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-318">A card that enables a bot to request that a user sign in.</span></span> <span data-ttu-id="3b7eb-319">Поддерживается в Teams в несколько другом формате, чем в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-319">Supported in Teams in a slightly different form than is found in the Bot Framework.</span></span> <span data-ttu-id="3b7eb-320">Карточка для регистрации в Teams похожа на карточку для регистрации в структуре бота, за исключением того, что карточка для регистрации в Teams поддерживает только два действия: `signin` и `openUrl` .</span><span class="sxs-lookup"><span data-stu-id="3b7eb-320">The signin card in Teams is similar to the signin card in the bot framework with the exception that the signin card in Teams only supports two actions: `signin` and `openUrl`.</span></span>

<span data-ttu-id="3b7eb-321">Действие *для регистрации можно* использовать с любой карточки в Teams, а не только с карточки для регистрации.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-321">The *signin action* can be used from any card in Teams, not just the signin card.</span></span> <span data-ttu-id="3b7eb-322">Дополнительные сведения о проверке подлинности ботов см. в разделе "Поток проверки подлинности [Microsoft Teams".](~/bots/how-to/authentication/auth-flow-bot.md)</span><span class="sxs-lookup"><span data-stu-id="3b7eb-322">See the topic [Microsoft Teams authentication flow for bots](~/bots/how-to/authentication/auth-flow-bot.md) for more details on authentication.</span></span>

### <a name="support-for-signin-cards"></a><span data-ttu-id="3b7eb-323">Поддержка карточек для регистрации</span><span class="sxs-lookup"><span data-stu-id="3b7eb-323">Support for Signin cards</span></span>

| <span data-ttu-id="3b7eb-324">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="3b7eb-324">Bots in Teams</span></span> | <span data-ttu-id="3b7eb-325">Расширения для сообщений</span><span class="sxs-lookup"><span data-stu-id="3b7eb-325">Messaging Extensions</span></span>  | <span data-ttu-id="3b7eb-326">Соединители</span><span class="sxs-lookup"><span data-stu-id="3b7eb-326">Connectors</span></span> | <span data-ttu-id="3b7eb-327">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="3b7eb-327">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b7eb-328">✔</span><span class="sxs-lookup"><span data-stu-id="3b7eb-328">✔</span></span> | <span data-ttu-id="3b7eb-329">✖</span><span class="sxs-lookup"><span data-stu-id="3b7eb-329">✖</span></span> | <span data-ttu-id="3b7eb-330">✖</span><span class="sxs-lookup"><span data-stu-id="3b7eb-330">✖</span></span> | <span data-ttu-id="3b7eb-331">✔</span><span class="sxs-lookup"><span data-stu-id="3b7eb-331">✔</span></span> |
|

### <a name="for-more-information-on-signin-cards"></a><span data-ttu-id="3b7eb-332">Дополнительные сведения о карточках для подписи</span><span class="sxs-lookup"><span data-stu-id="3b7eb-332">For more information on Signin cards</span></span>

<span data-ttu-id="3b7eb-333">Справка по Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="3b7eb-333">Bot Framework reference:</span></span>

* [<span data-ttu-id="3b7eb-334">Узел карточки для подписи</span><span class="sxs-lookup"><span data-stu-id="3b7eb-334">Signin card Node</span></span>](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="3b7eb-335">Карточка для подписи C #</span><span class="sxs-lookup"><span data-stu-id="3b7eb-335">Signin card C#</span></span>](/dotnet/api/microsoft.bot.connector.signincard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="thumbnail-card"></a><span data-ttu-id="3b7eb-336">Эскиз карточки</span><span class="sxs-lookup"><span data-stu-id="3b7eb-336">Thumbnail card</span></span>

<span data-ttu-id="3b7eb-337">Карточка, которая обычно содержит один эскиз, одну или несколько кнопок и текст.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-337">A card that typically contains a single thumbnail image, one or more buttons, and text.</span></span>

### <a name="support-for-thumbnail-cards"></a><span data-ttu-id="3b7eb-338">Поддержка карточек эскизов</span><span class="sxs-lookup"><span data-stu-id="3b7eb-338">Support for Thumbnail cards</span></span>

| <span data-ttu-id="3b7eb-339">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="3b7eb-339">Bots in Teams</span></span> | <span data-ttu-id="3b7eb-340">Расширения для сообщений</span><span class="sxs-lookup"><span data-stu-id="3b7eb-340">Messaging Extensions</span></span>  | <span data-ttu-id="3b7eb-341">Соединители</span><span class="sxs-lookup"><span data-stu-id="3b7eb-341">Connectors</span></span> | <span data-ttu-id="3b7eb-342">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="3b7eb-342">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b7eb-343">✔</span><span class="sxs-lookup"><span data-stu-id="3b7eb-343">✔</span></span> | <span data-ttu-id="3b7eb-344">✔</span><span class="sxs-lookup"><span data-stu-id="3b7eb-344">✔</span></span> | <span data-ttu-id="3b7eb-345">✖</span><span class="sxs-lookup"><span data-stu-id="3b7eb-345">✖</span></span> | <span data-ttu-id="3b7eb-346">✔</span><span class="sxs-lookup"><span data-stu-id="3b7eb-346">✔</span></span> |
|

![Пример карточки эскиза](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a><span data-ttu-id="3b7eb-348">Свойства карточки thumbnail</span><span class="sxs-lookup"><span data-stu-id="3b7eb-348">Properties of a Thumbnail card</span></span>

| <span data-ttu-id="3b7eb-349">Свойство</span><span class="sxs-lookup"><span data-stu-id="3b7eb-349">Property</span></span> | <span data-ttu-id="3b7eb-350">Тип</span><span class="sxs-lookup"><span data-stu-id="3b7eb-350">Type</span></span>  | <span data-ttu-id="3b7eb-351">Описание</span><span class="sxs-lookup"><span data-stu-id="3b7eb-351">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b7eb-352">title</span><span class="sxs-lookup"><span data-stu-id="3b7eb-352">title</span></span> | <span data-ttu-id="3b7eb-353">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="3b7eb-353">Rich text</span></span> | <span data-ttu-id="3b7eb-354">Название карточки.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-354">Title of the card.</span></span> <span data-ttu-id="3b7eb-355">Не более 2 строк.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-355">Maximum 2 lines.</span></span>|
| <span data-ttu-id="3b7eb-356">subtitle</span><span class="sxs-lookup"><span data-stu-id="3b7eb-356">subtitle</span></span> | <span data-ttu-id="3b7eb-357">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="3b7eb-357">Rich text</span></span> | <span data-ttu-id="3b7eb-358">Субтитры на карточке.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-358">Subtitle of the card.</span></span> <span data-ttu-id="3b7eb-359">Не более 2 строк.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-359">Maximum 2 lines.</span></span>|
| <span data-ttu-id="3b7eb-360">текст</span><span class="sxs-lookup"><span data-stu-id="3b7eb-360">text</span></span> | <span data-ttu-id="3b7eb-361">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="3b7eb-361">Rich text</span></span> | <span data-ttu-id="3b7eb-362">Текст отображается сразу под субтитром; См. [параметры форматирования](~/task-modules-and-cards/cards/cards-format.md) карточки</span><span class="sxs-lookup"><span data-stu-id="3b7eb-362">Text appears just below the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options</span></span> |
| <span data-ttu-id="3b7eb-363">images</span><span class="sxs-lookup"><span data-stu-id="3b7eb-363">images</span></span> | <span data-ttu-id="3b7eb-364">Массив изображений</span><span class="sxs-lookup"><span data-stu-id="3b7eb-364">Array of images</span></span> | <span data-ttu-id="3b7eb-365">Изображение, отображаемого в верхней части карточки.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-365">Image displayed at top of card.</span></span> <span data-ttu-id="3b7eb-366">Пропорции 1:1 (квадрат)</span><span class="sxs-lookup"><span data-stu-id="3b7eb-366">Aspect ratio 1:1 (square)</span></span> |
| <span data-ttu-id="3b7eb-367">buttons</span><span class="sxs-lookup"><span data-stu-id="3b7eb-367">buttons</span></span> | <span data-ttu-id="3b7eb-368">Массив объектов действий</span><span class="sxs-lookup"><span data-stu-id="3b7eb-368">Array of action objects</span></span> | <span data-ttu-id="3b7eb-369">Набор действий, применимых к текущей карточке.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-369">Set of actions applicable to the current card.</span></span> <span data-ttu-id="3b7eb-370">Максимум 6</span><span class="sxs-lookup"><span data-stu-id="3b7eb-370">Maximum 6</span></span> |
| <span data-ttu-id="3b7eb-371">tap</span><span class="sxs-lookup"><span data-stu-id="3b7eb-371">tap</span></span> | <span data-ttu-id="3b7eb-372">Объект Action</span><span class="sxs-lookup"><span data-stu-id="3b7eb-372">Action object</span></span> | <span data-ttu-id="3b7eb-373">Это действие будет активировано, когда пользователь коснитесь самой карточки</span><span class="sxs-lookup"><span data-stu-id="3b7eb-373">This action will be activated when the user taps on the card itself</span></span> |
|

### <a name="example-thumbnail-card"></a><span data-ttu-id="3b7eb-374">Пример карточки thumbnail</span><span class="sxs-lookup"><span data-stu-id="3b7eb-374">Example Thumbnail card</span></span>

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

### <a name="for-more-information"></a><span data-ttu-id="3b7eb-375">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="3b7eb-375">For more information</span></span>

<span data-ttu-id="3b7eb-376">Справка по Bot Framework:</span><span class="sxs-lookup"><span data-stu-id="3b7eb-376">Bot Framework reference:</span></span>

* [<span data-ttu-id="3b7eb-377">Узел карты эскиза</span><span class="sxs-lookup"><span data-stu-id="3b7eb-377">Thumbnail card Node</span></span>](https://docs.microsoft.com/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="3b7eb-378">Эскиз карточки C #</span><span class="sxs-lookup"><span data-stu-id="3b7eb-378">Thumbnail card C#</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.thumbnailcard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="card-collections"></a><span data-ttu-id="3b7eb-379">Коллекции карт</span><span class="sxs-lookup"><span data-stu-id="3b7eb-379">Card collections</span></span>

<span data-ttu-id="3b7eb-380">Коллекции карт поддерживаются в Teams.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-380">Card collections are supported in Teams.</span></span>

<span data-ttu-id="3b7eb-381">Коллекции карт: `builder.AttachmentLayout.carousel` и `builder.AttachmentLayout.list` .</span><span class="sxs-lookup"><span data-stu-id="3b7eb-381">Card collections: `builder.AttachmentLayout.carousel` and `builder.AttachmentLayout.list`.</span></span> <span data-ttu-id="3b7eb-382">Эти коллекции содержат адаптивные карточки, карты hero или thumbnail.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-382">These collections contain Adaptive, Hero, or Thumbnail cards.</span></span>

## <a name="carousel-collection"></a><span data-ttu-id="3b7eb-383">Коллекция карусели</span><span class="sxs-lookup"><span data-stu-id="3b7eb-383">Carousel collection</span></span>

<span data-ttu-id="3b7eb-384">На [макете карусели](/azure/bot-service/dotnet/bot-builder-dotnet-add-rich-card-attachments?view=azure-bot-service-3.0&preserve-view=true) показана карусели карт, при желании с кнопками связанных действий.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-384">The [carousel layout](/azure/bot-service/dotnet/bot-builder-dotnet-add-rich-card-attachments?view=azure-bot-service-3.0&preserve-view=true) shows a carousel of cards, optionally with associated action buttons.</span></span>

### <a name="support-for-carousel-collections"></a><span data-ttu-id="3b7eb-385">Поддержка коллекций карусели</span><span class="sxs-lookup"><span data-stu-id="3b7eb-385">Support for Carousel collections</span></span>

| <span data-ttu-id="3b7eb-386">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="3b7eb-386">Bots in Teams</span></span> | <span data-ttu-id="3b7eb-387">Расширения для сообщений</span><span class="sxs-lookup"><span data-stu-id="3b7eb-387">Messaging Extensions</span></span>  | <span data-ttu-id="3b7eb-388">Соединители</span><span class="sxs-lookup"><span data-stu-id="3b7eb-388">Connectors</span></span> | <span data-ttu-id="3b7eb-389">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="3b7eb-389">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b7eb-390">✔</span><span class="sxs-lookup"><span data-stu-id="3b7eb-390">✔</span></span> | <span data-ttu-id="3b7eb-391">✖</span><span class="sxs-lookup"><span data-stu-id="3b7eb-391">✖</span></span> | <span data-ttu-id="3b7eb-392">✖</span><span class="sxs-lookup"><span data-stu-id="3b7eb-392">✖</span></span> | <span data-ttu-id="3b7eb-393">✔</span><span class="sxs-lookup"><span data-stu-id="3b7eb-393">✔</span></span> |
|

> [!NOTE]
> <span data-ttu-id="3b7eb-394">Карусель может отображать не более 10 карт на сообщение.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-394">A carousel can display a maximum of 10 cards per message.</span></span>

### <a name="properties-of-a-carousel-card"></a><span data-ttu-id="3b7eb-395">Свойства карточки карусели</span><span class="sxs-lookup"><span data-stu-id="3b7eb-395">Properties of a Carousel card</span></span>

<span data-ttu-id="3b7eb-396">Свойства карточки карусели такие же, как и у карт главного и эскиза.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-396">Properties of a Carousel card are same as those of the Hero and Thumbnail cards.</span></span>

### <a name="example-carousel-collection"></a><span data-ttu-id="3b7eb-397">Пример коллекции Carousel</span><span class="sxs-lookup"><span data-stu-id="3b7eb-397">Example Carousel collection</span></span>

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

### <a name="syntax-for-carousel-collections"></a><span data-ttu-id="3b7eb-399">Синтаксис для коллекций карусели</span><span class="sxs-lookup"><span data-stu-id="3b7eb-399">Syntax for Carousel collections</span></span>

`builder.AttachmentLayoutTypes.Carousel`

## <a name="list-collection"></a><span data-ttu-id="3b7eb-400">Коллекция List</span><span class="sxs-lookup"><span data-stu-id="3b7eb-400">List collection</span></span>

### <a name="support-for-list-collections"></a><span data-ttu-id="3b7eb-401">Поддержка коллекций списков</span><span class="sxs-lookup"><span data-stu-id="3b7eb-401">Support for List collections</span></span>

<span data-ttu-id="3b7eb-402">Макет списка отображает список карт с вертикальным расположением, при желании с связанными кнопками действий.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-402">The list layout shows a vertically stacked list of cards, optionally with associated action buttons.</span></span>

| <span data-ttu-id="3b7eb-403">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="3b7eb-403">Bots in Teams</span></span> | <span data-ttu-id="3b7eb-404">Расширения для сообщений</span><span class="sxs-lookup"><span data-stu-id="3b7eb-404">Messaging Extensions</span></span>  | <span data-ttu-id="3b7eb-405">Соединители</span><span class="sxs-lookup"><span data-stu-id="3b7eb-405">Connectors</span></span> | <span data-ttu-id="3b7eb-406">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="3b7eb-406">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b7eb-407">✔</span><span class="sxs-lookup"><span data-stu-id="3b7eb-407">✔</span></span> | <span data-ttu-id="3b7eb-408">✔</span><span class="sxs-lookup"><span data-stu-id="3b7eb-408">✔</span></span> | <span data-ttu-id="3b7eb-409">✖</span><span class="sxs-lookup"><span data-stu-id="3b7eb-409">✖</span></span> | <span data-ttu-id="3b7eb-410">✔</span><span class="sxs-lookup"><span data-stu-id="3b7eb-410">✔</span></span> |
|

### <a name="example-list-collection"></a><span data-ttu-id="3b7eb-411">Пример коллекции List</span><span class="sxs-lookup"><span data-stu-id="3b7eb-411">Example List collection</span></span>

![Пример списка карточек](~/assets/images/cards/list.png)

<span data-ttu-id="3b7eb-413">Свойства такие же, как для главного или эскиза карточки.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-413">Properties are the same as for the hero or thumbnail card.</span></span>

<span data-ttu-id="3b7eb-414">В списке может отображаться не более 10 карт на сообщение.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-414">A list can display a maximum of 10 cards per message.</span></span>

> [!NOTE]
> <span data-ttu-id="3b7eb-415">Некоторые сочетания карточек списков пока не поддерживаются в iOS и Android.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-415">Some combinations of list cards are not yet supported on iOS and Android.</span></span>

### <a name="syntax-for-list-collections"></a><span data-ttu-id="3b7eb-416">Синтаксис для коллекций списков</span><span class="sxs-lookup"><span data-stu-id="3b7eb-416">Syntax for List collections</span></span>

`builder.AttachmentLayout.list`

## <a name="cards-not-supported-in-teams"></a><span data-ttu-id="3b7eb-417">Карточки не поддерживаются в Teams</span><span class="sxs-lookup"><span data-stu-id="3b7eb-417">Cards not supported in Teams</span></span>

<span data-ttu-id="3b7eb-418">Следующие карточки реализованы в Bot Framework, но НЕ поддерживаются Teams.</span><span class="sxs-lookup"><span data-stu-id="3b7eb-418">The following cards are implemented by the Bot Framework, but are NOT supported by Teams.</span></span>

* <span data-ttu-id="3b7eb-419">Карты анимации</span><span class="sxs-lookup"><span data-stu-id="3b7eb-419">Animation cards</span></span>
* <span data-ttu-id="3b7eb-420">Аудиокарты</span><span class="sxs-lookup"><span data-stu-id="3b7eb-420">Audio cards</span></span>
* <span data-ttu-id="3b7eb-421">Видеокарты</span><span class="sxs-lookup"><span data-stu-id="3b7eb-421">Video cards</span></span>
