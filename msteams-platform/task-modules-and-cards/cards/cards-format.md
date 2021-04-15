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
# <a name="format-cards-in-teams"></a>Формат карт в Teams

В зависимости от типа карты можно добавить в карты форматирование текста с помощью Markdown или HTML.

Карточки поддерживают форматирование только в свойстве текста, а не в свойствах заголовка или субтитров. Форматирование можно задать с помощью подмножество форматирования XML (HTML) или Markdown в зависимости от типа карты. Для текущих и будущих карт разработки рекомендуется использовать форматирование Markdown.

Поддержка форматирования отличается между различными типами карт, а отрисовка карты может незначительно отличаться между настольным компьютером и клиентами мобильных групп, а также Teams в браузере настольных компьютеров.

Вы можете включить inline-изображение с любой картой Teams. Изображения форматированы как , или файлы и не должны превышать  `.png` `.jpg` `.gif` 1024 ×1024 px или 1 МБ. Анимированный GIF не поддерживается официально. *См.* [ссылку На карточки](./cards-reference.md#inline-card-images)

## <a name="formatting-cards-with-markdown"></a>Форматирование карт с помощью Markdown

Существует два типа карт, поддерживаюных Markdown в Teams:

> [!div class="checklist"]
> * **Адаптивные карты:** Markdown поддерживается в поле адаптивных карт, а `Textblock` также и `Fact.Title` `Fact.Value` . HTML не поддерживается в адаптивных картах.
> * **Карты соединителя O365:** Markdown и ограниченный HTML поддерживаются в карточках Соединитель Office 365 в текстовых полях.

# <a name="markdown-formatting-adaptive-cards"></a>[**Форматирование разметки: адаптивные карты**](#tab/adaptive-md)

 Поддерживаемые стили `Textblock` для и `Fact.Title` `Fact.Value` являются:

| Style | Пример | Markdown |
| --- | --- | --- |
| bold | **Bold** | ```**Bold**``` |
| italic | _Italic_ | ```_Italic_``` |
| необученный список | <ul><li>текст</li><li>текст</li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| упорядоченный список | <ol><li>текст</li><li>текст</li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| Гиперссылки |[Bing](https://www.bing.com/)| ```[Title](url)``` |

Следующие теги Markdown не поддерживаются:

* Заголовки
* Таблицы
* изображения;
* Предформатированный текст
* Blockquotes

> [!IMPORTANT]
> Адаптивные карты не поддерживают форматирование HTML.

### <a name="newlines-for-adaptive-cards"></a>Newlines для адаптивных карт

В списках можно использовать `\r` последовательности `\n` или последовательности побега для newlines. Использование в списке приведет к отступам следующего элемента `\n\n` в списке. Если вам нужны новые линии в другом месте в текстовом блокпосте, используйте `\n\n` .

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a>Различия для мобильных и настольных компьютеров для адаптивных карт

Форматирование несколько отличается от рабочего стола к мобильным версиям Teams.

На рабочем столе форматирование разметки адаптивной карты выглядит так как в веб-браузерах, так и в клиентском приложении Teams:

![Форматирование разметки адаптивной карты в клиенте рабочего стола](../../assets/images/cards/Adaptive-markdown-desktop-client.png)

В iOS форматирование разметки адаптивной карты выглядит так:

![Форматирование разметки адаптивной карты в iOS](../../assets/images/cards/Adaptive-markdown-iOS-75.png)

На Android форматирование разметки адаптивной карты выглядит так:

![Форматирование разметки адаптивной карты в Android](../../assets/images/cards/Adaptive-markdown-Android.png)

### <a name="more-information-on-adaptive-cards"></a>Дополнительные сведения о адаптивных картах

[Текстовые функции в адаптивных картах](/adaptive-cards/create/textfeatures) Функции даты и локализации, упомянутые в этой теме, не поддерживаются в Teams.

### <a name="formatting-sample-for-adaptive-cards"></a>Пример форматирования для адаптивных карт

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

### <a name="mention-support-within-adaptive-cards-v12"></a>Упоминание поддержки в адаптивных картах v1.2

Упоминания на основе карт поддерживаются в веб-, настольных и мобильных клиентах. Вы можете добавить @ упоминания в тексте адаптивной карты для ботов и ответов на расширение обмена сообщениями. Чтобы добавить @mentions in cards, следуйте той же логике уведомлений и визуализации, что и упоминания на основе сообщений в беседах в чатах каналов и [групп.](../../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions)

Боты и расширения обмена сообщениями могут включать упоминания в контенте карты в [элементах TextBlock](https://adaptivecards.io/explorer/TextBlock.html) и [FactSet.](https://adaptivecards.io/explorer/FactSet.html)

> [!NOTE]
> * [Элементы мультимедиа в](https://adaptivecards.io/explorer/Media.html) настоящее время не поддерживаются в адаптивных картах v1.2 на платформе Teams.
> * Упоминания & группы не поддерживаются в сообщениях ботов.

#### <a name="constructing-mentions"></a>Построение упоминаний

Чтобы включить упоминание в адаптивной карте, приложение должно включить следующие элементы

* `<at>username</at>` в поддерживаемых элементах адаптивной карты
* Объект внутри свойства в содержимом карты, который включает пользовательский `mention` `msteams` id Teams упоминаемого пользователя

#### <a name="sample-adaptive-card-with-a-mention"></a>Пример адаптивной карты с упоминанием

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


### <a name="information-masking-in-adaptive-cards"></a>Маскировка сведений в адаптивных картах
Используйте свойство маскировки информации для маскировки определенных сведений, таких как пароль или конфиденциальные сведения пользователей в элементе ввода адаптивной [`Input.Text`](https://adaptivecards.io/explorer/Input.Text.html) карты. 

> [!NOTE]
> Эта функция поддерживает только маскировку стороной клиента, текст ввода в маске отправляется в виде четкого текста на адрес конечной точки https, заданный во время [конфигурации бота.](../../build-your-first-app/build-bot.md#4-configure-your-bot) 

> [!NOTE]
> Свойство маскировки информации в настоящее время доступно только в предварительном просмотре разработчика.

Чтобы скрыть сведения в адаптивных картах, добавьте свойство введите и установите `isMasked`  `Input.Text` значение true. 

#### <a name="sample-adaptive-card-with-masking-property"></a>Пример адаптивной карты с свойством маскировки

```json
{
    "type": "Input.Text",
    "id": "secretThing",
    "style": "password",
    "isMasked": true
  },
```

Ниже приводится пример маскировки сведений в адаптивных картах:

![Маскировка информационного изображения](../../assets/images/cards/masking-information-view.png)

### <a name="full-width-adaptive-card"></a>Адаптивная карта с полной шириной
Свойство можно использовать для расширения ширины адаптивной карты и использования `msteams` дополнительного пространства холста. Сведения об использовании свойства см. в следующем примере:

#### <a name="constructing-full-width-cards"></a>Построение карт полной ширины
Чтобы сделать полную ширину адаптивной карты, объект в свойстве контента карточки `width` `msteams` должен быть задат. `Full`
Кроме того, приложение должно включать следующие элементы:

#### <a name="sample-adaptive-card-with-full-width"></a>Пример адаптивной карты с полной шириной

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

Адаптивная карта с полной шириной отображается следующим образом: представление адаптивной карты полной ![ ширины](../../assets/images/cards/full-width-adaptive-card.png)

Если свойство не настроено до полного, представление адаптивной карты по умолчанию следующим образом: представление адаптивной карты малой `width`  ![ ширины](../../assets/images/cards/small-width-adaptive-card.png)

### <a name="typeahead-support"></a>Поддержка typeahead

В элементе схемы запрос на фильтрацию и выбор большого количества вариантов может значительно замедлить [`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) выполнение задач. Поддержка ввода в адаптивных картах может упростить выбор входных данных, сужая или фильтруя набор вариантов ввода при вводе ввода пользователем. 

#### <a name="enable-typeahead-in-adaptive-cards"></a>Включить введите в адаптивных картах

Чтобы включить введите в `Input.Choiceset` наборе, `style` чтобы `filtered` и `isMultiSelect` убедиться, установлено `false` . 

#### <a name="sample-adaptive-card-with-typeahead-support"></a>Пример адаптивной карты с поддержкой typeahead

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

### <a name="stage-view-for-images-in-adaptive-cards"></a>Представление сцены для изображений в адаптивных картах

> [!NOTE]
> В настоящее время эта функция доступна только в предварительном просмотре разработчика.
 
В адаптивной карте свойство можно использовать для выборочного отображения изображений в представлении `msteams` сцены. Когда пользователи наведите курсор над изображениями, они увидят значок расширения, для которого установлен `allowExpand` атрибут `true` . Сведения об использовании свойства см. в следующем примере:

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

Когда пользователи наведите курсор над изображением, в правом верхнем углу изображения появляется значок расширения: адаптивная карта ![ с расширяемым изображением](../../assets/images/cards/adaptivecard-hover-expand-icon.png)

Изображение отображается в представлении сцены, когда пользователь выбирает кнопку расширения: ![ изображение расширено до представления сцены](../../assets/images/cards/adaptivecard-expand-image.png)

В представлении сцены пользователи могут масштабировать изображение и увеличивать его. Вы можете выбрать, какие изображения в адаптивной карте должны иметь эту возможность.

> [!NOTE]
> Возможность масштабирования и масштабирования применяется только к элементам изображения (тип изображения) в адаптивной карте.

> [!NOTE]
> Для мобильных приложений Teams функции представления этапов для изображений в адаптивных картах доступны по умолчанию, и пользователи смогут просматривать адаптивные изображения карт в стадии представления, просто нажав на изображение, независимо от того, присутствует атрибут или `allowExpand` нет.

# <a name="markdown-formatting-o365-connector-cards"></a>[**Форматирование разметки: карты соединителения O365**](#tab/connector-md)

Карты Connector поддерживают ограниченное форматирование Markdown и HTML. Поддержка HTML описана в последнем разделе.

| Style | Пример | Markdown |
| --- | --- | --- |
| bold | **text** | `**text**` |
| italic | *text* | `*text*` |
| загон (уровни 1 &ndash; 3) | **Text** | `### Text`|
| strikethrough | ~~text~~ | `~~text~~` |
| необученный список | <ul><li>текст</li><li>текст</li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| упорядоченный список | <ol><li>текст</li><li>текст</li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| предформатированный текст | `text` | ``preformatted text`` |
| blockquote | >блокквойта | `>blockquote text` |
| гиперссылка | [Bing](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| ссылка на изображение |![Утка на скале](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

В соединитеных картах новые линии отрисовываются для `\n\n` , но не для или `\n` `\r` .

### <a name="mobile-and-desktop-differences-for-connector-cards-using-markdown"></a>Различия для мобильных и настольных компьютеров для соединительная карта с помощью Markdown

На рабочем столе форматирование Markdown для карт соединительная система выглядит так:

![Форматирование разметки для соединительная карта в клиенте Desktop](../../assets/images/cards/connector-desktop-markdown-combined.png)

В iOS форматирование markdown для соединители-карт выглядит так:

![Форматирование markdown для карт соединителения в клиенте iOS](../../assets/images/cards/connector-iphone-markdown-combined-80.png)

Вопросы:

* Клиент iOS для Teams не отрисовывает встроенные изображения Markdown или HTML в соединительных картах.
* Блокквоты отрисовываются как отступные, но без серого фона.

На Android форматирование markdown для карт соединителения выглядит так:

![Форматирование разметки для карт соединителения в клиенте Android](../../assets/images/cards/connector-android-markdown-combined.png)

### <a name="formatting-example-for-markdown-connector-cards"></a>Пример форматирования карт соединителения Markdown

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

## <a name="formatting-cards-with-html"></a>Форматирование карт с ПОМОЩЬЮ HTML

# <a name="html-formatting-o365-connector-cards"></a>[**Форматирование HTML: карты соединителя O365**](#tab/connector-html)

Карты Connector поддерживают ограниченное форматирование Markdown и HTML. Markdown описан в следующем разделе.

| Style | Пример | HTML |
| --- | --- | --- |
| bold | **text** | `<strong>text</strong>` |
| italic | *text* | `<em>text</em>` |
| загон (уровни 1 &ndash; 3) | **Text** | `<h3>Text</h3>` |
| strikethrough | ~~text~~ | `<strike>text</strike>` |
| необученный список | <ul><li>текст</li><li>текст</li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| упорядоченный список | <ol><li>текст</li><li>текст</li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| предформатированный текст | `text` | `<pre>text</pre>` |
| blockquote | <blockquote>текст</blockquote> | `<blockquote>text</blockquote>` |
| гиперссылка | [Bing](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| ссылка на изображение | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

В соединительных картах новые линии отрисовываются в HTML с помощью `<p>` тега.

### <a name="mobile-and-desktop-differences-for-connector-cards-using-html"></a>Различия между мобильными и настольными устройствами для соединительная карта с помощью HTML

Форматирование HTML-форматов для соединительная карточки на рабочем столе выглядит так:

![ФОРМАТирование HTML для соединителя карт в клиенте Desktop](../../assets/images/cards/Connector-desktop-html-combined.png)

В iOS форматирование HTML выглядит так:

![Форматирование HTML для соединительных карт в клиенте iOS](../../assets/images/cards/connector-iphone-html-combined-80.png)

Вопросы:

* Встроенные изображения не отрисовываются в iOS с помощью markdown или HTML-кодов в соединителях.
* Предформатированный текст отрисовывается, но не имеет серого фона.

На Android форматирование HTML выглядит так:

![Форматирование HTML для соединительных карт в клиенте Android](../../assets/images/cards/connector-android-html-combined.png)

### <a name="formatting-sample-for-html-connector-cards"></a>Пример форматирования для HTML-карт соединителя

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

# <a name="html-formatting-hero-and-thumbnail-cards"></a>[**Форматирование HTML: карты героя и эскиза**](#tab/simple-html)

HTML-теги поддерживаются для простых карт, таких как карта героя и эскиза. Markdown не поддерживается.

| Style | Пример | HTML |
| --- | --- | --- |
| bold | **text** | `<strong>text</strong>` |
| italic | *text* | `<em>text</em>` |
| загон (уровни 1 &ndash; 3) | **Text** | `<h3>Text</h3>` |
| strikethrough | ~~text~~ | `<strike>text</strike>` |
| необученный список | <ul><li>текст</li><li>текст</li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| упорядоченный список | <ol><li>текст</li><li>текст</li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| предформатированный текст | `text` | `<pre>text</pre>` |
| blockquote | <blockquote>текст</blockquote> | `<blockquote>text</blockquote>` |
| гиперссылка | [Bing](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| ссылка на изображение |<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a>Различия для мобильных и настольных компьютеров для простых карт

Из-за различий в разрешении между настольной и мобильной платформами форматирование отличается между настольным компьютером и мобильной версией Teams.

На рабочем столе форматирование HTML выглядит так:

![Форматирование HTML в клиенте Desktop](../../assets/images/cards/card-formatting-xml-desktop-v2.png)

На iOS форматирование HTML выглядит так:

![Форматирование HTML в клиенте iOS](../../assets/images/cards/card-formatting-xml-mobile-v2.png)

Вопросы:

* Форматирование символов, как смелый и italic, не отрисовка в iOS.

На Android форматирование HTML выглядит так:

![Форматирование HTML в клиенте Android](../../assets/images/cards/card-formatting-xml-android-60.png)

Форматирование символов, как смелый и italic отображения правильно на Android.

### <a name="formatting-sample-for-html-formatting-in-simple-cards"></a>Пример форматирования форматирования HTML в простых картах

Эти скриншоты были созданы с помощью Teams AppStudio, где текстовое свойство карты-героя было задано следующей строке. Вы можете протестировать форматирование в собственных картах, изменяя этот код.

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"https://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`

---
