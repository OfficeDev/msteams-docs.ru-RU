---
title: Форматирование текста в картах
description: Описывает форматирование текста карты в Microsoft Teams
keywords: teams bots cards format
ms.topic: reference
ms.date: 03/29/2018
ms.openlocfilehash: e6b8cc835780e03cf4e23eae31fa447c8a03c002
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696537"
---
# <a name="format-cards-in-teams"></a><span data-ttu-id="e23ba-104">Формат карт в Teams</span><span class="sxs-lookup"><span data-stu-id="e23ba-104">Format cards in Teams</span></span>

<span data-ttu-id="e23ba-105">В зависимости от типа карты можно добавить в карты форматирование текста с помощью Markdown или HTML.</span><span class="sxs-lookup"><span data-stu-id="e23ba-105">You can add rich text formatting to your cards using either Markdown or HTML, depending on the card type.</span></span>

<span data-ttu-id="e23ba-106">Карточки поддерживают форматирование только в свойстве текста, а не в свойствах заголовка или субтитров.</span><span class="sxs-lookup"><span data-stu-id="e23ba-106">Cards support formatting in the text property only, not in the title or subtitle properties.</span></span> <span data-ttu-id="e23ba-107">Форматирование можно задать с помощью подмножество форматирования XML (HTML) или Markdown в зависимости от типа карты.</span><span class="sxs-lookup"><span data-stu-id="e23ba-107">Formatting can be specified using a subset of XML (HTML) formatting, or Markdown depending on card type.</span></span> <span data-ttu-id="e23ba-108">Для текущих и будущих карт разработки рекомендуется использовать форматирование Markdown.</span><span class="sxs-lookup"><span data-stu-id="e23ba-108">For current and future development Adaptive cards using Markdown formatting is recommended.</span></span>

<span data-ttu-id="e23ba-109">Поддержка форматирования отличается между различными типами карт, а отрисовка карты может незначительно отличаться между настольным компьютером и клиентами мобильных групп, а также Teams в браузере настольных компьютеров.</span><span class="sxs-lookup"><span data-stu-id="e23ba-109">Formatting support differs between different card types, and rendering of the card can differ slightly between the desktop and the mobile Teams clients, as well as Teams in the desktop browser.</span></span>

