---
title: Справочник по карточкам
description: Описывает все карточки и действия карточки, доступные боты в Teams.
keywords: Справочник по карточкам Боты
ms.openlocfilehash: 9cd868e504e426cbe56ed1c5d05c8e6adc1e1ddf
ms.sourcegitcommit: 61edf47c9dd1dbc1df03d0d9fb83bfedca4c423b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2020
ms.locfileid: "44801489"
---
# <a name="cards-reference"></a><span data-ttu-id="eafa9-104">Справочник по карточкам</span><span class="sxs-lookup"><span data-stu-id="eafa9-104">Cards Reference</span></span>

<span data-ttu-id="eafa9-105">Карточки, перечисленные в этом разделе, поддерживаются в боты для Teams.</span><span class="sxs-lookup"><span data-stu-id="eafa9-105">The cards listed in this section are supported in bots for Teams.</span></span> <span data-ttu-id="eafa9-106">Они основаны на карточках, определенных с помощью Bot Framework, но в Teams не поддерживаются все карточки с интерфейсом Bot и добавлены некоторые из них.</span><span class="sxs-lookup"><span data-stu-id="eafa9-106">They are based on cards defined by the Bot Framework, but Teams does not support all Bot Framework cards and has added some of its own.</span></span> <span data-ttu-id="eafa9-107">Различия вызываемы в приведенных ниже ссылках.</span><span class="sxs-lookup"><span data-stu-id="eafa9-107">Differences are called out in the references below.</span></span>

## <a name="card-examples"></a><span data-ttu-id="eafa9-108">Примеры карточек</span><span class="sxs-lookup"><span data-stu-id="eafa9-108">Card examples</span></span>

<span data-ttu-id="eafa9-109">Дополнительные сведения об использовании карточек можно найти в документации по пакету SDK для Bot Builder (v3).</span><span class="sxs-lookup"><span data-stu-id="eafa9-109">You can find additional information on how to use cards in the documentation for the Bot Builder SDK (v3).</span></span> <span data-ttu-id="eafa9-110">Кроме того, вы можете найти примеры кода в репозитории Microsoft/Ботбуилдер-Samples на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="eafa9-110">There are also code samples available in the Microsoft/BotBuilder-Samples repository on GitHub.</span></span>

* <span data-ttu-id="eafa9-111">.NET</span><span class="sxs-lookup"><span data-stu-id="eafa9-111">.NET</span></span>
  * [<span data-ttu-id="eafa9-112">Добавление карточек в качестве вложений в сообщения</span><span class="sxs-lookup"><span data-stu-id="eafa9-112">Add cards as attachments to messages</span></span>](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments)
  * [<span data-ttu-id="eafa9-113">Пример кода карточек (построитель построителя)</span><span class="sxs-lookup"><span data-stu-id="eafa9-113">Cards sample code (Bot Builder v3)</span></span>](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/CSharp/cards-RichCards)
* <span data-ttu-id="eafa9-114">Node.js</span><span class="sxs-lookup"><span data-stu-id="eafa9-114">Node.js</span></span>
  * [<span data-ttu-id="eafa9-115">Добавление карточек в качестве вложений в сообщения</span><span class="sxs-lookup"><span data-stu-id="eafa9-115">Add cards as attachments to messages</span></span>](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)
  * [<span data-ttu-id="eafa9-116">Пример кода карточек (построитель построителя)</span><span class="sxs-lookup"><span data-stu-id="eafa9-116">Cards sample code (Bot Builder v3)</span></span>](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/Node/cards-RichCards)

## <a name="types-of-cards"></a><span data-ttu-id="eafa9-117">Типы карточек</span><span class="sxs-lookup"><span data-stu-id="eafa9-117">Types of cards</span></span>

<span data-ttu-id="eafa9-118">В этой таблице перечислены доступные типы карт.</span><span class="sxs-lookup"><span data-stu-id="eafa9-118">This table shows the types of cards available to you.</span></span>

