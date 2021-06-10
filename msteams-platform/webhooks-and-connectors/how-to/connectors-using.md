---
title: Отправка сообщений соединителям и веб-перехватчикам
description: Сведения о том, как использовать Соединители Office 365 в Microsoft Teams.
ms.topic: how-to
localization_priority: Normal
keywords: соединитель teams o365
ms.openlocfilehash: 96092e4589f218a96f31ce05339b89acb82f1fd7
ms.sourcegitcommit: 20764037458026e5870ee3975b966404103af650
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/20/2021
ms.locfileid: "52583738"
---
# <a name="sending-messages-to-connectors-and-webhooks"></a><span data-ttu-id="a362e-104">Отправка сообщений соединителям и веб-перехватчикам</span><span class="sxs-lookup"><span data-stu-id="a362e-104">Sending messages to connectors and webhooks</span></span>

<span data-ttu-id="a362e-105">Чтобы отправить сообщение через соединитель Office 365 или входящий веб-перехватчик, необходимо отправить полезные данные JSON на URL-адрес веб-перехватчика.</span><span class="sxs-lookup"><span data-stu-id="a362e-105">To send a message through your Office 365 Connector or incoming webhook, you post a JSON payload to the webhook URL.</span></span> <span data-ttu-id="a362e-106">Как правило, эти полезные данные будут отображаться в [форме карточки соединителя Office 365](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).</span><span class="sxs-lookup"><span data-stu-id="a362e-106">Typically this payload will be in the form of an [Office 365 Connector Card](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).</span></span>

<span data-ttu-id="a362e-107">С помощью этого кода JSON также можно создавать карточки с различными элементами для ввода данных, например текстовыми полями, переключателями множественного выбора или средствами выбора даты и времени.</span><span class="sxs-lookup"><span data-stu-id="a362e-107">You can also use this JSON to create cards containing rich inputs, such as text entry, multi-select, or picking a date and time.</span></span> <span data-ttu-id="a362e-108">Код, генерирующий карточку и отправляющий ее на URL-адрес веб-перехватчика, может выполняться в любой размещенной службе.</span><span class="sxs-lookup"><span data-stu-id="a362e-108">The code that generates the card and posts to the webhook URL can be running on any hosted service.</span></span> <span data-ttu-id="a362e-109">Эти карточки определяются в составе сообщений с действиями, а также поддерживаются в [карточках](~/task-modules-and-cards/what-are-cards.md), используемых ботами Teams и расширениями для обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="a362e-109">These cards are defined as part of actionable messages, and are also supported in [cards](~/task-modules-and-cards/what-are-cards.md) used in Teams bots and Messaging extensions.</span></span>

### <a name="example-connector-message"></a><span data-ttu-id="a362e-110">Пример сообщения соединителя</span><span class="sxs-lookup"><span data-stu-id="a362e-110">Example connector message</span></span>

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

<span data-ttu-id="a362e-111">Это сообщение создает следующую карточку в канале:</span><span class="sxs-lookup"><span data-stu-id="a362e-111">This message produces the following card in the channel:</span></span>

![Снимок экрана с карточкой соединителя](~/assets/images/connectors/connector_message.png)

## <a name="creating-actionable-messages"></a><span data-ttu-id="a362e-113">Создание сообщений с действиями</span><span class="sxs-lookup"><span data-stu-id="a362e-113">Creating actionable messages</span></span>

<span data-ttu-id="a362e-114">В примере карточки из предыдущего раздела отображаются три кнопки.</span><span class="sxs-lookup"><span data-stu-id="a362e-114">The example in the preceding section includes three visible buttons on the card.</span></span> <span data-ttu-id="a362e-115">Каждая кнопка определена в свойстве `potentialAction` сообщения с помощью действий `ActionCard`, каждое из которых содержит тип элемента ввода: текстовое поле, элемент управления "Выбор даты" или список с возможностью выбора нескольких вариантов.</span><span class="sxs-lookup"><span data-stu-id="a362e-115">Each button is defined in the `potentialAction` property of the message by using `ActionCard` actions, each containing an input type: a text field, a date picker, or a multi-choice list.</span></span> <span data-ttu-id="a362e-116">С каждым действием `ActionCard` связано другое действие, например `HttpPOST`.</span><span class="sxs-lookup"><span data-stu-id="a362e-116">Each `ActionCard` action has an associated action, for example `HttpPOST`.</span></span>

