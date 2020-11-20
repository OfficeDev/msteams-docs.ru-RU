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
# <a name="format-cards-in-teams"></a>Форматирование карточек в Teams

В зависимости от типа карты в карточки можно добавлять форматированный текст в карточки с помощью Markdown или HTML.

Карточки поддерживают форматирование только в свойстве Text, а не в свойствах Title и субтитров. Форматирование можно указать с помощью подмножества форматирования XML (HTML) или Markdown в зависимости от типа карты. Для текущих и будущих развертываний рекомендуется использовать форматирование Markdown.

Поддержка форматирования различается для разных типов карточек, а отображение карты может незначительно отличаться между настольным компьютером и мобильными клиентами Teams, а также с Teams в браузере настольного компьютера.

Встроенное изображение можно добавить с помощью любой карточки Teams. Изображения в формате "  `.png` ," `.jpg` или " `.gif` файлы" не должны превышать 1024 × 1024 px или 1 МБ. Анимированный GIF-файл не поддерживается официально. *См* . [Справочник по карточкам](./cards-reference.md#inline-card-images)

## <a name="formatting-cards-with-markdown"></a>Форматирование карточек с помощью Markdown

Существует два типа карточек, поддерживающих Markdown в teams:

> [!div class="checklist"]
> * **Адаптивные карты**: Markdown поддерживается в поле адаптивной карточки `Textblock` , а также `Fact.Title` и `Fact.Value` . HTML не поддерживается в адаптивных картах.
> * **Соединительные карты O365**: Markdown и ограниченный HTML-код поддерживаются в карточках соединителей Office 365 в текстовых полях.

# <a name="markdown-formatting-adaptive-cards"></a>[**Форматирование Markdown: адаптивные карты**](#tab/adaptive-md)

 Поддерживаются следующие стили `Textblock` `Fact.Title` `Fact.Value` :

| Style | Пример | Markdown |
| --- | --- | --- |
| bold | **Bold** | ```**Bold**``` |
| italic | _Italic_ | ```_Italic_``` |
| неупорядоченный список | <ul><li>текст</li><li>текст</li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| упорядоченный список | <ol><li>текст</li><li>текст</li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| Гиперссылки |[Bing](https://www.bing.com/)| ```[Title](url)``` |

Следующие теги Markdown не поддерживаются:

* Заголовки
* Таблицы
* Изображения
* Предварительно отформатированный текст
* блокккуотес

> [!IMPORTANT]
> Адаптивные карты не поддерживают форматирование HTML.

### <a name="newlines-for-adaptive-cards"></a>Строки для адаптивных карточек

В списках можно использовать `\r` `\n` последовательности или escape-последовательности для новой строки. Использование `\n\n` в списке приводит к тому, что следующий элемент в списке будет иметь отступы. Если в элементе TextBlock требуются строки новой строки, используйте `\n\n` .

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a>Различия между мобильными и настольными компьютерами для адаптивных карт

Форматирование слегка отличается между настольными и мобильными версиями Teams.

На рабочем столе Адаптивное форматирование карточки Markdown выглядит так же, как в веб-браузерах и в клиентском приложении teams:

![Адаптивное форматирование карточки Markdown в клиенте для настольных ПК](../../assets/images/cards/Adaptive-markdown-desktop-client.png)

В iOS форматирование адаптивной карточки Markdown выглядит следующим образом:

![Адаптивное форматирование карточки Markdown в iOS](../../assets/images/cards/Adaptive-markdown-iOS-75.png)

В Android Адаптивное форматирование карточки Markdown выглядит следующим образом:

![Адаптивное форматирование карточки Markdown в Android](../../assets/images/cards/Adaptive-markdown-Android.png)

### <a name="more-information-on-adaptive-cards"></a>Дополнительные сведения о адаптивных картах

[Функции для текста в адаптивных карточках](/adaptive-cards/create/textfeatures) Функции даты и локализации, упомянутые в этом разделе, не поддерживаются в Teams.

### <a name="formatting-sample-for-adaptive-cards"></a>Пример форматирования для адаптивных карточек

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

### <a name="mention-support-within-adaptive-cards-v12"></a>Упоминание поддержки в адаптивных картах версии 1.2

Упоминания на основе карточек поддерживаются в веб-, настольных и мобильных клиентах. Вы можете добавлять @ упоминания в тексте адаптивной карточки для Боты и расширений обмена сообщениями.  Чтобы добавить @ упоминания в карточки, следуйте той же логике уведомлений и отрисовки, что и [в упомянутых сообщениях в беседах канала и группового чата](../../bots/how-to/conversations/channel-and-group-conversations.md#working-with-mentions ).

Расширения Боты и обмена сообщениями могут включать упоминание в содержимом карточки в элементах [TextBlock](https://adaptivecards.io/explorer/TextBlock.html) и в элементах [фактов](https://adaptivecards.io/explorer/FactSet.html) .

> [!NOTE]
> * В настоящее время [элементы мультимедиа](https://adaptivecards.io/explorer/Media.html) в настоящее время не поддерживаются в адаптивных картах версии 1.2 на платформе Teams.
> * Упоминание каналов & участников группы не поддерживаются в сообщениях Bot.

### <a name="constructing-mentions"></a>Создание упоминаний

Чтобы включить в адаптивную карточку упоминание, необходимо, чтобы приложение включало следующие элементы:

* `<at>username</at>` в поддерживаемых элементах адаптивной карточки
* `mention`Объект внутри `msteams` свойства в содержимом карточки, включающий идентификатор пользователя Teams для указанного пользователя.

### <a name="sample-adaptive-card-with-a-mention"></a>Пример адаптивной карточки с упоминанием

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

# <a name="markdown-formatting-o365-connector-cards"></a>[**Форматирование Markdown: карты соединителей O365**](#tab/connector-md)

Карты соединителей поддерживают ограниченные Markdown и форматирование HTML. Поддержка HTML описана в предыдущем разделе.

| Style | Пример | Markdown |
| --- | --- | --- |
| bold | **text** | `**text**` |
| italic | *text* | `*text*` |
| Верхний колонтитул (уровни 1 &ndash; 3) | **Text** | `### Text`|
| strikethrough | ~~text~~ | `~~text~~` |
| неупорядоченный список | <ul><li>текст</li><li>текст</li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| упорядоченный список | <ol><li>текст</li><li>текст</li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| предварительно отформатированный текст | `text` | ``preformatted text`` |
| blockquote | >текст блокккуоте | `>blockquote text` |
| гиперссылка | [Bing](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| Ссылка на изображение |![Дукк на рок](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

В соединителях соединителей отображаются строки `\n\n` , но не for `\n` или `\r` .

### <a name="mobile-and-desktop-differences-for-connector-cards-using-markdown"></a>Различия между мобильными и рабочими столами для соединителей карт с помощью Markdown

На рабочем столе Markdown форматирование карт для соединителей выглядит следующим образом:

![Markdown форматирование карт подключателя в клиенте для настольных ПК](../../assets/images/cards/connector-desktop-markdown-combined.png)

В iOS форматирование Markdown для карт подключателя выглядит следующим образом:

![Markdown форматирование карт подключателя в клиенте iOS](../../assets/images/cards/connector-iphone-markdown-combined-80.png)

Вопросы:

* Клиент iOS для Teams не отображает Markdown или встроенные изображения HTML в соединительных картах.
* Блокккуотес отображаются с отступом, но без серого фона.

На Android Markdown форматирование карт для соединителей выглядит следующим образом:

![Markdown форматирование карт подключателя в клиенте Android](../../assets/images/cards/connector-android-markdown-combined.png)

### <a name="formatting-example-for-markdown-connector-cards"></a>Пример форматирования для карточек соединителей Markdown

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

## <a name="formatting-cards-with-html"></a>Форматирование карточек с помощью HTML

# <a name="html-formatting-o365-connector-cards"></a>[**Форматирование HTML: карты соединителей O365**](#tab/connector-html)

Карты соединителей поддерживают ограниченные Markdown и форматирование HTML. Markdown описывается в следующем разделе.

| Style | Пример | HTML |
| --- | --- | --- |
| bold | **text** | `<strong>text</strong>` |
| italic | *text* | `<em>text</em>` |
| Верхний колонтитул (уровни 1 &ndash; 3) | **Text** | `<h3>Text</h3>` |
| strikethrough | ~~text~~ | `<strike>text</strike>` |
| неупорядоченный список | <ul><li>текст</li><li>текст</li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| упорядоченный список | <ol><li>текст</li><li>текст</li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| предварительно отформатированный текст | `text` | `<pre>text</pre>` |
| blockquote | <blockquote>текст</blockquote> | `<blockquote>text</blockquote>` |
| гиперссылка | [Bing](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| Ссылка на изображение | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

В соединительных карточках строки новой строки отображаются в HTML-коде с помощью `<p>` тега.

### <a name="mobile-and-desktop-differences-for-connector-cards-using-html"></a>Различия между мобильными и рабочими столами для соединителей карт с помощью HTML

На рабочем столе форматирование HTML-карт для соединителей выглядит следующим образом:

![Формат HTML для соединителей карт в клиенте для настольных ПК](../../assets/images/cards/Connector-desktop-html-combined.png)

В iOS форматирование HTML выглядит следующим образом:

![Формат HTML для соединителей карт в клиенте iOS](../../assets/images/cards/connector-iphone-html-combined-80.png)

Вопросы:

* Встроенные изображения не отправляются на iOS с помощью Markdown или HTML в соединительных карточках.
* Предварительно отформатированный текст отображается, но не является серым фоном.

На Android форматирование HTML выглядит следующим образом:

![Форматирование HTML-карт для соединителей в клиенте Android](../../assets/images/cards/connector-android-html-combined.png)

### <a name="formatting-sample-for-html-connector-cards"></a>Пример форматирования для карточек соединителей HTML

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

# <a name="html-formatting-hero-and-thumbnail-cards"></a>[**HTML-форматирование: карточки главный Имиджевый баннер и эскиза**](#tab/simple-html)

Теги HTML поддерживаются для простых карточек, таких как карта главный Имиджевый баннер и эскиза. Markdown не поддерживается.

| Style | Пример | HTML |
| --- | --- | --- |
| bold | **text** | `<strong>text</strong>` |
| italic | *text* | `<em>text</em>` |
| Верхний колонтитул (уровни 1 &ndash; 3) | **Text** | `<h3>Text</h3>` |
| strikethrough | ~~text~~ | `<strike>text</strike>` |
| неупорядоченный список | <ul><li>текст</li><li>текст</li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| упорядоченный список | <ol><li>текст</li><li>текст</li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| предварительно отформатированный текст | `text` | `<pre>text</pre>` |
| blockquote | <blockquote>текст</blockquote> | `<blockquote>text</blockquote>` |
| гиперссылка | [Bing](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| Ссылка на изображение |<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a>Различия между мобильными и рабочими столами для простых карточек

Из-за различий в разрешениях между настольными и мобильными платформами форматирование различается для настольных ПК и мобильных версий Teams.

На настольном компьютере форматирование HTML выглядит следующим образом:

![Форматирование HTML в клиенте для настольных ПК](../../assets/images/cards/card-formatting-xml-desktop-v2.png)

В iOS форматирование HTML выглядит следующим образом:

![Форматирование HTML в клиенте iOS](../../assets/images/cards/card-formatting-xml-mobile-v2.png)

Вопросы:

* Форматирование символов, например полужирный шрифт и курсив, не отображается в iOS.

На Android форматирование HTML выглядит следующим образом:

![Форматирование HTML в клиенте Android](../../assets/images/cards/card-formatting-xml-android-60.png)

Правильное форматирование знаков, как полужирное и курсивное отображение на Android.

### <a name="formatting-sample-for-html-formatting-in-simple-cards"></a>Пример форматирования форматирования HTML на простых карточках

Эти снимки создаются с помощью Teams Аппстудио, где для свойства Text карточки главный Имиджевый баннер задано значение, равное следующей строке. Вы можете проверить форматирование в собственных карточках, изменив этот код.

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"https://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`

---
