---
title: Форматирование текста в карточках
description: Описание форматирования текста карточки в Microsoft Teams
keywords: формат карточек Боты Teams
ms.date: 03/29/2018
ms.openlocfilehash: 4a467c5b0b21cc3c19977bf7caa25e6790904b10
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675609"
---
# <a name="card-formatting"></a>Форматирование карточки

В зависимости от типа карты в карточки можно добавлять форматированный текст в карточки с помощью Markdown или HTML.

Карточки поддерживают форматирование только в свойстве Text, а не в свойствах Title и субтитров. Форматирование можно указать с помощью подмножества форматирования XML (HTML) или Markdown в зависимости от типа карты. Для текущих приложений AMD в будущем рекомендуется использовать форматирование Markdown.

Поддержка форматирования различается для разных типов карточек, а отображение карты может незначительно отличаться между настольным компьютером и мобильными клиентами Teams, а также с Teams в браузере настольного компьютера.

## <a name="card-types"></a>Типы карточек

Существует три типа карт, поддерживающих Markdown в teams:

* **Адаптивные карты**: Markdown поддерживается в поле адаптивной карточки `Textblock` , а также `Fact.Title` и `Fact.Value`. HTML не поддерживается в адаптивных картах.
* **Соединительные карты O365**: Markdown и ограниченный HTML-код поддерживаются в карточках соединителей Office 365 в текстовых полях.
* **Простые карты**: ограниченный HTML-код поддерживается, но Markdown не поддерживается на простых карточках.

## <a name="markdown-formatting-for-adaptive-cards"></a>Markdown форматирование для адаптивных карточек

 Поддерживаются следующие стили `Textblock` `Fact.Title` `Fact.Value` :

| Стиль | Пример | Markdown |
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

Адаптивные карточки не поддерживают форматирование HTML.

### <a name="newlines-for-adaptive-cards"></a>Строки для адаптивных карточек

В списках можно использовать последовательности `\r` или `\n` escape-последовательности для новой строки. Использование `\n\n` в списке приводит к тому, что следующий элемент в списке будет иметь отступы. Если в элементе TextBlock требуются строки новой строки, используйте `\n\n`.

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a>Различия между мобильными и настольными компьютерами для адаптивных карт

Форматирование слегка отличается между настольными и мобильными версиями Teams.

На рабочем столе Адаптивное форматирование карточки Markdown выглядит так же, как в веб-браузерах и в клиентском приложении teams:

![Адаптивное форматирование карточки Markdown в клиенте для настольных ПК](~/assets/images/cards/Adaptive-markdown-desktop-client.png)

В iOS форматирование адаптивной карточки Markdown выглядит следующим образом:

![Адаптивное форматирование карточки Markdown в iOS](~/assets/images/cards/Adaptive-markdown-iOS-75.png)

В Android Адаптивное форматирование карточки Markdown выглядит следующим образом:

![Адаптивное форматирование карточки Markdown в Android](~/assets/images/cards/Adaptive-markdown-Android.png)

### <a name="for-more-information-on-adaptive-cards"></a>Дополнительные сведения о адаптивных картах

[Функции для текста в адаптивных карточках](/adaptive-cards/create/textfeatures) Функции даты и локализации, упомянутые в этом разделе, не поддерживаются в Teams.

### <a name="formatting-sample-for-adaptive-cards"></a>Пример форматирования для адаптивных карточек

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
## <a name="mention-support-within-adaptive-cards"></a>Упоминание поддержки в адаптивных картах 

> [!NOTE]
> Упоминание поддержки в карточках в настоящее время поддерживается только в [режиме предварительного просмотра разработчика](~/resources/dev-preview/developer-preview-intro) .

Теперь расширения Боты и обмена сообщениями могут включать упоминания в содержимом карточки в элементах text и Block. 

### <a name="constructing-mentions"></a>Создание упоминаний
Чтобы включить в адаптивную карточку упоминание, необходимо, чтобы приложение включало следующие элементы:

* `<at>username</at>`в поддерживаемых элементах адаптивной карточки
* `mention` Объект внутри `msteams` свойства в содержимом карточки, включающий идентификатор пользователя Teams для указанного пользователя.

Обратите внимание, что карточки со упоминанием в мобильных клиентах в настоящее время не поддерживаются.

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

## <a name="html-formatting-for-connector-cards"></a>Формат HTML для соединителей карт

Карты соединителей поддерживают ограниченные Markdown и форматирование HTML. Markdown описывается в следующем разделе.