<span data-ttu-id="a362e-117">Карточки соединителей поддерживают действия трех типов:</span><span class="sxs-lookup"><span data-stu-id="a362e-117">Connector cards support three types of actions:</span></span>

- <span data-ttu-id="a362e-118">`ActionCard`: представляет один или несколько типов входных данных и соответствующие действия;</span><span class="sxs-lookup"><span data-stu-id="a362e-118">`ActionCard` Presents one or more input types and associated actions</span></span>
- <span data-ttu-id="a362e-119">`HttpPOST`: отправляет запрос POST на URL-адрес;</span><span class="sxs-lookup"><span data-stu-id="a362e-119">`HttpPOST` Sends a POST request to a URL</span></span>
- <span data-ttu-id="a362e-120">`OpenUri`: открывает URI в отдельном браузере или приложении; при необходимости ссылается на разные URI в зависимости от операционной системы.</span><span class="sxs-lookup"><span data-stu-id="a362e-120">`OpenUri` Opens a URI in a separate browser or app; optionally targets different URIs based on operating systems</span></span>

<span data-ttu-id="a362e-121">Действие `ActionCard` поддерживает три типа входных данных:</span><span class="sxs-lookup"><span data-stu-id="a362e-121">The `ActionCard` action supports three input types:</span></span>

- <span data-ttu-id="a362e-122">`TextInput`: однострочное или многострочное текстовое поле с необязательным ограничением длины;</span><span class="sxs-lookup"><span data-stu-id="a362e-122">`TextInput` A single-line or multiline text field with an optional length limit</span></span>
- <span data-ttu-id="a362e-123">`DateInput`: средство выбора даты с необязательным выбором времени;</span><span class="sxs-lookup"><span data-stu-id="a362e-123">`DateInput` A date selector with an optional time selector</span></span>
- <span data-ttu-id="a362e-124">`MultichoiceInput`: нумерованный список вариантов с возможностью выбора одного или нескольких пунктов;</span><span class="sxs-lookup"><span data-stu-id="a362e-124">`MultichoiceInput` A enumerated list of choices offering either a single selection or multiple selections</span></span>

<span data-ttu-id="a362e-125">`MultichoiceInput` поддерживает свойство `style`, указывающее, отображается ли список изначально полностью развернутым.</span><span class="sxs-lookup"><span data-stu-id="a362e-125">`MultichoiceInput` supports a `style` property that controls whether the list initially appears fully expanded.</span></span> <span data-ttu-id="a362e-126">Значение `style` по умолчанию зависит от значения `isMultiSelect`.</span><span class="sxs-lookup"><span data-stu-id="a362e-126">The default value of `style` depends on the value of `isMultiSelect`.</span></span>

| `isMultiSelect` | <span data-ttu-id="a362e-127">Значение `style` по умолчанию</span><span class="sxs-lookup"><span data-stu-id="a362e-127">`style` default</span></span> |
| --- | --- |
| <span data-ttu-id="a362e-128">`false` или не задано</span><span class="sxs-lookup"><span data-stu-id="a362e-128">`false` or not specified</span></span> | `compact` |
| `true` | `expanded` |

<span data-ttu-id="a362e-129">Если вам нужно, чтобы список со множественным выбором изначально отображался в компактном стиле, необходимо задать значения `"isMultiSelect": true` и `"style": true`.</span><span class="sxs-lookup"><span data-stu-id="a362e-129">If you want a multiselect list initially displayed in the compact style, you must specify both `"isMultiSelect": true` and `"style": true`.</span></span>

