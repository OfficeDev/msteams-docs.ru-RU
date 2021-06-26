---
title: Создание и отправка сообщений
author: laujan
description: Сведения о том, как использовать Соединители Office 365 в Microsoft Teams.
ms.topic: how-to
localization_priority: Normal
keywords: соединитель teams o365
ms.openlocfilehash: e396d0048831634f683b6df925853464698fb96a
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140532"
---
# <a name="create-and-send-messages"></a><span data-ttu-id="d2c70-104">Создание и отправка сообщений</span><span class="sxs-lookup"><span data-stu-id="d2c70-104">Create and send messages</span></span>

<span data-ttu-id="d2c70-105">Вы можете создавать действия сообщения и отправлять их через входящие веб-ок или Office 365 соединителю.</span><span class="sxs-lookup"><span data-stu-id="d2c70-105">You can create actionable messages and send it through Incoming Webhook or Office 365 Connector.</span></span>

## <a name="create-actionable-messages"></a><span data-ttu-id="d2c70-106">Создание actionable messages</span><span class="sxs-lookup"><span data-stu-id="d2c70-106">Create actionable messages</span></span>

<span data-ttu-id="d2c70-107">Действия сообщений включают три видимые кнопки на карте.</span><span class="sxs-lookup"><span data-stu-id="d2c70-107">The actionable messages include three visible buttons on the card.</span></span> <span data-ttu-id="d2c70-108">Каждая кнопка определяется в свойстве сообщения с помощью действий, каждая из которых имеет тип ввода, текстовое поле, выбор даты или список нескольких `potentialAction` `ActionCard` вариантов.</span><span class="sxs-lookup"><span data-stu-id="d2c70-108">Each button is defined in the `potentialAction` property of the message by using `ActionCard` actions, each with an input type, a text field, a date picker, or a multi-choice list.</span></span> <span data-ttu-id="d2c70-109">Каждое `ActionCard` из них имеет связанное действие, например `HttpPOST` .</span><span class="sxs-lookup"><span data-stu-id="d2c70-109">Each `ActionCard` has an associated action, for example `HttpPOST`.</span></span>

<span data-ttu-id="d2c70-110">Карты соединители поддерживают следующие действия:</span><span class="sxs-lookup"><span data-stu-id="d2c70-110">The connector cards support the following actions:</span></span>

- <span data-ttu-id="d2c70-111">`ActionCard`: Представляет один или несколько типов ввода и связанных действий.</span><span class="sxs-lookup"><span data-stu-id="d2c70-111">`ActionCard`: Presents one or more input types and associated actions.</span></span>
- <span data-ttu-id="d2c70-112">`HttpPOST`: Отправляет запрос POST на URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="d2c70-112">`HttpPOST`: Sends POST request to a URL.</span></span>
- <span data-ttu-id="d2c70-113">`OpenUri`: Открывает URI в отдельном браузере или приложении, необязательно нацелены различные URL-адреса на основе операционных систем.</span><span class="sxs-lookup"><span data-stu-id="d2c70-113">`OpenUri`: Opens URI in a separate browser or app, optionally targets different URIs based on operating systems.</span></span>

<span data-ttu-id="d2c70-114">Действие `ActionCard` поддерживает три типа входных данных:</span><span class="sxs-lookup"><span data-stu-id="d2c70-114">The `ActionCard` action supports three input types:</span></span>

- <span data-ttu-id="d2c70-115">`TextInput`: Одно строковое или многолинейное текстовое поле с необязательным ограничением длины.</span><span class="sxs-lookup"><span data-stu-id="d2c70-115">`TextInput`: A single line or multiline text field with an optional length limit.</span></span>
- <span data-ttu-id="d2c70-116">`DateInput`: Селектор даты с необязательным селектором времени.</span><span class="sxs-lookup"><span data-stu-id="d2c70-116">`DateInput`: A date selector with an optional time selector.</span></span>
- <span data-ttu-id="d2c70-117">`MultichoiceInput`: Перечисляется список вариантов, предлагающих один выбор или несколько вариантов.</span><span class="sxs-lookup"><span data-stu-id="d2c70-117">`MultichoiceInput`: An enumerated list of choices offering either a single selection or multiple selections.</span></span>