| Стиль | Пример | HTML |
| --- | --- | --- |
| bold | **text** | `<strong>text</strong>` |
| italic | *text* | `<em>text</em>` |
| Верхний колонтитул (уровни&ndash;1 3) | **Text** | `<h3>Text</h3>` |
| strikethrough | ~~text~~ | `<strike>text</strike>` |
| неупорядоченный список | <ul><li>текст</li><li>текст</li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| упорядоченный список | <ol><li>текст</li><li>текст</li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| предварительно отформатированный текст | `text` | `<pre>text</pre>` |
| blockquote | <blockquote>текст</blockquote> | `<blockquote>text</blockquote>` |
| гиперссылка | [Bing](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| Ссылка на изображение | <img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

В соединительных карточках строки новой строки отображаются в HTML- `<p>` коде с помощью тега.

### <a name="mobile-and-desktop-differences-for-connector-cards-using-html"></a>Различия между мобильными и рабочими столами для соединителей карт с помощью HTML

На рабочем столе форматирование HTML-карт для соединителей выглядит следующим образом:

![Формат HTML для соединителей карт в клиенте для настольных ПК](~/assets/images/cards/Connector-desktop-html-combined.png)

В iOS форматирование HTML выглядит следующим образом:

![Формат HTML для соединителей карт в клиенте iOS](~/assets/images/cards/connector-iphone-html-combined-80.png)

Вопросы:

* Встроенные изображения не отправляются на iOS с помощью Markdown или HTML в соединительных карточках.
* Предварительно отформатированный текст отображается, но не является серым фоном.

На Android форматирование HTML выглядит следующим образом:

![Форматирование HTML-карт для соединителей в клиенте Android](~/assets/images/cards/connector-android-html-combined.png)

### <a name="formatting-sample-for-html-connector-cards"></a>Пример форматирования для карточек соединителей HTML

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

## <a name="markdown-formatting-for-connector-cards"></a>Markdown форматирование карт подключателя

Карты соединителей поддерживают ограниченные Markdown и форматирование HTML. КОД HTML описывается в последнем разделе.

| Стиль | Пример | Markdown |
| --- | --- | --- |
| bold | **text** | `**text**` |
| italic | *text* | `*text*` |
| Верхний колонтитул (уровни&ndash;1 3) | **Text** | `### Text`|
| strikethrough | ~~text~~ | `~~text~~` |
| неупорядоченный список | <ul><li>текст</li><li>текст</li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| упорядоченный список | <ol><li>текст</li><li>текст</li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| предварительно отформатированный текст | `text` | ``preformatted text`` |
| blockquote | >текст блокккуоте | `>blockquote text` |
| гиперссылка | [Bing](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| Ссылка на изображение |![Дукк на рок](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

В соединителях соединителей отображаются строки `\n\n`, но не for `\n` или. `\r`

### <a name="mobile-and-desktop-differences-for-connector-cards-using-markdown"></a>Различия между мобильными и рабочими столами для соединителей карт с помощью Markdown

На рабочем столе Markdown форматирование карт для соединителей выглядит следующим образом:

![Формат HTML для соединителей карт в клиенте для настольных ПК](~/assets/images/cards/connector-desktop-markdown-combined.png)

В iOS форматирование Markdown для карт подключателя выглядит следующим образом:

![Формат HTML для соединителей карт в клиенте iOS](~/assets/images/cards/connector-iphone-markdown-combined-80.png)

Вопросы:

* Клиент iOS для Teams не отображает Markdown или встроенные изображения HTML в соединительных картах.
* Блокккуотес отображаются с отступом, но без серого фона.

На Android Markdown форматирование карт для соединителей выглядит следующим образом:

![Форматирование HTML-карт для соединителей в клиенте Android](~/assets/images/cards/connector-android-markdown-combined.png)

### <a name="formatting-example-for-markdown-connector-cards"></a>Пример форматирования для карточек соединителей Markdown

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

## <a name="html-formatting-for-simple-cards"></a>Форматирование HTML для простых карточек

Эти теги HTML поддерживаются для простых карточек, таких как карта главный Имиджевый баннер и эскиза. Markdown не поддерживается.

| Стиль | Пример | HTML |
| --- | --- | --- |
| bold | **text** | `<strong>text</strong>` |
| italic | *text* | `<em>text</em>` |
| Верхний колонтитул (уровни&ndash;1 3) | **Text** | `<h3>Text</h3>` |
| strikethrough | ~~text~~ | `<strike>text</strike>` |
| неупорядоченный список | <ul><li>текст</li><li>текст</li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| упорядоченный список | <ol><li>текст</li><li>текст</li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| предварительно отформатированный текст | `text` | `<pre>text</pre>` |
| blockquote | <blockquote>текст</blockquote> | `<blockquote>text</blockquote>` |
| гиперссылка | [Bing](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| Ссылка на изображение |<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a>Различия между мобильными и рабочими столами для простых карточек

Из-за различий в разрешениях между настольными и мобильными платформами форматирование различается для настольных ПК и мобильных версий Teams.

На настольном компьютере форматирование HTML выглядит следующим образом:

![Форматирование HTML в клиенте для настольных ПК](~/assets/images/cards/card-formatting-xml-desktop-v2.png)

В iOS форматирование HTML выглядит следующим образом:

![Форматирование HTML в клиенте iOS](~/assets/images/cards/card-formatting-xml-mobile-v2.png)

Вопросы:

* Форматирование символов, например полужирный шрифт и курсив, не отображается в iOS.

На Android форматирование HTML выглядит следующим образом:

![Форматирование HTML в клиенте Android](~/assets/images/cards/card-formatting-xml-android-60.png)

Правильное форматирование знаков, как полужирное и курсивное отображение на Android.

### <a name="formatting-sample-for-html-formatting-in-simple-cards"></a>Пример форматирования форматирования HTML на простых карточках

Эти снимки создаются с помощью Teams Аппстудио, где для свойства Text карточки главный Имиджевый баннер задано значение, равное следующей строке. Вы можете проверить форматирование в собственных карточках, изменив этот код.

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"http://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`
