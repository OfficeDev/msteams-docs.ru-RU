---
title: Форматирование текста в карточках
description: Описание форматирования текста карточки в Microsoft Teams
keywords: формат карточек Боты Teams
ms.date: 03/29/2018
ms.openlocfilehash: eb8aa13b9e75d08dadd5e615029a9d418c6c7892
ms.sourcegitcommit: 44ac886c0ca34a16222d3991a61606f8483b8481
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/05/2020
ms.locfileid: "41783971"
---
# <a name="card-formatting"></a><span data-ttu-id="c08c8-104">Форматирование карточки</span><span class="sxs-lookup"><span data-stu-id="c08c8-104">Card formatting</span></span>

<span data-ttu-id="c08c8-105">В зависимости от типа карты в карточки можно добавлять форматированный текст в карточки с помощью Markdown или HTML.</span><span class="sxs-lookup"><span data-stu-id="c08c8-105">You can add rich text formatting to your cards using either markdown or HTML, depending on the card type.</span></span>

<span data-ttu-id="c08c8-106">Карточки поддерживают форматирование только в свойстве Text, а не в свойствах Title и субтитров.</span><span class="sxs-lookup"><span data-stu-id="c08c8-106">Cards support formatting in the text property only, not in the title or subtitle properties.</span></span> <span data-ttu-id="c08c8-107">Форматирование можно указать с помощью подмножества форматирования XML (HTML) или Markdown в зависимости от типа карты.</span><span class="sxs-lookup"><span data-stu-id="c08c8-107">Formatting can be specified using a subset of XML (HTML) formatting, or Markdown depending on card type.</span></span> <span data-ttu-id="c08c8-108">Для текущих приложений AMD в будущем рекомендуется использовать форматирование Markdown.</span><span class="sxs-lookup"><span data-stu-id="c08c8-108">For current amd future development Adaptive cards using markdown formatting is recommended.</span></span>

<span data-ttu-id="c08c8-109">Поддержка форматирования различается для разных типов карточек, а отображение карты может незначительно отличаться между настольным компьютером и мобильными клиентами Teams, а также с Teams в браузере настольного компьютера.</span><span class="sxs-lookup"><span data-stu-id="c08c8-109">Formatting support differs between different card types, and rendering of the card can differ slightly between the desktop and the mobile Teams clients, as well as Teams in the desktop browser.</span></span>

## <a name="card-types"></a><span data-ttu-id="c08c8-110">Типы карточек</span><span class="sxs-lookup"><span data-stu-id="c08c8-110">Card types</span></span>

<span data-ttu-id="c08c8-111">Существует три типа карт, поддерживающих Markdown в teams:</span><span class="sxs-lookup"><span data-stu-id="c08c8-111">There are three types of cards that support Markdown in Teams:</span></span>

* <span data-ttu-id="c08c8-112">**Адаптивные карты**: Markdown поддерживается в поле адаптивной карточки `Textblock` , а также `Fact.Title` и `Fact.Value`.</span><span class="sxs-lookup"><span data-stu-id="c08c8-112">**Adaptive Cards**: Markdown is supported in Adaptive Card `Textblock` field, as well as `Fact.Title` and `Fact.Value`.</span></span> <span data-ttu-id="c08c8-113">HTML не поддерживается в адаптивных картах.</span><span class="sxs-lookup"><span data-stu-id="c08c8-113">HTML is not supported in adaptive cards.</span></span>
* <span data-ttu-id="c08c8-114">**Соединительные карты O365**: Markdown и ограниченный HTML-код поддерживаются в карточках соединителей Office 365 в текстовых полях.</span><span class="sxs-lookup"><span data-stu-id="c08c8-114">**O365 Connector Cards**: Markdown and limited HTML is supported in Office 365 Connector cards in the text fields.</span></span>
* <span data-ttu-id="c08c8-115">**Простые карты**: ограниченный HTML-код поддерживается, но Markdown не поддерживается на простых карточках.</span><span class="sxs-lookup"><span data-stu-id="c08c8-115">**Simple Cards**: Limited HTML is supported, but markdown is not supported in simple cards.</span></span>