<span data-ttu-id="d2c70-118">`MultichoiceInput` поддерживает свойство `style`, указывающее, отображается ли список изначально полностью развернутым.</span><span class="sxs-lookup"><span data-stu-id="d2c70-118">`MultichoiceInput` supports a `style` property that controls whether the list initially appears fully expanded.</span></span> <span data-ttu-id="d2c70-119">Значение по умолчанию `style` зависит от `isMultiSelect` значения:</span><span class="sxs-lookup"><span data-stu-id="d2c70-119">The default value of `style` depends on the value of `isMultiSelect` as follows:</span></span>

| `isMultiSelect` | <span data-ttu-id="d2c70-120">Значение `style` по умолчанию</span><span class="sxs-lookup"><span data-stu-id="d2c70-120">`style` default</span></span> |
| --- | --- |
| <span data-ttu-id="d2c70-121">`false` или не задано</span><span class="sxs-lookup"><span data-stu-id="d2c70-121">`false` or not specified</span></span> | `compact` |
| `true` | `expanded` |

<span data-ttu-id="d2c70-122">Чтобы отобразить список multiselect в компактном стиле, необходимо указать оба `"isMultiSelect": true` и `"style": true` .</span><span class="sxs-lookup"><span data-stu-id="d2c70-122">To display the multiselect list in the compact style, you must specify both `"isMultiSelect": true` and `"style": true`.</span></span>

