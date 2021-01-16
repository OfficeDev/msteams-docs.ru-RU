---
title: Отправка сообщений соединителям и веб-перехватчикам
description: Сведения о том, как использовать Соединители Office 365 в Microsoft Teams.
localization_priority: Priority
keywords: соединитель teams o365
ms.openlocfilehash: 55cfbc870ed8b04a8fbac58fdfa9b40110410ad7
ms.sourcegitcommit: 5e1300d6f4f2ea23beb3cdbbf4bd46999eef4e87
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/15/2021
ms.locfileid: "49875016"
---
# <a name="sending-messages-to-connectors-and-webhooks"></a><span data-ttu-id="beeb1-104">Отправка сообщений соединителям и веб-перехватчикам</span><span class="sxs-lookup"><span data-stu-id="beeb1-104">Sending messages to connectors and webhooks</span></span>

<span data-ttu-id="beeb1-105">Чтобы отправить сообщение через соединитель Office 365 или входящий веб-перехватчик, необходимо отправить полезные данные JSON на URL-адрес веб-перехватчика.</span><span class="sxs-lookup"><span data-stu-id="beeb1-105">To send a message through your Office 365 Connector or incoming webhook, you post a JSON payload to the webhook URL.</span></span> <span data-ttu-id="beeb1-106">Как правило, эти полезные данные будут отображаться в [форме карточки соединителя Office 365](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).</span><span class="sxs-lookup"><span data-stu-id="beeb1-106">Typically this payload will be in the form of an [Office 365 Connector Card](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).</span></span>

<span data-ttu-id="beeb1-107">С помощью этого кода JSON также можно создавать карточки с различными элементами для ввода данных, например текстовыми полями, переключателями множественного выбора или средствами выбора даты и времени.</span><span class="sxs-lookup"><span data-stu-id="beeb1-107">You can also use this JSON to create cards containing rich inputs, such as text entry, multi-select, or picking a date and time.</span></span> <span data-ttu-id="beeb1-108">Код, генерирующий карточку и отправляющий ее на URL-адрес веб-перехватчика, может выполняться в любой размещенной службе.</span><span class="sxs-lookup"><span data-stu-id="beeb1-108">The code that generates the card and posts to the webhook URL can be running on any hosted service.</span></span> <span data-ttu-id="beeb1-109">Эти карточки определяются в составе сообщений с действиями, а также поддерживаются в [карточках](~/task-modules-and-cards/what-are-cards.md), используемых ботами Teams и расширениями для обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="beeb1-109">These cards are defined as part of actionable messages, and are also supported in [cards](~/task-modules-and-cards/what-are-cards.md) used in Teams bots and Messaging extensions.</span></span>

### <a name="example-connector-message"></a><span data-ttu-id="beeb1-110">Пример сообщения соединителя</span><span class="sxs-lookup"><span data-stu-id="beeb1-110">Example connector message</span></span>

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

<span data-ttu-id="beeb1-111">Это сообщение создает на канале представленную ниже карточку.</span><span class="sxs-lookup"><span data-stu-id="beeb1-111">This message produces the following card in the channel.</span></span>

![Снимок экрана с карточкой соединителя](~/assets/images/connectors/connector_message.png)

## <a name="creating-actionable-messages"></a><span data-ttu-id="beeb1-113">Создание сообщений с действиями</span><span class="sxs-lookup"><span data-stu-id="beeb1-113">Creating actionable messages</span></span>

<span data-ttu-id="beeb1-114">В примере карточки из предыдущего раздела отображаются три кнопки.</span><span class="sxs-lookup"><span data-stu-id="beeb1-114">The example in the preceding section includes three visible buttons on the card.</span></span> <span data-ttu-id="beeb1-115">Каждая кнопка определена в свойстве `potentialAction` сообщения с помощью действий `ActionCard`, каждое из которых содержит тип элемента ввода: текстовое поле, элемент управления "Выбор даты" или список с возможностью выбора нескольких вариантов.</span><span class="sxs-lookup"><span data-stu-id="beeb1-115">Each button is defined in the `potentialAction` property of the message by using `ActionCard` actions, each containing an input type: a text field, a date picker, or a multi-choice list.</span></span> <span data-ttu-id="beeb1-116">С каждым действием `ActionCard` связано другое действие, например `HttpPOST`.</span><span class="sxs-lookup"><span data-stu-id="beeb1-116">Each `ActionCard` action has an associated action, for example `HttpPOST`.</span></span>

