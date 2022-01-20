---
title: Форматирование текста карточек
description: Описание форматирования текста карточек в Microsoft Teams
keywords: Форматирование карточек в ботах Teams
ms.localizationpriority: high
ms.topic: reference
ms.date: 06/25/2021
ms.openlocfilehash: d660d58b00624b4d91ce4241829b204c66ba95df
ms.sourcegitcommit: 9e448dcdfd78f4278e9600808228e8158d830ef7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/17/2022
ms.locfileid: "62059604"
---
# <a name="format-cards-in-microsoft-teams"></a>Форматирование карточек в Microsoft Teams

Ниже приводится два способа добавления форматирования текста в карточки:
* [Markdown](#format-cards-with-markdown)
* [HTML](#format-cards-with-html)

Карточки не поддерживают форматирование в свойствах заголовка или подзаголовка, но поддерживают его в свойстве текста. Форматирование можно задать с помощью подмножества для форматирования XML либо HTML или Markdown в зависимости от типа карточки. Для текущей и будущей разработки адаптивных карточек рекомендуется форматирование Markdown.

Поддержка форматирования зависит от типа карточки. Отрисовка карточек может незначительно отличаться в классическом и мобильном клиентах Microsoft Teams, а также Teams в браузере на компьютере.

Вы можете включить встроенный рисунок в любую карточку Teams. Изображения могут быть в формате `.png`, `.jpg` или `.gif` и не должны превышать размер 1024 ×1024 пикселей или 1 МБ. GIF с анимацией не поддерживается. Дополнительные сведения см. в разделе [Типы карточек](./cards-reference.md#inline-card-images).

Адаптивные карточки и карточки соединителей Office 365 можно отформатировать с помощью Markdown, включающего определенные поддерживаемые стили.

## <a name="format-cards-with-markdown"></a>Форматирование карточек с помощью Markdown

Следующие типы карточек поддерживают форматирование Markdown в Teams:

* Адаптивные карточки: Markdown поддерживается в поле `Textblock` адаптивной карточки, а также в `Fact.Title` и `Fact.Value`. HTML не поддерживается в адаптивных карточках.
* Карточки соединителей Office 365: Markdown и ограниченный HTML поддерживаются в текстовых полях.

Вы можете использовать новые строки для адаптивных карточек с помощью escape-последовательности `\r` или `\n` для новых строк в списках. Форматирование адаптивных карточек отличается в классической и мобильной версиях Teams. Упоминания на основе карточек поддерживаются в классическом, мобильном и веб-клиенте. Вы можете использовать свойство маскировки информации для маскировки определенных сведений, например пароля или конфиденциальной информации от пользователей, во входном элементе `Input.Text` адаптивной карточки. Ширину адаптивной карточки можно увеличить с помощью объекта `width`. Вы можете включить поддержку опережающего ввода в адаптивных карточках и отфильтровать варианты ввода при наборе входных данных пользователем. Свойство `msteams` можно использовать для добавления возможности выборочного отображения изображений в представлении "Экран".

Форматирование адаптивных карточек и карточек соединителей отличается в классической и мобильной версиях Teams. В этом разделе можно ознакомиться с примером форматирования Markdown для адаптивных карточек и карточек соединителей.

# <a name="markdown-format-for-adaptive-cards"></a>[Форматирование Markdown для адаптивных карточек](#tab/adaptive-md)

 В таблице ниже указаны поддерживаемые стили для `Textblock`, `Fact.Title` и `Fact.Value`:

| Style | Пример | Markdown |
| --- | --- | --- |
| Полужирный | **Bold** | ```**Bold**``` |
| Курсив | _Italic_ | ```_Italic_``` |
| Неупорядоченный список | <ul><li>текст</li><li>текст</li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| Упорядоченный список | <ol><li>текст</li><li>текст</li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| Гиперссылки |[Bing](https://www.bing.com/)| ```[Title](url)``` |

Следующие теги Markdown не поддерживаются:

* Заголовки
* Таблицы
* изображения;
* Предварительно отформатированный текст
* Цитаты

### <a name="newlines-for-adaptive-cards"></a>Новые строки для адаптивных карточек

Вы можете использовать escape-последовательность `\r` или `\n` для новых строк в списках. Использование `\n\n` в списках приводит к добавлению отступа перед следующим элементом в списке. Если вам нужны новые строки где либо еще в TextBlock, используйте `\n\n`.

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a>Различия, связанные с адаптивными карточками, в классической и мобильной версиях

В классической версии форматирование Markdown для адаптивных карточек отображается в веб-браузерах и в клиентском приложении Teams следующим образом:

![Форматирование Markdown для адаптивных карточек в классическом клиенте](../../assets/images/cards/Adaptive-markdown-desktop-client.png)

В iOS форматирование Markdown для адаптивных карточек отображается следующим образом:

![Форматирование Markdown для адаптивных карточек в iOS](../../assets/images/cards/Adaptive-markdown-iOS-75.png)

В Android форматирование Markdown для адаптивных карточек отображается следующим образом:

![Форматирование Markdown для адаптивных карточек в Android](../../assets/images/cards/Adaptive-markdown-Android.png)

Дополнительные сведения см. в разделе [Текстовые функции в адаптивных карточках](/adaptive-cards/create/textfeatures).

> [!NOTE]
> Упомянутые в этом разделе функции даты и локализации не поддерживаются в Teams.

### <a name="adaptive-cards-format-sample"></a>Пример форматирования адаптивных карточек

В следующем коде показан пример форматирования адаптивных карточек:

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

### <a name="mention-support-within-adaptive-cards"></a>Поддержка упоминаний в адаптивных карточках 

Вы можете добавить @упоминания в текст адаптивных карточек для ботов и ответы расширения для сообщений. Чтобы добавить @упоминания в карточки, используйте ту же логику уведомления и отрисовки, что и в [упоминаниях на основе сообщений в беседах в каналах и групповых чатах](../../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions).

Боты и расширения для сообщений могут включать упоминания в содержимом карточек в элементах [TextBlock](https://adaptivecards.io/explorer/TextBlock.html) и [FactSet](https://adaptivecards.io/explorer/FactSet.html).

> [!NOTE]
> * [Элементы мультимедиа](https://adaptivecards.io/explorer/Media.html) в настоящее время не поддерживаются в адаптивных карточках на платформе Teams.
> * Упоминания каналов и команд не поддерживаются в сообщениях ботов.

Чтобы включить упоминание в адаптивную карточку, ваше приложение должно содержать следующие элементы:

* `<at>username</at>` в поддерживаемых элементах адаптивной карточки.
* Объект `mention` в свойстве `msteams` в содержимом карточки включает ИД пользователя Teams упоминаемого пользователя.
* `userId` является уникальным для идентификатора бота и определенного пользователя. Его можно использовать для @упоминания определенного пользователя. `userId` можно получить с помощью одного из параметров, указанных в разделе [Получение ИД пользователя](/microsoftteams/platform/bots/how-to/conversations/send-proactive-messages?tabs=dotnet#get-the-user-id-team-id-or-channel-id).

#### <a name="sample-adaptive-card-with-a-mention"></a>Пример адаптивной карточки с упоминанием

В следующем коде показан пример адаптивной карточки с упоминанием:

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

### <a name="aad-object-id-and-upn-in-user-mention"></a>ИД объекта AAD и имя участника-пользователя в упоминании пользователя 

Платформа Teams позволяет упоминать пользователей с ИД объекта AAD и именем участника-пользователя (UPN), помимо существующих идентификаторов упоминаний. Боты с адаптивными карточками и соединители с входящими веб-перехватчиками поддерживают два идентификатора упоминаний пользователей. 

В таблице ниже описываются идентификаторы упоминаний пользователей, которые поддерживаются с недавнего времени:

|Идентификаторы  | Вспомогательные возможности |   Описание | Пример |
|----------|--------|---------------|---------|
| ИД объекта AAD | Бот, соединитель |  ИД объекта пользователя AAD |  49c4641c-ab91-4248-aebb-6a7de286397b |
| Имя участника-пользователя | Бот, соединитель | Имя участника-пользователя AAD | john.smith@microsoft.com |

#### <a name="user-mention-in-bots-with-adaptive-cards"></a>Упоминание пользователей в ботах с адаптивными карточками 

Боты поддерживают упоминание пользователей с ИД объекта AAD и именем участника-пользователя, помимо существующих идентификаторов. Поддержка двух новых идентификаторов доступна в ботах для текстовых сообщений, текста адаптивных карточек и ответов расширения для сообщений. Боты поддерживают идентификаторы упоминаний в беседе и сценариях `invoke`. Пользователь получает уведомление от ленты новостей при @упоминании с ИД. 

> [!NOTE]
> Обновление схемы и изменения интерфейса не требуются для упоминания пользователей в адаптивных карточках в боте.

##### <a name="example"></a>Пример 

Пример упоминания пользователей в ботах с адаптивными карточками:

```json 
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "version": "1.0",
  "type": "AdaptiveCard",
  "body": [
    {
      "type": "TextBlock",
      "text": "Hi <at>Adele UPN</at>, <at>Adele AAD</at>"
    }
  ],
  "msteams": {
    "entities": [
      {
        "type": "mention",
        "text": "<at>Adele UPN</at>",
        "mentioned": {
          "id": "AdeleV@contoso.onmicrosoft.com",
          "name": "Adele Vance"
        }
      },
      {
        "type": "mention",
        "text": "<at>Adele AAD</at>",
        "mentioned": {
          "id": "87d349ed-44d7-43e1-9a83-5f2406dee5bd",
          "name": "Adele Vance"
        }
      }
    ]
  }
}
```

На изображении ниже показано упоминание пользователя в адаптивной карточке в боте:

![Упоминание пользователя в боте с адаптивной карточкой](~/assets/images/authentication/user-mention-in-bot.png)

#### <a name="user-mention-in-incoming-webhook-with-adaptive-cards"></a>Упоминание пользователя во входящем веб-перехватчике с адаптивными карточками 

Входящие веб-перехватчики начинают поддерживать упоминание пользователей в адаптивных карточках с ИД объекта AAD и именем участника-пользователя.

> [!NOTE]    
> * Включите упоминание пользователей в схеме входящих веб-перехватчиков для поддержки ИД объекта AAD и имени участника-пользователя. 
> * Изменения интерфейса не требуются для упоминания пользователей с ИД объекта AAD и именем участника-пользователя.      

##### <a name="example"></a>Пример 

Пример упоминания пользователя во входящем веб-перехватчике:

```json
{
    "type": "message",
    "attachments": [
        {
        "contentType": "application/vnd.microsoft.card.adaptive",
        "content": {
            "type": "AdaptiveCard",
            "body": [
                {
                    "type": "TextBlock",
                    "size": "Medium",
                    "weight": "Bolder",
                    "text": "Sample Adaptive Card with User Mention"
                },
                {
                    "type": "TextBlock",
                    "text": "Hi <at>Adele UPN</at>, <at>Adele AAD</at>"
                }
            ],
            "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
            "version": "1.0",
            "msteams": {
                "entities": [
                    {
                        "type": "mention",
                        "text": "<at>Adele UPN</at>",
                        "mentioned": {
                          "id": "AdeleV@contoso.onmicrosoft.com",
                          "name": "Adele Vance"
                        }
                      },
                      {
                        "type": "mention",
                        "text": "<at>Adele AAD</at>",
                        "mentioned": {
                          "id": "87d349ed-44d7-43e1-9a83-5f2406dee5bd",
                          "name": "Adele Vance"
                        }
                      }
                ]
            }
        }
    }]
}
```

На изображении ниже показано упоминание пользователя во входящем веб-перехватчике:

![Упоминание пользователя во входящем веб-перехватчике](~/assets/images/authentication/user-mention-in-incoming-webhook.png)

### <a name="information-masking-in-adaptive-cards"></a>Маскировка сведений в адаптивных карточках

Используйте свойство маскировки информации для маскировки определенных сведений, например пароля или конфиденциальной информации от пользователей, во входном элементе [`Input.Text`](https://adaptivecards.io/explorer/Input.Text.html) адаптивной карточки.

> [!NOTE]
> Эта функция поддерживает только маскировку клиентской информации. Маскируемый текст ввода отправляется в виде открытого текста на адрес конечной точки HTTPS, указанный при [настройке бота](../../build-your-first-app/build-bot.md#4-register-your-bot-endpoint).

Чтобы замаскировать сведения в адаптивных карточках, добавьте свойство `style` в **Тип** `input.text` и задайте для него значение **Пароль**.

#### <a name="sample-adaptive-card-with-masking-property"></a>Пример адаптивной карточки со свойством маскировки

В следующем коде показан пример адаптивной карточки со свойством маскировки:

```json
{
    "type": "Input.Text",
    "id": "secretThing",
    "style": "password",
},
```

На изображении ниже приводится пример маскировки сведений в адаптивных карточках:

![Изображение маскировки сведений](../../assets/images/cards/masking-information-view.png)

### <a name="full-width-adaptive-card"></a>Полноширинная адаптивная карточка

С помощью свойства `msteams` можно увеличить ширину адаптивной карточки и использовать дополнительное пространство холста. В следующем разделе приводятся сведения об использовании этого свойства.

#### <a name="construct-full-width-cards"></a>Создание полноширинных карточек

Чтобы создать полноширинную адаптивную карточку, для объекта `width` в свойстве `msteams` в содержимом карточки необходимо задать значение `Full`.

#### <a name="sample-adaptive-card-with-full-width"></a>Пример полноширинной адаптивной карточки

Чтобы создать полноширинную адаптивную карточку, приложение должно включать элементы из следующего примера кода:

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

На изображении ниже показана полноширинная адаптивная карточка:

![Представление полноширинной адаптивной карточки](../../assets/images/cards/full-width-adaptive-card.png)

На изображении ниже показано стандартное представление адаптивной карточки, если для свойства `width` не задано значение **Полная ширина**:

![Представление адаптивной карточки с небольшой шириной](../../assets/images/cards/small-width-adaptive-card.png)

### <a name="typeahead-support"></a>Поддержка опережающего ввода

В элементе схемы [`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) фильтрация многочисленных вариантов и выбор подходящего пользователями может значительно замедлить выполнение задачи. Поддержка опережающего ввода в адаптивных карточках может упростить выбор, сужая или фильтруя варианты ввода при наборе входных данных пользователем.

Чтобы включить опережающий ввод в `Input.Choiceset`, задайте для `style` значение `filtered` и убедитесь, что для `isMultiSelect` задано значение `false`.

#### <a name="sample-adaptive-card-with-typeahead-support"></a>Пример адаптивной карточки с поддержкой опережающего ввода

В следующем коде показан пример адаптивной карточки с поддержкой опережающего ввода:

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

### <a name="stage-view-for-images-in-adaptive-cards"></a>Представление "Экран" для изображений в адаптивных карточках

В адаптивной карточке можно использовать свойство `msteams` для добавления возможности выборочного отображения изображений в представлении "Экран". При наведении курсора на изображения пользователи могут видеть значок "Развернуть", для которого атрибут `allowExpand` имеет значение `true`. Сведения об использовании этого свойства см. в следующем примере:

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
          }
     ],
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.2"
}
```

При наведении курсора на изображения значок "Развернуть" появляется в правом верхнем углу, как показано на изображении ниже:

![Адаптивная карточка с расширяемым изображением](../../assets/images/cards/adaptivecard-hover-expand-icon.png)

Изображение отображается в представлении "Экран", когда пользователь нажимает значок "Развернуть", как показано на изображении ниже:

![Изображение, развернутое для представления "Экран"](../../assets/images/cards/adaptivecard-expand-image.png)

В представлении "Экран" пользователи могут увеличивать и уменьшать изображение. Вы можете выбрать изображения в адаптивной карточке, для которых должна использоваться эта возможность.

> [!NOTE]
> * Возможность увеличения и уменьшения применяется только к элементам изображения типа изображения в адаптивной карточке.
> * В мобильных приложениях Teams функциональность представления "Экран" для изображений в адаптивных карточках доступна по умолчанию. Пользователи могут просматривать изображения в адаптивных карточках в представлении "Экран", просто нажав на изображение, независимо от наличия атрибута `allowExpand`.

# <a name="markdown-format-for-office-365-connector-cards"></a>[Форматирование Markdown для карточек соединителей Office 365](#tab/connector-md)

Карточки соединителей поддерживают ограниченное форматирование Markdown и HTML.

| Style | Пример | Markdown |
| --- | --- | --- |
| Полужирный | **text** | `**text**` |
| Курсив | *text* | `*text*` |
| Заголовок (уровни 1&ndash;3) | **Text** | `### Text`|
| Зачеркнутый | ~~text~~ | `~~text~~` |
| Неупорядоченный список | <ul><li>текст</li><li>текст</li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| Упорядоченный список | <ol><li>текст</li><li>текст</li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| Предварительно отформатированный текст | `text` | ``preformatted text`` |
| Цитата | >текст цитаты | `>blockquote text` |
| Hyperlink | [Bing](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| Ссылка на изображение |![Утка на камне](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

В карточках соединителей новые строки не отображаются для `\n` или `\r`, но отображаются для `\n\n`.

### <a name="mobile-and-desktop-differences-for-connector-cards"></a>Различия, связанные с карточками соединителей, в классической и мобильной версиях

В классической версии форматирование Markdown для карточек соединителей отображается следующим образом:

![Форматирование Markdown для карточек соединителей в классическом клиенте](../../assets/images/cards/connector-desktop-markdown-combined.png)

В iOS форматирование Markdown для карточек соединителей отображается следующим образом:

![Форматирование Markdown для карточек соединителей в клиенте iOS](../../assets/images/cards/connector-iphone-markdown-combined-80.png)

С карточками соединителей, использующими Markdown для iOS, возникают следующие проблемы:

* Клиент iOS для Teams не отображает встроенные рисунки Markdown или HTML в карточках соединителей.
* Цитаты отображаются с отступом, но без серого фона.

В Android форматирование Markdown для карточек соединителей отображается следующим образом:

![Форматирование Markdown для карточек соединителей в клиенте Android](../../assets/images/cards/connector-android-markdown-combined.png)

### <a name="format-example-for-markdown-connector-cards"></a>Пример форматирования для карточек соединителей Markdown

В следующем коде показан пример форматирования для карточек соединителей Markdown:

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

## <a name="format-cards-with-html"></a>Форматирование карточек с помощью HTML

Следующие типы карточек поддерживают форматирование HTML в Teams:

* Карточки соединителей Office 365: поддерживается ограниченное форматирование Markdown и HTML.
* Карточки эскизов и главного имиджевого баннера: HTML-теги поддерживаются для простых карточек, таких как карточки эскизов и главного имиджевого баннера.

Форматирование карточек соединителей Office 365 и простых карточек отличается в классической и мобильной версиях Teams. В этом разделе можно ознакомиться с примером форматирования HTML для карточек соединителей и простых карточек.

# <a name="html-format-for-office-365-connector-cards"></a>[Форматирование HTML для карточек соединителей Office 365](#tab/connector-html)

Карточки соединителей поддерживают ограниченное форматирование Markdown и HTML.

| Style | Пример | HTML |
| --- | --- | --- |
| Полужирный | **text** | `<strong>text</strong>` |
| Курсив | *text* | `<em>text</em>` |
| Заголовок (уровни 1&ndash;3) | **Text** | `<h3>Text</h3>` |
| Зачеркнутый | ~~text~~ | `<strike>text</strike>` |
| Неупорядоченный список | <ul><li>текст</li><li>текст</li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| Упорядоченный список | <ol><li>текст</li><li>текст</li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| Предварительно отформатированный текст | `text` | `<pre>text</pre>` |
| Цитата | <blockquote>текст</blockquote> | `<blockquote>text</blockquote>` |
| Hyperlink | [Bing](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| Ссылка на изображение | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

В карточках соединителей новые строки отображаются в HTML с помощью тега `<p>`.

### <a name="mobile-and-desktop-differences-for-connector-cards"></a>Различия, связанные с карточками соединителей, в классической и мобильной версиях

В классической версии форматирование HTML для карточек соединителей отображается следующим образом:

![Форматирование HTML для карточек соединителей в классическом клиенте](../../assets/images/cards/Connector-desktop-html-combined.png)

В iOS форматирование HTML отображается следующим образом:

![Форматирование HTML для карточек соединителей в клиенте iOS](../../assets/images/cards/connector-iphone-html-combined-80.png)

С карточками соединителей, использующими HTML для iOS, возникают следующие проблемы:

* Встроенные рисунки не отображаются в iOS с помощью Markdown или HTML в карточках соединителей.
* Предварительно отформатированный текст отображается, но без серого фона.

В Android форматирование HTML отображается следующим образом:

![Форматирование HTML для карточек соединителей в клиенте Android](../../assets/images/cards/connector-android-html-combined.png)

### <a name="format-sample-for-html-connector-cards"></a>Пример форматирования для карточек соединителей HTML

В следующем коде показан пример форматирования для карточек соединителей HTML:

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

# <a name="html-format-for-hero-and-thumbnail-cards"></a>[Форматирование HTML для карточек эскизов и главного имиджевого баннера](#tab/simple-html)

HTML-теги поддерживаются для простых карточек, таких как карточки эскизов и главного имиджевого баннера. Markdown не поддерживается.

| Style | Пример | HTML |
| --- | --- | --- |
| Полужирный | **text** | `<strong>text</strong>` |
| Курсив | *text* | `<em>text</em>` |
| Заголовок (уровни 1&ndash;3) | **Text** | `<h3>Text</h3>` |
| Зачеркнутый | ~~text~~ | `<strike>text</strike>` |
| Неупорядоченный список | <ul><li>текст</li><li>текст</li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| Упорядоченный список | <ol><li>текст</li><li>текст</li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| Предварительно отформатированный текст | `text` | `<pre>text</pre>` |
| Цитата | <blockquote>текст</blockquote> | `<blockquote>text</blockquote>` |
| Hyperlink | [Bing](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| Ссылка на изображение |<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a>Различия, связанные с простыми карточками, в классической и мобильной версиях

Поскольку между классической и мобильной платформами существуют различия в разрешении, форматирование в классической и мобильной версиях Teams отличается.

В классической версии форматирование HTML отображается следующим образом:

![Форматирование HTML в классическом клиенте](../../assets/images/cards/card-formatting-xml-desktop-v2.png)

В iOS форматирование HTML отображается следующим образом:

![Форматирование HTML в клиенте iOS](../../assets/images/cards/card-formatting-xml-mobile-v2.png)

Форматирование знаков, например полужирный шрифт и курсив, не отображается в iOS.

В Android форматирование HTML отображается следующим образом:

![Форматирование HTML в клиенте Android](../../assets/images/cards/card-formatting-xml-android-60.png)

Форматирование знаков, например полужирный шрифт и курсив, правильно отображается в Android.

### <a name="format-example-for-simple-cards"></a>Пример форматирования для простых карточек

Изображения в предыдущем разделе созданы с использованием Teams **App Studio**, где свойство текста карточки главного имиджевого баннера задано следующей строкой:

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"https://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`

Вы можете проверить форматирование в своих карточках, изменяя этот код.

---

## <a name="see-also"></a>См. также

* [Действия карточек](./cards-actions.md)
* [Использование модулей задач из ботов](~/task-modules-and-cards/task-modules/task-modules-bots.md)
* [Модули задач](~/task-modules-and-cards/cards/cards-format.md)
* [Формат сообщений бота](~/bots/how-to/format-your-bot-messages.md)
