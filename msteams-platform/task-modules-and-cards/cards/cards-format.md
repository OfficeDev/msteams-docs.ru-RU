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
# <a name="format-cards-in-teams"></a><span data-ttu-id="e1e3c-104">Форматные карты в Teams</span><span class="sxs-lookup"><span data-stu-id="e1e3c-104">Format cards in Teams</span></span>

<span data-ttu-id="e1e3c-105">Вы можете добавить богатый текстовый форматирование в карты, используя Либо Markdown или HTML, в зависимости от типа карты.</span><span class="sxs-lookup"><span data-stu-id="e1e3c-105">You can add rich text formatting to your cards using either Markdown or HTML, depending on the card type.</span></span>

<span data-ttu-id="e1e3c-106">Карты поддерживают форматирование только в свойстве текста, а не в свойствах заголовка или субтитра.</span><span class="sxs-lookup"><span data-stu-id="e1e3c-106">Cards support formatting in the text property only, not in the title or subtitle properties.</span></span> <span data-ttu-id="e1e3c-107">Форматирование может быть указано с помощью подмножества форматирования XML (HTML) или Markdown в зависимости от типа карты.</span><span class="sxs-lookup"><span data-stu-id="e1e3c-107">Formatting can be specified using a subset of XML (HTML) formatting, or Markdown depending on card type.</span></span> <span data-ttu-id="e1e3c-108">Для текущей и будущей разработки рекомендуются адаптивные карты с использованием форматирования Markdown.</span><span class="sxs-lookup"><span data-stu-id="e1e3c-108">For current and future development Adaptive cards using Markdown formatting is recommended.</span></span>

<span data-ttu-id="e1e3c-109">Поддержка форматирования отличается между различными типами карт, и визуализация карты может немного отличаться между настольным и мобильным Teams клиентами, а также Teams в настольном браузере.</span><span class="sxs-lookup"><span data-stu-id="e1e3c-109">Formatting support differs between different card types, and rendering of the card can differ slightly between the desktop and the mobile Teams clients, as well as Teams in the desktop browser.</span></span>