<span data-ttu-id="beeb1-117">Карточки соединителей поддерживают действия трех типов:</span><span class="sxs-lookup"><span data-stu-id="beeb1-117">Connector cards support three types of actions:</span></span>

- <span data-ttu-id="beeb1-118">`ActionCard`: представляет один или несколько типов входных данных и соответствующие действия;</span><span class="sxs-lookup"><span data-stu-id="beeb1-118">`ActionCard` Presents one or more input types and associated actions</span></span>
- <span data-ttu-id="beeb1-119">`HttpPOST`: отправляет запрос POST на URL-адрес;</span><span class="sxs-lookup"><span data-stu-id="beeb1-119">`HttpPOST` Sends a POST request to a URL</span></span>
- <span data-ttu-id="beeb1-120">`OpenUri`: открывает URI в отдельном браузере или приложении; при необходимости ссылается на разные URI в зависимости от операционной системы.</span><span class="sxs-lookup"><span data-stu-id="beeb1-120">`OpenUri` Opens a URI in a separate browser or app; optionally targets different URIs based on operating systems</span></span>

<span data-ttu-id="beeb1-121">Действие `ActionCard` поддерживает три типа входных данных:</span><span class="sxs-lookup"><span data-stu-id="beeb1-121">The `ActionCard` action supports three input types:</span></span>

- <span data-ttu-id="beeb1-122">`TextInput`: однострочное или многострочное текстовое поле с необязательным ограничением длины;</span><span class="sxs-lookup"><span data-stu-id="beeb1-122">`TextInput` A single-line or multiline text field with an optional length limit</span></span>
- <span data-ttu-id="beeb1-123">`DateInput`: средство выбора даты с необязательным выбором времени;</span><span class="sxs-lookup"><span data-stu-id="beeb1-123">`DateInput` A date selector with an optional time selector</span></span>
- <span data-ttu-id="beeb1-124">`MultichoiceInput`: нумерованный список вариантов с возможностью выбора одного или нескольких пунктов;</span><span class="sxs-lookup"><span data-stu-id="beeb1-124">`MultichoiceInput` A enumerated list of choices offering either a single selection or multiple selections</span></span>

<span data-ttu-id="beeb1-125">`MultichoiceInput` поддерживает свойство `style`, указывающее, отображается ли список изначально полностью развернутым.</span><span class="sxs-lookup"><span data-stu-id="beeb1-125">`MultichoiceInput` supports a `style` property that controls whether the list initially appears fully expanded.</span></span> <span data-ttu-id="beeb1-126">Значение `style` по умолчанию зависит от значения `isMultiSelect`.</span><span class="sxs-lookup"><span data-stu-id="beeb1-126">The default value of `style` depends on the value of `isMultiSelect`.</span></span>

| `isMultiSelect` | <span data-ttu-id="beeb1-127">Значение `style` по умолчанию</span><span class="sxs-lookup"><span data-stu-id="beeb1-127">`style` default</span></span> |
| --- | --- |
| <span data-ttu-id="beeb1-128">`false` или не задано</span><span class="sxs-lookup"><span data-stu-id="beeb1-128">`false` or not specified</span></span> | `compact` |
| `true` | `expanded` |

<span data-ttu-id="beeb1-129">Если вам нужно, чтобы список со множественным выбором изначально отображался в компактном стиле, необходимо задать значения `"isMultiSelect": true` и `"style": true`.</span><span class="sxs-lookup"><span data-stu-id="beeb1-129">If you want a multiselect list initially displayed in the compact style, you must specify both `"isMultiSelect": true` and `"style": true`.</span></span>

> [!NOTE]
> <span data-ttu-id="beeb1-130">Значение `compact` для свойства `style` в Microsoft Teams равноценно значению `normal` для свойства `style` в Microsoft Outlook.</span><span class="sxs-lookup"><span data-stu-id="beeb1-130">Specifying `compact` for the `style` property in Microsoft Teams is the same as specifying `normal` for the `style` property in Microsoft Outlook.</span></span>

