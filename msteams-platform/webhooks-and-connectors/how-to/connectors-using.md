---
title: Отправка сообщений соединителям и веб-перехватчикам
description: Сведения о том, как использовать Соединители Office 365 в Microsoft Teams.
localization_priority: Priority
keywords: соединитель teams o365
ms.openlocfilehash: b22159002713ccec6441f2128190e9944945aff6
ms.sourcegitcommit: 44ac886c0ca34a16222d3991a61606f8483b8481
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/05/2020
ms.locfileid: "41783915"
---
# <a name="sending-messages-to-connectors-and-webhooks"></a><span data-ttu-id="c259e-104">Отправка сообщений соединителям и веб-перехватчикам</span><span class="sxs-lookup"><span data-stu-id="c259e-104">Sending messages to Connectors and Webhooks</span></span>

<span data-ttu-id="c259e-105">Чтобы отправить сообщение через соединитель Office 365 или входящий веб-перехватчик, необходимо отправить полезные данные JSON на URL-адрес веб-перехватчика.</span><span class="sxs-lookup"><span data-stu-id="c259e-105">To send a message through your Office 365 Connector or incoming webhook, you post a JSON payload to the webhook URL.</span></span> <span data-ttu-id="c259e-106">Как правило, эти полезные данные будут отображаться в [форме карточки соединителя Office 365](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).</span><span class="sxs-lookup"><span data-stu-id="c259e-106">Typically this payload will be in the form of an [Office 365 Connector Card](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).</span></span>

<span data-ttu-id="c259e-107">С помощью этого кода JSON также можно создавать карточки с различными элементами для ввода данных, например текстовыми полями, переключателями множественного выбора или средствами выбора даты и времени.</span><span class="sxs-lookup"><span data-stu-id="c259e-107">You can also use this JSON to create cards containing rich inputs, such as text entry, multi-select, or picking a date and time.</span></span> <span data-ttu-id="c259e-108">Код, генерирующий карточку и отправляющий ее на URL-адрес веб-перехватчика, может выполняться в любой размещенной службе.</span><span class="sxs-lookup"><span data-stu-id="c259e-108">The code that generates the card and posts to the webhook URL can be running on any hosted service.</span></span> <span data-ttu-id="c259e-109">Эти карточки определяются в составе сообщений с действиями, а также поддерживаются в [карточках](~/task-modules-and-cards/what-are-cards.md), используемых ботами Teams и расширениями для обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="c259e-109">These cards are defined as part of actionable messages, and are also supported in [cards](~/task-modules-and-cards/what-are-cards.md) used in Teams bots and Messaging extensions.</span></span>

### <a name="example-connector-message"></a><span data-ttu-id="c259e-110">Пример сообщения соединителя</span><span class="sxs-lookup"><span data-stu-id="c259e-110">Example Connector message</span></span>

```json
{
    "@type": "MessageCard",
    "@context": "http://schema.org/extensions",
    "themeColor": "0076D7",
    "summary": "Larry Bryant created a new task",
    "sections": [{
        "activityTitle": "![TestImage](https://47a92947.ngrok.io/Content/Images/default.png)Larry Bryant created a new task",
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
            "target": "http://..."
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
            "target": "http://..."
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
            "target": "http://..."
        }]
    }]
}
```

<span data-ttu-id="c259e-111">Это сообщение создает на канале представленную ниже карточку.</span><span class="sxs-lookup"><span data-stu-id="c259e-111">This message produces the following card in the channel.</span></span>

![Снимок экрана с карточкой соединителя](~/assets/images/connectors/connector_message.png)

## <a name="creating-actionable-messages"></a><span data-ttu-id="c259e-113">Создание сообщений с действиями</span><span class="sxs-lookup"><span data-stu-id="c259e-113">Creating actionable messages</span></span>

