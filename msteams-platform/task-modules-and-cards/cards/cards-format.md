---
title: Форматирование текста в картах
description: Описывает форматирование текста карты в Microsoft Teams
keywords: teams bots cards format
localization_priority: Normal
ms.topic: reference
ms.date: 03/29/2018
ms.openlocfilehash: d2806271f99af53139c76dcbd1090a96adcd0f31
ms.sourcegitcommit: 303fc214aa04757779a171337f31a6539f47fd03
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2021
ms.locfileid: "52068824"
---
# <a name="format-cards-in-teams"></a><span data-ttu-id="b17ae-104">Формат карт в Teams</span><span class="sxs-lookup"><span data-stu-id="b17ae-104">Format cards in Teams</span></span>

<span data-ttu-id="b17ae-105">В зависимости от типа карты можно добавить в карты форматирование текста с помощью Markdown или HTML.</span><span class="sxs-lookup"><span data-stu-id="b17ae-105">You can add rich text formatting to your cards using either Markdown or HTML, depending on the card type.</span></span>

<span data-ttu-id="b17ae-106">Карточки поддерживают форматирование только в свойстве текста, а не в свойствах заголовка или субтитров.</span><span class="sxs-lookup"><span data-stu-id="b17ae-106">Cards support formatting in the text property only, not in the title or subtitle properties.</span></span> <span data-ttu-id="b17ae-107">Форматирование можно задать с помощью подмножество форматирования XML (HTML) или Markdown в зависимости от типа карты.</span><span class="sxs-lookup"><span data-stu-id="b17ae-107">Formatting can be specified using a subset of XML (HTML) formatting, or Markdown depending on card type.</span></span> <span data-ttu-id="b17ae-108">Для текущих и будущих карт разработки рекомендуется использовать форматирование Markdown.</span><span class="sxs-lookup"><span data-stu-id="b17ae-108">For current and future development Adaptive cards using Markdown formatting is recommended.</span></span>

<span data-ttu-id="b17ae-109">Поддержка форматирования отличается между различными типами карт, а отрисовка карты может незначительно отличаться между настольным компьютером и клиентами мобильных групп, а также Teams в браузере настольных компьютеров.</span><span class="sxs-lookup"><span data-stu-id="b17ae-109">Formatting support differs between different card types, and rendering of the card can differ slightly between the desktop and the mobile Teams clients, as well as Teams in the desktop browser.</span></span>