| <span data-ttu-id="eafa9-119">Тип карточки</span><span class="sxs-lookup"><span data-stu-id="eafa9-119">Card Type</span></span> | <span data-ttu-id="eafa9-120">Описание</span><span class="sxs-lookup"><span data-stu-id="eafa9-120">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="eafa9-121">Адаптивная карта</span><span class="sxs-lookup"><span data-stu-id="eafa9-121">Adaptive Card</span></span>](#adaptive-card) | <span data-ttu-id="eafa9-122">Карточка с широкими возможностями настройки, которая может содержать любую комбинацию текста, речи, изображений, кнопок и полей ввода.</span><span class="sxs-lookup"><span data-stu-id="eafa9-122">Highly customizable card that can contain any combination of text, speech, images, buttons and input fields.</span></span> |
| [<span data-ttu-id="eafa9-123">Карточка главный Имиджевый баннер</span><span class="sxs-lookup"><span data-stu-id="eafa9-123">Hero Card</span></span>](#hero-card) | <span data-ttu-id="eafa9-124">Обычно содержит одно крупное изображение, одну или несколько кнопок и небольшое количество текста.</span><span class="sxs-lookup"><span data-stu-id="eafa9-124">Typically contains a single large image, one or more buttons, and a small amount of text.</span></span> |
| [<span data-ttu-id="eafa9-125">Карточка списка</span><span class="sxs-lookup"><span data-stu-id="eafa9-125">List Card</span></span>](#list-card) | <span data-ttu-id="eafa9-126">Прокручиваемый список элементов.</span><span class="sxs-lookup"><span data-stu-id="eafa9-126">A scrolling list of items.</span></span> |
| [<span data-ttu-id="eafa9-127">Соединительная карта Office 365</span><span class="sxs-lookup"><span data-stu-id="eafa9-127">Office 365 Connector Card</span></span>](#office-365-connector-card) | <span data-ttu-id="eafa9-128">Гибкий макет с несколькими разделами, полями, изображениями и действиями.</span><span class="sxs-lookup"><span data-stu-id="eafa9-128">Flexible layout with multiple sections, fields, images and actions.</span></span> |
| [<span data-ttu-id="eafa9-129">Карточка приходной накладной</span><span class="sxs-lookup"><span data-stu-id="eafa9-129">Receipt Card</span></span>](#receipt-card) | <span data-ttu-id="eafa9-130">Предоставляет пользователю уведомление.</span><span class="sxs-lookup"><span data-stu-id="eafa9-130">Provides a receipt to the user.</span></span> |
| [<span data-ttu-id="eafa9-131">Карточка входа</span><span class="sxs-lookup"><span data-stu-id="eafa9-131">Signin Card</span></span>](#signin-card) | <span data-ttu-id="eafa9-132">Позволяет роботу отправить запрос на вход пользователя.</span><span class="sxs-lookup"><span data-stu-id="eafa9-132">Enables a bot to request that a user sign in.</span></span> |
| [<span data-ttu-id="eafa9-133">Карточка эскиза</span><span class="sxs-lookup"><span data-stu-id="eafa9-133">Thumbnail Card</span></span>](#thumbnail-card) | <span data-ttu-id="eafa9-134">Обычно содержит одно эскизное изображение, некоторый короткий текст, а также одну или несколько кнопок.</span><span class="sxs-lookup"><span data-stu-id="eafa9-134">Typically contains a single thumbnail image, some short text, and one or more buttons.</span></span> |
| [<span data-ttu-id="eafa9-135">Коллекции карточек</span><span class="sxs-lookup"><span data-stu-id="eafa9-135">Card Collections</span></span>](#card-collections) | <span data-ttu-id="eafa9-136">Используется для возвращения нескольких элементов в едином ответе</span><span class="sxs-lookup"><span data-stu-id="eafa9-136">Used to return multiple items in a single response</span></span> |

## <a name="common-properties-for-all-cards"></a><span data-ttu-id="eafa9-137">Общие свойства для всех карточек</span><span class="sxs-lookup"><span data-stu-id="eafa9-137">Common properties for all cards</span></span>

### <a name="inline-card-images"></a><span data-ttu-id="eafa9-138">Изображения в виде встроенных карточек</span><span class="sxs-lookup"><span data-stu-id="eafa9-138">Inline card images</span></span>

<span data-ttu-id="eafa9-139">Ваша карточка может содержать встроенное изображение, включив ссылку на общедоступное изображение.</span><span class="sxs-lookup"><span data-stu-id="eafa9-139">Your card can contain an inline image by including a link to your publicly available image.</span></span> <span data-ttu-id="eafa9-140">В целях повышения производительности мы настоятельно рекомендуем размещать образ в общедоступной сети обмена контентом (CDN).</span><span class="sxs-lookup"><span data-stu-id="eafa9-140">For performance purposes we highly recommend you host your image on a public content-delivery network (CDN).</span></span>

<span data-ttu-id="eafa9-141">Изображения масштабируются вверх или вниз, сохраняя пропорции изображения, а затем обрезаются из центра для достижения соответствующих пропорций карточки.</span><span class="sxs-lookup"><span data-stu-id="eafa9-141">Images are scaled up or down in size while maintaining the aspect ratio to cover the image area, and then cropped from center to achieve the appropriate aspect ratio for the card.</span></span>

<span data-ttu-id="eafa9-142">Изображения должны быть не менее 1024 × 1024 и 1 МБ в формате PNG, JPEG или GIF; анимированный GIF-файл не поддерживается официально.</span><span class="sxs-lookup"><span data-stu-id="eafa9-142">Images must be at most 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF is not officially supported.</span></span>

| <span data-ttu-id="eafa9-143">Свойство</span><span class="sxs-lookup"><span data-stu-id="eafa9-143">Property</span></span> | <span data-ttu-id="eafa9-144">Тип</span><span class="sxs-lookup"><span data-stu-id="eafa9-144">Type</span></span>  | <span data-ttu-id="eafa9-145">Описание</span><span class="sxs-lookup"><span data-stu-id="eafa9-145">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="eafa9-146">url</span><span class="sxs-lookup"><span data-stu-id="eafa9-146">url</span></span> | <span data-ttu-id="eafa9-147">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="eafa9-147">URL</span></span> | <span data-ttu-id="eafa9-148">URL-адрес HTTPS для изображения</span><span class="sxs-lookup"><span data-stu-id="eafa9-148">HTTPS URL to the image</span></span> |
| <span data-ttu-id="eafa9-149">alt</span><span class="sxs-lookup"><span data-stu-id="eafa9-149">alt</span></span> | <span data-ttu-id="eafa9-150">String</span><span class="sxs-lookup"><span data-stu-id="eafa9-150">String</span></span> | <span data-ttu-id="eafa9-151">Доступное описание изображения</span><span class="sxs-lookup"><span data-stu-id="eafa9-151">Accessible description of the image</span></span> |

### <a name="buttons"></a><span data-ttu-id="eafa9-152">Кнопки</span><span class="sxs-lookup"><span data-stu-id="eafa9-152">Buttons</span></span>

<span data-ttu-id="eafa9-153">Кнопки отображаются в нижней части карточки.</span><span class="sxs-lookup"><span data-stu-id="eafa9-153">Buttons are shown stacked at the bottom of the card.</span></span> <span data-ttu-id="eafa9-154">Текст на кнопке всегда находится в одной строке и будет обрезан, если текст превышает ширину кнопки.</span><span class="sxs-lookup"><span data-stu-id="eafa9-154">Button text is always on a single line and will be truncated if the text exceeds the button width.</span></span> <span data-ttu-id="eafa9-155">Все дополнительные кнопки, превышающие максимальное число, поддерживаемое картой, не будут отображаться.</span><span class="sxs-lookup"><span data-stu-id="eafa9-155">Any additional buttons beyond the maximum number supported by the card will not be shown.</span></span>

<span data-ttu-id="eafa9-156">Для получения дополнительных сведений просмотрите [действия с картой](~/task-modules-and-cards/cards/cards-actions.md) .</span><span class="sxs-lookup"><span data-stu-id="eafa9-156">See [Card Actions](~/task-modules-and-cards/cards/cards-actions.md) for more information.</span></span>

### <a name="card-formatting"></a><span data-ttu-id="eafa9-157">Форматирование карточки</span><span class="sxs-lookup"><span data-stu-id="eafa9-157">Card Formatting</span></span>

<span data-ttu-id="eafa9-158">Дополнительные сведения о форматировании текста [в карточках см.](~/task-modules-and-cards/cards/cards-format.md)</span><span class="sxs-lookup"><span data-stu-id="eafa9-158">See [Card Formatting](~/task-modules-and-cards/cards/cards-format.md) for more information on text formatting in cards.</span></span>

## <a name="adaptive-card"></a><span data-ttu-id="eafa9-159">Адаптивная карта</span><span class="sxs-lookup"><span data-stu-id="eafa9-159">Adaptive card</span></span>

<span data-ttu-id="eafa9-160">Настраиваемая карточка, которая может содержать любую комбинацию текста, речи, изображений, кнопок и полей ввода.</span><span class="sxs-lookup"><span data-stu-id="eafa9-160">A customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> <span data-ttu-id="eafa9-161">*Просмотрите раздел* [адаптивные карточки v 1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span><span class="sxs-lookup"><span data-stu-id="eafa9-161">*See* [Adaptive Cards v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span></span>

### <a name="support-for-adaptive-cards"></a><span data-ttu-id="eafa9-162">Поддержка адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="eafa9-162">Support for Adaptive cards</span></span>

| <span data-ttu-id="eafa9-163">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="eafa9-163">Bots in Teams</span></span> | <span data-ttu-id="eafa9-164">Расширения для сообщений</span><span class="sxs-lookup"><span data-stu-id="eafa9-164">Messaging Extensions</span></span>  | <span data-ttu-id="eafa9-165">Соединители</span><span class="sxs-lookup"><span data-stu-id="eafa9-165">Connectors</span></span> | <span data-ttu-id="eafa9-166">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="eafa9-166">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="eafa9-167">✔</span><span class="sxs-lookup"><span data-stu-id="eafa9-167">✔</span></span> | <span data-ttu-id="eafa9-168">✔</span><span class="sxs-lookup"><span data-stu-id="eafa9-168">✔</span></span> | <span data-ttu-id="eafa9-169">✖</span><span class="sxs-lookup"><span data-stu-id="eafa9-169">✖</span></span> | <span data-ttu-id="eafa9-170">✔</span><span class="sxs-lookup"><span data-stu-id="eafa9-170">✔</span></span> |
|

### <a name="example-adaptive-card"></a><span data-ttu-id="eafa9-171">Пример адаптивной карточки</span><span class="sxs-lookup"><span data-stu-id="eafa9-171">Example Adaptive card</span></span>

![Пример адаптивной карточки карты](~/assets/images/cards/adaptivecard.png)

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

#### <a name="for-more-information-on-adaptive-cards"></a><span data-ttu-id="eafa9-173">Дополнительные сведения о адаптивных картах</span><span class="sxs-lookup"><span data-stu-id="eafa9-173">For more information on Adaptive cards</span></span>

* [<span data-ttu-id="eafa9-174">Обзор адаптивных карточек</span><span class="sxs-lookup"><span data-stu-id="eafa9-174">Adaptive Cards Overview</span></span>](/adaptive-cards/)
* [<span data-ttu-id="eafa9-175">Действия адаптивной карточки в Teams</span><span class="sxs-lookup"><span data-stu-id="eafa9-175">Adaptive card actions in Teams</span></span>](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)

## <a name="hero-card"></a><span data-ttu-id="eafa9-176">Карточка главный Имиджевый баннер</span><span class="sxs-lookup"><span data-stu-id="eafa9-176">Hero card</span></span>

<span data-ttu-id="eafa9-177">Карточка, которая обычно содержит одно крупное изображение, одну или несколько кнопок и текста.</span><span class="sxs-lookup"><span data-stu-id="eafa9-177">A card that typically contains a single large image, one or more buttons and text.</span></span>

### <a name="support-for-hero-cards"></a><span data-ttu-id="eafa9-178">Поддержка карточек главный Имиджевый баннер</span><span class="sxs-lookup"><span data-stu-id="eafa9-178">Support for Hero cards</span></span>

| <span data-ttu-id="eafa9-179">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="eafa9-179">Bots in Teams</span></span> | <span data-ttu-id="eafa9-180">Расширения для сообщений</span><span class="sxs-lookup"><span data-stu-id="eafa9-180">Messaging Extensions</span></span>  | <span data-ttu-id="eafa9-181">Соединители</span><span class="sxs-lookup"><span data-stu-id="eafa9-181">Connectors</span></span> | <span data-ttu-id="eafa9-182">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="eafa9-182">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="eafa9-183">✔</span><span class="sxs-lookup"><span data-stu-id="eafa9-183">✔</span></span> | <span data-ttu-id="eafa9-184">✔</span><span class="sxs-lookup"><span data-stu-id="eafa9-184">✔</span></span> | <span data-ttu-id="eafa9-185">✖</span><span class="sxs-lookup"><span data-stu-id="eafa9-185">✖</span></span> | <span data-ttu-id="eafa9-186">✔</span><span class="sxs-lookup"><span data-stu-id="eafa9-186">✔</span></span> |
|

### <a name="properties-of-a-hero-card"></a><span data-ttu-id="eafa9-187">Свойства карточки главный Имиджевый баннер</span><span class="sxs-lookup"><span data-stu-id="eafa9-187">Properties of a Hero card</span></span>

| <span data-ttu-id="eafa9-188">Свойство</span><span class="sxs-lookup"><span data-stu-id="eafa9-188">Property</span></span> | <span data-ttu-id="eafa9-189">Тип</span><span class="sxs-lookup"><span data-stu-id="eafa9-189">Type</span></span>  | <span data-ttu-id="eafa9-190">Описание</span><span class="sxs-lookup"><span data-stu-id="eafa9-190">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="eafa9-191">title</span><span class="sxs-lookup"><span data-stu-id="eafa9-191">title</span></span> | <span data-ttu-id="eafa9-192">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="eafa9-192">Rich text</span></span> | <span data-ttu-id="eafa9-193">Название карточки.</span><span class="sxs-lookup"><span data-stu-id="eafa9-193">Title of the card.</span></span> <span data-ttu-id="eafa9-194">Максимум 2 строки; форматирование в настоящее время не поддерживается</span><span class="sxs-lookup"><span data-stu-id="eafa9-194">Maximum 2 lines; formatting not currently supported</span></span> |
| <span data-ttu-id="eafa9-195">Подзаголовок</span><span class="sxs-lookup"><span data-stu-id="eafa9-195">subtitle</span></span> | <span data-ttu-id="eafa9-196">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="eafa9-196">Rich text</span></span> | <span data-ttu-id="eafa9-197">Подзаголовок карточки.</span><span class="sxs-lookup"><span data-stu-id="eafa9-197">Subtitle of the card.</span></span> <span data-ttu-id="eafa9-198">Максимум 2 строки; форматирование в настоящее время не поддерживается</span><span class="sxs-lookup"><span data-stu-id="eafa9-198">Maximum 2 lines; formatting not currently supported</span></span> |
| <span data-ttu-id="eafa9-199">текст</span><span class="sxs-lookup"><span data-stu-id="eafa9-199">text</span></span> | <span data-ttu-id="eafa9-200">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="eafa9-200">Rich text</span></span> | <span data-ttu-id="eafa9-201">Текст отображается сразу под подназванием; сведения о [форматировании карточек](~/task-modules-and-cards/cards/cards-format.md) для параметров форматирования</span><span class="sxs-lookup"><span data-stu-id="eafa9-201">Text appears just below the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options</span></span> |
| <span data-ttu-id="eafa9-202">изображения</span><span class="sxs-lookup"><span data-stu-id="eafa9-202">images</span></span> | <span data-ttu-id="eafa9-203">Массив изображений</span><span class="sxs-lookup"><span data-stu-id="eafa9-203">Array of images</span></span> | <span data-ttu-id="eafa9-204">Изображение, отображаемое в верхней части карточки.</span><span class="sxs-lookup"><span data-stu-id="eafa9-204">Image displayed at top of card.</span></span> <span data-ttu-id="eafa9-205">Пропорции 16:9</span><span class="sxs-lookup"><span data-stu-id="eafa9-205">Aspect ratio 16:9</span></span> |
| <span data-ttu-id="eafa9-206">Button</span><span class="sxs-lookup"><span data-stu-id="eafa9-206">buttons</span></span> | <span data-ttu-id="eafa9-207">Массив объектов Action</span><span class="sxs-lookup"><span data-stu-id="eafa9-207">Array of action objects</span></span> | <span data-ttu-id="eafa9-208">Набор действий, применяемых к текущей карточке.</span><span class="sxs-lookup"><span data-stu-id="eafa9-208">Set of actions applicable to the current card.</span></span> <span data-ttu-id="eafa9-209">Максимум 6</span><span class="sxs-lookup"><span data-stu-id="eafa9-209">Maximum 6</span></span> |
| <span data-ttu-id="eafa9-210">тематическ</span><span class="sxs-lookup"><span data-stu-id="eafa9-210">tap</span></span> | <span data-ttu-id="eafa9-211">Объект Action</span><span class="sxs-lookup"><span data-stu-id="eafa9-211">Action object</span></span> | <span data-ttu-id="eafa9-212">Это действие активируется, когда пользователь найдет на саму карточку</span><span class="sxs-lookup"><span data-stu-id="eafa9-212">This action will be activated when the user taps on the card itself</span></span> |
|

### <a name="example-hero-card"></a><span data-ttu-id="eafa9-213">Пример карточки главный Имиджевый баннер</span><span class="sxs-lookup"><span data-stu-id="eafa9-213">Example Hero card</span></span>

![Пример карточки главный Имиджевый баннер](~/assets/images/cards/hero.png)

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

### <a name="for-more-information-on-hero-cards"></a><span data-ttu-id="eafa9-215">Дополнительные сведения о карточках главный Имиджевый баннер</span><span class="sxs-lookup"><span data-stu-id="eafa9-215">For more information on Hero cards</span></span>

<span data-ttu-id="eafa9-216">Справочные материалы по платформе Bot:</span><span class="sxs-lookup"><span data-stu-id="eafa9-216">Bot Framework reference:</span></span>

* [<span data-ttu-id="eafa9-217">Узел карточки главный Имиджевый баннер</span><span class="sxs-lookup"><span data-stu-id="eafa9-217">Hero card Node</span></span>](https://docs.microsoft.com/javascript/api/botframework-schema/herocard)
* [<span data-ttu-id="eafa9-218">Карточка главный Имиджевый баннер C #</span><span class="sxs-lookup"><span data-stu-id="eafa9-218">Hero card C#</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.herocard?view=botbuilder-dotnet-3.0)

## <a name="list-card"></a><span data-ttu-id="eafa9-219">Карточка списка</span><span class="sxs-lookup"><span data-stu-id="eafa9-219">List card</span></span>

<span data-ttu-id="eafa9-220">В Microsoft Teams карточка списка была добавлена для предоставления функций, помимо того, что может предоставить коллекция списков.</span><span class="sxs-lookup"><span data-stu-id="eafa9-220">The list card has been added by Teams to provide functions beyond what the list collection can provide.</span></span> <span data-ttu-id="eafa9-221">Карточка List предоставляет прокручиваемый список элементов.</span><span class="sxs-lookup"><span data-stu-id="eafa9-221">The list card provides a scrolling list of items.</span></span>

### <a name="support-for-list-cards"></a><span data-ttu-id="eafa9-222">Поддержка карточек со списками</span><span class="sxs-lookup"><span data-stu-id="eafa9-222">Support for List cards</span></span>

| <span data-ttu-id="eafa9-223">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="eafa9-223">Bots in Teams</span></span> | <span data-ttu-id="eafa9-224">Расширения для сообщений</span><span class="sxs-lookup"><span data-stu-id="eafa9-224">Messaging Extensions</span></span>  | <span data-ttu-id="eafa9-225">Соединители</span><span class="sxs-lookup"><span data-stu-id="eafa9-225">Connectors</span></span> | <span data-ttu-id="eafa9-226">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="eafa9-226">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="eafa9-227">✔</span><span class="sxs-lookup"><span data-stu-id="eafa9-227">✔</span></span> | <span data-ttu-id="eafa9-228">✖</span><span class="sxs-lookup"><span data-stu-id="eafa9-228">✖</span></span> | <span data-ttu-id="eafa9-229">✖</span><span class="sxs-lookup"><span data-stu-id="eafa9-229">✖</span></span> |<span data-ttu-id="eafa9-230">✔</span><span class="sxs-lookup"><span data-stu-id="eafa9-230">✔</span></span> |
|

### <a name="properties-of-a-list-card"></a><span data-ttu-id="eafa9-231">Свойства карточки списка</span><span class="sxs-lookup"><span data-stu-id="eafa9-231">Properties of a List card</span></span>

| <span data-ttu-id="eafa9-232">Свойство</span><span class="sxs-lookup"><span data-stu-id="eafa9-232">Property</span></span> | <span data-ttu-id="eafa9-233">Тип</span><span class="sxs-lookup"><span data-stu-id="eafa9-233">Type</span></span>  | <span data-ttu-id="eafa9-234">Описание</span><span class="sxs-lookup"><span data-stu-id="eafa9-234">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="eafa9-235">title</span><span class="sxs-lookup"><span data-stu-id="eafa9-235">title</span></span> | <span data-ttu-id="eafa9-236">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="eafa9-236">Rich text</span></span> | <span data-ttu-id="eafa9-237">Название карточки.</span><span class="sxs-lookup"><span data-stu-id="eafa9-237">Title of the card.</span></span> <span data-ttu-id="eafa9-238">Максимум 2 строки; форматирование в настоящее время не поддерживается</span><span class="sxs-lookup"><span data-stu-id="eafa9-238">Maximum 2 lines; formatting not currently supported</span></span> |
| <span data-ttu-id="eafa9-239">items</span><span class="sxs-lookup"><span data-stu-id="eafa9-239">items</span></span> | <span data-ttu-id="eafa9-240">Массив элементов списка</span><span class="sxs-lookup"><span data-stu-id="eafa9-240">Array of list items</span></span>  ||
| <span data-ttu-id="eafa9-241">Button</span><span class="sxs-lookup"><span data-stu-id="eafa9-241">buttons</span></span> | <span data-ttu-id="eafa9-242">Массив объектов Action</span><span class="sxs-lookup"><span data-stu-id="eafa9-242">Array of action objects</span></span> | <span data-ttu-id="eafa9-243">Набор действий, применяемых к текущей карточке.</span><span class="sxs-lookup"><span data-stu-id="eafa9-243">Set of actions applicable to the current card.</span></span> <span data-ttu-id="eafa9-244">Не более 6.</span><span class="sxs-lookup"><span data-stu-id="eafa9-244">Maximum 6.</span></span> <span data-ttu-id="eafa9-245">Не отображается на мобильном устройстве.</span><span class="sxs-lookup"><span data-stu-id="eafa9-245">Does not render on mobile.</span></span> |
|

### <a name="example-list-card"></a><span data-ttu-id="eafa9-246">Пример карточки списка</span><span class="sxs-lookup"><span data-stu-id="eafa9-246">Example List card</span></span>

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

## <a name="office-365-connector-card"></a><span data-ttu-id="eafa9-247">Соединительная карта Office 365</span><span class="sxs-lookup"><span data-stu-id="eafa9-247">Office 365 connector card</span></span>

<span data-ttu-id="eafa9-248">Поддерживается в Microsoft Teams, а не в среде Bot.</span><span class="sxs-lookup"><span data-stu-id="eafa9-248">Supported in Teams, not in Bot Framework.</span></span>

<span data-ttu-id="eafa9-249">Соединительная карта Office 365 предоставляет гибкий макет с несколькими разделами, полями, изображениями и действиями.</span><span class="sxs-lookup"><span data-stu-id="eafa9-249">The Office 365 Connector card provides a flexible layout with multiple sections, fields, images, and actions.</span></span> <span data-ttu-id="eafa9-250">Эта карточка содержит карту подключателя, чтобы ее можно было использовать в Боты.</span><span class="sxs-lookup"><span data-stu-id="eafa9-250">This card encapsulates a connector card so that it can be used by bots.</span></span> <span data-ttu-id="eafa9-251">В разделе "Примечания" представлены различия между соединителными картами и картой O365.</span><span class="sxs-lookup"><span data-stu-id="eafa9-251">See the notes section for differences between connector cards and the O365 card.</span></span>

### <a name="support-for-office-365-connector-cards"></a><span data-ttu-id="eafa9-252">Поддержка карт соединителей Office 365</span><span class="sxs-lookup"><span data-stu-id="eafa9-252">Support for Office 365 connector cards</span></span>

| <span data-ttu-id="eafa9-253">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="eafa9-253">Bots in Teams</span></span> | <span data-ttu-id="eafa9-254">Расширения для сообщений</span><span class="sxs-lookup"><span data-stu-id="eafa9-254">Messaging Extensions</span></span>  | <span data-ttu-id="eafa9-255">Соединители</span><span class="sxs-lookup"><span data-stu-id="eafa9-255">Connectors</span></span> | <span data-ttu-id="eafa9-256">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="eafa9-256">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="eafa9-257">✔</span><span class="sxs-lookup"><span data-stu-id="eafa9-257">✔</span></span> | <span data-ttu-id="eafa9-258">✔</span><span class="sxs-lookup"><span data-stu-id="eafa9-258">✔</span></span> | <span data-ttu-id="eafa9-259">✔</span><span class="sxs-lookup"><span data-stu-id="eafa9-259">✔</span></span> | <span data-ttu-id="eafa9-260">✖</span><span class="sxs-lookup"><span data-stu-id="eafa9-260">✖</span></span> |
|

### <a name="properties-of-the-office-365-connector-card"></a><span data-ttu-id="eafa9-261">Свойства карточки соединителя Office 365</span><span class="sxs-lookup"><span data-stu-id="eafa9-261">Properties of the Office 365 connector card</span></span>

| <span data-ttu-id="eafa9-262">Свойство</span><span class="sxs-lookup"><span data-stu-id="eafa9-262">Property</span></span> | <span data-ttu-id="eafa9-263">Тип</span><span class="sxs-lookup"><span data-stu-id="eafa9-263">Type</span></span>  | <span data-ttu-id="eafa9-264">Описание</span><span class="sxs-lookup"><span data-stu-id="eafa9-264">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="eafa9-265">title</span><span class="sxs-lookup"><span data-stu-id="eafa9-265">title</span></span> | <span data-ttu-id="eafa9-266">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="eafa9-266">Rich text</span></span> | <span data-ttu-id="eafa9-267">Название карточки.</span><span class="sxs-lookup"><span data-stu-id="eafa9-267">Title of the card.</span></span> <span data-ttu-id="eafa9-268">Максимум 2 строки; форматирование в настоящее время не поддерживается</span><span class="sxs-lookup"><span data-stu-id="eafa9-268">Maximum 2 lines; formatting not currently supported</span></span> |
| <span data-ttu-id="eafa9-269">summary</span><span class="sxs-lookup"><span data-stu-id="eafa9-269">summary</span></span> | <span data-ttu-id="eafa9-270">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="eafa9-270">Rich text</span></span> | <span data-ttu-id="eafa9-271">Сводка по карточке.</span><span class="sxs-lookup"><span data-stu-id="eafa9-271">Summary of the card.</span></span> <span data-ttu-id="eafa9-272">Максимум 2 строки; форматирование в настоящее время не поддерживается</span><span class="sxs-lookup"><span data-stu-id="eafa9-272">Maximum 2 lines; formatting not currently supported</span></span> |
| <span data-ttu-id="eafa9-273">текст</span><span class="sxs-lookup"><span data-stu-id="eafa9-273">text</span></span> | <span data-ttu-id="eafa9-274">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="eafa9-274">Rich text</span></span> | <span data-ttu-id="eafa9-275">Текст отображается сразу под подназванием; сведения о [форматировании карточек](~/task-modules-and-cards/cards/cards-format.md) для параметров форматирования</span><span class="sxs-lookup"><span data-stu-id="eafa9-275">Text appears just below the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options</span></span> |
| <span data-ttu-id="eafa9-276">themeColor</span><span class="sxs-lookup"><span data-stu-id="eafa9-276">themeColor</span></span> | <span data-ttu-id="eafa9-277">ШЕСТНАДЦАТЕРИЧная строка</span><span class="sxs-lookup"><span data-stu-id="eafa9-277">HEX string</span></span> | <span data-ttu-id="eafa9-278">цвет, переопределяющий Акцентколор, предоставленный в манифесте приложения</span><span class="sxs-lookup"><span data-stu-id="eafa9-278">color that overrides the accentColor provided from the application manifest</span></span> |

### <a name="notes-on-the-office-365-connector-card"></a><span data-ttu-id="eafa9-279">Примечания к соединительной карте Office 365</span><span class="sxs-lookup"><span data-stu-id="eafa9-279">Notes on the Office 365 connector card</span></span>

<span data-ttu-id="eafa9-280">Карты соединителей Office 365 правильно работают в Microsoft Teams, включая [действия ActionCard](/outlook/actionable-messages/card-reference#actioncard-action).</span><span class="sxs-lookup"><span data-stu-id="eafa9-280">Office 365 Connector cards function properly on Microsoft Teams, including [ActionCard actions](/outlook/actionable-messages/card-reference#actioncard-action).</span></span>

<span data-ttu-id="eafa9-281">Одним из важных различий между использованием карт соединителей с соединителя и карт подключателя в Bot является обработка действий с картой.</span><span class="sxs-lookup"><span data-stu-id="eafa9-281">One important difference between using Connector cards from a Connector and using Connector cards in your bot is the handling of card actions.</span></span>

* <span data-ttu-id="eafa9-282">Для соединителя конечная точка получает полезные данные карточки через HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="eafa9-282">For a Connector, the endpoint receives the card payload via HTTP POST.</span></span>
* <span data-ttu-id="eafa9-283">Для элемента Bot `HttpPOST` действие запускает `invoke` действие, которое ОТПРАВЛЯЕТ только идентификатор действия и основной текст в Bot.</span><span class="sxs-lookup"><span data-stu-id="eafa9-283">For a bot, the `HttpPOST` action triggers an `invoke` activity that sends only the action ID and body to the bot.</span></span>

<span data-ttu-id="eafa9-284">Каждая соединительная карта может отображать не более 10 разделов, а каждый раздел может содержать не более 5 изображений и 5 действий.</span><span class="sxs-lookup"><span data-stu-id="eafa9-284">Each Connector card can display a maximum of 10 sections, and each section can contain a maximum of 5 images and 5 actions.</span></span>

> [!NOTE]
> <span data-ttu-id="eafa9-285">Дополнительные разделы, изображения или действия в сообщении не будут отображаться.</span><span class="sxs-lookup"><span data-stu-id="eafa9-285">Any additional sections, images, or actions in a message will not appear.</span></span>

<span data-ttu-id="eafa9-286">Все текстовые поля поддерживают Markdown и HTML.</span><span class="sxs-lookup"><span data-stu-id="eafa9-286">All text fields support Markdown and HTML.</span></span> <span data-ttu-id="eafa9-287">Вы можете управлять тем, какие разделы используют Markdown или HTML, задав `markdown` свойство в сообщении.</span><span class="sxs-lookup"><span data-stu-id="eafa9-287">You can control which sections use Markdown or HTML by setting the `markdown` property in a message.</span></span> <span data-ttu-id="eafa9-288">По умолчанию `markdown` имеет значение `true` ;, если вы хотите использовать HTML, задайте значение `markdown` `false` .</span><span class="sxs-lookup"><span data-stu-id="eafa9-288">By default, `markdown` is set to `true`; if you want to use HTML instead, set `markdown` to `false`.</span></span>

<span data-ttu-id="eafa9-289">Если указать `themeColor` свойство, оно переопределяет `accentColor` свойство в манифесте приложения.</span><span class="sxs-lookup"><span data-stu-id="eafa9-289">If you specify the `themeColor` property, it overrides the `accentColor` property in the app manifest.</span></span>

<span data-ttu-id="eafa9-290">Чтобы указать стиль отображения для `activityImage` , можно задать следующие значения `activityImageType` :</span><span class="sxs-lookup"><span data-stu-id="eafa9-290">To specify the rendering style for `activityImage`, you can set `activityImageType` as follows.</span></span>

| <span data-ttu-id="eafa9-291">Значение</span><span class="sxs-lookup"><span data-stu-id="eafa9-291">Value</span></span> | <span data-ttu-id="eafa9-292">Описание</span><span class="sxs-lookup"><span data-stu-id="eafa9-292">Description</span></span> |
| --- | --- |
| `avatar` | <span data-ttu-id="eafa9-293">Умолчани `activityImage`будет обрезан как круг</span><span class="sxs-lookup"><span data-stu-id="eafa9-293">Default; `activityImage` will be cropped as a circle</span></span> |
| `article` | <span data-ttu-id="eafa9-294">`activityImage`будет отображаться как прямоугольник и сохранять пропорции</span><span class="sxs-lookup"><span data-stu-id="eafa9-294">`activityImage` will be displayed as a rectangle and retain its aspect ratio</span></span> |

<span data-ttu-id="eafa9-295">Дополнительные сведения о свойствах карт соединителей можно узнать в статье [Справочник по карточкам сообщений с действиями](/outlook/actionable-messages/card-reference).</span><span class="sxs-lookup"><span data-stu-id="eafa9-295">For all other details about Connector card properties, see the [Actionable message card reference](/outlook/actionable-messages/card-reference).</span></span> <span data-ttu-id="eafa9-296">В настоящее время в Microsoft Teams в настоящее время не поддерживаются следующие свойства карточки соединителя:</span><span class="sxs-lookup"><span data-stu-id="eafa9-296">The only Connector card properties that Microsoft Teams does not currently support are as follows:</span></span>

* `heroImage`
* `hideOriginalBody`
* <span data-ttu-id="eafa9-297">`startGroup`(всегда обрабатываются как `true` в Teams)</span><span class="sxs-lookup"><span data-stu-id="eafa9-297">`startGroup` (always treated as `true` in Teams)</span></span>
* `originator`
* `correlationId`

### <a name="example-office-365-connector-card"></a><span data-ttu-id="eafa9-298">Пример карточки соединителя Office 365</span><span class="sxs-lookup"><span data-stu-id="eafa9-298">Example Office 365 connector card</span></span>

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

## <a name="receipt-card"></a><span data-ttu-id="eafa9-299">Карточка приходной накладной</span><span class="sxs-lookup"><span data-stu-id="eafa9-299">Receipt card</span></span>

<span data-ttu-id="eafa9-300">Поддерживается в Teams.</span><span class="sxs-lookup"><span data-stu-id="eafa9-300">Supported in Teams.</span></span>

<span data-ttu-id="eafa9-301">Карточка, позволяющая роботу получить уведомление для пользователя.</span><span class="sxs-lookup"><span data-stu-id="eafa9-301">A card that enables a bot to provide a receipt to the user.</span></span> <span data-ttu-id="eafa9-302">Как правило, он содержит список элементов, которые необходимо включить в сведения о получении, налогах и итогах, а также другие тексты.</span><span class="sxs-lookup"><span data-stu-id="eafa9-302">It typically contains the list of items to include on the receipt, tax and total information, and other text.</span></span>

### <a name="support-for-receipts-cards"></a><span data-ttu-id="eafa9-303">Поддержка карточек чеков</span><span class="sxs-lookup"><span data-stu-id="eafa9-303">Support for Receipts cards</span></span>

| <span data-ttu-id="eafa9-304">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="eafa9-304">Bots in Teams</span></span> | <span data-ttu-id="eafa9-305">Расширения для сообщений</span><span class="sxs-lookup"><span data-stu-id="eafa9-305">Messaging Extensions</span></span>  | <span data-ttu-id="eafa9-306">Соединители</span><span class="sxs-lookup"><span data-stu-id="eafa9-306">Connectors</span></span> | <span data-ttu-id="eafa9-307">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="eafa9-307">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="eafa9-308">✔</span><span class="sxs-lookup"><span data-stu-id="eafa9-308">✔</span></span> | <span data-ttu-id="eafa9-309">✔</span><span class="sxs-lookup"><span data-stu-id="eafa9-309">✔</span></span> | <span data-ttu-id="eafa9-310">✖</span><span class="sxs-lookup"><span data-stu-id="eafa9-310">✖</span></span> | <span data-ttu-id="eafa9-311">✔</span><span class="sxs-lookup"><span data-stu-id="eafa9-311">✔</span></span> |
|

### <a name="for-more-information-on-receipt-cards"></a><span data-ttu-id="eafa9-312">Дополнительные сведения о карточках прихода</span><span class="sxs-lookup"><span data-stu-id="eafa9-312">For more information on Receipt cards</span></span>

<span data-ttu-id="eafa9-313">Справочные материалы по платформе Bot:</span><span class="sxs-lookup"><span data-stu-id="eafa9-313">Bot Framework reference:</span></span>

* [<span data-ttu-id="eafa9-314">Узел карточки чеков</span><span class="sxs-lookup"><span data-stu-id="eafa9-314">Receipt card Node</span></span>](https://docs.microsoft.com/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest)
* [<span data-ttu-id="eafa9-315">Карточка прихода C #</span><span class="sxs-lookup"><span data-stu-id="eafa9-315">Receipt card C#</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.receiptcard?view=botbuilder-dotnet-3.0)

## <a name="signin-card"></a><span data-ttu-id="eafa9-316">Карточка входа</span><span class="sxs-lookup"><span data-stu-id="eafa9-316">Signin card</span></span>

<span data-ttu-id="eafa9-317">Карточка, позволяющая роботу отправить запрос на вход пользователя.</span><span class="sxs-lookup"><span data-stu-id="eafa9-317">A card that enables a bot to request that a user sign in.</span></span> <span data-ttu-id="eafa9-318">Поддерживается в Microsoft Teams в несколько разных формах, чем в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="eafa9-318">Supported in Teams in a slightly different form than is found in the Bot Framework.</span></span> <span data-ttu-id="eafa9-319">Карточка входа в Teams аналогична карте входа в Bot Framework с исключением, что карточка входа в Teams поддерживает только два действия: `signin` и `openUrl` .</span><span class="sxs-lookup"><span data-stu-id="eafa9-319">The signin card in Teams is similar to the signin card in the bot framework with the exception that the signin card in Teams only supports two actions: `signin` and `openUrl`.</span></span>

<span data-ttu-id="eafa9-320">*Действие SignIn* можно использовать с любой карточки в Teams, а не только с помощью карточки входа.</span><span class="sxs-lookup"><span data-stu-id="eafa9-320">The *signin action* can be used from any card in Teams, not just the signin card.</span></span> <span data-ttu-id="eafa9-321">Для получения дополнительных сведений о проверке подлинности обратитесь к разделу [Проверка подлинности Microsoft Teams для Боты](~/bots/how-to/authentication/auth-flow-bot.md) .</span><span class="sxs-lookup"><span data-stu-id="eafa9-321">See the topic [Microsoft Teams authentication flow for bots](~/bots/how-to/authentication/auth-flow-bot.md) for more details on authentication.</span></span>

### <a name="support-for-signin-cards"></a><span data-ttu-id="eafa9-322">Поддержка карточек входа</span><span class="sxs-lookup"><span data-stu-id="eafa9-322">Support for Signin cards</span></span>

| <span data-ttu-id="eafa9-323">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="eafa9-323">Bots in Teams</span></span> | <span data-ttu-id="eafa9-324">Расширения для сообщений</span><span class="sxs-lookup"><span data-stu-id="eafa9-324">Messaging Extensions</span></span>  | <span data-ttu-id="eafa9-325">Соединители</span><span class="sxs-lookup"><span data-stu-id="eafa9-325">Connectors</span></span> | <span data-ttu-id="eafa9-326">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="eafa9-326">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="eafa9-327">✔</span><span class="sxs-lookup"><span data-stu-id="eafa9-327">✔</span></span> | <span data-ttu-id="eafa9-328">✖</span><span class="sxs-lookup"><span data-stu-id="eafa9-328">✖</span></span> | <span data-ttu-id="eafa9-329">✖</span><span class="sxs-lookup"><span data-stu-id="eafa9-329">✖</span></span> | <span data-ttu-id="eafa9-330">✔</span><span class="sxs-lookup"><span data-stu-id="eafa9-330">✔</span></span> |
|

### <a name="for-more-information-on-signin-cards"></a><span data-ttu-id="eafa9-331">Дополнительные сведения о карточках входа</span><span class="sxs-lookup"><span data-stu-id="eafa9-331">For more information on Signin cards</span></span>

<span data-ttu-id="eafa9-332">Справочные материалы по платформе Bot:</span><span class="sxs-lookup"><span data-stu-id="eafa9-332">Bot Framework reference:</span></span>

* [<span data-ttu-id="eafa9-333">Узел карточки входа</span><span class="sxs-lookup"><span data-stu-id="eafa9-333">Signin card Node</span></span>](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest)
* [<span data-ttu-id="eafa9-334">Карточка входа в систему C #</span><span class="sxs-lookup"><span data-stu-id="eafa9-334">Signin card C#</span></span>](/dotnet/api/microsoft.bot.connector.signincard?view=botbuilder-dotnet-3.0)

## <a name="thumbnail-card"></a><span data-ttu-id="eafa9-335">Карточка эскиза</span><span class="sxs-lookup"><span data-stu-id="eafa9-335">Thumbnail card</span></span>

<span data-ttu-id="eafa9-336">Карточка, которая обычно содержит одно эскизное изображение, одну или несколько кнопок и текст.</span><span class="sxs-lookup"><span data-stu-id="eafa9-336">A card that typically contains a single thumbnail image, one or more buttons, and text.</span></span>

### <a name="support-for-thumbnail-cards"></a><span data-ttu-id="eafa9-337">Поддержка карт эскизов</span><span class="sxs-lookup"><span data-stu-id="eafa9-337">Support for Thumbnail cards</span></span>

| <span data-ttu-id="eafa9-338">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="eafa9-338">Bots in Teams</span></span> | <span data-ttu-id="eafa9-339">Расширения для сообщений</span><span class="sxs-lookup"><span data-stu-id="eafa9-339">Messaging Extensions</span></span>  | <span data-ttu-id="eafa9-340">Соединители</span><span class="sxs-lookup"><span data-stu-id="eafa9-340">Connectors</span></span> | <span data-ttu-id="eafa9-341">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="eafa9-341">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="eafa9-342">✔</span><span class="sxs-lookup"><span data-stu-id="eafa9-342">✔</span></span> | <span data-ttu-id="eafa9-343">✔</span><span class="sxs-lookup"><span data-stu-id="eafa9-343">✔</span></span> | <span data-ttu-id="eafa9-344">✖</span><span class="sxs-lookup"><span data-stu-id="eafa9-344">✖</span></span> | <span data-ttu-id="eafa9-345">✔</span><span class="sxs-lookup"><span data-stu-id="eafa9-345">✔</span></span> |
|

![Пример карточки эскиза](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a><span data-ttu-id="eafa9-347">Свойства карточки эскиза</span><span class="sxs-lookup"><span data-stu-id="eafa9-347">Properties of a Thumbnail card</span></span>

| <span data-ttu-id="eafa9-348">Свойство</span><span class="sxs-lookup"><span data-stu-id="eafa9-348">Property</span></span> | <span data-ttu-id="eafa9-349">Тип</span><span class="sxs-lookup"><span data-stu-id="eafa9-349">Type</span></span>  | <span data-ttu-id="eafa9-350">Описание</span><span class="sxs-lookup"><span data-stu-id="eafa9-350">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="eafa9-351">title</span><span class="sxs-lookup"><span data-stu-id="eafa9-351">title</span></span> | <span data-ttu-id="eafa9-352">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="eafa9-352">Rich text</span></span> | <span data-ttu-id="eafa9-353">Название карточки.</span><span class="sxs-lookup"><span data-stu-id="eafa9-353">Title of the card.</span></span> <span data-ttu-id="eafa9-354">Максимум 2 строки; форматирование в настоящее время не поддерживается</span><span class="sxs-lookup"><span data-stu-id="eafa9-354">Maximum 2 lines; formatting not currently supported</span></span> |
| <span data-ttu-id="eafa9-355">Подзаголовок</span><span class="sxs-lookup"><span data-stu-id="eafa9-355">subtitle</span></span> | <span data-ttu-id="eafa9-356">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="eafa9-356">Rich text</span></span> | <span data-ttu-id="eafa9-357">Подзаголовок карточки.</span><span class="sxs-lookup"><span data-stu-id="eafa9-357">Subtitle of the card.</span></span> <span data-ttu-id="eafa9-358">Максимум 2 строки; форматирование в настоящее время не поддерживается</span><span class="sxs-lookup"><span data-stu-id="eafa9-358">Maximum 2 lines; formatting not currently supported</span></span> |
| <span data-ttu-id="eafa9-359">текст</span><span class="sxs-lookup"><span data-stu-id="eafa9-359">text</span></span> | <span data-ttu-id="eafa9-360">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="eafa9-360">Rich text</span></span> | <span data-ttu-id="eafa9-361">Текст отображается сразу под подназванием; сведения о [форматировании карточек](~/task-modules-and-cards/cards/cards-format.md) для параметров форматирования</span><span class="sxs-lookup"><span data-stu-id="eafa9-361">Text appears just below the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options</span></span> |
| <span data-ttu-id="eafa9-362">изображения</span><span class="sxs-lookup"><span data-stu-id="eafa9-362">images</span></span> | <span data-ttu-id="eafa9-363">Массив изображений</span><span class="sxs-lookup"><span data-stu-id="eafa9-363">Array of images</span></span> | <span data-ttu-id="eafa9-364">Изображение, отображаемое в верхней части карточки.</span><span class="sxs-lookup"><span data-stu-id="eafa9-364">Image displayed at top of card.</span></span> <span data-ttu-id="eafa9-365">Пропорции 1:1 (квадрат)</span><span class="sxs-lookup"><span data-stu-id="eafa9-365">Aspect ratio 1:1 (square)</span></span> |
| <span data-ttu-id="eafa9-366">Button</span><span class="sxs-lookup"><span data-stu-id="eafa9-366">buttons</span></span> | <span data-ttu-id="eafa9-367">Массив объектов Action</span><span class="sxs-lookup"><span data-stu-id="eafa9-367">Array of action objects</span></span> | <span data-ttu-id="eafa9-368">Набор действий, применяемых к текущей карточке.</span><span class="sxs-lookup"><span data-stu-id="eafa9-368">Set of actions applicable to the current card.</span></span> <span data-ttu-id="eafa9-369">Максимум 6</span><span class="sxs-lookup"><span data-stu-id="eafa9-369">Maximum 6</span></span> |
| <span data-ttu-id="eafa9-370">тематическ</span><span class="sxs-lookup"><span data-stu-id="eafa9-370">tap</span></span> | <span data-ttu-id="eafa9-371">Объект Action</span><span class="sxs-lookup"><span data-stu-id="eafa9-371">Action object</span></span> | <span data-ttu-id="eafa9-372">Это действие активируется, когда пользователь найдет на саму карточку</span><span class="sxs-lookup"><span data-stu-id="eafa9-372">This action will be activated when the user taps on the card itself</span></span> |
|

### <a name="example-thumbnail-card"></a><span data-ttu-id="eafa9-373">Пример карточки эскиза</span><span class="sxs-lookup"><span data-stu-id="eafa9-373">Example Thumbnail card</span></span>

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

### <a name="for-more-information"></a><span data-ttu-id="eafa9-374">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="eafa9-374">For more information</span></span>

<span data-ttu-id="eafa9-375">Справочные материалы по платформе Bot:</span><span class="sxs-lookup"><span data-stu-id="eafa9-375">Bot Framework reference:</span></span>

* [<span data-ttu-id="eafa9-376">Узел карточки эскиза</span><span class="sxs-lookup"><span data-stu-id="eafa9-376">Thumbnail card Node</span></span>](https://docs.microsoft.com/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest)
* [<span data-ttu-id="eafa9-377">Карта с эскизом C #</span><span class="sxs-lookup"><span data-stu-id="eafa9-377">Thumbnail card C#</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.thumbnailcard?view=botbuilder-dotnet-3.0)

## <a name="card-collections"></a><span data-ttu-id="eafa9-378">Коллекции карточек</span><span class="sxs-lookup"><span data-stu-id="eafa9-378">Card collections</span></span>

<span data-ttu-id="eafa9-379">Коллекции карточек поддерживаются в Teams.</span><span class="sxs-lookup"><span data-stu-id="eafa9-379">Card collections are supported in Teams.</span></span>

<span data-ttu-id="eafa9-380">Коллекции карточек предоставляются с помощью Bot Framework: `builder.AttachmentLayout.carousel` и `builder.AttachmentLayout.list` .</span><span class="sxs-lookup"><span data-stu-id="eafa9-380">Card collections are provided by the Bot Framework: `builder.AttachmentLayout.carousel` and `builder.AttachmentLayout.list`.</span></span> <span data-ttu-id="eafa9-381">Эти коллекции могут содержать адаптивные, главный Имиджевый баннер или карты эскиза.</span><span class="sxs-lookup"><span data-stu-id="eafa9-381">These collections can contain Adaptive, Hero, or Thumbnail cards.</span></span>

## <a name="carousel-collection"></a><span data-ttu-id="eafa9-382">Коллекция обойм</span><span class="sxs-lookup"><span data-stu-id="eafa9-382">Carousel collection</span></span>

<span data-ttu-id="eafa9-383">[Макет обоймы](/azure/bot-service/dotnet/bot-builder-dotnet-add-rich-card-attachments?view=azure-bot-service-3.0) отображает обойму карточек (при необходимости) с соответствующими кнопками действия.</span><span class="sxs-lookup"><span data-stu-id="eafa9-383">The [carousel layout](/azure/bot-service/dotnet/bot-builder-dotnet-add-rich-card-attachments?view=azure-bot-service-3.0) shows a carousel of cards, optionally with associated action buttons.</span></span>

### <a name="support-for-carousel-collections"></a><span data-ttu-id="eafa9-384">Поддержка коллекций обойм</span><span class="sxs-lookup"><span data-stu-id="eafa9-384">Support for Carousel collections</span></span>

| <span data-ttu-id="eafa9-385">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="eafa9-385">Bots in Teams</span></span> | <span data-ttu-id="eafa9-386">Расширения для сообщений</span><span class="sxs-lookup"><span data-stu-id="eafa9-386">Messaging Extensions</span></span>  | <span data-ttu-id="eafa9-387">Соединители</span><span class="sxs-lookup"><span data-stu-id="eafa9-387">Connectors</span></span> | <span data-ttu-id="eafa9-388">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="eafa9-388">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="eafa9-389">✔</span><span class="sxs-lookup"><span data-stu-id="eafa9-389">✔</span></span> | <span data-ttu-id="eafa9-390">✖</span><span class="sxs-lookup"><span data-stu-id="eafa9-390">✖</span></span> | <span data-ttu-id="eafa9-391">✖</span><span class="sxs-lookup"><span data-stu-id="eafa9-391">✖</span></span> | <span data-ttu-id="eafa9-392">✔</span><span class="sxs-lookup"><span data-stu-id="eafa9-392">✔</span></span> |
|

> [!NOTE]
> <span data-ttu-id="eafa9-393">В обойме может отображаться не более 10 карточек для каждого сообщения.</span><span class="sxs-lookup"><span data-stu-id="eafa9-393">A carousel can display a maximum of 10 cards per message.</span></span>

### <a name="example-carousel-collection"></a><span data-ttu-id="eafa9-394">Пример коллекции обойм</span><span class="sxs-lookup"><span data-stu-id="eafa9-394">Example Carousel collection</span></span>

![Пример обоймы карточек](~/assets/images/cards/carousel.png)

<span data-ttu-id="eafa9-396">Это те же свойства, что и для карты главный Имиджевый баннер или эскиза.</span><span class="sxs-lookup"><span data-stu-id="eafa9-396">Properties are the same as for the hero or thumbnail card.</span></span>

### <a name="syntax-for-carousel-collections"></a><span data-ttu-id="eafa9-397">Синтаксис для коллекций обойм</span><span class="sxs-lookup"><span data-stu-id="eafa9-397">Syntax for Carousel collections</span></span>

`builder.AttachmentLayout.carousel`

## <a name="list-collection"></a><span data-ttu-id="eafa9-398">Коллекция List</span><span class="sxs-lookup"><span data-stu-id="eafa9-398">List collection</span></span>

### <a name="support-for-list-collections"></a><span data-ttu-id="eafa9-399">Поддержка коллекций списков</span><span class="sxs-lookup"><span data-stu-id="eafa9-399">Support for List collections</span></span>

<span data-ttu-id="eafa9-400">В раскладке списка отображается вертикальный список карточек, при необходимости связанные с ними кнопки действий.</span><span class="sxs-lookup"><span data-stu-id="eafa9-400">The list layout shows a vertically stacked list of cards, optionally with associated action buttons.</span></span>

| <span data-ttu-id="eafa9-401">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="eafa9-401">Bots in Teams</span></span> | <span data-ttu-id="eafa9-402">Расширения для сообщений</span><span class="sxs-lookup"><span data-stu-id="eafa9-402">Messaging Extensions</span></span>  | <span data-ttu-id="eafa9-403">Соединители</span><span class="sxs-lookup"><span data-stu-id="eafa9-403">Connectors</span></span> | <span data-ttu-id="eafa9-404">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="eafa9-404">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="eafa9-405">✔</span><span class="sxs-lookup"><span data-stu-id="eafa9-405">✔</span></span> | <span data-ttu-id="eafa9-406">✔</span><span class="sxs-lookup"><span data-stu-id="eafa9-406">✔</span></span> | <span data-ttu-id="eafa9-407">✖</span><span class="sxs-lookup"><span data-stu-id="eafa9-407">✖</span></span> | <span data-ttu-id="eafa9-408">✔</span><span class="sxs-lookup"><span data-stu-id="eafa9-408">✔</span></span> |
|

### <a name="example-list-collection"></a><span data-ttu-id="eafa9-409">Пример коллекции списков</span><span class="sxs-lookup"><span data-stu-id="eafa9-409">Example List collection</span></span>

![Пример списка карточек](~/assets/images/cards/list.png)

<span data-ttu-id="eafa9-411">Это те же свойства, что и для карты главный Имиджевый баннер или эскиза.</span><span class="sxs-lookup"><span data-stu-id="eafa9-411">Properties are the same as for the hero or thumbnail card.</span></span>

<span data-ttu-id="eafa9-412">В списке может отображаться не более 10 карточек для каждого сообщения.</span><span class="sxs-lookup"><span data-stu-id="eafa9-412">A list can display a maximum of 10 cards per message.</span></span>

> [!NOTE]
> <span data-ttu-id="eafa9-413">Некоторые комбинации карточек со списками пока не поддерживаются в iOS и Android.</span><span class="sxs-lookup"><span data-stu-id="eafa9-413">Some combinations of list cards are not yet supported on iOS and Android.</span></span>

### <a name="syntax-for-list-collections"></a><span data-ttu-id="eafa9-414">Синтаксис коллекций списков</span><span class="sxs-lookup"><span data-stu-id="eafa9-414">Syntax for List collections</span></span>

`builder.AttachmentLayout.list`

## <a name="cards-not-supported-in-teams"></a><span data-ttu-id="eafa9-415">Карточки, не поддерживаемые в Teams</span><span class="sxs-lookup"><span data-stu-id="eafa9-415">Cards not supported in Teams</span></span>

<span data-ttu-id="eafa9-416">Следующие карты реализуются с помощью Bot Framework, но не поддерживаются в Teams.</span><span class="sxs-lookup"><span data-stu-id="eafa9-416">The following cards are implemented by the Bot Framework, but are NOT supported by Teams.</span></span>

* <span data-ttu-id="eafa9-417">Карты анимации</span><span class="sxs-lookup"><span data-stu-id="eafa9-417">Animation cards</span></span>
* <span data-ttu-id="eafa9-418">Звуковые карты</span><span class="sxs-lookup"><span data-stu-id="eafa9-418">Audio cards</span></span>
* <span data-ttu-id="eafa9-419">Видеокарты</span><span class="sxs-lookup"><span data-stu-id="eafa9-419">Video cards</span></span>