## <a name="markdown-formatting-for-adaptive-cards"></a><span data-ttu-id="c08c8-116">Markdown форматирование для адаптивных карточек</span><span class="sxs-lookup"><span data-stu-id="c08c8-116">Markdown formatting for Adaptive Cards</span></span>

 <span data-ttu-id="c08c8-117">Поддерживаются следующие стили `Textblock` `Fact.Title` `Fact.Value` :</span><span class="sxs-lookup"><span data-stu-id="c08c8-117">The supported styles for `Textblock`, `Fact.Title` and `Fact.Value` are:</span></span>

| <span data-ttu-id="c08c8-118">Стиль</span><span class="sxs-lookup"><span data-stu-id="c08c8-118">Style</span></span> | <span data-ttu-id="c08c8-119">Пример</span><span class="sxs-lookup"><span data-stu-id="c08c8-119">Example</span></span> | <span data-ttu-id="c08c8-120">Markdown</span><span class="sxs-lookup"><span data-stu-id="c08c8-120">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c08c8-121">bold</span><span class="sxs-lookup"><span data-stu-id="c08c8-121">bold</span></span> | <span data-ttu-id="c08c8-122">**Bold**</span><span class="sxs-lookup"><span data-stu-id="c08c8-122">**Bold**</span></span> | ```**Bold**``` |
| <span data-ttu-id="c08c8-123">italic</span><span class="sxs-lookup"><span data-stu-id="c08c8-123">italic</span></span> | <span data-ttu-id="c08c8-124">_Italic_</span><span class="sxs-lookup"><span data-stu-id="c08c8-124">_Italic_</span></span> | ```_Italic_``` |
| <span data-ttu-id="c08c8-125">неупорядоченный список</span><span class="sxs-lookup"><span data-stu-id="c08c8-125">unordered list</span></span> | <ul><li><span data-ttu-id="c08c8-126">текст</span><span class="sxs-lookup"><span data-stu-id="c08c8-126">text</span></span></li><li><span data-ttu-id="c08c8-127">текст</span><span class="sxs-lookup"><span data-stu-id="c08c8-127">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="c08c8-128">упорядоченный список</span><span class="sxs-lookup"><span data-stu-id="c08c8-128">ordered list</span></span> | <ol><li><span data-ttu-id="c08c8-129">текст</span><span class="sxs-lookup"><span data-stu-id="c08c8-129">text</span></span></li><li><span data-ttu-id="c08c8-130">текст</span><span class="sxs-lookup"><span data-stu-id="c08c8-130">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="c08c8-131">Гиперссылки</span><span class="sxs-lookup"><span data-stu-id="c08c8-131">Hyperlinks</span></span> |[<span data-ttu-id="c08c8-132">Bing</span><span class="sxs-lookup"><span data-stu-id="c08c8-132">Bing</span></span>](https://www.bing.com/)| ```[Title](url)``` |

<span data-ttu-id="c08c8-133">Следующие теги Markdown не поддерживаются:</span><span class="sxs-lookup"><span data-stu-id="c08c8-133">The following markdown tags are not supported:</span></span>

* <span data-ttu-id="c08c8-134">Заголовки</span><span class="sxs-lookup"><span data-stu-id="c08c8-134">Headers</span></span>
* <span data-ttu-id="c08c8-135">Таблицы</span><span class="sxs-lookup"><span data-stu-id="c08c8-135">Tables</span></span>
* <span data-ttu-id="c08c8-136">Изображения</span><span class="sxs-lookup"><span data-stu-id="c08c8-136">Images</span></span>
* <span data-ttu-id="c08c8-137">Предварительно отформатированный текст</span><span class="sxs-lookup"><span data-stu-id="c08c8-137">Preformatted text</span></span>
* <span data-ttu-id="c08c8-138">блокккуотес</span><span class="sxs-lookup"><span data-stu-id="c08c8-138">Blockquotes</span></span>

<span data-ttu-id="c08c8-139">Адаптивные карточки не поддерживают форматирование HTML.</span><span class="sxs-lookup"><span data-stu-id="c08c8-139">Adaptive cards do not support any HTML formatting.</span></span>

### <a name="newlines-for-adaptive-cards"></a><span data-ttu-id="c08c8-140">Строки для адаптивных карточек</span><span class="sxs-lookup"><span data-stu-id="c08c8-140">Newlines for Adaptive Cards</span></span>

<span data-ttu-id="c08c8-141">В списках можно использовать последовательности `\r` или `\n` escape-последовательности для новой строки.</span><span class="sxs-lookup"><span data-stu-id="c08c8-141">In lists you can use the `\r` or `\n` escape sequences for newlines.</span></span> <span data-ttu-id="c08c8-142">Использование `\n\n` в списке приводит к тому, что следующий элемент в списке будет иметь отступы.</span><span class="sxs-lookup"><span data-stu-id="c08c8-142">Using `\n\n` in a list will cause the next element in the list to be indented.</span></span> <span data-ttu-id="c08c8-143">Если в элементе TextBlock требуются строки новой строки, используйте `\n\n`.</span><span class="sxs-lookup"><span data-stu-id="c08c8-143">If you need newlines elsewhere in the textblock, use `\n\n`.</span></span>

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a><span data-ttu-id="c08c8-144">Различия между мобильными и настольными компьютерами для адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="c08c8-144">Mobile and desktop differences for Adaptive Cards</span></span>

<span data-ttu-id="c08c8-145">Форматирование слегка отличается между настольными и мобильными версиями Teams.</span><span class="sxs-lookup"><span data-stu-id="c08c8-145">Formatting is slightly different between the desktop and the mobile versions of Teams.</span></span>

<span data-ttu-id="c08c8-146">На рабочем столе Адаптивное форматирование карточки Markdown выглядит так же, как в веб-браузерах и в клиентском приложении teams:</span><span class="sxs-lookup"><span data-stu-id="c08c8-146">On the desktop, Adaptive Card markdown formatting appears like this in both web browsers and in the Teams client application:</span></span>

![Адаптивное форматирование карточки Markdown в клиенте для настольных ПК](~/assets/images/cards/Adaptive-markdown-desktop-client.png)

<span data-ttu-id="c08c8-148">В iOS форматирование адаптивной карточки Markdown выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c08c8-148">On iOS, Adaptive Card markdown formatting appears like this:</span></span>

![Адаптивное форматирование карточки Markdown в iOS](~/assets/images/cards/Adaptive-markdown-iOS-75.png)

<span data-ttu-id="c08c8-150">В Android Адаптивное форматирование карточки Markdown выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c08c8-150">On Android, Adaptive Card markdown formatting appears like this:</span></span>

![Адаптивное форматирование карточки Markdown в Android](~/assets/images/cards/Adaptive-markdown-Android.png)

### <a name="for-more-information-on-adaptive-cards"></a><span data-ttu-id="c08c8-152">Дополнительные сведения о адаптивных картах</span><span class="sxs-lookup"><span data-stu-id="c08c8-152">For more information on Adaptive Cards</span></span>

<span data-ttu-id="c08c8-153">[Функции для текста в адаптивных карточках](/adaptive-cards/create/textfeatures) Функции даты и локализации, упомянутые в этом разделе, не поддерживаются в Teams.</span><span class="sxs-lookup"><span data-stu-id="c08c8-153">[Text features in Adaptive cards](/adaptive-cards/create/textfeatures) The date and localization features mentioned in this topic are not supported in Teams.</span></span>

### <a name="formatting-sample-for-adaptive-cards"></a><span data-ttu-id="c08c8-154">Пример форматирования для адаптивных карточек</span><span class="sxs-lookup"><span data-stu-id="c08c8-154">Formatting sample for Adaptive cards</span></span>

``` json
{
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
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
            "text": "Check out [Adaptive Cards](http://adaptivecards.io)"
        }
    ]
}
```

## <a name="mention-support-within-adaptive-cards"></a><span data-ttu-id="c08c8-155">Упоминание поддержки в адаптивных картах</span><span class="sxs-lookup"><span data-stu-id="c08c8-155">Mention support within Adaptive cards</span></span> 

> [!NOTE]
> <span data-ttu-id="c08c8-156">Упоминание поддержки в карточках в настоящее время поддерживается только в [режиме предварительного просмотра разработчика](~/resources/dev-preview/developer-preview-intro.md) .</span><span class="sxs-lookup"><span data-stu-id="c08c8-156">Mention support in cards is currently supported in [Developer Preview](~/resources/dev-preview/developer-preview-intro.md) only.</span></span>

<span data-ttu-id="c08c8-157">Теперь расширения Боты и обмена сообщениями могут включать упоминания в содержимом карточки в элементах text и Block.</span><span class="sxs-lookup"><span data-stu-id="c08c8-157">Bots and Messaging extensions can now include mentions within the card content in Text Block and FactSet elements.</span></span> 

### <a name="constructing-mentions"></a><span data-ttu-id="c08c8-158">Создание упоминаний</span><span class="sxs-lookup"><span data-stu-id="c08c8-158">Constructing mentions</span></span>

<span data-ttu-id="c08c8-159">Чтобы включить в адаптивную карточку упоминание, необходимо, чтобы приложение включало следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="c08c8-159">To include a mention in an Adaptive Card your app needs to include the following elements</span></span>

* <span data-ttu-id="c08c8-160">`<at>username</at>`в поддерживаемых элементах адаптивной карточки</span><span class="sxs-lookup"><span data-stu-id="c08c8-160">`<at>username</at>` in the supported adaptive card elements</span></span>
* <span data-ttu-id="c08c8-161">`mention` Объект внутри `msteams` свойства в содержимом карточки, включающий идентификатор пользователя Teams для указанного пользователя.</span><span class="sxs-lookup"><span data-stu-id="c08c8-161">The `mention` object inside of an `msteams` property in the card content, which includes the Teams user id of the user being mentioned</span></span>

<span data-ttu-id="c08c8-162">Обратите внимание, что карточки со упоминанием в мобильных клиентах в настоящее время не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="c08c8-162">Note that cards with mentions aren't supported on mobile clients at the moment.</span></span>

### <a name="sample-adaptive-card-with-a-mention"></a><span data-ttu-id="c08c8-163">Пример адаптивной карточки с упоминанием</span><span class="sxs-lookup"><span data-stu-id="c08c8-163">Sample Adaptive card with a mention</span></span>

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
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
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

## <a name="html-formatting-for-connector-cards"></a><span data-ttu-id="c08c8-164">Формат HTML для соединителей карт</span><span class="sxs-lookup"><span data-stu-id="c08c8-164">HTML formatting for Connector Cards</span></span>

<span data-ttu-id="c08c8-165">Карты соединителей поддерживают ограниченные Markdown и форматирование HTML.</span><span class="sxs-lookup"><span data-stu-id="c08c8-165">Connector cards support limited markdown and HTML formatting.</span></span> <span data-ttu-id="c08c8-166">Markdown описывается в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="c08c8-166">Markdown is described in the next section.</span></span>

| <span data-ttu-id="c08c8-167">Стиль</span><span class="sxs-lookup"><span data-stu-id="c08c8-167">Style</span></span> | <span data-ttu-id="c08c8-168">Пример</span><span class="sxs-lookup"><span data-stu-id="c08c8-168">Example</span></span> | <span data-ttu-id="c08c8-169">HTML</span><span class="sxs-lookup"><span data-stu-id="c08c8-169">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c08c8-170">bold</span><span class="sxs-lookup"><span data-stu-id="c08c8-170">bold</span></span> | <span data-ttu-id="c08c8-171">**text**</span><span class="sxs-lookup"><span data-stu-id="c08c8-171">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="c08c8-172">italic</span><span class="sxs-lookup"><span data-stu-id="c08c8-172">italic</span></span> | <span data-ttu-id="c08c8-173">*text*</span><span class="sxs-lookup"><span data-stu-id="c08c8-173">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="c08c8-174">Верхний колонтитул (уровни&ndash;1 3)</span><span class="sxs-lookup"><span data-stu-id="c08c8-174">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="c08c8-175">**Text**</span><span class="sxs-lookup"><span data-stu-id="c08c8-175">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="c08c8-176">strikethrough</span><span class="sxs-lookup"><span data-stu-id="c08c8-176">strikethrough</span></span> | <span data-ttu-id="c08c8-177">~~text~~</span><span class="sxs-lookup"><span data-stu-id="c08c8-177">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="c08c8-178">неупорядоченный список</span><span class="sxs-lookup"><span data-stu-id="c08c8-178">unordered list</span></span> | <ul><li><span data-ttu-id="c08c8-179">текст</span><span class="sxs-lookup"><span data-stu-id="c08c8-179">text</span></span></li><li><span data-ttu-id="c08c8-180">текст</span><span class="sxs-lookup"><span data-stu-id="c08c8-180">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="c08c8-181">упорядоченный список</span><span class="sxs-lookup"><span data-stu-id="c08c8-181">ordered list</span></span> | <ol><li><span data-ttu-id="c08c8-182">текст</span><span class="sxs-lookup"><span data-stu-id="c08c8-182">text</span></span></li><li><span data-ttu-id="c08c8-183">текст</span><span class="sxs-lookup"><span data-stu-id="c08c8-183">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="c08c8-184">предварительно отформатированный текст</span><span class="sxs-lookup"><span data-stu-id="c08c8-184">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="c08c8-185">blockquote</span><span class="sxs-lookup"><span data-stu-id="c08c8-185">blockquote</span></span> | <blockquote><span data-ttu-id="c08c8-186">текст</span><span class="sxs-lookup"><span data-stu-id="c08c8-186">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="c08c8-187">гиперссылка</span><span class="sxs-lookup"><span data-stu-id="c08c8-187">hyperlink</span></span> | [<span data-ttu-id="c08c8-188">Bing</span><span class="sxs-lookup"><span data-stu-id="c08c8-188">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="c08c8-189">Ссылка на изображение</span><span class="sxs-lookup"><span data-stu-id="c08c8-189">image link</span></span> | <img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

<span data-ttu-id="c08c8-190">В соединительных карточках строки новой строки отображаются в HTML- `<p>` коде с помощью тега.</span><span class="sxs-lookup"><span data-stu-id="c08c8-190">In connector cards, newlines are rendered in HTML using the `<p>` tag.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-html"></a><span data-ttu-id="c08c8-191">Различия между мобильными и рабочими столами для соединителей карт с помощью HTML</span><span class="sxs-lookup"><span data-stu-id="c08c8-191">Mobile and desktop differences for connector cards using HTML</span></span>

<span data-ttu-id="c08c8-192">На рабочем столе форматирование HTML-карт для соединителей выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c08c8-192">On the desktop, HTML formatting for connector cards looks like this:</span></span>

![Формат HTML для соединителей карт в клиенте для настольных ПК](~/assets/images/cards/Connector-desktop-html-combined.png)

<span data-ttu-id="c08c8-194">В iOS форматирование HTML выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c08c8-194">On iOS, HTML formatting looks like this:</span></span>

![Формат HTML для соединителей карт в клиенте iOS](~/assets/images/cards/connector-iphone-html-combined-80.png)

<span data-ttu-id="c08c8-196">Вопросы:</span><span class="sxs-lookup"><span data-stu-id="c08c8-196">Issues:</span></span>

* <span data-ttu-id="c08c8-197">Встроенные изображения не отправляются на iOS с помощью Markdown или HTML в соединительных карточках.</span><span class="sxs-lookup"><span data-stu-id="c08c8-197">Inline images are not rendered on iOS using either markdown or HTML in Connector Cards.</span></span>
* <span data-ttu-id="c08c8-198">Предварительно отформатированный текст отображается, но не является серым фоном.</span><span class="sxs-lookup"><span data-stu-id="c08c8-198">Preformatted text is rendered but does not have a gray background.</span></span>

<span data-ttu-id="c08c8-199">На Android форматирование HTML выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c08c8-199">On Android, HTML formatting looks like this:</span></span>

![Форматирование HTML-карт для соединителей в клиенте Android](~/assets/images/cards/connector-android-html-combined.png)

### <a name="formatting-sample-for-html-connector-cards"></a><span data-ttu-id="c08c8-201">Пример форматирования для карточек соединителей HTML</span><span class="sxs-lookup"><span data-stu-id="c08c8-201">Formatting sample for HTML Connector Cards</span></span>

``` json
{
  "contentType": "application/vnd.microsoft.teams.card.o365connector",
  "content": {
    "@type": "MessageCard",
    "@context": "http://schema.org/extensions",
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
            "text": "embedded image <img src=\"http://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img>"
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

## <a name="markdown-formatting-for-connector-cards"></a><span data-ttu-id="c08c8-202">Markdown форматирование карт подключателя</span><span class="sxs-lookup"><span data-stu-id="c08c8-202">Markdown formatting for Connector Cards</span></span>

<span data-ttu-id="c08c8-203">Карты соединителей поддерживают ограниченные Markdown и форматирование HTML.</span><span class="sxs-lookup"><span data-stu-id="c08c8-203">Connector cards support limited markdown and HTML formatting.</span></span> <span data-ttu-id="c08c8-204">КОД HTML описывается в последнем разделе.</span><span class="sxs-lookup"><span data-stu-id="c08c8-204">HTML is described in the last section.</span></span>

| <span data-ttu-id="c08c8-205">Стиль</span><span class="sxs-lookup"><span data-stu-id="c08c8-205">Style</span></span> | <span data-ttu-id="c08c8-206">Пример</span><span class="sxs-lookup"><span data-stu-id="c08c8-206">Example</span></span> | <span data-ttu-id="c08c8-207">Markdown</span><span class="sxs-lookup"><span data-stu-id="c08c8-207">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c08c8-208">bold</span><span class="sxs-lookup"><span data-stu-id="c08c8-208">bold</span></span> | <span data-ttu-id="c08c8-209">**text**</span><span class="sxs-lookup"><span data-stu-id="c08c8-209">**text**</span></span> | `**text**` |
| <span data-ttu-id="c08c8-210">italic</span><span class="sxs-lookup"><span data-stu-id="c08c8-210">italic</span></span> | <span data-ttu-id="c08c8-211">*text*</span><span class="sxs-lookup"><span data-stu-id="c08c8-211">*text*</span></span> | `*text*` |
| <span data-ttu-id="c08c8-212">Верхний колонтитул (уровни&ndash;1 3)</span><span class="sxs-lookup"><span data-stu-id="c08c8-212">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="c08c8-213">**Text**</span><span class="sxs-lookup"><span data-stu-id="c08c8-213">**Text**</span></span> | `### Text`|
| <span data-ttu-id="c08c8-214">strikethrough</span><span class="sxs-lookup"><span data-stu-id="c08c8-214">strikethrough</span></span> | <span data-ttu-id="c08c8-215">~~text~~</span><span class="sxs-lookup"><span data-stu-id="c08c8-215">~~text~~</span></span> | `~~text~~` |
| <span data-ttu-id="c08c8-216">неупорядоченный список</span><span class="sxs-lookup"><span data-stu-id="c08c8-216">unordered list</span></span> | <ul><li><span data-ttu-id="c08c8-217">текст</span><span class="sxs-lookup"><span data-stu-id="c08c8-217">text</span></span></li><li><span data-ttu-id="c08c8-218">текст</span><span class="sxs-lookup"><span data-stu-id="c08c8-218">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="c08c8-219">упорядоченный список</span><span class="sxs-lookup"><span data-stu-id="c08c8-219">ordered list</span></span> | <ol><li><span data-ttu-id="c08c8-220">текст</span><span class="sxs-lookup"><span data-stu-id="c08c8-220">text</span></span></li><li><span data-ttu-id="c08c8-221">текст</span><span class="sxs-lookup"><span data-stu-id="c08c8-221">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="c08c8-222">предварительно отформатированный текст</span><span class="sxs-lookup"><span data-stu-id="c08c8-222">preformatted text</span></span> | `text` | ``preformatted text`` |
| <span data-ttu-id="c08c8-223">blockquote</span><span class="sxs-lookup"><span data-stu-id="c08c8-223">blockquote</span></span> | <span data-ttu-id="c08c8-224">>текст блокккуоте</span><span class="sxs-lookup"><span data-stu-id="c08c8-224">>blockquote text</span></span> | `>blockquote text` |
| <span data-ttu-id="c08c8-225">гиперссылка</span><span class="sxs-lookup"><span data-stu-id="c08c8-225">hyperlink</span></span> | [<span data-ttu-id="c08c8-226">Bing</span><span class="sxs-lookup"><span data-stu-id="c08c8-226">Bing</span></span>](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| <span data-ttu-id="c08c8-227">Ссылка на изображение</span><span class="sxs-lookup"><span data-stu-id="c08c8-227">image link</span></span> |![Дукк на рок](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

<span data-ttu-id="c08c8-229">В соединителях соединителей отображаются строки `\n\n`, но не for `\n` или. `\r`</span><span class="sxs-lookup"><span data-stu-id="c08c8-229">In connector cards, newlines are rendered for `\n\n`, but not for `\n` or `\r`.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-markdown"></a><span data-ttu-id="c08c8-230">Различия между мобильными и рабочими столами для соединителей карт с помощью Markdown</span><span class="sxs-lookup"><span data-stu-id="c08c8-230">Mobile and desktop differences for connector cards using markdown</span></span>

<span data-ttu-id="c08c8-231">На рабочем столе Markdown форматирование карт для соединителей выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c08c8-231">On the desktop, markdown formatting for connector cards looks like this:</span></span>

![Формат HTML для соединителей карт в клиенте для настольных ПК](~/assets/images/cards/connector-desktop-markdown-combined.png)

<span data-ttu-id="c08c8-233">В iOS форматирование Markdown для карт подключателя выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c08c8-233">On iOS, markdown formatting for connector cards looks like this:</span></span>

![Формат HTML для соединителей карт в клиенте iOS](~/assets/images/cards/connector-iphone-markdown-combined-80.png)

<span data-ttu-id="c08c8-235">Вопросы:</span><span class="sxs-lookup"><span data-stu-id="c08c8-235">Issues:</span></span>

* <span data-ttu-id="c08c8-236">Клиент iOS для Teams не отображает Markdown или встроенные изображения HTML в соединительных картах.</span><span class="sxs-lookup"><span data-stu-id="c08c8-236">The iOS client for Teams does not render markdown or HTML inline images in Connector Cards.</span></span>
* <span data-ttu-id="c08c8-237">Блокккуотес отображаются с отступом, но без серого фона.</span><span class="sxs-lookup"><span data-stu-id="c08c8-237">Blockquotes are rendered as indented but without a gray background.</span></span>

<span data-ttu-id="c08c8-238">На Android Markdown форматирование карт для соединителей выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c08c8-238">On Android, markdown formatting for connector cards looks like this:</span></span>

![Форматирование HTML-карт для соединителей в клиенте Android](~/assets/images/cards/connector-android-markdown-combined.png)

### <a name="formatting-example-for-markdown-connector-cards"></a><span data-ttu-id="c08c8-240">Пример форматирования для карточек соединителей Markdown</span><span class="sxs-lookup"><span data-stu-id="c08c8-240">Formatting example for markdown Connector Cards</span></span>

``` json
{
  "contentType": "application/vnd.microsoft.teams.card.o365connector",
  "content": {
    "@type": "MessageCard",
    "@context": "http://schema.org/extensions",
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
            "text": "embedded image link: ![Duck on a rock](http://aka.ms/Fo983c)"
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

## <a name="html-formatting-for-simple-cards"></a><span data-ttu-id="c08c8-241">Форматирование HTML для простых карточек</span><span class="sxs-lookup"><span data-stu-id="c08c8-241">HTML Formatting for simple cards</span></span>

<span data-ttu-id="c08c8-242">Эти теги HTML поддерживаются для простых карточек, таких как карта главный Имиджевый баннер и эскиза.</span><span class="sxs-lookup"><span data-stu-id="c08c8-242">These HTML tags are supported for simple cards such as the hero and thumbnail card.</span></span> <span data-ttu-id="c08c8-243">Markdown не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="c08c8-243">Markdown is not supported.</span></span>

| <span data-ttu-id="c08c8-244">Стиль</span><span class="sxs-lookup"><span data-stu-id="c08c8-244">Style</span></span> | <span data-ttu-id="c08c8-245">Пример</span><span class="sxs-lookup"><span data-stu-id="c08c8-245">Example</span></span> | <span data-ttu-id="c08c8-246">HTML</span><span class="sxs-lookup"><span data-stu-id="c08c8-246">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c08c8-247">bold</span><span class="sxs-lookup"><span data-stu-id="c08c8-247">bold</span></span> | <span data-ttu-id="c08c8-248">**text**</span><span class="sxs-lookup"><span data-stu-id="c08c8-248">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="c08c8-249">italic</span><span class="sxs-lookup"><span data-stu-id="c08c8-249">italic</span></span> | <span data-ttu-id="c08c8-250">*text*</span><span class="sxs-lookup"><span data-stu-id="c08c8-250">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="c08c8-251">Верхний колонтитул (уровни&ndash;1 3)</span><span class="sxs-lookup"><span data-stu-id="c08c8-251">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="c08c8-252">**Text**</span><span class="sxs-lookup"><span data-stu-id="c08c8-252">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="c08c8-253">strikethrough</span><span class="sxs-lookup"><span data-stu-id="c08c8-253">strikethrough</span></span> | <span data-ttu-id="c08c8-254">~~text~~</span><span class="sxs-lookup"><span data-stu-id="c08c8-254">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="c08c8-255">неупорядоченный список</span><span class="sxs-lookup"><span data-stu-id="c08c8-255">unordered list</span></span> | <ul><li><span data-ttu-id="c08c8-256">текст</span><span class="sxs-lookup"><span data-stu-id="c08c8-256">text</span></span></li><li><span data-ttu-id="c08c8-257">текст</span><span class="sxs-lookup"><span data-stu-id="c08c8-257">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="c08c8-258">упорядоченный список</span><span class="sxs-lookup"><span data-stu-id="c08c8-258">ordered list</span></span> | <ol><li><span data-ttu-id="c08c8-259">текст</span><span class="sxs-lookup"><span data-stu-id="c08c8-259">text</span></span></li><li><span data-ttu-id="c08c8-260">текст</span><span class="sxs-lookup"><span data-stu-id="c08c8-260">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="c08c8-261">предварительно отформатированный текст</span><span class="sxs-lookup"><span data-stu-id="c08c8-261">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="c08c8-262">blockquote</span><span class="sxs-lookup"><span data-stu-id="c08c8-262">blockquote</span></span> | <blockquote><span data-ttu-id="c08c8-263">текст</span><span class="sxs-lookup"><span data-stu-id="c08c8-263">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="c08c8-264">гиперссылка</span><span class="sxs-lookup"><span data-stu-id="c08c8-264">hyperlink</span></span> | [<span data-ttu-id="c08c8-265">Bing</span><span class="sxs-lookup"><span data-stu-id="c08c8-265">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="c08c8-266">Ссылка на изображение</span><span class="sxs-lookup"><span data-stu-id="c08c8-266">image link</span></span> |<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a><span data-ttu-id="c08c8-267">Различия между мобильными и рабочими столами для простых карточек</span><span class="sxs-lookup"><span data-stu-id="c08c8-267">Mobile and desktop differences for simple cards</span></span>

<span data-ttu-id="c08c8-268">Из-за различий в разрешениях между настольными и мобильными платформами форматирование различается для настольных ПК и мобильных версий Teams.</span><span class="sxs-lookup"><span data-stu-id="c08c8-268">Because of resolution differences between the desktop and mobile platform, formatting is different between the desktop and the mobile version of Teams.</span></span>

<span data-ttu-id="c08c8-269">На настольном компьютере форматирование HTML выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c08c8-269">On the desktop, HTML formatting appears like this:</span></span>

![Форматирование HTML в клиенте для настольных ПК](~/assets/images/cards/card-formatting-xml-desktop-v2.png)

<span data-ttu-id="c08c8-271">В iOS форматирование HTML выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c08c8-271">On iOS, HTML formatting appears like this:</span></span>

![Форматирование HTML в клиенте iOS](~/assets/images/cards/card-formatting-xml-mobile-v2.png)

<span data-ttu-id="c08c8-273">Вопросы:</span><span class="sxs-lookup"><span data-stu-id="c08c8-273">Issues:</span></span>

* <span data-ttu-id="c08c8-274">Форматирование символов, например полужирный шрифт и курсив, не отображается в iOS.</span><span class="sxs-lookup"><span data-stu-id="c08c8-274">Character formatting like bold and italic are not rendered on iOS.</span></span>

<span data-ttu-id="c08c8-275">На Android форматирование HTML выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c08c8-275">On Android, HTML formatting appears like this:</span></span>

![Форматирование HTML в клиенте Android](~/assets/images/cards/card-formatting-xml-android-60.png)

<span data-ttu-id="c08c8-277">Правильное форматирование знаков, как полужирное и курсивное отображение на Android.</span><span class="sxs-lookup"><span data-stu-id="c08c8-277">Character formatting like bold and italic display correctly on Android.</span></span>

### <a name="formatting-sample-for-html-formatting-in-simple-cards"></a><span data-ttu-id="c08c8-278">Пример форматирования форматирования HTML на простых карточках</span><span class="sxs-lookup"><span data-stu-id="c08c8-278">Formatting sample for HTML formatting in simple cards</span></span>

<span data-ttu-id="c08c8-279">Эти снимки создаются с помощью Teams Аппстудио, где для свойства Text карточки главный Имиджевый баннер задано значение, равное следующей строке.</span><span class="sxs-lookup"><span data-stu-id="c08c8-279">These screenshots were created using Teams AppStudio, where the text property of a hero card was set to the following string.</span></span> <span data-ttu-id="c08c8-280">Вы можете проверить форматирование в собственных карточках, изменив этот код.</span><span class="sxs-lookup"><span data-stu-id="c08c8-280">You can test formatting in your own cards by modifying this code.</span></span>

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"http://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`
