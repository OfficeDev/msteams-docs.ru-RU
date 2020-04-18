---
title: Форматирование текста в карточках
description: Описание форматирования текста карточки в Microsoft Teams
keywords: формат карточек Боты Teams
ms.date: 03/29/2018
ms.openlocfilehash: 9ced8a8956265322e91b9d40dc7dc7064ee4659f
ms.sourcegitcommit: 510ae42f72798fb24ddef0afa771ecd9d38e5348
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2020
ms.locfileid: "43550954"
---
# <a name="format-cards-in-teams"></a><span data-ttu-id="a1760-104">Форматирование карточек в Teams</span><span class="sxs-lookup"><span data-stu-id="a1760-104">Format cards in Teams</span></span>

<span data-ttu-id="a1760-105">В зависимости от типа карты в карточки можно добавлять форматированный текст в карточки с помощью Markdown или HTML.</span><span class="sxs-lookup"><span data-stu-id="a1760-105">You can add rich text formatting to your cards using either Markdown or HTML, depending on the card type.</span></span>

<span data-ttu-id="a1760-106">Карточки поддерживают форматирование только в свойстве Text, а не в свойствах Title и субтитров.</span><span class="sxs-lookup"><span data-stu-id="a1760-106">Cards support formatting in the text property only, not in the title or subtitle properties.</span></span> <span data-ttu-id="a1760-107">Форматирование можно указать с помощью подмножества форматирования XML (HTML) или Markdown в зависимости от типа карты.</span><span class="sxs-lookup"><span data-stu-id="a1760-107">Formatting can be specified using a subset of XML (HTML) formatting, or Markdown depending on card type.</span></span> <span data-ttu-id="a1760-108">Для текущих и будущих развертываний рекомендуется использовать форматирование Markdown.</span><span class="sxs-lookup"><span data-stu-id="a1760-108">For current and future development Adaptive cards using Markdown formatting is recommended.</span></span>

<span data-ttu-id="a1760-109">Поддержка форматирования различается для разных типов карточек, а отображение карты может незначительно отличаться между настольным компьютером и мобильными клиентами Teams, а также с Teams в браузере настольного компьютера.</span><span class="sxs-lookup"><span data-stu-id="a1760-109">Formatting support differs between different card types, and rendering of the card can differ slightly between the desktop and the mobile Teams clients, as well as Teams in the desktop browser.</span></span>