<span data-ttu-id="beeb1-131">Все остальные сведения о действиях карточек соединителей представлены в разделе **[Действия](/outlook/actionable-messages/card-reference#actions)** справки по карточкам сообщений с действиями.</span><span class="sxs-lookup"><span data-stu-id="beeb1-131">For all other details about Connector card actions, see **[Actions](/outlook/actionable-messages/card-reference#actions)** in the actionable message card reference.</span></span>

## <a name="setting-up-a-custom-incoming-webhook"></a><span data-ttu-id="beeb1-132">Настройка пользовательского входящего веб-перехватчика</span><span class="sxs-lookup"><span data-stu-id="beeb1-132">Setting up a custom incoming webhook</span></span>

<span data-ttu-id="beeb1-133">Выполните указанные ниже действия, чтобы отправить простую карточку в соединитель.</span><span class="sxs-lookup"><span data-stu-id="beeb1-133">Follow these steps to see how to send a simple card to a Connector.</span></span>

1. <span data-ttu-id="beeb1-134">В Microsoft Teams нажмите **Дополнительные параметры** (**&#8943;**) рядом с названием канала и выберите **Соединители**.</span><span class="sxs-lookup"><span data-stu-id="beeb1-134">In Microsoft Teams, choose **More options** (**&#8943;**) next to the channel name and then choose **Connectors**.</span></span>
2. <span data-ttu-id="beeb1-135">Прокрутите список соединителей до пункта **Входящий веб-перехватчик** и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="beeb1-135">Scroll through the list of Connectors to **Incoming Webhook**, and choose **Add**.</span></span>
3. <span data-ttu-id="beeb1-136">Введите имя веб-перехватчика, отправьте изображение, которое следует связать с данными от веб-перехватчика, и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="beeb1-136">Enter a name for the webhook, upload an image to associate with data from the webhook, and choose **Create**.</span></span>
4. <span data-ttu-id="beeb1-137">Скопируйте веб-перехватчик в буфер обмена и сохраните его.</span><span class="sxs-lookup"><span data-stu-id="beeb1-137">Copy the webhook to the clipboard and save it.</span></span> <span data-ttu-id="beeb1-138">Для отправки информации в Microsoft Teams вам потребуется URL-адрес веб-перехватчика.</span><span class="sxs-lookup"><span data-stu-id="beeb1-138">You'll need the webhook URL for sending information to Microsoft Teams.</span></span>
5. <span data-ttu-id="beeb1-139">Нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="beeb1-139">Choose **Done**.</span></span>

### <a name="post-a-message-to-the-webhook-using-curl"></a><span data-ttu-id="beeb1-140">Отправка сообщения веб-перехватчику с помощью cURL</span><span class="sxs-lookup"><span data-stu-id="beeb1-140">Post a message to the webhook using cURL</span></span>

<span data-ttu-id="beeb1-141">Для выполнения описанных ниже действий используется [cURL](https://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="beeb1-141">The following steps use [cURL](https://curl.haxx.se/).</span></span> <span data-ttu-id="beeb1-142">Предполагается, что у вас уже установлена эта программа, а вы знакомы с основами ее использования.</span><span class="sxs-lookup"><span data-stu-id="beeb1-142">We assume that you have this installed and are familiar with its basic usage.</span></span>

1. <span data-ttu-id="beeb1-143">Введите в командной строке следующую команду cURL:</span><span class="sxs-lookup"><span data-stu-id="beeb1-143">From the command line, enter the following cURL command:</span></span>

   ```bash
   // on macOS or Linux
   curl -H 'Content-Type: application/json' -d '{"text": "Hello World"}' <YOUR WEBHOOK URL>
   ```

   ```bash
   // on Windows
   curl.exe -H "Content-Type:application/json" -d "{'text':'Hello World'}" <YOUR WEBHOOK URL>
   ```

2. <span data-ttu-id="beeb1-144">В случае успешного выполнения запроса POST команда `curl` должна возвращать простой отклик **1**.</span><span class="sxs-lookup"><span data-stu-id="beeb1-144">If the POST succeeds, you should see a simple **1** output by `curl`.</span></span>
3. <span data-ttu-id="beeb1-145">Проверьте клиент Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="beeb1-145">Check the Microsoft Team client.</span></span> <span data-ttu-id="beeb1-146">Вы увидите новую карточку, опубликованную в группе.</span><span class="sxs-lookup"><span data-stu-id="beeb1-146">You should see the new card posted to the team.</span></span>

### <a name="post-a-message-to-the-webhook-using-powershell"></a><span data-ttu-id="beeb1-147">Отправка сообщения веб-перехватчику с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="beeb1-147">Post a message to the webhook using PowerShell</span></span>

<span data-ttu-id="beeb1-148">Для выполнения описанных ниже действий используется PowerShell.</span><span class="sxs-lookup"><span data-stu-id="beeb1-148">The following steps use PowerShell.</span></span> <span data-ttu-id="beeb1-149">Предполагается, что у вас уже установлена эта программа, а вы знакомы с основами ее использования.</span><span class="sxs-lookup"><span data-stu-id="beeb1-149">We assume that you have this installed and are familiar with its basic usage.</span></span>

1. <span data-ttu-id="beeb1-150">В командной строке PowerShell введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="beeb1-150">From the PowerShell prompt, enter the following command:</span></span>

   ```powershell
   Invoke-RestMethod -Method post -ContentType 'Application/Json' -Body '{"text":"Hello World!"}' -Uri <YOUR WEBHOOK URL>
   ```

2. <span data-ttu-id="beeb1-151">В случае успешного выполнения запроса POST команда `Invoke-RestMethod` должна возвращать простой отклик **1**.</span><span class="sxs-lookup"><span data-stu-id="beeb1-151">If the POST succeeds, you should see a simple **1** output by `Invoke-RestMethod`.</span></span>
3. <span data-ttu-id="beeb1-152">Проверьте канал Microsoft Teams, связанный с URL-адресом веб-перехватчика.</span><span class="sxs-lookup"><span data-stu-id="beeb1-152">Check the Microsoft Teams channel associated with the webhook URL.</span></span> <span data-ttu-id="beeb1-153">На канале должна появиться новая карточка.</span><span class="sxs-lookup"><span data-stu-id="beeb1-153">You should see the new card posted to the channel.</span></span>

- <span data-ttu-id="beeb1-154">[Включение двух значков](../../concepts/build-and-test/apps-package.md#app-icons).</span><span class="sxs-lookup"><span data-stu-id="beeb1-154">[Include two icons](../../concepts/build-and-test/apps-package.md#app-icons).</span></span>
- <span data-ttu-id="beeb1-155">Измените раздел `icons` манифеста, чтобы он ссылался на имена файлов значков, а не на их URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="beeb1-155">Modify the `icons` portion of the manifest to refer to the file names of the icons instead of URLs.</span></span>

<span data-ttu-id="beeb1-156">Приведенный ниже файл manifest.json содержит основные элементы, необходимые для тестирования и отправки приложения.</span><span class="sxs-lookup"><span data-stu-id="beeb1-156">The following manifest.json file contains the basic elements needed to test and submit your app.</span></span>

> [!NOTE]
> <span data-ttu-id="beeb1-157">Замените `id` и `connectorId` в приведенном ниже примере на GUID соединителя.</span><span class="sxs-lookup"><span data-stu-id="beeb1-157">Replace `id` and `connectorId` in the following example with the GUID of your Connector.</span></span>

#### <a name="example-manifestjson-with-connector"></a><span data-ttu-id="beeb1-158">Пример manifest.json с соединителем</span><span class="sxs-lookup"><span data-stu-id="beeb1-158">Example manifest.json with connector</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "id": "e9343a03-0a5e-4c1f-95a8-263a565505a5",
  "version": "1.0",
  "packageName": "com.sampleapp",
  "developer": {
    "name": "Publisher",
    "websiteUrl": "https://www.microsoft.com",
    "privacyUrl": "https://www.microsoft.com",
    "termsOfUseUrl": "https://www.microsoft.com"
  },
  "description": {
    "full": "This is a small sample app we made for you! This app has samples of all capabilities Microsoft Teams supports.",
    "short": "This is a small sample app we made for you!"
  },
  "icons": {
    "outline": "sampleapp-outline.png",
    "color": "sampleapp-color.png"
  },
  "connectors": [
    {
      "connectorId": "e9343a03-0a5e-4c1f-95a8-263a565505a5",
      "scopes": [
        "team"
      ]
    }
  ],
  "name": {
    "short": "Sample App",
    "full": "Sample App"
  },
  "accentColor": "#FFFFFF",
  "needsIdentity": "true"
}
```

## <a name="send-adaptive-cards-using-an-incoming-webhook"></a><span data-ttu-id="beeb1-159">Отправка адаптивных карточек с помощью входящего веб-перехватчика</span><span class="sxs-lookup"><span data-stu-id="beeb1-159">Send adaptive cards using an incoming webhook</span></span>

> [!NOTE]
>
> <span data-ttu-id="beeb1-160">✔ Все встроенные элементы схемы адаптивной карточки, кроме `Action.Submit`, полностью поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="beeb1-160">✔ All native adaptive card schema elements, except `Action.Submit`, are fully supported.</span></span>
>
> <span data-ttu-id="beeb1-161">✔ Поддерживаемые действия: [**Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html), [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html) и [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html).</span><span class="sxs-lookup"><span data-stu-id="beeb1-161">✔ The supported Actions are [**Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html), [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html), and [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html).</span></span>

### <a name="the-flow-for-sending-adaptive-cards-via-an-incoming-webhook-is-as-follows"></a><span data-ttu-id="beeb1-162">Для отправки [адаптивных карточек](../../task-modules-and-cards/cards/cards-reference.md#adaptive-card) через входящий веб-перехватчик используется следующий поток:</span><span class="sxs-lookup"><span data-stu-id="beeb1-162">The flow for sending [adaptive cards](../../task-modules-and-cards/cards/cards-reference.md#adaptive-card) via an incoming webhook is as follows:</span></span>

<span data-ttu-id="beeb1-163">**1.** [Настройка пользовательского веб-перехватчика](#setting-up-a-custom-incoming-webhook) в Teams.</span><span class="sxs-lookup"><span data-stu-id="beeb1-163">**1.** [Setup a custom webhook](#setting-up-a-custom-incoming-webhook) in Teams.</span></span></br></br>
<span data-ttu-id="beeb1-164">**2.** Создание файла JSON адаптивной карточки:</span><span class="sxs-lookup"><span data-stu-id="beeb1-164">**2.** Create your adaptive card JSON file:</span></span>

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
                "text": "For Samples and Templates, see [https://adaptivecards.io/samples](https://adaptivecards.io/samples)",
                }
            ]
         }
      }
   ]
}
```

> [!div class="checklist"]
>
> - <span data-ttu-id="beeb1-165">Поле `"type"` должно иметь значение `"message"`.</span><span class="sxs-lookup"><span data-stu-id="beeb1-165">The `"type"` field must be `"message"`.</span></span>
> - <span data-ttu-id="beeb1-166">Массив `"attachments"` содержит набор объектов card.</span><span class="sxs-lookup"><span data-stu-id="beeb1-166">The `"attachments"` array contains a set of card objects.</span></span>
> - <span data-ttu-id="beeb1-167">В поле `"contentType"` следует задать тип "Адаптивная карточка".</span><span class="sxs-lookup"><span data-stu-id="beeb1-167">The `"contentType"` field must be set to adaptive card type.</span></span>
> - <span data-ttu-id="beeb1-168">Объект `"content"` — это карточка, отформатированная в JSON.</span><span class="sxs-lookup"><span data-stu-id="beeb1-168">The `"content"` object is the card formatted in JSON.</span></span>

<span data-ttu-id="beeb1-169">**3.** Тестирование адаптивной карточки с помощью Postman</span><span class="sxs-lookup"><span data-stu-id="beeb1-169">**3.** Test your adaptive card with Postman</span></span>

<span data-ttu-id="beeb1-170">Вы можете протестировать адаптивную карточку с помощью [Postman](https://www.postman.com), чтобы отправить запрос POST на URL-адрес, который вы создали при настройке входящего веб-перехватчика.</span><span class="sxs-lookup"><span data-stu-id="beeb1-170">You can test your adaptive card using [Postman](https://www.postman.com) to send a POST request to the URL that you created when you setup your incoming webhook.</span></span> <span data-ttu-id="beeb1-171">Вставьте файл JSON в текст запроса и просмотрите сообщение адаптивной карточки в Teams.</span><span class="sxs-lookup"><span data-stu-id="beeb1-171">Paste your JSON file in the body of the request and view your adaptive card message in Teams.</span></span>

>[!TIP]
> <span data-ttu-id="beeb1-172">В тексте запроса проверки POST можно использовать [образцы и шаблоны](https://adaptivecards.io/samples) кода адаптивной карточки.</span><span class="sxs-lookup"><span data-stu-id="beeb1-172">You can use adaptive card code [Samples and Templates](https://adaptivecards.io/samples) for the body of your test Post request.</span></span>

## <a name="testing-your-connector"></a><span data-ttu-id="beeb1-173">Тестирование соединителя</span><span class="sxs-lookup"><span data-stu-id="beeb1-173">Testing your connector</span></span>

<span data-ttu-id="beeb1-174">Чтобы тестировать соединитель, отправьте его команде, как в любом другом приложении.</span><span class="sxs-lookup"><span data-stu-id="beeb1-174">To test your Connector, upload it to a team as you would with any other app.</span></span> <span data-ttu-id="beeb1-175">Вы можете создать ZIP-пакет, используя файл манифеста с панели администрирования для разработчиков соединителей (измененный согласно инструкциям из предыдущего раздела) и два файла значков.</span><span class="sxs-lookup"><span data-stu-id="beeb1-175">You can create a .zip package using the manifest file from the Connectors Developer Dashboard (modified as directed in the preceding section) and the two icon files.</span></span>

<span data-ttu-id="beeb1-176">После отправки приложения откройте список соединителей с любого канала.</span><span class="sxs-lookup"><span data-stu-id="beeb1-176">After you upload the app, open the Connectors list from any channel.</span></span> <span data-ttu-id="beeb1-177">Прокрутите вниз, чтобы найти свое приложение в разделе **Отправленные**.</span><span class="sxs-lookup"><span data-stu-id="beeb1-177">Scroll to the bottom to see your app in the **Uploaded** section.</span></span>

![Снимок экрана раздела отправленных приложений в диалоговом окне соединителя](~/assets/images/connectors/connector_dialog_uploaded.png)

<span data-ttu-id="beeb1-179">Теперь можно запустить среду настройки.</span><span class="sxs-lookup"><span data-stu-id="beeb1-179">You can now launch the configuration experience.</span></span> <span data-ttu-id="beeb1-180">Обратите внимание, что этот процесс полностью выполняется в Microsoft Teams во всплывающем окне.</span><span class="sxs-lookup"><span data-stu-id="beeb1-180">Be aware that this flow occurs entirely within Microsoft Teams through a pop-up window.</span></span> <span data-ttu-id="beeb1-181">В настоящее время он отличается от процесса настройки в созданных нами соединителях. Мы работаем над согласованием этих процессов.</span><span class="sxs-lookup"><span data-stu-id="beeb1-181">Currently, this behavior differs from the configuration experience in Connectors that we created; we are working on unifying the experiences.</span></span>

<span data-ttu-id="beeb1-182">Чтобы убедиться в правильной работе действия `HttpPOST`, используйте [пользовательский входящий веб-перехватчик](#setting-up-a-custom-incoming-webhook).</span><span class="sxs-lookup"><span data-stu-id="beeb1-182">To verify that an `HttpPOST` action is working correctly, use your [custom incoming webhook](#setting-up-a-custom-incoming-webhook).</span></span>

## <a name="rate-limiting-for-connectors"></a><span data-ttu-id="beeb1-183">Ограничение скорости для соединителей</span><span class="sxs-lookup"><span data-stu-id="beeb1-183">Rate limiting for connectors</span></span>

<span data-ttu-id="beeb1-184">Ограничения скорости приложений управляют трафиком, который разрешено создавать в канале соединителю или входящему веб-перехватчику.</span><span class="sxs-lookup"><span data-stu-id="beeb1-184">Application rate limits control the traffic that a connector or an incoming webhook is allowed to generate on a channel.</span></span> <span data-ttu-id="beeb1-185">В Teams запросы отслеживаются с помощью окна фиксированной скорости и инкрементного счетчика с измерением в секундах.</span><span class="sxs-lookup"><span data-stu-id="beeb1-185">Teams tracks requests via a fixed-rate window and incremental counter measured in seconds.</span></span>  <span data-ttu-id="beeb1-186">При наличии слишком большого количества запросов скорость подключения клиента будет ограничена до обновления окна, т. е. в течение длительности окна фиксированной скорости.</span><span class="sxs-lookup"><span data-stu-id="beeb1-186">If too many requests are made, the client connection will be throttled until the window refreshes, i.e., for the duration of the fixed rate.</span></span>

### <a name="transactions-per-second-thresholds"></a><span data-ttu-id="beeb1-187">**Пороговые значения количества транзакций в секунду**</span><span class="sxs-lookup"><span data-stu-id="beeb1-187">**Transactions per second thresholds**</span></span>

| <span data-ttu-id="beeb1-188">Время (секунды)</span><span class="sxs-lookup"><span data-stu-id="beeb1-188">Time (seconds)</span></span>  | <span data-ttu-id="beeb1-189">Максимальное разрешенное количество запросов</span><span class="sxs-lookup"><span data-stu-id="beeb1-189">Maximum allowed requests</span></span>  |
|---|---|
| <span data-ttu-id="beeb1-190">1</span><span class="sxs-lookup"><span data-stu-id="beeb1-190">1</span></span>   | <span data-ttu-id="beeb1-191">4</span><span class="sxs-lookup"><span data-stu-id="beeb1-191">4</span></span>  |  
| <span data-ttu-id="beeb1-192">30</span><span class="sxs-lookup"><span data-stu-id="beeb1-192">30</span></span>   | <span data-ttu-id="beeb1-193">60</span><span class="sxs-lookup"><span data-stu-id="beeb1-193">60</span></span>  |  
| <span data-ttu-id="beeb1-194">3600</span><span class="sxs-lookup"><span data-stu-id="beeb1-194">3600</span></span>   | <span data-ttu-id="beeb1-195">100</span><span class="sxs-lookup"><span data-stu-id="beeb1-195">100</span></span>  |
| <span data-ttu-id="beeb1-196">7200</span><span class="sxs-lookup"><span data-stu-id="beeb1-196">7200</span></span> | <span data-ttu-id="beeb1-197">150</span><span class="sxs-lookup"><span data-stu-id="beeb1-197">150</span></span>  |
| <span data-ttu-id="beeb1-198">86 400</span><span class="sxs-lookup"><span data-stu-id="beeb1-198">86400</span></span>  | <span data-ttu-id="beeb1-199">1800</span><span class="sxs-lookup"><span data-stu-id="beeb1-199">1800</span></span>  |

<span data-ttu-id="beeb1-200">*Также см.* [Соединители Office 365 — Microsoft Teams](https://docs.microsoft.com/connectors/teams/)</span><span class="sxs-lookup"><span data-stu-id="beeb1-200">*See also* [Office 365 Connectors — Microsoft Teams](https://docs.microsoft.com/connectors/teams/)</span></span>

<span data-ttu-id="beeb1-201">[Логика повторных попыток с экспоненциальной задержкой](/azure/architecture/patterns/retry), подобная приведенной ниже, поможет избежать ограничения скорости в тех случаях, когда число запросов за секунду превышает пределы.</span><span class="sxs-lookup"><span data-stu-id="beeb1-201">A [retry logic with exponential back-off](/azure/architecture/patterns/retry) like below would mitigate rate limiting for cases where requests are exceeding the limits within a second.</span></span> <span data-ttu-id="beeb1-202">Следуйте [рекомендациям](../../bots/how-to/rate-limit.md#best-practices), чтобы предотвратить достижение пределов скорости.</span><span class="sxs-lookup"><span data-stu-id="beeb1-202">Please follow [best practices](../../bots/how-to/rate-limit.md#best-practices) to avoid hitting the rate limits.</span></span>

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
 
<span data-ttu-id="beeb1-203">Эти ограничения установлены с целью предотвратить перегрузку канала запросами от соединителя и обеспечивают удобство работы пользователей.</span><span class="sxs-lookup"><span data-stu-id="beeb1-203">These limits are in place to reduce spamming a channel by a connector and ensures an optimal experience to your end users.</span></span>
