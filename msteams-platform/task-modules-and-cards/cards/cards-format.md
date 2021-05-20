---
title: Форматирование текста в картах
description: Описывает форматирование текста карты в Microsoft Teams
keywords: формат карт команд ботов
localization_priority: Normal
ms.topic: reference
ms.date: 03/29/2018
ms.openlocfilehash: 848656097f2c865705cc0d91dece93049d8c6790
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566586"
---
# <a name="format-cards-in-teams"></a>Форматные карты в Teams

Вы можете добавить богатый текстовый форматирование в карты, используя Либо Markdown или HTML, в зависимости от типа карты.

Карты поддерживают форматирование только в свойстве текста, а не в свойствах заголовка или субтитра. Форматирование может быть указано с помощью подмножества форматирования XML (HTML) или Markdown в зависимости от типа карты. Для текущей и будущей разработки рекомендуются адаптивные карты с использованием форматирования Markdown.

Поддержка форматирования отличается между различными типами карт, и визуализация карты может немного отличаться между настольным и мобильным Teams клиентами, а также Teams в настольном браузере.

Вы можете включить изображение в линию с любой Teams картой. Изображения отформатированы  `.png` как , `.jpg` или `.gif` файлы и не должны превышать 1024 ×1024 px или 1 MB. Анимированный GIF официально не поддерживается. Для получения дополнительной информации [см.](./cards-reference.md#inline-card-images)

## <a name="formatting-cards-with-markdown"></a>Форматирование карт с Markdown

Есть два типа карт, которые поддерживают Markdown в Teams:

> [!div class="checklist"]
> * **Адаптивные** карты : Markdown поддерживается в области `Textblock` адаптивных карт, а также `Fact.Title` `Fact.Value` и . HTML не поддерживается в адаптивных картах.
> * **O365 Connector Cards**: Markdown и ограниченный HTML поддерживается в Office 365-коннекторных карт в текстовых полях.

# <a name="markdown-formatting-adaptive-cards"></a>[**Форматирование разметки: Адаптивные карты**](#tab/adaptive-md)

 Поддерживаемые стили `Textblock` для , и `Fact.Title` `Fact.Value` являются:

| Style | Пример | Markdown |
| --- | --- | --- |
| bold | **Bold** | ```**Bold**``` |
| italic | _Italic_ | ```_Italic_``` |
| неупорядочеченный список | <ul><li>текст</li><li>текст</li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| упорядоченный список | <ol><li>текст</li><li>текст</li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| Гиперссылки |[Bing](https://www.bing.com/)| ```[Title](url)``` |

Следующие теги Markdown не поддерживаются:

* Заголовки
* Таблицы
* изображения;
* Предварительноформированный текст
* Блокциты

> [!IMPORTANT]
> Адаптивные карты не поддерживают форматирование HTML.

### <a name="newlines-for-adaptive-cards"></a>Новые линии для адаптивных карт

В списках вы можете использовать `\r` `\n` последовательности или избежать для новых линий. Использование `\n\n` в списке приведет к отступу следующего элемента в списке. Если вам нужны новые строки в другом месте в текстовом блоке, используйте `\n\n` .

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a>Мобильные и настольные различия для адаптивных карт

Форматирование немного отличается между настольными и мобильными версиями Teams.

На рабочем столе форматирование Adaptive card Markdown выглядит так как в веб-браузерах, так и в Teams клиентском приложении:

![Форматирование адаптивной карты Markdown в настольном клиенте](../../assets/images/cards/Adaptive-markdown-desktop-client.png)

На iOS форматирование Adaptive card Markdown выглядит так:

![Форматирование адаптивной карты Markdown в iOS](../../assets/images/cards/Adaptive-markdown-iOS-75.png)

На Android форматирование Adaptive Card Markdown выглядит так:

![Форматирование адаптивной карты Markdown в Android](../../assets/images/cards/Adaptive-markdown-Android.png)

### <a name="more-information-on-adaptive-cards"></a>Более подробная информация об адаптивных картах

[Текстовые функции в адаптивных картах](/adaptive-cards/create/textfeatures) Упомянутые в этой теме функции даты и локализации не поддерживаются в Teams.

### <a name="formatting-sample-for-adaptive-cards"></a>Образец форматирования для адаптивных карт

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

### <a name="mention-support-within-adaptive-cards-v12"></a>Поддержка упоминания в адаптивных картах v1.2

Упоминания на основе карт поддерживаются в веб-, настольных и мобильных клиентах. Вы можете добавить упоминания в тело адаптивной карты для ботов и ответов на расширение обмена сообщениями. Чтобы добавить упоминания в карты, следуйте той же логике уведомлений и визуализации, что и упоминания на [основе сообщений в разговорах в канале и групповом чате.](../../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions)

Боты и расширения обмена сообщениями могут включать упоминания в содержимом карты в [элементах TextBlock](https://adaptivecards.io/explorer/TextBlock.html) [и FactSet.](https://adaptivecards.io/explorer/FactSet.html)

> [!NOTE]
> * [Медиа-элементы](https://adaptivecards.io/explorer/Media.html) в настоящее время не поддерживаются в адаптивных картах v1.2 Teams платформе.
> * Упоминания & channel & не поддерживаются в сообщениях ботов.

#### <a name="constructing-mentions"></a>Строительство упоминаний

Чтобы включить упоминание в адаптивную карту, приложение должно включить следующие элементы:

* `<at>username</at>` в поддерживаемых адаптивных элементах карты.
* Объект `mention` внутри свойства в `msteams` содержимом карты, который включает в себя Teams идентификатор пользователя, упомянутого.
* Уникальный `userId` для вашего бота ID и конкретного пользователя. Он может быть использован для @mention конкретного пользователя. Можно `userId` получить с помощью одного из вариантов, упомянутых [в получить идентификатор пользователя](/microsoftteams/platform/bots/how-to/conversations/send-proactive-messages?tabs=dotnet#get-the-user-id-team-id-or-channel-id).

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

### <a name="information-masking-in-adaptive-cards"></a>Информационная маскировка в адаптивных картах
Используйте свойство маскировки информации для маскировки определенной информации, такой как пароль или конфиденциальная информация от пользователей в элементе ввода [`Input.Text`](https://adaptivecards.io/explorer/Input.Text.html) адаптивной карты. 

> [!NOTE]
> Функция поддерживает только клиента стороне информации маскировки, в масках входной текст отправляется в качестве четкого текста на https конечной точки адрес, который был указан во время [конфигурации бота](../../build-your-first-app/build-bot.md). 

> [!NOTE]
> Свойство маскировки информации в настоящее время доступно только в предварительном просмотре разработчика.

Чтобы замаскировать информацию в адаптивных картах, `isMasked` добавьте свойство **к типу** `Input.Text` и установите его значение на *истинное.*

#### <a name="sample-adaptive-card-with-masking-property"></a>Пример адаптивной карты с свойством маскировки

```json
{
    "type": "Input.Text",
    "id": "secretThing",
    "style": "password",
    "isMasked": true
  },
```

Следующее изображение является примером маскировки информации в адаптивных картах:

![Маскировка информационного изображения](../../assets/images/cards/masking-information-view.png)

### <a name="full-width-adaptive-card"></a>Адаптивная карта полной ширины
Вы можете использовать `msteams` свойство, чтобы расширить ширину адаптивной карты и использовать дополнительное пространство холста. Для получения информации о том, как использовать свойство, смотрите следующий пример:

#### <a name="constructing-full-width-cards"></a>Построение карт полной ширины
Чтобы сделать полную ширину Адаптивной карты `width` объект `msteams` в свойстве в содержимом карты должны быть установлены `Full` на .
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

Полная ширина Адаптивная карта появляется следующим образом: ![ Полная ширина Адаптивная карта зрения](../../assets/images/cards/full-width-adaptive-card.png)

Если вы еще не установили `width` свойство для *полного*, то по умолчанию вид адаптивной карты заключается в следующем: Малая ![ ширина Адаптивная карта зрения](../../assets/images/cards/small-width-adaptive-card.png)

### <a name="typeahead-support"></a>Поддержка Typeahead

В [`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) элементе схемы запрос пользователей на фильтрацию и выбор через значительное количество вариантов может значительно замедлить завершение задачи. Поддержка Typeahead в адаптивных картах может упростить выбор ввода путем сужения или фильтрации набора входных вариантов при вводе ввода пользователем. 

#### <a name="enable-typeahead-in-adaptive-cards"></a>Включить typeahead в адаптивных картах

Для включения typeahead в `Input.Choiceset` набор и обеспечить установлен на `style` `filtered` `isMultiSelect` `false` . 

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

### <a name="stage-view-for-images-in-adaptive-cards"></a>Вид сцены для изображений в адаптивных картах

> [!NOTE]
> Эта функция в настоящее время доступна только в предварительном просмотре разработчика.
 
В адаптивной карте можно использовать `msteams` свойство, чтобы добавить возможность отображения изображений в виде сцены выборочно. Когда пользователи парят над изображениями, они видят значок расширения, для `allowExpand` которого атрибут установлен `true` на . Для получения информации о том, как использовать свойство, смотрите следующий пример:

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

Когда пользователи парят над изображением, в правом верхнем углу изображения появляется значок расширения: Адаптивная ![ карта с расширяемым изображением](../../assets/images/cards/adaptivecard-hover-expand-icon.png)

Изображение отображается в представлении сцены, когда пользователь выбирает кнопку расширения: ![ Изображение расширено до представления сцены](../../assets/images/cards/adaptivecard-expand-image.png)

В представлении сцены пользователи могут увеличить и увеличить изображение. Вы можете выбрать, какие изображения в вашей адаптивной карте должны иметь эту возможность.

> [!NOTE]
> Возможность увеличения и масштабирования применяется только к элементам изображения (тип изображения) в адаптивной карте.

> [!NOTE]
> Для Teams мобильных приложений функция просмотра сцены для изображений в адаптивных картах доступна по умолчанию, и пользователи смогут просматривать изображения адаптивных карт в режиме стадии просмотра, просто нажав на изображение, `allowExpand` независимо от того, присутствует атрибут или нет.

# <a name="markdown-formatting-o365-connector-cards"></a>[**Форматирование разметки: O365 Коннекторные карты**](#tab/connector-md)

Коннекторные карты поддерживают ограниченное форматирование Markdown и HTML. Поддержка HTML описана в последнем разделе.

| Style | Пример | Markdown |
| --- | --- | --- |
| bold | **text** | `**text**` |
| italic | *text* | `*text*` |
| заголовок (уровни 1 &ndash; 3) | **Text** | `### Text`|
| ударная попере | ~~text~~ | `~~text~~` |
| неупорядочеченный список | <ul><li>текст</li><li>текст</li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| упорядоченный список | <ol><li>текст</li><li>текст</li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| преформатированный текст | `text` | ``preformatted text`` |
| blockquote | >блок-квота | `>blockquote text` |
| гиперссылка | [Bing](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| ссылка на изображение |![Утка на скале](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

В разъемных картах, новые линии отображаются `\n\n` для, но не для `\n` или `\r` .

### <a name="mobile-and-desktop-differences-for-connector-cards-using-markdown"></a>Мобильные и настольные различия для разъемных карт с помощью Markdown

На рабочем столе форматирование Markdown для разъемных карт выглядит так:

![Форматирование разметки для разъемных карт в клиенте Desktop](../../assets/images/cards/connector-desktop-markdown-combined.png)

На iOS форматирование Markdown для разъемных карт выглядит так:

![Форматирование разметки для разъемных карт в клиенте iOS](../../assets/images/cards/connector-iphone-markdown-combined-80.png)

Вопросы:

* Клиент iOS для Teams не отображает Markdown или HTML-изображения в Connector Cards.
* Блокциты отображаются как отступные, но без серого фона.

На Android форматирование Markdown для разъемных карт выглядит так:

![Форматирование разметки для разъемных карт в клиенте Android](../../assets/images/cards/connector-android-markdown-combined.png)

### <a name="formatting-example-for-markdown-connector-cards"></a>Пример форматирования для карт разъема Markdown

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

## <a name="formatting-cards-with-html"></a>Форматирование карт с HTML

# <a name="html-formatting-o365-connector-cards"></a>[**HTML форматирование: O365 Коннекторные карты**](#tab/connector-html)

Коннекторные карты поддерживают ограниченное форматирование Markdown и HTML. Разметка описана в следующем разделе.

| Style | Пример | HTML |
| --- | --- | --- |
| bold | **text** | `<strong>text</strong>` |
| italic | *text* | `<em>text</em>` |
| заголовок (уровни 1 &ndash; 3) | **Text** | `<h3>Text</h3>` |
| ударная попере | ~~text~~ | `<strike>text</strike>` |
| неупорядочеченный список | <ul><li>текст</li><li>текст</li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| упорядоченный список | <ol><li>текст</li><li>текст</li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| преформатированный текст | `text` | `<pre>text</pre>` |
| blockquote | <blockquote>текст</blockquote> | `<blockquote>text</blockquote>` |
| гиперссылка | [Bing](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| ссылка на изображение | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

В разъемных картах новые линии отображаются в HTML с помощью `<p>` тега.

### <a name="mobile-and-desktop-differences-for-connector-cards-using-html"></a>Мобильные и настольные различия для разъемных карт с использованием HTML

На рабочем столе HTML-форматирование для разъемных карт выглядит так:

![HTML форматирование для разъемных карт в клиенте Desktop](../../assets/images/cards/Connector-desktop-html-combined.png)

На iOS форматирование HTML выглядит так:

![HTML форматирование для разъемных карт в клиенте iOS](../../assets/images/cards/connector-iphone-html-combined-80.png)

Вопросы:

* Вколчные изображения не отображаются на iOS с помощью Markdown или HTML в Connector Cards.
* Предварительно отобрабатированный текст отображается, но не имеет серого фона.

На Android форматирование HTML выглядит так:

![HTML форматирование для разъемных карт в клиенте Android](../../assets/images/cards/connector-android-html-combined.png)

### <a name="formatting-sample-for-html-connector-cards"></a>Образец форматирования для HTML-разъемных карт

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

# <a name="html-formatting-hero-and-thumbnail-cards"></a>[**HTML Форматирование: карты героя и эскиза**](#tab/simple-html)

HTML-теги поддерживаются для простых карт, таких как карта героя и эскиза. Разметка не поддерживается.

| Style | Пример | HTML |
| --- | --- | --- |
| bold | **text** | `<strong>text</strong>` |
| italic | *text* | `<em>text</em>` |
| заголовок (уровни 1 &ndash; 3) | **Text** | `<h3>Text</h3>` |
| ударная попере | ~~text~~ | `<strike>text</strike>` |
| неупорядочеченный список | <ul><li>текст</li><li>текст</li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| упорядоченный список | <ol><li>текст</li><li>текст</li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| преформатированный текст | `text` | `<pre>text</pre>` |
| blockquote | <blockquote>текст</blockquote> | `<blockquote>text</blockquote>` |
| гиперссылка | [Bing](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| ссылка на изображение |<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a>Мобильные и настольные различия для простых карт

Из-за различий в разрешении между настольной и мобильной платформой форматирование отличается между настольной и мобильной версией Teams.

На рабочем столе форматирование HTML выглядит так:

![Форматирование HTML в клиенте Desktop](../../assets/images/cards/card-formatting-xml-desktop-v2.png)

На iOS форматирование HTML выглядит так:

![Форматирование HTML в клиенте iOS](../../assets/images/cards/card-formatting-xml-mobile-v2.png)

Вопросы:

* Форматирование символов, как смелые и жирные не отображаются на iOS.

На Android форматирование HTML выглядит так:

![HTML форматирование в клиенте Android](../../assets/images/cards/card-formatting-xml-android-60.png)

Форматирование символов, как смелый и italic дисплей правильно на Android.

### <a name="formatting-sample-for-html-formatting-in-simple-cards"></a>Пример форматирования html-форматирования в простых картах

Эти скриншоты были созданы Teams AppStudio, где текстовое свойство карты героя было настроено на следующую строку. Вы можете протестировать форматирование в собственных картах, изменив этот код.

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"https://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`

---
