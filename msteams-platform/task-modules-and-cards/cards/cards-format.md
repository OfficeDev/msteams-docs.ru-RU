---
title: Форматирование текста в картах
description: Описывает форматирование текста карты в Microsoft Teams
keywords: teams bots cards format
localization_priority: Normal
ms.topic: reference
ms.date: 03/29/2018
ms.openlocfilehash: 877a16f884e91138dc656434438a5fe1dd2ffd6e
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140639"
---
# <a name="format-cards-in-microsoft-teams"></a><span data-ttu-id="837ab-104">Форматирование карт в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="837ab-104">Format cards in Microsoft Teams</span></span>

<span data-ttu-id="837ab-105">Ниже приводится два способа добавления насыщенного форматирования текста в карты:</span><span class="sxs-lookup"><span data-stu-id="837ab-105">Following are the two ways to add rich text formatting to your cards:</span></span>
* [<span data-ttu-id="837ab-106">Markdown</span><span class="sxs-lookup"><span data-stu-id="837ab-106">Markdown</span></span>](#format-cards-with-markdown)
* [<span data-ttu-id="837ab-107">HTML</span><span class="sxs-lookup"><span data-stu-id="837ab-107">HTML</span></span>](#format-cards-with-html)

<span data-ttu-id="837ab-108">Карточки поддерживают форматирование только в свойстве текста, а не в свойствах заголовка или субтитров.</span><span class="sxs-lookup"><span data-stu-id="837ab-108">Cards support formatting in the text property only, not in the title or subtitle properties.</span></span> <span data-ttu-id="837ab-109">Форматирование можно задать с помощью подмножество форматирования XML или HTML или Markdown в зависимости от типа карты.</span><span class="sxs-lookup"><span data-stu-id="837ab-109">Formatting can be specified using a subset of XML or HTML formatting or Markdown, depending on the card type.</span></span> <span data-ttu-id="837ab-110">Для текущей и будущей разработки адаптивных карт рекомендуется форматирование Markdown.</span><span class="sxs-lookup"><span data-stu-id="837ab-110">For current and future development of Adaptive Cards, Markdown formatting is recommended.</span></span>

<span data-ttu-id="837ab-111">Поддержка форматирования отличается между типами карт.</span><span class="sxs-lookup"><span data-stu-id="837ab-111">Formatting support differs between card types.</span></span> <span data-ttu-id="837ab-112">Отрисовка карты может незначительно отличаться между настольным компьютером и мобильными Microsoft Teams клиентами, а также Teams в настольном браузере.</span><span class="sxs-lookup"><span data-stu-id="837ab-112">Rendering of the card can differ slightly between the desktop and the mobile Microsoft Teams clients, as well as Teams in the desktop browser.</span></span>

<span data-ttu-id="837ab-113">Вы можете включить в линию изображение с любой Teams карточкой.</span><span class="sxs-lookup"><span data-stu-id="837ab-113">You can include an inline image with any Teams card.</span></span> <span data-ttu-id="837ab-114">Изображения могут быть отформатированы как , или файлы и не должны превышать `.png` `.jpg` `.gif` 1024 ×1024 px или 1 МБ.</span><span class="sxs-lookup"><span data-stu-id="837ab-114">Images can be formatted as `.png`, `.jpg`, or `.gif` files and must not exceed 1024 ×1024 px or 1 MB.</span></span> <span data-ttu-id="837ab-115">Анимированный GIF не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="837ab-115">Animated GIF is not supported.</span></span> <span data-ttu-id="837ab-116">Дополнительные сведения см. [в некоторых видах карт.](./cards-reference.md#inline-card-images)</span><span class="sxs-lookup"><span data-stu-id="837ab-116">For more information, see [types of cards](./cards-reference.md#inline-card-images).</span></span>

<span data-ttu-id="837ab-117">Можно форматирование адаптивных карт и Office 365 соединительные карты с markdown, которые включают определенные поддерживаемые стили.</span><span class="sxs-lookup"><span data-stu-id="837ab-117">You can format Adaptive Cards and Office 365 Connector cards with Markdown that include certain supported styles.</span></span>

## <a name="format-cards-with-markdown"></a><span data-ttu-id="837ab-118">Формат карт с Markdown</span><span class="sxs-lookup"><span data-stu-id="837ab-118">Format cards with Markdown</span></span>

<span data-ttu-id="837ab-119">Следующие типы карт поддерживают форматирование Markdown в Teams:</span><span class="sxs-lookup"><span data-stu-id="837ab-119">The following card types support Markdown formatting in Teams:</span></span>

* <span data-ttu-id="837ab-120">Адаптивные карты: Markdown поддерживается в поле Адаптивная карта, а `Textblock` также `Fact.Title` и `Fact.Value` .</span><span class="sxs-lookup"><span data-stu-id="837ab-120">Adaptive Cards: Markdown is supported in Adaptive Card `Textblock` field, as well as `Fact.Title` and `Fact.Value`.</span></span> <span data-ttu-id="837ab-121">HTML не поддерживается в адаптивных картах.</span><span class="sxs-lookup"><span data-stu-id="837ab-121">HTML is not supported in Adaptive Cards.</span></span>
* <span data-ttu-id="837ab-122">Карты соединители O365: Markdown и ограниченный HTML поддерживаются в картах соединитель O365 в текстовых полях.</span><span class="sxs-lookup"><span data-stu-id="837ab-122">O365 Connector cards: Markdown and limited HTML is supported in O365 Connector cards in the text fields.</span></span>

<span data-ttu-id="837ab-123">Вы можете использовать newlines для адаптивных карт с помощью последовательностей или `\r` `\n` побега для newlines в списках.</span><span class="sxs-lookup"><span data-stu-id="837ab-123">You can use newlines for Adaptive Cards using `\r` or `\n` escape sequences for newlines in lists.</span></span> <span data-ttu-id="837ab-124">Форматирование отличается между настольным компьютером и мобильными версиями Teams адаптивных карт.</span><span class="sxs-lookup"><span data-stu-id="837ab-124">Formatting is different between the desktop and the mobile versions of Teams for Adaptive Cards.</span></span> <span data-ttu-id="837ab-125">Упоминания на основе карт поддерживаются в веб-, настольных и мобильных клиентах.</span><span class="sxs-lookup"><span data-stu-id="837ab-125">Card-based mentions are supported in web, desktop, and mobile clients.</span></span> <span data-ttu-id="837ab-126">Свойство маскировки информации можно использовать для маскировки определенных сведений, таких как пароль или конфиденциальные сведения пользователей в элементе ввода адаптивной `Input.Text` карты.</span><span class="sxs-lookup"><span data-stu-id="837ab-126">You can use the information masking property to mask specific information, such as password or sensitive information from users within the Adaptive Card `Input.Text` input element.</span></span> <span data-ttu-id="837ab-127">Ширину адаптивной карты можно расширить с помощью `width` объекта.</span><span class="sxs-lookup"><span data-stu-id="837ab-127">You can expand the width of an Adaptive Card using the `width` object.</span></span> <span data-ttu-id="837ab-128">Вы можете включить поддержку ввода в адаптивных картах и фильтровать набор вариантов ввода при типе ввода пользователем.</span><span class="sxs-lookup"><span data-stu-id="837ab-128">You can enable typeahead support within Adaptive Cards and filter the set of input choices as the user types the input.</span></span> <span data-ttu-id="837ab-129">Свойство можно использовать для выборочного отображения изображений `msteams` в представлении сцены.</span><span class="sxs-lookup"><span data-stu-id="837ab-129">You can use the `msteams` property to add the ability to display images in stage view selectively.</span></span>

<span data-ttu-id="837ab-130">Форматирование отличается между настольным компьютером и мобильными версиями Teams для адаптивных карт и соединительные карты.</span><span class="sxs-lookup"><span data-stu-id="837ab-130">Formatting is different between the desktop and the mobile versions of Teams for Adaptive Cards and connector cards.</span></span> <span data-ttu-id="837ab-131">В этом разделе можно перейти к примеру формата Markdown для адаптивных карт и соединительные карты.</span><span class="sxs-lookup"><span data-stu-id="837ab-131">In this section, you can go through the Markdown format example for Adaptive Cards and connector cards.</span></span>

# <a name="markdown-format-for-adaptive-cards"></a>[<span data-ttu-id="837ab-132">Формат markdown для адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="837ab-132">Markdown format for Adaptive Cards</span></span>](#tab/adaptive-md)

 <span data-ttu-id="837ab-133">Следующая таблица содержит поддерживаемые стили `Textblock` для `Fact.Title` , и `Fact.Value` :</span><span class="sxs-lookup"><span data-stu-id="837ab-133">The following table provides the supported styles for `Textblock`, `Fact.Title`, and `Fact.Value`:</span></span>

| <span data-ttu-id="837ab-134">Style</span><span class="sxs-lookup"><span data-stu-id="837ab-134">Style</span></span> | <span data-ttu-id="837ab-135">Пример</span><span class="sxs-lookup"><span data-stu-id="837ab-135">Example</span></span> | <span data-ttu-id="837ab-136">Markdown</span><span class="sxs-lookup"><span data-stu-id="837ab-136">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="837ab-137">Полужирный</span><span class="sxs-lookup"><span data-stu-id="837ab-137">Bold</span></span> | <span data-ttu-id="837ab-138">**Bold**</span><span class="sxs-lookup"><span data-stu-id="837ab-138">**Bold**</span></span> | ```**Bold**``` |
| <span data-ttu-id="837ab-139">Курсив</span><span class="sxs-lookup"><span data-stu-id="837ab-139">Italic</span></span> | <span data-ttu-id="837ab-140">_Italic_</span><span class="sxs-lookup"><span data-stu-id="837ab-140">_Italic_</span></span> | ```_Italic_``` |
| <span data-ttu-id="837ab-141">Неупорядоченный список</span><span class="sxs-lookup"><span data-stu-id="837ab-141">Unordered list</span></span> | <ul><li><span data-ttu-id="837ab-142">текст</span><span class="sxs-lookup"><span data-stu-id="837ab-142">text</span></span></li><li><span data-ttu-id="837ab-143">текст</span><span class="sxs-lookup"><span data-stu-id="837ab-143">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="837ab-144">Упорядоченный список</span><span class="sxs-lookup"><span data-stu-id="837ab-144">Ordered list</span></span> | <ol><li><span data-ttu-id="837ab-145">текст</span><span class="sxs-lookup"><span data-stu-id="837ab-145">text</span></span></li><li><span data-ttu-id="837ab-146">текст</span><span class="sxs-lookup"><span data-stu-id="837ab-146">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="837ab-147">Гиперссылки</span><span class="sxs-lookup"><span data-stu-id="837ab-147">Hyperlinks</span></span> |[<span data-ttu-id="837ab-148">Bing</span><span class="sxs-lookup"><span data-stu-id="837ab-148">Bing</span></span>](https://www.bing.com/)| ```[Title](url)``` |

<span data-ttu-id="837ab-149">Следующие теги Markdown не поддерживаются:</span><span class="sxs-lookup"><span data-stu-id="837ab-149">The following Markdown tags are not supported:</span></span>

* <span data-ttu-id="837ab-150">Заголовки</span><span class="sxs-lookup"><span data-stu-id="837ab-150">Headers</span></span>
* <span data-ttu-id="837ab-151">Таблицы</span><span class="sxs-lookup"><span data-stu-id="837ab-151">Tables</span></span>
* <span data-ttu-id="837ab-152">изображения;</span><span class="sxs-lookup"><span data-stu-id="837ab-152">Images</span></span>
* <span data-ttu-id="837ab-153">Предформатированный текст</span><span class="sxs-lookup"><span data-stu-id="837ab-153">Preformatted text</span></span>
* <span data-ttu-id="837ab-154">Blockquotes</span><span class="sxs-lookup"><span data-stu-id="837ab-154">Blockquotes</span></span>

### <a name="newlines-for-adaptive-cards"></a><span data-ttu-id="837ab-155">Newlines для адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="837ab-155">Newlines for Adaptive Cards</span></span>

<span data-ttu-id="837ab-156">Вы можете использовать `\r` последовательности или `\n` последовательности побега для newlines в списках.</span><span class="sxs-lookup"><span data-stu-id="837ab-156">You can use the `\r` or `\n` escape sequences for newlines in lists.</span></span> <span data-ttu-id="837ab-157">Использование `\n\n` в списках приводит к отступам следующего элемента в списке.</span><span class="sxs-lookup"><span data-stu-id="837ab-157">Using `\n\n` in lists causes the next element in the list to be indented.</span></span> <span data-ttu-id="837ab-158">Если вам требуются новые линии в другом месте в TextBlock, используйте `\n\n` .</span><span class="sxs-lookup"><span data-stu-id="837ab-158">If you require newlines elsewhere in the TextBlock, use `\n\n`.</span></span>

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a><span data-ttu-id="837ab-159">Различия для мобильных и настольных компьютеров для адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="837ab-159">Mobile and desktop differences for Adaptive Cards</span></span>

<span data-ttu-id="837ab-160">На рабочем столе форматирование адаптивной карты markdown отображается на следующем изображении как в веб-браузерах, так и в клиентском приложении Teams:</span><span class="sxs-lookup"><span data-stu-id="837ab-160">On the desktop, Adaptive Card Markdown formatting appears as shown in the following image in both web browsers and in the Teams client application:</span></span>

![Форматирование разметки адаптивной карты в клиенте настольных компьютеров](../../assets/images/cards/Adaptive-markdown-desktop-client.png)

<span data-ttu-id="837ab-162">На iOS форматирование разметки адаптивной карты отображается на следующем изображении:</span><span class="sxs-lookup"><span data-stu-id="837ab-162">On iOS, Adaptive Card Markdown formatting appears as shown in the following image:</span></span>

![Форматирование разметки адаптивной карты в iOS](../../assets/images/cards/Adaptive-markdown-iOS-75.png)

<span data-ttu-id="837ab-164">На Android форматирование разметки адаптивной карты отображается так, как показано на следующем изображении:</span><span class="sxs-lookup"><span data-stu-id="837ab-164">On Android, Adaptive Card Markdown formatting appears as shown in the following image:</span></span>

![Форматирование разметки адаптивной карты в Android](../../assets/images/cards/Adaptive-markdown-Android.png)

<span data-ttu-id="837ab-166">Дополнительные сведения см. в [текстовом документе Adaptive Cards.](/adaptive-cards/create/textfeatures)</span><span class="sxs-lookup"><span data-stu-id="837ab-166">For more information, see [text features in Adaptive Cards](/adaptive-cards/create/textfeatures).</span></span>

> [!NOTE]
> <span data-ttu-id="837ab-167">Указанные в этом разделе функции даты и локализации не поддерживаются в Teams.</span><span class="sxs-lookup"><span data-stu-id="837ab-167">The date and localization features mentioned in this section are not supported in Teams.</span></span>

### <a name="adaptive-cards-format-sample"></a><span data-ttu-id="837ab-168">Пример формата адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="837ab-168">Adaptive Cards format sample</span></span>

<span data-ttu-id="837ab-169">В следующем коде показан пример форматирования адаптивных карт:</span><span class="sxs-lookup"><span data-stu-id="837ab-169">The following code shows an example of Adaptive Cards formatting:</span></span>

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

### <a name="mention-support-within-adaptive-cards-v12"></a><span data-ttu-id="837ab-170">Упоминание поддержки в адаптивных картах v1.2</span><span class="sxs-lookup"><span data-stu-id="837ab-170">Mention support within Adaptive Cards v1.2</span></span>

<span data-ttu-id="837ab-171">Вы можете добавить @mentions в тело адаптивной карты для ботов и ответов расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="837ab-171">You can add @mentions within an Adaptive Card body for bots and messaging extension responses.</span></span> <span data-ttu-id="837ab-172">Чтобы добавить @mentions в карты, следуйте той же логике уведомлений и отрисовки, что и упоминания на основе сообщений в беседах каналов и [групповых чатов.](../../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions)</span><span class="sxs-lookup"><span data-stu-id="837ab-172">To add @mentions in cards, follow the same notification logic and rendering as that of message based [mentions in channel and group chat conversations](../../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions).</span></span>

<span data-ttu-id="837ab-173">Боты и расширения обмена сообщениями могут включать упоминания в контенте карты в [элементах TextBlock](https://adaptivecards.io/explorer/TextBlock.html) и [FactSet.](https://adaptivecards.io/explorer/FactSet.html)</span><span class="sxs-lookup"><span data-stu-id="837ab-173">Bots and messaging extensions can include mentions within the card content in [TextBlock](https://adaptivecards.io/explorer/TextBlock.html) and [FactSet](https://adaptivecards.io/explorer/FactSet.html) elements.</span></span>

> [!NOTE]
> * <span data-ttu-id="837ab-174">[Элементы мультимедиа в](https://adaptivecards.io/explorer/Media.html) настоящее время не поддерживаются в адаптивных картах v1.2 на Teams платформе.</span><span class="sxs-lookup"><span data-stu-id="837ab-174">[Media elements](https://adaptivecards.io/explorer/Media.html) are currently not supported in Adaptive Cards v1.2 on the Teams platform.</span></span>
> * <span data-ttu-id="837ab-175">Упоминания каналов и команд не поддерживаются в сообщениях ботов.</span><span class="sxs-lookup"><span data-stu-id="837ab-175">Channel and team mentions are not supported in bot messages.</span></span>

<span data-ttu-id="837ab-176">Чтобы включить упоминание в адаптивной карте, вашему приложению необходимо включить следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="837ab-176">To include a mention in an Adaptive Card, your app needs to include the following elements:</span></span>

* <span data-ttu-id="837ab-177">`<at>username</at>` в поддерживаемых элементах адаптивной карты.</span><span class="sxs-lookup"><span data-stu-id="837ab-177">`<at>username</at>` in the supported Adaptive Card elements.</span></span>
* <span data-ttu-id="837ab-178">Объект внутри свойства в содержимом карточки включает Teams имя пользователя `mention` `msteams` упоминаемого пользователя.</span><span class="sxs-lookup"><span data-stu-id="837ab-178">The `mention` object inside of an `msteams` property in the card content includes the Teams user ID of the user being mentioned.</span></span>
* <span data-ttu-id="837ab-179">Уникальный `userId` для вашего бот-ИД и определенного пользователя.</span><span class="sxs-lookup"><span data-stu-id="837ab-179">The `userId` is unique to your bot ID and a particular user.</span></span> <span data-ttu-id="837ab-180">Его можно использовать для @mention определенного пользователя.</span><span class="sxs-lookup"><span data-stu-id="837ab-180">It can be used to @mention a particular user.</span></span> <span data-ttu-id="837ab-181">Можно получить с помощью одного из параметров, указанных в `userId` получить [пользовательский ID](/microsoftteams/platform/bots/how-to/conversations/send-proactive-messages?tabs=dotnet#get-the-user-id-team-id-or-channel-id).</span><span class="sxs-lookup"><span data-stu-id="837ab-181">The `userId` can be retrieved using one of the options mentioned in [get the user ID](/microsoftteams/platform/bots/how-to/conversations/send-proactive-messages?tabs=dotnet#get-the-user-id-team-id-or-channel-id).</span></span>

#### <a name="sample-adaptive-card-with-a-mention"></a><span data-ttu-id="837ab-182">Пример адаптивной карты с упоминанием</span><span class="sxs-lookup"><span data-stu-id="837ab-182">Sample Adaptive Card with a mention</span></span>

<span data-ttu-id="837ab-183">В следующем коде показан пример адаптивной карты с упоминанием:</span><span class="sxs-lookup"><span data-stu-id="837ab-183">The following code shows an example of Adaptive Card with a mention:</span></span>

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

### <a name="information-masking-in-adaptive-cards"></a><span data-ttu-id="837ab-184">Маскировка сведений в адаптивных картах</span><span class="sxs-lookup"><span data-stu-id="837ab-184">Information masking in Adaptive Cards</span></span>

<span data-ttu-id="837ab-185">Используйте свойство маскировки информации для маскировки определенных сведений, таких как пароль или конфиденциальные сведения пользователей в элементе ввода адаптивной [`Input.Text`](https://adaptivecards.io/explorer/Input.Text.html) карты.</span><span class="sxs-lookup"><span data-stu-id="837ab-185">Use the information masking property to mask specific information, such as password or sensitive information from users within the Adaptive Card [`Input.Text`](https://adaptivecards.io/explorer/Input.Text.html) input element.</span></span>

> [!NOTE]
> <span data-ttu-id="837ab-186">Эта функция поддерживает только маскировку сведений из стороны клиента.</span><span class="sxs-lookup"><span data-stu-id="837ab-186">The feature only supports client side information masking.</span></span> <span data-ttu-id="837ab-187">Текст ввода в маске отправляется в виде четкого текста на адрес конечной точки HTTPS, заданный во время [конфигурации бота.](../../build-your-first-app/build-bot.md#4-register-your-bot-endpoint)</span><span class="sxs-lookup"><span data-stu-id="837ab-187">The masked input text is sent as clear text to the HTTPS endpoint address that was specified during [bot configuration](../../build-your-first-app/build-bot.md#4-register-your-bot-endpoint).</span></span>

<span data-ttu-id="837ab-188">Чтобы скрыть сведения в адаптивных картах, добавьте свойство для введите и установите `isMasked`  `Input.Text` значение true . </span><span class="sxs-lookup"><span data-stu-id="837ab-188">To mask information in Adaptive Cards, add the `isMasked` property to **type** `Input.Text`, and set its value to **true**.</span></span>

#### <a name="sample-adaptive-card-with-masking-property"></a><span data-ttu-id="837ab-189">Пример адаптивной карты с свойством маскировки</span><span class="sxs-lookup"><span data-stu-id="837ab-189">Sample Adaptive Card with masking property</span></span>

<span data-ttu-id="837ab-190">В следующем коде показан пример адаптивной карты с свойством маскировки:</span><span class="sxs-lookup"><span data-stu-id="837ab-190">The following code shows an example of Adaptive Card with masking property:</span></span>

```json
{
    "type": "Input.Text",
    "id": "secretThing",
    "style": "password",
},
```

<span data-ttu-id="837ab-191">Ниже приводится пример маскировки сведений в адаптивных картах:</span><span class="sxs-lookup"><span data-stu-id="837ab-191">The following image is an example of masking information in Adaptive Cards:</span></span>

![Маскировка информационного изображения](../../assets/images/cards/masking-information-view.png)

### <a name="full-width-adaptive-card"></a><span data-ttu-id="837ab-193">Адаптивная карта с полной шириной</span><span class="sxs-lookup"><span data-stu-id="837ab-193">Full width Adaptive Card</span></span>

<span data-ttu-id="837ab-194">Свойство можно использовать для расширения ширины адаптивной карты и использования `msteams` дополнительного пространства холста.</span><span class="sxs-lookup"><span data-stu-id="837ab-194">You can use the `msteams` property to expand the width of an Adaptive Card and make use of additional canvas space.</span></span> <span data-ttu-id="837ab-195">В следующем разделе приводится информация об использовании свойства.</span><span class="sxs-lookup"><span data-stu-id="837ab-195">The next section provides information on how to use the property.</span></span>

#### <a name="construct-full-width-cards"></a><span data-ttu-id="837ab-196">Создание карт полной ширины</span><span class="sxs-lookup"><span data-stu-id="837ab-196">Construct full width cards</span></span>

<span data-ttu-id="837ab-197">Чтобы сделать полную ширину адаптивной карты, объект в свойстве контента карточки должен `width` `msteams` быть задат. `Full`</span><span class="sxs-lookup"><span data-stu-id="837ab-197">To make a full width Adaptive Card, the `width` object in `msteams` property in the card content must be set to `Full`.</span></span>

#### <a name="sample-adaptive-card-with-full-width"></a><span data-ttu-id="837ab-198">Пример адаптивной карты с полной шириной</span><span class="sxs-lookup"><span data-stu-id="837ab-198">Sample Adaptive Card with full width</span></span>

<span data-ttu-id="837ab-199">Чтобы сделать полную ширину адаптивной карты, приложение должно включать элементы из следующего примера кода:</span><span class="sxs-lookup"><span data-stu-id="837ab-199">To make a full width Adaptive Card, your app must include the elements from the following code sample:</span></span>

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

<span data-ttu-id="837ab-200">На следующем изображении показана адаптивная карта с полной шириной:</span><span class="sxs-lookup"><span data-stu-id="837ab-200">The following image shows a full width Adaptive Card:</span></span>

![Представление адаптивной карты полной ширины](../../assets/images/cards/full-width-adaptive-card.png)

<span data-ttu-id="837ab-202">На следующем изображении по умолчанию показано представление адаптивной карты, если свойство не настроено `width` на **полное:**</span><span class="sxs-lookup"><span data-stu-id="837ab-202">The following image shows the default view of the Adaptive Card when you have not set the `width` property to **Full**:</span></span>

![Представление адаптивной карты малой ширины](../../assets/images/cards/small-width-adaptive-card.png)

### <a name="typeahead-support"></a><span data-ttu-id="837ab-204">Поддержка typeahead</span><span class="sxs-lookup"><span data-stu-id="837ab-204">Typeahead support</span></span>

<span data-ttu-id="837ab-205">В элементе схемы запрос пользователей на фильтрацию и выбор значительного числа вариантов может значительно замедлить [`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) завершение задачи.</span><span class="sxs-lookup"><span data-stu-id="837ab-205">Within the [`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) schema element, asking users to filter and select a sizeable number of choices can significantly slow down task completion.</span></span> <span data-ttu-id="837ab-206">Поддержка ввода в адаптивных картах может упростить выбор входных данных, сужая или фильтруя набор вариантов ввода при типе ввода пользователем.</span><span class="sxs-lookup"><span data-stu-id="837ab-206">Typeahead support within Adaptive Cards can simplify input selection by narrowing or filtering the set of input choices as the user types the input.</span></span>

<span data-ttu-id="837ab-207">Чтобы включить введите в `Input.Choiceset` течение , установить и обеспечить `style` `filtered` `isMultiSelect` установлено `false` .</span><span class="sxs-lookup"><span data-stu-id="837ab-207">To enable typeahead within the `Input.Choiceset`, set `style` to `filtered` and ensure `isMultiSelect` is set to `false`.</span></span>

#### <a name="sample-adaptive-card-with-typeahead-support"></a><span data-ttu-id="837ab-208">Пример адаптивной карты с поддержкой введите вперед</span><span class="sxs-lookup"><span data-stu-id="837ab-208">Sample Adaptive Card with typeahead support</span></span>

<span data-ttu-id="837ab-209">В следующем коде показан пример адаптивной карты с поддержкой заранее:</span><span class="sxs-lookup"><span data-stu-id="837ab-209">The following code shows an example of Adaptive Card with typeahead support:</span></span>

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

### <a name="stage-view-for-images-in-adaptive-cards"></a><span data-ttu-id="837ab-210">Представление сцены для изображений в адаптивных картах</span><span class="sxs-lookup"><span data-stu-id="837ab-210">Stage view for images in Adaptive Cards</span></span>

<span data-ttu-id="837ab-211">В адаптивной карте свойство можно использовать для выборочного отображения изображений в представлении `msteams` сцены.</span><span class="sxs-lookup"><span data-stu-id="837ab-211">In an Adaptive Card, you can use the `msteams` property to add the ability to display images in stage view selectively.</span></span> <span data-ttu-id="837ab-212">Когда пользователи наведите курсор над изображениями, они могут видеть значок расширения, для которого `allowExpand` атрибуту `true` установлено .</span><span class="sxs-lookup"><span data-stu-id="837ab-212">When users hover over the images, they can see an expand icon, for which the `allowExpand` attribute is set to `true`.</span></span> <span data-ttu-id="837ab-213">Сведения об использовании свойства см. в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="837ab-213">For information on how to use the property, see the following example:</span></span>

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

<span data-ttu-id="837ab-214">Когда пользователи наведите курсор над изображением, в правом верхнем углу появится значок расширения, как показано на следующем изображении:</span><span class="sxs-lookup"><span data-stu-id="837ab-214">When users hover over the image, an expand icon appears at the top right corner as shown in the following image:</span></span>

![Адаптивная карта с расширяемым изображением](../../assets/images/cards/adaptivecard-hover-expand-icon.png)

<span data-ttu-id="837ab-216">Изображение отображается в представлении сцены, когда пользователь выбирает значок расширения, как показано на следующем изображении:</span><span class="sxs-lookup"><span data-stu-id="837ab-216">The image appears in stage view when the user selects the expand icon as shown in the following image:</span></span>

![Изображение, расширенное до представления сцены](../../assets/images/cards/adaptivecard-expand-image.png)

<span data-ttu-id="837ab-218">В представлении сцены пользователи могут масштабировать изображение и увеличивать его.</span><span class="sxs-lookup"><span data-stu-id="837ab-218">In the stage view, users can zoom in and zoom out of the image.</span></span> <span data-ttu-id="837ab-219">Вы можете выбрать изображения в адаптивной карте, которые должны иметь эту возможность.</span><span class="sxs-lookup"><span data-stu-id="837ab-219">You can select the images in your Adaptive Card that must have this capability.</span></span>

> [!NOTE]
> * <span data-ttu-id="837ab-220">Возможность масштабирования и масштабирования применяется только к элементам изображения, которые являются типом изображения в адаптивной карте.</span><span class="sxs-lookup"><span data-stu-id="837ab-220">Zoom in and zoom out capability applies only to the image elements that is image type in an Adaptive Card.</span></span>
> * <span data-ttu-id="837ab-221">Для Teams мобильных приложений по умолчанию доступны функции представления сцен для изображений в адаптивных картах.</span><span class="sxs-lookup"><span data-stu-id="837ab-221">For Teams mobile apps, stage view functionality for images in Adaptive Cards is available by default.</span></span> <span data-ttu-id="837ab-222">Пользователи могут просматривать изображения адаптивной карты в представлении сцены, просто нажав на изображение, независимо от того, присутствует атрибут или `allowExpand` нет.</span><span class="sxs-lookup"><span data-stu-id="837ab-222">Users can view Adaptive Card images in stage view by simply tapping on the image, irrespective of whether the `allowExpand` attribute is present or not.</span></span>

# <a name="markdown-format-for-o365-connector-cards"></a>[<span data-ttu-id="837ab-223">Формат Markdown для карт соединителения O365</span><span class="sxs-lookup"><span data-stu-id="837ab-223">Markdown format for O365 Connector cards</span></span>](#tab/connector-md)

<span data-ttu-id="837ab-224">Карты Connector поддерживают ограниченное форматирование Markdown и HTML.</span><span class="sxs-lookup"><span data-stu-id="837ab-224">Connector cards support limited Markdown and HTML formatting.</span></span>

| <span data-ttu-id="837ab-225">Style</span><span class="sxs-lookup"><span data-stu-id="837ab-225">Style</span></span> | <span data-ttu-id="837ab-226">Пример</span><span class="sxs-lookup"><span data-stu-id="837ab-226">Example</span></span> | <span data-ttu-id="837ab-227">Markdown</span><span class="sxs-lookup"><span data-stu-id="837ab-227">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="837ab-228">Полужирный</span><span class="sxs-lookup"><span data-stu-id="837ab-228">Bold</span></span> | <span data-ttu-id="837ab-229">**text**</span><span class="sxs-lookup"><span data-stu-id="837ab-229">**text**</span></span> | `**text**` |
| <span data-ttu-id="837ab-230">Курсив</span><span class="sxs-lookup"><span data-stu-id="837ab-230">Italic</span></span> | <span data-ttu-id="837ab-231">*text*</span><span class="sxs-lookup"><span data-stu-id="837ab-231">*text*</span></span> | `*text*` |
| <span data-ttu-id="837ab-232">Загон (уровни 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="837ab-232">Header (levels 1&ndash;3)</span></span> | <span data-ttu-id="837ab-233">**Text**</span><span class="sxs-lookup"><span data-stu-id="837ab-233">**Text**</span></span> | `### Text`|
| <span data-ttu-id="837ab-234">Зачеркнутый</span><span class="sxs-lookup"><span data-stu-id="837ab-234">Strikethrough</span></span> | <span data-ttu-id="837ab-235">~~text~~</span><span class="sxs-lookup"><span data-stu-id="837ab-235">~~text~~</span></span> | `~~text~~` |
| <span data-ttu-id="837ab-236">Неупорядоченный список</span><span class="sxs-lookup"><span data-stu-id="837ab-236">Unordered list</span></span> | <ul><li><span data-ttu-id="837ab-237">текст</span><span class="sxs-lookup"><span data-stu-id="837ab-237">text</span></span></li><li><span data-ttu-id="837ab-238">текст</span><span class="sxs-lookup"><span data-stu-id="837ab-238">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="837ab-239">Упорядоченный список</span><span class="sxs-lookup"><span data-stu-id="837ab-239">Ordered list</span></span> | <ol><li><span data-ttu-id="837ab-240">текст</span><span class="sxs-lookup"><span data-stu-id="837ab-240">text</span></span></li><li><span data-ttu-id="837ab-241">текст</span><span class="sxs-lookup"><span data-stu-id="837ab-241">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="837ab-242">Предформатированный текст</span><span class="sxs-lookup"><span data-stu-id="837ab-242">Preformatted text</span></span> | `text` | ``preformatted text`` |
| <span data-ttu-id="837ab-243">Blockquote</span><span class="sxs-lookup"><span data-stu-id="837ab-243">Blockquote</span></span> | <span data-ttu-id="837ab-244">>блокквойта</span><span class="sxs-lookup"><span data-stu-id="837ab-244">>blockquote text</span></span> | `>blockquote text` |
| <span data-ttu-id="837ab-245">Hyperlink</span><span class="sxs-lookup"><span data-stu-id="837ab-245">Hyperlink</span></span> | [<span data-ttu-id="837ab-246">Bing</span><span class="sxs-lookup"><span data-stu-id="837ab-246">Bing</span></span>](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| <span data-ttu-id="837ab-247">Ссылка на изображение</span><span class="sxs-lookup"><span data-stu-id="837ab-247">Image link</span></span> |![Утка на скале](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

<span data-ttu-id="837ab-249">В соединитеных картах новые линии отрисовываются для `\n\n` , но не для или `\n` `\r` .</span><span class="sxs-lookup"><span data-stu-id="837ab-249">In connector cards, newlines are rendered for `\n\n`, but not for `\n` or `\r`.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards"></a><span data-ttu-id="837ab-250">Различия между мобильными и настольными устройствами для соединительная карта</span><span class="sxs-lookup"><span data-stu-id="837ab-250">Mobile and desktop differences for connector cards</span></span>

<span data-ttu-id="837ab-251">На рабочем столе форматирование Markdown для карт соединительная система отображается на следующем изображении:</span><span class="sxs-lookup"><span data-stu-id="837ab-251">On the desktop, Markdown formatting for connector cards appears as shown in the following image:</span></span>

![Форматирование разметки для соединительная карта в клиенте Desktop](../../assets/images/cards/connector-desktop-markdown-combined.png)

<span data-ttu-id="837ab-253">На iOS форматирование Markdown для карт соединителения отображается на следующем изображении:</span><span class="sxs-lookup"><span data-stu-id="837ab-253">On iOS, Markdown formatting for connector cards appears as shown in the following image:</span></span>

![Форматирование markdown для карт соединителения в клиенте iOS](../../assets/images/cards/connector-iphone-markdown-combined-80.png)

<span data-ttu-id="837ab-255">Карты соединителения, использующие Markdown для iOS, включают следующие проблемы:</span><span class="sxs-lookup"><span data-stu-id="837ab-255">Connector cards using Markdown for iOS include the following issues:</span></span>

* <span data-ttu-id="837ab-256">Клиент iOS для Teams не отрисовывает встроенные изображения Markdown или HTML в соединителях.</span><span class="sxs-lookup"><span data-stu-id="837ab-256">The iOS client for Teams does not render Markdown or HTML inline images in connector cards.</span></span>
* <span data-ttu-id="837ab-257">Блокквоты отрисовываются как отступные, но без серого фона.</span><span class="sxs-lookup"><span data-stu-id="837ab-257">Blockquotes are rendered as indented but without a gray background.</span></span>

<span data-ttu-id="837ab-258">На Android форматирование markdown для карт соединителения отображается на следующем изображении:</span><span class="sxs-lookup"><span data-stu-id="837ab-258">On Android, Markdown formatting for connector cards appears as shown in the following image:</span></span>

![Форматирование разметки для карт соединителения в клиенте Android](../../assets/images/cards/connector-android-markdown-combined.png)

### <a name="format-example-for-markdown-connector-cards"></a><span data-ttu-id="837ab-260">Пример формата для карт соединителения Markdown</span><span class="sxs-lookup"><span data-stu-id="837ab-260">Format example for Markdown connector cards</span></span>

<span data-ttu-id="837ab-261">В следующем коде показан пример форматирования для карт соединители Markdown:</span><span class="sxs-lookup"><span data-stu-id="837ab-261">The following code shows an example of formatting for Markdown connector cards:</span></span>

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

## <a name="format-cards-with-html"></a><span data-ttu-id="837ab-262">Форматные карты с HTML</span><span class="sxs-lookup"><span data-stu-id="837ab-262">Format cards with HTML</span></span>

<span data-ttu-id="837ab-263">Следующие типы карт поддерживают форматирование HTML в Teams:</span><span class="sxs-lookup"><span data-stu-id="837ab-263">The following card types support HTML formatting in Teams:</span></span>

* <span data-ttu-id="837ab-264">Карты соединители O365: ограниченное разметка и форматирование HTML поддерживаются в Office 365 соединителях.</span><span class="sxs-lookup"><span data-stu-id="837ab-264">O365 Connector cards: Limited Markdown and HTML formatting is supported in Office 365 Connector cards.</span></span>
* <span data-ttu-id="837ab-265">Карточки героя и эскиза: HTML-теги поддерживаются для простых карт, таких как карты героя и эскизы.</span><span class="sxs-lookup"><span data-stu-id="837ab-265">Hero and thumbnail cards: HTML tags are supported for simple cards, such as the hero and thumbnail cards.</span></span>

<span data-ttu-id="837ab-266">Форматирование отличается между настольным компьютером и мобильными версиями Teams для карт соединительная система O365 и простых карт.</span><span class="sxs-lookup"><span data-stu-id="837ab-266">Formatting is different between the desktop and the mobile versions of Teams for O365 Connector cards and simple cards.</span></span> <span data-ttu-id="837ab-267">В этом разделе можно перейти к примеру формата HTML для соединительных карт и простых карт.</span><span class="sxs-lookup"><span data-stu-id="837ab-267">In this section, you can go through the HTML format example for connector cards and simple cards.</span></span>

# <a name="html-format-for-o365-connector-cards"></a>[<span data-ttu-id="837ab-268">HTML-формат для карт соединителя O365</span><span class="sxs-lookup"><span data-stu-id="837ab-268">HTML format for O365 Connector cards</span></span>](#tab/connector-html)

<span data-ttu-id="837ab-269">Карты Connector поддерживают ограниченное форматирование Markdown и HTML.</span><span class="sxs-lookup"><span data-stu-id="837ab-269">Connector cards support limited Markdown and HTML formatting.</span></span>

| <span data-ttu-id="837ab-270">Style</span><span class="sxs-lookup"><span data-stu-id="837ab-270">Style</span></span> | <span data-ttu-id="837ab-271">Пример</span><span class="sxs-lookup"><span data-stu-id="837ab-271">Example</span></span> | <span data-ttu-id="837ab-272">HTML</span><span class="sxs-lookup"><span data-stu-id="837ab-272">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="837ab-273">Полужирный</span><span class="sxs-lookup"><span data-stu-id="837ab-273">Bold</span></span> | <span data-ttu-id="837ab-274">**text**</span><span class="sxs-lookup"><span data-stu-id="837ab-274">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="837ab-275">Курсив</span><span class="sxs-lookup"><span data-stu-id="837ab-275">Italic</span></span> | <span data-ttu-id="837ab-276">*text*</span><span class="sxs-lookup"><span data-stu-id="837ab-276">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="837ab-277">Загон (уровни 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="837ab-277">Header (levels 1&ndash;3)</span></span> | <span data-ttu-id="837ab-278">**Text**</span><span class="sxs-lookup"><span data-stu-id="837ab-278">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="837ab-279">Зачеркнутый</span><span class="sxs-lookup"><span data-stu-id="837ab-279">Strikethrough</span></span> | <span data-ttu-id="837ab-280">~~text~~</span><span class="sxs-lookup"><span data-stu-id="837ab-280">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="837ab-281">Неупорядоченный список</span><span class="sxs-lookup"><span data-stu-id="837ab-281">Unordered list</span></span> | <ul><li><span data-ttu-id="837ab-282">текст</span><span class="sxs-lookup"><span data-stu-id="837ab-282">text</span></span></li><li><span data-ttu-id="837ab-283">текст</span><span class="sxs-lookup"><span data-stu-id="837ab-283">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="837ab-284">Упорядоченный список</span><span class="sxs-lookup"><span data-stu-id="837ab-284">Ordered list</span></span> | <ol><li><span data-ttu-id="837ab-285">текст</span><span class="sxs-lookup"><span data-stu-id="837ab-285">text</span></span></li><li><span data-ttu-id="837ab-286">текст</span><span class="sxs-lookup"><span data-stu-id="837ab-286">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="837ab-287">Предформатированный текст</span><span class="sxs-lookup"><span data-stu-id="837ab-287">Preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="837ab-288">Blockquote</span><span class="sxs-lookup"><span data-stu-id="837ab-288">Blockquote</span></span> | <blockquote><span data-ttu-id="837ab-289">текст</span><span class="sxs-lookup"><span data-stu-id="837ab-289">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="837ab-290">Hyperlink</span><span class="sxs-lookup"><span data-stu-id="837ab-290">Hyperlink</span></span> | [<span data-ttu-id="837ab-291">Bing</span><span class="sxs-lookup"><span data-stu-id="837ab-291">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="837ab-292">Ссылка на изображение</span><span class="sxs-lookup"><span data-stu-id="837ab-292">Image link</span></span> | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

<span data-ttu-id="837ab-293">В соединительных картах новые линии отрисовываются в HTML с помощью `<p>` тега.</span><span class="sxs-lookup"><span data-stu-id="837ab-293">In connector cards, newlines are rendered in HTML using the `<p>` tag.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards"></a><span data-ttu-id="837ab-294">Различия между мобильными и настольными устройствами для соединительная карта</span><span class="sxs-lookup"><span data-stu-id="837ab-294">Mobile and desktop differences for connector cards</span></span>

<span data-ttu-id="837ab-295">На рабочем столе форматирование HTML-форматов для карт соединителя отображается на следующем изображении:</span><span class="sxs-lookup"><span data-stu-id="837ab-295">On the desktop, HTML formatting for connector cards appears as shown in the following image:</span></span>

![Форматирование HTML для соединителя карт в клиенте рабочего стола](../../assets/images/cards/Connector-desktop-html-combined.png)

<span data-ttu-id="837ab-297">На iOS форматирование HTML отображается на следующем изображении:</span><span class="sxs-lookup"><span data-stu-id="837ab-297">On iOS, HTML formatting appears as shown in the following image:</span></span>

![Форматирование HTML для соединительных карт в клиенте iOS](../../assets/images/cards/connector-iphone-html-combined-80.png)

<span data-ttu-id="837ab-299">Карты соединителя, использующие HTML для iOS, включают следующие проблемы:</span><span class="sxs-lookup"><span data-stu-id="837ab-299">Connector cards using HTML for iOS include the following issues:</span></span>

* <span data-ttu-id="837ab-300">Встроенные изображения не отрисовываются на iOS с помощью markdown или HTML в соединителях.</span><span class="sxs-lookup"><span data-stu-id="837ab-300">Inline images are not rendered on iOS using either Markdown or HTML in connector cards.</span></span>
* <span data-ttu-id="837ab-301">Предформатированный текст отрисовывается, но не имеет серого фона.</span><span class="sxs-lookup"><span data-stu-id="837ab-301">Preformatted text is rendered but does not have a gray background.</span></span>

<span data-ttu-id="837ab-302">На Android форматирование HTML отображается на следующем изображении:</span><span class="sxs-lookup"><span data-stu-id="837ab-302">On Android, HTML formatting appears as shown in the following image:</span></span>

![Форматирование HTML для соединительных карт в клиенте Android](../../assets/images/cards/connector-android-html-combined.png)

### <a name="format-sample-for-html-connector-cards"></a><span data-ttu-id="837ab-304">Пример формата для htmL-соединителя карт</span><span class="sxs-lookup"><span data-stu-id="837ab-304">Format sample for HTML connector cards</span></span>

<span data-ttu-id="837ab-305">В следующем коде показан пример форматирования для htmL-соединителя карт:</span><span class="sxs-lookup"><span data-stu-id="837ab-305">The following code shows an example of formatting for HTML connector cards:</span></span>

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

# <a name="html-format-for-hero-and-thumbnail-cards"></a>[<span data-ttu-id="837ab-306">HTML-формат для карт-героев и эскизов</span><span class="sxs-lookup"><span data-stu-id="837ab-306">HTML format for hero and thumbnail cards</span></span>](#tab/simple-html)

<span data-ttu-id="837ab-307">HTML-теги поддерживаются для простых карт, таких как карты героя и эскизы.</span><span class="sxs-lookup"><span data-stu-id="837ab-307">HTML tags are supported for simple cards, such as the hero and thumbnail cards.</span></span> <span data-ttu-id="837ab-308">Markdown не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="837ab-308">Markdown is not supported.</span></span>

| <span data-ttu-id="837ab-309">Style</span><span class="sxs-lookup"><span data-stu-id="837ab-309">Style</span></span> | <span data-ttu-id="837ab-310">Пример</span><span class="sxs-lookup"><span data-stu-id="837ab-310">Example</span></span> | <span data-ttu-id="837ab-311">HTML</span><span class="sxs-lookup"><span data-stu-id="837ab-311">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="837ab-312">Полужирный</span><span class="sxs-lookup"><span data-stu-id="837ab-312">Bold</span></span> | <span data-ttu-id="837ab-313">**text**</span><span class="sxs-lookup"><span data-stu-id="837ab-313">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="837ab-314">Курсив</span><span class="sxs-lookup"><span data-stu-id="837ab-314">Italic</span></span> | <span data-ttu-id="837ab-315">*text*</span><span class="sxs-lookup"><span data-stu-id="837ab-315">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="837ab-316">Загон (уровни 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="837ab-316">Header (levels 1&ndash;3)</span></span> | <span data-ttu-id="837ab-317">**Text**</span><span class="sxs-lookup"><span data-stu-id="837ab-317">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="837ab-318">Зачеркнутый</span><span class="sxs-lookup"><span data-stu-id="837ab-318">Strikethrough</span></span> | <span data-ttu-id="837ab-319">~~text~~</span><span class="sxs-lookup"><span data-stu-id="837ab-319">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="837ab-320">Неупорядоченный список</span><span class="sxs-lookup"><span data-stu-id="837ab-320">Unordered list</span></span> | <ul><li><span data-ttu-id="837ab-321">текст</span><span class="sxs-lookup"><span data-stu-id="837ab-321">text</span></span></li><li><span data-ttu-id="837ab-322">текст</span><span class="sxs-lookup"><span data-stu-id="837ab-322">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="837ab-323">Упорядоченный список</span><span class="sxs-lookup"><span data-stu-id="837ab-323">Ordered list</span></span> | <ol><li><span data-ttu-id="837ab-324">текст</span><span class="sxs-lookup"><span data-stu-id="837ab-324">text</span></span></li><li><span data-ttu-id="837ab-325">текст</span><span class="sxs-lookup"><span data-stu-id="837ab-325">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="837ab-326">Предформатированный текст</span><span class="sxs-lookup"><span data-stu-id="837ab-326">Preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="837ab-327">Blockquote</span><span class="sxs-lookup"><span data-stu-id="837ab-327">Blockquote</span></span> | <blockquote><span data-ttu-id="837ab-328">текст</span><span class="sxs-lookup"><span data-stu-id="837ab-328">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="837ab-329">Hyperlink</span><span class="sxs-lookup"><span data-stu-id="837ab-329">Hyperlink</span></span> | [<span data-ttu-id="837ab-330">Bing</span><span class="sxs-lookup"><span data-stu-id="837ab-330">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="837ab-331">Ссылка на изображение</span><span class="sxs-lookup"><span data-stu-id="837ab-331">Image link</span></span> |<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a><span data-ttu-id="837ab-332">Различия для мобильных и настольных компьютеров для простых карт</span><span class="sxs-lookup"><span data-stu-id="837ab-332">Mobile and desktop differences for simple cards</span></span>

<span data-ttu-id="837ab-333">Поскольку между настольной и мобильной платформами существуют различия в разрешении, форматирование отличается между настольным компьютером и мобильной версией Teams.</span><span class="sxs-lookup"><span data-stu-id="837ab-333">As there are resolution differences between the desktop and mobile platform, formatting is different between the desktop and the mobile version of Teams.</span></span>

<span data-ttu-id="837ab-334">На рабочем столе форматирование HTML отображается на следующем изображении:</span><span class="sxs-lookup"><span data-stu-id="837ab-334">On the desktop, HTML formatting appears as shown in the following image:</span></span>

![Форматирование HTML в клиенте рабочего стола](../../assets/images/cards/card-formatting-xml-desktop-v2.png)

<span data-ttu-id="837ab-336">На iOS форматирование HTML отображается на следующем изображении:</span><span class="sxs-lookup"><span data-stu-id="837ab-336">On iOS, HTML formatting appears as shown in the following image:</span></span>

![Форматирование HTML в клиенте iOS](../../assets/images/cards/card-formatting-xml-mobile-v2.png)

<span data-ttu-id="837ab-338">Форматирование символов, таких как смелый и italic, не отрисовывался на iOS.</span><span class="sxs-lookup"><span data-stu-id="837ab-338">Character formatting, such as bold and italic are not rendered on iOS.</span></span>

<span data-ttu-id="837ab-339">На Android форматирование HTML отображается на следующем изображении:</span><span class="sxs-lookup"><span data-stu-id="837ab-339">On Android, HTML formatting appears as shown in the following image:</span></span>

![Форматирование HTML в клиенте Android](../../assets/images/cards/card-formatting-xml-android-60.png)

<span data-ttu-id="837ab-341">Форматирование символов, таких как смелый и italic отображения правильно на Android.</span><span class="sxs-lookup"><span data-stu-id="837ab-341">Character formatting, such as bold and italic display correctly on Android.</span></span>

### <a name="format-example-for-simple-cards"></a><span data-ttu-id="837ab-342">Пример формата для простых карт</span><span class="sxs-lookup"><span data-stu-id="837ab-342">Format example for simple cards</span></span>

<span data-ttu-id="837ab-343">Изображения в предыдущем разделе были созданы с Teams **App Studio,** где текстовое свойство карты-героя задалось следующей строке:</span><span class="sxs-lookup"><span data-stu-id="837ab-343">The images in the previous section were created using Teams **App Studio**, where the text property of a hero card is set to the following string:</span></span>

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"https://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`

<span data-ttu-id="837ab-344">Вы можете протестировать форматирование в собственных картах, изменяя этот код.</span><span class="sxs-lookup"><span data-stu-id="837ab-344">You can test formatting in your own cards by modifying this code.</span></span>

---

## <a name="see-also"></a><span data-ttu-id="837ab-345">См. также</span><span class="sxs-lookup"><span data-stu-id="837ab-345">See also</span></span>

* [<span data-ttu-id="837ab-346">Действия карты</span><span class="sxs-lookup"><span data-stu-id="837ab-346">Card actions</span></span>](./cards-actions.md)
* [<span data-ttu-id="837ab-347">Модули задач</span><span class="sxs-lookup"><span data-stu-id="837ab-347">Task modules</span></span>](~/task-modules-and-cards/cards/cards-format.md)
