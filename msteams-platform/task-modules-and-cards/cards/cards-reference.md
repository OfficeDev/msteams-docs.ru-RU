---
title: Справочник по карточкам
description: Описывает все карточки и действия карточки, доступные боты в Teams.
keywords: Справочник по карточкам Боты
ms.openlocfilehash: 76b9cb7e2508d300deb2e3cd4f392fdb9850062d
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675372"
---
# <a name="cards-reference"></a><span data-ttu-id="cd5eb-104">Справочник по карточкам</span><span class="sxs-lookup"><span data-stu-id="cd5eb-104">Cards Reference</span></span>

<span data-ttu-id="cd5eb-105">Карточки, перечисленные в этом разделе, поддерживаются в боты для Teams.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-105">The cards listed in this section are supported in bots for Teams.</span></span> <span data-ttu-id="cd5eb-106">Они основаны на карточках, определенных с помощью Bot Framework, но в Teams не поддерживаются все карточки с интерфейсом Bot и добавлены некоторые из них.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-106">They are based on cards defined by the Bot Framework, but Teams does not support all Bot Framework cards and has added some of its own.</span></span> <span data-ttu-id="cd5eb-107">Различия вызываемы в приведенных ниже ссылках.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-107">Differences are called out in the references below.</span></span>

## <a name="card-examples"></a><span data-ttu-id="cd5eb-108">Примеры карточек</span><span class="sxs-lookup"><span data-stu-id="cd5eb-108">Card examples</span></span>

<span data-ttu-id="cd5eb-109">Дополнительные сведения об использовании карточек можно найти в документации по пакету SDK для Bot Builder (v3).</span><span class="sxs-lookup"><span data-stu-id="cd5eb-109">You can find additional information on how to use cards in the documentation for the Bot Builder SDK (v3).</span></span> <span data-ttu-id="cd5eb-110">Кроме того, вы можете найти примеры кода в репозитории Microsoft/Ботбуилдер-Samples на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-110">There are also code samples available in the Microsoft/BotBuilder-Samples repository on GitHub.</span></span>

* <span data-ttu-id="cd5eb-111">.NET</span><span class="sxs-lookup"><span data-stu-id="cd5eb-111">.NET</span></span>
  * [<span data-ttu-id="cd5eb-112">Добавление карточек в качестве вложений в сообщения</span><span class="sxs-lookup"><span data-stu-id="cd5eb-112">Add cards as attachments to messages</span></span>](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments)
  * [<span data-ttu-id="cd5eb-113">Пример кода карточек (построитель построителя)</span><span class="sxs-lookup"><span data-stu-id="cd5eb-113">Cards sample code (Bot Builder v3)</span></span>](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/CSharp/cards-RichCards)
* <span data-ttu-id="cd5eb-114">Node.js</span><span class="sxs-lookup"><span data-stu-id="cd5eb-114">Node.js</span></span>
  * [<span data-ttu-id="cd5eb-115">Добавление карточек в качестве вложений в сообщения</span><span class="sxs-lookup"><span data-stu-id="cd5eb-115">Add cards as attachments to messages</span></span>](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)
  * [<span data-ttu-id="cd5eb-116">Пример кода карточек (построитель построителя)</span><span class="sxs-lookup"><span data-stu-id="cd5eb-116">Cards sample code (Bot Builder v3)</span></span>](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/Node/cards-RichCards)

## <a name="types-of-cards"></a><span data-ttu-id="cd5eb-117">Типы карточек</span><span class="sxs-lookup"><span data-stu-id="cd5eb-117">Types of cards</span></span>

<span data-ttu-id="cd5eb-118">В этой таблице перечислены доступные типы карт.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-118">This table shows the types of cards available to you.</span></span>