<span data-ttu-id="a1760-110">Встроенное изображение можно добавить с помощью любой карточки Teams.</span><span class="sxs-lookup"><span data-stu-id="a1760-110">You can include an inline image with any Teams card.</span></span> <span data-ttu-id="a1760-111">Изображения в формате " `.png`, `.jpg`" или `.gif` "файлы" не должны превышать 1024 × 1024 px или 1 МБ.</span><span class="sxs-lookup"><span data-stu-id="a1760-111">Images an be formatted as  `.png`, `.jpg`, or `.gif` files and must not exceed 1024 ×1024 px or 1 MB.</span></span> <span data-ttu-id="a1760-112">Анимированный GIF-файл не поддерживается официально.</span><span class="sxs-lookup"><span data-stu-id="a1760-112">Animated GIF is not officially supported.</span></span> <span data-ttu-id="a1760-113">*См* . [Справочник по карточкам](./cards-reference.md#inline-card-images)</span><span class="sxs-lookup"><span data-stu-id="a1760-113">*See* [Cards reference](./cards-reference.md#inline-card-images)</span></span>

## <a name="formatting-cards-with-markdown"></a><span data-ttu-id="a1760-114">Форматирование карточек с помощью Markdown</span><span class="sxs-lookup"><span data-stu-id="a1760-114">Formatting cards with Markdown</span></span>

<span data-ttu-id="a1760-115">Существует два типа карточек, поддерживающих Markdown в teams:</span><span class="sxs-lookup"><span data-stu-id="a1760-115">There are two card types that support Markdown in Teams:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a1760-116">**Адаптивные карты**: Markdown поддерживается в поле адаптивной карточки `Textblock` , а также `Fact.Title` и `Fact.Value`.</span><span class="sxs-lookup"><span data-stu-id="a1760-116">**Adaptive Cards**: Markdown is supported in Adaptive Card `Textblock` field, as well as `Fact.Title` and `Fact.Value`.</span></span> <span data-ttu-id="a1760-117">HTML не поддерживается в адаптивных картах.</span><span class="sxs-lookup"><span data-stu-id="a1760-117">HTML is not supported in adaptive cards.</span></span>
> * <span data-ttu-id="a1760-118">**Соединительные карты O365**: Markdown и ограниченный HTML-код поддерживаются в карточках соединителей Office 365 в текстовых полях.</span><span class="sxs-lookup"><span data-stu-id="a1760-118">**O365 Connector Cards**: Markdown and limited HTML is supported in Office 365 Connector cards in the text fields.</span></span>

# <a name="markdown-formatting-adaptive-cards"></a>[<span data-ttu-id="a1760-119">**Форматирование Markdown: адаптивные карты**</span><span class="sxs-lookup"><span data-stu-id="a1760-119">**Markdown formatting: Adaptive Cards**</span></span>](#tab/adaptive-md)

 <span data-ttu-id="a1760-120">Поддерживаются следующие стили `Textblock` `Fact.Title` `Fact.Value` :</span><span class="sxs-lookup"><span data-stu-id="a1760-120">The supported styles for `Textblock`, `Fact.Title` and `Fact.Value` are:</span></span>

| <span data-ttu-id="a1760-121">Стиль</span><span class="sxs-lookup"><span data-stu-id="a1760-121">Style</span></span> | <span data-ttu-id="a1760-122">Пример</span><span class="sxs-lookup"><span data-stu-id="a1760-122">Example</span></span> | <span data-ttu-id="a1760-123">Markdown</span><span class="sxs-lookup"><span data-stu-id="a1760-123">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a1760-124">bold</span><span class="sxs-lookup"><span data-stu-id="a1760-124">bold</span></span> | <span data-ttu-id="a1760-125">**Bold**</span><span class="sxs-lookup"><span data-stu-id="a1760-125">**Bold**</span></span> | ```**Bold**``` |
| <span data-ttu-id="a1760-126">italic</span><span class="sxs-lookup"><span data-stu-id="a1760-126">italic</span></span> | <span data-ttu-id="a1760-127">_Italic_</span><span class="sxs-lookup"><span data-stu-id="a1760-127">_Italic_</span></span> | ```_Italic_``` |
| <span data-ttu-id="a1760-128">неупорядоченный список</span><span class="sxs-lookup"><span data-stu-id="a1760-128">unordered list</span></span> | <ul><li><span data-ttu-id="a1760-129">текст</span><span class="sxs-lookup"><span data-stu-id="a1760-129">text</span></span></li><li><span data-ttu-id="a1760-130">текст</span><span class="sxs-lookup"><span data-stu-id="a1760-130">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="a1760-131">упорядоченный список</span><span class="sxs-lookup"><span data-stu-id="a1760-131">ordered list</span></span> | <ol><li><span data-ttu-id="a1760-132">текст</span><span class="sxs-lookup"><span data-stu-id="a1760-132">text</span></span></li><li><span data-ttu-id="a1760-133">текст</span><span class="sxs-lookup"><span data-stu-id="a1760-133">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="a1760-134">Гиперссылки</span><span class="sxs-lookup"><span data-stu-id="a1760-134">Hyperlinks</span></span> |[<span data-ttu-id="a1760-135">Bing</span><span class="sxs-lookup"><span data-stu-id="a1760-135">Bing</span></span>](https://www.bing.com/)| ```[Title](url)``` |

<span data-ttu-id="a1760-136">Следующие теги Markdown не поддерживаются:</span><span class="sxs-lookup"><span data-stu-id="a1760-136">The following Markdown tags are not supported:</span></span>

* <span data-ttu-id="a1760-137">Заголовки</span><span class="sxs-lookup"><span data-stu-id="a1760-137">Headers</span></span>
* <span data-ttu-id="a1760-138">Таблицы</span><span class="sxs-lookup"><span data-stu-id="a1760-138">Tables</span></span>
* <span data-ttu-id="a1760-139">Изображения</span><span class="sxs-lookup"><span data-stu-id="a1760-139">Images</span></span>
* <span data-ttu-id="a1760-140">Предварительно отформатированный текст</span><span class="sxs-lookup"><span data-stu-id="a1760-140">Preformatted text</span></span>
* <span data-ttu-id="a1760-141">блокккуотес</span><span class="sxs-lookup"><span data-stu-id="a1760-141">Blockquotes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a1760-142">Адаптивные карточки не поддерживают форматирование HTML.</span><span class="sxs-lookup"><span data-stu-id="a1760-142">Adaptive cards do not support any HTML formatting.</span></span>

### <a name="newlines-for-adaptive-cards"></a><span data-ttu-id="a1760-143">Строки для адаптивных карточек</span><span class="sxs-lookup"><span data-stu-id="a1760-143">Newlines for Adaptive Cards</span></span>

<span data-ttu-id="a1760-144">В списках можно использовать последовательности `\r` или `\n` escape-последовательности для новой строки.</span><span class="sxs-lookup"><span data-stu-id="a1760-144">In lists you can use the `\r` or `\n` escape sequences for newlines.</span></span> <span data-ttu-id="a1760-145">Использование `\n\n` в списке приводит к тому, что следующий элемент в списке будет иметь отступы.</span><span class="sxs-lookup"><span data-stu-id="a1760-145">Using `\n\n` in a list will cause the next element in the list to be indented.</span></span> <span data-ttu-id="a1760-146">Если в элементе TextBlock требуются строки новой строки, используйте `\n\n`.</span><span class="sxs-lookup"><span data-stu-id="a1760-146">If you need newlines elsewhere in the textblock, use `\n\n`.</span></span>

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a><span data-ttu-id="a1760-147">Различия между мобильными и настольными компьютерами для адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="a1760-147">Mobile and desktop differences for Adaptive Cards</span></span>

<span data-ttu-id="a1760-148">Форматирование слегка отличается между настольными и мобильными версиями Teams.</span><span class="sxs-lookup"><span data-stu-id="a1760-148">Formatting is slightly different between the desktop and the mobile versions of Teams.</span></span>

<span data-ttu-id="a1760-149">На рабочем столе Адаптивное форматирование карточки Markdown выглядит так же, как в веб-браузерах и в клиентском приложении teams:</span><span class="sxs-lookup"><span data-stu-id="a1760-149">On the desktop, Adaptive Card Markdown formatting appears like this in both web browsers and in the Teams client application:</span></span>

![Адаптивное форматирование карточки Markdown в клиенте для настольных ПК](../../assets/images/cards/Adaptive-markdown-desktop-client.png)

<span data-ttu-id="a1760-151">В iOS форматирование адаптивной карточки Markdown выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a1760-151">On iOS, Adaptive Card Markdown formatting appears like this:</span></span>

![Адаптивное форматирование карточки Markdown в iOS](../../assets/images/cards/Adaptive-markdown-iOS-75.png)

<span data-ttu-id="a1760-153">В Android Адаптивное форматирование карточки Markdown выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a1760-153">On Android, Adaptive Card Markdown formatting appears like this:</span></span>

![Адаптивное форматирование карточки Markdown в Android](../../assets/images/cards/Adaptive-markdown-Android.png)

### <a name="more-information-on-adaptive-cards"></a><span data-ttu-id="a1760-155">Дополнительные сведения о адаптивных картах</span><span class="sxs-lookup"><span data-stu-id="a1760-155">More information on Adaptive Cards</span></span>

<span data-ttu-id="a1760-156">[Функции для текста в адаптивных карточках](/adaptive-cards/create/textfeatures) Функции даты и локализации, упомянутые в этом разделе, не поддерживаются в Teams.</span><span class="sxs-lookup"><span data-stu-id="a1760-156">[Text features in Adaptive cards](/adaptive-cards/create/textfeatures) The date and localization features mentioned in this topic are not supported in Teams.</span></span>

### <a name="formatting-sample-for-adaptive-cards"></a><span data-ttu-id="a1760-157">Пример форматирования для адаптивных карточек</span><span class="sxs-lookup"><span data-stu-id="a1760-157">Formatting sample for Adaptive cards</span></span>

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

### <a name="mention-support-within-adaptive-cards"></a><span data-ttu-id="a1760-158">Упоминание поддержки в адаптивных картах</span><span class="sxs-lookup"><span data-stu-id="a1760-158">Mention support within Adaptive cards</span></span>

> [!NOTE]
> <span data-ttu-id="a1760-159">Упоминание поддержки в карточках в настоящее время поддерживается только в [режиме предварительного просмотра разработчика](../../resources/dev-preview/developer-preview-intro.md) .</span><span class="sxs-lookup"><span data-stu-id="a1760-159">Mention support in cards is currently supported in [Developer Preview](../../resources/dev-preview/developer-preview-intro.md) only.</span></span>

<span data-ttu-id="a1760-160">Теперь расширения Боты и обмена сообщениями могут включать упоминания в содержимом карточки в элементах text и Block.</span><span class="sxs-lookup"><span data-stu-id="a1760-160">Bots and Messaging extensions can now include mentions within the card content in Text Block and FactSet elements.</span></span>

### <a name="constructing-mentions"></a><span data-ttu-id="a1760-161">Создание упоминаний</span><span class="sxs-lookup"><span data-stu-id="a1760-161">Constructing mentions</span></span>

<span data-ttu-id="a1760-162">Чтобы включить в адаптивную карточку упоминание, необходимо, чтобы приложение включало следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="a1760-162">To include a mention in an Adaptive Card your app needs to include the following elements</span></span>

* <span data-ttu-id="a1760-163">`<at>username</at>`в поддерживаемых элементах адаптивной карточки</span><span class="sxs-lookup"><span data-stu-id="a1760-163">`<at>username</at>` in the supported adaptive card elements</span></span>
* <span data-ttu-id="a1760-164">`mention` Объект внутри `msteams` свойства в содержимом карточки, включающий идентификатор пользователя Teams для указанного пользователя.</span><span class="sxs-lookup"><span data-stu-id="a1760-164">The `mention` object inside of an `msteams` property in the card content, which includes the Teams user id of the user being mentioned</span></span>

<span data-ttu-id="a1760-165">Обратите внимание, что карточки со упоминанием в мобильных клиентах в настоящее время не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="a1760-165">Note that cards with mentions aren't supported on mobile clients at the moment.</span></span>

### <a name="sample-adaptive-card-with-a-mention"></a><span data-ttu-id="a1760-166">Пример адаптивной карточки с упоминанием</span><span class="sxs-lookup"><span data-stu-id="a1760-166">Sample Adaptive card with a mention</span></span>

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

# <a name="markdown-formatting-o365-connector-cards"></a>[<span data-ttu-id="a1760-167">**Форматирование Markdown: карты соединителей O365**</span><span class="sxs-lookup"><span data-stu-id="a1760-167">**Markdown formatting: O365 Connector Cards**</span></span>](#tab/connector-md)

<span data-ttu-id="a1760-168">Карты соединителей поддерживают ограниченные Markdown и форматирование HTML.</span><span class="sxs-lookup"><span data-stu-id="a1760-168">Connector cards support limited Markdown and HTML formatting.</span></span> <span data-ttu-id="a1760-169">Поддержка HTML описана в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="a1760-169">HTML support is described in the last section.</span></span>

| <span data-ttu-id="a1760-170">Стиль</span><span class="sxs-lookup"><span data-stu-id="a1760-170">Style</span></span> | <span data-ttu-id="a1760-171">Пример</span><span class="sxs-lookup"><span data-stu-id="a1760-171">Example</span></span> | <span data-ttu-id="a1760-172">Markdown</span><span class="sxs-lookup"><span data-stu-id="a1760-172">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a1760-173">bold</span><span class="sxs-lookup"><span data-stu-id="a1760-173">bold</span></span> | <span data-ttu-id="a1760-174">**text**</span><span class="sxs-lookup"><span data-stu-id="a1760-174">**text**</span></span> | `**text**` |
| <span data-ttu-id="a1760-175">italic</span><span class="sxs-lookup"><span data-stu-id="a1760-175">italic</span></span> | <span data-ttu-id="a1760-176">*text*</span><span class="sxs-lookup"><span data-stu-id="a1760-176">*text*</span></span> | `*text*` |
| <span data-ttu-id="a1760-177">Верхний колонтитул (уровни&ndash;1 3)</span><span class="sxs-lookup"><span data-stu-id="a1760-177">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="a1760-178">**Text**</span><span class="sxs-lookup"><span data-stu-id="a1760-178">**Text**</span></span> | `### Text`|
| <span data-ttu-id="a1760-179">strikethrough</span><span class="sxs-lookup"><span data-stu-id="a1760-179">strikethrough</span></span> | <span data-ttu-id="a1760-180">~~text~~</span><span class="sxs-lookup"><span data-stu-id="a1760-180">~~text~~</span></span> | `~~text~~` |
| <span data-ttu-id="a1760-181">неупорядоченный список</span><span class="sxs-lookup"><span data-stu-id="a1760-181">unordered list</span></span> | <ul><li><span data-ttu-id="a1760-182">текст</span><span class="sxs-lookup"><span data-stu-id="a1760-182">text</span></span></li><li><span data-ttu-id="a1760-183">текст</span><span class="sxs-lookup"><span data-stu-id="a1760-183">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="a1760-184">упорядоченный список</span><span class="sxs-lookup"><span data-stu-id="a1760-184">ordered list</span></span> | <ol><li><span data-ttu-id="a1760-185">текст</span><span class="sxs-lookup"><span data-stu-id="a1760-185">text</span></span></li><li><span data-ttu-id="a1760-186">текст</span><span class="sxs-lookup"><span data-stu-id="a1760-186">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="a1760-187">предварительно отформатированный текст</span><span class="sxs-lookup"><span data-stu-id="a1760-187">preformatted text</span></span> | `text` | ``preformatted text`` |
| <span data-ttu-id="a1760-188">blockquote</span><span class="sxs-lookup"><span data-stu-id="a1760-188">blockquote</span></span> | <span data-ttu-id="a1760-189">>текст блокккуоте</span><span class="sxs-lookup"><span data-stu-id="a1760-189">>blockquote text</span></span> | `>blockquote text` |
| <span data-ttu-id="a1760-190">гиперссылка</span><span class="sxs-lookup"><span data-stu-id="a1760-190">hyperlink</span></span> | [<span data-ttu-id="a1760-191">Bing</span><span class="sxs-lookup"><span data-stu-id="a1760-191">Bing</span></span>](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| <span data-ttu-id="a1760-192">Ссылка на изображение</span><span class="sxs-lookup"><span data-stu-id="a1760-192">image link</span></span> |![Дукк на рок](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

<span data-ttu-id="a1760-194">В соединителях соединителей отображаются строки `\n\n`, но не for `\n` или. `\r`</span><span class="sxs-lookup"><span data-stu-id="a1760-194">In connector cards, newlines are rendered for `\n\n`, but not for `\n` or `\r`.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-markdown"></a><span data-ttu-id="a1760-195">Различия между мобильными и рабочими столами для соединителей карт с помощью Markdown</span><span class="sxs-lookup"><span data-stu-id="a1760-195">Mobile and desktop differences for connector cards using Markdown</span></span>

<span data-ttu-id="a1760-196">На рабочем столе Markdown форматирование карт для соединителей выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a1760-196">On the desktop, Markdown formatting for connector cards looks like this:</span></span>

![Markdown форматирование карт подключателя в клиенте для настольных ПК](../../assets/images/cards/connector-desktop-markdown-combined.png)

<span data-ttu-id="a1760-198">В iOS форматирование Markdown для карт подключателя выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a1760-198">On iOS, Markdown formatting for connector cards looks like this:</span></span>

![Markdown форматирование карт подключателя в клиенте iOS](../../assets/images/cards/connector-iphone-markdown-combined-80.png)

<span data-ttu-id="a1760-200">Вопросы:</span><span class="sxs-lookup"><span data-stu-id="a1760-200">Issues:</span></span>

* <span data-ttu-id="a1760-201">Клиент iOS для Teams не отображает Markdown или встроенные изображения HTML в соединительных картах.</span><span class="sxs-lookup"><span data-stu-id="a1760-201">The iOS client for Teams does not render Markdown or HTML inline images in Connector Cards.</span></span>
* <span data-ttu-id="a1760-202">Блокккуотес отображаются с отступом, но без серого фона.</span><span class="sxs-lookup"><span data-stu-id="a1760-202">Blockquotes are rendered as indented but without a gray background.</span></span>

<span data-ttu-id="a1760-203">На Android Markdown форматирование карт для соединителей выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a1760-203">On Android, Markdown formatting for connector cards looks like this:</span></span>

![Markdown форматирование карт подключателя в клиенте Android](../../assets/images/cards/connector-android-markdown-combined.png)

### <a name="formatting-example-for-markdown-connector-cards"></a><span data-ttu-id="a1760-205">Пример форматирования для карточек соединителей Markdown</span><span class="sxs-lookup"><span data-stu-id="a1760-205">Formatting example for Markdown Connector Cards</span></span>

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

---

## <a name="formatting-cards-with-html"></a><span data-ttu-id="a1760-206">Форматирование карточек с помощью HTML</span><span class="sxs-lookup"><span data-stu-id="a1760-206">Formatting cards with HTML</span></span>

# <a name="html-formatting-o365-connector-cards"></a>[<span data-ttu-id="a1760-207">**Форматирование HTML: карты соединителей O365**</span><span class="sxs-lookup"><span data-stu-id="a1760-207">**HTML formatting: O365 Connector Cards**</span></span>](#tab/connector-html)

<span data-ttu-id="a1760-208">Карты соединителей поддерживают ограниченные Markdown и форматирование HTML.</span><span class="sxs-lookup"><span data-stu-id="a1760-208">Connector cards support limited Markdown and HTML formatting.</span></span> <span data-ttu-id="a1760-209">Markdown описывается в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="a1760-209">Markdown is described in the next section.</span></span>

| <span data-ttu-id="a1760-210">Стиль</span><span class="sxs-lookup"><span data-stu-id="a1760-210">Style</span></span> | <span data-ttu-id="a1760-211">Пример</span><span class="sxs-lookup"><span data-stu-id="a1760-211">Example</span></span> | <span data-ttu-id="a1760-212">HTML</span><span class="sxs-lookup"><span data-stu-id="a1760-212">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a1760-213">bold</span><span class="sxs-lookup"><span data-stu-id="a1760-213">bold</span></span> | <span data-ttu-id="a1760-214">**text**</span><span class="sxs-lookup"><span data-stu-id="a1760-214">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="a1760-215">italic</span><span class="sxs-lookup"><span data-stu-id="a1760-215">italic</span></span> | <span data-ttu-id="a1760-216">*text*</span><span class="sxs-lookup"><span data-stu-id="a1760-216">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="a1760-217">Верхний колонтитул (уровни&ndash;1 3)</span><span class="sxs-lookup"><span data-stu-id="a1760-217">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="a1760-218">**Text**</span><span class="sxs-lookup"><span data-stu-id="a1760-218">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="a1760-219">strikethrough</span><span class="sxs-lookup"><span data-stu-id="a1760-219">strikethrough</span></span> | <span data-ttu-id="a1760-220">~~text~~</span><span class="sxs-lookup"><span data-stu-id="a1760-220">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="a1760-221">неупорядоченный список</span><span class="sxs-lookup"><span data-stu-id="a1760-221">unordered list</span></span> | <ul><li><span data-ttu-id="a1760-222">текст</span><span class="sxs-lookup"><span data-stu-id="a1760-222">text</span></span></li><li><span data-ttu-id="a1760-223">текст</span><span class="sxs-lookup"><span data-stu-id="a1760-223">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="a1760-224">упорядоченный список</span><span class="sxs-lookup"><span data-stu-id="a1760-224">ordered list</span></span> | <ol><li><span data-ttu-id="a1760-225">текст</span><span class="sxs-lookup"><span data-stu-id="a1760-225">text</span></span></li><li><span data-ttu-id="a1760-226">текст</span><span class="sxs-lookup"><span data-stu-id="a1760-226">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="a1760-227">предварительно отформатированный текст</span><span class="sxs-lookup"><span data-stu-id="a1760-227">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="a1760-228">blockquote</span><span class="sxs-lookup"><span data-stu-id="a1760-228">blockquote</span></span> | <blockquote><span data-ttu-id="a1760-229">текст</span><span class="sxs-lookup"><span data-stu-id="a1760-229">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="a1760-230">гиперссылка</span><span class="sxs-lookup"><span data-stu-id="a1760-230">hyperlink</span></span> | [<span data-ttu-id="a1760-231">Bing</span><span class="sxs-lookup"><span data-stu-id="a1760-231">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="a1760-232">Ссылка на изображение</span><span class="sxs-lookup"><span data-stu-id="a1760-232">image link</span></span> | <img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

<span data-ttu-id="a1760-233">В соединительных карточках строки новой строки отображаются в HTML- `<p>` коде с помощью тега.</span><span class="sxs-lookup"><span data-stu-id="a1760-233">In connector cards, newlines are rendered in HTML using the `<p>` tag.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-html"></a><span data-ttu-id="a1760-234">Различия между мобильными и рабочими столами для соединителей карт с помощью HTML</span><span class="sxs-lookup"><span data-stu-id="a1760-234">Mobile and desktop differences for connector cards using HTML</span></span>

<span data-ttu-id="a1760-235">На рабочем столе форматирование HTML-карт для соединителей выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a1760-235">On the desktop, HTML formatting for connector cards looks like this:</span></span>

![Формат HTML для соединителей карт в клиенте для настольных ПК](../../assets/images/cards/Connector-desktop-html-combined.png)

<span data-ttu-id="a1760-237">В iOS форматирование HTML выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a1760-237">On iOS, HTML formatting looks like this:</span></span>

![Формат HTML для соединителей карт в клиенте iOS](../../assets/images/cards/connector-iphone-html-combined-80.png)

<span data-ttu-id="a1760-239">Вопросы:</span><span class="sxs-lookup"><span data-stu-id="a1760-239">Issues:</span></span>

* <span data-ttu-id="a1760-240">Встроенные изображения не отправляются на iOS с помощью Markdown или HTML в соединительных карточках.</span><span class="sxs-lookup"><span data-stu-id="a1760-240">Inline images are not rendered on iOS using either Markdown or HTML in Connector Cards.</span></span>
* <span data-ttu-id="a1760-241">Предварительно отформатированный текст отображается, но не является серым фоном.</span><span class="sxs-lookup"><span data-stu-id="a1760-241">Preformatted text is rendered but does not have a gray background.</span></span>

<span data-ttu-id="a1760-242">На Android форматирование HTML выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a1760-242">On Android, HTML formatting looks like this:</span></span>

![Форматирование HTML-карт для соединителей в клиенте Android](../../assets/images/cards/connector-android-html-combined.png)

### <a name="formatting-sample-for-html-connector-cards"></a><span data-ttu-id="a1760-244">Пример форматирования для карточек соединителей HTML</span><span class="sxs-lookup"><span data-stu-id="a1760-244">Formatting sample for HTML Connector Cards</span></span>

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

# <a name="html-formatting-hero-and-thumbnail-cards"></a>[<span data-ttu-id="a1760-245">**HTML-форматирование: карточки главный Имиджевый баннер и эскиза**</span><span class="sxs-lookup"><span data-stu-id="a1760-245">**HTML Formatting: hero and thumbnail cards**</span></span>](#tab/simple-html)

<span data-ttu-id="a1760-246">Теги HTML поддерживаются для простых карточек, таких как карта главный Имиджевый баннер и эскиза.</span><span class="sxs-lookup"><span data-stu-id="a1760-246">HTML tags are supported for simple cards such as the hero and thumbnail card.</span></span> <span data-ttu-id="a1760-247">Markdown не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="a1760-247">Markdown is not supported.</span></span>

| <span data-ttu-id="a1760-248">Стиль</span><span class="sxs-lookup"><span data-stu-id="a1760-248">Style</span></span> | <span data-ttu-id="a1760-249">Пример</span><span class="sxs-lookup"><span data-stu-id="a1760-249">Example</span></span> | <span data-ttu-id="a1760-250">HTML</span><span class="sxs-lookup"><span data-stu-id="a1760-250">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a1760-251">bold</span><span class="sxs-lookup"><span data-stu-id="a1760-251">bold</span></span> | <span data-ttu-id="a1760-252">**text**</span><span class="sxs-lookup"><span data-stu-id="a1760-252">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="a1760-253">italic</span><span class="sxs-lookup"><span data-stu-id="a1760-253">italic</span></span> | <span data-ttu-id="a1760-254">*text*</span><span class="sxs-lookup"><span data-stu-id="a1760-254">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="a1760-255">Верхний колонтитул (уровни&ndash;1 3)</span><span class="sxs-lookup"><span data-stu-id="a1760-255">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="a1760-256">**Text**</span><span class="sxs-lookup"><span data-stu-id="a1760-256">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="a1760-257">strikethrough</span><span class="sxs-lookup"><span data-stu-id="a1760-257">strikethrough</span></span> | <span data-ttu-id="a1760-258">~~text~~</span><span class="sxs-lookup"><span data-stu-id="a1760-258">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="a1760-259">неупорядоченный список</span><span class="sxs-lookup"><span data-stu-id="a1760-259">unordered list</span></span> | <ul><li><span data-ttu-id="a1760-260">текст</span><span class="sxs-lookup"><span data-stu-id="a1760-260">text</span></span></li><li><span data-ttu-id="a1760-261">текст</span><span class="sxs-lookup"><span data-stu-id="a1760-261">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="a1760-262">упорядоченный список</span><span class="sxs-lookup"><span data-stu-id="a1760-262">ordered list</span></span> | <ol><li><span data-ttu-id="a1760-263">текст</span><span class="sxs-lookup"><span data-stu-id="a1760-263">text</span></span></li><li><span data-ttu-id="a1760-264">текст</span><span class="sxs-lookup"><span data-stu-id="a1760-264">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="a1760-265">предварительно отформатированный текст</span><span class="sxs-lookup"><span data-stu-id="a1760-265">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="a1760-266">blockquote</span><span class="sxs-lookup"><span data-stu-id="a1760-266">blockquote</span></span> | <blockquote><span data-ttu-id="a1760-267">текст</span><span class="sxs-lookup"><span data-stu-id="a1760-267">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="a1760-268">гиперссылка</span><span class="sxs-lookup"><span data-stu-id="a1760-268">hyperlink</span></span> | [<span data-ttu-id="a1760-269">Bing</span><span class="sxs-lookup"><span data-stu-id="a1760-269">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="a1760-270">Ссылка на изображение</span><span class="sxs-lookup"><span data-stu-id="a1760-270">image link</span></span> |<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a><span data-ttu-id="a1760-271">Различия между мобильными и рабочими столами для простых карточек</span><span class="sxs-lookup"><span data-stu-id="a1760-271">Mobile and desktop differences for simple cards</span></span>

<span data-ttu-id="a1760-272">Из-за различий в разрешениях между настольными и мобильными платформами форматирование различается для настольных ПК и мобильных версий Teams.</span><span class="sxs-lookup"><span data-stu-id="a1760-272">Because of resolution differences between the desktop and mobile platform, formatting is different between the desktop and the mobile version of Teams.</span></span>

<span data-ttu-id="a1760-273">На настольном компьютере форматирование HTML выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a1760-273">On the desktop, HTML formatting appears like this:</span></span>

![Форматирование HTML в клиенте для настольных ПК](../../assets/images/cards/card-formatting-xml-desktop-v2.png)

<span data-ttu-id="a1760-275">В iOS форматирование HTML выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a1760-275">On iOS, HTML formatting appears like this:</span></span>

![Форматирование HTML в клиенте iOS](../../assets/images/cards/card-formatting-xml-mobile-v2.png)

<span data-ttu-id="a1760-277">Вопросы:</span><span class="sxs-lookup"><span data-stu-id="a1760-277">Issues:</span></span>

* <span data-ttu-id="a1760-278">Форматирование символов, например полужирный шрифт и курсив, не отображается в iOS.</span><span class="sxs-lookup"><span data-stu-id="a1760-278">Character formatting like bold and italic are not rendered on iOS.</span></span>

<span data-ttu-id="a1760-279">На Android форматирование HTML выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a1760-279">On Android, HTML formatting appears like this:</span></span>

![Форматирование HTML в клиенте Android](../../assets/images/cards/card-formatting-xml-android-60.png)

<span data-ttu-id="a1760-281">Правильное форматирование знаков, как полужирное и курсивное отображение на Android.</span><span class="sxs-lookup"><span data-stu-id="a1760-281">Character formatting like bold and italic display correctly on Android.</span></span>

### <a name="formatting-sample-for-html-formatting-in-simple-cards"></a><span data-ttu-id="a1760-282">Пример форматирования форматирования HTML на простых карточках</span><span class="sxs-lookup"><span data-stu-id="a1760-282">Formatting sample for HTML formatting in simple cards</span></span>

<span data-ttu-id="a1760-283">Эти снимки создаются с помощью Teams Аппстудио, где для свойства Text карточки главный Имиджевый баннер задано значение, равное следующей строке.</span><span class="sxs-lookup"><span data-stu-id="a1760-283">These screenshots were created using Teams AppStudio, where the text property of a hero card was set to the following string.</span></span> <span data-ttu-id="a1760-284">Вы можете проверить форматирование в собственных карточках, изменив этот код.</span><span class="sxs-lookup"><span data-stu-id="a1760-284">You can test formatting in your own cards by modifying this code.</span></span>

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"http://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`

---