<span data-ttu-id="b17ae-110">Вы можете включить inline-изображение с любой картой Teams.</span><span class="sxs-lookup"><span data-stu-id="b17ae-110">You can include an inline image with any Teams card.</span></span> <span data-ttu-id="b17ae-111">Изображения форматированы как , или файлы и не должны превышать  `.png` `.jpg` `.gif` 1024 ×1024 px или 1 МБ.</span><span class="sxs-lookup"><span data-stu-id="b17ae-111">Images an be formatted as  `.png`, `.jpg`, or `.gif` files and must not exceed 1024 ×1024 px or 1 MB.</span></span> <span data-ttu-id="b17ae-112">Анимированный GIF не поддерживается официально.</span><span class="sxs-lookup"><span data-stu-id="b17ae-112">Animated GIF is not officially supported.</span></span> <span data-ttu-id="b17ae-113">*См.* [ссылку На карточки](./cards-reference.md#inline-card-images)</span><span class="sxs-lookup"><span data-stu-id="b17ae-113">*See* [Cards reference](./cards-reference.md#inline-card-images)</span></span>

## <a name="formatting-cards-with-markdown"></a><span data-ttu-id="b17ae-114">Форматирование карт с помощью Markdown</span><span class="sxs-lookup"><span data-stu-id="b17ae-114">Formatting cards with Markdown</span></span>

<span data-ttu-id="b17ae-115">Существует два типа карт, поддерживаюных Markdown в Teams:</span><span class="sxs-lookup"><span data-stu-id="b17ae-115">There are two card types that support Markdown in Teams:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b17ae-116">**Адаптивные карты:** Markdown поддерживается в поле адаптивных карт, а `Textblock` также и `Fact.Title` `Fact.Value` .</span><span class="sxs-lookup"><span data-stu-id="b17ae-116">**Adaptive cards**: Markdown is supported in Adaptive card `Textblock` field, as well as `Fact.Title` and `Fact.Value`.</span></span> <span data-ttu-id="b17ae-117">HTML не поддерживается в адаптивных картах.</span><span class="sxs-lookup"><span data-stu-id="b17ae-117">HTML is not supported in Adaptive cards.</span></span>
> * <span data-ttu-id="b17ae-118">**Карты соединителя O365:** Markdown и ограниченный HTML поддерживаются в карточках Соединитель Office 365 в текстовых полях.</span><span class="sxs-lookup"><span data-stu-id="b17ae-118">**O365 Connector Cards**: Markdown and limited HTML is supported in Office 365 Connector cards in the text fields.</span></span>

# <a name="markdown-formatting-adaptive-cards"></a>[<span data-ttu-id="b17ae-119">**Форматирование разметки: адаптивные карты**</span><span class="sxs-lookup"><span data-stu-id="b17ae-119">**Markdown formatting: Adaptive cards**</span></span>](#tab/adaptive-md)

 <span data-ttu-id="b17ae-120">Поддерживаемые стили `Textblock` для и `Fact.Title` `Fact.Value` являются:</span><span class="sxs-lookup"><span data-stu-id="b17ae-120">The supported styles for `Textblock`, `Fact.Title` and `Fact.Value` are:</span></span>

| <span data-ttu-id="b17ae-121">Style</span><span class="sxs-lookup"><span data-stu-id="b17ae-121">Style</span></span> | <span data-ttu-id="b17ae-122">Пример</span><span class="sxs-lookup"><span data-stu-id="b17ae-122">Example</span></span> | <span data-ttu-id="b17ae-123">Markdown</span><span class="sxs-lookup"><span data-stu-id="b17ae-123">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b17ae-124">bold</span><span class="sxs-lookup"><span data-stu-id="b17ae-124">bold</span></span> | <span data-ttu-id="b17ae-125">**Bold**</span><span class="sxs-lookup"><span data-stu-id="b17ae-125">**Bold**</span></span> | ```**Bold**``` |
| <span data-ttu-id="b17ae-126">italic</span><span class="sxs-lookup"><span data-stu-id="b17ae-126">italic</span></span> | <span data-ttu-id="b17ae-127">_Italic_</span><span class="sxs-lookup"><span data-stu-id="b17ae-127">_Italic_</span></span> | ```_Italic_``` |
| <span data-ttu-id="b17ae-128">необученный список</span><span class="sxs-lookup"><span data-stu-id="b17ae-128">unordered list</span></span> | <ul><li><span data-ttu-id="b17ae-129">текст</span><span class="sxs-lookup"><span data-stu-id="b17ae-129">text</span></span></li><li><span data-ttu-id="b17ae-130">текст</span><span class="sxs-lookup"><span data-stu-id="b17ae-130">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="b17ae-131">упорядоченный список</span><span class="sxs-lookup"><span data-stu-id="b17ae-131">ordered list</span></span> | <ol><li><span data-ttu-id="b17ae-132">текст</span><span class="sxs-lookup"><span data-stu-id="b17ae-132">text</span></span></li><li><span data-ttu-id="b17ae-133">текст</span><span class="sxs-lookup"><span data-stu-id="b17ae-133">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="b17ae-134">Гиперссылки</span><span class="sxs-lookup"><span data-stu-id="b17ae-134">Hyperlinks</span></span> |[<span data-ttu-id="b17ae-135">Bing</span><span class="sxs-lookup"><span data-stu-id="b17ae-135">Bing</span></span>](https://www.bing.com/)| ```[Title](url)``` |

<span data-ttu-id="b17ae-136">Следующие теги Markdown не поддерживаются:</span><span class="sxs-lookup"><span data-stu-id="b17ae-136">The following Markdown tags are not supported:</span></span>

* <span data-ttu-id="b17ae-137">Заголовки</span><span class="sxs-lookup"><span data-stu-id="b17ae-137">Headers</span></span>
* <span data-ttu-id="b17ae-138">Tables</span><span class="sxs-lookup"><span data-stu-id="b17ae-138">Tables</span></span>
* <span data-ttu-id="b17ae-139">изображения;</span><span class="sxs-lookup"><span data-stu-id="b17ae-139">Images</span></span>
* <span data-ttu-id="b17ae-140">Предформатированный текст</span><span class="sxs-lookup"><span data-stu-id="b17ae-140">Preformatted text</span></span>
* <span data-ttu-id="b17ae-141">Blockquotes</span><span class="sxs-lookup"><span data-stu-id="b17ae-141">Blockquotes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b17ae-142">Адаптивные карты не поддерживают форматирование HTML.</span><span class="sxs-lookup"><span data-stu-id="b17ae-142">Adaptive cards do not support HTML formatting.</span></span>

### <a name="newlines-for-adaptive-cards"></a><span data-ttu-id="b17ae-143">Newlines для адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="b17ae-143">Newlines for Adaptive cards</span></span>

<span data-ttu-id="b17ae-144">В списках можно использовать `\r` последовательности `\n` или последовательности побега для newlines.</span><span class="sxs-lookup"><span data-stu-id="b17ae-144">In lists you can use the `\r` or `\n` escape sequences for newlines.</span></span> <span data-ttu-id="b17ae-145">Использование в списке приведет к отступам следующего элемента `\n\n` в списке.</span><span class="sxs-lookup"><span data-stu-id="b17ae-145">Using `\n\n` in a list will cause the next element in the list to be indented.</span></span> <span data-ttu-id="b17ae-146">Если вам нужны новые линии в другом месте в текстовом блокпосте, используйте `\n\n` .</span><span class="sxs-lookup"><span data-stu-id="b17ae-146">If you need newlines elsewhere in the textblock, use `\n\n`.</span></span>

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a><span data-ttu-id="b17ae-147">Различия для мобильных и настольных компьютеров для адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="b17ae-147">Mobile and desktop differences for Adaptive cards</span></span>

<span data-ttu-id="b17ae-148">Форматирование несколько отличается от рабочего стола к мобильным версиям Teams.</span><span class="sxs-lookup"><span data-stu-id="b17ae-148">Formatting is slightly different between the desktop and the mobile versions of Teams.</span></span>

<span data-ttu-id="b17ae-149">На рабочем столе форматирование разметки адаптивной карты выглядит так как в веб-браузерах, так и в клиентском приложении Teams:</span><span class="sxs-lookup"><span data-stu-id="b17ae-149">On the desktop, Adaptive card Markdown formatting appears like this in both web browsers and in the Teams client application:</span></span>

![Форматирование разметки адаптивной карты в клиенте рабочего стола](../../assets/images/cards/Adaptive-markdown-desktop-client.png)

<span data-ttu-id="b17ae-151">В iOS форматирование разметки адаптивной карты выглядит так:</span><span class="sxs-lookup"><span data-stu-id="b17ae-151">On iOS, Adaptive card Markdown formatting appears like this:</span></span>

![Форматирование разметки адаптивной карты в iOS](../../assets/images/cards/Adaptive-markdown-iOS-75.png)

<span data-ttu-id="b17ae-153">На Android форматирование разметки адаптивной карты выглядит так:</span><span class="sxs-lookup"><span data-stu-id="b17ae-153">On Android, Adaptive Card Markdown formatting appears like this:</span></span>

![Форматирование разметки адаптивной карты в Android](../../assets/images/cards/Adaptive-markdown-Android.png)

### <a name="more-information-on-adaptive-cards"></a><span data-ttu-id="b17ae-155">Дополнительные сведения о адаптивных картах</span><span class="sxs-lookup"><span data-stu-id="b17ae-155">More information on Adaptive cards</span></span>

<span data-ttu-id="b17ae-156">[Текстовые функции в адаптивных картах](/adaptive-cards/create/textfeatures) Функции даты и локализации, упомянутые в этой теме, не поддерживаются в Teams.</span><span class="sxs-lookup"><span data-stu-id="b17ae-156">[Text features in Adaptive cards](/adaptive-cards/create/textfeatures) The date and localization features mentioned in this topic are not supported in Teams.</span></span>

### <a name="formatting-sample-for-adaptive-cards"></a><span data-ttu-id="b17ae-157">Пример форматирования для адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="b17ae-157">Formatting sample for Adaptive cards</span></span>

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

### <a name="mention-support-within-adaptive-cards-v12"></a><span data-ttu-id="b17ae-158">Упоминание поддержки в адаптивных картах v1.2</span><span class="sxs-lookup"><span data-stu-id="b17ae-158">Mention support within Adaptive cards v1.2</span></span>

<span data-ttu-id="b17ae-159">Упоминания на основе карт поддерживаются в веб-, настольных и мобильных клиентах.</span><span class="sxs-lookup"><span data-stu-id="b17ae-159">Card based mentions are supported in web, desktop and mobile clients.</span></span> <span data-ttu-id="b17ae-160">Вы можете добавить @ упоминания в тексте адаптивной карты для ботов и ответов на расширение обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="b17ae-160">You can add @ mentions within an adaptive card body for bots and messaging extension responses.</span></span> <span data-ttu-id="b17ae-161">Чтобы добавить @mentions in cards, следуйте той же логике уведомлений и визуализации, что и упоминания на основе сообщений в беседах в чатах каналов и [групп.](../../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions)</span><span class="sxs-lookup"><span data-stu-id="b17ae-161">To add @ mentions in cards, follow the same notification logic and rendering as that of message based [mentions in channel and group chat conversations](../../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions).</span></span>

<span data-ttu-id="b17ae-162">Боты и расширения обмена сообщениями могут включать упоминания в контенте карты в [элементах TextBlock](https://adaptivecards.io/explorer/TextBlock.html) и [FactSet.](https://adaptivecards.io/explorer/FactSet.html)</span><span class="sxs-lookup"><span data-stu-id="b17ae-162">Bots and messaging extensions can include mentions within the card content in [TextBlock](https://adaptivecards.io/explorer/TextBlock.html) and [FactSet](https://adaptivecards.io/explorer/FactSet.html) elements.</span></span>

> [!NOTE]
> * <span data-ttu-id="b17ae-163">[Элементы мультимедиа в](https://adaptivecards.io/explorer/Media.html) настоящее время не поддерживаются в адаптивных картах v1.2 на платформе Teams.</span><span class="sxs-lookup"><span data-stu-id="b17ae-163">[Media elements](https://adaptivecards.io/explorer/Media.html) are currently not supported in Adaptive cards v1.2 on the Teams platform.</span></span>
> * <span data-ttu-id="b17ae-164">Упоминания & группы не поддерживаются в сообщениях ботов.</span><span class="sxs-lookup"><span data-stu-id="b17ae-164">Channel & Team mentions are not supported in bot messages.</span></span>

#### <a name="constructing-mentions"></a><span data-ttu-id="b17ae-165">Построение упоминаний</span><span class="sxs-lookup"><span data-stu-id="b17ae-165">Constructing mentions</span></span>

<span data-ttu-id="b17ae-166">Чтобы включить упоминание в адаптивной карте, приложение должно включить следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="b17ae-166">To include a mention in an Adaptive Card your app needs to include the following elements:</span></span>

* <span data-ttu-id="b17ae-167">`<at>username</at>` в поддерживаемых элементах адаптивной карты.</span><span class="sxs-lookup"><span data-stu-id="b17ae-167">`<at>username</at>` in the supported Adaptive card elements.</span></span>
* <span data-ttu-id="b17ae-168">Объект `mention` внутри свойства в содержимом карточки, который включает в себя `msteams` id пользователя Teams упомянутого пользователя.</span><span class="sxs-lookup"><span data-stu-id="b17ae-168">The `mention` object inside of an `msteams` property in the card content, which includes the Teams user id of the user being mentioned.</span></span>
* <span data-ttu-id="b17ae-169">Уникальный `userId` для вашего бот-ИД и определенного пользователя.</span><span class="sxs-lookup"><span data-stu-id="b17ae-169">The `userId` is unique to your bot ID and a particular user.</span></span> <span data-ttu-id="b17ae-170">Его можно использовать для @mention определенного пользователя.</span><span class="sxs-lookup"><span data-stu-id="b17ae-170">It can be used to @mention a particular user.</span></span> <span data-ttu-id="b17ae-171">Можно получить с помощью одного из параметров, указанных в `userId` получить [пользовательский ID](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/conversations/send-proactive-messages?tabs=dotnet#get-the-user-id-team-id-or-channel-id).</span><span class="sxs-lookup"><span data-stu-id="b17ae-171">The `userId` can be retrieved using one of the options mentioned in [get the user ID](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/conversations/send-proactive-messages?tabs=dotnet#get-the-user-id-team-id-or-channel-id).</span></span>

#### <a name="sample-adaptive-card-with-a-mention"></a><span data-ttu-id="b17ae-172">Пример адаптивной карты с упоминанием</span><span class="sxs-lookup"><span data-stu-id="b17ae-172">Sample Adaptive card with a mention</span></span>

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

### <a name="information-masking-in-adaptive-cards"></a><span data-ttu-id="b17ae-173">Маскировка сведений в адаптивных картах</span><span class="sxs-lookup"><span data-stu-id="b17ae-173">Information masking in Adaptive cards</span></span>
<span data-ttu-id="b17ae-174">Используйте свойство маскировки информации для маскировки определенных сведений, таких как пароль или конфиденциальные сведения пользователей в элементе ввода адаптивной [`Input.Text`](https://adaptivecards.io/explorer/Input.Text.html) карты.</span><span class="sxs-lookup"><span data-stu-id="b17ae-174">Use the information masking property to mask specific information, such as password or sensitive information from users within the Adaptive card [`Input.Text`](https://adaptivecards.io/explorer/Input.Text.html) input element.</span></span> 

> [!NOTE]
> <span data-ttu-id="b17ae-175">Эта функция поддерживает только маскировку стороной клиента, текст ввода в маске отправляется в виде четкого текста на адрес конечной точки https, заданный во время [конфигурации бота.](../../build-your-first-app/build-bot.md)</span><span class="sxs-lookup"><span data-stu-id="b17ae-175">The feature only supports client side information masking, the masked input text is sent as clear text to the https endpoint address that was specified during [bot configuration](../../build-your-first-app/build-bot.md).</span></span> 

> [!NOTE]
> <span data-ttu-id="b17ae-176">Свойство маскировки информации в настоящее время доступно только в предварительном просмотре разработчика.</span><span class="sxs-lookup"><span data-stu-id="b17ae-176">The information masking property is currently available in the developer preview only.</span></span>

<span data-ttu-id="b17ae-177">Чтобы скрыть сведения в адаптивных картах, добавьте свойство введите и установите `isMasked`  `Input.Text` значение true. </span><span class="sxs-lookup"><span data-stu-id="b17ae-177">To mask information in Adaptive cards, add the `isMasked` property to **type** `Input.Text`, and set its value to *true*.</span></span>

#### <a name="sample-adaptive-card-with-masking-property"></a><span data-ttu-id="b17ae-178">Пример адаптивной карты с свойством маскировки</span><span class="sxs-lookup"><span data-stu-id="b17ae-178">Sample Adaptive card with masking property</span></span>

```json
{
    "type": "Input.Text",
    "id": "secretThing",
    "style": "password",
    "isMasked": true
  },
```

<span data-ttu-id="b17ae-179">Ниже приводится пример маскировки сведений в адаптивных картах:</span><span class="sxs-lookup"><span data-stu-id="b17ae-179">The following image is an example of masking information in Adaptive cards:</span></span>

![Маскировка информационного изображения](../../assets/images/cards/masking-information-view.png)

### <a name="full-width-adaptive-card"></a><span data-ttu-id="b17ae-181">Адаптивная карта с полной шириной</span><span class="sxs-lookup"><span data-stu-id="b17ae-181">Full width Adaptive card</span></span>
<span data-ttu-id="b17ae-182">Свойство можно использовать для расширения ширины адаптивной карты и использования `msteams` дополнительного пространства холста.</span><span class="sxs-lookup"><span data-stu-id="b17ae-182">You can use the `msteams` property to expand the width of an Adaptive card and make use of additional canvas space.</span></span> <span data-ttu-id="b17ae-183">Сведения об использовании свойства см. в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="b17ae-183">For information on how to use the property, see the following example:</span></span>

#### <a name="constructing-full-width-cards"></a><span data-ttu-id="b17ae-184">Построение карт полной ширины</span><span class="sxs-lookup"><span data-stu-id="b17ae-184">Constructing full width cards</span></span>
<span data-ttu-id="b17ae-185">Чтобы сделать полную ширину адаптивной карты, объект в свойстве контента карточки `width` `msteams` должен быть задат. `Full`</span><span class="sxs-lookup"><span data-stu-id="b17ae-185">To make a full width Adaptive card the `width` object in `msteams` property in the card content must be set to `Full`.</span></span>
<span data-ttu-id="b17ae-186">Кроме того, приложение должно включать следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="b17ae-186">In addition, your app must include the following elements:</span></span>

#### <a name="sample-adaptive-card-with-full-width"></a><span data-ttu-id="b17ae-187">Пример адаптивной карты с полной шириной</span><span class="sxs-lookup"><span data-stu-id="b17ae-187">Sample adaptive card with full width</span></span>

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

<span data-ttu-id="b17ae-188">Адаптивная карта с полной шириной отображается следующим образом: представление адаптивной карты полной ![ ширины](../../assets/images/cards/full-width-adaptive-card.png)</span><span class="sxs-lookup"><span data-stu-id="b17ae-188">A full width Adaptive Card appears as follows: ![Full width Adaptive Card view](../../assets/images/cards/full-width-adaptive-card.png)</span></span>

<span data-ttu-id="b17ae-189">Если свойство не настроено до полного, представление адаптивной карты по умолчанию следующим образом: представление адаптивной карты малой `width`  ![ ширины](../../assets/images/cards/small-width-adaptive-card.png)</span><span class="sxs-lookup"><span data-stu-id="b17ae-189">If you have not set the `width` property to *Full*, then the default view of the Adaptive Card is as follows: ![Small width Adaptive Card view](../../assets/images/cards/small-width-adaptive-card.png)</span></span>

### <a name="typeahead-support"></a><span data-ttu-id="b17ae-190">Поддержка typeahead</span><span class="sxs-lookup"><span data-stu-id="b17ae-190">Typeahead support</span></span>

<span data-ttu-id="b17ae-191">В элементе схемы запрос на фильтрацию и выбор большого количества вариантов может значительно замедлить [`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) выполнение задач.</span><span class="sxs-lookup"><span data-stu-id="b17ae-191">Within the [`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) schema element, asking users to filter through and select through a sizable number of choices can significantly slow down task completion.</span></span> <span data-ttu-id="b17ae-192">Поддержка ввода в адаптивных картах может упростить выбор входных данных, сужая или фильтруя набор вариантов ввода при вводе ввода пользователем.</span><span class="sxs-lookup"><span data-stu-id="b17ae-192">Typeahead support within Adaptive cards can simplify input selection by narrowing or filtering the set of input choices as a user is typing the input.</span></span> 

#### <a name="enable-typeahead-in-adaptive-cards"></a><span data-ttu-id="b17ae-193">Включить введите в адаптивных картах</span><span class="sxs-lookup"><span data-stu-id="b17ae-193">Enable typeahead in Adaptive cards</span></span>

<span data-ttu-id="b17ae-194">Чтобы включить введите в `Input.Choiceset` наборе, `style` чтобы `filtered` и `isMultiSelect` убедиться, установлено `false` .</span><span class="sxs-lookup"><span data-stu-id="b17ae-194">To enable typeahead within the `Input.Choiceset` set `style` to `filtered` and ensure `isMultiSelect` is set to `false`.</span></span> 

#### <a name="sample-adaptive-card-with-typeahead-support"></a><span data-ttu-id="b17ae-195">Пример адаптивной карты с поддержкой typeahead</span><span class="sxs-lookup"><span data-stu-id="b17ae-195">Sample adaptive card with typeahead support</span></span>

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

### <a name="stage-view-for-images-in-adaptive-cards"></a><span data-ttu-id="b17ae-196">Представление сцены для изображений в адаптивных картах</span><span class="sxs-lookup"><span data-stu-id="b17ae-196">Stage view for images in Adaptive Cards</span></span>

> [!NOTE]
> <span data-ttu-id="b17ae-197">В настоящее время эта функция доступна только в предварительном просмотре разработчика.</span><span class="sxs-lookup"><span data-stu-id="b17ae-197">This feature is currently available in developer preview only.</span></span>
 
<span data-ttu-id="b17ae-198">В адаптивной карте свойство можно использовать для выборочного отображения изображений в представлении `msteams` сцены.</span><span class="sxs-lookup"><span data-stu-id="b17ae-198">In an Adaptive card, you can use the `msteams` property to add the ability to display images in stage view selectively.</span></span> <span data-ttu-id="b17ae-199">Когда пользователи наведите курсор над изображениями, они увидят значок расширения, для которого установлен `allowExpand` атрибут `true` .</span><span class="sxs-lookup"><span data-stu-id="b17ae-199">When users hover over the images, they would see an expand icon, for which the `allowExpand` attribute is set to `true`.</span></span> <span data-ttu-id="b17ae-200">Сведения об использовании свойства см. в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="b17ae-200">For information on how to use the property, see the following example:</span></span>

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

<span data-ttu-id="b17ae-201">Когда пользователи наведите курсор над изображением, в правом верхнем углу изображения появляется значок расширения: адаптивная карта ![ с расширяемым изображением](../../assets/images/cards/adaptivecard-hover-expand-icon.png)</span><span class="sxs-lookup"><span data-stu-id="b17ae-201">When users hover over the image, an expand icon appears at top right corner of the image: ![Adaptive card with expandable image](../../assets/images/cards/adaptivecard-hover-expand-icon.png)</span></span>

<span data-ttu-id="b17ae-202">Изображение отображается в представлении сцены, когда пользователь выбирает кнопку расширения: ![ изображение расширено до представления сцены](../../assets/images/cards/adaptivecard-expand-image.png)</span><span class="sxs-lookup"><span data-stu-id="b17ae-202">The image appears in stage view when the user selects the expand button: ![Image expanded to stage view](../../assets/images/cards/adaptivecard-expand-image.png)</span></span>

<span data-ttu-id="b17ae-203">В представлении сцены пользователи могут масштабировать изображение и увеличивать его.</span><span class="sxs-lookup"><span data-stu-id="b17ae-203">In the stage view, users can zoom in and zoom out of the image.</span></span> <span data-ttu-id="b17ae-204">Вы можете выбрать, какие изображения в адаптивной карте должны иметь эту возможность.</span><span class="sxs-lookup"><span data-stu-id="b17ae-204">You can select which images in your Adaptive card needs to have this capability.</span></span>

> [!NOTE]
> <span data-ttu-id="b17ae-205">Возможность масштабирования и масштабирования применяется только к элементам изображения (тип изображения) в адаптивной карте.</span><span class="sxs-lookup"><span data-stu-id="b17ae-205">Zoom in and zoom out capability applies only to the image elements (Image type) in an Adaptive card.</span></span>

> [!NOTE]
> <span data-ttu-id="b17ae-206">Для мобильных приложений Teams функции представления этапов для изображений в адаптивных картах доступны по умолчанию, и пользователи смогут просматривать адаптивные изображения карт в стадии представления, просто нажав на изображение, независимо от того, присутствует атрибут или `allowExpand` нет.</span><span class="sxs-lookup"><span data-stu-id="b17ae-206">For Teams mobile apps, stage view functionality for images in Adaptive Cards are available by default and users will be able to view Adaptive card images in stage view by simply tapping on the image, irrespective of whether the `allowExpand` attribute is present or not.</span></span>

# <a name="markdown-formatting-o365-connector-cards"></a>[<span data-ttu-id="b17ae-207">**Форматирование разметки: карты соединителения O365**</span><span class="sxs-lookup"><span data-stu-id="b17ae-207">**Markdown formatting: O365 Connector Cards**</span></span>](#tab/connector-md)

<span data-ttu-id="b17ae-208">Карты Connector поддерживают ограниченное форматирование Markdown и HTML.</span><span class="sxs-lookup"><span data-stu-id="b17ae-208">Connector cards support limited Markdown and HTML formatting.</span></span> <span data-ttu-id="b17ae-209">Поддержка HTML описана в последнем разделе.</span><span class="sxs-lookup"><span data-stu-id="b17ae-209">HTML support is described in the last section.</span></span>

| <span data-ttu-id="b17ae-210">Style</span><span class="sxs-lookup"><span data-stu-id="b17ae-210">Style</span></span> | <span data-ttu-id="b17ae-211">Пример</span><span class="sxs-lookup"><span data-stu-id="b17ae-211">Example</span></span> | <span data-ttu-id="b17ae-212">Markdown</span><span class="sxs-lookup"><span data-stu-id="b17ae-212">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b17ae-213">bold</span><span class="sxs-lookup"><span data-stu-id="b17ae-213">bold</span></span> | <span data-ttu-id="b17ae-214">**text**</span><span class="sxs-lookup"><span data-stu-id="b17ae-214">**text**</span></span> | `**text**` |
| <span data-ttu-id="b17ae-215">italic</span><span class="sxs-lookup"><span data-stu-id="b17ae-215">italic</span></span> | <span data-ttu-id="b17ae-216">*text*</span><span class="sxs-lookup"><span data-stu-id="b17ae-216">*text*</span></span> | `*text*` |
| <span data-ttu-id="b17ae-217">загон (уровни 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="b17ae-217">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="b17ae-218">**Text**</span><span class="sxs-lookup"><span data-stu-id="b17ae-218">**Text**</span></span> | `### Text`|
| <span data-ttu-id="b17ae-219">strikethrough</span><span class="sxs-lookup"><span data-stu-id="b17ae-219">strikethrough</span></span> | <span data-ttu-id="b17ae-220">~~text~~</span><span class="sxs-lookup"><span data-stu-id="b17ae-220">~~text~~</span></span> | `~~text~~` |
| <span data-ttu-id="b17ae-221">необученный список</span><span class="sxs-lookup"><span data-stu-id="b17ae-221">unordered list</span></span> | <ul><li><span data-ttu-id="b17ae-222">текст</span><span class="sxs-lookup"><span data-stu-id="b17ae-222">text</span></span></li><li><span data-ttu-id="b17ae-223">текст</span><span class="sxs-lookup"><span data-stu-id="b17ae-223">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="b17ae-224">упорядоченный список</span><span class="sxs-lookup"><span data-stu-id="b17ae-224">ordered list</span></span> | <ol><li><span data-ttu-id="b17ae-225">текст</span><span class="sxs-lookup"><span data-stu-id="b17ae-225">text</span></span></li><li><span data-ttu-id="b17ae-226">текст</span><span class="sxs-lookup"><span data-stu-id="b17ae-226">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="b17ae-227">предформатированный текст</span><span class="sxs-lookup"><span data-stu-id="b17ae-227">preformatted text</span></span> | `text` | ``preformatted text`` |
| <span data-ttu-id="b17ae-228">blockquote</span><span class="sxs-lookup"><span data-stu-id="b17ae-228">blockquote</span></span> | <span data-ttu-id="b17ae-229">>блокквойта</span><span class="sxs-lookup"><span data-stu-id="b17ae-229">>blockquote text</span></span> | `>blockquote text` |
| <span data-ttu-id="b17ae-230">гиперссылка</span><span class="sxs-lookup"><span data-stu-id="b17ae-230">hyperlink</span></span> | [<span data-ttu-id="b17ae-231">Bing</span><span class="sxs-lookup"><span data-stu-id="b17ae-231">Bing</span></span>](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| <span data-ttu-id="b17ae-232">ссылка на изображение</span><span class="sxs-lookup"><span data-stu-id="b17ae-232">image link</span></span> |![Утка на скале](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

<span data-ttu-id="b17ae-234">В соединитеных картах новые линии отрисовываются для `\n\n` , но не для или `\n` `\r` .</span><span class="sxs-lookup"><span data-stu-id="b17ae-234">In connector cards, newlines are rendered for `\n\n`, but not for `\n` or `\r`.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-markdown"></a><span data-ttu-id="b17ae-235">Различия для мобильных и настольных компьютеров для соединительная карта с помощью Markdown</span><span class="sxs-lookup"><span data-stu-id="b17ae-235">Mobile and desktop differences for connector cards using Markdown</span></span>

<span data-ttu-id="b17ae-236">На рабочем столе форматирование Markdown для карт соединительная система выглядит так:</span><span class="sxs-lookup"><span data-stu-id="b17ae-236">On the desktop, Markdown formatting for connector cards looks like this:</span></span>

![Форматирование разметки для соединительная карта в клиенте Desktop](../../assets/images/cards/connector-desktop-markdown-combined.png)

<span data-ttu-id="b17ae-238">В iOS форматирование markdown для соединители-карт выглядит так:</span><span class="sxs-lookup"><span data-stu-id="b17ae-238">On iOS, Markdown formatting for connector cards looks like this:</span></span>

![Форматирование markdown для карт соединителения в клиенте iOS](../../assets/images/cards/connector-iphone-markdown-combined-80.png)

<span data-ttu-id="b17ae-240">Вопросы:</span><span class="sxs-lookup"><span data-stu-id="b17ae-240">Issues:</span></span>

* <span data-ttu-id="b17ae-241">Клиент iOS для Teams не отрисовывает встроенные изображения Markdown или HTML в соединительных картах.</span><span class="sxs-lookup"><span data-stu-id="b17ae-241">The iOS client for Teams does not render Markdown or HTML inline images in Connector Cards.</span></span>
* <span data-ttu-id="b17ae-242">Блокквоты отрисовываются как отступные, но без серого фона.</span><span class="sxs-lookup"><span data-stu-id="b17ae-242">Blockquotes are rendered as indented but without a gray background.</span></span>

<span data-ttu-id="b17ae-243">На Android форматирование markdown для карт соединителения выглядит так:</span><span class="sxs-lookup"><span data-stu-id="b17ae-243">On Android, Markdown formatting for connector cards looks like this:</span></span>

![Форматирование разметки для карт соединителения в клиенте Android](../../assets/images/cards/connector-android-markdown-combined.png)

### <a name="formatting-example-for-markdown-connector-cards"></a><span data-ttu-id="b17ae-245">Пример форматирования карт соединителения Markdown</span><span class="sxs-lookup"><span data-stu-id="b17ae-245">Formatting example for Markdown Connector Cards</span></span>

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

## <a name="formatting-cards-with-html"></a><span data-ttu-id="b17ae-246">Форматирование карт с ПОМОЩЬЮ HTML</span><span class="sxs-lookup"><span data-stu-id="b17ae-246">Formatting cards with HTML</span></span>

# <a name="html-formatting-o365-connector-cards"></a>[<span data-ttu-id="b17ae-247">**Форматирование HTML: карты соединителя O365**</span><span class="sxs-lookup"><span data-stu-id="b17ae-247">**HTML formatting: O365 Connector Cards**</span></span>](#tab/connector-html)

<span data-ttu-id="b17ae-248">Карты Connector поддерживают ограниченное форматирование Markdown и HTML.</span><span class="sxs-lookup"><span data-stu-id="b17ae-248">Connector cards support limited Markdown and HTML formatting.</span></span> <span data-ttu-id="b17ae-249">Markdown описан в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="b17ae-249">Markdown is described in the next section.</span></span>

| <span data-ttu-id="b17ae-250">Style</span><span class="sxs-lookup"><span data-stu-id="b17ae-250">Style</span></span> | <span data-ttu-id="b17ae-251">Пример</span><span class="sxs-lookup"><span data-stu-id="b17ae-251">Example</span></span> | <span data-ttu-id="b17ae-252">HTML</span><span class="sxs-lookup"><span data-stu-id="b17ae-252">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b17ae-253">bold</span><span class="sxs-lookup"><span data-stu-id="b17ae-253">bold</span></span> | <span data-ttu-id="b17ae-254">**text**</span><span class="sxs-lookup"><span data-stu-id="b17ae-254">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="b17ae-255">italic</span><span class="sxs-lookup"><span data-stu-id="b17ae-255">italic</span></span> | <span data-ttu-id="b17ae-256">*text*</span><span class="sxs-lookup"><span data-stu-id="b17ae-256">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="b17ae-257">загон (уровни 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="b17ae-257">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="b17ae-258">**Text**</span><span class="sxs-lookup"><span data-stu-id="b17ae-258">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="b17ae-259">strikethrough</span><span class="sxs-lookup"><span data-stu-id="b17ae-259">strikethrough</span></span> | <span data-ttu-id="b17ae-260">~~text~~</span><span class="sxs-lookup"><span data-stu-id="b17ae-260">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="b17ae-261">необученный список</span><span class="sxs-lookup"><span data-stu-id="b17ae-261">unordered list</span></span> | <ul><li><span data-ttu-id="b17ae-262">текст</span><span class="sxs-lookup"><span data-stu-id="b17ae-262">text</span></span></li><li><span data-ttu-id="b17ae-263">текст</span><span class="sxs-lookup"><span data-stu-id="b17ae-263">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="b17ae-264">упорядоченный список</span><span class="sxs-lookup"><span data-stu-id="b17ae-264">ordered list</span></span> | <ol><li><span data-ttu-id="b17ae-265">текст</span><span class="sxs-lookup"><span data-stu-id="b17ae-265">text</span></span></li><li><span data-ttu-id="b17ae-266">текст</span><span class="sxs-lookup"><span data-stu-id="b17ae-266">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="b17ae-267">предформатированный текст</span><span class="sxs-lookup"><span data-stu-id="b17ae-267">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="b17ae-268">blockquote</span><span class="sxs-lookup"><span data-stu-id="b17ae-268">blockquote</span></span> | <blockquote><span data-ttu-id="b17ae-269">текст</span><span class="sxs-lookup"><span data-stu-id="b17ae-269">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="b17ae-270">гиперссылка</span><span class="sxs-lookup"><span data-stu-id="b17ae-270">hyperlink</span></span> | [<span data-ttu-id="b17ae-271">Bing</span><span class="sxs-lookup"><span data-stu-id="b17ae-271">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="b17ae-272">ссылка на изображение</span><span class="sxs-lookup"><span data-stu-id="b17ae-272">image link</span></span> | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

<span data-ttu-id="b17ae-273">В соединительных картах новые линии отрисовываются в HTML с помощью `<p>` тега.</span><span class="sxs-lookup"><span data-stu-id="b17ae-273">In connector cards, newlines are rendered in HTML using the `<p>` tag.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-html"></a><span data-ttu-id="b17ae-274">Различия между мобильными и настольными устройствами для соединительная карта с помощью HTML</span><span class="sxs-lookup"><span data-stu-id="b17ae-274">Mobile and desktop differences for connector cards using HTML</span></span>

<span data-ttu-id="b17ae-275">Форматирование HTML-форматов для соединительная карточки на рабочем столе выглядит так:</span><span class="sxs-lookup"><span data-stu-id="b17ae-275">On the desktop, HTML formatting for connector cards looks like this:</span></span>

![ФОРМАТирование HTML для соединителя карт в клиенте Desktop](../../assets/images/cards/Connector-desktop-html-combined.png)

<span data-ttu-id="b17ae-277">В iOS форматирование HTML выглядит так:</span><span class="sxs-lookup"><span data-stu-id="b17ae-277">On iOS, HTML formatting looks like this:</span></span>

![Форматирование HTML для соединительных карт в клиенте iOS](../../assets/images/cards/connector-iphone-html-combined-80.png)

<span data-ttu-id="b17ae-279">Вопросы:</span><span class="sxs-lookup"><span data-stu-id="b17ae-279">Issues:</span></span>

* <span data-ttu-id="b17ae-280">Встроенные изображения не отрисовываются в iOS с помощью markdown или HTML-кодов в соединителях.</span><span class="sxs-lookup"><span data-stu-id="b17ae-280">Inline images are not rendered on iOS using either Markdown or HTML in Connector Cards.</span></span>
* <span data-ttu-id="b17ae-281">Предформатированный текст отрисовывается, но не имеет серого фона.</span><span class="sxs-lookup"><span data-stu-id="b17ae-281">Preformatted text is rendered but does not have a gray background.</span></span>

<span data-ttu-id="b17ae-282">На Android форматирование HTML выглядит так:</span><span class="sxs-lookup"><span data-stu-id="b17ae-282">On Android, HTML formatting looks like this:</span></span>

![Форматирование HTML для соединительных карт в клиенте Android](../../assets/images/cards/connector-android-html-combined.png)

### <a name="formatting-sample-for-html-connector-cards"></a><span data-ttu-id="b17ae-284">Пример форматирования для HTML-карт соединителя</span><span class="sxs-lookup"><span data-stu-id="b17ae-284">Formatting sample for HTML Connector Cards</span></span>

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

# <a name="html-formatting-hero-and-thumbnail-cards"></a>[<span data-ttu-id="b17ae-285">**Форматирование HTML: карты героя и эскиза**</span><span class="sxs-lookup"><span data-stu-id="b17ae-285">**HTML Formatting: hero and thumbnail cards**</span></span>](#tab/simple-html)

<span data-ttu-id="b17ae-286">HTML-теги поддерживаются для простых карт, таких как карта героя и эскиза.</span><span class="sxs-lookup"><span data-stu-id="b17ae-286">HTML tags are supported for simple cards such as the hero and thumbnail card.</span></span> <span data-ttu-id="b17ae-287">Markdown не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="b17ae-287">Markdown is not supported.</span></span>

| <span data-ttu-id="b17ae-288">Style</span><span class="sxs-lookup"><span data-stu-id="b17ae-288">Style</span></span> | <span data-ttu-id="b17ae-289">Пример</span><span class="sxs-lookup"><span data-stu-id="b17ae-289">Example</span></span> | <span data-ttu-id="b17ae-290">HTML</span><span class="sxs-lookup"><span data-stu-id="b17ae-290">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b17ae-291">bold</span><span class="sxs-lookup"><span data-stu-id="b17ae-291">bold</span></span> | <span data-ttu-id="b17ae-292">**text**</span><span class="sxs-lookup"><span data-stu-id="b17ae-292">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="b17ae-293">italic</span><span class="sxs-lookup"><span data-stu-id="b17ae-293">italic</span></span> | <span data-ttu-id="b17ae-294">*text*</span><span class="sxs-lookup"><span data-stu-id="b17ae-294">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="b17ae-295">загон (уровни 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="b17ae-295">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="b17ae-296">**Text**</span><span class="sxs-lookup"><span data-stu-id="b17ae-296">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="b17ae-297">strikethrough</span><span class="sxs-lookup"><span data-stu-id="b17ae-297">strikethrough</span></span> | <span data-ttu-id="b17ae-298">~~text~~</span><span class="sxs-lookup"><span data-stu-id="b17ae-298">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="b17ae-299">необученный список</span><span class="sxs-lookup"><span data-stu-id="b17ae-299">unordered list</span></span> | <ul><li><span data-ttu-id="b17ae-300">текст</span><span class="sxs-lookup"><span data-stu-id="b17ae-300">text</span></span></li><li><span data-ttu-id="b17ae-301">текст</span><span class="sxs-lookup"><span data-stu-id="b17ae-301">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="b17ae-302">упорядоченный список</span><span class="sxs-lookup"><span data-stu-id="b17ae-302">ordered list</span></span> | <ol><li><span data-ttu-id="b17ae-303">текст</span><span class="sxs-lookup"><span data-stu-id="b17ae-303">text</span></span></li><li><span data-ttu-id="b17ae-304">текст</span><span class="sxs-lookup"><span data-stu-id="b17ae-304">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="b17ae-305">предформатированный текст</span><span class="sxs-lookup"><span data-stu-id="b17ae-305">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="b17ae-306">blockquote</span><span class="sxs-lookup"><span data-stu-id="b17ae-306">blockquote</span></span> | <blockquote><span data-ttu-id="b17ae-307">текст</span><span class="sxs-lookup"><span data-stu-id="b17ae-307">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="b17ae-308">гиперссылка</span><span class="sxs-lookup"><span data-stu-id="b17ae-308">hyperlink</span></span> | [<span data-ttu-id="b17ae-309">Bing</span><span class="sxs-lookup"><span data-stu-id="b17ae-309">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="b17ae-310">ссылка на изображение</span><span class="sxs-lookup"><span data-stu-id="b17ae-310">image link</span></span> |<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a><span data-ttu-id="b17ae-311">Различия для мобильных и настольных компьютеров для простых карт</span><span class="sxs-lookup"><span data-stu-id="b17ae-311">Mobile and desktop differences for simple cards</span></span>

<span data-ttu-id="b17ae-312">Из-за различий в разрешении между настольной и мобильной платформами форматирование отличается между настольным компьютером и мобильной версией Teams.</span><span class="sxs-lookup"><span data-stu-id="b17ae-312">Because of resolution differences between the desktop and mobile platform, formatting is different between the desktop and the mobile version of Teams.</span></span>

<span data-ttu-id="b17ae-313">На рабочем столе форматирование HTML выглядит так:</span><span class="sxs-lookup"><span data-stu-id="b17ae-313">On the desktop, HTML formatting appears like this:</span></span>

![Форматирование HTML в клиенте Desktop](../../assets/images/cards/card-formatting-xml-desktop-v2.png)

<span data-ttu-id="b17ae-315">На iOS форматирование HTML выглядит так:</span><span class="sxs-lookup"><span data-stu-id="b17ae-315">On iOS, HTML formatting appears like this:</span></span>

![Форматирование HTML в клиенте iOS](../../assets/images/cards/card-formatting-xml-mobile-v2.png)

<span data-ttu-id="b17ae-317">Вопросы:</span><span class="sxs-lookup"><span data-stu-id="b17ae-317">Issues:</span></span>

* <span data-ttu-id="b17ae-318">Форматирование символов, как смелый и italic, не отрисовка в iOS.</span><span class="sxs-lookup"><span data-stu-id="b17ae-318">Character formatting like bold and italic are not rendered on iOS.</span></span>

<span data-ttu-id="b17ae-319">На Android форматирование HTML выглядит так:</span><span class="sxs-lookup"><span data-stu-id="b17ae-319">On Android, HTML formatting appears like this:</span></span>

![Форматирование HTML в клиенте Android](../../assets/images/cards/card-formatting-xml-android-60.png)

<span data-ttu-id="b17ae-321">Форматирование символов, как смелый и italic отображения правильно на Android.</span><span class="sxs-lookup"><span data-stu-id="b17ae-321">Character formatting like bold and italic display correctly on Android.</span></span>

### <a name="formatting-sample-for-html-formatting-in-simple-cards"></a><span data-ttu-id="b17ae-322">Пример форматирования форматирования HTML в простых картах</span><span class="sxs-lookup"><span data-stu-id="b17ae-322">Formatting sample for HTML formatting in simple cards</span></span>

<span data-ttu-id="b17ae-323">Эти скриншоты были созданы с помощью Teams AppStudio, где текстовое свойство карты-героя было задано следующей строке.</span><span class="sxs-lookup"><span data-stu-id="b17ae-323">These screenshots were created using Teams AppStudio, where the text property of a hero card was set to the following string.</span></span> <span data-ttu-id="b17ae-324">Вы можете протестировать форматирование в собственных картах, изменяя этот код.</span><span class="sxs-lookup"><span data-stu-id="b17ae-324">You can test formatting in your own cards by modifying this code.</span></span>

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"https://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`

---
