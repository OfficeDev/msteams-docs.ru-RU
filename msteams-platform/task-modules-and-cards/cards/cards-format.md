---
title: Форматирование текста в карточках
description: Описание форматирования текста карточки в Microsoft Teams
keywords: формат карточек Боты Teams
ms.date: 03/29/2018
ms.openlocfilehash: fcf0692fe033cd3c30ea1e3ac7bda8ddd06297ca
ms.sourcegitcommit: 64acd30eee8af5fe151e9866c13226ed3f337c72
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/18/2020
ms.locfileid: "49346709"
---
# <a name="format-cards-in-teams"></a><span data-ttu-id="9c8f9-104">Форматирование карточек в Teams</span><span class="sxs-lookup"><span data-stu-id="9c8f9-104">Format cards in Teams</span></span>

<span data-ttu-id="9c8f9-105">В зависимости от типа карты в карточки можно добавлять форматированный текст в карточки с помощью Markdown или HTML.</span><span class="sxs-lookup"><span data-stu-id="9c8f9-105">You can add rich text formatting to your cards using either Markdown or HTML, depending on the card type.</span></span>

<span data-ttu-id="9c8f9-106">Карточки поддерживают форматирование только в свойстве Text, а не в свойствах Title и субтитров.</span><span class="sxs-lookup"><span data-stu-id="9c8f9-106">Cards support formatting in the text property only, not in the title or subtitle properties.</span></span> <span data-ttu-id="9c8f9-107">Форматирование можно указать с помощью подмножества форматирования XML (HTML) или Markdown в зависимости от типа карты.</span><span class="sxs-lookup"><span data-stu-id="9c8f9-107">Formatting can be specified using a subset of XML (HTML) formatting, or Markdown depending on card type.</span></span> <span data-ttu-id="9c8f9-108">Для текущих и будущих развертываний рекомендуется использовать форматирование Markdown.</span><span class="sxs-lookup"><span data-stu-id="9c8f9-108">For current and future development Adaptive cards using Markdown formatting is recommended.</span></span>

<span data-ttu-id="9c8f9-109">Поддержка форматирования различается для разных типов карточек, а отображение карты может незначительно отличаться между настольным компьютером и мобильными клиентами Teams, а также с Teams в браузере настольного компьютера.</span><span class="sxs-lookup"><span data-stu-id="9c8f9-109">Formatting support differs between different card types, and rendering of the card can differ slightly between the desktop and the mobile Teams clients, as well as Teams in the desktop browser.</span></span>