<span data-ttu-id="c259e-114">В примере карточки из предыдущего раздела отображаются три кнопки.</span><span class="sxs-lookup"><span data-stu-id="c259e-114">The example in the preceding section includes three visible buttons on the card.</span></span> <span data-ttu-id="c259e-115">Каждая кнопка определена в свойстве `potentialAction` сообщения с помощью действий `ActionCard`, каждое из которых содержит тип элемента ввода: текстовое поле, элемент управления "Выбор даты" или список с возможностью выбора нескольких вариантов.</span><span class="sxs-lookup"><span data-stu-id="c259e-115">Each button is defined in the `potentialAction` property of the message by using `ActionCard` actions, each containing an input type: a text field, a date picker, or a multi-choice list.</span></span> <span data-ttu-id="c259e-116">С каждым действием `ActionCard` связано другое действие, например `HttpPOST`.</span><span class="sxs-lookup"><span data-stu-id="c259e-116">Each `ActionCard` action has an associated action, for example `HttpPOST`.</span></span>

<span data-ttu-id="c259e-117">Карточки соединителей поддерживают действия трех типов:</span><span class="sxs-lookup"><span data-stu-id="c259e-117">Connector cards support three types of actions:</span></span>

- <span data-ttu-id="c259e-118">`ActionCard`: представляет один или несколько типов входных данных и соответствующие действия;</span><span class="sxs-lookup"><span data-stu-id="c259e-118">`ActionCard` Presents one or more input types and associated actions</span></span>
- <span data-ttu-id="c259e-119">`HttpPOST`: отправляет запрос POST на URL-адрес;</span><span class="sxs-lookup"><span data-stu-id="c259e-119">`HttpPOST` Sends a POST request to a URL</span></span>
- <span data-ttu-id="c259e-120">`OpenUri`: открывает URI в отдельном браузере или приложении; при необходимости ссылается на разные URI в зависимости от операционной системы.</span><span class="sxs-lookup"><span data-stu-id="c259e-120">`OpenUri` Opens a URI in a separate browser or app; optionally targets different URIs based on operating systems</span></span>

<span data-ttu-id="c259e-121">(Четвертое действие, `ViewAction`, также поддерживается, но больше не требуется. Используйте вместо него действие `OpenUri`.)</span><span class="sxs-lookup"><span data-stu-id="c259e-121">(A fourth action, `ViewAction`, is still supported but no longer needed; use `OpenUri` instead.)</span></span>

<span data-ttu-id="c259e-122">Действие `ActionCard` поддерживает три типа входных данных:</span><span class="sxs-lookup"><span data-stu-id="c259e-122">The `ActionCard` action supports three input types:</span></span>

- <span data-ttu-id="c259e-123">`TextInput`: однострочное или многострочное текстовое поле с необязательным ограничением длины;</span><span class="sxs-lookup"><span data-stu-id="c259e-123">`TextInput` A single-line or multiline text field with an optional length limit</span></span>
- <span data-ttu-id="c259e-124">`DateInput`: средство выбора даты с необязательным выбором времени;</span><span class="sxs-lookup"><span data-stu-id="c259e-124">`DateInput` A date selector with an optional time selector</span></span>
- <span data-ttu-id="c259e-125">`MultichoiceInput`: нумерованный список вариантов с возможностью выбора одного или нескольких пунктов;</span><span class="sxs-lookup"><span data-stu-id="c259e-125">`MultichoiceInput` A enumerated list of choices offering either a single selection or multiple selections</span></span>

<span data-ttu-id="c259e-126">`MultichoiceInput` поддерживает свойство `style`, указывающее, отображается ли список изначально полностью развернутым.</span><span class="sxs-lookup"><span data-stu-id="c259e-126">`MultichoiceInput` supports a `style` property that controls whether the list initially appears fully expanded.</span></span> <span data-ttu-id="c259e-127">Значение `style` по умолчанию зависит от значения `isMultiSelect`.</span><span class="sxs-lookup"><span data-stu-id="c259e-127">The default value of `style` depends on the value of `isMultiSelect`.</span></span>