<span data-ttu-id="d2c70-123">Дополнительные сведения о действиях карт соединители см. в см. в ["Действиях".](/outlook/actionable-messages/card-reference#actions)</span><span class="sxs-lookup"><span data-stu-id="d2c70-123">For more information on connector card actions, see [Actions](/outlook/actionable-messages/card-reference#actions).</span></span>

> [!NOTE]
> * <span data-ttu-id="d2c70-124">Значение `compact` для свойства `style` в Microsoft Teams равноценно значению `normal` для свойства `style` в Microsoft Outlook.</span><span class="sxs-lookup"><span data-stu-id="d2c70-124">Specifying `compact` for the `style` property in Microsoft Teams is the same as specifying `normal` for the `style` property in Microsoft Outlook.</span></span>
> * <span data-ttu-id="d2c70-125">Для действия HttpPOST маркер носителя включается в запросы.</span><span class="sxs-lookup"><span data-stu-id="d2c70-125">For the HttpPOST action, the bearer token is included with the requests.</span></span> <span data-ttu-id="d2c70-126">Маркер содержит удостоверение Azure AD пользователя Office 365, выполнившего действие.</span><span class="sxs-lookup"><span data-stu-id="d2c70-126">This token includes the Azure AD identity of the Office 365 user who took the action.</span></span>

## <a name="send-a-message-through-incoming-webhook-or-office-365-connector"></a><span data-ttu-id="d2c70-127">Отправка сообщения через входящий веб-ок или Office 365 соединителю</span><span class="sxs-lookup"><span data-stu-id="d2c70-127">Send a message through Incoming Webhook or Office 365 Connector</span></span>

<span data-ttu-id="d2c70-128">Чтобы отправить сообщение через входящий веб-Office 365 соединитель, отправьте полезное сообщение JSON в URL-адрес веб-страницы.</span><span class="sxs-lookup"><span data-stu-id="d2c70-128">To send a message through your Incoming Webhook or Office 365 Connector, post a JSON payload to the webhook URL.</span></span> <span data-ttu-id="d2c70-129">Эта нагрузка должна быть в виде Office 365 [соединители.](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)</span><span class="sxs-lookup"><span data-stu-id="d2c70-129">This payload must be in the form of an [Office 365 connector card](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).</span></span>

<span data-ttu-id="d2c70-130">Вы также можете использовать этот JSON для создания карт, содержащих богатые входные данные, такие как запись текста, многоцелевая или выбор даты и времени.</span><span class="sxs-lookup"><span data-stu-id="d2c70-130">You can also use this JSON to create cards containing rich inputs, such as text entry, multiselect, or selecting date and time.</span></span> <span data-ttu-id="d2c70-131">Код, который создает карточку и публикует ее на URL-адрес веб-страницы, может работать на любой хост-службе.</span><span class="sxs-lookup"><span data-stu-id="d2c70-131">The code that generates the card and posts it to the webhook URL can run on any hosted service.</span></span> <span data-ttu-id="d2c70-132">Эти карточки определяются как часть действий, а [](~/task-modules-and-cards/what-are-cards.md)также поддерживаются в картах, используемых в Teams ботах и расширениях обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="d2c70-132">These cards are defined as part of actionable messages and are also supported in [cards](~/task-modules-and-cards/what-are-cards.md), used in Teams bots and messaging extensions.</span></span>

### <a name="example-of-connector-message"></a><span data-ttu-id="d2c70-133">Пример сообщения соединитетеля</span><span class="sxs-lookup"><span data-stu-id="d2c70-133">Example of connector message</span></span>

<span data-ttu-id="d2c70-134">Пример сообщения соединители следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d2c70-134">An example of connector message is as follows:</span></span>

```json
{
    "@type": "MessageCard",
    "@context": "http://schema.org/extensions",
    "themeColor": "0076D7",
    "summary": "Larry Bryant created a new task",
    "sections": [{
        "activityTitle": "Larry Bryant created a new task",
        "activitySubtitle": "On Project Tango",
        "activityImage": "https://teamsnodesample.azurewebsites.net/static/img/image5.png",
        "facts": [{
            "name": "Assigned to",
            "value": "Unassigned"
        }, {
            "name": "Due date",
            "value": "Mon May 01 2017 17:07:18 GMT-0700 (Pacific Daylight Time)"
        }, {
            "name": "Status",
            "value": "Not started"
        }],
        "markdown": true
    }],
    "potentialAction": [{
        "@type": "ActionCard",
        "name": "Add a comment",
        "inputs": [{
            "@type": "TextInput",
            "id": "comment",
            "isMultiline": false,
            "title": "Add a comment here for this task"
        }],
        "actions": [{
            "@type": "HttpPOST",
            "name": "Add comment",
            "target": "https://docs.microsoft.com/outlook/actionable-messages"
        }]
    }, {
        "@type": "ActionCard",
        "name": "Set due date",
        "inputs": [{
            "@type": "DateInput",
            "id": "dueDate",
            "title": "Enter a due date for this task"
        }],
        "actions": [{
            "@type": "HttpPOST",
            "name": "Save",
            "target": "https://docs.microsoft.com/outlook/actionable-messages"
        }]
    }, {
        "@type": "OpenUri",
        "name": "Learn More",
        "targets": [{
            "os": "default",
            "uri": "https://docs.microsoft.com/outlook/actionable-messages"
        }]
    }, {
        "@type": "ActionCard",
        "name": "Change status",
        "inputs": [{
            "@type": "MultichoiceInput",
            "id": "list",
            "title": "Select a status",
            "isMultiSelect": "false",
            "choices": [{
                "display": "In Progress",
                "value": "1"
            }, {
                "display": "Active",
                "value": "2"
            }, {
                "display": "Closed",
                "value": "3"
            }]
        }],
        "actions": [{
            "@type": "HttpPOST",
            "name": "Save",
            "target": "https://docs.microsoft.com/outlook/actionable-messages"
        }]
    }]
}
```

<span data-ttu-id="d2c70-135">Это сообщение содержит следующую карточку в канале:</span><span class="sxs-lookup"><span data-stu-id="d2c70-135">This message provides the following card in the channel:</span></span>

![Снимок экрана карты соединители](~/assets/images/connectorcard.png)

## <a name="send-messages-using-curl-and-powershell"></a><span data-ttu-id="d2c70-137">Отправка сообщений с помощью cURL и PowerShell</span><span class="sxs-lookup"><span data-stu-id="d2c70-137">Send messages using cURL and PowerShell</span></span>

# <a name="curl"></a>[<span data-ttu-id="d2c70-138">cURL</span><span class="sxs-lookup"><span data-stu-id="d2c70-138">cURL</span></span>](#tab/cURL)

<span data-ttu-id="d2c70-139">**Публикация сообщения в веб-сайте cURL**</span><span class="sxs-lookup"><span data-stu-id="d2c70-139">**To post a message in the webhook with cURL**</span></span>

1. <span data-ttu-id="d2c70-140">Установка cURL с помощью: https://curl.haxx.se/ .</span><span class="sxs-lookup"><span data-stu-id="d2c70-140">Install cURL using: https://curl.haxx.se/.</span></span>

1. <span data-ttu-id="d2c70-141">Введите в командной строке следующую команду cURL:</span><span class="sxs-lookup"><span data-stu-id="d2c70-141">From the command line, enter the following cURL command:</span></span>

   ```bash
   // on macOS or Linux
   curl -H 'Content-Type: application/json' -d '{"text": "Hello World"}' <YOUR WEBHOOK URL>
   ```

   ```bash
   // on Windows
   curl.exe -H "Content-Type:application/json" -d "{'text':'Hello World'}" <YOUR WEBHOOK URL>
   ```

    > [!NOTE]
    > <span data-ttu-id="d2c70-142">Если post успешно, вы должны увидеть простой **выход 1** `curl` по .</span><span class="sxs-lookup"><span data-stu-id="d2c70-142">If the POST succeeds, you must see a simple **1** output by `curl`.</span></span>

1. <span data-ttu-id="d2c70-143">Проверьте Microsoft Teams клиента для новой карты.</span><span class="sxs-lookup"><span data-stu-id="d2c70-143">Check the Microsoft Teams client for the new card posted.</span></span>

# <a name="powershell"></a>[<span data-ttu-id="d2c70-144">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d2c70-144">PowerShell</span></span>](#tab/PowerShell)

 <span data-ttu-id="d2c70-145">Обязательное условие: установка PowerShell и ознакомление с его базовым использованием.</span><span class="sxs-lookup"><span data-stu-id="d2c70-145">Prerequisite: Installation of PowerShell and familiarization with its basic usage.</span></span>

<span data-ttu-id="d2c70-146">**Публикация сообщения на веб-сайте с помощью PowerShell**</span><span class="sxs-lookup"><span data-stu-id="d2c70-146">**To post a message to the webhook with PowerShell**</span></span>

1. <span data-ttu-id="d2c70-147">В командной строке PowerShell введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d2c70-147">From the PowerShell prompt, enter the following command:</span></span>

   ```powershell
   Invoke-RestMethod -Method post -ContentType 'Application/Json' -Body '{"text":"Hello World!"}' -Uri <YOUR WEBHOOK URL>
   ```

    > [!NOTE]
    > <span data-ttu-id="d2c70-148">Если post успешно, вы должны увидеть простой **выход 1** `Invoke-RestMethod` по .</span><span class="sxs-lookup"><span data-stu-id="d2c70-148">If the POST succeeds, you must see a simple **1** output by `Invoke-RestMethod`.</span></span>

1. <span data-ttu-id="d2c70-149">Проверьте канал Microsoft Teams, связанный с URL-адресом веб-перехватчика.</span><span class="sxs-lookup"><span data-stu-id="d2c70-149">Check the Microsoft Teams channel associated with the webhook URL.</span></span> <span data-ttu-id="d2c70-150">Вы можете увидеть новую карту, размещенную на канале.</span><span class="sxs-lookup"><span data-stu-id="d2c70-150">You can see the new card posted to the channel.</span></span> <span data-ttu-id="d2c70-151">Прежде чем использовать соединители для тестирования или публикации приложения, необходимо сделать следующее:</span><span class="sxs-lookup"><span data-stu-id="d2c70-151">Before you use the connector to test or publish your app, you must do the following:</span></span>

    - <span data-ttu-id="d2c70-152">[Включение двух значков](../../concepts/build-and-test/apps-package.md#app-icons).</span><span class="sxs-lookup"><span data-stu-id="d2c70-152">[Include two icons](../../concepts/build-and-test/apps-package.md#app-icons).</span></span>
    - <span data-ttu-id="d2c70-153">Измените `icons` часть манифеста на имена файлов значков вместо URL-адресов.</span><span class="sxs-lookup"><span data-stu-id="d2c70-153">Modify the `icons` portion of the manifest to the file names of the icons instead of URLs.</span></span>

---

## <a name="send-adaptive-cards-using-an-incoming-webhook"></a><span data-ttu-id="d2c70-154">Отправка адаптивных карт с помощью входящих веб-ок</span><span class="sxs-lookup"><span data-stu-id="d2c70-154">Send Adaptive Cards using an Incoming Webhook</span></span>

> [!NOTE]
> * <span data-ttu-id="d2c70-155">Все элементы схемы адаптивной карты, за `Action.Submit` исключением, полностью поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="d2c70-155">All native Adaptive Card schema elements, except `Action.Submit`, are fully supported.</span></span>
> * <span data-ttu-id="d2c70-156">Поддерживаемые [**действия: Action.OpenURL,**](https://adaptivecards.io/explorer/Action.OpenUrl.html) [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html)и [**Action.ToggleVisibility.**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html)</span><span class="sxs-lookup"><span data-stu-id="d2c70-156">The supported actions are [**Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html), [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html), and [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html).</span></span>

<span data-ttu-id="d2c70-157">**Отправка адаптивных карт через входящий веб-сайт**</span><span class="sxs-lookup"><span data-stu-id="d2c70-157">**To send Adaptive Cards through an Incoming Webhook**</span></span>

1. <span data-ttu-id="d2c70-158">[Настройка настраиваемой веб-страницы](/add-incoming-webhook.md) в Teams.</span><span class="sxs-lookup"><span data-stu-id="d2c70-158">[Setup a custom webhook](/add-incoming-webhook.md) in Teams.</span></span>
1. <span data-ttu-id="d2c70-159">Создание файла JSON адаптивной карты с помощью следующего кода:</span><span class="sxs-lookup"><span data-stu-id="d2c70-159">Create Adaptive Card JSON file using the following code:</span></span>

    ```json
    {
       "type":"message",
       "attachments":[
          {
             "contentType":"application/vnd.microsoft.card.adaptive",
             "contentUrl":null,
             "content":{
                "$schema":"http://adaptivecards.io/schemas/adaptive-card.json",
                "type":"AdaptiveCard",
                "version":"1.2",
                "body":[
                    {
                    "type": "TextBlock",
                    "text": "For Samples and Templates, see [https://adaptivecards.io/samples](https://adaptivecards.io/samples)"
                    }
                ]
             }
          }
       ]
    }
    ```

    <span data-ttu-id="d2c70-160">Свойства файла Adaptive Card JSON:</span><span class="sxs-lookup"><span data-stu-id="d2c70-160">The properties for Adaptive Card JSON file are as follows:</span></span>

    * <span data-ttu-id="d2c70-161">Поле `"type"` должно иметь значение `"message"`.</span><span class="sxs-lookup"><span data-stu-id="d2c70-161">The `"type"` field must be `"message"`.</span></span>
    * <span data-ttu-id="d2c70-162">Массив `"attachments"` содержит набор объектов card.</span><span class="sxs-lookup"><span data-stu-id="d2c70-162">The `"attachments"` array contains a set of card objects.</span></span>
    * <span data-ttu-id="d2c70-163">Поле `"contentType"` должно быть настроено на тип адаптивной карты.</span><span class="sxs-lookup"><span data-stu-id="d2c70-163">The `"contentType"` field must be set to Adaptive Card type.</span></span>
    * <span data-ttu-id="d2c70-164">Объект `"content"` — это карточка, отформатированная в JSON.</span><span class="sxs-lookup"><span data-stu-id="d2c70-164">The `"content"` object is the card formatted in JSON.</span></span>

1. <span data-ttu-id="d2c70-165">Проверьте адаптивную карту с помощью почтальонов:</span><span class="sxs-lookup"><span data-stu-id="d2c70-165">Test your Adaptive Card with Postman:</span></span>

    * <span data-ttu-id="d2c70-166">Проверьте адаптивную карту с помощью [postman](https://www.postman.com) для отправки запроса POST на URL-адрес, созданный для создания входящих веб-ок.</span><span class="sxs-lookup"><span data-stu-id="d2c70-166">Test the Adaptive Card using [Postman](https://www.postman.com) to send a POST request to the URL, created to set up Incoming Webhook.</span></span>
    * <span data-ttu-id="d2c70-167">Вклеить файл JSON в тело запроса и просмотреть сообщение адаптивной карты в Teams.</span><span class="sxs-lookup"><span data-stu-id="d2c70-167">Paste the JSON file in the body of the request and view the Adaptive Card message in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="d2c70-168">Используйте образцы и [шаблоны](https://adaptivecards.io/samples) кода адаптивной карты для проверки тела запроса POST.</span><span class="sxs-lookup"><span data-stu-id="d2c70-168">Use Adaptive Card [code samples and templates](https://adaptivecards.io/samples) to test the body of POST request.</span></span>

## <a name="rate-limiting-for-connectors"></a><span data-ttu-id="d2c70-169">Ограничение скорости для соединителей</span><span class="sxs-lookup"><span data-stu-id="d2c70-169">Rate limiting for connectors</span></span>

<span data-ttu-id="d2c70-170">Ограничения скорости приложений контролируют трафик, который может создавать соединителя или входящий веб-ок на канале.</span><span class="sxs-lookup"><span data-stu-id="d2c70-170">Application rate limits control the traffic that a connector or an Incoming Webhook is permitted to generate on a channel.</span></span> <span data-ttu-id="d2c70-171">Teams отслеживать запросы с помощью окна фиксированной скорости и инкрементного счетчика, измеряемой в секундах.</span><span class="sxs-lookup"><span data-stu-id="d2c70-171">Teams track requests using a fixed rate window and incremental counter measured in seconds.</span></span> <span data-ttu-id="d2c70-172">Если за секунду будет выполнено более четырех запросов, подключение клиента будет отлажено до тех пор, пока окно не обновит срок действия фиксированной скорости.</span><span class="sxs-lookup"><span data-stu-id="d2c70-172">If more than four requests are made in a second, the client connection is throttled until the window refreshes for the duration of the fixed rate.</span></span>

### <a name="transactions-per-second-thresholds"></a><span data-ttu-id="d2c70-173">Пороговые значения количества транзакций в секунду</span><span class="sxs-lookup"><span data-stu-id="d2c70-173">Transactions per second thresholds</span></span>

<span data-ttu-id="d2c70-174">В следующей таблице данная статья содержит сведения о транзакциях, основанных на времени:</span><span class="sxs-lookup"><span data-stu-id="d2c70-174">The following table provides the time based transaction details:</span></span>

| <span data-ttu-id="d2c70-175">Время в секундах</span><span class="sxs-lookup"><span data-stu-id="d2c70-175">Time in seconds</span></span>  | <span data-ttu-id="d2c70-176">Максимальное разрешенное количество запросов</span><span class="sxs-lookup"><span data-stu-id="d2c70-176">Maximum allowed requests</span></span>  |
|---|---|
| <span data-ttu-id="d2c70-177">1 </span><span class="sxs-lookup"><span data-stu-id="d2c70-177">1</span></span>   | <span data-ttu-id="d2c70-178">4 </span><span class="sxs-lookup"><span data-stu-id="d2c70-178">4</span></span>  |  
| <span data-ttu-id="d2c70-179">30</span><span class="sxs-lookup"><span data-stu-id="d2c70-179">30</span></span>   | <span data-ttu-id="d2c70-180">60</span><span class="sxs-lookup"><span data-stu-id="d2c70-180">60</span></span>  |  
| <span data-ttu-id="d2c70-181">3600</span><span class="sxs-lookup"><span data-stu-id="d2c70-181">3600</span></span>   | <span data-ttu-id="d2c70-182">100</span><span class="sxs-lookup"><span data-stu-id="d2c70-182">100</span></span>  |
| <span data-ttu-id="d2c70-183">7200</span><span class="sxs-lookup"><span data-stu-id="d2c70-183">7200</span></span> | <span data-ttu-id="d2c70-184">150</span><span class="sxs-lookup"><span data-stu-id="d2c70-184">150</span></span>  |
| <span data-ttu-id="d2c70-185">86400</span><span class="sxs-lookup"><span data-stu-id="d2c70-185">86400</span></span>  | <span data-ttu-id="d2c70-186">1800</span><span class="sxs-lookup"><span data-stu-id="d2c70-186">1800</span></span>  |

<span data-ttu-id="d2c70-187">Логика повторной работы с [экспоненциальным](/azure/architecture/patterns/retry) отсевом может уменьшить ограничение скорости для случаев, когда запросы превышают ограничения в течение секунды.</span><span class="sxs-lookup"><span data-stu-id="d2c70-187">A [retry logic with exponential back-off](/azure/architecture/patterns/retry) can mitigate rate limiting for cases where requests are exceeding the limits within a second.</span></span> <span data-ttu-id="d2c70-188">Следуйте [лучшим практикам,](../../bots/how-to/rate-limit.md) чтобы не ударить по ограничениям скорости.</span><span class="sxs-lookup"><span data-stu-id="d2c70-188">Follow [best practices](../../bots/how-to/rate-limit.md) to avoid hitting the rate limits.</span></span>

> [!NOTE]
> <span data-ttu-id="d2c70-189">Логика повторной работы с [экспоненциальным](/azure/architecture/patterns/retry) отсевом может уменьшить ограничение скорости для случаев, когда запросы превышают ограничения в течение секунды.</span><span class="sxs-lookup"><span data-stu-id="d2c70-189">A [retry logic with exponential back-off](/azure/architecture/patterns/retry) can mitigate rate limiting for cases where requests are exceeding the limits within a second.</span></span> <span data-ttu-id="d2c70-190">См. за [откликами HTTP 429](../../bots/how-to/rate-limit.md#handle-http-429-responses), чтобы не достигать ограничений по скорости.</span><span class="sxs-lookup"><span data-stu-id="d2c70-190">Refer [HTTP 429 responses](../../bots/how-to/rate-limit.md#handle-http-429-responses) to avoid hitting the rate limits.</span></span>

```csharp
// Please note that response body needs to be extracted and read 
// as Connectors do not throw 429s
try
{
    // Perform Connector POST operation     
    var httpResponseMessage = await _client.PostAsync(IncomingWebhookUrl, new StringContent(content));
    // Read response content
    var responseContent = await httpResponseMessage.Content.ReadAsStringAsync();
    if (responseContent.Contains("Microsoft Teams endpoint returned HTTP error 429")) 
    {
        // initiate retry logic
    }
}
```

<span data-ttu-id="d2c70-191">Эти ограничения имеются для уменьшения нежелательной почты канала соединитетелем и обеспечения оптимального опытом для пользователей.</span><span class="sxs-lookup"><span data-stu-id="d2c70-191">These limits are in place to reduce spamming a channel by a connector and ensures an optimal experience to users.</span></span>

## <a name="see-also"></a><span data-ttu-id="d2c70-192">См. также</span><span class="sxs-lookup"><span data-stu-id="d2c70-192">See also</span></span>

* [<span data-ttu-id="d2c70-193">Office 365 Соединители для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="d2c70-193">Office 365 Connectors for Microsoft Teams</span></span>](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [<span data-ttu-id="d2c70-194">Создание входящих веб-ок</span><span class="sxs-lookup"><span data-stu-id="d2c70-194">Create an Incoming Webhook</span></span>](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [<span data-ttu-id="d2c70-195">Создание исходятого веб-окка</span><span class="sxs-lookup"><span data-stu-id="d2c70-195">Create an Outgoing Webhook</span></span>](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)