<span data-ttu-id="9c8f9-110">Встроенное изображение можно добавить с помощью любой карточки Teams.</span><span class="sxs-lookup"><span data-stu-id="9c8f9-110">You can include an inline image with any Teams card.</span></span> <span data-ttu-id="9c8f9-111">Изображения в формате "  `.png` ," `.jpg` или " `.gif` файлы" не должны превышать 1024 × 1024 px или 1 МБ.</span><span class="sxs-lookup"><span data-stu-id="9c8f9-111">Images an be formatted as  `.png`, `.jpg`, or `.gif` files and must not exceed 1024 ×1024 px or 1 MB.</span></span> <span data-ttu-id="9c8f9-112">Анимированный GIF-файл не поддерживается официально.</span><span class="sxs-lookup"><span data-stu-id="9c8f9-112">Animated GIF is not officially supported.</span></span> <span data-ttu-id="9c8f9-113">*См* . [Справочник по карточкам](./cards-reference.md#inline-card-images)</span><span class="sxs-lookup"><span data-stu-id="9c8f9-113">*See* [Cards reference](./cards-reference.md#inline-card-images)</span></span>

## <a name="formatting-cards-with-markdown"></a><span data-ttu-id="9c8f9-114">Форматирование карточек с помощью Markdown</span><span class="sxs-lookup"><span data-stu-id="9c8f9-114">Formatting cards with Markdown</span></span>

<span data-ttu-id="9c8f9-115">Существует два типа карточек, поддерживающих Markdown в teams:</span><span class="sxs-lookup"><span data-stu-id="9c8f9-115">There are two card types that support Markdown in Teams:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9c8f9-116">**Адаптивные карты**: Markdown поддерживается в поле адаптивной карточки `Textblock` , а также `Fact.Title` и `Fact.Value` .</span><span class="sxs-lookup"><span data-stu-id="9c8f9-116">**Adaptive Cards**: Markdown is supported in Adaptive Card `Textblock` field, as well as `Fact.Title` and `Fact.Value`.</span></span> <span data-ttu-id="9c8f9-117">HTML не поддерживается в адаптивных картах.</span><span class="sxs-lookup"><span data-stu-id="9c8f9-117">HTML is not supported in adaptive cards.</span></span>
> * <span data-ttu-id="9c8f9-118">**Соединительные карты O365**: Markdown и ограниченный HTML-код поддерживаются в карточках соединителей Office 365 в текстовых полях.</span><span class="sxs-lookup"><span data-stu-id="9c8f9-118">**O365 Connector Cards**: Markdown and limited HTML is supported in Office 365 Connector cards in the text fields.</span></span>

# <a name="markdown-formatting-adaptive-cards"></a>[<span data-ttu-id="9c8f9-119">**Форматирование Markdown: адаптивные карты**</span><span class="sxs-lookup"><span data-stu-id="9c8f9-119">**Markdown formatting: Adaptive Cards**</span></span>](#tab/adaptive-md)

 <span data-ttu-id="9c8f9-120">Поддерживаются следующие стили `Textblock` `Fact.Title` `Fact.Value` :</span><span class="sxs-lookup"><span data-stu-id="9c8f9-120">The supported styles for `Textblock`, `Fact.Title` and `Fact.Value` are:</span></span>

| <span data-ttu-id="9c8f9-121">Style</span><span class="sxs-lookup"><span data-stu-id="9c8f9-121">Style</span></span> | <span data-ttu-id="9c8f9-122">Пример</span><span class="sxs-lookup"><span data-stu-id="9c8f9-122">Example</span></span> | <span data-ttu-id="9c8f9-123">Markdown</span><span class="sxs-lookup"><span data-stu-id="9c8f9-123">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9c8f9-124">bold</span><span class="sxs-lookup"><span data-stu-id="9c8f9-124">bold</span></span> | <span data-ttu-id="9c8f9-125">**Bold**</span><span class="sxs-lookup"><span data-stu-id="9c8f9-125">**Bold**</span></span> | ```**Bold**``` |
| <span data-ttu-id="9c8f9-126">italic</span><span class="sxs-lookup"><span data-stu-id="9c8f9-126">italic</span></span> | <span data-ttu-id="9c8f9-127">_Italic_</span><span class="sxs-lookup"><span data-stu-id="9c8f9-127">_Italic_</span></span> | ```_Italic_``` |
| <span data-ttu-id="9c8f9-128">неупорядоченный список</span><span class="sxs-lookup"><span data-stu-id="9c8f9-128">unordered list</span></span> | <ul><li><span data-ttu-id="9c8f9-129">текст</span><span class="sxs-lookup"><span data-stu-id="9c8f9-129">text</span></span></li><li><span data-ttu-id="9c8f9-130">текст</span><span class="sxs-lookup"><span data-stu-id="9c8f9-130">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="9c8f9-131">упорядоченный список</span><span class="sxs-lookup"><span data-stu-id="9c8f9-131">ordered list</span></span> | <ol><li><span data-ttu-id="9c8f9-132">текст</span><span class="sxs-lookup"><span data-stu-id="9c8f9-132">text</span></span></li><li><span data-ttu-id="9c8f9-133">текст</span><span class="sxs-lookup"><span data-stu-id="9c8f9-133">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="9c8f9-134">Гиперссылки</span><span class="sxs-lookup"><span data-stu-id="9c8f9-134">Hyperlinks</span></span> |[<span data-ttu-id="9c8f9-135">Bing</span><span class="sxs-lookup"><span data-stu-id="9c8f9-135">Bing</span></span>](https://www.bing.com/)| ```[Title](url)``` |

<span data-ttu-id="9c8f9-136">Следующие теги Markdown не поддерживаются:</span><span class="sxs-lookup"><span data-stu-id="9c8f9-136">The following Markdown tags are not supported:</span></span>

* <span data-ttu-id="9c8f9-137">Заголовки</span><span class="sxs-lookup"><span data-stu-id="9c8f9-137">Headers</span></span>
* <span data-ttu-id="9c8f9-138">Таблицы</span><span class="sxs-lookup"><span data-stu-id="9c8f9-138">Tables</span></span>
* <span data-ttu-id="9c8f9-139">Изображения</span><span class="sxs-lookup"><span data-stu-id="9c8f9-139">Images</span></span>
* <span data-ttu-id="9c8f9-140">Предварительно отформатированный текст</span><span class="sxs-lookup"><span data-stu-id="9c8f9-140">Preformatted text</span></span>
* <span data-ttu-id="9c8f9-141">блокккуотес</span><span class="sxs-lookup"><span data-stu-id="9c8f9-141">Blockquotes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9c8f9-142">Адаптивные карты не поддерживают форматирование HTML.</span><span class="sxs-lookup"><span data-stu-id="9c8f9-142">Adaptive cards do not support HTML formatting.</span></span>

### <a name="newlines-for-adaptive-cards"></a><span data-ttu-id="9c8f9-143">Строки для адаптивных карточек</span><span class="sxs-lookup"><span data-stu-id="9c8f9-143">Newlines for Adaptive Cards</span></span>

<span data-ttu-id="9c8f9-144">В списках можно использовать `\r` `\n` последовательности или escape-последовательности для новой строки.</span><span class="sxs-lookup"><span data-stu-id="9c8f9-144">In lists you can use the `\r` or `\n` escape sequences for newlines.</span></span> <span data-ttu-id="9c8f9-145">Использование `\n\n` в списке приводит к тому, что следующий элемент в списке будет иметь отступы.</span><span class="sxs-lookup"><span data-stu-id="9c8f9-145">Using `\n\n` in a list will cause the next element in the list to be indented.</span></span> <span data-ttu-id="9c8f9-146">Если в элементе TextBlock требуются строки новой строки, используйте `\n\n` .</span><span class="sxs-lookup"><span data-stu-id="9c8f9-146">If you need newlines elsewhere in the textblock, use `\n\n`.</span></span>

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a><span data-ttu-id="9c8f9-147">Различия между мобильными и настольными компьютерами для адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="9c8f9-147">Mobile and desktop differences for Adaptive Cards</span></span>

<span data-ttu-id="9c8f9-148">Форматирование слегка отличается между настольными и мобильными версиями Teams.</span><span class="sxs-lookup"><span data-stu-id="9c8f9-148">Formatting is slightly different between the desktop and the mobile versions of Teams.</span></span>

<span data-ttu-id="9c8f9-149">На рабочем столе Адаптивное форматирование карточки Markdown выглядит так же, как в веб-браузерах и в клиентском приложении teams:</span><span class="sxs-lookup"><span data-stu-id="9c8f9-149">On the desktop, Adaptive Card Markdown formatting appears like this in both web browsers and in the Teams client application:</span></span>

![Адаптивное форматирование карточки Markdown в клиенте для настольных ПК](../../assets/images/cards/Adaptive-markdown-desktop-client.png)

<span data-ttu-id="9c8f9-151">В iOS форматирование адаптивной карточки Markdown выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9c8f9-151">On iOS, Adaptive Card Markdown formatting appears like this:</span></span>

![Адаптивное форматирование карточки Markdown в iOS](../../assets/images/cards/Adaptive-markdown-iOS-75.png)

<span data-ttu-id="9c8f9-153">В Android Адаптивное форматирование карточки Markdown выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9c8f9-153">On Android, Adaptive Card Markdown formatting appears like this:</span></span>

![Адаптивное форматирование карточки Markdown в Android](../../assets/images/cards/Adaptive-markdown-Android.png)

### <a name="more-information-on-adaptive-cards"></a><span data-ttu-id="9c8f9-155">Дополнительные сведения о адаптивных картах</span><span class="sxs-lookup"><span data-stu-id="9c8f9-155">More information on Adaptive Cards</span></span>

<span data-ttu-id="9c8f9-156">[Функции для текста в адаптивных карточках](/adaptive-cards/create/textfeatures) Функции даты и локализации, упомянутые в этом разделе, не поддерживаются в Teams.</span><span class="sxs-lookup"><span data-stu-id="9c8f9-156">[Text features in Adaptive cards](/adaptive-cards/create/textfeatures) The date and localization features mentioned in this topic are not supported in Teams.</span></span>

### <a name="formatting-sample-for-adaptive-cards"></a><span data-ttu-id="9c8f9-157">Пример форматирования для адаптивных карточек</span><span class="sxs-lookup"><span data-stu-id="9c8f9-157">Formatting sample for Adaptive cards</span></span>

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

### <a name="mention-support-within-adaptive-cards-v12"></a><span data-ttu-id="9c8f9-158">Упоминание поддержки в адаптивных картах версии 1.2</span><span class="sxs-lookup"><span data-stu-id="9c8f9-158">Mention support within Adaptive cards v1.2</span></span>

<span data-ttu-id="9c8f9-159">Упоминания на основе карточек поддерживаются в веб-, настольных и мобильных клиентах.</span><span class="sxs-lookup"><span data-stu-id="9c8f9-159">Card based mentions are supported in Web, Desktop and mobile clients.</span></span> <span data-ttu-id="9c8f9-160">Вы можете добавлять @ упоминания в тексте адаптивной карточки для Боты и расширений обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="9c8f9-160">You can add @ mentions within an adaptive card body for bots and messaging extension responses.</span></span>  <span data-ttu-id="9c8f9-161">Чтобы добавить @ упоминания в карточки, следуйте той же логике уведомлений и отрисовки, что и [в упомянутых сообщениях в беседах канала и группового чата](../../bots/how-to/conversations/channel-and-group-conversations.md#working-with-mentions ).</span><span class="sxs-lookup"><span data-stu-id="9c8f9-161">To add @ mentions in cards, follow the same notification logic and rendering as that of message based [mentions in channel and group chat conversations](../../bots/how-to/conversations/channel-and-group-conversations.md#working-with-mentions ).</span></span>

<span data-ttu-id="9c8f9-162">Расширения Боты и обмена сообщениями могут включать упоминание в содержимом карточки в элементах [TextBlock](https://adaptivecards.io/explorer/TextBlock.html) и в элементах [фактов](https://adaptivecards.io/explorer/FactSet.html) .</span><span class="sxs-lookup"><span data-stu-id="9c8f9-162">Bots and messaging extensions can include mentions within the card content in [TextBlock](https://adaptivecards.io/explorer/TextBlock.html) and [FactSet](https://adaptivecards.io/explorer/FactSet.html) elements.</span></span>

> [!NOTE]
> * <span data-ttu-id="9c8f9-163">В настоящее время [элементы мультимедиа](https://adaptivecards.io/explorer/Media.html) в настоящее время не поддерживаются в адаптивных картах версии 1.2 на платформе Teams.</span><span class="sxs-lookup"><span data-stu-id="9c8f9-163">[Media elements](https://adaptivecards.io/explorer/Media.html) are currently not supported in Adaptive cards v1.2 on the Teams platform.</span></span>
> * <span data-ttu-id="9c8f9-164">Упоминание каналов & участников группы не поддерживаются в сообщениях Bot.</span><span class="sxs-lookup"><span data-stu-id="9c8f9-164">Channel & Team mentions are not supported in bot messages.</span></span>

### <a name="constructing-mentions"></a><span data-ttu-id="9c8f9-165">Создание упоминаний</span><span class="sxs-lookup"><span data-stu-id="9c8f9-165">Constructing mentions</span></span>

<span data-ttu-id="9c8f9-166">Чтобы включить в адаптивную карточку упоминание, необходимо, чтобы приложение включало следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="9c8f9-166">To include a mention in an Adaptive Card your app needs to include the following elements</span></span>

* <span data-ttu-id="9c8f9-167">`<at>username</at>` в поддерживаемых элементах адаптивной карточки</span><span class="sxs-lookup"><span data-stu-id="9c8f9-167">`<at>username</at>` in the supported adaptive card elements</span></span>
* <span data-ttu-id="9c8f9-168">`mention`Объект внутри `msteams` свойства в содержимом карточки, включающий идентификатор пользователя Teams для указанного пользователя.</span><span class="sxs-lookup"><span data-stu-id="9c8f9-168">The `mention` object inside of an `msteams` property in the card content, which includes the Teams user id of the user being mentioned</span></span>

### <a name="sample-adaptive-card-with-a-mention"></a><span data-ttu-id="9c8f9-169">Пример адаптивной карточки с упоминанием</span><span class="sxs-lookup"><span data-stu-id="9c8f9-169">Sample Adaptive card with a mention</span></span>

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

# <a name="markdown-formatting-o365-connector-cards"></a>[<span data-ttu-id="9c8f9-170">**Форматирование Markdown: карты соединителей O365**</span><span class="sxs-lookup"><span data-stu-id="9c8f9-170">**Markdown formatting: O365 Connector Cards**</span></span>](#tab/connector-md)

<span data-ttu-id="9c8f9-171">Карты соединителей поддерживают ограниченные Markdown и форматирование HTML.</span><span class="sxs-lookup"><span data-stu-id="9c8f9-171">Connector cards support limited Markdown and HTML formatting.</span></span> <span data-ttu-id="9c8f9-172">Поддержка HTML описана в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="9c8f9-172">HTML support is described in the last section.</span></span>

| <span data-ttu-id="9c8f9-173">Style</span><span class="sxs-lookup"><span data-stu-id="9c8f9-173">Style</span></span> | <span data-ttu-id="9c8f9-174">Пример</span><span class="sxs-lookup"><span data-stu-id="9c8f9-174">Example</span></span> | <span data-ttu-id="9c8f9-175">Markdown</span><span class="sxs-lookup"><span data-stu-id="9c8f9-175">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9c8f9-176">bold</span><span class="sxs-lookup"><span data-stu-id="9c8f9-176">bold</span></span> | <span data-ttu-id="9c8f9-177">**text**</span><span class="sxs-lookup"><span data-stu-id="9c8f9-177">**text**</span></span> | `**text**` |
| <span data-ttu-id="9c8f9-178">italic</span><span class="sxs-lookup"><span data-stu-id="9c8f9-178">italic</span></span> | <span data-ttu-id="9c8f9-179">*text*</span><span class="sxs-lookup"><span data-stu-id="9c8f9-179">*text*</span></span> | `*text*` |
| <span data-ttu-id="9c8f9-180">Верхний колонтитул (уровни 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="9c8f9-180">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="9c8f9-181">**Text**</span><span class="sxs-lookup"><span data-stu-id="9c8f9-181">**Text**</span></span> | `### Text`|
| <span data-ttu-id="9c8f9-182">strikethrough</span><span class="sxs-lookup"><span data-stu-id="9c8f9-182">strikethrough</span></span> | <span data-ttu-id="9c8f9-183">~~text~~</span><span class="sxs-lookup"><span data-stu-id="9c8f9-183">~~text~~</span></span> | `~~text~~` |
| <span data-ttu-id="9c8f9-184">неупорядоченный список</span><span class="sxs-lookup"><span data-stu-id="9c8f9-184">unordered list</span></span> | <ul><li><span data-ttu-id="9c8f9-185">текст</span><span class="sxs-lookup"><span data-stu-id="9c8f9-185">text</span></span></li><li><span data-ttu-id="9c8f9-186">текст</span><span class="sxs-lookup"><span data-stu-id="9c8f9-186">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="9c8f9-187">упорядоченный список</span><span class="sxs-lookup"><span data-stu-id="9c8f9-187">ordered list</span></span> | <ol><li><span data-ttu-id="9c8f9-188">текст</span><span class="sxs-lookup"><span data-stu-id="9c8f9-188">text</span></span></li><li><span data-ttu-id="9c8f9-189">текст</span><span class="sxs-lookup"><span data-stu-id="9c8f9-189">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="9c8f9-190">предварительно отформатированный текст</span><span class="sxs-lookup"><span data-stu-id="9c8f9-190">preformatted text</span></span> | `text` | ``preformatted text`` |
| <span data-ttu-id="9c8f9-191">blockquote</span><span class="sxs-lookup"><span data-stu-id="9c8f9-191">blockquote</span></span> | <span data-ttu-id="9c8f9-192">>текст блокккуоте</span><span class="sxs-lookup"><span data-stu-id="9c8f9-192">>blockquote text</span></span> | `>blockquote text` |
| <span data-ttu-id="9c8f9-193">гиперссылка</span><span class="sxs-lookup"><span data-stu-id="9c8f9-193">hyperlink</span></span> | [<span data-ttu-id="9c8f9-194">Bing</span><span class="sxs-lookup"><span data-stu-id="9c8f9-194">Bing</span></span>](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| <span data-ttu-id="9c8f9-195">Ссылка на изображение</span><span class="sxs-lookup"><span data-stu-id="9c8f9-195">image link</span></span> |![Дукк на рок](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

<span data-ttu-id="9c8f9-197">В соединителях соединителей отображаются строки `\n\n` , но не for `\n` или `\r` .</span><span class="sxs-lookup"><span data-stu-id="9c8f9-197">In connector cards, newlines are rendered for `\n\n`, but not for `\n` or `\r`.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-markdown"></a><span data-ttu-id="9c8f9-198">Различия между мобильными и рабочими столами для соединителей карт с помощью Markdown</span><span class="sxs-lookup"><span data-stu-id="9c8f9-198">Mobile and desktop differences for connector cards using Markdown</span></span>

<span data-ttu-id="9c8f9-199">На рабочем столе Markdown форматирование карт для соединителей выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9c8f9-199">On the desktop, Markdown formatting for connector cards looks like this:</span></span>

![Markdown форматирование карт подключателя в клиенте для настольных ПК](../../assets/images/cards/connector-desktop-markdown-combined.png)

<span data-ttu-id="9c8f9-201">В iOS форматирование Markdown для карт подключателя выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9c8f9-201">On iOS, Markdown formatting for connector cards looks like this:</span></span>

![Markdown форматирование карт подключателя в клиенте iOS](../../assets/images/cards/connector-iphone-markdown-combined-80.png)

<span data-ttu-id="9c8f9-203">Вопросы:</span><span class="sxs-lookup"><span data-stu-id="9c8f9-203">Issues:</span></span>

* <span data-ttu-id="9c8f9-204">Клиент iOS для Teams не отображает Markdown или встроенные изображения HTML в соединительных картах.</span><span class="sxs-lookup"><span data-stu-id="9c8f9-204">The iOS client for Teams does not render Markdown or HTML inline images in Connector Cards.</span></span>
* <span data-ttu-id="9c8f9-205">Блокккуотес отображаются с отступом, но без серого фона.</span><span class="sxs-lookup"><span data-stu-id="9c8f9-205">Blockquotes are rendered as indented but without a gray background.</span></span>

<span data-ttu-id="9c8f9-206">На Android Markdown форматирование карт для соединителей выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9c8f9-206">On Android, Markdown formatting for connector cards looks like this:</span></span>

![Markdown форматирование карт подключателя в клиенте Android](../../assets/images/cards/connector-android-markdown-combined.png)

### <a name="formatting-example-for-markdown-connector-cards"></a><span data-ttu-id="9c8f9-208">Пример форматирования для карточек соединителей Markdown</span><span class="sxs-lookup"><span data-stu-id="9c8f9-208">Formatting example for Markdown Connector Cards</span></span>

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

## <a name="formatting-cards-with-html"></a><span data-ttu-id="9c8f9-209">Форматирование карточек с помощью HTML</span><span class="sxs-lookup"><span data-stu-id="9c8f9-209">Formatting cards with HTML</span></span>

# <a name="html-formatting-o365-connector-cards"></a>[<span data-ttu-id="9c8f9-210">**Форматирование HTML: карты соединителей O365**</span><span class="sxs-lookup"><span data-stu-id="9c8f9-210">**HTML formatting: O365 Connector Cards**</span></span>](#tab/connector-html)

<span data-ttu-id="9c8f9-211">Карты соединителей поддерживают ограниченные Markdown и форматирование HTML.</span><span class="sxs-lookup"><span data-stu-id="9c8f9-211">Connector cards support limited Markdown and HTML formatting.</span></span> <span data-ttu-id="9c8f9-212">Markdown описывается в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="9c8f9-212">Markdown is described in the next section.</span></span>

| <span data-ttu-id="9c8f9-213">Style</span><span class="sxs-lookup"><span data-stu-id="9c8f9-213">Style</span></span> | <span data-ttu-id="9c8f9-214">Пример</span><span class="sxs-lookup"><span data-stu-id="9c8f9-214">Example</span></span> | <span data-ttu-id="9c8f9-215">HTML</span><span class="sxs-lookup"><span data-stu-id="9c8f9-215">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9c8f9-216">bold</span><span class="sxs-lookup"><span data-stu-id="9c8f9-216">bold</span></span> | <span data-ttu-id="9c8f9-217">**text**</span><span class="sxs-lookup"><span data-stu-id="9c8f9-217">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="9c8f9-218">italic</span><span class="sxs-lookup"><span data-stu-id="9c8f9-218">italic</span></span> | <span data-ttu-id="9c8f9-219">*text*</span><span class="sxs-lookup"><span data-stu-id="9c8f9-219">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="9c8f9-220">Верхний колонтитул (уровни 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="9c8f9-220">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="9c8f9-221">**Text**</span><span class="sxs-lookup"><span data-stu-id="9c8f9-221">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="9c8f9-222">strikethrough</span><span class="sxs-lookup"><span data-stu-id="9c8f9-222">strikethrough</span></span> | <span data-ttu-id="9c8f9-223">~~text~~</span><span class="sxs-lookup"><span data-stu-id="9c8f9-223">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="9c8f9-224">неупорядоченный список</span><span class="sxs-lookup"><span data-stu-id="9c8f9-224">unordered list</span></span> | <ul><li><span data-ttu-id="9c8f9-225">текст</span><span class="sxs-lookup"><span data-stu-id="9c8f9-225">text</span></span></li><li><span data-ttu-id="9c8f9-226">текст</span><span class="sxs-lookup"><span data-stu-id="9c8f9-226">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="9c8f9-227">упорядоченный список</span><span class="sxs-lookup"><span data-stu-id="9c8f9-227">ordered list</span></span> | <ol><li><span data-ttu-id="9c8f9-228">текст</span><span class="sxs-lookup"><span data-stu-id="9c8f9-228">text</span></span></li><li><span data-ttu-id="9c8f9-229">текст</span><span class="sxs-lookup"><span data-stu-id="9c8f9-229">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="9c8f9-230">предварительно отформатированный текст</span><span class="sxs-lookup"><span data-stu-id="9c8f9-230">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="9c8f9-231">blockquote</span><span class="sxs-lookup"><span data-stu-id="9c8f9-231">blockquote</span></span> | <blockquote><span data-ttu-id="9c8f9-232">текст</span><span class="sxs-lookup"><span data-stu-id="9c8f9-232">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="9c8f9-233">гиперссылка</span><span class="sxs-lookup"><span data-stu-id="9c8f9-233">hyperlink</span></span> | [<span data-ttu-id="9c8f9-234">Bing</span><span class="sxs-lookup"><span data-stu-id="9c8f9-234">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="9c8f9-235">Ссылка на изображение</span><span class="sxs-lookup"><span data-stu-id="9c8f9-235">image link</span></span> | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

<span data-ttu-id="9c8f9-236">В соединительных карточках строки новой строки отображаются в HTML-коде с помощью `<p>` тега.</span><span class="sxs-lookup"><span data-stu-id="9c8f9-236">In connector cards, newlines are rendered in HTML using the `<p>` tag.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-html"></a><span data-ttu-id="9c8f9-237">Различия между мобильными и рабочими столами для соединителей карт с помощью HTML</span><span class="sxs-lookup"><span data-stu-id="9c8f9-237">Mobile and desktop differences for connector cards using HTML</span></span>

<span data-ttu-id="9c8f9-238">На рабочем столе форматирование HTML-карт для соединителей выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9c8f9-238">On the desktop, HTML formatting for connector cards looks like this:</span></span>

![Формат HTML для соединителей карт в клиенте для настольных ПК](../../assets/images/cards/Connector-desktop-html-combined.png)

<span data-ttu-id="9c8f9-240">В iOS форматирование HTML выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9c8f9-240">On iOS, HTML formatting looks like this:</span></span>

![Формат HTML для соединителей карт в клиенте iOS](../../assets/images/cards/connector-iphone-html-combined-80.png)

<span data-ttu-id="9c8f9-242">Вопросы:</span><span class="sxs-lookup"><span data-stu-id="9c8f9-242">Issues:</span></span>

* <span data-ttu-id="9c8f9-243">Встроенные изображения не отправляются на iOS с помощью Markdown или HTML в соединительных карточках.</span><span class="sxs-lookup"><span data-stu-id="9c8f9-243">Inline images are not rendered on iOS using either Markdown or HTML in Connector Cards.</span></span>
* <span data-ttu-id="9c8f9-244">Предварительно отформатированный текст отображается, но не является серым фоном.</span><span class="sxs-lookup"><span data-stu-id="9c8f9-244">Preformatted text is rendered but does not have a gray background.</span></span>

<span data-ttu-id="9c8f9-245">На Android форматирование HTML выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9c8f9-245">On Android, HTML formatting looks like this:</span></span>

![Форматирование HTML-карт для соединителей в клиенте Android](../../assets/images/cards/connector-android-html-combined.png)

### <a name="formatting-sample-for-html-connector-cards"></a><span data-ttu-id="9c8f9-247">Пример форматирования для карточек соединителей HTML</span><span class="sxs-lookup"><span data-stu-id="9c8f9-247">Formatting sample for HTML Connector Cards</span></span>

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

# <a name="html-formatting-hero-and-thumbnail-cards"></a>[<span data-ttu-id="9c8f9-248">**HTML-форматирование: карточки главный Имиджевый баннер и эскиза**</span><span class="sxs-lookup"><span data-stu-id="9c8f9-248">**HTML Formatting: hero and thumbnail cards**</span></span>](#tab/simple-html)

<span data-ttu-id="9c8f9-249">Теги HTML поддерживаются для простых карточек, таких как карта главный Имиджевый баннер и эскиза.</span><span class="sxs-lookup"><span data-stu-id="9c8f9-249">HTML tags are supported for simple cards such as the hero and thumbnail card.</span></span> <span data-ttu-id="9c8f9-250">Markdown не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="9c8f9-250">Markdown is not supported.</span></span>

| <span data-ttu-id="9c8f9-251">Style</span><span class="sxs-lookup"><span data-stu-id="9c8f9-251">Style</span></span> | <span data-ttu-id="9c8f9-252">Пример</span><span class="sxs-lookup"><span data-stu-id="9c8f9-252">Example</span></span> | <span data-ttu-id="9c8f9-253">HTML</span><span class="sxs-lookup"><span data-stu-id="9c8f9-253">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9c8f9-254">bold</span><span class="sxs-lookup"><span data-stu-id="9c8f9-254">bold</span></span> | <span data-ttu-id="9c8f9-255">**text**</span><span class="sxs-lookup"><span data-stu-id="9c8f9-255">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="9c8f9-256">italic</span><span class="sxs-lookup"><span data-stu-id="9c8f9-256">italic</span></span> | <span data-ttu-id="9c8f9-257">*text*</span><span class="sxs-lookup"><span data-stu-id="9c8f9-257">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="9c8f9-258">Верхний колонтитул (уровни 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="9c8f9-258">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="9c8f9-259">**Text**</span><span class="sxs-lookup"><span data-stu-id="9c8f9-259">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="9c8f9-260">strikethrough</span><span class="sxs-lookup"><span data-stu-id="9c8f9-260">strikethrough</span></span> | <span data-ttu-id="9c8f9-261">~~text~~</span><span class="sxs-lookup"><span data-stu-id="9c8f9-261">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="9c8f9-262">неупорядоченный список</span><span class="sxs-lookup"><span data-stu-id="9c8f9-262">unordered list</span></span> | <ul><li><span data-ttu-id="9c8f9-263">текст</span><span class="sxs-lookup"><span data-stu-id="9c8f9-263">text</span></span></li><li><span data-ttu-id="9c8f9-264">текст</span><span class="sxs-lookup"><span data-stu-id="9c8f9-264">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="9c8f9-265">упорядоченный список</span><span class="sxs-lookup"><span data-stu-id="9c8f9-265">ordered list</span></span> | <ol><li><span data-ttu-id="9c8f9-266">текст</span><span class="sxs-lookup"><span data-stu-id="9c8f9-266">text</span></span></li><li><span data-ttu-id="9c8f9-267">текст</span><span class="sxs-lookup"><span data-stu-id="9c8f9-267">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="9c8f9-268">предварительно отформатированный текст</span><span class="sxs-lookup"><span data-stu-id="9c8f9-268">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="9c8f9-269">blockquote</span><span class="sxs-lookup"><span data-stu-id="9c8f9-269">blockquote</span></span> | <blockquote><span data-ttu-id="9c8f9-270">текст</span><span class="sxs-lookup"><span data-stu-id="9c8f9-270">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="9c8f9-271">гиперссылка</span><span class="sxs-lookup"><span data-stu-id="9c8f9-271">hyperlink</span></span> | [<span data-ttu-id="9c8f9-272">Bing</span><span class="sxs-lookup"><span data-stu-id="9c8f9-272">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="9c8f9-273">Ссылка на изображение</span><span class="sxs-lookup"><span data-stu-id="9c8f9-273">image link</span></span> |<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a><span data-ttu-id="9c8f9-274">Различия между мобильными и рабочими столами для простых карточек</span><span class="sxs-lookup"><span data-stu-id="9c8f9-274">Mobile and desktop differences for simple cards</span></span>

<span data-ttu-id="9c8f9-275">Из-за различий в разрешениях между настольными и мобильными платформами форматирование различается для настольных ПК и мобильных версий Teams.</span><span class="sxs-lookup"><span data-stu-id="9c8f9-275">Because of resolution differences between the desktop and mobile platform, formatting is different between the desktop and the mobile version of Teams.</span></span>

<span data-ttu-id="9c8f9-276">На настольном компьютере форматирование HTML выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9c8f9-276">On the desktop, HTML formatting appears like this:</span></span>

![Форматирование HTML в клиенте для настольных ПК](../../assets/images/cards/card-formatting-xml-desktop-v2.png)

<span data-ttu-id="9c8f9-278">В iOS форматирование HTML выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9c8f9-278">On iOS, HTML formatting appears like this:</span></span>

![Форматирование HTML в клиенте iOS](../../assets/images/cards/card-formatting-xml-mobile-v2.png)

<span data-ttu-id="9c8f9-280">Вопросы:</span><span class="sxs-lookup"><span data-stu-id="9c8f9-280">Issues:</span></span>

* <span data-ttu-id="9c8f9-281">Форматирование символов, например полужирный шрифт и курсив, не отображается в iOS.</span><span class="sxs-lookup"><span data-stu-id="9c8f9-281">Character formatting like bold and italic are not rendered on iOS.</span></span>

<span data-ttu-id="9c8f9-282">На Android форматирование HTML выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9c8f9-282">On Android, HTML formatting appears like this:</span></span>

![Форматирование HTML в клиенте Android](../../assets/images/cards/card-formatting-xml-android-60.png)

<span data-ttu-id="9c8f9-284">Правильное форматирование знаков, как полужирное и курсивное отображение на Android.</span><span class="sxs-lookup"><span data-stu-id="9c8f9-284">Character formatting like bold and italic display correctly on Android.</span></span>

### <a name="formatting-sample-for-html-formatting-in-simple-cards"></a><span data-ttu-id="9c8f9-285">Пример форматирования форматирования HTML на простых карточках</span><span class="sxs-lookup"><span data-stu-id="9c8f9-285">Formatting sample for HTML formatting in simple cards</span></span>

<span data-ttu-id="9c8f9-286">Эти снимки создаются с помощью Teams Аппстудио, где для свойства Text карточки главный Имиджевый баннер задано значение, равное следующей строке.</span><span class="sxs-lookup"><span data-stu-id="9c8f9-286">These screenshots were created using Teams AppStudio, where the text property of a hero card was set to the following string.</span></span> <span data-ttu-id="9c8f9-287">Вы можете проверить форматирование в собственных карточках, изменив этот код.</span><span class="sxs-lookup"><span data-stu-id="9c8f9-287">You can test formatting in your own cards by modifying this code.</span></span>

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"https://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`

---