| `isMultiSelect` | <span data-ttu-id="c259e-128">Значение `style` по умолчанию</span><span class="sxs-lookup"><span data-stu-id="c259e-128">`style` default</span></span> |
| --- | --- |
| <span data-ttu-id="c259e-129">`false` или не задано</span><span class="sxs-lookup"><span data-stu-id="c259e-129">`false` or not specified</span></span> | `compact` |
| `true` | `expanded` |

<span data-ttu-id="c259e-130">Если вам нужно, чтобы список со множественным выбором изначально отображался в компактном стиле, необходимо задать значения `"isMultiSelect": true` и `"style": true`.</span><span class="sxs-lookup"><span data-stu-id="c259e-130">If you want a multiselect list initially displayed in the compact style, you must specify both `"isMultiSelect": true` and `"style": true`.</span></span>

> [!NOTE]
> <span data-ttu-id="c259e-131">Значение `compact` для свойства `style` в Microsoft Teams равноценно значению `normal` для свойства `style` в Microsoft Outlook.</span><span class="sxs-lookup"><span data-stu-id="c259e-131">Specifying `compact` for the `style` property in Microsoft Teams is the same as specifying `normal` for the `style` property in Microsoft Outlook.</span></span>

<span data-ttu-id="c259e-132">Все остальные сведения о действиях карточек соединителей представлены в разделе **[Действия](/outlook/actionable-messages/card-reference#actions)** справки по карточкам сообщений с действиями.</span><span class="sxs-lookup"><span data-stu-id="c259e-132">For all other details about Connector card actions, see **[Actions](/outlook/actionable-messages/card-reference#actions)** in the actionable message card reference.</span></span>

## <a name="setting-up-a-custom-incoming-webhook"></a><span data-ttu-id="c259e-133">Настройка пользовательского входящего веб-перехватчика</span><span class="sxs-lookup"><span data-stu-id="c259e-133">Setting up a custom incoming webhook</span></span>

<span data-ttu-id="c259e-134">Выполните указанные ниже действия, чтобы отправить простую карточку в соединитель.</span><span class="sxs-lookup"><span data-stu-id="c259e-134">Follow these steps to see how to send a simple card to a Connector.</span></span>

1. <span data-ttu-id="c259e-135">В Microsoft Teams нажмите **Дополнительные параметры** (**&#8943;**) рядом с названием канала и выберите **Соединители**.</span><span class="sxs-lookup"><span data-stu-id="c259e-135">In Microsoft Teams, choose **More options** (**&#8943;**) next to the channel name and then choose **Connectors**.</span></span>
2. <span data-ttu-id="c259e-136">Прокрутите список соединителей до пункта **Входящий веб-перехватчик** и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="c259e-136">Scroll through the list of Connectors to **Incoming Webhook**, and choose **Add**.</span></span>
3. <span data-ttu-id="c259e-137">Введите имя веб-перехватчика, отправьте изображение, которое следует связать с данными от веб-перехватчика, и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="c259e-137">Enter a name for the webhook, upload an image to associate with data from the webhook, and choose **Create**.</span></span>
4. <span data-ttu-id="c259e-138">Скопируйте веб-перехватчик в буфер обмена и сохраните его.</span><span class="sxs-lookup"><span data-stu-id="c259e-138">Copy the webhook to the clipboard and save it.</span></span> <span data-ttu-id="c259e-139">Для отправки информации в Microsoft Teams вам потребуется URL-адрес веб-перехватчика.</span><span class="sxs-lookup"><span data-stu-id="c259e-139">You'll need the webhook URL for sending information to Microsoft Teams.</span></span>
5. <span data-ttu-id="c259e-140">Нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="c259e-140">Choose **Done**.</span></span>

### <a name="post-a-message-to-the-webhook-using-curl"></a><span data-ttu-id="c259e-141">Отправка сообщения веб-перехватчику с помощью cURL</span><span class="sxs-lookup"><span data-stu-id="c259e-141">Post a message to the webhook using cURL</span></span>

<span data-ttu-id="c259e-142">Для выполнения описанных ниже действий используется [cURL](https://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="c259e-142">The following steps use [cURL](https://curl.haxx.se/).</span></span> <span data-ttu-id="c259e-143">Предполагается, что у вас уже установлена эта программа, а вы знакомы с основами ее использования.</span><span class="sxs-lookup"><span data-stu-id="c259e-143">We assume that you have this installed and are familiar with its basic usage.</span></span>

1. <span data-ttu-id="c259e-144">Введите в командной строке следующую команду cURL:</span><span class="sxs-lookup"><span data-stu-id="c259e-144">From the command line, enter the following cURL command:</span></span>

   ```bash
   curl -H "Content-Type: application/json" -d "{\"text\": \"Hello World\"}" <YOUR WEBHOOK URL>
   ```

2. <span data-ttu-id="c259e-145">В случае успешного выполнения запроса POST команда `curl` должна возвращать простой отклик **1**.</span><span class="sxs-lookup"><span data-stu-id="c259e-145">If the POST succeeds, you should see a simple **1** output by `curl`.</span></span>
3. <span data-ttu-id="c259e-146">Проверьте клиент Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="c259e-146">Check the Microsoft Team client.</span></span> <span data-ttu-id="c259e-147">Вы увидите новую карточку, опубликованную в группе.</span><span class="sxs-lookup"><span data-stu-id="c259e-147">You should see the new card posted to the team.</span></span>

### <a name="post-a-message-to-the-webhook-using-powershell"></a><span data-ttu-id="c259e-148">Отправка сообщения веб-перехватчику с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="c259e-148">Post a message to the webhook using PowerShell</span></span>

<span data-ttu-id="c259e-149">Для выполнения описанных ниже действий используется PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c259e-149">The following steps use PowerShell.</span></span> <span data-ttu-id="c259e-150">Предполагается, что у вас уже установлена эта программа, а вы знакомы с основами ее использования.</span><span class="sxs-lookup"><span data-stu-id="c259e-150">We assume that you have this installed and are familiar with its basic usage.</span></span>

1. <span data-ttu-id="c259e-151">В командной строке PowerShell введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c259e-151">From the PowerShell prompt, enter the following command:</span></span>

   ```powershell
   Invoke-RestMethod -Method post -ContentType 'Application/Json' -Body '{"text":"Hello World!"}' -Uri <YOUR WEBHOOK URL>
   ```

2. <span data-ttu-id="c259e-152">В случае успешного выполнения запроса POST команда `Invoke-RestMethod` должна возвращать простой отклик **1**.</span><span class="sxs-lookup"><span data-stu-id="c259e-152">If the POST succeeds, you should see a simple **1** output by `Invoke-RestMethod`.</span></span>
3. <span data-ttu-id="c259e-153">Проверьте канал Microsoft Teams, связанный с URL-адресом веб-перехватчика.</span><span class="sxs-lookup"><span data-stu-id="c259e-153">Check the Microsoft Teams channel associated with the webhook URL.</span></span> <span data-ttu-id="c259e-154">На канале должна появиться новая карточка.</span><span class="sxs-lookup"><span data-stu-id="c259e-154">You should see the new card posted to the channel.</span></span>

- <span data-ttu-id="c259e-155">Включите два значка, следуя инструкциям из раздела [Значки](~/concepts/build-and-test/apps-package.md#icons).</span><span class="sxs-lookup"><span data-stu-id="c259e-155">Include two icons, following the instructions in [Icons](~/concepts/build-and-test/apps-package.md#icons).</span></span>
- <span data-ttu-id="c259e-156">Измените раздел `icons` манифеста, чтобы он ссылался на имена файлов значков, а не на их URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="c259e-156">Modify the `icons` portion of the manifest to refer to the file names of the icons instead of URLs.</span></span>

<span data-ttu-id="c259e-157">Приведенный ниже файл manifest.json содержит основные элементы, необходимые для тестирования и отправки приложения.</span><span class="sxs-lookup"><span data-stu-id="c259e-157">The following manifest.json file contains the basic elements needed to test and submit your app.</span></span>

> [!NOTE]
> <span data-ttu-id="c259e-158">Замените `id` и `connectorId` в приведенном ниже примере на GUID соединителя.</span><span class="sxs-lookup"><span data-stu-id="c259e-158">Replace `id` and `connectorId` in the following example with the GUID of your Connector.</span></span>

#### <a name="example-manifestjson-with-connector"></a><span data-ttu-id="c259e-159">Пример файла manifest.json с соединителем</span><span class="sxs-lookup"><span data-stu-id="c259e-159">Example manifest.json with Connector</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",
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

## <a name="testing-your-connector"></a><span data-ttu-id="c259e-160">Тестирование соединителя</span><span class="sxs-lookup"><span data-stu-id="c259e-160">Testing your Connector</span></span>

<span data-ttu-id="c259e-161">Чтобы тестировать соединитель, отправьте его команде, как в любом другом приложении.</span><span class="sxs-lookup"><span data-stu-id="c259e-161">To test your Connector, upload it to a team as you would with any other app.</span></span> <span data-ttu-id="c259e-162">Вы можете создать ZIP-пакет, используя файл манифеста с панели администрирования для разработчиков соединителей (измененный согласно инструкциям из предыдущего раздела) и два файла значков.</span><span class="sxs-lookup"><span data-stu-id="c259e-162">You can create a .zip package using the manifest file from the Connectors Developer Dashboard (modified as directed in the preceding section) and the two icon files.</span></span>

<span data-ttu-id="c259e-163">После отправки приложения откройте список соединителей с любого канала.</span><span class="sxs-lookup"><span data-stu-id="c259e-163">After you upload the app, open the Connectors list from any channel.</span></span> <span data-ttu-id="c259e-164">Прокрутите вниз, чтобы найти свое приложение в разделе **Отправленные**.</span><span class="sxs-lookup"><span data-stu-id="c259e-164">Scroll to the bottom to see your app in the **Uploaded** section.</span></span>

![Снимок экрана раздела отправленных приложений в диалоговом окне соединителя](~/assets/images/connectors/connector_dialog_uploaded.png)

<span data-ttu-id="c259e-166">Теперь можно запустить среду настройки.</span><span class="sxs-lookup"><span data-stu-id="c259e-166">You can now launch the configuration experience.</span></span> <span data-ttu-id="c259e-167">Обратите внимание, что этот процесс полностью выполняется в Microsoft Teams во всплывающем окне.</span><span class="sxs-lookup"><span data-stu-id="c259e-167">Be aware that this flow occurs entirely within Microsoft Teams through a pop-up window.</span></span> <span data-ttu-id="c259e-168">В настоящее время он отличается от процесса настройки в созданных нами соединителях. Мы работаем над согласованием этих процессов.</span><span class="sxs-lookup"><span data-stu-id="c259e-168">Currently, this behavior differs from the configuration experience in Connectors that we created; we are working on unifying the experiences.</span></span>

<span data-ttu-id="c259e-169">Чтобы убедиться в правильной работе действия `HttpPOST`, используйте [пользовательский входящий веб-перехватчик](#setting-up-a-custom-incoming-webhook).</span><span class="sxs-lookup"><span data-stu-id="c259e-169">To verify that an `HttpPOST` action is working correctly, use your [custom incoming webhook](#setting-up-a-custom-incoming-webhook).</span></span>


## <a name="rate-limiting-for-connectors"></a><span data-ttu-id="c259e-170">Ограничение скорости для соединителей</span><span class="sxs-lookup"><span data-stu-id="c259e-170">Rate limiting for Connectors</span></span>

<span data-ttu-id="c259e-171">Это ограничение распространяется на трафик, который соединителю или входящий веб-перехватчику разрешено создавать на канале.</span><span class="sxs-lookup"><span data-stu-id="c259e-171">This limit controls the traffic that a connector or an incoming webhook is allowed to generate on a channel.</span></span> <span data-ttu-id="c259e-172">Количество запросов веб-перехватчиков или соединителей будет ограничено при превышении ограничения скорости.</span><span class="sxs-lookup"><span data-stu-id="c259e-172">Requests made by your webhook or connector will be throttled when the rate limit threshhold is exceeded.</span></span> <span data-ttu-id="c259e-173">Время, в течение которого применяется регулирование, напрямую связано с параметрами превышения частоты запросов.</span><span class="sxs-lookup"><span data-stu-id="c259e-173">The length of time for the throttling behavior is directly correlated to the exceeded request rate parameters.</span></span> <span data-ttu-id="c259e-174">Например, если соединитель или веб-перехватчик направляет более 100 запросов сообщений за 3600 секунд, в течение следующих 3600 секунд он будет регулироваться следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c259e-174">For example, if a connector or webhook exceeds 100 message requests in 3600 seconds, the connector will be throttled for the next 3600 seconds:</span></span>

| <span data-ttu-id="c259e-175">Период времени (с)</span><span class="sxs-lookup"><span data-stu-id="c259e-175">Time-period (sec)</span></span>  | <span data-ttu-id="c259e-176">Максимально допустимое число запросов сообщений</span><span class="sxs-lookup"><span data-stu-id="c259e-176">Max allowed message requests</span></span>  |
|---|---|
| <span data-ttu-id="c259e-177">1</span><span class="sxs-lookup"><span data-stu-id="c259e-177">1</span></span>   | <span data-ttu-id="c259e-178">4</span><span class="sxs-lookup"><span data-stu-id="c259e-178">4</span></span>  |  
| <span data-ttu-id="c259e-179">30</span><span class="sxs-lookup"><span data-stu-id="c259e-179">30</span></span>   | <span data-ttu-id="c259e-180">60</span><span class="sxs-lookup"><span data-stu-id="c259e-180">60</span></span>  |  
| <span data-ttu-id="c259e-181">3600 (1 час)</span><span class="sxs-lookup"><span data-stu-id="c259e-181">3600 (1 hour)</span></span>  | <span data-ttu-id="c259e-182">100</span><span class="sxs-lookup"><span data-stu-id="c259e-182">100</span></span>  | 
| <span data-ttu-id="c259e-183">7200</span><span class="sxs-lookup"><span data-stu-id="c259e-183">7200</span></span> | <span data-ttu-id="c259e-184">150</span><span class="sxs-lookup"><span data-stu-id="c259e-184">150</span></span>  | 
| <span data-ttu-id="c259e-185">86400 (1 день)</span><span class="sxs-lookup"><span data-stu-id="c259e-185">86400 (1 day)</span></span> | <span data-ttu-id="c259e-186">1800</span><span class="sxs-lookup"><span data-stu-id="c259e-186">1800</span></span>  | 

<span data-ttu-id="c259e-187">[Логика повторных попыток с экспоненциальной задержкой](/azure/architecture/patterns/retry), подобная приведенной ниже, поможет избежать ограничения скорости в тех случаях, когда число запросов за секунду превышает пределы.</span><span class="sxs-lookup"><span data-stu-id="c259e-187">A [retry logic with exponential back-off](/azure/architecture/patterns/retry) like below would mitigate rate limiting for cases where requests are exceeding the limits within a second.</span></span> <span data-ttu-id="c259e-188">Следуйте [рекомендациям](../../bots/how-to/rate-limit.md#best-practices), чтобы предотвратить достижение пределов скорости.</span><span class="sxs-lookup"><span data-stu-id="c259e-188">Please follow [best practices](../../bots/how-to/rate-limit.md#best-practices) to avoid hitting the rate limits.</span></span>

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
 
<span data-ttu-id="c259e-189">Эти ограничения установлены с целью предотвратить перегрузку канала запросами от соединителя и обеспечивают удобство работы пользователей.</span><span class="sxs-lookup"><span data-stu-id="c259e-189">These limits are in place to reduce spamming a channel by a connector and ensures an optimal experience to your end users.</span></span>