| <span data-ttu-id="cd5eb-119">Тип карточки</span><span class="sxs-lookup"><span data-stu-id="cd5eb-119">Card Type</span></span> | <span data-ttu-id="cd5eb-120">Описание</span><span class="sxs-lookup"><span data-stu-id="cd5eb-120">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="cd5eb-121">Адаптивная карта</span><span class="sxs-lookup"><span data-stu-id="cd5eb-121">Adaptive Card</span></span>](#adaptive-card) | <span data-ttu-id="cd5eb-122">Карточка с широкими возможностями настройки, которая может содержать любую комбинацию текста, речи, изображений, кнопок и полей ввода.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-122">Highly customizable card that can contain any combination of text, speech, images, buttons and input fields.</span></span> |
| [<span data-ttu-id="cd5eb-123">Карточка главный Имиджевый баннер</span><span class="sxs-lookup"><span data-stu-id="cd5eb-123">Hero Card</span></span>](#hero-card) | <span data-ttu-id="cd5eb-124">Обычно содержит одно крупное изображение, одну или несколько кнопок и небольшое количество текста.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-124">Typically contains a single large image, one or more buttons, and a small amount of text.</span></span> |
| [<span data-ttu-id="cd5eb-125">Карточка списка</span><span class="sxs-lookup"><span data-stu-id="cd5eb-125">List Card</span></span>](#list-card) | <span data-ttu-id="cd5eb-126">Прокручиваемый список элементов.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-126">A scrolling list of items.</span></span> |
| [<span data-ttu-id="cd5eb-127">Соединительная карта Office 365</span><span class="sxs-lookup"><span data-stu-id="cd5eb-127">Office 365 Connector Card</span></span>](#office-365-connector-card) | <span data-ttu-id="cd5eb-128">Гибкий макет с несколькими разделами, полями, изображениями и действиями.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-128">Flexible layout with multiple sections, fields, images and actions.</span></span> |
| [<span data-ttu-id="cd5eb-129">Карточка приходной накладной</span><span class="sxs-lookup"><span data-stu-id="cd5eb-129">Receipt Card</span></span>](#receipt-card) | <span data-ttu-id="cd5eb-130">Предоставляет пользователю уведомление.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-130">Provides a receipt to the user.</span></span> |
| [<span data-ttu-id="cd5eb-131">Карточка входа</span><span class="sxs-lookup"><span data-stu-id="cd5eb-131">Signin Card</span></span>](#signin-card) | <span data-ttu-id="cd5eb-132">Позволяет роботу отправить запрос на вход пользователя.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-132">Enables a bot to request that a user sign in.</span></span> |
| [<span data-ttu-id="cd5eb-133">Карточка эскиза</span><span class="sxs-lookup"><span data-stu-id="cd5eb-133">Thumbnail Card</span></span>](#thumbnail-card) | <span data-ttu-id="cd5eb-134">Обычно содержит одно эскизное изображение, некоторый короткий текст, а также одну или несколько кнопок.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-134">Typically contains a single thumbnail image, some short text, and one or more buttons.</span></span> |
| [<span data-ttu-id="cd5eb-135">Коллекции карточек</span><span class="sxs-lookup"><span data-stu-id="cd5eb-135">Card Collections</span></span>](#card-collections) | <span data-ttu-id="cd5eb-136">Используется для возвращения нескольких элементов в едином ответе</span><span class="sxs-lookup"><span data-stu-id="cd5eb-136">Used to return multiple items in a single response</span></span> |

## <a name="common-properties-for-all-cards"></a><span data-ttu-id="cd5eb-137">Общие свойства для всех карточек</span><span class="sxs-lookup"><span data-stu-id="cd5eb-137">Common properties for all cards</span></span>

### <a name="inline-card-images"></a><span data-ttu-id="cd5eb-138">Изображения в виде встроенных карточек</span><span class="sxs-lookup"><span data-stu-id="cd5eb-138">Inline card images</span></span>

<span data-ttu-id="cd5eb-139">Ваша карточка может содержать встроенное изображение, включив ссылку на общедоступное изображение.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-139">Your card can contain an inline image by including a link to your publically available image.</span></span> <span data-ttu-id="cd5eb-140">В целях повышения производительности мы настоятельно рекомендуем размещать образ в общедоступной сети обмена контентом (CDN).</span><span class="sxs-lookup"><span data-stu-id="cd5eb-140">For performance purposes we highly recommend you host your image on a public content-delivery network (CDN).</span></span>

<span data-ttu-id="cd5eb-141">Изображения масштабируются вверх или вниз, сохраняя пропорции изображения, а затем обрезаются из центра для достижения соответствующих пропорций карточки.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-141">Images are scaled up or down in size while maintaining the aspect ratio to cover the image area, and then cropped from center to achieve the appropriate aspect ratio for the card.</span></span>

<span data-ttu-id="cd5eb-142">Изображения должны быть не менее 1024 × 1024 и 1 МБ в формате PNG, JPEG или GIF; анимированный GIF-файл не поддерживается официально.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-142">Images must be at most 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF is not officially supported.</span></span>

| <span data-ttu-id="cd5eb-143">Свойство</span><span class="sxs-lookup"><span data-stu-id="cd5eb-143">Property</span></span> | <span data-ttu-id="cd5eb-144">Тип</span><span class="sxs-lookup"><span data-stu-id="cd5eb-144">Type</span></span>  | <span data-ttu-id="cd5eb-145">Описание</span><span class="sxs-lookup"><span data-stu-id="cd5eb-145">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cd5eb-146">url</span><span class="sxs-lookup"><span data-stu-id="cd5eb-146">url</span></span> | <span data-ttu-id="cd5eb-147">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="cd5eb-147">URL</span></span> | <span data-ttu-id="cd5eb-148">URL-адрес HTTPS для изображения</span><span class="sxs-lookup"><span data-stu-id="cd5eb-148">HTTPS URL to the image</span></span> |
| <span data-ttu-id="cd5eb-149">alt</span><span class="sxs-lookup"><span data-stu-id="cd5eb-149">alt</span></span> | <span data-ttu-id="cd5eb-150">String</span><span class="sxs-lookup"><span data-stu-id="cd5eb-150">String</span></span> | <span data-ttu-id="cd5eb-151">Доступное описание изображения</span><span class="sxs-lookup"><span data-stu-id="cd5eb-151">Accessible description of the image</span></span> |

### <a name="buttons"></a><span data-ttu-id="cd5eb-152">Кнопки</span><span class="sxs-lookup"><span data-stu-id="cd5eb-152">Buttons</span></span>

<span data-ttu-id="cd5eb-153">Кнопки отображаются в нижней части карточки.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-153">Buttons are shown stacked at the bottom of the card.</span></span> <span data-ttu-id="cd5eb-154">Текст на кнопке всегда находится в одной строке и будет обрезан, если текст превышает ширину кнопки.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-154">Button text is always on a single line and will be truncated if the text exceeds the button width.</span></span> <span data-ttu-id="cd5eb-155">Все дополнительные кнопки, превышающие максимальное число, поддерживаемое картой, не будут отображаться.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-155">Any additional buttons beyond the maximum number supported by the card will not be shown.</span></span>

<span data-ttu-id="cd5eb-156">Для получения дополнительных сведений просмотрите [действия с картой](~/task-modules-and-cards/cards/cards-actions.md) .</span><span class="sxs-lookup"><span data-stu-id="cd5eb-156">See [Card Actions](~/task-modules-and-cards/cards/cards-actions.md) for more information.</span></span>

### <a name="card-formatting"></a><span data-ttu-id="cd5eb-157">Форматирование карточки</span><span class="sxs-lookup"><span data-stu-id="cd5eb-157">Card Formatting</span></span>

<span data-ttu-id="cd5eb-158">Дополнительные сведения о форматировании текста [в карточках см.](~/task-modules-and-cards/cards/cards-format.md)</span><span class="sxs-lookup"><span data-stu-id="cd5eb-158">See [Card Formatting](~/task-modules-and-cards/cards/cards-format.md) for more information on text formatting in cards.</span></span>

## <a name="adaptive-card"></a><span data-ttu-id="cd5eb-159">Адаптивная карта</span><span class="sxs-lookup"><span data-stu-id="cd5eb-159">Adaptive card</span></span>

> [!NOTE]
> <span data-ttu-id="cd5eb-160">Для всех пользователей поддерживается только адаптивные карты версии 1,0.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-160">Only version 1.0 of Adaptive Cards is supported for all users.</span></span> <span data-ttu-id="cd5eb-161">В настоящее время версия 1,2 доступна только в предварительной версии для разработчиков</span><span class="sxs-lookup"><span data-stu-id="cd5eb-161">Version 1.2 is currently available only in Developer Preview</span></span>

<span data-ttu-id="cd5eb-162">Настраиваемая карточка, которая может содержать любую комбинацию текста, речи, изображений, кнопок и полей ввода.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-162">A customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span>

### <a name="support-for-adaptive-cards"></a><span data-ttu-id="cd5eb-163">Поддержка адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="cd5eb-163">Support for Adaptive cards</span></span>

| <span data-ttu-id="cd5eb-164">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="cd5eb-164">Bots in Teams</span></span> | <span data-ttu-id="cd5eb-165">Расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="cd5eb-165">Messaging Extensions</span></span>  | <span data-ttu-id="cd5eb-166">Соединители</span><span class="sxs-lookup"><span data-stu-id="cd5eb-166">Connectors</span></span> | <span data-ttu-id="cd5eb-167">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="cd5eb-167">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="cd5eb-168">✔</span><span class="sxs-lookup"><span data-stu-id="cd5eb-168">✔</span></span> | <span data-ttu-id="cd5eb-169">✔</span><span class="sxs-lookup"><span data-stu-id="cd5eb-169">✔</span></span> | <span data-ttu-id="cd5eb-170">✖</span><span class="sxs-lookup"><span data-stu-id="cd5eb-170">✖</span></span> | <span data-ttu-id="cd5eb-171">✔</span><span class="sxs-lookup"><span data-stu-id="cd5eb-171">✔</span></span> |
|

### <a name="example-adaptive-card"></a><span data-ttu-id="cd5eb-172">Пример адаптивной карточки</span><span class="sxs-lookup"><span data-stu-id="cd5eb-172">Example Adaptive card</span></span>

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

#### <a name="for-more-information-on-adaptive-cards"></a><span data-ttu-id="cd5eb-174">Дополнительные сведения о адаптивных картах</span><span class="sxs-lookup"><span data-stu-id="cd5eb-174">For more information on Adaptive cards</span></span>

* [<span data-ttu-id="cd5eb-175">Обзор адаптивных карточек</span><span class="sxs-lookup"><span data-stu-id="cd5eb-175">Adaptive Cards Overview</span></span>](/adaptive-cards/)
* [<span data-ttu-id="cd5eb-176">Действия адаптивной карточки в Teams</span><span class="sxs-lookup"><span data-stu-id="cd5eb-176">Adaptive card actions in Teams</span></span>](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)

## <a name="hero-card"></a><span data-ttu-id="cd5eb-177">Карточка главный Имиджевый баннер</span><span class="sxs-lookup"><span data-stu-id="cd5eb-177">Hero card</span></span>

<span data-ttu-id="cd5eb-178">Карточка, которая обычно содержит одно крупное изображение, одну или несколько кнопок и текста.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-178">A card that typically contains a single large image, one or more buttons and text.</span></span>

### <a name="support-for-hero-cards"></a><span data-ttu-id="cd5eb-179">Поддержка карточек главный Имиджевый баннер</span><span class="sxs-lookup"><span data-stu-id="cd5eb-179">Support for Hero cards</span></span>

| <span data-ttu-id="cd5eb-180">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="cd5eb-180">Bots in Teams</span></span> | <span data-ttu-id="cd5eb-181">Расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="cd5eb-181">Messaging Extensions</span></span>  | <span data-ttu-id="cd5eb-182">Соединители</span><span class="sxs-lookup"><span data-stu-id="cd5eb-182">Connectors</span></span> | <span data-ttu-id="cd5eb-183">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="cd5eb-183">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="cd5eb-184">✔</span><span class="sxs-lookup"><span data-stu-id="cd5eb-184">✔</span></span> | <span data-ttu-id="cd5eb-185">✔</span><span class="sxs-lookup"><span data-stu-id="cd5eb-185">✔</span></span> | <span data-ttu-id="cd5eb-186">✖</span><span class="sxs-lookup"><span data-stu-id="cd5eb-186">✖</span></span> | <span data-ttu-id="cd5eb-187">✔</span><span class="sxs-lookup"><span data-stu-id="cd5eb-187">✔</span></span> |
|

### <a name="properties-of-a-hero-card"></a><span data-ttu-id="cd5eb-188">Свойства карточки главный Имиджевый баннер</span><span class="sxs-lookup"><span data-stu-id="cd5eb-188">Properties of a Hero card</span></span>

| <span data-ttu-id="cd5eb-189">Свойство</span><span class="sxs-lookup"><span data-stu-id="cd5eb-189">Property</span></span> | <span data-ttu-id="cd5eb-190">Тип</span><span class="sxs-lookup"><span data-stu-id="cd5eb-190">Type</span></span>  | <span data-ttu-id="cd5eb-191">Описание</span><span class="sxs-lookup"><span data-stu-id="cd5eb-191">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cd5eb-192">title</span><span class="sxs-lookup"><span data-stu-id="cd5eb-192">title</span></span> | <span data-ttu-id="cd5eb-193">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="cd5eb-193">Rich text</span></span> | <span data-ttu-id="cd5eb-194">Название карточки.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-194">Title of the card.</span></span> <span data-ttu-id="cd5eb-195">Максимум 2 строки; форматирование в настоящее время не поддерживается</span><span class="sxs-lookup"><span data-stu-id="cd5eb-195">Maximum 2 lines; formatting not currently supported</span></span> |
| <span data-ttu-id="cd5eb-196">Подзаголовок</span><span class="sxs-lookup"><span data-stu-id="cd5eb-196">subtitle</span></span> | <span data-ttu-id="cd5eb-197">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="cd5eb-197">Rich text</span></span> | <span data-ttu-id="cd5eb-198">Подзаголовок карточки.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-198">Subtitle of the card.</span></span> <span data-ttu-id="cd5eb-199">Максимум 2 строки; форматирование в настоящее время не поддерживается</span><span class="sxs-lookup"><span data-stu-id="cd5eb-199">Maximum 2 lines; formatting not currently supported</span></span> |
| <span data-ttu-id="cd5eb-200">текст</span><span class="sxs-lookup"><span data-stu-id="cd5eb-200">text</span></span> | <span data-ttu-id="cd5eb-201">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="cd5eb-201">Rich text</span></span> | <span data-ttu-id="cd5eb-202">Текст отображается сразу под подназванием; сведения о [форматировании карточек](~/task-modules-and-cards/cards/cards-format.md) для параметров форматирования</span><span class="sxs-lookup"><span data-stu-id="cd5eb-202">Text appears just below the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options</span></span> |
| <span data-ttu-id="cd5eb-203">изображения</span><span class="sxs-lookup"><span data-stu-id="cd5eb-203">images</span></span> | <span data-ttu-id="cd5eb-204">Массив изображений</span><span class="sxs-lookup"><span data-stu-id="cd5eb-204">Array of images</span></span> | <span data-ttu-id="cd5eb-205">Изображение, отображаемое в верхней части карточки.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-205">Image displayed at top of card.</span></span> <span data-ttu-id="cd5eb-206">Пропорции 16:9</span><span class="sxs-lookup"><span data-stu-id="cd5eb-206">Aspect ratio 16:9</span></span> |
| <span data-ttu-id="cd5eb-207">Button</span><span class="sxs-lookup"><span data-stu-id="cd5eb-207">buttons</span></span> | <span data-ttu-id="cd5eb-208">Массив объектов Action</span><span class="sxs-lookup"><span data-stu-id="cd5eb-208">Array of action objects</span></span> | <span data-ttu-id="cd5eb-209">Набор действий, применяемых к текущей карточке.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-209">Set of actions applicable to the current card.</span></span> <span data-ttu-id="cd5eb-210">Максимум 6</span><span class="sxs-lookup"><span data-stu-id="cd5eb-210">Maximum 6</span></span> |
| <span data-ttu-id="cd5eb-211">тематическ</span><span class="sxs-lookup"><span data-stu-id="cd5eb-211">tap</span></span> | <span data-ttu-id="cd5eb-212">Объект Action</span><span class="sxs-lookup"><span data-stu-id="cd5eb-212">Action object</span></span> | <span data-ttu-id="cd5eb-213">Это действие активируется, когда пользователь найдет на саму карточку</span><span class="sxs-lookup"><span data-stu-id="cd5eb-213">This action will be activated when the user taps on the card itself</span></span> |
|

### <a name="example-hero-card"></a><span data-ttu-id="cd5eb-214">Пример карточки главный Имиджевый баннер</span><span class="sxs-lookup"><span data-stu-id="cd5eb-214">Example Hero card</span></span>

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

### <a name="for-more-information-on-hero-cards"></a><span data-ttu-id="cd5eb-216">Дополнительные сведения о карточках главный Имиджевый баннер</span><span class="sxs-lookup"><span data-stu-id="cd5eb-216">For more information on Hero cards</span></span>

<span data-ttu-id="cd5eb-217">Справочные материалы по платформе Bot:</span><span class="sxs-lookup"><span data-stu-id="cd5eb-217">Bot Framework reference:</span></span>

* [<span data-ttu-id="cd5eb-218">Узел карточки главный Имиджевый баннер</span><span class="sxs-lookup"><span data-stu-id="cd5eb-218">Hero card Node</span></span>](https://docs.microsoft.com/javascript/api/botframework-schema/herocard)
* [<span data-ttu-id="cd5eb-219">Карточка главный Имиджевый баннер C #</span><span class="sxs-lookup"><span data-stu-id="cd5eb-219">Hero card C#</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.herocard?view=botbuilder-dotnet-3.0)

## <a name="list-card"></a><span data-ttu-id="cd5eb-220">Карточка списка</span><span class="sxs-lookup"><span data-stu-id="cd5eb-220">List card</span></span>

<span data-ttu-id="cd5eb-221">В Microsoft Teams карточка списка была добавлена для предоставления функций, помимо того, что может предоставить коллекция списков.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-221">The list card has been added by Teams to provide functions beyond what the list collection can provide.</span></span> <span data-ttu-id="cd5eb-222">Карточка List предоставляет прокручиваемый список элементов.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-222">The list card provides a scrolling list of items.</span></span>

### <a name="support-for-list-cards"></a><span data-ttu-id="cd5eb-223">Поддержка карточек со списками</span><span class="sxs-lookup"><span data-stu-id="cd5eb-223">Support for List cards</span></span>

| <span data-ttu-id="cd5eb-224">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="cd5eb-224">Bots in Teams</span></span> | <span data-ttu-id="cd5eb-225">Расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="cd5eb-225">Messaging Extensions</span></span>  | <span data-ttu-id="cd5eb-226">Соединители</span><span class="sxs-lookup"><span data-stu-id="cd5eb-226">Connectors</span></span> | <span data-ttu-id="cd5eb-227">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="cd5eb-227">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="cd5eb-228">✔</span><span class="sxs-lookup"><span data-stu-id="cd5eb-228">✔</span></span> | <span data-ttu-id="cd5eb-229">✖</span><span class="sxs-lookup"><span data-stu-id="cd5eb-229">✖</span></span> | <span data-ttu-id="cd5eb-230">✖</span><span class="sxs-lookup"><span data-stu-id="cd5eb-230">✖</span></span> |<span data-ttu-id="cd5eb-231">✔</span><span class="sxs-lookup"><span data-stu-id="cd5eb-231">✔</span></span> |
|

### <a name="properties-of-a-list-card"></a><span data-ttu-id="cd5eb-232">Свойства карточки списка</span><span class="sxs-lookup"><span data-stu-id="cd5eb-232">Properties of a List card</span></span>

| <span data-ttu-id="cd5eb-233">Свойство</span><span class="sxs-lookup"><span data-stu-id="cd5eb-233">Property</span></span> | <span data-ttu-id="cd5eb-234">Тип</span><span class="sxs-lookup"><span data-stu-id="cd5eb-234">Type</span></span>  | <span data-ttu-id="cd5eb-235">Описание</span><span class="sxs-lookup"><span data-stu-id="cd5eb-235">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cd5eb-236">title</span><span class="sxs-lookup"><span data-stu-id="cd5eb-236">title</span></span> | <span data-ttu-id="cd5eb-237">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="cd5eb-237">Rich text</span></span> | <span data-ttu-id="cd5eb-238">Название карточки.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-238">Title of the card.</span></span> <span data-ttu-id="cd5eb-239">Максимум 2 строки; форматирование в настоящее время не поддерживается</span><span class="sxs-lookup"><span data-stu-id="cd5eb-239">Maximum 2 lines; formatting not currently supported</span></span> |
| <span data-ttu-id="cd5eb-240">items</span><span class="sxs-lookup"><span data-stu-id="cd5eb-240">items</span></span> | <span data-ttu-id="cd5eb-241">Массив элементов списка</span><span class="sxs-lookup"><span data-stu-id="cd5eb-241">Array of list items</span></span>  ||
| <span data-ttu-id="cd5eb-242">Button</span><span class="sxs-lookup"><span data-stu-id="cd5eb-242">buttons</span></span> | <span data-ttu-id="cd5eb-243">Массив объектов Action</span><span class="sxs-lookup"><span data-stu-id="cd5eb-243">Array of action objects</span></span> | <span data-ttu-id="cd5eb-244">Набор действий, применяемых к текущей карточке.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-244">Set of actions applicable to the current card.</span></span> <span data-ttu-id="cd5eb-245">Не более 6.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-245">Maximum 6.</span></span> <span data-ttu-id="cd5eb-246">Не отображается на мобильном устройстве.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-246">Does not render on mobile.</span></span> |
|

### <a name="example-list-card"></a><span data-ttu-id="cd5eb-247">Пример карточки списка</span><span class="sxs-lookup"><span data-stu-id="cd5eb-247">Example List card</span></span>

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

## <a name="office-365-connector-card"></a><span data-ttu-id="cd5eb-248">Соединительная карта Office 365</span><span class="sxs-lookup"><span data-stu-id="cd5eb-248">Office 365 connector card</span></span>

<span data-ttu-id="cd5eb-249">Поддерживается в Microsoft Teams, а не в среде Bot.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-249">Supported in Teams, not in Bot Framework.</span></span>

<span data-ttu-id="cd5eb-250">Соединительная карта Office 365 предоставляет гибкий макет с несколькими разделами, полями, изображениями и действиями.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-250">The Office 365 Connector card provides a flexible layout with multiple sections, fields, images, and actions.</span></span> <span data-ttu-id="cd5eb-251">Эта карточка содержит карту подключателя, чтобы ее можно было использовать в Боты.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-251">This card encapsulates a connector card so that it can be used by bots.</span></span> <span data-ttu-id="cd5eb-252">В разделе "Примечания" представлены различия между соединителными картами и картой O365.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-252">See the notes section for differences between connector cards and the O365 card.</span></span>

### <a name="support-for-office-365-connector-cards"></a><span data-ttu-id="cd5eb-253">Поддержка карт соединителей Office 365</span><span class="sxs-lookup"><span data-stu-id="cd5eb-253">Support for Office 365 connector cards</span></span>

| <span data-ttu-id="cd5eb-254">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="cd5eb-254">Bots in Teams</span></span> | <span data-ttu-id="cd5eb-255">Расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="cd5eb-255">Messaging Extensions</span></span>  | <span data-ttu-id="cd5eb-256">Соединители</span><span class="sxs-lookup"><span data-stu-id="cd5eb-256">Connectors</span></span> | <span data-ttu-id="cd5eb-257">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="cd5eb-257">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="cd5eb-258">✔</span><span class="sxs-lookup"><span data-stu-id="cd5eb-258">✔</span></span> | <span data-ttu-id="cd5eb-259">✔</span><span class="sxs-lookup"><span data-stu-id="cd5eb-259">✔</span></span> | <span data-ttu-id="cd5eb-260">✔</span><span class="sxs-lookup"><span data-stu-id="cd5eb-260">✔</span></span> | <span data-ttu-id="cd5eb-261">✖</span><span class="sxs-lookup"><span data-stu-id="cd5eb-261">✖</span></span> |
|

### <a name="properties-of-the-office-365-connector-card"></a><span data-ttu-id="cd5eb-262">Свойства карточки соединителя Office 365</span><span class="sxs-lookup"><span data-stu-id="cd5eb-262">Properties of the Office 365 connector card</span></span>

| <span data-ttu-id="cd5eb-263">Свойство</span><span class="sxs-lookup"><span data-stu-id="cd5eb-263">Property</span></span> | <span data-ttu-id="cd5eb-264">Тип</span><span class="sxs-lookup"><span data-stu-id="cd5eb-264">Type</span></span>  | <span data-ttu-id="cd5eb-265">Описание</span><span class="sxs-lookup"><span data-stu-id="cd5eb-265">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cd5eb-266">title</span><span class="sxs-lookup"><span data-stu-id="cd5eb-266">title</span></span> | <span data-ttu-id="cd5eb-267">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="cd5eb-267">Rich text</span></span> | <span data-ttu-id="cd5eb-268">Название карточки.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-268">Title of the card.</span></span> <span data-ttu-id="cd5eb-269">Максимум 2 строки; форматирование в настоящее время не поддерживается</span><span class="sxs-lookup"><span data-stu-id="cd5eb-269">Maximum 2 lines; formatting not currently supported</span></span> |
| <span data-ttu-id="cd5eb-270">summary</span><span class="sxs-lookup"><span data-stu-id="cd5eb-270">summary</span></span> | <span data-ttu-id="cd5eb-271">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="cd5eb-271">Rich text</span></span> | <span data-ttu-id="cd5eb-272">Сводка по карточке.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-272">Summary of the card.</span></span> <span data-ttu-id="cd5eb-273">Максимум 2 строки; форматирование в настоящее время не поддерживается</span><span class="sxs-lookup"><span data-stu-id="cd5eb-273">Maximum 2 lines; formatting not currently supported</span></span> |
| <span data-ttu-id="cd5eb-274">текст</span><span class="sxs-lookup"><span data-stu-id="cd5eb-274">text</span></span> | <span data-ttu-id="cd5eb-275">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="cd5eb-275">Rich text</span></span> | <span data-ttu-id="cd5eb-276">Текст отображается сразу под подназванием; сведения о [форматировании карточек](~/task-modules-and-cards/cards/cards-format.md) для параметров форматирования</span><span class="sxs-lookup"><span data-stu-id="cd5eb-276">Text appears just below the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options</span></span> |
| <span data-ttu-id="cd5eb-277">themeColor</span><span class="sxs-lookup"><span data-stu-id="cd5eb-277">themeColor</span></span> | <span data-ttu-id="cd5eb-278">ШЕСТНАДЦАТЕРИЧная строка</span><span class="sxs-lookup"><span data-stu-id="cd5eb-278">HEX string</span></span> | <span data-ttu-id="cd5eb-279">цвет, переопределяющий Акцентколор, предоставленный в манифесте приложения</span><span class="sxs-lookup"><span data-stu-id="cd5eb-279">color that overrides the accentColor provided from the application manifest</span></span> |

### <a name="notes-on-the-office-365-connector-card"></a><span data-ttu-id="cd5eb-280">Примечания к соединительной карте Office 365</span><span class="sxs-lookup"><span data-stu-id="cd5eb-280">Notes on the Office 365 connector card</span></span>

<span data-ttu-id="cd5eb-281">Карты соединителей Office 365 правильно работают в Microsoft Teams, включая [действия ActionCard](/outlook/actionable-messages/card-reference#actioncard-action).</span><span class="sxs-lookup"><span data-stu-id="cd5eb-281">Office 365 Connector cards function properly on Microsoft Teams, including [ActionCard actions](/outlook/actionable-messages/card-reference#actioncard-action).</span></span>

<span data-ttu-id="cd5eb-282">Одним из важных различий между использованием карт соединителей с соединителя и карт подключателя в Bot является обработка действий с картой.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-282">One important difference between using Connector cards from a Connector and using Connector cards in your bot is the handling of card actions.</span></span>

* <span data-ttu-id="cd5eb-283">Для соединителя конечная точка получает полезные данные карточки через HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-283">For a Connector, the endpoint receives the card payload via HTTP POST.</span></span>
* <span data-ttu-id="cd5eb-284">Для элемента Bot `HttpPOST` действие запускает `invoke` действие, которое отправляет только идентификатор действия и основной текст в Bot.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-284">For a bot, the `HttpPOST` action triggers an `invoke` activity that sends only the action ID and body to the bot.</span></span>

<span data-ttu-id="cd5eb-285">Каждая соединительная карта может отображать не более 10 разделов, а каждый раздел может содержать не более 5 изображений и 5 действий.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-285">Each Connector card can display a maximum of 10 sections, and each section can contain a maximum of 5 images and 5 actions.</span></span>

> [!NOTE]
> <span data-ttu-id="cd5eb-286">Дополнительные разделы, изображения или действия в сообщении не будут отображаться.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-286">Any additional sections, images, or actions in a message will not appear.</span></span>

<span data-ttu-id="cd5eb-287">Все текстовые поля поддерживают Markdown и HTML.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-287">All text fields support Markdown and HTML.</span></span> <span data-ttu-id="cd5eb-288">Вы можете управлять тем `markdown` , какие разделы используют MARKDOWN или HTML, задав свойство в сообщении.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-288">You can control which sections use Markdown or HTML by setting the `markdown` property in a message.</span></span> <span data-ttu-id="cd5eb-289">По умолчанию `markdown` задано значение `true`; Если вместо этого вы хотите использовать HTML, задайте `markdown` значение `false`.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-289">By default, `markdown` is set to `true`; if you want to use HTML instead, set `markdown` to `false`.</span></span>

<span data-ttu-id="cd5eb-290">Если указать `themeColor` свойство, оно переопределяет `accentColor` свойство в манифесте приложения.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-290">If you specify the `themeColor` property, it overrides the `accentColor` property in the app manifest.</span></span>

<span data-ttu-id="cd5eb-291">Чтобы указать стиль отображения для `activityImage`, можно задать `activityImageType` следующие значения:</span><span class="sxs-lookup"><span data-stu-id="cd5eb-291">To specify the rendering style for `activityImage`, you can set `activityImageType` as follows.</span></span>

| <span data-ttu-id="cd5eb-292">Значение</span><span class="sxs-lookup"><span data-stu-id="cd5eb-292">Value</span></span> | <span data-ttu-id="cd5eb-293">Описание</span><span class="sxs-lookup"><span data-stu-id="cd5eb-293">Description</span></span> |
| --- | --- |
| `avatar` | <span data-ttu-id="cd5eb-294">Умолчани `activityImage` будет обрезан как круг</span><span class="sxs-lookup"><span data-stu-id="cd5eb-294">Default; `activityImage` will be cropped as a circle</span></span> |
| `article` | <span data-ttu-id="cd5eb-295">`activityImage`будет отображаться как прямоугольник и сохранять пропорции</span><span class="sxs-lookup"><span data-stu-id="cd5eb-295">`activityImage` will be displayed as a rectangle and retain its aspect ratio</span></span> |

<span data-ttu-id="cd5eb-296">Дополнительные сведения о свойствах карт соединителей можно узнать в статье [Справочник по карточкам сообщений с действиями](/outlook/actionable-messages/card-reference).</span><span class="sxs-lookup"><span data-stu-id="cd5eb-296">For all other details about Connector card properties, see the [Actionable message card reference](/outlook/actionable-messages/card-reference).</span></span> <span data-ttu-id="cd5eb-297">В настоящее время в Microsoft Teams в настоящее время не поддерживаются следующие свойства карточки соединителя:</span><span class="sxs-lookup"><span data-stu-id="cd5eb-297">The only Connector card properties that Microsoft Teams does not currently support are as follows:</span></span>

* `heroImage`
* `hideOriginalBody`
* <span data-ttu-id="cd5eb-298">`startGroup`(всегда обрабатываются как `true` в Teams)</span><span class="sxs-lookup"><span data-stu-id="cd5eb-298">`startGroup` (always treated as `true` in Teams)</span></span>
* `originator`
* `correlationId`

### <a name="example-office-365-connector-card"></a><span data-ttu-id="cd5eb-299">Пример карточки соединителя Office 365</span><span class="sxs-lookup"><span data-stu-id="cd5eb-299">Example Office 365 connector card</span></span>

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

## <a name="receipt-card"></a><span data-ttu-id="cd5eb-300">Карточка приходной накладной</span><span class="sxs-lookup"><span data-stu-id="cd5eb-300">Receipt card</span></span>

<span data-ttu-id="cd5eb-301">Поддерживается в Teams.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-301">Supported in Teams.</span></span>

<span data-ttu-id="cd5eb-302">Карточка, позволяющая роботу получить уведомление для пользователя.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-302">A card that enables a bot to provide a receipt to the user.</span></span> <span data-ttu-id="cd5eb-303">Как правило, он содержит список элементов, которые необходимо включить в сведения о получении, налогах и итогах, а также другие тексты.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-303">It typically contains the list of items to include on the receipt, tax and total information, and other text.</span></span>

### <a name="support-for-receipts-cards"></a><span data-ttu-id="cd5eb-304">Поддержка карточек чеков</span><span class="sxs-lookup"><span data-stu-id="cd5eb-304">Support for Receipts cards</span></span>

| <span data-ttu-id="cd5eb-305">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="cd5eb-305">Bots in Teams</span></span> | <span data-ttu-id="cd5eb-306">Расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="cd5eb-306">Messaging Extensions</span></span>  | <span data-ttu-id="cd5eb-307">Соединители</span><span class="sxs-lookup"><span data-stu-id="cd5eb-307">Connectors</span></span> | <span data-ttu-id="cd5eb-308">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="cd5eb-308">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="cd5eb-309">✔</span><span class="sxs-lookup"><span data-stu-id="cd5eb-309">✔</span></span> | <span data-ttu-id="cd5eb-310">✔</span><span class="sxs-lookup"><span data-stu-id="cd5eb-310">✔</span></span> | <span data-ttu-id="cd5eb-311">✖</span><span class="sxs-lookup"><span data-stu-id="cd5eb-311">✖</span></span> | <span data-ttu-id="cd5eb-312">✔</span><span class="sxs-lookup"><span data-stu-id="cd5eb-312">✔</span></span> |
|

### <a name="for-more-information-on-receipt-cards"></a><span data-ttu-id="cd5eb-313">Дополнительные сведения о карточках прихода</span><span class="sxs-lookup"><span data-stu-id="cd5eb-313">For more information on Receipt cards</span></span>

<span data-ttu-id="cd5eb-314">Справочные материалы по платформе Bot:</span><span class="sxs-lookup"><span data-stu-id="cd5eb-314">Bot Framework reference:</span></span>

* [<span data-ttu-id="cd5eb-315">Узел карточки чеков</span><span class="sxs-lookup"><span data-stu-id="cd5eb-315">Receipt card Node</span></span>](https://docs.microsoft.com/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest)
* [<span data-ttu-id="cd5eb-316">Карточка прихода C #</span><span class="sxs-lookup"><span data-stu-id="cd5eb-316">Receipt card C#</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.receiptcard?view=botbuilder-dotnet-3.0)

## <a name="signin-card"></a><span data-ttu-id="cd5eb-317">Карточка входа</span><span class="sxs-lookup"><span data-stu-id="cd5eb-317">Signin card</span></span>

<span data-ttu-id="cd5eb-318">Карточка, позволяющая роботу отправить запрос на вход пользователя.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-318">A card that enables a bot to request that a user sign in.</span></span> <span data-ttu-id="cd5eb-319">Поддерживается в Microsoft Teams в несколько разных формах, чем в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-319">Supported in Teams in a slightly different form than is found in the Bot Framework.</span></span> <span data-ttu-id="cd5eb-320">Карточка входа в Teams аналогична карте входа в Bot Framework с исключением, что карточка входа в Teams поддерживает только два действия: `signin` и. `openUrl`</span><span class="sxs-lookup"><span data-stu-id="cd5eb-320">The signin card in Teams is similar to the signin card in the bot framework with the exception that the signin card in Teams only supports two actions: `signin` and `openUrl`.</span></span>

<span data-ttu-id="cd5eb-321">*Действие SignIn* можно использовать с любой карточки в Teams, а не только с помощью карточки входа.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-321">The *signin action* can be used from any card in Teams, not just the signin card.</span></span> <span data-ttu-id="cd5eb-322">Для получения дополнительных сведений о проверке подлинности обратитесь к разделу [Проверка подлинности Microsoft Teams для Боты](~/bots/how-to/authentication/auth-flow-bot.md) .</span><span class="sxs-lookup"><span data-stu-id="cd5eb-322">See the topic [Microsoft Teams authentication flow for bots](~/bots/how-to/authentication/auth-flow-bot.md) for more details on authentication.</span></span>

### <a name="support-for-signin-cards"></a><span data-ttu-id="cd5eb-323">Поддержка карточек входа</span><span class="sxs-lookup"><span data-stu-id="cd5eb-323">Support for Signin cards</span></span>

| <span data-ttu-id="cd5eb-324">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="cd5eb-324">Bots in Teams</span></span> | <span data-ttu-id="cd5eb-325">Расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="cd5eb-325">Messaging Extensions</span></span>  | <span data-ttu-id="cd5eb-326">Соединители</span><span class="sxs-lookup"><span data-stu-id="cd5eb-326">Connectors</span></span> | <span data-ttu-id="cd5eb-327">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="cd5eb-327">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="cd5eb-328">✔</span><span class="sxs-lookup"><span data-stu-id="cd5eb-328">✔</span></span> | <span data-ttu-id="cd5eb-329">✖</span><span class="sxs-lookup"><span data-stu-id="cd5eb-329">✖</span></span> | <span data-ttu-id="cd5eb-330">✖</span><span class="sxs-lookup"><span data-stu-id="cd5eb-330">✖</span></span> | <span data-ttu-id="cd5eb-331">✔</span><span class="sxs-lookup"><span data-stu-id="cd5eb-331">✔</span></span> |
|

### <a name="for-more-information-on-signin-cards"></a><span data-ttu-id="cd5eb-332">Дополнительные сведения о карточках входа</span><span class="sxs-lookup"><span data-stu-id="cd5eb-332">For more information on Signin cards</span></span>

<span data-ttu-id="cd5eb-333">Справочные материалы по платформе Bot:</span><span class="sxs-lookup"><span data-stu-id="cd5eb-333">Bot Framework reference:</span></span>

* [<span data-ttu-id="cd5eb-334">Узел карточки входа</span><span class="sxs-lookup"><span data-stu-id="cd5eb-334">Signin card Node</span></span>](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest)
* [<span data-ttu-id="cd5eb-335">Карточка входа в систему C #</span><span class="sxs-lookup"><span data-stu-id="cd5eb-335">Signin card C#</span></span>](/dotnet/api/microsoft.bot.connector.signincard?view=botbuilder-dotnet-3.0)

## <a name="thumbnail-card"></a><span data-ttu-id="cd5eb-336">Карточка эскиза</span><span class="sxs-lookup"><span data-stu-id="cd5eb-336">Thumbnail card</span></span>

<span data-ttu-id="cd5eb-337">Карточка, которая обычно содержит одно эскизное изображение, одну или несколько кнопок и текст.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-337">A card that typically contains a single thumbnail image, one or more buttons, and text.</span></span>

### <a name="support-for-thumbnail-cards"></a><span data-ttu-id="cd5eb-338">Поддержка карт эскизов</span><span class="sxs-lookup"><span data-stu-id="cd5eb-338">Support for Thumbnail cards</span></span>

| <span data-ttu-id="cd5eb-339">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="cd5eb-339">Bots in Teams</span></span> | <span data-ttu-id="cd5eb-340">Расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="cd5eb-340">Messaging Extensions</span></span>  | <span data-ttu-id="cd5eb-341">Соединители</span><span class="sxs-lookup"><span data-stu-id="cd5eb-341">Connectors</span></span> | <span data-ttu-id="cd5eb-342">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="cd5eb-342">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="cd5eb-343">✔</span><span class="sxs-lookup"><span data-stu-id="cd5eb-343">✔</span></span> | <span data-ttu-id="cd5eb-344">✔</span><span class="sxs-lookup"><span data-stu-id="cd5eb-344">✔</span></span> | <span data-ttu-id="cd5eb-345">✖</span><span class="sxs-lookup"><span data-stu-id="cd5eb-345">✖</span></span> | <span data-ttu-id="cd5eb-346">✔</span><span class="sxs-lookup"><span data-stu-id="cd5eb-346">✔</span></span> |
|

![Пример карточки эскиза](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a><span data-ttu-id="cd5eb-348">Свойства карточки эскиза</span><span class="sxs-lookup"><span data-stu-id="cd5eb-348">Properties of a Thumbnail card</span></span>

| <span data-ttu-id="cd5eb-349">Свойство</span><span class="sxs-lookup"><span data-stu-id="cd5eb-349">Property</span></span> | <span data-ttu-id="cd5eb-350">Тип</span><span class="sxs-lookup"><span data-stu-id="cd5eb-350">Type</span></span>  | <span data-ttu-id="cd5eb-351">Описание</span><span class="sxs-lookup"><span data-stu-id="cd5eb-351">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cd5eb-352">title</span><span class="sxs-lookup"><span data-stu-id="cd5eb-352">title</span></span> | <span data-ttu-id="cd5eb-353">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="cd5eb-353">Rich text</span></span> | <span data-ttu-id="cd5eb-354">Название карточки.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-354">Title of the card.</span></span> <span data-ttu-id="cd5eb-355">Максимум 2 строки; форматирование в настоящее время не поддерживается</span><span class="sxs-lookup"><span data-stu-id="cd5eb-355">Maximum 2 lines; formatting not currently supported</span></span> |
| <span data-ttu-id="cd5eb-356">Подзаголовок</span><span class="sxs-lookup"><span data-stu-id="cd5eb-356">subtitle</span></span> | <span data-ttu-id="cd5eb-357">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="cd5eb-357">Rich text</span></span> | <span data-ttu-id="cd5eb-358">Подзаголовок карточки.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-358">Subtitle of the card.</span></span> <span data-ttu-id="cd5eb-359">Максимум 2 строки; форматирование в настоящее время не поддерживается</span><span class="sxs-lookup"><span data-stu-id="cd5eb-359">Maximum 2 lines; formatting not currently supported</span></span> |
| <span data-ttu-id="cd5eb-360">текст</span><span class="sxs-lookup"><span data-stu-id="cd5eb-360">text</span></span> | <span data-ttu-id="cd5eb-361">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="cd5eb-361">Rich text</span></span> | <span data-ttu-id="cd5eb-362">Текст отображается сразу под подназванием; сведения о [форматировании карточек](~/task-modules-and-cards/cards/cards-format.md) для параметров форматирования</span><span class="sxs-lookup"><span data-stu-id="cd5eb-362">Text appears just below the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options</span></span> |
| <span data-ttu-id="cd5eb-363">изображения</span><span class="sxs-lookup"><span data-stu-id="cd5eb-363">images</span></span> | <span data-ttu-id="cd5eb-364">Массив изображений</span><span class="sxs-lookup"><span data-stu-id="cd5eb-364">Array of images</span></span> | <span data-ttu-id="cd5eb-365">Изображение, отображаемое в верхней части карточки.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-365">Image displayed at top of card.</span></span> <span data-ttu-id="cd5eb-366">Пропорции 1:1 (квадрат)</span><span class="sxs-lookup"><span data-stu-id="cd5eb-366">Aspect ratio 1:1 (square)</span></span> |
| <span data-ttu-id="cd5eb-367">Button</span><span class="sxs-lookup"><span data-stu-id="cd5eb-367">buttons</span></span> | <span data-ttu-id="cd5eb-368">Массив объектов Action</span><span class="sxs-lookup"><span data-stu-id="cd5eb-368">Array of action objects</span></span> | <span data-ttu-id="cd5eb-369">Набор действий, применяемых к текущей карточке.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-369">Set of actions applicable to the current card.</span></span> <span data-ttu-id="cd5eb-370">Максимум 6</span><span class="sxs-lookup"><span data-stu-id="cd5eb-370">Maximum 6</span></span> |
| <span data-ttu-id="cd5eb-371">тематическ</span><span class="sxs-lookup"><span data-stu-id="cd5eb-371">tap</span></span> | <span data-ttu-id="cd5eb-372">Объект Action</span><span class="sxs-lookup"><span data-stu-id="cd5eb-372">Action object</span></span> | <span data-ttu-id="cd5eb-373">Это действие активируется, когда пользователь найдет на саму карточку</span><span class="sxs-lookup"><span data-stu-id="cd5eb-373">This action will be activated when the user taps on the card itself</span></span> |
|

### <a name="example-thumbnail-card"></a><span data-ttu-id="cd5eb-374">Пример карточки эскиза</span><span class="sxs-lookup"><span data-stu-id="cd5eb-374">Example Thumbnail card</span></span>

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

### <a name="for-more-information"></a><span data-ttu-id="cd5eb-375">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="cd5eb-375">For more information</span></span>

<span data-ttu-id="cd5eb-376">Справочные материалы по платформе Bot:</span><span class="sxs-lookup"><span data-stu-id="cd5eb-376">Bot Framework reference:</span></span>

* [<span data-ttu-id="cd5eb-377">Узел карточки эскиза</span><span class="sxs-lookup"><span data-stu-id="cd5eb-377">Thumbnail card Node</span></span>](https://docs.microsoft.com/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest)
* [<span data-ttu-id="cd5eb-378">Карта с эскизом C #</span><span class="sxs-lookup"><span data-stu-id="cd5eb-378">Thumbnail card C#</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.thumbnailcard?view=botbuilder-dotnet-3.0)

## <a name="card-collections"></a><span data-ttu-id="cd5eb-379">Коллекции карточек</span><span class="sxs-lookup"><span data-stu-id="cd5eb-379">Card collections</span></span>

<span data-ttu-id="cd5eb-380">Коллекции карточек поддерживаются в Teams.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-380">Card collections are supported in Teams.</span></span>

<span data-ttu-id="cd5eb-381">Коллекции карточек предоставляются с помощью Bot Framework: `builder.AttachmentLayout.carousel` и. `builder.AttachmentLayout.list`</span><span class="sxs-lookup"><span data-stu-id="cd5eb-381">Card collections are provided by the Bot Framework: `builder.AttachmentLayout.carousel` and `builder.AttachmentLayout.list`.</span></span> <span data-ttu-id="cd5eb-382">Эти коллекции могут содержать адаптивные, главный Имиджевый баннер или карты эскиза.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-382">These collections can contain Adaptive, Hero, or Thumbnail cards.</span></span>

## <a name="carousel-collection"></a><span data-ttu-id="cd5eb-383">Коллекция обойм</span><span class="sxs-lookup"><span data-stu-id="cd5eb-383">Carousel collection</span></span>

<span data-ttu-id="cd5eb-384">[Макет обоймы](/azure/bot-service/dotnet/bot-builder-dotnet-add-rich-card-attachments?view=azure-bot-service-3.0) отображает обойму карточек (при необходимости) с соответствующими кнопками действия.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-384">The [carousel layout](/azure/bot-service/dotnet/bot-builder-dotnet-add-rich-card-attachments?view=azure-bot-service-3.0) shows a carousel of cards, optionally with associated action buttons.</span></span>

### <a name="support-for-carousel-collections"></a><span data-ttu-id="cd5eb-385">Поддержка коллекций обойм</span><span class="sxs-lookup"><span data-stu-id="cd5eb-385">Support for Carousel collections</span></span>

| <span data-ttu-id="cd5eb-386">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="cd5eb-386">Bots in Teams</span></span> | <span data-ttu-id="cd5eb-387">Расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="cd5eb-387">Messaging Extensions</span></span>  | <span data-ttu-id="cd5eb-388">Соединители</span><span class="sxs-lookup"><span data-stu-id="cd5eb-388">Connectors</span></span> | <span data-ttu-id="cd5eb-389">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="cd5eb-389">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="cd5eb-390">✔</span><span class="sxs-lookup"><span data-stu-id="cd5eb-390">✔</span></span> | <span data-ttu-id="cd5eb-391">✖</span><span class="sxs-lookup"><span data-stu-id="cd5eb-391">✖</span></span> | <span data-ttu-id="cd5eb-392">✖</span><span class="sxs-lookup"><span data-stu-id="cd5eb-392">✖</span></span> | <span data-ttu-id="cd5eb-393">✔</span><span class="sxs-lookup"><span data-stu-id="cd5eb-393">✔</span></span> |
|

> [!NOTE]
> <span data-ttu-id="cd5eb-394">В обойме может отображаться не более 10 карточек для каждого сообщения.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-394">A carousel can display a maximum of 10 cards per message.</span></span>

### <a name="example-carousel-collection"></a><span data-ttu-id="cd5eb-395">Пример коллекции обойм</span><span class="sxs-lookup"><span data-stu-id="cd5eb-395">Example Carousel collection</span></span>

![Пример обоймы карточек](~/assets/images/cards/carousel.png)

<span data-ttu-id="cd5eb-397">Это те же свойства, что и для карты главный Имиджевый баннер или эскиза.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-397">Properties are the same as for the hero or thumbnail card.</span></span>

### <a name="syntax-for-carousel-collections"></a><span data-ttu-id="cd5eb-398">Синтаксис для коллекций обойм</span><span class="sxs-lookup"><span data-stu-id="cd5eb-398">Syntax for Carousel collections</span></span>

`builder.AttachmentLayout.carousel`

## <a name="list-collection"></a><span data-ttu-id="cd5eb-399">Коллекция List</span><span class="sxs-lookup"><span data-stu-id="cd5eb-399">List collection</span></span>

### <a name="support-for-list-collections"></a><span data-ttu-id="cd5eb-400">Поддержка коллекций списков</span><span class="sxs-lookup"><span data-stu-id="cd5eb-400">Support for List collections</span></span>

<span data-ttu-id="cd5eb-401">В раскладке списка отображается вертикальный список карточек, при необходимости связанные с ними кнопки действий.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-401">The list layout shows a vertically stacked list of cards, optionally with associated action buttons.</span></span>

| <span data-ttu-id="cd5eb-402">Боты в Teams</span><span class="sxs-lookup"><span data-stu-id="cd5eb-402">Bots in Teams</span></span> | <span data-ttu-id="cd5eb-403">Расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="cd5eb-403">Messaging Extensions</span></span>  | <span data-ttu-id="cd5eb-404">Соединители</span><span class="sxs-lookup"><span data-stu-id="cd5eb-404">Connectors</span></span> | <span data-ttu-id="cd5eb-405">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="cd5eb-405">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="cd5eb-406">✔</span><span class="sxs-lookup"><span data-stu-id="cd5eb-406">✔</span></span> | <span data-ttu-id="cd5eb-407">✔</span><span class="sxs-lookup"><span data-stu-id="cd5eb-407">✔</span></span> | <span data-ttu-id="cd5eb-408">✖</span><span class="sxs-lookup"><span data-stu-id="cd5eb-408">✖</span></span> | <span data-ttu-id="cd5eb-409">✔</span><span class="sxs-lookup"><span data-stu-id="cd5eb-409">✔</span></span> |
|

### <a name="example-list-collection"></a><span data-ttu-id="cd5eb-410">Пример коллекции списков</span><span class="sxs-lookup"><span data-stu-id="cd5eb-410">Example List collection</span></span>

![Пример списка карточек](~/assets/images/cards/list.png)

<span data-ttu-id="cd5eb-412">Это те же свойства, что и для карты главный Имиджевый баннер или эскиза.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-412">Properties are the same as for the hero or thumbnail card.</span></span>

<span data-ttu-id="cd5eb-413">В списке может отображаться не более 10 карточек для каждого сообщения.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-413">A list can display a maximum of 10 cards per message.</span></span>

> [!NOTE]
> <span data-ttu-id="cd5eb-414">Некоторые комбинации карточек со списками пока не поддерживаются в iOS и Android.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-414">Some combinations of list cards are not yet supported on iOS and Android.</span></span>

### <a name="syntax-for-list-collections"></a><span data-ttu-id="cd5eb-415">Синтаксис коллекций списков</span><span class="sxs-lookup"><span data-stu-id="cd5eb-415">Syntax for List collections</span></span>

`builder.AttachmentLayout.list`

## <a name="cards-not-supported-in-teams"></a><span data-ttu-id="cd5eb-416">Карточки, не поддерживаемые в Teams</span><span class="sxs-lookup"><span data-stu-id="cd5eb-416">Cards not supported in Teams</span></span>

<span data-ttu-id="cd5eb-417">Следующие карты реализуются с помощью Bot Framework, но не поддерживаются в Teams.</span><span class="sxs-lookup"><span data-stu-id="cd5eb-417">The following cards are implemented by the Bot Framework, but are NOT supported by Teams.</span></span>

* <span data-ttu-id="cd5eb-418">Карты анимации</span><span class="sxs-lookup"><span data-stu-id="cd5eb-418">Animation cards</span></span>
* <span data-ttu-id="cd5eb-419">Звуковые карты</span><span class="sxs-lookup"><span data-stu-id="cd5eb-419">Audio cards</span></span>
* <span data-ttu-id="cd5eb-420">Видеокарты</span><span class="sxs-lookup"><span data-stu-id="cd5eb-420">Video cards</span></span>