<span data-ttu-id="a362e-130">Дополнительные сведения о действиях карточек соединителей см. в разделе **[Действия]**(/outlook/actionable-messages/card-reference#actions) справки по карточкам сообщений с действиями.</span><span class="sxs-lookup"><span data-stu-id="a362e-130">For more information on Connector card actions, see **[Actions]**(/outlook/actionable-messages/card-reference#actions) in the actionable message card reference.</span></span>

> [!NOTE]
> <span data-ttu-id="a362e-131">Значение `compact` для свойства `style` в Microsoft Teams равноценно значению `normal` для свойства `style` в Microsoft Outlook.</span><span class="sxs-lookup"><span data-stu-id="a362e-131">Specifying `compact` for the `style` property in Microsoft Teams is the same as specifying `normal` for the `style` property in Microsoft Outlook.</span></span>
> 
> <span data-ttu-id="a362e-132">Для действия HttpPOST маркер носителя включается в запросы.</span><span class="sxs-lookup"><span data-stu-id="a362e-132">For the HttpPOST action, the bearer token is included with the requests.</span></span> <span data-ttu-id="a362e-133">Маркер содержит удостоверение Azure AD пользователя Office 365, выполнившего действие.</span><span class="sxs-lookup"><span data-stu-id="a362e-133">This token includes the Azure AD identity of the Office 365 user who took the action.</span></span>

## <a name="setting-up-a-custom-incoming-webhook"></a><span data-ttu-id="a362e-134">Настройка пользовательского входящего веб-перехватчика</span><span class="sxs-lookup"><span data-stu-id="a362e-134">Setting up a custom incoming webhook</span></span>

<span data-ttu-id="a362e-135">Выполните следующие действия, чтобы узнать, как отправить простую карту в соединителю:</span><span class="sxs-lookup"><span data-stu-id="a362e-135">Follow these steps to see how to send a simple card to a Connector:</span></span>

1. <span data-ttu-id="a362e-136">В Microsoft Teams нажмите **Дополнительные параметры** (**&#8943;**) рядом с названием канала и выберите **Соединители**.</span><span class="sxs-lookup"><span data-stu-id="a362e-136">In Microsoft Teams, choose **More options** (**&#8943;**) next to the channel name and then choose **Connectors**.</span></span>
1. <span data-ttu-id="a362e-137">Прокрутите список соединителей до пункта **Входящий веб-перехватчик** и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="a362e-137">Scroll through the list of Connectors to **Incoming Webhook**, and choose **Add**.</span></span>
1. <span data-ttu-id="a362e-138">Введите имя веб-перехватчика, отправьте изображение, которое следует связать с данными от веб-перехватчика, и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a362e-138">Enter a name for the webhook, upload an image to associate with data from the webhook, and choose **Create**.</span></span>
1. <span data-ttu-id="a362e-139">Скопируйте веб-перехватчик в буфер обмена и сохраните его.</span><span class="sxs-lookup"><span data-stu-id="a362e-139">Copy the webhook to the clipboard and save it.</span></span> <span data-ttu-id="a362e-140">Для отправки информации в Microsoft Teams вам потребуется URL-адрес веб-перехватчика.</span><span class="sxs-lookup"><span data-stu-id="a362e-140">You'll need the webhook URL for sending information to Microsoft Teams.</span></span>
1. <span data-ttu-id="a362e-141">Нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="a362e-141">Choose **Done**.</span></span>

### <a name="post-a-message-to-the-webhook-using-curl"></a><span data-ttu-id="a362e-142">Отправка сообщения веб-перехватчику с помощью cURL</span><span class="sxs-lookup"><span data-stu-id="a362e-142">Post a message to the webhook using cURL</span></span>

<span data-ttu-id="a362e-143">Для выполнения описанных ниже действий используется [cURL](https://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="a362e-143">The following steps use [cURL](https://curl.haxx.se/).</span></span> <span data-ttu-id="a362e-144">Предполагается, что у вас уже установлена эта программа, а вы знакомы с основами ее использования.</span><span class="sxs-lookup"><span data-stu-id="a362e-144">We assume that you have this installed and are familiar with its basic usage.</span></span>

1. <span data-ttu-id="a362e-145">Введите в командной строке следующую команду cURL:</span><span class="sxs-lookup"><span data-stu-id="a362e-145">From the command line, enter the following cURL command:</span></span>

   ```bash
   // on macOS or Linux
   curl -H 'Content-Type: application/json' -d '{"text": "Hello World"}' <YOUR WEBHOOK URL>
   ```

   ```bash
   // on Windows
   curl.exe -H "Content-Type:application/json" -d "{'text':'Hello World'}" <YOUR WEBHOOK URL>
   ```

1. <span data-ttu-id="a362e-146">В случае успешного выполнения запроса POST команда `curl` должна возвращать простой отклик **1**.</span><span class="sxs-lookup"><span data-stu-id="a362e-146">If the POST succeeds, you should see a simple **1** output by `curl`.</span></span>
1. <span data-ttu-id="a362e-147">Проверьте клиент Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="a362e-147">Check the Microsoft Team client.</span></span> <span data-ttu-id="a362e-148">Вы увидите новую карточку, опубликованную в группе.</span><span class="sxs-lookup"><span data-stu-id="a362e-148">You should see the new card posted to the team.</span></span>

### <a name="post-a-message-to-the-webhook-using-powershell"></a><span data-ttu-id="a362e-149">Отправка сообщения веб-перехватчику с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="a362e-149">Post a message to the webhook using PowerShell</span></span>

<span data-ttu-id="a362e-150">Для выполнения описанных ниже действий используется PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a362e-150">The following steps use PowerShell.</span></span> <span data-ttu-id="a362e-151">Предполагается, что у вас уже установлена эта программа, а вы знакомы с основами ее использования.</span><span class="sxs-lookup"><span data-stu-id="a362e-151">We assume that you have this installed and are familiar with its basic usage.</span></span>

1. <span data-ttu-id="a362e-152">В командной строке PowerShell введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a362e-152">From the PowerShell prompt, enter the following command:</span></span>

   ```powershell
   Invoke-RestMethod -Method post -ContentType 'Application/Json' -Body '{"text":"Hello World!"}' -Uri <YOUR WEBHOOK URL>
   ```

1. <span data-ttu-id="a362e-153">В случае успешного выполнения запроса POST команда `Invoke-RestMethod` должна возвращать простой отклик **1**.</span><span class="sxs-lookup"><span data-stu-id="a362e-153">If the POST succeeds, you should see a simple **1** output by `Invoke-RestMethod`.</span></span>
1. <span data-ttu-id="a362e-154">Проверьте канал Microsoft Teams, связанный с URL-адресом веб-перехватчика.</span><span class="sxs-lookup"><span data-stu-id="a362e-154">Check the Microsoft Teams channel associated with the webhook URL.</span></span> <span data-ttu-id="a362e-155">На канале должна появиться новая карточка.</span><span class="sxs-lookup"><span data-stu-id="a362e-155">You should see the new card posted to the channel.</span></span>

- <span data-ttu-id="a362e-156">[Включение двух значков](../../concepts/build-and-test/apps-package.md#app-icons).</span><span class="sxs-lookup"><span data-stu-id="a362e-156">[Include two icons](../../concepts/build-and-test/apps-package.md#app-icons).</span></span>
- <span data-ttu-id="a362e-157">Измените раздел `icons` манифеста, чтобы он ссылался на имена файлов значков, а не на их URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="a362e-157">Modify the `icons` portion of the manifest to refer to the file names of the icons instead of URLs.</span></span>

<span data-ttu-id="a362e-158">В следующем manifest.jsфайле содержатся основные элементы, необходимые для тестирования и отправки приложения:</span><span class="sxs-lookup"><span data-stu-id="a362e-158">The following manifest.json file contains the basic elements needed to test and submit your app:</span></span>

> [!NOTE]
> <span data-ttu-id="a362e-159">Замените `id` и `connectorId` в приведенном ниже примере на GUID соединителя.</span><span class="sxs-lookup"><span data-stu-id="a362e-159">Replace `id` and `connectorId` in the following example with the GUID of your Connector.</span></span>

#### <a name="example-manifestjson-with-connector"></a><span data-ttu-id="a362e-160">Пример manifest.json с соединителем</span><span class="sxs-lookup"><span data-stu-id="a362e-160">Example manifest.json with connector</span></span>

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

## <a name="send-adaptive-cards-using-an-incoming-webhook"></a><span data-ttu-id="a362e-161">Отправка адаптивных карточек с помощью входящего веб-перехватчика</span><span class="sxs-lookup"><span data-stu-id="a362e-161">Send adaptive cards using an incoming webhook</span></span>

> [!NOTE]
>
> <span data-ttu-id="a362e-162">✔ Все встроенные элементы схемы адаптивной карточки, кроме `Action.Submit`, полностью поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="a362e-162">✔ All native adaptive card schema elements, except `Action.Submit`, are fully supported.</span></span>
>
> <span data-ttu-id="a362e-163">✔ Поддерживаемые действия: [**Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html), [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html) и [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html).</span><span class="sxs-lookup"><span data-stu-id="a362e-163">✔ The supported Actions are [**Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html), [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html), and [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html).</span></span>

### <a name="the-flow-for-sending-adaptive-cards-via-an-incoming-webhook-is-as-follows"></a><span data-ttu-id="a362e-164">Для отправки [адаптивных карточек](../../task-modules-and-cards/cards/cards-reference.md#adaptive-card) через входящий веб-перехватчик используется следующий поток:</span><span class="sxs-lookup"><span data-stu-id="a362e-164">The flow for sending [adaptive cards](../../task-modules-and-cards/cards/cards-reference.md#adaptive-card) via an incoming webhook is as follows:</span></span>

1. <span data-ttu-id="a362e-165">[Настройка настраиваемой веб-страницы](#setting-up-a-custom-incoming-webhook) в Teams.</span><span class="sxs-lookup"><span data-stu-id="a362e-165">[Setup a custom webhook](#setting-up-a-custom-incoming-webhook) in Teams.</span></span>
1. <span data-ttu-id="a362e-166">Создайте файл JSON адаптивной карты:</span><span class="sxs-lookup"><span data-stu-id="a362e-166">Create your adaptive card JSON file:</span></span>

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

    > [!div class="checklist"]
    >
    > - <span data-ttu-id="a362e-167">Поле `"type"` должно иметь значение `"message"`.</span><span class="sxs-lookup"><span data-stu-id="a362e-167">The `"type"` field must be `"message"`.</span></span>
    > - <span data-ttu-id="a362e-168">Массив `"attachments"` содержит набор объектов card.</span><span class="sxs-lookup"><span data-stu-id="a362e-168">The `"attachments"` array contains a set of card objects.</span></span>
    > - <span data-ttu-id="a362e-169">В поле `"contentType"` следует задать тип "Адаптивная карточка".</span><span class="sxs-lookup"><span data-stu-id="a362e-169">The `"contentType"` field must be set to adaptive card type.</span></span>
    > - <span data-ttu-id="a362e-170">Объект `"content"` — это карточка, отформатированная в JSON.</span><span class="sxs-lookup"><span data-stu-id="a362e-170">The `"content"` object is the card formatted in JSON.</span></span>

1. <span data-ttu-id="a362e-171">Проверьте адаптивную карту с помощью Почтальон.</span><span class="sxs-lookup"><span data-stu-id="a362e-171">Test your adaptive card with Postman.</span></span>

<span data-ttu-id="a362e-172">Вы можете протестировать адаптивную карточку с помощью [Postman](https://www.postman.com), чтобы отправить запрос POST на URL-адрес, который вы создали при настройке входящего веб-перехватчика.</span><span class="sxs-lookup"><span data-stu-id="a362e-172">You can test your adaptive card using [Postman](https://www.postman.com) to send a POST request to the URL that you created when you setup your incoming webhook.</span></span> <span data-ttu-id="a362e-173">Вставьте файл JSON в текст запроса и просмотрите сообщение адаптивной карточки в Teams.</span><span class="sxs-lookup"><span data-stu-id="a362e-173">Paste your JSON file in the body of the request and view your adaptive card message in Teams.</span></span>

>[!TIP]
> <span data-ttu-id="a362e-174">В тексте запроса проверки POST можно использовать [образцы и шаблоны](https://adaptivecards.io/samples) кода адаптивной карточки.</span><span class="sxs-lookup"><span data-stu-id="a362e-174">You can use adaptive card code [Samples and Templates](https://adaptivecards.io/samples) for the body of your test Post request.</span></span>

## <a name="testing-your-connector"></a><span data-ttu-id="a362e-175">Тестирование соединителя</span><span class="sxs-lookup"><span data-stu-id="a362e-175">Testing your connector</span></span>

<span data-ttu-id="a362e-176">Чтобы тестировать соединитель, отправьте его команде, как в любом другом приложении.</span><span class="sxs-lookup"><span data-stu-id="a362e-176">To test your Connector, upload it to a team as you would with any other app.</span></span> <span data-ttu-id="a362e-177">Вы можете создать пакет .zip с помощью файла манифеста из панели мониторинга разработчика соединителов, которая была изменена в предыдущем разделе и двух файлах значков.</span><span class="sxs-lookup"><span data-stu-id="a362e-177">You can create a .zip package using the manifest file from the Connectors Developer Dashboard which was modified as directed in the preceding section and the two icon files.</span></span>

<span data-ttu-id="a362e-178">После отправки приложения откройте список соединителей с любого канала.</span><span class="sxs-lookup"><span data-stu-id="a362e-178">After you upload the app, open the Connectors list from any channel.</span></span> <span data-ttu-id="a362e-179">Прокрутите вниз, чтобы просмотреть приложение в разделе **Uploaded:**</span><span class="sxs-lookup"><span data-stu-id="a362e-179">Scroll to the bottom to see your app in the **Uploaded** section:</span></span>

![Снимок экрана раздела отправленных приложений в диалоговом окне соединителя](~/assets/images/connectors/connector_dialog_uploaded.png)

<span data-ttu-id="a362e-181">Теперь можно запустить среду настройки.</span><span class="sxs-lookup"><span data-stu-id="a362e-181">You can now launch the configuration experience.</span></span> <span data-ttu-id="a362e-182">Обратите внимание, что этот процесс полностью выполняется в Microsoft Teams во всплывающем окне.</span><span class="sxs-lookup"><span data-stu-id="a362e-182">Be aware that this flow occurs entirely within Microsoft Teams through a pop-up window.</span></span> <span data-ttu-id="a362e-183">В настоящее время он отличается от процесса настройки в созданных нами соединителях. Мы работаем над согласованием этих процессов.</span><span class="sxs-lookup"><span data-stu-id="a362e-183">Currently, this behavior differs from the configuration experience in Connectors that we created; we are working on unifying the experiences.</span></span>

<span data-ttu-id="a362e-184">Чтобы убедиться в правильной работе действия `HttpPOST`, используйте [пользовательский входящий веб-перехватчик](#setting-up-a-custom-incoming-webhook).</span><span class="sxs-lookup"><span data-stu-id="a362e-184">To verify that an `HttpPOST` action is working correctly, use your [custom incoming webhook](#setting-up-a-custom-incoming-webhook).</span></span>

## <a name="rate-limiting-for-connectors"></a><span data-ttu-id="a362e-185">Ограничение скорости для соединителей</span><span class="sxs-lookup"><span data-stu-id="a362e-185">Rate limiting for connectors</span></span>

<span data-ttu-id="a362e-186">Ограничения скорости приложений управляют трафиком, который разрешено создавать в канале соединителю или входящему веб-перехватчику.</span><span class="sxs-lookup"><span data-stu-id="a362e-186">Application rate limits control the traffic that a connector or an incoming webhook is allowed to generate on a channel.</span></span> <span data-ttu-id="a362e-187">В Teams запросы отслеживаются с помощью окна фиксированной скорости и инкрементного счетчика с измерением в секундах.</span><span class="sxs-lookup"><span data-stu-id="a362e-187">Teams tracks requests via a fixed-rate window and incremental counter measured in seconds.</span></span>  <span data-ttu-id="a362e-188">При наличии слишком большого количества запросов скорость подключения клиента будет ограничена до обновления окна, т. е. в течение длительности окна фиксированной скорости.</span><span class="sxs-lookup"><span data-stu-id="a362e-188">If too many requests are made, the client connection will be throttled until the window refreshes, i.e., for the duration of the fixed rate.</span></span>

### <a name="transactions-per-second-thresholds"></a><span data-ttu-id="a362e-189">**Пороговые значения количества транзакций в секунду**</span><span class="sxs-lookup"><span data-stu-id="a362e-189">**Transactions per second thresholds**</span></span>

| <span data-ttu-id="a362e-190">Время (секунды)</span><span class="sxs-lookup"><span data-stu-id="a362e-190">Time (seconds)</span></span>  | <span data-ttu-id="a362e-191">Максимальное разрешенное количество запросов</span><span class="sxs-lookup"><span data-stu-id="a362e-191">Maximum allowed requests</span></span>  |
|---|---|
| <span data-ttu-id="a362e-192">1</span><span class="sxs-lookup"><span data-stu-id="a362e-192">1</span></span>   | <span data-ttu-id="a362e-193">4 </span><span class="sxs-lookup"><span data-stu-id="a362e-193">4</span></span>  |  
| <span data-ttu-id="a362e-194">30</span><span class="sxs-lookup"><span data-stu-id="a362e-194">30</span></span>   | <span data-ttu-id="a362e-195">60</span><span class="sxs-lookup"><span data-stu-id="a362e-195">60</span></span>  |  
| <span data-ttu-id="a362e-196">3600</span><span class="sxs-lookup"><span data-stu-id="a362e-196">3600</span></span>   | <span data-ttu-id="a362e-197">100</span><span class="sxs-lookup"><span data-stu-id="a362e-197">100</span></span>  |
| <span data-ttu-id="a362e-198">7200</span><span class="sxs-lookup"><span data-stu-id="a362e-198">7200</span></span> | <span data-ttu-id="a362e-199">150</span><span class="sxs-lookup"><span data-stu-id="a362e-199">150</span></span>  |
| <span data-ttu-id="a362e-200">86400</span><span class="sxs-lookup"><span data-stu-id="a362e-200">86400</span></span>  | <span data-ttu-id="a362e-201">1800</span><span class="sxs-lookup"><span data-stu-id="a362e-201">1800</span></span>  |

<span data-ttu-id="a362e-202">[Логика повторных попыток с экспоненциальной задержкой](/azure/architecture/patterns/retry), подобная приведенной ниже, поможет избежать ограничения скорости в тех случаях, когда число запросов за секунду превышает пределы.</span><span class="sxs-lookup"><span data-stu-id="a362e-202">A [retry logic with exponential back-off](/azure/architecture/patterns/retry) like below would mitigate rate limiting for cases where requests are exceeding the limits within a second.</span></span> <span data-ttu-id="a362e-203">См. за [откликами HTTP 429](../../bots/how-to/rate-limit.md#handle-http-429-responses), чтобы не достигать ограничений по скорости.</span><span class="sxs-lookup"><span data-stu-id="a362e-203">Refer [HTTP 429 responses](../../bots/how-to/rate-limit.md#handle-http-429-responses) to avoid hitting the rate limits.</span></span>

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
 
<span data-ttu-id="a362e-204">Эти ограничения установлены с целью предотвратить перегрузку канала запросами от соединителя и обеспечивают удобство работы пользователей.</span><span class="sxs-lookup"><span data-stu-id="a362e-204">These limits are in place to reduce spamming a channel by a connector and ensures an optimal experience to your end users.</span></span>

## <a name="see-also"></a><span data-ttu-id="a362e-205">См. также</span><span class="sxs-lookup"><span data-stu-id="a362e-205">See also</span></span>

[<span data-ttu-id="a362e-206">Office 365 Соединители — Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="a362e-206">Office 365 Connectors — Microsoft Teams</span></span>](/connectors/teams/)
