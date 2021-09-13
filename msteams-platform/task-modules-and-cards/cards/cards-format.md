---
title: Форматирование текста в картах
description: Описывает форматирование текста карты в Microsoft Teams
keywords: teams bots cards format
ms.localizationpriority: medium
ms.topic: reference
ms.date: 06/25/2021
ms.openlocfilehash: abbdc0d1fa77744ae061e5430c4450d0e7cf83c7
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/12/2021
ms.locfileid: "59157255"
---
# <a name="format-cards-in-microsoft-teams"></a>Форматирование карточек в Microsoft Teams

Ниже приводится два способа добавления насыщенного форматирования текста в карты:
* [Markdown](#format-cards-with-markdown)
* [HTML](#format-cards-with-html)

Карточки поддерживают форматирование только в свойстве текста, а не в свойствах заголовка или субтитров. Форматирование можно задать с помощью подмножество форматирования XML или HTML или Markdown в зависимости от типа карты. Для текущей и будущей разработки адаптивных карт рекомендуется форматирование Markdown.

Поддержка форматирования отличается между типами карт. Отрисовка карты может незначительно отличаться между настольным компьютером и мобильными Microsoft Teams клиентами, а также Teams в настольном браузере.

Вы можете включить в линию изображение с любой Teams карточкой. Изображения могут быть отформатированы как , или файлы и не должны превышать `.png` `.jpg` `.gif` 1024 ×1024 px или 1 МБ. Анимированный GIF не поддерживается. Дополнительные сведения см. [в некоторых видах карт.](./cards-reference.md#inline-card-images)

Можно форматирование адаптивных карт и Office 365 соединительные карты с markdown, которые включают определенные поддерживаемые стили.

## <a name="format-cards-with-markdown"></a>Формат карт с Markdown

Следующие типы карт поддерживают форматирование Markdown в Teams:

* Адаптивные карты: Markdown поддерживается в поле Адаптивная карта, а `Textblock` также `Fact.Title` и `Fact.Value` . HTML не поддерживается в адаптивных картах.
* Карты соединители O365: Markdown и ограниченный HTML поддерживаются в картах соединитель O365 в текстовых полях.

Вы можете использовать newlines для адаптивных карт с помощью последовательностей или `\r` `\n` побега для newlines в списках. Форматирование отличается между настольным компьютером и мобильными версиями Teams адаптивных карт. Упоминания на основе карт поддерживаются в веб-, настольных и мобильных клиентах. Свойство маскировки информации можно использовать для маскировки определенных сведений, таких как пароль или конфиденциальные сведения пользователей в элементе ввода адаптивной `Input.Text` карты. Ширину адаптивной карты можно расширить с помощью `width` объекта. Вы можете включить поддержку ввода в адаптивных картах и фильтровать набор вариантов ввода при типе ввода пользователем. Свойство можно использовать для выборочного отображения изображений `msteams` в представлении сцены.

Форматирование отличается между настольным компьютером и мобильными версиями Teams для адаптивных карт и соединительные карты. В этом разделе можно перейти к примеру формата Markdown для адаптивных карт и соединительные карты.

# <a name="markdown-format-for-adaptive-cards"></a>[Формат markdown для адаптивных карт](#tab/adaptive-md)

 Следующая таблица содержит поддерживаемые стили `Textblock` для `Fact.Title` , и `Fact.Value` :

| Стиль | Пример | Markdown |
| --- | --- | --- |
| Полужирный | **Bold** | ```**Bold**``` |
| Курсив | _Italic_ | ```_Italic_``` |
| Неупорядоченный список | <ul><li>текст</li><li>текст</li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| Упорядоченный список | <ol><li>текст</li><li>текст</li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| Гиперссылки |[Bing](https://www.bing.com/)| ```[Title](url)``` |

Следующие теги Markdown не поддерживаются:

* Заголовки
* Таблицы
* Изображения
* Предформатированный текст
* Blockquotes

### <a name="newlines-for-adaptive-cards"></a>Newlines для адаптивных карт

Вы можете использовать `\r` последовательности или `\n` последовательности побега для newlines в списках. Использование `\n\n` в списках приводит к отступам следующего элемента в списке. Если вам требуются новые линии в другом месте в TextBlock, используйте `\n\n` .

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a>Различия для мобильных и настольных компьютеров для адаптивных карт

На рабочем столе форматирование адаптивной карты markdown отображается на следующем изображении как в веб-браузерах, так и в клиентском приложении Teams:

![Форматирование разметки адаптивной карты в клиенте настольных компьютеров](../../assets/images/cards/Adaptive-markdown-desktop-client.png)

На iOS форматирование разметки адаптивной карты отображается на следующем изображении:

![Форматирование разметки адаптивной карты в iOS](../../assets/images/cards/Adaptive-markdown-iOS-75.png)

На Android форматирование разметки адаптивной карты отображается так, как показано на следующем изображении:

![Форматирование разметки адаптивной карты в Android](../../assets/images/cards/Adaptive-markdown-Android.png)

Дополнительные сведения см. в [текстовом документе Adaptive Cards.](/adaptive-cards/create/textfeatures)

> [!NOTE]
> Указанные в этом разделе функции даты и локализации не поддерживаются в Teams.

### <a name="adaptive-cards-format-sample"></a>Пример формата адаптивных карт

В следующем коде показан пример форматирования адаптивных карт:

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

Вы можете добавить @mentions в тело адаптивной карты для ботов и ответов расширения обмена сообщениями. Чтобы добавить @mentions в карты, следуйте той же логике уведомлений и отрисовки, что и упоминания на основе сообщений в беседах каналов и [групповых чатов.](../../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions)

Боты и расширения обмена сообщениями могут включать упоминания в контенте карты в [элементах TextBlock](https://adaptivecards.io/explorer/TextBlock.html) и [FactSet.](https://adaptivecards.io/explorer/FactSet.html)

> [!NOTE]
> * [Элементы мультимедиа в](https://adaptivecards.io/explorer/Media.html) настоящее время не поддерживаются в адаптивных картах v1.2 на Teams платформе.
> * Упоминания каналов и команд не поддерживаются в сообщениях ботов.

Чтобы включить упоминание в адаптивной карте, вашему приложению необходимо включить следующие элементы:

* `<at>username</at>` в поддерживаемых элементах адаптивной карты.
* Объект внутри свойства в содержимом карточки включает Teams имя пользователя `mention` `msteams` упоминаемого пользователя.
* Уникальный `userId` для вашего бот-ИД и определенного пользователя. Его можно использовать для @mention определенного пользователя. Можно получить с помощью одного из параметров, указанных в `userId` получить [пользовательский ID](/microsoftteams/platform/bots/how-to/conversations/send-proactive-messages?tabs=dotnet#get-the-user-id-team-id-or-channel-id).

#### <a name="sample-adaptive-card-with-a-mention"></a>Пример адаптивной карты с упоминанием

В следующем коде показан пример адаптивной карты с упоминанием:

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
> Эта функция поддерживает только маскировку сведений из стороны клиента. Текст ввода в маске отправляется в виде четкого текста на адрес конечной точки HTTPS, заданный во время [конфигурации бота.](../../build-your-first-app/build-bot.md#4-register-your-bot-endpoint)

Чтобы скрыть сведения в адаптивных картах, добавьте свойство для введите и установите `isMasked`  `Input.Text` значение true . 

#### <a name="sample-adaptive-card-with-masking-property"></a>Пример адаптивной карты с свойством маскировки

В следующем коде показан пример адаптивной карты с свойством маскировки:

```json
{
    "type": "Input.Text",
    "id": "secretThing",
    "style": "password",
},
```

Ниже приводится пример маскировки сведений в адаптивных картах:

![Маскировка информационного изображения](../../assets/images/cards/masking-information-view.png)

### <a name="full-width-adaptive-card"></a>Адаптивная карта с полной шириной

Свойство можно использовать для расширения ширины адаптивной карты и использования `msteams` дополнительного пространства холста. В следующем разделе приводится информация об использовании свойства.

#### <a name="construct-full-width-cards"></a>Создание карт полной ширины

Чтобы сделать полную ширину адаптивной карты, объект в свойстве контента карточки должен `width` `msteams` быть задат. `Full`

#### <a name="sample-adaptive-card-with-full-width"></a>Пример адаптивной карты с полной шириной

Чтобы сделать полную ширину адаптивной карты, приложение должно включать элементы из следующего примера кода:

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

На следующем изображении показана адаптивная карта с полной шириной:

![Представление адаптивной карты полной ширины](../../assets/images/cards/full-width-adaptive-card.png)

На следующем изображении по умолчанию показано представление адаптивной карты, если свойство не настроено `width` на **полное:**

![Представление адаптивной карты малой ширины](../../assets/images/cards/small-width-adaptive-card.png)

### <a name="typeahead-support"></a>Поддержка typeahead

В элементе схемы запрос пользователей на фильтрацию и выбор значительного числа вариантов может значительно замедлить [`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) завершение задачи. Поддержка ввода в адаптивных картах может упростить выбор входных данных, сужая или фильтруя набор вариантов ввода при типе ввода пользователем.

Чтобы включить введите в `Input.Choiceset` течение , установить и обеспечить `style` `filtered` `isMultiSelect` установлено `false` .

#### <a name="sample-adaptive-card-with-typeahead-support"></a>Пример адаптивной карты с поддержкой введите вперед

В следующем коде показан пример адаптивной карты с поддержкой заранее:

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

В адаптивной карте свойство можно использовать для выборочного отображения изображений в представлении `msteams` сцены. Когда пользователи наведите курсор над изображениями, они могут видеть значок расширения, для которого `allowExpand` атрибуту `true` установлено . Сведения об использовании свойства см. в следующем примере:

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

Когда пользователи наведите курсор над изображением, в правом верхнем углу появится значок расширения, как показано на следующем изображении:

![Адаптивная карта с расширяемым изображением](../../assets/images/cards/adaptivecard-hover-expand-icon.png)

Изображение отображается в представлении сцены, когда пользователь выбирает значок расширения, как показано на следующем изображении:

![Изображение, расширенное до представления сцены](../../assets/images/cards/adaptivecard-expand-image.png)

В представлении сцены пользователи могут масштабировать изображение и увеличивать его. Вы можете выбрать изображения в адаптивной карте, которые должны иметь эту возможность.

> [!NOTE]
> * Возможность масштабирования и масштабирования применяется только к элементам изображения, которые являются типом изображения в адаптивной карте.
> * Для Teams мобильных приложений по умолчанию доступны функции представления сцен для изображений в адаптивных картах. Пользователи могут просматривать изображения адаптивной карты в представлении сцены, просто нажав на изображение, независимо от того, присутствует атрибут или `allowExpand` нет.

# <a name="markdown-format-for-o365-connector-cards"></a>[Формат Markdown для карт соединителения O365](#tab/connector-md)

Карты Connector поддерживают ограниченное форматирование Markdown и HTML.

| Стиль | Пример | Markdown |
| --- | --- | --- |
| Полужирный | **text** | `**text**` |
| Курсив | *text* | `*text*` |
| Загон (уровни 1 &ndash; 3) | **Text** | `### Text`|
| Зачеркнутый | ~~text~~ | `~~text~~` |
| Неупорядоченный список | <ul><li>текст</li><li>текст</li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| Упорядоченный список | <ol><li>текст</li><li>текст</li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| Предформатированный текст | `text` | ``preformatted text`` |
| Blockquote | >блокквойта | `>blockquote text` |
| Hyperlink | [Bing](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| Ссылка на изображение |![Утка на скале](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

В соединитеных картах новые линии отрисовываются для `\n\n` , но не для или `\n` `\r` .

### <a name="mobile-and-desktop-differences-for-connector-cards"></a>Различия между мобильными и настольными устройствами для соединительная карта

На рабочем столе форматирование Markdown для карт соединительная система отображается на следующем изображении:

![Форматирование разметки для соединительная карта в клиенте Desktop](../../assets/images/cards/connector-desktop-markdown-combined.png)

На iOS форматирование Markdown для карт соединителения отображается на следующем изображении:

![Форматирование markdown для карт соединителения в клиенте iOS](../../assets/images/cards/connector-iphone-markdown-combined-80.png)

Карты соединителения, использующие Markdown для iOS, включают следующие проблемы:

* Клиент iOS для Teams не отрисовывает встроенные изображения Markdown или HTML в соединителях.
* Блокквоты отрисовываются как отступные, но без серого фона.

На Android форматирование markdown для карт соединителения отображается на следующем изображении:

![Форматирование разметки для карт соединителения в клиенте Android](../../assets/images/cards/connector-android-markdown-combined.png)

### <a name="format-example-for-markdown-connector-cards"></a>Пример формата для карт соединителения Markdown

В следующем коде показан пример форматирования для карт соединители Markdown:

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

## <a name="format-cards-with-html"></a>Форматные карты с HTML

Следующие типы карт поддерживают форматирование HTML в Teams:

* Карты соединители O365: ограниченное разметка и форматирование HTML поддерживаются в Office 365 соединителях.
* Карточки героя и эскиза: HTML-теги поддерживаются для простых карт, таких как карты героя и эскизы.

Форматирование отличается между настольным компьютером и мобильными версиями Teams для карт соединительная система O365 и простых карт. В этом разделе можно перейти к примеру формата HTML для соединительных карт и простых карт.

# <a name="html-format-for-o365-connector-cards"></a>[HTML-формат для карт соединителя O365](#tab/connector-html)

Карты Connector поддерживают ограниченное форматирование Markdown и HTML.

| Стиль | Пример | HTML |
| --- | --- | --- |
| Полужирный | **text** | `<strong>text</strong>` |
| Курсив | *text* | `<em>text</em>` |
| Загон (уровни 1 &ndash; 3) | **Text** | `<h3>Text</h3>` |
| Зачеркнутый | ~~text~~ | `<strike>text</strike>` |
| Неупорядоченный список | <ul><li>текст</li><li>текст</li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| Упорядоченный список | <ol><li>текст</li><li>текст</li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| Предформатированный текст | `text` | `<pre>text</pre>` |
| Blockquote | <blockquote>текст</blockquote> | `<blockquote>text</blockquote>` |
| Hyperlink | [Bing](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| Ссылка на изображение | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

В соединительных картах новые линии отрисовываются в HTML с помощью `<p>` тега.

### <a name="mobile-and-desktop-differences-for-connector-cards"></a>Различия между мобильными и настольными устройствами для соединительная карта

На рабочем столе форматирование HTML-форматов для карт соединителя отображается на следующем изображении:

![Форматирование HTML для соединителя карт в клиенте рабочего стола](../../assets/images/cards/Connector-desktop-html-combined.png)

На iOS форматирование HTML отображается на следующем изображении:

![Форматирование HTML для соединительных карт в клиенте iOS](../../assets/images/cards/connector-iphone-html-combined-80.png)

Карты соединителя, использующие HTML для iOS, включают следующие проблемы:

* Встроенные изображения не отрисовываются на iOS с помощью markdown или HTML в соединителях.
* Предформатированный текст отрисовывается, но не имеет серого фона.

На Android форматирование HTML отображается на следующем изображении:

![Форматирование HTML для соединительных карт в клиенте Android](../../assets/images/cards/connector-android-html-combined.png)

### <a name="format-sample-for-html-connector-cards"></a>Пример формата для htmL-соединителя карт

В следующем коде показан пример форматирования для htmL-соединителя карт:

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

# <a name="html-format-for-hero-and-thumbnail-cards"></a>[HTML-формат для карт-героев и эскизов](#tab/simple-html)

HTML-теги поддерживаются для простых карт, таких как карты героя и эскизы. Markdown не поддерживается.

| Стиль | Пример | HTML |
| --- | --- | --- |
| Полужирный | **text** | `<strong>text</strong>` |
| Курсив | *text* | `<em>text</em>` |
| Загон (уровни 1 &ndash; 3) | **Text** | `<h3>Text</h3>` |
| Зачеркнутый | ~~text~~ | `<strike>text</strike>` |
| Неупорядоченный список | <ul><li>текст</li><li>текст</li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| Упорядоченный список | <ol><li>текст</li><li>текст</li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| Предформатированный текст | `text` | `<pre>text</pre>` |
| Blockquote | <blockquote>текст</blockquote> | `<blockquote>text</blockquote>` |
| Hyperlink | [Bing](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| Ссылка на изображение |<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a>Различия для мобильных и настольных компьютеров для простых карт

Поскольку между настольной и мобильной платформами существуют различия в разрешении, форматирование отличается между настольным компьютером и мобильной версией Teams.

На рабочем столе форматирование HTML отображается на следующем изображении:

![Форматирование HTML в клиенте рабочего стола](../../assets/images/cards/card-formatting-xml-desktop-v2.png)

На iOS форматирование HTML отображается на следующем изображении:

![Форматирование HTML в клиенте iOS](../../assets/images/cards/card-formatting-xml-mobile-v2.png)

Форматирование символов, таких как смелый и italic, не отрисовывался на iOS.

На Android форматирование HTML отображается на следующем изображении:

![Форматирование HTML в клиенте Android](../../assets/images/cards/card-formatting-xml-android-60.png)

Форматирование символов, таких как смелый и italic отображения правильно на Android.

### <a name="format-example-for-simple-cards"></a>Пример формата для простых карт

Изображения в предыдущем разделе были созданы с Teams **App Studio,** где текстовое свойство карты-героя задалось следующей строке:

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"https://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`

Вы можете протестировать форматирование в собственных картах, изменяя этот код.

---

## <a name="see-also"></a>См. также

* [Действия карточек](./cards-actions.md)
* [Модули задач](~/task-modules-and-cards/cards/cards-format.md)