<span data-ttu-id="e1e3c-110">Вы можете включить изображение в линию с любой Teams картой.</span><span class="sxs-lookup"><span data-stu-id="e1e3c-110">You can include an inline image with any Teams card.</span></span> <span data-ttu-id="e1e3c-111">Изображения отформатированы  `.png` как , `.jpg` или `.gif` файлы и не должны превышать 1024 ×1024 px или 1 MB.</span><span class="sxs-lookup"><span data-stu-id="e1e3c-111">Images an be formatted as  `.png`, `.jpg`, or `.gif` files and must not exceed 1024 ×1024 px or 1 MB.</span></span> <span data-ttu-id="e1e3c-112">Анимированный GIF официально не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="e1e3c-112">Animated GIF is not officially supported.</span></span> <span data-ttu-id="e1e3c-113">Для получения дополнительной информации [см.](./cards-reference.md#inline-card-images)</span><span class="sxs-lookup"><span data-stu-id="e1e3c-113">For more information, see [Cards reference](./cards-reference.md#inline-card-images).</span></span>

## <a name="formatting-cards-with-markdown"></a><span data-ttu-id="e1e3c-114">Форматирование карт с Markdown</span><span class="sxs-lookup"><span data-stu-id="e1e3c-114">Formatting cards with Markdown</span></span>

<span data-ttu-id="e1e3c-115">Есть два типа карт, которые поддерживают Markdown в Teams:</span><span class="sxs-lookup"><span data-stu-id="e1e3c-115">There are two card types that support Markdown in Teams:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e1e3c-116">**Адаптивные** карты : Markdown поддерживается в области `Textblock` адаптивных карт, а также `Fact.Title` `Fact.Value` и .</span><span class="sxs-lookup"><span data-stu-id="e1e3c-116">**Adaptive cards**: Markdown is supported in Adaptive card `Textblock` field, as well as `Fact.Title` and `Fact.Value`.</span></span> <span data-ttu-id="e1e3c-117">HTML не поддерживается в адаптивных картах.</span><span class="sxs-lookup"><span data-stu-id="e1e3c-117">HTML is not supported in Adaptive cards.</span></span>
> * <span data-ttu-id="e1e3c-118">**O365 Connector Cards**: Markdown и ограниченный HTML поддерживается в Office 365-коннекторных карт в текстовых полях.</span><span class="sxs-lookup"><span data-stu-id="e1e3c-118">**O365 Connector Cards**: Markdown and limited HTML is supported in Office 365 Connector cards in the text fields.</span></span>

# <a name="markdown-formatting-adaptive-cards"></a>[<span data-ttu-id="e1e3c-119">**Форматирование разметки: Адаптивные карты**</span><span class="sxs-lookup"><span data-stu-id="e1e3c-119">**Markdown formatting: Adaptive cards**</span></span>](#tab/adaptive-md)

 <span data-ttu-id="e1e3c-120">Поддерживаемые стили `Textblock` для , и `Fact.Title` `Fact.Value` являются:</span><span class="sxs-lookup"><span data-stu-id="e1e3c-120">The supported styles for `Textblock`, `Fact.Title` and `Fact.Value` are:</span></span>

| <span data-ttu-id="e1e3c-121">Style</span><span class="sxs-lookup"><span data-stu-id="e1e3c-121">Style</span></span> | <span data-ttu-id="e1e3c-122">Пример</span><span class="sxs-lookup"><span data-stu-id="e1e3c-122">Example</span></span> | <span data-ttu-id="e1e3c-123">Markdown</span><span class="sxs-lookup"><span data-stu-id="e1e3c-123">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e1e3c-124">bold</span><span class="sxs-lookup"><span data-stu-id="e1e3c-124">bold</span></span> | <span data-ttu-id="e1e3c-125">**Bold**</span><span class="sxs-lookup"><span data-stu-id="e1e3c-125">**Bold**</span></span> | ```**Bold**``` |
| <span data-ttu-id="e1e3c-126">italic</span><span class="sxs-lookup"><span data-stu-id="e1e3c-126">italic</span></span> | <span data-ttu-id="e1e3c-127">_Italic_</span><span class="sxs-lookup"><span data-stu-id="e1e3c-127">_Italic_</span></span> | ```_Italic_``` |
| <span data-ttu-id="e1e3c-128">неупорядочеченный список</span><span class="sxs-lookup"><span data-stu-id="e1e3c-128">unordered list</span></span> | <ul><li><span data-ttu-id="e1e3c-129">текст</span><span class="sxs-lookup"><span data-stu-id="e1e3c-129">text</span></span></li><li><span data-ttu-id="e1e3c-130">текст</span><span class="sxs-lookup"><span data-stu-id="e1e3c-130">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="e1e3c-131">упорядоченный список</span><span class="sxs-lookup"><span data-stu-id="e1e3c-131">ordered list</span></span> | <ol><li><span data-ttu-id="e1e3c-132">текст</span><span class="sxs-lookup"><span data-stu-id="e1e3c-132">text</span></span></li><li><span data-ttu-id="e1e3c-133">текст</span><span class="sxs-lookup"><span data-stu-id="e1e3c-133">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="e1e3c-134">Гиперссылки</span><span class="sxs-lookup"><span data-stu-id="e1e3c-134">Hyperlinks</span></span> |[<span data-ttu-id="e1e3c-135">Bing</span><span class="sxs-lookup"><span data-stu-id="e1e3c-135">Bing</span></span>](https://www.bing.com/)| ```[Title](url)``` |

<span data-ttu-id="e1e3c-136">Следующие теги Markdown не поддерживаются:</span><span class="sxs-lookup"><span data-stu-id="e1e3c-136">The following Markdown tags are not supported:</span></span>

* <span data-ttu-id="e1e3c-137">Заголовки</span><span class="sxs-lookup"><span data-stu-id="e1e3c-137">Headers</span></span>
* <span data-ttu-id="e1e3c-138">Таблицы</span><span class="sxs-lookup"><span data-stu-id="e1e3c-138">Tables</span></span>
* <span data-ttu-id="e1e3c-139">изображения;</span><span class="sxs-lookup"><span data-stu-id="e1e3c-139">Images</span></span>
* <span data-ttu-id="e1e3c-140">Предварительноформированный текст</span><span class="sxs-lookup"><span data-stu-id="e1e3c-140">Preformatted text</span></span>
* <span data-ttu-id="e1e3c-141">Блокциты</span><span class="sxs-lookup"><span data-stu-id="e1e3c-141">Blockquotes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e1e3c-142">Адаптивные карты не поддерживают форматирование HTML.</span><span class="sxs-lookup"><span data-stu-id="e1e3c-142">Adaptive cards do not support HTML formatting.</span></span>

### <a name="newlines-for-adaptive-cards"></a><span data-ttu-id="e1e3c-143">Новые линии для адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="e1e3c-143">Newlines for Adaptive cards</span></span>

<span data-ttu-id="e1e3c-144">В списках вы можете использовать `\r` `\n` последовательности или избежать для новых линий.</span><span class="sxs-lookup"><span data-stu-id="e1e3c-144">In lists you can use the `\r` or `\n` escape sequences for newlines.</span></span> <span data-ttu-id="e1e3c-145">Использование `\n\n` в списке приведет к отступу следующего элемента в списке.</span><span class="sxs-lookup"><span data-stu-id="e1e3c-145">Using `\n\n` in a list will cause the next element in the list to be indented.</span></span> <span data-ttu-id="e1e3c-146">Если вам нужны новые строки в другом месте в текстовом блоке, используйте `\n\n` .</span><span class="sxs-lookup"><span data-stu-id="e1e3c-146">If you need newlines elsewhere in the textblock, use `\n\n`.</span></span>

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a><span data-ttu-id="e1e3c-147">Мобильные и настольные различия для адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="e1e3c-147">Mobile and desktop differences for Adaptive cards</span></span>

<span data-ttu-id="e1e3c-148">Форматирование немного отличается между настольными и мобильными версиями Teams.</span><span class="sxs-lookup"><span data-stu-id="e1e3c-148">Formatting is slightly different between the desktop and the mobile versions of Teams.</span></span>

<span data-ttu-id="e1e3c-149">На рабочем столе форматирование Adaptive card Markdown выглядит так как в веб-браузерах, так и в Teams клиентском приложении:</span><span class="sxs-lookup"><span data-stu-id="e1e3c-149">On the desktop, Adaptive card Markdown formatting appears like this in both web browsers and in the Teams client application:</span></span>

![Форматирование адаптивной карты Markdown в настольном клиенте](../../assets/images/cards/Adaptive-markdown-desktop-client.png)

<span data-ttu-id="e1e3c-151">На iOS форматирование Adaptive card Markdown выглядит так:</span><span class="sxs-lookup"><span data-stu-id="e1e3c-151">On iOS, Adaptive card Markdown formatting appears like this:</span></span>

![Форматирование адаптивной карты Markdown в iOS](../../assets/images/cards/Adaptive-markdown-iOS-75.png)

<span data-ttu-id="e1e3c-153">На Android форматирование Adaptive Card Markdown выглядит так:</span><span class="sxs-lookup"><span data-stu-id="e1e3c-153">On Android, Adaptive Card Markdown formatting appears like this:</span></span>

![Форматирование адаптивной карты Markdown в Android](../../assets/images/cards/Adaptive-markdown-Android.png)

### <a name="more-information-on-adaptive-cards"></a><span data-ttu-id="e1e3c-155">Более подробная информация об адаптивных картах</span><span class="sxs-lookup"><span data-stu-id="e1e3c-155">More information on Adaptive cards</span></span>

<span data-ttu-id="e1e3c-156">[Текстовые функции в адаптивных картах](/adaptive-cards/create/textfeatures) Упомянутые в этой теме функции даты и локализации не поддерживаются в Teams.</span><span class="sxs-lookup"><span data-stu-id="e1e3c-156">[Text features in Adaptive cards](/adaptive-cards/create/textfeatures) The date and localization features mentioned in this topic are not supported in Teams.</span></span>

### <a name="formatting-sample-for-adaptive-cards"></a><span data-ttu-id="e1e3c-157">Образец форматирования для адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="e1e3c-157">Formatting sample for Adaptive cards</span></span>

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

### <a name="mention-support-within-adaptive-cards-v12"></a><span data-ttu-id="e1e3c-158">Поддержка упоминания в адаптивных картах v1.2</span><span class="sxs-lookup"><span data-stu-id="e1e3c-158">Mention support within Adaptive cards v1.2</span></span>

<span data-ttu-id="e1e3c-159">Упоминания на основе карт поддерживаются в веб-, настольных и мобильных клиентах.</span><span class="sxs-lookup"><span data-stu-id="e1e3c-159">Card based mentions are supported in web, desktop and mobile clients.</span></span> <span data-ttu-id="e1e3c-160">Вы можете добавить упоминания в тело адаптивной карты для ботов и ответов на расширение обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="e1e3c-160">You can add @ mentions within an adaptive card body for bots and messaging extension responses.</span></span> <span data-ttu-id="e1e3c-161">Чтобы добавить упоминания в карты, следуйте той же логике уведомлений и визуализации, что и упоминания на [основе сообщений в разговорах в канале и групповом чате.](../../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions)</span><span class="sxs-lookup"><span data-stu-id="e1e3c-161">To add @ mentions in cards, follow the same notification logic and rendering as that of message based [mentions in channel and group chat conversations](../../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions).</span></span>

<span data-ttu-id="e1e3c-162">Боты и расширения обмена сообщениями могут включать упоминания в содержимом карты в [элементах TextBlock](https://adaptivecards.io/explorer/TextBlock.html) [и FactSet.](https://adaptivecards.io/explorer/FactSet.html)</span><span class="sxs-lookup"><span data-stu-id="e1e3c-162">Bots and messaging extensions can include mentions within the card content in [TextBlock](https://adaptivecards.io/explorer/TextBlock.html) and [FactSet](https://adaptivecards.io/explorer/FactSet.html) elements.</span></span>

> [!NOTE]
> * <span data-ttu-id="e1e3c-163">[Медиа-элементы](https://adaptivecards.io/explorer/Media.html) в настоящее время не поддерживаются в адаптивных картах v1.2 Teams платформе.</span><span class="sxs-lookup"><span data-stu-id="e1e3c-163">[Media elements](https://adaptivecards.io/explorer/Media.html) are currently not supported in Adaptive cards v1.2 on the Teams platform.</span></span>
> * <span data-ttu-id="e1e3c-164">Упоминания & channel & не поддерживаются в сообщениях ботов.</span><span class="sxs-lookup"><span data-stu-id="e1e3c-164">Channel & Team mentions are not supported in bot messages.</span></span>

#### <a name="constructing-mentions"></a><span data-ttu-id="e1e3c-165">Строительство упоминаний</span><span class="sxs-lookup"><span data-stu-id="e1e3c-165">Constructing mentions</span></span>

<span data-ttu-id="e1e3c-166">Чтобы включить упоминание в адаптивную карту, приложение должно включить следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="e1e3c-166">To include a mention in an Adaptive Card your app needs to include the following elements:</span></span>

* <span data-ttu-id="e1e3c-167">`<at>username</at>` в поддерживаемых адаптивных элементах карты.</span><span class="sxs-lookup"><span data-stu-id="e1e3c-167">`<at>username</at>` in the supported Adaptive card elements.</span></span>
* <span data-ttu-id="e1e3c-168">Объект `mention` внутри свойства в `msteams` содержимом карты, который включает в себя Teams идентификатор пользователя, упомянутого.</span><span class="sxs-lookup"><span data-stu-id="e1e3c-168">The `mention` object inside of an `msteams` property in the card content, which includes the Teams user id of the user being mentioned.</span></span>
* <span data-ttu-id="e1e3c-169">Уникальный `userId` для вашего бота ID и конкретного пользователя.</span><span class="sxs-lookup"><span data-stu-id="e1e3c-169">The `userId` is unique to your bot ID and a particular user.</span></span> <span data-ttu-id="e1e3c-170">Он может быть использован для @mention конкретного пользователя.</span><span class="sxs-lookup"><span data-stu-id="e1e3c-170">It can be used to @mention a particular user.</span></span> <span data-ttu-id="e1e3c-171">Можно `userId` получить с помощью одного из вариантов, упомянутых [в получить идентификатор пользователя](/microsoftteams/platform/bots/how-to/conversations/send-proactive-messages?tabs=dotnet#get-the-user-id-team-id-or-channel-id).</span><span class="sxs-lookup"><span data-stu-id="e1e3c-171">The `userId` can be retrieved using one of the options mentioned in [get the user ID](/microsoftteams/platform/bots/how-to/conversations/send-proactive-messages?tabs=dotnet#get-the-user-id-team-id-or-channel-id).</span></span>

#### <a name="sample-adaptive-card-with-a-mention"></a><span data-ttu-id="e1e3c-172">Пример адаптивной карты с упоминанием</span><span class="sxs-lookup"><span data-stu-id="e1e3c-172">Sample Adaptive card with a mention</span></span>

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

### <a name="information-masking-in-adaptive-cards"></a><span data-ttu-id="e1e3c-173">Информационная маскировка в адаптивных картах</span><span class="sxs-lookup"><span data-stu-id="e1e3c-173">Information masking in Adaptive cards</span></span>
<span data-ttu-id="e1e3c-174">Используйте свойство маскировки информации для маскировки определенной информации, такой как пароль или конфиденциальная информация от пользователей в элементе ввода [`Input.Text`](https://adaptivecards.io/explorer/Input.Text.html) адаптивной карты.</span><span class="sxs-lookup"><span data-stu-id="e1e3c-174">Use the information masking property to mask specific information, such as password or sensitive information from users within the Adaptive card [`Input.Text`](https://adaptivecards.io/explorer/Input.Text.html) input element.</span></span> 

> [!NOTE]
> <span data-ttu-id="e1e3c-175">Функция поддерживает только клиента стороне информации маскировки, в масках входной текст отправляется в качестве четкого текста на https конечной точки адрес, который был указан во время [конфигурации бота](../../build-your-first-app/build-bot.md).</span><span class="sxs-lookup"><span data-stu-id="e1e3c-175">The feature only supports client side information masking, the masked input text is sent as clear text to the https endpoint address that was specified during [bot configuration](../../build-your-first-app/build-bot.md).</span></span> 

> [!NOTE]
> <span data-ttu-id="e1e3c-176">Свойство маскировки информации в настоящее время доступно только в предварительном просмотре разработчика.</span><span class="sxs-lookup"><span data-stu-id="e1e3c-176">The information masking property is currently available in the developer preview only.</span></span>

<span data-ttu-id="e1e3c-177">Чтобы замаскировать информацию в адаптивных картах, `isMasked` добавьте свойство **к типу** `Input.Text` и установите его значение на *истинное.*</span><span class="sxs-lookup"><span data-stu-id="e1e3c-177">To mask information in Adaptive cards, add the `isMasked` property to **type** `Input.Text`, and set its value to *true*.</span></span>

#### <a name="sample-adaptive-card-with-masking-property"></a><span data-ttu-id="e1e3c-178">Пример адаптивной карты с свойством маскировки</span><span class="sxs-lookup"><span data-stu-id="e1e3c-178">Sample Adaptive card with masking property</span></span>

```json
{
    "type": "Input.Text",
    "id": "secretThing",
    "style": "password",
    "isMasked": true
  },
```

<span data-ttu-id="e1e3c-179">Следующее изображение является примером маскировки информации в адаптивных картах:</span><span class="sxs-lookup"><span data-stu-id="e1e3c-179">The following image is an example of masking information in Adaptive cards:</span></span>

![Маскировка информационного изображения](../../assets/images/cards/masking-information-view.png)

### <a name="full-width-adaptive-card"></a><span data-ttu-id="e1e3c-181">Адаптивная карта полной ширины</span><span class="sxs-lookup"><span data-stu-id="e1e3c-181">Full width Adaptive card</span></span>
<span data-ttu-id="e1e3c-182">Вы можете использовать `msteams` свойство, чтобы расширить ширину адаптивной карты и использовать дополнительное пространство холста.</span><span class="sxs-lookup"><span data-stu-id="e1e3c-182">You can use the `msteams` property to expand the width of an Adaptive card and make use of additional canvas space.</span></span> <span data-ttu-id="e1e3c-183">Для получения информации о том, как использовать свойство, смотрите следующий пример:</span><span class="sxs-lookup"><span data-stu-id="e1e3c-183">For information on how to use the property, see the following example:</span></span>

#### <a name="constructing-full-width-cards"></a><span data-ttu-id="e1e3c-184">Построение карт полной ширины</span><span class="sxs-lookup"><span data-stu-id="e1e3c-184">Constructing full width cards</span></span>
<span data-ttu-id="e1e3c-185">Чтобы сделать полную ширину Адаптивной карты `width` объект `msteams` в свойстве в содержимом карты должны быть установлены `Full` на .</span><span class="sxs-lookup"><span data-stu-id="e1e3c-185">To make a full width Adaptive card the `width` object in `msteams` property in the card content must be set to `Full`.</span></span>
<span data-ttu-id="e1e3c-186">Кроме того, приложение должно включать следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="e1e3c-186">In addition, your app must include the following elements:</span></span>

#### <a name="sample-adaptive-card-with-full-width"></a><span data-ttu-id="e1e3c-187">Пример адаптивной карты с полной шириной</span><span class="sxs-lookup"><span data-stu-id="e1e3c-187">Sample adaptive card with full width</span></span>

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

<span data-ttu-id="e1e3c-188">Полная ширина Адаптивная карта появляется следующим образом: ![ Полная ширина Адаптивная карта зрения](../../assets/images/cards/full-width-adaptive-card.png)</span><span class="sxs-lookup"><span data-stu-id="e1e3c-188">A full width Adaptive Card appears as follows: ![Full width Adaptive Card view](../../assets/images/cards/full-width-adaptive-card.png)</span></span>

<span data-ttu-id="e1e3c-189">Если вы еще не установили `width` свойство для *полного*, то по умолчанию вид адаптивной карты заключается в следующем: Малая ![ ширина Адаптивная карта зрения](../../assets/images/cards/small-width-adaptive-card.png)</span><span class="sxs-lookup"><span data-stu-id="e1e3c-189">If you have not set the `width` property to *Full*, then the default view of the Adaptive Card is as follows: ![Small width Adaptive Card view](../../assets/images/cards/small-width-adaptive-card.png)</span></span>

### <a name="typeahead-support"></a><span data-ttu-id="e1e3c-190">Поддержка Typeahead</span><span class="sxs-lookup"><span data-stu-id="e1e3c-190">Typeahead support</span></span>

<span data-ttu-id="e1e3c-191">В [`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) элементе схемы запрос пользователей на фильтрацию и выбор через значительное количество вариантов может значительно замедлить завершение задачи.</span><span class="sxs-lookup"><span data-stu-id="e1e3c-191">Within the [`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) schema element, asking users to filter through and select through a sizable number of choices can significantly slow down task completion.</span></span> <span data-ttu-id="e1e3c-192">Поддержка Typeahead в адаптивных картах может упростить выбор ввода путем сужения или фильтрации набора входных вариантов при вводе ввода пользователем.</span><span class="sxs-lookup"><span data-stu-id="e1e3c-192">Typeahead support within Adaptive cards can simplify input selection by narrowing or filtering the set of input choices as a user is typing the input.</span></span> 

#### <a name="enable-typeahead-in-adaptive-cards"></a><span data-ttu-id="e1e3c-193">Включить typeahead в адаптивных картах</span><span class="sxs-lookup"><span data-stu-id="e1e3c-193">Enable typeahead in Adaptive cards</span></span>

<span data-ttu-id="e1e3c-194">Для включения typeahead в `Input.Choiceset` набор и обеспечить установлен на `style` `filtered` `isMultiSelect` `false` .</span><span class="sxs-lookup"><span data-stu-id="e1e3c-194">To enable typeahead within the `Input.Choiceset` set `style` to `filtered` and ensure `isMultiSelect` is set to `false`.</span></span> 

#### <a name="sample-adaptive-card-with-typeahead-support"></a><span data-ttu-id="e1e3c-195">Пример адаптивной карты с поддержкой typeahead</span><span class="sxs-lookup"><span data-stu-id="e1e3c-195">Sample adaptive card with typeahead support</span></span>

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

### <a name="stage-view-for-images-in-adaptive-cards"></a><span data-ttu-id="e1e3c-196">Вид сцены для изображений в адаптивных картах</span><span class="sxs-lookup"><span data-stu-id="e1e3c-196">Stage view for images in Adaptive Cards</span></span>

> [!NOTE]
> <span data-ttu-id="e1e3c-197">Эта функция в настоящее время доступна только в предварительном просмотре разработчика.</span><span class="sxs-lookup"><span data-stu-id="e1e3c-197">This feature is currently available in developer preview only.</span></span>
 
<span data-ttu-id="e1e3c-198">В адаптивной карте можно использовать `msteams` свойство, чтобы добавить возможность отображения изображений в виде сцены выборочно.</span><span class="sxs-lookup"><span data-stu-id="e1e3c-198">In an Adaptive card, you can use the `msteams` property to add the ability to display images in stage view selectively.</span></span> <span data-ttu-id="e1e3c-199">Когда пользователи парят над изображениями, они видят значок расширения, для `allowExpand` которого атрибут установлен `true` на .</span><span class="sxs-lookup"><span data-stu-id="e1e3c-199">When users hover over the images, they would see an expand icon, for which the `allowExpand` attribute is set to `true`.</span></span> <span data-ttu-id="e1e3c-200">Для получения информации о том, как использовать свойство, смотрите следующий пример:</span><span class="sxs-lookup"><span data-stu-id="e1e3c-200">For information on how to use the property, see the following example:</span></span>

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

<span data-ttu-id="e1e3c-201">Когда пользователи парят над изображением, в правом верхнем углу изображения появляется значок расширения: Адаптивная ![ карта с расширяемым изображением](../../assets/images/cards/adaptivecard-hover-expand-icon.png)</span><span class="sxs-lookup"><span data-stu-id="e1e3c-201">When users hover over the image, an expand icon appears at top right corner of the image: ![Adaptive card with expandable image](../../assets/images/cards/adaptivecard-hover-expand-icon.png)</span></span>

<span data-ttu-id="e1e3c-202">Изображение отображается в представлении сцены, когда пользователь выбирает кнопку расширения: ![ Изображение расширено до представления сцены](../../assets/images/cards/adaptivecard-expand-image.png)</span><span class="sxs-lookup"><span data-stu-id="e1e3c-202">The image appears in stage view when the user selects the expand button: ![Image expanded to stage view](../../assets/images/cards/adaptivecard-expand-image.png)</span></span>

<span data-ttu-id="e1e3c-203">В представлении сцены пользователи могут увеличить и увеличить изображение.</span><span class="sxs-lookup"><span data-stu-id="e1e3c-203">In the stage view, users can zoom in and zoom out of the image.</span></span> <span data-ttu-id="e1e3c-204">Вы можете выбрать, какие изображения в вашей адаптивной карте должны иметь эту возможность.</span><span class="sxs-lookup"><span data-stu-id="e1e3c-204">You can select which images in your Adaptive card needs to have this capability.</span></span>

> [!NOTE]
> <span data-ttu-id="e1e3c-205">Возможность увеличения и масштабирования применяется только к элементам изображения (тип изображения) в адаптивной карте.</span><span class="sxs-lookup"><span data-stu-id="e1e3c-205">Zoom in and zoom out capability applies only to the image elements (Image type) in an Adaptive card.</span></span>

> [!NOTE]
> <span data-ttu-id="e1e3c-206">Для Teams мобильных приложений функция просмотра сцены для изображений в адаптивных картах доступна по умолчанию, и пользователи смогут просматривать изображения адаптивных карт в режиме стадии просмотра, просто нажав на изображение, `allowExpand` независимо от того, присутствует атрибут или нет.</span><span class="sxs-lookup"><span data-stu-id="e1e3c-206">For Teams mobile apps, stage view functionality for images in Adaptive Cards are available by default and users will be able to view Adaptive card images in stage view by simply tapping on the image, irrespective of whether the `allowExpand` attribute is present or not.</span></span>

# <a name="markdown-formatting-o365-connector-cards"></a>[<span data-ttu-id="e1e3c-207">**Форматирование разметки: O365 Коннекторные карты**</span><span class="sxs-lookup"><span data-stu-id="e1e3c-207">**Markdown formatting: O365 Connector Cards**</span></span>](#tab/connector-md)

<span data-ttu-id="e1e3c-208">Коннекторные карты поддерживают ограниченное форматирование Markdown и HTML.</span><span class="sxs-lookup"><span data-stu-id="e1e3c-208">Connector cards support limited Markdown and HTML formatting.</span></span> <span data-ttu-id="e1e3c-209">Поддержка HTML описана в последнем разделе.</span><span class="sxs-lookup"><span data-stu-id="e1e3c-209">HTML support is described in the last section.</span></span>

| <span data-ttu-id="e1e3c-210">Style</span><span class="sxs-lookup"><span data-stu-id="e1e3c-210">Style</span></span> | <span data-ttu-id="e1e3c-211">Пример</span><span class="sxs-lookup"><span data-stu-id="e1e3c-211">Example</span></span> | <span data-ttu-id="e1e3c-212">Markdown</span><span class="sxs-lookup"><span data-stu-id="e1e3c-212">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e1e3c-213">bold</span><span class="sxs-lookup"><span data-stu-id="e1e3c-213">bold</span></span> | <span data-ttu-id="e1e3c-214">**text**</span><span class="sxs-lookup"><span data-stu-id="e1e3c-214">**text**</span></span> | `**text**` |
| <span data-ttu-id="e1e3c-215">italic</span><span class="sxs-lookup"><span data-stu-id="e1e3c-215">italic</span></span> | <span data-ttu-id="e1e3c-216">*text*</span><span class="sxs-lookup"><span data-stu-id="e1e3c-216">*text*</span></span> | `*text*` |
| <span data-ttu-id="e1e3c-217">заголовок (уровни 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="e1e3c-217">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="e1e3c-218">**Text**</span><span class="sxs-lookup"><span data-stu-id="e1e3c-218">**Text**</span></span> | `### Text`|
| <span data-ttu-id="e1e3c-219">ударная попере</span><span class="sxs-lookup"><span data-stu-id="e1e3c-219">strikethrough</span></span> | <span data-ttu-id="e1e3c-220">~~text~~</span><span class="sxs-lookup"><span data-stu-id="e1e3c-220">~~text~~</span></span> | `~~text~~` |
| <span data-ttu-id="e1e3c-221">неупорядочеченный список</span><span class="sxs-lookup"><span data-stu-id="e1e3c-221">unordered list</span></span> | <ul><li><span data-ttu-id="e1e3c-222">текст</span><span class="sxs-lookup"><span data-stu-id="e1e3c-222">text</span></span></li><li><span data-ttu-id="e1e3c-223">текст</span><span class="sxs-lookup"><span data-stu-id="e1e3c-223">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="e1e3c-224">упорядоченный список</span><span class="sxs-lookup"><span data-stu-id="e1e3c-224">ordered list</span></span> | <ol><li><span data-ttu-id="e1e3c-225">текст</span><span class="sxs-lookup"><span data-stu-id="e1e3c-225">text</span></span></li><li><span data-ttu-id="e1e3c-226">текст</span><span class="sxs-lookup"><span data-stu-id="e1e3c-226">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="e1e3c-227">преформатированный текст</span><span class="sxs-lookup"><span data-stu-id="e1e3c-227">preformatted text</span></span> | `text` | ``preformatted text`` |
| <span data-ttu-id="e1e3c-228">blockquote</span><span class="sxs-lookup"><span data-stu-id="e1e3c-228">blockquote</span></span> | <span data-ttu-id="e1e3c-229">>блок-квота</span><span class="sxs-lookup"><span data-stu-id="e1e3c-229">>blockquote text</span></span> | `>blockquote text` |
| <span data-ttu-id="e1e3c-230">гиперссылка</span><span class="sxs-lookup"><span data-stu-id="e1e3c-230">hyperlink</span></span> | [<span data-ttu-id="e1e3c-231">Bing</span><span class="sxs-lookup"><span data-stu-id="e1e3c-231">Bing</span></span>](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| <span data-ttu-id="e1e3c-232">ссылка на изображение</span><span class="sxs-lookup"><span data-stu-id="e1e3c-232">image link</span></span> |![Утка на скале](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

<span data-ttu-id="e1e3c-234">В разъемных картах, новые линии отображаются `\n\n` для, но не для `\n` или `\r` .</span><span class="sxs-lookup"><span data-stu-id="e1e3c-234">In connector cards, newlines are rendered for `\n\n`, but not for `\n` or `\r`.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-markdown"></a><span data-ttu-id="e1e3c-235">Мобильные и настольные различия для разъемных карт с помощью Markdown</span><span class="sxs-lookup"><span data-stu-id="e1e3c-235">Mobile and desktop differences for connector cards using Markdown</span></span>

<span data-ttu-id="e1e3c-236">На рабочем столе форматирование Markdown для разъемных карт выглядит так:</span><span class="sxs-lookup"><span data-stu-id="e1e3c-236">On the desktop, Markdown formatting for connector cards looks like this:</span></span>

![Форматирование разметки для разъемных карт в клиенте Desktop](../../assets/images/cards/connector-desktop-markdown-combined.png)

<span data-ttu-id="e1e3c-238">На iOS форматирование Markdown для разъемных карт выглядит так:</span><span class="sxs-lookup"><span data-stu-id="e1e3c-238">On iOS, Markdown formatting for connector cards looks like this:</span></span>

![Форматирование разметки для разъемных карт в клиенте iOS](../../assets/images/cards/connector-iphone-markdown-combined-80.png)

<span data-ttu-id="e1e3c-240">Вопросы:</span><span class="sxs-lookup"><span data-stu-id="e1e3c-240">Issues:</span></span>

* <span data-ttu-id="e1e3c-241">Клиент iOS для Teams не отображает Markdown или HTML-изображения в Connector Cards.</span><span class="sxs-lookup"><span data-stu-id="e1e3c-241">The iOS client for Teams does not render Markdown or HTML inline images in Connector Cards.</span></span>
* <span data-ttu-id="e1e3c-242">Блокциты отображаются как отступные, но без серого фона.</span><span class="sxs-lookup"><span data-stu-id="e1e3c-242">Blockquotes are rendered as indented but without a gray background.</span></span>

<span data-ttu-id="e1e3c-243">На Android форматирование Markdown для разъемных карт выглядит так:</span><span class="sxs-lookup"><span data-stu-id="e1e3c-243">On Android, Markdown formatting for connector cards looks like this:</span></span>

![Форматирование разметки для разъемных карт в клиенте Android](../../assets/images/cards/connector-android-markdown-combined.png)

### <a name="formatting-example-for-markdown-connector-cards"></a><span data-ttu-id="e1e3c-245">Пример форматирования для карт разъема Markdown</span><span class="sxs-lookup"><span data-stu-id="e1e3c-245">Formatting example for Markdown Connector Cards</span></span>

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

## <a name="formatting-cards-with-html"></a><span data-ttu-id="e1e3c-246">Форматирование карт с HTML</span><span class="sxs-lookup"><span data-stu-id="e1e3c-246">Formatting cards with HTML</span></span>

# <a name="html-formatting-o365-connector-cards"></a>[<span data-ttu-id="e1e3c-247">**HTML форматирование: O365 Коннекторные карты**</span><span class="sxs-lookup"><span data-stu-id="e1e3c-247">**HTML formatting: O365 Connector Cards**</span></span>](#tab/connector-html)

<span data-ttu-id="e1e3c-248">Коннекторные карты поддерживают ограниченное форматирование Markdown и HTML.</span><span class="sxs-lookup"><span data-stu-id="e1e3c-248">Connector cards support limited Markdown and HTML formatting.</span></span> <span data-ttu-id="e1e3c-249">Разметка описана в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="e1e3c-249">Markdown is described in the next section.</span></span>

| <span data-ttu-id="e1e3c-250">Style</span><span class="sxs-lookup"><span data-stu-id="e1e3c-250">Style</span></span> | <span data-ttu-id="e1e3c-251">Пример</span><span class="sxs-lookup"><span data-stu-id="e1e3c-251">Example</span></span> | <span data-ttu-id="e1e3c-252">HTML</span><span class="sxs-lookup"><span data-stu-id="e1e3c-252">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e1e3c-253">bold</span><span class="sxs-lookup"><span data-stu-id="e1e3c-253">bold</span></span> | <span data-ttu-id="e1e3c-254">**text**</span><span class="sxs-lookup"><span data-stu-id="e1e3c-254">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="e1e3c-255">italic</span><span class="sxs-lookup"><span data-stu-id="e1e3c-255">italic</span></span> | <span data-ttu-id="e1e3c-256">*text*</span><span class="sxs-lookup"><span data-stu-id="e1e3c-256">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="e1e3c-257">заголовок (уровни 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="e1e3c-257">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="e1e3c-258">**Text**</span><span class="sxs-lookup"><span data-stu-id="e1e3c-258">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="e1e3c-259">ударная попере</span><span class="sxs-lookup"><span data-stu-id="e1e3c-259">strikethrough</span></span> | <span data-ttu-id="e1e3c-260">~~text~~</span><span class="sxs-lookup"><span data-stu-id="e1e3c-260">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="e1e3c-261">неупорядочеченный список</span><span class="sxs-lookup"><span data-stu-id="e1e3c-261">unordered list</span></span> | <ul><li><span data-ttu-id="e1e3c-262">текст</span><span class="sxs-lookup"><span data-stu-id="e1e3c-262">text</span></span></li><li><span data-ttu-id="e1e3c-263">текст</span><span class="sxs-lookup"><span data-stu-id="e1e3c-263">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="e1e3c-264">упорядоченный список</span><span class="sxs-lookup"><span data-stu-id="e1e3c-264">ordered list</span></span> | <ol><li><span data-ttu-id="e1e3c-265">текст</span><span class="sxs-lookup"><span data-stu-id="e1e3c-265">text</span></span></li><li><span data-ttu-id="e1e3c-266">текст</span><span class="sxs-lookup"><span data-stu-id="e1e3c-266">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="e1e3c-267">преформатированный текст</span><span class="sxs-lookup"><span data-stu-id="e1e3c-267">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="e1e3c-268">blockquote</span><span class="sxs-lookup"><span data-stu-id="e1e3c-268">blockquote</span></span> | <blockquote><span data-ttu-id="e1e3c-269">текст</span><span class="sxs-lookup"><span data-stu-id="e1e3c-269">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="e1e3c-270">гиперссылка</span><span class="sxs-lookup"><span data-stu-id="e1e3c-270">hyperlink</span></span> | [<span data-ttu-id="e1e3c-271">Bing</span><span class="sxs-lookup"><span data-stu-id="e1e3c-271">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="e1e3c-272">ссылка на изображение</span><span class="sxs-lookup"><span data-stu-id="e1e3c-272">image link</span></span> | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

<span data-ttu-id="e1e3c-273">В разъемных картах новые линии отображаются в HTML с помощью `<p>` тега.</span><span class="sxs-lookup"><span data-stu-id="e1e3c-273">In connector cards, newlines are rendered in HTML using the `<p>` tag.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-html"></a><span data-ttu-id="e1e3c-274">Мобильные и настольные различия для разъемных карт с использованием HTML</span><span class="sxs-lookup"><span data-stu-id="e1e3c-274">Mobile and desktop differences for connector cards using HTML</span></span>

<span data-ttu-id="e1e3c-275">На рабочем столе HTML-форматирование для разъемных карт выглядит так:</span><span class="sxs-lookup"><span data-stu-id="e1e3c-275">On the desktop, HTML formatting for connector cards looks like this:</span></span>

![HTML форматирование для разъемных карт в клиенте Desktop](../../assets/images/cards/Connector-desktop-html-combined.png)

<span data-ttu-id="e1e3c-277">На iOS форматирование HTML выглядит так:</span><span class="sxs-lookup"><span data-stu-id="e1e3c-277">On iOS, HTML formatting looks like this:</span></span>

![HTML форматирование для разъемных карт в клиенте iOS](../../assets/images/cards/connector-iphone-html-combined-80.png)

<span data-ttu-id="e1e3c-279">Вопросы:</span><span class="sxs-lookup"><span data-stu-id="e1e3c-279">Issues:</span></span>

* <span data-ttu-id="e1e3c-280">Вколчные изображения не отображаются на iOS с помощью Markdown или HTML в Connector Cards.</span><span class="sxs-lookup"><span data-stu-id="e1e3c-280">Inline images are not rendered on iOS using either Markdown or HTML in Connector Cards.</span></span>
* <span data-ttu-id="e1e3c-281">Предварительно отобрабатированный текст отображается, но не имеет серого фона.</span><span class="sxs-lookup"><span data-stu-id="e1e3c-281">Preformatted text is rendered but does not have a gray background.</span></span>

<span data-ttu-id="e1e3c-282">На Android форматирование HTML выглядит так:</span><span class="sxs-lookup"><span data-stu-id="e1e3c-282">On Android, HTML formatting looks like this:</span></span>

![HTML форматирование для разъемных карт в клиенте Android](../../assets/images/cards/connector-android-html-combined.png)

### <a name="formatting-sample-for-html-connector-cards"></a><span data-ttu-id="e1e3c-284">Образец форматирования для HTML-разъемных карт</span><span class="sxs-lookup"><span data-stu-id="e1e3c-284">Formatting sample for HTML Connector Cards</span></span>

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

# <a name="html-formatting-hero-and-thumbnail-cards"></a>[<span data-ttu-id="e1e3c-285">**HTML Форматирование: карты героя и эскиза**</span><span class="sxs-lookup"><span data-stu-id="e1e3c-285">**HTML Formatting: hero and thumbnail cards**</span></span>](#tab/simple-html)

<span data-ttu-id="e1e3c-286">HTML-теги поддерживаются для простых карт, таких как карта героя и эскиза.</span><span class="sxs-lookup"><span data-stu-id="e1e3c-286">HTML tags are supported for simple cards such as the hero and thumbnail card.</span></span> <span data-ttu-id="e1e3c-287">Разметка не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="e1e3c-287">Markdown is not supported.</span></span>

| <span data-ttu-id="e1e3c-288">Style</span><span class="sxs-lookup"><span data-stu-id="e1e3c-288">Style</span></span> | <span data-ttu-id="e1e3c-289">Пример</span><span class="sxs-lookup"><span data-stu-id="e1e3c-289">Example</span></span> | <span data-ttu-id="e1e3c-290">HTML</span><span class="sxs-lookup"><span data-stu-id="e1e3c-290">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e1e3c-291">bold</span><span class="sxs-lookup"><span data-stu-id="e1e3c-291">bold</span></span> | <span data-ttu-id="e1e3c-292">**text**</span><span class="sxs-lookup"><span data-stu-id="e1e3c-292">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="e1e3c-293">italic</span><span class="sxs-lookup"><span data-stu-id="e1e3c-293">italic</span></span> | <span data-ttu-id="e1e3c-294">*text*</span><span class="sxs-lookup"><span data-stu-id="e1e3c-294">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="e1e3c-295">заголовок (уровни 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="e1e3c-295">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="e1e3c-296">**Text**</span><span class="sxs-lookup"><span data-stu-id="e1e3c-296">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="e1e3c-297">ударная попере</span><span class="sxs-lookup"><span data-stu-id="e1e3c-297">strikethrough</span></span> | <span data-ttu-id="e1e3c-298">~~text~~</span><span class="sxs-lookup"><span data-stu-id="e1e3c-298">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="e1e3c-299">неупорядочеченный список</span><span class="sxs-lookup"><span data-stu-id="e1e3c-299">unordered list</span></span> | <ul><li><span data-ttu-id="e1e3c-300">текст</span><span class="sxs-lookup"><span data-stu-id="e1e3c-300">text</span></span></li><li><span data-ttu-id="e1e3c-301">текст</span><span class="sxs-lookup"><span data-stu-id="e1e3c-301">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="e1e3c-302">упорядоченный список</span><span class="sxs-lookup"><span data-stu-id="e1e3c-302">ordered list</span></span> | <ol><li><span data-ttu-id="e1e3c-303">текст</span><span class="sxs-lookup"><span data-stu-id="e1e3c-303">text</span></span></li><li><span data-ttu-id="e1e3c-304">текст</span><span class="sxs-lookup"><span data-stu-id="e1e3c-304">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="e1e3c-305">преформатированный текст</span><span class="sxs-lookup"><span data-stu-id="e1e3c-305">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="e1e3c-306">blockquote</span><span class="sxs-lookup"><span data-stu-id="e1e3c-306">blockquote</span></span> | <blockquote><span data-ttu-id="e1e3c-307">текст</span><span class="sxs-lookup"><span data-stu-id="e1e3c-307">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="e1e3c-308">гиперссылка</span><span class="sxs-lookup"><span data-stu-id="e1e3c-308">hyperlink</span></span> | [<span data-ttu-id="e1e3c-309">Bing</span><span class="sxs-lookup"><span data-stu-id="e1e3c-309">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="e1e3c-310">ссылка на изображение</span><span class="sxs-lookup"><span data-stu-id="e1e3c-310">image link</span></span> |<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a><span data-ttu-id="e1e3c-311">Мобильные и настольные различия для простых карт</span><span class="sxs-lookup"><span data-stu-id="e1e3c-311">Mobile and desktop differences for simple cards</span></span>

<span data-ttu-id="e1e3c-312">Из-за различий в разрешении между настольной и мобильной платформой форматирование отличается между настольной и мобильной версией Teams.</span><span class="sxs-lookup"><span data-stu-id="e1e3c-312">Because of resolution differences between the desktop and mobile platform, formatting is different between the desktop and the mobile version of Teams.</span></span>

<span data-ttu-id="e1e3c-313">На рабочем столе форматирование HTML выглядит так:</span><span class="sxs-lookup"><span data-stu-id="e1e3c-313">On the desktop, HTML formatting appears like this:</span></span>

![Форматирование HTML в клиенте Desktop](../../assets/images/cards/card-formatting-xml-desktop-v2.png)

<span data-ttu-id="e1e3c-315">На iOS форматирование HTML выглядит так:</span><span class="sxs-lookup"><span data-stu-id="e1e3c-315">On iOS, HTML formatting appears like this:</span></span>

![Форматирование HTML в клиенте iOS](../../assets/images/cards/card-formatting-xml-mobile-v2.png)

<span data-ttu-id="e1e3c-317">Вопросы:</span><span class="sxs-lookup"><span data-stu-id="e1e3c-317">Issues:</span></span>

* <span data-ttu-id="e1e3c-318">Форматирование символов, как смелые и жирные не отображаются на iOS.</span><span class="sxs-lookup"><span data-stu-id="e1e3c-318">Character formatting like bold and italic are not rendered on iOS.</span></span>

<span data-ttu-id="e1e3c-319">На Android форматирование HTML выглядит так:</span><span class="sxs-lookup"><span data-stu-id="e1e3c-319">On Android, HTML formatting appears like this:</span></span>

![HTML форматирование в клиенте Android](../../assets/images/cards/card-formatting-xml-android-60.png)

<span data-ttu-id="e1e3c-321">Форматирование символов, как смелый и italic дисплей правильно на Android.</span><span class="sxs-lookup"><span data-stu-id="e1e3c-321">Character formatting like bold and italic display correctly on Android.</span></span>

### <a name="formatting-sample-for-html-formatting-in-simple-cards"></a><span data-ttu-id="e1e3c-322">Пример форматирования html-форматирования в простых картах</span><span class="sxs-lookup"><span data-stu-id="e1e3c-322">Formatting sample for HTML formatting in simple cards</span></span>

<span data-ttu-id="e1e3c-323">Эти скриншоты были созданы Teams AppStudio, где текстовое свойство карты героя было настроено на следующую строку.</span><span class="sxs-lookup"><span data-stu-id="e1e3c-323">These screenshots were created using Teams AppStudio, where the text property of a hero card was set to the following string.</span></span> <span data-ttu-id="e1e3c-324">Вы можете протестировать форматирование в собственных картах, изменив этот код.</span><span class="sxs-lookup"><span data-stu-id="e1e3c-324">You can test formatting in your own cards by modifying this code.</span></span>

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"https://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`

---