<span data-ttu-id="e23ba-110">Вы можете включить inline-изображение с любой картой Teams.</span><span class="sxs-lookup"><span data-stu-id="e23ba-110">You can include an inline image with any Teams card.</span></span> <span data-ttu-id="e23ba-111">Изображения форматированы как , или файлы и не должны превышать  `.png` `.jpg` `.gif` 1024 ×1024 px или 1 МБ.</span><span class="sxs-lookup"><span data-stu-id="e23ba-111">Images an be formatted as  `.png`, `.jpg`, or `.gif` files and must not exceed 1024 ×1024 px or 1 MB.</span></span> <span data-ttu-id="e23ba-112">Анимированный GIF не поддерживается официально.</span><span class="sxs-lookup"><span data-stu-id="e23ba-112">Animated GIF is not officially supported.</span></span> <span data-ttu-id="e23ba-113">*См.* [ссылку На карточки](./cards-reference.md#inline-card-images)</span><span class="sxs-lookup"><span data-stu-id="e23ba-113">*See* [Cards reference](./cards-reference.md#inline-card-images)</span></span>

## <a name="formatting-cards-with-markdown"></a><span data-ttu-id="e23ba-114">Форматирование карт с помощью Markdown</span><span class="sxs-lookup"><span data-stu-id="e23ba-114">Formatting cards with Markdown</span></span>

<span data-ttu-id="e23ba-115">Существует два типа карт, поддерживаюных Markdown в Teams:</span><span class="sxs-lookup"><span data-stu-id="e23ba-115">There are two card types that support Markdown in Teams:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e23ba-116">**Адаптивные карты:** Markdown поддерживается в поле адаптивных карт, а `Textblock` также и `Fact.Title` `Fact.Value` .</span><span class="sxs-lookup"><span data-stu-id="e23ba-116">**Adaptive cards**: Markdown is supported in Adaptive card `Textblock` field, as well as `Fact.Title` and `Fact.Value`.</span></span> <span data-ttu-id="e23ba-117">HTML не поддерживается в адаптивных картах.</span><span class="sxs-lookup"><span data-stu-id="e23ba-117">HTML is not supported in Adaptive cards.</span></span>
> * <span data-ttu-id="e23ba-118">**Карты соединителя O365:** Markdown и ограниченный HTML поддерживаются в карточках Соединитель Office 365 в текстовых полях.</span><span class="sxs-lookup"><span data-stu-id="e23ba-118">**O365 Connector Cards**: Markdown and limited HTML is supported in Office 365 Connector cards in the text fields.</span></span>

# <a name="markdown-formatting-adaptive-cards"></a>[<span data-ttu-id="e23ba-119">**Форматирование разметки: адаптивные карты**</span><span class="sxs-lookup"><span data-stu-id="e23ba-119">**Markdown formatting: Adaptive cards**</span></span>](#tab/adaptive-md)

 <span data-ttu-id="e23ba-120">Поддерживаемые стили `Textblock` для и `Fact.Title` `Fact.Value` являются:</span><span class="sxs-lookup"><span data-stu-id="e23ba-120">The supported styles for `Textblock`, `Fact.Title` and `Fact.Value` are:</span></span>

| <span data-ttu-id="e23ba-121">Style</span><span class="sxs-lookup"><span data-stu-id="e23ba-121">Style</span></span> | <span data-ttu-id="e23ba-122">Пример</span><span class="sxs-lookup"><span data-stu-id="e23ba-122">Example</span></span> | <span data-ttu-id="e23ba-123">Markdown</span><span class="sxs-lookup"><span data-stu-id="e23ba-123">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e23ba-124">bold</span><span class="sxs-lookup"><span data-stu-id="e23ba-124">bold</span></span> | <span data-ttu-id="e23ba-125">**Bold**</span><span class="sxs-lookup"><span data-stu-id="e23ba-125">**Bold**</span></span> | ```**Bold**``` |
| <span data-ttu-id="e23ba-126">italic</span><span class="sxs-lookup"><span data-stu-id="e23ba-126">italic</span></span> | <span data-ttu-id="e23ba-127">_Italic_</span><span class="sxs-lookup"><span data-stu-id="e23ba-127">_Italic_</span></span> | ```_Italic_``` |
| <span data-ttu-id="e23ba-128">необученный список</span><span class="sxs-lookup"><span data-stu-id="e23ba-128">unordered list</span></span> | <ul><li><span data-ttu-id="e23ba-129">текст</span><span class="sxs-lookup"><span data-stu-id="e23ba-129">text</span></span></li><li><span data-ttu-id="e23ba-130">текст</span><span class="sxs-lookup"><span data-stu-id="e23ba-130">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="e23ba-131">упорядоченный список</span><span class="sxs-lookup"><span data-stu-id="e23ba-131">ordered list</span></span> | <ol><li><span data-ttu-id="e23ba-132">текст</span><span class="sxs-lookup"><span data-stu-id="e23ba-132">text</span></span></li><li><span data-ttu-id="e23ba-133">текст</span><span class="sxs-lookup"><span data-stu-id="e23ba-133">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="e23ba-134">Гиперссылки</span><span class="sxs-lookup"><span data-stu-id="e23ba-134">Hyperlinks</span></span> |[<span data-ttu-id="e23ba-135">Bing</span><span class="sxs-lookup"><span data-stu-id="e23ba-135">Bing</span></span>](https://www.bing.com/)| ```[Title](url)``` |

<span data-ttu-id="e23ba-136">Следующие теги Markdown не поддерживаются:</span><span class="sxs-lookup"><span data-stu-id="e23ba-136">The following Markdown tags are not supported:</span></span>

* <span data-ttu-id="e23ba-137">Заголовки</span><span class="sxs-lookup"><span data-stu-id="e23ba-137">Headers</span></span>
* <span data-ttu-id="e23ba-138">Таблицы</span><span class="sxs-lookup"><span data-stu-id="e23ba-138">Tables</span></span>
* <span data-ttu-id="e23ba-139">изображения;</span><span class="sxs-lookup"><span data-stu-id="e23ba-139">Images</span></span>
* <span data-ttu-id="e23ba-140">Предформатированный текст</span><span class="sxs-lookup"><span data-stu-id="e23ba-140">Preformatted text</span></span>
* <span data-ttu-id="e23ba-141">Blockquotes</span><span class="sxs-lookup"><span data-stu-id="e23ba-141">Blockquotes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e23ba-142">Адаптивные карты не поддерживают форматирование HTML.</span><span class="sxs-lookup"><span data-stu-id="e23ba-142">Adaptive cards do not support HTML formatting.</span></span>

### <a name="newlines-for-adaptive-cards"></a><span data-ttu-id="e23ba-143">Newlines для адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="e23ba-143">Newlines for Adaptive cards</span></span>

<span data-ttu-id="e23ba-144">В списках можно использовать `\r` последовательности `\n` или последовательности побега для newlines.</span><span class="sxs-lookup"><span data-stu-id="e23ba-144">In lists you can use the `\r` or `\n` escape sequences for newlines.</span></span> <span data-ttu-id="e23ba-145">Использование в списке приведет к отступам следующего элемента `\n\n` в списке.</span><span class="sxs-lookup"><span data-stu-id="e23ba-145">Using `\n\n` in a list will cause the next element in the list to be indented.</span></span> <span data-ttu-id="e23ba-146">Если вам нужны новые линии в другом месте в текстовом блокпосте, используйте `\n\n` .</span><span class="sxs-lookup"><span data-stu-id="e23ba-146">If you need newlines elsewhere in the textblock, use `\n\n`.</span></span>

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a><span data-ttu-id="e23ba-147">Различия для мобильных и настольных компьютеров для адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="e23ba-147">Mobile and desktop differences for Adaptive cards</span></span>

<span data-ttu-id="e23ba-148">Форматирование несколько отличается от рабочего стола к мобильным версиям Teams.</span><span class="sxs-lookup"><span data-stu-id="e23ba-148">Formatting is slightly different between the desktop and the mobile versions of Teams.</span></span>

<span data-ttu-id="e23ba-149">На рабочем столе форматирование разметки адаптивной карты выглядит так как в веб-браузерах, так и в клиентском приложении Teams:</span><span class="sxs-lookup"><span data-stu-id="e23ba-149">On the desktop, Adaptive card Markdown formatting appears like this in both web browsers and in the Teams client application:</span></span>

![Форматирование разметки адаптивной карты в клиенте рабочего стола](../../assets/images/cards/Adaptive-markdown-desktop-client.png)

<span data-ttu-id="e23ba-151">В iOS форматирование разметки адаптивной карты выглядит так:</span><span class="sxs-lookup"><span data-stu-id="e23ba-151">On iOS, Adaptive card Markdown formatting appears like this:</span></span>

![Форматирование разметки адаптивной карты в iOS](../../assets/images/cards/Adaptive-markdown-iOS-75.png)

<span data-ttu-id="e23ba-153">На Android форматирование разметки адаптивной карты выглядит так:</span><span class="sxs-lookup"><span data-stu-id="e23ba-153">On Android, Adaptive Card Markdown formatting appears like this:</span></span>

![Форматирование разметки адаптивной карты в Android](../../assets/images/cards/Adaptive-markdown-Android.png)

### <a name="more-information-on-adaptive-cards"></a><span data-ttu-id="e23ba-155">Дополнительные сведения о адаптивных картах</span><span class="sxs-lookup"><span data-stu-id="e23ba-155">More information on Adaptive cards</span></span>

<span data-ttu-id="e23ba-156">[Текстовые функции в адаптивных картах](/adaptive-cards/create/textfeatures) Функции даты и локализации, упомянутые в этой теме, не поддерживаются в Teams.</span><span class="sxs-lookup"><span data-stu-id="e23ba-156">[Text features in Adaptive cards](/adaptive-cards/create/textfeatures) The date and localization features mentioned in this topic are not supported in Teams.</span></span>

### <a name="formatting-sample-for-adaptive-cards"></a><span data-ttu-id="e23ba-157">Пример форматирования для адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="e23ba-157">Formatting sample for Adaptive cards</span></span>

``` json
{
    "$schema": "https://adaptivecards.io/schemas/adaptive-card.json",
    "type": "AdaptiveCard",
    "version": "1.0",
    "body": [
        {
            "type": "TextBlock",
            "text": "This is some **bold** text"
        },
        {
            "type": "TextBlock",
            "text": "This is some _italic_ text"
        },
        {
            "type": "TextBlock",
            "text": "- Bullet \r- List \r",
            "wrap": true
        },
        {
            "type": "TextBlock",
            "text": "1. Numbered\r2. List\r",
            "wrap": true
        },
        {
            "type": "TextBlock",
            "text": "Check out [Adaptive Cards](https://adaptivecards.io)"
        }
    ]
}
```

### <a name="mention-support-within-adaptive-cards-v12"></a><span data-ttu-id="e23ba-158">Упоминание поддержки в адаптивных картах v1.2</span><span class="sxs-lookup"><span data-stu-id="e23ba-158">Mention support within Adaptive cards v1.2</span></span>

<span data-ttu-id="e23ba-159">Упоминания на основе карт поддерживаются в веб-, настольных и мобильных клиентах.</span><span class="sxs-lookup"><span data-stu-id="e23ba-159">Card based mentions are supported in web, desktop and mobile clients.</span></span> <span data-ttu-id="e23ba-160">Вы можете добавить @ упоминания в тексте адаптивной карты для ботов и ответов на расширение обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="e23ba-160">You can add @ mentions within an adaptive card body for bots and messaging extension responses.</span></span> <span data-ttu-id="e23ba-161">Чтобы добавить @mentions in cards, следуйте той же логике уведомлений и визуализации, что и упоминания на основе сообщений в беседах в чатах каналов и [групп.](../../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions)</span><span class="sxs-lookup"><span data-stu-id="e23ba-161">To add @ mentions in cards, follow the same notification logic and rendering as that of message based [mentions in channel and group chat conversations](../../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions).</span></span>

<span data-ttu-id="e23ba-162">Боты и расширения обмена сообщениями могут включать упоминания в контенте карты в [элементах TextBlock](https://adaptivecards.io/explorer/TextBlock.html) и [FactSet.](https://adaptivecards.io/explorer/FactSet.html)</span><span class="sxs-lookup"><span data-stu-id="e23ba-162">Bots and messaging extensions can include mentions within the card content in [TextBlock](https://adaptivecards.io/explorer/TextBlock.html) and [FactSet](https://adaptivecards.io/explorer/FactSet.html) elements.</span></span>

> [!NOTE]
> * <span data-ttu-id="e23ba-163">[Элементы мультимедиа в](https://adaptivecards.io/explorer/Media.html) настоящее время не поддерживаются в адаптивных картах v1.2 на платформе Teams.</span><span class="sxs-lookup"><span data-stu-id="e23ba-163">[Media elements](https://adaptivecards.io/explorer/Media.html) are currently not supported in Adaptive cards v1.2 on the Teams platform.</span></span>
> * <span data-ttu-id="e23ba-164">Упоминания & группы не поддерживаются в сообщениях ботов.</span><span class="sxs-lookup"><span data-stu-id="e23ba-164">Channel & Team mentions are not supported in bot messages.</span></span>

#### <a name="constructing-mentions"></a><span data-ttu-id="e23ba-165">Построение упоминаний</span><span class="sxs-lookup"><span data-stu-id="e23ba-165">Constructing mentions</span></span>

<span data-ttu-id="e23ba-166">Чтобы включить упоминание в адаптивной карте, приложение должно включить следующие элементы</span><span class="sxs-lookup"><span data-stu-id="e23ba-166">To include a mention in an Adaptive card your app needs to include the following elements</span></span>

* <span data-ttu-id="e23ba-167">`<at>username</at>` в поддерживаемых элементах адаптивной карты</span><span class="sxs-lookup"><span data-stu-id="e23ba-167">`<at>username</at>` in the supported Adaptive card elements</span></span>
* <span data-ttu-id="e23ba-168">Объект внутри свойства в содержимом карты, который включает пользовательский `mention` `msteams` id Teams упоминаемого пользователя</span><span class="sxs-lookup"><span data-stu-id="e23ba-168">The `mention` object inside of an `msteams` property in the card content, which includes the Teams user id of the user being mentioned</span></span>

#### <a name="sample-adaptive-card-with-a-mention"></a><span data-ttu-id="e23ba-169">Пример адаптивной карты с упоминанием</span><span class="sxs-lookup"><span data-stu-id="e23ba-169">Sample Adaptive card with a mention</span></span>

``` json
{
  "contentType": "application/vnd.microsoft.card.adaptive",
  "content": {
    "type": "AdaptiveCard",
    "body": [
      {
        "type": "TextBlock",
        "text": "Hi <at>John Doe</at>"
      }
    ],
    "$schema": "https://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.0",
    "msteams": {
      "entities": [
        {
          "type": "mention",
          "text": "<at>John Doe</at>",
          "mentioned": {
            "id": "29:123124124124",
            "name": "John Doe"
          }
        }
      ]
    }
  }
}
```


### <a name="information-masking-in-adaptive-cards"></a><span data-ttu-id="e23ba-170">Маскировка сведений в адаптивных картах</span><span class="sxs-lookup"><span data-stu-id="e23ba-170">Information masking in Adaptive cards</span></span>
<span data-ttu-id="e23ba-171">Используйте свойство маскировки информации для маскировки определенных сведений, таких как пароль или конфиденциальные сведения пользователей в элементе ввода адаптивной [`Input.Text`](https://adaptivecards.io/explorer/Input.Text.html) карты.</span><span class="sxs-lookup"><span data-stu-id="e23ba-171">Use the information masking property to mask specific information, such as password or sensitive information from users within the Adaptive card [`Input.Text`](https://adaptivecards.io/explorer/Input.Text.html) input element.</span></span> 

> [!NOTE]
> <span data-ttu-id="e23ba-172">Эта функция поддерживает только маскировку стороной клиента, текст ввода в маске отправляется в виде четкого текста на адрес конечной точки https, заданный во время [конфигурации бота.](../../build-your-first-app/build-bot.md#4-configure-your-bot)</span><span class="sxs-lookup"><span data-stu-id="e23ba-172">The feature only supports client side information masking, the masked input text is sent as clear text to the https endpoint address that was specified during [bot configuration](../../build-your-first-app/build-bot.md#4-configure-your-bot).</span></span> 

> [!NOTE]
> <span data-ttu-id="e23ba-173">Свойство маскировки информации в настоящее время доступно только в предварительном просмотре разработчика.</span><span class="sxs-lookup"><span data-stu-id="e23ba-173">The information masking property is currently available in the developer preview only.</span></span>

<span data-ttu-id="e23ba-174">Чтобы скрыть сведения в адаптивных картах, добавьте свойство введите и установите `isMasked`  `Input.Text` значение true. </span><span class="sxs-lookup"><span data-stu-id="e23ba-174">To mask information in Adaptive cards, add the `isMasked` property to **type** `Input.Text`, and set its value to *true*.</span></span>

#### <a name="sample-adaptive-card-with-masking-property"></a><span data-ttu-id="e23ba-175">Пример адаптивной карты с свойством маскировки</span><span class="sxs-lookup"><span data-stu-id="e23ba-175">Sample Adaptive card with masking property</span></span>

```json
{
    "type": "Input.Text",
    "id": "secretThing",
    "style": "password",
    "isMasked": true
  },
```

<span data-ttu-id="e23ba-176">Ниже приводится пример маскировки сведений в адаптивных картах:</span><span class="sxs-lookup"><span data-stu-id="e23ba-176">The following image is an example of masking information in Adaptive cards:</span></span>

![Маскировка информационного изображения](../../assets/images/cards/masking-information-view.png)

### <a name="full-width-adaptive-card"></a><span data-ttu-id="e23ba-178">Адаптивная карта с полной шириной</span><span class="sxs-lookup"><span data-stu-id="e23ba-178">Full width Adaptive card</span></span>
<span data-ttu-id="e23ba-179">Свойство можно использовать для расширения ширины адаптивной карты и использования `msteams` дополнительного пространства холста.</span><span class="sxs-lookup"><span data-stu-id="e23ba-179">You can use the `msteams` property to expand the width of an Adaptive card and make use of additional canvas space.</span></span> <span data-ttu-id="e23ba-180">Сведения об использовании свойства см. в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="e23ba-180">For information on how to use the property, see the following example:</span></span>

#### <a name="constructing-full-width-cards"></a><span data-ttu-id="e23ba-181">Построение карт полной ширины</span><span class="sxs-lookup"><span data-stu-id="e23ba-181">Constructing full width cards</span></span>
<span data-ttu-id="e23ba-182">Чтобы сделать полную ширину адаптивной карты, объект в свойстве контента карточки `width` `msteams` должен быть задат. `Full`</span><span class="sxs-lookup"><span data-stu-id="e23ba-182">To make a full width Adaptive card the `width` object in `msteams` property in the card content must be set to `Full`.</span></span>
<span data-ttu-id="e23ba-183">Кроме того, приложение должно включать следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="e23ba-183">In addition, your app must include the following elements:</span></span>

#### <a name="sample-adaptive-card-with-full-width"></a><span data-ttu-id="e23ba-184">Пример адаптивной карты с полной шириной</span><span class="sxs-lookup"><span data-stu-id="e23ba-184">Sample adaptive card with full width</span></span>

``` json
{
    "type": "AdaptiveCard",
    "body": [{
        "type": "Container",
        "items": [{
            "type": "TextBlock",
            "text": "Digest card",
            "size": "Large",
            "weight": "Bolder"
        }]
    }],

    "msteams": {
        "width": "Full"
    },
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.2"
}
```

<span data-ttu-id="e23ba-185">Адаптивная карта с полной шириной отображается следующим образом: представление адаптивной карты полной ![ ширины](../../assets/images/cards/full-width-adaptive-card.png)</span><span class="sxs-lookup"><span data-stu-id="e23ba-185">A full width Adaptive Card appears as follows: ![Full width Adaptive Card view](../../assets/images/cards/full-width-adaptive-card.png)</span></span>

<span data-ttu-id="e23ba-186">Если свойство не настроено до полного, представление адаптивной карты по умолчанию следующим образом: представление адаптивной карты малой `width`  ![ ширины](../../assets/images/cards/small-width-adaptive-card.png)</span><span class="sxs-lookup"><span data-stu-id="e23ba-186">If you have not set the `width` property to *Full*, then the default view of the Adaptive Card is as follows: ![Small width Adaptive Card view](../../assets/images/cards/small-width-adaptive-card.png)</span></span>

### <a name="typeahead-support"></a><span data-ttu-id="e23ba-187">Поддержка typeahead</span><span class="sxs-lookup"><span data-stu-id="e23ba-187">Typeahead support</span></span>

<span data-ttu-id="e23ba-188">В элементе схемы запрос на фильтрацию и выбор большого количества вариантов может значительно замедлить [`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) выполнение задач.</span><span class="sxs-lookup"><span data-stu-id="e23ba-188">Within the [`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) schema element, asking users to filter through and select through a sizable number of choices can significantly slow down task completion.</span></span> <span data-ttu-id="e23ba-189">Поддержка ввода в адаптивных картах может упростить выбор входных данных, сужая или фильтруя набор вариантов ввода при вводе ввода пользователем.</span><span class="sxs-lookup"><span data-stu-id="e23ba-189">Typeahead support within Adaptive cards can simplify input selection by narrowing or filtering the set of input choices as a user is typing the input.</span></span> 

#### <a name="enable-typeahead-in-adaptive-cards"></a><span data-ttu-id="e23ba-190">Включить введите в адаптивных картах</span><span class="sxs-lookup"><span data-stu-id="e23ba-190">Enable typeahead in Adaptive cards</span></span>

<span data-ttu-id="e23ba-191">Чтобы включить введите в `Input.Choiceset` наборе, `style` чтобы `filtered` и `isMultiSelect` убедиться, установлено `false` .</span><span class="sxs-lookup"><span data-stu-id="e23ba-191">To enable typeahead within the `Input.Choiceset` set `style` to `filtered` and ensure `isMultiSelect` is set to `false`.</span></span> 

#### <a name="sample-adaptive-card-with-typeahead-support"></a><span data-ttu-id="e23ba-192">Пример адаптивной карты с поддержкой typeahead</span><span class="sxs-lookup"><span data-stu-id="e23ba-192">Sample adaptive card with typeahead support</span></span>

``` json
{
   "type": "Input.ChoiceSet",
   "label": "Select a user",
   "isMultiSelect": false,
   "choices":  [
      { "title": "User 1", "value": "User1" },
      { "title": "User 2", "value": "User2" }
    ],
   "style": "filtered"
}
``` 

### <a name="stage-view-for-images-in-adaptive-cards"></a><span data-ttu-id="e23ba-193">Представление сцены для изображений в адаптивных картах</span><span class="sxs-lookup"><span data-stu-id="e23ba-193">Stage view for images in Adaptive Cards</span></span>

> [!NOTE]
> <span data-ttu-id="e23ba-194">В настоящее время эта функция доступна только в предварительном просмотре разработчика.</span><span class="sxs-lookup"><span data-stu-id="e23ba-194">This feature is currently available in developer preview only.</span></span>
 
<span data-ttu-id="e23ba-195">В адаптивной карте свойство можно использовать для выборочного отображения изображений в представлении `msteams` сцены.</span><span class="sxs-lookup"><span data-stu-id="e23ba-195">In an Adaptive card, you can use the `msteams` property to add the ability to display images in stage view selectively.</span></span> <span data-ttu-id="e23ba-196">Когда пользователи наведите курсор над изображениями, они увидят значок расширения, для которого установлен `allowExpand` атрибут `true` .</span><span class="sxs-lookup"><span data-stu-id="e23ba-196">When users hover over the images, they would see an expand icon, for which the `allowExpand` attribute is set to `true`.</span></span> <span data-ttu-id="e23ba-197">Сведения об использовании свойства см. в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="e23ba-197">For information on how to use the property, see the following example:</span></span>

``` json
{
    "type": "AdaptiveCard",
     "body": [
          {
            "type": "Image",
            "url": "https://picsum.photos/200/200?image=110",
            "msTeams": {
              "allowExpand": true
            }
          },
     ],
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.2"
}
```

<span data-ttu-id="e23ba-198">Когда пользователи наведите курсор над изображением, в правом верхнем углу изображения появляется значок расширения: адаптивная карта ![ с расширяемым изображением](../../assets/images/cards/adaptivecard-hover-expand-icon.png)</span><span class="sxs-lookup"><span data-stu-id="e23ba-198">When users hover over the image, an expand icon appears at top right corner of the image: ![Adaptive card with expandable image](../../assets/images/cards/adaptivecard-hover-expand-icon.png)</span></span>

<span data-ttu-id="e23ba-199">Изображение отображается в представлении сцены, когда пользователь выбирает кнопку расширения: ![ изображение расширено до представления сцены](../../assets/images/cards/adaptivecard-expand-image.png)</span><span class="sxs-lookup"><span data-stu-id="e23ba-199">The image appears in stage view when the user selects the expand button: ![Image expanded to stage view](../../assets/images/cards/adaptivecard-expand-image.png)</span></span>

<span data-ttu-id="e23ba-200">В представлении сцены пользователи могут масштабировать изображение и увеличивать его.</span><span class="sxs-lookup"><span data-stu-id="e23ba-200">In the stage view, users can zoom in and zoom out of the image.</span></span> <span data-ttu-id="e23ba-201">Вы можете выбрать, какие изображения в адаптивной карте должны иметь эту возможность.</span><span class="sxs-lookup"><span data-stu-id="e23ba-201">You can select which images in your Adaptive card needs to have this capability.</span></span>

> [!NOTE]
> <span data-ttu-id="e23ba-202">Возможность масштабирования и масштабирования применяется только к элементам изображения (тип изображения) в адаптивной карте.</span><span class="sxs-lookup"><span data-stu-id="e23ba-202">Zoom in and zoom out capability applies only to the image elements (Image type) in an Adaptive card.</span></span>

> [!NOTE]
> <span data-ttu-id="e23ba-203">Для мобильных приложений Teams функции представления этапов для изображений в адаптивных картах доступны по умолчанию, и пользователи смогут просматривать адаптивные изображения карт в стадии представления, просто нажав на изображение, независимо от того, присутствует атрибут или `allowExpand` нет.</span><span class="sxs-lookup"><span data-stu-id="e23ba-203">For Teams mobile apps, stage view functionality for images in Adaptive Cards are available by default and users will be able to view Adaptive card images in stage view by simply tapping on the image, irrespective of whether the `allowExpand` attribute is present or not.</span></span>

# <a name="markdown-formatting-o365-connector-cards"></a>[<span data-ttu-id="e23ba-204">**Форматирование разметки: карты соединителения O365**</span><span class="sxs-lookup"><span data-stu-id="e23ba-204">**Markdown formatting: O365 Connector Cards**</span></span>](#tab/connector-md)

<span data-ttu-id="e23ba-205">Карты Connector поддерживают ограниченное форматирование Markdown и HTML.</span><span class="sxs-lookup"><span data-stu-id="e23ba-205">Connector cards support limited Markdown and HTML formatting.</span></span> <span data-ttu-id="e23ba-206">Поддержка HTML описана в последнем разделе.</span><span class="sxs-lookup"><span data-stu-id="e23ba-206">HTML support is described in the last section.</span></span>

| <span data-ttu-id="e23ba-207">Style</span><span class="sxs-lookup"><span data-stu-id="e23ba-207">Style</span></span> | <span data-ttu-id="e23ba-208">Пример</span><span class="sxs-lookup"><span data-stu-id="e23ba-208">Example</span></span> | <span data-ttu-id="e23ba-209">Markdown</span><span class="sxs-lookup"><span data-stu-id="e23ba-209">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e23ba-210">bold</span><span class="sxs-lookup"><span data-stu-id="e23ba-210">bold</span></span> | <span data-ttu-id="e23ba-211">**text**</span><span class="sxs-lookup"><span data-stu-id="e23ba-211">**text**</span></span> | `**text**` |
| <span data-ttu-id="e23ba-212">italic</span><span class="sxs-lookup"><span data-stu-id="e23ba-212">italic</span></span> | <span data-ttu-id="e23ba-213">*text*</span><span class="sxs-lookup"><span data-stu-id="e23ba-213">*text*</span></span> | `*text*` |
| <span data-ttu-id="e23ba-214">загон (уровни 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="e23ba-214">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="e23ba-215">**Text**</span><span class="sxs-lookup"><span data-stu-id="e23ba-215">**Text**</span></span> | `### Text`|
| <span data-ttu-id="e23ba-216">strikethrough</span><span class="sxs-lookup"><span data-stu-id="e23ba-216">strikethrough</span></span> | <span data-ttu-id="e23ba-217">~~text~~</span><span class="sxs-lookup"><span data-stu-id="e23ba-217">~~text~~</span></span> | `~~text~~` |
| <span data-ttu-id="e23ba-218">необученный список</span><span class="sxs-lookup"><span data-stu-id="e23ba-218">unordered list</span></span> | <ul><li><span data-ttu-id="e23ba-219">текст</span><span class="sxs-lookup"><span data-stu-id="e23ba-219">text</span></span></li><li><span data-ttu-id="e23ba-220">текст</span><span class="sxs-lookup"><span data-stu-id="e23ba-220">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="e23ba-221">упорядоченный список</span><span class="sxs-lookup"><span data-stu-id="e23ba-221">ordered list</span></span> | <ol><li><span data-ttu-id="e23ba-222">текст</span><span class="sxs-lookup"><span data-stu-id="e23ba-222">text</span></span></li><li><span data-ttu-id="e23ba-223">текст</span><span class="sxs-lookup"><span data-stu-id="e23ba-223">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="e23ba-224">предформатированный текст</span><span class="sxs-lookup"><span data-stu-id="e23ba-224">preformatted text</span></span> | `text` | ``preformatted text`` |
| <span data-ttu-id="e23ba-225">blockquote</span><span class="sxs-lookup"><span data-stu-id="e23ba-225">blockquote</span></span> | <span data-ttu-id="e23ba-226">>блокквойта</span><span class="sxs-lookup"><span data-stu-id="e23ba-226">>blockquote text</span></span> | `>blockquote text` |
| <span data-ttu-id="e23ba-227">гиперссылка</span><span class="sxs-lookup"><span data-stu-id="e23ba-227">hyperlink</span></span> | [<span data-ttu-id="e23ba-228">Bing</span><span class="sxs-lookup"><span data-stu-id="e23ba-228">Bing</span></span>](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| <span data-ttu-id="e23ba-229">ссылка на изображение</span><span class="sxs-lookup"><span data-stu-id="e23ba-229">image link</span></span> |![Утка на скале](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

<span data-ttu-id="e23ba-231">В соединитеных картах новые линии отрисовываются для `\n\n` , но не для или `\n` `\r` .</span><span class="sxs-lookup"><span data-stu-id="e23ba-231">In connector cards, newlines are rendered for `\n\n`, but not for `\n` or `\r`.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-markdown"></a><span data-ttu-id="e23ba-232">Различия для мобильных и настольных компьютеров для соединительная карта с помощью Markdown</span><span class="sxs-lookup"><span data-stu-id="e23ba-232">Mobile and desktop differences for connector cards using Markdown</span></span>

<span data-ttu-id="e23ba-233">На рабочем столе форматирование Markdown для карт соединительная система выглядит так:</span><span class="sxs-lookup"><span data-stu-id="e23ba-233">On the desktop, Markdown formatting for connector cards looks like this:</span></span>

![Форматирование разметки для соединительная карта в клиенте Desktop](../../assets/images/cards/connector-desktop-markdown-combined.png)

<span data-ttu-id="e23ba-235">В iOS форматирование markdown для соединители-карт выглядит так:</span><span class="sxs-lookup"><span data-stu-id="e23ba-235">On iOS, Markdown formatting for connector cards looks like this:</span></span>

![Форматирование markdown для карт соединителения в клиенте iOS](../../assets/images/cards/connector-iphone-markdown-combined-80.png)

<span data-ttu-id="e23ba-237">Вопросы:</span><span class="sxs-lookup"><span data-stu-id="e23ba-237">Issues:</span></span>

* <span data-ttu-id="e23ba-238">Клиент iOS для Teams не отрисовывает встроенные изображения Markdown или HTML в соединительных картах.</span><span class="sxs-lookup"><span data-stu-id="e23ba-238">The iOS client for Teams does not render Markdown or HTML inline images in Connector Cards.</span></span>
* <span data-ttu-id="e23ba-239">Блокквоты отрисовываются как отступные, но без серого фона.</span><span class="sxs-lookup"><span data-stu-id="e23ba-239">Blockquotes are rendered as indented but without a gray background.</span></span>

<span data-ttu-id="e23ba-240">На Android форматирование markdown для карт соединителения выглядит так:</span><span class="sxs-lookup"><span data-stu-id="e23ba-240">On Android, Markdown formatting for connector cards looks like this:</span></span>

![Форматирование разметки для карт соединителения в клиенте Android](../../assets/images/cards/connector-android-markdown-combined.png)

### <a name="formatting-example-for-markdown-connector-cards"></a><span data-ttu-id="e23ba-242">Пример форматирования карт соединителения Markdown</span><span class="sxs-lookup"><span data-stu-id="e23ba-242">Formatting example for Markdown Connector Cards</span></span>

``` json
{
  "contentType": "application/vnd.microsoft.teams.card.o365connector",
  "content": {
    "@type": "MessageCard",
    "@context": "https://schema.org/extensions",
    "summary": "Summary",
    "title": "Connector Card Markdown formatting",
    "sections": [
        {
            "text": "This is some **bold** text"
        },
        {
            "text": "This is some _italic_ text"
        },
        {
            "text": "# Header 1\r## Header 2\r### Header 3"
        },
        {
            "text": "- Bullet \r- List \r"
        },
        {
            "text": "1. Numbered\r1. List \r"
        },
        {
            "text": "Link: [Bing](https://www.bing.com)"
        },
        {
            "text": "embedded image link: ![Duck on a rock](https://aka.ms/Fo983c)"
        },
        {
            "text": "`preformatted text`"
        },
        {
            "text": "Newlines (backslash n, backslash n):\n\nline a\n\nline b\n\nline c"
        },
        {
            "text": ">This is a blockquote"
        }
     ]
  }
}

```

---

## <a name="formatting-cards-with-html"></a><span data-ttu-id="e23ba-243">Форматирование карт с ПОМОЩЬЮ HTML</span><span class="sxs-lookup"><span data-stu-id="e23ba-243">Formatting cards with HTML</span></span>

# <a name="html-formatting-o365-connector-cards"></a>[<span data-ttu-id="e23ba-244">**Форматирование HTML: карты соединителя O365**</span><span class="sxs-lookup"><span data-stu-id="e23ba-244">**HTML formatting: O365 Connector Cards**</span></span>](#tab/connector-html)

<span data-ttu-id="e23ba-245">Карты Connector поддерживают ограниченное форматирование Markdown и HTML.</span><span class="sxs-lookup"><span data-stu-id="e23ba-245">Connector cards support limited Markdown and HTML formatting.</span></span> <span data-ttu-id="e23ba-246">Markdown описан в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="e23ba-246">Markdown is described in the next section.</span></span>

| <span data-ttu-id="e23ba-247">Style</span><span class="sxs-lookup"><span data-stu-id="e23ba-247">Style</span></span> | <span data-ttu-id="e23ba-248">Пример</span><span class="sxs-lookup"><span data-stu-id="e23ba-248">Example</span></span> | <span data-ttu-id="e23ba-249">HTML</span><span class="sxs-lookup"><span data-stu-id="e23ba-249">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e23ba-250">bold</span><span class="sxs-lookup"><span data-stu-id="e23ba-250">bold</span></span> | <span data-ttu-id="e23ba-251">**text**</span><span class="sxs-lookup"><span data-stu-id="e23ba-251">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="e23ba-252">italic</span><span class="sxs-lookup"><span data-stu-id="e23ba-252">italic</span></span> | <span data-ttu-id="e23ba-253">*text*</span><span class="sxs-lookup"><span data-stu-id="e23ba-253">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="e23ba-254">загон (уровни 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="e23ba-254">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="e23ba-255">**Text**</span><span class="sxs-lookup"><span data-stu-id="e23ba-255">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="e23ba-256">strikethrough</span><span class="sxs-lookup"><span data-stu-id="e23ba-256">strikethrough</span></span> | <span data-ttu-id="e23ba-257">~~text~~</span><span class="sxs-lookup"><span data-stu-id="e23ba-257">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="e23ba-258">необученный список</span><span class="sxs-lookup"><span data-stu-id="e23ba-258">unordered list</span></span> | <ul><li><span data-ttu-id="e23ba-259">текст</span><span class="sxs-lookup"><span data-stu-id="e23ba-259">text</span></span></li><li><span data-ttu-id="e23ba-260">текст</span><span class="sxs-lookup"><span data-stu-id="e23ba-260">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="e23ba-261">упорядоченный список</span><span class="sxs-lookup"><span data-stu-id="e23ba-261">ordered list</span></span> | <ol><li><span data-ttu-id="e23ba-262">текст</span><span class="sxs-lookup"><span data-stu-id="e23ba-262">text</span></span></li><li><span data-ttu-id="e23ba-263">текст</span><span class="sxs-lookup"><span data-stu-id="e23ba-263">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="e23ba-264">предформатированный текст</span><span class="sxs-lookup"><span data-stu-id="e23ba-264">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="e23ba-265">blockquote</span><span class="sxs-lookup"><span data-stu-id="e23ba-265">blockquote</span></span> | <blockquote><span data-ttu-id="e23ba-266">текст</span><span class="sxs-lookup"><span data-stu-id="e23ba-266">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="e23ba-267">гиперссылка</span><span class="sxs-lookup"><span data-stu-id="e23ba-267">hyperlink</span></span> | [<span data-ttu-id="e23ba-268">Bing</span><span class="sxs-lookup"><span data-stu-id="e23ba-268">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="e23ba-269">ссылка на изображение</span><span class="sxs-lookup"><span data-stu-id="e23ba-269">image link</span></span> | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

<span data-ttu-id="e23ba-270">В соединительных картах новые линии отрисовываются в HTML с помощью `<p>` тега.</span><span class="sxs-lookup"><span data-stu-id="e23ba-270">In connector cards, newlines are rendered in HTML using the `<p>` tag.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-html"></a><span data-ttu-id="e23ba-271">Различия между мобильными и настольными устройствами для соединительная карта с помощью HTML</span><span class="sxs-lookup"><span data-stu-id="e23ba-271">Mobile and desktop differences for connector cards using HTML</span></span>

<span data-ttu-id="e23ba-272">Форматирование HTML-форматов для соединительная карточки на рабочем столе выглядит так:</span><span class="sxs-lookup"><span data-stu-id="e23ba-272">On the desktop, HTML formatting for connector cards looks like this:</span></span>

![ФОРМАТирование HTML для соединителя карт в клиенте Desktop](../../assets/images/cards/Connector-desktop-html-combined.png)

<span data-ttu-id="e23ba-274">В iOS форматирование HTML выглядит так:</span><span class="sxs-lookup"><span data-stu-id="e23ba-274">On iOS, HTML formatting looks like this:</span></span>

![Форматирование HTML для соединительных карт в клиенте iOS](../../assets/images/cards/connector-iphone-html-combined-80.png)

<span data-ttu-id="e23ba-276">Вопросы:</span><span class="sxs-lookup"><span data-stu-id="e23ba-276">Issues:</span></span>

* <span data-ttu-id="e23ba-277">Встроенные изображения не отрисовываются в iOS с помощью markdown или HTML-кодов в соединителях.</span><span class="sxs-lookup"><span data-stu-id="e23ba-277">Inline images are not rendered on iOS using either Markdown or HTML in Connector Cards.</span></span>
* <span data-ttu-id="e23ba-278">Предформатированный текст отрисовывается, но не имеет серого фона.</span><span class="sxs-lookup"><span data-stu-id="e23ba-278">Preformatted text is rendered but does not have a gray background.</span></span>

<span data-ttu-id="e23ba-279">На Android форматирование HTML выглядит так:</span><span class="sxs-lookup"><span data-stu-id="e23ba-279">On Android, HTML formatting looks like this:</span></span>

![Форматирование HTML для соединительных карт в клиенте Android](../../assets/images/cards/connector-android-html-combined.png)

### <a name="formatting-sample-for-html-connector-cards"></a><span data-ttu-id="e23ba-281">Пример форматирования для HTML-карт соединителя</span><span class="sxs-lookup"><span data-stu-id="e23ba-281">Formatting sample for HTML Connector Cards</span></span>

``` json
{
  "contentType": "application/vnd.microsoft.teams.card.o365connector",
  "content": {
    "@type": "MessageCard",
    "@context": "https://schema.org/extensions",
    "summary": "Summary",
    "title": "Connector Card HTML formatting",
    "sections": [
        {
            "text": "This is some <strong>bold</strong> text"
        },
        {
            "text": "This is some <em>italic</em> text"
        },
        {
            "text": "This is some <strike>strikethrough</strike> text"
        },
        {
            "text": "<h1>Header 1</h1>\r<h2>Header 2</h2>\r <h3>Header 3</h3>"
        },
        {
            "text": "bullet list <ul><li>text</li><li>text</li></ul>"
        },
        {
            "text": "ordered list <ol><li>text</li><li>text</li></ol>"
        },
        {
            "text": "hyperlink <a href=\"https://www.bing.com/\">Bing</a>"
        },
        {
            "text": "embedded image <img src=\"https://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img>"
        },
        {
            "text": "preformatted text <pre>text</pre>"
        },
        {
            "text": "Paragraphs <p>Line a</p><p>Line b</p>"
        },
        {
            "text": "<blockquote>Blockquote text</blockquote>"
        }
     ]
  }
}

```

# <a name="html-formatting-hero-and-thumbnail-cards"></a>[<span data-ttu-id="e23ba-282">**Форматирование HTML: карты героя и эскиза**</span><span class="sxs-lookup"><span data-stu-id="e23ba-282">**HTML Formatting: hero and thumbnail cards**</span></span>](#tab/simple-html)

<span data-ttu-id="e23ba-283">HTML-теги поддерживаются для простых карт, таких как карта героя и эскиза.</span><span class="sxs-lookup"><span data-stu-id="e23ba-283">HTML tags are supported for simple cards such as the hero and thumbnail card.</span></span> <span data-ttu-id="e23ba-284">Markdown не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="e23ba-284">Markdown is not supported.</span></span>

| <span data-ttu-id="e23ba-285">Style</span><span class="sxs-lookup"><span data-stu-id="e23ba-285">Style</span></span> | <span data-ttu-id="e23ba-286">Пример</span><span class="sxs-lookup"><span data-stu-id="e23ba-286">Example</span></span> | <span data-ttu-id="e23ba-287">HTML</span><span class="sxs-lookup"><span data-stu-id="e23ba-287">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e23ba-288">bold</span><span class="sxs-lookup"><span data-stu-id="e23ba-288">bold</span></span> | <span data-ttu-id="e23ba-289">**text**</span><span class="sxs-lookup"><span data-stu-id="e23ba-289">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="e23ba-290">italic</span><span class="sxs-lookup"><span data-stu-id="e23ba-290">italic</span></span> | <span data-ttu-id="e23ba-291">*text*</span><span class="sxs-lookup"><span data-stu-id="e23ba-291">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="e23ba-292">загон (уровни 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="e23ba-292">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="e23ba-293">**Text**</span><span class="sxs-lookup"><span data-stu-id="e23ba-293">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="e23ba-294">strikethrough</span><span class="sxs-lookup"><span data-stu-id="e23ba-294">strikethrough</span></span> | <span data-ttu-id="e23ba-295">~~text~~</span><span class="sxs-lookup"><span data-stu-id="e23ba-295">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="e23ba-296">необученный список</span><span class="sxs-lookup"><span data-stu-id="e23ba-296">unordered list</span></span> | <ul><li><span data-ttu-id="e23ba-297">текст</span><span class="sxs-lookup"><span data-stu-id="e23ba-297">text</span></span></li><li><span data-ttu-id="e23ba-298">текст</span><span class="sxs-lookup"><span data-stu-id="e23ba-298">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="e23ba-299">упорядоченный список</span><span class="sxs-lookup"><span data-stu-id="e23ba-299">ordered list</span></span> | <ol><li><span data-ttu-id="e23ba-300">текст</span><span class="sxs-lookup"><span data-stu-id="e23ba-300">text</span></span></li><li><span data-ttu-id="e23ba-301">текст</span><span class="sxs-lookup"><span data-stu-id="e23ba-301">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="e23ba-302">предформатированный текст</span><span class="sxs-lookup"><span data-stu-id="e23ba-302">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="e23ba-303">blockquote</span><span class="sxs-lookup"><span data-stu-id="e23ba-303">blockquote</span></span> | <blockquote><span data-ttu-id="e23ba-304">текст</span><span class="sxs-lookup"><span data-stu-id="e23ba-304">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="e23ba-305">гиперссылка</span><span class="sxs-lookup"><span data-stu-id="e23ba-305">hyperlink</span></span> | [<span data-ttu-id="e23ba-306">Bing</span><span class="sxs-lookup"><span data-stu-id="e23ba-306">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="e23ba-307">ссылка на изображение</span><span class="sxs-lookup"><span data-stu-id="e23ba-307">image link</span></span> |<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a><span data-ttu-id="e23ba-308">Различия для мобильных и настольных компьютеров для простых карт</span><span class="sxs-lookup"><span data-stu-id="e23ba-308">Mobile and desktop differences for simple cards</span></span>

<span data-ttu-id="e23ba-309">Из-за различий в разрешении между настольной и мобильной платформами форматирование отличается между настольным компьютером и мобильной версией Teams.</span><span class="sxs-lookup"><span data-stu-id="e23ba-309">Because of resolution differences between the desktop and mobile platform, formatting is different between the desktop and the mobile version of Teams.</span></span>

<span data-ttu-id="e23ba-310">На рабочем столе форматирование HTML выглядит так:</span><span class="sxs-lookup"><span data-stu-id="e23ba-310">On the desktop, HTML formatting appears like this:</span></span>

![Форматирование HTML в клиенте Desktop](../../assets/images/cards/card-formatting-xml-desktop-v2.png)

<span data-ttu-id="e23ba-312">На iOS форматирование HTML выглядит так:</span><span class="sxs-lookup"><span data-stu-id="e23ba-312">On iOS, HTML formatting appears like this:</span></span>

![Форматирование HTML в клиенте iOS](../../assets/images/cards/card-formatting-xml-mobile-v2.png)

<span data-ttu-id="e23ba-314">Вопросы:</span><span class="sxs-lookup"><span data-stu-id="e23ba-314">Issues:</span></span>

* <span data-ttu-id="e23ba-315">Форматирование символов, как смелый и italic, не отрисовка в iOS.</span><span class="sxs-lookup"><span data-stu-id="e23ba-315">Character formatting like bold and italic are not rendered on iOS.</span></span>

<span data-ttu-id="e23ba-316">На Android форматирование HTML выглядит так:</span><span class="sxs-lookup"><span data-stu-id="e23ba-316">On Android, HTML formatting appears like this:</span></span>

![Форматирование HTML в клиенте Android](../../assets/images/cards/card-formatting-xml-android-60.png)

<span data-ttu-id="e23ba-318">Форматирование символов, как смелый и italic отображения правильно на Android.</span><span class="sxs-lookup"><span data-stu-id="e23ba-318">Character formatting like bold and italic display correctly on Android.</span></span>

### <a name="formatting-sample-for-html-formatting-in-simple-cards"></a><span data-ttu-id="e23ba-319">Пример форматирования форматирования HTML в простых картах</span><span class="sxs-lookup"><span data-stu-id="e23ba-319">Formatting sample for HTML formatting in simple cards</span></span>

<span data-ttu-id="e23ba-320">Эти скриншоты были созданы с помощью Teams AppStudio, где текстовое свойство карты-героя было задано следующей строке.</span><span class="sxs-lookup"><span data-stu-id="e23ba-320">These screenshots were created using Teams AppStudio, where the text property of a hero card was set to the following string.</span></span> <span data-ttu-id="e23ba-321">Вы можете протестировать форматирование в собственных картах, изменяя этот код.</span><span class="sxs-lookup"><span data-stu-id="e23ba-321">You can test formatting in your own cards by modifying this code.</span></span>

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"https://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`

---
